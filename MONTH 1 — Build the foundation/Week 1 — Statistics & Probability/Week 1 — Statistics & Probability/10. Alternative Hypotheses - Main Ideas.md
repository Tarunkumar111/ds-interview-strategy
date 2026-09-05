# Alternative Hypothesis — Main Ideas

The **alternative hypothesis**, written as **H₁** or **Hₐ**, is the statement that represents the **effect, difference, or relationship we are looking for evidence for**.

Think of it as:

> **H₀ = "Nothing changed."**
> **H₁ = "Something changed."**

---

## 1. Simple Example

Suppose a company introduces a new training program and wants to know whether it improves employee productivity.

### Null Hypothesis

$$
H_0: \mu_{new} = \mu_{old}
$$

> The new training program does **not** change productivity.

### Alternative Hypothesis

$$
H_1: \mu_{new} > \mu_{old}
$$

> The new training program **increases** productivity.

The alternative hypothesis represents the claim the company is interested in investigating.

---

## 2. Three Types of Alternative Hypotheses

The alternative hypothesis can be **directional** or **non-directional**.

### A. Greater Than — Right-tailed test

Used when you want to determine whether something **increased**.

$$
H_1: \mu > \mu_0
$$

Example:

> Does the new model have **higher accuracy**?

```text
H₀: μ ≤ 90%
H₁: μ > 90%
```

---

### B. Less Than — Left-tailed test

Used when you want to determine whether something **decreased**.

$$
H_1: \mu < \mu_0
$$

Example:

> Does the new system **reduce processing time**?

```text
H₀: μ ≥ 5 seconds
H₁: μ < 5 seconds
```

---

### C. Not Equal — Two-tailed test

Used when you only want to know whether there is **a difference**, without specifying the direction.

$$
H_1: \mu \neq \mu_0
$$

Example:

> Does the new website change conversion rate?

```text
H₀: μ = 10%
H₁: μ ≠ 10%
```

The change could be either higher or lower.

---

## 3. How H₁ Determines the Test

A very important relationship:

```text
             Alternative Hypothesis
                      │
          ┌───────────┼───────────┐
          ↓           ↓           ↓
        μ > μ₀      μ < μ₀      μ ≠ μ₀
          ↓           ↓           ↓
     Right-tailed  Left-tailed  Two-tailed
```

So when setting up a hypothesis test, **look at H₁ to determine the direction of the test**.

---

## 4. Real-World Data Science Example

Suppose you're testing whether a new ML model performs better than the existing model.

Current model:

```text
Accuracy = 85%
```

You believe the new model performs better.

### Hypotheses

```text
H₀: μ_new ≤ 85%

H₁: μ_new > 85%
```

Here, H₁ says:

> **The new model's accuracy is greater than 85%.**

This is a **one-tailed/right-tailed test**.

If the statistical evidence is strong enough, you reject H₀ in favor of H₁.

---

## 5. H₁ Does NOT Automatically Mean "Your Claim"

Be careful here.

Suppose you believe:

> "The new model is better."

You don't simply declare:

```text
H₁: New model is better
```

You need to translate the claim into a precise statistical statement.

For example:

$$
H_1: \mu_{new} > \mu_{old}
$$

The hypothesis must be expressed in terms of the **population parameter** you're testing.

---

## 6. H₀ and H₁ Work Together

They are competing statements.

For example:

```text
Question:
Does the new website increase conversion?

H₀: μ_new ≤ μ_old
H₁: μ_new > μ_old
```

Then:

```text
Collect sample data
       ↓
Perform statistical test
       ↓
Calculate p-value
       ↓
Compare p-value with α
       ↓
 ┌───────────────┐
 ↓               ↓
p < α           p ≥ α
 ↓               ↓
Reject H₀       Fail to reject H₀
 ↓               ↓
Evidence        Insufficient
supports H₁     evidence for H₁
```

Notice that we don't normally say:

> "We proved H₁."

Instead:

> **"The data provides sufficient evidence to reject H₀ in favor of H₁."**

---

## 7. The Key Difference

|           | Null Hypothesis           | Alternative Hypothesis               |
| --------- | ------------------------- | ------------------------------------ |
| Symbol    | H₀                        | H₁ / Hₐ                              |
| Main idea | No effect/difference      | Effect/difference exists             |
| Role      | Default assumption        | Claim we're looking for evidence for |
| Example   | μ = 100                   | μ ≠ 100                              |
| Direction | Usually includes equality | >, <, or ≠                           |

---

# Main Ideas to Remember

### 1. Alternative hypothesis represents the effect you're investigating

> **H₁ says there is a meaningful difference, effect, or relationship.**

### 2. It determines the type of test

```text
H₁: μ > μ₀  → Right-tailed

H₁: μ < μ₀  → Left-tailed

H₁: μ ≠ μ₀  → Two-tailed
```

### 3. You don't "prove" H₁ directly

You collect evidence and determine whether you can **reject H₀**.

### 4. H₁ should be defined before looking at the results

Otherwise, you risk changing your hypothesis based on what the data happens to show.

---

## Interview-ready answer

> **The alternative hypothesis is the statement that there is an effect, difference, or relationship in the population. It is written as H₁ or Hₐ, and its form determines whether the hypothesis test is one-tailed or two-tailed. We use sample data to determine whether there is sufficient evidence to reject the null hypothesis in favor of the alternative hypothesis.**

### Easy mental model

> **H₀ = Nothing happened**
> **H₁ = Something happened**
> **Data = Evidence**
> **p-value = How strong is the evidence against H₀?**
