#check exact value of 25%ile
master_loan_df["loan_amnt"].quantile(.25)

#Divide Loan Amount into Bins
bins = [0, 5000, 10000, 15000, 20000, 25000,45000]
slot = ['0-5000', '5000-10000', '10000-15000', '15000-20000', '20000-25000','25000 and above']
master_loan_df.loc[:, 'loan_amnt_bins'] = pd.cut(master_loan_df['loan_amnt'], bins, labels=slot)

# Correlation data gathering
correlation_data =master_loan_df.corr()
round(correlation_data.fillna(0),2)


# Heatmop plotting on continuous variables
sns.set(font_scale=1.6)
plt.figure(figsize=(30,30))
continous_var= ['loan_amnt','funded_amnt','funded_amnt_inv','int_rate','installment',
       'emp_length', 'annual_inc','dti', 'delinq_2yrs', 'earliest_cr_line_month', 'earliest_cr_line_year',
        'inq_last_6mths', 'open_acc', 'pub_rec', 'revol_bal', 'revol_util','issue_d_month','issue_d_year',
       'total_acc', 'last_pymnt_amnt','pub_rec_bankruptcies', 'last_pymnt_d_month', 'last_pymnt_d_year', 'last_credit_pull_d_month',
       'last_credit_pull_d_year', 'loan_approval_perc']
corr = round(master_loan_df[continous_var].corr(),2)
sns.heatmap(corr, annot=True, center=0.5,cmap="YlGnBu")


# Generating a pivot to see loan_status impact via Grade and loan amount
pivot =master_loan_df.pivot_table(values ='loan_amnt',index =['grade','sub_grade','loan_status'],aggfunc=sum)
pivot

# Create derived variable for dti
master_loan_df['dti_range'] = pd.cut(master_loan_df['dti'], [0,5,10,15,20,25,30], labels=['0-5','5-10','10-15','15-20','20-25','25-30'])