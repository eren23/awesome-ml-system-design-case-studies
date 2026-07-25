---
id: cs2368
title: Automated Incident Response Infrastructure in GCP
company: Spotify
primary_category: anomaly
sub_category: outlier-detection
year: 2019
source_url: https://engineering.atspotify.com/2019/04/whacking-a-million-moles-automated-incident-response-infrastructure-in-gcp/
tags: [incident-response, anomaly-detection, baseline-monitoring, GCP, automation, alerting]
---

# Automated Incident Response Infrastructure in GCP
**Spotify** · 2019 · [source](https://engineering.atspotify.com/2019/04/whacking-a-million-moles-automated-incident-response-infrastructure-in-gcp/)

## Problem
Spotify's security team needed to run forensic investigations across tens of thousands of hosts. When investigating potential malware compromises they had to rapidly identify anomalies, retrieve process memory, and collect disk artifacts — but manual, host-by-host investigation at that fleet size was slow, inefficient, and error-prone.

## Approach / System design
Spotify deployed Google's GRR Rapid Response forensics framework on GCP via a custom Terraform module they open-sourced. The architecture has three core components: the GRR Frontend (relays messages between agents and backend), GRR Workers (execute investigation flows), and the Admin UI (interface for incident responders). All components run on GCE instance groups using Container-Optimized OS behind load balancers with automated health checks; a single Cloud SQL instance handles cross-component state. Agents provisioned across the fleet enable automated scans (e.g., Yara signature searches) and remote memory forensics.

## Key decisions
- Infrastructure as code: Terraform for reproducible, standardized deployments instead of manual setup.
- Security hardening: HTTPS load balancer in front of Admin UI/Frontend, client verification via CA key pairs, encrypted agent communication.
- Contributed an authentication hook using Google Identity-Aware Proxy upstream, eliminating a separately maintained user database.
- Centralized state in one Google Cloud SQL instance for component communication.

## Stack
Google GRR Rapid Response, Terraform, Google Compute Engine (Container-Optimized OS), Google Cloud Load Balancer, Google Cloud SQL, Google Identity-Aware Proxy, Yara.

## Results
No specific metrics in the source. The post emphasizes that fleet-wide agent provisioning, automated scanning, and remote memory forensics became easy and systematic rather than manual drudgery.

## Takeaways
Automating incident response at fleet scale turns forensics from reactive whack-a-mole into systematic detection and remediation. Building on a managed cloud (load balancers, IAP, managed SQL) plus IaC keeps a security-critical system reproducible and hardened, and open-sourcing the deployment module and auth contributions benefits the wider security community.
