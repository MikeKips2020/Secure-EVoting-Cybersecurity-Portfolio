# Secure Electronic Voting System — Security Testing and Evaluation Report

**Author:** Micah K. Yego  
**Qualification:** MSc Computer Science (Cybersecurity)  
**Project:** Secure Electronic Voting System  
**Document Type:** Security Testing and Evaluation Report  
**Classification:** Public Technical Portfolio Documentation

---

## 1. Executive Summary

This report documents selected security tests conducted during the development and evaluation of a Secure Electronic Voting System.

The application was developed as an MSc Computer Science (Cybersecurity) research project to investigate how authentication, cryptography, access controls and integrity verification can contribute to the security of electronic voting systems.

The security evaluation focused on five areas:

1. Duplicate-voting prevention.
2. Concurrent ballot submission handling.
3. SHA-256 hash-chain integrity verification.
4. Detection of unauthorised ballot modifications.
5. Integrity reporting through the election results interface.

The selected tests produced successful outcomes in the local testing environment.

These results provide evidence of the tested controls under the conditions examined. They do not establish that the complete application is free from vulnerabilities or suitable for real-world elections.

---

## 2. Security Testing Objectives

The security testing activities were designed to:

- Evaluate selected application security controls.
- Assess protection against duplicate ballot submissions.
- Examine the handling of simultaneous voting requests.
- Verify the integrity of recorded ballot data.
- Evaluate the detection of deliberately modified records.
- Confirm that integrity failures are communicated through the application interface.
- Identify limitations and opportunities for further security improvements.

---

## 3. Testing Environment

The application was developed using the following technologies.

| Component | Technology |
|---|---|
| Programming language | Python |
| Application framework | Flask |
| Database | PostgreSQL |
| Ballot encryption | Fernet authenticated encryption |
| Integrity mechanism | SHA-256 hash chaining |
| Authentication | Session-based authentication |
| Access control | Role-based access control |
| Deployment platform | Render |
| Version control | GitHub |

Security tests were performed using a local testing environment.

The project also used separate staging and production deployments during development.

**Testing limitation:** The successful local test results documented below should not be interpreted as proof that every security control has been independently verified in the production environment.

---

## 4. Security Test Cases

### Test 1 — Duplicate-Voting Prevention

**Objective**

Determine whether the application prevents a voter from submitting a duplicate ballot.

**Security risk**

Without effective duplicate-voting controls, an attacker or user might attempt to submit multiple ballots for the same electoral contest.

**Testing approach**

Controlled repeated voting attempts were performed to evaluate the application's duplicate-voting prevention mechanisms.

**Expected outcome**

The application should reject duplicate submissions and prevent unauthorised additional ballots from being recorded.

**Observed outcome**

The duplicate-voting prevention test passed in local testing.

**Result: PASS**

**Security significance**

This test provides evidence that the application's duplicate-voting controls operated as expected under the tested conditions.

---

### Test 2 — Concurrent Ballot Submission

**Objective**

Evaluate the application's behaviour when voting requests are submitted concurrently.

**Security risk**

Simultaneous requests may expose race conditions that could undermine duplicate-voting prevention.

**Testing approach**

Controlled concurrent submission tests were conducted against the local application.

**Expected outcome**

Concurrent requests should not result in unauthorised duplicate ballot recording.

**Observed outcome**

The concurrent submission test passed in local testing.

**Result: PASS**

**Security significance**

The result provides evidence that the tested voting workflow handled the simulated concurrent submissions without the duplicate-voting failure being investigated.

Further load and concurrency testing would be required to evaluate behaviour under larger workloads.

---

### Test 3 — SHA-256 Hash-Chain Verification

**Objective**

Evaluate whether the application can verify the integrity of recorded ballot data.

**Security risk**

Unauthorised changes to stored ballot records may undermine confidence in election results.

**Testing approach**

The application's integrity verification mechanism was evaluated using locally recorded test ballots.

The system uses SHA-256 hash chaining to support the detection of changes to protected ballot records.

**Expected outcome**

The verification process should report valid integrity when the tested ballot records remain consistent with their stored integrity information.

**Observed outcome**

The hash-chain verification test passed in local testing.

**Result: PASS**

**Security significance**

This demonstrates the operation of the application's integrity-checking mechanism under the tested conditions.

**Limitation**

A hash chain alone does not prevent a sufficiently privileged attacker from rewriting records and recomputing the chain. Stronger guarantees would require additional safeguards, such as independently protected integrity checkpoints.

---

### Test 4 — Controlled Ballot Tampering

**Objective**

Determine whether the integrity verification mechanism detects deliberately modified ballot data.

**Security risk**

An attacker with unauthorised database access might attempt to alter recorded ballots.

**Testing approach**

Controlled modifications were introduced into test ballot data within the local testing environment.

The integrity verification mechanism was then executed to assess whether the modifications could be detected.

**Expected outcome**

The system should identify inconsistencies introduced by the controlled modification.

**Observed outcome**

The application detected the controlled tampering during local testing.

**Result: PASS**

**Security significance**

This test provides evidence that the implemented integrity mechanism can detect the type of record modification used during the evaluation.

**Limitation**

The result does not demonstrate resistance to every form of database compromise or attacker behaviour.

---

### Test 5 — Results-Page Integrity Reporting

**Objective**

Evaluate whether an integrity verification failure is communicated through the election results interface.

**Security risk**

A security failure that is not clearly reported may go unnoticed by an administrator.

**Testing approach**

The application was evaluated to determine whether a detected integrity failure would be reflected in the results interface.

**Expected outcome**

The interface should report the detected integrity failure rather than incorrectly presenting the affected records as valid.

**Observed outcome**

The results page reported the integrity failure during local testing.

**Result: PASS**

**Security significance**

This demonstrates the integration of a security verification mechanism with an administrative reporting interface.

---

## 5. Summary of Security Test Results

| Test ID | Security Control | Observed Result | Status |
|---|---|---|---|
| ST-01 | Duplicate-voting prevention | Duplicate-voting test passed locally | PASS |
| ST-02 | Concurrent submission handling | Concurrent submission test passed locally | PASS |
| ST-03 | SHA-256 hash-chain verification | Integrity verification passed locally | PASS |
| ST-04 | Controlled ballot tampering | Deliberate modification detected locally | PASS |
| ST-05 | Results-page integrity reporting | Integrity failure reported locally | PASS |

**Overall finding:** All five selected security tests passed under the local test conditions.

These results should not be interpreted as a comprehensive penetration test, security certification or independent assessment of the application.

---

## 6. Security Architecture Evaluation

### 6.1 Authentication

The application incorporates account authentication and email verification.

These controls support account access and registration verification.

Further evaluation should include session security, account enumeration, brute-force resistance and authentication recovery mechanisms.

### 6.2 Encryption

The application uses Fernet authenticated encryption to protect stored ballot contents.

This provides confidentiality and authenticated protection for encrypted data when cryptographic keys are appropriately managed.

Encryption does not independently guarantee voter anonymity or prevent compromise of the application itself.

### 6.3 Access Control

The system implements role-based access control to separate voter and administrator functions.

A more comprehensive assessment should evaluate whether every protected endpoint consistently enforces its required permissions.

### 6.4 Integrity Verification

SHA-256 hash chaining provides a mechanism for identifying certain modifications to recorded ballot data.

Additional controls would be required to protect against attackers capable of modifying both ballot records and their integrity metadata.

### 6.5 Audit Logging

The application incorporates security audit logging to support investigation and administrative monitoring.

Further evaluation should examine audit-log retention, access restrictions, completeness and resistance to unauthorised modification.

---

## 7. Limitations of the Security Evaluation

The testing activities were conducted as part of an academic research project.

The evaluation has several limitations:

- The documented tests were performed in a controlled local environment.
- The tests do not represent a comprehensive penetration test.
- The application has not been independently security-certified.
- Large-scale performance and denial-of-service testing have not been established by these results.
- The tests do not establish end-to-end election verifiability.
- Voter anonymity and coercion resistance have not been established.
- The tests do not demonstrate protection against every privileged attacker.
- A complete assessment of production infrastructure and operational security is outside the scope of the documented results.

These limitations are important when interpreting the findings.

---

## 8. Security Improvement Recommendations

The following improvements are recommended for future development.

### 8.1 Independent Security Assessment

Conduct a structured application security assessment, including authentication, authorisation, session management and input validation.

### 8.2 Automated Security Testing

Expand automated tests to include additional negative test cases and regression checks.

### 8.3 Stronger Integrity Protection

Investigate independently protected integrity checkpoints or digitally signed audit records to strengthen tamper-evidence.

### 8.4 Security Monitoring

Develop additional monitoring and alerting for suspicious authentication activity, access-control failures and integrity-check failures.

### 8.5 Load and Concurrency Testing

Conduct further performance and concurrency testing under realistic simulated workloads.

### 8.6 Secure Deployment Practices

Continue using separate staging and production environments, protected configuration values, controlled deployment procedures and database backups.

---

## 9. Cybersecurity Skills Demonstrated

This project provided practical experience relevant to entry-level cybersecurity roles.

**Security Testing**
- Developing security test scenarios.
- Evaluating expected and observed outcomes.
- Investigating security-control behaviour.
- Documenting test limitations.

**Security Operations**
- Reviewing security-relevant application events.
- Interpreting integrity verification results.
- Recognising suspicious data modifications.
- Supporting incident investigation through audit information.

**Application Security**
- Authentication and authorisation concepts.
- Cryptographic data protection.
- Database integrity mechanisms.
- Secure application development principles.

**Technical Reporting**
- Documenting test objectives.
- Recording security findings.
- Communicating technical risks.
- Recommending security improvements.

These activities demonstrate practical cybersecurity learning and research experience rather than professional SOC employment experience.

---

## 10. Conclusion

The selected security tests demonstrated that the Secure Electronic Voting System's duplicate-voting prevention, concurrent submission handling, hash-chain verification, controlled tampering detection and results-page integrity reporting mechanisms operated as expected under the local testing conditions.

The evaluation also identified important limitations and areas for future security improvement.

The project demonstrates the practical application of cybersecurity principles in the development and evaluation of a cloud-hosted web application.

It provides evidence of technical skills relevant to cybersecurity analysis, application security and entry-level security operations.

---

## 11. Project Information

**Project:** Secure Electronic Voting System  
**Author:** Micah K. Yego  
**Qualification:** MSc Computer Science (Cybersecurity)

**Live Demonstration:**  
https://secure-election-system.onrender.com

**GitHub Profile:**  
https://github.com/MikeKips2020

**Source Code:** Maintained in a private repository.

**Disclaimer:** This project is an academic research prototype and is not intended or certified for use in real elections.
