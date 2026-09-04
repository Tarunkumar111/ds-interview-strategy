# False Discovery Rate (FDR) — Clearly Explained

**False Discovery Rate (FDR)** is a statistical concept used when you perform **many hypothesis tests at the same time**.

The main problem is:

> **The more tests you perform, the more likely you are to get some statistically significant results just by chance.**

FDR methods help control how many of the results you call "significant" are expected to be **false discoveries**.

---

## 1. Start with a Simple Example

Suppose you're a Data Scientist analyzing whether a new treatment affects **1,000 different genes**.

You perform:

```text
1,000 hypothesis tests
```

For every gene:

```text
H₀: Treatment has no effect on this gene
H₁: Treatment has an effect
```

Suppose you use:

$$
\alpha = 0.05
$$

and find:

```text
100 genes with p < 0.05
```

It might be tempting to say:

> "The treatment affects 100 genes."

But there's a problem.

---

# 2. Some Significant Results Can Occur by Chance

If all 1,000 null hypotheses were actually true, using a 5% threshold could still produce roughly:

$$
1000 \times 0.05 = 50
$$

significant results **on average** just due to random variation.

So if you find 100 significant results, some could be false discoveries.

This is the **multiple testing problem**.

---

# 3. What Does FDR Mean?

FDR stands for:

> **False Discovery Rate**

It controls the expected proportion of **false discoveries among the results you declare significant**.

Conceptually:

$$
\boxed{
FDR =
\frac{\text{False Discoveries}}
{\text{Total Discoveries}}
}
$$

For example, suppose you declare 100 results significant.

If approximately 5 of them are expected to be false discoveries:

$$
FDR = \frac{5}{100}=0.05
$$

So the FDR is **5%**.

### Important

FDR does **not** mean:

> "There is a 5% chance that every individual significant result is false."

It is about the **expected proportion of false discoveries among the collection of rejected hypotheses**.

---

# 4. Why Do We Need FDR?

Imagine you test:

```text
10 hypotheses
```

At:

$$
\alpha=0.05
$$

The chance of getting at least one false positive can already be greater than 5% when many null hypotheses are true.

Now imagine:

```text
10,000 hypotheses
```

You'll have many more opportunities to obtain small p-values just by chance.

This occurs frequently in:

* Genomics
* Medical research
* Neuroscience
* A/B testing
* Feature selection
* Large-scale experiments
* Machine Learning experiments

---

# 5. FDR vs P-value

These are **not the same thing**.

### P-value

Answers:

> **"How surprising is this result under H₀?"**

### FDR procedure

Helps answer:

> **"Among the discoveries I'm calling significant, how much false discovery can I expect to tolerate?"**

---

# 6. FDR vs Family-Wise Error Rate

This is a very important distinction.

There are two common approaches to multiple testing.

### Family-Wise Error Rate (FWER)

Controls the probability of making **at least one false positive**.

A common method:

> **Bonferroni correction**

It is relatively conservative.

---

### False Discovery Rate (FDR)

Controls the **expected proportion of false discoveries among the rejected hypotheses**.

It is generally less conservative than FWER methods and can therefore identify more discoveries when many tests are being performed.

Think:

```text
FWER
↓
"Don't make even one false discovery."

FDR
↓
"Allow some false discoveries, but control their proportion."
```

---

# 7. Bonferroni vs FDR

Suppose you perform:

```text
100 tests
```

with:

$$
\alpha=0.05
$$

### Bonferroni

Bonferroni uses:

$$
\alpha_{adjusted}
=
\frac{0.05}{100}
=
0.0005
$$

So a result generally needs:

$$
p < 0.0005
$$

to be considered significant under this simple Bonferroni rule.

This can be quite strict.

---

### FDR

FDR procedures, such as **Benjamini–Hochberg**, generally allow a larger set of discoveries while controlling the expected false-discovery proportion.

This makes FDR especially useful when you're testing **hundreds or thousands of hypotheses** and expect multiple genuine discoveries.

---

# 8. Benjamini–Hochberg Procedure

One of the most widely used FDR procedures is the **Benjamini–Hochberg (BH) procedure**.

Suppose we have these p-values:

```text
0.001
0.008
0.012
0.030
0.040
```

### Step 1 — Sort the p-values

Sort them from smallest to largest.

```text
p₁ = 0.001
p₂ = 0.008
p₃ = 0.012
p₄ = 0.030
p₅ = 0.040
```

### Step 2 — Assign ranks

```text
p-value    Rank
0.001       1
0.008       2
0.012       3
0.030       4
0.040       5
```

### Step 3 — Calculate the BH threshold

For each rank \(i\):

$$
\frac{i}{m}q
$$

where:

* \(i\) = rank
* \(m\) = total number of tests
* \(q\) = desired FDR level

Suppose:

$$
q=0.05
$$

and:

$$
m=5
$$

Then:

| Rank | p-value | BH threshold |
| ---: | ------: | -----------: |
|    1 |   0.001 |        0.010 |
|    2 |   0.008 |        0.020 |
|    3 |   0.012 |        0.030 |
|    4 |   0.030 |        0.040 |
|    5 |   0.040 |        0.050 |

We find the **largest rank** where:

$$
p_i \leq \frac{i}{m}q
$$

Here:

```text
0.040 ≤ 0.050
```

So the discoveries up to that rank are considered significant under the BH procedure.

---

# 9. FDR in Data Science

Imagine you're analyzing **10,000 features** to determine which ones are associated with customer churn.

You perform:

```text
10,000 hypothesis tests
```

Without correction:

```text
p < 0.05
```

might produce a large number of apparently significant features.

Instead, you could apply an FDR procedure such as Benjamini–Hochberg.

```text
10,000 p-values
       ↓
Sort p-values
       ↓
Benjamini–Hochberg
       ↓
Adjusted significance decisions
       ↓
Selected features
```

This helps control the expected proportion of false discoveries among the selected features.

---

# 10. FDR and P-hacking

FDR is also related to the **p-hacking** concept you just learned.

Suppose someone tests:

```text
1000 variables
```

and reports only:

```text
p < 0.05
```

They may end up with many false discoveries.

Using an appropriate multiple-testing correction can reduce this problem.

However:

> **FDR correction does not make p-hacking acceptable.**

You should still:

* Define hypotheses appropriately
* Plan the analysis
* Avoid selectively reporting results
* Distinguish exploratory from confirmatory findings
* Report the number of tests performed

---

# 11. FDR vs FWER — Easy Mental Model

Imagine you have **100 discoveries**.

### FWER approach

> "I want to keep the probability of making **even one false discovery** very low."

### FDR approach

> "I'm okay with some false discoveries, but I want the **proportion of false discoveries among my discoveries** to remain controlled."

Therefore:

```text
FWER
More conservative
      ↓
Fewer discoveries
      ↓
Stronger control of false positives


FDR
Less conservative
      ↓
More discoveries
      ↓
Controls proportion of false discoveries
```

Neither is universally "better." The appropriate method depends on the scientific or business objective.

---

# 12. Important Terminology

When working with FDR, you'll often hear:

### False Positive

Rejecting H₀ when H₀ is actually true.

```text
H₀ is true
     ↓
Reject H₀
     ↓
False positive
```

### False Discovery

A result declared significant that turns out to correspond to a true null hypothesis.

### Discovery

A hypothesis that you reject H₀ for.

---

# 13. The Big Picture

Connect everything you've learned:

```text
             Many Hypothesis Tests
                      ↓
             Multiple Testing Problem
                      ↓
          Many small p-values by chance
                      ↓
             False discoveries
                      ↓
        ┌─────────────┴─────────────┐
        ↓                           ↓
      FWER                         FDR
        ↓                           ↓
Control probability            Control expected
of ≥1 false positive            proportion of false
                                discoveries
        ↓                           ↓
   Bonferroni                 Benjamini-Hochberg
```

---

# 14. What to Remember

### FDR

> **Controls the expected proportion of false discoveries among the hypotheses declared significant.**

### Why is it needed?

> Because performing many hypothesis tests increases the chance of obtaining false positives.

### Common FDR method

> **Benjamini–Hochberg procedure**

### FDR vs Bonferroni

> **Bonferroni controls the probability of at least one false positive (FWER), while FDR controls the expected proportion of false discoveries among the rejected hypotheses.**

---

# Interview-Ready Answer

If an interviewer asks:

**"What is False Discovery Rate?"**

You can say:

> **False Discovery Rate is the expected proportion of false discoveries among all the hypotheses that we reject. It is useful when performing many hypothesis tests because simply using a p-value threshold such as 0.05 can produce many false positives. Methods such as Benjamini–Hochberg control the FDR while generally being less conservative than methods that control the family-wise error rate, such as Bonferroni.**

### Easy Mental Model

> **Many tests → many chances for false positives → FDR controls the proportion of false discoveries among the results we call significant.**
