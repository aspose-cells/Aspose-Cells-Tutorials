---
category: general
date: 2026-11-19
description: Cómo exportar un gráfico de Excel como una imagen PNG usando Aspose.Cells.
  Aprende a guardar la imagen del gráfico de Excel y establecer el formato de imagen
  PNG en solo unos pocos pasos.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to export excel chart
- save excel chart image
- set image format png
- save excel picture file
language: es
lastmod: 2026-11-19
og_description: Cómo exportar un gráfico de Excel como una imagen PNG con Aspose.Cells.
  Sigue esta guía paso a paso para guardar la imagen del gráfico de Excel y establecer
  el formato de imagen PNG de manera eficiente.
og_image_alt: How to export Excel chart as a PNG image
og_title: Cómo exportar un gráfico de Excel como imagen PNG – guía rápida de C#
schemas:
- author: Aspose
  dateModified: '2026-11-19'
  description: How to export Excel chart as a PNG image using Aspose.Cells. Learn
    to save Excel chart image and set image format PNG in just a few steps.
  headline: How to export Excel chart as a PNG image with C#
  type: TechArticle
tags:
- Excel
- C#
- Aspose.Cells
- Chart export
title: Cómo exportar un gráfico de Excel como imagen PNG con C#
url: /es/net/chart-rendering-and-conversion/how-to-export-excel-chart-as-a-png-image-with-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo exportar un gráfico de Excel como imagen PNG con C#

Si necesitas **cómo exportar un gráfico de Excel** a una imagen portátil, esta guía muestra una solución completa y lista para ejecutar. Usando Aspose.Cells puedes **guardar la imagen del gráfico de Excel** en formato PNG con solo tres líneas de código, y el tutorial también explica cómo **establecer el formato de imagen png** y **guardar el archivo de imagen de Excel** de forma segura.

Terminarás este artículo con un programa ejecutable que carga un libro, renderiza el primer gráfico y escribe un archivo `pivot.png` en disco. Sin herramientas adicionales, sin copiar‑pegar manual—solo código C# limpio que puedes incorporar a cualquier proyecto .NET.

## Requisitos previos

Antes de comenzar, asegúrate de tener:

* .NET 6.0 SDK o posterior (el código también funciona con .NET Framework 4.6+)
* Visual Studio 2022 o cualquier editor de C#
* Una licencia de Aspose.Cells for .NET (o una clave de evaluación temporal)
* Un archivo de Excel (`pivot.xlsx`) que contenga al menos un gráfico en la primera hoja de cálculo

Estos elementos son las únicas dependencias externas; el tutorial no requiere que Office esté instalado en la máquina.

## Paso 1: Instalar Aspose.Cells

Abre una terminal en la carpeta de tu proyecto y ejecuta:

```bash
dotnet add package Aspose.Cells
```

El paquete agrega el espacio de nombres `Aspose.Cells`, que proporciona las clases `Workbook`, `ImageOrPrintOptions` y otras necesarias para **guardar la imagen del gráfico de Excel**.

## Paso 2: Crear un programa de consola mínimo

Crea una nueva aplicación de consola (`dotnet new console -n ExportChartDemo`) y reemplaza el `Program.cs` autogenerado con el siguiente código. El programa demuestra **cómo exportar un gráfico de Excel** e incluye comentarios que explican cada decisión.

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Rendering;   // Required for ImageOrPrintOptions
using System.Drawing.Imaging;  // Provides ImageFormat enum

namespace ExportChartDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -----------------------------------------------------------------
            // 1️⃣ Load the workbook that contains the pivot chart
            // -----------------------------------------------------------------
            // Replace the path with the actual location of your Excel file.
            string workbookPath = @"YOUR_DIRECTORY\pivot.xlsx";
            Workbook workbook = new Workbook(workbookPath);

            // -----------------------------------------------------------------
            // 2️⃣ Set up image export options (PNG format)
            // -----------------------------------------------------------------
            // This is where we **set image format png** for the exported picture.
            ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
            {
                ImageFormat = ImageFormat.Png,
                // Optional: control the resolution (DPI) of the output image.
                // Higher DPI yields larger files but sharper charts.
                HorizontalResolution = 300,
                VerticalResolution = 300
            };

            // -----------------------------------------------------------------
            // 3️⃣ Render the first picture (the chart) on the first worksheet
            // -----------------------------------------------------------------
            // Aspose.Cells stores charts as Picture objects inside the worksheet.
            // The index [0] refers to the first chart; adjust if you have multiple.
            Worksheet sheet = workbook.Worksheets[0];
            if (sheet.Pictures.Count == 0)
            {
                Console.WriteLine("No pictures found on the first worksheet.");
                return;
            }

            // Render the picture to a PNG file.
            string outputPath = @"YOUR_DIRECTORY\pivot.png";
            sheet.Pictures[0].RenderToImage(imageOptions, outputPath);

            Console.WriteLine($"Chart exported successfully to: {outputPath}");
        }
    }
}
```

### Por qué cada parte es importante

* **Cargar el libro** – `Workbook` analiza el archivo `.xlsx` sin necesidad de tener Microsoft Excel instalado.
* **ImageOrPrintOptions** – Este objeto controla el formato de salida. Establecer `ImageFormat = ImageFormat.Png` **establece el formato de imagen png**, que es sin pérdida y ampliamente compatible.
* **RenderToImage** – El método `RenderToImage` convierte el gráfico (un objeto `Picture`) en un archivo de imagen. El método también gestiona el escalado, DPI y transparencia automáticamente.
* **Manejo de errores** – La comprobación `sheet.Pictures.Count == 0` evita una excepción en tiempo de ejecución si la hoja no tiene gráficos, un caso límite frecuente cuando los usuarios apuntan a la hoja equivocada.

## Paso 3: Ejecutar el programa y verificar el resultado

1. Compila el proyecto: `dotnet build`.
2. Ejecútalo: `dotnet run --project ExportChartDemo`.

Si todo está configurado correctamente, verás:

```
Chart exported successfully to: YOUR_DIRECTORY\pivot.png
```

Abre `pivot.png` con cualquier visor de imágenes. Deberías ver la representación visual exacta del gráfico de Excel, confirmando que has **guardado el archivo de imagen de Excel** con éxito.

### Salida esperada

A continuación se muestra una muestra de cómo podría verse el PNG exportado (el gráfico real depende de tu archivo fuente).

![Exported Excel chart saved as PNG image](images/exported-chart.png){: .center alt="Cómo exportar un gráfico de Excel como imagen PNG"}

## Paso 4: Opciones avanzadas – exportar varios gráficos

Si tu libro contiene más de un gráfico, puedes iterar sobre la colección `Pictures`:

```csharp
for (int i = 0; i < sheet.Pictures.Count; i++)
{
    string chartPath = $@"YOUR_DIRECTORY\chart_{i + 1}.png";
    sheet.Pictures[i].RenderToImage(imageOptions, chartPath);
    Console.WriteLine($"Chart {i + 1} saved to {chartPath}");
}
```

Este patrón te permite **guardar la imagen del gráfico de Excel** para cada gráfico en la hoja, lo cual es útil para pipelines de informes.

## Problemas comunes y cómo evitarlos

| Síntoma | Causa probable | Solución |
|---------|----------------|----------|
| `ArgumentOutOfRangeException` en `Pictures[0]` | La hoja no tiene gráfico o el gráfico está en otra hoja. | Verifica el índice de la hoja (`Worksheets[0]`) y asegura que el gráfico exista. Usa `Worksheets["SheetName"]` si es necesario. |
| La imagen exportada está borrosa | DPI configurado demasiado bajo (predeterminado 96). | Incrementa `HorizontalResolution` y `VerticalResolution` en `ImageOrPrintOptions`. |
| El archivo PNG está vacío o corrupto | Falta de licencia que causa restricciones de evaluación. | Aplica una licencia válida de Aspose.Cells antes de cargar el libro (`License license = new License(); license.SetLicense("Aspose.Total.lic");`). |
| Errores de ruta de archivo (`FileNotFoundException`) | Marcador de posición `YOUR_DIRECTORY` incorrecto. | Usa rutas absolutas o `Path.Combine(Environment.CurrentDirectory, "pivot.xlsx")`. |

Abordar estos problemas garantiza una experiencia fluida al **guardar el archivo de imagen de Excel**.

## Consejo profesional: Exportar directamente a un flujo de memoria

A veces necesitas la imagen en memoria (p. ej., para subirla a una API web) en lugar de escribirla en disco:

```csharp
using (var ms = new MemoryStream())
{
    sheet.Pictures[0].RenderToImage(imageOptions, ms);
    // ms now contains the PNG bytes – you can send them over HTTP, store in DB, etc.
}
```

La misma lógica de **establecer el formato de imagen png** se aplica; solo reemplazas la ruta del archivo por un stream.

## Conclusión

Ahora sabes **cómo exportar un gráfico de Excel** como archivo PNG usando Aspose.Cells para .NET. El tutorial cubrió:

* Instalación de la biblioteca
* Carga de un libro
* **Establecer el formato de imagen png**
* **Guardar la imagen del gráfico de Excel** en disco
* Manejo de varios gráficos y errores comunes

Con esta base puedes integrar la exportación de gráficos en informes automatizados, servicios web o utilidades de escritorio. A continuación, explora temas relacionados como **guardar el archivo de imagen de Excel** como JPEG (`ImageFormat.Jpeg`) o convertir gráficos a PDF para informes imprimibles.

¡Feliz codificación!

## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos con explicaciones paso a paso para ayudarte a dominar funciones adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Convertir gráfico de pastel de Excel a imagen usando Aspose.Cells .NET: Guía paso a paso](/cells/english/net/charts-graphs/convert-excel-pie-chart-image-aspose-cells-net/)
- [Exportar gráfico como PNG – Guía completa para convertir Excel a HTML con Aspose.Cells](/cells/english/net/chart-rendering-and-conversion/export-chart-as-png-complete-guide-to-convert-excel-to-html/)
- [Exportar celdas de Excel a imagen usando Aspose.Cells .NET: Guía paso a paso](/cells/english/net/import-export/export-excel-cells-to-image-aspose-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}