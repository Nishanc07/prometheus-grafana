# Database Monitoring with Prometheus + Grafana

This doc sets up a comprehensive monitoring solution for database performance and system metrics using Prometheus for metrics collection and Grafana for visualization. The setup monitors PostgreSQL, MySQL databases, and system resources (CPU, RAM, disk) with real-time dashboards.

## Prerequisites

- A VM running Linux (Ubuntu/Debian recommended)
- Sudo privileges
- PostgreSQL and MySQL installed and running
- Internet access to download exporters, Prometheus, and Grafana
- Make sure all the necessary ports are open (9090, 3000, 9100, 9187, 9104, 1860, 9628, 7362)

Architecture:

```
Linux VM
├── Prometheus (Port 9090) - Metrics Collection & Storage
├── Grafana (Port 3000) - Dashboard & Visualization
├── Node Exporter (Port 9100) - System Metrics
├── PostgreSQL Exporter (Port 9187) - PostgreSQL Metrics
├── MySQL Exporter (Port 9104) - MySQL Metrics
├── PostgreSQL Database - Target Database
└── MySQL Database - Target Database

```

1. Download Prometheus:

```
wget https://github.com/prometheus/prometheus/releases/download/v2.49.0/prometheus-2.49.0.linux-amd64.tar.gz
tar xvf prometheus-2.49.0.linux-amd64.tar.gz
cd prometheus-2.49.0.linux-amd64
```

and so on from the offcial documentation for all

2. Create Prometheus Service and run the service.. Access prometheus on public_ip:9090

3. Install PostgreSQL Exporter

4. Install Exporters

5. Install MySQL Exporter

6. Database Setup
   PostgreSQL Database and User Creation
   Mysql Database and User creation
   give necessary permissions for these users and database

7. Manual PostgreSQL Exporter Run

```
export DATA_SOURCE_NAME="postgresql://postgres_exporter:root123@localhost:5432/mydb?sslmode=disable"
./postgres_exporter
```

8. Mysql manual exporter run

```
export DATA_SOURCE_NAME="mysql_exporter:root123@tcp(localhost:3306)/"
./mysqld_exporter
```

- Test Prometheus: curl http://<public_ip>:9090/metrics
- Test Node Exporter: curl http://<public_ip>:9100/metrics
- Test PostgreSQL Exporter: curl http://<public_ip>:9187/metrics
- Test MySQL Exporter: curl http://<public_ip>:9104/metrics

## Grafana Setup

1. Access Grafana

- Open browser and navigate to http://public_ip:3000
- Login with default credentials: admin/admin
- Change password when prompted

2. Add Prometheus Datasource

- Go to Configuration → Data Sources
- Click "Add data source"
- Select "Prometheus"
- Set URL to: http://<public_ip>t:9090
- Click "Save & Test"

3. To create dashboards...

- import and give ID of 1860 for Nodeport, 7362 for MySql and 9528 for postgres
- Select Prometheus and load

Node Exporter: https://nishanc604.grafana.net/dashboard/snapshot/lGXHIZXnMRuGMwAIQjLsqKAKjU77ZJqI?orgId=1&from=now-6h&to=now&timezone=browser&var-DS_PROMETHEUS=grafanacloud-prom&var-job=node&var-nodename=prgr&var-node=localhost:9100&var-diskdevices=%5Ba-z%5D%2B%7Cnvme%5B0-9%5D%2Bn%5B0-9%5D%2B%7Cmmcblk%5B0-9%5D%2B&refresh=1m

Postres: https://nishanc604.grafana.net/dashboard/snapshot/43gaFKUvBvMtSnEym9D3Ph8NZtbJ75Oq?orgId=1&from=now-3h&to=now&timezone=browser&var-DS_PROMETHEUS=grafanacloud-prom&var-interval=$__auto&var-namespace=&var-release=&var-instance=localhost:9187&var-datname=$__all&var-mode=$__all&refresh=10s

![alt text](https://github.com/Nishanc07/prometheus-grafana/blob/main/public/Screenshot%202025-08-20%20at%2016.06.40.png)

![alt text](https://github.com/Nishanc07/prometheus-grafana/blob/main/public/Screenshot%202025-08-20%20at%2017.02.46.png)

![alt text](https://github.com/Nishanc07/prometheus-grafana/blob/main/public/Screenshot%202025-08-20%20at%2016.41.57.png)

![alt text](https://github.com/Nishanc07/prometheus-grafana/blob/main/public/Screenshot%202025-08-20%20at%2017.02.59.png)

![alt text](https://github.com/Nishanc07/prometheus-grafana/blob/main/public/Screenshot%202025-08-20%20at%2014.35.20.png)
