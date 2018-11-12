---
layout: post
title: Fundamentals of Unconstrained Optimization
subtitle: Notes on Numerical Optimization
categories: optimization
---
# Fundamentals of Unconstrained Optimization

In unconstrained optimization, we minimize an objective function that depends on real variable, with no restriction:

$$\min_{x} f(x)$$

where $x \in \mathbb{R}^n$ is a real vector with $n \ge 1$ components and $f: \mathbb{R}^n \rightarrow \mathbb{R}$ is a smooth function.

## What is a solution?

> A point x* is a *global minimizer* if $f(x^*) \le f(x), \forall x \in \mathbb{R}^n$

The global minimizer can be difficult to find. And most algorithms are able to find only a *local minimizer*:

> A point x* is a *local minimizer* if there is a neighborhood N of x* such that $f(x^*) \le f(x), \forall x \in N$

This is sometimes called a *weak local minimizer*.

> A point x* is a *strict local minimizer* (also called a strong local minimizer) if there is a neighborhood N of x* such that $f(x^*) < f(x), \forall x \in N$  with $x \ne x^*$.

A slightly more exotic type of local minimizer:

> A point x* is an *isolated local minimizer* if there is a neighborhood N of x* such that x* is the only local minimizer in N

While strict local minimizers are not always isolated, it is true that all isolated local minimizers are strict.

## Recognizing a local minimum

Is x* is a local minimum? → Examine all the points in its immediate vicinity to make sure that none of them has a smaller function value.

If f is twice continuously differentiable, we may be able to tell that x* is a local minimizer (and possibly a strict local minimizer) by examining just the gradient $\nabla f(x^ * )$ and the Hessian $\nabla^2 f(x^ * )$  by using Taylor's theorem.

> **Taylor's Theorem**
>
> Suppose that $f: \mathbb{R}^2 \rightarrow \mathbb{R}$ is continuously differentiable and that $p \in \mathbb{R}^n$. Then we have that
>
> $$f(x+p) = f(x) + \nabla f(x+tp)^Tp$$
>
> for some $t \in (0,1)$. 
> Moreover, if f is twice continuously differentiable, we have that
>
> $$\nabla f(x+p) = \nabla f(x) + \int_0^1 \nabla ^2 f(x+tp)p \mathrm{d}t $$
>
> and that
>
> $$f(x+p) = f(x) + \nabla f(x+tp)^Tp +\frac{1}{2}p^T \nabla ^2 f(x+tp)p$$

*Necessary conditions* for optimality are derived by assuming that x* is a local minimizer and then providing facts about $\nabla f(x^ * $ and $\nabla^2 f(x^ * )$

> **First-Order Necessary Conditions**
>
> If x* is a local minimizer and f is continuous differentiable in an open neighborhood of x* , then $\nabla f(x^*) = 0$.

> **Second-Order Necessary Conditions**
>
> If x* is a local minimizer of $f$ and $\nabla^2 f$ is continuous in an open neighborhood of x* , then  $\nabla f(x^ * ) = 0$ and $\nabla^2 f(x^*)$  is positive semidefinite.

> **Second-Order Sufficient Conditions**
>
> Suppose that $\nabla^2 f$ is continuous in an open neighborhood of x* and that $\nabla f(x^ *)=0$ and $\nabla^2 f(x^ *)$ is positive definite. Then x* is a strict *local minimizer* of $f$. 

> **Theorem**
>
> When $f$ is convex, any local minimizer x* is a global minimizer of $f$. If in addition $f$ is differentiable, then any stationary point x* is a global minimizer of $f$.

## Algorithms

### Line Search *vs* Trust Region

General approach of algorithms for unconstrained minimization:

* Supply a starting point $x_0$
* Generate a sequence of iterates $\{x_k\}_{k=0}^\infty$
* Terminate when either no more progress can be made or when it seems that a solution point has been approximated with sufficient accuracy.

There are 2 common strategies for moving from the current point $x_k$ to a new iterate $x_{k+1}$: *Line search* and *Trust region*.

#### *Line search* strategy

* Choose a direction $p_k$ 
* Search along this direction from the current state $x_k$ for a new state with a lower function value
* The distance can be found by solving approximately ($\alpha$ is step length): 

$$
\min_{\alpha>0} f(x_k + \alpha p_k)
$$

The exact minimization is expensive and unnecessary. In fact, the line search algorithm generates a limited number of trial step lengths until it finds one that the loosely approximates the minimum of above minimization.

#### *Trust region* strategy

* Construct a *model function* $m_k$ that approximately similar to $f$ in neighborhood of $x_k$.
* Search minimizer of $m_k$ (also $x_k$) in some region around $x_k$. In other words, we find the candidate step p by approximately solving the following subproblem:

$$
\min_{p} m_k(x_k+p)
$$

where $x_k +p$ lies inside the trust region.

* If solution does not produce a sufficient decrease in $f$ → *Trust region* is too large → Shrink it and re-solve.

The trust region is defined by $\|p\|_2 \le \Delta$ where the scalar $\Delta > 0$ is called the trust-region radius. The model $m_k$  is usually defined to be a quadratic function of the form:

$$
m_k(x_k + p)= f_k + p^T \nabla f_k + \frac{1}{2} p^T B_k p
$$

where $f_k, \nabla f_k, B_k$ are a scalar, vector, matrix, respectively. $B_k$ is either the Hessian $\nabla^2 f_k$ or some approximation to it.

The *line search* and *trust region* approaches differ in the order in which they choose the direction and distance of the move to the next iterate.

For line search, fixing the direction $p_k$ → identifying an appropriate distance $\alpha_k$

For trust region, choose a maximum distance - the trust region radius $\Delta_k$ → seek a direction and step

#### Search directions for *Line search* methods

##### The steepest-descent direction

The most obvious choice for search direction for line search method is *the steepest-descent direction* $- \nabla f_k$. That means among all the directions we could move from $x_k$, this is the way that $f$ decreases most rapidly.

Let's prove this. By Taylor's theorem, we have

$$
f(x_k +\alpha p) = f(x_k) +\alpha p^T \nabla f_k + \frac{1}{2} \alpha^2 p^T \nabla^2 f(x_k + tp) p \text{, for some }t \in (o, \alpha)
$$

which p is the search direction and $\alpha$ is the step-length parameter.

So, in this formula, *the rate of change* in $f$ along the direction $p$ at $x_k$ is $p^T \nabla f_k$.

As the result, the unit direction $p$ of the most rapid decrease is the solution to the problem

$$
\min_p p^T \nabla f_k \text{, subject to} \|p\| =1
$$

Because $p^T \nabla f_k = \|p\| \| \nabla f_k \| \cos \theta$ and $\| p\|=1$, we have $p^T \nabla f_k = \| \nabla f_k \| \cos \theta$. Minimization in (9) occurs when $\cos \theta = -1$ at $\theta = \pi$. In other words, the solution to (9) is

$$
p = -\nabla f_k / \|\nabla f_k\|
$$

In visual representation, this direction is orthogonal to the contours of the function.

![The direction](http://trond.hjorteland.com/thesis/img200.gif)

**Advantage of the steepest descent direction** is that it require calculation of the gradient $\nabla f_k$ but not of second derivatives. However, it can be excruciatingly slow on difficult problems.

When the $\theta$ is not exactly $\pi$ or the direction is just descent, Taylor's theorem also verifies that $f$ is still decreased with a sufficiently small. In this situation, $p_k$ is *a down hill direction*.

##### Newton direction

From the second-order Taylor series approximation to $f(x_k + p)$ :

$$
f(x_k + p) \approx f_k + p^T \nabla f_k + \frac{1}{2} p^T \nabla^2 f_k p \overset{def}{=} m_k(p)
$$

Assuming that $\nabla^2 f_k$ is positive definite, the Newton direction is defined by finding the vector $p$ that minimizes $m_k (p)$. By simply setting the derivative of $m_k(p)$ to zero, we obtain the following explicit formula:

$$
p^N_k = -\nabla^2 f_k^{-1} \nabla f_k
$$
