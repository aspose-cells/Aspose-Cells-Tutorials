---
category: general
date: 2026-10-07
description: Crea hojas de detalle duplicadas en Excel usando C#. Aprende cómo generar
  múltiples hojas de cálculo y crear un informe a partir de tablas en una sola ejecución.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create duplicated detail sheets
- how to generate multiple worksheets
- generate excel report from tables
language: es
lastmod: 2026-10-07
og_description: Crea hojas de detalle duplicadas en Excel con C#. Este tutorial muestra
  cómo generar múltiples hojas de cálculo y producir un informe completo de Excel
  a partir de tablas.
og_image_alt: Screenshot of an Excel file that has create duplicated detail sheets
  output
og_title: Crear hojas de detalle duplicadas en Excel – guía paso a paso en C#
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: Create duplicated detail sheets in Excel using C#. Learn how to generate
    multiple worksheets and build a report from tables in a single run.
  headline: Create duplicated detail sheets in Excel using C#
  type: TechArticle
- description: Create duplicated detail sheets in Excel using C#. Learn how to generate
    multiple worksheets and build a report from tables in a single run.
  name: Create duplicated detail sheets in Excel using C#
  steps:
  - name: '**Obtain the data source** that contains a master table and two detail
      tables.'
    text: '**Obtain the data source** that contains a master table and two detail
      tables.'
  - name: '**Configure the Smart‑marker processor** so each duplicated detail sheet
      receives a unique name.'
    text: '**Configure the Smart‑marker processor** so each duplicated detail sheet
      receives a unique name.'
  - name: '**Create a new workbook** and place a smart‑marker that references the
      master table.'
    text: '**Create a new workbook** and place a smart‑marker that references the
      master table.'
  - name: '**Run the processor** to generate the master sheet and all detail sheets.'
    text: '**Run the processor** to generate the master sheet and all detail sheets.'
  - name: '**Save the workbook** – each detail sheet now has a distinct name.'
    text: '**Save the workbook** – each detail sheet now has a distinct name.'
  type: HowTo
tags:
- C#
- Excel automation
- Aspose.Cells
title: Crear hojas de detalle duplicadas en Excel usando C#
url: /es/net/excel-copy-worksheet/create-duplicated-detail-sheets-in-excel-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crear hojas de detalle duplicadas en Excel usando C#

Si necesitas **crear hojas de detalle duplicadas** en un libro de Excel, esta guía te lleva a través del proceso completo. Verás cómo **generar múltiples hojas de cálculo** a partir de un conjunto de datos maestro‑detalle y producir un informe de Excel pulido directamente desde tablas.

Generar un informe de Excel a partir de tablas es un requisito común para sistemas de facturación, paneles de inventario, o cualquier escenario donde un registro maestro tiene varias filas de detalle relacionadas. Al final de este tutorial tendrás un programa C# ejecutable que crea un libro con una hoja maestra y una hoja con nombre único para cada grupo de detalle.

## Requisitos previos

* .NET 6.0 (o posterior) instalado  
* Visual Studio 2022 o cualquier IDE compatible con C#  
* El paquete NuGet **Aspose.Cells for .NET** (provee `SmartMarkerProcessor`)  

Puedes añadir el paquete con el siguiente comando:

```bash
dotnet add package Aspose.Cells
```

## Visión general de la solución

La solución sigue estos cinco pasos:

1. **Obtener la fuente de datos** que contiene una tabla maestra y dos tablas de detalle.  
2. **Configurar el procesador Smart‑marker** para que cada hoja de detalle duplicada reciba un nombre único.  
3. **Crear un nuevo libro de trabajo** y colocar un smart‑marker que haga referencia a la tabla maestra.  
4. **Ejecutar el procesador** para generar la hoja maestra y todas las hojas de detalle.  
5. **Guardar el libro de trabajo** – cada hoja de detalle ahora tiene un nombre distinto.

Cada paso se explica en detalle a continuación, con código completo y razonamiento.

## Paso 1: Obtener la fuente de datos que contiene una tabla maestra y dos tablas de detalle

La primera tarea es crear un `DataSet` que imite los datos que normalmente recuperarías de una base de datos. El `DataSet` debe contener una tabla llamada **Master** y una o más tablas llamadas **Detail**. El motor Smart‑marker usa estos nombres de tabla para rellenar el libro de trabajo.

```csharp
using System.Data;

/// <summary>
/// Returns a DataSet with a master table and two detail tables.
/// In a real application you would fill these tables from a database.
/// </summary>
static DataSet GetReportDataSet()
{
    var ds = new DataSet();

    // Master table – one row per invoice
    var master = new DataTable("Master");
    master.Columns.Add("InvoiceId", typeof(int));
    master.Columns.Add("CustomerName", typeof(string));
    master.Columns.Add("InvoiceDate", typeof(DateTime));
    master.Rows.Add(101, "Acme Corp", new DateTime(2024, 12, 01));
    master.Rows.Add(102, "Beta Ltd.", new DateTime(2024, 12, 03));
    ds.Tables.Add(master);

    // Detail table – multiple rows per invoice
    var detail = new DataTable("Detail");
    detail.Columns.Add("InvoiceId", typeof(int));
    detail.Columns.Add("Product", typeof(string));
    detail.Columns.Add("Quantity", typeof(int));
    detail.Columns.Add("Price", typeof(decimal));

    // Detail rows for Invoice 101
    detail.Rows.Add(101, "Widget A", 5, 9.99m);
    detail.Rows.Add(101, "Widget B", 2, 19.95m);

    // Detail rows for Invoice 102
    detail.Rows.Add(102, "Gadget X", 1, 99.00m);
    detail.Rows.Add(102, "Gadget Y", 3, 49.50m);
    ds.Tables.Add(detail);

    return ds;
}
```

**Por qué es importante:**  
*Smart‑marker* funciona con objetos `DataSet`; cada nombre de tabla se convierte en un marcador que el motor puede reemplazar. Al estructurar los datos de esta manera habilitas al procesador para duplicar automáticamente la hoja de detalle para cada `InvoiceId` distinto.

## Paso 2: Configurar el procesador Smart‑marker para dar a cada hoja de detalle duplicada un nombre único

Cuando el procesador encuentra un marcador de detalle, crea una nueva hoja de cálculo para cada grupo de filas. Por defecto, las nuevas hojas comparten el mismo nombre, lo que genera un conflicto de nombres. Configurar `DetailSheetNewName` indica al motor cómo renombrar cada copia.

```csharp
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

/// <summary>
/// Configures the SmartMarkerProcessor to rename duplicated detail sheets.
/// The placeholder {0} is replaced with a sequential number (1, 2, …).
/// </summary>
static SmartMarkerProcessor ConfigureProcessor()
{
    var processor = new SmartMarkerProcessor();

    // The pattern "Detail_{0}" becomes Detail_1, Detail_2, …
    processor.Options.DetailSheetNewName = "Detail_{0}";

    // Optional: keep the original sheet as a template (if you have one)
    processor.Options.KeepTemplateSheet = false;

    return processor;
}
```

**Por qué es importante:**  
Sin un patrón de nombres único el libro de trabajo lanzaría una excepción cuando el procesador intente agregar una segunda hoja de detalles. El marcador `{0}` asegura que cada hoja reciba un nombre distinto y predecible.

## Paso 3: Crear un nuevo libro de trabajo y colocar un smart‑marker que haga referencia a la tabla maestra

Ahora creas un `Workbook` nuevo, añades un marcador que apunta a la tabla **Master**, y opcionalmente formateas la fila de encabezado.

```csharp
/// <summary>
/// Creates a workbook with a single cell that contains the master smart‑marker.
/// </summary>
static Workbook CreateTemplateWorkbook()
{
    var workbook = new Workbook();
    var sheet = workbook.Worksheets[0];

    // Put the master smart‑marker in cell A1.
    // The double braces {{ }} tell SmartMarker to replace the content with the Master table.
    sheet.Cells["A1"].PutValue("{{Master}}");

    // Optional: add a header row for visual clarity.
    sheet.Cells["A2"].PutValue("Invoice ID");
    sheet.Cells["B2"].PutValue("Customer");
    sheet.Cells["C2"].PutValue("Date");
    sheet.Cells["A2:C2"].Style.Font.IsBold = true;

    return workbook;
}
```

**Por qué es importante:**  
El marcador `{{Master}}` indica al procesador que expanda la tabla maestra comenzando en `A1`. Las filas posteriores se convierten en las filas de datos para cada registro maestro. Este es el punto de entrada para **generate excel report from tables**.

## Paso 4: Ejecutar el procesador smart‑marker para generar la hoja maestra y las hojas de detalle

Con la fuente de datos, el procesador y la plantilla listos, invocas `Process`. El motor expande el marcador maestro y luego crea una hoja de detalle separada para cada `InvoiceId` distinto.

```csharp
static void GenerateReport()
{
    // 1️⃣ Obtain data
    DataSet reportData = GetReportDataSet();

    // 2️⃣ Configure processor
    SmartMarkerProcessor processor = ConfigureProcessor();

    // 3️⃣ Create template workbook
    Workbook workbook = CreateTemplateWorkbook();

    // 4️⃣ Process the smart‑markers – this creates the master sheet and duplicated detail sheets
    processor.Process(workbook, reportData);

    // 5️⃣ Save the file
    string outputPath = Path.Combine(
        Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
        "DuplicatedDetailSheets.xlsx");
    workbook.Save(outputPath);

    Console.WriteLine($"Report generated successfully: {outputPath}");
}
```

**Por qué es importante:**  
`processor.Process` realiza el trabajo pesado: lee las filas maestras, crea una hoja de detalle para cada clave única y renombra esas hojas según el patrón definido anteriormente. El resultado es un libro de trabajo que cumple con el requisito de **how to generate multiple worksheets**.

## Paso 5: Guardar el libro de trabajo resultante – cada hoja de detalle ahora tiene un nombre distinto

La llamada `Save` escribe el archivo en disco. Cuando abras el libro de trabajo, verás:

* **Sheet1** – la hoja maestra que contiene los encabezados de facturas.  
* **Detail_1**, **Detail_2**, … – cada hoja contiene las filas de la tabla **Detail** que pertenecen a una factura específica.

A continuación se muestra una maqueta del diseño esperado del libro de trabajo (la imagen es ilustrativa; puedes reemplazarla con una captura de pantalla real si lo deseas).

![Screenshot of an Excel file that has create duplicated detail sheets output](https://example.com/images/duplicated-detail-sheets.png)

### Resultado esperado

| Nombre de hoja | Descripción del contenido |
|----------------|---------------------------|
| **Sheet1** | Filas maestras: InvoiceId, CustomerName, InvoiceDate |
| **Detail_1** | Filas de detalle donde `InvoiceId = 101` |
| **Detail_2** | Filas de detalle donde `InvoiceId = 102` |

Al abrir `DuplicatedDetailSheets.xlsx` debería mostrarse exactamente esta estructura.

## Código fuente completo (listo para copiar)

```csharp
using System;
using System.Data;
using System.IO;
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

namespace ExcelDetailSheetsDemo
{
    class Program
    {
        static void Main()
        {
            GenerateReport();
        }

        // ------------------------------------------------------------
        // Step 1 – data source
        // ------------------------------------------------------------
        static DataSet GetReportDataSet()
        {
            var ds = new DataSet();

            var master = new DataTable("Master");
            master.Columns.Add("InvoiceId", typeof(int));
            master.Columns.Add("CustomerName", typeof(string));
            master.Columns.Add("InvoiceDate", typeof(DateTime));
            master.Rows.Add(101, "Acme Corp", new DateTime(2024, 12, 01));
            master.Rows.Add(102, "Beta Ltd.", new DateTime(2024, 12, 03));
            ds.Tables.Add(master);

            var detail = new DataTable("Detail");
            detail.Columns.Add("InvoiceId", typeof(int));
            detail.Columns.Add("Product", typeof(string));
            detail.Columns.Add("Quantity", typeof(int));
            detail.Columns.Add("Price", typeof(decimal));
            detail.Rows.Add(101, "Widget A", 5, 9.99m);
            detail.Rows.Add(101, "Widget B", 2, 19.95m);
            detail.Rows.Add(102, "Gadget X", 1, 99.00m);
            detail.Rows.Add(102, "Gadget Y", 3, 49.50m);
            ds.Tables.Add(detail);

            return ds;
        }

        // ------------------------------------------------------------
        // Step 2 – processor configuration
        // ------------------------------------------------------------
        static SmartMarkerProcessor ConfigureProcessor()
        {
            var processor = new SmartMarkerProcessor();
            processor.Options.DetailSheetNewName = "Detail_{0}";
            processor.Options.KeepTemplate


## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que se basan en las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y funcionales con explicaciones paso a paso para ayudarte a dominar características adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Cómo nombrar hojas automáticamente – Generar múltiples hojas en C#](/cells/english/net/smart-markers-dynamic-data/how-to-name-sheets-automatically-generate-multiple-sheets-in/)
- [Cómo crear hojas de cálculo – Guía paso a paso para generación dinámica de Excel](/cells/english/net/worksheet-operations/how-to-create-worksheets-step-by-step-guide-for-dynamic-exce/)
- [Cómo generar informe de Excel en C# – Guía completa usando SmartMarker](/cells/english/net/smart-markers-dynamic-data/how-to-generate-excel-report-in-c-full-guide-using-smartmark/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}