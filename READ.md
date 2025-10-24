# Best Buy Automation Project
> An E-commerce purchase process automation testing project using Playwright and Python.

[![Python](https://img.shields.io/badge/Python-3.9%2B-blue)](https://www.python.org/)
[![Playwright](https://img.shields.io/badge/Playwright-UI_Automation-green)](https://playwright.dev/)
[![pytest](https://img.shields.io/badge/pytest-Testing_Framework-orange)](https://docs.pytest.org/)
[![Project Status](https://img.shields.io/badge/Status-In_Progress-yellowgreen)](README.md)

## 📌 Project Overview

This is an automation testing project for the Best Buy E-commerce platform, leveraging **Playwright** and **Python**. It covers the entire purchase flow, from guest sign-in, product browsing, cart management, to checkout. It includes both **End-to-End (E2E) UI testing** and **backend API performance and stability testing**.

### Project Goals:

* Automate the **User-Centric E-commerce Purchase Flow**.
* Utilize diverse testing techniques (**DDT**, **Security Testing**, **Performance Testing**).
* Build a robust and maintainable **Test Automation Framework**.

---

## 🎯 Testing Strategy

### Test Layers

| Layer | Technology | Objective |
| :--- | :--- | :--- |
| **UI Testing** | Playwright | Verification of user interface functionality and usability (E2E). |
| **API Testing** | Python Requests | Verification of backend API performance, stability, and data integrity. |
| **Security Testing** | Data-Driven | Verification against malicious input like SQL Injection and XSS attacks. |

### Testing Techniques

* **DDT (Data-Driven Testing):** Parameterized tests using JSON files for valid/invalid data to maximize test reusability.
* **Boundary Value Analysis:** Focused testing on maximum/minimum values and normal range boundaries.
* **Error Handling:** Validation of exception scenarios like timeouts, network failures, and server errors (5xx).

---

## 📋 UI Test Scenarios & Test Cases

| Scenario | Description | Expected Benefit |
| :--- | :--- | :--- |
| **1️⃣ Guest Sign-in** | Validates the sign-in form using both valid and invalid data. | Ensures secure and accurate login processing. |
| **2️⃣ Product Search & Cart Addition** | Validates normal search functionality and exception handling (typos, special characters). | Provides a user-friendly search experience. |
| **3️⃣ Pagination & Scrolling** | Validates multi-page navigation and dynamic loading (infinite scroll) features. | Ensures smooth product browsing and fast page loading. |
| **4️⃣ Cart Quantity Adjustment** | Validates quantity adjustment and boundary values (zero, max stock, negative numbers). | Ensures safe and intuitive quantity management. |
| **5️⃣ Checkout - Shipping Address Input** | Performs validation and security checks (SQLi, XSS) on shipping information input. | Ensures secure user data handling and input validation. |

### Detailed Test Cases (Excerpt)

| TC ID | Test Case | Input Value | Expected Result | Status |
| :---: | :--- | :--- | :--- | :---: |
| **1-1** | Enter valid email and password | valid\_email@test.com / password123 | Sign-in successful, redirect to homepage | ⏳ |
| **1-2** | Enter invalid email format | invalidEmail / password123 | Error message "Please enter a valid email" | ⏳ |
| **2-3** | Enter non-existent search term | "xyzabc123notfound" | "0 results" message, friendly guidance displayed | ⏳ |
| **4-3** | Enter quantity as 0 | Quantity: 0 | Product is removed from the cart | ⏳ |
| **4-5** | Enter quantity exceeding stock | Stock: 10, Input: 15 | Quantity auto-adjusts to max stock (10), notification displayed | ⏳ |
| **5-4** | **Attempt SQL Injection** | Name: `'; DROP TABLE users; --` | Malicious code sanitized/blocked, processed normally | ⏳ |
| **5-5** | **Attempt XSS Attack** | Name: `<script>alert('XSS')</script>` | Script tags removed/escaped, stored as text only | ⏳ |

*Data Files*: `data/login_test_data.json`, `data/delivery_test_data.json`

---

## 🌐 API Test Scenarios (Performance & Stability)

| Scenario | Description | SLA (Target Response Time) |
| :--- | :--- | :--- |
| **A: Product Search API** | Verification of backend search API response time and load performance. | `< 500ms` |
| **B: Cart API** | Verification of API response time and stability for adding/modifying/viewing the cart. | `< 300ms` |
| **C: Network Error & Timeout Handling** | Verification of resilience against network instability and server errors (5xx). | - |

### Detailed Test Cases (Excerpt)

| TC ID | Test Case | Request (Example) | Expected Result | SLA | Status |
| :---: | :--- | :--- | :--- | :--- | :---: |
| **API-1** | Product Search API Response Time | `GET /api/products?search=laptop` | Status: 200 OK, Response time recorded | `< 500ms` | ⏳ |
| **API-4** | Add Product to Cart | `POST /api/cart/add` (Payload) | Status: 201 Created, Product added | `< 300ms` | ⏳ |
| **API-8** | Server Error (500) Response | API returns 500 Internal Server Error | User-friendly error message displayed | - | ⏳ |

---

## 🛠️ Technology Stack

| Category | Technology | Role and Usage |
| :--- | :--- | :--- |
| **Testing Framework** | **pytest** | Python-based test execution and management. |
| **UI Automation** | **Playwright** | Performing E2E tests across Chromium, Firefox, and WebKit. |
| **API Testing** | **requests** | Sending and validating backend REST API requests. |
| **Programming Language** | **Python** | Development of test code and utility scripts. |
| **Reporting** | **pytest-html** | Visualizing test results in an HTML report file. |
| **Data Management** | **JSON** | Storing test data for Data-Driven Testing. |

---

## 📂 Project Structure
best-buy-automation/
├── tests/
│   ├── ui_tests/
│   │   ├── test_login.py
│   │   ├── test_search.py
│   │   ├── test_pagination_scroll.py
│   │   ├── test_cart_quantity.py
│   │   └── test_delivery_checkout.py
│   ├── api_tests/
│   │   ├── test_product_api.py
│   │   ├── test_cart_api.py
│   │   └── test_error_handling.py
│   └── conftest.py
├── data/
│   ├── login_test_data.json
│   ├── delivery_test_data.json
│   └── api_test_data.json
├── utils/
│   ├── helpers.py
│   └── constants.py
├── reports/
│   └── report.html (자동 생성)
├── pytest.ini
├── requirements.txt
├── .gitignore
└── README.md


🛠️ 기술 스택

Test Framework: Playwright (UI), pytest
Programming Language: Python
API Test: requests
Reporting: pytest-html, Allure Report (선택사항)
Data: JSON
Version Control: Git

## 🚀 How to Run

### 1. Setup Environment

```bash
# Clone the repository
git clone <repository-url>
cd best-buy-automation

# Create and activate a virtual environment
python -m venv venv
source venv/bin/activate  # Windows: venv\Scripts\activate

# Install dependencies (pytest, requests, playwright, etc.)
pip install -r requirements.txt

# Install Playwright browser binaries (required)
playwright install
```

### 2. Execute Tests

| 명령어 (Command) | 설명 (Description) |
| :--- | :--- |
| `pytest tests/ui_tests/ -v` | Execute all UI tests. |
| `pytest tests/api_tests/ -v` | Execute all API tests. |
| `pytest tests/ui_tests/test_login.py -v` | Execute tests from a specific file. |
| `pytest tests/ --html=reports/report.html --self-contained-html -v` | Execute tests and generate an **HTML Report**. |
| `pytest tests/ui_tests/ --headed --video=retain-on-failure -v` | Run with browser GUI visible and capture video on failure. |


## 📊 Status Tracker (진행 상태)

| Category | TC/API ID | Test Case Description | Status |
| :--- | :--- | :--- | :---: |
| **UI Testing** | TC 1 | Guest Sign-in (DDT) | [ ] |
| **UI Testing** | TC 2 | Product Search and Add to Cart | [ ] |
| **UI Testing** | TC 3 | Pagination and Infinite Scroll | [ ] |
| **UI Testing** | TC 4 | Cart Quantity Adjustment | [ ] |
| **UI Testing** | TC 5 | Checkout - Shipping Address Selection | [ ] |
| **API Testing** | API 1-3 | Product Search API Performance | [ ] |
| **API Testing** | API 4-6 | Shopping Cart API (Add/Update/View) | [ ] |
| **API Testing** | API 7-10 | Network Error Handling and Timeouts | [ ] |

### 품질 메트릭 (Quality Metrics)

| Metric | Target | Current Status |
| :--- | :--- | :---: |
| **Test Coverage** | > 80% | ⏳ |
| **Pass Rate** | > 95% | ⏳ |
| **Average Execution Time** | < 10 mins | ⏳ |


## 🎬 Execution Results & Screenshots
(To be added after test completion: Screenshots of key test results, e.g., successful sign-in, product added to cart, and an example of the generated HTML report.)

------------------------------------------------------------------------------------------------------

---
## 📝 Test Data Examples

### `data/login_test_data.json` (Guest Sign-in Validation)
```json
{
  "valid_login": {
    "email": "valid_user@test.com",
    "password": "SecurePassword123!"
  },
  "invalid_email_format": {
    "email": "invalid_email_format",
    "password": "password123"
  },
  "empty_fields": {
    "email": "",
    "password": "password123"
  }
}
```
### `data/delivery_test_data.json (Checkout/Security - Updated for Canadian Address)
```json
{
  "valid_delivery": {
    "name": "Jane Doe",
    "address": "123 Main Street, Toronto, ON",
    "postal_code": "M5V 2J5"
  },
  "security_test": {
    "sql_injection": "'; DROP TABLE users; --",
    "xss_attack": "<script>alert('XSS')</script>"
  },
  "boundary_test": {
    "long_address": "A".repeat(255)
  }
}
```
### `data/search_test_data.json (DDT for Product Search Functionality)
```json
{
  "valid_keywords": [
    "laptop",
    "apple watch",
    "sony headphones"
  ],
  "invalid_keywords": [
    "xyzabc123notfound", 
    "!@#$%", 
    "very very long search query exceeding the typical limit..." 
  ]
}
```

---
## 👨‍💻 Author & Update

**Best Buy Automation Test Project**

**Last Updated:** 2025.10.24




