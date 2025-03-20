---

layout: post  
title:  "teenytiny: Learning from Compilers"  
date:   2025-03-19 23:36:09 -0500  
categories:   
---

## How Much Did I Work Today?

Today was an intense day. I worked at least 8 hours.

## What Did I Work on Today?

I took advantage of having time since I'm on a break from university and decided to work on the frontend of a compiler. It was something I had wanted to do for a long time, and it turned out to be much less work than I expected for such a simple program.

This time, since it was my first time, I must confess that I followed this [tutorial](https://austinhenley.com/blog/teenytinycompiler1.html), but I commit to repeating this first for a Brainfuck interpreter in Gleam and then repeating this process to transpile simple Python code to Fortran or C, so I can face this challenge again and really learn it well.

## Anything Worth Sharing?

The truth is that what I have to share that I found extremely interesting is how easy it is to transpile. It's really simple to analyze each term of every word to create useful structures. I'm also surprised by how important recursion is in this process, and how happy that makes me. I think I can appreciate how fabulous it is.

In addition to that, I’ll brag a little about my transpiler. Imagine we have the following script:
```basic
PRINT "How many fibonacci numbers do you want?"
INPUT nums
PRINT ""

LET a = 0
LET b = 1
WHILE nums > 0 REPEAT
    PRINT a
    LET c = a + b
    LET a = b
    LET b = c
    LET nums = nums - 1
ENDWHILE
```

This code doesn't do anything special. It simply calculates Fibonacci numbers. Now, if we pass this through the transpiler, we get:
```c
#include <stdio.h>
int main(void) {
float nums;
float a;
float b;
float c;
printf("How many fibonacci numbers do you want?\n");
if(0 == scanf("%f", &nums)) {
nums = 0;
scanf("%*s");
}
printf("\n");
a = 0;
b = 1;
while (nums>0){
printf("%.2f\n", (float)(a));
c = a+b;
a = b;
b = c;
nums = nums-1;
}
return 0;
}
```

Which is unformatted code. Let me tidy it up a bit:
```c
#include <stdio.h>
int main(void) {
    float nums;
    float a;
    float b;
    float c;
    printf("How many fibonacci numbers do you want?\n");
    if(0 == scanf("%f", &nums)) {
        nums = 0;
        scanf("%*s");
    }
    printf("\n");
    a = 0;
    b = 1;
    while (nums>0){
        printf("%.2f\n", (float)(a));
        c = a+b;
        a = b;
        b = c;
        nums = nums-1;
    }
    return 0;
}
```

And these two codes are exactly the same. There's nothing particularly strange about this code. It simply calculates the Fibonacci value. It turned out to be a really fun project.

## Cool Links?

* [tutorial](https://austinhenley.com/blog/teenytinycompiler1.html)
* [My Implementation](https://github.com/S1e7J/TeenyTiny.git)

