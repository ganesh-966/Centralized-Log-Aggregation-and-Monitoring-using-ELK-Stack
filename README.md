# Centralized-Log-Aggregation-and-Monitoring-using-ELK-Stack

🚀 Project Overview

As part of improving production reliability, this project implements a centralized logging system using the ELK Stack (Elasticsearch, Logstash, Kibana).

The goal is to collect logs from multiple application servers, process them centrally, and visualize them in a single dashboard for faster troubleshooting and proactive monitoring.


🧱 Step 1: Launch EC2 Instances

Create 3 EC2 instances in AWS:

Server Type	Count	Purpose
Log Server	1	ELK Stack
App Server	2	Nginx + Logs

![](./images/Screenshot%202026-03-11%20162817.png)

✅ Configuration

OS: Ubuntu 22.04

Instance Type: t2.midium (for log server)
Instance Type: t2.micro (for app server)

Security Groups:

22 → SSH

80 → HTTP

5601 → Kibana

9200 → Elasticsearch

5044 → Logstash

 Install Java on log server -
sudo apt update
sudo apt install openjdk-11-jdk -y

![](./images/Screenshot%202026-03-11%20153657.png)

##  Install Elasticsearch

![](./images/Screenshot%202026-03-11%20153745.png)

### Install Logstash

![](./images/Screenshot%202026-03-11%20160432.png)

### Install Kibana

![](./images/Screenshot%202026-03-11%20160934.png)

Edit config:

sudo nano /etc/kibana/kibana.yml

![](./images/Screenshot%202026-03-18%20122557.png)


## SSH into App Server 1 & 2

## Install Nginx

## Install Filebeat in app server

![](./images/Screenshot%202026-03-11%20163317.png)

### Configure Filebeat
sudo nano /etc/filebeat/filebeat.yml

![](./images/Screenshot%202026-03-18%20122125.png)

![](./images/Screenshot%202026-03-18%20122142.png)


Enable Nginx Module

sudo filebeat modules enable nginx

 Start Filebeat

sudo systemctl enable filebeat

sudo systemctl start filebeat

## Setup Kibana Dashboard

## http://<PUBLIC_IP>:5601

Open Kibana

Go to Stack Management → Index Patterns

Create index pattern:

nginx-logs-*

Select @timestamp

🔍 View Logs

Go to:

👉 Discover → Select nginx-logs-*

![](./images/Screenshot%202026-03-18%20120224.png)

![](./images/Screenshot%202026-03-18%20121717.png)


✅ Project Conclusion

The Centralized Log Aggregation and Monitoring using ELK Stack project successfully addresses the challenge of scattered logs across multiple servers by implementing a unified, scalable logging solution.

By deploying Elasticsearch, Logstash, and Kibana along with Filebeat on application servers, all logs are now collected, processed, and visualized in a single platform. This transformation significantly improves the efficiency of troubleshooting and system monitoring.

The system enables real-time visibility into application behavior, allowing teams to quickly identify errors, monitor traffic patterns, and analyze system performance. Instead of manually checking individual servers, developers and SREs can now rely on a centralized dashboard to gain actionable insights.

Additionally, the solution is highly scalable and can be extended to support more servers, applications, and advanced monitoring features such as alerting and security.

