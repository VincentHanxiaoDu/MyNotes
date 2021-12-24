---
title: Gauss-Markov Theorem (Matrix Form)
listings-disable-line-numbers: true
documentclass: article
toc: true
---

# Statement of Gauss-Markov Theorem

\begin{theorem}[Gauss-Markov theorem]
Suppose there is a linear model $Y=X\underaccent{\tilde}{\beta}+
\underaccent{\tilde}{\epsilon}$, where $X$ is an $n \times d$ design matrix,
$\underaccent{\tilde}{\beta}$ is a $d \times 1$ matrix of weights (i.e. coefficients), and
$\underaccent{\tilde}{\epsilon}$ is a $n \times 1$ matrix of \href{../../Optimization/Errors_and_Residuals/Errors_and_Residuals.pdf}{errors}
$\epsilon_i$'s, $i \in [n]$. 

Under the Gauss-Markov Assumptions, i.e.:
\begin{enumerate}
\def\labelenumi{\arabic{enumi}.}
\item
  \label{assumption1}$\epsilon_i$'s have mean zero, 
  
  i.e. $\mathbb{E}[\epsilon_i]=0, \forall i \in [n]$.
\item
  \label{assumption2}$\epsilon_i$'s are \href{https://en.wikipedia.org/wiki/Homoscedasticity}{homoscedastic}, 
  
  i.e. $Var[\epsilon_i]=\sigma^2 < \infty, \forall i \in [n]$.
\item
  \label{assumption3}Distinct error terms are uncorrelated, 
  
  i.e. $Cov[\epsilon_i, \epsilon_j]=0, \forall i \neq j$ \& $i, j \in [n]$.
\end{enumerate}
or equavalently to the above assumptions, $\mathbb{E}[\underaccent{\tilde}{\epsilon}] = \underaccent{\tilde}{0}$, $Var[\underaccent{\tilde}{\epsilon}]=\sigma^2I$, where $\sigma^2 < \infty$ and $I$ is an $n \times n$ identity matrix, we have that the ordinary least square (OLS) estimator of the parameter $\underaccent{\tilde}{\beta}$:
$$\hat{\underaccent{\tilde}{\beta}}_{OLS} = (X^TX)^{-1}X^TY$$
is the best linear unbiased estimator (BLUE), i.e. it is the most efficient estimator (i.e. has lowest variance) among all linear unbiased estimators.
\end{theorem}

# Proof of Gauss-Markov Theorem

\begin{proof}
The OLS estimator:
\begin{align}
\hat{\underaccent{\tilde}{\beta}}_{OLS}&=(X^TX)^{-1}X^TY\\
&=(X^TX)^{-1}X^T(X\underaccent{\tilde}{\beta} + \underaccent{\tilde}{\epsilon})\\
&=(X^TX)^{-1}X^TX\underaccent{\tilde}{\beta}+(X^TX)^{-1}X^T\underaccent{\tilde}{\epsilon}\\
&=\label{eq4}\underaccent{\tilde}{\beta}+(X^TX)^{-1}X^T\underaccent{\tilde}{\epsilon}
\end{align}

Thus, the unbiasedness of $\hat{\underaccent{\tilde}{\beta}}_{OLS}$ is given by:
\begin{align}
\mathbb{E}[\hat{\underaccent{\tilde}{\beta}}_{OLS}] &= \mathbb{E}[\underaccent{\tilde}{\beta}+(X^TX)^{-1}X^T\underaccent{\tilde}{\epsilon}]\\
&=\underaccent{\tilde}{\beta}+(X^TX)^{-1}X^T\mathbb{E}[\underaccent{\tilde}{\epsilon}]\\
&=\underaccent{\tilde}{\beta}\text{, since by assumption \ref{assumption1}, $\mathbb{E}[\underaccent{\tilde}{\epsilon}]=\underaccent{\tilde}{0}$.}
\end{align}

Also by assumption \ref{assumption1},
\begin{align}
\label{eq8}Var[\underaccent{\tilde}{\epsilon}]=\mathbb{E}[(\underaccent{\tilde}{\epsilon}-\mathbb{E}[\underaccent{\tilde}{\epsilon}])(\underaccent{\tilde}{\epsilon}-\mathbb{E}[\underaccent{\tilde}{\epsilon}])^T]=\mathbb{E}[\underaccent{\tilde}{\epsilon}\underaccent{\tilde}{\epsilon}^T]=\sigma^2I
\end{align}

Thus,
\begin{align}
\label{eq9}Var[Y]=Var[X\underaccent{\tilde}{\beta}+\underaccent{\tilde}{\epsilon}] = Var[\underaccent{\tilde}{\epsilon}] = \sigma^2I
\end{align}

The variance of $\hat{\underaccent{\tilde}{\beta}}_{OLS}$:
\begin{align}
Var[\hat{\underaccent{\tilde}{\beta}}_{OLS}] &= \mathbb{E}[(\hat{\underaccent{\tilde}{\beta}}_{OLS}-\underaccent{\tilde}{\beta})(\hat{\underaccent{\tilde}{\beta}}_{OLS}-\underaccent{\tilde}{\beta})^T]\\
&= \mathbb{E}[((X^TX)^{-1}X^T\underaccent{\tilde}{\epsilon})((X^TX)^{-1}X^T\underaccent{\tilde}{\epsilon})^T]\text{, by (\ref{eq4})}\\
&= \mathbb{E}[(X^TX)^{-1}X^T\underaccent{\tilde}{\epsilon}\underaccent{\tilde}{\epsilon}^TX(X^TX)^{-1}]\\
&= (X^TX)^{-1}X^T\mathbb{E}[\underaccent{\tilde}{\epsilon}\underaccent{\tilde}{\epsilon}^T]X(X^TX)^{-1}\\
&= (X^TX)^{-1}X^T\sigma^2IX(X^TX)^{-1} \text{, by (\ref{eq8})}\\
&= \sigma^2(X^TX)^{-1}X^TX(X^TX)^{-1}\\
&\label{eq16}= \sigma^2(X^TX)^{-1}
\end{align}

For any unbiasedness linear estimator $\hat{\underaccent{\tilde}{\beta}}$ for $\underaccent{\tilde}{\beta}$, it must can be expressed in the linear form by the definition of linear estimators:
$$\hat{\underaccent{\tilde}{\beta}} = CY$$
for some constant matrix $C$ where $C$ is independent to $\underaccent{\tilde}{\beta}$ which is unobservable.

Let $D$ be a matrix so that
\begin{align}
\label{eq17}D = C - (X^TX)^{-1}X^T \iff C = D + (X^TX)^{-1}X^T.
\end{align}
Additionally, by the unbiasedness of $\hat{\underaccent{\tilde}{\beta}}$:
\begin{align}
\label{eq18}\mathbb{E}[\hat{\underaccent{\tilde}{\beta}}] &= \underaccent{\tilde}{\beta}
\end{align}

Thus,
\begin{align}
\mathbb{E}[\hat{\underaccent{\tilde}{\beta}}] &= \mathbb{E}[CY]\\
&= \mathbb{E}[(D + (X^TX)^{-1}X^T)(X\underaccent{\tilde}{\beta}+\underaccent{\tilde}{\epsilon})]\\
&= \mathbb{E}[DX\underaccent{\tilde}{\beta} + D\underaccent{\tilde}{\epsilon} + (X^TX)^{-1}X^TX\underaccent{\tilde}{\beta} + (X^TX)^{-1}X^T\underaccent{\tilde}{\epsilon}]\\
&= DX\underaccent{\tilde}{\beta} + D\mathbb{E}[\underaccent{\tilde}{\epsilon}] + \underaccent{\tilde}{\beta} + (X^TX)^{-1}X^T\mathbb{E}[\underaccent{\tilde}{\epsilon}]\\
&= DX\underaccent{\tilde}{\beta} + \underaccent{\tilde}{\beta} \text{, by assumption \ref{assumption1}}\\
&= \underaccent{\tilde}{\beta} \text{, by (\ref{eq18})}\\
&\implies DX\underaccent{\tilde}{\beta}=\underaccent{\tilde}{0}\\
&\label{eq26}\implies DX=\underaccent{\tilde}{0}
\end{align}

Finally, the variance of any unbiased linear estimator $\hat{\underaccent{\tilde}{\beta}}$ of $\underaccent{\tilde}{\beta}$:
\begin{align}
Var[\hat{\underaccent{\tilde}{\beta}}] &= Var[CY]\\
&= CVar[Y]C^T\\
&= C\sigma^2IC^T \text{, by (\ref{eq9})}\\
&= \sigma^2(D + (X^TX)^{-1}X^T)(D + (X^TX)^{-1}X^T)^T \text{, by (\ref{eq17})}\\
&= \sigma^2[DD^T + DX(X^TX)^{-1}\\
&+ (X^TX)^{-1}(DX)^T + (X^TX)^{-1}X^TX(X^TX)^{-1}]\\
&= \sigma^2DD^T + \sigma^2(X^TX)^{-1} \text{, by (\ref{eq26})}\\
&= Var[\hat{\underaccent{\tilde}{\beta}}_{OLS}] + \sigma^2DD^T \text{, by (\ref{eq16})}
\end{align}

Notice that $\sigma^2 \geq 0$ and $DD^T$ is always \href{https://en.wikipedia.org/wiki/Definite_matrix}{definite symmetric}.

Therefore, $\hat{\underaccent{\tilde}{\beta}}_{OLS}$ has the lowest variance among all linear unbiased estimators of $\underaccent{\tilde}{\beta}$ so that it is the best linear unbiased estimator (BLUE).

\end{proof}
