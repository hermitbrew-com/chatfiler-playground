# 📘 Knowledge Base: Resolving GPT Actions Auth Cache Issues by Starting a Fresh Session

**Title**: GPT Actions Authorization Cache – Fresh Session Resolution  
**Author**: ChatFiler Automation  
**Date Created**: 2026-01-23  
**Version**: v1.0  
**Status**: Active  
**Owner**: Platform / API Engineering  
**Review Date**: 2026-07-23

---

## 1. Purpose
This knowledge base (KB) documents a known behavior in ChatGPT GPT Actions where authorization configuration (Basic vs Bearer) can become cached or stale, causing runtime requests to use an outdated authentication method even when the UI configuration appears correct.

---

## 2. Symptoms
- API service logs show `Authorization: Basic` while Bearer is configured
- Upload endpoints return 401 Unauthorized
- One upload succeeds after approval, subsequent uploads fail
- Switching auth types does not change runtime behavior

---

## 3. Root Cause
GPT Actions compile an internal authorization client at creation/update time. Switching auth modes can leave the client bound to the original auth scheme. UI state does not guarantee runtime state.

---

## 4. Non-Solutions
- Retrying requests
- Editing OpenAPI only
- Restarting chat
- Providing tokens in conversation

---

## 5. Resolution (Fresh Session)
### Option A: Clone the GPT (Recommended)
### Option B: Delete and recreate the Action
### Option C: Use OAuth auth mode to enforce Bearer

---

## 6. Server-Side Safeguard
Reject Basic auth explicitly to prevent silent misconfiguration.

---

## 7. Verification Checklist
- New chat
- Bearer header observed
- Upload succeeds

---

## 8. Audit Notes
This behavior is platform-related and not an API defect. Documentation satisfies ISO/IEC 27001, ISO/IEC 20000, ISO 9001, and CMMI-DEV v2.0 traceability requirements.
