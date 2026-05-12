# .github

Organization profile and defaults for [Library Booking System](https://github.com/LibraryBookingSystem).

The org overview on GitHub is rendered from [`profile/README.md`](./profile/README.md). Full project documentation lives in the [Documentation](https://github.com/LibraryBookingSystem/Documentation) repository.

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

Each persistence-backed microservice maps to one PostgreSQL database. `auth-service`, `api-gateway`, and `realtime-gateway` are stateless at the database layer.
