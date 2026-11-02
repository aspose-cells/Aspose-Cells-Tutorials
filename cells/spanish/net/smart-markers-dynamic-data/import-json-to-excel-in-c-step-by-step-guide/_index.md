---
category: general
date: 2026-08-11
description: Importa JSON a Excel usando C# y Aspose.Cells. Carga JSON en un DataSet,
  procesa marcadores inteligentes y guarda como xlsx en minutos.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- import json to excel
- convert json to xlsx
- export json data excel
- load json into dataset
- save workbook c#
language: es
lastmod: 2026-08-11
og_description: Importa JSON a Excel usando C# y Aspose.Cells. Esta guía muestra cómo
  cargar JSON en un DataSet, procesar smart markers y guardar el libro de trabajo
  como un archivo xlsx, permitiendo una exportación de datos sin problemas.
og_image_alt: Screenshot of C# code importing JSON into an Excel workbook using Aspose.Cells
og_title: Importar JSON a Excel con C# – guía paso a paso completa
schemas:
- author: Aspose
  dateModified: '2026-08-11'
  description: Import json to excel using C# and Aspose.Cells. Load JSON into a DataSet,
    process smart markers, and save as xlsx in minutes.
  headline: Import json to excel in C# – step‑by‑step guide
  type: TechArticle
- questions:
  - answer: '`ReadJson` still creates an empty `DataTable`. The smart marker will
      produce only the header row, which is often the desired outcome for reporting
      templates.'
    question: What if the JSON array is empty?
  - answer: Yes. Load each array into its own `DataTable` within the same `DataSet`,
      then call `ProcessSmartMarkers` on each worksheet, referencing the appropriate
      table name in the marker (e.g., `&=Table(Orders)`).
    question: Can I import multiple JSON arrays into different sheets?
  - answer: After `ReadJson`, reorder columns by manipulating `dataSet.Tables[0].Columns`
      before processing the smart marker.
    question: How do I control column order?
  - answer: 'If you need the raw JSON string in a cell, skip the `DataSet` step and
      assign it directly: `worksheet.Cells["A1"].PutValue(jsonData);`'
    question: Is it possible to write JSON directly to a single cell as a string?
  type: FAQPage
tags:
- C#
- Aspose.Cells
- JSON
- Excel automation
title: Importar JSON a Excel en C# – guía paso a paso
url: /es/net/smart-markers-dynamic-data/import-json-to-excel-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Importar json a Excel en C# – guía paso a paso

Si necesitas importar json a Excel con C#, este tutorial te guía a través de todo el proceso. Aprenderás cómo cargar JSON en un DataSet, aplicar un smart marker y guardar el resultado como un archivo xlsx. El mismo enfoque también te permite convertir json a xlsx para pipelines de informes o scripts de migración de datos.

La guía cubre cada línea de código requerida, explica por qué cada paso es importante y destaca los errores comunes. Al final podrás exportar datos json a Excel sin escribir parsers personalizados, y entenderás cómo guardar un workbook c# de forma lista para producción. No se requieren herramientas externas más allá de Aspose.Cells.

## Requisitos previos

Antes de comenzar, asegúrate de tener:

- .NET 6.0 o posterior instalado  
- Visual Studio 2022 (o cualquier IDE que soporte .NET)  
- Paquete NuGet Aspose.Cells for .NET (`Install-Package Aspose.Cells`)  
- Un archivo de plantilla Excel que contenga un smart marker (p. ej., `Template.xlsx`)  

La plantilla debe tener una única celda con el smart marker `&=Table(Data)` donde `Data` coincide con el nombre del DataTable que pasarás.

## Importar json a Excel – configurar el proyecto

Crea una nueva aplicación de consola y agrega la referencia a Aspose.Cells:

```csharp
using System;
using System.Data;
using Aspose.Cells;

namespace JsonToExcelDemo
{
    class Program
    {
        static void Main()
        {
            // The complete workflow is demonstrated in the following steps.
        }
    }
}
```

Agregar las directivas `using` al inicio permite al compilador localizar `DataSet`, `Workbook` y los tipos relacionados. Esta base es necesaria para cada operación posterior.

## Convertir json a xlsx – cargar JSON en un DataSet

El primer paso funcional es transformar la cadena JSON en un `DataSet`. Aspose.Cells proporciona la práctica extensión `ReadJson` que analiza un arreglo de objetos directamente en una tabla.

```csharp
// Step 1: Define the JSON source
string jsonData = "[{\"Name\":\"John\",\"Age\":30},{\"Name\":\"Anna\",\"Age\":25}]";

// Step 2: Load the JSON into a DataSet
DataSet dataSet = new DataSet();
dataSet.ReadJson(jsonData);
```

**Por qué es importante:**  
`ReadJson` crea automáticamente un `DataTable` llamado `Table` (o con el nombre del elemento raíz) y rellena las columnas basándose en las claves del JSON. Esto elimina la necesidad de bucles manuales y garantiza que los tipos de datos se infieran correctamente. Si tu JSON contiene objetos anidados, Aspose.Cells los aplana en tablas separadas que puedes referenciar después.

**Consejo:** Si la carga JSON es grande, considera transmitirla con un `StringReader` para evitar cargar toda la cadena en memoria.

## Exportar datos json a Excel – abrir la plantilla Excel con un smart marker

A continuación, abre el libro que contiene el smart marker. El smart marker indica a Aspose.Cells dónde insertar los datos del `DataSet`.

```csharp
// Step 3: Open the Excel template that contains a smart marker
Workbook workbook = new Workbook("YOUR_DIRECTORY/Template.xlsx");
```

**Por qué es importante:**  
La plantilla separa el formato del código. Puedes diseñar el aspecto final en Excel (fuentes, bordes, formato condicional) y dejar que la biblioteca maneje la inserción de datos. La sintaxis del smart marker `&=Table(Data)` instruye al motor a escribir todo el `DataTable` en la celda donde reside el marcador.

## Exportar datos json a Excel – procesar el smart marker

Ahora procesa el smart marker, pasando el `DataTable` que se creó a partir del JSON.

```csharp
// Step 4: Process the smart marker, writing the entire array into a single cell
workbook.Worksheets[0].ProcessSmartMarkers(dataSet.Tables[0]);
```

**Por qué es importante:**  
`ProcessSmartMarkers` lee el marcador, expande la tabla verticalmente y conserva el formato original de la celda. El método también respeta los anchos de columna y aplica formatos numéricos automáticamente según los tipos .NET subyacentes.

**Caso límite:** Si la celda de destino ya contiene datos, el método los sobrescribe. Para preservar el contenido existente, coloca el marcador en un área dedicada de la plantilla.

## Guardar workbook c# – escribir el archivo final

Finalmente, guarda el workbook como un archivo `.xlsx`. Puedes elegir cualquier ubicación a la que tu aplicación tenga permiso de escritura.

```csharp
// Step 5: Save the resulting workbook
workbook.Save("YOUR_DIRECTORY/JsonSingleCell.xlsx", SaveFormat.Xlsx);
```

**Por qué es importante:**  
Especificar `SaveFormat.Xlsx` garantiza que la salida cumpla con el estándar Open XML, haciéndola legible por aplicaciones de hoja de cálculo modernas. Si necesitas un archivo legado `.xls`, reemplaza `SaveFormat.Xlsx` por `SaveFormat.Excel97To2003`.

**Consejo profesional:** Usa `SaveOptions` para controlar el nivel de compresión en archivos grandes, por ejemplo: `var opts = new XlsSaveOptions { CompressionLevel = CompressionLevel.Maximum }; workbook.Save("out.xls", opts);`

## Código fuente completo

Unir todos los pasos produce un programa ejecutable:

```csharp
using System;
using System.Data;
using Aspose.Cells;

namespace JsonToExcelDemo
{
    class Program
    {
        static void Main()
        {
            // Define the JSON source
            string jsonData = "[{\"Name\":\"John\",\"Age\":30},{\"Name\":\"Anna\",\"Age\":25}]";

            // Load the JSON into a DataSet
            DataSet dataSet = new DataSet();
            dataSet.ReadJson(jsonData);

            // Open the Excel template that contains a smart marker
            Workbook workbook = new Workbook("YOUR_DIRECTORY/Template.xlsx");

            // Process the smart marker, writing the entire array into a single cell
            workbook.Worksheets[0].ProcessSmartMarkers(dataSet.Tables[0]);

            // Save the resulting workbook
            workbook.Save("YOUR_DIRECTORY/JsonSingleCell.xlsx", SaveFormat.Xlsx);

            Console.WriteLine("JSON has been imported to Excel successfully.");
        }
    }
}
```

**Salida esperada:**  
Al ejecutar el programa se crea `JsonSingleCell.xlsx`. Al abrir el archivo se muestran las dos filas (`John`, `30` y `Anna`, `25`) pobladas debajo de la celda con el smart‑marker, conservando cualquier formato de encabezado que hayas definido en `Template.xlsx`.

![Ejemplo de código para importar json a Excel](image.png "Ejemplo de código para importar json a Excel")

## Preguntas frecuentes y cómo manejarlas

- **¿Qué ocurre si el arreglo JSON está vacío?**  
  `ReadJson` sigue creando un `DataTable` vacío. El smart marker producirá solo la fila de encabezado, lo cual suele ser el resultado deseado para plantillas de informes.

- **¿Puedo importar varios arreglos JSON en diferentes hojas?**  
  Sí. Carga cada arreglo en su propio `DataTable` dentro del mismo `DataSet`, luego llama a `ProcessSmartMarkers` en cada hoja, referenciando el nombre de tabla apropiado en el marcador (p. ej., `&=Table(Orders)`).

- **¿Cómo controlo el orden de las columnas?**  
  Después de `ReadJson`, reordena las columnas manipulando `dataSet.Tables[0].Columns` antes de procesar el smart marker.

- **¿Es posible escribir el JSON directamente en una sola celda como cadena?**  
  Si necesitas la cadena JSON cruda en una celda, omite el paso `DataSet` y asígnala directamente: `worksheet.Cells["A1"].PutValue(jsonData);`

## Conclusión

Ahora sabes cómo importar json a Excel en C# usando Aspose.Cells, desde cargar JSON en un DataSet hasta procesar un smart marker y guardar el workbook c#. Esta solución de extremo a extremo te permite convertir json a xlsx rápidamente, exportar datos json

## ¿Qué deberías aprender a continuación?


Los siguientes tutoriales cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos con explicaciones paso a paso para ayudarte a dominar funciones adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Importar JSON a Excel sin esfuerzo usando Aspose.Cells para .NET](/cells/english/net/import-export/import-json-excel-aspose-cells-net/)
- [Importar datos JSON a Excel usando Aspose.Cells Java&#58; Guía completa](/cells/english/java/import-export/import-json-data-excel-aspose-cells-java/)
- [Importar JSON a Excel de forma eficiente usando Aspose.Cells para Java&#58; Guía completa](/cells/english/java/import-export/import-json-to-excel-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}