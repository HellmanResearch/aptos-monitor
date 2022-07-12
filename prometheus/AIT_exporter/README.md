# Prometheus exporter for Aptos Incentivized Testnet

### public exporter
ait2-exporter.aptos.hellman.team:9116/metrics

### metrics
* aptos_validator_liveness
* aptos_validator_participation
* aptos_validator_votes

### requires
Python3 (Python3.8 is recommended)

### Install
```bash
git clone https://github.com/HellmanResearch/aptos-monitor.git
cd aptos-monitor/prometheus/AIT_exporter
pip3 install -r requirements.txt
```

### Start
```bash
./start.sh
```

### Stop
```bash
./stop.sh
```

### Add job to prometheus.yml
```yaml
  - job_name: "ait_exporter"
    static_configs:
      - targets:
        - 'localhost:9116'
```

### Add alert rules (replace peer_id)
```yaml
groups:
  - name: 'Aptos'
    rules:
      - alert: 'Liveness is low'
        expr: 'aptos_validator_liveness{peer_id="<peer_id>"}<99'
        for: 2m

      - alert: 'Participation is low'
        expr: 'aptos_validator_participation{peer_id="<peer_id>"}<94'
        for: 2m
```
