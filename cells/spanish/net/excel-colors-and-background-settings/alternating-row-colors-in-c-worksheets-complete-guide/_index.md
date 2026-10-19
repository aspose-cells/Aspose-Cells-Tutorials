---
category: general
date: 2026-05-30
description: Aprende a añadir colores alternados a las filas en hojas de cálculo C#,
  establecer el fondo de la celda con un patrón de relleno sólido y personalizar el
  estilo de la celda de la hoja de cálculo sin esfuerzo.
draft: false
keywords:
- alternating row colors
- set cell background
- solid fill pattern
- add background color
- worksheet cell style
language: es
og_description: Colores de fila alternados en hojas de cálculo C# de forma sencilla.
  Aprende a establecer el fondo de la celda, usar un patrón de relleno sólido y dominar
  el estilo de celda de la hoja.
og_title: Colores alternados de filas en hojas de cálculo C# – Guía completa
schemas:
- author: Aspose
  dateModified: '2026-05-30'
  description: Learn how to add alternating row colors in C# worksheets, set cell
    background with a solid fill pattern, and customize worksheet cell style effortlessly.
  headline: Alternating Row Colors in C# Worksheets – Complete Guide
  type: TechArticle
- description: Learn how to add alternating row colors in C# worksheets, set cell
    background with a solid fill pattern, and customize worksheet cell style effortlessly.
  name: Alternating Row Colors in C# Worksheets – Complete Guide
  steps:
  - name: Why Use a **Solid Fill Pattern**?
    text: The `Pattern` property tells the engine how to render the color. A `Solid`
      fill guarantees that the entire cell background is painted, eliminating any
      faint gridlines that might otherwise show through. This is the most common way
      to **set cell background** when you want a clean look.
  - name: Change the Colors
    text: 'If your brand uses different hues, just replace `Color.LightYellow` and
      `Color.LightCyan` with any `System.Drawing.Color` you prefer. For example:'
  - name: Use a Different **Background Type**
    text: While `BackgroundType.Solid` is the most common, you can experiment with
      `BackgroundType.Gray125`, `BackgroundType.Horizontal`, or any pattern that the
      library supports. This changes the visual texture while still **adding background
      color**.
  - name: Apply a **Worksheet Cell Style** to Specific Columns
    text: 'Sometimes you only want the alternating effect on data columns, leaving
      the first column (e.g., IDs) untouched. Create a separate style for that column
      and assign it after the import:'
  type: HowTo
tags:
- C#
- Excel
- Aspose.Cells
- DataTable
- Styling
title: Colores alternados de filas en hojas de cálculo C# – Guía completa
url: /es/net/excel-colors-and-background-settings/alternating-row-colors-in-c-worksheets-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Colores de fila alternados en hojas de cálculo C# – Guía completa

¿Alguna vez te has preguntado cómo lograr que tu exportación de Excel se vea pulida usando **colores de fila alternados**? No estás solo—los desarrolladores preguntan constantemente cómo *agregar color de fondo* a las filas sin escribir un millón de líneas de código.  

En este tutorial recorreremos una forma sencilla de **establecer el fondo de la celda** en cada fila, aplicar un **patrón de relleno sólido**, y controlar el **estilo de celda de la hoja de cálculo** para que el resultado sea tanto legible como visualmente atractivo.

## Lo que aprenderás

- Obtener datos en un `DataTable` (o cualquier fuente tabular).  
- Construir una matriz de objetos `Style` que alternen entre dos colores.  
- Importar el `DataTable` a una hoja de cálculo mientras se aplican esos estilos.  
- Verificar la salida y ajustar los colores o patrones si es necesario.  

No se requieren herramientas externas más allá de un entorno .NET y una biblioteca de hojas de cálculo (usaremos **Aspose.Cells** en los ejemplos). Al final tendrás un método reutilizable que puedes incorporar en cualquier flujo de generación de informes.

---

## Paso 1: Obtener los datos de origen como un `DataTable`

Lo primero, sin datos no hay nada que estilizar. A continuación hay un pequeño asistente que crea un `DataTable` con filas de ejemplo. En un proyecto real lo reemplazarías con una llamada a base de datos o un analizador CSV.

```csharp
using System;
using System.Data;

static DataTable GetData()
{
    // Create a simple table with three columns
    DataTable table = new DataTable("Report");
    table.Columns.Add("ID", typeof(int));
    table.Columns.Add("Name", typeof(string));
    table.Columns.Add("Score", typeof(double));

    // Populate with dummy rows
    for (int i = 1; i <= 10; i++)
    {
        table.Rows.Add(i, $"Item {i}", Math.Round(new Random().NextDouble() * 100, 2));
    }

    return table;
}
```

> **Por qué es importante:** Tener los datos en un `DataTable` permite que el motor de la hoja de cálculo *importe* todo en una sola llamada, preservando automáticamente los nombres de columnas y los tipos de datos.

## Paso 2: Crear estilos de **colores de fila alternados**

Ahora generaremos una matriz de objetos `Style`—uno por fila—de modo que las filas pares obtengan un tono amarillo claro mientras que las filas impares reciban un cian suave. Este es el núcleo de la técnica de **colores de fila alternados**.

```csharp
using Aspose.Cells;
using System.Drawing;

// Assume workbook and worksheet are already instantiated
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.Worksheets[0];

// Retrieve data
DataTable dataTable = GetData();

// Prepare an array of styles – one for each row in the table
Style[] rowStyles = new Style[dataTable.Rows.Count];

for (int i = 0; i < rowStyles.Length; i++)
{
    // Create a fresh style for the current row
    rowStyles[i] = workbook.CreateStyle();

    // **Add background color**: LightYellow for even rows, LightCyan for odd rows
    rowStyles[i].ForegroundColor = (i % 2 == 0)
        ? Color.LightYellow
        : Color.LightCyan;

    // **Set cell background** using a **solid fill pattern**
    rowStyles[i].Pattern = BackgroundType.Solid;

    // Optional: you could also set font color, borders, etc., here
}
```

### ¿Por qué usar un **patrón de relleno sólido**?

La propiedad `Pattern` indica al motor cómo renderizar el color. Un relleno `Solid` garantiza que todo el fondo de la celda se pinte, eliminando cualquier línea de cuadrícula tenue que pudiera aparecer. Esta es la forma más común de **establecer el fondo de la celda** cuando deseas un aspecto limpio.

## Paso 3: Importar el `DataTable` con los estilos preparados

Con la matriz de estilos lista, la llamada de importación se convierte en una única línea. Aspose.Cells aplicará automáticamente el estilo correspondiente a cada fila.

```csharp
// Import the DataTable into the worksheet, applying the prepared styles
worksheet.Cells.ImportDataTable(
    dataTable,                     // source
    true,                          // include column names
    0,                             // start row (0‑based)
    0,                             // start column (0‑based)
    rowStyles);                    // array of styles
```

> **¿Qué ocurre internamente?**  
> La biblioteca itera sobre cada fila, copia los valores en las celdas y luego aplica el `Style` correspondiente de `rowStyles`. Como ya definimos un **patrón de relleno sólido**, cada celda de una fila hereda el mismo color de fondo, brindándote perfectos **colores de fila alternados**.

## Paso 4: Guardar el libro y verificar el resultado

Una guardada rápida te permite abrir el archivo en Excel (o cualquier visor compatible) y ver el efecto.

```csharp
// Save to disk – you can change the format to .xlsx, .xls, .csv, etc.
workbook.Save("AlternatingRowsReport.xlsx", SaveFormat.Xlsx);
Console.WriteLine("Workbook saved. Open 'AlternatingRowsReport.xlsx' to see the result.");
```

Al abrir el archivo, las filas 1, 3, 5… serán de color amarillo claro, mientras que las filas 2, 4, 6… serán de color cian claro. Los encabezados de columna permanecen blancos, haciendo que los datos destaquen.

![Hoja de cálculo que muestra colores de fila alternados](/images/alternating-row-colors.png "Captura de pantalla de la hoja de cálculo con colores de fila alternados")

*Texto alternativo de la imagen:* **colores de fila alternados** captura de pantalla de una hoja de cálculo donde el fondo de cada fila alterna entre amarillo claro y cian claro.

## Paso 5: Personalizar más (Opcional)

### Cambiar los colores

Si tu marca utiliza tonos diferentes, simplemente reemplaza `Color.LightYellow` y `Color.LightCyan` con cualquier `System.Drawing.Color` que prefieras. Por ejemplo:

```csharp
rowStyles[i].ForegroundColor = (i % 2 == 0) ? Color.FromArgb(255, 235, 205) // Peach
                                            : Color.FromArgb(205, 235, 255); // Soft blue
```

### Usar un **tipo de fondo** diferente

Aunque `BackgroundType.Solid` es el más común, puedes experimentar con `BackgroundType.Gray125`, `BackgroundType.Horizontal`, o cualquier patrón que la biblioteca admita. Esto cambia la textura visual mientras sigue **agregando color de fondo**.

### Aplicar un **estilo de celda de hoja de cálculo** a columnas específicas

A veces solo deseas el efecto alternado en columnas de datos, dejando la primera columna (p. ej., IDs) sin tocar. Crea un estilo separado para esa columna y asígnalo después de la importación:

```csharp
Style idStyle = workbook.CreateStyle();
idStyle.ForegroundColor = Color.White;
idStyle.Pattern = BackgroundType.Solid;

// Apply to the first column (A)
for (int row = 0; row < dataTable.Rows.Count + 1; row++) // +1 for header
{
    worksheet.Cells[row, 0].SetStyle(idStyle);
}
```

---

## Conclusión

Tienes ahora una solución completa y reutilizable para **colores de fila alternados** en hojas de cálculo C#. Al construir una matriz de objetos `Style`, **establecer el fondo de la celda** con un **patrón de relleno sólido**, e importar un `DataTable` en una sola llamada, puedes producir informes de aspecto profesional con código mínimo.  

A partir de aquí podrías:

- **Agregar color de fondo** a las filas de encabezado para mayor énfasis.  
- Combinar la técnica con formato condicional para indicaciones visuales dinámicas.  
- Explorar otras propiedades del **estilo de celda de hoja de cálculo** como fuentes, bordes o formatos numéricos.

¡Pruébalo en tu próxima rutina de exportación—tus usuarios te agradecerán por hojas de cálculo más limpias y legibles. ¡Feliz codificación!

## ¿Qué deberías aprender a continuación?

- [Establecer altura de fila en la hoja de cálculo con Aspose.Cells para .NET](/cells/english/net/size-and-spacing-customization/setting-height-of-all-rows-in-worksheet/)
- [Convertir nombres de celdas de Excel a índices de fila y columna usando Aspose.Cells para .NET](/cells/english/net/cell-operations/convert-excel-cell-names-to-indices-aspose-cells-dotnet/)
- [Establecer colores de pestaña de hoja de cálculo en Excel usando Aspose.Cells .NET - Guía completa](/cells/english/net/worksheet-management/set-worksheet-tab-colors-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}