## Finding: Broken Object Level Authorization (BOLA/IDOR)

### Severity

**High**

---

### Affected Endpoint

```
GET /workshop/api/mechanic_report?id={id}
```

---

### Description

The application fails to enforce proper object-level authorization. By modifying the `id` parameter in the request, an authenticated user can access mechanic reports belonging to other users. The response exposes Personally Identifiable Information (PII), including email addresses and phone numbers.

---

### Steps to Reproduce

1. Log in as a valid user.
2. Request your own mechanic report:

```
GET /workshop/api/mechanic_report?id=6
```

3. Modify the `id` parameter from `6` to `1`.
4. Send the modified request.
5. Observe that the application returns another user’s mechanic report containing PII.

---

### Evidence

The response disclosed the following information for another user:

* **Email:** `robot001@example.com`
* **Phone:** `987657001`

---

### Impact

* Unauthorized access to other users’ mechanic reports
* Exposure of sensitive customer information
* Loss of confidentiality of user data
* Potential privacy and regulatory compliance risks

---

### Root Cause

The application performs authentication but does not validate whether the authenticated user is authorized to access the requested report object.

---

### Remediation

* Implement server-side authorization checks for every object request.
* Verify ownership of the requested report before returning data.
* Avoid exposing predictable sequential identifiers where possible.
* Log and monitor unauthorized object access attempts.

---

### Reference

**OWASP API1:2023 – Broken Object Level Authorization**

