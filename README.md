# Final-Project
## Prediction of the salary of workers who work for NYC

Group members: Winnie Yang and Sophie Dang

## Introduction
The purpose of this project is to find out which model works best for predicting the salary of a NYC worker. We use the NYC payroll dataset from NYC open data, which contains payroll information for all NYC employees. This serves as a comprehensive repository of public sector compensation across all city agencies and job titles. Our primary objective is to find a predictive model that estimates NYC government employee salary based on available different features, like their job title. Through models we seek to answer what determines how much a NYC employee is paid, what influences their salary, and how accurate are the predictions. 

## Data description
Our data is from NYC open data and is titled “Citywide Payroll Data (Fiscal Year).” This data includes how the city’s budget is spent on salary for municipal employees. The data contains many variables but we selected a few to focus on such as agency name, title description, pay basis, hours, and gross paid. While this dataset can help show how the city spends its money, for our purpose, it also helps display the changes in a worker’s salary depending on the different variables. With over 6 million rows, this data is pretty representative of NYC workers and how their income has shifted and varies from one another. 

## Overview of models and implementation
Linear Regression
The model evaluates its performance using R-squared and mean squared error. R-squared shows how well the model explains the differences in workers’ salaries. Mean squared error measures how different the predicted salaries are from the actual salaries.

KNN
This model aims to predict the salaries of NYC workers based on various features indicated in the dataset above. Through this confusion matrix, the model indicates which salary classes were predicted accurately and were predicted inaccurately. Continuous salary values are determined by grouping individuals into classes: low, middle, or high. Using KNN, the model makes predictions on a worker’s salary class based on similar workers’ salary classes. The confusion matrix then visualizes the model performance through a heatmap. In the heatmap, each cell shows the predicted salary class aligned with the actual salary class. The diagonal cells represent accurate class predictions, while the other cells respresent misclassifications. The model also displays the intensity of colors reflecting the number of workers for each category, with darker colors indicating higher numbers of accurate classification. 
Decision Tree
This model works by splitting the data into subsets based on feature values, creating a tree-like structure of decisions. It's capable of capturing non-linear relationships. The Decision Tree Regressor was implemented by first selecting key features and splitting the data 80/20 for training and testing. A pipeline was constructed that used a ColumnTransformer to apply one-hot encoding to categorical variables and standardization to numerical features, followed by a DecisionTreeRegressor with a max depth of 10 to control complexity. After training on the processed data, predictions were made on the test set, yielding a strong R² score of 0.9670 and identifying "Pay Basis_per Annum" and "Regular Gross Paid" as the most influential features for salary prediction.

XGBoost
This is an ensemble learning method that uses a gradient boosting framework. It builds multiple decision trees sequentially, with each new tree correcting the errors of the previous ones. XGBoost often delivers high accuracy and robustness. The XGBoost Regressor was implemented by installing the library, importing the model, and defining a pipeline that applied the same preprocessing steps (categorical encoding and numerical standardization) before training the XGBRegressor. After fitting on the training data, predictions were made on the test set and evaluated, achieving an RMSE of 7,070.64 and an R² score of 0.9756. Feature importance analysis revealed that "Pay Basis_per Annum" and "Regular Gross Paid," along with certain agency names, were the most influential predictors of salary.


## Results and Interpretation
Linear Regression

KNN

Decision Tree
The Decision Tree model with max_depth=10 achieved an RMSE of 8,220.36 and an R² score of 0.9670, indicating better performance than the Linear Regression model. The Decision Tree Regressor delivered a very strong predictive performance, with an R² score of 0.9670, indicating it explains approximately 96.7% of the variance in salaries. This is an excellent result, suggesting the model has captured the underlying data patterns effectively. The top features it identified—"Pay Basis_per Annum" and "Regular Gross Paid"—are logically sound and provide a useful, interpretable insight into the main salary determinants. However, despite the high score, the model's simplicity (with a manually limited max_depth=10) likely means it is slightly underfitting the data compared to a more complex ensemble like XGBoost, which achieved a marginally higher R². This trade-off is common: the Decision Tree offers better transparency and lower risk of overfitting on noisy data, but may sacrifice a small degree of predictive power for that interpretability and robustness.

XGB Boost
Rmse shows that the model’s predictions are off by around 7000 from true salary value. The XGBoost model achieved the best performance among the regression models with an RMSE of 7,070.64 and an R² score of 0.9756. The XGBoost model’s performance is outstanding, achieving an R² of 0.9756, meaning it explains nearly all variance in salaries, and an RMSE of 7,071, indicating relatively low prediction error. It outperformed all other models tested, and its identified top features—Pay Basis_per Annum, Regular Gross Paid, and specific agencies—make intuitive sense. However, such high performance requires careful validation to ensure it is not the result of overfitting or data leakage, particularly by confirming these metrics on a truly held-out test set and verifying that influential features are not circularly related to the target.

## Conclusion
