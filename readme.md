# Code for Lasso Learning

### Single-variable objective function

We aim to minimize the Lasso objective for a single variable $\beta_j$.

Expanding the squared term:

$$
\|\mathbf{r}_j - \mathbf{X}_j \beta_j\|_2^2 
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

Since the term $\tfrac{1}{2m}\sum_{i=1}^m r_{j,i}^2$ does not depend on $\beta_j$, we can ignore it w.r.t.$ \beta_j$:

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
