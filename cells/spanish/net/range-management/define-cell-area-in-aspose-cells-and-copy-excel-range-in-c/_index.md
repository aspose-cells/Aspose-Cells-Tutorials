---
category: general
date: 2026-08-04
description: Definir el área de celdas en Aspose.Cells y aprender cómo copiar tablas
  dinámicas, copiar rangos de Excel en C# y copiar rangos en la misma hoja de manera
  eficiente.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- define cell area
- how to copy pivot
- copy excel range c#
- copy range same sheet
- aspose.cells copy range
language: es
lastmod: 2026-08-04
og_description: Defina el área de celdas en Aspose.Cells y copie un rango de Excel
  en C# preservando las tablas dinámicas. Siga esta guía paso a paso para obtener
  resultados fiables.
og_image_alt: Screenshot showing how to define cell area and copy range in Aspose.Cells
og_title: Definir área de celda en Aspose.Cells – copiar rango de Excel en C#
schemas:
- author: Aspose
  dateModified: '2026-08-04'
  description: Define cell area in Aspose.Cells and learn how to copy pivot tables,
    copy Excel range C#, and copy range same sheet efficiently.
  headline: Define cell area in Aspose.Cells and copy Excel range in C#
  type: TechArticle
- description: Define cell area in Aspose.Cells and learn how to copy pivot tables,
    copy Excel range C#, and copy range same sheet efficiently.
  name: Define cell area in Aspose.Cells and copy Excel range in C#
  steps:
  - name: The range A61:J110 contains a copy of the original data.
    text: The range A61:J110 contains a copy of the original data.
  - name: A new pivot table appears at the top of the copied range.
    text: A new pivot table appears at the top of the copied range.
  - name: Refreshing the pivot reflects changes in the source data, confirming that
      **how to copy pivot** succeeded.
    text: Refreshing the pivot reflects changes in the source data, confirming that
      **how to copy pivot** succeeded.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
- Pivot tables
title: Definir área de celda en Aspose.Cells y copiar rango de Excel en C#
url: /es/net/range-management/define-cell-area-in-aspose-cells-and-copy-excel-range-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Definir área de celda en Aspose.Cells y copiar rango de Excel en C#

Si necesitas **define cell area** para un rango y luego copiar ese rango en la misma hoja de cálculo, esta guía te muestra exactamente cómo hacerlo con Aspose.Cells para .NET. Ya sea que estés moviendo un informe impulsado por una tabla dinámica o duplicando un bloque de datos, aprenderás el proceso completo en solo unos pasos.

También descubrirás **how to copy pivot** tables sin perder sus conexiones, y verás un ejemplo claro de **copy excel range c#** que funciona en el escenario de **copy range same sheet**. No se requieren herramientas externas, solo Aspose.Cells y unas pocas líneas de C#.

## Lo que necesitarás

- .NET 6.0 o posterior (el código también funciona con .NET Framework 4.7+)
- Aspose.Cells for .NET (paquete NuGet `Aspose.Cells`)
- Un libro de Excel (`input.xlsx`) que contiene una tabla dinámica en el rango A1:J50
- Un entorno de desarrollo como Visual Studio 2022

## Paso 1: Definir el área de celda para el rango de origen

La primera tarea es **define cell area** que representa el bloque que deseas copiar. Aspose.Cells utiliza la estructura `CellArea`, que almacena índices de fila y columna basados en cero.

```csharp
using Aspose.Cells;

// Load the source workbook
Workbook srcWorkbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

// Define the source range that contains the pivot table (A1:J50)
CellArea sourceRange = new CellArea
{
    StartRow = 0,      // Row 1 (zero‑based)
    StartColumn = 0,   // Column A
    EndRow = 49,       // Row 50
    EndColumn = 9      // Column J
};
```

**Por qué es importante:** `CellArea` le indica a Aspose.Cells exactamente qué celdas actuar. Usar índices basados en cero evita errores de desplazamiento que son comunes al traducir la notación A1 de Excel al código.

## Paso 2: Definir el área de celda de destino en la misma hoja de cálculo

Para **copy range same sheet**, también debes especificar dónde deben ubicarse los datos. El destino puede comenzar en cualquier fila; aquí comenzamos en la fila 61 (índice basado en cero 60) para dejar un espacio en blanco.

```csharp
// Define the destination area on the same sheet (starting at row 61)
CellArea destinationRange = new CellArea
{
    StartRow = 60,     // Row 61
    StartColumn = 0,   // Column A
    EndRow = 109,      // Row 110 (same height as source)
    EndColumn = 9      // Column J (same width as source)
};
```

**Por qué es importante:** Al reflejar las dimensiones de origen, garantizas que el bloque copiado encaje perfectamente sin truncamiento.

## Paso 3: Copiar el rango preservando las tablas dinámicas

Ahora puedes **how to copy pivot** de forma segura. La clase `CopyOptions` incluye una bandera `CopyPivotTables` que conserva la definición de la tabla dinámica, la fuente de datos y el formato.

```csharp
// Copy the range while preserving pivot tables
srcWorkbook.Worksheets[0].Cells.CopyRange(
    sourceRange,
    destinationRange,
    new CopyOptions
    {
        CopyPivotTables = true   // Ensure pivot tables are retained
    });
```

**Por qué es importante:** Sin establecer `CopyPivotTables = true`, la tabla dinámica se convertiría en una instantánea estática, perdiendo interactividad. Esta opción copia la caché subyacente y las conexiones, de modo que la nueva tabla dinámica se comporte exactamente como la original.

## Paso 4: Guardar el libro de trabajo

Finalmente, escribe los cambios de vuelta al disco. El archivo de salida demuestra que la tabla dinámica se ha duplicado en la misma hoja.

```csharp
// Save the modified workbook
srcWorkbook.Save("YOUR_DIRECTORY/CopyWithPivot.xlsx");
```

**Consejo profesional:** Usa `srcWorkbook.Save("CopyWithPivot.xlsx", SaveFormat.Xlsx)` si necesitas forzar un formato específico, especialmente al trabajar con versiones antiguas de Excel.

## Paso 5: Verificar la tabla dinámica copiada

Abre `CopyWithPivot.xlsx` en Excel y verifica lo siguiente:

1. El rango A61:J110 contiene una copia de los datos originales.
2. Una nueva tabla dinámica aparece en la parte superior del rango copiado.
3. Actualizar la tabla dinámica refleja cambios en los datos de origen, confirmando que **how to copy pivot** tuvo éxito.

Si la tabla dinámica no se actualiza, asegúrate de que el rango de datos de origen en la definición de la tabla dinámica aún apunte al área original del libro. Aspose.Cells actualiza automáticamente la referencia de origen cuando `CopyPivotTables` es true.

## Casos límite y variaciones

| Situación | Qué cambiar |
|-----------|-------------|
| **Copy to a different worksheet** | Reemplaza `srcWorkbook.Worksheets[0]` con el índice o nombre de la hoja de cálculo de destino, y ajusta `destinationRange` en consecuencia. |
| **Copy a merged cell block** | Establece `CopyOptions.PasteType = PasteType.All` para preservar celdas combinadas y formato. |
| **Copy only values, not formulas** | Usa `CopyOptions.PasteType = PasteType.Values` para evitar transferir fórmulas que referencien la hoja original. |
| **Large ranges ( > 10,000 rows )** | Considera usar `Workbook.Copy` para hojas completas y mejorar el rendimiento, luego elimina las filas no deseadas. |

Estas variaciones demuestran que la misma lógica **aspose.cells copy range** puede adaptarse a muchos escenarios del mundo real.

## Ejemplo completo funcional

A continuación se muestra el programa completo, listo para ejecutar. Reemplaza `YOUR_DIRECTORY` con una ruta de carpeta real en tu máquina.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Load the source workbook
        Workbook srcWorkbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // Step 1: Define the source cell area (A1:J50)
        CellArea sourceRange = new CellArea
        {
            StartRow = 0,
            StartColumn = 0,
            EndRow = 49,
            EndColumn = 9
        };

        // Step 2: Define the destination cell area on the same sheet (A61:J110)
        CellArea destinationRange = new CellArea
        {
            StartRow = 60,
            StartColumn = 0,
            EndRow = 109,
            EndColumn = 9
        };

        // Step 3: Copy the range while preserving pivot tables
        srcWorkbook.Worksheets[0].Cells.CopyRange(
            sourceRange,
            destinationRange,
            new CopyOptions { CopyPivotTables = true });

        // Step 4: Save the modified workbook
        srcWorkbook.Save("YOUR_DIRECTORY/CopyWithPivot.xlsx");
    }
}
```

**Salida esperada:** Después de ejecutar el programa, `CopyWithPivot.xlsx` contiene los datos originales más un bloque idéntico que comienza en la fila 61, completo con una tabla dinámica funcional.

## Conclusión

Ahora sabes cómo **define cell area** en Aspose.Cells, **copy excel range c#**, y **copy range same sheet** mientras preservas toda la funcionalidad de las tablas dinámicas. Esta técnica elimina errores manuales de copiar‑pegar y escala a libros de trabajo grandes.

A continuación, explora temas relacionados como **how to copy pivot** a través de múltiples hojas de cálculo, o usa **aspose.cells copy range** para duplicar hojas completas con formato. Experimenta con diferentes configuraciones de `CopyOptions` para adaptar el comportamiento de copia a las necesidades de tu proyecto.

¡Feliz codificación!

## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y funcionales con explicaciones paso a paso para ayudarte a dominar características adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Excel Aspose Cells .NET Copiar rango de datos](/cells/hindi/net/range-management/excel-aspose-cells-dotnet-copy-range-data/)
- [Excel Aspose Cells .NET Copiar rango de datos](/cells/spanish/net/range-management/excel-aspose-cells-dotnet-copy-range-data/)
- [Excel Aspose Cells .NET Copiar rango de datos](/cells/german/net/range-management/excel-aspose-cells-dotnet-copy-range-data/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}