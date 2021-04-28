# Capstone-Project---Venture-Capital-Investments

# Problem Statement
The main goal of this project is to classify whether a startup’s current status is in operating status, acquired status or closed status using various features variables in investment venture capital data set.

# Overview ofthe dataset
The data set that we will be looking into is investment Venture Capital data set. There are totally 54249 rows and 39 columns in this data set which I think is a pretty decent size for a toy data set when compared to other traditional datasets. This data set was created by the author using information about startup companies and its investment details which are available in CrunchBase (an online platform where we can find some basic information about private companies).

We will be using this data set to predict whether a startup is currently in operating status, acquired status or closed status depending on independent features such as round wise funding, age of the startup, location of the startup etc. Please note that there are various other factors such as the quality of the management, quality of the product, price points, revenue, expenses, tangible and intangible assets etc. that determines the status of a startup but for this project we will not be considering them since we don’t have the required data and also the main goal of this project is to show the entire Machine Learning pipeline for a non-traditional data set.

# Data Preprocessing
- Stripping white spaces
- Dropping Rows and Columns
- Checking and deleting rows where all the values are NaN (missing)
- Checking for duplicate records
- Dropping rows where target variable ‘status’ is NaN
- Removing the rows for which we don’t have total funding and the breakup of the funding is null as well
- Rows with high NaN percentage
- Removing Columns that don’t contribute to model building
- Removing redundant features

# Model Buidling

# Dummy Classifer Model
Dummy classifier model is a simple model that either predicts 
1. The most frequent occuring target category
2. A constant value prescribed by the data scientist
3. A random value from a uniform distribution

This dummy model as you may have guessed does not take the relationship between the feature variables and target variables into account for predicting the target class. The primary reason for using a dummy variable model is to compare the evaluation scores obtained by this model against the evaluation scores obtained by the actual model that you will be building. If the evaluation score built by your model is less than that of the dummy model then we need to definitely rethink about either fine tuning our existing model or building a new model.

# Random Classifer Model
Just as a reminder Random Forest is a powerful decision tree ensemble model that can be used for both regression and classification model. I have used this model since it is easy to interpret.

As we have seen previously, the data set is a highly imbalanced data set. One approach to solve this issue is by data augmentation — you can either up sample the minority class or down sample the majority class. In this project we have used a technique described by Nitesh Chawla called SMOTE: Synthetic Minority Over-sampling Technique . Basically, SMOTE works by selecting examples that are close in the feature space, drawing a line between the examples in the feature space and drawing a new sample at a point along that line.


# Model Evaluation 
Until now we have only built the models and model evaluation helps us to
Quantify the performance of a model
Choose the best model among the models that we had built.
This step goes hand in hand with model building — we either tune the hyper-parameters of a model or build a new feature or drop a feature or build an entirely new model based on the current model’s performance. As explained earlier since this is a highly imbalanced data set, we will be using F1-Score to evaluate the models
The below table summarizes the metrics for the above models that we had built and we can see that Random Forest model that was trained on a balanced data set with optimum hyper parameters chosen using Random Search CV has clearly won the race with the highest F1-score. We can say that this model will have a F1-Score of 87.73% in the production environment with 95% (± 0.93%) confidence.

| Dataset | Model | Cross Validation - F1-Score | Test Dataset - F1-Score |
| --- | --- | --- | --- |
| Imbalanced Dataset |Dummy Classifier| 80.29% | 80.74% |
| Imbalanced Dataset |Random Forest Classifier| 82.20% | 81.14% |
| Imbalanced Dataset |Random Forest Classifier (Optimum parameters)| 81.19% | 80.66% |
| Balanced Dataset |Dummy Classifier| 43.88% | 79.60% |
| Balanced Dataset |Random Forest Classifier| 87.28% | 80.74% |
| Balanced Dataset |Random Forest Classifier (Optimum parameters)| **87.73%** | **80.65%** |

Since the performance of the model is almost the same for both the training data set and testing data set, we can say that our model has the optimum point in the bias-variance trade-off graph.
