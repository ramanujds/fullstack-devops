# Advanced DevOps for Banking Cloud Platforms


## Authentication & Security (AWS Identity Center, MFA, fraud) – 6 hours

- Theory (2h):
    - AWS IAM Identity Center basics: centralized identity, SSO patterns, and where it fits in a multi‑account banking environment.[3][4]
    - MFA options, device binding, and step‑up authentication for privileged operations.[5][6]
    - Encryption foundations: keys, KMS, envelope encryption; data at rest vs in transit for APIs and databases.

- Hands‑on (4h):
    - Set up an AWS Identity Center instance in a lab: create users/groups and assign access to a couple of accounts or apps.[3]
    - Enforce MFA and register a test MFA device; configure a basic device‑binding policy (e.g., trusted browser/device).[7][5]
    - Enable HTTPS with TLS for a sample API, store secrets/keys securely (Parameter Store/Secrets Manager), and turn on default KMS encryption for an S3 bucket and RDS instance.

- Use case / case study:
    - “Fraud portal access hardening”: trainees design how a fraud‑operations portal is protected with Identity Center SSO, mandatory MFA, device binding, and per‑role permissions; then implement a minimal version in the lab and discuss how it mitigates account‑takeover risk in banking.[8][9]

***

## Performance & Scalability (Autoscaling, failover) – 8 hours

- Theory (3h):
    - Autoscaling basics: scaling metrics, step vs target tracking policies, warm‑up considerations for banking APIs under peak loads.[2][1]
    - Load balancing strategies: ALB vs NLB high‑level; health checks; session stickiness for stateful vs stateless services.
    - Capacity planning and failover principles: multi‑AZ, active‑active vs active‑passive, RTO/RPO terms for critical applications.

- Hands‑on (5h):
    - Configure an Auto Scaling Group behind an ALB for a containerized “payments API,” then run a load test and watch instances scale out/in.
    - Simulate an AZ failure by intentionally failing health checks or stopping instances in one AZ and validate that traffic fails over to healthy instances.
    - Use CloudWatch dashboards and alarms to monitor CPU, latency, and error rates; adjust scaling thresholds based on observations.

- Use case / case study:
    - “Black Friday/Salary‑day peak handling”: design and implement an autoscaling and load‑balancing strategy for a bank’s card‑authorization service, showing how it copes with sharp, time‑bound spikes without over‑provisioning.

***

## Kafka Fundamentals – 8 hours

- Theory (3h):
    - What Kafka is: topics, partitions, producers, consumers, consumer groups, and retention.[10]
    - Why Kafka: decoupling, back‑pressure handling, replay, exactly‑once/at‑least‑once semantics; comparison with traditional queues.[9]
    - Key banking use cases: real‑time payments, fraud detection, transaction streaming to risk engines and regulatory reporting.[11][12]

- Hands‑on (5h):
    - Set up a local Kafka cluster (or managed Kafka) and create topics for “transactions,” “alerts,” and “audit‑events.”
    - Build a simple producer that publishes mock card transactions; build consumers for fraud‑rule evaluation and an audit store.
    - Demonstrate consumer group scaling: increase consumer count and show parallel processing and rebalancing.

- Use case / case study:
    - “Real‑time fraud scoring stream”: trainees implement a basic flow where card‑swipe events flow into Kafka, a consumer applies simple rules (e.g., unusual geography or amount), and suspicious transactions are flagged for review, illustrating low‑latency fraud detection.

***

## Advanced CI/CD – 12 hours

- Theory (4h):
    - Multi‑stage pipelines for microservices: separate build, test, security scan, image build, deploy, and post‑deploy verification stages.[13]
    - Rollback models: blue/green, canary, and feature flags; when to use which in regulated banking environments.
    - Artifact management: artifact repositories (e.g., ECR/Nexus), traceability of builds to commits and change requests.
    - CI/CD specifics for EKS workloads: manifests/Helm, GitOps patterns, and environment promotion (dev → test → UAT → prod).

- Hands‑on (8h):
    - Build a multi‑stage pipeline for an EKS‑deployed microservice: compile, run tests, build Docker image, push to ECR, deploy to a test namespace.
    - Implement blue/green or canary deployment for this service using Kubernetes deployments or a service mesh/ingress to control traffic.
    - Configure artifact retention and metadata (build number, git SHA, change ticket) so each deployment is auditable.
    - Break a deployment (intentional bug), perform a pipeline‑driven rollback, and confirm the previous version is restored.

- Use case / case study:
    - “Regulated release pipeline for Temenos‑like core services”: design a pipeline where every production deployment requires approvals, change‑ticket linkage, automated tests, and a reversible rollout strategy.

***

## Automated provisioning & autoscaling (IaC + ASG + EKS) – 12 hours

- Theory (4h):
    - Infrastructure‑as‑Code concepts and benefits; introduction to AWS CloudFormation (stacks, templates, parameters) as a baseline.[1]
    - Automated environment creation: dev/test/prod stacks from the same templates; drift detection and controlled changes.
    - ASG basics and EKS cluster autoscaler concepts; relationship between pod requests/limits and node scaling.[14][2]

- Hands‑on (8h):
    - Write a CloudFormation template that provisions a VPC, subnets, security groups, an ASG, and an ALB for a sample service.
    - Parameterize the template for multiple environments (e.g., dev with small instances vs prod with larger instances) and deploy multiple stacks.
    - Create an EKS cluster using IaC, deploy the cluster‑autoscaler add‑on, and observe node scaling in response to varying pod loads.[15][1]

- Use case / case study:
    - “One‑click environment creation for a new country rollout”: define how a new country instance of a Temenos‑like platform can be created via IaC stack deployment, including compute, networking, and basic monitoring, then autoscaled as usage grows.

***

## Containerization & Orchestration (Kubernetes/EKS) – 16 hours

- Theory (5h):
    - Kubernetes basics: cluster architecture, control plane, nodes, pods, ReplicaSets, Deployments, Services, and Ingress.[1]
    - EKS‑specific components: managed control plane, node groups, Fargate profiles; how banks benefit from managed Kubernetes vs self‑managed clusters.[2]
    - ConfigMaps and Secrets for separating config from code and for secure secret distribution; RBAC basics.
    - Rolling updates, deployments, and basic health/readiness probes for zero‑downtime changes.

- Hands‑on (11h):
    - Deploy a simple banking microservice (e.g., customer‑profile API) to EKS with Deployment, Service, and Ingress.
    - Externalize configuration via ConfigMaps and Secrets, then rotate a secret without redeploying the entire stack.
    - Perform rolling updates with different strategies (e.g., update maxSurge/maxUnavailable) and observe behaviour.
    - Simulate node/pod failures, inspect events and logs, and verify self‑healing behaviour of Deployments.

- Use case / case study:
    - “Microservices platform for Temenos‑like workloads”: design an EKS‑based layout where multiple banking microservices run with shared base images, centralized logging, and per‑team namespaces, then implement a minimal slice of it in the lab.

***

## Monitoring & Logging – 8 hours

- Theory (3h):
    - CloudWatch metrics, logs, and alarms; golden signals (latency, traffic, errors, saturation) for banking APIs.[1]
    - Log Insights basics for querying structured logs; correlation of app logs and infrastructure metrics.
    - End‑to‑end tracing concepts using X‑Ray or equivalent: traces, segments, spans, and how tracing helps in debugging slow or failing requests.

- Hands‑on (5h):
    - Enable detailed metrics and logging for a sample EKS‑based service (e.g., via CloudWatch Container Insights or Fluent‑bit).
    - Create metric and log‑based alarms (high error rate, high latency, CPU spikes) and trigger them using a small load or error script.
    - Instrument a simple service for tracing and visualize a request path through multiple services to find a bottleneck.

- Use case / case study:
    - “Debugging intermittent failures in payments”: use logs, metrics, and traces to identify that a downstream fraud‑check service is intermittently timing out, then propose changes (timeouts/retries, scaling) and verify improvements.

***

## Cost Management & Optimization – 8 hours

- Theory (3h):
    - Cost drivers in cloud: compute, storage, data transfer, managed services; why cost transparency is critical in banking programs.
    - Identifying unused or underutilized resources; right‑sizing; reserved instances/savings plans at a conceptual level.[16]
    - S3 cost optimization levers: storage classes, lifecycle policies, versioning impact; Cost Explorer and Budgets basics.

- Hands‑on (5h):
    - Use Cost Explorer in a sandbox account to identify top cost contributors and idle resources; tag key workloads for showback/chargeback.
    - Implement S3 lifecycle rules to move old logs to cheaper tiers and delete obsolete versions; validate savings estimates.
    - Create Budgets with alerts for overall monthly spend and for a specific banking application environment.

- Use case / case study:
    - “Optimizing costs for non‑prod Temenos environments”: learners analyze a mock bill, find idle dev/test resources, propose right‑sizing or shutdown schedules, and implement at least one optimization via console or IaC.

***

Continuing the advanced journey with the remaining three topics and the same structure (≈30% theory, ≈70% hands‑on) and banking‑centric use cases.

***

## Serverless Architecture – 8 hours

- Theory (3h):
    - Lambda basics: execution model, cold starts, timeouts, and integration with API Gateway, SQS, SNS, EventBridge.[1]
    - Event‑driven design patterns: producers, consumers, fan‑out, and orchestration with Step Functions in regulated systems.
    - When serverless is helpful vs when containers/VMs are better; banking‑safe use cases where data residency, latency, and auditability are satisfied.

- Hands‑on (5h):
    - Create a Lambda function that processes mock “transaction” events from an SQS queue and writes sanitized results to DynamoDB or an S3 bucket.
    - Expose a simple API endpoint via API Gateway → Lambda for “mini‑statement” retrieval with proper input validation and logging.
    - Configure concurrency limits, retries, and DLQ for failed events; observe logs and metrics in CloudWatch for the function.

- Use case / case study:
    - “Lightweight services around core banking”: design a serverless‑only component for low‑risk use cases such as SMS alerts or statement generation exports, and justify why serverless is acceptable and efficient for that scenario in banking.

***

## High Availability & Disaster Recovery – 12 hours

- Theory (4h):
    - High availability concepts: multi‑AZ vs multi‑region; quorum, failover, and how HA differs from DR; RPO/RTO targets for critical vs non‑critical banking workloads.[1]
    - RDS internals at a high level: multi‑AZ deployments, read replicas, automatic failover, snapshots and backups.[1]
    - DR strategies: backup‑and‑restore, pilot light, warm standby, active‑active; trade‑offs in complexity, cost, and recovery time.

- Hands‑on (8h):
    - Deploy a multi‑AZ RDS instance for a “core accounts” database and connect an app tier to it; monitor failover events during planned maintenance.
    - Take manual and automated snapshots, restore to a new instance, and re‑point a sample application to validate recovery.
    - Build a basic multi‑AZ architecture for an EKS or EC2‑based banking front‑end with ALB, Auto Scaling, and RDS; simulate AZ degradation (e.g., shutting down resources in one AZ) and verify the system continues to serve traffic.

- Use case / case study:
    - “Regional outage playbook for internet banking”: define a DR strategy using warm‑standby or active‑active in a secondary region, including data replication, DNS failover, and runbook steps; run a tabletop exercise where the primary region is “lost” and teams explain how they would recover within agreed RTO/RPO.

***

