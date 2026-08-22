A **histogram** is used in the real world to understand **how numerical data is distributed**. It quickly tells you where most values fall, how spread out they are, and whether there are unusual values.

For example, suppose you have the salaries of **1,000 employees**:

| Salary range | Employees |
| ------------ | --------: |
| ₹20k–₹40k    |       120 |
| ₹40k–₹60k    |       300 |
| ₹60k–₹80k    |       350 |
| ₹80k–₹100k   |       160 |
| ₹100k–₹120k  |        70 |

A histogram would immediately show that most employees earn between **₹40k and ₹80k**.

![Employee salary distribution](images/Employee%20salary%20distribution.png)


### Why is this useful?

Imagine you're a **Data Scientist** working for an e-commerce company. You have customers' ages:

```text
18, 19, 21, 22, 22, 23, 24, 25, 25, 26...
```

Looking at thousands of numbers is useless. A histogram can show:

```text
Age        Customers
18–25      ███████████████████
26–35      ███████████████████████████
36–45      ███████████
46–55      █████
56–65      ██
```

Now you immediately understand: **most customers are 26–35 years old.**

In real Data Science work, histograms are commonly used to examine **salary, age, transaction amount, delivery time, customer spending, model errors, house prices, response times**, etc.

They also help you spot important things such as **skewness and outliers**. For example, if most transactions are ₹500–₹5,000 but a few are ₹2 lakh+, the histogram will make that unusual tail visible.

### Histogram vs bar chart

This is an important interview distinction:

**Histogram → continuous numerical data grouped into ranges**

> Age: 20–30, 30–40, 40–50

**Bar chart → categorical data**

> Product: iPhone, Samsung, Pixel

So when you hear **histogram**, think:

**"I have a numerical variable. I want to understand its distribution."**

That's the main real-world purpose.
