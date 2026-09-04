# In Statistics, Probability Is Not Likelihood, Clearly Explained!!!

One of the most important distinctions in statistics is:

> **Probability and likelihood use the same mathematical ingredients, but they answer different questions.**

This distinction becomes especially important when learning:

* Maximum Likelihood Estimation (MLE)
* Bayesian statistics
* Hypothesis testing
* Probability distributions
* Machine learning

---

# 1. Probability vs Likelihood

Let's start with the simplest possible distinction.

### Probability asks:

> **"Given a model/parameter, how likely is the data?"**

### Likelihood asks:

> **"Given the data, which parameter values make the data most plausible?"**

The same mathematical expression can be used for both.

But **what we treat as unknown is different**.

---

# 2. A Simple Coin Example

Suppose we flip a coin 10 times and observe:

```text
H H H H H H H T T T
```

We got:

```text
7 Heads
3 Tails
```

Let:

$$
p=P(Heads)
$$

We don't know \(p\).

---

# 3. Probability

Suppose I tell you:

$$
p=0.5
$$

The question becomes:

> **If the coin has \(p=0.5\), what is the probability of getting exactly 7 heads in 10 flips?**

That's a probability question.

$$
P(X=7|p=0.5)
$$

Using the binomial distribution:

$$
P(X=7|p=0.5)
=
\binom{10}{7}(0.5)^7(0.5)^3
$$

$$
\approx 0.117
$$

So:

> If \(p=0.5\), getting exactly 7 heads has probability about 11.7%.

Here:

```text
p = fixed
Data = variable/random
```

---

# 4. Likelihood

Now let's reverse the question.

We already observed:

```text
7 Heads
3 Tails
```

Now ask:

> **Which value of \(p\) makes this observed data most plausible?**

We write:

$$
L(p|data)
$$

For 7 heads and 3 tails:

$$
L(p)
=
\binom{10}{7}p^7(1-p)^3
$$

Now:

```text
Data = fixed
p = variable
```

That's **likelihood**.

---

# 5. The Same Formula!

Here's the tricky part.

Probability:

$$
P(data|p)
=
\binom{10}{7}p^7(1-p)^3
$$

Likelihood:

$$
L(p|data)
=
\binom{10}{7}p^7(1-p)^3
$$

They look identical!

So what's the difference?

### The difference is what we're asking about.

```text
Probability:

Parameter → Data
   fixed      random


Likelihood:

Data → Parameter
fixed    variable
```

This is the key.

---

# 6. Think About the Direction

A very useful mental model:

```text
             PROBABILITY

        Assume parameter p
                │
                ▼
          What data might
             occur?
                │
                ▼
              DATA
```

Likelihood reverses the perspective:

```text
             LIKELIHOOD

          Observe DATA
                │
                ▼
        Which parameter p
        makes it plausible?
                │
                ▼
            Parameter
```

---

# 7. Maximum Likelihood Estimation

This leads directly to **Maximum Likelihood Estimation (MLE)**.

We observed:

```text
7 Heads
3 Tails
```

We want to find the \(p\) that maximizes:

$$
L(p)=p^7(1-p)^3
$$

The answer is:

$$
\hat p=\frac{7}{10}=0.7
$$

So MLE says:

> **The value of \(p\) that makes the observed data most likely is 0.7.**

---

# 8. Why Does \(p=0.7\) Make Sense?

Imagine different possible coins.

```text
p = 0.1
p = 0.3
p = 0.5
p = 0.7
p = 0.9
```

We observed:

```text
7 Heads out of 10
```

Which coin makes that observation most plausible?

Probably:

```text
p = 0.7
```

So:

```text
Observed data
      ↓
Likelihood
      ↓
Find p that maximizes likelihood
      ↓
MLE = 0.7
```

---

# 9. Likelihood Is Not a Probability Distribution Over Parameters

This is **extremely important**.

Suppose:

$$
L(p|data)
$$

has its highest value at:

$$
p=0.7
$$

You might incorrectly say:

> "There is a 70% probability that \(p=0.7\)."

❌ **That's not what likelihood says.**

Likelihood does **not** directly tell us:

$$
P(p=0.7|data)
$$

Instead, it tells us how well different parameter values explain the observed data.

---

# 10. Likelihood Can Compare Parameters

Suppose:

$$
L(0.7|data)=0.267
$$

and:

$$
L(0.5|data)=0.117
$$

Then:

$$
\frac{L(0.7|data)}{L(0.5|data)}
\approx2.28
$$

We can say:

> The observed data are about **2.28 times as likely under \(p=0.7\) as under \(p=0.5\)**, under the same model.

That's a valid likelihood comparison.

But don't say:

> "\(p=0.7\) has a 2.28 times greater probability of being true."

That's a different statement.

---

# 11. Probability vs Likelihood Table

|            | Probability                        | Likelihood                                      |
| ---------- | ---------------------------------- | ----------------------------------------------- |
| Data       | Variable/random                    | Observed/fixed                                  |
| Parameter  | Fixed                              | Variable                                        |
| Question   | What data could occur?             | Which parameter explains data best?             |
| Notation   | \(P(data\mid\theta)\)              | \(L(\theta\mid data)\)                          |
| Common use | Prediction                         | Parameter estimation                            |
| Example    | Probability of 7 heads if \(p=.5\) | Plausibility of different \(p\)'s given 7 heads |

---

# 12. Probability Distribution vs Likelihood Function

This distinction is even more important.

Suppose:

$$
X\sim Binomial(n,p)
$$

The probability mass function is:

$$
P(X=x|p)
=
\binom{n}{x}p^x(1-p)^{n-x}
$$

If \(p\) is fixed and \(x\) changes:

```text
p = fixed
   ↓
P(X=x|p)
   ↓
Probability distribution over X
```

But if \(x\) is observed and fixed:

```text
x = fixed
   ↓
L(p|x)
   ↓
Likelihood function over p
```

Same expression.

Different interpretation.

---

# 13. A Graph Makes This Much Easier

Imagine:

```text
Likelihood
   ↑
   │              ●
   │            ●   ●
   │          ●       ●
   │        ●           ●
   │      ●               ●
   │   ●                     ●
   └────────────────────────────→
       .1 .2 .3 .4 .5 .6 .7 .8 .9
                         p
```

The peak occurs around:

$$
p=0.7
$$

Therefore:

$$
\hat p_{MLE}=0.7
$$

The graph tells us:

> Which parameter values make the observed data more or less plausible.

---

# 14. Likelihood Does Not Have to Sum to 1

Another important difference.

A probability distribution must satisfy:

$$
\sum_x P(X=x)=1
$$

or for continuous variables:

$$
\int f(x)\,dx=1
$$

But a likelihood function doesn't have to integrate or sum to 1 over the parameter.

That's because likelihood isn't a probability distribution over \(p\).

For example:

```text
L(p | data)
```

can be rescaled by a positive constant without changing which \(p\) maximizes it.

---

# 15. Likelihood Ratios

Because likelihood is useful for comparing parameter values, we often use a **likelihood ratio**.

For two parameter values:

$$
\theta_1,\theta_0
$$

the likelihood ratio is:

$$
LR=
\frac{L(\theta_1|data)}
     {L(\theta_0|data)}
$$

Interpretation:

> How much more compatible are the observed data with \(\theta_1\) than with \(\theta_0\), according to the model?

This idea is fundamental in statistical inference.

---

# 16. Probability in Bayesian Statistics

Now here's where the distinction becomes really interesting.

Bayes' theorem says:

$$
P(\theta|data)
=
\frac{P(data|\theta)P(\theta)}
{P(data)}
$$

Notice:

$$
P(data|\theta)
$$

is a probability model for the data.

When we view it as a function of \(\theta\) after observing the data, it is also proportional to the **likelihood**:

$$
L(\theta|data)\propto P(data|\theta)
$$

Then Bayesian inference combines:

```text
Likelihood
     +
Prior
     ↓
Posterior
```

More explicitly:

$$
Posterior
\propto
Likelihood\times Prior
$$

---

# 17. This Is Where Probability and Likelihood Meet

Suppose:

```text
Data = 7 heads, 3 tails
```

Likelihood tells us:

> Which values of \(p\) make this data plausible?

Prior tells us:

> What did we believe about \(p\) before seeing the data?

Bayesian inference combines them:

```text
Prior
  +
Likelihood
  ↓
Posterior
```

The **posterior is a probability distribution over the parameter**.

That's different from likelihood.

---

# 18. Probability of a Parameter vs Likelihood of a Parameter

This is a classic interview question.

### Likelihood:

$$
L(p|data)
$$

asks:

> How well does \(p\) explain the observed data?

### Bayesian posterior:

$$
P(p|data)
$$

asks:

> Given the data and prior assumptions, how probable are different values of \(p\)?

That's why Bayesian statistics can meaningfully talk about:

> "The posterior probability that \(p\) lies between 0.6 and 0.8."

Likelihood alone doesn't provide that interpretation.

---

# 19. A Useful Analogy

Imagine you're investigating a crime.

You have:

```text
Evidence = observed data
```

And suspects:

```text
Suspect A
Suspect B
Suspect C
```

### Likelihood asks:

> "If this suspect were responsible, how likely would we be to see this evidence?"

### Probability/posterior reasoning asks:

> "Given the evidence and what we knew beforehand, how probable is it that this suspect is responsible?"

The distinction is subtle but powerful.

---

# 20. Another Way to Remember It

Think:

### Probability

**Model → Data**

```text
"If the coin has p = 0.5,
what data might I see?"
```

### Likelihood

**Data → Model**

```text
"I saw 7 heads.
Which p makes that observation most plausible?"
```

### Bayesian posterior

**Data + Prior → Updated belief about model**

```text
"I saw 7 heads.
Given what I believed before,
what should I now believe about p?"
```

---

# 21. Likelihood in Machine Learning

Likelihood is also fundamental in machine learning.

For independent observations:

$$
L(\theta)
=
\prod_{i=1}^{n}P(y_i|x_i,\theta)
$$

Instead of maximizing the product, we usually maximize the **log-likelihood**:

$$
\log L(\theta)
=
\sum_{i=1}^{n}\log P(y_i|x_i,\theta)
$$

Why?

Because products can become extremely tiny.

Logs turn:

$$
\prod_i P_i
$$

into:

$$
\sum_i\log P_i
$$

which is computationally easier.

---

# 22. Maximum Likelihood in Logistic Regression

In logistic regression:

$$
P(Y=1|X)
=
\frac{1}{1+e^{-(\beta_0+\beta_1X)}}
$$

The model produces probabilities.

Then we ask:

> Which coefficients \(\beta_0,\beta_1,\ldots\) make the observed outcomes most likely?

That's maximum likelihood estimation.

```text
Data
 ↓
Logistic model
 ↓
Likelihood
 ↓
Log-likelihood
 ↓
Optimize coefficients
 ↓
MLE coefficients
```

This is one reason likelihood is so important in machine learning.

---

# 23. Probability, Likelihood, and Loss

There is another useful connection.

For many models:

$$
-\log L(\theta)
$$

is called the **negative log-likelihood**.

Minimizing negative log-likelihood is equivalent to maximizing likelihood:

$$
\arg\min_\theta[-\log L(\theta)]
=
\arg\max_\theta L(\theta)
$$

This connects statistical estimation to machine-learning optimization.

For classification, **cross-entropy / log loss** is closely related to negative log-likelihood under the appropriate probabilistic model.

---

# 24. Common Mistakes

### ❌ "Likelihood is the probability that the parameter is true."

No.

Likelihood evaluates how well parameter values explain observed data.

---

### ❌ "\(L(\theta|data)\) is a probability distribution over \(\theta\)."

Not by itself.

Likelihood does not automatically sum/integrate to 1 over the parameter.

---

### ❌ "A likelihood of 0.8 means there is an 80% chance the model is correct."

No.

Likelihood values are not generally interpreted as probabilities of hypotheses.

---

### ❌ "Probability and likelihood are completely unrelated."

No.

They often use the **same mathematical function**.

The distinction comes from which quantity is treated as fixed and which is varied.

---

### ❌ "Likelihood reverses the conditional probability using Bayes' theorem."

Not exactly.

Likelihood is the same data-model function viewed as a function of the parameter.

Bayes' theorem is what allows us to combine likelihood with a prior to obtain a posterior.

---

# 25. The Most Important Equation

Remember this:

$$
\boxed{
P(data|\theta)
\quad\text{and}\quad
L(\theta|data)
}
$$

can be numerically the same function.

But:

```text
Probability:

P(data | θ)
     ↑
     │
 θ fixed
 data varies
```

while:

```text
Likelihood:

L(θ | data)
     ↑
     │
 data fixed
 θ varies
```

---

# 26. The Big Picture

This connects many statistical concepts we've discussed:

```text
                 MODEL
                   │
                   ▼
             Probability
                   │
                   ▼
            Observed data
                   │
                   ▼
              Likelihood
                   │
                   ▼
       Estimate parameters
                   │
                   ▼
                 MLE
```

And in Bayesian statistics:

```text
             Prior
               +
           Likelihood
               │
               ▼
           Posterior
```

---

# 🧠 Mental Model

Remember:

> **Probability looks forward. Likelihood looks backward.**

```text
PROBABILITY

Parameter ─────────→ Data
   p             What might happen?


LIKELIHOOD

Data ────────────→ Parameter
Observed       Which p explains it?
```

Even though the mathematical expression can be the same, **the question has changed**.

---

# 🎯 Interview-Ready Answer

> **Probability treats the model parameters as fixed and asks how likely different data are. Likelihood treats the observed data as fixed and evaluates how plausible different parameter values are under the model. The expression \(P(data|\theta)\) can be viewed as a likelihood function \(L(\theta|data)\) when considered as a function of \(\theta\). Likelihood is therefore not itself a probability distribution over parameters; it is commonly used for parameter estimation through maximum likelihood.**

---

# 🔑 One-Line Takeaway

> **Probability asks "Given the parameter, how likely is the data?" while likelihood asks "Given the data, which parameter values make it most plausible?"**
