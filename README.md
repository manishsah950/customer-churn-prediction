# Customer Churn Prediction & Retention Management System (ChurnGuard AI)

[![FastAPI](https://img.shields.io/badge/Backend-FastAPI-009688.svg?style=flat&logo=fastapi)](https://fastapi.tiangolo.com)
[![React](https://img.shields.io/badge/Frontend-React%2019%20%2B%20TypeScript-61DAFB.svg?style=flat&logo=react)](https://react.dev)
[![Tailwind CSS](https://img.shields.io/badge/Styling-Tailwind%20CSS-38B2AC.svg?style=flat&logo=tailwind-css)](https://tailwindcss.com)
[![Scikit-Learn](https://img.shields.io/badge/ML-Scikit--Learn-F7931E.svg?style=flat&logo=scikit-learn)](https://scikit-learn.org)
[![Python](https://img.shields.io/badge/Python-3.13-3776AB.svg?style=flat&logo=python)](https://python.org)
[![License](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)

An enterprise-grade, full-stack predictive SaaS platform that predicts customer churn probabilities, diagnoses localized risk factors, organizes human-in-the-loop retention campaigns, and tracks financial impact.

---

## 🌟 Key Capabilities

1. **Executive Churn Dashboard**: Real-time aggregated KPIs (Active Customers, Observed Churn Rate, High Risk Customers, Revenue at Risk, Retention Success Rate, Recharts tenure cohort trends).
2. **Leak-Free Machine Learning Pipeline**: Automated preprocessing pipeline (median numeric imputation, StandardScaler, OneHotEncoder) strictly fitted on training folds.
3. **Competitive Model Registry**: Compare **Random Forest**, **Logistic Regression**, and **Gradient Boosting** side-by-side using holdout test metrics (Accuracy, Precision, Recall, F1, ROC-AUC, PR-AUC, Confusion Matrix).
4. **Controlled Active Model Deployment**: Single-click activation of validated models into the real-time production inference registry.
5. **Interactive Single Prediction Engine**: Dynamic customer parameter form producing real-time probability scores, risk tiers, key risk drivers, protective factors, and suggested human-in-the-loop interventions.
6. **High-Throughput Batch Scoring**: Upload customer CSV files for automated batch inference, summary analytics, and downloadable scored records.
7. **Customer Directory & Risk Segmentation**: Searchable directory with sorting by churn score, risk tier filters, and manager assignment modal.
8. **Retention Campaign Management**: Create campaigns targeting high-risk cohorts, auto-enroll matching customers, record outreach activities (calls, discounts, extensions), and track conversion ROI.
9. **Role-Based Access Control (RBAC)**: JWT authentication with direct bcrypt hashing enforcing permissions for `Admin`, `Business Analyst`, and `Retention Manager`.
10. **Automated Testing Suite**: 16 Pytest backend tests and 3 Vitest frontend tests with 100% pass rates.

---

## 🛠️ Technology Stack

| Layer | Technologies |
|---|---|
| **Frontend** | React 19, Vite 8, TypeScript 5.8, Tailwind CSS, Recharts, Lucide React, Axios, React Router v7 |
| **Backend** | Python 3.13, FastAPI, Pydantic v2, SQLAlchemy 2.0, Uvicorn, Bcrypt, PyJWT |
| **Machine Learning** | Scikit-learn, Pandas, NumPy, Joblib, Permutation Feature Importance |
| **Databases** | SQLite (Zero-config local development) / PostgreSQL 15 (Production Docker) |
| **DevOps & QA** | Docker, Docker Compose, Pytest, Vitest, React Testing Library |

---

## 🚀 Quick Start Guide

### Prerequisites
- **Python 3.10+** (Python 3.13 supported)
- **Node.js v18+** and **npm**
- **Git**

---

### Step 1: Clone the Repository
```bash
git clone https://github.com/your-username/customer-churn-system.git
cd customer-churn-system
```

---

### Step 2: Backend Setup & Database Seeding

#### On Windows (PowerShell):
```powershell
# 1. Install backend dependencies
python -m pip install -r backend/requirements.txt

# 2. Seed database, train baseline ML models, and populate sample records
python scripts/seed_data.py

# 3. Start the FastAPI backend server
$env:PYTHONPATH="backend;."
python -m uvicorn app.main:app --host 127.0.0.1 --port 8000 --reload
```

#### On Linux / macOS (Bash):
```bash
# 1. Create and activate virtual environment (optional)
python3 -m venv venv
source venv/bin/activate

# 2. Install backend dependencies
pip install -r backend/requirements.txt

# 3. Seed database and train models
python scripts/seed_data.py

# 4. Start the FastAPI backend server
export PYTHONPATH="backend:."
uvicorn app.main:app --host 127.0.0.1 --port 8000 --reload
```

The backend REST API will now be running at:
- **API Server**: `http://127.0.0.1:8000`
- **Swagger Documentation**: `http://127.0.0.1:8000/docs`
- **Health Check**: `http://127.0.0.1:8000/health`

---

### Step 3: Frontend Setup

Open a **new terminal window**:

```bash
cd frontend

# 1. Install node dependencies
npm install

# 2. Start the Vite development server
npm run dev
```

The frontend application will now be running at:
- **Web App**: `http://localhost:5173`

---

## 🔐 Default Demo Login Credentials

The system includes pre-seeded user accounts for testing Role-Based Access Control:

| Role | Email Address | Password | Permissions |
|---|---|---|---|
| **System Admin** | `admin@churnguard.com` | `Admin@123456` | Full access (Users, Datasets, Models, Settings, Audit Logs) |
| **Business Analyst** | `analyst@churnguard.com` | `Analyst@123456` | Datasets, Model Training, Comparison, Inferences |
| **Retention Manager** | `manager@churnguard.com` | `Manager@123456` | Customer Assignments, Retention Campaigns, Outreach |

*(Quick-login buttons are provided directly on the `/login` screen for fast testing!)*

---

## 🧪 Running Automated Tests

### 1. Backend Tests (Pytest)
Runs 16 isolated tests covering auth, ML pipeline, single/batch prediction, customer directory filters, campaigns, and reports:
```powershell
# Windows PowerShell
$env:PYTHONPATH="backend;."
python -m pytest backend/tests -v
```
```bash
# Linux / macOS
export PYTHONPATH="backend:."
pytest backend/tests -v
```

### 2. Frontend Tests (Vitest)
Runs component tests covering login forms, role navigation, and documentation:
```bash
cd frontend
npm test
```

### 3. Production Frontend Build
Verifies that all TypeScript types and Tailwind CSS bundles compile with zero errors:
```bash
cd frontend
npm run build
```

---

## 🐳 Docker Deployment

To launch the complete multi-container stack (React Frontend + FastAPI Backend + PostgreSQL Database):

```bash
docker-compose up --build
```

Access points:
- Frontend: `http://localhost:5173`
- Backend API: `http://localhost:8000/docs`
- PostgreSQL: `localhost:5432`

---

## 📊 Experimental Model Evaluation Results

Results generated through actual execution on the benchmark Telco churn dataset:

| Model Version | Algorithm | Accuracy | Precision | Recall | F1-Score | ROC-AUC | Status |
|---|---|---|---|---|---|---|---|
| **v1.0.0** | **Random Forest** | **76.67%** | **61.2%** | **68.8%** | **0.648** | **0.8366** | **ACTIVE** |
| **v1.1.0** | **Logistic Regression** | 77.00% | 60.5% | 72.0% | 0.658 | 0.8443 | Archived |
| **v1.2.0** | **Gradient Boosting** | 77.33% | 62.5% | 67.7% | 0.650 | 0.8313 | Archived |

---

## 📁 Repository Structure

```
customer-churn-system/
├── backend/
│   ├── app/
│   │   ├── api/v1/endpoints/  # Auth, Dashboard, Customers, Models, Campaigns, etc.
│   │   ├── core/              # Config, Security (Bcrypt, JWT), Database session
│   │   ├── ml/                # Preprocessor, Trainer, Evaluator, Explainer, Registry
│   │   ├── models/            # SQLAlchemy database entities
│   │   ├── schemas/           # Pydantic v2 validation models
│   │   └── main.py            # FastAPI entry point
│   ├── tests/                 # Complete Pytest test suite
│   ├── Dockerfile
│   └── requirements.txt
├── frontend/
│   ├── src/
│   │   ├── components/        # ProtectedRoute, UI components
│   │   ├── context/           # AuthContext (JWT session state)
│   │   ├── layouts/           # DashboardLayout (Dark navy sidebar)
│   │   ├── pages/             # 17 complete application pages
│   │   ├── services/          # Axios REST API client
│   │   ├── test/              # Vitest test suite
│   │   └── types/             # TypeScript definitions
│   ├── Dockerfile
│   └── package.json
├── data/
│   ├── telco_churn_sample.csv # 1,500 record benchmark dataset
│   └── README.md
├── docs/
│   ├── architecture.md        # Architecture diagrams & component design
│   ├── database_er.md         # Database ER diagram & schema dictionary
│   ├── data_flow.md           # DFD Level 0, 1, and 2 diagrams
│   ├── college_project_report.md # Formal final-year project report
│   └── viva_questions_answers.md # 30 Technical viva questions & answers
├── ml/artifacts/              # Trained .joblib model artifacts
├── scripts/
│   ├── generate_sample_data.py # Telco data generator
│   └── seed_data.py           # Database seeder & baseline model trainer
├── docker-compose.yml
├── .env.example
├── .gitignore
└── README.md
```

---

## 🎓 College Submission & Viva Deliverables

Detailed college submission assets are prepared under the [`docs/`](file:///c:/Users/asham/OneDrive/Desktop/projects/customer-churn-system/docs) folder:
- **System Architecture**: [`docs/architecture.md`](file:///c:/Users/asham/OneDrive/Desktop/projects/customer-churn-system/docs/architecture.md)
- **Database ER Diagram**: [`docs/database_er.md`](file:///c:/Users/asham/OneDrive/Desktop/projects/customer-churn-system/docs/database_er.md)
- **Data Flow Diagrams (DFD)**: [`docs/data_flow.md`](file:///c:/Users/asham/OneDrive/Desktop/projects/customer-churn-system/docs/data_flow.md)
- **Project Report**: [`docs/college_project_report.md`](file:///c:/Users/asham/OneDrive/Desktop/projects/customer-churn-system/docs/college_project_report.md)
- **Viva Questions & Answers**: [`docs/viva_questions_answers.md`](file:///c:/Users/asham/OneDrive/Desktop/projects/customer-churn-system/docs/viva_questions_answers.md)

---

## ⚖️ License
This project is open-source and available under the [MIT License](LICENSE).
