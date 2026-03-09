---
layout: page
title: U.S. Recession Indicators Analysis
description: An empirical analysis of key economic indicators to forecast the likelihood of a U.S. recession.
img: assets/img/22.jpg
importance: 1
category: work
related_publications: true
---

This project presents an empirical analysis of several key economic indicators to build a predictive model for U.S. recessions. By examining historical data, we can identify patterns that have historically preceded economic downturns and assess the current economic climate.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/Coe.jpg" title="Model Coefficients" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/Cor.jpg" title="Indicator Correlation Matrix" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/Reg.jpg" title="Regression Results" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    A selection of key visualizations from the analysis. From left to right: model coefficients for leading indicators, a correlation matrix of economic variables, and initial regression results.
</div>
<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/Reg.png" title="Regression Summary Output" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    The summary output from the multiple regression model, detailing coefficients, standard errors, p-values, and overall model fit statistics like R-squared.
</div>

The core of the analysis involves building and validating a multiple regression model to predict economic outcomes based on several indicators. I used historical data on variables such as the S&P 500 Price Index, industrial production, CPI, and various Treasury yields. The regression results, shown above, indicate that several factors like the S&P 500 index, industrial production, and long-term interest rates are statistically significant predictors. The model has a moderate explanatory power with an R-squared of approximately 0.38, suggesting these indicators account for a meaningful portion of economic variance.

<div class="row justify-content-sm-center">
    <div class="col-sm-8 mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/cpi_vs_gdp.png" title="CPI vs. GDP Growth" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm-4 mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/gdp_rolling_average.png" title="GDP Rolling Average" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Further visualizations exploring relationships between key variables, such as the relationship between CPI and GDP growth, and time-series trends like the rolling average of GDP.
</div>

### Conclusion

This analysis set out to identify key leading indicators for U.S. recessions using a multiple regression model. The model, with an R-squared of 0.38, demonstrates that a combination of financial and economic variables can explain a significant portion of economic fluctuations.

Key findings from the regression analysis include:
*   **Financial Markets:** The S&P 500 index was found to be a highly significant negative predictor, aligning with the theory that stock market downturns often precede economic recessions.
*   **Real Economy:** Industrial production also showed a strong negative correlation, reinforcing its role as a classic coincident indicator of economic health.
*   **Inflation and Interest Rates:** Both CPI and various long-term Treasury yields (10-year, 30-year) were identified as significant factors. The relationship between different parts of the yield curve and economic expectations appears complex and is a critical area for monitoring.
*   **Other Indicators:** The BBK and Housing indices also proved to be powerful predictors, highlighting the importance of broad market and housing sector health.

While the model provides valuable insights, the moderate R-squared value suggests that other factors not included in this analysis also play a role. Future work could explore non-linear relationships, incorporate a wider range of indicators (such as consumer sentiment or credit spreads), and test alternative modeling techniques like logistic regression or machine learning models for a more direct probabilistic forecast.

Ultimately, this project successfully demonstrates a quantitative approach to recession forecasting, confirming the predictive power of several well-known indicators and providing a framework for ongoing economic monitoring.
