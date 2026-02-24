---
category: general
date: 2026-01-14
description: Cómo copiar una tabla dinámica usando Aspose.Cells y también aprender
  a convertir Excel a PPTX, copiar un rango a otro libro de trabajo y hacer que el
  cuadro de texto sea editable en PPTX en un solo tutorial.
draft: false
keywords:
- how to copy pivot table
- convert excel to pptx
- copy range to another workbook
- make textbox editable pptx
- save workbook as pptx
language: es
og_description: Cómo copiar una tabla dinámica y luego convertir Excel a PPTX, copiar
  un rango a otro libro de trabajo y hacer que el cuadro de texto sea editable en
  PPTX, todo con Aspose.Cells.
og_title: Cómo copiar una tabla dinámica en C# – Guía completa de Excel a PPTX
tags:
- Aspose.Cells
- C#
- Excel automation
- PowerPoint export
title: Cómo copiar una tabla dinámica en C# – Convertir Excel a PPTX, copiar rango
  y hacer editable el cuadro de texto
url: /es/net/pivot-tables/how-to-copy-pivot-table-in-c-convert-excel-to-pptx-copy-rang/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo copiar una tabla dinámica en C# – Guía completa de Excel a PPTX

Cómo copiar una tabla dinámica de un libro a otro es una pregunta frecuente cuando automatizas informes basados en Excel. En este tutorial recorreremos tres escenarios del mundo real usando **Aspose.Cells for .NET**: copiar un rango de tabla dinámica, exportar una hoja de cálculo a un archivo PPTX con un cuadro de texto editable y rellenar una sola celda con un arreglo JSON mediante Smart Markers.  

También verás cómo **convertir Excel a PPTX**, **copiar rangos a otro libro** y **hacer que el cuadro de texto sea editable en PPTX** sin romper el formato. Al final tendrás una base de código lista para ejecutar que puedes incorporar a cualquier proyecto .NET.

> **Consejo profesional:** Todos los ejemplos están dirigidos a Aspose.Cells 23.12, pero los mismos conceptos se aplican a versiones anteriores con pequeñas variaciones en la API.

![Diagrama que muestra cómo se copia una tabla dinámica, se exporta una hoja a PPTX y se inserta un arreglo JSON – flujo de trabajo para copiar tabla dinámica](how-to-copy-pivot-table-diagram.png)

---

## Qué necesitarás

- Visual Studio 2022 (o cualquier IDE de C#)
- .NET 6.0 o versión posterior
- Paquete NuGet de Aspose.Cells for .NET  
  ```bash
  dotnet add package Aspose.Cells
  ```
- Dos archivos de Excel de ejemplo (`source.xlsx`, `chartWithTextbox.xlsx`) ubicados en una carpeta que controles (reemplaza `YOUR_DIRECTORY` con tu ruta real).

No se requieren bibliotecas adicionales; el mismo ensamblado `Aspose.Cells` gestiona Excel, PPTX y Smart Markers.

---

## Cómo copiar una tabla dinámica y conservar sus datos

Cuando copias un rango que contiene una tabla dinámica, el comportamiento predeterminado es pegar solo los **valores**. Para mantener intacta la definición de la tabla dinámica debes habilitar la bandera `CopyPivotTable`.

### Paso a paso

1. **Carga el libro de origen** que contiene la tabla dinámica.  
2. **Crea un libro de destino vacío** – recibirá el rango copiado.  
3. **Usa `CopyRange` con `CopyPivotTable = true`** para que la definición de la tabla dinámica viaje con los datos.  
4. **Guarda el archivo de destino** donde lo necesites.

#### Ejemplo de código completo

```csharp
using Aspose.Cells;

class PivotCopyDemo
{
    static void Main()
    {
        // Step 1: Load the source workbook and define the range to copy
        Workbook sourceWorkbook = new Workbook(@"YOUR_DIRECTORY\source.xlsx");
        Worksheet sourceSheet = sourceWorkbook.Worksheets[0];
        // Assuming the pivot table lives inside A1:G20
        Range sourceRange = sourceSheet.Cells.CreateRange("A1:G20");

        // Step 2: Create a destination workbook (blank)
        Workbook destinationWorkbook = new Workbook();
        Worksheet destinationSheet = destinationWorkbook.Worksheets[0];

        // Step 3: Copy the range, preserving the pivot table
        destinationSheet.Cells.CopyRange(
            sourceRange,
            "B2", // paste start cell
            new CopyOptions { CopyPivotTable = true });

        // Step 4: Save the result
        destinationWorkbook.Save(@"YOUR_DIRECTORY\copyWithPivot.xlsx");
    }
}
```

**Por qué funciona:**  
`CopyOptions.CopyPivotTable` indica a Aspose.Cells que clone el objeto subyacente `PivotTable` en lugar de solo sus valores renderizados. El libro de destino ahora contiene una tabla dinámica totalmente funcional que puedes actualizar o modificar programáticamente.

**Caso límite:** Si el libro de origen usa fuentes de datos externas, puede que necesites incrustar los datos o ajustar las cadenas de conexión después de copiar; de lo contrario, la tabla mostrará “#REF!”.

---

## Convertir Excel a PPTX y hacer que el cuadro de texto sea editable

Exportar una hoja a PowerPoint es útil para crear presentaciones directamente desde los datos. Por defecto, el cuadro de texto exportado se convierte en una forma estática, pero al establecer `IsTextBoxEditable` se invierte ese comportamiento.

### Paso a paso

1. **Abre el libro** que contiene el gráfico y el cuadro de texto que deseas exportar.  
2. **Configura `ImageOrPrintOptions`** con `SaveFormat = SaveFormat.Pptx`.  
3. **Define un área de impresión** que incluya el cuadro de texto.  
4. **Habilita `IsTextBoxEditable`** para que el texto pueda editarse después de abrir el PPTX.  
5. **Guarda el archivo PPTX**.

#### Ejemplo de código completo

```csharp
using Aspose.Cells;

class ExcelToPptxDemo
{
    static void Main()
    {
        // Step 1: Load the workbook with chart and textbox
        Workbook chartWorkbook = new Workbook(@"YOUR_DIRECTORY\chartWithTextbox.xlsx");

        // Step 2: Set export options for PPTX
        ImageOrPrintOptions pptxOptions = new ImageOrPrintOptions
        {
            SaveFormat = SaveFormat.Pptx
        };

        // Step 3: Define the print area that captures the textbox (A1:D20)
        chartWorkbook.Worksheets[0].PageSetup.PrintArea = "A1:D20";

        // Step 4: Make the textbox editable in the exported PPTX
        chartWorkbook.Worksheets[0].PageSetup.IsTextBoxEditable = true;

        // Step 5: Export the worksheet to a PPTX file
        chartWorkbook.Save(@"YOUR_DIRECTORY\result.pptx", pptxOptions);
    }
}
```

**Resultado:** Abre `result.pptx` en PowerPoint – el cuadro de texto que colocaste en Excel será ahora un cuadro de texto regular en el que podrás escribir. No es necesario volver a crearlo manualmente.

**Trampa común:** Si la hoja contiene celdas combinadas que intersectan el área de impresión, la diapositiva resultante puede desplazarse. Ajusta el área de impresión o descombina las celdas antes de exportar.

---

## Copiar rango a otro libro con Smart Markers (JSON → Celda única)

A veces necesitas incrustar un arreglo JSON en una sola celda de Excel, por ejemplo al pasar datos a sistemas posteriores que esperan una cadena JSON. Los Smart Markers de Aspose.Cells pueden serializar un arreglo como una celda única cuando estableces `ArrayAsSingle = true`.

### Paso a paso

1. **Carga un libro plantilla** que contenga un marcador inteligente (p. ej., `&=Items.Name`).  
2. **Prepara el objeto de datos** – un tipo anónimo con un arreglo `Items`.  
3. **Crea un `SmartMarkerProcessor`** y aplica los datos con `ArrayAsSingle`.  
4. **Guarda el libro poblado**.

#### Ejemplo de código completo

```csharp
using Aspose.Cells;
using System;

class SmartMarkerDemo
{
    static void Main()
    {
        // Step 1: Load the template workbook containing a smart marker like "&=Items.Name"
        Workbook templateWorkbook = new Workbook(@"YOUR_DIRECTORY\SmartMarkerTemplate.xlsx");

        // Step 2: Prepare the data object with an array of items
        var data = new
        {
            Items = new[]
            {
                new { Name = "A" },
                new { Name = "B" }
            }
        };

        // Step 3: Apply the SmartMarkerProcessor with ArrayAsSingle option
        SmartMarkerProcessor processor = new SmartMarkerProcessor(templateWorkbook);
        processor.Apply(data, new SmartMarkerOptions { ArrayAsSingle = true });

        // Step 4: Save the result – the JSON array will appear in a single cell
        templateWorkbook.Save(@"YOUR_DIRECTORY\jsonSingleCell.xlsx");
    }
}
```

**Explicación:**  
Cuando `ArrayAsSingle` es verdadero, Aspose.Cells concatena cada elemento de `Items.Name` en una cadena con estilo JSON (`["A","B"]`) y la escribe en la celda que contenía el marcador inteligente. Esto evita crear una fila separada por cada elemento del arreglo.

**Cuándo usarlo:** Ideal para exportar tablas de configuración, cargas útiles de API o cualquier escenario donde el consumidor espere una cadena JSON compacta en lugar de un diseño tabular.

---

## Consejos adicionales y manejo de casos límite

| Escenario | Qué observar | Solución sugerida |
|----------|--------------|-------------------|
| **Tablas dinámicas grandes** | Picos de uso de memoria al copiar cachés de tabla dinámica. | Usa `WorkbookSettings.MemorySetting = MemorySetting.MemoryPreference` antes de cargar. |
| **Exportar a PPTX con imágenes** | Las imágenes pueden rasterizarse a baja DPI. | Establece `pptxOptions.ImageResolution = 300` para diapositivas más nítidas. |
| **Formato JSON en Smart Marker** | Caracteres especiales (`"` , `\`) rompen el JSON. | Escápalos manualmente o usa `JsonSerializer` para pre‑serializar antes de pasar a Smart Markers. |
| **Copiar rango entre versiones diferentes de Excel** | Los archivos `.xls` antiguos pueden perder formato. | Guarda el destino como `.xlsx` para preservar características modernas. |

---

## Recapitulación – Cómo copiar una tabla dinámica y mucho más

Comenzamos respondiendo **cómo copiar una tabla dinámica** conservando su funcionalidad, luego te mostramos cómo **convertir Excel a PPTX**, **hacer que el cuadro de texto sea editable en PPTX**, y finalmente cómo **copiar un rango a otro libro** usando Smart Markers para incrustar un arreglo JSON en una sola celda.  

Los tres fragmentos son autónomos; puedes pegarlos en una nueva aplicación de consola, ajustar las rutas de archivo y ejecutarlos hoy mismo.

---

## ¿Qué sigue?

- **Explora otros formatos de exportación** – Aspose.Cells también admite PDF, XPS y HTML.  
- **Actualiza programáticamente las tablas dinámicas** usando `PivotTable.RefreshData()` después de copiarlas.  
- **Combina Smart Markers con gráficos** para generar paneles dinámicos que se actualicen automáticamente.  

Si te interesa **guardar el libro como PPTX** con diseños de diapositiva personalizados, revisa la documentación de Aspose.Cells sobre `SlideOptions`.  

Siéntete libre de experimentar: cambia el área de impresión, prueba diferentes `CopyOptions` o alimenta una carga JSON más compleja. La API es lo suficientemente flexible para la mayoría de los pipelines de informes.

---

### Preguntas frecuentes

**P: ¿`CopyPivotTable` también copia los segmentadores (slicers)?**  
R: No directamente. Los segmentadores son objetos separados; después de copiar deberás recrearlos o copiarlos mediante la colección `Worksheet.Shapes`.

**P: ¿Puedo exportar varias hojas a un solo deck PPTX?**  
R: Sí. Recorre cada hoja, llama a `Save` con el mismo `ImageOrPrintOptions` y establece `pptxOptions.StartSlideNumber` para continuar la numeración.

**P: ¿Qué pasa si mi arreglo JSON contiene objetos anidados?**  
R: Establece `ArrayAsSingle = false` y usa una plantilla personalizada que itere sobre los objetos anidados.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}