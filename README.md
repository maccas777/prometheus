#docker-monitoring
monitoring docker containers using cadvisor, prometheus,redis and grafana
# run - docker-compose up
if everything is working good, you should see this message <br>
msg="Server is ready to receive web requests." <br>
check three containers are running using docker-compose ps
# accessing cadvisor
http://localhost:8080
# accessing prometheus
http://localhost:9090
# accessing SNMP
http://localhost:9116
# running grafana on docker host
docker run -d --name grafana -p 3000:3000 grafana/grafana <br> <br>
Access grafana using
http://localhost:3000

# Windows Machine Monitoring - Exchange, AD, DNS
Install Windows ExporterPermalink
Download Windows Exporter MSI file.
https://github.com/prometheus-community/windows_exporter

Make sure this service is running. It will also automatically add firewall rule by opening TCP Port 9182. Allow only your Prometheus server IP in that rule.
Now your exporter is running, it will start exposing windows metrics on http://localhost:9182/metrics.

By default only few collectors “cpu, cs, logical_disk, net, os, service, system, textfile” are enabled. If you want to monitor like “exchange, ad, dns” then you should manually enable that collectors.

# Change through regedit directly
Enable Collectors AD,DNSPermalink
1. Enable through regedit

Win + R > regedit > HKEY_LOCAL_MACHINE > SYSTEM > CurrentControlSet > Services > Windows_exporter

# AD and DNS
C:\Program files\windows_exporter\windows_exporter.exe --log.format logger:eventlog?name=windows_exporter --collectors.enabled ad,dns,cs,cpu,logical_disk,memory,service,system,tcp --telemetry.addr :9182

# Exchange
C:\Program files\windows_exporter\windows_exporter.exe  --log.format logger:eventlog?name=windows_exporter --collectors.enabled "exchange,cpu,cs,logical_disk,logon,memory,net,os,system,tcp" --collectors.exchange.enabled=TransportQueues,HttpProxy,ActiveSync,AvailabilityService,OutlookWebAccess,Autodiscover

