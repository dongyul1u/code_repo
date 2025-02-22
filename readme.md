# Code for Lasso Learning

### Single-variable objective function

We aim to minimize the Lasso objective for a single variable βj.

Expanding the squared term:

$$
|\mathbf{r}_j - \mathbf{X}_j \beta_j\|_2^2 
= \sum_{i=1}^{m} (\,r_{j,i} - X_{i,j}\,\beta_j\,)^2.
$$

Next:

$$
\sum_{i=1}^{m} \Bigl(\,r_{j,i}^2 \;-\; 2\,r_{j,i}\,X_{i,j}\,\beta_j 
\;+\; X_{i,j}^2 \,\beta_j^2\Bigr).
$$

Substituting into the objective function:

$$
\frac{1}{2m} \sum_{i=1}^{m} 
\Bigl(\,r_{j,i}^2 \;-\; 2\,r_{j,i}\,X_{i,j}\,\beta_j \;+\; X_{i,j}^2 \,\beta_j^2\Bigr)
\;+\;\lambda\,|\beta_j|.
$$

Rearranging:

$$
\frac{1}{2m} \sum_{i=1}^{m} X_{i,j}^2\,\beta_j^2 
\;-\;\frac{1}{m} \sum_{i=1}^{m} r_{j,i}\,X_{i,j}\,\beta_j 
\;+\;\frac{1}{2m} \sum_{i=1}^{m} r_{j,i}^2 
\;+\;\lambda\,|\beta_j|.
$$

Since the term 
$$
\tfrac{1}{2m}\sum_{i=1}^m r_{j,i}^2
$$


does not depend on βj, we can ignore it :
$$
\frac{1}{2m} \sum_{i=1}^{m} X_{i,j}^2\,\beta_j^2 
\;-\;\frac{1}{m} \sum_{i=1}^{m} r_{j,i}\,X_{i,j}\,\beta_j 
\;+\;\lambda\,|\beta_j|.
$$

$$
\text{Define } 
\|\mathbf{X}_j\|_2^2 
\;=\; \sum_{i=1}^{m} X_{i,j}^2,
\quad
\rho_j 
\;=\; \sum_{i=1}^{m} \bigl(X_{i,j}\,r_{j,i}\bigr).
$$

Then the function simplifies to:

$$
\frac{1}{2m}\,\|\mathbf{X}_j\|_2^2\,\beta_j^2 
\;-\;\frac{1}{m}\,\rho_j\,\beta_j 
\;+\;\lambda\,|\beta_j|.
$$

### Finding the Optimal Solution using Subgradient Method
For Lasso regression, the L1 penalty term βj is not differentiable at βj = 0, but we can use the **subgradient**:

$$
\frac{\partial}{\partial \beta_j} |\beta_j| =
\begin{cases}
+1, & \text{if } \beta_j > 0, \\
-1, & \text{if } \beta_j < 0, \\
[-1,1], & \text{if } \beta_j = 0.
\end{cases}
$$

Taking the subgradient of the objective function:

$$
\frac{1}{m} \|X_j\|_2^2 \beta_j - \frac{1}{m} \rho_j + \lambda g = 0, \quad \text{where } g \in \frac{\partial}{\partial \beta_j} |\beta_j|.
$$

Rearranging:

$$
\|X_j\|_2^2 \beta_j - \rho_j + m\lambda g = 0.
$$

#### Case 1: βj ≠ 0
If βj > 0, then g = 1, and the equation becomes:

$$
\|X_j\|_2^2 \beta_j = \rho_j - m\lambda.
$$

Solving for βj:

$$
\beta_j = \frac{\rho_j - m\lambda}{\|X_j\|_2^2}.
$$

Similarly, if βj < 0, then g = -1 and the equation becomes:

$$
\|X_j\|_2^2 \beta_j = \rho_j + m\lambda.
$$

Solving for βj:

$$
\beta_j = \frac{\rho_j + m\lambda}{\|X_j\|_2^2}.
$$

#### Case 2: βj = 0
For βj = 0 to be optimal, the subgradient condition requires:

$$
- m\lambda \leq \rho_j \leq m\lambda.
$$

And we will use the mean of the interval. So just take 0 here. 


### Conclusion
For Lasso regression, the optimal solution using the subgradient method is:

$$
\beta_j =
\begin{cases}
\frac{\rho_j - m\lambda}{\|X_j\|_2^2}, & \text{if } \beta_j > 0, \\
\frac{\rho_j + m\lambda}{\|X_j\|_2^2}, & \text{if } \beta_j < 0, \\
0, & \text{if } |\beta_j| = 0.
\end{cases}
$$

This method ensures that small coefficients are shrunk to zero, achieving feature selection while maintaining computational efficiency.
