---
title: Modular Inverses
date: 2021-04-19 11:15:00 -0400
categories: [Math]
tags: [Math, Guide, Modular Arithmetic]
math: true
toc: true
toc_sticky: true
excerpt: For modular arithmetic, the operations of addition, subtraction, and multiplication are pretty easy to define and understand. You simply perform the operation and then perform the modulo operator on the output. However, this doesn't apply to division, since division frequently leads to fractions/decimals, which is not what we are looking for when considering remainders.
---

<blockquote class="blockquote-note">
<hr>
This post assumes a basic knowledge of modular arithmetic and the notation for it. In this article, we will use the following notation to denote $b$ as the remainder when $a$ is divided by $n$.

$$a \equiv b \pmod{n} $$

We will also less frequently use the notation $a\ \%\ n = c$ to denote the same thing.

</blockquote>

## Division in Modular Arithmetic

For modular arithmetic, the operations of addition, subtraction, and multiplication are pretty easy to define and understand. You simply perform the operation and then perform the modulo operator on the output.

$$3 + 4 \equiv 7 \equiv 0 \pmod{7}$$

$$3 - 4 \equiv -1 \equiv 6 \pmod{7}$$

$$3 * 4 \equiv 12 \equiv 5 \pmod{7}$$

However, this doesn't apply to division, since division frequently leads to fractions/decimals, which is not what we are looking for when considering remainders. However, what if we want to solve this problem:

$$3x \equiv 4 \pmod{7}$$

In typical arithmetic, we would divide both sides by $3$ to solve for $x$, but that doesn't work here since $\dfrac{3}{4}$ doesn't make sense as a remainder for $x$ after division if we assume that $x$ must be a whole number.

Divison is a pretty weird thing in modular arithmetic, although it can be applied in some cases. We actually can do division in modular arithmetic with respect to $n$ to solve the equation under a few conditions:

1. Both sides of the equation are divisible by the divisor.
2. The divisor is coprime with $n$.

|                         | Condition (1) Met                           | Condition (1) Not Met          |
|-------------------------|-----------------------------------------------|----------------------------------|
| Condition (2) Met     | You can divide safely                         | You have to use modular inverses |
| Condition (2) Not Met | You have to divide everything by $\gcd(a, n)$ | The equation has no solutions    |

Here are examples of equations that would belong in each box:

|                         | Condition (1) Met       | Condition (1) Not Met   |
|-------------------------|---------------------------|---------------------------|
| Condition (2) Met     | $3x \equiv 6 \pmod{7}$    | $3x \equiv 4 \pmod{7}$    |
| Condition (2) Not Met | $6x \equiv 12 \pmod{15}$  | $3x \equiv 4 \pmod{6}$    |


For instance, the given bottom right equation has no integer solutions. For the upper right equation, we can divide both sides by 3 to solve:

$$x \equiv 2 \pmod{7}$$

We will primarily go over the upper right condition in this article. At the end, we will briefly discuss the lower left condition. The other two conditions are easily solved.

## Modular Inverse Basics

<blockquote class="blockquote-definition">
<hr>
The modular inverse of a number $a$ is defined as $a^{-1}$ such that
$$a * a^{-1} \equiv 1 \pmod{n}$$
</blockquote>

If we knew the modular inverse of $3$ with respect to $7$, we could multiply that on both sides of our equation to cancel out the $3$ and obtain our whole number answer.

There are many ways we can find modular inverses of a number, and the most simple of these is to simply try every possible number from $0$ to $n - 1$. For instance, we could calculate $3 * x \pmod{7}$ for all values $x$ from $0$ to $6$.

In this case, we can relatively quickly find that the modular inverse of $3$ is $5$ since $3 * 5 = 15$, which is $1$ above a multiple of $7$. Therefore, we can solve our equation as follows:

$$3x * 5 \equiv 4 * 5 \pmod{7} \rightarrow x \equiv 6 \pmod{7}$$

Therefore, we can conclude that all numbers that leave a remainder of $6$ when divided by $7$ satisfy the original equation.

However, not all numbers have a modular inverse. For instance, $2$ does not have a modular inverse with respect to $4$. You can try it out and you will quickly see that there are no values $x$ such that $2x \equiv 1 \pmod{4}$.

<blockquote class="blockquote-theorem">
<hr>
The modular inverse of $a$ with respect to $n$ only exists if $a$ and $n$ share no common factors besides $1$ or, more formally, $\gcd(a, n) = 1$.
</blockquote>

We can prove this by first assuming that there exists a number $a$ and its modular inverse $a^{-1}$ with respect to $n$ such that $\gcd(a, n) \neq 1$. Then, we can write the following equation:

$$a * a^{-1} \equiv 1 \pmod{n}$$

This is equivalent to writing the following equation for some integer $k$:

$$a * a^{-1} = kn + 1$$

We can rearrange this to obtain the following:

$$a * a^{-1} - kn = 1$$

However, note that we previously assumed that $\gcd(a, n) \neq 1$, but that implies that the left hand side of the above equation has the common factor $\gcd(a, n) \neq 1$. However, the only integer factors of the right hand side are $1$, making this statement impossible. Therefore, we have reached a contradiction and we can conclude that there exists no modular inverse of a number $a$ if $\gcd(a, n) \neq 1$.

## Calculating Modular Inverses with Euler's Theorem

While we introduced the brute-force method above for calculating modular inverses, we can actually solve for the modular inverse directly with Euler's theorem.

<blockquote class="blockquote-theorem">
<hr>
If $a$ and $n$ are coprime, then the following is true:

$$a^{\phi(n)} \equiv 1 \pmod{n}$$

where $\phi(n)$ is the Euler totient function and is defined as the number of positive integers $x < n$ such that $x$ and $n$ are coprime. If $n$ is prime, then $\phi(n) = n - 1$. If $n$ is not prime and has the prime factorization 

$$n = {p_1}^{a_1}{p_2}^{a_2}...$$

then $\phi(n)$ can be calculated as

$$\phi(n) = n * \dfrac{p_1 - 1}{p_1} * \dfrac{p_2 - 1}{p_2} * ...$$
</blockquote>

By cleverly using this fact, we can actually calculate the modular inverse of $a$ as follows:

$$a * a^{-1} \equiv 1 \pmod{n}$$

$$a^{\phi(n)} \equiv 1 \pmod{n}$$

By substituting the second equation into the first one, we obtain the following relation:

$$a * a^{-1} \equiv a^{\phi(n)} \pmod{n}$$

$$\boxed{a^{-1} \equiv a^{\phi(n) - 1} \pmod{n}}$$

In this case, we actually divided both sides by $a$, which is valid since $a$ and $n$ are coprime (if there exists a modular inverse) and both sides were divisible by $a$.

By using this fact, we can actually calculate directly the modular inverse. For instance, if we wanted to calculate $3^{-1} \pmod{7}$ without brute force, we could do the following:

$$\phi(7) = 7 - 1 = 6$$

$$3^{-1} \equiv 3^{6 - 1} \equiv 3^5 \equiv 243 \equiv 5 \pmod{7}$$

However, as you can probably guess, this method, although direct, can require some intense calculation with very large powers for large $n$. However, for small $n$, it can be much faster, especially when used for calculating several modular inverses with respect to $n$. Additionally, this method is also much more reasonable when done using a computer, which can churn these out very quickly. When combined with binary exponentiation, calculating large exponents is not that daunting.

However, there is another method that can be used to calculate modular inverses, which we will discuss next.

## Calculating Modular Inverses with Extended Euclidean Algorithm

Another method of calculating modular inverses that doesn't require huge exponents is with the extended euclidean algorithm.

### Extended Euclidean Algorithm

You may have heard of the Euclidean algorithm, which is a computational method for determining the $\gcd$ of two numbers. For those who haven't or need a quick refresher, it is described below.

<blockquote class="blockquote-theorem">
<hr>
Let the two numbers be $a$ and $b$, with $a > b$.
If $b = 0$, then the $\gcd(a, b) = a$
Otherwise, 

$$\gcd(a, b) = \gcd(a\ \%\ b, b)$$
</blockquote>

As an example, we can compute $\gcd(100, 40)$.

$$\gcd(100, 40) = \gcd(20, 40) = \gcd(20, 0) = \boxed{20}$$

The extended Euclidean algorithm is a bit different, although it also calculates the $\gcd$.

<blockquote class="blockquote-theorem">
<hr>
Bézout's identity states there always exists integers $x$ and $y$ such that the following is true:

$$ax + by = \gcd(a, b)$$
</blockquote>

Given the numbers $a$ and $b$, the extended Euclidean algorithm gives us a method to calculate both the coefficients $x$ and $y$ given in Bézout's identity, as well as $\gcd(a, b)$. This is why it's called the **extended** Euclidean algorithm. While the normal Euclidean algorithm just gives us $\gcd(a, b)$, the extended version also tells us how to form that $\gcd$ through a linear combination of $a$ and $b$.

To show how it works, we can use an example with $a = 42$ and $b = 56$. As mentioned before, this will give us $\gcd(42, 56)$, as well as $x$ and $y$ in the equation:

$$46x + 56y = \gcd(46, 56)$$

To do this, we first write $56$ as the sum of a multiple of $46$ and a remainder.

$$56 = \colorbox{Aquamarine}{46}(1) + \colorbox{BurntOrange}{10}$$

Next, this may seem pretty arbitrary, but we repeat the same process, this time writing $42$ as the sum of a multiple of the previous remainder, $10$, and another remainder.

$$\colorbox{Aquamarine}{46} = \colorbox{BurntOrange}{10}(4) + \colorbox{ForestGreen}{6}$$

We repeat this process again until we obtain $0$ as a remainder.

$$
\begin{aligned}
    \colorbox{BurntOrange}{10} &= \colorbox{ForestGreen}{6}(1) + \colorbox{Orchid}{4} \\
    \colorbox{ForestGreen}{6} &= \colorbox{Orchid}{4}(2) + \colorbox{Aquamarine}{2} \\
    \colorbox{Orchid}{4} &= \colorbox{Aquamarine}{2}(2) + 0 \\
\end{aligned}
$$

Once we obtain $0$ as the remainder, we can stop. From this process, the last non-zero remainder that we obtained is actually $\gcd(a, b)$. Since in this case it was $2$, $\gcd(46, 56) = 2$.

Note that this process is actually just running the Euclidean algorithm, it's just that we kept a bunch of extra information as well. We can summarize this process below:

$$
\begin{aligned}
    56 &= \colorbox{Aquamarine}{46}(1) + \colorbox{BurntOrange}{10} \\
    \colorbox{Aquamarine}{46} &= \colorbox{BurntOrange}{10}(4) + \colorbox{ForestGreen}{6} \\
    \colorbox{BurntOrange}{10} &= \colorbox{ForestGreen}{6}(1) + \colorbox{Orchid}{4} \\
    \colorbox{ForestGreen}{6} &= \colorbox{Orchid}{4}(1) + \colorbox{Aquamarine}{2} \\
    \colorbox{Orchid}{4} &= \colorbox{Aquamarine}{2}(2) + 0
\end{aligned}
$$

To determine $x$ and $y$, we need to do a bit of rearranging to isolate the remainder term in each of the equations as follows. We're simply just subtracting a term from the right side and placing it on the right side.

$$
\begin{aligned}
    \colorbox{BurntOrange}{56 - 46(1) = 10} \\
    \colorbox{ForestGreen}{46 - 10(4) = 6} \\
    \colorbox{Orchid}{10 - 6(1) = 4} \\
    \colorbox{Aquamarine}{6 - 4(1) = 2}
\end{aligned}
$$

Now that we have this, we are actually all set to solve for $x$ and $y$! Remember, we are trying to find $x$ and $y$ such that:
$$46x + 56y = \gcd(46, 56) = 2$$

To do so, we look at the last equation, which expresses $\gcd(46, 56)$ as a linear combination of $6$ and $4$, not the desired $46$ and $56$.

$$6 - \colorbox{Orchid}{4}(1) = 2$$

However, the equation right above it is an expression for $4$.

$$\colorbox{Orchid}{10 - 6(1) = 4}$$

We can substitute this in to obtain the following:

$$6 - \colorbox{Orchid}{(10 - 6(1))}(1) = 6 - 10(1) + 6(1) = \colorbox{ForestGreen}{6}(2) - 10(1) = 2$$

This expression now expresses $\gcd(46, 56)$ as a linear combination of $6$ and $10$. Once again, we can use the expression above it to substitute, this time for $6$.

$$\colorbox{ForestGreen}{46 - 10(4) = 6}$$

$$\colorbox{ForestGreen}{(46 - 10(4))}(2) - 10(1) = 2(46) - \colorbox{BurntOrange}{10}(9) = 2$$

We can repeat this step one last time and obtain the following:

$$\colorbox{BurntOrange}{56 - 46(1) = 10}$$

$$46(2) - \colorbox{BurntOrange}{(56 - 46(1))}(9) = \boxed{46(11) - 56(9) = 2}$$

From this, we can determine that $x = 11$ and $y = -9$!

Here all of the calculations sorted:

1. Express each term as the sum of a multiple of the other term and a remainder.

$$
\begin{aligned}
    56 &= \colorbox{Aquamarine}{46}(1) + \colorbox{BurntOrange}{10} \\
    \colorbox{Aquamarine}{46} &= \colorbox{BurntOrange}{10}(4) + \colorbox{ForestGreen}{6} \\
    \colorbox{BurntOrange}{10} &= \colorbox{ForestGreen}{6}(1) + \colorbox{Orchid}{4} \\
    \colorbox{ForestGreen}{6} &= \colorbox{Orchid}{4}(1) + \colorbox{Aquamarine}{2} \\
    \colorbox{Orchid}{4} &= \colorbox{Aquamarine}{2}(2) + 0
\end{aligned}
$$

2. Rearrange each of those equations except the last to obtain an expression for the remainder.

$$
\begin{aligned}
    \colorbox{BurntOrange}{56 - 46(1) = 10} \\
    \colorbox{ForestGreen}{46 - 10(4) = 6} \\
    \colorbox{Orchid}{10 - 6(1) = 4} \\
    \colorbox{Aquamarine}{6 - 4(1) = 2}
\end{aligned}
$$

3. Starting from the last equation, substitute in the expression directly on top and combine like terms.

$$
\begin{aligned}
    6 - \colorbox{Orchid}{4}(1) = 2 \\
    6 - \colorbox{Orchid}{(10 - 6(1))}(1) = \colorbox{ForestGreen}{6}(2) - 10(1) = 2 \\
    \colorbox{ForestGreen}{(46 - 10(4))}(2) - 10(1) = 2(46) - \colorbox{BurntOrange}{10}(9) = 2 \\
    46(2) - \colorbox{BurntOrange}{(56 - 46(1))}(9) = \boxed{46(11) - 56(9) = 2}
\end{aligned}
$$



For another worked out example, check out this video:

<iframe width="560" height="315" src="https://www.youtube.com/embed/6KmhCKxFWOs" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen style="display: block; margin: auto"></iframe>

### Applying to Linear Diophantine Equations

As a quick side note, we can also apply this to solve linear diophantine equations of two variables, where **diophantine** means that the equation only has integer solutions. We won't get too deep into the details, but if we have an equation like the following, we can solve it pretty easily.

$$19a + 7b = 23$$

Since $\gcd(19, 7) = 1$, we can use the extended Euclidean algorithm to find the values of $a'$ and $b'$ that make $19a' + 7b' = 1$. Then, we can scale these values up by $23$ to get the solution for our original equation. This works for any value on the right side that we need to find, as long as it is is a multiple of the $\gcd$. It can actually be shown that this will always produce the solution for us if it exists since if the right side is **not** a multiple of the $\gcd$, there are **no** solutions.

### Applying to Modular Inverses

To see how this can be useful for what this article is about, let's consider what happens when $a$ and $b$ are coprime. By definition then, $\gcd(a, b) = 1$, meaning that

$$ax + by = 1$$

If we consider this equation $\text{mod } b$, then we obtain the following:

$$ax = 1 \pmod{b}$$

Therefore, $a^{-1} \equiv x \pmod{b}$ and $b^{-1} \equiv y \pmod{a}$!

While this method may appear longer than the previous one, it does not involve any exponents and therefore does not require as large of calculations. For example, this method can actually be used to calculate the modular inverse of extremely large numbers with just a four-function calculator, which is especially useful when doing things such as decrypting RSA ciphers by hand (the reason why I bring this up is because of the Codebusters event I did in Science Olympiad).

<blockquote class="blockquote-example">
<hr>
Calculate the modular inverse of $1381937$ with respect to $283819382$.
</blockquote>

Clearly, exponentiating $1381937$ would not lead to a good time, as $\phi(283819382) = 108701280$. This **could** be done with a computer rather quickly if you use binary lifting exponentiation, but doing so by hand would almost definitely lead to a bad time. Instead, we should use the extended Euclidean algorithm to find the modular inverse.

We first write each term as the sum of multiples of the other term and a remainder:

$$
\begin{aligned}
    283819382 &= 1381937(205) + 522297 \\
    1381937 &= 522297(2) + 337343 \\
    522297 &= 337343(1) + 184954 \\
    337343 &= 184954(1) + 152389 \\
    184954 &= 152389(1) + 32565 \\
    152389 &= 32565(4) + 22129 \\
    32565 &= 22129(1) + 10436 \\
    22129 &= 10436(2) + 1257 \\
    10436 &= 1257(8) + 380 \\
    1257 &= 380(3) + 117 \\
    380 &= 117(3) + 29 \\
    117 &= 29(4) + 1 \\
    29 &= 1(29) + 0 \\
\end{aligned}
$$

From this exhausting amount of calculations, we can determine that $\gcd(283819382, 1381937) = 1$, so the modular inverse of $1381937$ does in fact exist. We can proceed with the next step, to rearrange each of the equations:

$$
\begin{aligned}
    283819382 - 1381937(205) &= 522297 \\
    1381937 - 522297(2) &= 337343 \\
    522297 - 337343(1) &= 184954 \\
    337343 - 184954(1) &= 152389 \\
    184954 - 152389(1) &= 32565 \\
    152389 - 32565(4) &= 22129 \\
    32565 - 22129(1) &= 10436 \\
    22129 - 10436(2) &= 1257 \\
    10436 - 1257(8) &= 380 \\
    1257 - 380(3) &= 117 \\
    380 - 117(3) &= 29 \\
    117 - 29(4) &= 1 \\
\end{aligned}
$$

Finally, we back-substitute each of the expressions one-by-one into the one below it, starting from the bottom.

$$
\begin{aligned}
    117 - 29(4) &= 1 \\
    117 - (380 - 117(3))(4) = 117(13) - 380(4) &= 1 \\
    (1257 - 380(3))(13) - 380(4) = 1257(13) - 380(43) &= 1 \\
    1257(13) - (10436 - 1257(8))(43) = 1257(357) - 10436(43) &= 1 \\
    (22129 - 10436(2))(357) - 10436(43) = 22129(357) - 10436(757) &= 1 \\
    22129(357) - (32565 - 22129(1))(757) = 22129(1114) - 32565(757) &= 1 \\
    (152389 - 32565(4))(1114) - 32565(757) = 152389(1114) - 32565(5213) &= 1 \\
    152389(1114) - (184954 - 152389(1))(5213) = 152389(6327) - 184954(5213) &= 1 \\
    (337343 - 184954(1))(6327) - 184954(5213) = 337343(6327) - 184954(11540) &= 1 \\
    337343(6327) - (522297 - 337343(1))(11540) = 337343(17867) - 522297(11540) &= 1 \\
    (1381937 - 522297(2))(17867) - 522297(11540) = 1381937(17867) - 522297(47274) &= 1 \\
    1381937(17867) - (283819382 - 1381937(205))(47274) = 1381937(9709037) - 283819382(47274) &= 1 \\
\end{aligned}
$$

Therefore, $x = 9709037$ and $y = 47274$. From this, we can conclude that the modular inverse of $1381937$ is $9709037$ with respect to $283819382$. We can multiply this out to see that this in fact works. While this set of equations was exhausting to go through, it works and only requires basic arithmetic operations.

### Chart Method

While the above gives a great amount of intuition for why the algorithm works and makes it easy to memorize, it is not that great for computation since you have to rewrite a **ton** of stuff. As a result, it is faster to use a chart to organize everything.

We can construct a chart as follows for the process of $\gcd(46, 56)$.

| Row | a  | b  | r  | q | x   | y   |
|-----|----|----|----|---|-----|-----|
| 1   | 56 | 46 |    |   |     |     |

To perform the first step of the algorithm, we have to fill in the columns $a, b, r, \text{ and } q$. The recurrence relation to calculate the values of the chart are listed below, where a term like $a_i$ represents the value in the column $a$ in the row $i$.

$$
\begin{aligned}
    & a_1 = a
    & b_1 = b \\
    \\
    & a_{i + 1} = b_i \\
    & b_{i + 1} = r_{i}
    \\\\
    & r_i = a_i \ \%\ b_i \\
    & q_i = \lfloor{a_i / b_i}\rfloor
    \\\\
    & x_{n - 1} = 1
    & y_{n - 1} = -1 \\
    \\
    & x_{i} = y_{i + 1} \\
    & y_{i} = x_{i + 1} - y_{i + 1} * q_{i}
    \end{aligned}
$$

$a$ and $b$ represent our two numbers, $r$ represents the remainder ($a\ \%\ b$) and $q$ represents the truncated quotient of the two $(\lfloor{a / b}\rfloor)$. After this, we transfer the value of $b$ to $a$ for the next row, and the value of $r$ to $b$ for the next row. Note that this is equivalent to the first step from the previously mentioned procedure, just in the form of a chart.

| Row | a  | b     | r  | q | x   | y   |
|-----|----|-------|----|---|-----|-----|
| 1   | 56 | 46    | 10 | 1 |     |     |
| 2   | 46 | 10    | 6  | 4 |     |     |
| 3   | 10 | 6     | 4  | 1 |     |     |
| 4   | 6  | 4     | 2  | 1 |     |     |
| 5   | 4  | **2** | 0  | 2 |     |     |

From this, we can find that the value of the $\gcd$ is the last non-zero value of $r$, which is $2$. Next, to fill in the values of $x$ and $y$, we first start off with the values of $1$ and $-1$ at the second to last row.

| Row | a  | b  | r  | q | x   | y   |
|-----|----|----|----|---|-----|-----|
| 1   | 56 | 46 | 10 | 1 |     |     |
| 2   | 46 | 10 | 6  | 4 |     |     |
| 3   | 10 | 6  | 4  | 1 |     |     |
| 4   | 6  | 4  | 2  | 1 | 1   | -1  |
| 5   | 4  | 2  | 0  | 2 | N/A | N/A |

To compute the values for $x$ and $y$ for the row above it, we set the transfer the $y$ from below to the $x$ above. Then, to compute the above $y$, we take the below value of $x$ and subtract from it the below value of $y$ multiplied by the upper value for $q$. For instance, the new value of $y$ here would be $$y_{\text{above}} = x_{\text{below}} - y_{\text{below}} * q_{\text{above}} = 1 - (-1) * 1 = 2$$. We can do this for the entire grid to get the following:

| Row | a  | b  | r  | q | x   | y   |
|-----|----|----|----|---|-----|-----|
| 1   | 56 | 46 | 10 | 1 | -9  | 11  |
| 2   | 46 | 10 | 6  | 4 | 2   | -9  |
| 3   | 10 | 6  | 4  | 1 | -1  | 2   |
| 4   | 6  | 4  | 2  | 1 | 1   | -1  |
| 5   | 4  | 2  | 0  | 2 | N/A | N/A |

We can verify that these values work, as $-9 * 56 + 11 * 46 = 2$, as we expected.

## Dealing With Nonexistent Modular Inverses

As we mentioned before, if $a$ shares any factors with $n$, the modular inverse of $a$ with respect to $n$ does not exist. This corresponds to the bottom left portion of the chart shown in the beginning of this post. However, there may still be equations that we need to solve, such as the following:

$$2x \equiv 2 \pmod{8}$$

In this case, we do not have a modular inverse for $2$ as $\gcd(2, 8) = 2 \neq 1$. However, the reason why this modular inverse does not exist is actually that this equation has multiple solutions modulo $8$. For instance, $x \equiv 1 \pmod{8}$ and $x \equiv 5 \pmod{8}$ both work for the above case!

The way we solve a problem like this is that if we want to divide by $a$, we first want to find $\gcd(a, n)$ and then divide everything by that value, including $n$. For instance, in this case, $\gcd(2, 8) = 2$, so we divide everything by $2$.

$$2x \equiv 2 \pmod{8} \rightarrow x \equiv 1 \pmod{4}$$

This is our new equation, and this gives us our solutions for $x$! Notice how they match up with the two that were mentioned earlier. However, it is not always the case that $\gcd(a, n) = a$, so it will not directly give you the solution as it did here. However, in those cases, you have divided out the shared factors, which means that the new $a$ and $n$ are now coprime! This means you can apply the modular inverse technique mentioned earlier to then solve that new equation.

However, all of this assumed that the right side of the equation was also divisible by $\gcd(a, n)$. However, it can be shown that if this is not the case, then the equation has no solutions, which means we do not have to worry about this case.

As a final example, we will solve the following equation:

$$26x \equiv 12 \pmod{16}$$

We can first find $\gcd(26, 16) = 2$ from inspection and reduce the equation to the following;

$$13x \equiv 6 \pmod{8}$$

Then, we just need to find $13^{-1} \pmod{8}$. To do this, we will apply the Euler's theorem method.

$$\phi(8) = 8 * \dfrac{1}{2} = 4$$

$$13^-1 \equiv 5^-1 \equiv 5^{\phi(8) - 1} \equiv 5^{3} \equiv 5 \pmod{8}$$

Therefore, we can multiply both sides of the equation by $5$ to obtain our answer:

$$x \equiv 30 \equiv 6 \pmod{8}$$

If we wanted to, we could convert this back to $\text{mod } 16$ and obtain

$$x \equiv 6, 14 \pmod{16}$$

With that, we're done!

## Summary

All in all, division in modular arithmetic can be pretty messy, and it is pretty important to carefully consider what you're doing before you do anything. Additionally, when calculating modular inverses, it is very important to keep good bookkeeping and to constantly check that the equations being written still satisfy the relations they're supposed to. For instance, periodically checking while you're doing the extended Euclidean algorithm to make sure the values still sum to the $\gcd$ properly while substituting is pretty important for avoiding mistakes.
