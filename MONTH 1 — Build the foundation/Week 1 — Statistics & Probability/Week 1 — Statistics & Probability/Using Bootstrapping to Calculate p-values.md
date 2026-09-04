# Using Bootstrapping to Calculate P-values, Clearly Explained!!!

Bootstrapping can be used for hypothesis testing, but there is an **important distinction**:

> **Ordinary bootstrap resampling is naturally suited to estimating standard errors and confidence intervals. For a p-value, the resampling procedure generally needs to represent the null hypothesis.**

This is one of the most important ideas to understand.

---

# 1. Quick Recap: What Is a P-value?

A **p-value** measures how surprising our observed result would be **if the null hypothesis \(H_0\) were true**.

For example:

$$
H_0:\mu=100
$$

Suppose we observe:

$$
\bar X=108
$$

The question is:

> **If the true mean were actually 100, how often would we see a result at least this extreme?**

That probability is the p-value.

---

# 2. Where Does Bootstrapping Come In?

Normally, we might use a theoretical distribution:

```text
Observed data
      ↓
Test statistic
      ↓
Theoretical null distribution
      ↓
Tail probability
      ↓
P-value
```

With resampling, we can instead approximate a distribution computationally.

But for a valid hypothesis-test p-value, we need:

```text
Observed data
      ↓
Create resamples consistent with H₀
      ↓
Calculate test statistic
      ↓
Build null distribution
      ↓
Compare observed statistic
      ↓
P-value
```

The key phrase is:

> **Resamples must be generated under the null hypothesis.**

---

# 3. Simple Example

Suppose we want to test whether the average delivery time is different from 30 minutes.

### Hypotheses

$$
H_0:\mu=30
$$

$$
H_1:\mu\ne30
$$

Suppose our sample gives:

$$
\bar X=33
$$

So our observed difference is:

$$
33-30=3
$$

We want to know:

> If the true mean is 30, how unusual is a difference of 3 minutes or more?

---

# 4. Create a Null Distribution

We need to generate many datasets that are consistent with:

$$
H_0:\mu=30
$$

One approach is to **center the observed data around the null value**.

Suppose our original observations are:

$$
[25,28,30,35,37]
$$

Their mean is:

$$
31
$$

But under \(H_0\), we want the mean to be:

$$
30
$$

So we shift every observation by:

$$
30-31=-1
$$

giving:

$$
[24,27,29,34,36]
$$

Now this null-centered dataset has mean 30.

We can resample from this null-centered data.

---

# 5. Generate Bootstrap Samples

From the null-centered data, repeatedly sample **with replacement**.

For example:

### Sample 1

$$
[24,27,27,34,36]
$$

Mean:

$$
29.6
$$

### Sample 2

$$
[29,29,34,36,36]
$$

Mean:

$$
32.8
$$

### Sample 3

$$
[24,24,27,29,36]
$$

Mean:

$$
28.0
$$

Continue thousands of times.

```text id="3t24gi"
Null-centered data
        ↓
Bootstrap sample 1 → mean
Bootstrap sample 2 → mean
Bootstrap sample 3 → mean
Bootstrap sample 4 → mean
       ...
Bootstrap sample 10,000 → mean
        ↓
Null distribution of means
```

---

# 6. Build the Null Distribution

After 10,000 repetitions, you'll have:

$$
\bar X_1^*,\bar X_2^*,...,\bar X_{10000}^*
$$

Plot them:

```text id="h0gk7x"
                Null Distribution

                  ▂▅█████▅▂
               ▂▆██████████▆▂
            ▂▅████████████████▅▂
────────────██████████████████████────────────
                    ↑
                   30
                 H₀ mean
```

This distribution represents the results we might obtain **if \(H_0\) were true**.

---

# 7. Compare the Observed Statistic

Our observed mean was:

$$
33
$$

The null hypothesis says:

$$
\mu=30
$$

So our observed statistic is 3 units away from the null value.

For a two-sided test, we look for bootstrap means at least as far from 30 as our observed mean:

$$
|\bar X^*-30|\ge|33-30|
$$

or:

$$
|\bar X^*-30|\ge3
$$

Graphically:

```text id="jwmw5r"
             Null Distribution

      Tail                         Tail
       ↓                             ↓
     ███                           ███
   ███████                       ███████
█████████████████      █████████████████
──────────────────────────────────────────
        27          30          33
        ←────3────→ ←────3────→
```

The shaded tails represent outcomes at least as extreme as the observed result.

---

# 8. Calculate the P-value

Suppose we generated:

$$
B=10,000
$$

null bootstrap samples.

And:

$$
250
$$

of them were at least as extreme as the observed statistic.

Then:

$$
p\approx\frac{250}{10,000}
$$

$$
\boxed{p\approx0.025}
$$

So the bootstrap p-value is approximately:

$$
\boxed{0.025}
$$

If:

$$
\alpha=0.05
$$

then:

$$
0.025<0.05
$$

Therefore:

$$
\boxed{\text{Reject }H_0}
$$

---

# 9. The Core Formula

For a two-sided bootstrap test, conceptually:

$$
\boxed{
p\approx
\frac{
\#\{\text{null bootstrap statistics at least as extreme as observed}\}
}{
B
}
}
$$

where:

* \(B\) = number of resamples
* numerator = number of resamples at least as extreme as observed

A commonly used finite-simulation adjustment is:

$$
\boxed{
p\approx\frac{k+1}{B+1}
}
$$

where \(k\) is the number of simulated null statistics at least as extreme as the observed statistic.

The \(+1\) adjustment avoids reporting an exact zero simply because no simulated value crossed the observed statistic.

---

# 10. One-Tailed vs Two-Tailed Tests

This is important.

## Right-tailed test

Suppose:

$$
H_1:\mu>30
$$

Observed:

$$
\bar X=33
$$

We count null bootstrap statistics:

$$
\bar X^*\ge33
$$

So:

$$
p\approx
P(\bar X^*\ge33\mid H_0)
$$

---

## Left-tailed test

Suppose:

$$
H_1:\mu<30
$$

Observed:

$$
\bar X=27
$$

We count:

$$
\bar X^*\le27
$$

---

## Two-tailed test

Suppose:

$$
H_1:\mu\ne30
$$

Observed:

$$
\bar X=33
$$

We count results at least as far from 30 in either direction:

$$
|\bar X^*-30|\ge3
$$

---

# 11. The Most Important Distinction: Bootstrap Distribution vs Null Distribution

This is where many people get confused.

### Ordinary bootstrap

You resample from the observed sample.

Purpose:

* estimate standard error
* estimate confidence intervals
* understand sampling variability

```text
Observed sample
      ↓
Resample
      ↓
Bootstrap distribution
```

### Bootstrap hypothesis test

You generate resamples in a way that represents:

$$
H_0
$$

Purpose:

* approximate the null distribution
* calculate a p-value

```text
Observed sample
      ↓
Impose / represent H₀
      ↓
Resample
      ↓
Null distribution
      ↓
P-value
```

### Key idea

> **A p-value requires a null distribution.**

Simply resampling the observed data does not automatically produce the correct null distribution.

---

# 12. Why Can't We Just Use Ordinary Bootstrap Samples?

Suppose the observed mean is:

$$
33
$$

and the null hypothesis says:

$$
\mu=30
$$

If you simply bootstrap from the original data, your bootstrap distribution will generally be centered around approximately:

$$
33
$$

not:

$$
30
$$

So it answers a different question.

```text id="4v3y3u"
Ordinary bootstrap

Observed sample
      ↓
Resample
      ↓
Distribution centered around observed estimate
      ↓
"What would my estimate look like
if my observed sample were representative?"


Null bootstrap

Observed sample
      ↓
Make data consistent with H₀
      ↓
Resample
      ↓
Distribution centered under H₀
      ↓
"How unusual is my observed result
if H₀ were true?"
```

---

# 13. Another Approach: Permutation Tests

For many hypothesis-testing problems, a **permutation test** is more natural than a bootstrap test.

For example, suppose we're comparing:

```text
Control     Treatment
  10           15
  12           17
  14           13
  11           18
```

Null hypothesis:

$$
H_0:\text{no difference between groups}
$$

A permutation test can:

1. Combine all observations.
2. Randomly shuffle group labels.
3. Split them into groups again.
4. Calculate the difference in means.
5. Repeat many times.
6. Compare the observed difference to the resulting null distribution.

```text id="0qk6qj"
Observed groups
      ↓
Shuffle labels
      ↓
New groups
      ↓
Calculate difference
      ↓
Repeat thousands of times
      ↓
Null distribution
      ↓
P-value
```

Permutation tests are often especially intuitive when the null hypothesis is about **exchangeability/no group effect**.

---

# 14. Bootstrap vs Permutation Test

|                                     | Bootstrap                    | Permutation Test               |
| ----------------------------------- | ---------------------------- | ------------------------------ |
| Main purpose                        | Estimate uncertainty         | Test null hypothesis           |
| Resampling                          | Usually with replacement     | Usually shuffle labels/values  |
| Number of observations              | Usually preserved            | Preserved                      |
| Main output                         | SE, CI, distribution         | Null distribution, p-value     |
| Null hypothesis explicitly imposed? | Needed for bootstrap p-value | Usually built into permutation |
| Common use                          | Confidence intervals         | Hypothesis tests               |

Don't interpret this as "bootstrap can't test hypotheses." It can. The important point is that **the resampling scheme must be appropriate for the null hypothesis**.

---

# 15. Connection to the P-value Definition

Remember the definition:

> **P-value = probability of observing a result at least as extreme as the observed result, assuming \(H_0\) is true.**

Bootstrapping approximates that probability computationally.

```text id="6ck2pi"
Assume H₀ is true
       ↓
Generate many null-consistent resamples
       ↓
Calculate statistic each time
       ↓
Look at extreme results
       ↓
Count them
       ↓
Divide by number of simulations
       ↓
Bootstrap p-value
```

That's the whole concept.

---

# 16. Example With Numbers

Suppose we're testing:

$$
H_0:\mu=50
$$

Observed:

$$
\bar X=54
$$

Therefore:

$$
\text{Observed difference}=54-50=4
$$

We generate:

$$
B=20,000
$$

null bootstrap samples.

For a two-sided test, suppose:

$$
k=620
$$

bootstrap means are at least 4 units away from 50.

Then:

$$
p\approx\frac{620+1}{20,000+1}
$$

$$
p\approx0.031
$$

Therefore:

$$
p\approx0.031
$$

At:

$$
\alpha=0.05
$$

we reject \(H_0\).

---

# 17. Python Concept

Conceptually, the algorithm looks like this:

```python
observed_stat = calculate_statistic(data)

null_stats = []

for _ in range(10000):
    null_sample = generate_sample_under_null(data, null_value)
    stat = calculate_statistic(null_sample)
    null_stats.append(stat)

p_value = (
    sum(abs(stat - null_value) >= abs(observed_stat - null_value)
        for stat in null_stats)
    + 1
) / (len(null_stats) + 1)
```

The exact implementation depends heavily on the statistic and null hypothesis.

For a two-group comparison, a permutation test may be more appropriate than this generic bootstrap structure.

---

# 18. What Does a Bootstrap P-value Mean?

Suppose:

$$
p=0.03
$$

Correct interpretation:

> **If the null hypothesis were true, results at least as extreme as the observed result would occur about 3% of the time under the specified resampling/null model.**

Incorrect:

> ❌ "There is a 3% probability that \(H_0\) is true."

Incorrect:

> ❌ "There is a 97% probability that \(H_1\) is true."

Incorrect:

> ❌ "There is a 3% chance that my result is wrong."

---

# 19. How Many Bootstrap Replications?

Common choices might be:

$$
B=1,000
$$

$$
B=5,000
$$

$$
B=10,000
$$

or more.

More repetitions generally make the **Monte Carlo approximation** more stable.

But remember:

> **More bootstrap repetitions do not create more information about the underlying population.**

If your original sample is poor or tiny, running one million resamples doesn't magically fix that.

---

# 20. Important Limitation

Bootstrapping depends on the original sample being reasonably informative about the population or data-generating process.

Potential problems include:

* very small samples
* biased samples
* extreme outliers
* dependence between observations
* time-series structure
* clustered observations
* statistics with unusual sampling behavior

For dependent data, you may need specialized methods such as:

* block bootstrap
* cluster bootstrap
* subject-level bootstrap

---

# 21. The Big Picture

Connect this with everything we've learned:

```text id="4x7h4h"
                    DATA
                      ↓
                Test statistic
                      ↓
              ┌───────┴────────┐
              ↓                ↓
        Theoretical         Resampling
        distribution          method
              │                │
              │                ↓
              │         Null-consistent
              │            resamples
              │                │
              └───────┬────────┘
                      ↓
                Null distribution
                      ↓
             Compare observed result
                      ↓
                   P-value
                      ↓
             Reject / Fail to reject H₀
```

---

# 22. Bootstrapping vs Everything We've Learned

You can now connect several concepts:

### Standard Deviation

$$
SD
$$

→ variability of individual observations.

### Standard Error

$$
SE
$$

→ uncertainty of an estimate.

### Bootstrap

→ computationally approximates the sampling distribution.

### P-value

→ tail probability under \(H_0\).

### Statistical Power

→ probability of detecting a specified real effect.

### Central Limit Theorem

→ theoretical result explaining why sampling distributions can become approximately normal.

The relationship is:

```text id="qj6p9b"
Observed Data
     ↓
Statistic
     ↓
Sampling / Null Distribution
     ↓
     ├── Spread → Standard Error
     │
     ├── Percentiles → Confidence Interval
     │
     └── Extreme tail probability under H₀
                       ↓
                    P-value
```

---

# 23. 🧠 Ultimate Mental Model

Remember this sentence:

> **To calculate a p-value with resampling, create many results that could occur if the null hypothesis were true, then see how often those simulated results are at least as extreme as what you actually observed.**

Or:

```text id="z7jj80"
Assume H₀
    ↓
Resample under H₀
    ↓
Calculate statistic
    ↓
Repeat many times
    ↓
Build null distribution
    ↓
Count extreme results
    ↓
P-value
```

### One-line takeaway

> **Bootstrapping can estimate a p-value by generating many null-consistent resamples and calculating the fraction of simulated test statistics that are at least as extreme as the observed statistic.**

**Important:** For hypothesis testing, don't blindly take an ordinary bootstrap distribution and call its tail area a p-value—the resampling scheme needs to correctly represent the null hypothesis.
