---
category: general
date: 2026-10-20
description: Copiar tabla dinámica a un nuevo libro de trabajo usando Aspose.Cells
  y aprender cómo exportar una forma editable a PowerPoint en una única guía.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy pivot table to new workbook
- copy rows between worksheets
- Aspose.Cells copy rows
- export shape to PowerPoint
- editable textbox in PowerPoint
language: es
lastmod: 2026-10-20
og_description: 'Copiar tabla dinámica a un nuevo libro de trabajo usando Aspose.Cells
  y exportar una forma editable a PowerPoint: código paso a paso que puedes ejecutar
  hoy.'
og_image_alt: Screenshot showing copy pivot table to new workbook using Aspose.Cells
og_title: Copiar tabla dinámica a un nuevo libro de trabajo, exportar forma a PowerPoint
schemas:
- author: Aspose
  dateModified: '2026-10-20'
  description: Copy pivot table to new workbook using Aspose.Cells and learn how to
    export an editable shape to PowerPoint in a single guide.
  headline: Copy pivot table to new workbook, export shape to PowerPoint
  type: TechArticle
- description: Copy pivot table to new workbook using Aspose.Cells and learn how to
    export an editable shape to PowerPoint in a single guide.
  name: Copy pivot table to new workbook, export shape to PowerPoint
  steps:
  - name: – Load the source workbook and select the first worksheet
    text: '```csharp // Load the workbook that already contains the pivot table Workbook
      srcWorkbook = new Workbook("YOUR_DIRECTORY/Source.xlsx");'
  - name: – Define the cell area that includes the pivot table
    text: '```csharp // CellArea(startRow, startColumn, endRow, endColumn) // Here
      we copy rows 0‑20 and columns 0‑10, which covers the whole pivot table CellArea
      sourceArea = new CellArea(0, 0, 20, 10); ```'
  - name: – Create the destination workbook and get its first worksheet
    text: '```csharp // Create an empty workbook that will receive the copied range
      Workbook destWorkbook = new Workbook();'
  - name: – Copy the rows from the source area to the destination sheet
    text: '```csharp // CopyRows(startRow, endRow, destinationCells, destinationStartRow)
      srcWorksheet.Cells.CopyRows( sourceArea.StartRow, sourceArea.EndRow, destWorksheet.Cells,
      0); // start at row 0 in the destination sheet ```'
  - name: – Save the new workbook
    text: '```csharp destWorkbook.Save("YOUR_DIRECTORY/CopyWithPivot.xlsx"); ```'
  - name: – Create a new workbook and access its first worksheet
    text: '```csharp Workbook workbook = new Workbook(); // Empty workbook Worksheet
      worksheet = workbook.Worksheets[0]; // First (and only) sheet ```'
  - name: – Add a textbox shape to the worksheet
    text: '```csharp // AddTextBox(startRow, startColumn, width, height, text) int
      shapeIndex = worksheet.Shapes.AddTextBox(10, 10, 200, 50, "Editable text");
      ```'
  - name: – Retrieve the shape and modify its text
    text: '```csharp Shape textShape = worksheet.Shapes[shapeIndex]; textShape.Text
      = "Change me in PowerPoint"; ```'
  - name: – Save the workbook as a PowerPoint presentation
    text: '```csharp workbook.Save("YOUR_DIRECTORY/Presentation.pptx", SaveFormat.Pptx);
      ```'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Pivot Table
- PowerPoint Export
title: Copiar tabla dinámica a un nuevo libro, exportar forma a PowerPoint
url: /es/net/pivot-tables/copy-pivot-table-to-new-workbook-export-shape-to-powerpoint/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Copiar tabla dinámica a un nuevo libro, exportar forma a PowerPoint

Si necesitas **copiar tabla dinámica a un nuevo libro** conservando su funcionalidad, esta guía te muestra exactamente cómo hacerlo con Aspose.Cells. También verás la forma más rápida de **exportar una forma editable a PowerPoint**, de modo que el cuadro de texto permanezca editable después de la conversión.

Muchos desarrolladores asumen que copiar un rango que contiene una tabla dinámica perderá la lógica de la tabla, o que las formas se convierten en imágenes estáticas al guardarse como PPTX. Este tutorial desmiente esos mitos y te brinda una solución fiable y lista para producción.

En las siguientes secciones podrás:

* Cargar un libro de origen y copiar un rango que incluye una tabla dinámica.
* Crear un libro de destino que contenga la misma tabla dinámica.
* Añadir una forma de cuadro de texto, modificar su texto y guardar el libro como una presentación de PowerPoint donde el cuadro de texto siga siendo editable.
* Entender por qué cada llamada a la API es necesaria y cómo evitar errores comunes.

**Requisitos previos**

* .NET 6.0 o posterior (el código también funciona con .NET Framework 4.7+).
* Aspose.Cells para .NET instalado (`Install-Package Aspose.Cells`).
* Conocimientos básicos de C# y Visual Studio (o cualquier IDE que prefieras).

---

## Copiar tabla dinámica a un nuevo libro

Esta sección paso a paso muestra cómo copiar un rango que contiene una tabla dinámica y conservar la definición de la tabla en el nuevo archivo.

### Paso 1 – Cargar el libro de origen y seleccionar la primera hoja

```csharp
// Load the workbook that already contains the pivot table
Workbook srcWorkbook = new Workbook("YOUR_DIRECTORY/Source.xlsx");

// The first worksheet (index 0) holds the pivot table we want to copy
Worksheet srcWorksheet = srcWorkbook.Worksheets[0];
```

*¿Por qué?*  
`Workbook` es el punto de entrada para cualquier manipulación de Excel en Aspose.Cells. Seleccionar la hoja correcta garantiza que trabajemos con la ubicación exacta de la tabla dinámica.

### Paso 2 – Definir el área de celdas que incluye la tabla dinámica

```csharp
// CellArea(startRow, startColumn, endRow, endColumn)
// Here we copy rows 0‑20 and columns 0‑10, which covers the whole pivot table
CellArea sourceArea = new CellArea(0, 0, 20, 10);
```

*¿Por qué?*  
La tabla dinámica vive dentro de un bloque específico de celdas. Al especificar un `CellArea` que englobe completamente la tabla, Aspose.Cells sabe copiar también la caché subyacente de la tabla dinámica.

### Paso 3 – Crear el libro de destino y obtener su primera hoja

```csharp
// Create an empty workbook that will receive the copied range
Workbook destWorkbook = new Workbook();

// Destination worksheet (also index 0)
Worksheet destWorksheet = destWorkbook.Worksheets[0];
```

*¿Por qué?*  
Un libro nuevo garantiza que no haya rangos nombrados conflictivos ni tablas dinámicas existentes, lo que hace que la operación de copia sea limpia.

### Paso 4 – Copiar las filas del área de origen a la hoja de destino

```csharp
// CopyRows(startRow, endRow, destinationCells, destinationStartRow)
srcWorksheet.Cells.CopyRows(
    sourceArea.StartRow,
    sourceArea.EndRow,
    destWorksheet.Cells,
    0); // start at row 0 in the destination sheet
```

*¿Por qué?*  
`CopyRows` forma parte de la **Aspose.Cells copy rows** API. Copia tanto los valores de las celdas como la caché oculta de la tabla dinámica, de modo que la tabla sigue siendo funcional después del traslado.

### Paso 5 – Guardar el nuevo libro

```csharp
destWorkbook.Save("YOUR_DIRECTORY/CopyWithPivot.xlsx");
```

*Resultado*  
Abre `CopyWithPivot.xlsx` en Excel. La tabla dinámica aparece exactamente como en el archivo de origen, y puedes actualizarla o modificarla normalmente.

---

## Exportar forma editable a PowerPoint

Ahora añadiremos una forma de cuadro de texto, cambiaremos su contenido y guardaremos el libro como un archivo PPTX. La forma permanecerá totalmente editable al abrirse en PowerPoint.

### Paso 1 – Crear un nuevo libro y acceder a su primera hoja

```csharp
Workbook workbook = new Workbook();          // Empty workbook
Worksheet worksheet = workbook.Worksheets[0]; // First (and only) sheet
```

### Paso 2 – Añadir una forma de cuadro de texto a la hoja

```csharp
// AddTextBox(startRow, startColumn, width, height, text)
int shapeIndex = worksheet.Shapes.AddTextBox(10, 10, 200, 50, "Editable text");
```

*¿Por qué?*  
`AddTextBox` crea una **forma de cuadro de texto editable compatible con PowerPoint**. Las coordenadas están en puntos; ajústalas para que encajen en tu diseño.

### Paso 3 – Obtener la forma y modificar su texto

```csharp
Shape textShape = worksheet.Shapes[shapeIndex];
textShape.Text = "Change me in PowerPoint";
```

*¿Por qué?*  
Acceder directamente al objeto `Shape` te permite cambiar propiedades como `Text`, `Font` o `Fill`. Este paso muestra cómo establecer programáticamente el contenido inicial.

### Paso 4 – Guardar el libro como una presentación de PowerPoint

```csharp
workbook.Save("YOUR_DIRECTORY/Presentation.pptx", SaveFormat.Pptx);
```

*Resultado*  
Abre `Presentation.pptx` en Microsoft PowerPoint. El cuadro de texto aparece en la primera diapositiva y puedes hacer doble clic para editar el texto como cualquier forma nativa de PowerPoint.

---

## Resultado esperado

| Archivo | Lo que verás |
|------|-----------------|
| `CopyWithPivot.xlsx` | Una hoja que contiene la tabla dinámica original, totalmente funcional (la actualización funciona). |
| `Presentation.pptx` | Una sola diapositiva con un cuadro de texto editable que dice “Change me in PowerPoint”. |

---

## Errores comunes y consejos de buenas prácticas

* **Pérdida de caché de la tabla dinámica** – Si solo copias valores de celda (p. ej., usando `CopyRows` con la bandera `PasteOptions` establecida en `PasteValues`), la caché de la tabla se omite y la tabla se vuelve estática. Siempre usa la sobrecarga predeterminada de `CopyRows` como se muestra.
* **Posicionamiento de la forma** – `AddTextBox` utiliza unidades de punto, no índices de celdas de Excel. Prueba las coordenadas en un archivo de muestra para evitar que la forma quede fuera de la diapositiva.
* **Desajuste de formato de archivo** – Guardar un libro como PPTX con `SaveFormat.Pptx` convierte automáticamente todas las formas compatibles. Intentar guardarlo como `Pdf` rasterizará la forma, haciéndola no editable.

---

## Conclusión

Ahora sabes cómo **copiar tabla dinámica a un nuevo libro** y cómo **exportar una forma editable a PowerPoint** usando Aspose.Cells para .NET. Los ejemplos de código completos y ejecutables cubren cada llamada a la API requerida, explican por qué cada paso es importante y muestran los resultados esperados.

A continuación, podrías explorar:

* **Trabajar con gráficos** – copiar gráficos junto con tablas dinámicas (`Aspose.Cells copy rows between worksheets`).
* 

## ¿Qué deberías aprender a continuación?

Los tutoriales siguientes cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos con explicaciones paso a paso para ayudarte a dominar funciones adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Create New Workbook – How to Copy a Worksheet with a Pivot Table](/cells/english/net/excel-copy-worksheet/create-new-workbook-how-to-copy-a-worksheet-with-a-pivot-tab/)
- [Copy pivot table and export Excel to PPTX with Aspose.Cells](/cells/english/net/converting-excel-files-to-other-formats/copy-pivot-table-and-export-excel-to-pptx-with-aspose-cells/)
- [Create New Workbook in C# – Copy Pivot Table](/cells/english/net/pivot-tables/create-new-workbook-in-c-copy-pivot-table/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}