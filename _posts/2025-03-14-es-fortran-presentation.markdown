---
layout: post
title:  "Fortran: Un inicio en el camino"
date:   2025-03-14 21:55:00 -0500
categories: ES CS
---

## ¿Cuanto Trabaje Hoy?

Hoy no fue un dia particularmente dado al trabajo. Me lo tome con calma y me
dedique a estar tranquilo. Tengo aun trabajos que entregar para la universidad
pero queria descansar un poco de una semana intensa que resulto ser esta.

## ¿En que trabaje?

Hoy estudie Fortran, pase el dia aprendiendo su sintaxis y comparando su eficiencia
con C. Resulto ser una experiencia muy distinta a todo lo que esperaba. Ademas de
eso los otros proyectos fue el inicio de una entrada para mi Blog que va a servir
como guion para un video que planeo subir eventualmente. Empezar a mirar maneras
de crear fractales de modo tal que los pueda guardar y considerar la idea de crearme
una cuenta de Mastodon en la que compartir no solo estos escritos si no las imagenes
matematicas que cree y los videos que grabe. Nada de esto lo hice de manera muy
formal pero espero poder compartir con mas detalles en un futuro por aqui el como
resulte.

## ¿Algo Digno de Compartir?

Lo mas importante que hice hoy fue estudiar fortran. Por lo tanto, voy a compartir
un poco cual es el plan que tengo para aprender Fortran y por que resulta importante
para mi el aprenderlo bien.

Lo primero que hice fue visitar la pagina oficial de
[fortran](https://fortran-lang.org/learn/). En ella aprendi lo basico de cualquier
lenguaje. Como funciona su sintaxis, que tipos tiene, como se ven en memoria.
Segui cada uno de los code snippets de esta guia y con eso empece a buscar
maneras de aprender.

Entonces encontre la pagina del [proyecto Euler](https://projecteuler.net). Esta
es una lista de problemas con las soluciones. Hagamos el primer problema aqui mismo
pues resulta ser super sencillo:

El enunciado es:

_If we list all the natural numbers below 10 that are multiples of 3 or 5,_
_we get 3, 5, 6 and 9. The sum of these multiples is 23. Find the sum of all_
_the multiples of 3 or 5 below 1000._

que traduce como:

_Si miramos los numeros debajo de 10 que son multiplos de 3 o 5 obtenemos_
_3, 5, 6 y 9. La suma de estos es 23. Encuentre la suma de todos los multiplos_
_de 3 y 5 debajo de 1000._

Este es un problema realmente simple. De hecho, pude escribir una solución en
C en menos de 2 minutos. Quedo algo como esto:

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

Este es un codigo supremamente simple que solo va desde `0` hasta `999` y pregunta
en cada caso si al dividir de manera entera por `3` o por `5` el residuo es `0`.
En caso de que asi sea suma el valor a resultado y por ultimo imprime cuanto
fue lo que sumo.

Luego de esto, cuando ya habia comprobado que entendia el problema intente hacer
una solución pero ahora con fortran. De lo cual saque dos resultados.

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

Esta es una traducción directa de mi solución en C. no hace absolutamente nada mas.
Esta traducción me devolvia exactamente el mismo resultado y con eso podia estar
tranquilo de que funcionaba.

Luego de esto, decidi usar una nueva opción que tenia fortran y que me resulto
muy llamativo pues se veia realmente simple y con eso consegui el siguiente resultado

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

Ok... ahora si estamos hablando de algo mas interesante. Derrepente la solución
se siente muy similar pero esencialmente distinta. Lo que estamos haciendo aqui
es tener dos iteradores. El primero va desde `1` hasta `999` dando pasos de a `3`
es decir que va en `1, 3, 6, 9, ...` con eso nos aseguramos de que todos los valores
son multiplos de 3. Por lo tanto, podemos sumar absolutamente todos los valores que
iteremos aqui. Luego de esto hay otro ciclo que esta vez va dando pasos de a `5`.
Sin embargo, aqui tenemos que hacer una pequeña revisión y es que no lo hayamos
sumado antes (es decir, que no sea tambien multiplo de 3). Todo esto habria
funcionado esencialmente igual en `C` pero la cosa que realmente queria probar era
ese concurrent. Aun me estoy debiendo que resulta hacer concurrent exactamente
y quizas deba ir a mirar mas la documentación pero en mi entendimiento actual
(que probablemente esta errado) lo que hace es que estos dos ciclos se ejecuten
de manera paralela. Eso suena genial sin duda y me sorprende lo facil que resulta.
Tengo mis dudas de que realmente este haciendo algo en este contexto pues hay muchas
cosas que no tienen sentido para mi y que en otros lenguajes me habrian
disparado en
el pie. Por ejemplo, el hecho de que este iterando sobre la misma variable podria
causar en otros programas que ubiera conflictos y que los valores cambiaran en
mitad de la ejecución. Sin embargo, no he hecho suficiente investigación para
asegurar nada. Probablemente sea algo que deba verificar mejor.

Al final hice varios ejercicios asi y actualmente me encuentro solucionando
un problema que me tiene pensando en la implementación que tienen de los enteros
pues necesito acceder a un entero de al menos 64 bytes y no estoy seguro de como
hacerlo. Pero hablare de eso luego cuando resulte que no era tan extraño como esperaba
o quizas simplemente implemente mi propio tipo de entero para solucionarlo. Aun
no estoy seguro. Pero bueno, supongo que lo contare por aqui en un futuro.

## Cool Links?

Todos los links que quisiera compartir hoy ya estan alla arriba pero aqui los
pongo un poco mas organizados.

* [fortran](https://fortran-lang.org/learn/)
* [proyecto Euler](https://projecteuler.net)
