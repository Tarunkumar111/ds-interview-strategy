The **exponential distribution** is useful when you want to model **how long you have to wait until an event happens**.

### Simple mental model

> **Exponential distribution = waiting time until the next event.**

For example:

* How long until the next customer enters a store?
* How long until the next phone call arrives?
* How long until the next server request?
* How long until a machine fails?
* How long until the next bus arrives?

![Exponential Distribution](images/exponential%20distribution.png)

### Real-world example: Customer support

Suppose a support center receives calls at an average rate of **6 calls per hour**.

You want to know:

> **What's the probability that I have to wait more than 10 minutes for the next call?**

This is a classic exponential-distribution problem because we're interested in the **waiting time until the next event**.

The rate is:

$$
\lambda = 6 \text{ calls/hour}
$$

The exponential probability density function is:

$$
f(t) = \lambda e^{-\lambda t}, \qquad t \geq 0
$$

For waiting **more than** time $t$, we use:

$$
P(T > t) = e^{-\lambda t}
$$

---

### Where you see it in Data Science

| Situation        | What you're modeling            |
| ---------------- | ------------------------------- |
| Website requests | Time until next request         |
| Call center      | Time until next call            |
| ATM/bank         | Time until next customer        |
| Server systems   | Time until next request/failure |
| Manufacturing    | Time until machine failure      |
| Network          | Time between events             |
| Insurance        | Time until certain events       |

### Very important distinction

Don't confuse **Exponential** and **Poisson** distributions.

**Poisson → How many events occur in a fixed period?**

> "How many customers arrive in the next 1 hour?"

**Exponential → How long until the next event?**

> "How long until the next customer arrives?"

They are closely related.

If events occur independently at a **constant average rate**, then:

> **Poisson → number of events**

> **Exponential → waiting time between events**

### Interview-ready answer

> **The exponential distribution is used to model the waiting time between consecutive independent events occurring at a constant rate. For example, it can model the time until the next customer arrives, the next server request, or a machine failure.**

The key phrase to remember is:

**"Exponential = waiting time."**
