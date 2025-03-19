---
layout: post  
title: "Gleam FFI First Look"  
date: 2025-03-18 22:36:28 -0500  
categories:  
---  

## How much did I work?  

Today was not a particularly busy day. I only worked 3 hours.  

## What was I working on?  

Today I learned a little about Erlang and Gleam FFI. I wanted to learn Erlang for quite some time, but I didn't have time until now. One of the things I really like about Gleam is how easily you can make an interface between itself and the target that you run.  

That way, you can use libraries from other languages, and you can even use Erlang’s NIF for using other languages. For example, you can bind Rust or C just by compiling to the correct target.  

I think this is a way to make a language in which access to other functionality is really great, and you can use the best tool for the job in every case. Because the moment you encounter some problem, you could simply translate it to another tool if it happens to be too difficult for Gleam.  

## Something worthy to share?  

The FFI in Gleam was a really nice surprise because it lets me do almost anything—even things that aren't trivial in the language using some other language for its purpose. Let's look at an example of how you can do that.  

First of all, a little disclaimer. This will not be a great example, just because the function I program in other languages here would be fairly easy to make in Gleam. However, imagine you are dealing with some non-trivial problem and take this with a grain of salt.  

First of all, let's look at the other function’s code. We will begin with Erlang:  

```erlang  
-module(play_ground_ffi).  
-export([fac/1]).  

fac(N) when N =< 1 ->  
  1;  
fac(N) ->  
  N * fac(N - 1).  
```  

Put this code in the file `src/play_ground_ffi.erl` in the Gleam project. This is fairly simple Erlang code. The only thing it does is calculate the factorial of a number. When the number is 1 or less, it returns 1, and when it is bigger, it returns the multiplication between its number and the result of the function with one number less. Let's see an example:  

```
= factorial(4)  
= 4 * factorial(3)  
= 4 * 3 * factorial(2)  
= 4 * 3 * 2 * factorial(1)  
= 4 * 3 * 2 * 1  
= 24  
```

This is the definition of recursion, and I wanted to make this clear just so you can understand what this code does. You also need to put this in a file for JavaScript because Gleam can target both languages (which I think is super cool, to be honest). Let's see how this code looks in JavaScript.  

```javascript  
export function fac(N) {  
  if (N <= 1) {  
    return 1;  
  }  
  return N * fac(N - 1);  
}
```  

Also, really simple code that does the same thing. Now, how can I call this code from Gleam? Just use the `@external` decorator.  

```gleam  
import gleam/io  

@external(javascript, "./play_ground_ffi.mjs", "fac")  
@external(erlang, "play_ground_ffi", "fac")  
pub fn fac(n: Int) -> Int  

pub fn main() {  
  io.debug(fac(4))  
}
```  

What this means is that the function `fac` in this code is actually the function `fac` in Erlang or in JavaScript accordingly to the compile target. Now you can use this function without a problem. I think this is really cool and makes the work of making bindings really simple for Gleam. Now, to run this, you could just compile it and run:  

```bash  
❯ gleam run  
  Compiling play_ground  
   Compiled in 0.58s  
    Running play_ground.main  
24  
```  

And also:  

```bash  
❯ gleam run --target javascript  
  Compiling play_ground  
   Compiled in 0.07s  
    Running play_ground.main  
24  
```  

Really cool, though. I have studied more about Erlang, but I haven’t finished its documentation yet. I will probably talk more about it because it is one of the most interesting languages I have found, but not for now.  

## Cool Links?  

* [Erlang QuickStart](https://www.erlang.org/doc/system/getting_started.html)  
* [Blog Post for Gleam FFI](https://www.jonashietala.se/blog/2024/01/11/exploring_the_gleam_ffi/)  
