# API Testing Project: ReqRes Classic Playground

This is a pet project focused on API testing using the public REST API https://reqres.in/ 
used for practicing and demonstrating HTTP requests and CRUD operations on user resources.

The goal of this project is to verify the correctness of core endpoints,
input validation, and to document actual API behavior in cases
where it is not explicitly described in the official documentation.

---

## ✅ What Was Done

- Reviewed the official API documentation
- Designed positive, negative, and boundary test cases
- Performed manual API testing using Postman
- Tested the API's response to invalid and edge case input data
- Documented undocumented (or undefined) API behavior
- Prepared reusable Postman collection and environment

---

## 🛠 Tools Used

- Postman — for sending and validating HTTP requests
- Google Sheets — for test case documentation
- GitHub — for version control and project storage

---

## 📂 Project Artifacts

📄 [**Test Cases (Google Sheets)**](https://docs.google.com/spreadsheets/d/1jQ0LReieGNVyiKcxLB3OkHmihXePb5PHUEBmF2nkYws/edit?usp=sharing)  
A table containing positive, negative, and boundary scenarios.
Each test case includes an ID, description, preconditions, steps,
input data, expected result, and actual result.

📬 **Postman Collection**  
A structured set of requests grouped by functionality
(Create, Read, Update, Delete, Auth).

📁 **Postman Environment**  
An environment with predefined variables for convenient test execution.

---

## ▶️ How to Use
To run these tests, you **must** provide a valid API key, as the Playground environment restricts anonymous access.

1. **Get your API Key:**
   - Go to [app.reqres.in](https://app.reqres.in/).
   - Sign up (free) to generate your unique **API Key**.
2. **Import to Postman:**
   - Import the `collection.json` and `environment.json` files.
3. **Configure Environment:**
   - Open the environment settings.
   - Paste your key into the `api_key` variable (Current Value).
4. **Run Tests:**
   - Ensure the correct environment is selected.
   - The collection is configured to **Inherit Auth** from the parent folder, automatically adding the `x-api-key` header to all requests.

---

## ⚠️ Undocumented Behavior and Defect Criteria

In this project, a "Defect" is a clear deviation from the documentation. However, in cases where the documentation is ambiguous, the status **Inconclusive** is used.

These cases are not necessarily "Fails," but they represent architectural inconsistencies or security risks that would require a discussion with the development team. All such cases are detailed in the `testing_summary.md` file.
