# Mapping SQL Queries to GRC / Risk Frameworks

This document maps each SQL query from `SECURITY_INVESTIGATION_QUERIES.md` to principles and clauses from major GRC / risk frameworks (e.g., ISO 27001, NIS2, DORA, GDPR). The goal is to show how simple SQL patterns can underpin **risk‑logic and control‑design**.

---

## 1. After‑hours failed login attempts

**Query**:
```sql
SELECT *
FROM log_in_attempts
WHERE login_time > '18:00'
  AND success = 0;
```

**Relevant frameworks**:

- **ISO 27001 A.9 – Access Control**  
  - A.9.4.1: Monitor user access to detect unauthorized activity.  
  - This query supports **monitoring and logging** of failed logins outside business hours.

- **GDPR Art. 32 – Security of Processing**  
  - Requires appropriate technical measures to detect and respond to security incidents.  
  - After‑hours failed logins are a classic **indicator** for incident response.

- **NIS2 / DORA – ICT Risk Management**  
  - Both require logging and monitoring of access events to detect and respond to incidents.  
  - This query is a **basic evidence‑gathering** step for incident triage.

---

## 2. Login attempts on specific dates

**Query**:
```sql
SELECT *
FROM log_in_attempts
WHERE login_date = '2022-05-09'
   OR login_date = '2022-05-08';
```

**Relevant frameworks**:

- **GDPR Art. 33–34 – Breach Notification**  
  - Requires documentation of **when and how** a breach occurred.  
  - This query helps **bound the incident timeline** for regulatory reporting.

- **DORA – Incident Reporting**  
  - Requires incident timelines and evidence.  
  - This is a **basic SQL‑based evidence‑gathering** step.

- **ISO 27001 A.16 – Information Security Incident Management**  
  - A.16.1.1–16.1.6: Incident detection, analysis, and reporting.  
  - This query supports **incident analysis** by narrowing data to specific dates.
  ## 3. Login attempts outside Mexico

**Query**:
```sql
SELECT *
FROM log_in_attempts
WHERE NOT country LIKE 'MEX%';
```

**Relevant frameworks**:

- **DORA / NIS2 – ICT Risk Management**  
  - Both emphasize **threat modeling** and **risk‑based controls**.  
  - This query reflects a **geo‑filtering** assumption (e.g., “no threat from Mexico”).

- **ISO 27001 A.15 – Supplier Relationships**  
  - A.15.1.1–15.1.3: Risk‑based management of suppliers and third parties.  
  - This pattern can be extended to **exclude** known‑safe regions or partners.

- **GRC / Risk‑Logic**  
  - This is a clean example of **positive and negative rules** (inclusion/exclusion) in risk‑logic.

---

## 4. Employees in Marketing (East building)

**Query**:
```sql
SELECT *
FROM employees
WHERE department = 'Marketing'
  AND office LIKE 'East%';
```

**Relevant frameworks**:

- **ISO 27001 A.5 – Information Security Policies**  
  - A.5.1.1: Management directive on information security.  
  - This query supports **control scoping**: applying a policy to a specific department and location.

- **ISO 27001 A.9 – Access Control**  
  - A.9.1.1–9.1.2: Define access‑control policy and manage user access.  
  - This mirrors how you’d **scope access‑control rules** to specific groups.

- **Change‑Management / Risk‑Register**  
  - This is the **SQL equivalent** of “apply control X to Marketing department machines in the East building only.”

---

## 5. Employees in Finance or Sales

**Query**:
```sql
SELECT *
FROM employees
WHERE department = 'Sales'
   OR department = 'Finance';
```

**Relevant frameworks**:

- **ISO 27001 A.5 – Information Security Policies**  
  - A.5.1.1: Management directive on information security.  
  - This query supports **multi‑department controls** (e.g., MFA rollout, password policy update).

- **GRC / Risk‑Logic**  
  - This is a classic **multi‑department applicability** rule, often seen in GRC documents.
  ## 6. All employees not in IT

**Query**:
```sql
SELECT *
FROM employees
WHERE NOT department = 'Information Technology';
```

**Relevant frameworks**:

- **ISO 27001 A.5 – Information Security Policies**  
  - A.5.1.1: Management directive on information security.  
  - This supports **control applicability clauses** that exclude specific groups.

- **Change‑Management / Risk‑Register**  
  - This is the **SQL equivalent** of “apply this control to all departments except IT.”

---

## 7. General Observations

- **SQL as a GRC tool**: These queries show how **simple SQL** can underpin **risk‑logic**, incident triage, and control‑design.  
- **Risk‑Logic and Frameworks**: The same patterns (`AND`, `OR`, `NOT`, `LIKE`) map directly to **inclusion/exclusion rules** in policies and risk registers.  
- **Audit‑Ready**: Each query is **clean, well‑scoped, and easy to document**, which is important for **auditors** or **non‑technical stakeholders**.

  
