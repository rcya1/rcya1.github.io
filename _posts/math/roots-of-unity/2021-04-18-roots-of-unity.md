---
title: Roots of Unity Filter Part 2 - Roots of Unity
date: 2021-04-18 15:00:00 -0400
categories: [Math, Roots of Unity Filter]
tags: [math, article, roots of unity filter, roots of unity]
math: true
---

## Note

This is a three part series I wrote back in 2019 on a technique applicable to certain competitive math problems: roots of unity filters. The first two parts are just a recap of complex numbers and roots of unity respectively. If you're already comfortable with both of these topics, feel free to skip to Part 3.

## Basics

<blockquote class="blockquote-definition">
<hr>
The $n$th roots of unity for a positive integer $n$ are all of the complex numbers $z$ that satisfy the following equation:
$$z^n = 1$$
</blockquote>

One thing to note from this equation is that there are $n$ $n$th roots of unity since the roots of unity could be interpreted as the $n$ roots to the polynomial
$$z^n - 1$$

In this document, we will denote the "smallest" $n$th root of unity as the $n$th root of unity with the smallest positive angle $\theta$ when graphed on the complex coordinate plane. Note that this means although $1$ is always an $n$th root of unity, it is not considered in this document as the "smallest" $n$th root of unity.

<blockquote class="blockquote-theorem">
<hr>
If $\omega$ is the smallest $n$th root of unity, then all of the powers of $\omega$ are also roots of unity.
$$\omega^1, \omega^2, ..., \omega^{n}$$
</blockquote>

This can be proven as follows:
$$z^n = 1$$
$$\omega^n = 1$$
$$(\omega^i)^n = (\omega^n)^i = 1^i = 1$$

In fact, all of the $n$th roots of unity can be written as the first $n$ powers of the smallest $n$th root of unity.

Note that with this method, we do not obtain more than $n$ roots of unity because if we raise $\omega$ to the $n + 1$th power, we can factor out a term of $w^n = 1$ to obtain the root of unity $w$ again. This shows that the $n$th roots of unity are cyclicnature, which is a really powerful application of them especially towards things like roots of unity filter, which we will cover next.

## Polynomial Interpretation

As we stated before, we can consider the $n$th roots of unity as the roots of the polynomial
$$x^n - 1$$

However, we can also write a polynomial in terms of its factors, which means that we can write the polynomial $x^n - 1$ as the following:
$$x^n - 1 = (x - \omega)(x - \omega^2)...(x - \omega^n) = (x - 1)(x - \omega)...(x - \omega^{n - 1})$$

This interpretation can be pretty useful in a few problems, as we will see in an example later.

A more important aspect of this interpretation is the following result. Note that we can actually factor the equation $x^n - 1 = 0$ as $(x - 1)(1 + x + x^2 + ... + x^{n - 1}) = 0$. Try multiplying out the factorization to see why. If we divide both sides by $x - 1$ we obtain the following theorem:

<blockquote class="blockquote-theorem">
<hr>
For any $n$th root of unity $w \neq 1$, the following equation is true:
$$1 + \omega + \omega^2 + ... + \omega^{n - 1} = 0$$
</blockquote>

Note that for this theorem, $\omega$ does **not** have to be the smallest $n$th root of unity.

## Calculating Roots of Unity

We can calculate roots of unity using de Moivre's Theorem. Consider the equation
$$x^n = 1$$

We can rewrite $1$ in its polar form as $\text{cis}(2\pi k)$, where $k$ is any integer. Then, by applying de Moivre's Theorem with the exponent $-n$, we obtain the following:
$$x = \text{cis}\left(\dfrac{2\pi k}{n}\right)$$

Note that a negative exponent with de Moivre's Theorem corresponds to dividing the angle by $n$, not multiplying it by $-n$.

By ranging $k$ in the interval $[0, n - 1]$, all $n$ roots of unity can be obtained. By setting $k = 1$, we can show that the smallest $n$th root of unity is:
$$\omega = \text{cis}\left(\dfrac{2\pi}{n}\right)$$

<blockquote class="blockquote-example">
<hr>
The 5th roots of unity are as follows:
$$\omega^5 = 1$$
$$\omega = \text{cis}\left(\dfrac{2\pi k}{5}\right)$$
$$\omega = 1, \text{cis}\left(\dfrac{2\pi}{5}\right), \text{cis}\left(\dfrac{4\pi}{5}\right), \text{cis}\left(\dfrac{6\pi}{5}\right), \text{cis}\left(\dfrac{8\pi}{5}\right)$$
</blockquote>

<blockquote class="blockquote-example">
<hr>
The 4th roots of unity are as follows:
$$\omega^4 = 1$$
$$\omega = \text{cis}\left(\dfrac{2\pi k}{4}\right)$$
$$\omega = 1, \text{cis}\left(\dfrac{2\pi}{4}\right), \text{cis}\left(\dfrac{4\pi}{4}\right), \text{cis}\left(\dfrac{6\pi}{4}\right)$$
$$\omega = 1, i, -1, -i$$
</blockquote>

## Graphing Roots of Unity

A quite interesting property emerges once we graph the nth roots of unity. To demonstrate this, we shall graph the 5th roots of unity below.

![5th Roots of Unity](/assets/img/roots-of-unity/5th.jpg){: width="300"}

As seen above, the 5th roots of unity produce a set of points evenly spaced around the complex plane. In fact, they form a regular pentagon. This is true for any $n$th roots of unity.

<blockquote class="blockquote-theorem">
<hr>
The $n$th roots of unity will produce a regular $n$-gon when graphed in the complex plane.
</blockquote>

This can be seen when we look at the $\text{cis}$ form of the roots of unity, as all of our points are evenly spaced around the unit circle.

This visualization can help give some visual intuition towards
$$1 + \omega + \omega^2 + ... + \omega^{n-1}$$

The nth roots of unity are all evenly spaced around the point $(0, 0)$, making their average the point $(0, 0)$. As a result, the sum of their real components must be $0$ and the sum of their imaginary components must be $0$. As a result, their total sum must be $0$.

This visualization also helps with showing why the roots of unity are cyclic intuitively, as once you multiply the angle of a root of unity $n$ times to obtain more roots of unity, you will come back around the unit circle and start again.

## Example Problems

<blockquote class="blockquote-example">
<hr>
<i>Problem from Brilliant.org by Andy Hayes </i>

<br>

Consider the equation 
$$x^7 + x^6 + x^5 + ... + x + 1 = 0$$
Let $x_k$ be the $k$th distinct root of the equation, and let $\Re(x_k)$ be the real part of the root. Find
$$\sum_{k=1}^7[\Re(x_k)^2]$$
</blockquote>

There are three primary ways to approach this problem:

- The given equation may remind you of the result we derived earlier, which states that the given equation is valid for all of the $8$th roots of unity besides 1. As a result, we can immediately apply our knowledge about roots of unity and solve the problem.

<hr>

- However, if you do not see the above connection immediately, there are a few other ways to see the above. First, you could realize that the sum given is a geometric series, which means that it can be rewritten in the form
    $$\dfrac{x^8 - 1}{x - 1} = 0$$
    From this, it is clear that the numerator will be equal to $0$ for each of the $8$th roots of unity, while the denominator eliminates $1$ as a solution.

<hr>

- Another way to see the above is to multiply the entire given equation by $x$.
    $$x(x^7 + x^6 + x^5 + ... + x + 1) = x^8 + x^7 + x^6 + ... + x^2 + x$$

    We can then subtract the original equation from this equation to obtain:
    $$x^8 - 1 = 0$$

    We can see that all of the $8$th roots of unity are solutions, although $1$ is an extraneous solution we obtained after multiplying everything by $x$. We can be sure there is an extraneous solution since there are 8 8th roots of unity, but the original polynomial only has degree 7.

<hr>

Once we find this, we can easily calculate the 8th roots of unity because each of them will correspond to angles in increments of $\dfrac{\pi}{4}$.

![8th Roots of Unity](/assets/img/roots-of-unity/8th.jpg){: width="400"}

By computing the cosine (which produces the real component of the roots of unity) of all of these angles and including $\theta = 0$, we obtain the answer:

$$\cos\left(\dfrac{\pi}{4}\right)^2 + \cos\left(\dfrac{\pi}{2}\right)^2 + \cos\left(\dfrac{3\pi}{4}\right)^2 + \cos(\pi)^2 + $$

$$\cos\left(\dfrac{5\pi}{4}\right)^2 + \cos\left(\dfrac{3\pi}{2}\right)^2 + \cos\left(\dfrac{7\pi}{4}\right)^2 = \boxed{3}$$

<blockquote class="blockquote-example">
<hr>
<i>Problem from Thomas Mildorf's Mock AIME 1: #10</i>

<br>

$ABCDEF$ is a regular heptagon inscribed in a unit circle centered at $O$. $l$ is the line tangent to the circumcircle of $ABCDEFG$ at $A$, and $P$ is a point on $l$ such that $\triangle AOP$ is isosceles. Let $p$ denote the value of $AP * BP * CP * DP * EP * FP * GP$. Determine the value of $p^2$.
</blockquote>

At first glance, this problem may not seem related to roots of unity. However, it can be solved really nicely with roots of unity.

The first hint that roots of unity can be applied is the fact that there is a regular heptagon inscribed in a unit circle. Heptagons are nasty in geometry, as they have fractional angle measures. Secondly, the 7th roots of unity are perfect for expressing 7 points equally spaced around the unit circle, which is what this heptagon $ABCDEF$ is.

As a result, we can graph the 7 roots of unity as $ABCDEF$ as shown below.

![ABCDEF](/assets/img/roots-of-unity/ABCDEF.png){: width="300"}

Note that we aligned $A$ with the x-axis (making it equal to 1) to make the next step simpler. We then have to draw the line $l$ such that $l$ is tangent to the heptagon. Since we alined $A$ with the x-axis, the line $l$ is simply a vertical line.

![ABCDEF with line l](/assets/img/roots-of-unity/ABCDEF-Line.png){: width="300"}

We can then draw the point $P$ such that $\triangle AOP$ is isosceles. Note that since the roots of unity are centered around the origin, the center $O$ of our heptagon will be the origin. Since $P$ is going to have to lie on $l$ and $l$ is vertical, the angle $OAP$ is going to be a right angle. Therefore, the triangle must have that $\overline{OA} \cong \overline{AP}$. If the triangle had any other two sides equal, then the angles would be impossible. You can try drawing it and seeing for yourself.

Note that $OA = 1$ since $A$ is on the unit circle, so $AP = OA = 1$. We will arbitrarily choose $P$ to be $1$ unit above the x-axis. The answer will be the same regardless of whether $P$ is above or below the x-axis due to symmetry.

![ABCDEF with line l and point P](/assets/img/roots-of-unity/ABCDEF-Line-P.png){: width="300"}

Now that the diagram is set up, we can proceed with calculating the given product, with is the square of the product of all of the distances from $P$ to all of the points on in $ABCDEF$.

To calculate the distance between two complex numbers, we need to do a bit of thinking. To find the distance between two complex numbers in the complex plane, we can first find the complex number that represents the difference between the two. Then, we can just find the magnitude of this complex number. For instance, the distance between complex numbers $z = 1 + 2i$ and $w = 3 + 4i$ would be:

$$|w - z| = |2 + 2i| = \sqrt{2^2 + 2^2} = 2\sqrt{2}$$

Now that we have this out of the way, we can go back to the problem. We can label all of the points of our hexagon as the roots of unity $1, \omega, \omega^2, \omega^3, ..., \omega^6$.

![ABCDEF with point P and Distances](/assets/img/roots-of-unity/ABCDEF-Line-P-Dist.png){: width="300"}

We can also label our point $P$ as the complex number $P = 1 + i$. To find the product of the distances from $P$ to each of the points, we can do the following:
$$p = |P - 1| * |P - \omega| * |P - \omega^2| * ... * |P - \omega^6|$$

By using the properties of multiplied complex numbers, we can show that this is equal to the following:

$$p = |(P - 1)(P - \omega)(P - \omega^2)...(P - \omega^6)|$$

You may realize that this looks similar to what we discussed earlier with an alternative form of the polynomial $x^n - 1$, but with $P$ plugged in for $x$.

$$x^7 - 1 = (x - 1)(x - \omega)(x - \omega^2)...(x - \omega^6)$$

Therefore, we can rewrite $p$ as the following:

$$p = |P^7 - 1|$$

We know what $P$ is, so now we can just plug in the numbers! However, rather than calculating $P^7$ by hand, we can take a shortcut with de Moivre's theorem.

We can calculate $\lvert P \rvert = \sqrt{1^2 + 1^2} = \sqrt{2}$ and $\text{arg}(P) = \text{atan}(1/1) = \dfrac{\pi}{4}$. Therefore, we can write $P$ in polar form as $P = \sqrt{2}\text{cis}\left(\dfrac{\pi}{4}\right)$. We can then calculate $P^7$ easily using de Moivre's as:

$$P^7 = 2^{7/2}\text{cis}\left(\dfrac{7\pi}{4}\right) = 8\sqrt{2}\left(\dfrac{\sqrt{2}}{2} - i\dfrac{\sqrt{2}}{2}\right) = 8 - 8i$$

We can then finish the problem:

$$p = |P^7 - 1| = |7 - 8i| = \sqrt{7^2 + 8^2} = \sqrt{113}$$

$$p^2 = \boxed{113}$$
