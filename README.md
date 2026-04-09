# Lendsqr Adjutor API Automation & Audit

## 🚀 Project Overview
This repository contains a defensive automated test suite for the Lendsqr Adjutor API. It covers **Validation, Credit Bureaus, Direct Debit, and Decisioning** modules.

## 🛠 Setup Instructions
1. **Clone the repo:** `https://github.com/YannickAtabong9/lendsqr-adjutor-api-automation`
2. **Import into Postman:** Import the files located in the `/postman` folder.
3. **Configure API Key:** In Postman, set the `api_key` variable to your personal Adjutor key.

## 📊 Task 2: Test Results Summary
| Module | Endpoint | Status | Observation |
| :--- | :--- | :--- | :--- |
| **Validation** | BVN Consent & Accounts | ❌ FAIL | Systemic Empty Payload bug. |
| **Credit Bureaus** | CRC & FirstCentral | ❌ FAIL | 200 OK returned with `{}` body. |
| **Direct Debit** | Banks & Lookup | ❌ FAIL | Missing data arrays and resolved names. |
| **Decisioning** | Models & Details | ❌ FAIL | Empty payloads on 100% of requests. |

## 📈 Task 3: Performance Inference
- **Observation:** Average latency is **~500ms** for empty responses.
- **Risk:** Latency will spike once data serialization is fixed.
- **Recommendation:** Implement **Redis Caching** and **Async Webhooks** for 3rd-party bureau lookups.

## 🛡 Task 4: Security Audit
- **Vulnerability:** **Improper Error Handling (Silent Failure)**.
- **Analysis:** Returning `200 OK` for failed data fetches allows attackers to bypass security monitoring (IDS/SIEM).
- **Recommendation:** Implement **Fail-Fast** error codes (404/400) and **Egress PII Masking**.
