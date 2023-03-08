---
title: El patrón Model-View-ViewModel (MVVM) en Spring Boot
description: 
published: true
date: 2023-02-08T12:32:37.802Z
tags: 
editor: markdown
dateCreated: 2023-02-08T12:32:36.158Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [The Model-View-ViewModel (MVVM) Pattern in Spring Boot***English** document is available*](/en/Knowledge-base/Spring-Boot/the-model-view-viewmodel-mvvm-pattern-in-spring-boot)
{.links-list}


# El patrón Model-View-ViewModel (MVVM) en Spring Boot

Model-View-ViewModel (MVVM) es un patrón de diseño arquitectónico que separa una aplicación en tres componentes lógicos principales Model, View y ViewModel.

La idea principal detrás de MVVM es trasladar la mayor parte de la lógica de negocios y la manipulación de datos de la capa View a la capa ViewModel. Esto ayuda a limpiar y desacoplar el código, lo que hace que la aplicación sea más mantenible y comprobable.

ViewModel luego expone datos relevantes para View a través de observables. ViewModel también expone comandos a los que View puede vincularse. Esto le da a ViewModel control total sobre View sin que View tenga que saber sobre ViewModel.

## Modelo

El modelo representa los datos y la lógica empresarial de la aplicación. En una aplicación MVVM, el modelo no conoce el modelo de vista y, por lo tanto, no tiene ninguna dependencia en el modelo de vista.

La Modelo es la encargada de gestionar los datos de la aplicación. Responde a las solicitudes de datos y notifica a los observadores cuando los datos cambian.

El modelo también contiene la lógica empresarial de la aplicación. Esta es la lógica que manipula los datos y hace cumplir las reglas comerciales de la aplicación.

## Vista

La vista es responsable de mostrar los datos e invocar operaciones en ViewModel.

La vista no debe contener ninguna lógica que manipule los datos o haga cumplir las reglas comerciales de la aplicación. Esta lógica debe estar contenida en ViewModel.

La Vista tampoco debe ser consciente de la existencia de ViewModel. ViewModel debe ser completamente independiente de View.

## Ver modelo

ViewModel es responsable de proporcionar datos a View y de procesar la entrada del usuario.

ViewModel expone datos a View a través de observables. ViewModel también expone comandos a los que View puede vincularse.

ViewModel contiene la lógica que manipula los datos y hace cumplir las reglas comerciales de la aplicación. ViewModel también contiene el código que es específico de View.

El modelo de vista no debe ser consciente de la vista. ViewModel debe ser completamente independiente de View.

## El enlace de datos

El enlace de datos es un mecanismo que permite que View y ViewModel se sincronicen automáticamente.

El enlace de datos permite que ViewModel actualice la vista automáticamente cuando cambien los datos en ViewModel. El enlace de datos también permite que View actualice ViewModel automáticamente cuando cambia la entrada del usuario.

El enlace de datos es un proceso bidireccional. Los cambios realizados en los datos de la vista se propagan al modelo de vista. Los cambios realizados en los datos de ViewModel se propagan a View.

El enlace de datos es un mecanismo poderoso que ayuda a mantener sincronizados View y ViewModel.

## Conclusión

Model-View-ViewModel (MVVM) es un patrón de diseño arquitectónico que separa una aplicación en tres componentes lógicos principales Model, View y ViewModel.

La idea principal detrás de MVVM es trasladar la mayor parte de la lógica de negocios y la manipulación de datos de la capa View a la capa ViewModel. Esto ayuda a limpiar y desacoplar el código, lo que hace que la aplicación sea más mantenible y comprobable.

ViewModel luego expone datos relevantes para View a través de observables. ViewModel también expone comandos a los que View puede vincularse. Esto le da a ViewModel control total sobre View sin que View tenga que saber sobre ViewModel.

El enlace de datos es un mecanismo que permite que View y ViewModel se sincronicen automáticamente. El enlace de datos es un mecanismo poderoso que ayuda a mantener sincronizados View y ViewModel.

## Referencias

1. [El patrón Modelo-Vista-Modelo de vista (MVVM)](https://msdn.microsoft.com/en-us/library/hh848246.aspx)
2. [Explicación de Model View ViewModel (MVVM)] (https://www.codeproject.com/Articles/100175/Model-View-ViewModel-MVVM-Explained)
3. [Kit de herramientas de luz MVVM] (http://www.mvvmlight.net/)
4. [Enlace de datos en MVVM](https://www.tutorialspoint.com/mvvm/mvvm_data_binding.htm)