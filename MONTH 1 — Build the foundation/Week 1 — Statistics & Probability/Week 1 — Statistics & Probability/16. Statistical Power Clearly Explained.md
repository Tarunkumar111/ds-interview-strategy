# Statistical Power — Clearly Explained

**Statistical power** is an important concept in hypothesis testing.

The simplest way to remember it is:

> **Statistical power is the probability that a test correctly detects a real effect when that effect actually exists.**

In other words:

> **Power = ability to detect a true effect.**

---

# 1. Start With a Real-World Example

Suppose a company develops a new recommendation system.

You want to know whether it increases sales.

### Hypotheses

$$
H_0: \text{New system has no effect}
$$

$$
H_1: \text{New system increases sales}
$$

Suppose the new system **really does increase sales**.

You run your statistical test.

There are two possibilities:

### Good outcome

```text
Real effect exists
       ↓
Test detects it
       ↓
Reject H₀
```

### Bad outcome

```text
Real effect exists
       ↓
Test fails to detect it
       ↓
Fail to reject H₀
```

That second situation is called a **Type II error**.

Statistical power is about avoiding that situation.

---

# 2. Power and Type II Error

Statistical power is directly related to the **Type II error probability**.

Type II error is usually represented by:

$$
\beta
$$

Power is:

$$
\boxed{\text{Power}=1-\beta}
$$

So if:

$$
\beta=0.20
$$

then:

$$
\text{Power}=1-0.20=0.80
$$

Therefore:

$$
\boxed{\text{Power}=80\%}
$$

This means:

> **If the specified true effect exists, the test has an 80% probability of detecting it under the assumed conditions.**

---

# 3. Type I vs Type II Error

This is extremely important.

| Reality     | Your decision     | Result              |
| ----------- | ----------------- | ------------------- |
| H₀ is true  | Reject H₀         | **Type I error**    |
| H₀ is true  | Fail to reject H₀ | Correct             |
| H₀ is false | Reject H₀         | **Correct / Power** |
| H₀ is false | Fail to reject H₀ | **Type II error**   |

Think of it like this:

```text
                  Reality
             ┌───────────────┐
             │               │
          H₀ true         H₀ false
             │               │
             ↓               ↓
       Reject H₀         Reject H₀
             ↓               ↓
       Type I error      Correct
                          (Power)
```

---

# 4. Example: A/B Testing

Suppose you're testing a new website.

```text
Old website → 10% conversion
New website → 12% conversion
```

You want your experiment to reliably detect a **2 percentage-point improvement** if that improvement really exists.

Suppose your experiment has:

$$
\text{Power}=80\%
$$

This means:

> If the true improvement really is the effect size used in the power calculation, your test has an 80% chance of detecting it as statistically significant, assuming the planned design and assumptions hold.

There is therefore a:

$$
1-0.80=0.20
$$

or **20% Type II error probability** for that specified effect.

---

# 5. Why Does Sample Size Matter?

This is one of the most important relationships.

Generally:

> **Larger sample → Higher statistical power**

Why?

A larger sample gives you a more precise estimate.

For example:

### Small experiment

```text
100 users
     ↓
Large uncertainty
     ↓
Harder to detect small effects
     ↓
Lower power
```

### Large experiment

```text
10,000 users
     ↓
Smaller uncertainty
     ↓
Easier to detect effects
     ↓
Higher power
```

So if you want to detect a **small effect**, you generally need a larger sample.

---

# 6. What Factors Affect Statistical Power?

Four major factors are particularly important.

## 1. Sample Size

$$
n \uparrow \Rightarrow \text{Power} \uparrow
$$

More data generally means greater ability to detect an effect.

---

## 2. Effect Size

A larger true effect is easier to detect.

For example:

```text
Small effect:
10.0% → 10.2%

Large effect:
10.0% → 15.0%
```

The 5 percentage-point improvement is much easier to detect than the 0.2 percentage-point improvement, all else equal.

Therefore:

$$
\text{Effect size} \uparrow
\Rightarrow
\text{Power} \uparrow
$$

---

## 3. Significance Level (α)

Increasing \(\alpha\) generally increases power.

For example:

```text
α = 0.01 → harder to reject H₀
α = 0.05 → easier
α = 0.10 → easier still
```

So:

$$
\alpha \uparrow
\Rightarrow
\text{Power} \uparrow
$$

But there's a trade-off:

> Increasing α also increases the risk of a **Type I error**.

---

## 4. Variability / Noise

If the data is highly variable, it becomes harder to distinguish a real effect from random noise.

```text
Low variability
     ↓
Clearer signal
     ↓
Higher power
```

versus:

```text
High variability
     ↓
Noisier signal
     ↓
Lower power
```

Therefore, all else equal:

$$
\text{Variability} \uparrow
\Rightarrow
\text{Power} \downarrow
$$

---

# 7. A Useful Mental Model: Signal vs Noise

Think of statistical power as the ability to detect a **signal through noise**.

```text
              DATA
                │
       ┌────────┴────────┐
       ↓                 ↓
     Signal             Noise
   True effect       Random variation
       │                 │
       └────────┬────────┘
                ↓
         Statistical Test
                ↓
       Can we detect the
          true effect?
```

Power is higher when the signal is strong relative to the noise.

That's why:

* Larger effect → higher power
* Larger sample → higher power
* Lower variability → higher power

---

# 8. What is "80% Power"?

You will hear **80% power** very often.

Suppose you design an experiment with:

$$
\text{Power}=0.80
$$

This means:

> **For the effect size specified in the study design, the test has an 80% probability of rejecting H₀ when that effect truly exists, under the assumed conditions.**

It does **not** mean:

> "There is an 80% chance that my hypothesis is true."

That's incorrect.

It also doesn't mean:

> "The result is 80% accurate."

Power is about the **performance of the statistical test under a specified alternative**.

---

# 9. Power Analysis

Before conducting an experiment, we can perform a **power analysis** to determine how much data we need.

For example:

> "How many users do I need for my A/B test?"

You might specify:

```text
Significance level = 5%
Desired power = 80%
Expected effect size = 2 percentage points
Baseline conversion = 10%
```

Then a sample-size calculation can estimate how many observations are needed.

Conceptually:

```text
Desired effect
      +
Significance level
      +
Desired power
      +
Variability
      ↓
Sample size calculation
      ↓
Required sample size
```

---

# 10. What Happens If Power Is Too Low?

Suppose you conduct an experiment with only **20 users**.

There is a real effect, but your sample is too small to detect it reliably.

You might get:

```text
Real effect exists
       ↓
Sample is too small
       ↓
Large uncertainty
       ↓
p-value > 0.05
       ↓
Fail to reject H₀
```

You conclude:

> "We didn't find evidence of an effect."

But the effect may actually exist.

This is a **low-power study**.

---

# 11. Important Distinction: "No Significant Effect" vs "No Effect"

Suppose your experiment produces:

$$
p=0.20
$$

You fail to reject H₀.

You should **not automatically conclude**:

> "There is no effect."

If the experiment had low statistical power, the study might simply have been unable to detect the effect.

This is why power and sample size matter.

A better conclusion might be:

> **"We did not find sufficient evidence of an effect. Given the study's power and confidence interval, the data may still be compatible with effects of practical importance."**

---

# 12. Power and Sample Size Relationship

Think about it this way:

```text
                 Sample Size
                      ↑
                      │
              More information
                      │
                      ↓
              Smaller uncertainty
                      │
                      ↓
             Better signal detection
                      │
                      ↓
                Higher Power
```

So when designing an experiment:

> **If you want high power, you generally need enough observations to detect the effect that matters.**

---

# 13. Statistical Power in Machine Learning

Power is also relevant when comparing ML models.

Suppose:

```text
Model A accuracy = 90.0%
Model B accuracy = 90.5%
```

You might observe that Model B performs better.

But is the difference real, or just random variation?

You can use an appropriate statistical comparison to assess whether the observed difference is meaningful.

If your evaluation dataset is too small:

```text
True performance difference
          ↓
Small evaluation sample
          ↓
High uncertainty
          ↓
Low power
          ↓
Hard to detect difference
```

Therefore, **having a high observed score isn't enough**. You also need enough evaluation data to make reliable comparisons.

---

# 14. Statistical Power vs P-value

These concepts are closely related but different.

### P-value

Looks at the **data you actually observed**.

> "If H₀ were true, how surprising is this result?"

### Power

Looks at the **ability of the test to detect a specified real effect**.

> "If this effect really exists, how likely is my test to detect it?"

Think:

```text
P-value
→ What happened in this experiment?

Power
→ How capable was the experiment of detecting the effect?
```

---

# 15. Statistical Power vs Significance Level

Another important distinction:

### Significance level

$$
\alpha
$$

Controls the threshold for rejecting H₀ and is related to **Type I error**.

### Power

$$
1-\beta
$$

Measures the probability of detecting a specified true effect and is related to **Type II error**.

```text
α → Type I error

β → Type II error

1 − β → Power
```

---

# 16. The Complete Picture

You can connect all the hypothesis-testing concepts you've learned:

```text
                 Hypothesis Testing
                        │
          ┌─────────────┴─────────────┐
          ↓                           ↓
      H₀ is true                  H₀ is false
          │                           │
          ↓                           ↓
     Reject H₀                  Reject H₀
          │                           │
          ↓                           ↓
    Type I Error                  Correct
                                  = Power
                                     
If H₀ is false but we
fail to reject it:
          ↓
    Type II Error (β)
          ↓
       Power = 1 − β
```

---

# 17. What to Remember

### Statistical Power

> **The probability that a statistical test correctly rejects H₀ when a specified alternative effect is truly present.**

### Formula

$$
\boxed{\text{Power}=1-\beta}
$$

### Power increases with:

```text
Sample size ↑
Effect size ↑
α ↑
Variability ↓
```

### Common target

$$
\boxed{\text{80\% Power}}
$$

is a common planning target, though the appropriate target depends on the application.

---

# Interview-Ready Answer

If an interviewer asks:

**"What is statistical power?"**

You can say:

> **Statistical power is the probability that a hypothesis test will detect a specified true effect when that effect actually exists. It is equal to \(1-\beta\), where β is the probability of a Type II error. Power generally increases with sample size and effect size, decreases with greater variability, and increases when the significance level is made less stringent.**

### Easy Mental Model

> **Power = "If a real effect exists, how likely is my experiment to find it?"**

And remember the key relationship:

$$
\boxed{\text{Power}=1-\text{Type II Error}}
$$
