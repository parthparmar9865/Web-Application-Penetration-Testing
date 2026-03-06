# Web-Application-Penetration-Testing
Week 1: Study of OWASP Top 10 (2025)
# OWASP Top 10 Vulnerabilities – DVWA Analysis

This document explains the **OWASP Top 10 security vulnerabilities** and their **practical implementation in DVWA (Damn Vulnerable Web Application)**.  
DVWA is used to understand how common web security issues occur and how attackers exploit them.

---

## OWASP Top 10 and DVWA Focus

| Rank | Category | Description | Key Focus in DVWA |
|------|----------|-------------|-------------------|
| **A01** | Broken Access Control | Users can act outside their intended permissions (e.g., viewing other users' data). SSRF is now merged here. | Insecure Direct Object References (IDOR) and privilege escalation. |
| **A02** | Security Misconfiguration | Unhardened servers, default passwords, or open cloud storage. | Default credentials (`admin/password`) and verbose error messages. |
| **A03** | Software Supply Chain Failures | Includes compromised CI/CD pipelines and malicious dependencies. | Using outdated versions of Apache or PHP. |
| **A04** | Cryptographic Failures | Poor encryption of sensitive data in transit or at rest. | Storing user passwords in clear text or weak MD5 hashes. |
| **A05** | Injection | Malicious code (SQL, command, etc.) executed by the server. | SQL Injection and Command Injection modules. |
| **A06** | Insecure Design | Architectural flaws that cannot be fixed by coding alone. | Flawed business logic (e.g., bypassing a checkout step). |
| **A07** | Authentication Failures | Weak authentication mechanisms such as brute force attacks. | Brute Force module and session hijacking. |
| **A08** | Software or Data Integrity Failures | Failure to verify software updates or data integrity. | Insecure deserialization of user input. |
| **A09** | Security Logging & Alerting Failures | Lack of logging and monitoring to detect attacks. | Checking if `apache2` logs record failed login attempts. |
| **A10** | Mishandling of Exceptional Conditions | Poor error handling that leaks sensitive information. | Stack traces revealing database structures during errors. |

---

## Tools Used

- Kali Linux
- DVWA (Damn Vulnerable Web Application)
- Burp Suite
- OWASP ZAP
- Apache Server
- MySQL Database

---

## Purpose of the Project

- Understand common **web application vulnerabilities**
- Practice **penetration testing techniques**
- Learn **secure coding practices**
- Analyze vulnerabilities using **DVWA environment**

---

## Author

**Parth**  
Cybersecurity Learner | Web Security Enthusiast
