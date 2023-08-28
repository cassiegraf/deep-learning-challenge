<h3> Alphabet Soup Funding Predictions <h3>

#### Alphabet Soup is a nonprofit that is looking for a tool that can help it select the applicants for funding with the best chance of success in their ventures.

**The original dataset received from Alphabet Soup included the following columns:**

- EIN and NAME—Identification columns
- APPLICATION_TYPE—Alphabet Soup application type
- AFFILIATION—Affiliated sector of industry
- CLASSIFICATION—Government organization classification
- USE_CASE—Use case for funding
- ORGANIZATION—Organization type
- STATUS—Active status
- INCOME_AMT—Income classification
- SPECIAL_CONSIDERATIONS—Special considerations for application
- ASK_AMT—Funding amount requested
- IS_SUCCESSFUL—Was the money used effectively

**I created a total of 4 models, the original and then three attempts to optimize the accuracy results. All 4 of the models had the following similarities:**

- The 'EIN' and 'NAME' columns were removed from the dataframe 
- The target variable used the column header 'IS_SUCCESSFUL'
- All models achieved a 72% accuracy, below the goal of 75%

**Original Model**

The original model (file name: deep_learning.ipynb) used 'IS_SUCCESSFUL' as the target variable and the following were used as the features: 'APPLICATION_TYPE', 'AFFILIATION', 'CLASSIFICATION', 'USE_CASE', 'ORGANIZATION', 'STATUS', 'INCOME_AMT', 'SPECIAL CONSIDERATIONS', 'ASK_AMT'. In this model I used two hidden layers, the first layer had 80 nodes with ReLU activation, and the second layer used 30 nodes with the ReLU activation, the output activation was sigmoid, and it was trained using 100 epochs. The results had an accuracy of 72.37% and a loss of 56.7%.

**Optimization Attempt #1**

My first attempt at optimizing the data (**file name: AlphabetSoupCharity_Optimization1.ipynb**) used 'IS_SUCCESSFUL' as the target variable and the following were used as the featuers: 'APPLICATION_TYPE', 'AFFILIATION', 'CLASSIFICATION', 'USE_CASE', 'ORGANIZATION', 'STATUS', 'INCOME_AMT', 'SPECIAL CONSIDERATIONS', 'ASK_AMT'. In this attempt I used three hidden layers (instead of 2) and assigned 22 nodes to each layer. All other fields remained the same as the original model. The results were very similar to the original model, with a 72.58% accuracy and 55.7% loss.

**Optimization Attempt #2**

My second attempt at optimizating the data (**file name: AlphabetSoupCharity_Optimization2.ipynb**) used 'IS_SUCCESSFUL' as the target variable and the following were used as the features: 'APPLICATION_TYPE', 'AFFILIATION', 'CLASSIFICATION', 'USE_CASE', 'ORGANIZATION', 'STATUS', 'INCOME_AMT', 'SPECIAL CONSIDERATIONS', 'ASK_AMT'. In this attempt I added more data to train so I changed the 'APPLICATION_TYPE' cutoff from greater than 527 to include all points greater than 65. I also changed the 'CLASSIFICATION' from greater than 1882 to greater than 286. I thought maybe there was not enough data to train so by increasing the number of bins that would allow for more data points to train. I used the same number of layers and nodes as the original model - two hidden layers, one with 80 nodes and the other with 30 nodes. The results of this attempt were similar to but just slightly better than the original model and attempt #1, with 73% accuracy and 56% loss, so increasing the data did help, but not nearly enough. 

**Optimization Attempt #3**

My third attempt at optimizing the data (**file name: AlphabetSoupCharity_Optimization3.ipynb**) used 'IS_SUCCESSFUL' as the target variable and the following were used as the featuers: 'APPLICATION_TYPE', 'AFFILIATION', 'CLASSIFICATION', 'USE_CASE', 'ORGANIZATION', 'STATUS', 'INCOME_AMT', 'SPECIAL CONSIDERATIONS' - I did not include 'ASK_AMT' in this attempt since there were over 8,000 unique values. I used the same number of layers and nodes as the original model - two hidden layers, one with 80 nodes and the other with 30 nodes. However, I reduced the epochs to 75 since the other models hit their accuracy rate far before 100 epochs. The results of this attempt were similar to the original model, attemp #1, and attempt #2, with 72.59% accuracy and 56.5% loss. 


Overall my results were very similar among all models, with ~72% accuracy and ~56% loss. I believe if I had used the Keras Tuner I would have had more optimal results since the changes I made to my models were ideas to potentially optimize the data, however, none of my ideas increased the accuracy. Also, I may be misunderstanding the number of nodes vs features. I was basing my nodes off the dataset with the dummy values assigned to the strings, which meant my features were 43 vs the 9 features I referenced above. Looking back, I also would have tried using Random Forests to visualize the feature importance and reduced the dataset to only include the most important features.