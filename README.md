# 1. Heart Disease Risk Analysis & Prediction

## Introduction

Cardiovascular disease is one of the leading causes of death worldwide.
Early detection and prediction of heart disease can save lives by allowing
doctors to intervene before the condition becomes critical.

In this project I analyze a dataset of **918 patients** with **12 features**
including age, sex, cholesterol, blood pressure, and chest pain type to:

 Explore patterns in the data using **SQL** and **Python**
 Identify which features are most linked to heart disease
 Build machine learning models to **predict heart disease**
 Explain model predictions using **SHAP**

## Dataset
 **Source:** Kaggle - Heart Failure Prediction Dataset
 **Rows:** 918 patients
 **Columns:** 12 features
 **Target:** HeartDisease (0 = No Disease, 1 = Has Disease)

 ## SQL Analysis
 I conected csv file with a database and cretaed a table called 'patients'
 508 patient were with sick(heart disease) of which 458 were male and 50 female.
The minimum age affected by heart disease was 33 for women and 31 for men.
  ChestPainType  total  has_disease
0           ASY    496          392
1           NAP    203           72
2           ATA    173           24
3            TA     46           20
  Patients with high cholesterol above 250 were 305.
  Top 5 oldest patients with heart disease:
     Age Sex ChestPainType  Cholesterol
0   77   M           ASY          171
1   77   M           ASY          304
2   76   M           NAP          113
3   75   M           ASY          203
4   75   M           ASY          225



 ## 2. Exploratory Data Analysis (EDA)

After SQL analysis I used Python to explore the data deeper
and visualize patterns.

### Key Findings:
 Average age of sick patients is higher than healthy patients
 Males have a much higher heart disease rate than females
 ASY chest pain type is strongly linked to heart disease
 Patients with heart disease tend to have lower MaxHR
## 3. Feature Engineering

Machine learning models only understand numbers not text.
So I converted all categorical columns into numerical values.

### Label Encoding (2 categories):
Sex: M - 1, F - 0
 ExerciseAngina: Y - 1, N - 0

### One Hot Encoding (more than 2 categories):
 ChestPainType - 3 new columns ( asy dropped for reference)
 RestingECG - 2 new columns
 ST_Slope - 2 new columns
 ## 4. Data Preprocessing

Before building the model I split the data into:
 **X** → features (input)
 **y** → target (output)

Then split into training and testing sets:
 **80% training** → 734 patients (model learns from this)
 **20% testing** → 184 patients (model gets tested on this)

Finally applied **Feature Scaling** to normalize all 
numerical features to the same range so no feature 
dominates the model.
## 5. Machine Learning Models

I built 3 classification models and compared their performance.

### Results:
 Model : Logistic Regression, Random Forest, XGBoost
 Accuracy : Accuracy

Logistic Regression  85% 
Random Forest  86% 
XGBoost  86% 

SHAP (SHapley Additive exPlanations) explains WHY the model 
makes each prediction by showing which features pushed the 
prediction towards or away from heart disease.


### Key Insight:
XGBoost and Random Forest performed equally at 86% accuracy.
However XGBoost missed only 14 sick patients compared to 17 
in Logistic Regression - making it the better choice for 
healthcare where missing sick patients is dangerous.

The most important features for predicting heart disease are:
1. **ST_Slope_Up** - most protective, reduces heart disease risk
2. **ExerciseAngina** - having chest pain during exercise 
   strongly indicates heart disease
3. **ST_Slope_Flat** - flat ST slope is a strong risk factor
4. **Oldpeak** - higher values indicate more heart stress
5. **Sex** - males are at higher risk than females
6. ## 5. Conclusion

This project demonstrated a full data science pipeline:
SQL - EDA - Feature Engineering - Machine Learning.

### Main findings:
 ASY chest pain type is the strongest predictor of heart disease
 Males are at significantly higher risk than females
 Age is positively correlated with heart disease risk
 XGBoost is the best performing model at 86% accuracy
 SHAP, this is especially important in healthcare - a doctor needs 
to understand WHY a patient is predicted sick, not just 
that they are.

### Future improvements:
 Collect more data to improve model accuracy
 Try hyperparameter tuning to optimize XGBoost
 Deploy the model as a web application
