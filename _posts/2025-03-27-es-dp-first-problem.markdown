---
layout: post
title:  "DP Primeros Problemas"
date:   2025-03-27 23:39:15 -0500
categories: 
---

## ¿Cuanto Trabaje Hoy?

Hoy tuve clases desde las 8:00 hasta las 15:30. con una hora y media de descanso
entremedias. Por lo tanto, esto dan 6 horas de trabajo en clase. Ademas de eso,
al llegar a la casa le dedique 3 horas extras a estudiar programación dinamica.
Por lo tanto el total resulta ser 9 horas de trabajo el dia de hoy.

## ¿En que Trabaje?

Como ya dije, una buena parte del trabajo de hoy fue en clases. Estas eran clases
de física cuantica, física estadistica y electromagnetismo. Ademas, asisti al grupo
de astronomia de la universidad en el cual tuvimos un invitado de la universidad
nacional de Colombia. Este invitado era el encargado de gestionar y calibrar el
sistema de radiotelescopios y dio una de las charlas mas interesantes que he
experimentado mostrando muchos datos tecnicos respecto a su trabajo. Fue una
charla maravillosa.

Ademas de esto, decidi estudiar programación dinamica pues es un tema que vi en
semestres pasados y me di cuenta de que ya me estaba volviendo a costar. Por lo
tanto quice recordarlo y volver a afilar mis habilidades. Para esto, voy a hacer
uso de la lista de problemas de DP que esta en
[este enlace](https://algo.monster/problems/dp-list).

## ¿Algo Digno de Compartir?

Como ya dije, la charla que nos dieron hoy en el grupo de astronomia resulto
sumamente interesante y estimulante. Creo que me apasionan las herramientas y
trabajar para que a otros les resulte mas facil trabajar. Me encanto el como
presento y me encantan los retos tecnicos que se debian solucionar. El autor
fue [Javier Sanchez Gonzales](https://www.researchgate.net/profile/Javier-Sanchez-Gonzalez)
nos conto que iba a presentar su tesis pronto por lo tanto recomiendo estar atento
para todos aquellos que les resulte interesante un tema asi pues es sin duda muy
apasionante.

Por otro lado, hoy repitiendo un problema de DP decidi revisar otras soluciones
y me encontre con un teorema del que no habia escuchado pero que resulta fascinante.

Es el teorema de los 4 cuadrados de Legendre. Este teorema esencialmente dice que
todo numero natural puede escribirse como la suma de cuatro numeros al cuadrado.
O en terminos mas precisos

$$\forall x \in N \exists a, b, c, d\in N\ s.t.\ x = a^2 + b^2 + c^2 + d^2$$

Este teorema es ya de por si genial. Ahora bien, este teorema es claramente no
trivial. Por lo tanto recomiendo que vean una demostración. Por ejemplo
[esta](https://planetmath.org/proofoflagrangesfoursquaretheorem). Prefiero no
llenar este blog con la demostración pues no creo poder simplificarlo lo
suficiente para que todos lo entiendan. Sin embargo si quiero mostrar lo
bello que resulta el algoritmo.

El siguiente codigo lo que devuelve es el numero minimo de terminos que debemos
sumar al cuadrado para que nos de un numero n. Es decir nos devuelve cuantos
numeros no son $$0$$ entre los $$a, b, c, d$$ de la muestra anterior:

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

Este codigo me resulta sumamente bello pues simplemente va revisando caso por caso
aprovechando el teorema. Veamos poco a poco que es lo que dice:

```c
int isSquare(int n) {
    int r = sqrt(n);
    return r * r == n;
}
```

Esta función, basicamente nos devuelve si un numero es un cuadrado exacto.
El como lo hace es en esencia consiguiendo cuanto es el cuadrado y aproximandolo
a un entero. Ahora al multiplicarlo dado que sabemos que r es la raiz cuadrada de
n la unica manera de que se cumpla que $$r*r == n$$ es si $$r$$ era un entero desde
el comienzo.

```c
    if (isSquare(n)) return 1;
```

Este primer caso verifica si el numero $$n$$ es un cuadrado. En ese caso sabemos
que el unico numero que nos hace falta es $$n^2$$ por lo tanto seria 1.

```c
    int t = n;
    while (t % 4 == 0) {
        t /= 4;
    }
    if (t % 8 == 7) return 4;
```

Este punto basicamente verifica si hay alguna manera en la que podemos
expresar a este numero como $$4^k*(8*m + 7)$$. Lo primero que hace
es quitar todos los factores de $$4^k$$ cada vez que itera va removiendo un factor
hasta que se queda con el residuo que debe ser igual a $$7$$ modulo 8.

La razon por la que esta formula nos interesa es por otro teorema que se conoce
como el teorema de 3 cuadrados de legendre que basicamente dice que este numero
es 3 si y solo si no se cumple con esta formula. Nosotros sabemos que en ese caso
la respuesta es 4.

```c
    for (int i = 1; i * i <= n; i++) {
        if (isSquare(n - i*i)) return 2;
    }
```

Este simplementa va viendo si al quitarle un numero cuadrado a el numero original
da la casualidad de que de otro numero cuadrado y por lo tanto sea equivalente a
dos.

Ya despues de todo esto simplemente retorna 3 en caso de que ninguna de estas
condiciones se cumpla.

Como pueden ver este codigo es realmente genial y me parecio una gran mejora
frente al codigo en DP que habia hecho para solucionar el problema.

Creo que es una gran muestra de que aprender paga y que uno puede encontrar
soluciones cada vez mas bellas a medida que se tenga mas conocimiento.

## Cool Links?

* [Algo DP List](https://algo.monster/problems/dp-list).
* [Javier Sanchez Gonzales](https://www.researchgate.net/profile/Javier-Sanchez-Gonzalez)
* [Demostración](https://planetmath.org/proofoflagrangesfoursquaretheorem)
