---
category: general
date: 2026-10-26
description: ExportTableOptions personalizado cuando ExportAsStrin le permite exportar
  datos de Excel como cadenas en C#. Siga la guía paso a paso para configurar y ejecutar
  la exportación.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- Custom ExportTableOptions when ExportAsStrin
- how to export excel as string
- ExportTableOptions C#
- Excel to DataTable string conversion
- Aspose.Cells export as string
language: es
lastmod: 2026-10-26
og_description: Opciones personalizadas de ExportTable cuando ExportAsStrin permite
  la exportación a Excel solo con cadenas. Aprende los pasos exactos para configurar
  y ejecutar la exportación en C#.
og_image_alt: Code snippet showing ExportTableOptions configuration for string export
og_title: Opciones personalizadas de ExportTable al usar ExportAsString – exportar
  Excel como cadena en C#
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Custom ExportTableOptions when ExportAsStrin lets you export Excel
    data as strings in C#. Follow the step‑by‑step guide to configure and run the
    export.
  headline: Custom ExportTableOptions when ExportAsStrin for Excel
  type: TechArticle
tags:
- C#
- Aspose.Cells
- Excel
- DataTable
title: Opciones personalizadas de ExportTable al ExportarComoCadena para Excel
url: /es/net/excel-data-export-retrieval/custom-exporttableoptions-when-exportasstrin-for-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Opciones de ExportTable personalizadas cuando ExportAsStrin – exportar Excel como cadena en C#

Si necesitas **Custom ExportTableOptions when ExportAsStrin** para obtener el valor de cada celda como una cadena simple, esta guía te muestra exactamente cómo hacerlo. Ya sea que estés construyendo una canalización de importación de datos o necesites una exportación lista para CSV, verás por qué configurar las opciones de esta manera evita sorpresas de conversión de tipos.

En este tutorial aprenderás **cómo exportar excel as string** usando la biblioteca Aspose.Cells, verás el código completo y ejecutable, y comprenderás el razonamiento detrás de cada configuración. No se requiere documentación externa – todo lo que necesitas está aquí.

## Prerrequisitos

Antes de comenzar, asegúrate de tener:

* .NET 6.0 SDK o posterior instalado  
* Visual Studio 2022 (o cualquier IDE que soporte .NET)  
* Paquete Aspose.Cells for .NET (instalar vía NuGet: `Install-Package Aspose.Cells`)  
* Un libro de Excel (`sample.xlsx`) colocado en la carpeta raíz del proyecto  

Estos son los únicos dependencias; el código se ejecuta en Windows, Linux o macOS sin bibliotecas adicionales.

## Paso 1: Cargar el libro de trabajo que deseas exportar

Lo primero que haces al usar **Custom ExportTableOptions when ExportAsStrin** es obtener un objeto `Worksheet` de un libro de trabajo cargado. Este objeto te da acceso a filas, columnas y a la API de exportación.

```csharp
using Aspose.Cells;
using System.Data;

// Load the workbook from disk
Workbook workbook = new Workbook("sample.xlsx");

// Get the first worksheet (index 0)
Worksheet worksheet = workbook.Worksheets[0];
```

*Por qué es importante:*  
`Workbook` lee el archivo una sola vez y mantiene toda la información de formato en memoria. Al seleccionar una `Worksheet` específica, limitas el alcance de la exportación y evitas procesar innecesariamente hojas ocultas.

## Paso 2: Configurar ExportTableOptions con ExportAsString = true

El núcleo de **Custom ExportTableOptions when ExportAsStrin** es el objeto `ExportTableOptions`. Establecer `ExportAsString` obliga al exportador a tratar cada celda como una cadena, sin importar su tipo de datos original (fecha, número, booleano, etc.). Activar `PreserveFormatting` conserva el estilo visual (p. ej., símbolos de moneda) en la cadena resultante.

```csharp
// Create and configure the export options
ExportTableOptions exportOptions = new ExportTableOptions
{
    ExportAsString = true,          // Export every cell value as a string
    PreserveFormatting = true      // Keep the original cell formatting
};
```

*Por qué es importante:*  
Cuando luego llamas a `ExportDataTable`, la biblioteca normalmente intenta inferir el tipo .NET de cada columna. Con `ExportAsString = true`, ese paso de inferencia se omite, evitando conversiones inesperadas a `DateTime` o `double` que pueden romper analizadores CSV posteriores.

## Paso 3: Exportar un rango a un DataTable usando las opciones personalizadas

Ahora puedes exportar un rango rectangular (filas 0‑9, columnas 0‑4) de la hoja. El método devuelve un `DataTable` donde cada campo es un `string`.

```csharp
// Export rows 0‑9 and columns 0‑4 (5 columns total) as a DataTable
DataTable dataTable = worksheet.ExportDataTable(
    startRow: 0,
    startColumn: 0,
    totalRows: 10,
    totalColumns: 5,
    options: exportOptions);
```

*Por qué es importante:*  
`ExportDataTable` es la forma más cómoda de mover datos de Excel a una estructura relacional que muchas API de .NET ya entienden (p. ej., Entity Framework, Dapper). Al pasar las **Custom ExportTableOptions when ExportAsStrin**, garantizas que cada `DataColumn.DataType` será `typeof(string)`.

## Paso 4: Verificar el resultado – todos los valores son cadenas

Es una buena práctica confirmar que la exportación se comportó como se esperaba. El siguiente bucle imprime cada celda y su tipo en tiempo de ejecución.

```csharp
Console.WriteLine("Exported DataTable (all values as strings):");
foreach (DataRow row in dataTable.Rows)
{
    for (int i = 0; i < dataTable.Columns.Count; i++)
    {
        object value = row[i];
        Console.Write($"{value} ({value.GetType().Name})\t");
    }
    Console.WriteLine();
}
```

**Salida esperada**

```
123 (String)    2023‑01‑15 (String)    $45.67 (String)    TRUE (String)    Sample text (String)
...
```

Cada celda muestra `String` como su tipo, confirmando que **Custom ExportTableOptions when ExportAsStrin** funcionó correctamente.

## Paso 5: Opcional – escribir el DataTable a CSV

Si tu objetivo final es un archivo de texto plano, puedes serializar fácilmente el `DataTable` a CSV:



## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y funcionales con explicaciones paso a paso para ayudarte a dominar características adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Export HTML Strings from Excel to DataTable using Aspose.Cells for .NET: A Step‑by‑Step Guide](/cells/english/net/import-export/export-html-strings-excel-datatable-aspose-cells-net/)
- [Export Custom Properties Excel Pdf Aspose Cells Net](/cells/hongkong/net/workbook-operations/export-custom-properties-excel-pdf-aspose-cells-net/)
- [Aspose Cells Java Custom Load Filters Excel Export](/cells/hongkong/java/import-export/aspose-cells-java-custom-load-filters-excel-export/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}