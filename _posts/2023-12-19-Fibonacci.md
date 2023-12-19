---
layout: post
title: Fibonacci Numbers
author: Charles Thomas
---

# What are the Fibonacci numbers?
Fibonacci numbers are the sequence of numbers: 

$$1, 1, 2, 3, 5, 8, 13...$$

We define these starting with $$1,1$$ then every number afterwards is the sum of the previous two. 
So the third number is 

$$1 + 1 = 2$$

And the fourth is 

$$1 + 2 = 3$$

We can write this as using the following formula: 

$$f_n = f_{n-1} + f_{n-1}$$

# Recursive code
When you're first learning to program you may have written some code to calculate the find the nth fibonacci number.

```
def find_nth_fib(n):
    if n == 1:
        return 1
    if n == 2:
        return 1

    return find_nth_fib(n-1) + find_nth_fib(n-2)
```

The code above works by computing all the previous fibonacci numbers in order to find the one you're looking for.

# Is there another way?
However, there is a way of calculating the nth fibonacci number directly and it's given by this formula:

$$
\frac{1}{\sqrt{5}}((\frac{1 + \sqrt{5}}{2})^n - (\frac{1 - \sqrt{5}}{2})^n)
$$

# Proof of it
This formula looks really random so let's walk through the proof of it to see where it comes from.

## Define series $$F_n$$
To prove this formula we'll start by defining the following series:

$$
F(x) = \sum_{i=0}^{\infty}f_{i+1}x^i
$$

Where 

$$f_i$$ 

is the ith fibonacci number.


## Construct other series
Now let's construct two other related series: 

$$xF(x) = \sum_{i=0}^{\infty}f_{i+1}x^{i+1}$$ 

and 

$$x^2F(x) = \sum_{i=0}^{\infty}f_{i+1}x^{i+2}$$

## Take difference

Now let's note that

$$
F(x) - xF(x) - x^2F(x)
= F(x)(1 - x - x^2)
$$

Now let's write this a different way

$$F(x) - xF(x) - x^2F(x)$$

$$= f_1 + f_2x + ... + f_nx^{n-1} - (f_1x + f_2x^2 + ... + f_nx^{n}) - (f_1x^2 + f_2x^3 + ... + f_nx^{n+1})$$

$$= f_1 + (f_2 - f_1)x - (f_3 - f_2 - f_1)x^2 + ... + (f_n - f_{n-1} - f_{n-2})x^{n-1}$$

We now remember that

$$f_n = f_{n-1} + f_{n-2}$$ 

so all but the first two terms go to zero leaving:

$$=  f_1 + (f_2 - f_1)x$$

Next, we use the fact that

$$f_2 = f_1 = 1$$ 

to get 

$$= 1 + (1-1)x = 1$$

So after all that we get

$$F(x) - xF(x) - x^2F(x) = F(x)(1 - x - x^2) = 1$$

$$F(x) = \frac{1}{1 - x - x^2}$$

## Finding roots
We can solve this quadratic equation using the quadrartic formula

$$x = \frac{-b \pm \sqrt{b^2 - 4ac}}{2a}=\frac{1 \pm \sqrt{1 + 4}}{-2}$$

This means we can factor our equation it into:

$$1- x - x^2 = -(x + \frac{1 + \sqrt{5}}{2})(x + \frac{1 - \sqrt{5}}{2})$$

So we can write:

$$F(x) = \frac{1}{1 - x - x^2} = -\frac{1}{(x + \frac{1 + \sqrt{5}}{2})(x + \frac{1 - \sqrt{5}}{2})}$$

## Write as partial fractions
The next step is to use partial fractions to split out this nasty looking denominator into the the sum of two terms:


$$F(x) = - (\frac{A}{x + \frac{1 + \sqrt{5}}{2}} + \frac{B}{x + \frac{1 - \sqrt{5}}{2}})$$

To find A and B we know that:

$$A(x + \frac{1 - \sqrt{5}}{2}) + B(x + \frac{1 + \sqrt{5}}{2}) = 1$$

This most hold for all x, so we can specific x to make this calculation easy. We'll pick

$$x = -\frac{1 - \sqrt{5}}{2}$$

Putting this in we get:

$$B(-\frac{1 - \sqrt{5}}{2} + \frac{1 + \sqrt{5}}{2}) = B(\sqrt{5}) = 1$$

This means that

$$B = \frac{1}{\sqrt{5}}$$

We'll do a similar thing again but this time use

$$x = -\frac{1 +\sqrt{5}}{2}$$

So we get

$$A(-\frac{1 +\sqrt{5}}{2} + \frac{1 - \sqrt{5}}{2}) = 1 \Rightarrow A = -\frac{1}{\sqrt{5}}$$

Putting these values back in we get:

$$F(x) =  -\frac{1}{\sqrt{5}}(-\frac{1}{x + \frac{1 + \sqrt{5}}{2}} + \frac{1}{x + \frac{1 - \sqrt{5}}{2}})$$


## Geometric series
Now we have nice expression for F(x) but we wanted to be able to work out the coeffecients of each term rather than just the value of the series. Luckily, we can do some clever rewriting.

There is a famous series called the Geometric Series given by:

$$\sum_{k=0}^{\infty}ar^k = \frac{a}{1-r}$$

We can use this to rewrite our expression from the previous section. Starting with

$$-\frac{1}{x + \frac{1 + \sqrt{5}}{2}}$$

We can rewrite it as:

$$= -\frac{1}{x + \frac{1 + \sqrt{5}}{2}}*\frac{\frac{2}{1 + \sqrt{5}}}{\frac{2}{1 + \sqrt{5}}}=-\frac{\frac{2}{1 + \sqrt{5}}}{1+\frac{2}{1 + \sqrt{5}}x}=-\frac{\frac{2}{1 + \sqrt{5}}}{1-(-\frac{2}{1 + \sqrt{5}}x)}$$

This means it is now in the right form to apply the geometric series so we get:

$$=-\sum_{k=0}^{\infty}(\frac{2}{1 + \sqrt{5}})(-\frac{2}{1 + \sqrt{5}}x)^k$$

We can now do the same thing for:

$$\frac{1}{x + \frac{1 - \sqrt{5}}{2}}$$

Which gives us:

$$\frac{1}{x + \frac{1 - \sqrt{5}}{2}}=\frac{1}{x + \frac{1 - \sqrt{5}}{2}}*\frac{\frac{2}{1-\sqrt{5}}}{\frac{2}{1-\sqrt{5}}}=\frac{\frac{2}{1-\sqrt{5}}}{1+\frac{2}{1-\sqrt{5}}x}=\frac{\frac{2}{1-\sqrt{5}}}{1-(-\frac{2}{1-\sqrt{5}}x)}$$

$$=\sum_{k=0}^{\infty}(\frac{2}{1-\sqrt{5}})(-\frac{2}{1-\sqrt{5}}x)^k$$

## Factor
Finally, we can take these two new expressions we found and put them back in. So

$$F(x) = -\frac{1}{\sqrt{5}}(-\frac{1}{x + \frac{1 + \sqrt{5}}{2}} + \frac{1}{x + \frac{1 - \sqrt{5}}{2}})$$

becomes

$$=-\frac{1}{\sqrt{5}}(-\sum_{k=0}^{\infty}(\frac{2}{1 + \sqrt{5}})(-\frac{2}{1 + \sqrt{5}}x)^k + \sum_{k=0}^{\infty}(\frac{2}{1-\sqrt{5}})(-\frac{2}{1-\sqrt{5}}x)^k)$$

Next, we'll get the x on it's own

$$=\frac{1}{\sqrt{5}}(-\sum_{k=0}^{\infty}(-\frac{2}{1 + \sqrt{5}})(-\frac{2}{1 + \sqrt{5}}x)^k + \sum_{k=0}^{\infty}(-\frac{2}{1-\sqrt{5}})(-\frac{2}{1-\sqrt{5}}x)^k)$$

$$=\frac{1}{\sqrt{5}}(-\sum_{k=0}^{\infty}(-\frac{2}{1 + \sqrt{5}})^{k+1}(x)^k + \sum_{k=0}^{\infty}(-\frac{2}{1-\sqrt{5}})^{k+1}(x)^k)$$


Finally, we'll combine the two sums to get:

$$=\frac{1}{\sqrt{5}}(\sum_{k=0}^{\infty}((\frac{2}{1 + \sqrt{5}})^{k+1}- (\frac{2}{1-\sqrt{5}})^{k+1})x^k)$$

## Getting the Fibonacci numbers back out

We know have a complicated looking expression but what does it have to do with the fibonacci numbers. We'll remember that:

$$
F(x) = \sum_{i=0}^{\infty}f_{i+1}x^i
$$

So comparing it to

$$F(x) =\frac{1}{\sqrt{5}}(\sum_{i=0}^{\infty}((\frac{2}{1 + \sqrt{5}})^{i+1}- (\frac{2}{1-\sqrt{5}})^{i+1})x^i)$$

We see that 

$$f_{i+1} = (\frac{2}{1 + \sqrt{5}})^{i+1}- (\frac{2}{1-\sqrt{5}})^{i+1}$$

which completes our proof

## Bonus: proof that $$F_n$$ converges

We've completed the main body of our proof but for some of our steps we treated F(x) just like a number. But it is really an infinite sum

Most of these infinite sums just get infinitely big or infinitely small (we say these sums are divergent). So when working with them, we have to be careful as some steps are not justified.

Thankfully, the sum we have defined above actually becomes a number (we say it converges to a number) so long as

$$|x| < \frac{1}{2}$$ 

so we can work with it nicely.

To finish off our proof we will check that F(x) converges

To prove our series $$F(x)$$ is convergent. We'll use a common technique: showing that the terms of our series is smaller than the terms of some other series. Then showing that the other series converges. To do this we'll need two convergence tests

### Ratio Test 
For a series: 

$$\sum_{n=0}^{\infty}a_n$$

The ratio test looks at the ratio between adjacent terms: 

$$|\frac{a_{n+1}}{a_n}|$$

And then takes the limit as we go to infinity

$$\lim_{n \rightarrow \infty} |\frac{a_{n+1}}{a_n}|$$

This tells us if the terms eventually stay close to each and the series converges or not. Formally it says:


$$
\lim_{n \rightarrow \infty} |\frac{a_{n+1}}{a_n}| < 1
$$ 

then the series converges

$$
\lim_{n \rightarrow \infty} |\frac{a_{n+1}}{a_n}| = 1
$$ 

then the test doesn't tell you one way or the other.

$$
\lim_{n \rightarrow \infty} |\frac{a_{n+1}}{a_n}| > 1
$$ 

then the series is divergent

### Comparison Test
Another useful way to work out if a series converges is the comparison test

If we have the series of positive numbers 

$$\sum_{n=0}^{\infty}a_n$$ 

and a convergent series of positive numbers 

$$\sum_{n=0}^{\infty}b_n$$ 

and after some point in the series: 

$$
|a_n| \leq |b_n|
$$

then $$\sum_{n=0}^{\infty}a_n$$ also converges

### $$2^n$$ series
Now we can prove that F(x) converges

Consider the series 

$$\sum_{n=0}^{\infty}(2x)^n$$

We can show that 

$$f_n \leq 2^n$$

by applying induction.

For the case $$n = 1$$ we have 

$$f_n = 1$$, $$2^1 = 2$$ and $$1 < 2$$

Now we assume it for $$n = k$$, so we have 

$$f_k < 2^k$$

Next, we consider $$n = k+1$$, 

$$f_{k+1} = f_k + f_{k-1}$$ 

Which by our assumption: 

$$f_k + f_{k-1} < 2^{k} + 2^{k-1} = 2^{k-1}(2 + 1) = 2^{k-1} * 3 < 2^{k-1} * 4 = 2^{k-1} * 2^2 = 2^{k+1}$$

So now we need to show that 

$$\sum_{n=0}^{\infty}2^n$$

is convergent.

To do this we apply the ratio test:

$$
\lim_{n \rightarrow \infty} |\frac{(2x)^{n+1}}{(2x)^n}| 
=\lim_{n \rightarrow \infty} |(2x)^n| 
$$

Now $$
|(2x)^n| = |2^n x^n|  < 1
$$ only if $$x < \frac{1}{2}$$

Therefore our series $$F_n(x)$$ converges if $$x < \frac{1}{2}$$
