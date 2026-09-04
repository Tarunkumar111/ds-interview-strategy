# Maximum Likelihood, Clearly Explained!!!

**Maximum Likelihood Estimation (MLE)** is one of the most important ideas in statistics.

The core idea is beautifully simple:

> **Choose the parameter values that make the observed data most likely.**

In other words:

```text
Observed data
     ↓
Try different parameter values
     ↓
Calculate likelihood for each
     ↓
Choose the parameter with
the highest likelihood
     ↓
Maximum Likelihood Estimate
```

---

# 1. Start With a Simple Example: A Coin

Suppose we flip a coin **10 times** and observe:

```text
H H H H H H H T T T
```

We got:

```text
7 Heads
3 Tails
```

We don't know whether the coin is fair.

Let:

$$
p=P(Heads)
$$

Our goal is to estimate \(p\).

---

# 2. What Could \(p\) Be?

Maybe:

```text
p = 0.1
p = 0.3
p = 0.5
p = 0.7
p = 0.9
```

Which value makes our observed result:

```text
7 Heads + 3 Tails
```

most plausible?

That's exactly what **maximum likelihood** asks.

---

# 3. Calculate the Likelihood

For 7 heads and 3 tails, the binomial probability is:

$$
P(X=7|p)
=
\binom{10}{7}p^7(1-p)^3
$$

When we're treating the observed data as fixed and changing \(p\), we call this a **likelihood function**:

$$
L(p)
=
\binom{10}{7}p^7(1-p)^3
$$

Now we try different values of \(p\).

For example:

| \(p\) | Likelihood |
| ----: | ---------: |
|   0.1 | Very small |
|   0.3 |      Small |
|   0.5 |      0.117 |
|   0.7 |    ≈ 0.267 |
|   0.9 |    Smaller |

The likelihood is highest around:

$$
p=0.7
$$

Therefore:

$$
\boxed{\hat p_{MLE}=0.7}
$$

---

# 4. Why Does 0.7 Make Sense?

We observed:

```text
7 Heads
3 Tails
```

So the observed proportion of heads is:

$$
\frac{7}{10}=0.7
$$

The maximum likelihood estimate is therefore:

$$
\boxed{\hat p=0.7}
$$

Intuitively:

> A coin that produces heads 70% of the time is the coin that best explains 7 heads out of 10 flips.

---

# 5. The Big Idea

Imagine trying every possible value of \(p\):

```text
p = 0.00 ─────────────────────────── p = 1.00
             ↑
             │
       Calculate likelihood
             │
             ▼

             /\ 
            /  \
           /    \
          /      \
─────────/────────\──────────────
                  ↑
                p = 0.7
```

The highest point is the **maximum likelihood estimate**.

That's where the name comes from:

> **Maximum + Likelihood = the parameter value giving maximum likelihood.**

---

# 6. General Definition

Suppose we have observations:

$$
x_1,x_2,\ldots,x_n
$$

and a statistical model with parameter:

$$
\theta
$$

The likelihood is:

$$
L(\theta|x_1,\ldots,x_n)
$$

MLE chooses:

$$
\boxed{
\hat{\theta}
=
\arg\max_{\theta}L(\theta|data)
}
$$

In plain English:

> **Find the parameter value that maximizes the likelihood of the observed data.**

---

# 7. Probability → Likelihood → MLE

These three concepts fit together:

```text
Probability
    ↓
P(data | θ)
    ↓
View it as a function of θ
    ↓
Likelihood
    ↓
Find θ that maximizes it
    ↓
Maximum Likelihood Estimate
```

So:

```text
Probability → describes possible data
Likelihood  → compares parameter values
MLE         → picks the best parameter value
```

---

# 8. Multiple Observations

Now suppose we have independent observations:

$$
x_1,x_2,\ldots,x_n
$$

The probability of observing all of them is:

$$
P(x_1,x_2,\ldots,x_n|\theta)
$$

Under independence:

$$
P(x_1,\ldots,x_n|\theta)
=
\prod_{i=1}^{n}P(x_i|\theta)
$$

Therefore the likelihood is:

$$
\boxed{
L(\theta)
=
\prod_{i=1}^{n}P(x_i|\theta)
}
$$

MLE finds the \(\theta\) that maximizes this product.

---

# 9. Why Do We Use Log-Likelihood?

Here's a practical problem.

Suppose we have 1,000 observations.

The likelihood might be:

$$
L(\theta)
=
P(x_1|\theta)
P(x_2|\theta)
\cdots
P(x_{1000}|\theta)
$$

Multiplying hundreds or thousands of probabilities can produce extremely tiny numbers.

So we take the logarithm.

$$
\ell(\theta)=\log L(\theta)
$$

Because:

$$
\log(ab)=\log a+\log b
$$

we get:

$$
\boxed{
\ell(\theta)
=
\sum_{i=1}^{n}\log P(x_i|\theta)
}
$$

Much easier to calculate and optimize.

---

# 10. Does Maximizing Log-Likelihood Change the Answer?

No.

Because logarithm is a **monotonically increasing function**.

If:

$$
L(\theta_1)>L(\theta_2)
$$

then:

$$
\log L(\theta_1)>\log L(\theta_2)
$$

Therefore:

$$
\boxed{
\arg\max L(\theta)
=
\arg\max \log L(\theta)
}
$$

So we usually maximize **log-likelihood** instead of likelihood.

---

# 11. MLE for a Normal Distribution

Suppose:

$$
X_1,X_2,\ldots,X_n
\sim N(\mu,\sigma^2)
$$

We don't know:

$$
\mu,\sigma^2
$$

MLE can estimate both.

For the normal distribution, the maximum likelihood estimates are:

$$
\boxed{\hat{\mu}=\bar{x}}
$$

and:

$$
\boxed{
\hat{\sigma}^2_{MLE}
=
\frac{1}{n}
\sum_{i=1}^{n}(x_i-\bar{x})^2
}
$$

Notice something interesting.

The MLE for variance divides by:

$$
n
$$

not:

$$
n-1
$$

---

# 12. Why Is This Interesting?

Earlier we discussed:

> Why does sample variance use \(n-1\)?

Now we can connect the ideas.

The **MLE** of the normal variance is:

$$
\frac{1}{n}\sum(x_i-\bar{x})^2
$$

But this estimator is **biased downward** for finite samples.

The familiar unbiased sample variance is:

$$
s^2=
\frac{1}{n-1}
\sum(x_i-\bar{x})^2
$$

So:

```text
MLE variance
      ↓
divide by n

Unbiased sample variance
      ↓
divide by n − 1
```

This is a great example showing:

> **Maximum likelihood and unbiasedness are different goals.**

---

# 13. MLE Does Not Mean "Unbiased"

This is extremely important.

An estimator can be:

* maximum likelihood
* biased
* consistent
* efficient

These are different properties.

For example, the normal MLE variance estimator:

$$
\hat{\sigma}^2_{MLE}
=
\frac{1}{n}\sum(x_i-\bar{x})^2
$$

is biased for finite \(n\), but it is **consistent**: as \(n\) grows, it converges to the true variance under the usual assumptions.

So:

> **MLE does not automatically mean unbiased.**

---

# 14. MLE and Regression

Maximum likelihood also appears in regression.

For ordinary linear regression:

$$
Y=\beta_0+\beta_1X+\epsilon
$$

If we assume:

$$
\epsilon\sim N(0,\sigma^2)
$$

then maximizing the likelihood with respect to the regression coefficients is equivalent to minimizing:

$$
\sum_{i=1}^{n}(y_i-\hat y_i)^2
$$

That's ordinary **least squares**.

So under the normal-error assumption:

```text
Maximum Likelihood
        ↓
Normal error assumption
        ↓
Maximize likelihood
        ↓
Minimize squared errors
        ↓
Ordinary Least Squares
```

This is a very important connection.

---

# 15. Why Squared Errors Appear

Suppose:

$$
Y_i\sim N(\mu_i,\sigma^2)
$$

The likelihood contains terms like:

$$
e^{-\frac{(y_i-\mu_i)^2}{2\sigma^2}}
$$

Taking logs gives terms involving:

$$
-(y_i-\mu_i)^2
$$

So maximizing log-likelihood is equivalent to minimizing:

$$
\sum_i(y_i-\mu_i)^2
$$

That's why least squares and Gaussian maximum likelihood are mathematically connected.

---

# 16. MLE in Logistic Regression

MLE is especially important in **logistic regression**.

Suppose:

$$
P(Y=1|X)
=
\frac{1}{1+e^{-(\beta_0+\beta_1X)}}
$$

The model gives a probability for each observation.

We then ask:

> Which values of \(\beta_0,\beta_1\) make the observed 0/1 outcomes most likely?

So:

```text
Data
 ↓
Logistic regression model
 ↓
Likelihood
 ↓
Log-likelihood
 ↓
Optimization
 ↓
Estimated coefficients
```

Unlike ordinary linear regression, logistic regression doesn't have the same simple closed-form solution.

Numerical optimization is used.

---

# 17. MLE and Machine Learning

A huge number of machine-learning models can be understood through likelihood.

For example:

### Logistic regression

Maximum likelihood → log loss / cross-entropy

### Linear regression

Gaussian likelihood → squared-error objective

### Naive Bayes

Estimate probabilities from the data

### Poisson regression

Maximum likelihood → Poisson log-likelihood

So MLE is not just an old statistics technique.

It is deeply connected to modern machine learning.

---

# 18. MLE and Loss Functions

This connection is extremely useful.

Suppose:

$$
\ell(\theta)=\log L(\theta)
$$

Maximum likelihood wants to:

$$
\max_\theta \ell(\theta)
$$

Machine learning often minimizes a loss.

So we can instead minimize:

$$
-\ell(\theta)
$$

Therefore:

$$
\boxed{
\text{Maximum Likelihood}
\equiv
\text{Minimum Negative Log-Likelihood}
}
$$

This is why you'll often see:

> **Negative log-likelihood (NLL)**

used as a loss function.

---

# 19. A Simple Visual

Think of likelihood as a mountain:

```text id="i7q3tq"
Likelihood
    ↑
    │
    │             ●
    │           ●   ●
    │         ●       ●
    │       ●           ●
    │     ●               ●
    │   ●                   ●
    └────────────────────────────→
              Parameter θ
                     ↑
                     │
                   MLE
```

MLE is simply:

> **Find the peak.**

---

# 20. What If There Are Multiple Parameters?

Suppose our model has:

$$
\theta=(\theta_1,\theta_2,\theta_3)
$$

Then we're looking for the combination that maximizes likelihood:

$$
(\hat\theta_1,\hat\theta_2,\hat\theta_3)
=
\arg\max_{\theta_1,\theta_2,\theta_3}
L(\theta|data)
$$

Conceptually:

```text
Try parameter combinations
          ↓
Calculate likelihood
          ↓
Find highest point
          ↓
Best parameter combination
```

In multiple dimensions, the "peak" is a point in parameter space rather than a simple point on a 2D curve.

---

# 21. MLE Is Model-Dependent

This is another important idea.

MLE doesn't magically discover the truth without assumptions.

You first choose a model.

For example:

```text
Assume:
Data ~ Normal(μ, σ²)

       ↓

Use MLE
       ↓

Estimate μ and σ²
```

If the model is inappropriate, the MLE can also be inappropriate.

So the workflow is:

```text
Choose a reasonable model
          ↓
Write likelihood
          ↓
Maximize likelihood
          ↓
Estimate parameters
          ↓
Check model assumptions
```

---

# 22. MLE vs Method of Moments

Another common estimation method is **Method of Moments**.

### MLE

Choose parameters that maximize:

$$
L(\theta|data)
$$

### Method of Moments

Choose parameters so that sample moments match theoretical moments.

For example:

$$
\bar X \approx E[X]
$$

Both can produce parameter estimates, but they are based on different principles.

MLE is often especially attractive because of its strong large-sample properties.

---

# 23. MLE vs Bayesian Estimation

This distinction connects directly to our previous discussion of likelihood.

### MLE

Uses:

$$
Likelihood
$$

and finds:

$$
\hat\theta_{MLE}
=
\arg\max_\theta L(\theta|data)
$$

### Bayesian inference

Combines:

$$
Prior\times Likelihood
$$

to obtain:

$$
Posterior
$$

$$
P(\theta|data)
\propto
P(data|\theta)P(\theta)
$$

So:

```text
MLE:

Data
 ↓
Likelihood
 ↓
Best parameter
```

while:

```text
Bayesian:

Prior + Data
     ↓
Likelihood
     ↓
Posterior distribution
```

---

# 24. MLE vs MAP

There's an even closer connection.

**MAP = Maximum A Posteriori estimation.**

MLE:

$$
\hat\theta_{MLE}
=
\arg\max_\theta L(\theta|data)
$$

MAP:

$$
\hat\theta_{MAP}
=
\arg\max_\theta
P(\theta|data)
$$

Using Bayes:

$$
P(\theta|data)
\propto
L(\theta|data)P(\theta)
$$

Therefore MAP maximizes:

$$
L(\theta|data)P(\theta)
$$

So:

```text
MLE → likelihood only

MAP → likelihood + prior
```

If the prior is uniform over the relevant parameter space, MAP and MLE can coincide.

---

# 25. What Happens as Sample Size Gets Larger?

Under regularity conditions, MLE has excellent large-sample properties.

As \(n\) increases, MLE is typically:

### Consistent

$$
\hat\theta\rightarrow\theta
$$

as:

$$
n\rightarrow\infty
$$

### Approximately normal

For large samples:

$$
\hat\theta
\approx
N\left(
\theta,
\frac{1}{n}I(\theta)^{-1}
\right)
$$

where \(I(\theta)\) is the Fisher information per observation under one common convention.

This is one reason MLE is so important for statistical inference.

---

# 26. Fisher Information

Likelihood also leads to **Fisher information**.

Very roughly:

> Fisher information measures how much information the data contain about a parameter.

It is related to the curvature of the log-likelihood.

```text id="5edkmp"
Very sharp likelihood peak
        ↓
Parameter estimated precisely


Very flat likelihood peak
        ↓
Parameter estimated less precisely
```

So:

```text
Likelihood
   ↓
Curvature
   ↓
Fisher information
   ↓
Uncertainty of estimate
```

---

# 27. Likelihood Surface and Uncertainty

Suppose the likelihood looks like:

```text id="8gzxuo"
        Sharp peak
           /\
          /  \
         /    \
────────/──────\────────
             θ
```

The parameter is well identified.

But if it looks like:

```text id="wh3u8h"
        Flat peak
      __________
─────/          \─────
              θ
```

many parameter values explain the data similarly well.

That means greater uncertainty.

---

# 28. Common Mistakes

### ❌ "MLE finds the parameter that is most probable."

Not quite.

MLE finds the parameter value that **maximizes the likelihood of the observed data**.

---

### ❌ "The MLE is always unbiased."

No.

MLE can be biased, especially in small samples.

---

### ❌ "Maximum likelihood gives the probability that the parameter is correct."

No.

Likelihood is not a probability distribution over the parameter.

---

### ❌ "MLE and Bayesian estimation are the same."

No.

MLE uses the likelihood directly.

Bayesian inference combines likelihood with a prior to produce a posterior.

---

### ❌ "We must maximize the raw likelihood."

Not necessarily.

We almost always maximize the **log-likelihood**, because it is mathematically equivalent and computationally easier.

---

### ❌ "MLE guarantees the model is correct."

No.

MLE finds the best parameter values **within the chosen model**.

---

# 29. The Complete MLE Workflow

```text id="f7oyd0"
             Observed data
                   │
                   ▼
            Choose a model
                   │
                   ▼
       Specify P(data | θ)
                   │
                   ▼
          Construct likelihood
                   │
                   ▼
         Take log-likelihood
                   │
                   ▼
          Optimize parameters
                   │
                   ▼
        Maximum likelihood
             estimate
                   │
                   ▼
       Check model + uncertainty
```

---

# 🧠 Mental Model

Imagine you have a **mystery machine**.

You don't know its parameter.

You observe what the machine produced:

```text
Observed data
```

Now try different settings:

```text
θ = 0.1
θ = 0.2
θ = 0.3
...
θ = 0.9
```

For every setting, ask:

> **"How well would this setting explain the data I actually observed?"**

The setting that gives the highest likelihood wins.

```text
Observed data
      ↓
Try parameter values
      ↓
How well does each explain the data?
      ↓
Pick the highest
      ↓
MLE
```

---

# 🎯 Interview-Ready Answer

> **Maximum Likelihood Estimation is a method for estimating model parameters by choosing the parameter values that maximize the likelihood of the observed data. For independent observations, the likelihood is typically the product of the individual data probabilities, and we usually maximize the log-likelihood instead for numerical convenience. MLE is widely used in statistical models and machine learning, including logistic regression, and under suitable conditions has strong large-sample properties such as consistency and approximate normality.**

---

# 🔑 One-Line Takeaway

> **Maximum Likelihood chooses the parameter values that make the observed data most plausible under the chosen statistical model.**
