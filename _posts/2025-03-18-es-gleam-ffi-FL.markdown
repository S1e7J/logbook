---  
layout: post  
title: "Primer vistazo a Gleam FFI"  
date: 2025-03-18 22:36:28 -0500  
categories:  
---  

## ¿Cuánto trabajé?  

Hoy no fue un día particularmente ocupado. Solo trabajé 3 horas.  

## ¿En qué estuve trabajando?  

Hoy aprendí un poco sobre Erlang y Gleam FFI. Quería aprender Erlang desde hace bastante tiempo, pero no había tenido oportunidad hasta ahora. Una de las cosas que realmente me gusta de Gleam es lo fácil que es crear una interfaz entre sí mismo y el objetivo en el que se ejecuta.  

De esta manera, puedes usar bibliotecas de otros lenguajes e incluso utilizar los NIFs de Erlang para emplear otros lenguajes. Por ejemplo, puedes vincular Rust o C simplemente compilando al objetivo correcto.  

Creo que esta es una manera de hacer que un lenguaje tenga un acceso excelente a otras funcionalidades, permitiéndote usar la mejor herramienta para cada tarea. En el momento en que encuentres un problema, podrías simplemente trasladarlo a otra herramienta si resulta ser demasiado difícil de resolver en Gleam.  

## ¿Algo digno de compartir?  

El FFI en Gleam fue una grata sorpresa porque me permite hacer casi cualquier cosa, incluso aquellas que no son triviales en el lenguaje, utilizando otro lenguaje para ese propósito. Veamos un ejemplo de cómo se puede hacer esto.  

Antes que nada, una pequeña advertencia. Este no será un gran ejemplo, simplemente porque la función que programo en otros lenguajes aquí sería bastante fácil de hacer en Gleam. Sin embargo, imagina que estás lidiando con un problema no trivial y toma esto con cautela.  

Primero, veamos el código de la función en otro lenguaje. Comenzaremos con Erlang:  

```erlang  
-module(play_ground_ffi).  
-export([fac/1]).  

fac(N) when N =< 1 ->  
  1;  
fac(N) ->  
  N * fac(N - 1).  
```  

Coloca este código en el archivo `src/play_ground_ffi.erl` dentro del proyecto en Gleam. Este es un código bastante sencillo en Erlang. Lo único que hace es calcular el factorial de un número. Cuando el número es 1 o menor, devuelve 1; cuando es mayor, devuelve la multiplicación entre ese número y el resultado de la función con un número menos. Veámoslo con un ejemplo:  

```
= factorial(4)  
= 4 * factorial(3)  
= 4 * 3 * factorial(2)  
= 4 * 3 * 2 * factorial(1)  
= 4 * 3 * 2 * 1  
= 24  
```

Esta es la definición de recursión y quería dejarlo claro para que se entienda lo que hace este código. También necesitas crear un archivo para JavaScript, porque Gleam puede compilar a ambos lenguajes (lo cual me parece muy genial, siendo sincero). Veamos cómo se vería este código en JavaScript.  

```javascript  
export function fac(N) {  
  if (N <= 1) {  
    return 1;  
  }  
  return N * fac(N - 1);  
}
```  

También es un código muy simple que hace lo mismo. Ahora, ¿cómo podemos llamar a esta función desde Gleam? Solo usamos el decorador `@external`.  

```gleam  
import gleam/io  

@external(javascript, "./play_ground_ffi.mjs", "fac")  
@external(erlang, "play_ground_ffi", "fac")  
pub fn fac(n: Int) -> Int  

pub fn main() {  
  io.debug(fac(4))  
}
```  

Esto significa que la función `fac` en este código en realidad es la función `fac` en Erlang o en JavaScript, dependiendo del objetivo de compilación. Ahora puedes usar esta función sin problemas. Creo que esto es realmente genial y hace que la creación de enlaces (bindings) en Gleam sea muy sencilla. Para ejecutarlo, solo necesitas compilarlo y correr el siguiente comando:  

```bash  
❯ gleam run  
  Compiling play_ground  
   Compiled in 0.58s  
    Running play_ground.main  
24  
```  

Y también:  

```bash  
❯ gleam run --target javascript  
  Compiling play_ground  
   Compiled in 0.07s  
    Running play_ground.main  
24  
```  

Muy genial, la verdad. He estado estudiando más sobre Erlang, pero aún no he terminado su documentación. Probablemente hablaré más sobre esto en el futuro, porque es uno de los lenguajes más interesantes que he encontrado, pero no por ahora.  

## ¿Enlaces interesantes?  

* [Erlang QuickStart](https://www.erlang.org/doc/system/getting_started.html)  
* [Publicación de blog sobre Gleam FFI](https://www.jonashietala.se/blog/2024/01/11/exploring_the_gleam_ffi/)  
