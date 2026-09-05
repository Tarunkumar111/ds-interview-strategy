# Hypothesis Testing and the Null Hypothesis — Clearly Explained

**Hypothesis testing** is a statistical method used to determine whether the evidence from a sample is strong enough to support a claim about a population.

The easiest way to think about it is:

> **We start with a default assumption, collect data, and check whether the data provides enough evidence to reject that assumption.**

---

# 1. A Real-World Example

Suppose an e-commerce company claims:

> **"Our new recommendation system increases the average order value."**

You don't want to simply believe the claim.

You run an experiment:

* Group A → Old recommendation system
* Group B → New recommendation system

Suppose you observe:

```text
Old system:
Average order value = ₹500

New system:
Average order value = ₹530
```

The question is:

> **Is the ₹30 difference actually meaningful, or could it have happened just because of random variation?**

This is where **hypothesis testing** comes in.

---

# 2. What is a Hypothesis?

A **hypothesis** is a statement about a population that we want to test using data.

In our example:

> "The new recommendation system increases average order value."

We translate this into two competing hypotheses:

### Null Hypothesis — H₀

The default assumption:

> **The new system does not increase the average order value.**

### Alternative Hypothesis — H₁ / Hₐ

What we are trying to find evidence for:

> **The new system increases the average order value.**

So:

```text
H₀: No improvement
H₁: Improvement
```

---

# 3. What is the Null Hypothesis?

The **null hypothesis (H₀)** represents the **default position** that there is no effect, no difference, or no relationship, depending on the test.

For example:

### Testing a new medicine

```text
H₀: New medicine has no effect
H₁: New medicine has an effect
```

### Testing a new ML model

```text
H₀: New model performs the same as the old model
H₁: New model performs differently
```

### Testing a new website design

```text
H₀: New design does not change conversion rate
H₁: New design changes conversion rate
```

### Testing a recommendation system

```text
H₀: μnew = μold
H₁: μnew > μold
```

The exact form of H₁ depends on the question.

---

# 4. Why Do We Start With the Null Hypothesis?

This is one of the most important ideas.

We don't normally try to **prove** that our preferred hypothesis is true.

Instead, we assume the null hypothesis is true and ask:

> **"If the null hypothesis were true, how surprising would our observed data be?"**

If the data would be extremely unlikely under H₀, we reject H₀.

Think of it like this:

```text
                Start
                  ↓
        Assume H₀ is true
                  ↓
          Collect sample data
                  ↓
        Calculate test statistic
                  ↓
            Calculate p-value
                  ↓
       ┌──────────┴──────────┐
       ↓                     ↓
   p-value small          p-value large
       ↓                     ↓
 Reject H₀              Fail to reject H₀
```

---

# 5. What is a P-value?

The **p-value** is one of the most misunderstood concepts in statistics.

A useful definition is:

> **The p-value is the probability of observing data at least as extreme as what we observed, assuming the null hypothesis is true.**

Suppose:

```text
p-value = 0.02
```

This means:

> **If H₀ were true, there would be about a 2% chance of observing results this extreme or more extreme.**

That's relatively unlikely.

So we have evidence against H₀.

---

# 6. Significance Level (α)

Before performing the test, we usually choose a **significance level**.

A common choice is:

$$
\alpha = 0.05
$$

That means we're using a **5% significance threshold**.

Then:

### If:

$$
p < 0.05
$$

We **reject $H_0$**.

### If:

$$
p \geq 0.05
$$

We **fail to reject $H_0$**.

---

# 7. Important: "Fail to Reject" ≠ "Accept"

This is an important interview point.

Suppose:

```text
p = 0.20
```

You should **not** say:

> "We proved that H₀ is true."

Instead say:

> **"We fail to reject the null hypothesis."**

Why?

Because a high p-value doesn't prove that there is no effect.

It simply means:

> **We don't have sufficient evidence to reject H₀.**

---

# 8. Complete Example

Suppose a company says:

> "Our new website increases conversion rate."

We conduct an A/B test.

```text
Old website:
Conversion = 10%

New website:
Conversion = 11.5%
```

There is a 1.5 percentage-point difference.

But is that difference statistically significant?

We formulate:

### Null Hypothesis

$$
H_0: p_{\text{new}} = p_{\text{old}}
$$

### Alternative Hypothesis

$$
H_1: p_{\text{new}} > p_{\text{old}}
$$

Suppose our statistical test produces:

```text
p-value = 0.03
```

Using:

```text
α = 0.05
```

We compare:

$$
0.03 < 0.05
$$

Therefore:

> **Reject H₀.**

We have statistically significant evidence that the new website increases conversion.

---

# 9. Statistical Significance ≠ Business Significance

This is **very important in Data Science**.

Suppose:

```text
Old conversion = 10.00%
New conversion = 10.01%

p-value = 0.001
```

The result could be statistically significant.

But the actual improvement is only:

```text
0.01 percentage points
```

That might not have meaningful business value.

So always distinguish:

**Statistical significance**

> Is the observed difference unlikely to be explained by random variation under H₀?

**Practical/business significance**

> Is the difference large enough to actually matter?

---

# 10. One-Tailed vs Two-Tailed Tests

The alternative hypothesis determines the type of test.

### Two-tailed

You want to know whether there is **any difference**.

```text
H₀: μnew = μold

H₁: μnew ≠ μold
```

You're interested in both:

```text
Higher ↑
Lower ↓
```

### One-tailed

You specifically care about one direction.

For example:

```text
H₀: μnew ≤ μold

H₁: μnew > μold
```

You're only testing whether the new system is **better**.

---

# 11. Common Hypothesis Tests

Depending on your data and question, you might use different tests:

| Test                | Common use                                                 |
| ------------------- | ---------------------------------------------------------- |
| **Z-test**          | Mean/proportion under appropriate assumptions              |
| **t-test**          | Comparing means, especially with unknown population SD     |
| **Chi-square test** | Categorical variables / independence                       |
| **ANOVA**           | Comparing means across multiple groups                     |
| **Proportion test** | Comparing proportions                                      |
| **Mann–Whitney U**  | Comparing distributions/ranks without normality assumption |

The choice of test depends on:

* Type of data
* Number of groups
* Sample size
* Distribution/assumptions
* Whether observations are independent
* What exactly you want to test

---

# 12. The Data Science Mental Model

When you hear **hypothesis testing**, think:

```text
Question
   ↓
Define H₀ and H₁
   ↓
Collect sample data
   ↓
Choose appropriate statistical test
   ↓
Calculate test statistic
   ↓
Calculate p-value
   ↓
Compare p-value with α
   ↓
Make a decision
```

For example:

```text
Question:
Does the new ML model perform better?

H₀:
New model = Old model

H₁:
New model > Old model

        ↓

Run statistical test

        ↓

p-value = 0.02

        ↓

0.02 < 0.05

        ↓

Reject H₀

        ↓

Evidence suggests the new model performs better
```

---

# 13. The Most Important Things to Remember

### **Hypothesis testing**

> A framework for making decisions about population claims using sample data.

### **Null hypothesis (H₀)**

> The default assumption, typically representing no effect or no difference.

### **Alternative hypothesis (H₁)**

> The competing claim that there is an effect, difference, or relationship.

### **P-value**

> How surprising the observed result would be, or something more extreme, if H₀ were true.

### **Significance level (α)**

> The threshold used to decide when evidence is strong enough to reject H₀.

### **Decision**

```text
p < α
   ↓
Reject H₀

p ≥ α
   ↓
Fail to reject H₀
```

---

## Interview-ready answer

If an interviewer asks **"What is hypothesis testing?"**, you can say:

> **Hypothesis testing is a statistical framework for determining whether sample data provides sufficient evidence against a null hypothesis about a population. We formulate a null and alternative hypothesis, collect data, calculate a test statistic and p-value, and compare the p-value with a predefined significance level to make a statistical decision.**

And remember this simple sentence:

> **"Start with H₀, collect evidence, calculate the p-value, and decide whether the evidence is strong enough to reject H₀."**
