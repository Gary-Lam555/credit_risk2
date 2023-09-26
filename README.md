# credit_risk2
This repositionary contains the capstone project 2<br/>
The capstone project 1 is located at https://github.com/Gary-Lam555/credit_risk<br/>

<h2>Problem Statement</h2>
<b>Research question you intend to answer</b></br>
In this project, we would like created a reliable machine learning prediction model to predict a new loan whether it may be becoming default (loanee stops to return the loan money) based on a given set of features.<br/>
</br>
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

<h2>Exploratory Data Analysis (EDA)</h2>
<p>BoxPlot</p>
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
<p>Heatmap</p>
Next, we use heatmap to verify the correlations between features and label (default case)<br/>
we notice among all features, Rate/loan rate has the highest correlation with default case (0.5) , however for the Amount/loan amount, it doesn't has strong correlation (0.04) being shown on the map 

<img src=p3a.png>

