# Analyze_customer_behavior_based_on_transaction_data
Analyze customer behavior based on transaction data

Developing a data analysis project that focuses on understanding and analyzing customer behavior based on transactional data. The goal is to perform Exploratory Data Analysis (EDA) to derive valuable insights into customer preferences, purchasing patterns, and overall behavior.

Data Collection:

Firstly reading a CSV file named "Hackathon_Ideal_Data.csv" using pandas and assigns it to a DataFrame called "ideal_data". It then prints the first 5 rows of the DataFrame to the console. Then reading another CSV file named "Hackathon_Working_Data.csv" using pandas and stores it in a DataFrame called "working_data". It then prints the first 10 rows of the DataFrame to the console.

Data Preprocessing:

working_data.shape:

This code simply returns the shape of the DataFrame working data, which represents the dimensions of the DataFrame. The output will be a tuple containing the number of rows and columns in the DataFrame.

working_data.describe():

The describe() method in pandas DataFrame provides a summary of descriptive statistics for numerical columns in the DataFrame. It includes count, mean, standard deviation, minimum, maximum, and quartile values for each numeric column. This summary is helpful for understanding the distribution and range of values in the dataset.

working_data.isnull().sum():

The isnull() method in pandas DataFrame returns a DataFrame of the same shape as the original, where each element is True if the corresponding element in the original DataFrame is null (NaN), and False otherwise.

The sum() method applied to the result of isnull() then calculates the total number of null values in each column, as summing boolean values treats True as 1 and False as 0.

So, will give the count of null values in each column of the workingdata DataFrame.

working_data.nunique():

The nunique() method in pandas DataFrame returns the number of unique values for each column. It's useful for understanding the variety of data within each column. For example, if a column has many unique values, it may indicate high diversity or granularity in the data. So, will give the count of unique values in each column of the working_data DataFrame.

working_data.loc[working_data.duplicated()]:

The code filters the DataFrame to return only rows that are duplicates. This helps in identifying and examining duplicate records in the dataset.

new_working_data=working_data.loc[~working_data.duplicated()]:

The code creates a new DataFrame by removing duplicate rows from the original DataFrame . The ~ operator is used to negate the boolean mask returned, ensuring that only non-duplicate rows are retained.

Exploratory Data Analysis (EDA): 窗体顶端

new_working_data.reset_index(drop="true"):

The method is used to reset the index of the DataFrame and drop the previous index. By setting drop=true, it indicates that the old index should not be added as a column in the DataFrame.

new_working_data = new_working_data[(new_working_data['PRICE'] != 0) & (new_working_data['VALUE'] != 0) & (new_working_data['BILL_AMT'] != 0)] :

This code filters the DataFrame to remove rows where the values in the columns price, value and bill_amt are all equal to zero.

new_working_data = new_working_data[new_working_data['QTY'] == new_working_data['QTY'].astype(int)]:

This code filters the DataFrame to keep only rows where the values in the 'QTY' column are integer values.

new_working_data.drop(columns=['BRD'], inplace=True) new_working_data.drop(columns=['SSGRP'], inplace=True) new_working_data.drop(columns=['SGRP'], inplace=True)

This code drops the columns 'BRD', 'SSGRP', and 'SGRP' from the DataFrame.

Visualization:

dx=new_working_data['STORECODE'].value_counts()
.plot(kind='bar',title='Top Store Code',color='hotpink') dx.set_xlabel('Store Names') dx.set_ylabel('Count')

This code generates a bar plot showing the count of occurrences of each unique value in the 'STORECODE' column of the DataFrame.

print("DAY VS BILL_AMT") xaxis=new_working_data['DAY'].astype(int) yaxis=new_working_data['BILL_AMT'].astype(int) barlist=plt.bar(xaxis,yaxis,color='maroon')

This code snippet appears to create a bar plot showing the relationship between the 'DAY' column and the 'BILL_AMT' column in the DataFrame.

data_corr=new_working_data[['PRICE', 'VALUE']].corr() sns.heatmap(data_corr,annot=True)

This code snippet calculates the correlation matrix between the columns 'PRICE' and 'VALUE' in the DataFrame and creates a heatmap to visualize the correlations.

plt.pie(new_working_data['MONTH'].value_counts(),labels=['Month1','Month2','Month3'],startangle=90,autopct='%.1f%%')

This code snippet creates a pie chart to visualize the distribution of values in the 'MONTH' column of the DataFrame.

top_10_grp = new_working_data['GRP'].value_counts().head(5) dx = top_10_grp.plot(kind='bar', title='Top 5 GROUPS', color='goldenrod') dx.set_xlabel('GROUP Names') dx.set_ylabel('Count') plt.xticks(rotation=75) # Rotate x-axis labels for better readability if needed plt.tight_layout() plt.show()

This code snippet generates a bar plot to display the top 5 groups ('GRP') based on their frequency counts in the DataFrame.

new_working_data['STORECODE'] = new_working_data['STORECODE'].astype(str).str.extract('(\d+)').astype(int) store_sales = new_working_data.groupby('STORECODE')['BILL_AMT'].sum().reset_index() plt.figure(figsize=(6, 6)) plt.bar(store_sales['STORECODE'], store_sales['BILL_AMT'], color='navy') plt.xlabel('Store Code') plt.ylabel('Total Bill Amount') plt.title('Total Bill Amount by Store Code') plt.show()

This code generates a bar plot to visualize the total bill amount for each store code in the DataFrame.
