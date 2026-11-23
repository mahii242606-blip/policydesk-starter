# PolicyDesk – Insurance Management System

**PolicyDesk** is a web-based insurance management application developed using Python and FastAPI. It simplifies the insurance workflow by managing customers, insurance products, quotations, policies, and claims in one application.

The project was developed as part of the **TalentPath Academy – AI-Powered SDLC Workshop**.

## 🚀 Project Overview

PolicyDesk provides an end-to-end insurance management workflow:

**Customers → Products → Quotes → Policies → Claims**

The application includes customer management, insurance product management, premium calculation, policy issuance, and claims processing with an approval and rejection workflow.

## ✨ Key Features

- **Dashboard:** View insurance application information.
- **Customer Management:** Create, view, and manage customer records.
- **Product Management:** Manage Health, Motor, and Term Life insurance products.
- **Quotation Management:** Generate and view insurance quotations.
- **Premium Calculation:** Calculate premiums using age, tenure, and add-on factors.
- **Policy Management:** Issue policies from quotations and update policy status.
- **Claims Management:** File claims and view claim details.
- **Claims Approval:** Review, approve, or reject claims with reasons.
- **Database Management:** Store application information using SQLite.
- **API Documentation:** Interactive API documentation using Swagger UI.
- **Automated Testing:** Test application functionality using Pytest.
- **CI/CD Pipeline:** Automated testing and deployment configuration using GitHub Actions.

## 🛠️ Technologies Used

| Technology | Purpose |
|---|---|
| Python | Backend programming |
| FastAPI | Backend framework and REST APIs |
| SQLModel | Database models and ORM |
| SQLite | Database |
| Jinja2 | HTML templates |
| HTML, CSS, JavaScript | Frontend development |
| Uvicorn | Application server |
| Pytest | Automated testing |
| Git & GitHub | Version control |
| GitHub Actions | CI/CD |
| Render & Vercel | Deployment configuration |

## 📁 Project Structure

```text
policydesk-starter/
│
├── api/
│   └── index.py
│
├── app/
│   ├── routers/
│   │   ├── claims.py
│   │   ├── customers.py
│   │   ├── pages.py
│   │   ├── policies.py
│   │   ├── products.py
│   │   └── quotes.py
│   │
│   ├── services/
│   │   └── pricing.py
│   │
│   ├── static/
│   ├── templates/
│   ├── db.py
│   ├── init_db.py
│   ├── main.py
│   ├── models.py
│   └── seed.py
│
├── data/
│   ├── seed_customers.csv
│   └── seed_products.csv
│
├── docs/
├── tests/
│
├── .github/
│   └── workflows/
│       └── ci.yml
│
├── check_setup.py
├── requirements.txt
├── pyproject.toml
├── render.yaml
├── vercel.json
└── README.md
```

## ⚙️ Installation and Setup

### Prerequisites

- Python 3.12 or later
- Git
- VS Code or any Python-supported code editor

### Step 1: Clone the repository

```bash
git clone https://github.com/YOUR-USERNAME/policydesk-starter.git
```

### Step 2: Open the project folder

```bash
cd policydesk-starter
```

### Step 3: Create a virtual environment

```bash
python -m venv .venv
```

### Step 4: Activate the virtual environment

For Windows PowerShell:

```powershell
.venv\Scripts\Activate.ps1
```

For macOS/Linux:

```bash
source .venv/bin/activate
```

### Step 5: Install dependencies

```bash
python -m pip install -r requirements.txt
```

### Step 6: Check the project setup

```bash
python check_setup.py
```

### Step 7: Run the application

```bash
python -m uvicorn app.main:app --reload
```

## 🌐 Application URLs

After starting the application, open these URLs in your browser:

| Service | URL |
|---|---|
| Main Application | http://127.0.0.1:8000 |
| API Documentation | http://127.0.0.1:8000/docs |
| Health Check | http://127.0.0.1:8000/health |

## 🔗 API Endpoints

| Method | Endpoint | Description |
|---|---|---|
| GET, POST | `/api/customers` | List and create customers |
| GET | `/api/customers/{customer_id}` | Retrieve customer details |
| GET | `/api/products` | List insurance products |
| GET | `/api/products/{product_id}` | Retrieve product details |
| GET, POST | `/api/quotes` | List and create quotations |
| GET | `/api/quotes/{quote_id}` | Retrieve quotation details |
| GET, POST | `/api/policies` | List and issue policies |
| GET | `/api/policies/{policy_id}` | Retrieve policy details |
| PATCH | `/api/policies/{policy_id}/status` | Update policy status |
| GET, POST | `/api/claims` | List and file claims |
| GET | `/api/claims/{claim_id}` | Retrieve claim details |
| PATCH | `/api/claims/{claim_id}/status` | Update claim status |
| GET | `/health` | Check application health |

## 💰 Premium Calculation

The application calculates insurance premiums using the following formula:

```text
Premium = Sum Insured × Base Rate
          × Age Factor
          × Tenure Factor
          × Add-on Factor
```

### Age Factor

| Age | Factor |
|---|---|
| Below 25 | 1.2 for Motor, 0.8 for other products |
| 25–45 | 1.0 |
| 46–60 | 1.3 |
| Above 60 | 1.6 |

### Tenure Factor

| Tenure | Factor |
|---|---|
| 1 Year | 1.0 |
| 2 Years | 0.95 |
| 3 Years | 0.90 |

### Available Add-ons

- Health: Critical Illness – 15%
- Motor: Zero Depreciation – 10%

The minimum premium is ₹1,000.

## 📋 Claims Management

The claims module supports:

- Filing insurance claims.
- Listing claims.
- Retrieving individual claim details.
- Filtering claims by status and policy.
- Reviewing claims.
- Approving or rejecting claims with a reason.

### Claim Status Workflow

```text
Filed
  |
  v
Under Review
  |
  +----------+
  |          |
  v          v
Approved   Rejected
```

### Claim Validation Rules

- Claims require a valid policy.
- Cancelled policies result in automatic rejection.
- Lapsed policies cannot be used to file claims.
- The incident date must fall within the policy period.
- Claim amounts must not exceed the remaining sum insured after approved claims.
- Motor claims require vehicle registration details.

## 🗄️ Database

PolicyDesk uses **SQLite** with SQLModel for database operations.

The application automatically creates database tables and loads sample data during startup.

Main database entities:

- Customer
- Product
- Quote
- Policy
- Claim

The local database file is `policydesk.db`.

## 🧪 Testing

The project uses Pytest for automated testing.

Run the following commands:

```bash
# Run smoke tests
pytest -m smoke

# Run regression tests
pytest -m regression

# Run all tests except lab tests
pytest -m "not lab"

# Run the complete test suite
pytest
```

Test files cover:

- Health checks
- Customer and application pages
- Quotation calculations
- Policy management
- Claims management
- Claims administration
- Regression testing

## 🔄 CI/CD Pipeline

The project includes a GitHub Actions workflow:

`.github/workflows/ci.yml`

The workflow performs:

1. Smoke testing.
2. Regression testing.
3. Running all non-lab tests.
4. Optional deployment to Render.
5. Optional deployment to Vercel.

Deployment requires the appropriate GitHub repository secrets.

## ☁️ Deployment

Deployment configuration is included for:

**Render**
- Configuration file: `render.yaml`
- Runs the FastAPI application using Uvicorn.
- Uses `/health` as the health-check endpoint.

**Vercel**
- Configuration file: `vercel.json`
- Application entry point: `api/index.py`
- Uses the Vercel Python service configuration.

## 📚 Documentation

Additional workshop documentation is available in the `docs/` directory:

- Workshop Guide
- Setup Guide
- Git Workflow
- Phase 2 Prompts
- Phase 3 Admin Approval
- Day 2 Quotation Calculator
- Day 2 Issue Policy
- Deployment Guide
- DBeaver Demo
- Workshop Handout

## 🔮 Future Enhancements

- User authentication and role-based access.
- Advanced analytics and reporting.
- AI-powered claim processing.
- Enhanced admin dashboard.
- Additional insurance products.
- Improved security and production database support.

## 👨‍💻 Project Credits

**TalentPath Academy**

AI-Powered SDLC Workshop

*Train. Learn. Grow. Succeed.*

---

⭐ If you find this project useful, feel free to explore the code and contribute!