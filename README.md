# metis-project-3
My third Metis project. 

# Goal
Detect fake job postings using a classification model

# Methods
- Oversample minority class (fraudulent job listings)
- Apply CountVectorizer to combined text fields
- Apply classification models
  - Logistic Regression
  - Random Forest
  - Naive Bayes
  - XGBoost
  
# Results
Logistic Regression performed best on the validation data, detecting 78% of fraudulent listings, with a false postive rate of 20%. 
