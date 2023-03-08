---
title: Secuencias de comandos Bash avanzadas
description: 
published: true
date: 2023-02-11T10:32:39.503Z
tags: 
editor: markdown
dateCreated: 2023-02-11T10:32:37.756Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Advanced Bash Scripting***English** document is available*](/en/Knowledge-base/Linux/advanced-bash-scripting)
{.links-list}


# Secuencias de comandos Bash avanzadas

El Bourne Again SHell (Bash) es un shell gratuito para sistemas UNIX. Es el shell predeterminado para la mayoría de las distribuciones de Linux y se puede encontrar en Mac OS X y otros sistemas UNIX.

Bash proporciona un poderoso lenguaje de secuencias de comandos que se puede usar para todo, desde simples secuencias de comandos hasta aplicaciones complejas. En este artículo, veremos algunas de las funciones avanzadas de Bash que se pueden usar para hacer que sus scripts sean más potentes y robustos.

## Condicionales

Bash proporciona varias formas de probar condiciones y tomar decisiones en sus scripts. La forma más común de probar una condición es usar la instrucción `if`.

La sintaxis de la declaración `if` se ve así:

```
if CONDITION
then
    STATEMENTS
fi
```

La `CONDICIÓN` puede ser cualquier prueba que devuelva un valor booleano (verdadero o falso). Las 'DECLARACIONES' entre las palabras clave 'entonces' y 'fi' se ejecutarán si la 'CONDICIÓN' se evalúa como verdadera.

Aquí hay un ejemplo simple:

```bash
if [ $USER = "root" ]
then
    echo "You are logged in as the root user."
fi
```

En este ejemplo, la variable `$USER` se verifica para ver si es igual a la cadena `"root"`. Si es así, se ejecuta el comando `echo` para imprimir un mensaje en la pantalla.

También puede usar la palabra clave `else` para ejecutar un conjunto diferente de `DECLARACIONES` si la `CONDICIÓN` es falsa:

```bash
if [ $USER = "root" ]
then
    echo "You are logged in as the root user."
else
    echo "You are logged in as a normal user."
fi
```

Si necesita verificar varias condiciones, puede usar la palabra clave `elif` (abreviatura de "else if"):

```bash
if [ $USER = "root" ]
then
    echo "You are logged in as the root user."
elif [ $USER = "bob" ]
then
    echo "You are logged in as Bob."
else
    echo "You are logged in as a normal user."
fi
```

También puede usar los operadores `&&` y `||` para combinar múltiples condiciones:

```bash
if [ $USER = "root" ] && [ $SHELL = "/bin/bash" ]
then
    echo "You are logged in as the root user and using the Bash shell."
fi

if [ $USER = "root" ] || [ $USER = "bob" ]
then
    echo "You are logged in as the root user or Bob."
fi
```

## Bucles

Los bucles se utilizan para ejecutar un conjunto de sentencias varias veces. Bash proporciona dos tipos diferentes de bucles: bucles `for` y bucles `while`.

### Para bucles

Los bucles for se utilizan para iterar sobre una lista de valores. La sintaxis para un bucle for se ve así:

```
for VARIABLE in LIST
do
    STATEMENTS
done
```

La `LISTA` puede ser cualquier lista de valores, como una lista de archivos, una lista de argumentos o una lista de números. Las `DECLARACIONES` entre las palabras clave `do` y `done` se ejecutarán una vez para cada valor en la `LISTA`.

Aquí hay un ejemplo simple:

```bash
for FILE in *.txt
do
    echo $FILE
done
```

Este ejemplo imprimirá los nombres de todos los archivos en el directorio actual que terminen con la extensión `.txt`.

También puedes usar el comando `seq` para generar una lista de números:

```bash
for NUM in $(seq 1 10)
do
    echo $NUM
done
```

Este ejemplo imprimirá los números del 1 al 10.

### Ciclos while

Los bucles while se utilizan para ejecutar un conjunto de instrucciones hasta que se cumple una condición. La sintaxis para un ciclo while se ve así:

```
while CONDITION
do
    STATEMENTS
done
```

Las `DECLARACIONES` entre las palabras clave `do` y `done` se ejecutarán hasta que la `CONDICIÓN` se evalúe como falsa.

Aquí hay un ejemplo simple:

```bash
while [ $USER != "root" ]
do
    echo "You are not logged in as the root user."
done
```

Este ejemplo seguirá imprimiendo el mensaje "No ha iniciado sesión como usuario raíz". hasta que la variable `$USER` contenga la cadena `"root"`.

## Funciones

Las funciones se utilizan para agrupar un conjunto de sentencias. Las funciones se pueden usar como comandos y pueden tomar argumentos. La sintaxis de una función se ve así:

```
function NAME {
    STATEMENTS
}
```

El `NOMBRE` puede ser cualquier nombre que quieras darle a la función. Las `DECLARACIONES` entre las palabras clave `{` y `}` se ejecutarán cuando se llame a la función.

Aquí hay un ejemplo simple:

```bash
function print_message {
    echo "This is a message."
}

print_message
```

Este ejemplo define una función llamada `print_message` que imprime un mensaje en la pantalla. La función se llama al final del script.

También puede pasar argumentos a una función:

```bash
function print_message {
    echo $1
}

print_message "This is a message."
```

En este ejemplo, la variable `$1` contiene el primer argumento pasado a la función. Puede acceder a argumentos adicionales con las variables `$2`, `$3`, etc.

## matrices

Los arreglos son variables que pueden contener múltiples valores. La sintaxis para crear una matriz se ve así:

```bash
NAME=(VALUE1 VALUE2 VALUE3...)
```

El `NOMBRE` puede ser cualquier nombre que quieras darle a la matriz. Los `VALUE`s son los valores que se almacenarán en la matriz.

Aquí hay un ejemplo simple:

```bash
FILES=(*.txt *.sh)

for FILE in ${FILES[@]}
do
    echo $FILE
done
```

Este ejemplo crea una matriz llamada `FILES` que contiene todos los archivos en el directorio actual que terminan con las extensiones `.txt` o `.sh`. El símbolo `@` se usa para expandir la matriz en una lista de valores individuales.

También puede acceder a valores individuales en una matriz usando su índice:

```bash
FILES=(*.txt *.sh)

echo ${FILES[0]}
echo ${FILES[1]}
```

Este ejemplo imprimirá el primer y segundo valor en la matriz `FILES` (`*.txt` y `*.sh`, respectivamente).

## Referencias

  - [Tutorial de secuencias de comandos de Bash] (https://www.shellscript.sh/)
  - [Guía avanzada de secuencias de comandos de Bash] (https://tldp.org/LDP/abs/html/)
  - [Guía de Bash para principiantes](https://www.softpanorama.org/Scripting/Shellorama/bash_guide_for_beginners.shtml)