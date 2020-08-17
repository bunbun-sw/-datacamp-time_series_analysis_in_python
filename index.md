## Course Notes

The notes are taken from [time series analysis in Python on DataCamp](https://campus.datacamp.com/courses/time-series-analysis-in-python/correlation-and-autocorrelation?ex=1).

### Use pandas to calculate correlations of two time series 
1. calcualate percent changes of both series: `df_changes = df.pct_change()`
2. calculate correlation: `cor = df[col_1].corr(df[col_2])`
Rather than using the values over time, calculate the changes over time for each time series by `df_changes = df.pct_change()`. Then use `corr` to calcualate the correlation. Because the two series can be totally unrelated, but the calculated correlations over the values can be high. 

### statsmodel to apply linear regression model
1. add constant column ones to a dataframe for the regression intercept, otherwise statsmodel will fit it without intercept. `df_with_const=sm.add_constant(df)`
2. run regression `results=sm.OLS(df[dependent_col],df_with_const).fit()`
3. correlation and R-Squared: 
- sign(correlation) = sign(regression slope)
- [corr]^2 = R^2
- R-squared measures how closely the data fit the regression line, so the R-squared in a simple regression is related to the correlation between the two variables. In particular, the magnitude of the correlation is the square root of the R-squared and the sign of the correlation is the sign of the regression coefficient.

### Autocorrelation
- Correlation of a time series with lagged copy of itself
1. Interpretation of autocorrelation
- mean reversion

Following large jumps, up or down, the stock price tends to reverse. Mathmatically, it is called negative correlation. 
- trend following: positive correlation
2. Calculation Steps
- convert data into an interval like weekly or monthly using `resample()`
- compute percentage changes
- calculate autocorrelation using `autocorr()`

3. Confidence Interval of ACF
- Two horizontal dotted line or blue region around 0 is the CI of ACF. If a spike falls out of the region, that means the autocorrelation is significantly different from zero. 
