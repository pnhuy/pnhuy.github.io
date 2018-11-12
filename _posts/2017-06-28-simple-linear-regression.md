---
layout: post
title: Simple linear model
subtitle: I just want to test the functions.
---

# Building the model

Assuming that we have observations on N objects consisting of a **response variable**\\( Y \\) and a **predictor** \\(X\\).

| Observation | \\( Y \\) | \\( X \\)|
| :------ |:--- | :--- |
| 1 | $y_1$ | $x_1$ |
| 2 | $y_2$ | $x_2$ |
| ... | ... | ... |
| **N** |$y_N$  | $ x_N $ |

The relationship between Response and Predictor (if had) is reprented by the equation:

$$ Y = \beta_0 + \beta_1 X + \epsilon $$

where $\beta_0$ is **constant** (bias in Machine learning language or intercept in geometry language) and $\beta_1$ is **slope** or coefficient. The term $\epsilon$ is called **error**.

![Vertical distance](http://www.sharetechnote.com/image/EngMath_LeastSquare_Calculus_01.png)

To estimate the parameters ($\beta_0 $ and $ \beta_1$), we usually use [**least square method**](https://en.wikipedia.org/wiki/Least_squares). In this problem, we try to minimize the sum of square of the vertical distances from each point to the regression line. The vertical distance represent by:
$$ e = y_i - \hat{y_i}$$
where $y_i$ are the real value and $\hat{y}$ are the fitted value which were calculated by the model. The sum of square error is:

$$ SSE = e^2 = ( y_i - \hat{y_i})^2 = (y_i - \beta_0 - \beta_1 X)^2$$

Solving the minimal problem of SSE gives the answers of $\beta_0$ and $\beta_1$:

$$ \beta_1 = \frac{\Sigma (y_i - \bar{y})(x_i - \bar{x})}{\Sigma (x_i - \bar{x})^2}$$ 

$$ \beta_0 = \bar{y} - \beta_1 \bar{x}$$