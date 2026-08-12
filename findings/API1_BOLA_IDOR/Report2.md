## Finding: Broken Object Level Authorization (BOLA / IDOR)

### Severity

**High**

---

### Affected Endpoint

```
GET /identity/api/v2/vehicle/{id}/location
```

---

### Description

The application fails to properly enforce **object-level authorization** when accessing vehicle location information. By modifying the `vehicle id` in the request, an authenticated user can access location and related vehicle information belonging to other users.

The vulnerability becomes more critical because valid vehicle identifiers can be obtained from the **community API**, which exposes excessive information associated with user comments.

---

### Discovery Path

The following endpoint exposed vehicle identifiers associated with community posts:

```
GET /community/api/v2/community/posts/{encoded_value}
```

The response revealed vehicle-related identifiers that could be reused in other API endpoints.

---

### Steps to Reproduce

1. Authenticate as a valid user.
2. Browse the community section of the application.
3. Capture the request to:

```
GET /community/api/v2/community/posts/{encoded_value}
```

4. Observe that the response contains **vehicle IDs belonging to multiple users**.
5. Access your own vehicle location endpoint:

```
GET /identity/api/v2/vehicle/4bae9968-ec7f-4de3-a3a0-balb2ab5e5e5/location
```

6. Replace the vehicle ID with another exposed identifier:

```
GET /identity/api/v2/vehicle/9abdd5b3-0e25-45c8-8df4-8df4e4a8c0f7/location
```

7. Send the modified request.
8. Observe that the application returns **another user’s vehicle location and associated information**.

---

### Evidence

* Community API response exposing vehicle identifiers
* Successful access to another user’s vehicle location after modifying the `vehicle id` parameter
* Location and user-related information returned in the API response

---

### Impact

* Unauthorized access to other users’ vehicle information
* Exposure of sensitive customer data
* Disclosure of vehicle location information
* Loss of confidentiality of user data
* Potential privacy and physical security risks if location information is misused

---

### Root Cause

The application performs authentication but **does not validate whether the authenticated user is authorized to access the requested vehicle resource**. Additionally, the community API exposes **excessive vehicle-related information**, which facilitates enumeration of valid object identifiers.

---

### Remediation

* Implement **server-side authorization checks** for every vehicle resource request.
* Verify ownership of the requested vehicle before returning location data.
* Avoid exposing predictable sequential identifiers where possible.
* Minimize unnecessary data exposure in community API responses.
* Implement monitoring and alerting for unauthorized object access attempts.
* Review all APIs for **excessive data exposure and identifier leakage**.

---

### OWASP Reference

**OWASP API1:2023 – Broken Object Level Authorization**

---
