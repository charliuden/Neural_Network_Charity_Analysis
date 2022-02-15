# Neural Network Charity Analysis

## Overview of the analysis: 

Alphabet Soup is a nonprofit organization that gives financial support to businesses dedicated to protecting the environment, people's wellbeing and unifying the world. Efforts include improvements to technology and reforestation projects. In the past 20 years, Alphabet Soup has raised over 10 billion dollars. 
 
However, not all donations result in a successful outcome. Either projects fail, or organizations simply take the donation and disappear. This analysis uses a neural network model to build a binary classifier that can predict whether or not a charity campaign will be successful.

### Data

The data is held in a CSV containing more than 34,000 organizations that have received funding from Alphabet Soup over the years. Within this dataset are a number of columns that capture metadata about each organization, such as the following:

- EIN and NAME—Identification columns
- APPLICATION_TYPE—Alphabet Soup application type
- AFFILIATION—Affiliated sector of industry
- CLASSIFICATION—Government organization classification
- USE_CASE—Use case for funding
- ORGANIZATION—Organization type
- STATUS—Active status
- INCOME_AMT—Income classification
- SPECIAL_CONSIDERATIONS—Special consideration for application
- ASK_AMT—Funding amount requested
- IS_SUCCESSFUL—Was the money used effectively - this is the target column

- Deliverable 1: Preprocessing Data for a Neural Network Model
- Deliverable 2: Compile, Train, and Evaluate the Model
- Deliverable 3: Optimize the Model
- Deliverable 4: A Written Report on the Neural Network Model


## Results: 

### Data Preprocessing
- The target variable for this model is the IS_SUCCESSFUL column. 
- The columns that will be used as features in the model include STATUS, ASK_AMT, CLASSIFICATION, APPLICATION_TYPE, INCOME_AMT, and SPECIAL_CONSIDERATIONS. 
- The NAME and  EIN columns are neither targets nor features and should be removed from the input data. 

### Compiling, Training, and Evaluating the Model
- After trying multiple combinations of layers and neurons, the model with the best performance had three layers, each with 90, 50, and 30 neurons respectively. The tahn function was used as an activation function for all three hidden layers. The tahn function is most appropriate for wide data (which after encoding all of the categorical data, the input data contains 43 columns). The sigmoid activation function was used in the output layer because this model is predicting a binary outcome. The sigmoid function predicts the probability (between 0 and 1) that an outcome one of two potions.
- The target performance was an accuracy score of 0.75 (accurately predict 75% of the test data). This was not achieved. The highest accuracy score achieved was 0.726. 

The following steps were taken to try and increase model performance:

#### Attempt 1: change from relu to tahn function - tahn is more appropriate for wide data. 

- this improved the accuracy score from 0.7243148684501648 to 0.7245481014251709 -that's just a 0.0002 difference. 
- but I will keep this modification to the model.

#### Attempt 2: remove outliers from ASK_AMT
- The ASK_AMT column gives information on the asking amount. I used a boxplot to find outliers and removed them
- This reduced the accuracy score to 0.5557586550712585 - YIKES!
- I have commented out the code for removing outliers. 
- Below is a boxplot showing the outliers in the ASK_AMT column. 

![box_plot_ASK_AMT_outliers.png](https://github.com/charliuden/Neural_Network_Charity_Analysis/blob/main/images/box_plot_ASK_AMT_outliers.png)

#### Attempt 3: decrease the number of bins
- increase the cutoff value for binning, which will decrease the number of bins -may deal with potential overfitting.
- cut off for APPLICATION_TYPE column from 500 to 1000: decrease the number of bins from 9 to 6
- cut off for CLASSIFICATION column from 1000 to 2500: decrease the number of bins from 6 to 4
- This again reduced the accuracy score to 0.7216326594352722 from attempt 1 (0.7245481014251709). 

#### Attempt 4: increase the number of bins
- decrease the cutoff value, resulting in more bins:
- cut off for APPLICATION_TYPE column from 500 to 250: increase the number of bins from 9 to 10
- cut off for CLASSIFICATION column from 1000 to 500: increase the number of bins from 6 to 7
- This improved the accuracy score to 0.7258309125900269!
- I will keep this modification to the input data. 

#### Attempt 5: increase epochs, neurons, and hidden layers
- increase epochs from 50 to 100
- add one more hidden layer
- add neurons to all three hidden layers
- This improved the accuracy score to 0.7261807322502136

## Summary

Overall, this deep learning model did not perform well. I would not recommend that Alphabet Soup uses this model to predict donation outcomes. Instead, I would recommend they turn to logistic regression or random forest.

A logistic regression model is a classification algorithm that can analyze continuous and categorical variables. Logistic regression uses a sigmoid curve identical to the one used for the output activation function in this model. This would be a good place to start because it is a simpler, easily understood model. 

Random forest is another model that can classify data. Its results are a little more difficult to interpret but can perform well with large amounts of input data. 
