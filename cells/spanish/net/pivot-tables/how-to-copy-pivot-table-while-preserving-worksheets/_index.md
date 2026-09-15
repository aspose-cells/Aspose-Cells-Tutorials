---
category: general
date: 2026-09-15
description: Aprende cómo copiar una tabla dinámica, copiar una hoja de cálculo con
  tabla dinámica y guardar el libro como pptx usando Aspose.Cells en C#. Guía completa
  paso a paso.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy pivot table
- copy worksheet with pivot
- save workbook as pptx
language: es
lastmod: 2026-09-15
og_description: Cómo copiar una tabla dinámica, copiar una hoja de cálculo con tabla
  dinámica y guardar el libro como pptx usando Aspose.Cells. Sigue los ejemplos completos
  y ejecutables en C#.
og_image_alt: Screenshot showing how to copy pivot table in a C# code editor
og_title: Cómo copiar una tabla dinámica y exportar hojas de cálculo – guía completa
  de C#
schemas:
- author: Aspose
  dateModified: '2026-09-15'
  description: Learn how to copy pivot table, copy worksheet with pivot, and save
    workbook as pptx using Aspose.Cells in C#. Complete step‑by‑step guide.
  headline: How to copy pivot table while preserving worksheets
  type: TechArticle
- description: Learn how to copy pivot table, copy worksheet with pivot, and save
    workbook as pptx using Aspose.Cells in C#. Complete step‑by‑step guide.
  name: How to copy pivot table while preserving worksheets
  steps:
  - name: – Load the source workbook that holds the pivot table
    text: '```csharp // Load the workbook that contains the pivot table you want to
      copy Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/Source.xlsx"); ```'
  - name: – Create an empty destination workbook
    text: '```csharp // Create a new, empty workbook that will receive the copied
      data Workbook destinationWorkbook = new Workbook(); ```'
  - name: – Copy the rows that include the pivot table
    text: '```csharp // Copy rows 0‑19 (A1:G20) from the first worksheet of the source
      sourceWorkbook.Worksheets[0].Cells.CopyRows(0, 0, 20); ```'
  - name: – Copy the columns that contain the pivot table
    text: '```csharp // Copy columns 0‑6 (A‑G) from the same worksheet sourceWorkbook.Worksheets[0].Cells.CopyColumns(0,
      0, 7); ```'
  - name: – Transfer the prepared sheet into the destination workbook
    text: '```csharp // Move the fully prepared worksheet into the destination workbook
      sourceWorkbook.Worksheets[0].Copy(destinationWorkbook.Worksheets[0]); ```'
  - name: – Save the result – the pivot table remains intact
    text: '```csharp // Save the destination workbook; the pivot table works exactly
      like the original destinationWorkbook.Save("YOUR_DIRECTORY/CopyWithPivot.xlsx");
      ```'
  - name: – Load the workbook that includes the textbox
    text: '```csharp // Load the Excel file that contains an editable textbox shape
      Workbook workbookWithTextbox = new Workbook("YOUR_DIRECTORY/DocWithTextbox.xlsx");
      ```'
  - name: – Configure PPTX save options
    text: '```csharp // Create PPTX save options and enable the editable textbox feature
      (available from v25.11) PptxSaveOptions pptxOptions = new PptxSaveOptions {
      ExportEditableTextBox = true }; ```'
  - name: – Save the workbook as PPTX
    text: '```csharp // Export the workbook to a PPTX file; the textbox stays editable
      in PowerPoint workbookWithTextbox.Save("YOUR_DIRECTORY/Result.pptx", pptxOptions);
      ```'
  - name: – Prepare the SmartMarkerProcessor
    text: '```csharp // Initialise the processor that will fill Smart Markers SmartMarkerProcessor
      smartMarkerProcessor = new SmartMarkerProcessor(); ```'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: Cómo copiar una tabla dinámica manteniendo las hojas de cálculo
url: /es/net/pivot-tables/how-to-copy-pivot-table-while-preserving-worksheets/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo copiar una tabla dinámica sin perder las hojas de cálculo

Si necesitas **how to copy pivot table** de un libro a otro sin perder la caché subyacente de la tabla dinámica, esta guía ofrece una solución lista para ejecutar. También verás cómo **copy worksheet with pivot** y cómo **save workbook as pptx** manteniendo los cuadros de texto editables intactos. Todos los ejemplos usan la última versión de Aspose.Cells para .NET, por lo que puedes insertar el código en cualquier proyecto C# y obtener resultados inmediatos.

Trabajar con archivos Excel de forma programática a menudo implica mover datos entre libros, exportar a presentaciones o insertar Smart Markers complejos. Los tres fragmentos de código a continuación cubren esos escenarios comunes y explican por qué cada paso es importante.

## Requisitos previos

Antes de comenzar, asegúrate de tener:

* .NET 6.0 o posterior instalado  
* Aspose.Cells para .NET (versión 25.11 o más reciente) referenciado en tu proyecto  
* Una carpeta llamada `YOUR_DIRECTORY` donde se leerán y escribirán los archivos de ejemplo  

No se requieren paquetes NuGet adicionales.

---

## Cómo copiar una tabla dinámica con Aspose.Cells

Copiar un rango que contiene una tabla dinámica mientras se preserva la caché de la tabla es una necesidad frecuente. Los pasos siguientes demuestran la secuencia exacta que necesitas.

### Paso 1 – Cargar el libro de origen que contiene la tabla dinámica

```csharp
// Load the workbook that contains the pivot table you want to copy
Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/Source.xlsx");
```

*Por qué*: Aspose.Cells lee el libro en memoria, dándote acceso a hojas, celdas y tablas dinámicas.

### Paso 2 – Crear un libro de destino vacío

```csharp
// Create a new, empty workbook that will receive the copied data
Workbook destinationWorkbook = new Workbook();
```

*Por qué*: Comenzar con un libro en blanco garantiza que no haya estilos ocultos o rangos nombrados que interfieran con la operación de copia.

### Paso 3 – Copiar las filas que incluyen la tabla dinámica

```csharp
// Copy rows 0‑19 (A1:G20) from the first worksheet of the source
sourceWorkbook.Worksheets[0].Cells.CopyRows(0, 0, 20);
```

*Por qué*: `CopyRows` copia los valores de celda sin procesar, formatos y referencias a la caché de la tabla dinámica. El rango debe incluir toda el área de la tabla dinámica.

### Paso 4 – Copiar las columnas que contienen la tabla dinámica

```csharp
// Copy columns 0‑6 (A‑G) from the same worksheet
sourceWorkbook.Worksheets[0].Cells.CopyColumns(0, 0, 7);
```

*Por qué*: Las tablas dinámicas abarcan filas y columnas; copiar columnas asegura que se mantenga el diseño completo de la tabla.

### Paso 5 – Transferir la hoja preparada al libro de destino

```csharp
// Move the fully prepared worksheet into the destination workbook
sourceWorkbook.Worksheets[0].Copy(destinationWorkbook.Worksheets[0]);
```

*Por qué*: El método `Copy` clona la hoja de cálculo, incluida la caché de la tabla dinámica, de modo que el libro de destino muestra una tabla idéntica.

### Paso 6 – Guardar el resultado – la tabla dinámica permanece intacta

```csharp
// Save the destination workbook; the pivot table works exactly like the original
destinationWorkbook.Save("YOUR_DIRECTORY/CopyWithPivot.xlsx");
```

*Por qué*: Persistir el libro escribe todas las estructuras internas, garantizando que la tabla pueda refrescarse más adelante.

**Consejo**: Después de copiar, puedes llamar a `destinationWorkbook.Worksheets[0].PivotTables[0].Refresh()` para actualizar los datos si la fuente cambió.

---

## Copiar hoja con tabla dinámica – una alternativa concisa

Si solo necesitas duplicar una hoja completa que ya contiene una tabla dinámica, puedes omitir los pasos de copia de filas/columnas y usar directamente el método `Copy` a nivel de hoja.

```csharp
// Load source workbook
Workbook src = new Workbook("YOUR_DIRECTORY/SourceWithPivot.xlsx");

// Create destination workbook
Workbook dst = new Workbook();

// Copy the first worksheet (including its pivot table) to the destination
src.Worksheets[0].Copy(dst.Worksheets[0]);

// Save the new file
dst.Save("YOUR_DIRECTORY/WorksheetCopy.xlsx");
```

Este enfoque es útil cuando la hoja no contiene datos adicionales fuera del área de la tabla dinámica. La operación **copy worksheet with pivot** preserva automáticamente todo el formato, rangos nombrados y cachés de tabla dinámica.

---

## Guardar libro como PPTX con cuadros de texto editables

Exportar una hoja de Excel que contiene un cuadro de texto editable a PowerPoint puede ser necesario para paneles de informes. El código a continuación muestra **save workbook as pptx** manteniendo el cuadro de texto editable.

### Paso 1 – Cargar el libro que incluye el cuadro de texto

```csharp
// Load the Excel file that contains an editable textbox shape
Workbook workbookWithTextbox = new Workbook("YOUR_DIRECTORY/DocWithTextbox.xlsx");
```

### Paso 2 – Configurar las opciones de guardado PPTX

```csharp
// Create PPTX save options and enable the editable textbox feature (available from v25.11)
PptxSaveOptions pptxOptions = new PptxSaveOptions
{
    ExportEditableTextBox = true
};
```

*Por qué*: Establecer `ExportEditableTextBox` indica a Aspose.Cells que traduzca el cuadro de texto de Excel en una forma de PowerPoint que siga siendo editable después de la exportación.

### Paso 3 – Guardar el libro como PPTX

```csharp
// Export the workbook to a PPTX file; the textbox stays editable in PowerPoint
workbookWithTextbox.Save("YOUR_DIRECTORY/Result.pptx", pptxOptions);
```

**Resultado esperado**: Abre `Result.pptx` en PowerPoint, selecciona el cuadro de texto y edita su contenido como cualquier forma nativa.

**Pregunta frecuente**: *¿Qué pasa si necesito mantener el cuadro de texto bloqueado?*  
Configura `pptxOptions.ExportEditableTextBox = false`; la forma se convertirá en una imagen estática.

---

## Exportar un Smart Marker que contiene un arreglo JSON como valor de una sola celda

Los Smart Markers te permiten rellenar plantillas Excel con estructuras de datos complejas. A continuación se muestra un ejemplo completo que demuestra el manejo de datos al estilo **how to copy pivot table** mientras inserta un arreglo JSON en una única celda.

### Paso 1 – Preparar el SmartMarkerProcessor

```csharp
// Initialise the processor that will fill Smart Markers
SmartMarkerProcessor smartMarkerProcessor = new SmartMarkerProcessor();
```

### Paso 2 – Insertar un Smart Marker en la celda A1

```csharp
// The marker ${Orders:ArrayAsSingle} tells the processor to write the whole array into one cell
Workbook workbook = new Workbook();
workbook.Worksheets[0].Cells["A1"].PutValue("${Orders:ArrayAsSingle}");
```

### Paso 3 – Definir la fuente de datos con un arreglo estilo JSON

```csharp
// Anonymous object that mimics a JSON array
var dataModel = new { Orders = new[] { "A", "B", "C" } };
```

### Paso 4 – Procesar el libro

```csharp
// Fill the Smart Marker with the array data; the array becomes a comma‑separated string
smartMarkerProcessor.Process(workbook, dataModel);
```

### Paso 5 – Guardar el libro resultante

```csharp
// Persist the workbook; cell A1 now contains "A,B,C"
workbook.Save("YOUR_DIRECTORY/JsonSingleCell.xlsx");
```

**Verificación del resultado**: Abre `JsonSingleCell.xlsx` y confirma que la celda A1 muestra `A,B,C`. Esto demuestra cómo tratar una colección como valor de una sola celda, un patrón frecuentemente necesario al exportar datos para sistemas downstream.

---

## Ejemplo completo

A continuación tienes un programa único que combina los tres escenarios. Puedes copiar el código en una aplicación de consola, ajustar las rutas de archivo y ejecutarlo para ver los tres resultados.

```csharp
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // 1. How to copy pivot table (preserve pivot cache)
        // -------------------------------------------------
        Workbook srcPivot = new Workbook("YOUR_DIRECTORY/Source.xlsx");
        Workbook dstPivot = new Workbook();
        srcPivot.Worksheets[0].Cells.CopyRows(0, 0, 20);
        srcPivot.Worksheets[0].Cells.CopyColumns(0, 0, 7);
        srcPivot.Worksheets[0].Copy(dstPivot.Worksheets[0]);
        dstPivot.Save("YOUR_DIRECTORY/CopyWithPivot.xlsx");

        // -------------------------------------------------
        // 2. Save workbook as PPTX with editable textbox
        // -------------------------------------------------
        Workbook txtWorkbook = new Workbook("YOUR_DIRECTORY/DocWithTextbox.xlsx");
        PptxSaveOptions pptxOpts = new PptxSaveOptions { ExportEditableTextBox = true };
        txtWorkbook.Save("YOUR_DIRECTORY/Result.pptx", pptxOpts);

        // -------------------------------------------------
        // 3. Export Smart Marker containing a JSON array
        // -------------------------------------------------
        SmartMarkerProcessor smProcessor = new SmartMarkerProcessor();
        Workbook smWorkbook = new Workbook();
        smWorkbook.Worksheets[0].Cells["A1"].PutValue("${Orders:ArrayAsSingle}");
        var model = new { Orders = new[] { "A", "B", "C" } };
        smProcessor.Process(smWorkbook, model);
        smWorkbook.Save("YOUR_DIRECTORY/JsonSingleCell.xlsx");
    }
}
```

Al ejecutar este programa se generan:

* `CopyWithPivot.xlsx` – una copia perfecta de la tabla dinámica original.  
* `Result.pptx` – una diapositiva PowerPoint con un cuadro de texto editable.  
* `JsonSingleCell.xlsx` – una hoja donde el arreglo JSON aparece en una sola celda.

---

## Conclusión

Ahora sabes **how to copy pivot table** de forma segura, cómo **copy worksheet with pivot** en una sola llamada y cómo **save workbook as pptx** preservando los cuadros de texto editables. Estos patrones cubren los flujos de trabajo más comunes de Excel‑a‑PowerPoint y Excel‑a‑JSON que encontrarás en proyectos de automatización empresarial.

A continuación, considera explorar:

* Refrescar tablas dinámicas copiadas programáticamente (`PivotTable.Refresh()`)  
* Exportar a otros formatos como PDF o HTML (`PdfSaveOptions`, `HtmlSaveOptions`)  
* Usar opciones avanzadas de Smart Marker como funciones personalizadas o formato condicional  

Siéntete libre de experimentar con diferentes rangos, múltiples hojas o estructuras JSON más grandes. La API de Aspose.Cells te brinda control granular, para que puedas adaptar estos ejemplos a cualquier escenario del mundo real. ¡Feliz codificación!

## ¿Qué deberías aprender a continuación?

Los tutoriales siguientes cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos con explicaciones paso a paso para ayudarte a dominar funciones adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Create New Workbook – How to Copy a Worksheet with a Pivot Table](/cells/english/net/excel-copy-worksheet/create-new-workbook-how-to-copy-a-worksheet-with-a-pivot-tab/)
- [How to Copy Pivot Table in C# – Convert Excel to PPTX, Copy Range & Make Textbox](/cells/english/net/pivot-tables/how-to-copy-pivot-table-in-c-convert-excel-to-pptx-copy-rang/)
- [Copy Sheets Within Workbook Using Aspose.Cells for .NET - Step‑By‑Step Guide](/cells/english/net/worksheet-management/copy-sheets-within-workbook-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}