---
title: D3.js
description: 
published: true
date: 2023-02-17T05:55:43.567Z
tags: 
editor: markdown
dateCreated: 2023-02-17T05:55:40.914Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [D3.js***English** document is available*](/en/Knowledge-base/Dictionary/d3-js)
{.links-list}


# Descripción general
D3.js es una biblioteca JavaScript de código abierto que se utiliza para crear visualizaciones de datos interactivas en navegadores web. Es una poderosa herramienta para el análisis de datos y la manipulación de documentos basados en datos.

# Descripción
D3.js es una biblioteca de JavaScript que permite a los desarrolladores crear visualizaciones de datos en navegadores web. Utiliza SVG, HTML y CSS para crear visualizaciones de datos interactivas, como gráficos de barras, gráficos de líneas y diagramas de dispersión. D3.js ofrece una amplia gama de funciones, que incluyen vinculación de datos, animación y manipulación dinámica de datos. También admite el uso de datos de fuentes externas, como archivos CSV, JSON y XML.

D3.js está diseñado para ser altamente modular y extensible, lo que permite a los desarrolladores crear visualizaciones de datos personalizadas. Tiene una amplia gama de complementos y bibliotecas que se pueden usar para agregar características y funcionalidades adicionales.

# Historia
D3.js fue creado por Mike Bostock en 2011. Inicialmente se lanzó como una biblioteca de JavaScript para crear visualizaciones de datos y documentos interactivos. Desde entonces, ha sido ampliamente adoptado por desarrolladores y científicos de datos para crear visualizaciones basadas en datos.

# Características
D3.js tiene una amplia gama de características que lo convierten en una poderosa herramienta para el análisis de datos y la manipulación de documentos basados en datos. Algunas de las características principales incluyen:

- Vinculación de datos: D3.js puede vincular datos a elementos DOM, lo que permite a los desarrolladores crear visualizaciones dinámicas de datos.
- Animación: D3.js admite animaciones y transiciones, lo que permite a los desarrolladores crear visualizaciones interactivas.
- Manipulación dinámica de datos: D3.js admite la manipulación de datos de fuentes externas, como archivos CSV, JSON y XML.
- Extensibilidad: D3.js está diseñado para ser altamente modular y extensible, lo que permite a los desarrolladores crear visualizaciones de datos personalizadas.

# Ejemplo
El siguiente es un ejemplo simple de un gráfico de barras creado con D3.js:

```
<script src="https://d3js.org/d3.v4.min.js"></script>
<script>
  var data = [4, 8, 15, 16, 23, 42];

  var x = d3.scaleLinear()
    .domain([0, d3.max(data)])
    .range([0, 420]);

  d3.select(".chart")
    .selectAll("div")
    .data(data)
    .enter().append("div")
    .style("width", function(d) { return x(d) + "px"; })
    .text(function(d) { return d; });
</script>

<div class="chart"></div>
```

# Pros y contras
D3.js es una poderosa herramienta para el análisis de datos y la manipulación de documentos basados en datos. Tiene una amplia gama de características y es altamente modular y extensible. Sin embargo, puede ser difícil de aprender y puede requerir una cantidad significativa de tiempo y esfuerzo para crear visualizaciones complejas.

# Tecnología relacionada
D3.js a menudo se usa junto con otras tecnologías, como React y Redux. React es una biblioteca de JavaScript para crear interfaces de usuario, mientras que Redux es una biblioteca de administración de estado para administrar el estado de la aplicación.

# Digresión
D3.js a menudo se usa junto con otras tecnologías, como React y Redux. React es una biblioteca de JavaScript para crear interfaces de usuario, mientras que Redux es una biblioteca de administración de estado para administrar el estado de la aplicación.

# Otros
D3.js es un proyecto de código abierto y es mantenido activamente por una gran comunidad de desarrolladores. También se utiliza en una variedad de industrias, como finanzas, atención médica y medios.