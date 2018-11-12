---
layout: post
title: Regression diagnostics
categories: machinelearning
---

# The Standard regression assumptions

The properties of linear regression estimating are based on 4 assumptions below:

## Assumptions about the form of the model:

$$ Y = \beta_0 + \beta_1 X_1 + ... + \beta_p X_p + \epsilon $$

This is *linearity* assumption. When the linearity assumption does not hold, _transformation_ of the data could be needed.

## Assumptions about the errors:

The errors $\epsilon_i$ are assumed to be _independently and identically distributed_ (iid) normal random variables each with mean zero and a common variances $\sigma^2$. This implies 4 assumptions:

- Normality assumption (normal distribution) of the errors
- Mean zero
- Constant variance assumption (if violated, we have heterogeneity/heteroscedasticity problem)
- Independent-errors assumptions (if violated, we have auto-correlation problem)

## Assumptions about the predictors:

- The predictors variables are nonrandom
- The values of predictors are measured without error.
- The predictors variables are assumed to be linearly independent of each other. (If violated, we have collinearity problem)

## Assumptions about the observation:

All observations are equally reliable and have approximately equal role in determining the regression results and in influencing conclusions.

# Various types of residuals
The analysis of residuals can:
- Detecting model deficiencies
- Pointing to serious violations in standard assumptions
- Suggestion of structure or point to information in data that might be missed or overlooked if the analysis is based only on summary statistics

Linear model:
$$ \hat{y}_i = \hat{\beta}_0 + \hat{\beta}_1 x_{i1} + ... + \hat{\beta}_p x_{ip} $$

Least square residuals:
 $$ e_i = y_i - \hat{y}_i $$

The linear model can be written as alternative form as:
 $$ \hat{y}_i = p_{i1}y_1 + p_{i2}y_2 + ... p_{in}y_n$$

 $p_{ij}$ is given by:

 $$ p{ij} = \frac{1}{n} + \frac{(x_i - \bar{x})(x_j - \bar{x})}{\Sigma (x_i - \bar{x})^2} $$

When i = j:

$$ p_{ii} = \frac{1}{n} + \frac{(x_i - \bar{x})^2}{\Sigma (x_i - \bar{x})^2} $$

The $p_{ii}$ is called the **leverage** value of the ith observation.

The *i* th **Standardized residuals**:
$$z_i = \frac{e_i}{\sigma \sqrt{1- p_{ii}}}$$

If $\sigma$ was estimate by:
$$ \hat{\sigma}^2 = \frac{\Sigma e_i ^2}{n-p-1} = \frac{\Sigma (y_i - \hat{y}_i)^2}{n-p-1} = \frac{SSE}{n-p-1}$$
the Standardized residual is called **_internally studentized residual_**.

If $\sigma$ was estimate by:
$$ \hat{\sigma}_{(i)}^2 = \frac{SSE}{(n-1)-p-1}= \frac{SSE}{n-p-2}$$
the Standardized residual is called **_externally studentized residual_**.

The relationship between 2 forms of residual:

$$ r^* _ i = r_i \sqrt{\frac{n-p-2}{n-p-1-r_i^2}}$$

# Graphical methods

Graphical method can be useful in many ways:
- Detect errors in the data
- Recognize pattern in data
- Explore relationships among variables
- Discover new phenomena
- Confirm or negate assumptions
- Assess the adequacy of a fitted model
- Suggest remedial actions
- Enhance numerical analyses in general

![Anscombe](https://upload.wikimedia.org/wikipedia/commons/thumb/f/f4/Anscombe_with_text.svg/808px-Anscombe_with_text.svg.png "Anscombe quartet")

# Checking _linearity_ and _normality_ assumptions

The following plots can be used to check the linearity and normality assumptions:
- Normal probability plot of the standardized residuals: this is the plot of the ordered standardized residuals vs normal scores. Under normality assumption, this plot should ensemble a (nearly) straight line with an intercept of zero and a slope of one (these are the mean and the standard deviation of the standardize residuals)
- Scatter plots of the standardized residual against each of the predictor variables: Under the standard assumption, the standardized residuals are uncorrelated with each of the predictor variables. Thus, the plot should be a random scatter of points. The transformation could be used in case of violations.
- Scatter plot of the standardized residual vs the fitted values: Under the standard assumption, the standardized residuals are also uncorrelated with the fitted values; therefore, this plot should be a random scatter of points.
- Index plot of the standardized residuals (standardized residuals vs the observation number) if the order is important - time series, spatial ordering... Under the asssumption of independent errors, the point should be scattered randomly within a horizontal band around zero.
