---
title: Robert C. Martin
description: 
published: true
date: 2023-02-02T17:24:40.957Z
tags: 
editor: markdown
dateCreated: 2023-02-02T17:24:38.979Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Robert C. Martin***English** document is available*](/en/Knowledge-base/Dictionary/robert-c-martin)
{.links-list}


# Descripción general
Robert C. Martin (también conocido como el tío Bob) es un reconocido ingeniero de software, autor y orador. Es conocido por su trabajo sobre principios de diseño de software, como los principios SOLID, y sus escritos sobre ingeniería de software y elaboración de software. Es un firme defensor de las prácticas ágiles de desarrollo de software y ha escrito varios libros sobre el tema.

# Descripción
Robert C. Martin es ingeniero de software, autor y orador, conocido por su trabajo sobre los principios de diseño de software, como los principios SOLID, y sus escritos sobre ingeniería de software y elaboración de software. Es un firme defensor de las prácticas ágiles de desarrollo de software y ha escrito varios libros sobre el tema.

Martin es el fundador de la exitosa empresa de consultoría Object Mentor Inc. y es autor de varios libros, entre ellos "Clean Code: A Handbook of Agile Software Craftsmanship" y "The Clean Coder: A Code of Conduct for Professional Programmers". También es el creador del popular marco de diseño y arquitectura de software, Uncle Bob's Architecture.

Martin es un firme defensor de la artesanía del software y de la importancia de escribir un código limpio y fácil de mantener. Es un orador frecuente en conferencias y ha dado muchas charlas sobre temas como el diseño de software, las pruebas de software y las mejores prácticas de ingeniería de software.

# Historia
Robert C. Martin nació en 1952 en Pensilvania y se graduó de la Universidad de Massachusetts en 1976 con una licenciatura en Ciencias de la Computación. Después de graduarse, comenzó a trabajar como ingeniero de software y desde entonces ha ocupado varios puestos en la industria del software.

A fines de la década de 1980, Martin comenzó a trabajar en los principios SOLID, que son un conjunto de cinco principios de diseño de software que brindan un marco para crear software mantenible y extensible. A mediados de la década de 1990, comenzó a escribir sobre ingeniería de software y elaboración de software, y en 2000 fundó Object Mentor Inc., una exitosa firma de consultoría.

Desde entonces, Martin ha escrito varios libros, incluidos "Clean Code: A Handbook of Agile Software Craftsmanship" y "The Clean Coder: A Code of Conduct for Professional Programmers". También es el creador del popular marco de diseño y arquitectura de software, Uncle Bob's Architecture.

# Características
Los principios SOLID son la piedra angular del trabajo de Robert C. Martin y son un conjunto de cinco principios de diseño de software que proporcionan un marco para crear software mantenible y extensible. Estos principios son:

- Principio de Responsabilidad Única: Una clase debe tener una y sólo una razón para cambiar.
- Principio abierto-cerrado: las entidades de software deben estar abiertas para la extensión, pero cerradas para la modificación.
- Principio de sustitución de Liskov: las clases derivadas deben ser sustituibles por sus clases base.
- Principio de segregación de la interfaz: los clientes no deben verse obligados a depender de métodos que no utilizan.
- Principio de Inversión de Dependencia: Depender de abstracciones, no de concreciones.

Martin también es un firme defensor de la artesanía del software y de la importancia de escribir un código limpio y fácil de mantener. Ha escrito varios libros y dado muchas charlas sobre temas como el diseño de software, las pruebas de software y las mejores prácticas de ingeniería de software.

# Ejemplo
Como ejemplo de cómo se pueden aplicar los principios SOLID, considere el siguiente código:

```
class Database {
  public void save(String data) {
    // code to save data to the database
  }
 
  public void delete(String data) {
    // code to delete data from the database
  }
}
```

Este código viola el principio de responsabilidad única, ya que tanto el guardado como la eliminación de datos se manejan en la misma clase. Para cumplir con el principio, el código debe refactorizarse para crear dos clases separadas: una para guardar datos y otra para eliminar datos.

# Pros y contras
Los principios SOLID son un conjunto de cinco principios de diseño de software que proporcionan un marco para crear software mantenible y extensible. El principal beneficio de estos principios es que facilitan el mantenimiento y la extensión del código, ya que cada clase tiene una única responsabilidad y está abierta a la extensión pero cerrada a la modificación.

Sin embargo, existen algunos inconvenientes en estos principios. Por ejemplo, puede ser difícil adherirse al principio de responsabilidad única al diseñar sistemas complejos, y puede llevar más tiempo y esfuerzo refactorizar el código para adherirse a los principios.

# Controversia
El trabajo de Martin sobre los principios de diseño de software y la artesanía del software ha sido objeto de cierta controversia. Algunos han argumentado que los principios SOLID son demasiado rígidos y pueden conducir a un código demasiado complicado. Otros han argumentado que el enfoque de Martin en la artesanía del software puede conducir a un enfoque en el código "perfecto", lo que puede llevar mucho tiempo y no siempre ser necesario.

# Tecnología relacionada
Los principios SOLID están estrechamente relacionados con el principio DRY (Don't Repeat Yourself), que establece que el código no debe repetirse innecesariamente. El principio DRY se usa a menudo junto con los principios SOLID para crear código mantenible y extensible.

# Digresión
Martin también es un firme defensor de las prácticas ágiles de desarrollo de software. Ha escrito varios libros sobre el tema, incluidos "Desarrollo de software ágil: principios, patrones y prácticas" y "El manifiesto ágil".

# Otros
Además de su trabajo en diseño de software y desarrollo ágil de software, Martin también es un firme defensor de las pruebas de software. Ha escrito varios libros sobre el tema, incluidos "El arte de las pruebas de software" y "Desarrollo basado en pruebas: con el ejemplo".