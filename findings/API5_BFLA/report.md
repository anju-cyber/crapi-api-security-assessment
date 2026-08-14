## Finding: Broken Function Level Authorization (BFLA)

### Severity

**High**

---

### Affected Endpoint

```
PUT /identity/api/v2/user/video/{id}
DELETE /identity/api/v2/admin/video/{id}
```

---

### Description

The application fails to properly enforce **function-level authorization** for administrative video management operations. A normal authenticated user is able to modify a legitimate user-level API request and access an **admin-only endpoint** by changing both the **HTTP method** and the **API resource path**.

The issue allows a low-privileged user to perform **unauthorized administrative actions**, including deletion of video resources that should only be accessible to administrators.

---

### Original User Functionality

A normal user can update the name of their own video using the following endpoint:

```http
PUT /identity/api/v2/user/video/52 HTTP/1.1
Host: 127.0.0.1:8888
Authorization: Bearer <JWT>
```

---

### Steps to Reproduce

1. Authenticate as a **normal user**.
2. Navigate to the **Profile → Edit Video** functionality.
3. Capture the request in **Burp Suite**.
4. Observe the original request:

```http
PUT /identity/api/v2/user/video/52 HTTP/1.1
```

5. Send the request to **Burp Repeater**.
6. Test the allowed HTTP methods for the endpoint.
7. Replace the user resource path with the predictable admin resource:

```http
DELETE /identity/api/v2/admin/video/52 HTTP/1.1
Host: 127.0.0.1:8888
Authorization: Bearer <JWT>
```

8. Send the modified request.
9. Observe that the application processes the request successfully and deletes the video resource despite the user not having administrative privileges.

---

### Evidence

#### 1. Original User Request

Screenshot showing the legitimate `PUT /user/video/52` request used to update the video name.

#### 2. Allowed HTTP Method Enumeration

Screenshot showing the testing of supported HTTP methods for the video endpoint.

#### 3. Modified Admin Request

Screenshot showing the modified request using:

```http
DELETE /identity/api/v2/admin/video/52
```

#### 4. Successful Unauthorized Action

Screenshot confirming that the video resource was deleted successfully through the admin endpoint.

---

### Impact

* Unauthorized access to **administrator-only functionality**
* Deletion of video resources by low-privileged users
* Horizontal and potentially vertical privilege escalation
* Loss of **integrity and availability** of application data
* Increased risk of unauthorized administrative operations across other API endpoints

---

### Root Cause

The application performs **authentication during login**, but it does not enforce **server-side authorization checks for sensitive administrative functions**. The API relies on predictable REST resource naming (`/user/` and `/admin/`) without validating whether the authenticated user has the required administrative role before executing the requested action.

---

### Remediation

* Implement **server-side role-based access control (RBAC)** for all administrative endpoints.
* Validate user privileges for **every sensitive API action**, especially `DELETE`, `PUT`, and `POST` operations.
* Return **403 Forbidden** for unauthorized access attempts instead of exposing predictable administrative resources.
* Avoid relying solely on URL path naming conventions (`/admin/`) to protect privileged functionality.
* Restrict unnecessary HTTP methods for non-administrative users.
* Add authorization checks within a **centralized middleware or API gateway layer**.
* Implement security logging and alerting for failed authorization attempts against administrative endpoints.

---

### OWASP Reference

**OWASP API5:2023 – Broken Function Level Authorization**

---

### Environment

This finding was identified in the **CRAPI laboratory environment** during an authorized educational security assessment.
