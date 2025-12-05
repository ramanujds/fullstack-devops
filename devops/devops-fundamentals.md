# Devops Fundamentals for Banking Professionals

## Duration: 60 hours

## 1. OS concepts (4 hours)

- Theory (1.5h):
    - Linux directory structure, FHS, where apps/logs/configs live.[4]
    - Permissions, ownership, basic security hygiene for multi‑user servers.
    - Services/daemons using `systemd` and `systemctl`, unit files, runlevels.
    - Log locations (`/var/log`), log rotation concepts, reading logs to diagnose issues.

- Hands‑on (2.5h):
    - Navigate directories, explore `/etc`, `/var`, `/opt`, and app logs on a practice VM.
    - Change file/directory ownership and permissions for a sample banking API service user.
    - Enable/disable and restart a mock “payments-api” service via `systemctl`, check its logs, and fix a failing start by reading error messages.

- Use case / case study:
    - “Core‑banking API node is down”: Trainees act as L1 DevOps, log into a Linux server, inspect the directory layout, check systemd service status, read logs, and restore the service—mirroring a real banking production incident.

***

## 2. Linux Shell Scripting (8 hours)

- Theory (2.5h):
    - Process management (`ps`, `top`, `htop`, `kill`, exit codes) and why monitoring processes matters in 24x7 banking systems.[1]
    - Shell variables, environment variables, and secure handling of secrets (no passwords in history).
    - Conditional statements and loops; exit codes and error handling patterns.
    - Good practices: shebangs, comments, parameterization, and idempotent scripts.

- Hands‑on (5.5h):
    - Monitor and kill a hung “statement‑generator” process safely in a lab VM.
    - Write small scripts to:
        - Check disk usage and alert if above a threshold.
        - Tail and filter application logs for “ERROR” and “FAILED LOGIN” patterns.
        - Rotate and compress old log files daily.
    - Mini‑project: build a “pre‑deployment check” script that validates: service status, free disk/CPU, app log size, and connectivity to a database host, returning a pass/fail code for a CI job.

- Use case / case study:
    - “Nightly settlement job automation”: design a script that triggers a mock batch process, archives previous logs, and sends a summary to a log file that operations can review next morning—simulating end‑of‑day batch in a bank.

***

## 3. Networking basics (4 hours)

- Theory (1.5h):
    - IP concepts, subnetting, CIDR; public vs private IPs; DNS high‑level.[1]
    - Routing and NAT basics; how users reach internal services in a bank through load balancers and firewalls.

- Hands‑on (2.5h):
    - Use `ip`, `ss`/`netstat`, and `traceroute` to inspect connectivity between a “channel” VM and a “core‑banking” VM.
    - Simulate a NAT scenario using local VMs/containers and show what breaks when routes or masks are wrong.
    - Resolve names using `dig`/`nslookup` and verify public vs private access.

- Use case / case study:
    - “Internet banking is slow for some branches”: learners inspect IP configuration, use traceroute and DNS lookups to identify a misconfigured gateway or DNS entry for a branch proxy.

***

## 4. Protocols (4 hours)

- Theory (1.5h):
    - HTTP vs HTTPS in banking portals; request/response model, status codes, idempotent vs non‑idempotent calls.[1]
    - TLS handshake overview, certificates, CA trust, and why HSTS and modern ciphers matter for banking.
    - REST APIs and internal microservice calls in Temenos‑like environments (e.g., core banking microservices behind an API gateway).

- Hands‑on (2.5h):
    - Use `curl` and a REST client to call a sample “account-balance” service over HTTP and HTTPS, inspect headers and status codes.
    - Create a self‑signed certificate and configure a simple HTTPS endpoint (e.g., Nginx or a demo microservice).
    - Capture and review traffic with a browser dev‑tools or `tcpdump`/`Wireshark` in a controlled lab to see HTTP vs HTTPS.

- Use case / case study:
    - “Certificate expiry incident”: simulate a banking API whose HTTPS certificate is expired, observe client errors, renew the certificate in the lab and validate the fix.

***

## 5. Introduction to Cloud (4 hours)

- Theory (1.5h):
    - Cloud definition, why organizations adopt it (scalability, pay‑as‑you‑go), and typical banking constraints (regulation, data residency).[3][4]
    - Regions and Availability Zones; shared responsibility model (security of vs in the cloud).[5]

- Hands‑on (2.5h):
    - Use the AWS or Azure console to explore regions, AZs, and an example VPC or VN.
    - Deploy a tiny test EC2/VM and observe metadata (region, AZ) and basic monitoring dashboards.

- Use case / case study:
    - “Disaster recovery for internet banking”: discuss and whiteboard how multi‑AZ deployment protects a core banking front‑end, then show region/AZ configuration for the lab instance.

***

## 6. Cloud models and advantages (4 hours)

- Theory (1.5h):
    - IaaS, PaaS, SaaS definitions with banking‑oriented examples such as managed databases, integration runtimes, or SaaS AML tools.[3][4]
    - Customer vs provider responsibilities in each model, mapped to the shared responsibility model.

- Hands‑on (2.5h):
    - Classify a list of services (EC2, RDS, S3, Managed Kubernetes, CRM SaaS) into IaaS/PaaS/SaaS.
    - Use console or CLI to inspect configurations of a sample IaaS VM vs a managed DB, noting what the team controls vs the provider.

- Use case / case study:
    - “Migrating on‑prem payments app to cloud”: evaluate which components should be IaaS (custom app servers) and which can be PaaS/SaaS (managed DB, observability) to reduce operational risk.

***

## 7. Basic cloud services (compute, storage, networking) – 8 hours

- Theory (3h):
    - Global infrastructure overview; basic AWS constructs like VPC, subnets, internet/NAT gateways.[4]
    - Compute basics: EC2 vs containers, autoscaling groups, instance types.
    - Storage basics: S3 object storage concepts, versioning, lifecycle policies.
    - Database basics: high‑level RDS vs DynamoDB and when each might fit banking workloads.[6][4]

- Hands‑on (5h):
    - Create a VPC with public and private subnets, attach an internet gateway and route tables.
    - Launch an EC2 instance in a public subnet and store files in an S3 bucket, then secure S3 access via IAM policies.
    - Create a simple RDS instance or equivalent managed DB, connect from the EC2 instance, and run a few queries for a “customer profile” table.

- Use case / case study:
    - “Customer profile service” in cloud: design a simple architecture where a microservice runs on EC2/containers, stores static artifacts in S3 and data in RDS, and is reachable via public subnet while DB stays private.

***

## 8. Major cloud providers (AWS, Azure, GCP) – 4 hours

- Theory (2h):
    - High‑level comparison: core compute, storage, networking, serverless, DevOps tooling.[4][1]
    - Why many banks prefer AWS (mature services, compliance programs, regional coverage), plus notes on hybrid/multi‑cloud patterns.[3]

- Hands‑on (2h):
    - Map equivalent services: EC2 vs Azure VM vs GCE; S3 vs Blob Storage vs GCS; IAM vs AAD; RDS vs Azure SQL vs Cloud SQL.
    - Browse public documentation/compliance pages for AWS and one other provider to see banking‑relevant certifications.

- Use case / case study:
    - “Choosing a cloud provider for Temenos‑like core banking”: groups propose an architecture on AWS vs Azure for the same workload and justify their choice in terms of compliance, services, and ecosystem.

***

## 9. Cloud IAM (Identity and Access Management) – 4 hours

- Theory (1.5h):
    - IAM users, roles, groups, and policies; least‑privilege principle; separation of duties.[5][4]
    - Multi‑factor authentication and why it is mandatory for privileged banking accounts.

- Hands‑on (2.5h):
    - Create IAM users and groups for “Dev”, “Ops”, and “Audit” with different permissions.
    - Create a role for an application EC2 instance to access S3 without static credentials.
    - Enable MFA for an administrator account in the lab environment.

- Use case / case study:
    - “Third‑party vendor access to bank cloud account”: design a role that gives limited, time‑bound access to a vendor for troubleshooting, without exposing full admin privileges.

***

## 10. Secure cloud architecture (8 hours)

- Theory (3h):
    - Public vs private subnet design, DMZ concepts, and layering services (API gateway, app tier, DB tier) for internet‑facing banking workloads.
    - Security Groups vs Network ACLs, when to use each; bastion host model; encryption at rest (KMS, managed keys) and in transit.

- Hands‑on (5h):
    - Build a 3‑tier VPC: public subnet with bastion + load balancer, private subnets for app and DB tiers.
    - Configure Security Groups to allow only required ports between tiers and restrict SSH to the bastion.
    - Enable encryption at rest on a demo DB and S3 bucket; enforce HTTPS on a sample API endpoint.

- Use case / case study:
    - “Designing secure internet banking architecture”: teams design and then implement a minimal secure layout for a mock Temenos‑like core banking front‑end, presenting how they keep customer data isolated and minimize attack surface.

***

## 11. Security incident reporting (8 hours)

- Theory (3h):
    - What to check when something goes wrong: logs, metrics, recent deployments, access changes; basic incident‑response flow (detect, triage, contain, recover, learn).
    - Key cloud and application logs (CloudWatch / equivalent, load balancer logs, app logs), and which ones matter for security vs performance.
    - High‑level escalation paths in regulated banking environments: runbooks, incident severities, and communication.

- Hands‑on (5h):
    - Trigger a controlled “incident” (e.g., failing health checks, unauthorized API calls) and ask participants to investigate using logs and metrics.
    - Collect evidence: copy relevant log excerpts, note timestamps, identify impacted services, and fill an incident report template.
    - Draft a basic post‑incident review with root cause, impact, and action items (e.g., improved alerts, extra checks in CI/CD).

- Use case / case study:
    - “Suspicious login pattern in internet banking”: simulate repeated failed logins from unusual IPs, have participants detect it from logs, classify severity, and propose containment steps (WAF rule, temporary block, MFA enforcement).

***

## 12. DevOps culture and CI/CD concepts (4 hours)

- Theory (1.5h):
    - DevOps principles: collaboration, shared responsibility, automation, feedback loops; why these are critical for complex core‑banking environments.
    - CI/CD stages: code, build, test, security scan, package, deploy, monitor; trunk‑based vs feature‑branch workflows at a high level.

- Hands‑on (2.5h):
    - Draw the CI/CD pipeline for a sample “payments API” showing build, unit tests, container image creation, and deployment to a test environment.
    - Use a CI tool (GitHub Actions / GitLab CI / Jenkins) to build a simple application, run tests, and produce an artifact.

- Use case / case study:
    - “Reducing release risk for Temenos upgrades”: discuss how CI/CD and blue‑green or canary strategies reduce downtime and allow frequent releases of banking services.

***

## 13. Basic version control with Git (8 hours)

- Theory (2.5h):
    - Git objects, commits, branches, remotes; conceptual model needed to work confidently in teams.
    - Branching strategies suitable for regulated environments (e.g., main + release branches; protected branches; code review and approvals).

- Hands‑on (5.5h):
    - Initialize a repo for a sample microservice; practice `clone`, `status`, `add`, `commit`, `push`, `pull`.
    - Create feature branches, raise merge requests, resolve merge conflicts in code and configuration files.
    - Implement a simple team workflow: one learner plays “platform engineer”, another “application developer”, and they collaborate through feature branches, reviews, and approvals.

- Use case / case study:
    - “Managing infrastructure‑as‑code for multiple environments”: maintain separate branches/folders for dev, test, and prod environment definitions, showing how approvals are required before merging changes that impact production banking systems.

***

## 14. Content Delivery and DNS management (8 hours)

- Theory (3h):
    - What DNS does in a banking context: resolving internet banking URLs, internal service discovery, and importance of TTLs.
    - Common routing policies (simple, weighted, latency, failover, geolocation) and how they support high availability and DR.
    - CDN basics using CloudFront‑like services: caching static content, TLS termination, WAF integration, and why some banks prefer client‑managed DNS with strict controls.

- Hands‑on (5h):
    - Configure DNS records for a mock “onlinebank.temenos‑lab.com” with A/CNAME records pointing to a load balancer.
    - Implement a basic CloudFront‑style distribution in front of a static banking web front‑end, enforce HTTPS, and test cache behaviour.
    - Experiment with weighted or latency‑based routing between two simple endpoints (e.g., two “internet banking” demo sites in different regions).

- Use case / case study:
    - “Failover for internet banking front‑end”: design DNS and CDN settings so that if the primary region fails, traffic can be routed to a secondary region with minimal downtime, respecting typical banking SLAs.

***

## 15. Containers (Docker basics) – 12 hours

- Theory (4h):
    - What containers are and why they matter for DevOps and microservices: immutability, portability, resource efficiency.
    - Docker images, layers, registries; basic structure of a Dockerfile and image‑build pipeline.
    - Container networking and storage basics; mapping to cloud container services (ECS/EKS/AKS) and why Temenos relies heavily on container‑based deployments.

- Hands‑on (8h):
    - Containerize a simple “account‑service” application: write a Dockerfile, build and run the container, and expose an HTTP endpoint.
    - Use a local or cloud container registry to push and pull images, including version tags for different application releases.
    - Compose or script a small multi‑container setup: API + DB + log shipper; practice scaling the API container and observing behaviour.
    - Integrate the container build into CI/CD so that every commit builds, scans (basic image scan), and pushes a new version to the registry.

- Use case / case study:
    - “Standardizing deployments for Temenos‑like microservices”: create a base image for banking microservices (with common runtime, logging agent, security settings) and then derive service‑specific images, highlighting how this simplifies deployment and compliance audits.

***
