---
category: general
date: 2026-11-16
description: Aprende cómo guardar Excel como PowerPoint y convertir Excel a PowerPoint
  de forma programática. Esta guía paso a paso también cubre la exportación de Excel
  a PPTX y guardar un libro de trabajo como PPTX.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- save excel as powerpoint
- convert excel to powerpoint
- export excel to pptx
- how to convert excel slide
- save workbook as pptx
language: es
lastmod: 2026-11-16
og_description: Guarda Excel como PowerPoint usando Aspose.Cells. Sigue esta guía
  para convertir Excel a PowerPoint, exportar Excel a PPTX y guardar el libro de trabajo
  como PPTX en minutos.
og_image_alt: Screenshot showing the result of saving Excel as PowerPoint with editable
  shapes
og_title: Guardar Excel como PowerPoint – Guía completa de C#
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: Learn how to save Excel as PowerPoint and convert Excel to PowerPoint
    programmatically. This step‑by‑step guide also covers export Excel to PPTX and
    saving a workbook as PPTX.
  headline: How to save Excel as PowerPoint with Aspose.Cells in C#
  type: TechArticle
tags:
- Excel
- PowerPoint
- Aspose.Cells
- C#
- Export
title: Cómo guardar Excel como PowerPoint con Aspose.Cells en C#
url: /es/net/converting-excel-files-to-other-formats/how-to-save-excel-as-powerpoint-with-aspose-cells-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo guardar Excel como PowerPoint con Aspose.Cells en C#

Si necesita **guardar Excel como PowerPoint** de forma programática, este tutorial le brinda una solución completa y lista‑para‑ejecutar. Ya sea que esté construyendo un motor de informes o un generador de diapositivas automatizado, los pasos a continuación le permiten convertir una hoja de cálculo de Excel en una diapositiva PPTX editable con solo unas pocas líneas de código.

Aprenderá cómo **convertir Excel a PowerPoint**, exportar la hoja a un archivo PPTX y mantener los cuadros de texto y las formas editables, todo sin salir del entorno .NET.

## Requisitos previos

Antes de comenzar, asegúrese de tener:

* .NET 6.0 o posterior (el código también funciona con .NET Framework 4.7.2+)
* Una licencia válida de Aspose.Cells (la prueba gratuita funciona para evaluación)
* Visual Studio 2022 (o cualquier IDE de C#)
* Un libro de Excel que contenga los datos y las formas que desea exportar

## Paso 1: Instalar Aspose.Cells

Agregue el paquete NuGet de Aspose.Cells a su proyecto:

```bash
dotnet add package Aspose.Cells
```

> **Consejo profesional:** Use la bandera `-v` para apuntar a una versión específica, por ejemplo, `Aspose.Cells.24.5`.

## Paso 2: Cargar el libro de trabajo que desea exportar

La primera operación en el flujo de trabajo de **guardar Excel como PowerPoint** es cargar el libro de trabajo de origen.

```csharp
using Aspose.Cells;
using System;

// Load the workbook that contains the shapes
Workbook workbook = new Workbook(@"C:\Data\WithShapes.xlsx");
```

*Por qué es importante:* Cargar el libro de trabajo le brinda acceso a sus hojas, la configuración de página y los objetos de dibujo que se convertirán en formas editables de PowerPoint.

## Paso 3: Configurar opciones de exportación para una diapositiva PPTX editable

Para **convertir Excel a PowerPoint** manteniendo la editabilidad, debe establecer algunas propiedades en `ImageOrPrintOptions`.

```csharp
// Prepare export options to generate an editable PPTX slide
ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
{
    SaveFormat = SaveFormat.Pptx,      // Export format
    ExportEditableText = true,        // Keep text boxes editable
    ExportEditableShapes = true       // Keep shapes editable
};
```

*Explicación:*  
* `SaveFormat = SaveFormat.Pptx` indica a Aspose.Cells que genere un archivo PowerPoint.  
* `ExportEditableText` y `ExportEditableShapes` garantizan que la diapositiva resultante se comporte como una diapositiva nativa de PowerPoint: puede hacer clic en un cuadro de texto o forma y editarlo directamente en PowerPoint.

## Paso 4: Definir el área de exportación y ajustarla a una sola diapositiva

Cuando **exporta Excel a PPTX**, normalmente desea que un rango específico aparezca en la diapositiva. Configurar el área de impresión y las opciones de ajuste garantiza una salida limpia de una sola diapositiva.

```csharp
// Define the area of the first worksheet to export
Worksheet sheet = workbook.Worksheets[0];
sheet.PageSetup.PrintArea = "A1:G30";

// Fit the exported content to a single slide
sheet.PageSetup.FitToPagesTall = 1;
sheet.PageSetup.FitToPagesWide = 1;
```

*Por qué es importante:* `PrintArea` limita la exportación a las celdas A1 a G30, mientras que `FitToPagesTall` y `FitToPagesWide` comprimen todo en una sola diapositiva, evitando páginas adicionales no deseadas.

## Paso 5: Guardar la hoja de cálculo como un archivo PPTX editable

Ahora puede finalmente **guardar el libro como PPTX** y completar el proceso de **guardar Excel como PowerPoint**.

```csharp
// Save the worksheet as an editable PPTX file
workbook.Save(@"C:\Output\EditableShapes.pptx", exportOptions);
Console.WriteLine("Export completed: EditableShapes.pptx");
```

Después de ejecutar el programa, abra `EditableShapes.pptx` en Microsoft PowerPoint. Verá una diapositiva que refleja el rango de Excel seleccionado, y todos los cuadros de texto y formas son completamente editables.

### Resultado esperado

* Un archivo llamado `EditableShapes.pptx` ubicado en `C:\Output\`.
* Una diapositiva de PowerPoint que contiene el rango A1:G30.
* Cuadros de texto, gráficos y formas que puede hacer doble clic y editar directamente en PowerPoint.

## Código fuente completo (listo para copiar)

```csharp
using Aspose.Cells;
using System;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Load the workbook that contains the shapes
            Workbook workbook = new Workbook(@"C:\Data\WithShapes.xlsx");

            // Step 2: Prepare export options to generate an editable PPTX slide
            ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
            {
                SaveFormat = SaveFormat.Pptx,
                ExportEditableText = true,   // keep text boxes editable
                ExportEditableShapes = true  // keep shapes editable
            };

            // Step 3: Define the area of the first worksheet to export
            Worksheet sheet = workbook.Worksheets[0];
            sheet.PageSetup.PrintArea = "A1:G30";

            // Step 4: Fit the exported content to a single slide
            sheet.PageSetup.FitToPagesTall = 1;
            sheet.PageSetup.FitToPagesWide = 1;

            // Step 5: Save the worksheet as an editable PPTX file
            workbook.Save(@"C:\Output\EditableShapes.pptx", exportOptions);
            Console.WriteLine("Export completed: EditableShapes.pptx");
        }
    }
}
```

## Preguntas frecuentes y manejo de casos límite

| Question | Answer |
|----------|--------|
| **¿Qué pasa si tengo varias hojas de cálculo?** | Recorra `workbook.Worksheets` y repita los pasos 3‑5 para cada hoja, cambiando el nombre del archivo de salida (p. ej., `Sheet1.pptx`, `Sheet2.pptx`). |
| **¿Puedo exportar todo el libro a una sola presentación de PowerPoint?** | Sí. Establezca `ExportAllSheets = true` en `ImageOrPrintOptions`. Cada hoja de cálculo se convierte en una diapositiva separada. |
| **Mis formas aparecen como imágenes, no como objetos editables.** | Asegúrese de que `ExportEditableShapes = true` y de que está usando Aspose.Cells 24.5+ (las versiones anteriores carecen de esta función). |
| **El PPTX generado es demasiado grande.** | Reduzca el área de impresión o disminuya la resolución de la imagen mediante `exportOptions.ImageResolution`. |
| **¿Necesito una licencia para uso en producción?** | Una licencia de pago elimina la marca de agua de evaluación y desbloquea el rendimiento completo. La prueba gratuita funciona para pruebas. |

## Consejos para código de producción robusto

* **Validar rutas de archivo** antes de llamar a `Workbook` o `Save` para evitar `FileNotFoundException`.  
* **Encapsular la exportación en un bloque try/catch** para manejar errores de licencia (`Aspose.Cells.LicenseException`).  
* **Liberar el libro** (`workbook.Dispose()`) cuando haya terminado para liberar recursos no administrados.  
* **Utilizar I/O asíncrono** (`FileStream` con `await`) si está exportando muchas hojas grandes en un servicio web.

## Próximos pasos

Ahora que sabe cómo **guardar Excel como PowerPoint**, puede explorar temas relacionados:

* **Exportar Excel a PPTX con diseños de diapositiva personalizados** – ajuste `SlideSize` y agregue una diapositiva maestra.  
* **Convertir la diapositiva de Excel a PDF** – use `SaveFormat.Pdf` para una versión imprimible.  
* **Convertir por lotes una carpeta de libros** – combine el bucle mostrado arriba con `Directory.GetFiles`.  

Experimente con diferentes áreas de impresión, opciones de escalado y temas de PowerPoint para adaptar la salida a la identidad corporativa de su organización.

---

*¡Feliz codificación! Si esta guía le ayudó a **convertir Excel a PowerPoint**, siéntase libre de compartirla con sus compañeros o abrir un issue en el repositorio de Aspose.Cells en GitHub para obtener más ayuda.*

## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que se basan en las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y funcionales con explicaciones paso a paso para ayudarle a dominar características adicionales de la API y explorar enfoques de implementación alternativos en sus propios proyectos.

- [Cómo guardar Excel como PowerPoint usando C# y Aspose.Cells](/cells/english/net/converting-excel-files-to-other-formats/how-to-save-excel-as-powerpoint-using-c-and-aspose-cells/)
- [Cómo guardar PPTX desde Excel – Guía completa para exportar hoja de Excel a PowerPoint](/cells/english/java/integration-interoperability/how-to-save-pptx-from-excel-complete-guide-to-export-excel-s/)
- [Convertir Excel a PowerPoint – Guía completa paso a paso](/cells/english/java/integration-interoperability/convert-excel-to-powerpoint-full-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}