# StatQuickie: Thresholds for Significance

The main idea behind **thresholds for significance** is simple:

> **Before analyzing the data, we choose a cutoff for how much evidence we require before rejecting the null hypothesis.**

That cutoff is usually called **\(\alpha\)**, the **significance level**.

---

# 1. What Is a Significance Threshold?

Suppose we're performing a hypothesis test.

We start with:

$$
H_0
$$

and calculate a p-value.

Then we compare the p-value with our chosen significance threshold:

$$
\alpha
$$

A common choice is:

$$
\alpha=0.05
$$

The decision rule is:

$$
p<\alpha
\Rightarrow
\text{Reject }H_0
$$

and:

$$
p\geq\alpha
\Rightarrow
\text{Fail to reject }H_0
$$

---

# 2. Why Do We Need a Threshold?

A p-value is a continuous number:

```text
0.001
0.012
0.034
0.048
0.051
0.20
...
```

We need a rule for deciding when the evidence is sufficiently strong to reject \(H_0\).

So we choose:

$$
\alpha
$$

Think of it as a **decision boundary**.

```text
p-value
  ↓

0 ──────────────── 0.05 ─────────────────── 1
│                  │
│                  │
Reject H₀          Fail to reject H₀
```

---

# 3. What Does \(\alpha=0.05\) Mean?

This is frequently misunderstood.

It does **not** mean:

> "There is a 5% probability that the null hypothesis is true."

It also does not mean:

> "There is a 5% probability that my result is wrong."

Instead:

> **If the null hypothesis is true, a test performed at \(\alpha=0.05\) has a 5% long-run probability of rejecting the null hypothesis incorrectly, under the assumptions of the testing procedure.**

This is the **Type I error rate**.

---

# 4. Type I Error

A Type I error occurs when:

```text
H₀ is actually true
        ↓
We reject H₀
        ↓
False positive
```

For example:

> A drug actually has no effect, but our test concludes that it does.

If we use:

$$
\alpha=0.05
$$

we are controlling the long-run Type I error probability at 5% under the test's assumptions.

---

# 5. Different Significance Thresholds

We don't always have to use 0.05.

Common choices include:

$$
\alpha=0.10
$$

$$
\alpha=0.05
$$

$$
\alpha=0.01
$$

For example:

| \(\alpha\) | Evidence required |
| ---------: | ----------------- |
|       0.10 | Less stringent    |
|       0.05 | Common            |
|       0.01 | More stringent    |
|      0.001 | Very stringent    |

Smaller \(\alpha\) means:

> **We require stronger evidence before rejecting \(H_0\).**

---

# 6. Example

Suppose:

$$
p=0.03
$$

### If:

$$
\alpha=0.05
$$

Then:

$$
0.03<0.05
$$

So:

> Reject \(H_0\).

### But if:

$$
\alpha=0.01
$$

Then:

$$
0.03>0.01
$$

So:

> Fail to reject \(H_0\).

**The same data can lead to different decisions depending on the pre-specified significance threshold.**

---

# 7. Why Should We Choose \(\alpha\) Before Seeing the Results?

This is extremely important.

Imagine running an experiment and getting:

$$
p=0.08
$$

You initially planned:

$$
\alpha=0.05
$$

so the result isn't statistically significant.

Then you say:

> "Let's use 0.10 instead."

Now:

$$
0.08<0.10
$$

and suddenly it's significant.

This is problematic because you're changing the decision rule **after seeing the data**.

It increases the opportunity for false-positive findings and can become a form of **p-hacking**.

Better:

```text
Before experiment
       ↓
Choose α
       ↓
Collect/analyze data
       ↓
Calculate p-value
       ↓
Apply predetermined rule
```

---

# 8. Significance Threshold vs p-value

These are different things.

### Significance threshold

$$
\alpha
$$

is chosen **before the test**.

### p-value

$$
p
$$

is calculated **from the data**.

Then:

$$
p \quad \text{vs} \quad \alpha
$$

determines the conventional decision.

```text
α → Decision threshold
p → Evidence from data
```

---

# 9. Statistical Significance

If:

$$
p<\alpha
$$

we call the result:

> **Statistically significant at the \(\alpha\) level.**

For example:

$$
p=0.02,\quad\alpha=0.05
$$

means the result is statistically significant at the 5% level.

But statistical significance doesn't tell us whether the effect is **important in practice**.

---

# 10. Statistical Significance ≠ Practical Significance

Suppose a new website design increases conversion rate by:

$$
0.01\%
$$

With a huge sample, we might obtain:

$$
p<0.001
$$

So the result is statistically significant.

But a business may decide:

> The improvement is too small to matter.

Conversely, an important effect can fail to reach significance if the study has low power or substantial variability.

So always distinguish:

```text
Statistical significance
        ≠
Practical significance
```

---

# 11. Lowering \(\alpha\) Is Not Always "Better"

Suppose we change:

$$
\alpha=0.05
$$

to:

$$
\alpha=0.01
$$

We're demanding stronger evidence.

This reduces the probability of a Type I error under the null, but it generally makes it harder to detect real effects.

That can increase the chance of a **Type II error**:

```text
H₀ is false
   ↓
Fail to reject H₀
   ↓
False negative
```

So there is a trade-off.

```text
Smaller α
   ↓
Fewer false positives
   ↓
But potentially more false negatives
```

---

# 12. Connection to Statistical Power

Recall:

$$
Power=1-\beta
$$

where \(\beta\) is the Type II error probability.

If we make \(\alpha\) smaller while keeping everything else fixed:

```text
α ↓
 ↓
Harder to reject H₀
 ↓
Power usually ↓
```

To compensate, we may need:

* a larger sample
* a larger detectable effect
* lower variability
* a more efficient study design

---

# 13. One-Tailed vs Two-Tailed Tests

The significance threshold also interacts with the test direction.

Suppose:

$$
\alpha=0.05
$$

For a **two-tailed test**, the rejection region is split across both tails:

```text
        2.5%             2.5%
          ↓                 ↓
───────█████─────────────█████───────
              Center
```

For a **one-tailed test**:

```text
                         5%
                          ↓
────────────────────────█████───────
```

The choice should be based on the hypothesis and study design, not selected after seeing which direction gives significance.

---

# 14. Multiple Testing Changes the Picture

Suppose we perform:

$$
100
$$

hypothesis tests.

If all null hypotheses are actually true and each test uses:

$$
\alpha=0.05
$$

we shouldn't expect zero false positives.

Under simple independence assumptions, the expected number of false positives is:

$$
100(0.05)=5
$$

And the probability of at least one false positive is:

$$
1-(1-0.05)^{100}
$$

which is very high.

That's why multiple-testing procedures such as:

* Bonferroni
* Holm
* Benjamini–Hochberg FDR

may be needed when conducting many tests.

---

# 15. Thresholds and p-hacking

This connects directly to what you learned about **p-hacking**.

Imagine testing:

```text
Analysis 1 → p = .20
Analysis 2 → p = .11
Analysis 3 → p = .07
Analysis 4 → p = .04  ← "Success!"
```

If you keep trying analyses until:

$$
p<0.05
$$

you are exploiting the threshold rather than following a pre-specified analysis plan.

The problem isn't that 0.05 exists.

The problem is **using analytical flexibility to manufacture a significant result**.

---

# 16. The "Magic 0.05" Problem

There is nothing mathematically magical about:

$$
0.05
$$

It became a widely used convention.

Depending on the context, a researcher may choose:

$$
0.10,\quad0.05,\quad0.01
$$

or another threshold.

In high-stakes settings, much stricter standards may be appropriate.

The important thing is:

> **Choose a threshold based on the consequences of errors and the study context, ideally before seeing the results.**

---

# 17. Don't Treat p = 0.049 and p = 0.051 as Worlds Apart

Suppose:

$$
p=0.049
$$

and:

$$
p=0.051
$$

Using:

$$
\alpha=0.05
$$

one is technically significant and the other isn't.

But the evidence represented by these values is extremely similar.

So avoid thinking:

```text
0.049 → Great discovery!
0.051 → Nothing happened!
```

That's an overly rigid interpretation.

It's better to report:

* effect size
* confidence interval
* p-value
* study design
* practical importance

rather than focusing only on whether the p-value crossed 0.05.

---

# 18. Confidence Intervals and Significance

For a two-sided test at:

$$
\alpha=0.05
$$

there is a close relationship with a **95% confidence interval**.

For example:

$$
Difference=5
$$

with:

$$
95\%\,CI=[2,8]
$$

Because zero isn't inside the interval, this corresponds to rejecting:

$$
H_0:\text{Difference}=0
$$

at the 5% level under the usual assumptions.

If:

$$
95\%\,CI=[-1,8]
$$

zero is inside the interval, corresponding to failing to reject the null at the 5% level.

---

# 19. A Better Way to Think About Significance

Don't think:

> "Is the p-value small?"

Think:

> **"Before seeing the data, how much false-positive risk am I willing to tolerate, and does the observed evidence cross that pre-specified threshold?"**

Then separately ask:

> **"How large and practically important is the effect?"**

---

# 🧠 Mental Model

```text
Choose α
   ↓
Collect / analyze data
   ↓
Calculate test statistic
   ↓
Calculate p-value
   ↓
Compare p with α
   ↓
┌───────────────┬────────────────┐
│ p < α         │ p ≥ α          │
│               │                │
│ Reject H₀     │ Fail to reject │
│               │ H₀             │
└───────────────┴────────────────┘
```

And remember:

```text
α → chosen threshold
p → evidence from data
β → Type II error
1 − β → Power
```

---

# 🎯 Interview-Ready Answer

> **The significance threshold, or alpha (\(\alpha\)), is a pre-specified cutoff used to decide whether the evidence against the null hypothesis is strong enough to reject it. A common choice is 0.05, which controls the long-run Type I error rate at 5% under the assumptions of the test. If \(p<\alpha\), we reject the null; otherwise, we fail to reject it. The threshold should generally be chosen before looking at the results, and statistical significance should not be confused with practical significance.**

---

# 🔑 One-Line Takeaway

> **The significance threshold \(\alpha\) is a pre-chosen decision boundary for rejecting \(H_0\); 0.05 is a convention, not a magical number, and crossing it does not by itself tell you whether an effect is practically important.**
