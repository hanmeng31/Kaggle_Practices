There are a few reasons why there are missing data e.g. 'NA' of 'NaN' in a dataset. Reindexing, 

We should not use == np.nan to check if there missing values in data.

When summing data, NA (missing) values will be treated as zero.
If the data are all NA, the result will be 0.
Cumulative methods like cumsum() and cumprod() ignore NA values by default, but preserve them in the resulting arrays. To override this behaviour and include NA values, use skipna=False.

NA groups in GroupBy are automatically excluded.

There are a few methods we can use to clean or fill missing values:
    (1) We can use fillna() method to fill any arbitrary value into all NA locations. For example. df.fillna(0). If we don't want to fill a specific value for all NA, we can use either frontfill or backfill to fill values. For example, df.fillna(method='ffill', limit=3). It will fill NA locations up to 3 locations by using a previous non-NA value. With time-series data, frontfill is very common. We can also use fillna() to fill the mean values for NA locations.
    (2) We can use dropna() method to drop all rows or columns with NA values. For example, df.dropna(axis=0) will drop all rows with NA values.
    (3) We can use interpolate() method to add interpolated values to the NA locations. Depending on the arguments sent to interpolate() method, the function will do the linear interpolation differently.
        * If you are dealing with a time series that is growing at an increasing rate, method='quadratic' may be appropriate.
        * If you have values approximating a cumulative distribution function, then method='pchip' should work well.
        * To fill missing values with goal of smooth plotting, consider method='akima'.
        * When interpolating via a polynomial or spline approximation, you must also specify the degree or order of the approximation.
        


If you want to consider inf and -inf to be “NA” in computations, you can set pandas.options.mode.use_inf_as_na = True.


Lessons learned about treating missing values.
    (1) When the distribution for a feature is not wide and the values of the feature do not depend on other features, then we can use the average of the same type of replace NA values.
    (2) When NA values represent nothing, we may not want to replace them with 0. The reason is that if the distribution of valid values are far from 0, when scale the values between [0, 1], the result will be skewed a lot. Therefore, it will be better to replace NA with the global min value of the feature.
    (3) When the values in NA locations are potentially correlated with other features, it will be great to use interpolation methods (using the relationship with the other features, estimate the possible value for each NA location).
    (4) When the number of NA values is very tiny compared with the total amount of samples, we can consider drop those samples with NA values.