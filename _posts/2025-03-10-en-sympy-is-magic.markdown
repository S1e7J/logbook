---
layout: post
title:  "Sympy is Magic for Physics"
date:   2025-03-10 23:30:00 -0500
categories: EN Physics
---

## How much did I work?

I worked for a total of 10 hours today, from 10:00 to 23:30,
the time when I began writing this entry.

## What was I working on?

Being completely honest there were two big projects today. The first was my
third quantum mechanics homework. This was a really long
task and the reason why I named this entry like I did. The second major task was
this logbook. Coming with what was the format I wanted to work with and
getting all the tools I would need took me actually 2 hours so I consider it a
big project for the day.

## Something worty to Share?

The biggest thing I learned today was about Sympy. I was making a homework from
my quantum mechanics class (I'm not sure if I can share the work I made but
I'll ask tomorrow after class) but some of it were really hard to get along
without some computational help. For an example let's just see the
Associated Legendre polynomials. They're defined as:

$$
P_\ell^m \left( x \right) = \frac{\left( -1 \right)^m}{2^\ell \ell!}
\left( 1 - x^2 \right)^{\frac{m}{2}} \frac{d^{\ell + m}}{dx^{\ell + m}}
\left[ \left( x^2 - 1 \right)^\ell \right]
$$

so long it didn't seem hard or tiring. However I was needing $$\ell = 3; m = 3$$.
A 6th derivative is really the kind of thing you don't want to do by hand. So I get
to study Sympy once again and in a little time I came with this code

```python
def differentiate_n(n, expr, s=x):
    res = expr
    for _ in range(n):
        res = sp.diff(res, s)
    return sp.simplify(res)


def asociado(ell, m, s=x):
    first_factor = (-1)**m/(2**ell * sp.factorial(ell))
    second_factor = (1 - s**2)**(m/2)
    expr = (s**2 - 1)**ell
    tird_factor = differentiate_n((ell + m), expr, s=s)
    return first_factor * second_factor * tird_factor
```

the code is straightforward. If you know almost anything about sympy you
could see that this is almost a 1 to 1 translation. Of course this code is not
pretty and it almost non-reusable in other context but I wasn't aming for code
quality or prettines. I was looking for a little script that save me the trouble
of making a derivation 6 times. There are many examples like this in almost every
single point I make in this homework and doing it with Sympy really simplifies
my day by saving me the cost of making some mathematical problem by hand.

I can assure you this is not some kind of magical way to solve all of your problems.
After all I still needed more than 5 hours to solve some of the problems in this
homework even with the help of Sympy. However, I don't think I would be able to
end this assignment on time if it wasn't for sympy (and that is kind of magical).

## Cool Links?

* [Sympy](https://www.sympy.org/)
* [My Scripts](https://github.com/S1e7J/Cuantica_Tarea_3)
* [Associated Legendre Polynomials](https://en.wikipedia.org/wiki/Associated_Legendre_polynomials)
