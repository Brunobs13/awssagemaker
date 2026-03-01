# AWS SageMaker ML Pipeline for Mobile Price Classification

End-to-end machine learning project on AWS SageMaker for mobile price range prediction, from dataset preparation to endpoint deployment.

## Business Problem

Pricing teams need a fast way to classify smartphones into price bands based on hardware features.  
This project builds a reproducible ML workflow to train and deploy that classifier in SageMaker.

## Architecture (Text)

1. Prepare data splits (`train-V-1.csv`, `test-V-1.csv`).
2. Upload data to Amazon S3.
3. Run SageMaker training job using `script.py`.
4. Save trained artifact (`model.joblib`).
5. Deploy model to a SageMaker endpoint.
6. Send test payloads for online inference.

## Tech Stack

- Python
- AWS SageMaker (training + real-time inference endpoint)
- Amazon S3 (dataset and model artifact storage)
- scikit-learn (`RandomForestClassifier`)
- pandas, numpy, joblib
- Jupyter Notebook (`research.ipynb`)

## Project Files

- `research.ipynb`: Complete SageMaker workflow (EDA, split, S3 upload, train, deploy, predict, cleanup).
- `script.py`: SageMaker training entrypoint with model training and evaluation logging.
- `mob_price_classification_train.csv`: Source dataset.
- `train-V-1.csv`: Training split.
- `test-V-1.csv`: Test split.
- `requirements.txt`: Local dependencies.

## Run Locally

```bash
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

Then open and run:

```bash
jupyter notebook research.ipynb
```

## AWS Prerequisites

- Valid AWS credentials (`aws configure` or environment credentials)
- Existing S3 bucket
- SageMaker execution role ARN with S3/SageMaker permissions

Update placeholders in `research.ipynb` before running:
- `YOUR_S3_BUCKET_NAME`
- `YOUR_SAGEMAKER_EXECUTION_ROLE_ARN`

## Security Notes

- Do not hardcode access keys in notebooks or scripts.
- Keep secrets outside Git (environment variables or AWS profiles).
- Remove endpoint/resources after tests to avoid unnecessary cost.

## Current Scope and Next Steps

Current implementation uses `RandomForestClassifier` with notebook-driven orchestration.

Potential improvements:
- Add CI pipeline for tests and lint checks.
- Add CloudWatch metrics dashboard for endpoint monitoring.
- Add model versioning and automated retraining triggers.
