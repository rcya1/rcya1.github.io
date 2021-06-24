---
title: Solving Linear Recurrences
date: 2021-05-10 17:30:00 -0400
categories: [Math]
tags: [Math, Guide, Recurrences]
math: true
toc: true
toc_sticky: true
excerpt: In this article, we'll discuss how to solve both homogenous and non-homogenous linear recurrences with constant coefficients. If you already know what linear recurrences are and all of the vocabulary surrounding them, feel free to just skip to the next section to see how to solve homogenous and non-homogenous linear recurrences. If you're unfamilar with some of these terms, the first section goes over the basic definitions regarding linear recurrences.
---

In this article, we'll discuss how to solve both homogenous and non-homogenous linear recurrences with constant coefficients. If you already know what linear recurrences are and all of the vocabulary surrounding them, feel free to just skip to the next section to see how to solve homogenous and non-homogenous linear recurrences. If you're unfamilar with some of these terms, the first section goes over the basic definitions regarding linear recurrences.

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

### Homogenous vs Non-Homogenous

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

### What It Means to "Solve" a Linear Recurrence 

First, we have to clarify what it even means to "solve" a linear recurrence. After all, if we're given enough initial values and the recurrence relation, we can solve for any value of the sequence through just plug and chug. However, this can be extremely slow for huge values of $n$, making an explicit formula very desirable. The idea of "solving" a recurrence relation is to find some function such as $a_n = 4^n$ that we can plug a huge value of $n$ into directly to find the value of $a_n$. This function is known as the **closed-form** expression for $a_n$.

For instance, the Fibonacci numbers have the following closed-form expression known as **Binet's Formula**:

$$F_n = \frac{1}{\sqrt{5}}\left(\left(\frac{1 + \sqrt{5}}{2}\right)^n - \left(\frac{1-\sqrt{5}}{2}\right)^n\right)$$

To calculate any value of $F_n$, we can just plug $n$ into this formula rather than have to compute all values of $F_n$ up to the desired $n$. To show how this works, let's try to calculate $F_10$. From just applying the recurrence relation of the Fibonacci sequence, we get:

$$
\begin{align*}
F_2 &= F_0 + F_1 = 0 + 1 = 1 \\
F_3 &= F_1 + F_2 = 1 + 1 = 2 \\
F_4 &= F_2 + F_3 = 1 + 2 = 3 \\
F_5 &= F_3 + F_4 = 2 + 3 = 5 \\
F_6 &= F_4 + F_5 = 3 + 5 = 8 \\
F_7 &= F_5 + F_6 = 5 + 8 = 13 \\
F_8 &= F_6 + F_7 = 8 + 13 = 21 \\
F_9 &= F_7 + F_8 = 13 + 21 = 34 \\
F_{10} &= F_8 + F_9 = 21 + 34 = 55 \\
\end{align*}
$$

On the other hand, we can use Binet's formula to calculate the value for us directly without having to go through $F_2$ through $F_9$. Unfortunately, Binet's formula is not very friendly since it has this nasty binomial power that will require just as much work, if not more, to expand. If you do the expansion with the binomial theorem, many of the terms will actually cancel out between the two binomials, but it still isn't a fun time.

The best way to do this would probably be to just use decimals and a calculator, which can show that this formula does in fact work:

$$F_{10} = \frac{1}{\sqrt{5}}\left(\left(\frac{1 + \sqrt{5}}{2}\right)^{10} - \left(\frac{1-\sqrt{5}}{2}\right)^{10}\right)$$

$$F_{10} = \frac{122.991869381 - 0.00813061875}{2.2360679775} = 55$$

As a result, the Fibonacci sequence is typically not the best example for displaying the utility of having a closed form expression. Instead, let's take a look at a different recurrence relation:

$$
\begin{align*}
a_n &= 6a_{n-1} - 9a_{n-2} \\
a_0 &= 1 \\
a_1 &= 4
\end{align*}
$$

The closed form for this recurrence relation can be found to be:

$$a_n = 3^n + n3^{n-1}$$

Therefore, let's say we wanted to calculate $a_{100}$. Rather than plug and chug through all $100$ values of $a_n$, we can instead just plug in and quickly learn that $a_{100} = 3^{100} + 100 * 3^{99}$. In this case, the simple closed form expression is much simpler and faster than bashing through the values of $a_n$.

In the next two sections, we'll talk about how to derive these closed form expressions for any linear recurrence. We'll first discuss homogenous recurrences since solving them is much simpler and more systematic than solving non-homogenous recurrences.

## Solving Homogenous Recurrences

As a recap of what it means for a linear recurrence to be homogenous, a homogenous linear recurrence does not contain any terms besides $a_n$ in its recurrence relation. In particular, this means that there can be no constant coefficients or any terms that involve $n$ directly inside of the recurrence relation. See *Homogenous vs Non-Homogenous* for more details.

To solve these recurrences, we'll first construct something known as the characteristic polynomial and characteristic equation of the recurrence relation.

<blockquote class="blockquote-definition">
<hr>
The <b>characteristic polynomial</b> of the degree $k$ recurrence relation

$$a_n = c_1a_{n-1} + c_2a_{n-2} + ... c_ka_{n-k}$$

is denoted as

$$x^k - c_1x^{k-1} - c_2x^{k-2} - ... - c_{k-1}x - c_k$$

When we set this to zero, we get the <b>characteristic equation</b> of the recurrence relation. The solutions to this equation are known as the <b>characteristic roots</b>.

</blockquote>

To find the solution to our recurrence relation, we need to find the characteristic roots of it. Once we find the characteristic roots, there are two cases: either all of them are distinct or there are some duplicates. Let's first handle the case where all of them are distinct.

In the case where they are all distinct, let's call our characteristic roots $r_1, r_2, ..., r_k$. Our solution to the linear recurrence is then of the form:

$$a_n = \alpha_{\small 1} r_1^n + \alpha_{\small 2} r_2^n + ... + \alpha_{\small k} r_k^n$$

The next thing we need to do is just solve for our values of $\alpha$, which we can do by plugging in the initial conditions. See the *Homogenous Recurrence Examples* section below to see an example of this.

Next, let's consider the roots are not distinct. How many times a root appears as a solution to a polynomial is known as its multiplicity. For instance, the equation $(x-3)^2(x-2)$ has $2$ distinct roots. $2$ is a root with multiplicity $1$ while $3$ is a root with multiplicity $2$. Therefore, the idea of having non-distinct roots means that there are some characteristic roots with multiplicity greater than $1$.

Let's denote the multiplicity of the characteristic root $r_i$ by $m_i$, and let's say that we have $x$ distinct roots. Then, our solution has the following form instead:

$$a_n = \sum_{i=1}^{x}\sum_{j=1}^{m_i}\alpha_{\small i,j}n^{j-1}r_i^n$$

Once again, we can just plug in the initial conditions to find our values of $\alpha$. This form is pretty hard to understand from the formula, so see the example in the *Non-Homogenous Recurrence Examples* section below. What it does is basically just adds another exponential for each copy of the characteristic root but with an extra $n$ factor tacked onto it.

### Homogenous Recurrence Examples

<blockquote class="blockquote-example">
<hr>
Solve the following recurrence equation:

$$
\begin{align*}
a_n &= 5a_{n-1} - 6a_{n-2} \\
a_0 &= 2 \\
a_1 &= 3
\end{align*}
$$

</blockquote>

Let's first write the characteristic equation:

$$x^2 - 5x + 6 = 0$$

We can solve this by factoring to get $x = 2, 3$. All of our roots are distinct, so we can use the following form:

$$a_n = \alpha_{\small 1} r_1^n + \alpha_{\small 2} r_2^n + ... + \alpha_{\small k} r_k^n$$

$$a_n = \alpha_{\small 1} 2^n + \alpha_{\small 2} 3^n$$

From here, we can plug in our initial conditions of $a_0 = 2, a_1 = 3$. This gives us the following system of equations that we can use to solve for $\alpha_{\small 1}$ and $\alpha_{\small 2}$.

$$
\begin{align*}
a_0 = 2 = \alpha_{\small 1} * 2^0 + \alpha_{\small 2} * 3^0 \\
a_1 = 3 = \alpha_{\small 1} * 2^1 + \alpha_{\small 2} * 3^1
\end{align*}
$$

Solving, we get $\alpha_{\small 1} = 3, \alpha_{\small 2} = -1$. Therefore, the final solution to this recurrence equation is:

$$\boxed{a_n = 3 * 2^n - 3^n}$$

Try plugging in some values to verify this! Now, let's move on to an example that will have repeated roots.

<blockquote class="blockquote-example">
<hr>
Solve the following recurrence equation:

$$
\begin{align*}
a_n &= 14a_{n-1} - 72a_{n-2} + 160a_{n-3} - 128a_{n-4} \\
a_0 &= 2 \\
a_1 &= 3 \\
a_2 &= 5 \\
a_3 &= 9
\end{align*}
$$

</blockquote>

We can set up our characteristic equation:

$$x^4 - 14 x^3 + 72 x^2 - 160 x + 128 = 0$$

We can factor this to get the following, which shows that we have repeated roots:

$$(x-4)^3(x-2) = 0$$

Therefore, we have the characteristic root $4$ with multiplicity $3$ and the characteristic root $2$ with multiplicity $1$. We can then plug this into the form mentioned above:

$$a_n = \sum_{i=1}^{x}\sum_{j=1}^{m_i}\alpha_{\small i,j}n^{j-1}r_i^n$$

$$a_n = \alpha_{\small 1,1} 4^n + \alpha_{\small 1,2} n4^n + \alpha_{\small 1,3} n^2 4^n + \alpha_{\small 2,1} 2^n$$

We can then plug in our four initial conditions to solve this recurrence:

$$
\begin{align*}
a_0 = 2 = \alpha_{\small 1,1} * 4^0 + \alpha_{\small 1,2} * 0 * 4^0 + \alpha_{\small 1,3} * 0^2 * 4^0 + \alpha_{\small 2,1} 2^0 \\
a_1 = 3 = \alpha_{\small 1,1} * 4^1 + \alpha_{\small 1,2} * 1 * 4^1 + \alpha_{\small 1,3} * 1^2 * 4^1 + \alpha_{\small 2,1} 2^1 \\
a_2 = 5 = \alpha_{\small 1,1} * 4^2 + \alpha_{\small 1,2} * 2 * 4^2 + \alpha_{\small 1,3} * 2^2 * 4^2 + \alpha_{\small 2,1} 2^2 \\
a_3 = 9 = \alpha_{\small 1,1} * 4^3 + \alpha_{\small 1,2} * 3 * 4^3 + \alpha_{\small 1,3} * 3^2 * 4^3 + \alpha_{\small 2,1} 2^3
\end{align*}
$$

This gives us the following system of equations:

$$
\begin{align*}
2 &= \alpha_{\small 1, 1} + \alpha_{\small 2, 1} \\
3 &= 4\alpha_{\small 1, 1} + 4\alpha_{\small 1, 2} + 4\alpha_{\small 1, 3} + 2\alpha_{\small 2, 1} \\
5 &= 16\alpha_{\small 1, 1} + 32\alpha_{\small 1, 2} + 64\alpha_{\small 1, 3} + 4\alpha_{\small 2, 1} \\
9 &= 64\alpha_{\small 1, 1} + 192\alpha_{\small 1, 2} + 576 \alpha_{\small 1, 3} + 8\alpha_{\small 2, 1}
\end{align*}
$$

Solving this system, we get

$$\alpha_{\small 1,1} = -\frac{19}{8}, \alpha_{\small 1,2} = \frac{69}{64}, \alpha_{\small 1,3} = -\frac{9}{64}, \alpha_{\small 2,1} = \frac{35}{8}$$

Therefore, our final answer is:

$$\boxed{a_n = -\frac{19}{8} 4^n + \frac{69}{64} n4^n -\frac{9}{64} n^2 4^n + \frac{35}{8} 2^n}$$

## Solving Non-Homogenous Recurrences

While there was a systematic way to approach homogenous recurrences, solving non-homogenous recurrences requires more guessing. First, note that we can express any non-homogenous linear recurrence $a_n$ as the sum of a homogenous linear recurrence $b_n$ and a polynomial $f(n)$.

The first step of the procedure is to solve for the general form of $b_n$. That is, find the characteristic roots of $b_n$ but don't find the values of $\alpha$. Next, we need to do some guessing and checking to find an equation for $a_n$ that works in the relation given. When we're looking for this, we do **not** need to have this equation satisfy the initial conditions.

After we find this equation for $a_n$, we can then add on our solution to $b_n$. After this, we can solve for those values of $\alpha$ to make this combined equation match our initial conditions.

When searching for equation forms that will satisfy the relation for $a_n$, it is mostly guess and check. However, we can use a few tips to guide our searching. Most of the time, the correct relation will be very similar in form to $f(n)$. For instance, if $f(n)$ is a polynomial, we should try out polynomials of similar same degree. If $f(n)$ is an exponential like $d^n$, then we can try multiples of $d^n$ and also throw in some multiples of $nd^n, n^2d^n$, etc. In the sections below, we will go over some examples to show you how this process works since just describing it is difficult.

### Non-Homogenous Recurrence Example

<blockquote class="blockquote-example">
<hr>
Solve the following recurrence equation:

$$
\begin{align*}
a_n &= 3a_{n-1} - 2a_{n-2} + 3n + 4 \\
a_0 &= 1 \\
a_1 &= 2 \\
\end{align*}
$$

</blockquote>

The first step of the process is to isolate the homogenous linear recurrence from this equation. We can separate $a_n$ into a homogenous $b_n$ and a polynomial $f(n)$.

$$
\begin{align*}
a_n &= 3a_{n-1} - 2a_{n-2} + 3n + 4 \\
b_n &= 3a_{n-1} - 2a_{n-2} \\
f(n) &= 3n + 4 \\
\end{align*}
$$

To solve $b_n$, we can once apply the exact same method as in the previous step: find the characteristic roots and then write the general form of the recurrence. This gives us the following:

$$(x-2)(x-1) = 0$$

Therefore, our solution to $b_n$ will be of the form:

$$b_n = \alpha_{\small 1} 2^n + \alpha_{\small 2} 1^n = \alpha_{\small 1} 2^n + \alpha_{\small 2}$$

Now that we have solved the homogenous version of the problem, we can move on to guessing and checking for solutions to our non-homogenous $a_n$. First, note that $f(n)$ is a linear polynomial, so we may guess that a solution $a_n$ might also be a linear polynomial. Let's try this and do:

$$a_n = ax + b$$

Now, what we want to do is substitute this expression into our recurrence relation to solve for the coefficients $a$ and $b$ that make this form work. These coefficients for $a$ and $b$ must satisfy the recurrence relation for all integer values of $n$. Let's first do a bit of plugging in and rearranging:

$$
\begin{align*}
a_n &= 3a_{n-1} - 2a_{n-2} + 3n + 4 \\
an + b &= 3(a(n-1) + b) - 2(a(n-2) + b) + 3n + 4 \\
&= 3an - 3a + 3b - 2an + 4a - 2b + 3n + 4 \\ \\
0 &= a + 3n + 4 \\
\end{align*}
$$

Uh oh, we have a problem here. There is no constant value we can give to $a$ such that it will satisfy this equation for all $n$. As a result, we can conclude that the recurrence relation for $a_n$ does not have a linear solution. Let's try a quadratic instead:

$$a_n = ax^2 + bx + c$$

We can then do the exact same as before, although it will get a bit messy due to the quadratic:

$$
\begin{align*}
a_n &= 3a_{n-1} - 2a_{n-2} + 3n + 4 \\ \\
an^2 + bn + c &= 3(a(n-1)^2 + b(n-1) + c) - 2(a(n-2)^2 + b(n-2) + c) + 3n + 4 \\
&= 3(a(n^2 - 2n + 1) + b(n-1) + c) - 2(a(n^2-4n + 4) + b(n-2) + c) + 3n + 4 \\
&= 3an^2 - 6an + 3a + 3bn - 3b + 3c - 2an^2 + 8an - 8a - 2bn + 4b - 2c + 3n + 4 \\ \\
0 &= 2an - 5a + b + 3n + 4 \\
\end{align*}
$$

Now that we've simplified our equation greatly, this looks much more promising! Note that $c$ disappeared in our equation, which means that we can make $c$ anything. For simplicity, we'll just take $c = 0$. To solve for values of $a$ and $b$ for all values of $n$, we have a few options: the first is to just simply plug in a bunch of values of $n$ and then solve for $a$ and $b$ from there. However, a more rigorous solution would be to gather terms to form a polynomial in terms of $n$. Then, all of the coefficients in this polynomial must be $0$ for this to be a valid solution. If this isn't possible, then this form is also invalid.

$$
\begin{align*}
0 &= (2a+3)n - 5a + b + 4 \\
0 &= 2a + 3 \\
a &= -\frac{3}{2} \\ \\
0 &= -5a + b + 4 \\
b &= -\frac{23}{2} \\
\end{align*}
$$

Therefore, our solution to $a_n$ is:

$$a_n = -\frac{3}{2}n^2 - \frac{23}{2}n$$

If you plug this into the recurrence relation, this will satisfy that relationship! However, we have a major issue here: it doesn't satisfy any of our initial conditions! This is where our previous solution for $b_n$ comes into play. What we can do is add together these solutions to create a complete solution for $a_n$ that also has values for $\alpha$ that we can solve for to make sure it aligns with our specific solution.

$$
\begin{align*}
a_n &= -\frac{3}{2}n^2 - \frac{23}{2}n + \alpha_{\small 1} 2^n + \alpha_{\small 2} \\ \\
a_0 &= 1 = -\frac{3}{2} * 0^2 - \frac{23}{2} * 0 + \alpha_{\small 1} 2^0 + \alpha_{\small 2} \\
a_1 &= 2 = -\frac{3}{2}* 1^2 - \frac{23}{2} * 1 + \alpha_{\small 1} 2^1 + \alpha_{\small 2} \\ \\
1 &= \alpha_{\small 1} + \alpha_{\small 2} \\
2 &= -\frac{3}{2} - \frac{23}{2} + 2\alpha_{\small 1} + \alpha_{\small 2} \\
15 &= 2\alpha_{\small 1} + \alpha_{\small 2} \\ \\
\alpha_{\small 1} &= 14 \\
\alpha_{\small 2} &= -13
\end{align*}
$$

Therefore, we finally have our full solution:

$$a_n = -\frac{3}{2}n^2 - \frac{23}{2}n + 14 * 2^n - 13$$

## Why It Works

While the above goes over how to solve these recurrences, a lot of it just seems like magic formulas. In the below sections, I will try to explain *why* these equations work and how you can reason through them to the best of my ability, although the proofs may not be perfect.

### Homogenous Recurrences
There are two key theorems that we will use while solving homogenous linear recurrence relation:

<blockquote class="blockquote-theorem">
<hr>

If $a_n$ and $b_n$ are solutions to a recurrence relation, then their sum $a_n + b_n$ also satisfies that recurrence relation.
</blockquote>

To prove this, we can simply apply the recurrence relation definition a few times and do a bit of grouping.

$$
\begin{align*}
a_n &= c_1a_{n-1} + c_2a_{n-2} + ... + c_ka_{n-k} \\
b_n &= c_1b_{n-1} + c_2b_{n-2} + ... + c_kb_{n-k} \\
a_n + b_n &= c_1(a_{n-1} + b_{n-1}) + c_2(a_{n-2} + b_{n-2}) + ... + c_k(a_{n-k} + b_{n-k}) \\ \\
d_n &= a_n + b_n = c_1d_{n-1} + c_2d_{n-2} + ... + c_kd_{n-k}
\end{align*}
$$

<blockquote class="blockquote-theorem">
<hr>

If $a_n$ is a solution to a recurrence relation, then $\alpha a_n$ also satisfies that recurrence relation for any constant $\alpha$.
</blockquote>

To prove this, we can simply apply the recurrence relation definition.

$$
\begin{align*}
a_n &= c_1a_{n-1} + c_2a_{n-2} + ... + c_ka_{n-k} \\
\alpha * a_n &= c_1 \alpha * a_{n-1} + c_2 \alpha * a_{n-2} + ... + c_k \alpha * a_{n-k} \\ \\
d_n &= \alpha * a_n = c_1d_{n-1} + c_2d_{n-2} + ... + c_k d_{n-k}
\end{align*}
$$

Now that we have this, we can construct an approach to our problem. If we have a recurrence relation of degree $k$, then there will be $k$ initial values that we need to satisfy. Therefore, what we can do is find $k$ different sequences that satisfy our recurrence relation. We can add together these $k$ different sequences to get another sequence that will still satisfy this recurrence relation. If we take each of those $k$ different sequences and we multiply each one by some multipler $\alpha_{\small k}$, our recurrence relation will also have $k$ different parameters that we can use to completely modify the value of our sequence. Therefore, we can use this to make our sequence match the initial values of our recurrence sequence.

Now, that we have an approach, we can start finding small solutions that will fit into this recurrence equation.

<blockquote class="blockquote-theorem">
<hr>

If $a_n$ has the characteristic polynomial 

$$x^k - c_1x^{k-1} - c_2x^{k-2} - ... - c_{k-1}x - c_k$$

then $r^n$ is a solution to the recurrence equation if $r$ is a root of the characteristic polynomial.

</blockquote>

To prove this, we can plug $r$ into the characteristic polynomial and do a bit of rearranging:

$$
\begin{align*}
0 &= r^k - c_1r^{k-1} + c_2r^{k-2} + ... + c_k \\
r^k &= c_1r^{k-1} + c_2r^{k-2} + ... + c_k \\
r^k * r^{n-k} &= (c_1r^{k-1} + c_2r^{k-2} + ... + c_k) * r^{n-k} \\
r^n &= c_1r^{n-1} + c_2r^{n-2} + ... + c_kr^{n-k}
\end{align*}
$$

Since the last line matches the form of our recurrence relation, we can conclude that $r^n$ is a solution to our recurrence relation.

From here, we already have our solution for when the roots of our characteristic equation are distinct. Each distinct root $r_i$ will give us a distinct solution $r_i^n$ that we can then apply our above method to.

However, this doesn't work when the roots for our characteristic equation are not distinct, as we will then not get $k$ different sequences we can combine. However, when a root $r_i$ has a multiplicity $m_i > 1$, then we can construct another solution:

<blockquote class="blockquote-theorem">
<hr>

If $r$ is a solution to the characteristic polynomial of $a_n$ with a multiplicity of $m$, then $n^{i}r^n$ for any integer $i$ between $0$ and $m-1$ is a solution to the recurrence equation.

</blockquote>

Proving this is pretty complicated, so I'll omit it here. If you're interested int he full details, check out page 16 of [this document](https://www.eecs.yorku.ca/course_archive/2007-08/F/1019/A/recurrence.pdf) that also includes a ton of awesome in-depth information about solving recurrences.

Once we have this theorem, we can then see that for each root $r$ with multiplicity $m$, we get $m$ sequences out of it. Since the total sum of all multiplicities is equal to $k$, we obtain our $k$ sequences that we can then create a linear combination of to match our initial conditions. With that, we have created a systematic approach towards solving linear recurrences.

### Non-Homogenous Recurrences

With non-homogenous recurrences, the previous method does **not** apply because recurrences are not additive and the two forms we found also don't work. As a result, we have to do a bit more work to find an answer. The key is the following:

<blockquote class="blockquote-theorem">
<hr>

If $a_n$ be a linear non-homogenous recurrence relation. Write $a_n$ in the following form, where $b_n$ is a linear homogenous recurrence relation and $f(n)$ is a polynomial in terms of $n$.

$$a_n = b_n + f(n)$$

If we know any particular solution $a_n$ that satisfies the given non-homogenous recurrence relation and we know a solution $b_n$ that satisfies the homogenous recurrence relation, then

$$d_n = a_n + b_n$$

also satisfies the non-homogenous recurrence relation.

</blockquote>

To prove this, let us write out the definitions of our sequences and do a bit of rearranging:

$$
\begin{align*}
a_n &= c_1a_{n-1} + c_2a_{n-2} + ... + c_ka_{n-k} + f(n) \\
b_n &= c_1b_{n-1} + c_2b_{n-2} + ... + c_kb_{n-k} \\ \\
d_n &= a_n + b_n \\
&= c_1(a_{n-1} + b_{n-1}) + c_2(a_{n-2} + b_{n-2}) + ... + c_k(a_{n-k} + b_{n-k}) + f(n) \\
&= c_1d_{n-1} + c_2d_{n-2} + ... + c_kd_{n-k} + f(n)
\end{align*}
$$

Now that we have this tool, we can design an approach to solving this non-homogenous linear recurrence. We need to first design a single solution to the linear recurrence that will satisfy it. This must be done through guess and check and once we find it, it will not necessarily satisfy our initial conditions. However, we can use this as a building block and use the above theorem to add the homogenous solution to it. This homogenous solution will be fully customizable and allow our recurrence to pass through whichever $k$ values we want. As a result, we can use it to drive our non-homogenous solution towards our desired inputs.

Finding the specific non-homogenous solution is hard though. Fortunately, as mentioned before, just trying forms similar to $f(n)$ has been shown to work really well. In fact, there is a proof (which will be omitted here for brevity) that if $f(n)$ is a polynomial, then there will always be a polynomial that satisfies the recurrence relation of $a_n$.

## Conclusion

Solving linear recurrences can be very hard at times, but it can also be extremely powerful for solving some math problems. Not only can it greatly shorten calculations, but it can also put your answers into forms you may not have seen otherwise. For instance, if you have the closed form $a_n = 3^n - 2^n$, you can calculate your answer in a really nice way and see that it is the difference of two exponentials. If you bashed out the values of $a_n$ instead and got something like $a_{10} = 58025$, it would be really hard to see this connection.

## Sources

- [http://nms.lu.lv/wp-content/uploads/2016/04/21-linear-recurrences.pdf](http://nms.lu.lv/wp-content/uploads/2016/04/21-linear-recurrences.pdf)
- [http://www.cse.yorku.ca/course_archive/2007-08/F/1019/A/recurrence.pdf](http://www.cse.yorku.ca/course_archive/2007-08/F/1019/A/recurrence.pdf)
