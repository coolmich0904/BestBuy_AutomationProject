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
### Scenario 1️⃣: Guest Login

**Description:** Validates login form validity using both valid and invalid data.

| TC ID | Test Case | Input Values | Expected Result | Status |
|-------|-----------|--------------|-----------------|--------|
| 1-1 | Valid email and password input | valid_email@test.com / password123 | Login successful, redirect to homepage | ⏳ |
| 1-2 | Invalid email format input | invalidEmail / password123 | Error message "Please enter a valid email" | ⏳ |
| 1-3 | Empty email field | (empty) / password123 | Error message "Email is required" | ⏳ |
| 1-4 | Empty password field | valid_email@test.com / (empty) | Error message "Password is required" | ⏳ |
| 1-5 | All fields empty | (empty) / (empty) | Error messages displayed, login button disabled | ⏳ |

**Data File:** `data/login_test_data.json`

---

### Scenario 2️⃣: Product Search & Add to Cart

**Description:** Validates search functionality normal operation and exception handling.

| TC ID | Test Case | Input | Expected Result | Status |
|-------|-----------|-------|-----------------|--------|
| 2-1 | Valid single search term input | "laptop" | Search results page loads, 5+ products displayed | ⏳ |
| 2-2 | Add first product from search results to cart | "laptop" search then click first product | Product added to cart, confirmation message shown | ⏳ |
| 2-3 | Non-existent search term input | "xyzabc123notfound" | "0 results" message, "Try different keywords" helpful message displayed | ⏳ |
| 2-4 | Search term with typo | "lapto" (typo) | "0 results", suggested search terms or similar products recommended | ⏳ |
| 2-5 | Search with special characters | "$@#%&" | Safely processed or ignored, no errors | ⏳ |
| 2-6 | Whitespace only input | "   " | "Please enter search term" message or "0 results" | ⏳ |

**Expected Benefit:** User-friendly search experience

---

### Scenario 3️⃣: Pagination & Scroll-based Product Selection

**Description:** Validates multi-page product list navigation and dynamic loading functionality.

| TC ID | Test Case | Action | Expected Result | Status |
|-------|-----------|--------|-----------------|--------|
| 3-1 | First page product list loads | Page access | Product list loads normally, minimum 10+ products displayed | ⏳ |
| 3-2 | Page scroll (infinite scroll) | Scroll page down | Additional products auto-load, loading indicator displayed | ⏳ |
| 3-3 | Next page button click | Click "Next" button | New page product list loads, URL/page number updates | ⏳ |
| 3-4 | Select product on next page and add to cart | Select product on page 2, click "Add to Cart" | Product successfully added, cart quantity increases | ⏳ |
| 3-5 | Last page confirmation | Navigate to last page | "Next" button disabled or hidden, "Previous" button enabled | ⏳ |
| 3-6 | Previous page button functionality | Click "Previous" on page 2 | Navigate to previous page, product list redisplayed | ⏳ |

**Expected Benefit:** Smooth product browsing experience, fast page loading

---

### Scenario 4️⃣: Shopping Cart Quantity Adjustment

**Description:** Validates cart quantity adjustment and boundary value testing.

| TC ID | Test Case | Input | Expected Result | Status |
|-------|-----------|-------|-----------------|--------|
| 4-1 | Normal quantity increase | 1 → 3 | Quantity changed to 3, price auto-calculated | ⏳ |
| 4-2 | Normal quantity decrease | 3 → 1 | Quantity changed to 1, price auto-calculated | ⏳ |
| 4-3 | Quantity set to 0 | Quantity: 0 | Product removed from cart | ⏳ |
| 4-4 | Negative quantity input | Quantity: -5 | Input ignored or error message "Quantity must be 1 or more" | ⏳ |
| 4-5 | Quantity exceeds stock | Current stock: 10, Input: 15 | Auto-adjusted to max stock (10), advisory message shown | ⏳ |
| 4-6 | Very large number input | Quantity: 999999 | Auto-adjusted to max stock quantity, no errors | ⏳ |
| 4-7 | Quantity +/- button UI | Click +/- buttons | Quantity increments/decrements by 1 per click, real-time update | ⏳ |

**Expected Benefit:** Safe and intuitive quantity management

---

### Scenario 5️⃣: Checkout Screen - Shipping Address Selection & Input

**Description:** Validates shipping address input validity and security testing.

| TC ID | Test Case | Input | Expected Result | Status |
|-------|-----------|-------|-----------------|--------|
| 5-1 | Valid shipping address input (normal case) | Name: "Kim Min-su" / Address: "123 Main St, Seoul" | Info saved, successfully advance to next step (checkout) | ⏳ |
| 5-2 | Maximum character string in address field | 255 characters in address | Saved without errors, able to proceed to next step | ⏳ |
| 5-3 | Exceeding maximum characters in address field | 256+ characters in address | Error message "Address must be 255 characters or less" displayed | ⏳ |
| 5-4 | SQL injection attack attempt | Name: "'; DROP TABLE users; --" | Malicious code sanitized/blocked, processed normally | ⏳ |
| 5-5 | XSS attack attempt | Name: "<script>alert('XSS')</script>" | Script tags removed/escaped, stored as text only | ⏳ |
| 5-6 | Special characters input | Name: "O'Brien" / Address: "Apt. #501, 5th Ave." | Normally saved, special characters safely processed | ⏳ |
| 5-7 | Required field not filled | Name field empty | Error message "Name is required", next button disabled | ⏳ |
| 5-8 | Invalid postal code | Postal code: "ABCDE" | Error message "Please enter valid postal code format" | ⏳ |

**Data File:** `data/delivery_test_data.json`

**Expected Benefit:** Secure user information handling, input validity assurance

---

## 🌐 API Test Scenarios

### Scenario A: Product Search API Performance Testing

**Description:** Validates backend API response times and performance.

| TC ID | Test Case | Request | Expected Result | SLA | Status |
|-------|-----------|---------|-----------------|-----|--------|
| API-1 | Product search API response time | GET /api/products?search=laptop | Status: 200 OK, response time recorded | < 500ms | ⏳ |
| API-2 | Empty search term API request | GET /api/products?search= | Status: 200 OK, empty array returned | < 300ms | ⏳ |
| API-3 | Large search results handling | GET /api/products?search=a | Status: 200 OK, pagination handled | < 800ms | ⏳ |

---

### Scenario B: Shopping Cart API Performance Testing

**Description:** Validates shopping cart add/modify API response times.

| TC ID | Test Case | Request | Expected Result | SLA | Status |
|-------|-----------|---------|-----------------|-----|--------|
| API-4 | Add product to cart | POST /api/cart/add (product_id: 123, quantity: 1) | Status: 201 Created, product added | < 300ms | ⏳ |
| API-5 | Modify cart item quantity | PUT /api/cart/items/123 (quantity: 5) | Status: 200 OK, quantity updated | < 250ms | ⏳ |
| API-6 | Retrieve cart | GET /api/cart | Status: 200 OK, cart items list returned | < 400ms | ⏳ |

---

### Scenario C: Network Error & Timeout Handling

**Description:** Validates resilience to network instability and server errors.

| TC ID | Test Case | Scenario | Expected Behavior | Status |
|-------|-----------|----------|-------------------|--------|
| API-7 | Connection timeout | Request exceeds 1 second limit | Retry logic activates, max 3 retries then failure returned | ⏳ |
| API-8 | Server error (500) response | API returns 500 Internal Server Error | User-friendly error message displayed | ⏳ |
| API-9 | Server error (503) response | API returns 503 Service Unavailable | Display "Temporary error. Please try again later" message | ⏳ |
| API-10 | Network connection loss | Network disconnects during request | Auto-reconnect, wait then retry | ⏳ |

**Expected Benefit:** Stable and reliable API operation


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




