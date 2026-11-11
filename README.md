# System Design: 100 Practical Notes

A problem-first curriculum from HTTP contracts to distributed-system case studies. Notes 001–080 build the foundations; 081–100 combine them into complete design exercises. These are learning notes and hypothetical designs, not claims about any company's production architecture.

Start with [START-HERE](START-HERE.md), record attempts in [PRACTICE-LOG](PRACTICE-LOG.md), and use [REFERENCES](REFERENCES.md) for primary technical reading.

Each new note includes prerequisites, a prediction question, a collapsible worked approach, trade-offs, failure practice, and a 40-minute session. Do the exercise before marking a note complete. The original HTTP note is preserved in the first track.

## Tracks

| Track | Notes | Focus |
| --- | --- | --- |
| [http and apis](designs/01-http-and-apis/README.md) | 001–010 | Contracts and request boundaries |
| [data and storage](designs/02-data-and-storage/README.md) | 011–020 | Models, transactions, and data lifecycle |
| [architecture and capacity](designs/03-architecture-and-capacity/README.md) | 021–030 | Requirements and architecture choices |
| [performance and scaling](designs/04-performance-and-scaling/README.md) | 031–040 | Latency, capacity, caching, and overload |
| [jobs and events](designs/05-jobs-and-events/README.md) | 041–050 | Recoverable background workflows |
| [distributed systems](designs/06-distributed-systems/README.md) | 051–060 | Coordination, replication, and ownership |
| [reliability and operations](designs/07-reliability-and-operations/README.md) | 061–070 | Operating and recovering systems |
| [security and multi tenancy](designs/08-security-and-multi-tenancy/README.md) | 071–080 | Identity, isolation, and data protection |
| [product designs](designs/09-product-designs/README.md) | 081–090 | Ten product design exercises |
| [advanced case studies](designs/10-advanced-case-studies/README.md) | 091–100 | Advanced designs and a capstone |

## All notes


### 01 · http and apis

- [001 · HTTP API Requests and Responses](designs/01-http-and-apis/001-http-api-request-response.md)
- [002 · REST Resource and Endpoint Design](designs/01-http-and-apis/002-rest-resource-and-endpoint-design.md)
- [003 · Request Validation and Boundary Design](designs/01-http-and-apis/003-request-validation-and-boundary-design.md)
- [004 · Consistent API Error Responses](designs/01-http-and-apis/004-consistent-api-error-responses.md)
- [005 · Pagination and Stable Ordering](designs/01-http-and-apis/005-pagination-and-stable-ordering.md)
- [006 · Filtering Sorting and Search Contracts](designs/01-http-and-apis/006-filtering-sorting-and-search-contracts.md)
- [007 · Authentication and Session Design](designs/01-http-and-apis/007-authentication-and-session-design.md)
- [008 · API Versioning and Compatibility](designs/01-http-and-apis/008-api-versioning-and-compatibility.md)
- [009 · Conditional Requests and Concurrent API Updates](designs/01-http-and-apis/009-conditional-requests-and-concurrent-api-updates.md)
- [010 · Synchronous and Asynchronous API Contracts](designs/01-http-and-apis/010-synchronous-and-asynchronous-api-contracts.md)

### 02 · data and storage

- [011 · Relational Data Modeling](designs/02-data-and-storage/011-relational-data-modeling.md)
- [012 · SQL versus Document and Key Value Storage](designs/02-data-and-storage/012-sql-versus-document-and-key-value-storage.md)
- [013 · Indexes and Query Access Paths](designs/02-data-and-storage/013-indexes-and-query-access-paths.md)
- [014 · Transactions and Atomic Business Changes](designs/02-data-and-storage/014-transactions-and-atomic-business-changes.md)
- [015 · Isolation Levels and Read Anomalies](designs/02-data-and-storage/015-isolation-levels-and-read-anomalies.md)
- [016 · Optimistic and Pessimistic Concurrency](designs/02-data-and-storage/016-optimistic-and-pessimistic-concurrency.md)
- [017 · Schema Migrations without Downtime](designs/02-data-and-storage/017-schema-migrations-without-downtime.md)
- [018 · Object Storage and Metadata Design](designs/02-data-and-storage/018-object-storage-and-metadata-design.md)
- [019 · Data Retention Archival and Deletion](designs/02-data-and-storage/019-data-retention-archival-and-deletion.md)
- [020 · Read Models and Materialized Views](designs/02-data-and-storage/020-read-models-and-materialized-views.md)

### 03 · architecture and capacity

- [021 · Requirements and Quality Attributes](designs/03-architecture-and-capacity/021-requirements-and-quality-attributes.md)
- [022 · Traffic and Storage Estimation](designs/03-architecture-and-capacity/022-traffic-and-storage-estimation.md)
- [023 · Latency Throughput and Concurrency](designs/03-architecture-and-capacity/023-latency-throughput-and-concurrency.md)
- [024 · Tracing a Request through the Network](designs/03-architecture-and-capacity/024-tracing-a-request-through-the-network.md)
- [025 · Modular Monolith Design](designs/03-architecture-and-capacity/025-modular-monolith-design.md)
- [026 · Service Boundaries and Microservice Extraction](designs/03-architecture-and-capacity/026-service-boundaries-and-microservice-extraction.md)
- [027 · Stateless Compute and Shared State](designs/03-architecture-and-capacity/027-stateless-compute-and-shared-state.md)
- [028 · API Gateways and Backend for Frontend](designs/03-architecture-and-capacity/028-api-gateways-and-backend-for-frontend.md)
- [029 · Protocols for Real Time Communication](designs/03-architecture-and-capacity/029-protocols-for-real-time-communication.md)
- [030 · Architecture Decisions and Evolution](designs/03-architecture-and-capacity/030-architecture-decisions-and-evolution.md)

### 04 · performance and scaling

- [031 · Load Balancing and Health Checks](designs/04-performance-and-scaling/031-load-balancing-and-health-checks.md)
- [032 · Cache Aside Design](designs/04-performance-and-scaling/032-cache-aside-design.md)
- [033 · Cache Invalidation and Staleness](designs/04-performance-and-scaling/033-cache-invalidation-and-staleness.md)
- [034 · Cache Stampedes Hot Keys and Eviction](designs/04-performance-and-scaling/034-cache-stampedes-hot-keys-and-eviction.md)
- [035 · Content Delivery Networks](designs/04-performance-and-scaling/035-content-delivery-networks.md)
- [036 · Rate Limiting and Quotas](designs/04-performance-and-scaling/036-rate-limiting-and-quotas.md)
- [037 · Autoscaling and Capacity Headroom](designs/04-performance-and-scaling/037-autoscaling-and-capacity-headroom.md)
- [038 · Connection Pools and Resource Budgets](designs/04-performance-and-scaling/038-connection-pools-and-resource-budgets.md)
- [039 · Backpressure and Load Shedding](designs/04-performance-and-scaling/039-backpressure-and-load-shedding.md)
- [040 · Performance Testing and Bottleneck Analysis](designs/04-performance-and-scaling/040-performance-testing-and-bottleneck-analysis.md)

### 05 · jobs and events

- [041 · Durable Job Queues and Worker Acknowledgments](designs/05-jobs-and-events/041-durable-job-queues-and-worker-acknowledgments.md)
- [042 · Timeouts Deadlines and Cancellation](designs/05-jobs-and-events/042-timeouts-deadlines-and-cancellation.md)
- [043 · Retries Backoff and Jitter](designs/05-jobs-and-events/043-retries-backoff-and-jitter.md)
- [044 · Idempotency Keys and Duplicate Requests](designs/05-jobs-and-events/044-idempotency-keys-and-duplicate-requests.md)
- [045 · Dead Letter Queues and Safe Replay](designs/05-jobs-and-events/045-dead-letter-queues-and-safe-replay.md)
- [046 · Reliable Webhook Delivery](designs/05-jobs-and-events/046-reliable-webhook-delivery.md)
- [047 · Transactional Outbox](designs/05-jobs-and-events/047-transactional-outbox.md)
- [048 · Event Ordering and Partition Keys](designs/05-jobs-and-events/048-event-ordering-and-partition-keys.md)
- [049 · Sagas and Compensating Actions](designs/05-jobs-and-events/049-sagas-and-compensating-actions.md)
- [050 · Event Sourcing and Projection Rebuilds](designs/05-jobs-and-events/050-event-sourcing-and-projection-rebuilds.md)

### 06 · distributed systems

- [051 · Replication and Failover](designs/06-distributed-systems/051-replication-and-failover.md)
- [052 · Consistency Models and User Guarantees](designs/06-distributed-systems/052-consistency-models-and-user-guarantees.md)
- [053 · Network Partitions and CAP Tradeoffs](designs/06-distributed-systems/053-network-partitions-and-cap-tradeoffs.md)
- [054 · Quorums and Replica Overlap](designs/06-distributed-systems/054-quorums-and-replica-overlap.md)
- [055 · Sharding and Partition Key Selection](designs/06-distributed-systems/055-sharding-and-partition-key-selection.md)
- [056 · Consistent Hashing and Rebalancing](designs/06-distributed-systems/056-consistent-hashing-and-rebalancing.md)
- [057 · Leader Election and Consensus](designs/06-distributed-systems/057-leader-election-and-consensus.md)
- [058 · Distributed Locks Leases and Fencing](designs/06-distributed-systems/058-distributed-locks-leases-and-fencing.md)
- [059 · Distributed IDs and Clock Behavior](designs/06-distributed-systems/059-distributed-ids-and-clock-behavior.md)
- [060 · Cross Region Data and Conflict Resolution](designs/06-distributed-systems/060-cross-region-data-and-conflict-resolution.md)

### 07 · reliability and operations

- [061 · Logs Metrics and Distributed Traces](designs/07-reliability-and-operations/061-logs-metrics-and-distributed-traces.md)
- [062 · Service Level Indicators and Error Budgets](designs/07-reliability-and-operations/062-service-level-indicators-and-error-budgets.md)
- [063 · Actionable Alerting and Incident Response](designs/07-reliability-and-operations/063-actionable-alerting-and-incident-response.md)
- [064 · Rolling Canary and Blue Green Deployments](designs/07-reliability-and-operations/064-rolling-canary-and-blue-green-deployments.md)
- [065 · Feature Flags and Safe Rollback](designs/07-reliability-and-operations/065-feature-flags-and-safe-rollback.md)
- [066 · Circuit Breakers and Bulkheads](designs/07-reliability-and-operations/066-circuit-breakers-and-bulkheads.md)
- [067 · Backups Restore and Disaster Recovery](designs/07-reliability-and-operations/067-backups-restore-and-disaster-recovery.md)
- [068 · Graceful Degradation and Dependency Budgets](designs/07-reliability-and-operations/068-graceful-degradation-and-dependency-budgets.md)
- [069 · Failure Injection and Resilience Testing](designs/07-reliability-and-operations/069-failure-injection-and-resilience-testing.md)
- [070 · Operational Readiness and Runbooks](designs/07-reliability-and-operations/070-operational-readiness-and-runbooks.md)

### 08 · security and multi tenancy

- [071 · Authorization and Object Ownership](designs/08-security-and-multi-tenancy/071-authorization-and-object-ownership.md)
- [072 · Multi Tenant Data Isolation](designs/08-security-and-multi-tenancy/072-multi-tenant-data-isolation.md)
- [073 · Service Identity and Least Privilege](designs/08-security-and-multi-tenancy/073-service-identity-and-least-privilege.md)
- [074 · Secrets and Key Rotation](designs/08-security-and-multi-tenancy/074-secrets-and-key-rotation.md)
- [075 · Encryption and Data Protection Boundaries](designs/08-security-and-multi-tenancy/075-encryption-and-data-protection-boundaries.md)
- [076 · Audit Trails and Tamper Evidence](designs/08-security-and-multi-tenancy/076-audit-trails-and-tamper-evidence.md)
- [077 · Input Trust Boundaries and SSRF Defense](designs/08-security-and-multi-tenancy/077-input-trust-boundaries-and-ssrf-defense.md)
- [078 · Abuse Prevention and Resource Isolation](designs/08-security-and-multi-tenancy/078-abuse-prevention-and-resource-isolation.md)
- [079 · Privacy Deletion and Data Minimization](designs/08-security-and-multi-tenancy/079-privacy-deletion-and-data-minimization.md)
- [080 · Threat Modeling and Security Design Review](designs/08-security-and-multi-tenancy/080-threat-modeling-and-security-design-review.md)

### 09 · product designs

- [081 · URL Shortener](designs/09-product-designs/081-url-shortener.md)
- [082 · Notification Delivery Platform](designs/09-product-designs/082-notification-delivery-platform.md)
- [083 · Ticket Booking and Seat Reservations](designs/09-product-designs/083-ticket-booking-and-seat-reservations.md)
- [084 · Shopping Cart and Checkout](designs/09-product-designs/084-shopping-cart-and-checkout.md)
- [085 · Chat and Offline Message Delivery](designs/09-product-designs/085-chat-and-offline-message-delivery.md)
- [086 · File Sharing and Resumable Uploads](designs/09-product-designs/086-file-sharing-and-resumable-uploads.md)
- [087 · Product Search and Index Synchronization](designs/09-product-designs/087-product-search-and-index-synchronization.md)
- [088 · Social Feed and Fan Out](designs/09-product-designs/088-social-feed-and-fan-out.md)
- [089 · Location Based Nearby Search](designs/09-product-designs/089-location-based-nearby-search.md)
- [090 · Scheduled Jobs and Distributed Cron](designs/09-product-designs/090-scheduled-jobs-and-distributed-cron.md)

### 10 · advanced case studies

- [091 · Multi Region Order Processing](designs/10-advanced-case-studies/091-multi-region-order-processing.md)
- [092 · Payment Ledger and Reconciliation](designs/10-advanced-case-studies/092-payment-ledger-and-reconciliation.md)
- [093 · Live Video Streaming Delivery](designs/10-advanced-case-studies/093-live-video-streaming-delivery.md)
- [094 · Collaborative Document Editing](designs/10-advanced-case-studies/094-collaborative-document-editing.md)
- [095 · Distributed Web Crawler](designs/10-advanced-case-studies/095-distributed-web-crawler.md)
- [096 · Metrics Ingestion and Time Series Storage](designs/10-advanced-case-studies/096-metrics-ingestion-and-time-series-storage.md)
- [097 · Distributed Task Scheduler](designs/10-advanced-case-studies/097-distributed-task-scheduler.md)
- [098 · Inventory Reservation across Warehouses](designs/10-advanced-case-studies/098-inventory-reservation-across-warehouses.md)
- [099 · Large Scale Data Migration and Cutover](designs/10-advanced-case-studies/099-large-scale-data-migration-and-cutover.md)
- [100 · Architecture Capstone and Design Defense](designs/10-advanced-case-studies/100-architecture-capstone-and-design-defense.md)
