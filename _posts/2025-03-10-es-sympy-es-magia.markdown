---
layout: post
title:  "Sympy es Magia para Física"
date:   2025-03-10 23:29:00 -0500
categories: ES Fisica
---

## ¿Cuanto trabaje?

Hoy trabaje bastante. En mi sistema aparecen 10 horas de trabajo. Estas van
desde las 10 de la mañana hasta las 23:30 momento en el que me siento a escribir
esta entrada.

## ¿En que trabaje?

Hoy estuve en dos proyectos que consumieron la mayoria de mi tiempo (aunque llamarlos
simetricos seria, cuando menos, inexacto). El primero fue la tercera tarea de
cuantica I
que tenia para la universidad. Le dedique a esta tarea aproximadamente 8 horas
solo hoy.
El segundo proyecto es de hecho este logbook. Le dedique mas o menos 2 horas a pensar
que formato era el que queria y a montar y conseguir todas las herramientas que necesitaba.

## ¿Algo digno de Compartir?

Si hubo un heroe el dia de hoy ese tiene que ser Sympy. Creo que me habria resultado
imposible realizar todo lo que hice hoy sin ayuda de esta libreria. No estoy seguro
de que tan explicito puedo ser respecto a los trabajos que realice para esta tarea
pues no se si puedo usar textos del profesor y sus ejercicios para ejemplificar este
problema. Sin embargo, veamos un problema algo desconectado de ese contexto para
poder explicar mejor.

Tome los polinomios asociados de legendre. El que son o para que sirven resulta
irrelevante en este momento. Quizas despues le dedique una entrada a explicar con
mas detalle este tipo de problemas. Por ahora quedemonos con la simple definición
que esta en wikipedia que dice

$$
P_\ell^m \left( x \right) = \frac{\left( -1 \right)^m}{2^\ell \ell!}
\left( 1 - x^2 \right)^{\frac{m}{2}} \frac{d^{\ell + m}}{dx^{\ell + m}}
\left[ \left( x^2 - 1 \right)^\ell \right]
$$

Esta no parece una definición particularmente dificil. Simplemente para un $$m$$
y para un $$\ell$$ concreto reemplace con los valores y llegue a un resultado.
Sin embargo, yo necesitaba hacerlo para $$\ell = m = 3$$. Una 6-derivada es algo
que ciertamente no deseaba hacer a mano. Entonces me puse a estudiar y en un corto
tiempo termine con el siguiente script

```python
def differentiate_n(n, expr, s=x):
    res = expr
    for _ in range(n):
        res = sp.diff(res, s)
    return sp.simplify(res)


def asociado(ell, m, s=x):
    first_factor = (-1)**m/(2**ell * sp.factorial(ell))
    second_factor = (1 - s**2)**(m/2)
    expr = (s**2 - 1)**ell
    tird_factor = differentiate_n((ell + m), expr, s=s)
    return first_factor * second_factor * tird_factor
```

Este codigo es bastante simple. Con un poco de conocimiento basico de sympy se
puede notar que esto es practicamente una traducción directa de la definición
a codigo. Claro que no es bonito ni reutilizable este codigo pero es que mi objetivo
no era crear un codigo super versatil y bonito. Lo unico que queria era solucionar
mi problema y esto es suficiente para ello.

Debo confesar que Sympy no es una solución magica a todos los problemas. Sin embargo,
no creo que ubiera podido terminar a tiempo mi tarea de no ser por Sympy (lo cual
en mi libro es un tipo de magia).

## Cool Links?

* [Sympy](https://www.sympy.org/)
* [Mis Scripts](https:github.com/S1e7J/Cuantica_Tarea_3)
* [Polinomio Asociado de Legendre](https://en.wikipedia.org/wiki/Associated_Legendre_polynomials)
