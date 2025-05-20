# DevOps Tools Collection

This repository contains Docker Compose configurations for several popular DevOps and monitoring tools including Grafana, Prometheus, Kafka, and n8n.

## Table of Contents
- [Overview](#overview)
- [Prerequisites](#prerequisites)
- [Components](#components)
  - [Grafana](#grafana)
  - [Prometheus](#prometheus)
  - [Kafka](#kafka)
  - [n8n](#n8n)
- [Getting Started](#getting-started)
- [Configuration](#configuration)
- [Port Reference](#port-reference)
- [Volume Information](#volume-information)
- [Troubleshooting](#troubleshooting)

## Overview

This collection provides ready-to-use Docker Compose configurations for setting up a comprehensive DevOps monitoring and automation environment. Each tool can be deployed independently or as part of a complete stack.

## Prerequisites

- Docker and Docker Compose installed
- At least 4GB of available RAM
- 10GB of free disk space
- For n8n: external volume `n8n_data` must be created

## Components

### Grafana

Grafana is an open-source platform for monitoring and observability that allows you to query, visualize, and alert on metrics.

**Features:**
- Enterprise edition included
- Custom configuration with 1s minimum refresh interval
- Persistent storage through Docker volumes

### Prometheus

Prometheus is an open-source systems monitoring and alerting toolkit with a dimensional data model and powerful query language.

**Features:**
- 1s scrape interval for real-time monitoring
- Node Exporter integration for host metrics
- cAdvisor integration for container metrics
- Windows Exporter support
- Custom application metrics endpoints configured

### Kafka

A distributed event streaming platform capable of handling trillions of events a day.

**Features:**
- Kafdrop UI for Kafka management
- Internal and external listeners configured
- ZooKeeper included

### n8n

n8n is a workflow automation tool with a visual interface that helps you connect different services and automate tasks.

**Features:**
- Latest version
- Host drive mounting for data persistence
- Production mode enabled

## Getting Started

1. Clone this repository:
```
git clone <repository-url>
cd <repository-directory>
```

2. Start the services individually or together:

For Grafana:
```
cd grafana
docker-compose up -d
```

For Prometheus:
```
cd prometheus
docker-compose up -d
```

For Kafka:
```
cd kafka
docker-compose up -d
```

For n8n:
```
# Create the external volume first
docker volume create n8n_data
cd n8n
docker-compose up -d
```

## Configuration

### Grafana
- Configuration file: `grafana/grafana.ini`
- Minimum refresh interval: 1s

### Prometheus
- Configuration file: `prometheus/prometheus.yml`
- Configured to scrape:
  - Prometheus itself
  - Node Exporter
  - Windows Exporter
  - Custom Go application metrics
  - Custom Node.js metrics
  - cAdvisor

### Kafka
- Configured with internal and external listeners
- Accessible through Kafdrop UI

### n8n
- Host directory mounted for data persistence
- Running in production mode

## Port Reference

| Service | Port | Description |
|---------|------|-------------|
| Grafana | 3001 | Grafana UI (mapped from 3000) |
| Prometheus | 9090 | Prometheus UI |
| Node Exporter | 9100 | Host metrics |
| cAdvisor | 8085 | Container metrics (mapped from 8080) |
| Kafka | 9092 | Kafka broker |
| Kafka | 2181 | ZooKeeper |
| Kafdrop | 9000 | Kafka UI |
| n8n | 5678 | n8n workflow automation |

## Volume Information

| Volume | Description |
|--------|-------------|
| grafana-data | Persistent Grafana data |
| prometheus_data | Prometheus time-series data |
| n8n_data | n8n workflow and credentials (external) |

## Troubleshooting

**Grafana Issues:**
- If experiencing permission issues, ensure the user ID is set correctly in the docker-compose.yml file

**Prometheus Issues:**
- If targets show as "down", check if the services are accessible from the Prometheus container
- For 'host.docker.internal' targets, ensure your Docker version supports this feature

**Kafka Issues:**
- If Kafdrop cannot connect to Kafka, ensure the broker is up and running
- Check the logs with `docker-compose logs kafka`

**n8n Issues:**
- Ensure the external volume is created before starting the container
- Check permissions on the mounted host directory
