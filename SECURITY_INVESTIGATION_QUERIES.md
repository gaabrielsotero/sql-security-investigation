# SQL Security Investigation Queries (GRC‑oriented)

This document shows the SQL queries used to investigate suspicious login attempts and employee machines. Each query is framed as a **risk‑oriented task**, not a generic course exercise.

---

## 1. After‑hours failed login attempts

**Objective**: Identify possible brute‑force or credential‑stuffing attempts outside business hours.

```sql
SELECT *
FROM log_in_attempts
WHERE login_time > '18:00'
  AND success = 0;
```

**Explanation**:  
- Filters `log_in_attempts` for **login_time after 18:00** and **failed attempts** (`success = 0`).  
- In a GRC context, this supports **incident triage** and **access‑monitoring controls** (e.g., ISO 27001 A.9 – Access Control).  
- The `AND` operator ensures both conditions must be true, reflecting a strict risk‑logic rule.

**Risk‑oriented framing**:  
- This query is analogous to “flag all failed logins after standard business hours” in a security policy.

---

## 2. Login attempts on specific dates

**Objective**: Bound events to a specific incident window (e.g., the day of an alert plus the day before).

```sql
SELECT *
FROM log_in_attempts
WHERE login_date = '2022-05-09'
   OR login_date = '2022-05-08';
```

**Explanation**:  
- Uses `OR` to include records from **two specific dates**, which is common when defining an incident timeline.  
- In a GRC context, this mirrors how you’d define **“relevant data for a breach investigation”** (e.g., GDPR 33–34, DORA, NIS2 incident reporting).

**Risk‑oriented framing**:  
- This is the SQL equivalent of “collect all access events on the day of the incident and the day before” for regulatory or audit review.

---

## 3. Login attempts outside Mexico

**Objective**: Exclude known benign traffic from analysis when the incident is confirmed not to originate in Mexico.

```sql
SELECT *
FROM log_in_attempts
WHERE NOT country LIKE 'MEX%';
```

**Explanation**:  
- Uses `LIKE 'MEX%'` to match country codes starting with `MEX` (e.g., `MEX`, `MEXICO`) and `NOT` to exclude them.  
- Reflects a **geo‑filtering** or threat‑modeling assumption (e.g., “no threat from Mexico”).

**Risk‑oriented framing**:  
- This maps to a **threat model** or **policy rule** that excludes traffic from a specific region, aligning with DORA / NIS2 ICT‑risk‑management principles.

---

## 4. Employees in Marketing (East building)

**Objective**: Scope security updates to Marketing employees in the East building.

```sql
SELECT *
FROM employees
WHERE department = 'Marketing'
  AND office LIKE 'East%';
```

**Explanation**:  
- Uses `AND` to combine two conditions: specific **department** and **office pattern**.  
- The `LIKE 'East%'` allows matching any office code starting with `East` (e.g., `East‑170`, `East‑320`), which is realistic for large organizations.

**Risk‑oriented framing**:  
- This is analogous to “apply control X to Marketing department machines in the East building only,” which is typical in control scoping and change‑management.

---

## 5. Employees in Finance or Sales

**Objective**: Extend a control or update to multiple business units.

```sql
SELECT *
FROM employees
WHERE department = 'Sales'
   OR department = 'Finance';
```

**Explanation**:  
- Uses `OR` to cover multiple departments, which is common when a policy applies to more than one business unit.  
- Reflects a **multi‑department control** scenario (e.g., MFA rollout, password policy update).

**Risk‑oriented framing**:  
- This maps directly to “this control applies to Sales and Finance departments” in a GRC document or risk register.

---

## 6. All employees not in IT

**Objective**: Exclude IT machines that are already covered by a separate change window or baseline.

```sql
SELECT *
FROM employees
WHERE NOT department = 'Information Technology';
```

**Explanation**:  
- Uses `NOT` to exclude a specific department, which is useful when IT is managed under a different policy.  
- This pattern is common in change‑management or risk‑applicability rules.

**Risk‑oriented framing**:  
- This mirrors a **control applicability** clause that explicitly excludes a group (e.g., “all departments except IT”).

---

## 7. Notes on Risk‑Logic and SQL

- **AND / OR / NOT**: Directly mirror **inclusion/exclusion rules** you’d see in policies and risk registers.  
- **LIKE with %**: Useful for pattern‑matching in fields like `office`, `country`, or `application_name`.  
- **Scoped WHERE clauses**: Help you define **risk‑relevant subsets** of data for incident triage, audits, or change‑management.

