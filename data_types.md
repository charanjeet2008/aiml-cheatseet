type(missing_data)

loan_df['emp_length']=loan_df['emp_length'].str.extract('(\d+)', expand=False)

loan_df['emp_length'].median().astype(str)

loan_df['term'] =loan_df['term'].str.strip('months')

for el in datetime_columns:
    loan_df[el] =pd.to_datetime(loan_df[el], format='%b-%y')

# Let's now convert the datetime columns to month and year for further analysis
loan_df['issue_d_month'] =loan_df['issue_d'].dt.month
loan_df['issue_d_year'] =loan_df['issue_d'].dt.year


# Rounding off to 2 decimal places
round_off_list =['total_pymnt','funded_amnt_inv', 'total_rec_late_fee','collection_recovery_fee']
for el in round_off_list:
    loan_df[el] =round(loan_df[el],2) 

#check exact value of 25%ile
master_loan_df["loan_amnt"].quantile(.25)

sorted(sectors['category_list'].unique().astype(str))

#Split string and save in a new column
master_frame['newcol'] = master_frame["col"].str.split('|').str.get(0)