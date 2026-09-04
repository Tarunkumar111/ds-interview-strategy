# P-values: What They Are and How to Interpret Them

A **p-value** is one of the most important concepts in hypothesis testing.

The simplest way to remember it is:

> **A p-value tells us how surprising our observed result would be if the null hypothesis (H₀) were actually true.**

---

## 1. Start with an Example

Suppose a company claims:

> **"Our new website does not change the conversion rate."**

We want to test whether the new website actually improves conversion.

### Hypotheses

```text
H₀: New website does not improve conversion
H₁: New website improves conversion
```

We run an A/B test and observe:

```text
Old website → 10% conversion
New website → 12% conversion
```

The new website looks better.

But the difference could simply be due to **random sampling variation**.

So we perform a statistical test and get:

```text
p-value = 0.03
```

Now what does **0.03** mean?

---

# 2. What Does p = 0.03 Mean?

It means:

> **Assuming H₀ is true, there is a 3% probability of observing a result this extreme or more extreme.**

In simpler words:

> **If there were really no improvement, getting a result this unusual would be quite unlikely.**

Therefore, the data provides evidence **against H₀**.

---

# 3. What a p-value Does NOT Mean

This is extremely important.

### ❌ Incorrect

> "There is a 3% probability that H₀ is true."

A p-value does **not** tell you the probability that H₀ is true.

### ❌ Incorrect

> "There is a 97% probability that H₁ is true."

A p-value does **not** tell you the probability that H₁ is true either.

### ✅ Correct

> **"If H₀ were true, the probability of observing a result at least this extreme is 3%."**

---

# 4. Why Do We Compare p-value with α?

Before performing the test, we choose a **significance level**, usually:

$$
\alpha = 0.05
$$

Then compare:

```text id="0f9f1r"
p-value < α
```

or

```text id="5gd3rj"
p-value ≥ α
```

### Case 1: p-value < α

Example:

```text
p = 0.03
α = 0.05
```

Since:

$$
0.03 < 0.05
$$

We:

> **Reject H₀**

There is statistically significant evidence against the null hypothesis.

---

### Case 2: p-value ≥ α

Example:

```text
p = 0.20
α = 0.05
```

Since:

$$
0.20 > 0.05
$$

We:

> **Fail to reject H₀**

We don't have sufficient evidence to reject the null hypothesis.

**Important:** This does NOT prove that H₀ is true.

---

# 5. Think of p-value as "Evidence Against H₀"

A useful mental model:

```text
Small p-value
     ↓
Data is unusual under H₀
     ↓
Strong evidence against H₀
     ↓
Reject H₀


Large p-value
     ↓
Data isn't particularly unusual under H₀
     ↓
Weak evidence against H₀
     ↓
Fail to reject H₀
```

Generally:

> **Smaller p-value → stronger evidence against H₀**

But don't treat p-values as a direct measure of the **size of an effect**.

---

# 6. Example: A/B Testing

Suppose you're testing a new button design.

```text
Old button → 8.0% conversion
New button → 8.5% conversion
```

You perform a statistical test.

### Result:

```text
p-value = 0.01
```

Using:

```text
α = 0.05
```

We have:

$$
0.01 < 0.05
$$

Therefore:

> **Reject H₀.**

There is statistically significant evidence that the new button changes/improves conversion, assuming the test and its assumptions are appropriate.

---

# 7. But p-value Doesn't Tell You Effect Size

This is a **very important Data Science concept**.

Imagine you have a huge dataset with millions of users.

You find:

```text
Old conversion = 10.000%
New conversion = 10.001%

p-value = 0.001
```

The result can be statistically significant because the sample size is enormous.

But the actual improvement is:

```text
0.001 percentage points
```

That may be practically useless.

Therefore, when analyzing experiments, look at:

* **p-value** → evidence against H₀
* **Effect size** → how large is the difference?
* **Confidence interval** → plausible range for the effect
* **Business impact** → does the change actually matter?

---

# 8. What Happens When the p-value is Very Small?

Suppose:

```text
p = 0.0001
```

This means the observed result would be **very unusual if H₀ were true**.

So we have strong evidence against H₀.

But don't say:

> "The probability H₀ is true is 0.01%."

That's incorrect.

Instead say:

> **"The data provides very strong evidence against H₀."**

---

# 9. p-value and Significance Level

Here's the key relationship:

| p-value | Compared with α = 0.05 | Decision                   |
| ------: | ---------------------- | -------------------------- |
|   0.001 | < 0.05                 | Reject H₀                  |
|    0.01 | < 0.05                 | Reject H₀                  |
|    0.04 | < 0.05                 | Reject H₀                  |
|    0.05 | = 0.05                 | Depends on predefined rule |
|    0.10 | > 0.05                 | Fail to reject H₀          |
|    0.50 | > 0.05                 | Fail to reject H₀          |

---

# 10. A Common Misunderstanding

Suppose:

```text
p = 0.06
```

and:

```text
α = 0.05
```

You might think:

> "0.06 is very close to 0.05, so the result is almost significant."

Be careful.

Under the predefined threshold:

$$
0.06 > 0.05
$$

So you **fail to reject H₀**.

Don't change α after seeing the result just to obtain significance.

---

# 11. One-Tailed vs Two-Tailed p-values

The p-value depends on the **hypothesis test being performed**.

For example:

### One-tailed

You specifically test:

$$
H_1: \mu_{new} > \mu_{old}
$$

You're only interested in whether the new system is **better**.

### Two-tailed

You test:

$$
H_1: \mu_{new} \neq \mu_{old}
$$

You're interested in whether there is a difference **in either direction**.

Therefore, the p-value must always be interpreted in the context of the **test and alternative hypothesis**.

---

# 12. Complete Mental Model

Remember the entire hypothesis-testing process:

```text
                  QUESTION
                     ↓
              Define H₀ and H₁
                     ↓
                Collect data
                     ↓
              Perform test
                     ↓
                p-value
                     ↓
             Compare with α
                     ↓
          ┌──────────┴──────────┐
          ↓                     ↓
       p < α                  p ≥ α
          ↓                     ↓
      Reject H₀            Fail to reject H₀
          ↓                     ↓
   Evidence against H₀     Insufficient evidence
```

---

# 13. The Most Important Rules

### Rule 1

**Small p-value = stronger evidence against H₀.**

### Rule 2

**p-value is NOT the probability that H₀ is true.**

### Rule 3

**p-value does NOT tell you the size of the effect.**

### Rule 4

**Failing to reject H₀ does not prove H₀ is true.**

### Rule 5

Choose your **significance level (α)** before looking at the results.

---

# Interview-Ready Answer

If an interviewer asks:

**"What is a p-value?"**

You can say:

> **A p-value is the probability of observing a result at least as extreme as the one obtained, assuming the null hypothesis is true. We compare it with a predefined significance level, such as 0.05. If the p-value is smaller than α, we reject the null hypothesis; otherwise, we fail to reject it.**

### Easy mental model

> **H₀ → Assume it's true → Look at the data → Calculate p-value → Ask: "How surprising is this result if H₀ is true?"**

**Small p-value → Very surprising → Evidence against H₀.**
