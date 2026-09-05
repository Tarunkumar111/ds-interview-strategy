# P-hacking: What It Is and How to Avoid It

**P-hacking** is a statistical practice where researchers **manipulate or selectively analyze data until they obtain a statistically significant p-value**, often \(p < 0.05\).

The main problem is that the analysis is being influenced by the desired result.

> **P-hacking = searching for statistical significance instead of objectively testing a hypothesis.**

---

## 1. Simple Example

Suppose you are testing whether a **new website design increases sales**.

You start with:

```text
H₀: New design does not increase sales
H₁: New design increases sales
```

You run the experiment and get:

```text
p-value = 0.12
```

Since:

$$
0.12 > 0.05
$$

the result is **not statistically significant**.

But suppose you really want to show that the new design works.

You start trying different things:

* Remove a few observations
* Analyze different customer groups
* Try different time periods
* Try different metrics
* Run several statistical tests
* Stop collecting data when \(p < 0.05\)

Eventually you find:

```text
p-value = 0.03
```

Then you report:

> "The new website significantly increases sales."

That's an example of **p-hacking** if those choices were made because you wanted to obtain significance rather than being justified in advance.

---

# 2. Why Is P-hacking a Problem?

The significance level is often set at:

$$
\alpha = 0.05
$$

This means that **even when H₀ is actually true**, a properly conducted test can produce a statistically significant result by chance about 5% of the time under the usual assumptions.

Now imagine running **many tests**.

For example:

```text
Test 1 → p = 0.42
Test 2 → p = 0.31
Test 3 → p = 0.18
Test 4 → p = 0.07
Test 5 → p = 0.04  ← Significant!
```

If you only report Test 5, it can look like you found a meaningful effect.

But you actually searched through multiple possibilities.

This increases the chance of getting a **false positive**.

---

# 3. Common Forms of P-hacking

### 1. Testing many hypotheses

You test many variables or outcomes and only report the significant ones.

```text
100 tests
      ↓
Some produce p < 0.05 by chance
      ↓
Report only those results
```

---

### 2. Trying different statistical tests

You try:

```text
t-test
Mann–Whitney
ANOVA
Chi-square
...
```

and report whichever gives the desired result without a principled reason for choosing it.

---

### 3. Removing observations selectively

You remove "outliers" only because removing them makes the result significant.

For example:

```text
Before removing observations:
p = 0.08

Remove selected observations:
p = 0.03
```

If the removal wasn't justified independently of the result, this is problematic.

---

### 4. Stopping data collection when significance appears

Suppose:

```text
100 users → p = 0.20
200 users → p = 0.11
300 users → p = 0.07
400 users → p = 0.04
```

You stop at 400 because the result finally became significant.

This can inflate the false-positive rate when done without an appropriate sequential-testing design.

---

### 5. Trying different subgroups

Suppose your overall experiment isn't significant.

You then look at:

* Men
* Women
* Younger users
* Older users
* New customers
* Existing customers

Eventually one subgroup gives:

```text
p = 0.02
```

Reporting that subgroup as though it were the original hypothesis is potentially p-hacking.

---

# 4. P-hacking vs Honest Data Analysis

The difference is often about **when and why decisions are made**.

### Good practice

Before analyzing:

```text
Define hypothesis
      ↓
Define primary metric
      ↓
Define statistical test
      ↓
Define analysis plan
      ↓
Collect data
      ↓
Analyze
```

### P-hacking

```text
Collect data
      ↓
Look at results
      ↓
Try different analyses
      ↓
Try different subgroups
      ↓
Remove observations
      ↓
Keep trying
      ↓
p < 0.05!
```

The second approach gives the analysis many opportunities to find a result by chance.

---

# 5. How to Avoid P-hacking

## 1. Pre-register your hypotheses

Before collecting or analyzing the data, specify:

* Hypotheses
* Primary outcome
* Sample size
* Statistical test
* Analysis plan

This reduces the temptation to change the analysis based on the results.

---

## 2. Define the primary metric in advance

Suppose you're testing a new app feature.

Don't decide afterward:

> "Let's use whichever metric became significant."

Instead, decide beforehand:

```text
Primary metric:
7-day user retention
```

Then analyze that metric as planned.

---

## 3. Don't keep checking until p < 0.05

If you're running an experiment, don't repeatedly check the p-value and stop immediately when it becomes significant unless your statistical procedure explicitly accounts for sequential testing.

Use an appropriate **sample-size and stopping plan**.

---

## 4. Account for Multiple Comparisons

If you're testing many hypotheses, you need to account for the increased probability of false positives.

Common approaches include:

* **Bonferroni correction**
* **Holm correction**
* **False Discovery Rate (FDR)** methods such as Benjamini–Hochberg

For example, with Bonferroni correction:

$$
\alpha_{adjusted}=\frac{\alpha}{m}
$$

where:

* \(\alpha\) = original significance level
* \(m\) = number of tests

If:

```text
α = 0.05
m = 10 tests
```

then:

$$
\alpha_{adjusted}=\frac{0.05}{10}=0.005
$$

So you would require a much smaller p-value for significance under this correction.

---

# 6. Exploratory Analysis Is Not Bad

This is an important distinction.

You **should** explore your data.

For example, you might discover:

> "The effect seems particularly strong among users aged 18–25."

That's a valuable finding.

The problem occurs when you present an **exploratory finding as if it were a pre-planned confirmatory hypothesis**.

A better approach is:

> "This subgroup finding was identified during exploratory analysis and should be validated in a future study."

---

# 7. Replication Helps

Suppose you discover:

```text
Study 1:
p = 0.03
```

Instead of assuming you've definitely discovered a real effect, conduct another appropriately designed study.

```text
Study 1
   ↓
Interesting finding
   ↓
Independent replication
   ↓
Same effect?
   ↓
Stronger evidence
```

If the effect repeatedly appears under well-designed studies, confidence in the finding increases.

---

# 8. P-hacking and Data Science

P-hacking is particularly relevant to **A/B testing and experimentation**.

Imagine a Data Scientist tests a new feature.

They check:

```text
Conversion
Revenue
Retention
Session duration
Clicks
Time spent
Churn
```

Then they break users into:

```text
Male / Female
New / Existing
Age groups
Countries
Devices
```

That's already a huge number of comparisons.

If they keep searching, eventually they may find:

```text
p < 0.05
```

even if the feature has no real effect.

That's why professional experimentation requires a **clear analysis plan and appropriate multiple-testing controls**.

---

# 9. P-hacking vs Multiple Testing

These concepts are related but not identical.

### Multiple testing

You perform many statistical tests.

This is not automatically wrong.

### P-hacking

You **selectively exploit multiple analyses or decisions to obtain a desired significant result**, often without properly accounting for the multiple testing.

So:

> **Multiple testing can be legitimate. P-hacking is the problematic way of using flexibility in analysis to manufacture significance.**

---

# 10. The Big Picture

```text
              Research Question
                     ↓
              Define H₀ and H₁
                     ↓
          Predefine analysis plan
                     ↓
              Collect data
                     ↓
             Analyze the data
                     ↓
        ┌────────────────────────┐
        │                        │
        ↓                        ↓
   Planned analysis       Keep trying analyses
        ↓                        ↓
   Report results            p < 0.05
                                 ↓
                            P-hacking risk
```

---

# 11. What to Remember

### P-hacking

> **Manipulating or selectively analyzing data to obtain statistically significant results.**

### Why it's dangerous

It increases the risk of:

> **False positives and misleading conclusions.**

### How to avoid it

* Predefine hypotheses
* Predefine primary outcomes
* Plan sample size
* Define the analysis method in advance
* Avoid stopping just because \(p < 0.05\)
* Account for multiple comparisons
* Distinguish exploratory from confirmatory analysis
* Replicate important findings
* Report results transparently

---

# Interview-Ready Answer

If an interviewer asks:

**"What is p-hacking and how can you avoid it?"**

You can say:

> **P-hacking occurs when researchers use flexible or selective analysis choices to obtain a statistically significant p-value, such as trying multiple hypotheses, subgroups, or statistical tests and reporting only the significant result. It can increase the false-positive rate. We can reduce p-hacking by pre-registering hypotheses and analysis plans, defining primary outcomes in advance, planning sample sizes, accounting for multiple comparisons, and clearly distinguishing exploratory from confirmatory analysis.**

### Easy mental model

> **Don't ask: "How can I get p < 0.05?"**

> **Ask: "What was my hypothesis, what analysis did I plan, and what does the evidence actually show?"**
