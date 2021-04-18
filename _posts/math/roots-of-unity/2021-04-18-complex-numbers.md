---
title: Roots of Unity Filter Part 1 - Complex Numbers
date: 2021-04-18 14:00:00 -0400
categories: [Math, Roots of Unity Filter]
tags: [math, article, roots of unity filter, roots of unity, complex numbers]
math: true
---

## Note

This is a three part series I wrote back in 2019 on a technique applicable to certain competitive math problems: roots of unity filters. The first two parts are just a recap of complex numbers and roots of unity respectively. If you're already comfortable with both of these topics, feel free to skip to Part 3.

## Overview

<blockquote class="blockquote-definition">
<hr>
A <b>complex number</b> is a number $z$ that can be expressed in the form $z = a + bi$, where $a$ and $b$ are real numbers, and $i = \sqrt{-1}$.
<br><br>
$a$ and $b$ are known as the real and imaginary components of $z$ respectively.
</blockquote>

All complex numbers can be graphed on the coordinate plane, where the x-axis represents the real component of the complex number, while the y-axis represents the imaginary component of the complex number.

For instance, the complex number $1 + 2i$ can be graphed as shown below:

![(1, 2) on Coordinate Plane](/assets/img/roots-of-unity/complex-number.png){: width="400"}

The method of representing a complex number as $z = a + bi$ is known as **rectangular form** since we use a rectangular coordinate system. When we graph a complex number $z$, we can derive actually derive a different way of representing that complex number: **polar form**.

To express a complex number in polar form, we use the angle $\theta$ it makes with the positive x-axis and the positive distance $r$ from the origin.
If we have a complex number $z = a + bi$, then we can derive these two parameters with a bit of trigonometry. The angle $\theta$ is known as the argument of $z$, or $\text{arg}(z)$. The distance $r$ is known as the magnitude of $z$, or $\lvert z \rvert$.

<blockquote class="blockquote-theorem">
<hr>
For a complex number $z = a + bi$, the angle $\theta$ that $z$ makes with the positive x-axis can be expressed as:
$$ \theta = \text{arg}(z) = \text{atan}\left( \dfrac{b}{a} \right) $$
The magnitude $r$ can be expressed as:
$$ r = |z| = \sqrt{a^2 + b^2} $$
</blockquote>

However, we can also go from polar form back to rectangular form with the following relationship:

<blockquote class="blockquote-theorem">
<hr>
For a complex number $z$ with argument $\theta$ and magnitude $r$ can be expressed in rectangular form $z = a + bi$ with:
$$a = r \cos(\theta)$$
$$b = r \sin(\theta)$$
This implies that $z$ can be expressed in the following manner, which i sknown as the **polar form** of $z$.
$$ z = a + bi = r(\cos(\theta) + i \sin(\theta)) = r \text{cis}(\theta)$$

We use $\text{cis}(\theta)$ as a shorthand for writing $\cos(\theta) + i \sin(\theta)$
</blockquote>

There is one final form of a complex number, the **complex exponential form**. The proof for this relationship is beyond the scope of this document, but there are *plenty* of excellent tutorials by people like 3Blue1Brown who have covered this topic in detail.

<blockquote class="blockquote-theorem">
<hr>
For a complex number $z$ with argument $\theta$ and magnitude $r$ can be expressed as:
$$z = re^{i \theta}$$
</blockquote>

## de Moivre's Theorem

One super important theorem about complex numbers and their exponents is **de Moivre's Theorem**.

<blockquote class="blockquote-theorem">
<hr>
$$z = r\text{cis}(\theta)$$
$$z^n = r^n\text{cis}(n\theta)$$
</blockquote>

This theorem can be proven by considering the complex exponential form of $z$.

$$z = r\text{cis}(\theta)=re^{i\theta}$$

$$z^n = r^n(e^{i\theta})^n = r^ne^{in\theta}$$

$$z^n = r^n\text{cis}(n\theta)$$

## Arithmetic Operations

Complex numbers, much like real numbers, can be added, subtracted, and multiplied. The rules for applying these arithmetic operations to complex numbers are the same as what one would expect as long as it is remembered that $i^2 = -1$ when doing multiplication.

<blockquote class="blockquote-example">
<hr>
$$(1 + 2i) + (3 + 4i) = 4 + 6i$$
$$(1 + 2i) - (3 + 4i) = -2 - 2i$$
$$(1 + 2i) * (3 + 4i) = (3 - 8) + (6 + 4)i = -5 + 10i$$
</blockquote>

### Multiplication

When multiplying complex numbers, we obtain an interesting property regarding the magnitude and angle of the resulting product.

<blockquote class="blockquote-theorem">
<hr>
When $z$ and $w$ are two complex numbers, we can obtain the following information about their product $z * w$:
$$|z * w| = |z| * |w|$$
$$\text{arg}(z * w) = \text{arg}(z) + \text{arg}(w)$$
</blockquote>

We can prove this pretty easily once again with the complex exponential form:

$$z = r_ze^{i\theta_z}, w = r_we^{i\theta_w}$$

$$|z| = r_z, |w| = r_w$$

$$\text{arg}(z) = \theta_z, \text{arg}(w) = \theta_w$$

$$z * w = r_ze^{i\theta_z} * r_we^{i\theta_w} = r_zr_we^{i(\theta_z+\theta_w)}$$

$$|z * w| = r_z * r_w = |z| * |w|$$

$$\text{arg}(z * w) = \theta_z + \theta_w = \text{arg}(z) + \text{arg}(w)$$


With this theorem, we can make multiplying numbers in polar form very easy, since all we have to do is multiply the magnitudes and add the arguments.

<blockquote class="blockquote-example">
<hr>
$$3\text{cis}\left(\frac{\pi}{4}\right) * 4\text{cis}\left(\frac{3\pi}{4}\right) = 12 \text{cis}(\pi) = -12$$
</blockquote>

Note that applying this principle to exponentiation is what led us to de Moivre's theorem earlier.

### Division

Division of complex numbers is a bit more interesting, and there are two ways to approach it. The first involves complex conjugates to make the denominator real, similar to how one would rationalize a denominator with radicals in it. We will go over conjugates in-depth soon.

<blockquote class="blockquote-example">
<hr>
$$\dfrac{1 + 2i}{3 + 4i} = \dfrac{1 + 2i}{3 + 4i} * \dfrac{3 - 4i}{3 - 4i} = \dfrac{11 + 10i}{3^2 + 4^2} = \dfrac{11 + 10i}{25} $$
</blockquote>

The other method is to use de Moivre's theorem above with regards to the argument and the magnitude. If we have two complex numbers $z$ and $w$ and we want to perform $\frac{z}{w}$, we can write it as $z * w^{-1}$.

We can then see from de Moivre's theorem that $w^{-1}$ will be the same as $w$ but it will have a magnitude of $\frac{1}{\lvert w \rvert}$ and an argument of $-\text{arg}(w)$. Then, we just need to multiply the two numbers with the same process as above.

As a result, you can think of division as dividing the magnitudes and subtracting the arguments.

<blockquote class="blockquote-example">
<hr>
$$8\text{cis}\left(\frac{3\pi}{4}\right) \div 4\text{cis}\left(\frac{\pi}{2}\right) = 2\text{cis}\left(\frac{\pi}{4}\right)$$
</blockquote>

## Conjugates

<blockquote class="blockquote-definition">
<hr>
The conjugate of a complex number $z = a + bi$ is denoted as $\bar{z} = a - bi$
</blockquote>

There are a few important theorems that you can use with complex conjugates.

<blockquote class="blockquote-theorem">
<hr>
$$z * \bar{z} = |z|^2$$
</blockquote>

We can prove this pretty easily by considering the rectangular form of $z = a + bi$.

$$z * \bar{z} = (a + bi) * (a - bi) = a^2 + b^2 = \sqrt{a^2 + b^2}^2 = |z|^2$$

<blockquote class="blockquote-theorem">
<hr>
$$\overline{r\text{cis}(\theta)} = r\text{cis}(-\theta)$$
</blockquote>

We can also prove this by realizing that the complex conjugate just reflects the complex coordinate over the x-axis, which in turn just multiplies the angle by $-1$.

<blockquote class="blockquote-theorem">
<hr>
The complex conjugate operator is distributive.
$$\overline{z + w} = \bar{z} + \bar{w}$$
$$\overline{z - w} = \bar{z} - \bar{w}$$
$$\overline{z * w} = \bar{z} * \bar{w}$$
$$\overline{\dfrac{z}{w}} = \dfrac{\bar{z}}{\bar{w}}$$
$$\overline{z^a} = \bar{z}^a$$
</blockquote>

We can prove all of these pretty easily with rectangular coordinates, so they are omitted.

<blockquote class="blockquote-theorem">
<hr>
If a complex number $z$ is a root of a polynomial with real coefficients, then $\bar{z}$ is also a root of that polynomial.
</blockquote>

We can prove this by applying the operations above while also making use of the fact that the conjugate of a real number $a$ is equal to $a$.

$$P(x) = a_nx^n + a_{n-1}x^{n-1} + ... + a_1x + a_0 = \sum_{i = 0}^{n}a_ix^i$$

$$P(z) = \sum_{i = 0}^{n}a_iz^i = 0$$

$$P(\bar{z}) = \sum_{i = 0}^{n}a_i\bar{z}^i = \sum_{i = 0}^{n}a_i\overline{z^i} = \sum_{i = 0}^{n}\bar{a_i}\overline{z^i} = \sum_{i = 0}^{n}\overline{a_iz^i} = \overline{\sum_{i = 0}^{n}a_iz^i}$$

$$P(\bar{z}) = \bar{0} = 0$$

## Side Note

With complex exponentials, you can actually derive the formulas for sine and cosine addition. Additionally, you can derive the formulas for the sine and cosine of large multiples of angles with de Moivre's theorem. Look forward to another post that will go over this in depth!
