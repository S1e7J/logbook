---
layout: post
title:  "First DP Problems"
date:   2025-03-27 23:39:15 -0500
categories: 
---

## How Much Did I Work Today?

I had classes from 8:00 to 15:30 today, with an hour and a half break in between. That makes 6 hours of classroom work. Additionally, when I got home, I spent 3 extra hours studying dynamic programming. So the total comes to 9 hours of work today.

## What Did I Work On?

As I mentioned, a good portion of today's work was classes. These were quantum physics, statistical physics, and electromagnetism classes. I also attended the university's astronomy group meeting where we had a guest from the National University of Colombia. This guest was responsible for managing and calibrating the radio telescope system and gave one of the most interesting talks I've experienced, sharing many technical details about his work. It was a wonderful presentation.

Beyond this, I decided to study dynamic programming because it's a topic I'd seen in previous semesters and noticed I was starting to struggle with again. So I wanted to refresh my memory and sharpen my skills. For this, I'll be using the DP problem list from [this link](https://algo.monster/problems/dp-list).

## Anything Worth Sharing?

As I mentioned, today's astronomy group talk proved extremely interesting and stimulating. I think I'm passionate about tools and working to make others' jobs easier. I loved how it was presented and I'm fascinated by the technical challenges that needed solving. The speaker was [Javier Sanchez Gonzalez](https://www.researchgate.net/profile/Javier-Sanchez-Gonzalez), who mentioned he'll be defending his thesis soon, so I recommend keeping an eye out for those who might find such topics interesting as it's undoubtedly very exciting.

On another note, while redoing a DP problem today, I decided to check other solutions and came across a theorem I hadn't heard of before but find absolutely fascinating.

It's Legendre's four-square theorem. This theorem essentially states that every natural number can be expressed as the sum of four squared numbers. Or more precisely:

$$\forall x \in N \exists a, b, c, d\in N\ s.t.\ x = a^2 + b^2 + c^2 + d^2$$

This theorem is brilliant in itself. Now, this theorem is clearly non-trivial, so I recommend looking at a proof, like [this one](https://planetmath.org/proofoflagrangesfoursquaretheorem). I prefer not to fill this blog with the proof as I don't think I could simplify it enough for everyone to understand. However, I do want to show how beautiful the algorithm is.

The following code returns the minimum number of squared terms we need to sum to get a number n. That is, it tells us how many of the numbers $$a, b, c, d$$ in the above representation are non-zero:

```c
#include <math.h>

int isSquare(int n) {
    int r = sqrt(n);
    return r * r == n;
}

int numSquares(int n) {
    if (isSquare(n)) return 1;

    int t = n;
    while (t % 4 == 0) {
        t /= 4;
    }
    if (t % 8 == 7) return 4;

    for (int i = 1; i * i <= n; i++) {
        if (isSquare(n - i*i)) return 2;
    }

    return 3;
}
```

This code seems extremely beautiful to me because it simply checks case by case while leveraging the theorem. Let's look at what it does step by step:

```c
int isSquare(int n) {
    int r = sqrt(n);
    return r * r == n;
}
```

This function essentially tells us if a number is a perfect square. It does this by getting the square root and approximating it to an integer. When we square it, since we know r is the square root of n, the only way $$r*r == n$$ holds true is if $$r$$ was an integer to begin with.

```c
    if (isSquare(n)) return 1;
```

This first case checks if the number $$n$$ is itself a perfect square. In that case, we know the only number we need is $$\sqrt{n}^2$$, so we return 1.

```c
    int t = n;
    while (t % 4 == 0) {
        t /= 4;
    }
    if (t % 8 == 7) return 4;
```

This part checks if the number can be expressed as $$4^k*(8*m + 7)$$. It first removes all $$4^k$$ factors through iteration until only the remainder is left, which should equal $$7$$ modulo 8.

The reason we care about this formula relates to another theorem known as Legendre's three-square theorem, which essentially states that a number requires 3 squares if and only if it doesn't satisfy this formula. We know in this case the answer must be 4.

```c
    for (int i = 1; i * i <= n; i++) {
        if (isSquare(n - i*i)) return 2;
    }
```

This simply checks if subtracting a perfect square from the original number happens to leave another perfect square, meaning it can be expressed as two squares.

After all these checks, it defaults to returning 3 if none of the conditions are met.

As you can see, this code is truly brilliant and I found it to be a great improvement over the DP solution I had originally implemented for this problem.

I think it's a great demonstration that learning pays off and that one can find increasingly elegant solutions as one gains more knowledge.

## Cool Links?

* [Algo DP List](https://algo.monster/problems/dp-list)
* [Javier Sanchez Gonzalez](https://www.researchgate.net/profile/Javier-Sanchez-Gonzalez)
* [Proof](https://planetmath.org/proofoflagrangesfoursquaretheorem)
