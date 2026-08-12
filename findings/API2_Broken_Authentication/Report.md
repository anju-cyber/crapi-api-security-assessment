## Finding: Broken Authentication via API Version Downgrade and OTP Brute-Force Bypass

### Severity

**High**

---

### Affected Endpoint

```
POST /identity/api/auth/v2/check-otp
```

---

### Description

The application’s password reset workflow uses **API version 3 (`v3`)**, which implements brute-force protection for OTP verification. However, an older **API version 2 (`v2`)** endpoint remains accessible and does not enforce the same security controls.

By modifying the API version in the intercepted request from **`v3` to `v2`**, an unauthenticated attacker can perform unrestricted OTP brute-force attempts and successfully verify a valid OTP for another user’s password reset process.

This vulnerability allows an attacker to **bypass OTP brute-force protections and reset user passwords without possessing the original OTP**, resulting in a **Broken Authentication** condition.

---

### Affected Workflow

```
Forgot Password → OTP Sent to User → OTP Verification → Password Reset
```

---

### Steps to Reproduce

1. Navigate to the **Login** page.
2. Select **Forgot Password**.
3. Submit a valid email address.
4. Intercept the OTP verification request in **Burp Suite**.
5. Observe the original endpoint:

```http
POST /identity/api/auth/v3/check-otp HTTP/1.1
Host: 127.0.0.1:8888
```

6. Modify the request to use the legacy API version:

```http
POST /identity/api/auth/v2/check-otp HTTP/1.1
Host: 127.0.0.1:8888
```

7. Send the request to **Burp Intruder**.
8. Configure the OTP parameter as the payload position.
9. Launch the brute-force attack.
10. Observe that a valid OTP value is eventually accepted by the `v2` endpoint.
11. Submit the accepted OTP and proceed with the password reset process.
12. The application allows the password to be changed without proper OTP protection.

---

**Evidence**

_The following screenshots demonstrate the password reset workflow, API version downgrade, and successful OTP brute-force verification:
_
Screenshot	Description
screenshots/01-forgot-password-ui.png	Forgot password page used to initiate the password reset process
screenshots/02-otp-page-ui.png	OTP verification page displayed after submitting a valid email address
screenshots/03-burp-request-v3-to-v2.png	Burp Suite request showing the API version modified from v3 to v2
screenshots/04-valid-otp-response.png	Successful OTP validation response obtained through the legacy v2 endpoint

These screenshots provide evidence of the API version downgrade, OTP brute-force testing workflow, and successful password reset verification through the legacy API endpoint.

---

### Impact

* Bypass of OTP brute-force protection
* Weakening of multi-factor authentication controls in the password reset workflow
* Unauthorized password reset for valid user accounts
* Potential account takeover if a valid email address is known or can be enumerated
* Loss of confidentiality and integrity of affected user accounts

---

### Root Cause

The application has migrated to **API version 3**, which includes OTP brute-force protection, but the legacy **API version 2** endpoint remains active and does not enforce equivalent security controls such as:

* OTP attempt limits
* Rate limiting
* Temporary account or session lockout
* Consistent authentication and verification logic across API versions

This creates an **API version downgrade attack path** that allows attackers to bypass protections implemented in the newer version.

---

### Remediation

* **Disable or remove the legacy `v2` OTP verification endpoint** if it is no longer required.
* Ensure that **all API versions enforce identical authentication and OTP validation logic**.
* Implement **strict rate limiting** for OTP verification requests.
* Introduce **maximum OTP retry limits** and temporary lockouts after repeated failures.
* Return generic responses to prevent **user or email enumeration**.
* Perform regular **API inventory and deprecation reviews** to identify exposed legacy endpoints.

---

### OWASP Reference

**OWASP API2:2023 – Broken Authentication**

---
