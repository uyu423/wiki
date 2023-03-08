---
title: SOAP
description: 
published: true
date: 2023-02-05T23:17:50.818Z
tags: 
editor: markdown
dateCreated: 2023-02-05T23:17:44.500Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [SOAP***English** document is available*](/en/Knowledge-base/Dictionary/soap)
{.links-list}


# Descripción general
El Protocolo simple de acceso a objetos (SOAP) es un protocolo utilizado para intercambiar datos entre dos aplicaciones a través de Internet. Es un protocolo basado en XML que utiliza HTTP o HTTPS como protocolo de transporte. SOAP se usa típicamente en servicios web y otras aplicaciones informáticas distribuidas.

# Descripción
SOAP (Protocolo simple de acceso a objetos) es un protocolo basado en XML que se utiliza para intercambiar datos entre dos aplicaciones a través de Internet. Es un protocolo basado en XML que utiliza HTTP o HTTPS como protocolo de transporte. SOAP es un protocolo ligero que se utiliza para aplicaciones informáticas distribuidas, como los servicios web. Se basa en el lenguaje XML y está diseñado para ser independiente de la plataforma.

Los mensajes SOAP se envían en una estructura de sobre, que contiene un encabezado y un cuerpo. El encabezado contiene información sobre el mensaje, como el remitente y el receptor, mientras que el cuerpo contiene los datos reales que se intercambian. El cuerpo del mensaje suele estar codificado en XML y contiene los datos que se intercambian.

SOAP se usa típicamente en servicios web y otras aplicaciones informáticas distribuidas. Está diseñado para ser simple y extensible, y generalmente se usa junto con otros protocolos, como HTTP o HTTPS. SOAP también se utiliza en aplicaciones informáticas distribuidas, como bases de datos distribuidas y sistemas de objetos distribuidos.

# Historia
SOAP fue desarrollado originalmente por Microsoft en 1998 como parte de su iniciativa .NET. Fue diseñado como un protocolo ligero para aplicaciones informáticas distribuidas, como servicios web. Desde entonces, se ha convertido en un protocolo ampliamente utilizado para aplicaciones informáticas distribuidas.

La primera versión de SOAP se lanzó en 1999 y estaba basada en XML. Desde entonces, ha sido revisado varias veces, siendo la última versión SOAP 1.2, que se lanzó en 2003.

# Características
SOAP es un protocolo ligero que se utiliza para aplicaciones informáticas distribuidas. Está diseñado para ser simple y extensible, y generalmente se usa junto con otros protocolos, como HTTP o HTTPS. SOAP también se utiliza en aplicaciones informáticas distribuidas, como bases de datos distribuidas y sistemas de objetos distribuidos.

Las características principales de SOAP incluyen:

- Es independiente de la plataforma y se puede utilizar en cualquier plataforma.
- Está basado en el lenguaje XML.
- Admite múltiples tipos de datos, incluidas cadenas, enteros y flotantes.
- Admite múltiples protocolos de transporte, como HTTP y HTTPS.
- Admite múltiples estilos de codificación, como RPC y documento/literal.
- Admite características de seguridad, como encriptación y autenticación.

# Ejemplo
A continuación se muestra un ejemplo de un mensaje SOAP. Este mensaje se envía desde un cliente a un servidor para solicitar un servicio web.

```
<Envelope>
  <Header>
    <To>http://www.example.com/webservice</To>
    <Action>http://www.example.com/getData</Action>
  </Header>
  <Body>
    <GetData>
      <ID>12345</ID>
    </GetData>
  </Body>
</Envelope>
```

# Pros y contras
Las principales ventajas de SOAP son:

- Es independiente de la plataforma y se puede utilizar en cualquier plataforma.
- Se basa en el lenguaje XML, que está bien soportado y es ampliamente utilizado.
- Admite múltiples tipos de datos, incluidas cadenas, enteros y flotantes.
- Admite múltiples protocolos de transporte, como HTTP y HTTPS.
- Admite múltiples estilos de codificación, como RPC y documento/literal.
- Admite características de seguridad, como encriptación y autenticación.

Las principales desventajas de SOAP son:

- Es complejo y puede ser difícil de implementar.
- Puede ser lento e ineficiente debido a la sobrecarga de la codificación XML.
- Puede ser difícil de depurar debido a la complejidad de la codificación XML.

# Controversia
SOAP ha sido objeto de cierta controversia en los últimos años, debido a su complejidad y al hecho de estar basado en el lenguaje XML. Algunos desarrolladores han argumentado que SOAP es demasiado complejo y debería reemplazarse con protocolos más simples, como JSON.

# Tecnología relacionada
JSON (Notación de objetos de JavaScript) es un formato ligero de intercambio de datos que a menudo se usa como alternativa a SOAP. JSON es más simple y eficiente que SOAP, y se está volviendo cada vez más popular para las aplicaciones informáticas distribuidas.

# Digresión
El Protocolo simple de acceso a objetos (SOAP) es un protocolo basado en XML que se utiliza para intercambiar datos entre dos aplicaciones a través de Internet. Está diseñado para ser independiente de la plataforma y normalmente se usa en aplicaciones informáticas distribuidas, como los servicios web. SOAP se está volviendo cada vez más popular debido a su simplicidad y extensibilidad, y a menudo se usa junto con otros protocolos, como HTTP o HTTPS.

# Otros
SOAP es un estándar abierto y lo mantiene el World Wide Web Consortium (W3C). Es compatible con muchos lenguajes de programación, como Java, .NET y PHP.