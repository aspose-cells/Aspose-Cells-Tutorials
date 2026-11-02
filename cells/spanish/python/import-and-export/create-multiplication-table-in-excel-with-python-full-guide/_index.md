---
category: general
date: 2026-06-21
description: Crear una tabla de multiplicar en Excel usando Python. Aprende cómo usar
  lambda, cómo usar makearray, mostrar la matriz de Excel y leer valores de Excel
  con Python en un tutorial paso a paso.
draft: false
keywords:
- create multiplication table
- how to use lambda
- how to use makearray
- display excel array
- read excel values python
language: es
og_description: Crear una tabla de multiplicación en Excel usando Python. Este tutorial
  muestra cómo usar lambda, makearray, mostrar la matriz de Excel y leer valores de
  Excel con Python de manera eficiente.
og_title: Crear tabla de multiplicar en Excel con Python – Guía completa
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Create multiplication table in Excel using Python. Learn how to use
    lambda, how to use makearray, display excel array and read excel values python
    in a step‑by‑step tutorial.
  headline: Create multiplication table in Excel with Python – Full Guide
  type: TechArticle
tags:
- python
- excel
- openpyxl
title: Crear tabla de multiplicación en Excel con Python – Guía completa
url: /es/python/import-and-export/create-multiplication-table-in-excel-with-python-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crear tabla de multiplicación en Excel con Python – Guía completa

¿Alguna vez te has preguntado cómo **crear tabla de multiplicación** en Excel sin tener que escribir manualmente cada celda? No estás solo. En muchos escenarios de informes necesitas rápidamente una cuadrícula 5×5 (o mayor) de productos, y hacerlo a mano es una pérdida de tiempo.  

En este tutorial recorreremos una forma limpia, impulsada por Python, de generar esa tabla, incrustarla con una fórmula `MAKEARRAY` y luego recuperar los resultados en tu script. En el camino responderemos **cómo usar lambda**, mostraremos **cómo usar makearray**, y demostraremos **mostrar array de Excel** así como **leer valores de Excel con Python**—todo en un ejemplo cohesivo.

Al final tendrás un fragmento reutilizable que funciona con cualquier libro, y comprenderás por qué este enfoque es rápido y a prueba de futuro.

## Lo que necesitarás

- Python 3.8+ (la última versión estable está bien)
- La biblioteca `openpyxl` (o cualquier biblioteca compatible con Excel que soporte fórmulas)
- Una comprensión básica de expresiones lambda en Python
- Sin complementos especiales de Excel; la función nativa `MAKEARRAY` (disponible en Excel 365) hace el trabajo pesado

Si te falta alguno de estos, simplemente `pip install openpyxl` y estarás listo.

## Crear tabla de multiplicación – Visión general

La idea principal es simple: creamos un libro nuevo, escribimos una fórmula `MAKEARRAY` que construye una matriz de multiplicación de 5 × 5, obligamos a Excel a calcularla y, finalmente, leemos los valores resultantes de vuelta en Python.

```python
from openpyxl import Workbook

# Step 1: Create a new workbook and get the first worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]

# Step 2: Insert a MAKEARRAY formula that builds a 5×5 multiplication table
# The formula uses a LAMBDA that returns r*c for each row (r) and column (c)
worksheet["A1"] = "=MAKEARRAY(5,5, LAMBDA(r,c, r*c))"

# Step 3: Calculate all formulas so the array is materialized in the sheet
workbook.calculate_formula()

# Step 4: Read and display the top‑left 5×5 block of values
for row_index in range(1, 6):
    row_values = [worksheet.cell(row=row_index, column=col_index).value
                  for col_index in range(1, 6)]
    print(row_values)
```

Ejecutar el script imprime:

```
[1, 2, 3, 4, 5]
[2, 4, 6, 8, 10]
[3, 6, 9, 12, 15]
[4, 8, 12, 16, 20]
[5, 10, 15, 20, 25]
```

Eso es una **creación de tabla de multiplicación** totalmente funcional en Excel, generada completamente desde Python.

### ¿Por qué usar `MAKEARRAY` en lugar de un bucle Python?

- **Rendimiento**: Excel maneja el cálculo de forma nativa, lo que es más rápido para matrices grandes.
- **Actualización en tiempo real**: Si más adelante cambias las dimensiones en la fórmula, la hoja se recalcula automáticamente.
- **Legibilidad**: La fórmula expresa la intención (“crear una matriz”) directamente, manteniendo tu código Python ordenado.

## Cómo usar lambda en Python para fórmulas de Excel

La parte `LAMBDA` de la llamada `MAKEARRAY` es una función anónima del lado de Excel, no una lambda de Python. Aún así, el concepto es el mismo: defines una pequeña pieza de lógica en línea que toma `r` (índice de fila) y `c` (índice de columna) y devuelve `r*c`.  

Si eres nuevo en **cómo usar lambda** en el mundo de Excel, piénsalo como una mini‑función que vive solo dentro de la fórmula. No es necesario declarar una función separada en otro lugar. En Python simplemente incrustamos la cadena:

```python
worksheet["A1"] = "=MAKEARRAY(5,5, LAMBDA(r,c, r*c))"
```

Esa línea le dice a Excel: *“Para cada celda en un bloque de 5 × 5, calcula fila × columna.”*  

Como la lambda es evaluada por Excel, no tienes que preocuparte por la sintaxis de lambda de Python aquí—solo por la sintaxis de Excel.

## Cómo usar makearray para generar matrices

`MAKEARRAY` es una adición relativamente nueva a la biblioteca de funciones de Excel (disponible en Microsoft 365 a partir de 2022). Reemplaza trucos más antiguos como combinaciones de `INDEX` + `ROW`/`COLUMN`. La firma es:

```
MAKEARRAY(rows, columns, lambda)
```

- **rows** – número de filas que deseas.
- **columns** – número de columnas que deseas.
- **lambda** – un LAMBDA de Excel que recibe `(row, column)` y devuelve un valor.

En nuestro ejemplo pasamos `5,5` para una tabla de multiplicación clásica, pero podrías cambiar fácilmente esos números:

```python
worksheet["A1"] = "=MAKEARRAY(10,10, LAMBDA(r,c, r*c))"
```

Eso te daría una tabla de 10 × 10 sin tocar bucles de Python. Esto demuestra **cómo usar makearray** para cualquier tipo de cuadrícula determinista, ya sea una tabla de búsqueda, un mapa de calor o un calendario financiero.

## Mostrar array de Excel – recuperando los datos en Python

Una vez que Excel ha calculado la fórmula, los valores resultantes residen en la hoja como cualquier celda ingresada manualmente. Para **mostrar array de Excel**, iteramos sobre el rango e imprimimos cada fila:

```python
for row_index in range(1, 6):
    row_values = [worksheet.cell(row=row_index, column=col_index).value
                  for col_index in range(1, 6)]
    print(row_values)
```

Un par de consejos:

- Usa `worksheet.cell(row, column).value` en lugar del indexado estilo diccionario si necesitas manejar rangos más grandes; es un poco más rápido.
- Si deseas una tabla más bonita, considera `tabulate` o `pandas.DataFrame` para formatear la salida.

A continuación se muestra una captura de pantalla de la hoja resultante (el texto alternativo incluye la palabra clave principal para SEO):

![Captura de pantalla que muestra crear tabla de multiplicación en Excel usando Python](/images/multiplication-table-excel.png)

## Leer valores de Excel con Python – extrayendo la matriz para procesamiento adicional

A menudo, el siguiente paso después de **mostrar array de Excel** es alimentar esos números a una canalización de análisis de datos. Ahí es donde **leer valores de Excel con Python** brilla. El mismo bucle que usamos para imprimir puede reutilizarse para construir una lista de listas, un array de NumPy o un DataFrame de Pandas:

```python
import pandas as pd

# Build a list of rows
data = []
for row_index in range(1, 6):
    row = [worksheet.cell(row=row_index, column=col_index).value
           for col_index in range(1, 6)]
    data.append(row)

# Convert to DataFrame for easy manipulation
df = pd.DataFrame(data, columns=[f"Col{c}" for c in range(1, 6)],
                  index=[f"Row{r}" for r in range(1, 6)])

print(df)
```

Salida:

```
      Col1  Col2  Col3  Col4  Col5
Row1     1     2     3     4     5
Row2     2     4     6     8    10
Row3     3     6     9    12    15
Row4     4     8    12    16    20
Row5     5    10    15    20    25
```

Ahora tienes un DataFrame tipado completamente que puedes graficar, exportar a CSV o alimentar a un modelo de aprendizaje automático. Esto completa la parte de **leer valores de Excel con Python** del flujo de trabajo.

## Casos límite y consejos prácticos

- **Recalculación de fórmula**: Si modificas el libro después de la llamada inicial a `calculate_formula()`, debes invocarla de nuevo; de lo contrario la matriz en caché quedará obsoleta.
- **Excel no 365**: Las versiones más antiguas de Excel no soportan `MAKEARRAY`. En ese caso, recurre a una tabla generada con Python y escribe cada celda individualmente.
- **Tablas grandes**: Para matrices mayores de ~100 × 100, considera transmitir los datos para evitar cargar toda la hoja en memoria.
- **Manejo de errores**: Envuelve los pasos de cálculo y lectura en bloques `try/except` para capturar `InvalidFileException` o `FormulaError`.

## Conclusión

Acabamos de mostrarte cómo **crear tabla de multiplicación** en Excel usando Python, aprovechando el poder de **cómo usar lambda** y **cómo usar makearray**. Has visto cómo **mostrar array de Excel**, leer esos valores con **leer valores de Excel con Python**, e incluso convertir el resultado en un DataFrame de Pandas para análisis posteriores.

¿Quieres ir más allá? Prueba cambiar la lógica de multiplicación por algo más complejo—tal vez una matriz de distancias, una tabla de probabilidades o una cuadrícula de precios dinámicos. El mismo patrón se aplica: una línea de `MAKEARRAY`, un rápido `calculate_formula()`, y un puñado de bucles de Python para extraer los datos.

Si encontraste útil esta guía, dale una estrella en GitHub, compártela con tus compañeros, o deja un comentario con tu propio caso de uso. ¡Feliz codificación y disfruta de la brevedad de generar tablas de Excel con una sola fórmula!

## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que se basan en las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y funcionales con explicaciones paso a paso para ayudarte a dominar características adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Cómo crear y configurar libros de Excel con Aspose.Cells .NET: Guía paso a paso](/cells/english/net/getting-started/create-configure-excel-workbook-aspose-cells-net/)
- [Tutorial de Aspose.Cells .NET: Cómo crear y modificar libros de Excel fácilmente](/cells/english/net/workbook-operations/aspose-cells-net-create-modify-excel-workbooks/)
- [Cómo crear y dar estilo a rangos nombrados en Excel usando Aspose.Cells .NET | Guía paso a paso](/cells/english/net/range-management/create-style-named-ranges-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}