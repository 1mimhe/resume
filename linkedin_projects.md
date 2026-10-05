# LinkedIn Projects

LinkedIn limits: project description is 2,000 characters, and each entry has a name, dates, associated skills and a URL. All descriptions below are under 1,500 characters. Add the listed skills to each project, since they feed LinkedIn search.

---

## 1. SyncBoard — Real-Time Collaborative Workspace

**URL:** https://github.com/1mimhe/sync-board
**Skills:** NestJS, TypeScript, PostgreSQL, Redis, RabbitMQ

**Description:**
A real-time collaborative workspace (Kanban boards, cards and rich-text documents, in the style of Trello and Notion). I designed and built the whole backend as a NestJS modular monolith, with a React client to demo it.

What I built:
• Architecture: decoupled domain modules (auth, workspace, board, document, notification, activity, file) that talk through domain events, so any module can later be extracted into a microservice.
• Real-time collaboration: concurrent document editing with Yjs (CRDT) over Socket.IO, with debounced persistence to PostgreSQL, live cursors and snapshot versioning. WebSockets scale horizontally through the Redis adapter, and Redis tracks user presence.
• Database: PostgreSQL with Prisma, a monthly range-partitioned audit log, partial and composite indexes, and LexoRank ordering so moving a card updates a single row.
• Async processing: RabbitMQ with topic exchanges, dead letter exchanges, exponential-backoff retries, and Redis-backed idempotent consumers.
• Security: RS256 JWT with rotating refresh tokens and reuse detection, a Redis token blacklist, Google OAuth, multi-tenant RBAC, rate limiting, idempotency keys, and presigned S3 uploads.
• Quality and ops: 1,200+ unit tests (100% coverage), Swagger docs, health probes, structured logging, and a Docker Compose stack (Nginx, PgBouncer, read replicas).

---

## 2. HamBaar — Package Delivery Platform

**URL:** https://github.com/1mimhe/hambaar-backend
**Skills:** NestJS, PostgreSQL, Prisma, Redis, Amazon S3

**Description:**
A platform that matches people who want to send a package with travelers already driving the same route. I led the product definition and the backend design and development.

What I built:
• Matching engine: geospatial route-corridor analysis (Turf.js and the Neshan Maps API) with capacity checks and ranking of compatible trips.
• Pricing engine: dynamic pricing from distance tiers, weight, special handling (fragile or perishable), city factors and route-deviation cost. All rates are configurable.
• Delivery lifecycle: package and trip management, delivery requests, public tracking with unique codes, delivery confirmation codes, and a wallet with escrow and commission settlement.
• Auth and security: multi-stage SMS OTP registration with scoped JWTs (temporary, progress, access), RBAC, Redis sessions, OTP rate limiting and blocking, and presigned S3 uploads with size limits.
• Quality and delivery: 600+ unit tests (~92% coverage), integration tests against real PostgreSQL and Redis, e2e smoke tests, and a GitHub Actions CI/CD pipeline that builds Docker images and deploys them.

---

## 3. MenuChi — No-Code Restaurant Menu Builder (Backend)

**URL:** https://github.com/1mimhe/menuchi-backend
**Skills:** Node.js, Express.js, Prisma, PostgreSQL, Redis

**Description:**
The backend of a no-code platform where restaurants draft items in a backlog, publish menus, and take orders.

What I built:
• Domain model: a multi-tenant hierarchy (restaurant, branch, menu) with a reusable backlog of categories and items. Menus are published with day-based schedules, and customers can order with status tracking (pending, preparing, done).
• Auth: owner login (phone and password, session plus JWT) with scope-based permissions, and customer login by email OTP with rate limiting.
• Integrations: Redis Streams carry image-processing jobs and OTP requests to separate services. Menu images upload through presigned S3 URLs.
• Engineering: dependency injection, zod-validated environment config, centralized error handling that maps Prisma errors to HTTP responses, and Swagger docs generated with TSOA.
• Testing and CI: Vitest and Supertest suites (unit and HTTP router tests) running in GitHub Actions, with Docker for local and production setups.

---

## 4. Bookstore API

**URL:** https://github.com/1mimhe/bookstore-nest
**Skills:** NestJS, TypeORM, MySQL, Redis, REST APIs

**Description:**
A modular, event-driven e-commerce API for a bookstore, built with NestJS.

What I built:
• Data model: a normalized MySQL schema separating titles from physical editions, with authors, translators, publishers, hierarchical tags, blogs and collections.
• E-commerce: carts, discount codes (percentage and fixed), and orders that use atomic conditional SQL updates to decrement stock, which prevents overselling under concurrent requests. A provider-agnostic payment gateway verifies payments on the server and never trusts client-supplied status.
• Content and engagement: reviews with replies and emoji reactions, bookmarks, and support tickets.
• Redis: non-blocking view tracking and trending content, plus session storage.
• Architecture: session-based auth with role guards (RBAC), domain events for asynchronous staff audit logging, a standard response envelope, health probes, and Swagger docs.
• Quality: Jest unit tests, Supertest e2e tests, Docker Compose, and GitHub Actions CI.

---

## 5. NexCart — AI-Powered E-Commerce Engine (In Progress)

**URL:** https://github.com/1mimhe/nexcart (add it only if the repo is public)
**Skills:** Microservices, Apache Kafka, gRPC, System Design, PostgreSQL

**Description:**
A learning-focused project for studying how production microservice systems and AI features are built. It is in the design phase: the architecture, ADRs and documentation are complete, and implementation is starting.

Concepts I am studying and will apply:
• Distributed transactions: Saga orchestration across the Product, Payment and Order services with compensating actions and idempotency keys.
• Reliable events: the Transactional Outbox pattern with Debezium CDC and Kafka (with Schema Registry), to avoid dual-write bugs.
• Service communication: gRPC with Protobuf contracts for synchronous calls, Kafka for asynchronous events, and Kong as the API gateway.
• Identity: OIDC authentication with Keycloak.
• AI integration: hybrid product search (pgvector HNSW plus PostgreSQL full-text search, fused with Reciprocal Rank Fusion), a support chatbot with type-safe function calling streamed over SSE, and LLM cost control (caching, token budgets).
• Operations and testing: Prometheus and Grafana, Docker Compose to k3d, Pact contract tests, and k6 load tests.

Stack: NestJS, TypeScript, gRPC, Kafka, PostgreSQL, pgvector, Redis, Keycloak, Docker.

---

## Tips
- **Order:** put SyncBoard first, then HamBaar, MenuChi and Bookstore, with NexCart last.
- **Dates:** leave the end date empty for NexCart so LinkedIn shows "Present".
- **Link projects to jobs:** if a project was built during a role, you can link it to that position. HamBaar and the others were not done for an employer, so leave them unlinked.
- **Pasting:** LinkedIn keeps line breaks and "•" bullets as plain text. Paste each description as is.
