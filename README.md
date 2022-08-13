# Flu_Shot_DataDriven_Competition
Predicting H1N1 and Seasonal Flu Vaccines using Machine Learning Techniques.

What are we trying to predict?

The likelihood of a person being vaccinated against H1N1 and seasonal flu. 
DrivenData's vaccine challenge is a Multi-label classification machine learning problem.

## Data Preprocessing


-Mode Imputation for all binary features and two ordinal features h1n1_concern & h1n1_knowledge 
-Mean Imputation for rest of the ordinal features  
-Replace blanks with “None” for employment_status , employment_industry & employment_occupation  
-Health insurance has been ignored in the model due to a vast amount of missing data 

## Feature Engineering


**Interaction features**

-Average opinion columns for both vaccines  
-Sum, average etc. of 7 behavioral columns 
-Average values for various columns based on age, race, etc 
-Average behavioral features based on education groups 
-Average of h1n1 concern and knowledge based on income 

**Encoding** 

-Ordinal encoding, Education, Age, Income 
-One hot encoding, rest of categorial features 
-Target encoding, create flag for 6 opinion features, such as opinoin_h1n1_vac or opinion_seas_vac, if it's over average

## Modeling/HyperParameter Tuning


-New features such as H1N1 concern average by demographics (i.e. age, education) were predominately ranked outside the top 100 features based on importance. 
-Initial cross-validation results did not improve significantly when introducing newly engineered features, and this pattern continued with competition scores. 
-Further Experiments with recursive feature elimination did not yield improvements in competition scores. 
-CatBoost model 100 trials with new features: 0.8600  
-CatBoost model 100 trials with RFE selected features: 0.7964 

-Initial experiments using RandomGridSearch were used on primary models (simple decision trees, RandomForestClassifiers) however results were abysmal (as expected).  
-Pivoted to using FLAML and Optuna on the benchmark models (XGBoost, CatBoost, LightGBM). 
-Optuna displayed stronger ability to define specific parameters and was easier to use. 


CatBoost models with Optuna hyperparameter tuning
![image](https://user-images.githubusercontent.com/41646192/184504897-0bd8f7bf-c1c6-43f0-9bc1-1d2f1e37007f.png)

![image](https://user-images.githubusercontent.com/41646192/184504934-1555de55-4a39-47fe-81da-82071a942b3f.png)


