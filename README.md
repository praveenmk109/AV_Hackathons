**PREDICTING EMPLOYEE ATTRITION**
# BRIEF

This employee attrition prediction was unlike any other I have done before.</br>
The time-series sort of entries for each employee was hard to comprehend at first.</br>
The goal was to predict if a currently working employee will be leaving the organization in the upcoming two quarters (01 Jan 2018-01 July 2018).</br>
So, the last working date was the target variable, but to treat this problem as a regression with the multiple time series was difficult.</br>
</br>
Hence, I chose to convert it into a simplified RISK based classification problem.</br>
</br>
  • Choose the data of only the employees that had already quit for training</br>
  • For each entry of such an employee, create a feature named RISK with values as</br>
</br>
    • RISK=0, if the difference between reporting date and last working date is more than 6 months (180 days)</br>
    • RISK=1, if the difference between reporting date and last working date is less than 6 months (180 days)</br>
</br>
After the further pre-processing steps(explained below), a simple logistic regression model showed goodaccuracy, </br>
I found the optimal parameters using GridsearchCV and tuned the threshold to produce a good f1 score for both the classes.</br>
</br>
Unfortunately, I could not figure out how to consider the total business value and quarterly ratings of the employees and thus this model can further be improved.</br>
</br>
# DATA PRE-PROCESSING

• From the dataset, we see that there are 2381 unique employees</br>
• Out of which 1616 had quit the organization, so I decided to use the data only from these employees (10359 entries)</br>
• Next, date columns were converted to datetime object type</br>
• Using these, I created these 2 features for each entry</br>
• Days to Quit : Last working date – Reporting date</br>
• Tenure : Reporting date – Date of joining</br>
• Then, categorical columns were encoded as follows</br>
• Gender – Binomial encoding : Male = 1, Female=0</br>
• Education level – Ordinal encoding</br>
• College=0, Bachelor=1, Master=2</br>
• City : One hot encoding </br>
</br>
• Next, the risk column was created with the condition defined in the brief.</br>
• The number of records per employee was not equal and varying from 1 to 24. Ideally, the records should be made equal, but here I chose to use :</br>
  • the first record where risk was 0 and the last record where risk was 1</br>
  • Now, each employee had 2 entries</br>
 </br>
# MODEL-BUILDING
• For training the model, the dataset was split with shuffle=False, so that the entries per employee remain either in the train split or test split and not both.</br>
• As seen above, there is still imbalance among the binary classes.</br>
• The train data was fit and scaled using the standardscaler and then fed into a logistic regression model to get a benchmark score.</br>
• The accuracy was looking good, but the f1-score for 0 class was not so, owing to the class imbalance in the training dataset</br>

# MODEL-TUNING
• First, using GridSearchCV I found the optimal parameters for the logistic regression model</br>
• To deal with the class imbalance, I decided to modify the threshold and found the threshold that maximizes balanced accuracy and the point where True Positive Rate is equal to the True Negative Rate</br>
• Thus, from the above figure, we see the threshold is around 0.8.</br>
• Setting it to 0.8, we see that the new model’s f1 score increased significantly.</br>

## Please check the html in the repository to get an idea of the  images and  plots described above
