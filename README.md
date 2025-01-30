# monitoring_tool
A log monitoring tool using Grafana, Loki, and Promtail for collecting, aggregating, and visualizing logs in real-time for efficient system and application monitoring.

- **Grafana**
    
    - Grafana is an open-source visualization and monitoring tool.
    - It supports multiple data sources like Prometheus, InfluxDB, and Loki.
    - Used to create dashboards, alerts, and reports for logs and metrics.

- **Loki**
    
    - Loki is a log aggregation system developed by Grafana Labs.
    - Unlike traditional log management tools, Loki does not index log contents but instead indexes metadata (labels).
    - It is designed to work efficiently with Prometheus and store logs in a cost-effective way.
- **Promtail**
    
    - Promtail is a lightweight log collector that ships logs to Loki.
    - It is similar to Fluentd or Logstash but optimized for Loki.
    - It collects logs from files and systemd journal and sends them to Loki for indexing.

### **How They Work Together**

- **Promtail** collects logs from applications and forwards them to **Loki**.
- **Loki** stores and indexes the logs efficiently.
- **Grafana** queries **Loki** to visualize logs in dashboards


### **Centralized Log Collection Setup Using Syslog**

#### **1. Introduction**

In this setup, we use a **centralized log collection server** to receive syslog messages from multiple remote servers. These logs are stored on the central server in `/var/log/`, organized by the hostname of the remote server and the program generating the log. This approach simplifies log management, monitoring, and troubleshooting by consolidating logs from various sources into a single location.

---

#### **2. Components of the Log Collection Setup**

1. **Central Log Collector**:  
    This server collects syslog messages from remote servers and stores them in log files. It is responsible for receiving and organizing logs in the `/var/log/` directory based on the hostname and program name.
    
2. **Remote Syslog Clients**:  
    These are the servers whose logs will be sent to the central log collector. They forward their log messages via **UDP** or **TCP** to the central server.
    
3. **Log Storage Structure**:  
    Logs are stored in `/var/log/<hostname>/<program>.log`, where `<hostname>` is the name of the remote server sending the logs, and `<program>` is the application or service that generated the log.


### Regular Expressions

**Regular Expressions (Regex)** are powerful tools for pattern matching and manipulating strings. They provide a concise and flexible means to search, match, or replace strings based on specific patterns. Regex is commonly used in text processing tasks, such as form validation, search functions, and log parsing.


some of the regex that I have written 

for sender to receiver pattern match 
```
from=<(?P<sender>[^>]+)> to=<(?P<receiver>[^>]+)>
```

LogQL

```
{job="abc"} |= `Sender address` | regexp `from=<(?P<sender>[^>]+)> to=<(?P<receiver>[^>]+)>`
```
