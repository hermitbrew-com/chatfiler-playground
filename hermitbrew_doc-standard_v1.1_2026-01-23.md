# HermitBrew Documentation Standard v1.1

**Author:** ChatFiler GPT-5  
**Date Created:** 2026-01-23  
**Version:** v1.1  
**Status:** Active  
**Owner:** Documentation Lead (HermitBrew)  
**Review Date:** 2026-06-23  

---

## 📘 Scope
Applies to all HermitBrew technical documentation (SOPs, KBs, Runbooks, Change Records, and Incident Reports). Ensures consistency, audit-readiness, and compliance with ISO/IEC 20000, 27001, and 9001.

---

## 🧱 File Naming Convention
```
{category}_{keywords}_v{major.minor}_{yyyy-mm-dd}_{hhmm}.md
```
Example: `kb_microcluster-arm-x86-wireguard_v1.7_2025-05-15_0000.md`

---

## 🧠 Required Metadata Block
Each document must begin with:
```markdown
**Title**: [Descriptive Title]  
**Author**: [Full Name]  
**Date Created**: YYYY-MM-DD  
**Version**: vX.Y  
**Status**: [Draft | Active | Deprecated]  
**Owner**: [Person or Team]  
**Review Date**: YYYY-MM-DD
```

---

## 🗂 Document Categories
| Type | Purpose | Examples |
|------|----------|-----------|
| SOP | Repeatable operational procedures | Provision VPN node |
| Runbook | System-specific workflows | Restore rclone backup |
| Incident Report | Postmortem RCA | API outage 2025-11-05 |
| Change Log | Config/deployment record | WireGuard IP reassignment |
| Risk Log | Known risks & mitigations | Node overheating CI-x86-01 |
| Knowledge Base | Architecture & reference | Hybrid ARM+x86 layout |

---

## 🔒 Compliance Requirements
- Traceability: All versions and edits logged.
- Responsibility: Each doc must have an owner.
- Versioning: Use semantic versioning (vX.Y).
- Access Control: Restrict sensitive SOPs.
- Backup: Sync to Git and offsite weekly.

---

## 🗓 Versioning & Changelog
```markdown
### 📝 Changelog
- v1.1 (2026-01-23): Standard updated for AI-assisted uploads.
- v1.0 (2025-12-06): Initial version.
```

---

**Commit Summary:** Updated HermitBrew documentation standard for AI-assisted uploads, clarified version control rules, and ensured ISO compliance alignment.