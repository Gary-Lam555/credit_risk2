# credit_risk2
This repositionary contains the capstone project 2<br/>
The capstone project 1 is located at https://github.com/Gary-Lam555/credit_risk<br/>

<h2>Problem Statement</h2>
<b>Research question you intend to answer</b></br>
In this project, we would like created a reliable machine learning prediction model to predict a new loan whether it may be becoming default (loanee stops to return the loan money) based on a given set of features.<br/>
<br/>
<b>Expected data sources and structure</b><br/>
The dataset can be found from https://www.kaggle.com/datasets/nanditapore/credit-risk-analysis , the dataset is about loan application data for credit risk analysis <br/>
The dataset is presented in csv file format with the following columns </br>
<table>
<tr><td>ID</td><td>Unique identifier for each loan applicant. </td></tr>
<tr><td>Age</td><td> Age of the loan applicant. </td></tr>
<tr><td>Income</td><td> Income of the loan applicant. </td></tr>
<tr><td>Home</td><td> Home ownership status (Own, Mortgage, Rent). </td></tr>
<tr><td>Emp_Length</td><td> Employment length in years. </td></tr>
<tr><td>Intent</td><td> Purpose of the loan (e.g., education, home improvement). </td></tr>
<tr><td>Amount</td><td> Loan amount applied for. </td></tr>
<tr><td>Rate</td><td>Interest rate on the loan. </td></tr>
<tr><td>Status</td><td> Loan approval status (Fully Paid, Charged Off, Current). </td></tr>
<tr><td>Percent_Income</td><td> Loan amount as a percentage of income. </td></tr>
<tr><td>Default</td><td> Whether the loan should be approved (Yes, No). </td></tr>
<tr><td>Cred_Length</td><td> Length of the applicant's credit history.</td></tr>
</table>
</br>
<b>Expected results</b><br/>
create several machine learning models based on the above dataset and locate a best model for prediction of loan default case.<br/>
<br/>
<b>Expected techniques</b><br/>
use jupyter notebook to created multiple machine learning models.<br/>
<br/>

<h2>Initial Report and EDA</h2>
<b>BoxPlot</b><br/>
We have conducted exploratory data analysis in this way. We try to use boxplot to identify the correlation between the features (Age, Income, Emp_length, amount, rates, percent_income, cred_length to default case. </br/>
We identity two things<br/>
1) Loan Amount and Default Case<br/>
Higher loan amount may potentially contribute to loan default case<br/>
<img src=p1a1.png>
<br/>
2) Interest Rate and Default Case<br/>
There are strong correlation between Interest Rate and Default Case, the higher the interest rate, the higher the possisblity of loan default case may happen<br/>
<img src=p2a.png>
<br/>
<b>Heatmap</b><br/>
Next, we use heatmap to verify the correlations between features and label (default case)<br/>
we notice among all features, Rate/loan rate has the highest correlation with default case (0.5) , however for the Amount/loan amount, it doesn't has strong correlation (0.04) being shown on the map 
<img src=p3a.png>
<br/>
<b>Pairplot</b><br/>
We change the Default column value for pairplot Y-> 1 and N->0, from pairplot of Rate feature, we aware default case Y is on the top.<br/>
<img src=p4a.png>
<b>Scatterplot</b><br/>
we try to look into the relationship between Loan amount, loan rate and default case toghether, we can't see there is not strong relationship between loan amount and loan rate, however, we can see <br/>
strong relationship between loan rate and default case,br/>
<img src=p5a.png>
<br/>
<h2>Data Cleaning and Data Preparation</h2><br/>
Before we fit the data into our model, we have conducted some basic cleaning activities on the dataset, this includes dropping off the null values from 
dataset (using df.dropna()). We learn that the null values are concentrated at column Emp_length and Rate. <br/>
Emp_length         895<br/>
Rate              3116<br/>
dtype: int64<br/>
<br/>
We also need to learn the values distribution per each column, this is an important step as we will need to understand whether the column whether contains numeric values or and categorical values (numeric features/categorical features), this will affect how we are going to transform the features later below. <br/>
An example of value distribution can be found from below<br/>
Home feature / Home column<br/>
RENT        14551<br/>
MORTGAGE    11801<br/>
OWN          2192<br/>
OTHER          94<br/>
<br/>
Next, we split our dataset into training dataset and testing dataset in a ratio of 70 to 30. We conduct data transformation right the data split, simply because we don't want to have data leaking in between the two datasets. After that, we conduct data transformation (standardscaler and onehotencoder) for training dataset and test dataset separately. <br/>
Our dataset expands to 18 features
<img src=p9a.PNG>
<br/>
<h2>Model Engineering and Model Evaluation</h2>
4 different models are built and evaluated, we would like to find out the best model to predict the default case (Yes) based on the provided features (18 features after the transformation). These models are <br/>
KNN<br/>
decision tree<br/>
Logistic regression<br/>
SVM<br/>

We evaluate these models based on the test data, the score comparation table can be found below. We notice the highest score model is SVM.<br/>
<img src=p10a.PNG>
<br/>
The historgram of the model comparation can be found from below<br/>
<img src=p11a.PNG>
<br/>
Next we are trying to fine tuning the SVM model to improve the prediction rate further. <br/>
We will use randomizedserchcv to find the best parameters (C, gamma, kernel) for the model. <br/>
C: [0.1,1,10]<br/>
gamma: [1,0.1,0.01,0.001]<br/>
kernel: ['rbf', 'sigmoid', 'linear']<br/>
<br/>
the score is returned as 0.823324, it is slightly woser than the SVM model before tunning and  
Considering the fitting time is too long as it requires 0.41 sec. The model is resource demanding and may not be fit for production use. We therefore turn our attention to linear regression<br/>
<img src=p12a.PNG><br/>
<br/>
We conduct similar parameters tuning for linear regression model via randomizedsearchcv, we want to find the best parameters of C, penalty and solver. <br/>
C = np.logspace(0, 4, num=10)<br/>
penalty = ['l1', 'l2']<br/>
solver = ['liblinear', 'saga']<br/>
<br/>
We got the answer from randomizedsearchcv for best parameters of linear regression model are C=2.7825594022071245, penalty='l1', solver='saga' and the score for these parameters with the model is 0.825535. The score is improved from 0.825419 to 0.825535. <br/>
<img src=p13a.PNG><br/>
<img src=p14a.PNG><br/>
<br/>
We create the confusion matrix for fine tunned linear regression model. By using the confusion matrix, we can understand the 4 different combinations of predicted and actual values. They can be found from below<br/>
<img src=p15a.PNG>
<br/>
True Positive(TP)  =  471<br/>
False Positive(FP) =  481<br/>
True Negative(TN)  =  6622<br/>
False Negative(FN) =  1018<br/>
<br/>
We then look into the values of precision and recall values. <br/>
For recall value, it is 0.31631967763599733, from all the classes we have predicted as positive, how many are actually positive or the formula of recall is TP/(TP + FN) . We get only 0.31 simply beacause the model has failed to predict 1018 positive cases and only 471 positive cases are reported correctly. <br/>
For precision, we get the result of 0.494,  from all the classes we have predicted as positive, 49.4% are actually positive. Precision formula can be calculated as TP/(TP + FP). By using precision value, we understand for those cases predicted by our model, half of them are correct. In other words, precision is mearsuring the quality of th model.
<br/>
As the model can achieve around 50% of prevision, we believe that we can use this model to predict the potential default case of loan payment (not able to return payment). Once we deploy the model to the production, we can continue to fine tune the model.
<br/>










    
