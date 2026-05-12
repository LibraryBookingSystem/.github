# Library Booking System

Microservice platform for reserving library seats and rooms. A Flutter client talks to Spring Boot services through one API gateway, with JWT and role-based access, policy checks before bookings, RabbitMQ-driven updates, and Docker Compose for a full local stack.

## What it does

- Authenticate users and issue JWTs with shared RBAC across services
- Manage users, resources, bookings, policies, notifications, and analytics
- Stream live availability and domain events over WebSockets
- Run the backend locally with PostgreSQL, Redis, RabbitMQ, and PowerShell setup scripts

## Architecture

```mermaid
flowchart TB
  Client[frontend-web] --> GW[api-gateway :8080]
  GW --> AUTH[auth-service :3002]
  GW --> USER[user-service :3001]
  GW --> CAT[catalog-service :3003]
  GW --> BOOK[booking-service :3004]
  GW --> POL[policy-service :3005]
  GW --> NOTIF[notification-service :3006]
  GW --> ANA[analytics-service :3007]
  GW --> RT[realtime-gateway :3008]

  USER --> USER_DB[(user_db)]
  CAT --> CAT_DB[(catalog_db)]
  BOOK --> BOOK_DB[(booking_db)]
  POL --> POL_DB[(policy_db)]
  NOTIF --> NOTIF_DB[(notification_db)]
  ANA --> ANA_DB[(analytics_db)]

  USER --> REDIS[(Redis)]
  BOOK --> RMQ[(RabbitMQ)]
  CAT --> RMQ
  POL --> RMQ
  NOTIF --> RMQ
  ANA --> RMQ
  RT --> RMQ
```

Each persistence-backed microservice owns one PostgreSQL database on the shared Postgres instance. `auth-service`, `api-gateway`, and `realtime-gateway` do not have their own databases.

## Start here

| Repository | Purpose |
| --- | --- |
| [Documentation](https://github.com/LibraryBookingSystem/Documentation) | Architecture, API reference, authorization |
| [docker-compose](https://github.com/LibraryBookingSystem/docker-compose) | Run the full backend locally |
| [frontend-web](https://github.com/LibraryBookingSystem/frontend-web) | Flutter client |

## Services

`auth-service` · `user-service` · `catalog-service` · `booking-service` · `policy-service` · `notification-service` · `analytics-service` · `api-gateway` · `realtime-gateway` · `common-aspects`

## Stack

Java 17 and Spring Boot 3.5, PostgreSQL, RabbitMQ, Redis, Nginx, Node.js WebSockets, Flutter / Dart 3+.
