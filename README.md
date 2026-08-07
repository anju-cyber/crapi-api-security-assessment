# API Security Testing Lab

Hands-on **API Security Testing** focused on the **OWASP API Security Top 10 (2023)** using **CRAPI (Completely Ridiculous API)**, **Burp Suite Professional**, and professional-style **penetration testing and reporting workflows**.

This repository is a continuously growing collection of **API vulnerability assessments, proof-of-concepts, Burp request/response captures, screenshots, and professional pentest findings** created during my API security learning journey.

---

## Project Goals

* Practice **manual API security testing**
* Learn **OWASP API Security Top 10 (2023)** vulnerabilities
* Improve **Burp Suite Repeater and Intruder workflows**
* Develop **professional vulnerability reporting skills**
* Build a **recruiter-friendly cybersecurity portfolio** for VAPT and API Security roles

---

## Lab Environment

| Component           | Details                           |
| ------------------- | --------------------------------- |
| Target Application  | CRAPI (Completely Ridiculous API) |
| Testing Environment | Local Docker Lab                  |
| Operating System    | Kali Linux                        |
| Proxy Tool          | Burp Suite Professional           |
| Additional Tools    | curl, Postman, Chromium           |

---

## Repository Structure

```
api-security-testing-lab/
├── README.md
│
├── API1_BOLA_IDOR/
│   ├── README.md
│   ├── report.md
│   ├── burp-request-response.txt
│   └── screenshots/
│
├── API2_Broken_Authentication/
│   ├── README.md
│   ├── report.md
│   ├── burp-request-response.txt
│   └── screenshots/
│
├── API3_BOPLA/
│   ├── README.md
│   ├── report.md
│   ├── burp-request-response.txt
│   └── screenshots/
│
└── API5_BFLA/
    ├── README.md
    ├── report.md
    ├── burp-request-response.txt
    └── screenshots/
```

Each vulnerability folder contains:

* **README.md** → Quick overview of the finding
* **report.md** → Detailed professional vulnerability report
* **burp-request-response.txt** → Captured HTTP evidence
* **screenshots/** → Supporting screenshots and proof-of-concept images

---

## OWASP API Security Top 10 Tracking

| ID    | Vulnerability                                   | Status    |
| ----- | ----------------------------------------------- | --------- |
| API1  | Broken Object Level Authorization (BOLA/IDOR)   | Completed |
| API2  | Broken Authentication                           | Planned   |
| API3  | Broken Object Property Level Authorization      | Planned   |
| API4  | Unrestricted Resource Consumption               | Planned   |
| API5  | Broken Function Level Authorization             | Planned   |
| API6  | Unrestricted Access to Sensitive Business Flows | Planned   |
| API7  | Server Side Request Forgery (SSRF)              | Planned   |
| API8  | Security Misconfiguration                       | Planned   |
| API9  | Improper Inventory Management                   | Planned   |
| API10 | Unsafe Consumption of APIs                      | Planned   |

---

## Completed Assessments

### API1 – Broken Object Level Authorization (BOLA/IDOR)

**Location:** `API1_BOLA_IDOR/`

**Covered:**

* Object identifier manipulation
* Unauthorized access to another user’s resource
* PII disclosure validation
* Burp Suite Repeater workflow
* Professional vulnerability write-up
* Impact and remediation documentation

---

## Testing Workflow

For every new API assessment, the following methodology is used:

```
Recon
  ↓
Capture Request
  ↓
Analyze Parameters
  ↓
Modify Request
  ↓
Validate Vulnerability
  ↓
Assess Impact
  ↓
Document Evidence
  ↓
Write Professional Report
  ↓
Update Repository
```

---

## Reporting Standard

Every `report.md` follows a consistent structure:

1. Severity
2. Affected Endpoint
3. Description
4. Steps to Reproduce
5. Original Request
6. Modified Request
7. Response Evidence
8. Impact Assessment
9. Root Cause
10. Remediation
11. OWASP Reference

This ensures **consistent, industry-style documentation** across all future API security findings.

---

## Tools Used

| Tool                    | Purpose                                  |
| ----------------------- | ---------------------------------------- |
| Burp Suite Professional | Interception and manual API testing      |
| curl                    | Raw HTTP request testing                 |
| Postman                 | API request validation                   |
| Docker                  | CRAPI lab deployment                     |
| Chromium / Firefox      | Browser-based testing                    |
| Git & GitHub            | Version control and portfolio management |

----------------------------------------------------------------------

## Future Roadmap

### Authorization Testing

* BOLA / IDOR
* Function-level authorization bypass
* Object property authorization issues

### Authentication & Session Security

* JWT analysis
* Token tampering
* Session handling flaws
* Password reset workflow testing

### Advanced API Testing

* Rate limit bypass
* Business logic abuse
* Mass assignment
* API versioning issues
* Undocumented / shadow endpoint discovery

### Professional Reporting

* Full API Pentest Reports
* Executive summaries
* Risk rating methodology
* CVSS-style severity justification
* Remediation prioritization

---

## Ethical Notice

All testing documented in this repository is performed **only in authorized laboratory environments** such as **CRAPI and other intentionally vulnerable applications** for **educational and defensive security learning purposes**.

No unauthorized systems or real-world targets are tested.

---

## Author

**Anju **

* MBA (IT) Student
* Cybersecurity & VAPT Learner
* Focus Areas: **API Security, Web Application Pentesting, OWASP Testing, Burp Suite, and Professional Security Reporting**

GitHub: **https://github.com/anju-cyber**

---

## Repository Status

This repository is **actively maintained** and will be continuously updated with new **API security findings, testing methodologies, Burp workflows, and professional pentest reports** as I progress through the **OWASP API Security Top 10** and advanced API penetration testing topics.

