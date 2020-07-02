loan_df =loan_df.drop(columns_with_all_missing_data,axis =1)


missing_data = missing_data[missing_data != 0]
missing_data

loan_df =loan_df.drop('desc',axis=1)

for el in list(['collections_12_mths_ex_med','chargeoff_within_12_mths','tax_liens','policy_code','acc_now_delinq',
                'delinq_amnt','pymnt_plan','initial_list_status','application_type']):
    loan_df =loan_df.drop(el,axis=1)


# Removing all the null values in column pub_rec_bankruptcies
loan_df =loan_df[~loan_df.pub_rec_bankruptcies.isnull()]

# Removing duplicates in 'id' column
loan_df.drop_duplicates(subset='id',keep=False,inplace=True)

#Check frequency distribution of loan_status
loan_df["loan_status"].value_counts()

#Remove rows with loan_status as Current
loan_df = loan_df[loan_df.loan_status != "Current"]

# Let's the number of unique values in the columns
loan_df.nunique().sort_values()

list(loan_df.columns)

datetime_columns =['issue_d','earliest_cr_line','last_pymnt_d','last_credit_pull_d']
loan_df[datetime_columns].info()

loan_df['issue_d_year'].unique()

loan_df[loan_df.loan_amnt != loan_df.funded_amnt]
loan_df[loan_df.funded_amnt_inv < loan_df.funded_amnt]

loan_df['loan_approval_perc'] =round((loan_df['funded_amnt_inv']/loan_df['loan_amnt'])*100,2)

master_loan_df =loan_df.copy()

master_frame.loc[master_frame['funding_round_type'] == 'seed']['raised_amount_usd'].mean()

#Group by Country to know top countries
by_country = master_frame.groupby('country_code')

#Rank grouped countries by funding amount raised to know the top ones
by_country.raised_amount_usd.sum().sort_values(ascending = False)
top9 = by_country.raised_amount_usd.sum().sort_values(ascending = False).iloc[0:8]

D1 = master_frame.loc[(master_frame['country_code'] == 'USA') & (master_frame['funding_round_type'] == 'venture') & (master_frame['raised_amount_usd'] > 5000000) & (master_frame['raised_amount_usd'] < 15000000)]

D1[(D1['main_sector'] == 'Others')].sort_values('raised_amount_usd', ascending=False)