# Calculating Mean, Variance, and Standard Deviation — Clearly Explained

These three are **fundamental concepts in statistics**:

> **Mean** → tells us the center of the data  
> **Variance** → tells us how much the data varies around the mean  
> **Standard deviation** → tells us the spread in the original units

Let's understand them using one simple dataset.

---

## 1. Example Dataset

Suppose we have the following exam scores:

```text
10, 20, 30, 40, 50
```

We want to calculate:

1. Mean
2. Variance
3. Standard deviation

---

# 2. Mean — Finding the Center

The **mean** is simply the average.

## Formula

$$
\text{Mean} =
\frac{\text{Sum of all values}}{\text{Number of values}}
$$

### For our data:

Given the values:

$$
10,\ 20,\ 30,\ 40,\ 50
$$

Calculate the mean:

$$
\text{Mean} =
\frac{10 + 20 + 30 + 40 + 50}{5}
$$

$$
= \frac{150}{5}
$$

$$
\boxed{30}
$$

**Therefore, the mean is 30.**

So the mean is **30**.

Think of the mean as the **center of gravity of the data**.

```text
10    20    30    40    50
           ↑
         Mean
          30
```

---

# 3. Why do we need Variance?

Knowing the mean alone isn't enough.

Consider these two datasets:

```text
Dataset A:
28, 29, 30, 31, 32

Dataset B:
10, 20, 30, 40, 50
```

Both have:

$$
\text{Mean} = 30
$$

But clearly, **Dataset B is much more spread out**.

So we need a measure of **spread**.

That's where **variance** comes in.

---

# 4. Variance — Measuring Spread

Variance measures **how far the observations are from the mean, on average, using squared deviations**.

For our dataset:

```text
10, 20, 30, 40, 50
```

Mean = 30.

First calculate the difference between every value and the mean.

| Value | Value − Mean | Squared difference |
| ----: | -----------: | -----------------: |
|    10 |          -20 |                400 |
|    20 |          -10 |                100 |
|    30 |            0 |                  0 |
|    40 |          +10 |                100 |
|    50 |          +20 |                400 |

Now add the squared differences:

$$
400 + 100 + 0 + 100 + 400 = 1000
$$

For a **population**, divide by the number of observations:

$$
\text{Variance} = \frac{1000}{5}
$$

$$
\boxed{200}
$$

So, the **population variance is 200**.

---

# 5. Why do we Square the Differences?

This is a very important question.

You might ask:

> Why not just calculate the average distance from the mean?

Because positive and negative differences would cancel each other.

For our data:

```text
-20 + (-10) + 0 + 10 + 20 = 0
```

That would incorrectly suggest that there is **no variation**.

So we square the differences:

```text
(-20)² = 400
(-10)² = 100
(0)²   = 0
(10)²  = 100
(20)²  = 400
```

Now everything is positive.

> **Variance uses squared deviations so that positive and negative deviations don't cancel each other.**

---

# 6. Standard Deviation

Variance is useful, but there's a problem.

Our original data is measured in **marks**, but variance is measured in **marks²**.

That's not very intuitive.

So we take the square root of variance.

$$
\text{Standard Deviation} = \sqrt{\text{Variance}}
$$

### Our variance is:

$$
200
$$

Therefore:

$$
SD = \sqrt{200}
$$

$$
\boxed{SD \approx 14.14}
$$

So, the **standard deviation is approximately 14.14 marks**.

![SD](images/standard_deviation.png)

---

# 7. The Complete Calculation

For:

```text
10, 20, 30, 40, 50
```

### Step 1 — Mean

$$
\mu = 30
$$

### Step 2 — Deviations

```text
10 − 30 = -20
20 − 30 = -10
30 − 30 =   0
40 − 30 = +10
50 − 30 = +20
```

### Step 3 — Square deviations

```text
400
100
0
100
400
```

### Step 4 — Variance

$$
\frac{400 + 100 + 0 + 100 + 400}{5} = 200
$$

## Step 5 — Standard Deviation

$$
\sqrt{200} \approx 14.14
$$

Therefore:

| Measure            |    Result | Meaning                    |
| ------------------ | --------: | -------------------------- |
| Mean               |    **30** | Center                     |
| Variance           |   **200** | Squared spread             |
| Standard deviation | **14.14** | Typical spread around mean |

---

# 8. Population vs Sample Variance

This is very **important for Data Science interviews**.

There are two formulas.

## Population Variance

When you have the **entire population**:

$$
\sigma^2 =
\frac{\sum (x_i - \mu)^2}{N}
$$

Divide by **N**.

## Sample Variance

When your data is a **sample from a larger population**:

$$
s^2 =
\frac{\sum (x_i - \bar{x})^2}{n - 1}
$$

Divide by **n − 1**.

### Why $n - 1$?

Because when estimating population variance from a sample, using (n-1) gives an **unbiased estimator** of the population variance under the usual assumptions.

This is called **Bessel's correction**.

---

# 9. Why Standard Deviation is More Useful

Suppose the average salary in a company is:

```text
₹80,000
```

and the standard deviation is:

```text
₹10,000
```

This gives us an intuitive idea of the spread.

A salary of:

```text
₹90,000
```

is **1 standard deviation above the mean**.

A salary of:

```text
₹70,000
```

is **1 standard deviation below the mean**.

That's much easier to interpret than saying:

> "The variance is ₹100,000,000."

Variance is mathematically useful, but standard deviation is generally easier to interpret because it is in the **same units as the original data**.

---

# 10. A Very Important Mental Model

Remember the flow:

```text
                  DATA
                   ↓
              Calculate Mean
                   ↓
            Find deviations
                   ↓
           Square deviations
                   ↓
          Calculate average
                   ↓
               VARIANCE
                   ↓
             Take √
                   ↓
        STANDARD DEVIATION
```

Or even simpler:

> **Mean = Where is the center?**

> **Variance = How much does the data vary?**

> **Standard deviation = How spread out is the data, in the original units?**

---

# 11. Data Science Example

Suppose you're building a model that predicts house prices.

Your actual prices are:

```text
₹40L, ₹45L, ₹50L, ₹55L, ₹60L
```

You calculate:

* **Mean** → typical/central house price
* **Variance** → mathematical measure of price variability
* **Standard deviation** → how widely prices typically vary around the average

This helps you understand the **distribution and variability of your data before modeling**.

---

## Interview-ready answer

If an interviewer asks:

**"What is the difference between mean, variance, and standard deviation?"**

A good answer is:

> **Mean measures the central tendency of the data. Variance measures the average squared deviation from the mean, while standard deviation is the square root of variance and represents the spread of the data in the original units.**

### Remember:

$$
\boxed{\text{Mean} \rightarrow \text{Center}}
$$

$$
\boxed{\text{Variance} \rightarrow \text{Squared Spread}}
$$

$$
\boxed{\text{Standard Deviation} \rightarrow \text{Spread in Original Units}}
$$
