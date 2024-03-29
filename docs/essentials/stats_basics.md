---
layout: default
parent: Statistics
grand_parent: Essentials
nav_order: 1
title: Basic probability theory
---
# Basic probability theory

{: .motivation }
To do any form of reasoning in machine learning - e.g. predicting if a given molecule is toxic for humans - one 
needs to be able to express how certain one is about the prediction. The mathematics used for quantifying uncertainty is
probability theory. In this section, we will cover arguably the most important object in probability theory - the random
variable - and learn about how to formulate questions about uncertainty.


## Basics: Random variables and probabilities

To study machine learning well, we need to develop a mathematical language to deal with collecting, analyzing,
and interpreting data. This is what we commonly understand to be 'statistics', which is our major topic of study in this
section. However, before we can deep dive into statistics we need to study the mathematical foundations of statistics 
briefly. Most importantly, we need to look at probability theory, which is what we will do in this section!


Probability theory is a special type of mathematics that can handle the uncertainty of events. Even though this area
of mathematics is very, very vast, we will mainly focus on what very useful object in probability theory: the random variable. 
Suppose we have a streaming site, and the event of interest we want to represent is the rating some user will give for a new movie 
just uploaded to the site. Let us denote this variable as $$R$$ for rating. We assume the user can rate the 
movie on a $$5$$ star scale, i.e. they can give it exactly the values 1 up to 5. For example, we can understand
$$R=1$$ as the situation that the rating given is one star, et cetera. Because we do not yet know what the rating $$R$$ is
beforehand, its outcome is uncertain for us. To **quantify** this uncertainty, we use probabilities. We call $$R$$ a **random variable**. 



What does it mean for the probability of some event to be $$\frac{1}{6}$$? You might intuitively understand the probability 
of a die (that is, half a pair of dice) ending up on a face with $$4$$ dots as $$\frac{1}{6}$$ because if you would roll
that die a certain number of times, you would expect it landed on a $$4$$ roughly a $$\frac{1}{6}$$th of the times. That is, a 
probability would tell you how **frequently** some event occurs. Even though this intuition is nice when first learning about 
probabilities, this understanding of probabilities is quite restrictive. For instance, when we are interested in the 
probability of you becoming a great academic, there is no way to interpret that probability as a frequency. But still, 
if one says that the probability of you becoming a great academic is $$\frac{5}{6}$$ instead of $$\frac{1}{6}$$ after studying this site 
(sadly not an actual statistic), that does tell you something about the **degree of belief** in you becoming a 
great academic after reading this site. It turns out that this second interpretation of probability theory is more 
useful in deep learning, even though this exact question is a large philosophical debate called 'frequentist versus 
Bayesian interpretation of probability'. 

For now, two properties are very important when considering a random variable. If we consider the set of 
all outcomes, we assume that 

1. The probability of each outcome lies somewhere in the interval $$[0, 1]$$, that is each probability is at least $$0.0$$ and at most $$1.0$$.
2. If we sum over the probabilities of all the outcomes, the total should add up to be exactly $$1$$.


For example, suppose we are optimistic and assign a probability of $$0.6$$ to the rating of the user being 5 stars, and assign a 
probability of $$0.1$$ to all other outcomes, this would define a valid random variable. We call the function that
assigns the probability to each outcome a **probability mass function** (or: pmf). Often, we write $$f_R$$ or $$p_R$$ for
the pmf of random variable $$R$$, so in this case $$f_R(5) = 0.6$$. 

Often, we denote 'the probability' with the symbol $$\mathbb{P}$$, and denote the set of all outcomes as $$\Omega$$. Hence,
for some random variable, $$X$$ the above equations can be formalized as

1. $$\mathbb{P}(X=x) = f_X(x) \in [0, 1]$$ for all $$x \in \Omega$$;
2. $$\sum_{x \in \Omega} \mathbb{P}(X=x) =\sum_{x \in \Omega} f_X(x) = 1$$.

We call the way these probabilities are divided over the outcomes a **distribution** of the random variable.


### Continuous case

There is one subtlety: if the outcomes do not come from a discrete set but rather from a continuous set, we need a slightly 
more exotic way to assign probabilities. In short, if we would again assign a probability greater than $$0$$ to any outcome, 
the fact that are are so many outcomes will imply that the total integral (the continuous counterpart of a sum) will not be equal to $$1$$. 
This implies that each outcome **must** have a probability of $$0$$, i.e. for all $$x \in \Omega$$ we have $$f_X(x) = 0$$ when $X$ is
a continuous random variable. Technically, we say that the probability of $$0$$, but the event is not impossible to occur, but do
not worry too much about this.

But what if we want to compute values for our random variable? Suppose the outcomes of our event $$X$$ 
are the entire number line, and $$f_X$$ is some function over this interval (if you want, picture a normal distribution 
if you are familiar with this already). We can mimic the idea of probability mass functions, but rather than assigning the
probability to each point directly, we can associate the area under the curve between two points as the probability our observation
will lie between those two points. To obey the same rules as mentioned above, we just assume that 1) the total area underneath this 
curve is again $$1$$, i.e. that

$$\int_{- \infty}^{\infty} f_X(x) dx = 1,$$

and 2) that for all $$x \in \Omega$$ we have $$f_X(x) \geq 0$$.

When associating the area with probability, we can now also ask that the probability is that $$\mathbb{P}(X \geq 0)$$ by
just integrating overall outcome greater than zero or equal to:

$$\mathbb{P}(X \geq 0) = \int_{0}^{\infty} f_X(x) dx.$$

In the continuous case, we call this function $$f_X$$ a **probability density function** (or: pdf), rather than a pmf. 



## Basics: Distributions and queries

In general, we might be interested in multiple variables. Suppose we also care about a new random variable $$H$$ with denotes
'whether a person is happy'. In this case, $$\mathbb{P}(H=0)$$ denotes the 
probability that the customer is unhappy, and $$\mathbb{P}(H=1)$$ denotes the probability that the customer is happy. 
In this case, we assume that the customer is either happy or unhappy, so there is no third option. This now gives us
a lot of different outcomes if we want to model both $$H$$ and $$R$$ simultaneously since we could in theory have a probability for the combination of outcomes and 
happiness scores, giving a total of $$5 \times 2 = 10$$ different probabilities. The notation does not change much, e.g.
if we consider the probability that someone gives a five-star rating and is happy to be $$0.5$$, we write $$\mathbb{P}(R=5, H=1) = 0.5$$.
We call a distribution over multiple random variables a **joint distribution**. 


{: .exercise }
Suppose we have random variables $$X_1, \cdots, X_n$$ with possible outcomes $$\Omega_1, \cdots, \Omega_n$$. Explain why
in general the joint $$\mathbb{P}(X_1, \cdots, X_n)$$ has $$\prod_{i=1}^n \{ |\Omega_i| \} - 1$$ parameters. What problems could this cause when trying to learn this joint distribution?

The beauty of a joint distribution is that we derive any information we might want to know of the individual random variables it
describes. For example, given the joint distribution above, we might ask either of the following two things: 1) what if I do not care about 
the specific rating of a user, but rather care whether or not their happy? And: 2) how do I find the probability that someone will rate a move five stars if I know they are unhappy? These questions about
our variables of interest are sometimes also called **queries**. 

In general, we differentiate two different questions:

1. **Marginal probabilities.** In this case, we are interested in the outcomes of a strict subset of our variables. The
first question in the previous section is an example of such a query. Formally, we ask how to get from $$\mathbb{P}(X_1, \cdots, X_n)$$ 
to $$\mathbb{P}(X_i)$$. 
2. **Conditional probabilities.** In this case, we are interested in the outcome of some of our variables if we already
know the outcome of the rest. This query corresponds to the second question in the previous section. We denote the probability
of $$X=x$$ given the outcome that $$Y=y$$ as $$\mathbb{P}(X=x \mid Y=y),$$ but this notation will be made formal in the
next section where we also study how to calculate these probabilities.

In the next section, we will cover how to answer these queries from the joint.


{: .summary }
In this section, you have seen how to formalize uncertain events and you have covered the most basic queries one can ask based on the joint distribution we have of our events.
