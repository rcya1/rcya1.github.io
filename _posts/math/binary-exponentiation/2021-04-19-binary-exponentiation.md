---
title: Binary Exponentiation
date: 2021-04-19 11:00:00 -0400
categories: [Math]
tags: [Math, Guide, Modular Arithmetic]
math: true
toc: true
toc_sticky: true
excerpt: Let's say you wanted to calculate the large power of a number modulo another such as 7^39 mod 1000. The most naive way to do this would be to multiply 7 by itself 39 times and then take the remainder when divided by 1000, aka the last 3 digits. However, this technique quickly becomes unmanageable, especially since 7^39 has 32 digits, which would lead to a lot of work and the opportunity to make a lot of mistakes. Instead, we could work smarter, not harder.
---

## Typical Exponentiation

Let's say you wanted to calculate the large power of a number modulo another such as

$$7^{39} \pmod{1000}$$

The most naive way to do this would be to multiply $7$ by itself $39$ times and then take the remainder when divided by $1000$, aka the last $3$ digits. However, this technique quickly becomes unmanageable, especially since $7^{39}$ has $32$ digits, which would lead to a lot of work and the opportunity to make a lot of mistakes. Instead, we could work smarter, not harder.

The next way we could augment this process is by realizing that after each successive multiplication, we could take the intermediate product modulo $1000$. For instance, we would first have $7, 7^2 = 49, 7^3 = 343$. After this, we would have $7^4 = 2401$, but we can ignore everything but the last $3$ digits and simply take the $401$ as our product moving forward. By continuing this strategy, we will constantly stay with small numbers and not have to deal with $32$ digit monstrosities. However, this still involves us doing $38$ multiplications to get from $7$ to $7^{39}$. As the exponent grows even larger, it would become infeasible for humans to do it by hand.

While computers can solve these problems easily, even computers have their limitations. If the computer has to do thousands of these calculations and take powers that go up to the hundreds of millions, this strategy quickly grows infeasible as well.

However, there is a solution that can drastically speed up this calculation for large numbers known as **binary exponentiation**. Binary exponentiation takes advantage of the fact that we can **square** numbers in a single operation by simply multiplying it with itself, which doubles the exponent.

## Applying Squaring

Let's say that the power we wanted to calculate was $7^8$. While we could multiply $7$ with itself $8$ times, let's use squaring. We can first calculate $7^2 = 49$. Then, rather than multiplying $49$ by $7$ twice, we can instead square $7^2 = 49$ in a single operation to get $$7^4 = \left(7^2\right)^2 = 49^2 = 2401$$

Finally, we can square this number to get $$7^8 = \left(7^4\right)^2 = 2401^2 = 5764801$$

By using squaring, we were able to reduce our multiplication from $8$ steps to only $3$. While one may say that this may have made the operation harder since we had to square very large numbers, if we had even larger exponents and were also taking the values modulo something, the benefits of this method quickly become apparent as the number of multiplications required would actually be logarithmic when compared to the exponent. Going all the way up to something like the $1024$th exponent would only require $10$ operations, compared to the $1023$ from before.

However, this very simple trick only works at the moment with exponents that are powers of $2$. However, this is where the **binary** part of binary exponentiation comes in.

## Binary

If you aren't familiar with the concept of other number bases, please look at [this explanation from Better Explained](https://betterexplained.com/articles/numbers-and-bases/) that covers it well.

Now that you are familiar with number bases, binary is another word for base $2$, where each digit in a number can be either $0$ or $1$ and represents a power of $2$. You may have heard about binary in other contexts such as describing things that only have $2$ options or with computers since binary is used to represent all numbers for a computer.

Let's look at a few examples to make sure we are comfortable with binary, but feel free to skip to the next section if you are already comfortable.

<blockquote class="blockquote-example">
<hr>
Express the binary number $111011$ in base $10$.
</blockquote>

We can do this by looking at each digit from right to left and using those to see which powers of $2$ are present in our number. Since the first two digits on the right are both $1$s, we know that $2^0$ and $2^1$ are present in our number. Since the third digit is a $0$, $2^2$ is not. However, the next three are, so the total sum would be $$2^0 + 2^1 + 2^3 + 2^4 + 2^5 = \boxed{52}$$

<blockquote class="blockquote-example">
<hr>
Express the number $37$ in binary.
</blockquote>

We can do this by first looking for the largest power of $2$ present in $37$. The powers of $2$ are $1, 2, 4, 8, 16, 32, 64, ...$ Since $32 < 37$ but $64 > 37$, we know that $32$ is the largest power of $2$ present. We can keep note that $32 = 2^5$ is present in the number and move on by subtracting $32$ from $37$. We are left with $5$ and we have to now find the largest power of $2$ present in that. The answer is $4 = 2^2$, and after subtracting that we are left with $1 = 2^0$. We know that the powers of $2$ present are $0, 2, 5$, which corresponds to the number $100101$, since all of the correct powers of $2$ are represented there.

## Full Binary Exponentiation

Now that we have a grasp on binary, we can move on to what exactly binary exponentiation is. The idea behind the technique is that we can break up the exponent into its binary representation and then use those corresponding powers of $2$s in our calculation. For instance, let's say we wanted to calculate the following:

$$3^{37}$$

We can first express our exponent, $37$, in binary, or as sums of powers of $2$. We can quickly get that it is 

$$37 = 32 + 4 + 1 = 2^5 + 2^2 + 2^0$$

We can then plug this representation back into our original equation to obtain:

$$3^{2^5 + 2^2 + 2^0}$$

Rewriting this with laws of exponents, we obtain the following result:

$$3^{37} = 3^{2^0} * 3^{2^2} * 3^{2^5}$$

However, remember what we said before about exponents that were powers of $2$. We can apply squaring to easily calculate all of those powers required in just $5$ operations. Then, we can simply multiply together the results to obtain the final answer in much less than $37$ operations.

**Calculating the Powers**

$$
\begin{aligned}
3^{2^0} &= 3 \\
3^{2^1} &= 3^2 = 9 \\
3^{2^2} &= 9^2 = 81 \\
3^{2^3} &= 81^2 = 6561 \\
3^{2^4} &= 6561^2 = 43046721 \\
3^{2^5} &= 43046721^2 = 1853020188851841
\end{aligned}
$$

**Final Result**

$$3^{37} = 3^{2^0} * 3^{2^2} * 3^{2^5} = 3 * 81 * 1853020188851841 = \boxed{450283905890997363}$$

Since those numbers were huge, a more reasonable calculation might be to instead calculate 

$$3^{37} \pmod{1000}$$

This could be done the mostly the same way, but you have to instead take each intermediate result mod $1000$.

**Calculating the Powers**

$$
\begin{aligned}
3^{2^0} &= 3 \\
3^{2^1} &= 3^2 = 9 \\
3^{2^2} &= 9^2 = 81 \\
3^{2^3} &= 81^2 = 6561 \rightarrow 561 \\
3^{2^4} &= 561^2 = 314721 \rightarrow 721 \\
3^{2^5} &= 721^2 = 519841 \rightarrow 841
\end{aligned}
$$

**Final Result**

$$3^{37} = 3^{2^0} * 3^{2^2} * 3^{2^5} = 3 * 81 * 841 = 204363 \rightarrow \boxed{363}$$

And that's pretty much the entire method! Next up, we'll go over the advantages of this algorithm and then some of the applications for such huge exponents.

## Big O Notation

For those not comfortable with big O notation from computer science, feel free to skip this section. But for those interested, it is essentially a measure of how the number of operations required in a calculation scale as the input size $N$ changes. Check out [this article](https://rob-bell.net/2009/06/a-beginners-guide-to-big-o-notation/) for more details if you're interested. It's a topic that is very important for analyzing the runtime of computer algorithms, but its core ideas can be applied in other subject areas.

For those who know what it is, you may have realized that the naive algorithm for calculating exponents runs in $O(N)$ linear time. However, the binary exponentiation method runs in $O(\log_2(N))$ time, which is a massive improvement as $N$ increases. This is because the number of digits in the binary representation of a number is approximately equal to $\log_2(N)$.

## Advantage Over Naive Method

One could appreciate the significant advantages of using this algorithm when calculating something like $$7^{1000000}$$

The naive method would require around $1000000$ operations since you would have to multiply by $7$ that many times. However, the binary representation of $1000000$ is $11110100001001000000$, which is only $20$ digits long. This means that you would have to calculate only $20$ powers of $7$ (with two of them being $7^0$ and $7^1$). Then, you would only need to multiply $7$ of those numbers, which would correspond to the $1$s in the binary representation. This totals only $27$ operations compared to the almost $1000000$ from before.

## Applications

### Modular Inverses

The first application is for calculating **modular inverses**. In the short future, I'll add a post that goes over this topic in depth, but essentially there's a formula that allows you to calculate the modular inverse of a number $a$ mod $n$.

$$a^{\phi(n) - 1} \pmod{n}$$

For extremely large $n$, especially when $n$ is prime, binary exponentiation is almost a necessity to do the operations with enough speed.

### Fibonacci Relation

However, this idea of binary exponentiation does not just apply to numbers; it can also be applied to ideas like matrices. For instance, it can even be used to calculate the Fibonacci numbers! If you're not familiar with matrices, and how they can be multiplied or used to represent linear systems, I would highly recommend checking it out since they can be really cool.

For those unfamiliar with the Fibonacci numbers, they are a sequence of integers such that $F_n$ represents the $n$th Fibonacci numbers. We define $F_0 = 0$ and $F_1 = 1$, and then we use the recurrence relation

$$F_n = F_{n - 1} + F_{n - 2}$$

Essentialy, each next term is the sum of the previous $2$ terms. The sequence goes like this:

$$0, 1, 1, 2, 3, 5, 8, 13, 21, 34, 55, 89, 144, 233, 377, ...$$

We can actually express this with the following equation:

$$
\begin{bmatrix}
  0 & 1 \\
  1 & 1
\end{bmatrix} * 
\begin{bmatrix}
  F_n \\
  F_{n+1}
\end{bmatrix} = 
\begin{bmatrix}
  F_{n+1} \\
  F_{n+2}
\end{bmatrix}
$$

To dissect how this matrix equation works, we can break it down into its component linear equations:

$$F_{n + 1} = 0 + F_{n + 1}$$

$$F_{n + 2} = F_{n} + F_{n + 1}$$

Both of these equations perfectly describe how the Fibonacci sequence is generated, showing how the matrix equation encodes the linear recurrence present in the system. The reason why this is so powerful is that we can continuously multiply these matrices to obtain higher values in the Fibonacci sequence.

In general, we can do the following:

$$
\begin{bmatrix}
  0 & 1 \\
  1 & 1
\end{bmatrix}^n * 
\begin{bmatrix}
  F_0 \\
  F_1
\end{bmatrix} = 
\begin{bmatrix}
  F_{n} \\
  F_{n+1}
\end{bmatrix}
$$

This gives us a method using matrix exponentiation to calculate the $n + 1$th Fibonacci number. However, with the power of binary exponentiation, we can calculate this exponent quickly, making calculating something like the $1000$th Fibonacci number relatively trivial. The same process of binary exponentiation can be used making this a relatively flexible technique.

## Conclusion

Overall, binary exponentiation is a pretty powerful technique to both do hand computations quickly and to speed up computer algorithms. It can be applied to pretty much any mathematical structure that has exponentiation as well, including real numbers, complex numbers, and matrices, two of which we saw above.

## Side Note: Implementation in Programming

As a quick side note, we could do the following to implement this algorithm in code (the code is in Java, but it is easily expandable to other languages). I'm not going to go over exactly how the code works as of now, but I might add it in the future.

```java
long binaryExpo(int base, int exponent) {
    long result = 1;
    long currPower = base;
    while(exponent > 0) {
        if (exponent % 2 > 0) {
            result = result * currPower;
        }
        currPower = currPower * base;
        exponent /= 2;
    }

    return result;
}
```

We could optimize this program with bitwise operations as following (although a good compiler would probably automatically substitute these in). This method might appear more intuitive for those familar with the binary operations utilized, since it more clearly shows how you're analyzing each binary digit of the exponent.

```java
long binaryExpo(int base, int exponent) {
    long result = 1;
    long currPower = base;
    while(exponent > 0) {
        if (exponent & 1 > 0) {
            result = result * currPower;
        }
        currPower = currPower * base;
        exponent >>= 1;
    }

    return result;
}
```
