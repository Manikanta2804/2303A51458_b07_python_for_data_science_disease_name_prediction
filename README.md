# Disease Name Prediction — Distributed ML System

A distributed machine-learning system for predicting disease names from clinical or medical data. This project demonstrates building scalable prediction pipelines using a mix of languages and technologies (Python, Java, C++, React, SQL) and distributed training/inference components.

## Table of Contents
- [Project Overview](#project-overview)
- [Key Features](#key-features)
- [Architecture](#architecture)
- [Tech Stack](#tech-stack)
- [Getting Started](#getting-started)
  - [Prerequisites](#prerequisites)
  - [Install](#install)
  - [Run Locally](#run-locally)
- [Dataset & Preprocessing](#dataset--preprocessing)
- [Training](#training)
- [Inference / API](#inference--api)
- [Evaluation](#evaluation)
- [Deployment](#deployment)
- [Contributing](#contributing)
- [License](#license)
- [Contact](#contact)

## Project Overview
This repository implements a distributed system that trains and serves models to predict disease names from input data (structured records, clinical notes, or feature vectors). The system is built for scale and speed, using distributed training and inference components, and focuses on practical concerns like data handling, model accuracy, and operational scalability.

## Key Features
- End-to-end pipeline: data ingestion → preprocessing → training → evaluation → serving
- Distributed training support (multi-node / multi-GPU)
- Microservices architecture with separate inference and frontend components
- Persistent storage using relational databases for datasets and results
- Modular code: Python for ML, Java/C++ for high-performance components, React for UI

## Architecture
- Data storage: Relational DB (Postgres / MySQL) for raw data and metadata
- Feature engineering & preprocessing: Python (pandas, sklearn)
- Model training: Python (PyTorch or TensorFlow) with distributed training orchestration
- High-performance components: C++ / Java modules (optional) for low-latency processing
- API / Serving: Python (FastAPI / Flask) or Java service
- Frontend: React app for visualization and interactive inference

A typical flow:
1. Data ingestion into the DB
2. Preprocessing & feature extraction (batch jobs)
3. Distributed training of models
4. Model registry / checkpoint storage
5. Model serving via REST endpoints
6. Frontend interacts with APIs for predictions and monitoring

## Tech Stack
- Languages: Python, Java, C++
- Frontend: React
- DB: PostgreSQL / MySQL (SQL)
- ML: PyTorch or TensorFlow (configurable)
- Serving: FastAPI / Flask (Python) or Java-based server
- Orchestration: Docker, Kubernetes (optional for production)
- CI/CD: GitHub Actions (recommended)

## Getting Started

### Prerequisites
- Python 3.8+
- Node.js 16+ / npm or yarn
- Java 11+ (if using Java components)
- C++ toolchain for native modules (gcc/clang + CMake)
- PostgreSQL or MySQL database
- Docker (recommended for containerized setup)

### Install
1. Clone the repository:
   git clone https://github.com/Manikanta2804/2303A51458_b07_python_for_data_science.git
2. Backend (Python) dependencies:
   cd backend
   python -m venv venv
   source venv/bin/activate
   pip install -r requirements.txt
3. Frontend:
   cd frontend
   npm install

(Adjust steps to your repo layout; create `requirements.txt` and `package.json` if not present.)

### Run Locally
1. Start the database and configure connection string in `backend/config.yml` or environment variables:
   - Example env:
     DATABASE_URL=postgresql://user:pass@localhost:5432/diseasedb
2. Run backend API:
   cd backend
   uvicorn app.main:app --reload --host 0.0.0.0 --port 8000
3. Run frontend:
   cd frontend
   npm start

## Dataset & Preprocessing
- Place raw datasets in `data/raw/` (or configure storage).
- Supported data types: CSV/TSV structured records, JSON, and text notes.
- Preprocessing steps:
  - Cleaning & normalization (handle missing values, standardize fields)
  - Tokenization & text cleaning for clinical notes
  - Feature extraction (one-hot, embeddings, numerical scaling)
  - Save processed features to `data/processed/` or to DB tables

Note: Always ensure patient privacy & compliance (de-identify data before pushing to this repo).

## Training
- Use the training script in `backend/train/` (e.g., `train.py`) to launch experiments.
- For distributed training:
  - Use PyTorch DistributedDataParallel or TF MultiWorkerMirroredStrategy.
  - Launch with an orchestration (SLURM, Kubernetes, or torch.distributed.launch).
- Example (single-node):
  python backend/train/train.py --config configs/default.yaml
- Example (torch DDP):
  python -m torch.distributed.run --nproc_per_node=4 backend/train/train.py --config configs/ddp.yaml

Model checkpoints are saved to `models/` and optionally to a model registry.

## Inference / API
- The serving API exposes endpoints for prediction:
  - POST /predict
    - Body: JSON payload with features or text
    - Response: predicted disease name + confidence score
  - GET /health
    - Response: service status
- Example:
  curl -X POST http://localhost:8000/predict -H "Content-Type: application/json" -d '{"features": {...}}'

Integrate the frontend to call these endpoints for interactive predictions.

## Evaluation
- Metrics to track: accuracy, precision, recall, F1-score, top-k accuracy, confusion matrix
- Use an evaluation script `backend/eval/evaluate.py` to compute metrics on test sets.
- Maintain experiment logs (e.g., TensorBoard, MLflow) for reproducibility.

## Deployment
- Containerize services with Docker:
  - Backend Dockerfile, Frontend Dockerfile
- Use Kubernetes for scaling:
  - Deploy training workers as Jobs or StatefulSets for model training
  - Deploy API as Deployment with HorizontalPodAutoscaler for inference
- Persist models and data using network-attached storage or object store (S3-compatible)

## Contributing
Contributions are welcome. Suggested workflow:
1. Fork the repo
2. Create a feature branch: git checkout -b feat/your-feature
3. Make changes and add tests
4. Open a pull request describing the changes

Please follow the code style in existing modules and include tests for new functionality.

## License
This project is provided under the MIT License. See LICENSE file for details.

## Contact
Author: Manikanta2804  
GitHub: https://github.com/Manikanta2804

If you want, I can:
- Commit this README.md to the repository, or
- Customize sections (detailed setup steps, exact scripts, or add a model card and dataset license) based on files already present in the repo.
