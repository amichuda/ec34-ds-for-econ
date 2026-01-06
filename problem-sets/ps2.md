# Problem Set 2

In chapter 8 of [Mostly Harmless Econometrics](https://www.mostlyharmlesseconometrics.com/) the authors indicate that 42 is the minimum number of clusters for reliable inference using the standard cluster adjustment of standard errors (p319). However, the authors do not spend time clarifying where that number came from.

For this homework you will explore how 1- the number of clusters and 2- the number of observations, affect the reliability of your estimate of the variance of your OLS estimates.

To do this, you will conduct a Monte Carlo (MC) simulation. The measure of "reliability" ratio of your clustered estimate will be the ratio of a) the average value of the estimate of the clustered standard errors from all the MC simulations relative to b) the standard deviation of the estimated betas from all your MC simulations (sampling distribution).

A ratio close to 1 means your estimate of the clustered SEs is reliable. A ratio substantially below 1 means that your clustered SEs are substantially smaller than the correct ones (this is because the within-cluster correlation is positive).

First, run this code snippet that creates clustered data and plots it:

```python
import pandas as pd

import numpy as np
import seaborn as sns
rng = np.random.default_rng()

r = 10**3 ## number of MC simulations
n = 1000 ## number of observations
g = 100 ## number of clusters
x1 = rng.normal(size=n) + np.tile(rng.normal(size=g), int(n/g)) ## generate clustered X

e1 = rng.normal(size=n) ## unique variance for each observation
e2 = np.tile(rng.normal(size=g), int(n/g)) ## variance common within each cluster
e = e1 + e2
clu = np.tile(range(g), int(n/g)) ## cluster id
clu_df = pd.DataFrame({'clu' : clu, 'e' : e}) ## turn it into a dataframe
sns.scatterplot(x = 'index', y= 'e', data=clu_df.reset_index(), hue='clu', palette='coolwarm')
```

How do the errors look? Are they bunched together? How would you expect the errors to look if there wasn't any clustering?

For your simulation:

Write a function that creates simulated data with different levels of sample sizes (n) and different numbers of clusters (g)

1. Use the code above and adapt it; create a variable y=b0 + b1*x1 + e , where b0=1, and b1=.1
2. Run OLS of y on x with clustered standard errors:
3. Add the parameter into fit to estimate clustered standard errors: `fit(cov_type='cluster', cov_kwds={'groups' : clu_df['clu']})`
4. Loop over the number of clusters (g): 2, 4, 5, 10, 20, 25, 50 and 100.
5. Loop over the sample sizes (n): 100, 200, 500, 10^3 and 10^4
6. Use r=1000 for every MC simulation

When showing the results, please indicate the number of clusters in the x-axis and the "reliability" ratio in the y-axis. Show simulations for different sample sizes in separate lines.

The target plot should be close to the plot below:

![](assets/howmanyclusters%20(1).png)