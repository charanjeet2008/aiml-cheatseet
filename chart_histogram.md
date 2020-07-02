#Function to draw Histogram for Univariate analysis
#df - Input Data Frame
#col - Column to analyze
#col - Subcolumn to analyze
#w - width of the plot
#h - height of the plot
def histChart(df,col,hue,w,h):
    temp = pd.Series(data = df[col])
    fig, ax = plt.subplots()
    fig.set_size_inches(w , h)
    ax = sns.countplot(data = df, 
                       x= df[col],
                       order=df[col].value_counts().index,
                       hue = df[hue]) 
        
    totals = df[col].value_counts()
    n_hues = df[hue].unique().size
    temp_totals = totals.values.tolist()*n_hues
    
    #annotate each bar with % wrt of the total in each group
    for p,t in zip(ax.patches,temp_totals):
        height = p.get_height()
        ax.text(p.get_x()+p.get_width()/2.,
            height + 3,
            '{0:.1%}'.format(height/t),
            ha="center", fontsize=15)



#Draw Histogram
histChart(df=master_loan_df,col='loan_amnt_bins',hue='loan_status',w=20,h=5)

#Nested Histogram if number of features are more
#Draw the impact of subgrade on loan status classes
fig, ax = plt.subplots(figsize=(30,15))
master_loan_df.groupby("loan_status").sub_grade.hist(alpha=0.6)  
plt.legend(master_loan_df["loan_status"])
plt.show()



#Plotting bar plot
sns.barplot(x='verification_status', y='loan_amnt', hue="loan_status", data=master_loan_df, estimator=np.mean)
# Plotting bar plot
sns.barplot(x='grade', y='loan_amnt', hue="term", data=master_loan_df, estimator=np.mean)
plt.show()
# Plotting bar plot
plt.figure(figsize=(20,5))
sns.barplot(x='addr_state', y='loan_amnt', hue='loan_status',data=master_loan_df, estimator=np.mean)
plt.xticks(rotation=90)
plt.show()
# Plotting bar plot
plt.figure(figsize=(20,5))
sns.barplot(x='delinq_2yrs', y='loan_amnt', hue='grade',data=master_loan_df, estimator=np.mean)
plt.show()
# Plotting bar plot
plt.figure(figsize=(20,5))
sns.barplot(x='delinq_2yrs', y='int_rate', hue='loan_status',data=master_loan_df, estimator=np.mean)
plt.show()


#Plot 2 - simple
countries = ['USA', 'CHN', 'GBR', 'IND', 'CAN', 'RUS', 'DEU', 'ISR']  
def venture_count(n):
    return (master_frame.loc[(master_frame['country_code'] == n) & (master_frame['funding_round_type'] == 'venture')]['raised_amount_usd'].sum())/1000000

venture = list(map(venture_count, countries))
plt.bar(countries, venture, color="#f3e151")  


plt.xlabel('Countries')  
plt.ylabel('Investment in Million USD')

plt.show()


#Plot 3 - sections of eachbar
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt

countries = ('USA','GBR','IND')

index = pd.Index(countries, name='Plot 3')

data = {
    'Others': (2422, 129, 78),
    'Social, Finance, Analytics, Advertising': (2216,118,45),
    'Cleantech / Semiconductors': (1950,121,0),
    'News, Search and Messaging': (0,0,41)
}

df = pd.DataFrame(data, index=index)
ax = df.plot(kind='bar', stacked=True, figsize=(18.5, 10.5))
ax.set_ylabel('Number of Investments')
plt.savefig('stacked.png')
plt.show()
