---
title: Técnicas de depuración del kernel de Linux
description: 
published: true
date: 2023-02-11T21:32:59.164Z
tags: 
editor: markdown
dateCreated: 2023-02-11T21:32:52.287Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Linux Kernel Debugging Techniques***English** document is available*](/en/Knowledge-base/Linux/linux-kernel-debugging-techniques)
{.links-list}


# Técnicas de depuración del kernel de Linux

El kernel de Linux es una pieza compleja de software con muchas partes móviles. Como tal, puede ser difícil depurar cuando las cosas van mal. Este artículo explorará algunas de las técnicas más útiles para depurar el kernel de Linux.

## Imprimiendo Mensajes del Kernel

Una de las técnicas más básicas y útiles para depurar el kernel es imprimir mensajes en el registro del kernel. El registro del kernel es un registro de toda la actividad del kernel que se almacena en el archivo `/var/log/kern.log`. Los mensajes se pueden imprimir en el registro del kernel usando la función `printk`.

La función `printk` toma una cadena de formato y un número variable de argumentos. La cadena de formato es similar a la de la función `printf` en el espacio de usuario, pero con algunas diferencias importantes. Primero, la cadena de formato `printk` puede contener especificadores de formato para `%p`, `%t` y `%i`, que son, respectivamente, la dirección de la tarea actual, la hora actual en santiamén y la ID de la CPU actual. . En segundo lugar, la cadena de formato `printk` puede contener especificadores `%ln`, que indican el tamaño del siguiente argumento en bytes. Finalmente, la cadena de formato `printk` puede contener especificadores `%s`, que imprimen la representación de cadena del siguiente argumento.

Aquí hay un ejemplo simple del uso de `printk`:

```c
#include <linux/kernel.h>

void print_message(void)
{
    printk("This is a test message.\n");
}
```

## Usando el Depurador del Kernel

El depurador del kernel, o `kdb`, es una poderosa herramienta para depurar el kernel. `kdb` se puede usar para examinar y cambiar las estructuras de datos del núcleo, establecer puntos de interrupción y código del núcleo de un solo paso. `kdb` se invoca agregando la opción de línea de comandos `kdb` a los parámetros de arranque del núcleo. Cuando el kernel se inicia con esta opción, `kdb` se ingresará automáticamente cuando ocurra un pánico del kernel.

`kdb` también se puede ingresar manualmente presionando la combinación de teclas `Ctrl-Alt-SysRq-K`. Una vez que se ingresa `kdb`, se mostrará el mensaje `kdb>`. Los comandos `kdb` se pueden ingresar en este indicador. Escriba `ayuda` en el indicador `kdb>` para ver una lista de los comandos disponibles.

Uno de los comandos `kdb` más útiles es `bt`. Este comando imprime un seguimiento de la pila de llamadas actual. Esto puede ser útil para comprender dónde ocurrió un kernel panic y por qué.

Otro comando `kdb` útil es `md`. Este comando se puede utilizar para examinar el contenido de la memoria. Por ejemplo, el comando `md 0xffffffff80000000 0x200` imprimirá el contenido de los primeros 512 bytes de la memoria del núcleo.

## Uso de la sonda del núcleo

La sonda del kernel, o `kprobe`, es una función del kernel de Linux que permite la ejecución de código de espacio de usuario cuando se llama a una función específica del kernel. `kprobe` se puede utilizar para instrumentar el núcleo con fines de depuración.

`kprobe` se invoca utilizando la opción de línea de comandos `kprobe`. La opción `kprobe` toma un nombre de función del núcleo y una función de controlador de espacio de usuario. La función del controlador se ejecuta cada vez que se llama a la función del kernel. La función del controlador tiene acceso a los argumentos de la función del kernel y al valor devuelto.

Aquí hay un ejemplo simple del uso de `kprobe`:

```c
#include <linux/kprobes.h>

static int handler_kprobe(struct kprobe *p, void *data)
{
    printk("kprobe hit!\n");
    return 0;
}

static struct kprobe kp = {
    .symbol_name    = "do_fork",
    .handler        = handler_kprobe,
};

static int __init kprobe_init(void)
{
    register_kprobe(&kp);
    return 0;
}

static void __exit kprobe_exit(void)
{
    unregister_kprobe(&kp);
}

module_init(kprobe_init)
module_exit(kprobe_exit)
```

En este ejemplo, se registra un `kprobe` para la función del núcleo `do_fork`. Cada vez que se llama a `do_fork`, se ejecuta la función `handler_kprobe`. La función `handler_kprobe` simplemente imprime un mensaje en el registro del kernel.

## Usando el Rastreo del Kernel

El seguimiento del kernel, o `ktrace`, es una característica del kernel de Linux que permite el seguimiento de la actividad del kernel. `ktrace` se puede utilizar para instrumentar el kernel con fines de depuración.

`ktrace` se invoca utilizando la opción de línea de comandos `ktrace`. La opción `ktrace` toma un tamaño de búfer de seguimiento y un nombre de archivo de seguimiento. El búfer de seguimiento se utiliza para almacenar eventos de seguimiento. El archivo de seguimiento se utiliza para almacenar una representación legible por humanos de los eventos de seguimiento.

Aquí hay un ejemplo simple del uso de `ktrace`:

```c
#include <linux/ktrace.h>

static int __init ktrace_init(void)
{
    ktrace("/tmp/ktrace.out", 1024);
    return 0;
}

static void __exit ktrace_exit(void)
{
    ktrace_stop();
}

module_init(ktrace_init)
module_exit(ktrace_exit)
```

En este ejemplo, `ktrace` está configurado para rastrear la actividad del kernel en el archivo `/tmp/ktrace.out`. El búfer de seguimiento se establece en 1024 KB.

## Uso del analizador de kernel

El generador de perfiles del kernel, o `kprof`, es una característica del kernel de Linux que permite la creación de perfiles del código del kernel. `kprof` se puede utilizar para recopilar información de rendimiento sobre el kernel.

`kprof` se invoca utilizando la opción de línea de comandos `kprof`. La opción `kprof` toma un intervalo de generación de perfiles y un nombre de archivo de seguimiento. El intervalo de perfilado es el tiempo, en nanosegundos, entre muestras. El archivo de seguimiento se utiliza para almacenar la información de creación de perfiles.

Aquí hay un ejemplo simple del uso de `kprof`:

```c
#include <linux/kprof.h>

static int __init kprof_init(void)
{
    kprof("/tmp/kprof.out", 10000000);
    return 0;
}

static void __exit kprof_exit(void)
{
    kprof_stop();
}

module_init(kprof_init)
module_exit(kprof_exit)
```

En este ejemplo, `kprof` está configurado para perfilar el código del kernel cada 10 milisegundos. La información de creación de perfiles se almacena en el archivo `/tmp/kprof.out`.

## Conclusión

Este artículo ha explorado algunas de las técnicas más útiles para depurar el kernel de Linux. Estas técnicas se pueden utilizar para depurar pánicos del kernel, problemas de rendimiento y otros problemas.