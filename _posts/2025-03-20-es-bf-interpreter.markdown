---
layout: post  
title: "Intérprete de Brainfuck"  
date: 2025-03-20 23:47:44 -0500  
categories: 
---

## ¿Cuánto trabajé hoy?

Hoy fue un día muy interesante. Trabajé un total de 9 horas en el intérprete de Brainfuck.

## ¿En qué trabajé?

Me dediqué a desarrollar un intérprete de Brainfuck en Go. Como mencioné en la entrada de ayer, quería profundizar en el frontend de compiladores e intérpretes. Para ello, repetí este proyecto simplificando el proceso hasta quedarme únicamente con el lexer, dado que Brainfuck posee una sintaxis sumamente simple.

## ¿Algo digno de compartir?

Me fascina Brainfuck y quiero compartir cómo se interpreta manualmente un programa en este lenguaje. Tomemos el siguiente código de ejemplo:

```brainfuck
>+++[<+++++++++++>-]<.
```

Este programa produce la salida `!`.  
A continuación, se detalla paso a paso cómo se ejecuta, mostrando el estado de la cinta (las celdas de memoria), la posición del puntero y la instrucción procesada:

| ESTADO    | PUNTERO | INSTRUCCIÓN |
| --------- | ------- | ----------- |
| `[0][0]`  |    1    | INICIO      |
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

**¿Qué ocurre durante la ejecución?**

1. **Inicialización:**  
   - Se inicia en la celda 0 con valor 0.  
   - El puntero se mueve a la celda 1 y se incrementa en 3 (se ejecutan tres `+`).

2. **Bucle principal (`[<+++++++++++>-]`):**  
   - Se evalúa la celda 1 (que vale 3) y, al ser distinta de 0, se entra en el bucle.  
   - Dentro del bucle, el puntero se mueve a la celda 0 y se incrementa en 11 (`+++++++++++`).  
   - Se regresa a la celda 1, se decrementa en 1 y se verifica nuevamente si el valor es distinto de 0.  
   - Este ciclo se repite 3 veces, acumulando en la celda 0 el valor 33 (11 × 3).

3. **Salida:**  
   - Tras finalizar el bucle (cuando la celda 1 llega a 0), se mueve el puntero de vuelta a la celda 0.  
   - Se imprime el contenido de la celda 0, que es 33. Según la tabla ASCII, el valor 33 corresponde al carácter `!`.

Esta tabla ilustra detalladamente el proceso de interpretación manual: cómo se modifican los valores de la cinta y cómo se mueve el puntero a lo largo del programa. A pesar de la simplicidad aparente del lenguaje, este ejercicio demuestra la potencia de Brainfuck, ya que, siendo Turing completo, es capaz de representar cualquier algoritmo.

Este intérprete (reflejado en la tabla anterior) fue el enfoque de mi trabajo hoy. Aunque realicé los cálculos manualmente, comprobé la eficacia de mi código y me siento muy satisfecho con el resultado. Además, este ejercicio me ha permitido distanciarme un poco del "infierno de los tutoriales". Estoy considerando documentar este proyecto junto con la implementación del Juego de la Vida que realicé anteriormente, pero aún no he tomado una decisión.

## Enlaces interesantes

* [Especificación de Brainfuck](https://github.com/sunjay/brainfuck/blob/master/brainfuck.md)
* [Mi intérprete](https://github.com/S1e7J/Go-BrainF-ck-Interpreter/tree/main)
