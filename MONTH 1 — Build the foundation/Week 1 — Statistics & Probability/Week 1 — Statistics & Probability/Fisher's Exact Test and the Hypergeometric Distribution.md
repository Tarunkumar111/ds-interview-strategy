# Fisher's Exact Test and the Hypergeometric Distribution

These two concepts are closely related and are especially useful when working with **categorical data and small sample sizes**.

The easiest way to remember the connection is:

> **Hypergeometric distribution → calculates probabilities when sampling without replacement.**
> **Fisher's Exact Test → uses this idea to test whether two categorical variables are associated.**

---

# 1. Start with a Real-World Example

Suppose you run an A/B test with a **small number of users**.

You want to know whether a new website design affects whether users make a purchase.

Your results are:

|                | Purchased | Didn't Purchase | Total |
| -------------- | --------: | --------------: | ----: |
| **Old design** |         1 |               9 |    10 |
| **New design** |         5 |               5 |    10 |
| **Total**      |         6 |              14 |    20 |

The question is:

> **Is there a real association between website design and purchasing, or could this difference have happened by chance?**

This is a situation where **Fisher's Exact Test** can be useful.

---

# 2. What is Fisher's Exact Test?

**Fisher's Exact Test** is a statistical test used to determine whether there is a **significant association between two categorical variables**.

It is particularly useful when:

* Sample size is small
* Expected cell counts are small
* You have a **2 × 2 contingency table**

For our example:

```text
Website Design → Old / New

Purchase → Yes / No
```

So we have two categorical variables.

---

# 3. The 2 × 2 Contingency Table

A typical Fisher's Exact Test looks like this:

|             | Success | Failure | Total |
| ----------- | ------: | ------: | ----: |
| **Group A** |       a |       b |   a+b |
| **Group B** |       c |       d |   c+d |
| **Total**   |     a+c |     b+d |     n |

For our example:

|     | Purchased | Didn't Purchase |
| --- | --------: | --------------: |
| Old |         1 |               9 |
| New |         5 |               5 |

Fisher's Exact Test asks:

> **If there were actually no association between the two variables, how likely would we be to observe a table this extreme or more extreme?**

---

# 4. What Does "Exact" Mean?

This is the key idea behind Fisher's test.

Some statistical tests rely on **approximations**, especially when calculating probabilities.

Fisher's Exact Test calculates the probability **exactly** under the null hypothesis for the observed table, conditional on the table's margins.

That's why it is particularly useful for **small samples**.

---

# 5. What is the Hypergeometric Distribution?

Now we get to the second part.

The **hypergeometric distribution** models the probability of getting a certain number of successes when:

> **You sample from a finite population without replacement.**

### Simple example

Imagine a box containing:

```text
10 balls

6 red
4 blue
```

You randomly select **3 balls without putting them back**.

Question:

> What is the probability of getting exactly 2 red balls?

This is a **hypergeometric distribution** problem.

---

# 6. Why "Without Replacement" Matters

Suppose you select one red ball.

Now there are fewer red balls remaining.

The probability of getting another red ball has changed.

That's different from sampling **with replacement**, where the probabilities stay the same.

So:

```text
With replacement
→ Probability stays the same

Without replacement
→ Probability changes after each selection
→ Hypergeometric distribution
```

---

# 7. Hypergeometric Formula

The probability of getting exactly \(k\) successes is:

$$
P(X=k)=
\frac{
\binom{K}{k}
\binom{N-K}{n-k}
}{
\binom{N}{n}
}
$$

Where:

* \(N\) = total population size
* \(K\) = number of successes in the population
* \(n\) = number of items sampled
* \(k\) = number of successes observed in the sample

---

# 8. Simple Hypergeometric Example

Suppose:

```text
N = 10 total balls
K = 6 red balls
N-K = 4 blue balls

Sample n = 3 balls
```

We want:

```text
k = 2 red balls
```

Therefore:

$$
P(X=2)=
\frac{
\binom{6}{2}
\binom{4}{1}
}{
\binom{10}{3}
}
$$

Calculate:

$$
\binom{6}{2}=15
$$

$$
\binom{4}{1}=4
$$

$$
\binom{10}{3}=120
$$

Therefore:

$$
P(X=2)=\frac{15\times4}{120}
$$

$$
=\frac{60}{120}
$$

$$
\boxed{0.5}
$$

So there's a **50% probability** of getting exactly 2 red balls.

---

# 9. How Does This Connect to Fisher's Exact Test?

This is the important part.

Consider our A/B test again:

|       | Purchased | Didn't Purchase | Total |
| ----- | --------: | --------------: | ----: |
| Old   |         1 |               9 |    10 |
| New   |         5 |               5 |    10 |
| Total |         6 |              14 |    20 |

Under the null hypothesis:

> **Website design and purchase behavior are independent.**

If we fix the row and column totals, the number of purchases in one group follows a **hypergeometric distribution**.

Fisher's Exact Test uses this probability to determine how unusual the observed table is.

So conceptually:

```text
Contingency Table
       ↓
Fix the margins
       ↓
Hypergeometric probability
       ↓
Calculate probability of observed
and more-extreme tables
       ↓
Fisher's Exact Test p-value
```

---

# 10. The Null and Alternative Hypotheses

For Fisher's Exact Test:

### Null Hypothesis

$$
H_0:
\text{The two categorical variables are independent}
$$

In our example:

> Website design and purchase behavior are not associated.

### Alternative Hypothesis

$$
H_1:
\text{The two categorical variables are associated}
$$

---

# 11. When Should You Use Fisher's Exact Test?

A good rule of thumb:

### Use Fisher's Exact Test when:

* You have categorical variables
* You're analyzing a contingency table
* Sample size is small
* Expected cell counts are low
* Especially for a **2 × 2 table**

For larger datasets, the **Chi-square test of independence** is often used.

---

# 12. Fisher's Exact Test vs Chi-Square Test

This is an important Data Science interview topic.

|                       | Fisher's Exact Test | Chi-square Test                 |
| --------------------- | ------------------- | ------------------------------- |
| Data                  | Categorical         | Categorical                     |
| Typical table         | 2 × 2               | 2 × 2 or larger                 |
| Small samples         | **Excellent**       | Can be problematic              |
| Small expected counts | **Good choice**     | Approximation may be unreliable |
| Probability           | Exact               | Approximate                     |
| Computational cost    | Can be higher       | Generally lower                 |

### Simple rule

> **Small sample → Think Fisher's Exact Test.**

> **Larger sample → Chi-square may be appropriate.**

But don't choose solely based on sample size; the assumptions and study design matter too.

---

# 13. Real-World Data Science Examples

### Medical research

```text
Treatment → Yes / No

Outcome → Recovered / Not Recovered
```

You want to know whether treatment and recovery are associated.

---

### A/B testing

```text
Website → A / B

Conversion → Yes / No
```

You want to know whether website version and conversion are associated.

---

### Fraud detection

```text
Transaction type → Normal / Suspicious

Fraud → Yes / No
```

You want to determine whether the categories are associated.

---

### Clinical trials

```text
Drug → Drug A / Drug B

Side effect → Yes / No
```

You want to determine whether side effects are associated with treatment group.

---

# 14. The Big Picture

Remember the relationship like this:

```text
              Categorical Data
                     ↓
             Contingency Table
                     ↓
             Is sample small?
                     ↓
                    Yes
                     ↓
          Fisher's Exact Test
                     ↓
        Uses Hypergeometric Probability
                     ↓
                 p-value
                     ↓
          Test H₀: Independence
```

---

# 15. The Most Important Distinction

Don't confuse these two:

### Hypergeometric Distribution

It's a **probability distribution**.

> "What is the probability of getting exactly k successes when sampling without replacement?"

### Fisher's Exact Test

It's a **statistical test**.

> "Is there evidence of an association between two categorical variables?"

The connection is:

> **Fisher's Exact Test calculates probabilities using the hypergeometric distribution.**

---

# Interview-Ready Answer

If asked:

### "What is Fisher's Exact Test?"

> **Fisher's Exact Test is a statistical test used to determine whether two categorical variables are associated, particularly when sample sizes are small or expected cell counts are low. It calculates an exact p-value based on the hypergeometric distribution rather than relying on a large-sample approximation.**

### "What is the Hypergeometric Distribution?"

> **The hypergeometric distribution gives the probability of obtaining a specific number of successes when sampling from a finite population without replacement.**

### Easy mental model

> **Hypergeometric = sampling without replacement**

> **Fisher's Exact Test = association between categorical variables using exact probabilities**

> **Chi-square = approximate test of categorical association, often useful for larger samples**
