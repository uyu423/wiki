---
title: Cómo crear una experiencia de realidad virtual (VR)
description: 
published: true
date: 2023-02-16T21:17:59.429Z
tags: 
editor: markdown
dateCreated: 2023-02-16T21:17:57.110Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [How to Create a Virtual Reality (VR) Experience***English** document is available*](/en/Knowledge-base/Common/how-to-create-a-virtual-reality-vr-experience)
{.links-list}


# Cómo crear una experiencia de realidad virtual (VR)

Con el reciente lanzamiento de varios visores de realidad virtual asequibles y accesibles, nunca ha habido un mejor momento para comenzar a desarrollar experiencias de realidad virtual. En este artículo, le mostraremos cómo comenzar a desarrollar para VR, incluida una descripción general de los diferentes tipos de visores VR y cómo crear una experiencia VR desde cero.

## Tipos de auriculares VR

Hay dos tipos principales de auriculares VR: atados y móviles. Los auriculares con cable, como Oculus Rift y HTC Vive, están conectados a una poderosa PC o consola de juegos y requieren mucha potencia de procesamiento para ejecutar aplicaciones de realidad virtual. Los auriculares móviles, como Samsung Gear VR y Google Daydream, utilizan un teléfono inteligente como unidad de visualización y procesamiento. La realidad virtual móvil es más asequible y fácil de usar, pero la realidad virtual conectada puede ofrecer una experiencia más inmersiva.

## Primeros pasos con el desarrollo de realidad virtual

Si recién está comenzando con el desarrollo de VR, le recomendamos comenzar con un auricular VR móvil. Estos auriculares son más asequibles y fáciles de usar, y hay muchas aplicaciones de realidad virtual disponibles para ellos.

Una vez que tenga un auricular VR, deberá instalar un SDK VR. Los SDK de realidad virtual más populares son Oculus Mobile SDK, Google VR SDK y Unity 3D. Oculus Mobile SDK solo es compatible con visores de la marca Oculus, como Gear VR. Google VR SDK es compatible con una amplia gama de auriculares, incluidos Daydream, Cardboard y Gear VR. Unity 3D es un motor de juego popular que tiene soporte integrado para el desarrollo de realidad virtual.

Una vez que haya instalado un auricular VR y SDK, estará listo para comenzar a desarrollar aplicaciones VR. Recomendamos consultar algunos de los siguientes recursos para comenzar:

- La [Guía de introducción al SDK móvil de Oculus](https://developer.oculus.com/documentation/mobilesdk/latest/concepts/mobile-getting-started/)
- La [Guía de introducción al SDK de Google VR para Android](https://developers.google.com/vr/android/get-started)
- La [Guía de desarrollo de realidad virtual en 3D de Unity](https://learn.unity.com/tutorial/virtual-reality-development)

## Crear una experiencia de realidad virtual desde cero

Ahora que tiene un auricular VR y SDK instalados, está listo para comenzar a desarrollar aplicaciones VR. En esta sección, le mostraremos cómo crear una experiencia de realidad virtual básica desde cero.

Primero, deberá crear un nuevo proyecto de Unity. Abra Unity, haga clic en "Nuevo proyecto" y asigne un nombre a su proyecto. Luego, seleccione la casilla de verificación "Compatible con realidad virtual" y haga clic en "Crear proyecto".

A continuación, deberá crear una escena. Una escena es una colección de objetos que componen tu experiencia de realidad virtual. Para crear una escena, seleccione "GameObject" > "Objeto 3D" > "Plano" en el menú de Unity. Esto creará un objeto plano en tu escena.

Ahora, deberá agregar algo de contenido a su escena. Para hacer esto, puede crear sus propios modelos 3D o usar recursos gratuitos de la tienda de recursos de Unity. Para este ejemplo, usaremos un recurso gratuito de la tienda de recursos de Unity. Para agregar un activo a su escena, seleccione "Activos" > "Importar paquete" > "Almacén de activos" en el menú de Unity. Esto abrirá la ventana de la tienda de recursos de Unity. Busque "activos gratuitos" y encuentre un activo que le guste. Para este ejemplo, usaremos el activo "Paquete de árboles Low Poly gratis". Una vez que haya encontrado un activo que le guste, haga clic en "Importar" para agregarlo a su proyecto.

Una vez que se importa el activo, puede agregarlo a su escena arrastrándolo desde la ventana "Proyecto" a la ventana "Jerarquía". Esto creará una instancia del recurso en su escena.

Ahora que tiene una escena con algo de contenido, está listo para agregar algo de interactividad. Para hacer esto, deberá agregar algunos scripts. Un script es una pieza de código que le dice a los objetos de tu juego qué hacer. Para crear un script, seleccione "Activos" > "Crear" > "Script C# " en el menú de Unity. Asigne un nombre a su secuencia de comandos y haga clic en "Crear". Esto abrirá el script en su editor de código predeterminado.

Para este ejemplo, agregaremos un script que haga que nuestro árbol se balancee hacia adelante y hacia atrás cuando el jugador lo mire. Para ello, utilizaremos el método de entrada "Mirada", que permite al jugador controlar el juego con la mirada.

Primero, necesitaremos agregar algo de código a nuestro script para que reconozca el método de entrada Gaze. Agrega el siguiente código a tu script:

```csharp
public class TreeSwing : MonoBehaviour {

// Use this for initialization
void Start () {
	
}

// Update is called once per frame
void Update () {
	
}
}
```

A continuación, necesitaremos agregar algo de código para hacer que nuestro árbol se balancee de un lado a otro. Agrega el siguiente código a tu script:

```csharp
public class TreeSwing : MonoBehaviour {

public float swingAmount = 10.0f;

// Use this for initialization
void Start () {
	
}

// Update is called once per frame
void Update () {
	transform.rotation = 
		Quaternion.Euler(0, Input.GetAxis("Horizontal") * swingAmount, 0);
}
}
```

Este código hará que nuestro árbol se balancee de un lado a otro según la mirada del jugador.

Finalmente, necesitaremos agregar nuestro script a nuestro objeto de árbol. Para hacer esto, seleccione el objeto de árbol en la ventana "Jerarquía" y haga clic en el botón "Agregar componente". Luego, seleccione "Scripts" > "TreeSwing" de la lista de componentes.

Ahora que nuestro script está agregado a nuestro árbol, nuestro árbol se moverá de un lado a otro cuando el jugador lo mire.

¡Felicidades! Acabas de crear tu primera experiencia de realidad virtual.

## Recursos para lecturas adicionales

- La [Guía de introducción al SDK móvil de Oculus](https://developer.oculus.com/documentation/mobilesdk/latest/concepts/mobile-getting-started/)
- La [Guía de introducción al SDK de Google VR para Android](https://developers.google.com/vr/android/get-started)
- La [Guía de desarrollo de realidad virtual en 3D de Unity](https://learn.unity.com/tutorial/virtual-reality-development)
- La [Guía para desarrolladores de Oculus Rift](https://developer.oculus.com/documentation/pcsdk/latest/concepts/index/)
- La [Guía para desarrolladores de HTC Vive](https://developer.vive.com/resources/knowledgebase/category_view/?catid=7)
- La [Guía para desarrolladores de Samsung Gear VR] (https://developer.samsung.com/gear-vr)
- La [Guía para desarrolladores de Google Daydream](https://developers.google.com/daydream)