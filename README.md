# Crowdsourced Local Issue Reporting Platform

## High-Level Design (HLD)

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

---

## Low-Level Design (LLD)

---

### 1. Entities & Database Schema

#### User

- id (UUID, PK)  
- username (String, unique)  
- password (String, hashed)  
- email (String, unique)  
- role (Enum: CITIZEN, AUTHORITY)  
- created_at (Timestamp)  

#### Issue

- id (UUID, PK)  
- title (String)  
- description (Text)  
- location (GeoPoint or string)  
- status (Enum: REPORTED, IN_PROGRESS, RESOLVED, REJECTED)  
- created_by (FK to User)  
- created_at (Timestamp)  
- updated_at (Timestamp)  

#### IssueImage

- id (UUID, PK)  
- issue_id (FK to Issue)  
- image_url (String)  
- uploaded_at (Timestamp)  

#### Comment

- id (UUID, PK)  
- issue_id (FK to Issue)  
- user_id (FK to User)  
- content (Text)  
- created_at (Timestamp)  

---

### 2. Spring Boot Modules & Packages

- controller  
- service  
- repository  
- security  
- dto  
- exception  
- config  

---

### 3. Key REST Endpoints

#### Authentication

- `POST /api/auth/register`  
- `POST /api/auth/login`  

#### Issue Management

- `POST /api/issues`  
- `GET /api/issues`  
- `GET /api/issues/{id}`  
- `PUT /api/issues/{id}/status`  
- `POST /api/issues/{id}/images`  
- `GET /api/issues/{id}/images`  

#### Comments

- `POST /api/issues/{id}/comments`  
- `GET /api/issues/{id}/comments`  

#### Analytics

- `GET /api/analytics/summary`  

#### Open Data

- `GET /api/open/issues`  

---

### 4. Security Design

- JWT authentication for all endpoints except open data  
- Role-based authorization  

---

### 5. File/Image Handling

- Upload via `/api/issues/{id}/images`  
- Store metadata in DB, files in storage  
- Serve images via secure URLs  

---

### 6. Analytics Module

- Aggregate data using custom queries or projections  
- Endpoints for trends, resolution time, status distribution  

---

### 7. Exception Handling

- Global exception handler  
- Standardized error response  

---

### 8. Testing

- Unit tests for services/controllers  
- Integration tests for API endpoints  
