# Power Analysis, Clearly Explained!!!

## 1. What is Power Analysis?

**Power analysis** is a statistical method used to determine whether an experiment has enough data to reliably detect a real effect.

In simple words:

> **Power analysis helps us decide how much data we need before running an experiment.**

The most common use is to determine the required **sample size**.

---

## 2. Why Do We Need Power Analysis?

Imagine you're testing whether a new website design increases the conversion rate.

You run an experiment with only **20 users**.

Suppose the new design actually improves conversion, but your sample is too small to detect the improvement statistically.

You might conclude:

> "The new design has no significant effect."

But the effect may actually exist—you simply didn't have enough data to detect it.

This is where **power analysis** helps.

```text
Before experiment
       ↓
Specify expected effect
       ↓
Choose significance level (α)
       ↓
Choose desired power
       ↓
Calculate required sample size
       ↓
Run experiment
```

---

# 3. The Four Important Components

Power analysis typically involves four key quantities:

| Component                  | Meaning                                |
| -------------------------- | -------------------------------------- |
| **Effect size**            | How large the effect is                |
| **Significance level (α)** | Probability of Type I error            |
| **Power (1 − β)**          | Probability of detecting a real effect |
| **Sample size (n)**        | Number of observations needed          |

These quantities are related.

If you know three of them, you can generally determine the fourth.

---

# 4. Statistical Power

Recall:

$$
\boxed{\text{Power}=1-\beta}
$$

where:

* \(\beta\) = probability of **Type II error**
* Power = probability of correctly detecting a real effect

For example:

$$
\text{Power}=0.80
$$

means:

> If the specified real effect exists, the experiment has an **80% probability of detecting it**.

---

# 5. Effect Size

**Effect size** describes how large or meaningful the difference is.

For example, suppose:

* Old conversion rate = 10%
* New conversion rate = 12%

The improvement is:

$$
12\%-10\%=2\text{ percentage points}
$$

That difference represents an **effect**.

A larger effect is generally easier to detect.

```text
Large effect
     ↓
Easier to detect
     ↓
Less data may be required
```

Whereas:

```text
Small effect
     ↓
Harder to detect
     ↓
More data may be required
```

---

# 6. Significance Level (α)

The significance level is usually:

$$
\boxed{\alpha=0.05}
$$

This represents the maximum Type I error rate we are willing to tolerate under the test's assumptions.

Recall:

### Type I Error

Rejecting \(H_0\) when \(H_0\) is actually true.

```text
H₀ is true
   ↓
We reject H₀
   ↓
Type I error
```

A smaller \(\alpha\) makes the test more stringent.

For example:

$$
\alpha=0.01
$$

is more stringent than:

$$
\alpha=0.05
$$

Generally, making \(\alpha\) smaller requires **more data** to maintain the same power.

---

# 7. Sample Size

Sample size is the number of observations or participants in the experiment.

Generally:

$$
\boxed{\text{Larger sample size} \Rightarrow \text{Higher power}}
$$

For example:

```text
100 observations
      ↓
Lower ability to detect small effects

10,000 observations
      ↓
Higher ability to detect small effects
```

However, more data is not always the answer—**study design, variability, effect size, and the statistical test also matter.**

---

# 8. How These Factors Work Together

A useful mental model:

| Change            | Effect on required sample size |
| ----------------- | ------------------------------ |
| Desired power ↑   | Sample size ↑                  |
| Effect size ↓     | Sample size ↑                  |
| Variability ↑     | Sample size ↑                  |
| α becomes smaller | Sample size ↑                  |
| Effect size ↑     | Sample size ↓                  |
| Desired power ↓   | Sample size ↓                  |
| Variability ↓     | Sample size ↓                  |

So:

> **Small effects + noisy data + high power + strict α → large sample size.**

---

# 9. Example: A/B Testing

Suppose you're comparing two versions of a website.

### Goal

Determine how many users are needed to detect an improvement in conversion rate.

You decide:

* Baseline conversion = 10%
* Minimum improvement worth detecting = 2 percentage points
* Significance level = 5%
* Desired power = 80%

So your design parameters are:

$$
\alpha=0.05
$$

$$
\text{Power}=0.80
$$

$$
\text{Effect}=2\text{ percentage points}
$$

A power analysis can then calculate the required sample size.

For example, a statistical software package might tell you that you need approximately **several thousand users per group** depending on the exact assumptions and test.

The important idea is:

> **We determine the sample size before collecting the data.**

---

# 10. What Happens If We Don't Do Power Analysis?

Suppose you run an experiment with too few observations.

You obtain:

$$
p=0.20
$$

Since:

$$
p>0.05
$$

you fail to reject \(H_0\).

You might say:

> "There is no evidence of an effect."

But you should be careful.

The experiment might simply have had **low statistical power**.

```text
Real effect exists
       ↓
Sample too small
       ↓
Weak evidence
       ↓
p-value > 0.05
       ↓
Fail to reject H₀
```

This is one reason why:

$$
\boxed{\text{Not statistically significant} \neq \text{No effect}}
$$

---

# 11. Power Analysis Before vs After an Experiment

### Before the experiment

Power analysis is primarily used for **study planning**.

For example:

> "How many users do we need?"

```text
Expected effect
      +
Significance level
      +
Desired power
      ↓
Required sample size
```

This is called **prospective power analysis**.

---

### After the experiment

You already have the data and may analyze the study's ability to detect an effect.

However, simply calculating "observed/post-hoc power" from the same observed effect and p-value is often not very informative. It's usually better to report the **effect estimate and confidence interval**, and consider whether the study was adequately powered based on the effect size that mattered in advance.

---

# 12. Power Analysis and Type II Error

Remember:

$$
\boxed{\text{Power}=1-\beta}
$$

Therefore:

| Power | Type II error (\(\beta\)) |
| ----: | ------------------------: |
|   70% |                       30% |
|   80% |                       20% |
|   90% |                       10% |
|   95% |                        5% |

So:

$$
\boxed{\text{Higher power} \Rightarrow \text{Lower probability of Type II error}}
$$

---

# 13. Why 80% Power Is Common

A common planning target is:

$$
\boxed{\text{Power}=80\%}
$$

This represents a balance between:

* collecting enough data to detect meaningful effects
* cost
* time
* participants
* computational resources

But **80% is not a universal requirement**.

Some studies may use:

$$
90\%
$$

or

$$
95\%
$$

when missing a real effect would be particularly costly or dangerous.

---

# 14. Power Analysis in Data Science

Power analysis is especially useful in:

### A/B Testing

Determine how many users are required to detect a meaningful difference.

### Product Experiments

Determine whether a new feature can be evaluated reliably.

### Clinical Studies

Determine how many participants are needed to detect a treatment effect.

### Marketing Experiments

Determine how many customers are needed to detect a change in conversion or response rate.

### Machine Learning

When comparing models, enough test/evaluation data may be needed to reliably detect a meaningful performance difference.

---

# 15. Power Analysis vs P-value

These are often confused.

| Power Analysis                              | P-value                                                            |
| ------------------------------------------- | ------------------------------------------------------------------ |
| Usually done during planning                | Usually calculated after observing data                            |
| Helps determine required sample size        | Measures evidence against \(H_0\)                                  |
| Uses desired power                          | Depends on observed data                                           |
| Concerned with detecting a specified effect | Concerned with how surprising the observed result is under \(H_0\) |

### Simple distinction

> **Power analysis asks: "How much data do I need?"**

> **P-value asks: "How surprising is my observed result if \(H_0\) is true?"**

---

# 16. A Simple Real-World Example

Imagine you're testing a new recommendation algorithm.

Current average order value:

$$
\$50
$$

You care about detecting at least a:

$$
\$2
$$

increase.

You choose:

$$
\alpha=0.05
$$

and:

$$
\text{Power}=80\%
$$

You perform a power analysis.

The analysis determines how many customers you need in each group.

Then:

```text
Power Analysis
      ↓
Required sample size
      ↓
Run experiment
      ↓
Collect data
      ↓
Perform hypothesis test
      ↓
Calculate p-value + confidence interval
      ↓
Make decision
```

---

# 17. Key Relationship to Remember

The most important relationships are:

$$
\boxed{\text{Power}=1-\beta}
$$

and generally:

$$
\boxed{n\uparrow \Rightarrow Power\uparrow}
$$

$$
\boxed{Effect\ Size\uparrow \Rightarrow Power\uparrow}
$$

$$
\boxed{Variability\uparrow \Rightarrow Power\downarrow}
$$

$$
\boxed{\alpha\uparrow \Rightarrow Power\uparrow}
$$

for a fixed sample size and other assumptions.

---

# 18. Interview-Ready Answer

> **Power analysis is a statistical method used to determine the required sample size for an experiment or study. It considers factors such as the expected effect size, significance level, desired statistical power, and variability. A common target is 80% power, meaning that if the specified real effect exists, the test has an 80% chance of detecting it. Power analysis helps prevent underpowered experiments and reduces the risk of Type II errors.**

---

# 19. Mental Model

Remember this:

```text
              POWER ANALYSIS
                    │
       ┌────────────┼────────────┐
       ↓            ↓            ↓
 Effect Size       α        Variability
       │            │            │
       └────────────┼────────────┘
                    ↓
             Desired Power
                    ↓
             Required Sample
                    ↓
             Run Experiment
```

### One-line takeaway

$$
\boxed{\text{Power Analysis = “How much data do I need to reliably detect an effect I care about?”}}
$$
