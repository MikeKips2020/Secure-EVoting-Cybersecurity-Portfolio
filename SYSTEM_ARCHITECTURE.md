# Secure Electronic Voting System — System Architecture

**Author:** Micah K. Yego  
**Qualification:** MSc Computer Science (Cybersecurity)  
**Project:** Secure Electronic Voting System  
**Document Type:** Technical Architecture and Security Design  
**Project Classification:** Academic Research Prototype

---

## 1. Introduction

This document describes the high-level architecture and security design of a Secure Electronic Voting System developed as part of my MSc Computer Science (Cybersecurity) dissertation.

The project explores how authentication, encryption, access control, database protection and integrity verification can be incorporated into an electronic voting application.

The application is designed as an academic research prototype, with particular consideration for electoral administration in developing countries.

**Live demonstration:** https://secure-election-system.onrender.com

**Disclaimer:** This application is an academic prototype and is not certified or intended for use in real elections.

---

## 2. System Architecture Overview

The application follows a web-based client-server architecture consisting of three primary layers.

### Presentation Layer

The presentation layer provides interfaces for:

- Voter registration and authentication.
- Email verification.
- Election and candidate selection.
- Electronic ballot submission.
- Administrator dashboards.
- Election management.
- Security audit monitoring.
- Election results and integrity reporting.

### Application Layer

The application layer is implemented using Python and Flask.

It handles:

- User authentication and session management.
- Role-based authorisation.
- Voter registration and verification.
- Election configuration.
- Ballot processing.
- Cryptographic operations.
- Duplicate-voting controls.
- Security audit logging.
- Ballot integrity verification.

### Data Layer

PostgreSQL provides persistent storage for application records, including:

- Registered voter accounts.
- Election configurations.
- Electoral contests.
- Candidate information.
- Encrypted ballot records.
- Voting participation information.
- Security audit records.

The application is deployed using Render cloud infrastructure.

---

## 3. High-Level Architecture Diagram

```text
                +------------------------+
                |      Web Browser       |
                |  Voters / Administrators|
                +-----------+------------+
                            |
                            | HTTPS
                            v
                +------------------------+
                |    Flask Application   |
                |    Hosted on Render    |
                +-----------+------------+
                            |
              +-------------+-------------+
              |             |             |
              v             v             v
       +------------+ +------------+ +-------------+
       |Authentication| | Election  | | Security    |
       |& Access     | | & Voting  | | Audit       |
       |Control      | | Services  | | Functions   |
       +------+-----+ +-----+------+ +------+------+
              |             |               |
              +-------------+---------------+
                            |
                            v
                +------------------------+
                | Cryptographic Controls |
                | Fernet / SHA-256       |
                +-----------+------------+
                            |
                            v
                +------------------------+
                | PostgreSQL Database    |
                | Persistent Records     |
                +------------------------+
```

This diagram represents the logical architecture. It does not disclose private infrastructure configuration or application secrets.

---

## 4. Authentication and Access Control

### 4.1 User Authentication

The application provides account authentication and session-based access management.

Users authenticate before accessing protected voting or administrative functionality.

### 4.2 Email Verification

Email verification supports the voter registration process by checking access to the email address supplied during registration.

Email verification alone does not establish a voter's legal identity or electoral eligibility.

### 4.3 Role-Based Access Control

The application separates functionality according to user roles.

**Voters** can access authorised election and ballot functions.

**General administrators** can access designated election administration features.

**Super administrators** can access broader system administration and security functions.

Role-based access control is intended to reduce unauthorised access to sensitive application operations.

---

## 5. Ballot Encryption

The application uses Fernet authenticated symmetric encryption to protect stored ballot contents.

### Encryption Workflow

1. An authenticated voter selects an eligible candidate.
2. The application validates the ballot submission.
3. The ballot information is encrypted before storage.
4. The encrypted ballot record is saved in PostgreSQL.
5. Authorised application functions can decrypt ballots when required for permitted processing.

Fernet provides confidentiality and authentication of encrypted data when implemented with appropriate key management.

Encryption keys are managed outside the public documentation and are not included in this repository.

### Security Considerations

Encryption helps protect stored ballot information against unauthorised disclosure.

However, database encryption alone does not establish voter anonymity, ballot secrecy throughout the entire workflow or protection against every form of application compromise.

---

## 6. Ballot Integrity Verification

The application implements a SHA-256-based hash chain to support verification of recorded ballot integrity.

### Integrity Workflow

1. A ballot record is created.
2. The application calculates a cryptographic hash associated with the ballot record.
3. The chain links successive ballot records through hash information.
4. An integrity verification function examines the recorded chain.
5. Detected inconsistencies are reported through the application's security monitoring and results interfaces.

### Purpose

The mechanism is designed to detect certain unauthorised changes to stored ballot records.

### Limitations

Hash chaining does not, by itself, guarantee that all forms of tampering will be detected.

For example, stronger guarantees against a privileged attacker rewriting an entire chain require additional protections, such as independently secured checkpoints or external verification.

The implementation is therefore presented as a prototype integrity control rather than a certified tamper-proof ledger.

---

## 7. Duplicate-Voting Prevention

The voting workflow incorporates controls designed to prevent repeated voting by the same account.

The system maintains voting participation information and validates ballot submissions.

The implementation was evaluated using controlled duplicate-voting and concurrent-submission tests.

These tests passed in the local test environment.

The results demonstrate the behaviour of the tested prototype under selected conditions, not a guarantee against every possible concurrency or application-level attack.

---

## 8. Security Audit Logging

The application records security-relevant events to support administrative monitoring and investigation.

Audit records provide visibility into selected system activities and security events.

### Audit Functions

The application includes:

- Administrative audit dashboards.
- Security event records.
- Ballot integrity verification.
- Reporting of detected integrity failures.

### Security Value

Audit logging supports:

- Accountability.
- Security investigation.
- Detection of suspicious activity.
- Troubleshooting.
- Review of application security controls.

Audit records require appropriate access restrictions and retention protections to maintain their reliability.

---

## 9. Election Results Security

The application distinguishes between voting activity, ballot integrity and results publication.

Its results interface can display:

- Encrypted ballot counts.
- Verified ballot counts.
- Ledger integrity status.
- Results publication status.

Candidate standings are restricted while voting remains open.

Results publication is controlled through election administration settings.

This separation is intended to support controlled release of election information.

---

## 10. Deployment Architecture

The application uses the following technologies:

| Layer | Technology |
|---|---|
| User interface | Web browser |
| Application framework | Flask |
| Programming language | Python |
| Database | PostgreSQL |
| Ballot encryption | Fernet |
| Integrity verification | SHA-256 |
| Hosting platform | Render |
| Version control | GitHub |

Separate staging and production environments were used during development and testing.

The production application uses a dedicated PostgreSQL database.

Application configuration and cryptographic keys are excluded from this public architecture document.

---

## 11. Security Testing

Selected security mechanisms were evaluated using controlled tests.

| Test | Objective | Local Test Result |
|---|---|---|
| Duplicate voting | Evaluate prevention of repeated voting | Passed |
| Concurrent submission | Evaluate simultaneous ballot submissions | Passed |
| Hash-chain verification | Verify ballot-record integrity | Passed |
| Controlled ballot modification | Evaluate detection of record tampering | Tampering detected |
| Results-page integrity reporting | Verify reporting of integrity failures | Failure reported |

These results relate to the tested academic prototype.

They do not represent an independent penetration test, formal verification or comprehensive security certification.

---

## 12. Security Limitations and Future Improvements

The prototype demonstrates selected cybersecurity principles but does not provide all protections required by a real-world electronic voting system.

Potential areas for future development include:

- Independent security testing.
- Formal threat modelling.
- Stronger protection of cryptographic keys.
- Independent integrity checkpoints.
- Enhanced voter privacy controls.
- Comprehensive penetration testing.
- Improved monitoring and incident response.
- End-to-end verifiability research.
- Formal election-security evaluation.

---

## 13. Cybersecurity Competencies Demonstrated

This project demonstrates practical experience in:

- Secure software development.
- Web application architecture.
- Authentication and authorisation.
- Applied cryptography.
- Database security.
- Security logging and monitoring.
- Integrity verification.
- Security testing.
- Cloud application deployment.
- Technical documentation.

These competencies are relevant to cybersecurity analyst, security operations and application security roles.

---

## 14. Conclusion

The Secure Electronic Voting System demonstrates how selected cybersecurity controls can be incorporated into a functional web application.

The project combines application development, cryptographic protection, role-based access control, security auditing and integrity verification.

It also highlights the importance of understanding security limitations and validating protection mechanisms through practical testing.

The project forms part of my cybersecurity portfolio and demonstrates the technical knowledge and practical skills developed during my MSc Computer Science (Cybersecurity) studies.

---

**Author:** Micah K. Yego  
**Project:** MSc Secure Electronic Voting System  
**Purpose:** Academic research, cybersecurity education and technical portfolio demonstration.
