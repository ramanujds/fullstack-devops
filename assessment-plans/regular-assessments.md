## 1. Pre‑ and Post‑Training Assessments

**Pre‑training baseline (before Day 1)**
- 20–25 question online quiz covering Linux, networking, Git, cloud basics, CI/CD, containers, and security.
- One 30‑minute practical task where participants:
    - Clone a repository.
    - Modify a simple configuration or script and commit/push changes.
    - Build and run a small containerized app and verify it via HTTP.
- Output: baseline scores and a short summary of strengths/gaps per group.

**Post‑training assessment (final week)**
- Quiz with similar structure and difficulty to the baseline, focused on topics actually covered.
- Short practical task that validates end‑to‑end competence (e.g., adjust a pipeline or fix a broken deployment).
- Output: comparison of pre vs post results, with percentage improvement and commentary.

***

## 2. Module‑Level Practical Evaluations

At the end of each major block (e.g., Linux & scripting, Git & CI/CD, Cloud/IAM, Containers & EKS, Security & Monitoring), participants complete a short graded lab.

**Examples**
- Linux/scripting: write a health‑check script and troubleshoot a failing service.
- Git/CI/CD: implement a small pipeline that builds and tests an application.
- Cloud/IAM: create a least‑privilege role and secure a sample resource.
- Containers/EKS: deploy a simple service to Kubernetes with ConfigMaps and Secrets.
- Security/Monitoring: configure basic metrics, alarms, and log queries for an app.

**Rubric (shared with you and learners)**  
Each lab is scored on a simple 0–5 scale across:
- Correctness (meets functional requirements).
- Quality (readable, maintainable, follows best practices).
- Automation (uses scripts/pipelines instead of manual steps).
- Security/Resilience (where relevant: least privilege, safe defaults, basic error handling).

Aggregated lab results will be provided as a summary per participant and per cohort.

***

## 3. Capstone Project Evaluation

The final capstone is an end‑to‑end 3‑tier, banking‑style application running on cloud infrastructure, with CI/CD, security controls, logging, and monitoring.

**Assessment dimensions**
- Architecture & Security
    - Sound VPC and networking layout, correct use of subnets and security groups.
    - Proper use of IAM roles, Secrets, and encryption where applicable.
- CI/CD & Automation
    - Multi‑stage pipeline implemented (build, test, image build, deploy, rollback).
    - Minimal manual intervention; clear rollback or recovery mechanism.
- Operations & Reliability
    - Logs and metrics available and usable for debugging.
    - Team can diagnose and fix at least one seeded issue (e.g., misconfig, failing pod).
- Documentation & Presentation
    - Architecture diagram and brief runbook (deploy/rollback, basic troubleshooting).
    - 10–15 minute demo showing the system working, plus explanation of design decisions.

Each capstone team receives a rubric‑based score and qualitative feedback. A consolidated report will highlight overall cohort capability and any participants who stand out as advanced.

***

## 4. Peer Review and Collaboration

To mirror real DevOps ways of working, participants will:
- Conduct at least one structured peer code review (pull/merge request) per module.
- Use a simple checklist (clarity, testing, security, maintainability).

Trainers will sample and comment on a subset of reviews to ensure quality. A brief summary of collaboration and review skills will be included in the final report.

***

## 5. Participation, Reflection, and Final Feedback

Throughout the course we will track:
- Attendance and active participation in discussions, labs, and incident simulations.
- Two brief reflection surveys (mid‑program and end‑program) where participants rate their confidence across key skills and describe how they expect to apply them.

You will receive:
- Pre/post quantitative results.
- Lab and capstone scores with rubrics.
- A short narrative summary of strengths, gaps, and recommended next steps for future training or on‑the‑job reinforcement.