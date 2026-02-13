This project aims to design a regime-switch detection method and a stressed VaR to capture VaR exceptions from delta-normal model in the Treasury bond market.  
  
To validate the use of delta-normal VaR as the baseline model, daily par yield change (dy) of bonds at multiple tenors are tested using QQ plot to ensure normality. While dy of shorter tenor bonds shows a higher kurtosis and more tail movements, those with longer tenors converge to normal distribution, which makes delta normal VaR appropriate as a risk measure.   
  
Then derived semi annual discount factors (df) by bootstrapping from par yields of bonds with 6-mo, 1-yr, 2-yr, 5-yr, 7-yr, and 10-yr tenor, interpolating with constant semi annual depreciation rate assumption, i.e. df_1.5yr = df_1yr * c, df_2yr = df_1.5yr * c. Used covariance matrix of dy over the last 252 trading days (1 year) and df to calculate KRDV and delta-normal VaR.  

Since dy tends to be normally distributed, most losses would fall into the range of delta-normal VaR under normal market conditions, and detecting outliers becomes the key of preventing extreme tail losses.  

The regime-switch detection method therefore uses mahalanobis distance and a chi-square test. Upon an outlier, model assumes a stressed market over 10 trading days (2 weeks), and multiplies VaR by a ratio (current short term (10 days) PnL volatility to the median of short term PnL volatility) to be stressed VaR.  

Backtested on data from 1990 - 2025, stressed VaR reduces exceptions by 50 percents and passes both unconditional test and independence test. Applied PCA to exceptions and calculated dot products of exceptions dy and first 3 PCs as a measure of dy movements, concluded VaR exception was mainly caused by shift in first PC (level) and stressed VaR can capture level movements but fails when there is shift in PC combination.
