
missing_data =round(loan_df.isnull().sum()/len(loan_df)*100,2)
missing_data

columns_with_all_missing_data =list(missing_data[missing_data >50].index)
loan_df =loan_df.drop(columns_with_all_missing_data,axis =1)

#companies without country to clean missing data
companies["country_code"].isnull().sum()

#Count of Null values column-wise
companies.isnull().sum()

#If Company has columns containing Null
companies.isnull().any()

#If Company has any row containing Null
companies.isnull().any(axis=1)
#If Company has any row with all values as Null
companies.isnull().all(axis=1)
#Count of Rows in Companies with all values as Null
companies.isnull().all(axis=1).sum()

#Count of Null values in Companies per Row
companies.isnull().sum(axis=1)

#Companies Columns-wise % of Null Values to understand if any important field has Null values
round(100*(companies.isnull().sum()/len(companies.index)), 2)

#Companies number of rows having more than 5 NaN
companies[companies.isnull().sum(axis=1) > 5]

companies[companies["country_code"].isnull()]
companies[companies["country_code"].isnull()].info()

#Number of companies with more than 3 NaNs
companies[companies.isnull().sum(axis=1) > 3]

#How much of the companies data will we lose if we delete companies with more than 3 NaNs
100*(len(companies[companies.isnull().sum(axis=1) > 3].index) / len(companies.index))
#Delete
companies = companies[companies.isnull().sum(axis=1) <= 3]

#Delete companies with Null value for category_list
companies = companies[companies["category_list"].notnull()]


#Remove NaNs in Raised Amount
rounds2 = rounds2[~np.isnan(rounds2['raised_amount_usd'])]

# Let's analyze unique values in columns in the dataset
for el in list(loan_df.columns):
    print("---------------------------------------------")
    print("No. of unique Values in {elements} :{length_of_unique}".format(elements=el,length_of_unique=len(loan_df[el].unique())))
    print("---------------------------------------------")
    print(loan_df[el].unique())


companies["permalink"] = companies["permalink"].str.lower()

#in sectors, "na" is mistyped as 0
sectors['category_list'] = sectors['category_list'].str.replace('0','na')

#Imputing with "Unknown"
loan_df.fillna(value={'emp_title': "Unknown"},inplace=True)
loan_df.fillna(value={'title': "Debt Consolidation Loan"},inplace=True)

loan_df.fillna(value={'emp_length': '4'},inplace=True)

loan_df.replace(to_replace ="Debt Consolidation", value ="Debt Consolidation Loan",inplace=True) 

#remove null
loan_df =loan_df[~loan_df.revol_util.isnull()]

#Delete Sectors with value 0
sectors = sectors_melted.loc[sectors_melted['value'] == 1]

# Function to fix year issue
def fix_year(x):

    if x > 2011:# Since 2011 is the latest loan issue year

        x = x - 100

    return (x)
loan_df['earliest_cr_line_year'] =loan_df['earliest_cr_line_year'].apply(fix_year)


percent_list =['int_rate','revol_util']
print("Object Type of:",percent_list,"Before Change")
print("----------------------------------")
loan_df[percent_list].info()

for el in percent_list:
    loan_df[el].dtype
    loan_df[el] =loan_df[el].str.strip('%').astype('float64')


#Remove outliers beyond 99%ile
q = master_loan_df["annual_inc"].quantile(0.99)
master_loan_df = master_loan_df[master_loan_df["annual_inc"] < q]
master_loan_df["annual_inc"].describe()    