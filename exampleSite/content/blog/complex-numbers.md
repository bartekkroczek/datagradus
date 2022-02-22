---
title: Five faces of complex numbers
author: Bartek Kroczek
date: '2021-01-29'
slug: five-faces-of-complex-numbers
categories: []
tags: []
subtitle: 'A brief preparation for understanding the Fourier Transform'
summary: ''
authors: []
lastmod: '2022-01-29T14:52:06+01:00'
featured: no
image:
  caption: ''
  focal_point: ''
  preview_only: no
projects: []
---


## Disclaimer
The purpose of this article is to briefly and intuitively recall the most important
properties of complex numbers. These concepts are necessary to understand the Fourier
transform, which I deal with in my other posts. However, please note that intuitiveness
is more important to me than puritanism, which may lead to shortcuts uncomfortable for
theoretical mathematicians.


## A simple question that leads to a complex problem
It’s usually doesn’t works that way, but the story of the complex number is driven 
by a simple idea applied to an even simpler equation:

$$ f(x) = x^2 + 1$$

Of course, this equation has no solution on the plane of real numbers, which can 
be easily checked by looking at the graph.

![Quadratic function plot, like in a formula above](img/x2plus1.svg)

But what happened when we forget about the traditional math and solve the equations above
as $\sqrt{-1}$? It turns out that adding such a quantity (usually denoted as $i$) to the
rational numbers leads to the creation of a numerical system full of interesting and 
useful properties, like a **field structure** [^1], which informally means that all classical 
algebraic operations are allowed.

What’s more this field is **algebraically closed**[^2] which - in relation to complex numbers 
- means that 
**every non-constant single-variable polynomial with complex coefficients has at least one complex root**. In the world of complex numbers, any equation is solvable! 
This statement is so important that we call this **Fundamental Theorem of Algebra**[^3] 

## Complex number representation

Complex numbers can be presented in various forms, each of them allows you to use their 
different properties.

### Algebraic (canonical) form

Let’s define a complex number as $z = a + bi$ where, $a, b \in \mathbb{R}$ (are rational) and 
$i = \sqrt{-1}$ as described above.

Basic algebraic operations look as follow:

$$ (a + bi) + (c + di) = (a +c) + (b+d)i $$
$$(a+bi) \cdot (c+di) = ac + ibc + aid + ibid  = ac + i (bc + ad) + i^2 bd = (ac-bd) + i(bc+ad)$$
$$\frac{a+bi}{c+di}  = \frac{ac + bd}{c^2 + d^2} + i \frac{bc-ad}{c^2 + d^2}, c^2 + d^2 \not = 0$$

What’s more interesting, each complex number (and it’s inverse) has root in the form:

$$a + bi = \bigg ( \sqrt{a + \sqrt{a^2 + b^2}} + i\sqrt{\frac{1}{2} (-a + \sqrt{a^2+b^2})} \bigg ) ^2$$

This form allows for convenient counting using complex numbers.

### Ordered pairs

Complex numbers may be introduced as the set of pairs of real numbers, $(a, b) \in \mathbb{R}^2$.
Please note, that this is this same $a$ and $b$ like in $z = a+bi$, so the relation between 
pairs and algebraic representation is trivial. This form is useful for
**formal construction of complex numbers**[^4] and introduces an idea of representing a complex 
number as a point in two-dimensional space, which leads to geometrical interpretation.
 
 ![Point (a, b) in a Real x Imaginary Cartesian space](img/ab.svg)
 
 #### Algebraic operations have very nice interpretations on the Cartesian plane.
 
 * Addition follows the known parallelogram rule for vectors
 ![Graphics form of adding rule](img/add.svg)
 * Multiplying by $i$ is a 90-degree ($\frac{\pi}{2}$) rotation.
 ![Rotation as multiplication](img/circle.svg)
 Note that from this perspective $ i^2 = -1$ makes perfect sense.
 
 Any other multiplication is just a rotation in point $(0,0)$ by some angle (described in the 
 next paragraph) and rescaling (stretch or shorten) of the vector.
 
 ### Polar coordinates
 
 The rotation angle announced above is written as $\theta$, and the scaling factor is called $r$.
 ![Polar coordinates to point convertion](img/ang.svg)
 
 The relationship between the algebraic and trigonometric notations is only slightly more 
 complicated, and requires some basic knowledge of trigonometry.
 
 For $z = a + bi$ $r$ is calculated using the Pythagorean theorem.

$$ r = \sqrt{a^2 + b^2} $$

In turn, $\theta$ is just a definition of the inverse of the tangent ($arctg$)

$$ \theta = arctg(\frac{b}{a}) $$

Importantly, note that again we are dealing with a pair of values, so the correct notation 
is: $z = (r, \theta)$

 This character is convenient because it makes multiplication so much easier:
 
 $$ (r_1, \theta_1) \cdot (r_2, \theta_2) = (r_1 r_2, \theta_1 + \theta_2) $$
 
 It is also a bridge to more sophisticated representations.
 
 
### Trigonometric representation
But how do you express a complex number using polar coordinates but as one number 
( not a pair, analogus to  $z = a + bi$) ?
Once again, trigonometry comes in handy, namely the definition of 
the sine and cosine functions.</p>

By definition:

$$sin (\theta) =\frac{b}{r}, cos (\theta) = \frac{a}{r}$$

so

$$a = r cos(\theta) , b = r sin(\theta)$$

Substituting the values calculated above into the equation $z = a + bi$ we get:

$$z = a + bi = r cos (\theta) + i r sin (\theta) = r \big ( cos (\theta) + i sin (\theta) \big )$$

This form, although very useful (it is embedded in the Fourier transform itself), is not 
convenient for counting. However this problem can be solved by a clever trick, what the next
paragraph will be about.

### Exponential form

We need to start with a few words about **Taylor series**[^5].

It’s a tool for expressing any function is some a form of polynomial

$$ f(a)+\frac {f'(a)}{1!} (x-a)+ \frac{f''(a)}{2!} (x-a)^2+\frac{f'''(a)}{3!}(x-a)^3+ \cdots $$

or in short:

$$ \sum_{n=0} ^ {\infty} \frac {f^{(n)}(a)}{n!} (x-a)^{n} $$

When we use a finite number of elements of the sum, the taylor series becomes an approximation
of the original function around point $a$. The closer to point $a$ is the value of the function 
we calculate, the smaller the error of the approximation will be. Taylor series expressing 
with $a = 0$ is called **Maclaurin series**[^6]. 

$$\sum_{n=0} ^ {\infty} f^{(n)}(0) \frac {x^n}{n!} =  f(0)+\frac {f'(0)}{1!} (x)+ \frac{f''(0)}{2!} (x)^2+\frac{f'''(0)}{3!}(x)^3+ \cdots$$

What happens when we try to expand the sine and cosine functions into a Maclaurin series?
Let’s start with calculating derivatives:


![Sin and Cos derivatives](img/prims.svg)

We can see that the cycle repeats itself from the fourth derivative. 
Expanding the sine and cosine functions into the Taylor series looks like this:

$$\sin x = \sum^{\infty}_{n=0} \frac{(-1)^n}{(2n+1)!} x^{2n+1} = x - \frac{x^3}{3!} + \frac{x^5}{5!} - \cdots $$

$$ \cos x = \sum^{\infty}_{n=0} \frac{(-1)^n}{(2n)!} x^{2n} = 1 - \frac{x^2}{2!} + \frac{x^4}{4!} - \cdots $$

## The magic begins

Let’s recall the definition of the exponential function
$$ e^x := \sum_{k = 0}^{\infty} \frac{x^k}{k!} = 1 + x + \frac{x^2}{2} + \frac{x^3}{3!} + \frac{x^4}{4!} + \cdots $$

Note that this definition looks similar to taylor series expansions!
If we substitute $x = i\theta$, even more similarities arise.

$$ e^{i\theta} =  1 + i\theta + \frac{(i\theta)^2}{2} + \frac{(i\theta)^3}{3!} + \frac{(i\theta)^4}{4!} + \cdots = 1 + i\theta - \frac{\theta^2}{2} -i \frac{\theta^3}{3!} + \frac{\theta^4}{4!} + \cdots $$ 

When we group the elements of the sum so that all real and all imaginary are next to each other 
and take $i$ in front of the parenthesis $\cdots$

$$ \bigg(1 - \frac{\theta^2}{2}  + \frac{\theta^4}{4!} - \frac{\theta^6}{6!}+  \dots \bigg ) + i \bigg (\theta - \frac{\theta^3}{3!} + \frac{\theta^5}{5!} - \frac{\theta^7}{7!} +\dots \bigg ) $$

$\cdots$ it turns out that the following equality is true:

$$ e^{i\theta} = cos(\theta) + i sin(\theta) $$ 

If that wasn’t neat enough if we substitute $\pi$ for $\theta$ we get:

$$ e^{\pi i } +1 = 0$$ 

What we call the **Euler’s identity**[^7], which is widely recognized as one of the most 
beautiful equations in all of mathematics.

Finally, we have to go back to the trigonometric form of complex numbers

$$ z = a + bi = r cos (\theta) + i r sin (\theta) = r \big ( cos (\theta) + i sin (\theta) \big ) = re^{i\theta} $$ 

## Conclusion

I believe that understanding the relationship between the different forms of complex numbers is 
crucial to understanding the technical details behind the **Fourier Transform**. 

## References
[^1]: https://en.wikipedia.org/wiki/Complex_number#Relations_and_operations 
[^2]: https://en.wikipedia.org/wiki/Algebraically_closed_field
[^3]: https://en.wikipedia.org/wiki/Fundamental_theorem_of_algebra
[^4]: https://en.wikipedia.org/wiki/Complex_number#Formal_construction
[^5]: https://en.wikipedia.org/wiki/Taylor_series
[^6]: https://en.wikipedia.org/wiki/Colin_Maclaurin#Contributions_to_mathematics
[^7]: https://en.wikipedia.org/wiki/Euler%27s_identity
 
