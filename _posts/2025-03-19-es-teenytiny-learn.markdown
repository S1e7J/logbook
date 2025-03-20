---
layout: post
title:  "teenytiny: Aprendiendo de Compiladores"
date:   2025-03-19 23:36:09 -0500
categories: 
---

## ¿Cuanto Trabaje Hoy?

Hoy fue un dia intenso. Trabaje al menos 8 horas.

## ¿En que trabaje hoy?

Aproveche que tengo tiempo dado que estoy en receso de mi universidad y decidi
hacer el frontend de un compilador. Era algo que llevaba mucho tiempo queriendo hacer
y resulto ser mucho menos trabajo del que esperaba para un programa tan simple.

Esta vez, dado que era una primera vez debo confesar que si segui este [tutorial](https://austinhenley.com/blog/teenytinycompiler1.html) pero me comprometo a repetir esto primero para un interprete de brainfuck en gleam y luego repetir este proceso para transpilar codigo simple de python a fortran o C de manera que me pueda enfrentar a este reto de nuevo y asi aprenderlo bien.

## ¿Algo Digno de Compartir?

La verdad es que lo que tengo para compartir que me parecio supremamente interesante es lo facil que resulta transpilar. Realmente
es sencillo el poder analizar termino a termino cada una de las palabras para crear estructuras utiles. Tambien me sorprende lo importante que resulta la recursión en este proceso y lo mucho que eso me alegra. Creo que puedo pensar en lo fabuloso que resulta.

Ademas de eso presumire un poco mi transpilador. Imagine que tenemos el siguiente script:
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

Este codigo no hace absolutamente nada especial. Simplemente calcula fibonacci. Ahora si pasamos esto por el transpilador tenemos
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

Lo cual es un codigo sin formato. permitanme lo arreglo un poco:
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

Y estos dos codigos son exactamente lo mismo. No hay nada particularmente extraño en este codigo. Simplemente calcula cuanto es el valor de fibonacci. Resulto ser un proyecto sumamente divertido.

## Cool Links?

* [tutorial](https://austinhenley.com/blog/teenytinycompiler1.html)
* [Mi implementación](https://github.com/S1e7J/TeenyTiny.git)
