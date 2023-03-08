---
title: Complementos de Kubernetes: Agregar funcionalidad personalizada a kubectl
description: 
published: true
date: 2023-02-06T06:17:30.675Z
tags: 
editor: markdown
dateCreated: 2023-02-06T06:17:25.039Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Kubernetes Plugins: Adding Custom Functionality to kubectl***English** document is available*](/en/Knowledge-base/Kubernetes/kubernetes-plugins-adding-custom-functionality-to-kubectl)
{.links-list}


# Complementos de Kubernetes: Agregar funcionalidad personalizada a kubectl

Kubernetes es una plataforma de orquestación de código abierto para automatizar la implementación, el escalado y la gestión de aplicaciones en contenedores. kubectl es una herramienta de línea de comandos para interactuar con un clúster de Kubernetes.

Si bien kubectl es extremadamente poderoso, hay momentos en los que es posible que desee agregar una funcionalidad personalizada para que sea aún más eficiente para su flujo de trabajo particular. Ahí es donde entran los complementos de Kubernetes.

Un complemento de Kubernetes es un fragmento de código que amplía la funcionalidad de kubectl. En este artículo, veremos cómo crear un complemento de Kubernetes y cómo usarlo para agregar funciones personalizadas a kubectl.

## Creación de un complemento de Kubernetes

Los complementos de Kubernetes están escritos en Go. El código del complemento debe compilarse en un binario y colocarse en su RUTA. El binario debe llamarse kubectl-{plugin-name}.

El complemento binario debe implementar la siguiente interfaz:

```go
type KubernetesPlugin interface {
	Run([]string) error
}
```

Se llama al método Run() cuando se ejecuta el complemento y se le pasa una serie de cadenas que contienen los argumentos del complemento.

Echemos un vistazo a un complemento de ejemplo que imprime un saludo:

```go
package main

import "fmt"

type GreetPlugin struct{}

func (p *GreetPlugin) Run(args []string) error {
	fmt.Println("Hello, world!")
	return nil
}

func main() {
	plugin := &GreetPlugin{}
	plugin.Run(nil)
}
```

Para compilar el complemento, podemos usar el comando go build:

```
$ go build -o kubectl-greet ./greet.go
```

Una vez que se crea el complemento, podemos agregarlo a nuestra RUTA y probarlo:

```
$ export PATH=$PATH:$(pwd)
$ kubectl greet
Hello, world!
```

## Agregar funcionalidad a kubectl

Ahora que hemos creado un complemento básico de Kubernetes, veamos cómo podemos usarlo para agregar funciones personalizadas a kubectl.

Para este ejemplo, crearemos un complemento que imprima una lista de los pods en un espacio de nombres determinado. Comenzaremos definiendo una estructura que contenga la información que necesitamos pasar al complemento:

```go
type PodListOptions struct {
	Namespace string
}
```

A continuación, crearemos una función que analice los argumentos del complemento e inicialice una estructura PodListOptions:

```go
func parseArgs(args []string) (*PodListOptions, error) {
	if len(args) == 0 {
		return nil, fmt.Errorf("namespace is required")
	}
	options := &PodListOptions{
		Namespace: args[0],
	}
	return options, nil
}
```

Ahora podemos actualizar el método Run() de nuestro complemento para llamar a nuestra función parseArgs() y usar la estructura PodListOptions resultante para imprimir una lista de los pods en el espacio de nombres dado:

```go
func (p *PodListPlugin) Run(args []string) error {
	options, err := parseArgs(args)
	if err != nil {
		return err
	}
	pods, err := p.listPods(options.Namespace)
	if err != nil {
		return err
	}
	for _, pod := range pods {
		fmt.Println(pod)
	}
	return nil
}
```

Finalmente, necesitaremos implementar el método listPods() para obtener la lista de pods de la API de Kubernetes:

```go
func (p *PodListPlugin) listPods(namespace string) ([]string, error) {
	// TODO: Implement me!
}
```

Con nuestro complemento completo, podemos agregarlo a nuestra RUTA y probarlo:

```
$ export PATH=$PATH:$(pwd)
$ kubectl pod-list my-namespace
pod-1
pod-2
pod-3
```

Como puede ver, los complementos de Kubernetes brindan una excelente manera de agregar funciones personalizadas a kubectl. Con solo unas pocas líneas de código, puede hacer que kubectl funcione exactamente como lo desea.

## Referencias

https://kubernetes.io/docs/reference/using-api/extending-api/
https://kubernetes.io/docs/tasks/extend-kubectl/kubectl-plugins/