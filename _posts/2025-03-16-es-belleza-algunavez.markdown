---
layout: post
title:  "Belleza en Algunos Momentos"
date:   2025-03-16 23:42:43 -0500
categories: 
---

## ¿Cuanto trabaje hoy?

Hoy trabaje apenas 3 horas. Creo que para ser un fin de semana esta bien y la
verdad en esas 3 horas me rindio lo suficiente. Ademas de eso empece un pequeño
proyecto para probar Gleam como Lenguaje que no lo conte dentro de las horas de
trabajo

## ¿En que trabaje hoy?

Hoy hice un trabajo de fisica estadistica. Aun no lo termino pero avance en un
punto y medio. Si leiste la entrada de ayer mas o menos te imaginaras lo que fue
eso pues no resulto muy distinto.

Ademas de eso empece a hacer el pequeño codigo para un navegador siguiendo esta
[guia](https://browser.engineering/). Resulto ser bastante buena aunque dada mi
falta absoluta de experiencia en Gleam me costo mucho mas de lo que deberia

## ¿Algo digno de Compartir?

La verdad es que hoy no paso nada que me sienta particularmente comodo compartiendo.
El nombre de esta entrada se debe a la gran belleza que resulta un lenguaje como
Gleam. Llevaba dias pensando en probar un nuevo lenguaje y gleam me habia obsecionado
durante mucho tiempo. Llegue incluso hace unos meses a soñar con el. Me gusta mucho
su sintaxis y creo que es un lenguaje al que me siento comodo llamando bello.

Imaginemos que queremos hacer una función que recibe un string e intenta convertirlo
en un numero. Si falla debe devolver un error

```python
def atoi(v: str) -> int:
    number = v.split("age:")[1]
    return int(number)


print(atoi("age:2"))
print(atoi("age:a"))
```

Se ve bien, pero ¿como resuleve el ultimo caso?

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

Derrepente esto nos exploto en la cara. No aviso que ubiera problemas en ningun
momento. Y claro, aquellos que sepan de python entre ustedes podria decir que
esto era obvio que se debia poner en un try catch. Sin embargo, esto no es para
nada obvio. A cambio miremos como se ve en gleam:

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

Esto se ve mucho peor a primera vista. Pero cuando uno se para a pensarlo absolutamente
todo es evidente en donde podria fallar y se ven cosas muy hermosas. Por ejemplo,
para quedarnos con el numero de la edad en python tenemos que partir el string y
quedarnos con la segunda parte. Eso es absurdo y podria fallar de muchas maneras.

En cambio, con gleam tenemos el keyword `<>` que nos permite revisar por los patrones
que cumple un string sin necesidad de abstraernos.

Solo queria mostrar lo lindo que me parecia a veces gleam.

## Cool Links?

* [guia](https://browser.engineering/)
