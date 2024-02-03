# Recogizer DevOps/Cloud Engineer Technical Challenge - Monitoring Solution

## Introduction:

This documentation guides you in establishing a centralized monitoring solution for dockerized applications using Prometheus, Grafana, and Alertmanager. Learn to collect metrics efficiently, create dynamic dashboards, and manage alerts effectively, providing a comprehensive monitoring stack for enhanced observability in cloud-native environments.

## Components
- [Prometheus](#prometheus)
- [Alert Manager](#alert-manager)
- [Grafana](#grafana)


I am employing a consolidated Docker Compose file to orchestrate the deployment of various components, all within a dedicated Docker network. This strategic setup enables us to independently manage our monitoring solution, ensuring seamless onboarding of new application logs in the future.

## Prometheus

Prometheus is an open-source monitoring tool for tracking and alerting system metrics. It excels in handling time-series data, offering flexibility in querying, visualization, and alerting for efficient system monitoring.

I am deploying Prometheus to monitor Caddy. Prometheus will scrape metrics from the Caddy scrap target, accessible at the /metrics endpoint (http://caddy:2019/metrics) of the Caddy server.

To streamline monitoring configuration, I made a slight adjustment to the Caddy Docker Compose file. Hostnames for services have been introduced, and a static name for the Docker network has been assigned. This specific network name will be referenced as an external network in the Prometheus deployment Docker Compose.

This approach ensures consistency, preventing potential issues when executing the Caddy Docker Compose from different directories. Without specifying a static network name, Docker appends the directory name to the network name, necessitating manual updates in the Prometheus Docker Compose each time Caddy is run from a new directory.

```yaml
# Caddy docker-compose.yaml
version: '3'

services:
  http-dummy-service:
    ....
    ....
    hostname: http-dummy

  caddy:
    ....
    ....
    hostname: caddy
    ....
    ....
networks:
  backend:
    name: backend
    driver: bridge
```
I included **"backend"** as the network name to serve as a reference in our future Docker Compose files. This ensures consistency in network naming conventions.

If this step is overlooked during the Docker Compose execution, the network name would default to something like **"directory-name_backend."** In our specific setup, we want the network name to be simply **"backend."**

```bash
# Example Output for docker network
SahirAbbas@sahir-pc:~/workshop/rg-devops-challenge$ docker network ls
NETWORK ID     NAME                       DRIVER    SCOPE
c4391b50d970   backend                    bridge    local
874c2aafe5b4   directory-name_backend     bridge    local
```

## Alert Manager

Contents here

## Grafana

Contents here