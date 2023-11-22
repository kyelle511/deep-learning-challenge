# deep-learning-challenge
Module 21 Challenge

Contributor: Katy Yelle

## Repository Structure
    -Main Folder
        -.gitignore
        -AlphabetSoupCharity.ipnyb
        -AlphabetSoupCharity_Optimization.ipnyb
        -README.md

      -Sub Folders
        -images
            -InitialModelSummary.png
            -ModelOptimization1Summary.png
            -unprocesseddataframe.png

## Overview of the Analysis
The nonprofit foundation Alphabet Soup wants a tool that can help it select the applicants for funding with the best chance of success in their ventures. Using machine learning and neural networks, the features in the provided dataset are used to create a binary classifier that can predict whether applicants will be successful if funded by Alphabet Soup. 

The CSV file provided from Alphabet Soup's business team contains more than 34,000 organizations that have received funding from Alphabet Soup over the years. 

## Results

* Data Preprocessing <br>
![Unprocessed Dataframe](/images/unprocesseddataframe.png "Unprocessed Dataframe") <br>

  * Target variable is 'IS_SUCCESSFUL'. 
  * Feature variables are 'APPLICATION_TYPE', 'AFFILIATION', 'CLASSIFICATION', 'USE_CASE', 'ORGANIZATION', 'STATUS', 'INCOME_AMOUNT', 'SPECIAL_CONSIDERATIONS' and 'ASK_AMT'.
  * The variables 'EIN' and 'NAME' were removed from the data because the were not targets or features. 

* Compiling, Training and Evaluating the Model<br>
![Initial Model Summary](/images/InitialModelSummary.png "Initial Model Summary") <br>
  * The initial model had 3 layers (input, hidden and output).  The input layer had 80 neurons, the hidden layer had 30 neurons, and the output layer had 1.  The input and hidden layer both used ReLu activation and the output used an activation of Sigmoid.  The initial 80 neurons was based off the approximately 2 times the input dimension (43), and the hidden layer's neurons were based off less than half of the initial neurons. The model ran for 100 epochs. 
  * The initial model did not achieve target level performance (75%), it achieved 72.9% accuracy. 

* Optimization
  * Model 1 - Additional Data Preprocessing:
      * Removed data rows with a 'STATUS' of 0 and then removed the 'STATUS' column because 34294 had a status of 1 and only 5 had a status of 0.
      * Removed data rows 'SPECIAL_CONSIDERATIONS' equal to Y, and then dropped the 'SPECIAL_CONSIDERATIONS column because there were only 29 Ys in the data. 
      * Combined the 'Family/Parent', 'National', 'Regional' and 'Other' into one bin called 'Other' in the 'AFFILIATION' column. 
      * Reduced the number of bins in the 'INCOME_AMT' column to 'No_Income', 'Lower_Income'and 'Higher_Income'. 
      * Combined the 'Heathcare' and 'Other' into one bin called 'Other' in the 'USE_CASE' column. 

      * Model 1 Compilation:<br>
      ![Model Optimization 1 Summary](/images/ModelOptimization1Summary.png "Model Optimization 1 Summary") <br>
      Similar structure to the initial model, however due to the decrease in input dimensions, the input neurons were reduced to 60, and the hidden layer neurons were reduced to 10. This model did not achieve the target level of performance, it achieved 73.8% accuracy (a slight improvement from the initial model). 
    
  * Model 2 - Automated Hyperparameter Model Optimization: <br>
  ![Model Optimization 2 Best Hyperparameters](/images/besthyperparameters.png "Model Optimization 2 Best Hyperparameters") <br>
      The additionally preprocessed data was then used with keras tuner to determine the best hyperparameters to be used. The identified best hyperparameters were to use the activation 'relu' and 4 layers. It identified 16 neurons for the input layer, then 11, 1, 6, 6 and 1 for the hidden layers. The accuracy achieved was 73.9%.

  * Model 3 - Automated Hyperparameters + increased epochs: <br>
  ![Model Optimization 3 Summary](/images/ModelOptimization3Summary.png "Model Optimization 3 Summary") <br>
      Created using the hyperparameters found through the automated optimization process, however rather than running for the 20 epochs, the number of epochs were increased to 100. The accuracy achieved was 73.6%.


## Summary
Four neural network models were created.  While the models came close with accuracy scores ranging from 72.9% to 73.9% none of them met the target threshold of 75%. Next steps are to utilize a different machine learning model, specifically the Random Forest model to help solve the classification problem with the neural network model. A Random Forest model should perform better because it is robust for non-linear data, and the majority of the dataset is categorical, non-linear data.

