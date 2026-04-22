# Insurance Prediction Model

<p align="center">
  <img src="https://img.shields.io/badge/Python-3.10%2B-blue?style=for-the-badge&logo=python&logoColor=white" />
  <img src="https://img.shields.io/badge/FastAPI-0.115-009688?style=for-the-badge&logo=fastapi&logoColor=white" />
  <img src="https://img.shields.io/badge/scikit--learn-1.6.1-F7931E?style=for-the-badge&logo=scikit-learn&logoColor=white" />
  <img src="https://img.shields.io/badge/Pydantic-v2-E92063?style=for-the-badge&logo=pydantic&logoColor=white" />
  <img src="https://img.shields.io/badge/License-MIT-green?style=for-the-badge" />
</p>

<p align="center">
  A production-ready REST API that predicts insurance charges based on demographic and health-related features, powered by a scikit-learn machine learning model and served via FastAPI.
</p>

---

## Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Project Structure](#project-structure)
- [Tech Stack](#tech-stack)
- [Getting Started](#getting-started)
  - [Prerequisites](#prerequisites)
  - [Installation](#installation)
  - [Running the API](#running-the-api)
- [API Reference](#api-reference)
- [Model Details](#model-details)
- [Configuration](#configuration)
- [Contributing](#contributing)
- [License](#license)

---

## Overview

This project provides an end-to-end machine learning pipeline for **insurance charge prediction**. Given a set of individual health and demographic attributes, the model estimates the expected insurance cost. The trained model is exposed through a clean **FastAPI** REST interface with Pydantic-powered input validation and a structured project layout ready for deployment.

---

## Features

- **REST API** — Fast, async HTTP endpoints via FastAPI and Uvicorn
- **Input Validation** — Schema-enforced request bodies using Pydantic v2
- **ML Pipeline** — scikit-learn model trained on insurance data with preprocessing
- **Modular Architecture** — Separate `config/`, `model/`, and `schema/` directories for clean separation of concerns
- **Interactive Docs** — Auto-generated Swagger UI at `/docs` and ReDoc at `/redoc`
- **Production-Ready** — Structured for easy containerization and deployment

---

## Project Structure

```
insurance-prediction-model/
│
├── app.py                  # FastAPI application entry point
├── requirements.txt        # Pinned Python dependencies
│
├── config/                 # App configuration (paths, hyperparameters, settings)
│
├── model/                  # Serialized trained model artifact(s)
│
└── schema/                 # Pydantic request/response schemas
```

---

## Tech Stack

| Layer | Technology |
|---|---|
| **API Framework** | FastAPI 0.115, Starlette, Uvicorn |
| **ML / Data** | scikit-learn 1.6.1, pandas 2.2.3, numpy 2.2.6, scipy |
| **Validation** | Pydantic v2 |
| **Serialization** | joblib |
| **Visualization** | Altair 5.5, pydeck |
| **Utilities** | python-dateutil, pytz, packaging |

---

## Getting Started

### Prerequisites

- Python **3.10** or higher
- `pip` package manager
- (Optional) A virtual environment tool such as `venv` or `conda`

### Installation

**1. Clone the repository**

```bash
git clone https://github.com/waleeedjaved/insurance-prediction-model.git
cd insurance-prediction-model
```

**2. Create and activate a virtual environment**

```bash
# Using venv
python -m venv venv

# Activate (Linux / macOS)
source venv/bin/activate

# Activate (Windows)
venv\Scripts\activate
```

**3. Install dependencies**

```bash
pip install -r requirements.txt
```

### Running the API

```bash
uvicorn app:app --reload
```

The API will be available at:

| URL | Description |
|---|---|
| `http://127.0.0.1:8000` | Base URL |
| `http://127.0.0.1:8000/docs` | Swagger UI (interactive) |
| `http://127.0.0.1:8000/redoc` | ReDoc documentation |

---

## API Reference

### `GET /`

Health check — returns a status message confirming the API is running.

**Response**

```json
{
  "message": "Insurance Prediction API is running."
}
```

---

### `POST /predict`

Predicts the insurance charge for a given individual.

**Request Body**

```json
{
  "age": 35,
  "sex": "male",
  "bmi": 27.5,
  "children": 2,
  "smoker": "no",
  "region": "southwest"
}
```

| Field | Type | Description |
|---|---|---|
| `age` | `int` | Age of the individual |
| `sex` | `string` | `"male"` or `"female"` |
| `bmi` | `float` | Body Mass Index |
| `children` | `int` | Number of dependents |
| `smoker` | `string` | `"yes"` or `"no"` |
| `region` | `string` | `"northeast"`, `"northwest"`, `"southeast"`, `"southwest"` |

**Response**

```json
{
  "predicted_charge": 7842.63
}
```

> **Note:** Exact field names and response shape may vary. Refer to the `/docs` endpoint after running the server for the live, auto-generated schema.

---

## Model Details

The predictive model is built using **scikit-learn** and follows a standard supervised regression pipeline:

- **Target variable:** Insurance charge (continuous)
- **Features:** Age, sex, BMI, number of children, smoker status, region
- **Preprocessing:** Categorical encoding (e.g., `sex`, `smoker`, `region`) and numerical scaling
- **Algorithm:** Regression model — see `model/` directory for the serialized artifact
- **Serialization:** Model persisted with `joblib` for fast loading at inference time

---

## Configuration

Application-level settings (model paths, feature lists, column names, etc.) are managed in the `config/` directory, keeping environment-specific values decoupled from application logic.

To change the model artifact location or feature configuration, update the relevant file inside `config/` rather than modifying `app.py` directly.

---

## Contributing

Contributions are welcome. To get started:

1. Fork the repository
2. Create a feature branch: `git checkout -b feature/your-feature-name`
3. Commit your changes: `git commit -m "feat: add your feature"`
4. Push to the branch: `git push origin feature/your-feature-name`
5. Open a Pull Request

Please make sure your code follows Python best practices and all existing functionality remains intact.

---

## License

This project is licensed under the [MIT License](LICENSE).

---

<p align="center">
  Made with care by <a href="https://github.com/waleeedjaved">waleeedjaved</a>
</p>
