---
title: Automatización y secuencias de comandos de shell de Linux
description: 
published: true
date: 2023-02-12T06:32:33.587Z
tags: 
editor: markdown
dateCreated: 2023-02-12T06:32:31.701Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Linux Shell Scripting and Automation***English** document is available*](/en/Knowledge-base/Linux/linux-shell-scripting-and-automation)
{.links-list}


# Linux Shell Scripting y Automatización

El shell de Linux es una poderosa herramienta para automatizar tareas y facilita mucho la vida de los desarrolladores. En este artículo, exploraremos algunos de los conceptos básicos de las secuencias de comandos de shell y cómo pueden ayudarlo en su trabajo.

## ¿Qué es una concha?

Un shell es un intérprete de línea de comandos que le permite interactuar con su sistema operativo. En Linux, el shell predeterminado es Bash (Bourne Again Shell).

Los scripts de shell son simplemente una secuencia de comandos de shell almacenados en un archivo de texto. Puede ejecutar un script de shell escribiendo su nombre en el símbolo del sistema.

## ¿Por qué usar secuencias de comandos de shell?

Las secuencias de comandos de Shell son una excelente manera de automatizar tareas que, de lo contrario, tendría que hacer manualmente. Por ejemplo, supongamos que desea enumerar todos los archivos en un directorio. Puede hacer esto manualmente escribiendo `ls` en el símbolo del sistema, pero si tuviera que hacer esto para miles de directorios, sería mucho más rápido escribir un script de shell para que lo haga por usted.

Otro uso común de los scripts de shell es automatizar tareas repetitivas. Por ejemplo, si necesita ejecutar el mismo comando una y otra vez con diferentes argumentos, puede escribir un script de shell para que lo haga por usted.

Los scripts de shell también son una excelente manera de automatizar tareas que deben ejecutarse regularmente, como las copias de seguridad. Puede programar un script de shell para que se ejecute diariamente, semanalmente o mensualmente usando una herramienta como `cron`.

## Cómo escribir un script de shell

Los scripts de shell son simplemente archivos de texto que contienen una secuencia de comandos de shell. Puede crear un nuevo script de shell con cualquier editor de texto, como `nano` o `vi`.

Vamos a crear un script de shell simple que enumere todos los archivos en el directorio actual. Primero, abre un nuevo archivo de texto con `nano`:

```
nano list-files.sh
```

Ahora escriba lo siguiente en el archivo:

```
#!/bin/bash
ls
```

Guarde el archivo y salga de `nano`.

Para hacer que el script de shell sea ejecutable, debe cambiar sus permisos con el comando `chmod`:

```
chmod +x list-files.sh
```

Ahora puede ejecutar el script de shell escribiendo su nombre:

```
./list-files.sh
```

Debería ver una lista de todos los archivos en el directorio actual.

Echemos un vistazo a lo que hace cada línea de nuestro script de shell:

- La primera línea, `# !/bin/bash`, se llama shebang. Le dice al shell qué intérprete usar para ejecutar el script.
- El comando `ls` enumera todos los archivos en el directorio actual.

## Variables

Los scripts de shell pueden utilizar variables para almacenar datos y hacer que sus scripts sean más flexibles.

Para crear una variable, solo necesita darle un nombre y un valor. Por ejemplo, para crear una variable `foo` con el valor `bar`, escribiría lo siguiente en el símbolo del sistema:

```
foo=bar
```

Ahora puede usar el símbolo `$` para acceder al valor de la variable. Por ejemplo, para imprimir el valor de la variable `foo`, escribiría lo siguiente:

```
echo $foo
```

También puede usar variables en sus scripts de shell. Modifiquemos nuestro script `list-files.sh` para hacer uso de una variable.

Primero, creemos una variable para almacenar el directorio que queremos listar:

```
directory=/path/to/directory
```

Ahora podemos usar la variable `$directory` en nuestro script de shell:

```
#!/bin/bash
ls $directory
```

Guarde el archivo y salga de `nano`.

Ahora puede ejecutar el script de shell con la variable `directorio`:

```
./list-files.sh
```

Debería ver una lista de todos los archivos en el directorio especificado.

## Condicionales

Los scripts de shell pueden hacer uso de condicionales para tomar decisiones sobre qué acciones tomar.

Los condicionales se basan en las palabras clave `if`, `then` y `fi`. Por ejemplo, el siguiente condicional verificará si la variable `foo` es igual a `bar` y, si es así, imprimirá `igual`:

```
if [ $foo = "bar" ]; then
  echo "equal"
fi
```

La palabra clave `if` va seguida de una condición entre corchetes (`[]`). La condición es seguida por la palabra clave `then`, que es seguida por la acción a tomar si se cumple la condición. La acción va seguida de la palabra clave `fi`, que finaliza el condicional.

Modifiquemos nuestro script `list-files.sh` para hacer uso de un condicional.

Primero, creemos una variable para almacenar el directorio que queremos listar:

```
directory=/path/to/directory
```

Ahora podemos usar la variable `$directory` en nuestro script de shell:

```
#!/bin/bash
if [ -d $directory ]; then
  ls $directory
fi
```

Guarde el archivo y salga de `nano`.

Ahora puede ejecutar el script de shell con la variable `directory`:

```
./list-files.sh
```

Debería ver una lista de todos los archivos en el directorio especificado.

La opción `-d` de la sentencia `if` comprueba si la variable `directorio` es un directorio. Si es así, se ejecuta el comando `ls` y se listan los contenidos del directorio.

## Bucles

Los scripts de shell pueden hacer uso de bucles para repetir un bloque de código hasta que se cumpla una condición.

Los bucles se basan en las palabras clave `while` y `do`. Por ejemplo, el siguiente bucle imprimirá los números del 1 al 10:

```
i=1
while [ $i -le 10 ]; do
  echo $i
  i=$((i+1))
done
```

La palabra clave `while` va seguida de una condición entre corchetes (`[]`). La condición es seguida por la palabra clave `do`, que es seguida por la acción a realizar. La acción va seguida de la palabra clave `done`, que finaliza el bucle.

En el ejemplo anterior, creamos una variable `i` y la configuramos en 1. El bucle `while` continuará ejecutándose mientras el valor de `i` sea menor o igual a 10.

Cada vez que se ejecuta el bucle, imprimirá el valor de `i` y luego incrementará `i` en 1. Entonces, la primera vez que se ejecuta el bucle, `i` es 1 y la segunda vez que `i` es 2, y así sucesivamente. .

## Funciones

Los scripts de shell pueden hacer uso de funciones para agrupar código relacionado.

Las funciones se basan en la palabra clave `función`. Por ejemplo, la siguiente función imprimirá la fecha y hora actuales:

```
function print-date {
  date
}
```

La palabra clave `función` va seguida del nombre de la función (`imprimir-fecha` en este ejemplo). El cuerpo de la función está encerrado entre corchetes (`{}`).

Para llamar a una función, solo necesita escribir su nombre. Por ejemplo, para llamar a la función `print-date`, escribiría lo siguiente:

```
print-date
```

## Conclusión

Shell scripting es una excelente manera de automatizar tareas y hacer que su vida como desarrollador sea mucho más fácil. En este artículo, hemos explorado algunos de los conceptos básicos de las secuencias de comandos de shell, incluido cómo escribir secuencias de comandos de shell, usar variables, condicionales y bucles, y cómo crear funciones.

## Recursos

- [Tutorial de creación de scripts de Shell](https://www.shellscript.sh/)
- [Guía de Bash para principiantes] (https://www.tldp.org/LDP/Bash-Beginners-Guide/html/)
- [Guía avanzada de secuencias de comandos de Bash] (https://www.tldp.org/LDP/abs/html/)