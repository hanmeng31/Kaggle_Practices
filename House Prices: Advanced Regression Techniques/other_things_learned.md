
We can use the following to plot the distribution of data.

sns.distplot(df_train['SalePrice']);

We can use skew() and kurt() to show skewness of data.

print("Skewness: %f" % df_train['SalePrice'].skew())
print("Kurtosis: %f" % df_train['SalePrice'].kurt())

We can use correlation matrix and seaborn library to show the correlation plot.

corrmat = df_train.corr()
f, ax = plt.subplots(figsize=(12, 9))
sns.heatmap(corrmat, vmax=.8, square=True);

If a column has many null values than a threshold (e.g. more than 15%), we can consider delete that column.

There is a need to detect outliers. They can affect models and tell some insights. To detect outliers, we can transform data into a distribution with mean 0 and std 1. If some samples are far from the mean, they might be the outliers.

We can possibly use log transformation to deal with skewness in distribution.