---
title: IP elásticas de AWS: asignación de direcciones IP estáticas para recursos en la nube
description: 
published: true
date: 2023-02-06T19:17:38.068Z
tags: 
editor: markdown
dateCreated: 2023-02-06T19:17:36.383Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [AWS Elastic IPs: Allocating Static IP Addresses for Cloud Resources***English** document is available*](/en/Knowledge-base/Cloud/aws-elastic-ips-allocating-static-ip-addresses-for-cloud-resources)
{.links-list}


# IP elásticas de AWS: asignación de direcciones IP estáticas para recursos en la nube

Las direcciones IP elásticas son direcciones IP estáticas diseñadas para la computación en la nube dinámica. Una dirección IP elástica está asociada con su cuenta de AWS. Con una dirección IP elástica, puede enmascarar la falla de una instancia o software reasignando rápidamente la dirección a otra instancia en su cuenta.

Una dirección IP elástica es una dirección IP pública que puede asignar a una instancia o una interfaz de red. Si asocia una dirección IP elástica con una instancia que ya tiene una dirección IP pública, la dirección IP pública original de la instancia se reemplaza con la dirección IP elástica. Si asocia una dirección IP elástica con una interfaz de red, la dirección IP se asocia con la dirección IP privada principal de la interfaz de red.

Puede asignar una nueva dirección IP elástica mientras crea una instancia mediante la consola de Amazon EC2. También puede asignar una nueva dirección IP elástica de su grupo existente de direcciones IP elásticas. Puede asociar una dirección IP elástica con una instancia o una interfaz de red en cualquier momento.

Si desasocia una dirección IP elástica de una instancia, a la instancia se le asigna una nueva dirección IP pública del grupo de direcciones IP públicas de Amazon EC2. Si desasocia una dirección IP elástica de una interfaz de red, la dirección IP privada principal de la interfaz de red se reasigna de la dirección IP elástica a otra dirección IP privada del conjunto de direcciones IP de la subred.

## Asignación de una dirección IP elástica

Para asignar una dirección IP elástica mediante la consola de Amazon EC2

1. Abra la consola de Amazon EC2 en https://console.aws.amazon.com/ec2/.

2. En el panel de navegación, seleccione **IPs elásticas**.

3. Elija **Asignar nueva dirección**.

4. Elija **Asignar**.

5. Elija **Cerrar**.

Su dirección IP elástica ahora está asignada y lista para asociarse con una instancia o interfaz de red.

## Asociación de una dirección IP elástica con una instancia

Para asociar una dirección IP elástica con una instancia mediante la consola de Amazon EC2

1. Abra la consola de Amazon EC2 en https://console.aws.amazon.com/ec2/.

2. En la lista de instancias, seleccione la instancia.

3. Elija **Acciones**, **Redes**, **Cambiar dirección IP elástica**, **Asociar dirección IP elástica**.

4. Seleccione la dirección IP elástica de la lista y luego elija **Asociar**.

Su instancia ahora está asociada con la dirección IP elástica.

## Asociación de una dirección IP elástica con una interfaz de red

Para asociar una dirección IP elástica con una interfaz de red mediante la consola de Amazon EC2

1. Abra la consola de Amazon EC2 en https://console.aws.amazon.com/ec2/.

2. En el panel de navegación, elija **Interfaces de red**.

3. Seleccione la interfaz de red y luego elija **Acción**, **Redes**, **Cambiar dirección IP elástica**, **Asociar dirección IP elástica**.

4. Seleccione la dirección IP elástica de la lista y luego elija **Asociar**.

Su interfaz de red ahora está asociada con la dirección IP elástica.

## Desasociar una dirección IP elástica

Para desasociar una dirección IP elástica de una instancia o interfaz de red mediante la consola de Amazon EC2

1. Abra la consola de Amazon EC2 en https://console.aws.amazon.com/ec2/.

2. En el panel de navegación, seleccione **IPs elásticas**.

3. Seleccione la casilla de verificación junto a la dirección IP elástica que desea desasociar.

4. Elija **Acciones**, **Redes**, **Cambiar dirección IP elástica**, **Desasociar dirección IP elástica**.

5. Cuando se le solicite confirmación, elija **Sí, desasociar**.

La dirección IP elástica ahora está desasociada de la instancia o la interfaz de red.

## Liberación de una dirección IP elástica

Puede liberar una dirección IP elástica cuando ya no la necesite. Para liberar una dirección IP elástica mediante la consola de Amazon EC2

1. Abra la consola de Amazon EC2 en https://console.aws.amazon.com/ec2/.

2. En el panel de navegación, seleccione **IPs elásticas**.

3. Seleccione la casilla de verificación junto a la dirección IP elástica que desea liberar.

4. Elija **Acciones**, **Redes**, **Cambiar dirección IP elástica**, **Liberar dirección IP elástica**.

5. Cuando se le solicite confirmación, seleccione **Sí, Liberar**.

La dirección IP elástica ahora está liberada y ya no está asociada con su cuenta de AWS.

## Información adicional

Para obtener más información acerca de las direcciones IP elásticas, consulte lo siguiente:

- Direcciones IP elásticas en la Guía del usuario de Amazon EC2 para instancias de Linux
- Direcciones IP elásticas en la Guía del usuario de Amazon EC2 para instancias de Windows

## Recursos externos

- Amazon EC2: direcciones IP elásticas (EIP)
- Planificación de direcciones IP de AWS
- Cómo usar las direcciones IP elásticas de AWS