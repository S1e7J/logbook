---
layout: post
title:  "El Juego de la vida para superar la Vida"
date:   2025-03-11 23:10:00 -0500
categories: ES ComputerScience
---

## ¿Cuanto Trabaje Hoy?

Hoy tuve algunas clases que en total sumaron 4 horas de trabajo. Sin embargo,
despues de eso no me sentia particularmente bien entonces decidi dedicarme
a un pequeño proyecto de programación que lograra subirme el animo.

## ¿En que Trabaje?

Hoy hice algunos pequeños puntos para tareas chiquitas de la universidad. Sin emabargo,
el proyecto mas interesante que hice hoy fue trabajar en un juego de la vida de Conway
pues queria un proyecto pequeño, rapido e interesante para poder sentirme realizado
al final del dia. Siendo honesto, lo conseguí.

## ¿Algo Digno de Compartir?

Fue genial trabajar con `C` y creo que puede ser una gran idea
hacer este tipo de pequeños proyectos que te ayuden espiritualmente.

Esta era mi primera vez programando el juego de la vida y la verdad es que no fue
un problema tan grande como esperaba. Resulto ser un proyecto de menos de 200 lineas
de codigo y creo que algunas de las ideas que tuve resultaron interesantes. A
continuación les comparto algunas de ellas.

```C
int GetMinWidthHeight() {
    return (GetScreenWidth() > GetScreenHeight()) ?
    GetScreenHeight() : GetScreenWidth();
}
```

Conocia el operador `?` en JS y en Ruby desde hace algun tiempo pero para ser
completamente honesto no sabia que este tipo de `syntacit sugar` estaba en C.
Me parecio genial verlo aparecer luego de un minimo de busqueda en internet.

```C
int CountLiveNeighbors(enum PosibleState **game, int i, int j) {
    int LiveNeighbors = 0;
    for (int k = -1; k <= 1; k++) {
        for (int l = -1; l <= 1; l++ ) {
            int XPos = (i + k + L_CELL) % (L_CELL);
            int YPos = (j + l + L_CELL) % (L_CELL);
            if ((k != 0 || l != 0) &&
                game[XPos][YPos] == Live ||
                game[XPos][YPos] == NextDie)
                LiveNeighbors++;
        }
    }

    return LiveNeighbors;
}
```

Esta función es realmente simple pero aun asi me hizo sentir muy orgulloso.
Mientras la hacia recordaba que para uno de mis primeros proyectos en Rust (creo
que era el problema de la Isla, pero no estoy seguro) tenia que hacer una función
basicamente igual a esta y recuerdo escribir absolutamente todas las opciones 1 a
1 en una lista e iterar sobre esta lista literal que estaba en mi codigo. Ver el
como he crecido programando me hizo sentir muy bien y calmo una parte importante
de mi ansiedad notar que a veces uno avanza poco a poco y sin darse cuenta.

```C
enum PosibleState{
    Die,
    Live,
    NextLive,
    NextDie,
};
```

Esta fue una de las grandes sorpresas del codigo. El hecho de que esta idea
funcionara me resulto muy interesante. Una de mis mayores dudas cuando estaba
iniciando este proyecto era como pensaba conservar el estado anterior para hacer
los cambios y en el mismo lugar realizar los cambios. Sabia que esto se podia soluciónar
simplemente creando una copia del juego y editando sobre el original para luego borrar
la copia de memoria. Sin embargo, el ir creando direcciones de memora me parecia
que solo hacia que ubiera mas riesgo de tener memory leaks. Con esto entonces
pense en tener valores intermedios que me permitieran hacer los cambios que queria
en dos pasos y asi no perder información mientras la necesitara para desacerme de
ella en cuanto ya no fuera importante.

Ahi esta, partes de mi codigo en este proyecto que creo que resultaron interesantes
o entretenidas y que me parecian dignas de compartir. Si quieren ver el codigo
esta en el primer link aqui abajo. Espero sea interesante para ustedes.

## Cool Links?

* [Conway's Game Of Life](https://github.com/S1e7J/RayLib-Game-Of-Life)
* [Explanation of GOL](https://en.wikipedia.org/wiki/Conway%27s_Game_of_Life)
