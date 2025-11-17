# Clinical-Trial-Outcome-Prediction
This project predicts the success or failure of Phase 3 clinical trials using a machine learning model.

Clinical Trial Outcome Prediction with XGBoost & Hybrid FeaturesThis project predicts the success or failure of Phase 3 clinical trials using a machine learning model. It combines chemical drug features (Morgan Fingerprints) with novel text-based features (a "Risk/Safe Keyword" scanner) extracted from trial eligibility criteria.The model is trained on the Therapeutics Data Commons (TDC) Trial Outcome Prediction dataset.Key FeaturesHybrid Feature Engineering:Chemical Features: 2048-bit Morgan Fingerprints are generated from drug SMILES strings using rdkit.Textual Features: The eligibility criteria text is scanned for a predefined list of "risk" and "safe" keywords. This provides a simple but powerful heuristic for trial complexity.Risk Keywords: tumor, metastatic, unresectable, refractory, relapsedSafe Keywords: pain, infection, healthy, volunteer, mildModel: An XGBClassifier is used, configured with scale_pos_weight to handle the imbalanced nature of the dataset (where trial successes are more common than failures).Feature Importance: The analysis shows that the custom Risk_Keyword_Score is the single most important predictor of a trial's outcome, validating the text-based feature engineering approach.Getting StartedPrerequisitesEnsure you have Python 3.7+ installed.InstallationClone this repository:git clone <your-repo-url>
cd <your-repo-directory>
Install the required Python packages:pip install -r requirements.txt
Running the AnalysisSimply run the Python script. It will automatically download the dataset from TDC, process the features, train the model, and print the evaluation results.python predict_trial_outcome.py
Example PredictionsThe script includes a live prediction demo to illustrate how the model weighs risk.Scenario A: Low RiskDrug: Ibuprofen (common painkiller)Protocol: "Inclusion Criteria: Healthy volunteers with mild pain. Exclusion: Infection."Keywords Found: 0 Risk / 5 SafeSuccess Probability: 49.01%Scenario B: High RiskDrug: Doxorubicin (chemotherapy drug)Protocol: "Inclusion Criteria: Patients with metastatic tumor. Disease must be refractory or relapsed."Keywords Found: 4 Risk / 0 SafeSuccess Probability: 25.45%Evaluation Results--- 4. EVALUATION ---
ROC-AUC Score: 0.6144
F1 Score: 0.7874

Classification Report:
              precision    recall  f1-score   support

     Failure       0.54      0.39      0.30       384
     Success       0.72      0.87      0.79       774

    accuracy                           0.68      1158
   macro avg       0.63      0.59      0.59      1158
weighted avg       0.66      0.68      0.63      1158

