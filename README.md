# Database Monitoring with Prometheus + Grafana

This doc sets up a comprehensive monitoring solution for database performance and system metrics using Prometheus for metrics collection and Grafana for visualization. The setup monitors PostgreSQL, MySQL databases, and system resources (CPU, RAM, disk) with real-time dashboards.

## Prerequisites

- A VM running Linux (Ubuntu/Debian recommended)
- Sudo privileges
- PostgreSQL and MySQL installed and running
- Internet access to download exporters, Prometheus, and Grafana

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

2. Install Exporters

```
wget https://github.com/prometheus/node_exporter/releases/download/v1.7.0/node_exporter-1.7.0.linux-amd64.tar.gz
tar xvf node_exporter-1.7.0.linux-amd64.tar.gz
cd node_exporter-1.7.0.linux-amd64
./node_exporter
```
