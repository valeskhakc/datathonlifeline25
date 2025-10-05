# datathonlifeline25
Readme
This project was developed for Datathon Lifeline 2025, organized by MLDA @ EEE, Nanyang Technological University.
It aims to build an AI-driven system that detects fetal distress using Cardiotocography (CTG) data — a tool that records a baby’s heart rate and uterine contractions during labor.
By analyzing CTG patterns, the model classifies fetal health into:
Normal (1) – No distress
Suspect (2) – Needs monitoring
Pathologic (3) – High risk, immediate attention required

Objective
Develop a clinically interpretable machine learning model that:
Accurately classifies CTG traces into Normal, Suspect, or Pathologic.
Handles class imbalance effectively.
Balances performance metrics like Balanced Accuracy and Macro F1-Score.

Dataset
Source: UCI Cardiotocography Dataset
Local file used: data_cardio.xlsx (Sheet: Raw Data)
Column
Description
LB
Baseline fetal heart rate (bpm)
AC
Number of accelerations per second
FM
Fetal movements
UC
Uterine contractions
DS / DP / DL
Deceleration patterns
ASTV / ALTV
Short- and long-term variability
Histogram features
Statistical properties of FHR distribution
NSP
Target label (1 = Normal, 2 = Suspect, 3 = Pathologic)


Workflow Summary
1. Data Loading & Exploration
df = pd.read_excel("data_cardio.xlsx", sheet_name="Raw Data")
sns.countplot(x="NSP", data=df, palette="Set2")
Visualized class imbalance (Normal dominates)
Examined distributions for features like LB and AC
Used boxplots and histograms to reveal feature–class relationships

2. Data Preprocessing
Missing values handled via SimpleImputer
Features scaled with StandardScaler
Labels encoded numerically
Used train_test_split for robust evaluation

pipeline = Pipeline([
    ('imputer', SimpleImputer(strategy='mean')),
    ('scaler', StandardScaler())
])


3. Model Development
The following models were trained and compared:
Model
Description
Logistic Regression
Baseline linear model
Decision Tree
Basic interpretable classifier
Random Forest
Ensemble model with feature importance
Gradient Boosting
Boosted ensemble for higher accuracy
SVM
Non-linear classifier with kernel optimization
KNN
Distance-based classifier
MLPClassifier
Multi-layer neural network

Each model was evaluated using Stratified K-Fold Cross Validation to maintain class balance.

4. Evaluation Metrics
Metrics computed for each model:
balanced_accuracy_score
f1_score(average='macro')
classification_report

ConfusionMatrixDisplay
Visuals:
Confusion Matrix
F1 & Accuracy comparison charts
Final model chosen: Gradient Boosting (best trade-off between performance and interpretability)

6. Explainability
Used feature importance plots from RandomForest
Discussed medical significance of top predictors (e.g., ASTV, DS, DP, LB)
Suggested SHAP for future interpretability improvements

Visual Insights
The notebook includes:
Class distribution plot
Correlation heatmap
Feature importance visualization
Confusion matrix

These help explain why the model makes its predictions for medical AI.
