# High-Level Design (HLD)

## Crowdsourced Local Issue Reporting Platform
---
### 1. Overview

A platform for citizens to report local civic issues (potholes, streetlights, garbage), upload photos, and track resolution status. Authorities can view/manage reports and access analytics. The system exposes open data APIs and analytics dashboards.

---
### 2. Architecture Diagram

```mermaid
flowchart LR

A[Citizens (Web/Mobile)] -- REST API --> B[Spring Boot Backend]

B -- DB Access --> C[(PostgreSQL/MongoDB)]

B -- File Upload --> D[File Storage]

B -- Analytics Data --> E[Analytics Dashboard]

B -- Open Data --> F[Open Data API]

G[Authorities (Web)] -- REST API --> B
```

---
### 3. Major Components

- **Frontend:** Citizen portal (web/mobile), Authority dashboard (web)
- **Backend:** Spring Boot REST API, authentication, issue management, analytics, open data
- **Database:** PostgreSQL or MongoDB
- **File Storage:** Local or cloud storage for images
- **Analytics Dashboard:** Data aggregation and visualization
- **Open Data API:** Public, anonymized civic data

---
### 4. Data Flow

1. Citizen reports issue, uploads photo, submits location.
2. Backend validates and stores data.
3. Authorities receive notifications, update status.
4. Analytics module aggregates data for dashboards and open APIs.
5. Public APIs expose anonymized, aggregated data.

---
### 5. Security

- JWT authentication
- Role-based authorization (citizen, authority)
- Input validation and rate limiting

---
### 6. Non-Functional Requirements

- Scalability
- Reliability
- Performance
- Extensibility

---
### 7. Integration Points

- Email/SMS notifications (optional)
- GIS/Map APIs for geolocation
- External civic data consumers via open data APIs

---
### 8. Deployment

- Dockerized Spring Boot app
- Cloud-hosted database and file storage
- CI/CD pipeline for automated testing and deployment
