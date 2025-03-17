---  
layout: post  
title: "Beauty in Some Moments"  
date: 2025-03-16 23:45:43 -0500  
categories:  
---  

## How Much Did I Work Today?  

Today, I worked only 3 hours. I think that's fine for a weekend, and honestly, those 3 hours were quite productive. Besides that, I started a small project to try out Gleam as a language, which I didn’t count as part of my working hours.  

## What Did I Work on Today?  

Today, I worked on statistical physics. I haven’t finished yet, but I made progress on one and a half points. If you read yesterday’s entry, you can probably imagine what it was like since it wasn’t very different.  

In addition to that, I started writing a small piece of code for a browser following this [guide](https://browser.engineering/). It turned out to be quite good, although due to my complete lack of experience in Gleam, it was much harder than it should have been.  

## Anything Worth Sharing?  

Honestly, nothing happened today that I feel particularly comfortable sharing. The title of this entry comes from the great beauty of a language like Gleam. I had been thinking for days about trying a new language, and Gleam had been an obsession of mine for a long time. A few months ago, I even dreamt about it. I really like its syntax, and I think it's a language I feel comfortable calling beautiful.  

Imagine we want to create a function that takes a string and tries to convert it into a number. If it fails, it should return an error.  

In Python, it might look like this:  

```python  
def atoi(v: str) -> int:  
    number = v.split("age:")[1]  
    return int(number)  

print(atoi("age:2"))  
print(atoi("age:a"))  
```  

It looks fine, but how does it handle the last case?  

```bash  
❯ python trash_16-03-25.py  
2  
Traceback (most recent call last):  
  File "/home/s1e7j/Devel/Python/Trash/trash_16-03-25.py", line 7, in <module>  
    print(atoi("age:a"))  
          ~~~~^^^^^^^^^  
  File "/home/s1e7j/Devel/Python/Trash/trash_16-03-25.py", line 3, in atoi  
    return int(number)  
ValueError: invalid literal for int() with base 10: 'a'  
```  

Suddenly, this blew up in our face. There was no warning that there would be a problem at any point. And of course, those familiar with Python might say that it was obvious that this needed a try-catch. However, this is not obvious at all. Now, let's see how it looks in Gleam:  

```gleam  
import gleam/int  

pub fn atoi(v: String) -> Result(Int, String) {  
  case v {  
    "age:" <> age_str ->  
      case int.parse(age_str) {  
        Ok(age) -> Ok(age)  
        Error(_) -> Error("Invalid age format")  
      }  
    _ -> Error("String does not start with 'age:'")  
  }  
}  

pub fn main() {  
  echo atoi("age:5")  
  echo atoi("age:32")  
  echo atoi("aasdf")  
}  
```  

At first glance, this looks much worse. But when you take a moment to think about it, everything is clear regarding where it might fail, and there are some beautiful aspects to it. For example, in Python, to extract the age number, we have to split the string and take the second part. That is absurd and could fail in many ways.  

On the other hand, with Gleam, we have the `<>` keyword, which allows us to check patterns that a string matches without needing to abstract ourselves.  

I just wanted to share how beautiful Gleam sometimes seems to me.  

## Cool Links?  

* [guide](https://browser.engineering/)
