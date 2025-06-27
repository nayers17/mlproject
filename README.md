# Student Exam Performance Prediction
A Flask application that predicts a student’s math score based on demographic and exam preparation data using a trained **Linear Regression** model and preprocessing pipeline.

## Project Structure
```
artifacts/                # Stored model and preprocessing artifacts
  ├── model.pkl           # Trained Linear Regression model
  └── preprocessor.pkl    # Preprocessing pipeline

data/                     # Raw and processed data files
  ├── train.csv
  └── test.csv

notebook/                 # Jupyter notebooks
  ├── 1. EDA STUDENT PERFORMANCE.ipynb
  └── 2. MODEL TRAINING.ipynb

src/                      # Application source code
  ├── components/         # Data validation and input schemas
  ├── pipeline/           # Inference pipeline assembly
  ├── exception.py        # Custom exception classes
  ├── logger.py           # Logging setup
  └── utils.py            # Utility functions

templates/                # HTML templates for Flask
  ├── home.html
  └── index.html

Dockerfile                # Docker build instructions
Dockerrun.aws.json        # AWS Elastic Beanstalk configuration
buildspec.yml             # AWS CodeBuild spec
application.py            # Flask application entry point
requirements.txt          # Python dependencies
.gitignore                # Files to ignore in Git
.dockerignore             # Files to ignore in Docker context
README.md                 # Project documentation (this file)
```

## Prerequisites
- Docker installed locally  
- (Optional) Python 3.8+ and pip if running without Docker  

## Quick Start with Docker
1. **Build the image** (from project root):  
   ```bash
   docker build -t ml-app .
   ```
2. **Run the container**:  
   ```bash
   docker run -d      -p 5000:5000      --name ml-app      ml-app
   ```
3. **Browse** to http://localhost:5000/predictdata

## Running Locally without Docker
```bash
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt
export FLASK_APP=application.py
export FLASK_ENV=production
flask run --host=0.0.0.0 --port=5000
```

## Model Training & Evaluation
See `notebook/2. MODEL TRAINING.ipynb` for full details.  
We compared multiple regressors and chose Linear Regression for production:

- **Linear Regression**: R² = 0.880, RMSE ≈ 5.32  
- Ridge Regression: R² = 0.881, RMSE ≈ 5.32  
- Random Forest: R² = 0.856, RMSE ≈ 5.15  
- CatBoost Regressor: R² = 0.851, RMSE ≈ 5.20  

The final Linear Regression model and preprocessing pipeline are serialized in:
- `artifacts/model.pkl`  
- `artifacts/preprocessor.pkl`  