---
layout: default
parent: Statistics
grand_parent: Essentials
nav_order: 2
title: Probability calculus
---

# Probability calculus

{: .motivation }
In the previous section, we hinted that a joint distribution is very useful to have, for it allows us to answer any
question we might have about (subsets of) the random variables. In this section, we will study how to compute these
questions by introducing the most important rules of probability theory.


## Chain rule and conditional probabilities

Suppose we have two random variables $$X$$ and $$Y$$ with joint distribution $$\mathbb{P}(X, Y)$$. We understand 
$$\mathbb{P}(X=x, Y=y)$$ as the probability that $$X$$ has outcome $$x$$ and $$Y$$ has outcome $$y$$. Intuitively, we
can also understand that joint probability as follows: my belief that $$X$$ will take on outcome $$x$$ and $$Y$$ takes on
outcome $$y$$ can be 'decomposed' into my belief that $$X$$ will take on $$x$$ in general, and then that $$Y$$ takes on 
value $$y$$ given that $$X$$ has taken on value $$x$$. For example, my belief in me studying well and passing the exam is 
simply my belief in me studying well in general combined with my belief that if I study well, I will pass the exam. Formally,
we write this as 


$$\mathbb{P}(X=x, Y=y) = \mathbb{P}(X=x) \cdot \mathbb{P}(Y=y \mid X=x).$$

The opposite reasoning also goes, so

$$\mathbb{P}(X=x, Y=y) = \mathbb{P}(Y=y) \cdot \mathbb{P}(X=x \mid Y=y).$$

This is called the **chain rule** of probability theory, and this rule you will use over and over when doing probability
calculus. At this point, it becomes a bit convoluted to write $$X=x$$ every time, so we might write this also as

$$\mathbb{P}(X, Y) = \mathbb{P}(X) \cdot \mathbb{P}(Y \mid X),$$

to mean that $$\mathbb{P}(X=x, Y=y) = \mathbb{P}(X=x) \cdot \mathbb{P}(Y=y \mid X=x)$$ for all $$x$$ and $$y$$. 

Moreover, this rule generalizes, e.g.

$$\mathbb{P}(X, Y, Z) = \mathbb{P}(X) \cdot \mathbb{P}(Y, Z \mid X)$$

and thus

$$\mathbb{P}(X, Y, Z) = \mathbb{P}(X) \cdot \mathbb{P}(Y \mid X) \cdot \mathbb{P}(Z \mid X, Y).$$

In its most general glory, it would say that

$$\boxed{\mathbb{P}(X_1, \cdots, X_n) = \prod_{k=1}^n \mathbb{P}(X_k \mid X_1, \cdots, X_{k-1})}.$$

This also gives us a way to define conditional probabilities directly. Since

$$\mathbb{P}(X, Y) = \mathbb{P}(X) \cdot \mathbb{P}(Y \mid X),$$

we know that 

$$\boxed{\mathbb{P}(Y \mid X) = \frac{\mathbb{P}(X, Y)}{\mathbb{P}(X)}}$$

given that $$\mathbb{P}(X) \neq 0$$.




## Marginalization and marginal probabilities

Another very important fact of probability theory is **marginalization**. It says that if we have two random variables $$X$$ 
and $$Y$$, we can understand $$\mathbb{P}(X=x)$$ also as a 'summed out' probabilities of the joint between $$X$$ and $$Y$$, i.e.

$$\boxed{\mathbb{P}(X=x) = \sum_{y} \mathbb{P}(X=x, Y=y)}.$$ 

Equivalently, we can say that 

$$\boxed{\mathbb{P}(X=x) = \sum_{y} \mathbb{P}(X=x \mid Y=y) \cdot \mathbb{P}(Y=y)}.$$ 

This definition makes intuitive sense: my believe in $$X$$ taking on outcome $$x$$ in general, is simply a combined version
of $$X$$ taking on $$x$$ given that $$Y=y$$, weighted by my belief in $$Y=y$$. Here, we say that $$\mathbb{P}(X)$$ is a **marginal probability.**  


{: .exercise }
Suppose we have a joint distribution $$\mathbb{P}(X_1, X_2, X_3, X_4)$$, how can we use the above two rules
to find $$\mathbb{P}(X_1 = 1 \mid X_4=1, X_2 = 0)$$? The answer will be covered in the section on graphical models.

## Bayes rule


Last, but certainly not least, is a rule that follows directly from the chain rule we covered earlier. We observed that 
$$\mathbb{P}(X, Y) = \mathbb{P}(X) \cdot \mathbb{P}(Y \mid X)$$ and also $$\mathbb{P}(X, Y) = \mathbb{P}(Y) \cdot \mathbb{P}(X \mid Y)$$. 
It is not hard to see that

$$\boxed{\mathbb{P}(X \mid Y) = \frac{\mathbb{P}(Y \mid X) \cdot \mathbb{P}(X)}{\mathbb{P}(Y)}}$$ 

This is called **Bayes' rule** and gives us a very nice way to 'swap' the variables in a conditional distribution. 
 
{: .summary }
In this section, we learned how to answer queries
such as marginals and conditionals given our joint distribution. For this, we looked at the most important rules of 
probability theory.