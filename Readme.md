# Installation Guide

## 1. Setting Up the Target Machine for Monitoring

1. Navigate to the `ec2-node-exporter` folder on your target machine.
2. Copy the `docker-compose.yml` file to the target machine.
3. Run the following command to start the container:
   ```bash
   docker-compose up -d
   ```

## 2. Setting Up the Monitoring Machine

1. Navigate to the `ec2-monitoring-tool` folder on your monitoring machine.
2. Copy the `docker-compose.yml` and `prometheus.yml` files to the monitoring machine.
3. Open the `prometheus.yml` file and update the target IP to the IP address of the target machine (from the previous step).
4. Run the following command to start the monitoring tools:
   ```bash
   docker-compose up -d
   ```

## 3. Accessing Prometheus and Grafana

1. Access Prometheus by navigating to `http://<monitoring_machine_ip>:9090`.
2. Access Grafana by navigating to `http://<monitoring_machine_ip>:3000` (default login: `admin/admin`).
3. In Grafana:
   - Add Prometheus as a data source with the URL `http://localhost:9090`.
   - Create a new dashboard by either importing it from Grafana Dashboards or by using the dashboard ID: `1860`.
  

## 4. Run a stress test

```
# Aktualisiere die Paketlisten
sudo apt-get update

# Installiere stress-ng (empfohlen für vielseitigere Tests)
sudo apt-get install stress-ng

# Stress mit nur 1 CPU für 60 Sekunden (bei Free Tier Instanzen)
nohup stress-ng --cpu 1 --timeout 1m --verbose > /dev/null 2>&1 &


# Teste den Arbeitsspeicher mit einer kleinen Menge (z. B. 256 MB)
nohup stress-ng --vm 1 --vm-bytes 256M --timeout 60s > /dev/null 2>&1 &

``` 

