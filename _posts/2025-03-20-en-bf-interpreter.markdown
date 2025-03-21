---
layout: post  
title: "Brainfuck Interpreter"  
date: 2025-03-20 23:47:44 -0500  
categories: 
---

## How Much Did I Work Today?

Today was a very interesting day. I spent a total of 9 hours working on the Brainfuck interpreter.

## What Did I Work On?

I dedicated my time to developing a Brainfuck interpreter in Go. As I mentioned in yesterday's entry, I wanted to deepen my understanding of the frontend of compilers and interpreters. To achieve this, I revisited this project, simplifying the process until I was left only with the lexer—since Brainfuck has an extremely simple syntax.

## Something Worth Sharing?

I’m fascinated by Brainfuck and want to share how to manually interpret a Brainfuck program. Let’s take the following example code:

```brainfuck
>+++[<+++++++++++>-]<.
```

This program produces the output `!`.  
Below is a step-by-step breakdown of the program execution, showing the state of the tape (memory cells), the pointer position, and the processed instruction:

| STATE     | POINTER | INSTRUCTION |
| --------- | ------- | ----------- |
| `[0][0]`  |    1    | START       |
| `[0][0]`  |    2    | >           |
| `[0][1]`  |    2    | +           |
| `[0][2]`  |    2    | +           |
| `[0][3]`  |    2    | +           |
| `[0][3]`  |    2    | [           |
| `[0][3]`  |    1    | <           |
| `[1][3]`  |    1    | +           |
| `[2][3]`  |    1    | +           |
| `[3][3]`  |    1    | +           |
| `[4][3]`  |    1    | +           |
| `[5][3]`  |    1    | +           |
| `[6][3]`  |    1    | +           |
| `[7][3]`  |    1    | +           |
| `[8][3]`  |    1    | +           |
| `[9][3]`  |    1    | +           |
| `[10][3]` |    1    | +           |
| `[11][3]` |    1    | +           |
| `[11][3]` |    2    | >           |
| `[11][2]` |    2    | -           |
| `[11][2]` |    2    | ]           |
| `[11][2]` |    1    | <           |
| `[12][2]` |    1    | +           |
| `[13][2]` |    1    | +           |
| `[14][2]` |    1    | +           |
| `[15][2]` |    1    | +           |
| `[16][2]` |    1    | +           |
| `[17][2]` |    1    | +           |
| `[18][2]` |    1    | +           |
| `[19][2]` |    1    | +           |
| `[20][2]` |    1    | +           |
| `[21][2]` |    1    | +           |
| `[22][2]` |    1    | +           |
| `[22][2]` |    2    | >           |
| `[22][1]` |    2    | -           |
| `[22][1]` |    2    | ]           |
| `[22][1]` |    1    | <           |
| `[23][1]` |    1    | +           |
| `[24][1]` |    1    | +           |
| `[25][1]` |    1    | +           |
| `[26][1]` |    1    | +           |
| `[27][1]` |    1    | +           |
| `[28][1]` |    1    | +           |
| `[29][1]` |    1    | +           |
| `[30][1]` |    1    | +           |
| `[31][1]` |    1    | +           |
| `[32][1]` |    1    | +           |
| `[33][1]` |    1    | +           |
| `[33][1]` |    2    | >           |
| `[33][0]` |    2    | -           |
| `[33][0]` |    2    | ]           |
| `[33][0]` |    1    | <           |
| `[33][0]` |    1    | .           |

**What happens during execution?**

1. **Initialization:**  
   - The process starts at cell 0 with a value of 0.  
   - The pointer moves to cell 1, where it is incremented by 3 (three `+` instructions).

2. **Main Loop (`[<+++++++++++>-]`):**  
   - The value in cell 1 (which is 3) is evaluated, and since it is not 0, the loop is entered.  
   - Inside the loop, the pointer moves to cell 0, where the value is incremented by 11 (`+++++++++++`).  
   - The pointer then returns to cell 1, where the value is decremented by 1, and the condition is checked again.  
   - This cycle repeats 3 times, accumulating a value of 33 (11 × 3) in cell 0.

3. **Output:**  
   - After the loop finishes (when cell 1 becomes 0), the pointer moves back to cell 0.  
   - The content of cell 0 is output, which is 33. According to the ASCII table, the value 33 corresponds to the character `!`.

This table meticulously details each step of the manual interpretation, showing how the tape values change and how the pointer moves throughout the program. Despite its minimalistic nature, this exercise demonstrates the power of Brainfuck, as it is Turing complete and capable of representing any algorithm.

I focused on developing this interpreter (as reflected in the table) today. Although I performed these calculations manually, I verified the efficiency of my code and feel very satisfied with the outcome. Additionally, this exercise has allowed me to gradually move away from the "hell of tutorials." I am considering documenting this project along with the implementation of the Game of Life that I did earlier, but I haven't decided yet.

## Interesting Links

* [Brainfuck Specification](https://github.com/sunjay/brainfuck/blob/master/brainfuck.md)
* [My Interpreter](https://github.com/S1e7J/Go-BrainF-ck-Interpreter/tree/main)
