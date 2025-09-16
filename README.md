# Vehicle Insurance Domain

[![Project Demo Video](https://img.youtube.com/vi/VIDEO_ID/0.jpg)](project_demo_video.mp4)

A complete end-to-end machine learning project for vehicle insurance prediction, featuring data ingestion, validation, transformation, model training, evaluation, deployment, and CI/CD integration with AWS and Docker.

## Project Structure & Setup

### 1. Project Template
- Generate the initial project structure by running `template.py`.

### 2. Local Package Management
- Use `setup.py` and `pyproject.toml` to import local packages.
- For more details, refer to `crashcourse.txt`.

### 3. Environment Setup
- Create and activate a virtual environment:
  ```bash
  conda create -n vehicle python=3.10 -y
  conda activate vehicle
  pip install -r requirements.txt
  ```
- Verify installed packages with `pip list`.

## MongoDB Atlas Integration
1. Sign up and create a new project in MongoDB Atlas.
2. Create a cluster (M0), set up DB user, and configure network access (`0.0.0.0/0`).
3. Obtain the connection string for Python and set it as an environment variable:
   ```bash
   export MONGODB_URL="mongodb+srv://<username>:<password>@..."
   echo $MONGODB_URL
   ```
4. Add your dataset to the `notebook` folder and push data to MongoDB using a Jupyter notebook (`mongoDB_demo.ipynb`).
5. Verify data in MongoDB Atlas collections.

## Logging, Exception Handling, and Notebooks
- Implement logging and exception handling in `logger` and `exception` modules, tested via `demo.py`.
- Perform EDA and feature engineering in Jupyter notebooks.

## Data Ingestion
- Define constants in `src/constants/__init__.py`.
- Configure MongoDB connection in `src/configuration/mongo_db_connection.py`.
- Fetch and transform data in `src/data_access/proj1_data.py`.
- Define config and artifact entities in `src/entity/config_entity.py` and `src/entity/artifact_entity.py`.
- Implement ingestion logic in `src/components/data_ingestion.py` and integrate with the training pipeline.

## Data Validation, Transformation & Model Training
- Add dataset schema info to `config/schema.yaml` and utility functions to `src/utils/main_utils.py`.
- Implement validation, transformation, and training components following the ingestion workflow.
- Add estimator classes to `src/entity/estimator.py`.

## AWS S3 Integration & Model Management
- Set up AWS IAM user and S3 bucket (`my-model-mlopsproj`).
- Store AWS credentials as environment variables:
  ```bash
  export AWS_ACCESS_KEY_ID="..."
  export AWS_SECRET_ACCESS_KEY="..."
  ```
- Add S3 configuration to `src/configuration/aws_connection.py` and constants to `src/constants/__init__.py`.
- Implement S3 model push/pull logic in `src/cloud_storage/aws_storage.py` and `src/entity/s3_estimator.py`.

## Model Evaluation & Pusher
- Implement model evaluation and pusher components.
- Set up prediction pipeline and `app.py` for serving predictions.
- Add `static` and `templates` directories for the web interface.

## CI/CD with Docker, GitHub Actions, and AWS
- Create `Dockerfile` and `.dockerignore` for containerization.
- Set up GitHub Actions workflow in `.github/workflows/aws.yaml`.
- Create AWS ECR repository and EC2 Ubuntu server for deployment.
- Install Docker on EC2 and connect GitHub self-hosted runner.
- Add GitHub secrets for AWS credentials and ECR repo.
- Open EC2 instance port (e.g., 5080) for app access.

## Usage
- Launch the app locally:
  ```bash
  python app.py
  ```
- Access the app via browser at `http://localhost:5000` (or your configured port).
- For cloud deployment, use your EC2 public IP and configured port.
- Model training available at `/training` route.

## Notebooks
- EDA, feature engineering, and MongoDB demo notebooks are available in the `notebook` folder.

## Additional Notes
- Add `artifact` and other sensitive directories to `.gitignore`.
- Ensure all environment variables are set before running pipelines.
- For troubleshooting, refer to logs in the `logs` directory.

---

This project demonstrates a full ML workflow, from data ingestion to cloud deployment, using best practices for modularity, reproducibility, and scalability.