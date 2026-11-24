# Diabetes Classification: Streamlit Model Lab

A teaching app built with Streamlit, pandas, seaborn, and scikit-learn. Students can choose one classifier or compare four classifiers using cross-validation, inspect holdout test metrics, make a sample prediction, and save or reload a fitted pipeline.

## Project files

- **app.py** — Streamlit interface, training, evaluation, prediction, and model persistence.
- **diabetes.csv** — the supplied 768-row diabetes dataset.
- **requirements.txt** — Python packages for the app.
- **models/** — created automatically when a model is saved; no saved model is included initially.

## Open and run in VS Code

1. Extract the ZIP file and open the extracted **diabetes_streamlit_app** folder in VS Code.
2. Open the VS Code terminal in that folder.
3. Create and activate a virtual environment.

### Windows PowerShell

```powershell
py -3.13 -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install --upgrade pip
pip install -r requirements.txt
streamlit run app.py
```

If PowerShell blocks activation, use Command Prompt:

```bat
py -3.13 -m venv .venv
.venv\Scripts\activate.bat
python -m pip install --upgrade pip
pip install -r requirements.txt
streamlit run app.py
```

### macOS or Linux

```bash
python3.13 -m venv .venv
source .venv/bin/activate
python -m pip install --upgrade pip
pip install -r requirements.txt
streamlit run app.py
```

The terminal will print a local address. Open it in a browser. Keep the terminal running while using the app; press **Ctrl+C** to stop it.

## Dynamic workflow

- **Select a model:** choose Logistic Regression, Decision Tree, Random Forest, or Support Vector Machine. The app trains the chosen pipeline when Train is clicked.
- **Compare models:** five-fold stratified cross-validation compares mean F1 scores on the training partition and selects the top model. The untouched test partition is then used for evaluation.
- **Save and reload:** the trained preprocessing-and-model pipeline can be saved as **models/diabetes_model.joblib** and loaded from the sidebar later. Saving is enabled by default and can be turned off.
- **Make a prediction:** enter sample features and get the predicted class and estimated probability for Outcome 1.

Missing-value imputation is fitted inside the pipeline after the train/test split. In the supplied dataset, zero measurements in Glucose, BloodPressure, SkinThickness, Insulin, and BMI are treated as missing and imputed using medians. Zero Pregnancies and Outcome values are retained.

## Model file notes

The app writes and reads the model file locally. Scikit-learn does not support loading persisted estimators across different scikit-learn versions, so use the same environment when saving and reloading. Only load model files you created or otherwise trust.

This dataset and app are for teaching only. The predictions are not medical advice or a clinical diagnosis.
