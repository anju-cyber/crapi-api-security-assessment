# API2 – Broken Authentication

This folder contains a practical assessment of an **OTP brute-force bypass caused by API version downgrade** in the CRAPI password reset workflow.

## Vulnerability Summary

* **Category:** OWASP API2:2023 – Broken Authentication
* **Technique:** API Version Downgrade (`v3 → v2`)
* **Impact:** OTP brute-force protection bypass leading to unauthorized password reset and potential account takeover

## Included Files

* `report.md` – Detailed professional vulnerability report
* `burp-request-response.txt` – Captured HTTP requests and responses
* `screenshots/` – Supporting screenshots and proof-of-concept evidence

The assessment was performed in an **authorized CRAPI laboratory environment** for educational and defensive security learning purposes.
