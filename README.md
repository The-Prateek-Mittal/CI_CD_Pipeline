# CI/CD Pipeline for Machine Learning Model Training

![Python](https://img.shields.io/badge/Python-3.10%2B-blue?logo=python)
![GitHub Actions](https://img.shields.io/badge/GitHub%20Actions-CI%2FCD-2088FF?logo=githubactions)
![Machine Learning](https://img.shields.io/badge/Machine%20Learning-Model%20Training-orange)
![Status](https://img.shields.io/badge/Status-Active-success)

A simple **Continuous Integration / Continuous Delivery (CI/CD) pipeline for a Machine Learning training workflow**, implemented using **Python and GitHub Actions**.

The project demonstrates how a machine learning training script can be automatically executed whenever changes are pushed to the main branch or a pull request is created.

---

## 📌 Project Overview

Machine Learning projects often require repetitive steps such as:

1. Installing dependencies
2. Preparing the development environment
3. Running the training code
4. Verifying that the training pipeline executes successfully

This project automates these steps using **GitHub Actions**.

Whenever code is pushed to the `main` branch, a GitHub Actions workflow automatically:

```text
Developer pushes code
        ↓
GitHub Repository
        ↓
GitHub Actions triggered
        ↓
Ubuntu Runner
        ↓
Python 3.10 Environment
        ↓
Install Dependencies
        ↓
Run train.py
        ↓
Training Pipeline Execution
```

The workflow can also be triggered by pull requests or manually through GitHub Actions.

---

## 🎯 Objectives

The main objectives of this project are:

* Implement a basic CI/CD workflow for an ML project
* Automate the Python environment setup
* Automatically install project dependencies
* Automatically execute the model training script
* Integrate machine learning workflows with GitHub Actions
* Demonstrate automation of repetitive ML development tasks

---

## 🛠️ Tech Stack

| Technology         | Purpose                            |
| ------------------ | ---------------------------------- |
| **Python**         | Model training and data processing |
| **NumPy**          | Numerical computation              |
| **Pandas**         | Data manipulation                  |
| **SciPy**          | Scientific computing               |
| **Scikit-learn**   | Machine learning                   |
| **Matplotlib**     | Visualization                      |
| **tqdm**           | Progress tracking                  |
| **GitHub Actions** | CI/CD automation                   |
| **Ubuntu**         | CI runner environment              |

The repository's dependency file currently specifies NumPy, Pandas, SciPy, Scikit-learn, Matplotlib and tqdm. TensorFlow and PyTorch are present as commented optional entries.

---

## 📂 Project Structure

```text
CI_CD_Pipeline/
│
├── .github/
│   └── workflows/
│       └── main.yml
│
├── train.py
│
├── requirements.txt
│
└── README.md
```

### `train.py`

Contains the machine learning model training workflow.

The current training script is based on a TensorFlow speech/keyword recognition training workflow and includes functionality for preparing audio data, configuring model parameters, training the model and evaluating training progress.

### `requirements.txt`

Contains the Python dependencies required by the project.

### `.github/workflows/main.yml`

Defines the GitHub Actions CI workflow responsible for automatically setting up the environment and executing the training script.

---

# ⚙️ CI/CD Workflow

The GitHub Actions workflow is configured to run when:

* Code is pushed to `main`
* A pull request targets `main`
* The workflow is manually triggered using `workflow_dispatch`

The workflow uses an Ubuntu runner and Python 3.10.

### Pipeline

```text
                 ┌─────────────────────┐
                 │   Developer Commit  │
                 └──────────┬──────────┘
                            │
                            ▼
                 ┌─────────────────────┐
                 │    GitHub Repo      │
                 └──────────┬──────────┘
                            │
                            ▼
                 ┌─────────────────────┐
                 │   GitHub Actions    │
                 └──────────┬──────────┘
                            │
                            ▼
                 ┌─────────────────────┐
                 │ Ubuntu Latest       │
                 │ Runner              │
                 └──────────┬──────────┘
                            │
                            ▼
                 ┌─────────────────────┐
                 │ Setup Python 3.10   │
                 └──────────┬──────────┘
                            │
                            ▼
                 ┌─────────────────────┐
                 │ Install Dependencies│
                 └──────────┬──────────┘
                            │
                            ▼
                 ┌─────────────────────┐
                 │    python train.py  │
                 └──────────┬──────────┘
                            │
                   ┌────────┴────────┐
                   ▼                 ▼
                Success             Failure
                   │                 │
                   ▼                 ▼
              CI Passes          CI Fails
```

---

# 🔄 GitHub Actions Configuration

The current workflow follows this general process:

```yaml
name: Model Training

on:
  push:
    branches: ["main"]

  pull_request:
    branches: ["main"]

  workflow_dispatch:

jobs:
  train:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout repository
        uses: actions/checkout@v4

      - name: Set up Python
        uses: actions/setup-python@v5
        with:
          python-version: '3.10'

      - name: Install dependencies
        run: |
          python -m pip install --upgrade pip
          if [ -f requirements.txt ]; then pip install -r requirements.txt; fi

      - name: Run training script
        run: python train.py
```

This configuration is implemented in the repository's `.github/workflows/main.yml`.

---

# 🚀 Getting Started

## 1. Clone the Repository

```bash
git clone https://github.com/The-Prateek-Mittal/CI_CD_Pipeline.git
```

Move into the project directory:

```bash
cd CI_CD_Pipeline
```

---

## 2. Create a Virtual Environment

### Windows

```bash
python -m venv venv
```

Activate it:

```bash
venv\Scripts\activate
```

### Linux / macOS

```bash
python3 -m venv venv
```

Activate it:

```bash
source venv/bin/activate
```

---

## 3. Upgrade pip

```bash
python -m pip install --upgrade pip
```

---

## 4. Install Dependencies

```bash
pip install -r requirements.txt
```

---

## 5. Run the Training Script

```bash
python train.py
```

> **Note:** The current `train.py` imports TensorFlow. Since TensorFlow is commented out in the current `requirements.txt`, a local TensorFlow installation may be required before running the script successfully.

For example:

```bash
pip install tensorflow
```

The exact TensorFlow version should be selected according to the Python version and execution environment being used.

---

# 🤖 Continuous Integration

The CI pipeline automatically performs the following steps:

### Step 1 — Checkout

GitHub Actions checks out the latest version of the repository.

```yaml
uses: actions/checkout@v4
```

### Step 2 — Python Setup

The workflow creates a Python environment using Python 3.10.

```yaml
uses: actions/setup-python@v5
```

### Step 3 — Dependency Installation

The workflow upgrades pip and installs packages from `requirements.txt`.

```bash
python -m pip install --upgrade pip
pip install -r requirements.txt
```

### Step 4 — Model Training

The training script is executed automatically.

```bash
python train.py
```

If the training process exits successfully, the GitHub Actions job passes.

---

# 🧠 Machine Learning Component

The repository contains a speech/keyword recognition training workflow.

The training script is based on a TensorFlow speech recognition example and is designed around **keyword spotting**, rather than full unrestricted speech recognition.

The original training workflow supports a small vocabulary of keywords such as:

```text
yes
no
up
down
left
right
on
off
stop
go
```

The training process works with short audio samples and converts the audio into features that can be supplied to a neural-network model.

---

# 🔊 Keyword Spotting Concept

The overall ML pipeline can be represented as:

```text
Audio Dataset
      │
      ▼
Audio Preprocessing
      │
      ▼
Feature Extraction
      │
      ▼
Training Data
      │
      ▼
Neural Network
      │
      ▼
Model Training
      │
      ▼
Evaluation
      │
      ▼
Trained Speech/Keyword Model
```

This makes the project particularly relevant to **TinyML, embedded AI and speech recognition applications**.

---

# 🔁 CI/CD for Machine Learning

Traditional software CI/CD usually looks like:

```text
Code
 ↓
Build
 ↓
Test
 ↓
Deploy
```

For a Machine Learning project, the workflow can be extended to:

```text
Code / Data
     ↓
Dependency Setup
     ↓
Data Processing
     ↓
Model Training
     ↓
Model Evaluation
     ↓
Model Validation
     ↓
Model Deployment
```

This repository demonstrates the foundation of this process by automatically executing the training workflow through GitHub Actions.

---

# 📈 Future Improvements

The current pipeline can be extended into a more complete **MLOps pipeline**.

Possible improvements include:

### 1. Automated Testing

Add unit tests and execute them automatically:

```bash
pytest
```

### 2. Model Evaluation

Automatically calculate metrics such as:

* Accuracy
* Precision
* Recall
* F1-score

### 3. Model Validation

The pipeline can reject a newly trained model if its performance falls below a predefined threshold.

Example:

```text
Accuracy < 90%
      ↓
Pipeline Failed
```

### 4. Experiment Tracking

Integrate tools such as:

* MLflow
* Weights & Biases

to track:

* Hyperparameters
* Model versions
* Training metrics
* Experiments

### 5. Model Versioning

Store trained model artifacts using:

* Git LFS
* DVC
* Cloud object storage

### 6. Dockerization

Package the training environment into a Docker container.

```text
GitHub
   ↓
GitHub Actions
   ↓
Docker Build
   ↓
Model Training
   ↓
Model Artifact
```

### 7. Cloud Deployment

The trained model could eventually be deployed using cloud infrastructure such as:

* AWS EC2
* AWS S3
* AWS SageMaker
* Kubernetes

---

# 🔐 Reproducibility

A major advantage of using CI/CD for machine learning is reproducibility.

Instead of manually configuring an environment every time, the pipeline defines:

```text
Python Version
      +
Dependencies
      +
Training Script
      =
Reproducible Training Environment
```

This reduces environment-related inconsistencies between development machines and CI runners.

---

# 📊 Current Pipeline

| Stage                   | Implementation               |
| ----------------------- | ---------------------------- |
| Source Control          | GitHub                       |
| CI/CD                   | GitHub Actions               |
| Operating System        | Ubuntu                       |
| Python                  | 3.10                         |
| Dependency Installation | `requirements.txt`           |
| ML Training             | `train.py`                   |
| Trigger                 | Push / Pull Request / Manual |
| Model Deployment        | Not currently implemented    |
| Experiment Tracking     | Not currently implemented    |
| Model Registry          | Not currently implemented    |

---

# 🧪 How to Trigger the Pipeline

## Automatically

Push a change to the `main` branch:

```bash
git add .
git commit -m "Update training pipeline"
git push origin main
```

GitHub Actions will automatically start the workflow.

---

## Pull Request

Create a pull request targeting:

```text
main
```

The workflow will run automatically.

---

## Manual Trigger

You can also manually run the workflow:

```text
GitHub Repository
      ↓
Actions
      ↓
Model Training
      ↓
Run workflow
```

The repository's workflow explicitly enables `workflow_dispatch` for this purpose.

---

# 📁 Important Files

| File                         | Description                      |
| ---------------------------- | -------------------------------- |
| `.github/workflows/main.yml` | GitHub Actions CI workflow       |
| `train.py`                   | Machine learning training script |
| `requirements.txt`           | Python dependencies              |
| `README.md`                  | Project documentation            |

---

# 🎓 Learning Outcomes

This project demonstrates practical understanding of:

* Continuous Integration
* Continuous Delivery concepts
* GitHub Actions
* Python environment management
* Dependency management
* Machine Learning workflows
* Automated model training
* Keyword spotting
* Reproducible ML workflows
* Introduction to MLOps

---

# 👨‍💻 Author

**Prateek Mittal**

B.Tech — Computing and Data Science

GitHub: [The-Prateek-Mittal](https://github.com/The-Prateek-Mittal)

LinkedIn: [Prateek Mittal](https://www.linkedin.com/in/prateek-mittal-75278b206)

---

# ⭐ Acknowledgements

The speech/keyword recognition training implementation is based on the TensorFlow speech recognition example and documentation.

The CI/CD automation is implemented using GitHub Actions.

---

# 📜 License

This repository contains a machine learning training workflow and supporting CI/CD configuration.

Please refer to the original source files and their respective licenses for third-party components included in the project.

---

## ⭐ If you find this project useful

Consider starring the repository and exploring the workflow to understand how machine learning training can be integrated into a CI/CD pipeline.
