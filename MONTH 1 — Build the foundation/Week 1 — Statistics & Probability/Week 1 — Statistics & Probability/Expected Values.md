# Expected Values, Main Ideas!!!

## 1. What is Expected Value?

**Expected value (EV)** is the **long-run average outcome** we would expect if we repeated a random experiment many times.

In simple words:

> **Expected value tells us the average result we can expect over many repetitions.**

It does **not** necessarily mean the value you will actually get in one trial.

---

## 2. Simple Example: Rolling a Die

Suppose we roll a fair die.

Possible outcomes:

$$
1,2,3,4,5,6
$$

Each has probability:

$$
\frac16
$$

The expected value is:

$$
E(X)
=
1\left(\frac16\right)
+2\left(\frac16\right)
+3\left(\frac16\right)
+4\left(\frac16\right)
+5\left(\frac16\right)
+6\left(\frac16\right)
$$

$$
=
\frac{21}{6}
$$

$$
\boxed{E(X)=3.5}
$$

### Important!

You can never roll a **3.5** on a die.

That's okay.

Expected value doesn't mean:

> "This is the outcome I'm going to get."

It means:

> **"If I roll the die many, many times, the average result will approach 3.5."**

---

# 3. The Main Formula

For a **discrete random variable**:

$$
\boxed{
E(X)=\sum_x xP(X=x)
}
$$

In simple terms:

$$
\boxed{
\text{Expected Value}
=
\sum
(\text{Outcome}\times\text{Probability})
}
$$

So expected value is a **weighted average**, where the weights are probabilities.

---

# 4. Another Example

Suppose a business has the following possible outcomes from a marketing campaign:

|  Profit | Probability |
| ------: | ----------: |
| ₹10,000 |         0.2 |
|  ₹5,000 |         0.5 |
|      ₹0 |         0.3 |

Expected profit:

$$
E(X)
=
10,000(0.2)
+
5,000(0.5)
+
0(0.3)
$$

$$
=2,000+2,500+0
$$

$$
\boxed{E(X)=₹4,500}
$$

So over many similar campaigns, the **average profit per campaign** would be expected to approach ₹4,500, assuming the probabilities and outcomes remain stable.

---

# 5. Expected Value Is a Weighted Average

This is the most important intuition.

Normal average:

$$
\frac{x_1+x_2+x_3}{3}
$$

Expected value:

$$
x_1P(x_1)+x_2P(x_2)+x_3P(x_3)
$$

The more likely an outcome is, the more influence it has on the expected value.

```text
High probability
       ↓
More influence on EV

Low probability
       ↓
Less influence on EV
```

---

# 6. Expected Value of a Fair Game

Suppose a game has:

* 50% chance of winning ₹100
* 50% chance of losing ₹100

Then:

$$
E(X)
=
100(0.5)+(-100)(0.5)
$$

$$
=50-50
$$

$$
\boxed{E(X)=0}
$$

This is called a **fair game** because the expected gain is zero.

---

# 7. Expected Value Can Be Negative

Expected value doesn't have to be positive.

Suppose a lottery ticket:

* Costs ₹100
* Has a 1% chance of winning ₹5,000
* Otherwise you receive ₹0

Your **net payoff** is:

* ₹4,900 if you win
* −₹100 if you lose

Then:

$$
E(X)
=
4,900(0.01)
+
(-100)(0.99)
$$

$$
=49-99
$$

$$
\boxed{E(X)=-₹50}
$$

So the expected loss per ticket is ₹50.

---

# 8. Expected Value of a Random Variable

If \(X\) is a random variable, then:

$$
\boxed{E[X]}
$$

is its expected value.

For example:

$$
X=\text{daily number of customers}
$$

Then:

$$
E[X]
$$

represents the **long-run average number of customers per day**.

Expected value is therefore widely used with **probability distributions**.

---

# 9. Expected Value and Probability Distributions

A probability distribution tells us:

> How likely is each possible value?

Expected value summarizes that distribution with its **probability-weighted average**.

```text
Probability Distribution
          ↓
Possible outcomes
          +
Their probabilities
          ↓
     Expected Value
          ↓
 Long-run average
```

For a continuous random variable:

$$
\boxed{
E[X]=\int_{-\infty}^{\infty}x f(x)\,dx
}
$$

where \(f(x)\) is the probability density function.

You don't need this formula for the basic intuition, but it becomes important for continuous distributions.

---

# 10. Expected Value vs Mean

These concepts are closely related but are not exactly the same thing.

### Expected value

The theoretical mean of a probability distribution:

$$
\boxed{E[X]}
$$

### Sample mean

The average calculated from observed data:

$$
\boxed{
\bar X=\frac{1}{n}\sum_{i=1}^{n}X_i
}
$$

For example:

```text
Probability Distribution
        ↓
Theoretical average
        ↓
Expected value

Observed data
        ↓
Actual calculated average
        ↓
Sample mean
```

With enough observations under appropriate conditions, the sample mean tends to approach the expected value.

---

# 11. Expected Value in Data Science

Expected value is fundamental to Data Science and Machine Learning.

### Decision Making

Suppose different business outcomes have different probabilities.

Expected value helps compare decisions based on their average predicted payoff.

### Risk Analysis

For example:

$$
E(\text{Loss})
$$

can represent expected financial loss.

### Machine Learning

Many ML concepts involve expectations, including:

* Expected loss
* Expected risk
* Expected reward
* Expected prediction error

For example:

$$
\boxed{
R(f)=E[L(Y,f(X))]
}
$$

This represents the **expected loss** of a prediction function.

### Reinforcement Learning

Expected future reward is central to evaluating actions and policies.

---

# 12. Expected Value of a Function

An important property is:

$$
\boxed{
E[aX+b]=aE[X]+b
}
$$

This is called **linearity of expectation**.

For example, if:

$$
E[X]=10
$$

then:

$$
E[3X+5]
=
3E[X]+5
$$

$$
=30+5
$$

$$
\boxed{35}
$$

---

# 13. Linearity of Expectation

One of the most useful rules:

$$
\boxed{
E[X+Y]=E[X]+E[Y]
}
$$

This is true **even when \(X\) and \(Y\) are not independent**.

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

No independence assumption is required.

This property is extremely useful in probability and Data Science.

---

# 14. Expected Value vs Variance

These measure different things.

### Expected value

Tells us the **center** or long-run average.

$$
\boxed{E[X]}
$$

### Variance

Tells us how much the values **spread around the expected value**.

$$
\boxed{
\operatorname{Var}(X)=E[(X-E[X])^2]
}
$$

Think:

```text
Expected Value
      ↓
   Center

Variance
      ↓
   Spread
```

---

# 15. Expected Value Doesn't Tell the Whole Story

Two probability distributions can have the **same expected value** but very different risks.

For example:

### Investment A

Almost always returns ₹100.

### Investment B

50% chance of ₹0 and 50% chance of ₹200.

Both have:

$$
E[X]=₹100
$$

But their risk is very different.

Therefore:

> **Expected value tells us the average outcome, but not how uncertain or variable the outcome is.**

That's why we often consider:

* Expected value
* Variance
* Standard deviation
* Distribution shape

together.

---

# 16. Important Properties

### Constant

If \(c\) is a constant:

$$
\boxed{E[c]=c}
$$

### Scaling

$$
\boxed{E[cX]=cE[X]}
$$

### Addition

$$
\boxed{E[X+Y]=E[X]+E[Y]}
$$

### Subtraction

$$
\boxed{E[X-Y]=E[X]-E[Y]}
$$

### Linear transformation

$$
\boxed{E[aX+b]=aE[X]+b}
$$

---

# 17. Common Mistake

Don't interpret:

$$
E[X]=50
$$

as:

> "The next observation will be 50."

Instead:

> **"Across many repetitions, the average outcome tends toward 50."**

For example, the expected value of a die is:

$$
3.5
$$

even though 3.5 can never appear on a single roll.

---

# 18. Interview-Ready Answer

> **Expected value is the probability-weighted average of all possible outcomes of a random variable. It represents the long-run average outcome if the random process is repeated many times under stable conditions. For a discrete random variable, it is calculated as \(E[X]=\sum_x xP(X=x)\). Expected value is widely used in probability, risk analysis, decision-making, and machine learning, particularly in concepts such as expected loss and expected risk.**

---

# 19. Mental Model

Remember:

```text
Possible Outcomes
       ↓
Their Probabilities
       ↓
Outcome × Probability
       ↓
Add Everything
       ↓
EXPECTED VALUE
       ↓
Long-run Average
```

### One-line takeaway

$$
\boxed{
\text{Expected Value}
=
\text{Probability-weighted average of possible outcomes}
}
$$

> **Expected value tells you what the average outcome would tend to be over many repetitions—not necessarily what will happen in one trial.**
