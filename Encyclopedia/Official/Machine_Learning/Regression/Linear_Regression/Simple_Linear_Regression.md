---
title: Simple Linear Regression
listings-disable-line-numbers: true
documentclass: article
toc: true
---

# Introduction

## Goal
The goal of simple linear regressions is to model the relationship between two variables $x$ and $y$ by fitting a linear (affine more generally) function $f$ of the form:
\begin{align}
    \label{eq1}y = f(x) = \beta_0 + \beta_1x
\end{align}
where $x \in \mathbb{R}$ is the independent variable, $y \in \mathbb{R}$ is the dependent variable, $\beta_0 \in \mathbb{R}$ is the intercept, and $\beta_1 \in \mathbb{R}$ is the coefficient of $x$. 

## Underlying Relationship Formulation

There could be underlying unobserved deviations from the equation (\ref{eq1}) which are called [errors](../../../Statistics/Optimization/Errors_and_Residuals/Errors_and_Residuals.pdf). Thus, for any data pair $(x_i, y_i)$, the underlying true relationship between $x_i$ and $y_i$ can be described by involving the error term $\epsilon_i$ into the equation:
\begin{align}
    \label{eq2}y_i = f(x_i)= \beta_0 + \beta_1 x_i + \epsilon_i
\end{align}
This relationship between the true (but unobserved) underlying parameters $\beta_0$ and $\beta_1$ and the data pairs is called a linear regression model. 

## Prediction

It is indispensable to find sufficiently good estimators $\hat{\beta_0}$ and $\hat{\beta_1}$ of $\beta_0$ and $\beta_1$ in simple linear regression problems, so that the predicted value of $y$ is given by:
\begin{align}
    \label{eq3}\hat{y} = \hat{f}(x) = \hat{\beta_0} + \hat{\beta_1} x
\end{align}
for any given value of $x$.

# Estimations of Parameters

## Goal

In order to find a good estimation of $y$ with any given value of $x$, finding decent estimates of $\beta_0$ and $\beta_1$ is essential. I.e., find $\hat{\beta_0}$ and $\hat{\beta_1}$ such that minimizes the [residuals](../../../Statistics/Optimization/Errors_and_Residuals/Errors_and_Residuals.pdf) $\{\hat{\epsilon_i}\}_{i=1}^n$ which are the differences between the actual value of $y_i$ and the predicted value of $y_i$ (i.e. $\hat{y_i}$):
\begin{align}
    \hat{\epsilon_i}
    &\label{eq4}= y_i - \hat{y_i}\\
    &= \beta_0 + \beta_1 x_i + \epsilon_i - \hat{\beta_0} - \hat{\beta_1} x_i \text{, by (\ref{eq2}) and (\ref{eq3})}\\
    &= (\beta_0 - \hat{\beta_0}) + (\beta_1 - \hat{\beta_1}) x_i + \epsilon_i
\end{align}
Note the difference between a residual $\hat{\epsilon_i}$ and an error $\epsilon_i$, see [Errors and Residuals](../../../Statistics/Optimization/Errors_and_Residuals/Errors_and_Residuals.pdf).

## Ordinary Least Square Estimation

### Introduction

The most commonly-used way to estimate the parameters is by least-square regression/estimation or ordinary least square (OLS) estimation. OLS chooses the parameters of a linear function of a set of explanatory variables by the principle of least squares. By [Gauss-Markov Theorem](../../../Statistics/Regression_Analysis/Gauss-Markov_Theorem/Gauss-Markov_Theorem.pdf), under Gauss-Markov assumptions, OLS estimation yields the best linear unbiased estimator (BLUE), i.e. it is the most efficient estimator (i.e. has lowest variance) among all linear unbiased estimators.

### Estimators

The OLS estimation yields $\hat{\beta_0}_{OLS}$ and $\hat{\beta_1}_{OLS}$ by minimizing the sum of Euclidean distance of $y_i$ and $\hat{y_i}$ which is just the sum of squared residuals $\hat{\epsilon_i}$ as described in equation (\ref{eq4}).

The sum of squared residuals with respect of the parameters $\beta_0$ and $\beta_1$ can be denoted as:
\begin{align}
    E_{OLS}(\beta_0,\beta_1)
    &= \displaystyle\sum_{i=1}^n \hat{\epsilon_i}^2\\
    &= \displaystyle\sum_{i=1}^n (y_i - \hat{y_i})^2\\
    \label{eq9}&= \displaystyle\sum_{i=1}^n (y_i - \beta_0 - \beta_1 x_i)^2
\end{align}

Note that the $\beta_0$ and $\beta_1$ here are not the the real value of the parameters but variables to be optimized over.

Thus, the OLS estimator of $\beta_0$ is given by:
\begin{align}
    \hat{\beta_0}_{OLS}
    &= \argmin_{\beta_0} E_{OLS}(\beta_0, \beta_1)
\end{align}

The analytic solution of $\hat{\beta_0}_{OLS}$ can be found by applying the derivative test.

First-derivative test:
\begin{align}
    \frac{\partial E_{OLS}(\beta_0, \beta_1)}{\partial \beta_0}
    &= \frac{\partial \displaystyle\sum_{i=1}^n (y_i - \beta_0 - \beta_1 x_i)^2}{\partial \beta_0} \text{, by (\ref{eq9})}\\
    &= -2 \displaystyle\sum_{i=1}^n (y_i - \beta_0 - \beta_1 x_i)\\
    &= -2 (\displaystyle\sum_{i=1}^n y_i -n\beta_0 - \beta_1 \displaystyle\sum_{i=1}^n x_i)
\end{align}
Set $\frac{\partial E_{OLS}}{\partial \beta_0} = 0$ to get extrema of $E_{OLS}$ with respect to $\beta_0$, denoting the value of $\beta_0$ at the extrema by $\beta_{0extrema}$:
\begin{align}
    &\implies -2 (\displaystyle\sum_{i=1}^n y_i -n\beta_{0extrema} - \beta_1\displaystyle\sum_{i=1}^n x_i) = 0\\
    &\implies \beta_{0extrema} = -\frac{\beta_1 \displaystyle\sum_{i=1}^n x_i - \displaystyle\sum_{i=1}^n y_i}{n}\\
    &\implies \beta_{0extrema} = \bar{y} - \beta_1 \bar{x}
\end{align}
where $\bar{x} = \displaystyle\sum_{i=1}^n x_i$ is the average of $x_i$'s and $\bar{y} = \displaystyle\sum_{i=1}^n y_i$ is the average of $y_i$'s.

Note that for $\hat{\beta_0}_{OLS} = \beta_{0extrema}$, it is necessary to check $\frac{\partial^2 E_{OLS}}{\partial \beta_{0extrema}^2} > 0$ (i.e. second-derivative test). However, from equation (\ref{eq9}), it is obvious that $E_{OLS}$ is a quadratic function opens upwards with respect of $\hat{\beta_0}$, which ensures that $\hat{\beta_0}_{OLS} = \beta_{0extrema} = \argmin_{\beta_0} E_{OLS}(\beta_0, \beta_1)$. Therefore,
\begin{align}
    \hat{\beta_0}_{OLS} = \bar{y} - \beta_1 \bar{x}
\end{align}

The OLS estimator of $\beta_1$ is given by:
\begin{align}
    \hat{\beta_1}_{OLS}
    &= \argmin_{\beta_1} E_{OLS}(\hat{\beta_0}_{OLS}, \beta_1)
\end{align}s

Again, the $\beta_1$ here is not the the real value of the parameter but a variable to be optimized over.

The analytic solution of $\hat{\beta_1}_{OLS}$ can be found by applying the derivative test.

First-derivative test:
\begin{align}
    \frac{\partial E_{OLS}(\hat{\beta_0}_{OLS}, \beta_1)}{\partial \beta_1}
    &= \frac{\partial \displaystyle\sum_{i=1}^n (y_i - \hat{\beta_0}_{OLS} - \beta_1 x_i)^2}{\partial \beta_1} \text{, by (\ref{eq9})}\\
    &= \frac{\partial \displaystyle\sum_{i=1}^n (y_i - (\bar{y} - \beta_1\bar{x}) - \beta_1 x_i)^2}{\partial \beta_1}\\
    &= \frac{\partial \displaystyle\sum_{i=1}^n (y_i - \bar{y} + \beta_1(\bar{x} - x_i))^2}{\partial \beta_1}\\
    &= 2 \displaystyle\sum_{i=1}^n (\bar{x} - x_i)(y_i - \bar{y} + \beta_1(\bar{x} - x_i))
\end{align}
Set $\frac{\partial E_{OLS}}{\partial \beta_1} = 0$ to get extrema of $E_{OLS}$ with respect to $\beta_1$, denoting the value of $\beta_1$ at the extrema by $\beta_{1extrema}$:
\begin{align}
    &\implies 2 \displaystyle\sum_{i=1}^n [(y_i-\bar{y})(\bar{x}-x_i)+\beta_{1extrema}(\bar{x}-x_i)^2] = 0\\
    &\implies \displaystyle\sum_{i=1}^n (y_i-\bar{y})(\bar{x}-x_i)+\beta_{1extrema} \displaystyle\sum_{i=1}^n(\bar{x}-x_i)^2 = 0\\
    &\implies \beta_{1extrema} = \frac{\displaystyle\sum_{i=1}^n (y_i-\bar{y})(x_i-\bar{x})}{\displaystyle\sum_{i=1}^n(\bar{x}-x_i)^2}
\end{align}

For the same reason as described above, $\beta_{1extrema}=\argmin_{\beta_1} E_{OLS}(\hat{\beta_0}_{OLS}, \beta_1)$. Thus,
\begin{align}
    \hat{\beta_1}_{OLS} = \frac{\displaystyle\sum_{i=1}^n (y_i-\bar{y})(x_i-\bar{x})}{\displaystyle\sum_{i=1}^n(\bar{x}-x_i)^2}
\end{align}
