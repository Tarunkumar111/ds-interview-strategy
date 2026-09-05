# The Binomial Distribution and Test, Clearly Explained!!!

## 1. What is the Binomial Distribution?

The **binomial distribution** is a probability distribution that tells us the probability of getting a certain number of **successes** in a fixed number of independent trials.

In simple words:

> **Binomial distribution answers: "Out of \(n\) attempts, how likely is it that I get exactly \(k\) successes?"**

Examples:

* Out of 10 customers, how many make a purchase?
* Out of 20 emails, how many are opened?
* Out of 100 products, how many are defective?
* Out of 50 coin flips, how many are heads?

---

# 2. The Key Idea

Every trial has only **two possible outcomes**:

```text
           Trial
          /     \
         /       \
    Success      Failure
```

Examples:

| Success   | Failure       |
| --------- | ------------- |
| Purchase  | No purchase   |
| Click     | No click      |
| Defective | Not defective |
| Head      | Tail          |
| Pass      | Fail          |

The names **success** and **failure** don't mean good or bad. "Success" simply means the outcome we're interested in counting.

---

# 3. The Four Conditions

A random variable follows a **binomial distribution** when these conditions are satisfied:

### 1. Fixed number of trials

There must be a fixed number:

$$
\boxed{n}
$$

of trials.

Example:

> Test 100 products.

---

### 2. Two possible outcomes

Each trial has two outcomes:

$$
\boxed{\text{Success or Failure}}
$$

---

### 3. Constant probability of success

The probability of success remains the same for every trial:

$$
\boxed{p}
$$

Failure probability is:

$$
\boxed{1-p}
$$

---

### 4. Independent trials

The outcome of one trial doesn't affect another.

```text
Trial 1 ──┐
Trial 2 ──┼── Independent
Trial 3 ──┘
```

---

# 4. Notation

We write:

$$
\boxed{X\sim Binomial(n,p)}
$$

Where:

* \(X\) = number of successes
* \(n\) = number of trials
* \(p\) = probability of success in each trial

For example:

$$
X\sim Binomial(10,0.3)
$$

means:

> 10 independent trials, with a 30% probability of success on each trial.

---

# 5. Binomial Probability Formula

The probability of getting exactly \(k\) successes is:

$$
\boxed{
P(X=k)
=
\binom{n}{k}
p^k(1-p)^{n-k}
}
$$

Where:

* \(n\) = total trials
* \(k\) = number of successes
* \(p\) = probability of success
* \(1-p\) = probability of failure

$$
\binom{n}{k}
= \text{number of ways to arrange the successes and failures}
$$

![binomial distribution](images/binomial-distribution.png)

---

# 6. Understanding the Formula

The formula has three main pieces:

$$
\binom nk
$$

counts **how many ways** the successes can occur.

$$
p^k
$$

represents the probability of getting \(k\) successes.

$$
(1-p)^{n-k}
$$

represents the probability of getting the remaining failures.

So:

$$
\boxed{
\text{Probability}
=
\text{Number of arrangements}
\times
\text{Probability of each arrangement}
}
$$

---

# 7. Simple Example: Coin Flips

Suppose we flip a fair coin:

$$
n=5
$$

times.

Probability of heads:

$$
p=0.5
$$

Question:

> What is the probability of getting exactly 3 heads?

Let:

$$
X=\text{number of heads}
$$

Then:

$$
X\sim Binomial(5,0.5)
$$

We want:

$$
P(X=3)
$$

Using the formula:

$$
P(X=3)
=
\binom53(0.5)^3(0.5)^2
$$

Since:

$$
\binom53=10
$$

we get:

$$
P(X=3)
=
10(0.5)^5
$$

$$
=\frac{10}{32}
$$

$$
\boxed{P(X=3)=0.3125}
$$

So there is a:

$$
\boxed{31.25\%}
$$

chance of getting exactly 3 heads.

---

# 8. Why Do We Need \(\binom nk\)?

This is an important part of the binomial distribution.

Suppose we want exactly 3 heads in 5 flips.

One possible sequence is:

```text
H H H T T
```

But there are many possible arrangements:

```text
H H H T T
H H T H T
H H T T H
H T H H T
H T H T H
...
```

All of these contain:

$$
3\text{ heads}
$$

and:

$$
2\text{ tails}
$$

The term:

$$
\binom53
$$

counts all possible arrangements.

The combination formula is:

$$
\boxed{
\binom nk
=
\frac{n!}{k!(n-k)!}
}
$$

---

# 9. Expected Value of a Binomial Distribution

If:

$$
X\sim Binomial(n,p)
$$

then:

$$
\boxed{
E[X]=np
}
$$

For example:

$$
n=100
$$

and:

$$
p=0.2
$$

Then:

$$
E[X]=100(0.2)
$$

$$
\boxed{20}
$$

So we expect approximately **20 successes** in the long run.

---

# 10. Variance and Standard Deviation

For a binomial random variable:

$$
\boxed{
Var(X)=np(1-p)
}
$$

Therefore:

$$
\boxed{
SD(X)=\sqrt{np(1-p)}
}
$$

Example:

$$
n=100,\quad p=0.2
$$

Variance:

$$
100(0.2)(0.8)=16
$$

Standard deviation:

$$
\sqrt{16}=4
$$

So:

$$
\boxed{E[X]=20,\quad SD(X)=4}
$$

---

# 11. "At Least" and "At Most"

Binomial problems don't always ask for **exactly** \(k\) successes.

### Exactly \(k\)

$$
P(X=k)
$$

Example:

> Exactly 5 customers purchase.

---

### At least \(k\)

$$
P(X\ge k)
$$

Example:

> At least 5 customers purchase.

This includes:

$$
5,6,7,\ldots,n
$$

---

### At most \(k\)

$$
P(X\le k)
$$

Example:

> At most 5 customers purchase.

This includes:

$$
0,1,2,3,4,5
$$

---

# 12. Real-World Example: Conversion Rate

Suppose an online store has:

* 100 visitors
* Each visitor has a 5% probability of purchasing
* Assume purchases are independent

Then:

$$
X\sim Binomial(100,0.05)
$$

We can ask:

### Exactly 5 purchases

$$
P(X=5)
$$

### At least 5 purchases

$$
P(X\ge5)
$$

### At most 5 purchases

$$
P(X\le5)
$$

### Expected purchases

$$
E[X]=100(0.05)=5
$$

This is a very common Data Science application.

---

# 13. Binomial Distribution vs Bernoulli Distribution

These are closely related.

### Bernoulli Distribution

One trial.

$$
\boxed{X\sim Bernoulli(p)}
$$

Example:

> Does one customer purchase?

---

### Binomial Distribution

Multiple independent Bernoulli trials.

$$
\boxed{X\sim Binomial(n,p)}
$$

Example:

> How many of 100 customers purchase?

Think:

```text
Bernoulli
    ↓
One yes/no trial

Binomial
    ↓
Many yes/no trials
    ↓
Count the successes
```

So:

$$
\boxed{\text{Binomial = sum of independent Bernoulli trials}}
$$

---

# 14. The Binomial Test

The **binomial test** is different from the **binomial distribution**, although they are closely related.

### Binomial distribution

Used to calculate probabilities of success counts.

### Binomial test

Used for **hypothesis testing involving a proportion/probability of success** when the data can be modeled as binomial.

---

# 15. Example of a Binomial Test

Suppose a company claims:

> "Our email open rate is 50%."

You test:

$$
n=100
$$

emails and observe:

$$
60
$$

opens.

You want to know whether the true open probability differs from 50%.

---

## Step 1: Set up hypotheses

Null hypothesis:

$$
\boxed{H_0:p=0.50}
$$

Alternative hypothesis:

$$
\boxed{H_1:p\ne0.50}
$$

This is a **two-sided binomial test**.

---

## Step 2: Observe the data

You observed:

$$
X=60
$$

successes out of:

$$
n=100
$$

---

## Step 3: Calculate the p-value

Under \(H_0\):

$$
X\sim Binomial(100,0.5)
$$

The binomial test calculates how unusual the observed result is under this null hypothesis.

For a two-sided test, the p-value accounts for outcomes at least as inconsistent with the null as the observed result, according to the test's specified two-sided definition.

Then:

```text
p-value < α
     ↓
Reject H₀

p-value ≥ α
     ↓
Fail to reject H₀
```

---

# 16. When Should You Use a Binomial Test?

A binomial test is useful when:

* You have **binary outcomes**.
* You have a fixed number of trials.
* Trials can reasonably be treated as independent.
* You want to test a hypothesized success probability.

Examples:

* Conversion rate
* Click-through rate
* Defect rate
* Survey yes/no responses
* Treatment success/failure
* Pass/fail outcomes

---

# 17. Binomial Test vs One-Proportion Z-Test

Both can be used to test a population proportion, but they differ in how the sampling distribution is handled.

### Binomial test

Uses the **exact binomial distribution**.

### One-proportion z-test

Uses a **normal approximation** to the binomial distribution under suitable conditions.

| Binomial Test                                   | One-Proportion Z-Test                           |
| ----------------------------------------------- | ----------------------------------------------- |
| Exact method                                    | Approximation                                   |
| Uses binomial distribution                      | Uses normal distribution                        |
| Useful for small samples or extreme proportions | Often convenient for sufficiently large samples |
| No normal approximation required                | Requires approximation conditions               |

For small samples, the exact binomial test can be preferable.

---

# 18. Binomial Distribution vs Normal Distribution

A binomial distribution is **discrete**.

Possible values are:

$$
0,1,2,\ldots,n
$$

A normal distribution is **continuous**.

```text
Binomial
0  1  2  3  4  5
●  ●  ●  ●  ●  ●

Normal
───────────────
   smooth curve
```

However, when \(n\) is sufficiently large and the probability isn't too close to 0 or 1, a binomial distribution can sometimes be approximated by a normal distribution.

---

# 19. Important Assumptions

Before using a binomial model, ask:

### Fixed number of trials?

$$
n=\text{fixed}
$$

### Only two outcomes?

```text
Success / Failure
```

### Same probability?

$$
p=\text{constant}
$$

### Independent?

Each trial doesn't affect the others.

If these assumptions don't hold, a binomial model may not be appropriate.

---

# 20. Common Real-World Applications

### Marketing

Number of customers who respond to an advertisement.

### E-commerce

Number of visitors who purchase.

### Manufacturing

Number of defective products in a sample.

### Healthcare

Number of patients responding to treatment.

### Machine Learning

Binary classification outcomes such as:

```text
Correct / Incorrect
```

### Quality Control

Number of failed units in a production batch.

---

# 21. Common Mistakes

### Mistake 1: Using binomial for more than two outcomes

If each trial can have:

```text
Red / Blue / Green
```

that's not directly binomial.

---

### Mistake 2: Ignoring independence

If one trial affects another, the standard binomial model may not apply.

---

### Mistake 3: Confusing \(p\) and \(1-p\)

$$
p=\text{success probability}
$$

$$
1-p=\text{failure probability}
$$

---

### Mistake 4: Confusing distribution with test

**Binomial distribution**:

> What is the probability of observing \(k\) successes?

**Binomial test**:

> Is the observed number of successes consistent with a hypothesized success probability?

---

# 22. Interview-Ready Answer

> **The binomial distribution models the number of successes in a fixed number of independent trials, where each trial has two possible outcomes and the probability of success remains constant. It is defined by \(n\), the number of trials, and \(p\), the probability of success. The probability of exactly \(k\) successes is \(P(X=k)=\binom nkp^k(1-p)^{n-k}\). The binomial test uses this distribution to test a hypothesis about a population success probability, such as whether a conversion rate differs from a specified value.**

---

# 23. Mental Model

Remember the difference:

```text
             BINOMIAL
                 │
        Fixed number of trials
                 ↓
         Two outcomes each
                 ↓
        Same probability p
                 ↓
         Independent trials
                 ↓
      Count the successes
                 ↓
       Binomial Distribution
```

And for the test:

```text
Observed successes
       +
Hypothesized probability
       ↓
  Binomial Test
       ↓
   p-value
       ↓
Reject / Fail to reject H₀
```

### One-line takeaway

$$
\boxed{
\text{Binomial Distribution}
=
\text{Number of successes in }n\text{ independent yes/no trials}
}
$$

$$
\boxed{
\text{Binomial Test}
=
\text{Test whether the observed success rate is consistent with a hypothesized probability}
}
$$
