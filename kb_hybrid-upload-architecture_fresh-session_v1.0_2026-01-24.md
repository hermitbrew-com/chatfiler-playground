# Hybrid Upload API Architecture — Fresh Session KB

## Purpose
This document provides a clean, end-to-end overview of the Hybrid Upload API architecture for new engineers or fresh review sessions. It captures **current decisions**, **rationale**, and **recommended setup** without historical debugging context.

---

## System Overview
The Upload API enables a trusted GPT to upload markdown files to GitHub through a controlled backend service.

Key properties:
- **Caller**: Single trusted GPT (via GPT Actions)
- **Auth model**: Bearer token (service-to-service)
- **Traffic profile**: Predictable, low–moderate
- **Primary goal**: Reliable document upload, not public API exposure

---

## High-Level Architecture (Current)

```
Client (GPT Action)
        |
        v
NGINX Reverse Proxy (AWS EC2)
        |
        +--> EC2 Express Server (Cloud-native)
        |
        +--> On-Prem Express Server (Legacy / Specialized)
```

### Key Notes
- NGINX performs **routing only** (no auth, no business logic).
- Express servers perform **authentication, validation, logging, and GitHub integration**.
- On-prem and cloud backends coexist for gradual migration.

---

## Why No AWS Load Balancer (Yet)

At the current stage, AWS ALB is intentionally excluded.

### Reasons:
- Single trusted caller (GPT)
- No browser or public traffic
- No bursty or unpredictable load
- NGINX already provides routing, TLS, and basic load balancing
- Avoids unnecessary cost and operational complexity

NGINX is sufficient and easier to reason about at this scale.

---

## Load Balancer Strategy (Future-Ready)

When required (e.g., multi-AZ ingress, horizontal scale), an **AWS Application Load Balancer (ALB)** can be inserted *without application changes*:

```
Client
   |
   v
AWS ALB
   |
   v
NGINX Reverse Proxy
   |
   +--> EC2 Express
   |
   +--> On-Prem Express
```

ALB is preferred over NLB or GLB because:
- HTTP/HTTPS awareness
- Path-based routing
- Native health checks
- TLS termination

---

## Identity & Security Model

### What identifies the caller
- **Bearer token** (primary trust signal)
- Known endpoint structure
- Known request shape

### What does NOT matter
- Client IP address
- User device or browser
- Geolocation

GPT Actions call the API **from OpenAI infrastructure**, not from end-user devices.

IP addresses are treated as **connection metadata**, not identity.

---

## Logging & Observability

Each request records:
- `sourceIp`, `relayIp`, `ipChain` (for audit/debug only)
- Request timing and outcome
- Filename and operation type
- Environment (staging / prod)

Logs are written to:
- MongoDB (structured, queryable)
- Flat file log (lightweight trace)

---

## Recommended Current Setup (Summary)

- ✅ Use **NGINX-only routing and light load balancing**
- ✅ Keep Express stateless
- ✅ Use token-based authentication
- ✅ Avoid IP-based trust or analytics
- ✅ Design so ALB can be added later without refactor

---

## Status
- **Architecture**: Active
- **Audience**: Engineering / Internal
- **Confidence**: Production-ready for current scale

---

*This KB intentionally omits historical debugging details to remain concise and forward-facing.*
