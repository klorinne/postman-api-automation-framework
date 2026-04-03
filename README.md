# 📇 Contact List API - E2E Test Suite
**Base URL:** `https://thinking-tester-contact-list.herokuapp.com`

This collection is designed to validate the full lifecycle of a contact record within the Contact List Application. It follows a sequential flow to ensure data integrity, starting from user authentication through to record cleanup and session termination.

## 🧪 Test Flow Logic
The suite is structured to handle dynamic data dependencies, where subsequent requests rely on variables captured from earlier steps:

* **Authentication & Session Initiation:** Authenticates the user and captures the required access token for all following requests.
* **Resource Creation:** Generates a new contact record and dynamically stores the unique `contactId`.
* **Data Persistence & Retrieval:** Confirms the new record is accessible both as an individual resource and within the global contact list.
* **Update Validation:**
    * **Full Update (PUT):** Replaces the entire contact object to verify schema consistency.
    * **Partial Update (PATCH):** Modifies specific fields to ensure granular data handling.
* **Cleanup & Negative Validation:** Deletes the record and performs a follow-up check to confirm the resource no longer exists (expecting a 404 Not Found).
* **Session Teardown:** Formally logs the user out to invalidate the active session.

---

## 📋 API Endpoint Reference

| Step | Method | Endpoint | Purpose |
| :--- | :--- | :--- | :--- |
| **1** | `POST` | `/users/login` | Authenticates user; sets `{{token}}`. |
| **2** | `POST` | `/contacts` | Creates a new contact; sets `{{contactId}}`. |
| **3** | `GET` | `/contacts/{{contactId}}` | Validates retrieval of the new record. |
| **4** | `GET` | `/contacts` | Validates the record appears in the full list. |
| **5** | `PUT` | `/contacts/{{contactId}}` | Executes a full record update. |
| **6** | `PATCH` | `/contacts/{{contactId}}` | Executes a partial field update. |
| **7** | `DELETE` | `/contacts/{{contactId}}` | Removes the contact record. |
| **8** | `GET` | `/contacts/{{contactId}}` | Confirms deletion of records. |
| **9** | `POST` | `/users/logout` | Terminates the user session. |

---

## 📖 Documentation Version History

| Version | Date | Author | Description of Revision |
| :--- | :--- | :--- | :--- |
| **v1.0** | 2026-04-03 | Corinne | Initial test suite creation with Basic Auth and CRUD endpoints. |

---

## 🛠 Tech Stack
* **Postman:** Request authoring and JavaScript assertions.
* **Newman:** CLI runner for Postman collections.
* **GitHub Actions:** CI/CD pipeline integration.
* **htmlextra:** Enhanced HTML