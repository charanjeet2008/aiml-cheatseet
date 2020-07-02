#Function to draw Distribution Chart for Univariate analysis
#df - Input data frame
#col - column to analyze
def distributionChart(df, col):
    fig, ax=plt.subplots(nrows =1,ncols=2,figsize=(20,8))
    
    #Draw Distribution Plot
    ax[0].set_title("Distribution Plot")
    sns.distplot(df[col],ax=ax[0])

    #Draw Box Plot
    ax[1].set_title("Box Plot")
    sns.boxplot(x=df[col], data=df, orient='v')