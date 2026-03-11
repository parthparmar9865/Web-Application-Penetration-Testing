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

## Test Environment Setup (DVWA)

To perform vulnerability testing, a controlled lab environment was created using **DVWA (Damn Vulnerable Web Application)** on **Kali Linux**. DVWA is intentionally vulnerable and helps security learners practice penetration testing techniques safely.

---

### Step 1: Update System

Update Kali Linux packages before installing required tools.

```bash
sudo apt update
sudo apt upgrade -y
```

---

### Step 2: Install Apache, MySQL, and PHP

DVWA requires a web server, database, and PHP.

```bash
sudo apt install apache2 -y
sudo apt install mariadb-server -y
sudo apt install php php-mysqli php-gd libapache2-mod-php -y
```

---

### Step 3: Start Services

Start Apache and MySQL services.

```bash
sudo service apache2 start
sudo service mysql start
```

Enable services at boot:

```bash
sudo systemctl enable apache2
sudo systemctl enable mysql
```

---

### Step 4: Download DVWA

Clone DVWA from GitHub into the Apache web directory.

```bash
cd /var/www/html
sudo git clone https://github.com/digininja/DVWA.git
```

---

### Step 5: Configure DVWA

Copy the configuration file.

```bash
cd DVWA/config
sudo cp config.inc.php.dist config.inc.php
```

Edit the configuration file if needed.

```bash
sudo nano config.inc.php
```

---

### Step 6: Set Permissions

```bash
sudo chmod -R 777 /var/www/html/DVWA
```

---

### Step 7: Access DVWA

Open a browser and go to:

```
http://localhost/DVWA
```

Click **Create / Reset Database** to initialize the database.

---

### Default Login Credentials

```
Username: admin
Password: password
```

---

### Environment Used

* Kali Linux
* Apache2 Web Server
* MariaDB / MySQL Database
* PHP
* DVWA (Damn Vulnerable Web Application)

---

### Purpose

The DVWA environment allows testing and understanding of common web vulnerabilities such as:

* SQL Injection
* Command Injection
* Cross-Site Scripting (XSS)
* Brute Force Attacks
* File Inclusion

This setup provides a safe environment for practicing **web application penetration testing**.
## Week 2: Vulnerability Testing

In this phase, multiple **OWASP Top 10 vulnerabilities** were tested using **DVWA (Damn Vulnerable Web Application)**. The objective was to understand how common web application vulnerabilities can be exploited.

---

## 1. SQL Injection (Injection)

**Description:**
SQL Injection occurs when user input is not properly validated and is directly used in SQL queries. Attackers can manipulate queries to access unauthorized data.

**Testing Steps:**

1. Navigate to **DVWA → SQL Injection** module.
2. Enter payload in the input field.

**Example Payload**

```sql
1' OR '1'='1
```

**Result:**
The application returned multiple user records from the database, confirming the vulnerability.

**Impact:**

* Unauthorized database access
* Data leakage
* Authentication bypass

<img width="940" height="588" alt="image" src="https://github.com/user-attachments/assets/316dd811-f7d8-4e87-a790-8da663a5363a" />

---

## 2. Broken Authentication

**Description:**
Broken authentication occurs when the application allows attackers to compromise passwords, session tokens, or authentication mechanisms.

**Testing Steps:**

1. Navigate to **DVWA → Brute Force module**.
2. Attempt multiple login combinations.

**Example Credentials**

```
Username: admin
Password: password
```

**Result:**
Weak credentials allowed successful login, demonstrating weak authentication controls.

**Impact:**

* Unauthorized account access
* Credential compromise
* Account takeover

---

## 3. Cross-Site Scripting (XSS)

**Description:**
XSS occurs when an application allows attackers to inject malicious scripts into web pages viewed by other users.

**Testing Steps:**

1. Navigate to **DVWA → XSS (Reflected)**.
2. Enter malicious JavaScript code.

**Example Payload**

```html
<script>alert('XSS')</script>
```

**Result:**
A JavaScript alert box appeared in the browser, confirming the XSS vulnerability.

**Impact:**

* Session hijacking
* Cookie theft
* Malicious script execution

---

## 4. Sensitive Data Exposure

**Description:**
Sensitive data exposure occurs when applications fail to properly protect sensitive information such as passwords or personal data.

**Testing Steps:**

1. Analyze login pages and responses.
2. Check encryption methods used for passwords.
3. Inspect network traffic using browser developer tools.

**Observation:**

* Weak hashing algorithms (e.g., MD5)
* Sensitive information exposed through insecure transmission.

**Impact:**

* Data theft
* Credential leakage
* Privacy violations

---

## Tools Used

* Kali Linux
* DVWA (Damn Vulnerable Web Application)
* Burp Suite
* Web Browser Developer Tools

---

## Conclusion

This testing phase demonstrated how common **OWASP Top 10 vulnerabilities** can affect web applications. Understanding these vulnerabilities helps developers implement proper security controls and build more secure systems.

**Vulnerability Focus and Proof-of-Concept (PoC)**

This phase of the project focused on analyzing critical OWASP Top 10 vulnerabilities, specifically Security Misconfiguration and Broken Access Control.
Each vulnerability was tested in the DVWA environment and documented with a Proof-of-Concept (PoC) report.

**1. Security Misconfiguration
Description**

Security Misconfiguration occurs when systems, frameworks, or applications are configured insecurely. This may include default credentials, unnecessary services, verbose error messages, or improperly configured permissions.

**Test Performed**

The DVWA application was accessed using default credentials without any security hardening.

**Steps to Reproduce**

Open the DVWA login page.

Enter default credentials.

Username: admin
Password: password

Login was successful without any restrictions.

Proof of Concept (PoC)

Application allowed login with default credentials.

Security level was set to Low, exposing multiple vulnerabilities.

**Impact**

Unauthorized access to the application

Exposure of sensitive information

Increased attack surface

Recommended Mitigation

Remove default credentials

Apply secure server configuration

Disable unnecessary services

Use proper error handling

**2. Broken Access Control
Description**

Broken Access Control occurs when users can access resources or perform actions beyond their intended permissions.

**Test Performed**

The application allowed users to access restricted resources by modifying parameters in the URL.

**Steps to Reproduce**

Navigate to a restricted page in DVWA.

Modify the URL parameter or access object IDs directly.

Example:

http://localhost/DVWA/vulnerable_page?id=1

Change the ID value to access other user data.

http://localhost/DVWA/vulnerable_page?id=2
Proof of Concept (PoC)

Unauthorized access to other user data was possible.

No proper access validation was implemented.

**Impact**

Exposure of sensitive user data

Unauthorized data modification

Privilege escalation

## Purpose of the Project

- Understand common **web application vulnerabilities**
- Practice **penetration testing techniques**
- Learn **secure coding practices**
- Analyze vulnerabilities using **DVWA environment**

---

## Author

**Parth**  
Cybersecurity Learner | Web Security Enthusiast
