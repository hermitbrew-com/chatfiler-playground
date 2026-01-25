# Upload API – IP Handling Summary

## Context
The Upload API is primarily called by a single, trusted GPT integration rather than by the general public. During debugging, significant effort was spent validating real client IP attribution through NGINX and Express.

## Key Findings
- GPT-originated traffic does **not** represent end-user IPs.
- Even with perfect proxy configuration, only shared OpenAI egress IPs are visible.
- IP-based identity is therefore **not a meaningful security or analytics signal** for this API.

## Current Architecture (Validated)
- **NGINX relay** correctly resolves and forwards client IPs using `real_ip_header` and trusted CIDRs.
- **Application logic** now deterministically resolves:
  - `sourceIp` (client or egress)
  - `relayIp` (NGINX / ingress hop)
  - `ipChain` (forensic trace)
- Logging is consistent across MongoDB and flat-file logs.

## Security Model (Effective)
Primary trust and security controls are:
- Bearer token authentication
- Controlled request shape and endpoints
- Known user agent (GPT)
- Non-discoverable API surface

IP addresses are treated as **connection metadata**, not identity.

## Conclusion
The IP-handling work is correct, safe, and future-proof, but **not critical** for current GPT-only usage. The system is production-ready without further IP-level refinement.

---
**Status**: Active
**Audience**: Internal / Engineering
