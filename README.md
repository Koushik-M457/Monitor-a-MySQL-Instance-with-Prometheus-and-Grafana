# Monitor-a-MySQL-Instance-with-Prometheus-and-Grafana

This setup uses Docker Compose to monitor a MySQL/MariaDB instance with:
- Prometheus (metrics collection)
- mysqld_exporter (MySQL metrics exporter)
- Grafana (visualization)

## 🧱 Architecture

  [MySQL Server] <-- mysqld_exporter --> [Prometheus] --> [Grafana Dashboards]


## ⚙️ Requirements

- Docker
- Docker Compose
- MySQL or MariaDB running (can be host or container)
- Prometheus compatible MySQL user

---

## 🛠️ Setup

### 1. Create a Monitoring MySQL User

Run this in your MySQL/MariaDB:

```sql
CREATE USER 'exporter'@'%' IDENTIFIED BY 'password';
GRANT PROCESS, REPLICATION CLIENT, SELECT ON *.* TO 'exporter'@'%';
FLUSH PRIVILEGES;


docker compose up -d

Access the Tools
Prometheus: http://localhost:9090

Grafana: http://localhost:3000
Login with admin / admin (you'll be prompted to change it)


Import Grafana Dashboard
Login to Grafana

Go to "Dashboards" > "Import"

Use Dashboard ID: 7362
(Official Percona MySQL Dashboard)


Verify Metrics
Prometheus: Go to http://localhost:9090/targets

Ensure mysqld_exporter is UP

Grafana: Should show MySQL metrics



 Troubleshooting
Error: connection refused

Check if MySQL is running and reachable from Docker

Prometheus target DOWN

Verify mysqld_exporter logs with docker logs mysqld_exporter

mysqld_exporter: permission denied

Ensure MySQL user has correct permissions

 References
https://prometheus.io/docs/

https://grafana.com/

https://github.com/prometheus/mysqld_exporter
