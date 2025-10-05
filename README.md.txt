# AT&T Website Clone with Prometheus & Grafana Monitoring

A complete monitoring solution for a cloned AT&T website using modern DevOps tools and practices.

## 🎯 Project Overview

This project demonstrates full-stack monitoring capabilities by combining:
- A responsive AT&T website clone
- Real-time monitoring with Prometheus
- Beautiful dashboards with Grafana
- Containerized deployment using Docker

## 🛠️ Technologies Used

- **Docker & Docker Compose** - Container orchestration
- **Prometheus** - Metrics collection and monitoring
- **Grafana** - Data visualization and dashboarding
- **Blackbox Exporter** - Website health checks and uptime monitoring
- **Nginx** - Web server
- **HTML/CSS/JavaScript** - Frontend development

## 📊 What This Project Monitors

- ✅ Website uptime and availability (99.9% SLA tracking)
- ✅ Response time and latency metrics
- ✅ HTTP status codes and error tracking
- ✅ DNS lookup performance
- ✅ Connection time analysis
- ✅ TLS/SSL handshake monitoring
- ✅ Real-time alerting capabilities

## 🚀 Quick Start

### Prerequisites

- Docker Desktop installed
- Docker Compose installed
- 8GB RAM minimum
- Ports available: 8080, 9090, 9115, 3000

### Installation

1. **Clone the repository**
```bash
   git clone https://github.com/YOUR-USERNAME/att-monitoring.git
   cd att-monitoring


Start the monitoring stack

bash   docker-compose up -d

Verify all services are running

bash   docker-compose ps
Access the Services
ServiceURLCredentialsAT&T Websitehttp://localhost:8080-Prometheushttp://localhost:9090-Grafanahttp://localhost:3000admin / admin
📈 Configure Grafana Dashboard

Open Grafana at http://localhost:3000
Login with admin / admin
Add Prometheus data source:

Go to Configuration → Data Sources
Add Prometheus
URL: http://prometheus:9090
Save & Test


Import pre-built dashboard:

Go to Dashboards → Import
Enter dashboard ID: 7587
Select Prometheus data source
Click Import



Or Create Custom Dashboard
Use these PromQL queries:
Website Status:
promqlprobe_success{job="att-website-health"}
Response Time:
promqlprobe_http_duration_seconds{job="att-website-health"}
HTTP Status Code:
promqlprobe_http_status_code{job="att-website-health"}
Uptime Percentage (24h):
promqlavg_over_time(probe_success{job="att-website-health"}[24h]) * 100

🏗️ Architecture
┌─────────────────┐
│  AT&T Website   │ ← User Access (Port 8080)
│    (Nginx)      │
└────────┬────────┘
         │
         │ Health Checks
         ↓
┌─────────────────┐
│    Blackbox     │ ← Probes website every 15s
│    Exporter     │
└────────┬────────┘
         │
         │ Metrics
         ↓
┌─────────────────┐
│   Prometheus    │ ← Stores time-series data
│                 │
└────────┬────────┘
         │
         │ Queries
         ↓
┌─────────────────┐
│    Grafana      │ ← Visualizes data
│                 │
└─────────────────┘
📁 Project Structure
att-monitoring/
├── att-website.html       # AT&T website clone
├── docker-compose.yml     # Container orchestration
├── prometheus.yml         # Prometheus configuration
├── blackbox.yml          # Blackbox exporter config
├── README.md             # This file
├── .gitignore           # Git ignore rules
└── screenshots/         # Dashboard screenshots
    ├── dashboard.png
    ├── website.png
    └── prometheus.png
🧪 Testing
Test website monitoring:

Stop the website

bash   docker-compose stop att-website

Grafana should show website as DOWN
Alerts trigger (if configured)


Restart the website

bash   docker-compose start att-website

Website status returns to UP
Metrics resume collection

View logs:
bash# All services
docker-compose logs -f

# Specific service
docker-compose logs -f prometheus
🔧 Configuration
Change Monitoring Interval
Edit prometheus.yml:
yamlglobal:
  scrape_interval: 15s  # Change this value
Add More Targets
Edit prometheus.yml under scrape_configs:
yaml- targets:
    - http://att-website:80
    - http://another-site.com  # Add more sites
Change Ports
Edit docker-compose.yml:
yamlports:
  - "8081:80"  # Change external port
📊 Key Metrics Tracked

Uptime SLA: 99.9% availability target
Response Time: < 200ms target
Error Rate: < 0.1% target
DNS Resolution: < 50ms target
Connection Time: < 100ms target

🎓 Skills Demonstrated

DevOps: Docker containerization, Infrastructure as Code
Monitoring: Prometheus metrics collection, PromQL queries
Observability: Grafana dashboards, real-time visualization
SRE Practices: SLA tracking, uptime monitoring, incident detection
Networking: HTTP protocol, DNS, TLS/SSL
Web Development: Responsive design, modern CSS/JS

🚀 Future Enhancements

 Add AlertManager for notifications (email, Slack, PagerDuty)
 Implement custom recording rules
 Add more complex SLI/SLO tracking
 Integrate with CI/CD pipeline
 Add performance testing with K6
 Implement distributed tracing with Jaeger
 Add log aggregation with Loki
 Deploy to Kubernetes cluster

🐛 Troubleshooting
Issue: Services won't start
bashdocker-compose down
docker-compose up -d
Issue: Port conflicts

Check if ports are in use: netstat -ano | findstr :3000
Change ports in docker-compose.yml

Issue: Grafana can't connect to Prometheus

Use http://prometheus:9090 (not localhost)
Verify with: docker-compose logs prometheus
📄 License
This project is open source and available under the MIT License.
🙏 Acknowledgments

Prometheus documentation
Grafana community dashboards
Docker best practices
Original AT&T website design inspiration


⭐ If you find this project useful, please consider giving it a star!
Made with ❤️ for learning and demonstrating SRE/DevOps skills.