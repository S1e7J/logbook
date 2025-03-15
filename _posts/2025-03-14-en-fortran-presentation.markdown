---
layout: post
title:  "Fortran: A Beginning on the Path"
date:   2025-03-14 21:55:00 -0500
categories: EN CS
---

## How Much Did I Work Today?

Today wasn't particularly dedicated to work. I took it easy and focused on staying relaxed. I still have assignments to submit for university, but I wanted to rest a bit after what turned out to be an intense week.

## What Did I Work On?

Today I studied Fortran, spending the day learning its syntax and comparing its efficiency with C. It turned out to be a very different experience from what I expected. Besides that, my other projects included starting an entry for my Blog that will serve as a script for a video I plan to upload eventually. I also started looking at ways to create fractals that I can save, and considered the idea of creating a Mastodon account where I can share not only these writings but also the mathematical images I create and the videos I record. I didn't do any of this very formally, but I hope to share more details here in the future about how it turns out.

## Anything Worth Sharing?

The most important thing I did today was study Fortran. Therefore, I'm going to share a bit about my plan for learning Fortran and why it's important for me to learn it well.

The first thing I did was visit the official [Fortran](https://fortran-lang.org/learn/) page. There I learned the basics of any language: how its syntax works, what types it has, how they look in memory. I followed each of the code snippets in this guide and with that I started looking for ways to learn.

Then I found the [Project Euler](https://projecteuler.net) page. This is a list of problems with solutions. Let's do the first problem right here since it turns out to be super simple:

The statement is:

_If we list all the natural numbers below 10 that are multiples of 3 or 5,_
_we get 3, 5, 6 and 9. The sum of these multiples is 23. Find the sum of all_
_the multiples of 3 or 5 below 1000._

This is a really simple problem. In fact, I was able to write a solution in C in less than 2 minutes. It ended up something like this:

```c
#include <stdio.h>
int main() {
    int result = 0;
    for (int i = 0; i < 1000; i++) {
        if (i % 3 == 0 || i % 5 == 0) result = result + i;
    }
    printf("%d\n", result);
}
```

This is an extremely simple code that only goes from `0` to `999` and asks in each case if when dividing by `3` or by `5` the remainder is `0`. If so, it adds the value to the result and finally prints how much it summed.

After this, when I had already verified that I understood the problem, I tried to make a solution but now with Fortran. From which I got two results.

```fortran
program name
        implicit none
        integer :: result, i
        result = 0
        do i = 1, 999
                if (MOD(i, 3) == 0 .or. MOD(i, 5) == 0) then
                        result = result + i;
                end if
        end do

        print *, result
                
end program name
```

This is a direct translation of my C solution. It doesn't do absolutely anything more. This translation returned exactly the same result, and with that I could be confident that it worked.

After this, I decided to use a new option that Fortran had and that I found very appealing because it looked really simple, and with that I got the following result:

```fortran
program name
        implicit none
        integer :: result, i
        result = 0;
        do concurrent (i = 1:999:3)
                result = result + i;
        end do

        do concurrent (i = 1:999:5)
                if (MOD(i, 3) /= 0) result = result + i;
        end do

        print *, result

end program name
```

Ok... now we're talking about something more interesting. Suddenly the solution feels very similar but essentially different. What we're doing here is having two iterators. The first goes from `1` to `999` taking steps of `3`, that is, it goes in `1, 3, 6, 9, ...` with that we ensure that all values are multiples of 3. Therefore, we can add absolutely all the values that we iterate here. After this there is another cycle that this time takes steps of `5`. However, here we have to make a small check, which is that we haven't added it before (that is, that it's not also a multiple of 3). All this would have worked essentially the same in `C`, but the thing I really wanted to try was that concurrent. I still owe myself to find out what concurrent exactly does and maybe I should go look at the documentation more, but in my current understanding (which is probably wrong), what it does is that these two cycles are executed in parallel. That sounds great without a doubt and I'm surprised how easy it is. I have my doubts that it's really doing anything in this context because there are many things that don't make sense to me and that in other languages would have shot me in the foot. For example, the fact that I'm iterating over the same variable could cause conflicts in other programs and values could change in the middle of execution. However, I haven't done enough research to ensure anything. It's probably something I should verify better.

In the end I did several exercises like this and I'm currently solving a problem that has me thinking about their implementation of integers because I need to access an integer of at least 64 bytes and I'm not sure how to do it. But I'll talk about that later when it turns out it wasn't as strange as I expected, or maybe I'll just implement my own integer type to solve it. I'm not sure yet. But well, I guess I'll tell you about it here in the future.

## Cool Links?

All the links I would like to share today are already up there, but here I put them a little more organized.

* [Fortran](https://fortran-lang.org/learn/)
* [Project Euler](https://projecteuler.net)
