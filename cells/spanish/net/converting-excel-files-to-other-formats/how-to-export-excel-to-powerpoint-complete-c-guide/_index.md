---
category: general
date: 2026-06-27
description: Cómo exportar Excel usando C# — aprende a convertir Excel a PowerPoint,
  crear PowerPoint desde Excel y cargar un libro de Excel en C# en minutos.
draft: false
keywords:
- how to export excel
- convert excel to powerpoint
- create powerpoint from excel
- load excel workbook c#
- export excel chart powerpoint
language: es
og_description: Cómo exportar Excel usando C# es sencillo. Sigue este tutorial paso
  a paso para convertir Excel a PowerPoint, crear PowerPoint desde Excel y cargar
  un libro de Excel en C#.
og_title: Cómo exportar Excel a PowerPoint – Guía completa de C#
schemas:
- author: Aspose
  dateModified: '2026-06-27'
  description: How to export Excel using C#—learn to convert Excel to PowerPoint,
    create PowerPoint from Excel, and load Excel workbook C# in minutes.
  headline: How to Export Excel to PowerPoint – Complete C# Guide
  type: TechArticle
- description: How to export Excel using C#—learn to convert Excel to PowerPoint,
    create PowerPoint from Excel, and load Excel workbook C# in minutes.
  name: How to Export Excel to PowerPoint – Complete C# Guide
  steps:
  - name: '**Load Excel workbook** – We read the `.xlsx` file into memory.'
    text: '**Load Excel workbook** – We read the `.xlsx` file into memory.'
  - name: '**Convert workbook to a PowerPoint presentation** – Aspose converts each
      worksheet (or selected chart) into a slide.'
    text: '**Convert workbook to a PowerPoint presentation** – Aspose converts each
      worksheet (or selected chart) into a slide.'
  - name: '**Save the generated presentation** – The final PPTX can be opened in PowerPoint,
      edited, or sent to stakeholders.'
    text: '**Save the generated presentation** – The final PPTX can be opened in PowerPoint,
      edited, or sent to stakeholders.'
  type: HowTo
- questions:
  - answer: Yes. Use `Workbook.Worksheets["Sheet1"]` to isolate a sheet, then call
      `SaveToPresentation` on that worksheet alone.
    question: Can I export only a single worksheet instead of the whole workbook?
  - answer: Macros are not transferred to PowerPoint—only visual objects (charts,
      tables) are exported. If you need macro functionality, consider generating the
      slides first, then adding VBA manually.
    question: What about preserving macros?
  - answer: Absolutely. Aspose.Cells supports legacy formats; just change the file
      extension in `excelPath`.
    question: Does this work with `.xls` files?
  - answer: 'After creating the `Presentation` object, set: ```csharp presentation.SlideSize.Size
      = SlideSizeType.Widescreen; ```'
    question: How do I change the slide size to widescreen (16:9)?
  - answer: 'Open‑source libraries like EPPlus can read Excel, but they don’t provide
      direct Excel‑to‑PowerPoint conversion. You’d need to manually render charts
      to images and insert them, which is far more code. ## Tips & Best Practices
      - **Batch processing:** If you have dozens of workbooks, wrap the conversio'
    question: Is there a free alternative?
  type: FAQPage
tags:
- C#
- Excel
- PowerPoint
- Aspose
title: Cómo exportar Excel a PowerPoint – Guía completa de C#
url: /es/net/converting-excel-files-to-other-formats/how-to-export-excel-to-powerpoint-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo exportar Excel a PowerPoint – Guía completa en C#

¿Alguna vez te has preguntado **cómo exportar datos de Excel** directamente a una presentación de PowerPoint sin perder el formato? No eres el único. En muchos flujos de informes, el cuello de botella es pasar gráficos y tablas de un libro de Excel a una presentación elegante. ¿La buena noticia? Con solo unas pocas líneas de C# puedes **convertir Excel a PowerPoint**, generar un PPTX totalmente editable e incluso conservar la fidelidad del gráfico.

En este tutorial recorreremos la carga de un libro de Excel en C#, la transformación de su contenido en una presentación de PowerPoint y el guardado del resultado. Al final podrás **crear PowerPoint desde Excel** de forma automática—sin copiar‑pegar manualmente. Sin complicaciones de UI, solo código limpio.

> **Lo que necesitarás**  
> * .NET 6+ (o .NET Framework 4.7.2+)  
> * Los paquetes NuGet Aspose.Cells y Aspose.Slides (se encargan del trabajo pesado)  
> * Un archivo Excel de ejemplo con al menos un gráfico (lo llamaremos `chartOle.xlsx`)  

Si ya tienes todo eso, vamos a sumergirnos.

![Diagrama que muestra cómo exportar Excel a PowerPoint usando C#](https://example.com/images/export-excel-to-pptx.png "Diagrama de cómo exportar Excel a PowerPoint")

## Cómo exportar Excel a PowerPoint con C# – Visión general

Antes de comenzar a programar, es útil entender el flujo de tres pasos:

1. **Cargar el libro de Excel** – Leemos el archivo `.xlsx` en memoria.  
2. **Convertir el libro a una presentación de PowerPoint** – Aspose convierte cada hoja (o gráfico seleccionado) en una diapositiva.  
3. **Guardar la presentación generada** – El PPTX final puede abrirse en PowerPoint, editarse o enviarse a los interesados.

Cada paso está aislado deliberadamente para que puedas sustituir lógica personalizada más adelante (p. ej., elegir hojas específicas, aplicar temas de diapositiva, etc.). Ahora desglosémoslo.

## Paso 1 – Cargar el libro de Excel al estilo C#

Lo primero que debes hacer es llevar el archivo Excel a tu aplicación. Con Aspose.Cells el código es directo:

```csharp
using Aspose.Cells;   // Handles Excel files
using Aspose.Slides;  // Handles PowerPoint files
using System;

// Step 1: Load the Excel workbook
string excelPath = @"YOUR_DIRECTORY\chartOle.xlsx";

if (!System.IO.File.Exists(excelPath))
{
    throw new FileNotFoundException($"Excel file not found at {excelPath}");
}

// The Workbook class reads the .xlsx file into memory
Workbook workbook = new Workbook(excelPath);
```

**Por qué es importante:**  
`Workbook` abstrae toda la hoja de cálculo, dándote acceso a hojas, celdas y—crucialmente—gráficos incrustados. Si omites la verificación de existencia, obtendrás una vaga `FileNotFoundException` más adelante, lo que puede ser una pesadilla de depurar en producción.

**Consejo profesional:** Si solo necesitas una hoja específica, puedes pasar un objeto `LoadOptions` para limitar el uso de memoria:

```csharp
LoadOptions options = new LoadOptions(LoadFormat.Xlsx) { LoadDataOnly = true };
Workbook workbook = new Workbook(excelPath, options);
```

Ese pequeño ajuste acelera dramáticamente los libros grandes.

## Paso 2 – Convertir Excel a PowerPoint (Exportar gráfico de Excel a PowerPoint)

Ahora llega la magia: transformar el libro en un PPTX. Aspose.Slides ofrece un único método que hace el trabajo pesado:

```csharp
// Step 2: Convert the workbook to a PowerPoint presentation (PPTX format)
Presentation presentation = workbook.SaveToPresentation(ExportToPresentationFormat.Pptx);
```

**¿Qué ocurre bajo el capó?**  
`SaveToPresentation` recorre cada hoja, extrae los objetos de gráfico y crea una diapositiva por gráfico. El método respeta el estilo original del gráfico, por lo que colores, fuentes y etiquetas de datos permanecen intactos. Si tu libro contiene tablas simples, se renderizarán como cuadros de texto en la diapositiva.

**Caso límite – varios gráficos:**  
Si una hoja tiene más de un gráfico, Aspose los apila verticalmente en la misma diapositiva. Para mantenerlos en diapositivas separadas puedes iterar los gráficos manualmente:

```csharp
Presentation presentation = new Presentation();

foreach (Worksheet sheet in workbook.Worksheets)
{
    foreach (Chart chart in sheet.Charts)
    {
        // Export each chart as an individual slide
        ISlide slide = presentation.Slides.AddEmptySlide(presentation.SlideSize.Size);
        chart.ExportToSlide(presentation, slide);
    }
}
```

Ese fragmento te brinda control granular—perfecto para una presentación pulida.

## Paso 3 – Guardar la presentación generada (Crear PowerPoint desde Excel)

El paso final es persistir el archivo PPTX en disco. Es tan simple como:

```csharp
// Step 3: Save the generated presentation to a file
string pptxPath = @"YOUR_DIRECTORY\editable.pptx";
presentation.Save(pptxPath, Aspose.Slides.Export.SaveFormat.Pptx);

Console.WriteLine($"Presentation saved successfully to {pptxPath}");
```

**Por qué debes verificar la salida:**  
Después de guardar, abre `editable.pptx` en PowerPoint. Deberías ver una diapositiva por gráfico, cada una totalmente editable (puedes cambiar colores, mover objetos, etc.). Si algún gráfico se ve extraño, verifica que el gráfico original de Excel use fuentes estándar—algunas fuentes personalizadas pueden no incrustarse correctamente.

**Trampa común:**  
Guardar en un recurso de red sin los permisos adecuados lanza una `UnauthorizedAccessException`. Asegúrate de que la cuenta en ejecución tenga permiso de escritura en `YOUR_DIRECTORY`.

## Ejemplo completo y funcional – Todos los pasos juntos

A continuación tienes el programa completo, listo para ejecutar. Pégalo en un nuevo proyecto de Console App, restaura los paquetes NuGet y pulsa **F5**.

```csharp
using System;
using Aspose.Cells;
using Aspose.Slides;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main()
        {
            // Paths – adjust to your environment
            string excelPath = @"YOUR_DIRECTORY\chartOle.xlsx";
            string pptxPath = @"YOUR_DIRECTORY\editable.pptx";

            // -------------------------------------------------
            // Step 1: Load the Excel workbook (load excel workbook c#)
            // -------------------------------------------------
            if (!System.IO.File.Exists(excelPath))
            {
                Console.WriteLine($"Error: File not found -> {excelPath}");
                return;
            }

            Workbook workbook = new Workbook(excelPath);
            Console.WriteLine("Excel workbook loaded successfully.");

            // -------------------------------------------------
            // Step 2: Convert Excel to PowerPoint (export excel chart powerpoint)
            // -------------------------------------------------
            Presentation presentation = workbook.SaveToPresentation(ExportToPresentationFormat.Pptx);
            Console.WriteLine("Workbook converted to PowerPoint.");

            // -------------------------------------------------
            // Step 3: Save the generated presentation (create powerpoint from excel)
            // -------------------------------------------------
            presentation.Save(pptxPath, Aspose.Slides.Export.SaveFormat.Pptx);
            Console.WriteLine($"Presentation saved at: {pptxPath}");
        }
    }
}
```

**Salida esperada (consola):**

```
Excel workbook loaded successfully.
Workbook converted to PowerPoint.
Presentation saved at: YOUR_DIRECTORY\editable.pptx
```

Abre `editable.pptx` y verás una diapositiva para cada gráfico, lista para ajustes adicionales.

## Preguntas frecuentes (FAQs)

**P: ¿Puedo exportar solo una hoja en lugar de todo el libro?**  
R: Sí. Usa `Workbook.Worksheets["Sheet1"]` para aislar una hoja y luego llama a `SaveToPresentation` solo sobre esa hoja.

**P: ¿Qué pasa con la preservación de macros?**  
R: Las macros no se transfieren a PowerPoint—solo se exportan los objetos visuales (gráficos, tablas). Si necesitas funcionalidad de macro, considera generar primero las diapositivas y luego añadir VBA manualmente.

**P: ¿Funciona con archivos `.xls`?**  
R: Absolutamente. Aspose.Cells soporta formatos heredados; solo cambia la extensión del archivo en `excelPath`.

**P: ¿Cómo cambio el tamaño de la diapositiva a pantalla ancha (16:9)?**  
R: Después de crear el objeto `Presentation`, establece:

```csharp
presentation.SlideSize.Size = SlideSizeType.Widescreen;
```

**P: ¿Existe una alternativa gratuita?**  
R: Bibliotecas de código abierto como EPPlus pueden leer Excel, pero no ofrecen conversión directa de Excel a PowerPoint. Tendrías que renderizar los gráficos a imágenes e insertarlos manualmente, lo que implica mucho más código.

## Consejos y buenas prácticas

- **Procesamiento por lotes:** Si tienes docenas de libros, envuelve la conversión en un bucle `Parallel.ForEach`—solo ten cuidado con los objetos de Aspose que no son seguros para subprocesos.  
- **Gestión de memoria:** Llama a `presentation.Dispose()` y `workbook.Dispose()` al trabajar con archivos grandes para liberar recursos nativos rápidamente.  
- **Estilizar diapositivas:** Después de la conversión, puedes aplicar un tema maestro usando `presentation.SlideMaster` para dar a todas las diapositivas un aspecto coherente.  
- **Pruebas:** Automatiza una prueba unitaria sencilla que cargue un libro conocido, ejecute la conversión y verifique que el PPTX resultante contenga el número esperado de diapositivas.

## Conclusión

Acabamos de mostrar **cómo exportar datos de Excel** a una presentación de PowerPoint usando C#. Al cargar el libro, convertirlo con Aspose y guardar el PPTX, ahora dispones de un método repetible y programático para **convertir Excel a PowerPoint**, **crear PowerPoint desde Excel** y **cargar libro de Excel en C#** sin esfuerzo manual. El código es autónomo, funciona con cualquier runtime .NET moderno y puede ampliarse para adaptarse a flujos de informes complejos.

¿Listo para el siguiente reto? Prueba incrustar varios gráficos por diapositiva, aplicar diseños de diapositiva personalizados o incluso generar notas del presentador automáticamente. El cielo es el límite cuando combinas la automatización de Excel con la generación de PowerPoint.

¿Tienes preguntas o un caso de uso interesante? Deja un comentario abajo, ¡y feliz codificación!

## ¿Qué deberías aprender a continuación?

Los tutoriales siguientes cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos con explicaciones paso a paso para ayudarte a dominar funciones adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [How to Convert Excel to PowerPoint Using Aspose.Cells for .NET&#58; A Complete Guide](/cells/english/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)
- [How to Export Excel Charts to PDF Using Aspose.Cells for .NET&#58; A Step-by-Step Guide](/cells/english/net/workbook-operations/export-excel-charts-pdf-aspose-cells-net/)
- [How to Export Excel to HTML with Grid Lines Using Aspose.Cells for .NET](/cells/english/net/workbook-operations/export-excel-to-html-grid-lines-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}