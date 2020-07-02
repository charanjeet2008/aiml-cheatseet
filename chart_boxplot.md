# Plotting box plot
bxplt =master_loan_df.boxplot(column='loan_amnt', by='grade',fontsize = 10)
bxplt.set_title('')
bxplt.set_xlabel('Grade')
bxplt.set_ylabel('Loan Amount')
plt.show()

# Plotting box plot
bxplt =master_loan_df.boxplot(column='int_rate', by='sub_grade',fontsize = 10,figsize=(10,5))
bxplt.set_title('')
bxplt.set_xlabel('Sub Grade')
bxplt.set_ylabel('Interest Rate')
plt.show()


# Plotting box plot
plt.figure(figsize=(16,12))
sns.boxplot(data =master_loan_df, x='purpose', y='loan_amnt', hue ='loan_status')
plt.xticks(rotation=90)
plt.title('Purpose of Loan w.r.t Loan Amount')
plt.show()

# Plotting box plot
ax = plt.figure(figsize=(30, 18))
ax = sns.boxplot(x='emp_length',y='loan_amnt',hue='purpose',data=loan_stat)
ax.set_title('Employment Length w.r.t Loan Amount w.r.t Purpose of Loan',fontsize=20,weight="bold")
ax.set_xlabel('Employment Length',fontsize=16)
ax.set_ylabel('Loan Amount',color = 'b',fontsize=16)
plt.show()