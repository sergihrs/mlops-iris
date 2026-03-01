# Iris MLOps: End-to-End Production ML Pipeline

A professional-grade MLOps repository demonstrating a complete lifecycle for machine learning models, from data versioning and reproducible training to containerized orchestration and live monitoring.

## 🚀 Key Highlights & Technologies

- **Core Logic:** Robust **Python** implementation for data processing and modeling.
- **Orchestration & Deployment:** Containerized services using **Docker** and **Docker Compose**, with production-ready manifests for **Kubernetes (GKE)**.
- **Reproducibility:** Rigorous data and pipeline versioning using **DVC** (Data Version Control) and **DAGsHub**.
- **Experiment Tracking:** Systematized logging of parameters, metrics, and artifacts via **MLflow**.
- **CI/CD & Automation:** Integrated **GitHub Actions** with **CML** (Continuous Machine Learning) for automated reporting on pull requests.
- **Observability:** Full-stack monitoring using **Prometheus** and **Grafana** to track model performance and API health in real-time.
- **API Layer:** Scalable **REST API** built with **Flask**, providing low-latency inference endpoints.
- **User Interface:** Interactive **Streamlit** dashboard for intuitive model interaction and data visualization.

---

## 📁 Project Structure

```bash
├── .github/workflows/    # CI/CD pipelines (CML & GKE Deployment)
├── data/                 # Data directory (versioned by DVC)
├── grafana-provisioning/ # Automated Grafana datasource configuration
├── api-deployment.yaml   # K8s Deployment for the Inference API
├── web-deployment.yaml   # K8s Deployment for the Streamlit UI
├── app.py                # Flask REST API
├── app_web.py            # Streamlit Dashboard
├── train.py              # MLflow-integrated training script
├── dvc.yaml              # DVC pipeline definition
├── docker-compose.yml    # Local multi-container orchestration
└── prometheus.yml        # Monitoring configuration

```

---

## ⚙️ Installation & Setup

### Prerequisites

- Python 3.11+
- Docker & Docker Compose
- DVC

### 1. Clone & Environment

```bash
git clone <repository-url>
cd mlops-iris
python -m venv venv
source venv/bin/activate # venv\Scripts\activate on Windows
pip install -r requirements.txt

```

### 2. Data Retrieval

This project uses DVC for data reproducibility. To pull the dataset:

```bash
dvc pull

```

### 3. Training & Pipeline

Run the reproducible pipeline defined in `dvc.yaml`:

```bash
dvc repro

```

This script will:

1. Validate data existence.
2. Train a **Random Forest** model (configured in `params.yaml`).
3. Log metrics and artifacts (like the confusion matrix) to **MLflow**.

---

## 🚀 Deployment

### Local Orchestration (Docker Compose)

To spin up the entire stack (API, Web UI, Prometheus, and Grafana) locally:

```bash
docker-compose up --build

```

- **API:** [http://localhost:5000](https://www.google.com/search?q=http://localhost:5000)
- **Web UI:** [http://localhost:8501](https://www.google.com/search?q=http://localhost:8501)
- **Prometheus:** [http://localhost:9090](https://www.google.com/search?q=http://localhost:9090)
- **Grafana:** [http://localhost:3000](https://www.google.com/search?q=http://localhost:3000) (Admin pwd: `admin`)

### Production (Kubernetes)

The repository includes ready-to-use manifests for GKE deployment:

```bash
kubectl apply -f api-service.yaml -f api-deployment.yaml
kubectl apply -f web-service.yaml -f web-deployment.yaml

```

---

## 📊 Monitoring & Observability

The system is designed with a "production-first" mentality:

- **Metrics:** `app.py` exposes a `/metrics` endpoint for Prometheus.
- **Tracking:** Every prediction is tracked by species to monitor for potential data drift or class imbalance via the Grafana dashboard.
- **CI/CD:** Automated CML reports provide instant feedback on model accuracy shifts during code reviews.

---

## 🤝 Collaborative Workflow

This project follows industry best practices for collaborative data science:

- **GitHub Actions:** Automates the testing and deployment lifecycle.
- **Code Review:** Consistent use of CML ensures that every PR is accompanied by a performance report.
- **Documentation:** Clear separation of concerns and well-typed Python code for maintainability.
