---
category: general
date: 2026-10-10
description: Aplica formato numérico en Excel rápidamente importando una DataTable,
  estableciendo formatos de fecha y moneda, y conservando la fila de encabezado en
  un solo paso.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- apply number format excel
- set date format excel
- format excel cells date
- set currency format excel
- preserve header row excel
language: es
lastmod: 2026-10-10
og_description: aplicar formato numérico en Excel con C# usando Aspose.Cells. Aprende
  a establecer el formato de fecha en Excel, el formato de moneda en Excel y a conservar
  la fila de encabezado en Excel al importar una DataTable.
og_image_alt: Excel worksheet showing currency and date columns formatted after import
og_title: Aplicar formato numérico de Excel en C# – guía paso a paso
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: apply number format excel quickly by importing a DataTable, setting
    date and currency formats, and preserving header row excel in a single step.
  headline: How to apply number format excel with Aspose.Cells
  type: TechArticle
tags:
- excel
- aspnet
- csharp
- excel-formatting
title: Cómo aplicar formato numérico en Excel con Aspose.Cells
url: /es/net/excel-custom-number-date-formatting/how-to-apply-number-format-excel-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo aplicar formato numérico en Excel con Aspose.Cells

Si necesitas **apply number format excel** mientras cargas datos desde un `DataTable`, esta guía te muestra exactamente cómo. También aprenderás a **set date format excel**, **set currency format excel** y **preserve header row excel** durante la importación, de modo que la hoja de cálculo resultante se vea profesional sin procesamiento adicional.

Cubriremos todo, desde la instalación de la biblioteca hasta escribir un fragmento completo y ejecutable. Al final podrás importar cualquier `DataTable` a un libro de Excel, formatear automáticamente las columnas numéricas y mantener la fila de encabezado intacta, todo en solo unas pocas líneas de C#.

## Requisitos previos

Antes de comenzar, asegúrate de tener:

* .NET 6.0 o posterior (el código también funciona con .NET Framework 4.6+)
* Visual Studio 2022 (o cualquier IDE de C# que prefieras)
* **Aspose.Cells for .NET** – instalar vía NuGet:

```bash
dotnet add package Aspose.Cells
```

* Una fuente `DataTable` – el ejemplo usa un método auxiliar `GetTable()` que devuelve datos de muestra.

> **Consejo profesional:** Aspose.Cells es una biblioteca comercial, pero ofrece un modo de evaluación gratuito que desactiva la marca de agua durante hasta 30 días.

## Paso 1: Crear un libro de trabajo y acceder a la primera hoja

El objeto workbook es el punto de entrada para todas las operaciones de Excel. Crear un nuevo workbook te proporciona una hoja de cálculo predeterminada en el índice 0.

```csharp
using Aspose.Cells;
using System;
using System.Data;

class Program
{
    static void Main()
    {
        // Create a new workbook
        Workbook wb = new Workbook();

        // Obtain reference to the first worksheet
        Worksheet sheet = wb.Worksheets[0];
```

*¿Por qué este paso?*  
`Workbook` gestiona el formato de archivo, el motor de cálculo y el repositorio de estilos. Acceder a `Worksheet` temprano nos permite pasar la hoja de destino al método de importación más adelante.

## Paso 2: Recuperar los datos de origen como un DataTable

En proyectos reales, los datos a menudo provienen de una consulta a base de datos, un analizador CSV o una respuesta de API. Para ilustrar, generamos un `DataTable` sencillo con tres columnas: **Product**, **Price**, y **ReleaseDate**.

```csharp
        // Step 2: Retrieve the source data as a DataTable
        DataTable sourceTable = GetTable();
```

```csharp
        // Helper method that builds a sample DataTable
        static DataTable GetTable()
        {
            DataTable dt = new DataTable();
            dt.Columns.Add("Product", typeof(string));
            dt.Columns.Add("Price", typeof(decimal));
            dt.Columns.Add("ReleaseDate", typeof(DateTime));

            dt.Rows.Add("Widget A", 12.99m, new DateTime(2023, 5, 1));
            dt.Rows.Add("Widget B", 23.50m, new DateTime(2023, 6, 15));
            dt.Rows.Add("Widget C", 7.75m, new DateTime(2023, 7, 30));
            return dt;
        }
```

*¿Por qué este paso?*  
Un `DataTable` proporciona una representación tabular en memoria que Aspose.Cells puede importar directamente, preservando el orden de columnas y los tipos de datos.

## Paso 3: Preparar una matriz `Style` – un estilo por columna

Aspose.Cells te permite aplicar un estilo distinto a cada columna durante la importación pasando una matriz de objetos `Style`. La longitud de la matriz debe coincidir con el número de columnas en la tabla de origen.

```csharp
        // Step 3: Prepare an array of Style objects – one for each column
        Style[] columnStyles = new Style[sourceTable.Columns.Count];
        for (int i = 0; i < columnStyles.Length; i++)
        {
            // Each entry must be instantiated before we can set properties
            columnStyles[i] = wb.CreateStyle();
        }
```

*¿Por qué este paso?*  
Si omites la creación explícita (`CreateStyle()`), intentar establecer `Number` lanzará una `NullReferenceException`. Inicializar cada `Style` garantiza que las asignaciones posteriores tengan éxito.

## Paso 4: Asignar formatos numéricos – moneda y fecha

Excel identifica los formatos numéricos incorporados por ID.

* **14** – Moneda (p.ej., `$1,234.00`)  
* **22** – Fecha corta (`mm/dd/yyyy`)

```csharp
        // Step 4: Assign number formats to the desired columns
        // Column 0 – Product name (no format needed)
        // Column 1 – Currency format (Number format ID 14)
        columnStyles[1].Number = 14;   // set currency format excel

        // Column 2 – Date format (Number format ID 22)
        columnStyles[2].Number = 22;   // set date format excel
```

> **Nota:** Si necesitas un formato personalizado (p.ej., `"¥#,##0.00"`), usa `Style.Custom = "¥#,##0.00"` en lugar de un ID incorporado.

*¿Por qué este paso?*  
Aplicar el **number format** correcto al momento de la importación elimina la necesidad de una segunda pasada que recorra las celdas para cambiar el formato. También garantiza que el **format excel cells date** y **set currency format excel** sean consistentes en todas las filas.

## Paso 5: Importar el DataTable preservando la fila de encabezado

El método `ImportDataTable` puede copiar datos, mantener la primera fila como encabezado y aplicar los estilos de columna que preparamos.

```csharp
        // Step 5: Import the DataTable into the worksheet
        // Parameters:
        //   sourceTable – the DataTable to import
        //   true        – preserve the header row (preserve header row excel)
        //   "A1"        – start cell
        //   columnStyles – array of styles for each column
        sheet.Cells.ImportDataTable(sourceTable, true, "A1", columnStyles);
```

```csharp
        // Save the workbook to disk
        wb.Save("FormattedReport.xlsx");
        Console.WriteLine("Workbook created successfully.");
    }
}
```

**Salida esperada** – Abre `FormattedReport.xlsx` y verás:

| Product | Price (currency) | ReleaseDate (date) |
|---------|------------------|--------------------|
| Widget A| $12.99           | 05/01/2023         |
| Widget B| $23.50           | 06/15/2023         |
| Widget C| $7.75            | 07/30/2023         |

La fila de encabezado permanece intacta, la columna **Price** muestra el símbolo de moneda y la columna **ReleaseDate** muestra un formato de fecha corta, todo sin código de estilo adicional.

### Manejo de casos límite comunes

| Situation                               | Solution |
|----------------------------------------|----------|
| **Más columnas que estilos**           | Asegúrate de que `columnStyles.Length` sea igual a `sourceTable.Columns.Count`. Las entradas faltantes usan el estilo predeterminado del workbook. |
| **Valores nulos en columnas numéricas**     | Excel trata `null` como una celda vacía; el formato numérico sigue aplicándose cuando se ingresa un valor más tarde. |
| **Moneda personalizada específica de la configuración regional**    | Usa `columnStyles[i].Custom = "\"€\"#,##0.00"` y establece `columnStyles[i].Number = -1` para desactivar el ID incorporado. |
| **Tablas grandes ( > 100 000 filas )**    | Considera usar la sobrecarga de `ImportDataTable` con `ImportTableOptions` para transmitir datos y reducir la presión de memoria. |
| **Aplicar el mismo estilo a múltiples columnas** | Reutiliza la misma instancia `Style` en la matriz (p.ej., `columnStyles[1] = columnStyles[2] = dateStyle;`). |

## Bonus: Usar una cadena de formato personalizada

Si los IDs incorporados no satisfacen tus necesidades, puedes definir un formato numérico personalizado:

```csharp
// Example: display Euro currency with no decimal places
Style euroStyle = wb.CreateStyle();
euroStyle.Custom = "\"€\"#,##0";
columnStyles[1] = euroStyle;   // replace the built‑in currency style
```

Este enfoque te brinda control total sobre **format excel cells date** y **set currency format excel** más allá de los IDs predefinidos.

## Conclusión

Ahora sabes cómo **apply number format excel** de manera eficiente al importar un `DataTable` con Aspose.Cells. Creando una matriz `Style` por columna, asignando IDs numéricos incorporados o personalizados, y usando la sobrecarga de `ImportDataTable` que **preserve header row excel**, puedes generar hojas de cálculo listas para publicar en una sola operación.

### ¿Qué sigue?

* Explora **set date format excel** con patrones personalizados como `"dddd, mmmm dd, yyyy"`.
* Combina esta técnica con **conditional formatting** para resaltar valores fuera de rango.
* Usa **format excel cells date** en tablas dinámicas o gráficos para informes dinámicos.

Siéntete libre de experimentar con diferentes IDs numéricos o cadenas personalizadas para que coincidan con la guía de estilo de tu organización. ¡Feliz codificación!

## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y funcionales con explicaciones paso a paso para ayudarte a dominar características adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [aplicar formato numérico excel – Guía paso a paso para formatear columnas](/cells/english/net/number-and-display-formats-in-excel/apply-number-format-excel-step-by-step-guide-to-formatting-c/)
- [Crear libro de Excel C# – Aplicar formato de moneda e importar DataTable](/cells/english/net/excel-data-import-export/create-excel-workbook-c-apply-currency-format-and-import-dat/)
- [Establecer formato de fecha en Excel con C# – Guía completa de formateo de importación](/cells/english/net/excel-custom-number-date-formatting/set-date-format-in-excel-with-c-full-import-formatting-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}