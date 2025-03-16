---
layout: post
title:  "AI Sin Pereza"
date:   2025-03-15 23:43:44 -0500
categories: ES CS
---

## ¿Cuánto trabajé?

Hoy no fue un día particularmente productivo. Sin embargo, trabajé 4 horas y media.

## ¿En qué estuve trabajando?

Hoy trabajé principalmente en una tarea para mi universidad. Se trataba principalmente del Modelo de Debye en Física Estadística.

## ¿Algo digno de compartir?

Hoy quería hablar sobre cómo la IA puede ser demasiado poco perezosa. Lo cierto es que creo firmemente que la pereza y la inteligencia son mucho más importantes que simplemente hacer _el trabajo_. Hay belleza en encontrar una forma más simple de hacer las cosas. Por supuesto, eso no significa que trabajar duro sea algo malo. Pero si estás trabajando duro y hay una manera de hacer las cosas más simples y obtener exactamente los mismos beneficios, no entiendo por qué deberías hacer lo difícil. Solo por un segundo, hagamos una pausa aquí y hablemos de algo. Me encanta aprender, y soy completamente consciente de que el aprendizaje es mejor cuando le pones esfuerzo. Cuando consideras los beneficios, ten en cuenta lo que aprendiste. Tal vez algunas veces deberías hacer el trabajo duro y simplemente tragarte la rana.

Sin embargo, la IA no tiene ningún concepto de pereza. Déjame mostrarte un ejemplo simple. Tengo estas dos preguntas:

* (a)

    Partiendo de la definición de la función de partición para un oscilador armónico cuántico, demuestra que la función de partición puede escribirse como

    $$
    Z_1 = \frac{1}{2\sinh\!\left(\frac{\beta\hbar\omega}{2}\right)}.
    $$

* (b)

    Luego, considerando un sistema de osciladores independientes, deduce que la función de partición total viene dada por

    $$
    Z_N = \prod_{v} \frac{1}{2\sinh\!\left(\frac{\beta\hbar\omega(v)}{2}\right)},
    $$

    y consecuentemente deriva la energía libre de Helmholtz como

    $$
    F = \sum_{v} \left( \hbar \omega \frac{1}{2} + \frac{1}{\beta}\ln \left(1 - e^{-\beta\hbar\omega}\right)\right) \\
    $$

Es un punto simple sin demasiados problemas. Sin embargo, cuando intentas resolverlo, es realmente absurdo usar los resultados de A en B sin dudarlo. No estoy seguro si esto será comprensible sin mucho contexto, pero intentemos resolverlo:

* Resolver (a)
    Tenemos la definición, así que lo único que queda es resolver:
    $$
    \begin{align*}
        Z &= \sum_{i = 0}^{\infty} e^{-\beta E_i}\\
        Z_1 &= \sum_{i = 0}^{\infty} e^{-\beta \hbar \omega
    \left( n + \frac{1}{2} \right)}\\
        &= \sum_{i = 0}^{\infty} e^{-\beta \hbar \omega n}  e^{- \beta \hbar \omega\frac{1}{2}}\\
        &= e^{- \beta \hbar \omega\frac{1}{2}} \sum_{i = 0}^{\infty}
    e^{-\beta \hbar \omega n}  \\
        &= e^{- \beta \hbar \omega\frac{1}{2}} \sum_{i = 0}^{\infty}
    \left(e^{-\beta \hbar \omega }\right)^n  \\
        \sum_{n=0}^{\infty} y^n &= \frac{1}{1 - y} \text{ Serie Geométrica}\\
        Z_1 &= e^{-\beta \hbar \omega \frac{1}{2}} \frac{1}{1 - e^{-\beta\hbar\omega}}\\
        &=  \frac{1}{e^{-\beta \hbar \omega \frac{1}{2}}\left(1 - e^{-\beta\hbar\omega}\right)}\\
        &=  \frac{1}{e^{-\beta \hbar \omega \frac{1}{2}} - e^{-\frac{1}{2}\beta\hbar\omega}}\\
        &=  \frac{1}{e^{-\beta \hbar \omega \frac{1}{2}} -
    e^{-\frac{1}{2}\beta\hbar\omega}} \frac{2}{2} \\
        &=  \frac{2}{e^{-\beta \hbar \omega \frac{1}{2}} -
    e^{-\frac{1}{2}\beta\hbar\omega}} \frac{1}{2} \\
        &=  \frac{1}{\sinh\left( \frac{\beta \hbar \omega}{2} \right) 2}  \\
        &=  \left[{\sinh\left( \frac{\beta \hbar \omega}{2} \right) 2}\right]^{-1}\square\\
    \end{align*}
    $$

    Intenté, en un esfuerzo por simplicidad, poner todos los pasos intermedios aquí. No estoy seguro si esto afectará la credibilidad, pero si no lo entendiste, no te preocupes. El único paso importante es ver que

    $$
        Z_1 = e^{-\beta \hbar \omega \frac{1}{2}} \frac{1}{1 - e^{-\beta\hbar\omega}}\\
    $$

    es un punto intermedio.

* Resolver (b)
    Veamos, lo que estamos buscando es básicamente

    $$
    F = - \frac{1}{\beta}\sum_v \ln Z_1 =
    \sum_{v} \left( \hbar \omega \frac{1}{2} + \frac{1}{\beta}\ln \left(1 - e^{-\beta\hbar\omega}\right)\right) \\
    $$

    Y por supuesto, podrías simplemente insertar el resultado del punto anterior y hacer un montón de trigonometría sobre las propiedades del logaritmo. Sin embargo, si te alejas un poco y tomas en consideración lo que dije antes, la solución es esencialmente trivial. Veámoslo

    $$
    \begin{align*}
        F &= - \frac{1}{\beta} \sum_{v} \ln Z_1\\
        Z_1 &= e^{-\beta \hbar \omega \frac{1}{2}} \frac{1}{1 - e^{-\beta\hbar\omega}}\\
        F &= - \frac{1}{\beta} \sum_{v} \ln e^{-\beta \hbar \omega \frac{1}{2}} \frac{1}{1 - e^{-\beta\hbar\omega}} \\
        &= - \frac{1}{\beta} \sum_{v} \left(\ln e^{-\beta \hbar \omega
    \frac{1}{2}} - \ln 1 - e^{-\beta\hbar\omega}\right) \\
        &= - \frac{1}{\beta} \sum_{v} \left( -\beta \hbar \omega \frac{1}{2} - \ln 1 - e^{-\beta\hbar\omega}\right) \\
        &= \sum_{v} \left(\frac{1}{\beta}\beta \hbar \omega \frac{1}{2} +
    \frac{1}{\beta}\ln \left(1 - e^{-\beta\hbar\omega}\right)\right) \\
        &= \sum_{v} \left( \hbar \omega \frac{1}{2} + \frac{1}{\beta}\ln \left(1 - e^{-\beta\hbar\omega}\right)\right) \\
        &= \sum_{v} F_v\square
    \end{align*}
    $$

La solución estaba básicamente libre para que la tomaras. La otra ruta era más larga, más voluminosa y más fea. Sin embargo, ¿sabes qué ruta me sugirieron todos los modelos cuando pregunté? La solución en la que tengo que conocer trigonometría y usar muchas más relaciones extrañas. No es que al hacerlo fueran más correctos. Está bien lo que hice. Pasé una buena cantidad de tiempo tratando de hacer que la IA lo hiciera de esta manera sin decirlo directamente. Sin embargo, cada vez que lo intentaba era un intento fallido. Por supuesto que podía hacerlo. La respuesta y la ruta eran correctas la mayoría de las veces. Pero era tal pérdida de tiempo hacerlo de esa manera que me llevó a esta conclusión.

El mayor problema de la IA es que no es perezosa. No tiene ningún problema en traer trigonometría o matemáticas de orden superior (en una solución mencionó la Función Zeta de Riemann, era correcta pero casi me caigo de la silla riendo por hacerlo en un entorno estrictamente real y literalmente solo para el Problema Basiliano). Conoce todas estas formas, pero obtener el resultado mejor y más simple no es cuestión de conocimiento. Es cuestión de gusto y pereza.

## ¿Enlaces interesantes?

No tengo ningún enlace hoy. Tal vez mañana o el lunes enlazaré mi trabajo y solución para este problema. Hasta entonces
