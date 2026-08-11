---
category: general
date: 2026-08-11
description: Crear hoja de Excel a partir de un DataTable en C# y exportar el DataTable
  a Excel con nombrado automático de la hoja. Aprende cómo agregar filas al DataTable
  y guardar el libro de trabajo como xlsx.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel sheet
- export datatable to excel
- add rows to datatable
- create multiple excel sheets
- save workbook as xlsx
language: es
lastmod: 2026-08-11
og_description: Crear hoja de Excel a partir de un DataTable en C#. Este tutorial
  muestra cómo exportar un DataTable a Excel, agregar filas al DataTable, generar
  múltiples hojas de Excel y guardar el libro de trabajo como xlsx.
og_image_alt: Screenshot of an Excel workbook created from a DataTable with automatically
  renamed sheets
og_title: Crear hoja de Excel a partir de una DataTable en C# – guía completa de programación
schemas:
- author: Aspose
  dateModified: '2026-08-11'
  description: Create excel sheet from a DataTable in C# and export datatable to excel
    with automatic sheet naming. Learn how to add rows to datatable and save workbook
    as xlsx.
  headline: Create excel sheet from a DataTable in C# – step‑by‑step guide
  type: TechArticle
tags:
- C#
- Excel automation
- Aspose.Cells
title: Crear hoja de Excel a partir de una DataTable en C# – guía paso a paso
url: /es/net/excel-data-export-retrieval/create-excel-sheet-from-a-datatable-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crear hoja de Excel a partir de un DataTable en C# – guía paso a paso

Si necesitas **crear una hoja de Excel** a partir de un `DataTable` en C#, esta guía te muestra exactamente cómo hacerlo. Verás cómo **exportar datatable a excel**, añadir filas, manejar nombres de hoja duplicados y, finalmente, **guardar el libro como xlsx**.

El ejemplo utiliza Aspose.Cells, una biblioteca .NET ampliamente usada para la automatización de Excel. Los mismos conceptos se aplican a otras bibliotecas que soportan procesamiento al estilo SmartMarker, pero el código a continuación funciona directamente con Aspose.Cells 22.12 o posterior.

## Requisitos previos

Antes de comenzar, asegúrate de tener:

* .NET 6.0 SDK o una versión posterior instalada  
* Una referencia al paquete NuGet **Aspose.Cells** (`Install-Package Aspose.Cells`)  
* Familiaridad básica con `DataTable` y aplicaciones de consola en C#  

Estos requisitos mantienen el tutorial autocontenido y evitan herramientas externas.

## Paso 1: Crear un DataTable que se exportará a Excel

El primer paso es construir un `DataTable` que refleje los datos que deseas en la hoja de cálculo. Aquí creamos una tabla llamada **Sheet1**, añadimos una columna `Id` e insertamos dos filas.

```csharp
using System;
using System.Data;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a DataTable named "Sheet1"
        DataTable dataTable = new DataTable("Sheet1");
        dataTable.Columns.Add("Id", typeof(int));

        // 2️⃣ Add rows to the DataTable
        dataTable.Rows.Add(1);
        dataTable.Rows.Add(2);

        // Subsequent steps are called from here
        ProcessAndSaveWorkbook(dataTable);
    }
```

**Por qué es importante:**  
`DataTable` es una representación conveniente en memoria de datos tabulares. Nombrar la tabla `"Sheet1"` indica a Aspose.Cells qué hoja debe dirigirse al procesar SmartMarkers.

## Paso 2: Añadir filas al DataTable (expansión opcional)

Si tus datos de origen son dinámicos, a menudo necesitarás añadir filas en un bucle. El siguiente fragmento muestra un patrón típico:

```csharp
        // Example: add rows from a collection
        int[] ids = { 3, 4, 5 };
        foreach (int id in ids)
        {
            dataTable.Rows.Add(id);
        }
```

**Consejo:** Al añadir muchas filas, considera desactivar las restricciones (`dataTable.Constraints.Clear()`) para mejorar el rendimiento.

## Paso 3: Configurar opciones de SmartMarker para crear múltiples hojas de Excel automáticamente

Las opciones de SmartMarker te permiten controlar cómo se manejan los nombres de hoja duplicados. Establecer `DetailSheetNewName` a `"Sheet1_{0}"` indica a Aspose.Cells que renombre las hojas posteriores como `Sheet1_1`, `Sheet1_2`, etc.

```csharp
    private static void ProcessAndSaveWorkbook(DataTable dataTable)
    {
        // 3️⃣ Set SmartMarker options for automatic sheet renaming
        SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions
        {
            // New sheets will be named Sheet1_1, Sheet1_2, etc.
            DetailSheetNewName = "Sheet1_{0}"
        };
```

**Por qué es importante:**  
Cuando procesas varios objetos `DataTable` que comparten el mismo nombre, Excel normalmente lanzaría un error porque los nombres de hoja deben ser únicos. El patrón `DetailSheetNewName` elimina ese conflicto automáticamente.

## Paso 4: Procesar los SmartMarkers y exportar datatable a excel

Ahora creamos un `Workbook` nuevo, ejecutamos `ProcessSmartMarkers` y dejamos que Aspose.Cells rellene la(s) hoja(s) basada(s) en el `DataTable`.

```csharp
        // 4️⃣ Create a workbook and process SmartMarkers
        Workbook workbook = new Workbook();
        workbook.ProcessSmartMarkers(dataTable, smartMarkerOptions);
```

**Explicación:**  
`ProcessSmartMarkers` escanea el libro en busca de marcadores como `&=Sheet1!A1` (no mostrados aquí) y los reemplaza con los datos de `dataTable`. Como comenzamos con un libro vacío, Aspose.Cells crea una hoja nueva que coincide con el nombre de la tabla y la llena con las filas que añadimos.

## Paso 5: Guardar el libro como xlsx

Finalmente, escribe el libro en disco con el formato OpenXML moderno (`.xlsx`). Puedes cambiar la ruta para adaptarla a tu entorno.

```csharp
        // 5️⃣ Save the workbook as an .xlsx file
        string outputPath = @"YOUR_DIRECTORY\DuplicateSheets.xlsx";
        workbook.Save(outputPath, SaveFormat.Xlsx);

        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

**Resultado:**  
Ejecutar el programa produce un archivo Excel que contiene:

| Nombre de hoja | Filas |
|----------------|-------|
| Sheet1         | 1, 2, 3, 4, 5 |
| Sheet1_1       | (si se procesara otro DataTable con el mismo nombre) |

La lógica de renombrado de hojas garantiza **crear múltiples hojas de excel** sin gestión manual de nombres.

## Variaciones comunes y casos límite

| Situación | Cómo manejarla |
|-----------|----------------|
| **Tablas muy grandes** (≥ 100 000 filas) | Usa `WorkbookSettings.MemorySetting = MemorySetting.MemoryOptimized` antes del procesamiento para mantener bajo el uso de memoria. |
| **Orden de columnas personalizado** | Reordena los objetos `DataColumn` en el `DataTable` antes de llamar a `ProcessSmartMarkers`. |
| **Múltiples DataTables con nombres diferentes** | Llama a `ProcessSmartMarkers` para cada tabla; Aspose.Cells creará una hoja separada para cada nombre automáticamente. |
| **Necesidad de una fila de encabezado con estilo** | Después del procesamiento, accede a `Worksheet.Cells["A1"]` y aplica propiedades de `Style` (fuente, fondo). |
| **Guardar en un stream en lugar de un archivo** | Reemplaza `workbook.Save(outputPath, SaveFormat.Xlsx)` por `workbook.Save(stream, SaveFormat.Xlsx)`. |

**Consejo profesional:** Siempre envuelve las operaciones de sistema de archivos en bloques `try…catch` para detectar problemas de permisos temprano.

## Código fuente completo (listo para copiar)

```csharp
using System;
using System.Data;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Create the DataTable that will be exported
        DataTable dataTable = new DataTable("Sheet1");
        dataTable.Columns.Add("Id", typeof(int));

        // Add rows – you can replace this with your own data source
        dataTable.Rows.Add(1);
        dataTable.Rows.Add(2);
        int[] extraIds = { 3, 4, 5 };
        foreach (int id in extraIds)
        {
            dataTable.Rows.Add(id);
        }

        // Process SmartMarkers and save the workbook
        ProcessAndSaveWorkbook(dataTable);
    }

    private static void ProcessAndSaveWorkbook(DataTable dataTable)
    {
        // Configure SmartMarkerOptions to rename duplicate sheets automatically
        SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions
        {
            DetailSheetNewName = "Sheet1_{0}"
        };

        // Create a new workbook and populate it from the DataTable
        Workbook workbook = new Workbook();
        workbook.ProcessSmartMarkers(dataTable, smartMarkerOptions);

        // Save the workbook as an .xlsx file
        string outputPath = @"YOUR_DIRECTORY\DuplicateSheets.xlsx";
        workbook.Save(outputPath, SaveFormat.Xlsx);

        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

### Salida esperada

Ejecutar el programa muestra:

```
Workbook saved to YOUR_DIRECTORY\DuplicateSheets.xlsx
```

Abrir `DuplicateSheets.xlsx` muestra una hoja llamada **Sheet1** con la columna `Id` que contiene los valores `1, 2, 3, 4, 5`. Si más adelante procesas otro `DataTable` llamado `"Sheet1"` en el mismo libro, Aspose.Cells creará **Sheet1_1**, **Sheet1_2**, etc., automáticamente.

## Conclusión

Ahora sabes cómo **crear una hoja de Excel** a partir de un `DataTable` en C#, **exportar datatable a excel**, **añadir filas al datatable**, generar **creación de múltiples hojas de excel** con nombrado automático y **guardar el libro como xlsx**. El ejemplo completo y ejecutable demuestra el flujo de trabajo de extremo a extremo y brinda consejos prácticos para conjuntos de datos grandes y estilos personalizados.

### ¿Qué sigue?

* Explora **formato de celdas** (fuentes, colores, bordes) accediendo a `Worksheet.Cells` después de `ProcessSmartMarkers`.  
* Usa **bucles SmartMarker** para generar informes maestro‑detalle en un solo libro.  
* Cambia a **exportación CSV** modificando `SaveFormat.Csv` si necesitas una representación de texto plano.  

Siéntete libre de adaptar el código a tus propias fuentes de datos—ya sea una consulta a base de datos, una respuesta de API o una colección en memoria. ¡Feliz codificación!


## ¿Qué deberías aprender a continuación?


Los siguientes tutoriales cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y funcionales con explicaciones paso a paso para ayudarte a dominar características adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [How to Create and Save an Excel Workbook as ODS Using Aspose.Cells for .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)
- [How to Create and Save an Excel Workbook as SVG using Aspose.Cells for Java](/cells/english/java/workbook-operations/create-save-workbook-svg-aspose-cells-java/)
- [How to Create and Export Excel to HTML Using Aspose.Cells Java | Workbook Operations Guide](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}