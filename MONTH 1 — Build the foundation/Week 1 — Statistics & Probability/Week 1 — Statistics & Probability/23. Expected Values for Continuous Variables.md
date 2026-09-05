# Expected Values for Continuous Variables!!!

## 1. What is Expected Value for a Continuous Variable?

For a **continuous random variable**, expected value represents the **long-run average value** of the variable.

The idea is the same as for discrete variables:

> **Expected value = probability-weighted average of all possible values.**

The difference is that a continuous variable can take **infinitely many possible values**, so instead of adding individual probabilities, we use **integration**.

---

# 2. The Formula

If \(X\) is a continuous random variable with probability density function \(f(x)\), then:

$$
\boxed{
E[X]
=
\int_{-\infty}^{\infty}x f(x)\,dx
}
$$

Where:

* \(X\) = continuous random variable
* \(x\) = a possible value of \(X\)
* \(f(x)\) = probability density function (PDF)
* \(E[X]\) = expected value

The basic idea is:

$$
\boxed{
\text{Expected Value}
=
\int
(\text{value}\times\text{probability density})
}
$$

---

# 3. Why Do We Need an Integral?

For a discrete variable, we can list the possible outcomes:

```text
X = 1, 2, 3, 4, 5, 6
```

and calculate:

$$
E[X]=\sum xP(X=x)
$$

But a continuous variable might be:

$$
X=1.1,\ 1.11,\ 1.111,\ 1.1111,\ldots
$$

There are infinitely many possible values.

We cannot simply list them all.

So we use an integral:

```text
Discrete
   ↓
Add individual outcomes
   ↓
Σ

Continuous
   ↓
Accumulate infinitely many tiny contributions
   ↓
∫
```

---

# 4. Understanding the PDF

For a continuous random variable, \(f(x)\) is a **probability density**, not the probability of exactly \(x\).

The probability that \(X\) falls between \(a\) and \(b\) is:

$$
\boxed{
P(a\le X\le b)
=
\int_a^b f(x)\,dx
}
$$

So the **area under the PDF curve** represents probability.

---

# 5. Expected Value as a Weighted Average

Think of the formula:

$$
E[X]
=
\int_{-\infty}^{\infty}x f(x)\,dx
$$

as doing this:

```text
Possible value x
      ↓
How much probability density is around x?
      ↓
x × f(x)
      ↓
Accumulate across all x
      ↓
Expected value
```

Values that have more probability density contribute more to the expected value.

---

# 6. Simple Example: Uniform Distribution

Suppose \(X\) is uniformly distributed between 0 and 10.

So:

$$
X\sim U(0,10)
$$

Its PDF is:

$$
f(x)=\frac{1}{10}
$$

for:

$$
0\le x\le10
$$

The expected value is:

$$
E[X]
=
\int_0^{10}x\frac{1}{10}\,dx
$$

$$
=
\frac{1}{10}\int_0^{10}x\,dx
$$

Since:

$$
\int x\,dx=\frac{x^2}{2}
$$

we get:

$$
E[X]
=
\frac{1}{10}
\left[\frac{x^2}{2}\right]_0^{10}
$$

$$
=
\frac{1}{10}\times\frac{100}{2}
$$

$$
\boxed{E[X]=5}
$$

This makes intuitive sense because the distribution is symmetric between 0 and 10.

---

# 7. Real-World Example: Delivery Time

Suppose:

$$
X=\text{delivery time in minutes}
$$

Delivery time is continuous because it could be:

$$
30.1,\ 30.15,\ 30.157,\ldots
$$

Suppose its probability density is described by \(f(x)\).

Then:

$$
E[X]
=
\int x f(x)\,dx
$$

If the result is:

$$
E[X]=35
$$

we interpret this as:

> **The long-run average delivery time is 35 minutes.**

It does **not** mean every delivery takes exactly 35 minutes.

---

# 8. Expected Value of a Function

Sometimes we aren't interested directly in \(X\).

Instead, we want the expected value of some function of \(X\).

For example:

$$
g(X)=X^2
$$

Then:

$$
\boxed{
E[g(X)]
=
\int_{-\infty}^{\infty}
g(x)f(x)\,dx
}
$$

Therefore:

$$
\boxed{
E[X^2]
=
\int_{-\infty}^{\infty}
x^2f(x)\,dx
}
$$

This concept is extremely important because variance uses \(E[X^2]\).

---

# 9. Expected Value and Variance

Recall:

$$
\boxed{
\operatorname{Var}(X)
=
E[(X-E[X])^2]
}
$$

There is another useful formula:

$$
\boxed{
\operatorname{Var}(X)
=
E[X^2]-(E[X])^2
}
$$

So for continuous variables:

$$
E[X]
=
\int xf(x)\,dx
$$

and:

$$
E[X^2]
=
\int x^2f(x)\,dx
$$

Then:

$$
\operatorname{Var}(X)
=
E[X^2]-(E[X])^2
$$

---

# 10. Expected Value vs Probability

Don't confuse these two.

### Probability

Answers:

> "How likely is an event?"

For example:

$$
P(10<X<20)
$$

### Expected value

Answers:

> "What is the long-run average value?"

For example:

$$
E[X]
$$

So:

```text
Probability
     ↓
How likely?

Expected Value
     ↓
What is the long-run average?
```

---

# 11. Expected Value Can Be Outside the Most Likely Value

The expected value doesn't necessarily have to be the value with the highest probability density.

For example, a skewed distribution might have:

```text
Most common value → 30
Expected value     → 40
```

This can happen because a small number of very large values pull the average upward.

This is common with things like:

* Income
* Transaction amounts
* House prices
* Insurance losses

---

# 12. Continuous Expected Value vs Discrete Expected Value

| Discrete              | Continuous                      |
| --------------------- | ------------------------------- |
| Countable outcomes    | Infinitely many possible values |
| Uses summation        | Uses integration                |
| \(E[X]=\sum xP(X=x)\) | \(E[X]=\int xf(x)dx\)           |
| Uses probability mass | Uses probability density        |

The underlying idea is the same:

$$
\boxed{\text{Probability-weighted average}}
$$

---

# 13. Important Property: Linearity

Expected value has a very useful property.

For constants \(a\) and \(b\):

$$
\boxed{
E[aX+b]=aE[X]+b
}
$$

For example, if:

$$
E[X]=20
$$

then:

$$
E[3X+5]
=
3(20)+5
$$

$$
\boxed{65}
$$

This property works for both discrete and continuous random variables.

---

# 14. Expected Value of Two Variables

Another important property is:

$$
\boxed{
E[X+Y]=E[X]+E[Y]
}
$$

Importantly, **independence is not required** for this property.

For example:

$$
E[X]=10
$$

$$
E[Y]=20
$$

Then:

$$
E[X+Y]=30
$$

regardless of whether \(X\) and \(Y\) are independent.

---

# 15. Expected Value in Data Science

Expected values appear throughout Data Science and Machine Learning.

### Expected Loss

A model's expected loss can be represented as:

$$
E[L(Y,\hat Y)]
$$

It asks:

> What is the average loss we would expect over the underlying data distribution?

### Expected Risk

$$
\boxed{
R(f)=E[L(Y,f(X))]
}
$$

Machine learning often aims to find a model that minimizes expected risk.

### Probability Distributions

Expected values summarize distributions such as:

* Normal distribution
* Exponential distribution
* Uniform distribution
* Gamma distribution
* Beta distribution

---

# 16. Example: Normal Distribution

Suppose:

$$
X\sim N(\mu,\sigma^2)
$$

The expected value is:

$$
\boxed{E[X]=\mu}
$$

For example:

$$
X\sim N(100,15^2)
$$

Then:

$$
\boxed{E[X]=100}
$$

So 100 is the long-run average of the random variable.

---

# 17. Example: Exponential Distribution

Suppose:

$$
X\sim\operatorname{Exponential}(\lambda)
$$

Then:

$$
\boxed{
E[X]=\frac{1}{\lambda}
}
$$

If:

$$
\lambda=0.2
$$

then:

$$
E[X]=\frac{1}{0.2}=5
$$

So the expected waiting time is:

$$
\boxed{5\text{ units}}
$$

This connects directly to the exponential distribution you studied earlier.

---

# 18. Important Concept: PDF vs Probability

For continuous variables:

$$
\boxed{P(X=x)=0}
$$

for any exact single value \(x\), under the usual continuous-distribution framework.

That doesn't mean \(x\) is impossible.

Instead, probability is assigned to **intervals**:

$$
P(a<X<b)
$$

using area under the PDF:

$$
P(a<X<b)
=
\int_a^b f(x)\,dx
$$

This is an important distinction when working with continuous distributions.

---

# 19. Interview-Ready Answer

> **For a continuous random variable, expected value represents the long-run average value of the variable. It is calculated by integrating the product of each possible value and its probability density: \(E[X]=\int_{-\infty}^{\infty}x f(x)\,dx\). Unlike discrete variables, where we use a summation, continuous variables use integration because they can take infinitely many possible values. Expected values are fundamental to probability distributions, variance, expected loss, and risk in Data Science and Machine Learning.**

---

# 20. Mental Model

Remember:

```text
Continuous Random Variable
          ↓
   Probability Density f(x)
          ↓
    x × f(x)
          ↓
 Integrate over all x
          ↓
     Expected Value
          ↓
   Long-run average
```

### The formula to remember

$$
\boxed{
E[X]
=
\int_{-\infty}^{\infty}x f(x)\,dx
}
$$

### One-line takeaway

> **Expected value for a continuous variable is the probability-weighted average of all possible values, calculated using an integral.**
