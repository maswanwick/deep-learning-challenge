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

**Layers/Neurons/Activation Function? Why?**
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

### Attempt #2 (AlphabetSoupCharity_Optimization.h5/AlphabetSoupCharity_Optimization.ipynb)

This attempt achieved a model accuracy of .7314

**Model Target?**
* IS_SUCCESSFUL value

**Model Features?**
* APPLICATION_TYPE
* AFFILIATION
* CLASSIFICATION
* USE_CASE
* ORGANIZATION
* INCOME_AMT
* ASK_AMT_CATEGORY

**Variables Removed?**
* EIN
* NAME
* STATUS
* SPECIAL_CONSIDERATIONS

**Layers/Neurons/Activation Function? Why?**
* Layers = 2
* Neurons = 80/80
* Activation Function = relu
* Attempted to add additional neurons to add more trainable parameters into the model.

**Achieve 75% Accuracy?**
* No - 73.14%

**Steps to improve for next time?**
* Binned APPLICATION_TYPE and CLASSIFICATION into two categories.  79% of the APPLICATION_TYPES are T3, so I created two bins, one for T3 and one for everything else.  50% of the CLASSIFICATION records are C1000, so I created two bins, one for C1000 and one for everything else.
* Trained the model with 90% of the dataset, instead of the default 75%.  The thought here was if I'm able to feed the model more training data, the test data will perform better.
* Added a third hidden layer.
* Increased the number of epochs to 300 (from 200).

### Attempt #3 (AlphabetSoupCharity_Optimization_Again.h5/AlphabetSoupCharity_Optimization_Again.ipynb)

This attempt achieved a model accuracy of .7122

**Model Target?**
* IS_SUCCESSFUL value

**Model Features?**
* APPLICATION_TYPE
* AFFILIATION
* CLASSIFICATION
* USE_CASE
* ORGANIZATION
* INCOME_AMT
* ASK_AMT_CATEGORY

**Variables Removed?**
* EIN
* NAME
* STATUS
* SPECIAL_CONSIDERATIONS

**Layers/Neurons/Activation Function? Why?**
* Layers = 3
* Neurons = 80/80/80
* Activation Function = relu
* Attempted to an additional layer with the same number of neurons to add more trainable parameters into the model.

**Achieve 75% Accuracy?**
* No - 71.22%

**Steps to improve for next time?**
* N/A - this was my last attempt

## Summary

Overall, all three attempts scored an accuracy score of over 70%, which is a good, but not great, accuracy score.  My attempts to improve the accuracy score were very frustrating, I was uncertain what the different changes would have on the overall performance.  Obviously, everything I thought would help (removing features, removing variance within features, increasing neurons, layers, and epochs) didn't - in fact, it decreased the accuracy score.

After watching [this](https://www.mathworks.com/videos/introduction-to-deep-learning-machine-learning-vs-deep-learning-1489503513018.html?gclid=EAIaIQobChMIhOWywvORgwMVKszCBB1z2gM0EAAYASAAEgKag_D_BwE&ef_id=EAIaIQobChMIhOWywvORgwMVKszCBB1z2gM0EAAYASAAEgKag_D_BwE:G:s&s_kwcid=AL!8664!3!591940647971!p!!g!!machine%20learning%20vs%20neural%20networks&s_eid=psn_68899282265&q=machine+learning+vs+neural+networks&gad_source=1) video on when you should use machine learning vs. deep learning, it seems that deep learning is best used for much larger datasets.  In this case, we might have seen better accuracy in a machine learning model such as LogisticRegression, since this dataset is "small" in comparision to other datasets intended for neural networks.
