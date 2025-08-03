# High-Level Design (HLD)

## Crowdsourced Local Issue Reporting Platform

---

### 1. Overview

A platform for citizens to report local civic issues (potholes, streetlights, garbage), upload photos, and track resolution status. Authorities can view/manage reports and access analytics. The system exposes open data APIs and analytics dashboards.

---

### 2. Architecture Diagram

```mermaid
Flowchart LR

A[Citizens (Web/Mobile)] -- REST API --> B[Spring Boot Backe

B--DB Access --> C[(PostgreSQL/MongoDB)]

B-File Upload --> D[File Storage]

B -- Analytics Data --> E[Analytics Dashboard]

B -- Open Data --> F[Open Data API]

G[Authorities (Web)] -- REST API --> B
```
