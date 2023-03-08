---
title: Plotly Dash
description: 
published: true
date: 2023-02-11T14:17:42.218Z
tags: 
editor: markdown
dateCreated: 2023-02-11T14:17:39.884Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Plotly Dash***English** document is available*](/en/Knowledge-base/Dictionary/plotly-dash)
{.links-list}


# Descripción general
Plotly Dash es una biblioteca Python de código abierto para crear aplicaciones web interactivas. Está construido sobre la popular biblioteca Plotly y permite a los usuarios crear visualizaciones de datos altamente personalizables e interactivas. Dash es utilizado por científicos de datos, desarrolladores y analistas para crear potentes aplicaciones basadas en datos.

# Descripción
Plotly Dash es una biblioteca para crear aplicaciones web interactivas con Python. Está construido sobre la popular biblioteca Plotly y permite a los usuarios crear visualizaciones de datos altamente personalizables e interactivas. Dash es utilizado por científicos de datos, desarrolladores y analistas para crear potentes aplicaciones basadas en datos. Las aplicaciones de Dash se componen de dos partes: el front-end de la aplicación web y el código de Python que ejecuta la aplicación. El front-end de la aplicación web está escrito en HTML, CSS y JavaScript y es responsable de mostrar las visualizaciones de datos. El código de Python es responsable de crear las visualizaciones de datos y está escrito en Python.

Las aplicaciones de Dash son altamente personalizables e interactivas. Dash permite a los usuarios crear visualizaciones de datos con varias funciones interactivas, como zoom, panorámica y desplazamiento. Dash también proporciona una amplia variedad de gráficos y diagramas, incluidos gráficos de líneas, gráficos de barras, diagramas de dispersión y más.

# Características
Plotly Dash ofrece una amplia variedad de funciones para crear aplicaciones web interactivas con Python. Algunas de las características incluyen:

- Una amplia variedad de gráficos y diagramas, incluidos gráficos de líneas, gráficos de barras, diagramas de dispersión y más.
- Visualizaciones de datos altamente personalizables e interactivas con funciones como zoom, panorámica y desplazamiento.
- Fácil integración con otras bibliotecas de Python como Pandas, SciPy y NumPy.
- Fácil implementación de aplicaciones Dash en la web.

# Ejemplo
Aquí hay un ejemplo de una aplicación Dash simple que muestra un gráfico de líneas.

```python
import dash
import dash_core_components as dcc
import dash_html_components as html
import plotly.graph_objects as go

app = dash.Dash()

app.layout = html.Div([
    dcc.Graph(
        figure=go.Figure(
            data=[
                go.Scatter(
                    x=[1, 2, 3],
                    y=[4, 5, 6],
                    mode='lines'
                )
            ]
        )
    )
])

if __name__ == '__main__':
    app.run_server(debug=True)
```

# Pros y contras
Ventajas:

- Fácil de usar y altamente personalizable.
- Gran variedad de gráficos y gráficos.
- Fácil integración con otras bibliotecas de Python.
- Fácil despliegue de aplicaciones a la web.

Contras:

- No apto para aplicaciones grandes y complejas.
- Soporte limitado para otros lenguajes como JavaScript y HTML.

# Tecnología relacionada
Plotly Dash está relacionado con otras bibliotecas como Plotly, Bokeh y Matplotlib. Todas estas bibliotecas se utilizan para crear visualizaciones de datos en Python. Plotly y Dash están construidos sobre la popular biblioteca Plotly y permiten a los usuarios crear visualizaciones de datos altamente personalizables e interactivas. Bokeh es una biblioteca para crear visualizaciones de datos interactivas con Python y se utiliza para crear aplicaciones web interactivas. Matplotlib es una biblioteca para crear visualizaciones de datos estáticos con Python y se utiliza para crear visualizaciones de datos estáticos.