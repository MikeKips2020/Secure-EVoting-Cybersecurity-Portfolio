# SOC Analyst Investigation Report

## Repeated Unauthorised Administrative Access Attempts

**Author:** Micah K. Yego  
**Qualification:** MSc Computer Science (Cybersecurity)  
**Project:** Secure Electronic Voting System  
**Investigation ID:** SOC-INV-001  
**Environment:** Staging — Academic Research Prototype  
**Investigation Type:** Authorised Security Testing  
**Classification:** Access Control / Security Monitoring  
**Status:** Completed — Controlled Testing Exercise

---

## 1. Executive Summary

This investigation examines security audit events generated during authorised access-control testing of a Secure Electronic Voting System developed as part of an MSc Computer Science (Cybersecurity) dissertation.

The objective was to assess whether the application could identify and record attempts by authenticated users to access administrative functions beyond their assigned permissions.

During testing, the application recorded multiple security warnings involving restricted administrative functions.

The audit logs demonstrated that the application generated security events when users attempted to access protected functions without the required permissions.

**Investigation outcome:** The reviewed events were confirmed as authorised security testing. The available evidence supports that access-control warnings were generated; it does not establish that an actual security breach occurred.

---

## 2. Investigation Objectives

The investigation aimed to:

1. Identify security-relevant events in application audit logs.
2. Examine repeated administrative access warnings.
3. Correlate events involving the same test account.
4. Assess the effectiveness of role-based access controls.
5. Distinguish authorised testing from potentially malicious activity.
6. Document findings using a structured SOC investigation approach.
7. Recommend improvements to security monitoring.

---

## 3. Environment and Technologies

| Component | Technology |
|---|---|
| Application | Secure Electronic Voting System |
| Programming language | Python |
| Framework | Flask |
| Database | PostgreSQL |
| Hosting | Render |
| Security monitoring | Application audit logs |
| Authentication | Session-based authentication |
| Authorisation | Role-based access control |
| Investigation environment | Staging |
| Test classification | Authorised security testing |

The investigation used application-generated audit records rather than a commercial Security Information and Event Management (SIEM) platform.

---

## 4. Initial Alert Identification

The application audit dashboard recorded repeated security warnings associated with attempts to access restricted administrative functions.

Examples included:

- `UNAUTHORIZED_SUPER_ADMIN_ACCESS`
- `UNAUTHORIZED_ADMIN_ACCESS`
- `UNAUTHORIZED_CANDIDATE_CHANGE`
- `ADMIN_VOTE_ACCESS_BLOCKED`

These events indicated that the application had identified requests involving restricted functions.

The repeated warnings were selected for investigation because multiple events were associated with the same test account.

---

## 5. Evidence Collection

Evidence was collected from the application's staging security audit dashboard.

The following fields were available:

- Event timestamp in UTC
- Event type
- Severity classification
- Internal user identifier
- Event details
- Attempted administrative function

### Selected Audit Events

| Date (UTC) | Event | Observed activity |
|---|---|---|
| 23 October 2026 | UNAUTHORIZED_SUPER_ADMIN_ACCESS | Attempted access to restricted administrator dashboard |
| 23 October 2026 | UNAUTHORIZED_SUPER_ADMIN_ACCESS | Attempted access to voter status controls |
| 24 October 2026 | UNAUTHORIZED_CANDIDATE_CHANGE | Blocked candidate modification attempt |
| 24 October 2026 | UNAUTHORIZED_SUPER_ADMIN_ACCESS | Attempted access to administrator management |
| 24 October 2026 | UNAUTHORIZED_SUPER_ADMIN_ACCESS | Attempted access to voter editing functions |

The public report omits account identifiers and other unnecessary personal information.

---

## 6. Event Correlation and Analysis

The reviewed events shared several characteristics.

**Common account:** Multiple warnings were associated with the same authorised test account.

**Restricted functions:** The attempted operations involved administrator management, candidate modification and voter administration.

**Repeated activity:** Related warnings appeared across multiple testing sessions.

**Security response:** The application recorded access-control warnings, including events explicitly identifying blocked operations.

### Analyst Interpretation

Repeated attempts to access restricted administrative functions can warrant investigation because they may indicate:

- Misconfigured user permissions.
- Unauthorised attempts to obtain administrative access.
- Application testing.
- Users attempting functions outside their assigned roles.

In this case, the activity was confirmed as part of authorised security testing.

Consequently, the events were classified as **expected test activity**, rather than evidence of a real intrusion.

---

## 7. Security-Control Assessment

The investigation examined the application's role-based access-control monitoring.

### Observed Findings

**Finding 1 — Access-control event generation**

The application generated audit events when restricted administrative functions were accessed without the required permissions.

**Finding 2 — Event severity classification**

The relevant access-control events were classified as warnings.

**Finding 3 — Audit traceability**

The audit records contained timestamps, event types, account identifiers and details of the attempted operations.

**Finding 4 — Repeated-event correlation**

The available records allowed related events involving the same test account to be identified.

**Finding 5 — Investigation context**

Confirmation of authorised testing was essential to interpreting the events accurately.

### Assessment Limitations

The available screenshots do not independently establish that every attempted operation was blocked at the database level.

Additional testing would be necessary to confirm that no unauthorised changes occurred across all affected functions.

---

## 8. Incident Classification

| Attribute | Assessment |
|---|---|
| Initial alert severity | Warning |
| Investigation priority | Low, following confirmation of authorised testing |
| Activity classification | Authorised security testing |
| Confirmed compromise | No compromise established by the reviewed evidence |
| Security-control observation | Access-control warnings generated |
| Investigation status | Closed — Expected Testing Activity |

The classification was based on the audit records and confirmation that the activity was authorised.

---

## 9. Recommendations

The following improvements would strengthen future security monitoring:

1. **Centralised logging:** Forward application security events to a dedicated log-management or SIEM platform.

2. **Alert correlation:** Generate alerts when repeated access-control violations occur within a defined period.

3. **Structured audit records:** Use consistent event fields to support automated analysis.

4. **Access-control verification:** Test that denied requests cannot modify protected database records.

5. **Security monitoring dashboards:** Introduce visual summaries of event frequency, severity and affected functions.

6. **Investigation procedures:** Maintain documented processes for reviewing and classifying security alerts.

7. **Log protection:** Apply appropriate access restrictions and retention controls to audit records.

---

## 10. Cybersecurity Skills Demonstrated

This investigation demonstrates practical experience in:

- Security event monitoring.
- Alert identification and triage.
- Audit-log analysis.
- Event correlation.
- Role-based access-control assessment.
- Evidence interpretation.
- Security incident classification.
- Technical investigation reporting.
- Security-control improvement recommendations.

These skills are relevant to entry-level SOC Analyst and Cybersecurity Analyst positions.

---

## 11. Conclusion

The investigation demonstrated how application security audit logs can support the identification and analysis of access-control events.

The reviewed warnings were associated with authorised testing of restricted administrative functions.

The exercise provided practical experience in interpreting security alerts, correlating related events and distinguishing expected testing activity from potential security incidents.

The findings also identified opportunities to improve monitoring through centralised logging, automated alert correlation and additional access-control verification.

**Final Classification: Authorised Security Testing — No Confirmed Security Incident**

---

## 12. Project Disclaimer

This investigation was conducted within an academic cybersecurity research prototype.

The documented activity was authorised testing, not a real cyberattack.

The report demonstrates selected security monitoring and investigation techniques. It does not represent an independent security certification or comprehensive penetration test.

---

**Prepared by:** Micah K. Yego  
**MSc Computer Science (Cybersecurity)**  
**Cybersecurity Portfolio — SOC Analyst Investigation**
