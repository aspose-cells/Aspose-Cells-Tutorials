---
category: general
date: 2026-10-26
description: Aprende cómo importar DataTable a una hoja de Excel con C# y Aspose.Cells,
  conservando estilos y encabezados en solo unas pocas líneas de código.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to import datatable
- ImportTableOptions
- ImportDataTableStyle
- Aspose.Cells
- Excel worksheet import
- C# DataTable import
language: es
lastmod: 2026-10-26
og_description: Cómo importar un DataTable en una hoja de Excel usando C# y Aspose.Cells.
  Sigue esta guía completa para conservar estilos, encabezados y formato.
og_image_alt: Screenshot of C# code that imports a DataTable into an Excel worksheet
  with Aspose.Cells
og_title: Cómo importar DataTable a una hoja de Excel – Guía paso a paso en C#
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Learn how to import DataTable into an Excel worksheet with C# and Aspose.Cells,
    preserving styles and headers in just a few lines of code.
  headline: How to import DataTable into an Excel worksheet using C#
  type: TechArticle
tags:
- C#
- Aspose.Cells
- Excel
- DataTable
title: Cómo importar DataTable en una hoja de Excel usando C#
url: /es/net/excel-data-import-export/how-to-import-datatable-into-an-excel-worksheet-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo importar DataTable a una hoja de Excel usando C#

Si necesitas **cómo importar datatable** a una hoja de Excel, esta guía muestra los pasos exactos en C#. Ya sea que estés construyendo un motor de informes o exportando datos de una cuadrícula, verás cómo mantener los encabezados de columna y los estilos de celda intactos con Aspose.Cells. La solución funciona con .NET 6+ y requiere solo unas pocas líneas de código.

Importar un DataTable es una tarea común al trabajar con hojas de cálculo, pero los desarrolladores a menudo olvidan habilitar la transferencia de estilo o pasar correctamente la bandera de encabezado. En este tutorial aprenderás a configurar **ImportTableOptions**, activar **ImportDataTableStyle**, y llamar a `ImportDataTable` de forma segura. Al final tendrás un método listo‑para‑ejecutar que podrás incorporar a cualquier proyecto C#.

## Requisitos previos

Antes de comenzar, asegúrate de tener:

* .NET 6 SDK o una versión posterior instalada.
* Una copia con licencia de **Aspose.Cells for .NET** (la prueba gratuita sirve para pruebas).
* Familiaridad básica con `DataTable` y conceptos de Excel.
* Un IDE como Visual Studio 2022 (cualquier editor que soporte C# funciona).

No se requieren paquetes NuGet adicionales más allá de `Aspose.Cells`.

## Paso 1: Obtener los datos de origen en un DataTable

Lo primero que haces cuando respondes **cómo importar datatable** es tener los datos listos. En la mayoría de los escenarios reales, el `DataTable` proviene de una consulta a base de datos, un parser CSV o una colección en memoria. Aquí tienes un ejemplo mínimo que crea una tabla con algunas filas:

```csharp
using System;
using System.Data;

public static DataTable GetSampleData()
{
    var table = new DataTable("Employees");
    table.Columns.Add("Id", typeof(int));
    table.Columns.Add("Name", typeof(string));
    table.Columns.Add("Department", typeof(string));

    table.Rows.Add(1, "Alice Johnson", "Finance");
    table.Rows.Add(2, "Bob Smith", "Engineering");
    table.Rows.Add(3, "Carol White", "Marketing");

    return table;
}
```

*Por qué es importante*: Al construir primero el `DataTable`, controlas el orden de las columnas, los tipos de datos y los nombres de los encabezados, todo lo cual se conserva cuando luego importas la tabla a una hoja de Excel.

## Paso 2: Crear `ImportTableOptions` y habilitar la importación de estilo

Cuando respondes **cómo importar datatable**, la siguiente decisión es si deseas el estilo visual (fuentes, colores, bordes) que ya pueda estar definido en el `DataTable` de origen. Aspose.Cells proporciona la clase `ImportTableOptions` para un control granular. Establecer `ImportDataTableStyle = true` copia la información de estilo a la hoja de destino.

```csharp
using Aspose.Cells;

public static ImportTableOptions CreateImportOptions()
{
    var options = new ImportTableOptions
    {
        // Preserve the style of the DataTable cells (font, background, borders)
        ImportDataTableStyle = true
    };
    return options;
}
```

*Por qué es importante*: Sin habilitar `ImportDataTableStyle`, las celdas importadas usarían el estilo predeterminado de la hoja, perdiendo cualquier formato personalizado que hayas aplicado al `DataTable`. Esta bandera es esencial para una exportación pulida.

## Paso 3: Importar el DataTable a la hoja, incluyendo los encabezados

Ahora tienes todo lo necesario para responder **cómo importar datatable** a un archivo Excel. Creas un libro, seleccionas una hoja y llamas a `ImportDataTable`. El segundo argumento del método (`true`) indica a Aspose.Cells que escriba los encabezados de columna como la primera fila.

```csharp
using Aspose.Cells;
using System.IO;

public static void ExportDataTableToExcel(string filePath)
{
    // 1️⃣ Retrieve the source data
    DataTable dataTable = GetSampleData();

    // 2️⃣ Prepare import options (style preservation)
    ImportTableOptions importOptions = CreateImportOptions();

    // 3️⃣ Create a new workbook and select the first worksheet
    var workbook = new Workbook();
    Worksheet ws = workbook.Worksheets[0];
    ws.Name = "Employees";

    // 4️⃣ Import the DataTable, include headers, and apply options
    ws.Cells.ImportDataTable(dataTable, true, importOptions);

    // 5️⃣ Save the workbook to the specified path
    workbook.Save(filePath, SaveFormat.Xlsx);
}
```

Ejecutar `ExportDataTableToExcel("Employees.xlsx")` genera un archivo `Employees.xlsx` donde la primera fila contiene **Id**, **Name** y **Department**, y cada celda conserva el estilo definido en el `DataTable` original.

### Ejemplo completo listo para ejecutar

A continuación se muestra un programa de consola completo y autocontenido que demuestra **cómo importar datatable** y guarda el resultado en el directorio actual. Copia‑pega este código en un nuevo proyecto de consola y ejecútalo.

```csharp
using System;
using System.Data;
using Aspose.Cells;

namespace DataTableImportDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            string outputPath = Path.Combine(Directory.GetCurrentDirectory(), "Employees.xlsx");
            ExportDataTableToExcel(outputPath);
            Console.WriteLine($"Excel file created at: {outputPath}");
        }

        // Retrieves sample data
        private static DataTable GetSampleData()
        {
            var table = new DataTable("Employees");
            table.Columns.Add("Id", typeof(int));
            table.Columns.Add("Name", typeof(string));
            table.Columns.Add("Department", typeof(string));

            table.Rows.Add(1, "Alice Johnson", "Finance");
            table.Rows.Add(2, "Bob Smith", "Engineering");
            table.Rows.Add(3, "Carol White", "Marketing");
            return table;
        }

        // Configures import options to keep styles
        private static ImportTableOptions CreateImportOptions()
        {
            return new ImportTableOptions
            {
                ImportDataTableStyle = true
            };
        }

        // Performs the import and saves the workbook
        private static void ExportDataTableToExcel(string filePath)
        {
            DataTable dataTable = GetSampleData();
            ImportTableOptions importOptions = CreateImportOptions();

            var workbook = new Workbook();
            Worksheet ws = workbook.Worksheets[0];
            ws.Name = "Employees";

            // Here we answer the core question: how to import datatable
            ws.Cells.ImportDataTable(dataTable, true, importOptions);
            workbook.Save(filePath, SaveFormat.Xlsx);
        }
    }
}
```

**Salida esperada**  
Al abrir `Employees.xlsx`, verás:

| Id | Name          | Department |
|----|---------------|------------|
| 1  | Alice Johnson | Finance    |
| 2  | Bob Smith     | Engineering|
| 3  | Carol White   | Marketing  |

Todas las celdas conservan el estilo predeterminado del DataTable (fuente, alineación). Si aplicaste estilos personalizados al `DataTable` antes de la importación, esos estilos aparecen idénticamente en la hoja porque `ImportDataTableStyle` está configurado en `true`.

## Problemas comunes y consejos de buenas prácticas

| Problema | Por qué ocurre | Cómo evitarlo |
|----------|----------------|---------------|
| **Faltan encabezados** | Pasar `false` como segundo argumento a `ImportDataTable` omite los nombres de columna. | Siempre usa `true` cuando necesites encabezados, o escríbelos manualmente antes de la importación. |
| **El estilo no se transfiere** | Olvidar habilitar `ImportDataTableStyle`. | Establece `ImportDataTableStyle = true` en `ImportTableOptions`. |
| **Tablas grandes provocan lentitud** | Importar millones de filas sin paginación. | Importa en lotes o usa la sobrecarga de `ImportDataTable` con `startRow` para transmitir los datos. |
| **Referencia a hoja incorrecta** | Usar `workbook.Worksheets[1]` cuando solo existe una hoja. | Usa `workbook.Worksheets[0]` o crea una nueva hoja con `workbook.Worksheets.Add()`. |
| **Caducidad de la licencia** | La versión de prueba de Aspose.Cells muestra una marca de agua después de 30 días. | Aplica una licencia válida con `License license = new License(); license.SetLicense("Aspose.Cells.lic");`. |

**Consejo profesional**: Si necesitas aplicar un tema personalizado después de la importación, llama a `ws.Cells.ApplyStyle(style)` donde `style` es un objeto `Style` que configuras una vez y reutilizas en todas las filas.

## Extender la solución

Ahora que sabes **cómo importar datatable**, puedes explorar escenarios relacionados:

* **Importar varias tablas** – repite la importación en diferentes hojas.
* **Formato condicional** – después de la importación, agrega reglas con `ws.Cells.ApplyConditionalFormatting`.
* **Exportar a CSV** – usa `workbook.Save("file.csv", SaveFormat.Csv)` si se requiere un formato de texto plano.
* **Leer de nuevo a un DataTable** – usa `ws.Cells.ExportDataTable` para verificar la integridad del proceso de ida y vuelta.

Todas estas extensiones se basan en el patrón central demostrado arriba: obtener los datos, configurar las opciones de importación y llamar a un único método de Aspose.Cells.

## Conclusión

Ahora dispones de una respuesta completa y lista para producción sobre **cómo importar datatable** a una hoja de Excel usando C#. El tutorial cubrió la obtención de datos de origen, la configuración de `ImportTableOptions` con `ImportDataTableStyle`, y la ejecución de la importación mediante `ImportDataTable`. Siguiendo el ejemplo de código conservarás automáticamente los encabezados y los estilos, y podrás adaptar el patrón a conjuntos de datos más grandes, múltiples hojas o necesidades de formato adicionales.

¿Listo para automatizar tu flujo de informes? Prueba reemplazando el `DataTable` de ejemplo por una consulta real a base de datos, experimenta con estilos de celda personalizados e integra el método en tu capa de servicios existente. ¡Feliz codificación!

## ¿Qué deberías aprender a continuación?

Los tutoriales siguientes cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y funcionales con explicaciones paso a paso para ayudarte a dominar características adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [How to Import Arrays into Excel Using Aspose.Cells for .NET&#58; A Step-by-Step Guide](/cells/english/net/import-export/import-arrays-excel-aspose-cells-net/)
- [How to Import XML Data into Excel with Aspose.Cells for .NET&#58; A Step-by-Step Guide](/cells/english/net/import-export/import-xml-data-net-aspose-cells-guide/)
- [How to Import HTML-Formatted DataTables into Excel Using Aspose.Cells for .NET](/cells/english/net/import-export/aspose-cells-net-data-table-import-html-formatting/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}