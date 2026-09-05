# Maximum Likelihood for the Binomial Distribution, Clearly Explained!!!

The **Binomial distribution** and **Maximum Likelihood Estimation (MLE)** fit together beautifully.

The goal is simple:

> **We observe a number of successes and failures, and use that data to estimate the probability of success \(p\).**

For the Binomial distribution, the MLE turns out to be wonderfully intuitive:

$$
\boxed{\hat p=\frac{\text{number of successes}}{\text{number of trials}}}
$$

Let's see exactly why.

---

# 1. Start With the Binomial Distribution

The Binomial distribution describes the number of successes in \(n\) independent trials when each trial has the same probability of success \(p\).

$$
X\sim Binomial(n,p)
$$

Its probability mass function is:

$$
P(X=k)
=
\binom nk p^k(1-p)^{n-k}
$$

where:

* \(n\) = number of trials
* \(k\) = number of successes
* \(p\) = probability of success
* \(1-p\) = probability of failure

---

# 2. A Simple Example

Suppose we show an advertisement to **10 people**.

We observe:

```text
Person 1  → Click
Person 2  → No click
Person 3  → Click
Person 4  → Click
Person 5  → No click
Person 6  → Click
Person 7  → Click
Person 8  → No click
Person 9  → Click
Person 10 → No click
```

We got:

$$
6\text{ clicks}
$$

and:

$$
4\text{ non-clicks}
$$

We don't know the true probability of a click.

Let's call it:

$$
p
$$

Our goal is:

> **Estimate \(p\) using Maximum Likelihood.**

---

# 3. What Could \(p\) Be?

Maybe:

```text
p = 0.1
p = 0.3
p = 0.5
p = 0.6
p = 0.8
p = 0.9
```

Which value makes our observed data most plausible?

That's the MLE question.

```text
Observed data
      ↓
6 successes out of 10
      ↓
Try different p values
      ↓
Calculate likelihood
      ↓
Find maximum
      ↓
MLE of p
```

---

# 4. Write the Likelihood

We observed:

$$
k=6
$$

successes out of:

$$
n=10
$$

The Binomial probability is:

$$
P(X=6|p)
=
\binom{10}{6}p^6(1-p)^4
$$

Now treat the observed data as fixed and let \(p\) vary.

That's our likelihood:

$$
L(p)
=
\binom{10}{6}p^6(1-p)^4
$$

We want:

$$
\boxed{
\hat p
=
\arg\max_p L(p)
}
$$

---

# 5. Which \(p\) Makes the Data Most Plausible?

Let's compare a few possibilities.

```text
p = 0.2 → unlikely to see 6 successes
p = 0.4 → possible
p = 0.6 → very plausible
p = 0.8 → possible, but less plausible
```

The likelihood reaches its maximum at:

$$
p=0.6
$$

So:

$$
\boxed{\hat p=0.6}
$$

And notice:

$$
\frac{6}{10}=0.6
$$

That's not a coincidence.

---

# 6. The General Result

Suppose we observe:

$$
k
$$

successes out of:

$$
n
$$

trials.

The likelihood is:

$$
L(p)
=
\binom nk p^k(1-p)^{n-k}
$$

We want to maximize this with respect to \(p\).

The answer is:

$$
\boxed{
\hat p=\frac{k}{n}
}
$$

In words:

> **The MLE of the Binomial success probability is the observed success proportion.**

---

# 7. Let's Derive It

This is where the mathematics becomes interesting.

Start with:

$$
L(p)
=
\binom nk p^k(1-p)^{n-k}
$$

Taking the logarithm:

$$
\ell(p)
=
\log\binom nk
+
k\log p
+
(n-k)\log(1-p)
$$

The first term:

$$
\log\binom nk
$$

doesn't depend on \(p\), so it won't affect where the maximum occurs.

Therefore we can focus on:

$$
\ell(p)
=
k\log p
+
(n-k)\log(1-p)
+
constant
$$

---

# 8. Take the Derivative

Differentiate with respect to \(p\):

$$
\frac{d\ell}{dp}
=
\frac{k}{p}
-
\frac{n-k}{1-p}
$$

Set it equal to zero:

$$
\frac{k}{p}
-
\frac{n-k}{1-p}
=
0
$$

Therefore:

$$
\frac{k}{p}
=
\frac{n-k}{1-p}
$$

Cross multiply:

$$
k(1-p)
=
p(n-k)
$$

Expand:

$$
k-kp
=
np-kp
$$

The \(-kp\) terms cancel:

$$
k=np
$$

Therefore:

$$
\boxed{
\hat p=\frac{k}{n}
}
$$

And we've derived the MLE!

---

# 9. Why Does This Make Intuitive Sense?

Suppose you observe:

```text
9 successes
1 failure
```

The observed success rate is:

$$
\frac{9}{10}=0.9
$$

It makes sense that the coin/process with:

$$
p=0.9
$$

would best explain those observations.

Similarly:

```text
1 success
9 failures
```

gives:

$$
\hat p=0.1
$$

So:

```text
Observed success rate
          ↓
      Best estimate
          ↓
        p̂ = k/n
```

MLE essentially says:

> **"Use the success rate you actually observed."**

---

# 10. The Likelihood Curve

For our example:

$$
n=10,\quad k=6
$$

the likelihood looks conceptually like:

```text
Likelihood
    ↑
    │
    │              ●
    │            ●   ●
    │          ●       ●
    │        ●           ●
    │      ●               ●
    │   ●                    ●
    └────────────────────────────→
    0    .2   .4   .6   .8    1.0
                   ↑
                   │
                  p̂=.6
```

The highest point occurs at:

$$
p=0.6
$$

---

# 11. Why Can We Ignore the Binomial Coefficient?

Remember:

$$
L(p)
=
\binom nk p^k(1-p)^{n-k}
$$

The term:

$$
\binom nk
$$

depends only on \(n\) and \(k\).

Those are already observed and fixed.

It doesn't depend on \(p\).

Therefore multiplying by it only scales the likelihood curve vertically.

It doesn't move the maximum.

So for finding the MLE, we can maximize:

$$
p^k(1-p)^{n-k}
$$

instead.

This is a very common MLE trick:

> **Terms that don't depend on the parameter can be ignored when finding the maximizing parameter value.**

---

# 12. Why Use Log-Likelihood?

Instead of maximizing:

$$
L(p)
=
\binom nk p^k(1-p)^{n-k}
$$

we maximize:

$$
\ell(p)=\log L(p)
$$

because:

$$
\log(ab)=\log a+\log b
$$

This turns multiplication into addition and makes differentiation much easier.

So:

```text
Likelihood
     ↓
Take log
     ↓
Log-likelihood
     ↓
Differentiate
     ↓
Set derivative = 0
     ↓
Solve for p
```

---

# 13. Checking That It Is a Maximum

We found a stationary point.

Let's verify it's actually a maximum.

The second derivative is:

$$
\frac{d^2\ell}{dp^2}
=
-\frac{k}{p^2}
-
\frac{n-k}{(1-p)^2}
$$

For:

$$
0<p<1
$$

this is negative.

Therefore:

$$
\frac{d^2\ell}{dp^2}<0
$$

So the log-likelihood is concave and the solution is indeed a maximum.

---

# 14. Another Way to Understand It

There is an even simpler way to see why:

$$
\hat p=\frac{k}{n}
$$

Suppose the observed data are individual 0/1 outcomes:

```text
1 = Success
0 = Failure
```

For example:

```text
1 1 0 1 0 1 1 0 1 0
```

The sample mean is:

$$
\bar X
=
\frac{1+1+0+1+0+1+1+0+1+0}{10}
$$

$$
\bar X=0.6
$$

For a Bernoulli random variable:

$$
E[X]=p
$$

So the sample mean naturally estimates \(p\).

And for the Binomial likelihood:

$$
\boxed{\hat p=\bar X=\frac{k}{n}}
$$

So MLE and the observed success proportion line up perfectly here.

---

# 15. Binomial MLE vs Binomial Test

Don't confuse these!

### Binomial MLE

Question:

> **What is the best estimate of \(p\)?**

Answer:

$$
\boxed{\hat p=\frac{k}{n}}
$$

### Binomial test

Question:

> **Is the data consistent with a particular hypothesized value \(p_0\)?**

For example:

$$
H_0:p=0.5
$$

These are different tasks.

```text
Data
 │
 ├──→ MLE → estimate p
 │
 └──→ Binomial test → test hypothesis about p
```

---

# 16. MLE vs Hypothesis Testing

Suppose:

```text
100 visitors
60 purchases
```

MLE:

$$
\hat p=\frac{60}{100}=0.60
$$

So our best estimate is:

$$
p=0.60
$$

But suppose we want to test:

$$
H_0:p=0.50
$$

Then we'd use a Binomial test or an appropriate large-sample alternative.

The MLE answers:

> "What is the best estimate?"

The hypothesis test answers:

> "Is 0.50 consistent with the data?"

---

# 17. MLE and Confidence Intervals

MLE gives us a **point estimate**:

$$
\hat p
$$

But we also want to know how uncertain that estimate is.

For example:

$$
\hat p=0.60
$$

doesn't mean the true \(p\) is exactly 0.60.

We might instead obtain a confidence interval such as:

```text
Estimated p = 0.60

Possible range:
        ├───────────────┤
       0.50            0.69
```

The exact interval depends on the method used.

So:

```text
MLE → point estimate

Confidence interval → uncertainty around estimate
```

---

# 18. What Happens as Sample Size Increases?

Suppose the true probability is:

$$
p=0.6
$$

With only 10 trials, we might observe:

```text
4 successes → p̂=.4
5 successes → p̂=.5
6 successes → p̂=.6
7 successes → p̂=.7
```

There's substantial variability.

But with:

```text
10,000 trials
```

the observed success proportion will generally be much closer to the true \(p\).

This is one reason MLE is useful:

> Under suitable conditions, the MLE becomes increasingly accurate as the sample size grows.

---

# 19. MLE and the Law of Large Numbers

The observed proportion is:

$$
\hat p=\frac{k}{n}
$$

As \(n\) becomes large:

$$
\hat p\rightarrow p
$$

under the usual independent-identical Bernoulli setup.

So:

```text
More trials
    ↓
Observed proportion stabilizes
    ↓
p̂ gets closer to true p
```

This is the **consistency** of the estimator.

---

# 20. MLE and Bernoulli Distribution

There's a beautiful connection.

A Bernoulli distribution describes **one** success/failure trial:

$$
X\sim Bernoulli(p)
$$

The Binomial distribution is the sum of \(n\) independent Bernoulli trials:

$$
X_1+\cdots+X_n\sim Binomial(n,p)
$$

The MLE is the same basic idea:

$$
\boxed{
\hat p
=
\frac{\text{successes}}{\text{trials}}
}
$$

So you can think of Binomial MLE as:

> **Estimate the probability of success by the fraction of trials that succeeded.**

---

# 21. Connection to Logistic Regression

This idea becomes much more powerful in logistic regression.

Suppose:

```text
X → probability of success
```

Instead of having one constant \(p\), logistic regression models:

$$
p_i=P(Y_i=1|X_i)
$$

using:

$$
p_i=
\frac{1}{1+e^{-(\beta_0+\beta_1X_i)}}
$$

MLE then finds the coefficients:

$$
\beta_0,\beta_1
$$

that maximize the likelihood of the observed 0/1 outcomes.

So:

```text
Simple Binomial
     ↓
Estimate p

Logistic regression
     ↓
Estimate β₀, β₁, ...
     ↓
Probability depends on X
```

The underlying MLE principle is exactly the same.

---

# 22. MLE and Cross-Entropy

For individual binary observations:

$$
y_i\in\{0,1\}
$$

the likelihood is:

$$
L
=
\prod_i
p_i^{y_i}(1-p_i)^{1-y_i}
$$

Taking the negative log:

$$
-\log L
=
-\sum_i
\left[
y_i\log p_i
+
(1-y_i)\log(1-p_i)
\right]
$$

That's the familiar **binary cross-entropy / log-loss** objective.

So:

```text
Maximum Likelihood
        ↓
Maximize log-likelihood
        ↓
Minimize negative log-likelihood
        ↓
Binary cross-entropy
```

This is one of the most useful connections between statistics and machine learning.

---

# 23. A Practical Example

Suppose an email campaign is sent to:

$$
n=1,000
$$

customers.

You observe:

$$
k=230
$$

clicks.

The MLE is:

$$
\hat p
=
\frac{230}{1000}
$$

$$
\boxed{\hat p=0.23}
$$

So the estimated click probability is:

$$
23\%
$$

And the estimated expected number of clicks in another 1,000 comparable trials would be:

$$
1000(0.23)=230
$$

assuming the same model and conditions.

---

# 24. What If We Observe Zero Successes?

Suppose:

```text
n = 10
k = 0
```

Then:

$$
\hat p=\frac{0}{10}=0
$$

So the MLE is:

$$
\boxed{\hat p=0}
$$

Similarly, if:

```text
n = 10
k = 10
```

then:

$$
\boxed{\hat p=1}
$$

These are legitimate MLEs at the boundaries of the parameter space.

However, in some models such as logistic regression, complete separation can cause MLE estimates to diverge rather than produce finite coefficients.

---

# 25. A Subtle Point: MLE Is Not the Same as "True Probability"

Suppose:

$$
\hat p=0.6
$$

That does **not** prove:

$$
p=0.6
$$

It means:

> **0.6 is the parameter value that maximizes the likelihood given the observed data and chosen Binomial model.**

There is sampling uncertainty.

This is why we may also calculate:

* standard errors
* confidence intervals
* hypothesis tests
* Bayesian posterior distributions

---

# 26. Common Mistakes

### ❌ "MLE proves that \(p=0.6\)."

No.

It gives the value that maximizes likelihood for the observed data.

---

### ❌ "MLE gives the probability that \(p=0.6\)."

No.

Likelihood is not a probability distribution over \(p\).

---

### ❌ "The Binomial test and Binomial MLE are the same."

No.

MLE estimates \(p\).

A Binomial test evaluates a hypothesis about \(p\).

---

### ❌ "The Binomial coefficient determines the MLE."

No.

$$
\binom nk
$$

doesn't depend on \(p\), so it doesn't affect the location of the maximum.

---

### ❌ "MLE always gives an unbiased estimate."

Not as a general rule.

For Binomial/Bernoulli \(p\), the MLE \(\hat p=k/n\) is unbiased:

$$
E[\hat p]=p
$$

But MLE estimators in general do not have to be unbiased.

---

# 27. The Complete Derivation at a Glance

```text
Observed:
n trials
k successes
       │
       ▼
Binomial probability

P(X=k|p)
       │
       ▼
Likelihood

L(p) = C(n,k)pᵏ(1-p)ⁿ⁻ᵏ
       │
       ▼
Take log

ℓ(p) = constant + k log(p)
       + (n-k)log(1-p)
       │
       ▼
Differentiate
       │
       ▼
Set derivative = 0
       │
       ▼
k/p = (n-k)/(1-p)
       │
       ▼
k = np
       │
       ▼
      p̂ = k/n
```

---

# 🧠 Mental Model

Imagine you have a mysterious coin.

You flip it 100 times:

```text
Heads = 63
Tails = 37
```

You ask:

> **"What value of \(p\) makes these observations most plausible?"**

MLE says:

$$
\boxed{
\hat p=\frac{63}{100}=0.63
}
$$

So:

```text
Observed success proportion
            ↓
        MLE of p
```

That's the whole idea.

---

## 🎯 Interview-Ready Answer

> For a Binomial distribution with $n$ trials and $k$ observed successes, the likelihood is
>
> $$
> L(p) = \binom{n}{k}p^k(1-p)^{n-k}
> $$
>
> Taking the log-likelihood, differentiating with respect to $p$, and setting the derivative to zero gives:
>
> $$
> \hat{p} = \frac{k}{n}
> $$
>
> Therefore, the **maximum likelihood estimate of the Binomial success probability is simply the observed proportion of successes**.

---

## 🔑 One-Line Takeaway

> For a Binomial distribution, **Maximum Likelihood estimates the success probability as the observed success rate**:
>
> $$
> \boxed{\hat{p} = \frac{k}{n}}
> $$
