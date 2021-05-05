---
title: Solving Linear Recurrences
categories: [Math Articles]
tags: [math, article, recurrences]
math: true
---

In this article, we'll discuss how to solve both homogenous and non-homogenous linear recurrences with constant coefficients. First, let's review a few definitions to see what all of these terms mean.

## Definitions

### Recurrence Relation

<blockquote class="blockquote-definition">
<hr>
A recurrence relation is an equation that relates the next term in a sequence of numbers as a function of the terms preceding it.
</blockquote>

A classic recurrence relation is the **Fibonacci sequence**:

$$
\begin{align*}
F_n &= F_{n-1} + F_{n-2} \\
F_0 &= 0 \\
F_1 &= 1
\end{align*}
$$

Note that when actually calculating the values of the recursive sequence, we need more than just the recurrence relation. We also need initial values for our sequence that we can use to calculate the rest of the sequence. In this case, we can use the values of $F_0$ and $F_1$ to calculate $F_2$. Once we solve for this, we can then use $F_1$ and the recently calculated $F_2$ to solve for $F_3$, and so on.

$$
\begin{align*}
F_2 &= F_{0} + F_{1} = 0 + 1 = 1 \\
F_3 &= F_{1} + F_{2} = 1 + 1 = 2 \\
F_4 &= F_{2} + F_{3} = 1 + 2 = 3 \\
\end{align*}
$$

### Linear

A linear recurrence relation is a recurrence relation that only contains linear multiples of previous terms. That is, there can be no terms in the recurrence relation such as $a_{n-1}^2$ or $a_{n-1}a_{n-2}$. Instead, you can only have first degree terms.

Here are a few examples of linear recurrences:

$$
\begin{align*}
a_n &= a_{n-1} + a_{n-5} \\
a_n &= 3a_{n-1} + 2a_{n-3} \\
a_n &= a_{n-1} - a_{n-2} + a_{n-3} \\
\end{align*}
$$

On the other hand, here are a few non-linear recurrences:

$$
\begin{align*}
a_n &= a_{n-1}^2 + a_{n-2} \\
a_n &= 3a_{n-1}a_{n-2} \\
a_n &= 4a_{n-1} - 3^{a_{n-2}} + \sqrt{a_{n-3}} \\
\end{align*}
$$

In general, linear recurrences are much easier to calculate and solve than non-linear recurrence relations. As a result, this article will be focused entirely on solving **linear** recurrences.

### Degree

In the case of the Fibonacci sequence, the recurrence relation depended on the previous $2$ values to calculate the next value in the sequence. This means that the Fibonacci relation has degree $2$.

Here's an example of a relation with degree $4$ since the next value of $a_n$ depends on the previous $4$ values of $a_n$.

$$a_n = a_{n-1} + 2a_{n-2} + 5a_{n-3} + a_{n-4}$$

However, the following recurrence relation still has degree $3$ even though it doesn't depend on necessarily $3$ terms:

$$a_n = a_{n-2} + a_{n - 3}$$

It is only the farthest back term that matters when calculating degrees, so it doesn't matter if the $a_{n-1}$ term was skipped. Here's the more formal definition of the degree of a linear recurrence relation:

<blockquote class="blockquote-definition">
<hr>
A linear recurrence relation has degree $k$ if and only if it can be expressed in the form

$$a_n = c_1a_{n-1} + c_2a_{n-2} + ... + c_ka_{n-k}$$

with $c_1, c_2, ..., c_k \in \mathbb{Z}$ and $c_k \neq 0$.

</blockquote>

### Homogenous vs Non-homogenous

There are two primary types of linear recurrences: homogenous and non-homogenous.

<blockquote class="blockquote-definition">
<hr>
A recurrence relation is homogenous if the degree of all terms in the equation is the same.
</blockquote>

When a recurrence relation is linear, which we will assume for the remainder of this article, homogenous vs non-homogenous becomes much simpler. In this case, since linear implies that the degree of all of our terms have a power of at most $1$, the only other terms that could appear are constant terms / polynomials of $n$. To see what this means, it's best to look at a few examples.

All of the previous examples of linear recurrence relations in this article were actually homogenous relations, so here are a few non-homogenous ones:

$$
\begin{align*}
a_n &= a_{n-1} + 4 \\
a_n &= 3a_{n-1} + n^2 \\
a_n &= 4a_{n-1} + n^2 + n + 1 \\
\end{align*}
$$

Note that we can actually separate non-homogenous recurrence relations into two parts: a homogenous part and then some polynomial $f(n)$. This will be key to solving the relation later.

## Solving Linear Recurrences

First, we have to clarify what it even means to "solve" a linear recurrence. After all, if we're given enough initial values and the recurrence relation, we can solve for any value of the sequence through just plug and chug. However, this can be extremely slow for huge values of $n$, making an explicit formula very desirable. The idea of "solving" a recurrence relation is to find some function such as $a_n = 4^n$ that we can plug a huge value of $n$ into directly to find the value of $a_n$. This function is known as the **closed-form** expression for $a_n$.

For instance, the Fibonacci numbers have the following closed-form expression known as **Binet's Formula**:

$$F_n = \frac{1}{\sqrt{5}}\left(\left(\frac{1 + \sqrt{5}}{2}\right)^n - (\left(\frac{1-\sqrt{5}}{2}\right)^n\right)$$

### Homogenous Recurrences



### Non-homogenous Recurrences



## Dealing with Complex Numbers (Maybe?)

## Sources

- [http://nms.lu.lv/wp-content/uploads/2016/04/21-linear-recurrences.pdf](http://nms.lu.lv/wp-content/uploads/2016/04/21-linear-recurrences.pdf)
- [http://www.cse.yorku.ca/course_archive/2007-08/F/1019/A/recurrence.pdf](http://www.cse.yorku.ca/course_archive/2007-08/F/1019/A/recurrence.pdf)
