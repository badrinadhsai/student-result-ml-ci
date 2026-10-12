# Student Result ML CI Pipeline

## 1. Project Overview

This project demonstrates Machine Learning Operations (MLOps) concepts using Python, scikit-learn, automated testing, model quality gates, and GitHub Actions.

The project builds a student result prediction model and automates model training, evaluation, quality validation, and artifact preservation through a Continuous Integration (CI) pipeline.

## 2. Objectives

- Generate a reproducible synthetic student dataset.
- Train and evaluate a Machine Learning classification model.
- Automate ML pipeline testing using Python unittest.
- Enforce a minimum model accuracy threshold.
- Preserve the trained model and evaluation files as GitHub Actions artifacts.
- Demonstrate intentional failures and verify successful recovery.

## 3. Technologies Used

- Python 3.11
- NumPy
- Pandas
- Scikit-learn
- Joblib
- Python unittest
- GitHub Actions
- YAML

## 4. Project Structure

- `train_model.py` — Generates the dataset, trains the model, evaluates performance, and saves output files.
- `test_ml_pipeline.py` — Contains automated tests for the ML pipeline.
- `quality_gate.py` — Checks whether model accuracy meets the required threshold.
- `requirements.txt` — Lists the Python dependencies.
- `.github/workflows/ml-ci.yml` — Defines the GitHub Actions CI pipeline.
- `README.md` — Documents the project and experiments.

## 5. Machine Learning Pipeline

The system generates 300 synthetic student records using attendance, internal marks, assignment marks, and previous scores.

The dataset is divided into:
- Training dataset: 240 records (80%)
- Testing dataset: 60 records (20%)

A Logistic Regression model with feature scaling is trained and evaluated. The pipeline calculates model accuracy and a confusion matrix.

The generated output files are:
- `student_result_model.pkl` — Trained ML model.
- `metrics.json` — Evaluation accuracy and dataset split information.
- `student_results.csv` — Generated student dataset.

## 6. Practical 2 — ML Model Training CI

This practical integrates model training and automated testing into GitHub Actions.

The workflow:
1. Checks out the repository.
2. Sets up Python 3.11.
3. Installs dependencies from `requirements.txt`.
4. Trains the ML model.
5. Runs automated tests using `test_ml_pipeline.py`.

The tests verify the dataset size and columns, model and metrics file creation, PASS/FAIL predictions, and valid accuracy values.

An intentional test failure was demonstrated by changing the expected dataset size from 300 to 301. The test was restored to 300, and the workflow passed successfully.

## 7. Practical 3 — ML Quality Gate

This practical introduces an automated model performance check.

The quality gate uses a minimum required accuracy threshold of 0.85 (85%).

- If model accuracy is at least 0.85, the quality gate passes.
- If model accuracy is below 0.85, the quality gate fails and exits with a non-zero status.

The threshold was temporarily increased to demonstrate failure and then restored to 0.85. The workflow was verified again after restoration.

## 8. Practical 4 — Preserve ML Artifacts

This practical preserves validated ML output files using the GitHub Actions artifact upload action.

The workflow uploads:
- `student_result_model.pkl`
- `metrics.json`
- `student_results.csv`

Artifact configuration:
- Action: `actions/upload-artifact@v4`
- Artifact name: `student-result-ml-artifacts`
- Retention period: 7 days
- Missing-file handling: `error`

A missing artifact filename was used to demonstrate an upload failure. The original filename was restored, and the final workflow completed successfully. The downloaded ZIP was verified to contain all three files.

## 9. Model Evaluation

The verified model evaluation recorded:

- Accuracy: approximately 96.67%
- Training records: 240
- Testing records: 60

These results apply to the generated dataset and the configured train/test split.

## 10. Continuous Integration Workflow

The GitHub Actions workflow automates model training, quality validation, automated tests, and artifact upload.

A successful workflow run indicates that the configured steps completed without errors. Intentional failures were introduced during the experiments and corrected to verify the pipeline's behavior.

## 11. Conclusion

This project demonstrates a basic end-to-end MLOps workflow using GitHub Actions. It combines automated Machine Learning training, unit testing, model quality validation, and artifact preservation.

The practicals show how CI can detect failures early, enforce model performance requirements, and preserve important outputs for later inspection.
