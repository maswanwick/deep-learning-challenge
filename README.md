# Deep Learning Analysis Report

## Overview of the Analysis

The purpose of this exercise was to evaluate approximately 34,000 historical funding endeavors to determine if specific traits of the projects contribute to its success (or failure).  To accomplish this, I setup a series of neural network models to evaluate the existing data.

## Results

### Attempt #1 (AlphabetSoupCharity.h5/AlphabetSoupCharity.ipynb)

This attempt achieved a model accuracy of .7328

**Model Target?**
* IS_SUCCESSFUL value

**Model Features?**
* APPLICATION_TYPE
* AFFILIATION
* CLASSIFICATION
* USE_CASE
* ORGANIZATION
* STATUS
* INCOME_AMT
* SPECIAL_CONSIDERATIONS
* ASK_AMT

**Variables Removed?**
* EIN
* NAME

**Layers/Neurons/Activation Function?**
* Layers = 2
* Neurons = 80/30
* Activation Function = relu
* This was the recommended starting point for the challenge.

**Achieve 75% Accuracy?**
* No - 73.28%

**Steps to improve for next time?**
* Remove STATUS and SPECIAL_CONSIDERATIONS.  These two features were essentially constant throughout the dataset (0.01% and 0.08% variance, respectively)
* Binned ASK_AMT into two categories.  There were 8747 distinct ASK_AMT values.  One of them was 5000, which made up 74% of the values.  So I created two bins, one for 5000 and one for everything else.
* Increased the second hidden layer to have the same number of neurons as the first (80).
* Increased the number of epochs to 200 (from 100).


| Question | Answer |
| - | - |
| Model Target? | IS_SUCCESSFUL value |
| Model Features? |  |
| Variables to remove? | EIN<br>NAME |
| Layers/Neurons/Activation Function?  Why? | 2, 80/30, relu<br>This was the recommended starting point for the challenge. |
| Achieve 75% accuracy? | No - 73.28% |
| Steps to improve for next time | Remove STATUS and SPECIAL

* LogisticRegression model:
  * Of all the loans the model predicted as healthy, 100% of them actually were. (Precision 0 = 1.00)
  * Of all the loans the model predicted as high-risk, 85% of them actually were. (Precision 1 = 0.85)
  * Of all the loans that were actually healthy, the model predicted 99% of them. (Recall 0 = 0.99)
  * Of all the loans that were actually high-risk, the model predicted 91% of them. (Recall 1 = 0.91)
  * Both F1 scores are very close to 1 (0 = 1.0, 1 = 0.88), with an overall accuracy of 99%, therefore, the logistic regression model does a good job of predicting both healthy and high-risk loans.

* RandomOverSample model:
  * Of all the loans the model predicted as healthy, 91% of them actually were. (Precision 0 = 0.91)
  * Of all the loans the model predicted as high-risk, 99% of them actually were. (Precision 1 = 0.99)
  * Of all the loans that were actually healthy, the model predicted 100% of them. (Recall 0 = 1.00)
  * Of all the loans that were actually high-risk, the model predicted 90% of them. (Recall 1 = 0.90)
  * Both F1 scores are very close to 1 (0 = 0.95, 1 = 0.95) with an overall accuracy of 95%, therefore, the logistic regression model does a good job of predicting both healthy and high-risk loans.

## Summary

Both models have a high overall accuracy score (LogisticRegression = 99%, RandomOverSample = 95%), so both would be a good choice when predicting borrower credit risk.  However, from a business standpoint, even though the LogisticRegression model had a 99% overall accuracy, it only had an 85% accuracy when predicting high-risk loans that actaully were high-risk.  Which means, there is a chance that the lender would reject an applicant that would actually be a successful loan.  So the lender might be missing out on potential revenue with this model.  Conversely, the RandomOverSample model was able to accurately predict 99% of these high-risk loans.  But, the cost of this increased accuracy comes at the expense of the accuracy of healthy loans - which means they might end up loaning to someone that is actually a credit risk.  So from a risk perspective, the LogisticRegression model seems to be the better option, since missing out on potential revenue is a better option than lending to a borrower who ultimately defaults.
