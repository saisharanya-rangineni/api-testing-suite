# 🔌 API Testing Suite

[![API Test Suite](https://github.com/saisharanya-rangineni/api-testing-suite/actions/workflows/api-tests.yml/badge.svg)](https://github.com/saisharanya-rangineni/api-testing-suite/actions/workflows/api-tests.yml)
![Postman](https://img.shields.io/badge/Postman-FF6C37?logo=postman&logoColor=white)
![Newman](https://img.shields.io/badge/Newman_CLI-FF6C37?logo=postman&logoColor=white)
![Node.js](https://img.shields.io/badge/Node.js-339933?logo=nodedotjs&logoColor=white)

A comprehensive API testing suite built with **Postman** and automated via **Newman CLI**, demonstrating CRUD validation, chained requests, JSON schema validation, error handling tests, and CI/CD integration through GitHub Actions.

> **Note:** This project is built for portfolio and demonstration purposes only. No proprietary or company-related information, code, or projects have been used. All tests run against the publicly available [ReqRes API](https://reqres.in/).

---

## 🏗️ Architecture

```
api-testing-suite/
├── collections/                    # Postman collections
│   └── reqres-api-tests.postman_collection.json
├── environments/                   # Environment configurations
│   ├── reqres-env.postman_environment.json         # Your local env (gitignored)
│   └── reqres-env.postman_environment.example.json # Safe template (committed)
├── reports/                        # Generated reports (gitignored)
├── .github/workflows/              # CI/CD pipeline
│   └── api-tests.yml
├── .gitignore
├── package.json                    # Newman runner & scripts
└── README.md
```

## ✨ Key Features

| Feature | Description |
|---|---|
| **CRUD Coverage** | GET, POST, PUT, DELETE with full validation |
| **Chained Requests** | Dynamic data passing between requests via environment variables |
| **JSON Schema Validation** | Structural contract testing for response payloads |
| **Error Handling Tests** | 400, 404 status code validation with error message checks |
| **Response Time SLA** | Performance assertions (< 2000ms) on every request |
| **Data Integrity** | Email format regex, required field checks, type validation |
| **Newman CLI** | Headless execution for CI/CD pipelines |
| **HTML Reports** | Rich interactive reports via newman-reporter-htmlextra |
| **Scheduled Runs** | Weekly automated execution via GitHub Actions cron |

## 🚀 Getting Started

### Prerequisites
- Node.js 18+
- npm
- A free ReqRes API key (see below)

### API Key Setup

ReqRes now requires an API key for all requests. Get one for free at [reqres.in](https://reqres.in/) (sign up takes under a minute).

Once you have your key:

```bash
# Copy the example environment file
cp environments/reqres-env.postman_environment.example.json \
   environments/reqres-env.postman_environment.json
```

Then open `environments/reqres-env.postman_environment.json` and replace `YOUR_REQRES_API_KEY_HERE` with your actual key:

```json
{
  "key": "apiKey",
  "value": "your_actual_key_here"
}
```

> **Note:** The real environment file is gitignored to keep your API key out of version control. Never commit it.

### Installation

```bash
# Clone the repository
git clone https://github.com/saisharanya-rangineni/api-testing-suite.git
cd api-testing-suite

# Install dependencies
npm install
```

### Running Tests

```bash
# Run full test suite with HTML report
npm test

# Run with verbose output
npm run test:verbose

# Run only User Management tests
npm run test:folder:users

# Run only Authentication tests
npm run test:folder:auth
```

### Viewing Reports

After running `npm test`, open the generated report:
```bash
open reports/api-test-report.html
```

The HTML report includes: summary dashboard, pass/fail per request, response times, request/response bodies, and assertion details.

## 🧪 Test Coverage

### User Management (6 tests)
| Test | Method | Validations |
|---|---|---|
| List Users | GET | Status 200, schema validation, data integrity, email regex |
| Single User (chained) | GET | Status 200, ID match, email format, support URL |
| User Not Found | GET | Status 404, empty body, Content-Type header |
| Create User | POST | Status 201, name/job match, ID generated, timestamp |
| Update User (chained) | PUT | Status 200, updated fields, timestamp present |
| Delete User | DELETE | Status 204, empty response body |

### Authentication (4 tests)
| Test | Method | Validations |
|---|---|---|
| Register Success | POST | Status 200, token present, user ID returned |
| Register Missing Password | POST | Status 400, error message validation |
| Login Success | POST | Status 200, token returned |
| Login Missing Password | POST | Status 400, error message validation |

### Cross-Cutting Validations
- Response time SLA (< 2000ms) on all endpoints
- Content-Type header verification
- JSON schema contract testing
- Chained request data passing via environment variables

## ⚙️ CI/CD Pipeline

The GitHub Actions workflow:

- Runs on every push, PR, and weekly (Monday 6 AM UTC)
- Executes full Newman test suite
- Uploads HTML report and JSON results as artifacts
- 30-day artifact retention

## 🛠️ Tech Stack

| Technology | Purpose |
|---|---|
| Postman | API test design and collection management |
| Newman | Command-line collection runner for CI/CD |
| newman-reporter-htmlextra | Rich HTML test reports |
| GitHub Actions | Continuous Integration pipeline |
| ReqRes API | Public REST API for testing |

## 📝 License

This project is licensed under the MIT License.

---

**Author:** [Sai Sharanya Rangineni](https://saisharanya-rangineni.github.io/) | [LinkedIn](https://www.linkedin.com/in/sai-sharanya-r-27b003257/)
