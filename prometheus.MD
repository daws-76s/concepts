### Prometheus

Download prometheus

https://github.com/prometheus/prometheus/releases/download/v2.51.0-rc.0/prometheus-2.51.0-rc.0.linux-amd64.tar.gz

```
[Unit]
Description=prometheus service.

[Service]
ExecStart=/opt/prometheus/prometheus --config.file=/opt/prometheus/prometheus.yml

[Install]
WantedBy=multi-user.target
```

```
[Unit]
Description=node exporter service.

[Service]
ExecStart=/opt/node_exporter/node_exporter

[Install]
WantedBy=multi-user.target
```

#### ec2_sd_config

```
- job_name: ec2_scrapping
    ec2_sd_configs:
    - region: us-east-1
      port: 9100
      filters:
      - name: tag:Monitoring
        values:
        - true
  relabel_configs:
  - source_labels: [__meta_ec2_private_ip]
    target_label: private_ip
  - source_labels: [__meta_ec2_instance_id]
    target_label: instance_id
```

```
[Unit]
Description=Alert Manager service.

[Service]
WorkingDirectory=/opt/alertmanager
ExecStart=/opt/alertmanager/alertmanager

[Install]
WantedBy=multi-user.target
```

Up/Down
CPU
free memory