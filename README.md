# AlertmanagerWrapper
Prometheus Alertmanager Wrapper

translate alerts from prometheus alertmanager to any language
and send to recivers phone number

## Installation

First: 
Install Golang
- $ sudo apt update
- $ sudo apt install golang
- $ go version
- $ go build  #Binary file created.
 seconds:
- $ mv paw.service /lib/systemd/system/
- $ nano paw.service # add location binery file createded

//////// alertmanager config to send alerts to /SendAlert of wrapper

```bash
route:
  group_by: ['alertname']
  group_wait: 30s
  group_interval: 5m
  repeat_interval: 1h
  receiver: 'web.hook'
receivers:
  - name: 'web.hook'
    webhook_configs:
      - url: 'http://hostIp:12001/SendAlert'
inhibit_rules:
  - source_match:
      severity: 'critical'
    target_match:
      severity: 'warning'
    equal: ['alertname', 'dev', 'instance']
```
    
