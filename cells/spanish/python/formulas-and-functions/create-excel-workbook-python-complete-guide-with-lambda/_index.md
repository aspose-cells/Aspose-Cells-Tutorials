---
category: general
date: 2026-06-08
description: Crear un ejemplo de libro de Excel con Python que muestre cómo usar lambda
  en Excel, sumar filas con BYROW y automatizar cálculos en unos pocos pasos.
draft: false
keywords:
- create excel workbook python
- how to use lambda
- how to sum rows
- use lambda excel
language: es
og_description: Crea un libro de Excel con Python y aprende a usar lambda en Excel
  para sumar filas de manera eficiente con fórmulas BYROW.
og_title: Crear libro de Excel con Python – Guía completa
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: Create Excel workbook Python example that shows how to use lambda in
    Excel, sum rows with BYROW, and automate calculations in a few steps.
  headline: Create Excel Workbook Python – Complete Guide with Lambda
  type: TechArticle
tags:
- python
- excel
- automation
title: Crear libro de Excel en Python – Guía completa con Lambda
url: /es/python/formulas-and-functions/create-excel-workbook-python-complete-guide-with-lambda/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crear libro de Excel con Python – Guía completa con Lambda

¿Alguna vez te has preguntado cómo **crear Excel workbook Python** scripts que automaticen cálculos aburridos? No estás solo: muchos desarrolladores se encuentran con un obstáculo cuando necesitan generar una hoja, insertar una fórmula y recuperar los resultados en su código.  

En este tutorial también mostraremos **cómo usar lambda** en Excel, explicaremos **cómo sumar filas** con la moderna función `BYROW`, y te daremos un ejemplo ordenado de extremo a extremo que puedes copiar‑pegar y ejecutar hoy.

## Qué aprenderás

- Configurar un libro nuevo desde Python sin abrir Excel manualmente.  
- Rellenar un rango con una matriz de números de 3 × 3.  
- Insertar una fórmula `BYROW` que aprovecha la sintaxis **use lambda excel** para sumar cada fila.  
- Recalcular la hoja para que la fórmula se evalúe y luego leer los resultados de vuelta en Python.  

Al final de esta guía tendrás un script autónomo que podrás adaptar para facturas, tarjetas de puntuación o cualquier situación en la que necesites **sumar filas** al vuelo.

### Prerrequisitos

- Python 3.8+ instalado.  
- La biblioteca `openpyxl` (o `xlwings` si prefieres un enfoque basado en COM). Usaremos `openpyxl` porque es puro‑Python y funciona en todas las plataformas.  
- Una versión reciente de Microsoft Excel (365 o 2021) que admita la función `BYROW` y las fórmulas Lambda.  

Instala la biblioteca con:

```bash
pip install openpyxl
```

> **Consejo profesional:** Si tienes problemas de permisos en Windows, usa `python -m pip install --user openpyxl`.

---

## Crear Excel Workbook Python – Inicializar el libro

Lo primero que necesitamos es un objeto de libro completamente nuevo que viva únicamente en memoria. Con `openpyxl` esto es una sola línea:

```python
from openpyxl import Workbook

# Step 1: Create a new workbook and grab the first worksheet
wb = Workbook()
ws = wb.active   # .active is the first sheet by default
```

¿Por qué usamos `wb.active` en lugar de indexar `Worksheets[0]`? `openpyxl` expone la hoja activa directamente, lo que es más claro y evita una búsqueda adicional en la lista. Si alguna vez necesitas trabajar con varias hojas, siempre puedes añadirlas con `wb.create_sheet(title="MySheet")`.

---

## Rellenar la hoja con datos – Una sencilla matriz 3×3

A continuación, poblamos la hoja con una pequeña matriz. Esto refleja el clásico ejemplo de “sumar cada fila” y mantiene el código compacto.

```python
# Step 2: Define a 3×3 matrix of numbers
matrix = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
]

# Import the matrix into the worksheet starting at cell A1
for r_idx, row in enumerate(matrix, start=1):
    for c_idx, value in enumerate(row, start=1):
        ws.cell(row=r_idx, column=c_idx, value=value)
```

Quizás te preguntes por qué iteramos manualmente en lugar de usar `ws.append()` o `ws.values`. Los bucles explícitos nos dan control total sobre la celda inicial y facilitan ajustar desplazamientos más adelante, útil cuando deseas dejar una fila o columna de encabezado en blanco.

---

## Cómo usar Lambda en fórmulas de Excel

La característica **use lambda excel** de Excel te permite escribir funciones anónimas directamente en una celda. Piensa en ella como el `lambda` de Python, pero dentro del motor de la hoja de cálculo. La sintaxis es:

```
=LAMBDA(parameter1, parameter2, …, calculation)
```

Cuando se combina con `BYROW`, puedes aplicar ese lambda a cada fila de un rango, produciendo una columna de resultados. Este es el núcleo de nuestro truco **how to sum rows**.

```python
# Step 3: Insert a BYROW formula that sums each row using a Lambda
ws["D1"] = "=BYROW(A1:C3, LAMBDA(r, SUM(r)))"
```

¿Qué está ocurriendo bajo el capó?

- `A1:C3` es el rango de origen (nuestra matriz).  
- `LAMBDA(r, SUM(r))` define una función temporal que recibe una sola fila (`r`) y devuelve su suma.  
- `BYROW` ejecuta ese lambda para **cada fila** y derrama los resultados en la columna D, comenzando en `D1`.  

Como `BYROW` es una función de *matriz dinámica*, Excel rellena automáticamente `D1:D3` con las tres sumas.

> **Nota:** Las fórmulas `BYROW` y Lambda solo están disponibles en Excel 365/2021 y versiones posteriores. Si usas una versión anterior, deberás recurrir a fórmulas tradicionales `SUM` o a VBA.

---

## Cómo sumar filas con BYROW y Lambda

Ahora que la fórmula está en la hoja, debemos indicarle a Excel que la evalúe. `openpyxl` en sí no calcula fórmulas; solo las lee/escribe. Para desencadenar un cálculo podemos:

1. Guardar el libro y abrirlo en Excel (manual).  
2. Usar el motor COM de `xlwings` para forzar el recálculo (requiere Excel instalado).  

Para una solución puramente Python usaremos `xlwings` solo para el paso de cálculo, nada más.

```python
import xlwings as xw

# Step 4: Recalculate the workbook so the BYROW formula is evaluated
# Save the workbook to a temporary file first
temp_path = "temp_workbook.xlsx"
wb.save(temp_path)

# Open the file with xlwings, force a calculation, then close
app = xw.App(visible=False)
book = app.books.open(temp_path)
book.api.CalculateFull()          # Full recalculation
book.save()
book.close()
app.quit()
```

¿Por qué no llamamos a `wb.calculate()`? `openpyxl` carece de un motor nativo, así que nos apoyamos en Excel mismo a través de `xlwings`. La sobrecarga es mínima para hojas pequeñas y nos brinda el mismo resultado que Excel mostraría.

---

## Recalcular y obtener resultados – Traer las sumas de vuelta a Python

Finalmente, leemos los resultados derramados en la columna D. `openpyxl` lo hace de forma sencilla:

```python
# Step 5: Load the recalculated workbook and grab the results
wb = Workbook()  # re‑open the saved file
wb = xw.Book(temp_path).api  # alternative: use xlwings again to read values

# Using xlwings to fetch the range values as a Python list
results = xw.Range('D1:D3').value
print(results)   # Expected output: [6, 15, 24]
```

Si prefieres quedarte dentro de `openpyxl`, puedes leer las celdas después del recálculo en Excel:

```python
from openpyxl import load_workbook

wb = load_workbook(temp_path, data_only=True)  # data_only reads calculated values
ws = wb.active
results = [ws[f"D{row}"].value for row in range(1, 4)]
print(results)   # -> [6, 15, 24]
```

Ambos enfoques devuelven la misma lista `[6, 15, 24]`, confirmando que **how to sum rows** con `BYROW` + Lambda funciona como se anuncia.

---

## Casos límite y errores comunes

| Situación | Qué vigilar | Solución |
|-----------|-------------|----------|
| Versión de Excel anterior a 365 | `BYROW` y `LAMBDA` aparecen como `#NAME?` | Usa `=SUM(A1:C1)` clásico copiado manualmente, o actualiza Excel. |
| Matrices grandes (más de 10 k filas) | El recálculo puede volverse lento | Llama a `book.api.CalculateFullRebuild()` solo una vez, o divide el libro. |
| Ejecutar en un servidor sin interfaz gráfica y sin Excel | `xlwings` no puede lanzar Excel | Cambia a una biblioteca puramente Python como `pandas` + `numpy` para los cálculos, y luego escribe los resultados. |
| Problemas de configuración regional (coma vs. punto y coma) | La fórmula puede ser rechazada | Usa `ws["D1"].value = "=BYROW(A1:C3; LAMBDA(r; SUM(r)))"` para regiones que usan `;`. |

---

## Ejemplo completo (listo para copiar‑pegar)



## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos con explicaciones paso a paso para ayudarte a dominar funciones adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Crear libro de Excel con Aspose.Cells Java - Guía completa](/cells/english/java/automation-batch-processing/excel-automation-aspose-cells-java-guide/)
- [Crear libro de Excel y automatizar informes con Aspose.Cells](/cells/english/java/automation-batch-processing/aspose-cells-java-two-three-color-scales/)
- [Cómo crear y guardar un libro de Excel como ODS usando Aspose.Cells para .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}