---
category: general
date: 2026-02-09
description: Crea PowerPoint a partir de Excel en minutos – aprende cómo convertir
  Excel a PowerPoint y exportar Excel a PPT con un sencillo ejemplo de código en C#.
draft: false
keywords:
- create powerpoint from excel
- convert excel to powerpoint
- export excel to ppt
- generate ppt from excel
- how to convert excel to pptx
language: es
og_description: Crea PowerPoint a partir de Excel rápidamente. Esta guía muestra cómo
  convertir Excel a PowerPoint, exportar Excel a PPT y generar PPT desde Excel usando
  C#.
og_title: Crear PowerPoint desde Excel – Guía completa de programación
tags:
- C#
- Aspose.Cells
- PowerPoint automation
- Office interop
title: Crear PowerPoint desde Excel – Guía paso a paso
url: /es/net/converting-excel-files-to-other-formats/create-powerpoint-from-excel-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crear PowerPoint desde Excel – Guía completa de programación

¿Alguna vez necesitaste **crear PowerPoint desde Excel** pero no estabas seguro de qué API llamar? No estás solo. Muchos desarrolladores se topan con un obstáculo cuando quieren convertir hojas de cálculo en presentaciones sin copiar‑pegar manualmente.  

Buenas noticias: con unas pocas líneas de C# puedes **convertir Excel a PowerPoint**, exportar las formas de la hoja y obtener un archivo PPTX listo para presentar. En este tutorial recorreremos todo el proceso, explicaremos por qué cada paso es importante y te mostraremos cómo manejar los problemas más comunes.

## Lo que aprenderás

- Cómo cargar un libro de Excel que contiene gráficos, imágenes o SmartArt.
- La llamada exacta que **exporta Excel a PPT** usando la biblioteca Aspose.Cells.
- Cómo guardar la presentación generada y verificar el resultado.
- Consejos para manejar libros sin formas, ajustar el tamaño de la diapositiva y solucionar incompatibilidades de versiones.

Sin herramientas externas, sin interop COM, solo código .NET puro que se ejecuta en cualquier entorno donde .NET Core o .NET 5+ sea compatible.

---

## Requisitos previos

Antes de comenzar, asegúrate de tener:

1. **Aspose.Cells for .NET** (la biblioteca que proporciona `SaveToPresentation`). Puedes obtenerla desde NuGet:  

   ```bash
   dotnet add package Aspose.Cells
   ```
2. Un SDK reciente de .NET (se recomienda 6.0 o superior).  
3. Un archivo Excel (`shapes.xlsx`) que contenga al menos una forma, gráfico o imagen que quieras que aparezca en una diapositiva.

Eso es todo: sin instalación de Office, sin complicaciones de licencias para el propósito de esta demo (la evaluación gratuita funciona sin problemas).

---

## Paso 1: Cargar el libro de Excel (Crear PowerPoint desde Excel)

Lo primero que necesitamos es un objeto `Workbook` que apunte al archivo fuente. Este objeto representa todo el documento de Excel, incluidas todas las hojas, gráficos y objetos incrustados.

```csharp
using Aspose.Cells;
using Aspose.Slides;

// Step 1: Load the Excel workbook containing the shapes
Workbook workbook = new Workbook(@"C:\MyProjects\ExcelToPpt\shapes.xlsx");

// Why this matters:
// - `Workbook` abstracts the file format, so you don’t have to worry about .xls vs .xlsx.
// - Loading the file early lets you inspect its contents (e.g., count of worksheets) before conversion.
```

> **Consejo profesional:** Si no estás seguro de que el archivo exista, envuelve el constructor en un `try/catch` y muestra un mensaje de error útil. Así evitas una críptica `FileNotFoundException` más adelante.

---

## Paso 2: Convertir el libro a una presentación PowerPoint (Exportar Excel a PPT)

Aspose.Cells incluye un exportador incorporado que transforma todo el libro —o solo hojas seleccionadas— en una presentación PowerPoint. El método `SaveToPresentation` realiza el trabajo pesado.

```csharp
// Step 2: Convert the workbook to a PowerPoint presentation (PPTX format)
Presentation presentation = workbook.SaveToPresentation(ExportTo.Pptx);

// How it works:
// - Each worksheet becomes a separate slide.
// - Shapes, charts, and images are rasterized and placed on the slide preserving their layout.
// - You can later tweak the `Presentation` object (e.g., add a title slide) before saving.
```

Si solo necesitas **generar ppt desde excel** para un subconjunto de hojas, puedes usar la sobrecarga que acepta una colección `SheetOptions`. Para la mayoría de los escenarios, la conversión predeterminada es suficiente.

---

## Paso 3: Guardar la presentación generada (Cómo convertir Excel a PPTX)

Ahora que tenemos una instancia `Presentation`, guardarla en disco es sencillo. El resultado será un archivo estándar `.pptx` que cualquier versión moderna de PowerPoint podrá abrir.

```csharp
// Step 3: Save the generated presentation to a file
presentation.Save(@"C:\MyProjects\ExcelToPpt\shapes.pptx");

// Verification:
// Open the file in PowerPoint or use Aspose.Slides to programmatically inspect slide count.
```

> **¿Qué pasa si el libro no tiene formas?**  
> El exportador seguirá creando diapositivas, pero estarán vacías. Puedes comprobar `workbook.Worksheets[i].Shapes.Count` antes de la conversión y decidir si omites esa hoja.

---

## Opcional: Ajuste fino de la salida (Exportación avanzada de Excel a PPT)

A veces el tamaño de diapositiva predeterminado (estándar 4:3) no es ideal para presentaciones en pantalla ancha. Puedes ajustar las dimensiones de la diapositiva antes de guardarla:

```csharp
// Set slide size to widescreen (16:9)
presentation.SlideSize.SetSize(SlideSizeType.Widescreen, SlideSizeScaleType.DoNotScale);

// Add a custom title slide (optional)
ISlide titleSlide = presentation.Slides.InsertEmptySlide(0, presentation.LayoutSlides[0]);
titleSlide.Shapes.AddAutoShape(ShapeType.Rectangle, 50, 50, 600, 100)
          .TextFrame.Text = "Quarterly Report – Exported from Excel";
```

Estos ajustes demuestran **cómo convertir Excel a PowerPoint** con un aspecto profesional, no solo un volcado bruto de datos.

---

## Ejemplo completo funcionando (Todos los pasos combinados)

A continuación tienes el programa completo, listo para ejecutar. Copia‑pégalo en una aplicación de consola, ajusta las rutas de archivo y pulsa **F5**.

```csharp
using System;
using Aspose.Cells;
using Aspose.Slides;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the workbook
            string excelPath = @"C:\MyProjects\ExcelToPpt\shapes.xlsx";
            Workbook workbook = new Workbook(excelPath);

            // 2️⃣ Convert to PPTX
            Presentation presentation = workbook.SaveToPresentation(ExportTo.Pptx);

            // Optional: set widescreen layout
            presentation.SlideSize.SetSize(SlideSizeType.Widescreen, SlideSizeScaleType.DoNotScale);

            // Optional: add a title slide
            ISlide titleSlide = presentation.Slides.InsertEmptySlide(0, presentation.LayoutSlides[0]);
            titleSlide.Shapes.AddAutoShape(ShapeType.Rectangle, 50, 50, 600, 100)
                      .TextFrame.Text = "Quarterly Report – Exported from Excel";

            // 3️⃣ Save the PPTX file
            string pptxPath = @"C:\MyProjects\ExcelToPpt\shapes.pptx";
            presentation.Save(pptxPath);

            Console.WriteLine($"✅ Successfully created PowerPoint from Excel! File saved at: {pptxPath}");
        }
    }
}
```

**Resultado esperado:** Abre `shapes.pptx` en PowerPoint. Verás una diapositiva por hoja de cálculo, cada una conservando los gráficos, imágenes y demás formas originales. La diapositiva de título opcional aparece al principio, dando al deck una introducción pulida.

---

## Preguntas frecuentes y casos límite

| Pregunta | Respuesta |
|----------|-----------|
| *¿Qué pasa si solo necesito una hoja única?* | Usa `Workbook.Worksheets[0]` y llama a `SaveToPresentation` sobre esa hoja mediante `SheetOptions`. |
| *¿Puedo conservar las fórmulas de Excel?* | No: las fórmulas se renderizan como valores estáticos en la diapositiva. Si necesitas datos en vivo, considera enlazar el PPTX al archivo Excel posteriormente. |
| *¿Funciona en Linux/macOS?* | Sí. Aspose.Cells es independiente de la plataforma; solo instala el runtime de .NET y listo. |
| *¿Qué ocurre con libros protegidos con contraseña?* | Cárgalos con `LoadOptions` que incluya la contraseña antes de llamar a `SaveToPresentation`. |
| *¿Por qué obtengo diapositivas en blanco?* | Verifica que el libro realmente contenga formas (`Shapes.Count > 0`). Las diapositivas en blanco se crean para hojas vacías. |

---

## Conclusión

Ahora dispones de una solución clara, de extremo a extremo, para **crear PowerPoint desde Excel** usando C#. Al cargar el libro, invocar `SaveToPresentation` y guardar el resultado, puedes **convertir Excel a PowerPoint**, **exportar Excel a PPT** y **generar PPT desde Excel** con solo unas cuantas líneas.  

A partir de aquí podrías explorar:

- Añadir animaciones a las diapositivas generadas con Aspose.Slides.  
- Automatizar todo el flujo (por ejemplo, leer archivos de una carpeta y convertirlos por lotes).  
- Integrar el código en una API ASP.NET Core para que los usuarios suban un archivo Excel y reciban instantáneamente un PPTX.

Pruébalo, ajusta el tamaño de la diapositiva, agrega un título personalizado; hay mucho espacio para que la salida sea realmente tuya. ¿Tienes preguntas o encuentras algún problema? Deja un comentario abajo, ¡y feliz codificación!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}