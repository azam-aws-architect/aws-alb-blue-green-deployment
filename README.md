# 🚀 Project 37: Enterprise Zero-Downtime Blue-Green Deployment Architecture via AWS Application Load Balancer (ALB)

## 📌 Project Overview
This project demonstrates the architectural implementation of an production-grade, highly available, and risk-mitigated **Blue-Green Deployment Pipeline** on AWS. By utilizing an **Application Load Balancer (ALB)** and decoupled **Target Groups**, the setup achieves near-instant traffic shifting between two isolated infrastructure versions (**Blue V1.0** and **Green V2.0**) with **Zero Downtime**, ensuring continuous application availability during critical enterprise updates.

---

## 🏗️ Infrastructure Routing Design
[ Public Internet Traffic ]
                │
                ▼ (Port 80)
  ┌─────────────────────────────┐
  │  Application Load Balancer  │
  │ (healthvitals-traffic-dir)  │
  └──────────────┬──────────────┘
                 │
     ┌───────────┴───────────┐
     │ (Active Route Switch) │
     ▼                       ▼ 
┌──────────────────┐    ┌──────────────────┐
│ Target Group V1  │    │ Target Group V2  │
│   (tg-blue-v1)   │    │  (tg-green-v2)   │
└────────┬─────────┘    └────────┬─────────┘
│                       │
▼                       ▼
┌──────────────────┐    ┌──────────────────┐
│  EC2 Instance    │    │  EC2 Instance    │
│ (blue-v1: Blue)  │    │ (green-v2: Green)│
└──────────────────┘    └──────────────────┘
---

## 🌟 Core Engineering Features
* **Zero-Downtime Strategy:** Version migrations occur instantly at the routing plane without severing active server sockets or dropping external client requests.
* **Complete Environment Isolation:** Independent compute and logical routing segments isolate production states, enabling granular rollback configurations if anomaly thresholds are tripped.
* **Decoupled Security Context:** Implemented shared unified security boundaries (`default` group ingress models) allowing secure ingress matching exclusively over Port 80 (HTTP).

---

## 🛠️ Step-by-Step Deployment Logs

### Phase 1: Isolated Target Plane Configuration
1. Provisioned two independent logical target pools inside the VPC cluster node:
   * `tg-blue-v1` (Assigned for initial stable baseline builds)
   * `tg-green-v2` (Assigned for modern candidate feature iterations)
2. Maintained standard operational health routing checks over baseline HTTP settings.

### Phase 2: Server Provisioning & Application Ingestion
1. Deployed an Ubuntu Server 24.04 LTS instance named `healthvitals-blue-v1`, ingesting the core product HTML profile shell onto Apache web services.
2. Deployed a duplicate mirror node named `healthvitals-green-v2` embedded with localized update states to depict an enterprise codebase refresh.
3. Registered both application hosts securely into their respective target logical configurations.

### Phase 3: Traffic Director Integration & Live Switch Execution
1. Built an Internet-facing AWS Application Load Balancer named `healthvitals-traffic-director`.
2. Mapped the system rule behavior to process inbound requests down to `tg-blue-v1` endpoints by default.
3. *Execution:* Edited the listener forward conditions dynamically to drop traffic allocation from `tg-blue-v1` and attach it instantly to `tg-green-v2`.

---

## 📊 Live End-to-End Validation Proof
System metrics verified complete runtime execution profiles successfully across both deployments:

* **Active Load Balancer Endpoint:** `http://healthvitals-traffic-director-550412191.us-east-1.elb.amazonaws.com`
* **Route Phase A (Blue Active):** Content rendered accurately with zero transmission drops (Production Version 1.0 Live).
* **Route Phase B (Green Switch):** Instant global mutation to green baseline profiles upon saving modifications on the ALB listener configuration matrix.

---
### 👤 Engineered By:
**Cloud Infrastructure & Architecture Engineer (Project Milestone #37)**
