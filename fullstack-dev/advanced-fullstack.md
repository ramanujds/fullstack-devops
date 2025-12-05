# Advanced Fullstack Developer Program for Banking Systems
## Program Overview

## Week 1 – Advanced Java & Python for services

**Focus:** Deepen backend language skills and patterns used for banking microservices.

- Java advanced
    - Topics: streams, concurrency basics, collections performance, error handling, and Spring Boot patterns for REST services.
    - Labs: build a “customer‑profile” Spring Boot service with layered architecture, DTOs, validation, and basic exception mapping.

- Python advanced
    - Topics: async/await, typing, packaging, virtual environments, and using Python for utilities, ETL, and test harnesses.
    - Labs: implement a Python “fraud rules runner” that consumes mock transactions and flags anomalies; expose core logic as reusable modules.

- Cross‑language exercise
    - Build the same simple business rule (e.g., overdraft check) in Java and Python, discuss performance, readability, and where each language fits in a banking stack.

***

## Week 2 – REST APIs, automation & databases (Postgres, Oracle)

**Focus:** Service design, automation mindset, and working with relational databases.

- REST APIs
    - Topics: resource modeling, idempotency, versioning, pagination, error codes, standards for banking APIs (e.g., OpenAPI/Swagger contracts).
    - Labs: design and implement REST endpoints for “accounts” and “transactions” with proper status codes, validation, and OpenAPI docs.

- Introduction to automation
    - Topics: scriptable builds, task runners, using Python or shell to automate repetitive tasks (data loading, test runs, schema migrations).
    - Labs: automate database migrations and seed data tasks for dev environments using scripts and CI jobs.

- Postgres & Oracle
    - Topics: schema design for banking entities (customers, accounts, transactions), indexing, constraints, basic performance tuning.
    - Labs:
        - Implement the same schema in Postgres and Oracle.
        - Build Java data access layers (JPA/JDBC) and Python data access (SQLAlchemy/psycopg2 or cx_Oracle) to run CRUD and simple report queries.

***

## Week 3 – Secure data & API integration for banking

**Focus:** Integrations across systems, secure APIs, and Open Banking‑style use cases.

- Secure APIs & Open Banking concepts
    - Topics: OAuth2/OIDC, JWT, mTLS overview, consent flows, rate limiting and throttling, and typical Open Banking standards.
    - Labs:
        - Protect a sample “account‑info” API with token‑based auth.
        - Implement rate limiting and basic API key model for partner access.

- Data and API integration
    - Topics: integrating core systems with external fraud/risk engines and third‑party fintech APIs; patterns like API gateway, message queues, and file‑based interfaces.
    - Labs:
        - Build a “transaction router” service that calls a mock fraud engine API before committing transactions to the DB.
        - Implement a small ETL pipeline in Python that pulls batched data from an external API, transforms it, and loads into Postgres for reporting.

- Mini‑case: Open Banking & fraud
    - Design an integration where a third‑party app accesses account data via secure APIs while a risk engine analyzes transactions in near real time; learners implement a minimal end‑to‑end flow with stubs for external parties.

***

## Week 4 – Testing, compliance, and API customization

**Focus:** Quality, non‑functional testing, and customizing APIs for banking scenarios.

- Testing banking systems and applications
    - Functional testing: write unit and integration tests for Java and Python services, including DB and API tests.
    - Compliance & security: introduce basic secure‑coding checks, static analysis, and simple penetration‑testing concepts (input validation, auth/authorization checks, common OWASP issues).
    - Load testing: use a tool like JMeter or k6 to simulate peak traffic on the account and transaction APIs, record throughput/latency, and identify bottlenecks.

- API and customization exercises
    - Customize APIs for different channels (retail vs corporate) with different fields, limits, and SLAs while reusing core services.
    - Add feature toggles or configuration‑driven behavior (e.g., different overdraft rules per market) to the existing services.
    - Final mini‑project:
        - Combine Java backend, Python utilities, REST APIs, Postgres/Oracle, and integration components into a small “mini‑banking platform.”
        - Demonstrate: secure login flow, account/transaction APIs, sample fraud check, and basic test reports (functional + performance).

