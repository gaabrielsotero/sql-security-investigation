# SQL‑Based Security Investigation for GRC & IT Risk

This repository demonstrates how **SQL** can be used in a **security and risk context** to filter, investigate, and triage login‑attempt data and employee records. The queries simulate real‑world GRC / IT‑Risk tasks such as:

- Incident triage and access‑control review  
- Scoping security updates to specific departments and locations  
- Framing evidence‑gathering steps for auditors or non‑technical stakeholders

This is not a generic course exercise; it’s a **risk‑oriented lab** that mirrors how GRC / IT‑Risk analysts use SQL to turn raw logs into **actionable risk information**.

---

## Overview

In this project, I:

- Analyzed `log_in_attempts` to identify suspicious after‑hours and out‑of‑country login activity.  
- Filtered `employees` to scope security updates to specific departments and office buildings.  
- Used `AND`, `OR`, `NOT`, and `LIKE` patterns that mirror **risk‑logic inclusion/exclusion rules**.

This helps show recruiters that I can:

- slice and filter data for **incident triage**,  
- map SQL conditions to **control scoping** and **risk‑logic** (e.g., ISO 27001 A.9, NIS2, DORA),  
- document evidence‑gathering in a clean, auditable way.

---

## What You’ll Find Here

- `SECURITY_INVESTIGATION_QUERIES.md`: SQL queries with explanations.  
- `RISK_MAPPING.md`: mapping of each query to risk‑management and compliance principles (e.g., ISO 27001, NIS2, DORA).  
- `data_samples/`: lightweight CSV examples of `log_in_attempts` and `employees` schemas.

These artifacts are meant to be:

- **professionally written**,  
- **framework‑aware**,  
- and easy to reference in your CV, LinkedIn, or internal interviews.

