---
layout: post
title: Fibonacci
author: Charles Thomas
---

# What is it?
Fibonacci numbers are the numbers: $$1, 1, 2, 3, 5, 8, 13...$$. These are defined by starting with $$1,1$$ then every number afterwards is the sum of the previous two.
We can write this as: $$f_n = f_{n-1} + f_{n-1}$$

# Recursive code
When you're first learning to program you may have written some code to calculate the find the nth fibonacci number.

```
def find_nth_fib(n):
    if n == 1:
        return 1
    if n == 2:
        return 1

    return find_nth_fib(n-1) + find_nth_fib(n-1)
```

# What is it?
The code above works by computing all the previous fibonacci numbers in order to find the one you're looking for. However, there is a way of calculating the nth fibonacci number directly and it's given by this formula:

$$
\frac{1}{\sqrt{5}}((\frac{1 + \sqrt{5}}{2})^n - (\frac{1 - \sqrt{5}}{2})^n)
$$

# Proof of it

## Define series $$F_n$$
Proving this starts by defining the following series:

$$
F(x) = \sum_{i=0}^{\infty}f_{i+1}x^i
$$

Where $$f_i$$ is the ith fibonacci number.

## Prove $$Fn$$ converges
Most of these infinite sums just get infinitely big or infinitely small (we say these sums are divergent). But the sum we have defined above actually becomes a number (we say it converges to a number) so long as $$|x| < \frac{1}{2}$$

### Ratio Test 
To prove this we need to use the ratio test. 

For a series: 

$$\sum_{n=0}^{\infty}a_n$$

The ratio test looks at the ratio between adjacent terms: 

$$|\frac{a_{n+1}}{a_n}|$$

And then takes the limit as we go to infinity

$$\lim_{n \rightarrow \infty} |\frac{a_{n+1}}{a_n}|$$

This tells us if the terms eventually stay close to each and the series converges or not. Formally it says:


$$
\lim_{n \rightarrow \infty} |\frac{a_{n+1}}{a_n}| < 1
$$ then the series converges

$$
\lim_{n \rightarrow \infty} |\frac{a_{n+1}}{a_n}| = 1
$$ then the test doesn't tell you one way or the other.

$$
\lim_{n \rightarrow \infty} |\frac{a_{n+1}}{a_n}| > 1
$$ then the series is divergent

### Comparison Test
Another useful way to work out if a series converges that we'll need is the comparison test. The comparison test allows us to say if we know the terms in one series are smaller than the terms in convergent. 

If we have the series of positive numbers $$\sum_{n=0}^{\infty}a_n$$ and the convergent series of positive numbers $$\sum_{n=0}^{\infty}b_n$$ and after some point in the series: 

$$
|a_n| \leq |b_n|
$$

then $$\sum_{n=0}^{\infty}a_n$$ also converges

### $$2^n$$ series
Now to prove our series $$F_n(x)$$ is convergent. We use the common technique of showing that the terms of our series is smaller than the terms of some other series then showing that the other series converges. This combines the two previous tests.

Consider the series $$\sum_{n=0}^{\infty}(2x)^n$$.

Now we can show that $$
f_n \leq 2^n
$$ by applying induction.

For the case $$n = 1$$ we have $$f_n = 1$$, $$2^1 = 2$$ and $$1 < 2$$

Now we assume it for $$n = k$$, so we have $$f_k < 2^k$$

Next, we consider $$n = k+1$$, $$f_{k+1} = f_k + f_{k-1}$$ which by our assumption: 

$$f_k + f_{k-1} < 2^{k} + 2^{k-1} = 2^{k-1}(2 + 1) = 2^{k-1} * 3 < 2^{k-1} * 4 = 2^{k-1} * 2^2 = 2^{k+1}$$

So now we need to show that $$\sum_{n=0}^{\infty}2^n$$ is convergent.

To do this we apply the ratio test:

$$
\lim_{n \rightarrow \infty} |\frac{(2x)^{n+1}}{(2x)^n}| 
=\lim_{n \rightarrow \infty} |(2x)^n| 
$$

Now $$
|(2x)^n| = |2^n x^n|  < 1
$$ only if $$x < \frac{1}{2}$$

Therefore our series $$F_n(x)$$ converges if $$x < \frac{1}{2}$$

## Construct other series
Now let's consider the series: $$xF(x)$$ and $$x^2F(x)$$

Todo: Show these converge

## Take difference

First let's note that
$$
F(x) - xF(x) - x^2F(x)
= F(x)(1 - x - x^2)
$$

Now let's write this a different way

$$F(x) - xF(x) - x^2F(x)$$
$$= f_1 + f_2x + f_3x^2 + ... + f_nx^{n-1} - (f_1x + f_2x^2 + f_3x^3 + ... + f_nx^{n}) - (f_1x^2 + f_2x^3 + f_3x^4 + ... + f_nx^{n+1})$$
$$= f_1 + (f_2 - f_1)x - (f_3 - f_2 - f_1)x^2 + ... + (f_n - f_{n-1} - f_{n-2})x^{n-1}$$

By applying $$f_n = f_{n-1} + f_{n-2}$$ and that $$f_2 = f_1 = 1$$ we get

$$F(x) - xF(x) - x^2F(x) = F(x)(1 - x - x^2) = f_1 = 1$$

Rearranging this gives:

$$F(x) = \frac{1}{1 - x - x^2}$$


## Write as partial fractions
Using the quadratic formula we solve $$1- x - x^2 = 0$$:

$$x = \frac{-b \pm \sqrt{b^2 - 4ac}}{2a}=\frac{1 \pm \sqrt{1 + 4}}{-2}=-\frac{1 \pm \sqrt{5}}{2}$$

 so we can factor it into:

$$1- x - x^2 = -(x + \frac{1 + \sqrt{5}}{2})(x + \frac{1 - \sqrt{5}}{2})$$

This means we can write:

$$F(x) = \frac{1}{1 - x - x^2} = -\frac{1}{(x + \frac{1 + \sqrt{5}}{2})(x + \frac{1 - \sqrt{5}}{2})} = - (\frac{A}{x + \frac{1 + \sqrt{5}}{2}} + \frac{B}{x + \frac{1 - \sqrt{5}}{2}})$$

To find A and B we know that:

$$A(x + \frac{1 - \sqrt{5}}{2}) + B(x + \frac{1 + \sqrt{5}}{2}) =1$$

Now substitute in $$x = -\frac{1 - \sqrt{5}}{2}$$:

$$B(-\frac{1 - \sqrt{5}}{2} + \frac{1 + \sqrt{5}}{2}) = B(\sqrt{5}) = 1 \Rightarrow B = \frac{1}{\sqrt{5}}$$

This time substitute in $$x = -\frac{1 +\sqrt{5}}{2}$$:

$$A(-\frac{1 +\sqrt{5}}{2} + \frac{1 - \sqrt{5}}{2}) = 1 \Rightarrow A = -\frac{1}{\sqrt{5}}$$

Putting these values back in we get:

$$F(x) =  -\frac{1}{\sqrt{5}}(-\frac{1}{x + \frac{1 + \sqrt{5}}{2}} + \frac{1}{x + \frac{1 - \sqrt{5}}{2}})$$


## Geometric series

$$\sum_{k=0}^{\infty}ar^k = \frac{a}{1-r}$$

$$-\frac{1}{x + \frac{1 + \sqrt{5}}{2}} = -\frac{1}{x + \frac{1 + \sqrt{5}}{2}}*\frac{\frac{2}{1 + \sqrt{5}}}{\frac{2}{1 + \sqrt{5}}}=-\frac{\frac{2}{1 + \sqrt{5}}}{1+\frac{2}{1 + \sqrt{5}}x}=-\frac{\frac{2}{1 + \sqrt{5}}}{1-(-\frac{2}{1 + \sqrt{5}}x)}$$

$$=-\sum_{k=0}^{\infty}(\frac{2}{1 + \sqrt{5}})(-\frac{2}{1 + \sqrt{5}}x)^k$$


$$\frac{1}{x + \frac{1 - \sqrt{5}}{2}}=\frac{1}{x + \frac{1 - \sqrt{5}}{2}}*\frac{\frac{2}{1-\sqrt{5}}}{\frac{2}{1-\sqrt{5}}}=\frac{\frac{2}{1-\sqrt{5}}}{1+\frac{2}{1-\sqrt{5}}x}=\frac{\frac{2}{1-\sqrt{5}}}{1-(-\frac{2}{1-\sqrt{5}}x)}$$

$$=\sum_{k=0}^{\infty}(\frac{2}{1-\sqrt{5}})(-\frac{2}{1-\sqrt{5}}x)^k$$

## Factor

$$F(x) = -\frac{1}{\sqrt{5}}(-\frac{1}{x + \frac{1 + \sqrt{5}}{2}} + \frac{1}{x + \frac{1 - \sqrt{5}}{2}})$$

$$=-\frac{1}{\sqrt{5}}(-\sum_{k=0}^{\infty}(\frac{2}{1 + \sqrt{5}})(-\frac{2}{1 + \sqrt{5}}x)^k + \sum_{k=0}^{\infty}(\frac{2}{1-\sqrt{5}})(-\frac{2}{1-\sqrt{5}}x)^k)$$

$$=\frac{1}{\sqrt{5}}(-\sum_{k=0}^{\infty}(-\frac{2}{1 + \sqrt{5}})(-\frac{2}{1 + \sqrt{5}}x)^k + \sum_{k=0}^{\infty}(-\frac{2}{1-\sqrt{5}})(-\frac{2}{1-\sqrt{5}}x)^k)$$

$$=\frac{1}{\sqrt{5}}(-\sum_{k=0}^{\infty}(-\frac{2}{1 + \sqrt{5}})^{k+1}(x)^k + \sum_{k=0}^{\infty}(-\frac{2}{1-\sqrt{5}})^{k+1}(x)^k)$$

$$=\frac{1}{\sqrt{5}}(\sum_{k=0}^{\infty}((\frac{2}{1 + \sqrt{5}})^{k+1}- (\frac{2}{1-\sqrt{5}})^{k+1})x^k)$$
