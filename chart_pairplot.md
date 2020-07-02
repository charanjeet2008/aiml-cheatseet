# Plotting Pair plot
plt.figure(figsize=(14, 14))
columns = ['loan_status', 'loan_amnt', 'int_rate', 'grade', 'sub_grade', 'dti', 'issue_d_year', 'open_acc']
sns.pairplot(master_loan_df[columns], diag_kind='kde')
plt.show()