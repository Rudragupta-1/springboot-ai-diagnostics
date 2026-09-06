# Spring Boot AI Diagnostics

An **Agentic AI-powered diagnostic system for Spring Boot applications** that uses multiple specialized AI agents to investigate application failures, analyze evidence, collaborate on findings, identify probable root causes, and generate a consolidated diagnostic report.

## Overview

Debugging production applications often requires developers to investigate multiple sources of information:

* Application logs
* Database queries
* Application code
* JVM and system metrics
* API failures
* Configuration
* Infrastructure health

This project aims to automate that investigation using an **orchestrated multi-agent architecture**.

Instead of relying on a single AI agent, the system uses specialized agents, where each agent focuses on a particular diagnostic area.

The agents' findings are then combined to produce a **consolidated root-cause analysis and recommendation report**, which can be delivered to the developer via email.

---

## 🧠 Architecture

```text
                         ┌──────────────────────┐
                         │      Developer       │
                         └──────────┬───────────┘
                                    │
                                    │ Start Diagnosis
                                    ▼
                         ┌──────────────────────┐
                         │   Spring Boot API    │
                         │                      │
                         │    /diagnose         │
                         └──────────┬───────────┘
                                    │
                                    ▼
                         ┌──────────────────────┐
                         │   Agent Orchestrator │
                         └──────────┬───────────┘
                                    │
              ┌─────────────────────┼─────────────────────┐
              │                     │                     │
              ▼                     ▼                     ▼
       ┌─────────────┐       ┌─────────────┐       ┌─────────────┐
       │  Log Agent  │       │   DB Agent  │       │  Code Agent │
       └──────┬──────┘       └──────┬──────┘       └──────┬──────┘
              │                     │                     │
              │                     │                     │
              └─────────────────────┼─────────────────────┘
                                    │
                                    ▼
                         ┌──────────────────────┐
                         │  Reasoning /        │
                         │  Evidence Analysis  │
                         └──────────┬───────────┘
                                    │
                                    ▼
                         ┌──────────────────────┐
                         │   Report Generator   │
                         └──────────┬───────────┘
                                    │
                                    ▼
                         ┌──────────────────────┐
                         │    Email Service     │
                         └──────────┬───────────┘
                                    │
                                    ▼
                              Developer
```

---

## 🤖 Specialized Agents

### 1. Log Analysis Agent

Responsible for analyzing application logs.

It can identify:

* Exceptions
* Stack traces
* Error patterns
* HTTP errors
* Timeouts
* Repeated failures
* Anomalous behavior

Example finding:

```text
PaymentService is generating repeated connection timeout
exceptions during checkout requests.
```

---

### 2. Database Agent

Responsible for investigating database-related problems.

It can analyze:

* Slow queries
* Failed queries
* Connection pool exhaustion
* Deadlocks
* Transaction failures
* Potential N+1 queries
* Missing indexes
* Database latency

Example finding:

```text
Query findOrdersByCustomer is taking significantly longer
than normal and may require index optimization.
```

---

### 3. Code Analysis Agent

Responsible for analyzing relevant application code.

It can investigate:

* Stack-trace locations
* Service-layer logic
* Repository usage
* Exception handling
* Configuration
* Potential N+1 queries
* Resource leaks
* Suspicious code patterns

Example finding:

```text
OrderService performs database access inside a loop,
indicating a possible N+1 query problem.
```

---

### 4. Metrics / JVM Agent

Responsible for analyzing application and JVM health.

Potential signals include:

* CPU usage
* Memory usage
* Heap utilization
* Garbage collection
* Thread count
* HTTP latency
* Throughput
* Connection pools

Example finding:

```text
JVM heap utilization reached 94% shortly before
application response latency increased.
```

---

### 5. Report Agent

The Report Agent combines findings from the other agents and generates:

* Overall application health
* Detected problems
* Evidence
* Root cause
* Impact
* Confidence
* Recommendations
* Priority/severity

Example:

```text
Root Cause:
HTTP connection pool exhaustion.

Confidence:
91%

Impact:
Checkout requests experienced increased latency
and timeout failures.

Recommendation:
Review HTTP connection pool configuration and
investigate downstream PaymentService latency.
```

---

## 🔄 Diagnostic Flow

```text
1. Developer starts diagnosis
              ↓
2. System collects diagnostic data
              ↓
3. Orchestrator assigns investigation tasks
              ↓
4. Specialized agents analyze their domains
              ↓
5. Agents produce structured findings
              ↓
6. Findings are correlated
              ↓
7. Conflicting evidence is investigated
              ↓
8. Root cause is determined
              ↓
9. Report Agent generates final report
              ↓
10. Report is emailed to developer
```

---

## 🏗️ Planned Technology Stack

### Backend

* Java
* Spring Boot
* Spring AI
* Spring Data JPA
* Spring Actuator

### AI

* Large Language Model
* Multi-agent architecture
* Agent orchestration
* Tool calling
* Structured AI responses

### Database

* PostgreSQL

### Messaging

Potentially:

* Kafka
* RabbitMQ

### Observability

Potentially:

* Micrometer
* Prometheus
* Grafana
* Spring Boot Actuator

### Infrastructure

* Docker
* Docker Compose

### Reporting

* Email
* HTML diagnostic reports

---

## 📁 Planned Project Structure

```text
springboot-ai-diagnostics/
│
├── src/
│   ├── main/
│   │   ├── java/
│   │   │   └── com/
│   │   │       └── diagnostics/
│   │   │           ├── controller/
│   │   │           ├── service/
│   │   │           ├── agent/
│   │   │           │   ├── log/
│   │   │           │   ├── database/
│   │   │           │   ├── code/
│   │   │           │   ├── metrics/
│   │   │           │   └── report/
│   │   │           ├── orchestrator/
│   │   │           ├── model/
│   │   │           ├── repository/
│   │   │           ├── config/
│   │   │           └── exception/
│   │   │
│   │   └── resources/
│   │       ├── application.yml
│   │       └── prompts/
│   │
│   └── test/
│
├── docker/
│
├── docs/
│
├── .gitignore
├── docker-compose.yml
├── pom.xml
└── README.md
```

---

## 🎯 Project Goals

The project is intended to demonstrate how **Agentic AI can be applied to real-world backend diagnostics**.

### Primary Goals

* Automate Spring Boot application diagnosis
* Use specialized AI agents
* Allow agents to work with different diagnostic tools
* Correlate findings from multiple sources
* Identify probable root causes
* Generate actionable recommendations
* Automatically deliver diagnostic reports

### Engineering Goals

* Clean Spring Boot architecture
* Modular agent design
* Structured communication between agents
* Fault-tolerant processing
* Asynchronous processing where appropriate
* Persistent diagnosis history
* Observability
* Production-oriented design

---

## 🔮 Future Improvements

Potential future capabilities:

* Automatic anomaly detection
* Historical incident comparison
* RAG over previous incidents
* Automatic remediation suggestions
* Safe automated remediation
* Kubernetes diagnostics
* Distributed tracing analysis
* CI/CD integration
* Slack/Teams notifications
* Incident severity prediction
* Learning from previous diagnostic reports

---

## 🚧 Project Status

**Currently under development.**

The initial version will focus on establishing the core diagnostic pipeline and agent orchestration architecture.

---

## 📜 License

License will be added as the project evolves.
