# MLOP_Proj1
Project using complete MLOPS concepts

````
# 🚗 Vehicle Data Processing and ML Pipeline (End-to-End MLOps Project)

Welcome to the Vehicle Data MLOps project! This repository showcases a complete end-to-end machine learning workflow — from data ingestion to model deployment using CI/CD with Docker and AWS. The aim of this project is to demonstrate real-world MLOps practices using modern tools and clean code.

---

## 📦 Project Setup

### 1. 📁 Create Project Template
Run the following command to generate the project structure:
```bash
python template.py
````

### 2. ⚙️ Configure Project Packaging

* Add local package configurations to `setup.py` and `pyproject.toml`.
* For more info, refer to `crashcourse.txt`.

### 3. 🐍 Create Virtual Environment and Install Dependencies

```bash
conda create -n vehicle python=3.10 -y
conda activate vehicle
pip install -r requirements.txt
pip list  # Verify packages
```

---

## ☁️ MongoDB Atlas Setup

1. Create an account on [MongoDB Atlas](https://www.mongodb.com/cloud/atlas) and start a new project.
2. Create a cluster (M0 free tier) and set up DB username/password.
3. Whitelist IP as `0.0.0.0/0` for public access.
4. Get the connection string: **Drivers > Python > 3.6+**.
5. In Jupyter Notebook (`notebook/mongoDB_demo.ipynb`), push local dataset to MongoDB and confirm upload via Atlas UI.

---

## 🧾 Logging, Exceptions, and EDA

* Custom logging handled in `logger.py` (tested via `demo.py`).
* Exception handling added in `exception.py`.
* Notebooks for EDA and Feature Engineering are provided.

---

## 🛠️ Data Ingestion Module

### Key Steps:

* Define constants in `constants/__init__.py`.
* Setup MongoDB connection in `configuration/mongo_db_connection.py`.
* Fetch and transform data to pandas DataFrame using `data_access/proj1_data.py`.
* Define config and artifact entities in:

  * `entity/config_entity.py`
  * `entity/artifact_entity.py`
* Develop pipeline in `components/data_ingestion.py` and test via `demo.py`.

### 🔐 MongoDB URL Setup

#### Bash

```bash
export MONGODB_URL="mongodb+srv://<username>:<password>@cluster..."
echo $MONGODB_URL
```

#### PowerShell

```powershell
$env:MONGODB_URL="mongodb+srv://<username>:<password>@cluster..."
echo $env:MONGODB_URL
```

---

## 🧪 Data Validation, Transformation & Model Training

* Update `utils/main_utils.py` and `config/schema.yaml`.
* Build components for:

  * ✅ Data Validation
  * 🔄 Data Transformation (`entity/estimator.py`)
  * 🤖 Model Training (`entity/estimator.py`)

---

## 🌩️ AWS Setup for Model Evaluation

1. Create IAM User → Attach **AdministratorAccess** → Get **Access Keys**.
2. Set environment variables:

```bash
export AWS_ACCESS_KEY_ID="..."
export AWS_SECRET_ACCESS_KEY="..."
```

3. Create S3 Bucket:

   * Name: `my-model-mlopsproj`
   * Region: `ap-south-1`
   * Disable public access block

4. Update:

   * `constants/__init__.py`
   * `src/configuration/aws_connection.py`
   * `entity/s3_estimator.py` (push/pull model)

---

## 📈 Model Evaluation & Model Pusher

* Evaluate model performance and push the best model to AWS S3.

---

## 🔮 Prediction Pipeline

* Add `app.py` for API-based predictions.
* Add `templates/` and `static/` folders for the UI.

---

## ⚙️ CI/CD Pipeline with GitHub Actions & AWS

### Docker Setup

* Add `Dockerfile` and `.dockerignore`.

### GitHub Actions Workflow

* Create `.github/workflows/aws.yaml`.

### AWS ECR & EC2 Setup

1. Create IAM user (`usvisa-user`) → Get Access Keys
2. Create ECR repo (`vehicleproj`)
3. Launch EC2 (Ubuntu, 30GB, T2 Medium)
4. Install Docker on EC2:

```bash
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh
sudo usermod -aG docker ubuntu
newgrp docker
```

### Connect GitHub with EC2 (Self-Hosted Runner)

* GitHub → Settings → Actions → Runners → Add New
* Follow setup commands on EC2 (`./run.sh` to activate)

### Setup GitHub Secrets

```
AWS_ACCESS_KEY_ID
AWS_SECRET_ACCESS_KEY
AWS_DEFAULT_REGION
ECR_REPO
```

---

## 🚀 Deploy & Access

1. CI/CD runs on every push to GitHub.
2. EC2 inbound rule must allow port `5080`.
3. Open browser and visit:

```
http://<EC2-public-ip>:5080
```

---

## ✅ Final Notes

* Training route: `/training`
* Prediction route: `/predict`
* Add `"artifact/"` to `.gitignore` for clean version control

---

## 📚 Tech Stack

* Python, Pandas, Scikit-learn
* MongoDB Atlas
* AWS (S3, IAM, ECR, EC2)
* Docker, GitHub Actions
* Conda, Pip, PyYAML
* CI/CD and MLOps Best Practices

---

## 👨‍💻 Author

**\[sai vinay]** — Passionate about MLOps, Software Engineering & End-to-End System Design.
Let’s connect on [LinkedIn](www.linkedin.com/in/saivinay-palakurthy) or check out more projects on [GitHub](https://github.com/saivinay129).

---

