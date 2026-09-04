# Conditional Probability, Clearly Explained!!!

## 1. What is Conditional Probability?

**Conditional probability** tells us the probability of an event happening **given that we already know another event has happened**.

In simple words:

> **Conditional probability = probability after receiving additional information.**

It is written as:

$$
\boxed{P(A\mid B)}
$$

Read this as:

> **"The probability of A given B."**

For example:

> What is the probability that a customer buys a product **given that they clicked the advertisement?**

The information that the customer **clicked the advertisement** changes the probability of purchase.

---

## 2. The Main Idea

Normally, we might ask:

> What is the probability that a customer buys something?

That's:

$$
P(\text{Buy})
$$

But if we learn that the customer clicked an advertisement, we can ask:

$$
P(\text{Buy}\mid\text{Clicked})
$$

The second probability uses **additional information**.

```text
Without additional information
          ↓
       P(Buy)

With additional information
          ↓
   P(Buy | Clicked)
```

This is the core idea behind conditional probability.

---

## 3. The Formula

The fundamental formula is:

$$
\boxed{
P(A\mid B)=\frac{P(A\cap B)}{P(B)}
}
$$

Where:

* \(P(A\mid B)\) = probability of \(A\) given \(B\)
* \(P(A\cap B)\) = probability that **both A and B happen**
* \(P(B)\) = probability that \(B\) happens

![Conditional Probability](images/conditional_probability.png)


### The key idea

Once we know that \(B\) happened, we are no longer considering the entire population.

We only consider the cases where **B happened**.

Then we ask:

> Out of those cases, how many also satisfy A?

---

# 4. Simple Example

Suppose a company has **100 customers**.

* 40 customers clicked an advertisement.
* 20 customers both clicked the advertisement **and purchased**.

We want:

> Probability that a customer purchased **given that they clicked**.

Let:

$$
A=\text{Purchased}
$$

$$
B=\text{Clicked}
$$

We know:

$$
P(A\cap B)=\frac{20}{100}=0.20
$$

and:

$$
P(B)=\frac{40}{100}=0.40
$$

Therefore:

$$
P(A\mid B)
=
\frac{0.20}{0.40}
$$

$$
\boxed{P(A\mid B)=0.50}
$$

So:

$$
\boxed{50\%}
$$

### Interpretation

> Among customers who clicked the advertisement, **50% purchased the product**.

---

# 5. The Most Important Intuition

Think of conditional probability as **changing the denominator**.

Normally:

$$
P(A)=\frac{\text{Number of A}}{\text{Total population}}
$$

But:

$$
P(A\mid B)
$$

means:

$$
\boxed{
P(A\mid B)
=
\frac{\text{Number of A and B}}
{\text{Number of B}}
}
$$

So instead of asking:

> "Out of everyone, how many are A?"

we ask:

> **"Out of the people who are B, how many are also A?"**

---

# 6. Another Real-World Example

Suppose an online store has 1,000 visitors.

|                  | Purchased | Didn't Purchase | Total |
| ---------------- | --------: | --------------: | ----: |
| **Used Mobile**  |       120 |             380 |   500 |
| **Used Desktop** |        80 |             420 |   500 |
| **Total**        |       200 |             800 | 1,000 |

Question:

> What is the probability that a visitor purchased **given that they used mobile**?

We only look at mobile users.

There are:

$$
500
$$

mobile users.

Among them:

$$
120
$$

purchased.

Therefore:

$$
P(\text{Purchase}\mid\text{Mobile})
=
\frac{120}{500}
$$

$$
\boxed{0.24=24\%}
$$

Notice that we **don't divide by 1,000**.

Why?

Because we already know the visitor used mobile.

Our relevant population has changed from:

$$
1000\rightarrow500
$$

---

# 7. Conditional Probability vs Normal Probability

| Normal Probability              | Conditional Probability              |
| ------------------------------- | ------------------------------------ |
| No additional condition         | Given additional information         |
| \(P(A)\)                        | \(P(A\mid B)\)                       |
| Uses entire relevant population | Uses only cases where \(B\) occurred |
| "Probability of A"              | "Probability of A given B"           |

Example:

$$
P(\text{Purchase})=20\%
$$

vs.

$$
P(\text{Purchase}\mid\text{Mobile})=24\%
$$

The second incorporates information about the device.

---

# 8. Conditional Probability Is Not Symmetric

This is **very important**.

In general:

$$
\boxed{P(A\mid B)\ne P(B\mid A)}
$$

For example:

$$
P(\text{Disease}\mid\text{Positive Test})
$$

is not necessarily equal to:

$$
P(\text{Positive Test}\mid\text{Disease})
$$

These answer different questions.

### Question 1

> Given that someone tested positive, what is the probability they have the disease?

$$
P(\text{Disease}\mid\text{Positive})
$$

### Question 2

> Given that someone has the disease, what is the probability they test positive?

$$
P(\text{Positive}\mid\text{Disease})
$$

They are not the same probability.

---

# 9. Conditional Probability and Independence

Conditional probability is closely connected to **independence**.

If A and B are independent:

$$
\boxed{P(A\mid B)=P(A)}
$$

Meaning:

> Knowing that B happened does not change the probability of A.

For example, when rolling a fair die twice:

* First roll = 6
* Second roll = 6

The first roll doesn't affect the second.

Therefore:

$$
P(\text{Second roll}=6\mid\text{First roll}=6)
=
P(\text{Second roll}=6)
=
\frac16
$$

---

# 10. Multiplication Rule

Conditional probability gives us an important relationship:

$$
\boxed{
P(A\cap B)=P(A\mid B)P(B)
}
$$

This is called the **multiplication rule**.

For example:

Suppose:

$$
P(B)=0.4
$$

and:

$$
P(A\mid B)=0.5
$$

Then:

$$
P(A\cap B)
=
0.5\times0.4
$$

$$
\boxed{P(A\cap B)=0.2}
$$

So there is a 20% probability that both A and B happen.

---

# 11. Conditional Probability and Bayes' Theorem

Conditional probability is the foundation of **Bayes' theorem**.

Bayes' theorem:

$$
\boxed{
P(A\mid B)
=
\frac{P(B\mid A)P(A)}
{P(B)}
}
$$

It allows us to **update our belief about A after observing B**.

A simple mental model:

```text
Initial belief
     ↓
Observe new evidence
     ↓
Update probability
     ↓
New belief
```

This is widely used in:

* Medical diagnosis
* Spam detection
* Fraud detection
* Machine learning
* Recommendation systems
* Search engines
* Risk assessment

---

# 12. Medical Example

Suppose:

* 1% of people have a disease.
* A test is positive for 95% of people who have the disease.
* The test also produces a positive result for 5% of healthy people.

A common question is:

> If someone tests positive, what is the probability they actually have the disease?

That's:

$$
P(\text{Disease}\mid\text{Positive})
$$

Notice that we need:

$$
P(\text{Positive}\mid\text{Disease})
$$

and the disease prevalence:

$$
P(\text{Disease})
$$

to calculate the desired probability.

This is exactly the kind of problem where **Bayes' theorem** becomes useful.

---

# 13. Conditional Probability in Data Science

Conditional probability is everywhere in Data Science.

### Classification

A classifier may estimate:

$$
P(Y=\text{Spam}\mid X)
$$

Meaning:

> Probability that an email is spam given its observed features.

### Recommendation Systems

$$
P(\text{Buy}\mid\text{Viewed Product})
$$

### Fraud Detection

$$
P(\text{Fraud}\mid\text{Transaction Features})
$$

### Medical Prediction

$$
P(\text{Disease}\mid\text{Symptoms})
$$

### Machine Learning

Many probabilistic ML algorithms work directly with conditional probabilities.

---

# 14. Conditional Probability in a Confusion Matrix

Suppose a model predicts whether customers will churn.

You might calculate:

$$
P(\text{Churn}\mid\text{High Risk})
$$

or:

$$
P(\text{High Risk}\mid\text{Churn})
$$

Again, these are different.

This distinction is important when interpreting:

* Precision
* Recall
* False-positive rate
* False-negative rate

For example, **precision** can be interpreted as:

$$
P(\text{Actually Positive}\mid\text{Predicted Positive})
$$

while **recall** is related to:

$$
P(\text{Predicted Positive}\mid\text{Actually Positive})
$$

The direction of the condition matters.

---

# 15. Common Mistake

A very common mistake is confusing:

$$
P(A\mid B)
$$

with:

$$
P(B\mid A)
$$

Remember:

### \(P(A\mid B)\)

Read **from right to left**:

> Probability of A **given B**.

The event after the vertical bar `|` is the **condition**.

```text
P(A | B)
     ↑
  condition
```

So:

$$
P(\text{Disease}\mid\text{Positive})
$$

means:

> Among people who tested positive, how many have the disease?

---

# 16. Quick Example to Remember

Suppose a class has 100 students:

* 60 are male.
* 30 males play cricket.
* 40 females play cricket.

Question:

> What is the probability that a student plays cricket **given that they are male**?

We only consider males.

$$
P(\text{Cricket}\mid\text{Male})
=
\frac{30}{60}
$$

$$
\boxed{50\%}
$$

The denominator is **60**, not 100.

That's conditional probability.

---

# 17. Important Properties

### Property 1

$$
0\le P(A\mid B)\le1
$$

### Property 2

$$
P(A\mid B)
=
\frac{P(A\cap B)}{P(B)}
$$

provided:

$$
P(B)>0
$$

### Property 3

If A and B are independent:

$$
P(A\mid B)=P(A)
$$

### Property 4

$$
P(A\cap B)=P(A\mid B)P(B)
$$

---

# 18. Interview-Ready Answer

> **Conditional probability is the probability of an event occurring given that another event has already occurred. It is represented as \(P(A\mid B)\) and calculated as \(P(A\mid B)=P(A\cap B)/P(B)\), provided \(P(B)>0\). The key idea is that once we know B occurred, we restrict our analysis to the cases where B is true. Conditional probability is fundamental to Bayes' theorem, machine learning, classification, medical diagnosis, and risk analysis.**

---

# 19. Mental Model

Remember this:

```text
            CONDITIONAL PROBABILITY
                     │
                     ↓
          "Given that B happened..."
                     │
                     ↓
        Ignore cases where B is false
                     │
                     ↓
       Look only at the B population
                     │
                     ↓
       How often does A occur there?
                     │
                     ↓
                 P(A | B)
```

### The formula to remember

$$
\boxed{
P(A\mid B)=
\frac{P(A\cap B)}{P(B)}
}
$$

### One-line takeaway

> **Conditional probability asks: "What is the probability of A after we know that B has happened?"**
