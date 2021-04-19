---
title: Roots of Unity Filter Part 3 - Roots of Unity Filter
date: 2021-04-18 15:15:00 -0400
categories: [Math Articles, Roots of Unity Filter]
tags: [math, article, roots of unity filter, roots of unity]
math: true
---

## Note

This is a three part series I wrote back in 2019 on a technique applicable to certain competitive math problems: roots of unity filters. See the first two parts for a recap of complex numbers and roots of unity respectively. This post will actually go over the technique as well as what kind of problems it can be applied to.

<blockquote class="blockquote-warning">
<hr>
Many of the explanations for this section will not be rigorous proofs.
</blockquote>

## Guiding Problem

The main problem we are trying to tackle in this section is the following from one of Thomas Mildorf's mock AIMEs:

<blockquote class="blockquote-example">
<hr>
<i>Problem from Thomas Mildorf's Mock AIME 1: #11</i>

<br>

Let $S$ denote the value of the sum
$$\sum_{n = 0}^{668}(-1)^n{2004 \choose 3n}$$
Determine $S$
</blockquote>

We can tackle this problem in a variety of ways, but the approach we will be using here is a technique known as **roots of unity filter**.

## Description

Roots of unity filter is a technique that allows us to find the sum of every $k$th coefficient in a polynomial with any given offset less than $k$. For instance, if you had a polynomial with a degree of $20$, you could find the sum of the 2nd, 5th, 8th, ..., and 20th coefficients. This would correspond to every 3rd coefficient with an offset of $2$.

While on its own the roots of unity filter doesn't have a lot of applications, it is especially powerful when applied to the binomial theorem. For instance, with the guiding problem, we can expand the summation to find the following;

$${2004 \choose 0} - {2004 \choose 3} + {2004 \choose 6} - {2004 \choose 9} + ... + {2004 \choose 2004} = $$

$${2004 \choose 0} + {2004 \choose 6} + ... + {2004 \choose 2004} - \left({2004 \choose 3} + {2004 \choose 9} + ... + {2004 \choose 2001}\right)$$

We can see that this problem is asking us to calculate the sum of every 6th binomial coefficient with an offset of $0$ and then subtract the sum of every 6th binomial coefficient with an offset of $3$.

We can apply the roots of unity filter if we had a polynomial that had binomial coefficients as its coefficients. We can obtain this with the following polynomial:

$$(x + 1)^n = {n \choose 0} + {n \choose 1} + {n \choose 2} + ... + {n \choose n}$$

To solve our problem from above, we can utilize the root of unity filter on this polynomial with $n = 2004$ to determine the sum of every 6th coefficient with offset $0$ and the sum of every 6th coefficient with offset $3$. Then, we can subtract the latter from the former and obtain the answer.

## No Offset Version

The simplest method to apply roots of unity filter is when you're dealing with an offset of $0$ since you don't have to do much work. If you want to find the sum of every $n$th coefficient with an offset of $0$ for a polynomial $P(x)$, you can calculate it with the following expression, where $\omega$ represents the smallest $nth$ root of unity:

$$\dfrac{P(1) + P(\omega) + P(\omega^2) + ... + P(\omega^{n - 1})}{n}$$

Essentially, we just have to plug in the $n$th roots of unity, where $n$ is the desired cycle length, and then take the average of the results.

### Explanation

To see why this works, we can utilize the following two facts that we proved previously about roots of unity:

$$\omega^{n + i} = \omega^i$$

$$1 + \omega + \omega^2 + ... + \omega^{n - 1} = 0$$

Armed with this information, we can examine what happens when we plug the roots of unity into the polynomial $P(x)$. For this section, we're going to use a polynomial $P(x)$ with a degree of $10$ and calculate the sum of every third term. However, this can be generalized to any degree polynomial for any cycle length. First of all, let's write a polynomial $P(x)$ with a degree of $10$ as the following:

$$P(x) = a_0 + a_1x + a_2x^2 + a_3x^3 + ... + a_{10}x^{10}$$

When we plug in $\omega$ as our root of unity, we obtain the following:

$$P(\omega) = a_0 + a_1\omega + a_2\omega^2 + a_3\omega^3 + ... + a_{10}\omega^{10}$$

However, note that when the power of $\omega$ exceeds $3$, we can factor out $\omega^3 = 1$. This means that after the term $\omega^2$, the powers of $\omega$ will repeat in a cycle of length $3$. We can show this result with the other powers of $\omega$ we are plugging in as well. Whenever we pass $\omega^{3i}$ in our polynomial after passing in $\omega^i$ to the polynomial, we can factor out that $\omega^{3i} = 1$.

Since the terms of all of the polynomials are cyclic when plugging in the roots of unities, if we can show that summing all of the polynomials makes it so that only the coefficient of $a_0$ remain, it will necessarily apply to $a_3, a_6, ...$ as well. Therefore, we can direct our focus to what happens with the first $3$ terms of the polynomial when we pass in $1, \omega$, and $\omega^2$.

We can make the following chart to look at what happens:

| Root of Unity | $a_0$ | $a_1$        | $a_2$        |   |
|----------|---|----------|----------|---|
| $1$        | $1$ | $1$        | $1$        |   |
| $\omega$   | $1$ | $\omega$   | $\omega^2$ |   |
| $\omega^2$ | $1$ | $\omega^2$ | $\omega^4$ |   |
| **Total Sum** | **$3$** | **$0$** | **$0$** | |

The columns each correspond to what power we are raising each of the roots of unity, while the rows indicate each of the roots of unity. If we sum all of the columns, we will obtain how much of each coefficient we shall receive in the final sum.

Note that from the equation
$$1 + \omega + \omega^2 + ... + \omega^{n - 1} = 0$$
all of the columns except for the one corresponding to $a_0$ end up with a sum of $0$. In the third column, the equation is applied with just $\omega$ plugged in, and in the fourth column, the equation is applied with $\omega^2$ plugged in. Therefore, our result is just $a_0$ added $3$ times, so we can divide by $3$ to obtain our desired sum.

Again, remember that since the roots of unity are cyclic with a period of $3$, the same values and chart will apply for $a_3$ through $a_5$, $a_6$ through $a_8$, etc. To see this, looking at the entire chart is useful, which is placed below for your convenience.

|            | $a_0$ |      $a_1$ |      $a_2$ |          $a_3$ |                 $a_4$ |                    $a_5$ |             $a_6$ |                    $a_7$ |                    $a_8$ |             $a_9$ |                      $a_{10}$ |
|------------|------:|-----------:|-----------:|---------------:|----------------------:|-------------------------:|------------------:|-------------------------:|-------------------------:|------------------:|----------------------------:|
| $1$        |   $1$ |        $1$ |        $1$ |            $1$ |                   $1$ |                      $1$ |               $1$ |                      $1$ |                      $1$ |               $1$ |                         $1$ |
| $\omega$   |   $1$ |   $\omega$ | $\omega^2$ | $\omega^3 = 1$ |   $\omega^4 = \omega$ |    $\omega^5 = \omega^2$ |    $\omega^6 = 1$ |      $\omega^7 = \omega$ |    $\omega^8 = \omega^2$ |    $\omega^6 = 1$ |         $\omega^7 = \omega$ |
| $\omega^2$ |   $1$ | $\omega^2$ | $\omega^4$ | $\omega^6 = 1$ | $\omega^8 = \omega^2$ | $\omega^{10} = \omega^4$ | $\omega^{12} = 1$ | $\omega^{14} = \omega^2$ | $\omega^{16} = \omega^4$ | $\omega^{18} = 1$ | $\omega^{20} = \omega^{20}$ |
| **Total Sum** | **$3$** | **$0$** | **$0$** | **$3$** | **$0$** | **$0$** | **$3$** | **$0$** | **$0$** | **$3$** | **$0$** | |

<blockquote class="blockquote-example">
<hr>
Find $S = {10 \choose 0} + {10 \choose 4} + {10 \choose 8}$ without calculating any binary coefficients
</blockquote>

We can approach this problem by first realizing that we need to find the sum of every 4th coefficient in the polynomial:

$$(x + 1)^{10}$$

By applying the roots of unity filter, we can realize that this is equivalent to the following:

$$\omega = \text{cis}\left( \dfrac{2\pi}{4} \right)$$

$$\dfrac{(1 + 1)^{10} + (\omega + 1)^{10} + (\omega^2 + 1)^{10} + (\omega^4 + 1)^{10}}{4}$$

$$\dfrac{(2)^{10} + (1 + i)^{10} + (0)^{10} + (1 - i)^{10}}{4}$$

We can then find this sum by converting each of the complex numbers to polar form, applying de Moivre's theorem, and then converting back to rectangular coordinates. While this may seem lengthy for a problem we could have just calculated the binomial coefficients for, it is a general technique that has the same number of terms even as the upper number increases to huge numbers.

We continue the calculation below for the sake of completeness:

$$(1 + i)^{10} = \left(\sqrt{2}\text{cis}\left(\dfrac{\pi}{4}\right)\right)^{10} = 2^5\text{cis}\left(\dfrac{10\pi}{4}\right) = 2^5(0 + i) = 2^5i$$

$$(1 - i)^{10} = \left(\sqrt{2}\text{cis}\left(\dfrac{-\pi}{4}\right)\right)^{10} = 2^5\text{cis}\left(\dfrac{-10\pi}{4}\right) = 2^5(0 - i) = -2^5i$$

$$S = \dfrac{2^{10} + 2^5i + 0 - 2^5i}{4} = \boxed{2^8 = 256}$$

To check our answer, we can compute the binomial coefficients manually and get $1 + 210 + 45 = 256$.

<blockquote class="blockquote-note">
<hr>
A frequent math competition technique is to plug $1$ and $-1$ into a polynomial $P(x)$, add them together, and then divide by $2$ to cancel out all of the odd degree terms. This is actually the roots of unity filter being used with $n = 2$ since $1$ and $-1$ are the second roots of unity!
</blockquote>

## With Offset Version

While the previous version of roots of unity filter is already pretty powerful and can solve a lot of math problems, the more general version to find sums with offsets. Note that we still cannot solve our guiding problem because, in that problem, we have to be able to calculate the sum of the coefficients with a period pf $6$, but with an offset of $3$.

To get an idea of how this will work, we can once again look at the chart we created earlier that matches up what happens when we plug in each of the roots of unity for the terms in our polynomial.

| Root of Unity | $a_0$ | $a_1$        | $a_2$        |   |
|----------|---|----------|----------|---|
| $1$        | $1$ | $1$        | $1$        |   |
| $\omega$   | $1$ | $\omega$   | $\omega^2$ |   |
| $\omega^2$ | $1$ | $\omega^2$ | $\omega^4$ |   |
| **Total Sum** | **$3$** | **$0$** | **$0$** | |

Note that the main reason this worked out was that we had $1$ appear in every row for the term we wanted: $a_0$. That way, when we summed up the polynomial evaluated at each of the roots of unity, everything else would cancel out via the crucial identity 
$$1 + \omega + \omega^2 + ... + \omega^{n - 1} = 0$$ but the $1$s would not.

This time, say that the desired coefficient is $a_1$, meaning that we want an offset of $1$ instead of $0$. To do this, the key is to add some coefficient in front of each term in our sum to ensure that our sum has $1$s in the column for our desired term: $a_1$. Then, if we called those coefficients $b_i$, the sum of every 3rd term with an offset of 1 would look like this:
$$\dfrac{b_0P(1) + b_1P(\omega) + b_2(\omega^2)}{3}$$

To calculate these coefficients, we can use our table from above. Currently, it would look something like this, where all of our coefficients would be $1$, meaning that the values for each row are not being changed.

| Root of Unity | $b_i$ | $a_0$ | $a_1$        | $a_2$        |   |
|----------|---|---|----------|----------|---|
| $1$        | $1$ | $1$ | $1$        | $1$        |   |
| $\omega$   | $1$ | $1$ | $\omega$   | $\omega^2$ |   |
| $\omega^2$ | $1$ | $1$ | $\omega^2$ | $\omega^4$ |   |
| **Total Sum** | | **$3$** | **$0$** | **$0$** | |

However, by using the crucial property that $\omega^n = 1$, we can adjust the coefficients for each row so that the $1$s appear in the column for $a_1$ instead:

| Root of Unity | $b_i$ | $a_0$ | $a_1$        | $a_2$        |   |
|----------|---|---|----------|----------|---|
| $1$        | $1$ | $1$ | $1$        | $1$        |   |
| $\omega$   | $\omega^2$ | $\omega^2$ | $1$   | $\omega^4$ |   |
| $\omega^2$ | $\omega$ | $\omega$ | $1$ | $\omega^2$ |   |
| **Total Sum** | | **$0$** | **$3$** | **$0$** | |

With these coefficients carefully, each sum now conveniently produces the values for $a_1$!

<blockquote class="blockquote-note">
<hr>
I currently don't have a good explanation for why all of the other columns conveniently end up still canceling each other out no matter which column you choose to make the $1$s generate in. To show that they do cancel out to $0$ (they don't nicely use the equation shown before anymore), you have to do a bit of work, but it should work out. If anyone has any ideas, feel free to leave a comment on this post.
</blockquote>

With this, our equation to find the sum of every 3rd term with an offset of $1$ looks like the following:
$$\dfrac{P(1) + \omega^2 P(\omega) + \omega P(\omega^2)}{3}$$

## Solving the Guiding Problem

Armed with this knowledge, we can know solve our guiding problem. If you need a refresher, the problem boils down to the following:

$${2004 \choose 0} + {2004 \choose 6} + ... + {2004 \choose 2004} - \left({2004 \choose 3} + {2004 \choose 9} + ... + {2004 \choose 2001}\right)$$

To do this, we need to find the sum of every 6th coefficient with an offset of 0 and the sum of every 6th coefficient with an offset of 3 for the polynomial

$$P(x) = (x + 1)^{2004}$$

We will call the first sum $S_1$ and the second sum $S_2$. We can apply the no offset roots of unity filter to calculate $S_1$:

$$\omega = \text{cis}\left(\dfrac{2\pi}{6}\right) = \text{cis}\left(\dfrac{\pi}{3}\right)$$

$$S_1 = \dfrac{P(1) + P(\omega) + P(\omega^2) + P(\omega^3) + P(\omega^4) + P(\omega^5)}{6}$$

While we could plug this in and solve for $S_1$ directly, it would be incredibly difficult. However, we can proceed with calculating $S_2$ to see if we get any nice cancellations. We can apply our offsetted roots of unity filter to calculate $S_2$. To do so, we first need to find what our coefficients will be to get our column of $1$s to shift to $a_3$, which will give us the offset of $3$ that we need.

| Root of Unity | $b_i$      | Original $a_3$ | Modified $a_3$ |
|---------------|------------|----------------|----------------|
| $1$           | $1$        | $1$            | $1$            |
| $\omega$      | $\omega^3$ | $\omega^3$     | $1$            |
| $\omega^2$    | $1$        | $\omega^6$     | $1$            |
| $\omega^3$    | $\omega^3$ | $\omega^9$     | $1$            |
| $\omega^4$    | $1$        | $\omega^{12}$  | $1$            |
| $\omega^5$    | $\omega^3$ | $\omega^{15}$  | $1$            |

Note that the way we choose the coefficients $b_i$ is that we want the coefficient of $\omega$ to increase so it becomes a multiple of $n = 6$ and the coefficient evaluates to $1$.

Then, we can calculate $S_2$ as:

$$\omega^3 = \text{cis}(\pi) = -1$$

$$S_2 = \dfrac{P(1) - P(\omega) + P(\omega^2) - P(\omega^3) + P(\omega^4) - P(\omega^5)}{6}$$

When we combine this with to get our total answer of $S_1 - S_2$, we obtain the following:

$$S_1 - S_2 = \dfrac{\cancel{P(1)} + P(\omega) + \cancel{P(\omega^2)} + P(\omega^3) + \cancel{P(\omega^4)} + P(\omega^5) - \cancel{P(1)} + P(\omega) - \cancel{P(\omega^2)} + P(\omega^3) - \cancel{P(\omega^4)} + P(\omega^5)}{6}$$

$$S_1 - S_2 = \dfrac{P(\omega) + P(\omega^3) + P(\omega^5)}{3}$$

Now that our sum is greatly simplified, we can plug in $P(x) = (x + 1)^{2004}$ and see what we can cancel out. The first thing we can notice is that $\omega^3 = -1$ as derived above, so our middle term cancels out to $(1 - 1)^{2004} = 0$, so we can ignore that. The next thing we can do is calculate what $\omega$ is in rectangular form so that we can add the $1$ to it as part of $P(x)$.

$$\omega = \text{cis}\left(\dfrac{\pi}{3}\right) = \cos\left(\dfrac{\pi}{3}\right) + i\sin\left(\dfrac{\pi}{3}\right) =
\dfrac{1}{2} + \dfrac{\sqrt{3}}{2}i$$

$$P(\omega) = \left(1 + \dfrac{1}{2} + \dfrac{\sqrt{3}}{2}i\right)^{2004} = \left(\dfrac{3}{2} + \dfrac{\sqrt{3}}{2}i\right)^{2004}$$

To calculate this, we can use de Moivre's theorem after converting $\dfrac{3}{2} + \dfrac{\sqrt{3}}{2}i$ to polar form.

$$\left|\dfrac{3}{2} + \dfrac{\sqrt{3}}{2}i\right| = \sqrt{\left(\dfrac{3}{2}\right)^2 + \left(\dfrac{\sqrt{3}}{2}\right)^2} = \sqrt{3}$$

$$\text{arg}\left(\dfrac{3}{2} + \dfrac{\sqrt{3}}{2}i\right) = \text{atan}\left(\dfrac{\sqrt{3}}{3}\right) = \dfrac{\pi}{6}$$

$$P(\omega) = \left(\dfrac{3}{2} + \dfrac{\sqrt{3}}{2}i\right)^{2004} = \left(\sqrt{3}\text{cis}\left(\dfrac{\pi}{6}\right)\right)^{2004} = 3^{1002}\text{cis}(334\pi) = 3^{1002}$$

We can do this with $\omega^5$ as well.

$$\omega^5 = \text{cis}\left(\dfrac{5\pi}{3}\right) = \cos\left(\dfrac{5\pi}{3}\right) + i\sin\left(\dfrac{5\pi}{3}\right) =
\dfrac{1}{2} - \dfrac{\sqrt{3}}{2}i$$

$$P(\omega^5) = \left(1 + \dfrac{1}{2} - \dfrac{\sqrt{3}}{2}i\right)^{2004} = \left(\dfrac{3}{2} - \dfrac{\sqrt{3}}{2}i\right)^{2004}$$

$$\left|\dfrac{3}{2} - \dfrac{\sqrt{3}}{2}i\right| = \sqrt{\left(\dfrac{3}{2}\right)^2 + \left(\dfrac{\sqrt{3}}{2}\right)^2} = \sqrt{3}$$

$$\text{arg}\left(\dfrac{3}{2} - \dfrac{\sqrt{3}}{2}i\right) = \text{atan}\left(\dfrac{\sqrt{3}}{-3}\right) = \dfrac{-\pi}{6}$$

$$P(\omega^5) = \left(\dfrac{3}{2} - \dfrac{\sqrt{3}}{2}i\right)^{2004} = \left(\sqrt{3}\text{cis}\left(\dfrac{-\pi}{6}\right)\right)^{2004} = 3^{1002}\text{cis}(-334\pi) = 3^{1002}$$

Therefore, our final sum evaluates to:

$$S_1 - S_2 = \dfrac{P(\omega) + P(\omega^3) + P(\omega^5)}{3} = \dfrac{3^{1002} + 0 + 3^{1002}}{3} = \boxed{2 * 3^{1001}}$$

<blockquote class="blockquote-note">
<hr>
The original problem was part of a mock AIME and asked for the answer mod $1000$. Since this post is about roots of unity filter, we won't cover that part in depth, but to calculate the value mod $1000$, you could apply the Euler's Totient Theorem with $\phi(1000) = 40$ to find that $3^{1001} \equiv 3 \text{ } (\text{mod } 1000)$. Then, the answer is $(2 * 3) \text{ mod 1000} = \boxed{006}$.
</blockquote>

## Final Notes

Roots of unity filter is a super useful technique on some problems, but it can involve a lot of calculations and is not applicable to everything. For our guiding problem, we were fortunate enough to have all of our complex roots of unities dissipate nicely, which is something that you will frequently see for math competition problems that use roots of unity filter. Generally, most problems will use the 4th roots of unity, which makes it incredibly convenient since all of the roots of unities are either entirely imaginary or entirely real. For less convenient problems, a calculator or some other clever insight may be necessary to evaluate the result.
