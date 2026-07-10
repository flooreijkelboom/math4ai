---
layout: default
parent: Essentials
nav_order: 2
title: Multivariate Calculus
has_children: true
---



# Multivariate Calculus

In multivariate calculus, we mainly concern ourselves with finding derivatives. You may know that the derivative describes 
the **rate of change** of the function. With rate of change we refer to how quickly the function value increases at some 
point $$x$$ when we increase the value of $$x$$. In the context of machine learning, 
we are often very interested in a function that describes how well our model performs given our parameters, that is: we want
to know which parameters give the best performance in our model. 

A running metaphor we will use is the following. We can imagine a variable $$y$$ which is formed through applying function $$f$$ to 
$$x$$, i.e. $$y = f(x)$$. In this case, we call $$x$$ an **input** and call $$y$$ an **output**. We are often interested in 
studying how **sensitive** our outputs are to a change in the inputs, or how much our inputs **influence** our outputs, 
as we will get more into it soon. This sensitivity is exactly what is captured by the derivative, e.g. if the derivative of the 
output with respect to the input is large in some point, we know that output is 'sensitive' to a small change increase around 
that point. Now, you can picture this as a machine spitting out outputs $$y$$ controlled with many knobs, where each knob 
corresponds to a variable $$x$$. The derivative tells us how sensitive the value our function spits out is to any turn of 
the knobs. Note that standard functions $$f: \mathbb{R} \to \mathbb{R}$$ are machines with one knob and spit out one value, 
but general functions $$f: \mathbb{R}^m \to \mathbb{R}^n$$ are machines with $$m$$ knobs and spit out $$n$$ different values. 
As we will look at later in this section, we have $$m \times n$$ derivatives in the latter case, for we can look at the 
sensitivity of each output to any of the knobs.

