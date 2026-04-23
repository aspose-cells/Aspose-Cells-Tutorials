---
category: general
date: 2026-02-09
description: Crear rango de referencia de tabla dinámica en C# y exportar la imagen
  de la tabla dinámica. Aprende cómo guardar un rango de Excel como PNG usando Aspose.Cells
  – guía rápida y completa.
draft: false
keywords:
- create pivot reference range
- export pivot table image
- save excel range as png
- Aspose.Cells C#
- Excel automation C#
language: es
og_description: Crear rango de referencia de tabla dinámica en C# y exportar la imagen
  de la tabla dinámica a PNG. Guía completa paso a paso para guardar un rango de Excel
  como PNG.
og_title: Crear rango de referencia de tabla dinámica – Exportar imagen de tabla dinámica
  como PNG
tags:
- Aspose.Cells
- C#
- Excel
title: Crear rango de referencia de tabla dinámica – Exportar imagen de tabla dinámica
  como PNG
url: /es/net/rendering-and-export/create-pivot-reference-range-export-pivot-table-image-as-png/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crear rango de referencia de tabla dinámica – Exportar imagen de tabla dinámica como PNG

¿Necesitas **crear rango de referencia de tabla dinámica** en un libro de Excel usando C#? También puedes **exportar imagen de tabla dinámica** y **guardar rango de Excel como png** con solo unas pocas líneas de código. En mi experiencia, convertir una tabla dinámica activa en una imagen estática es una forma práctica de incrustar análisis en informes, correos electrónicos o paneles sin tener que incluir todo el libro.

En este tutorial repasaremos todo lo que necesitas saber: las bibliotecas requeridas, el código exacto, por qué cada llamada es importante y algunos inconvenientes que podrías encontrar. Al final podrás generar un archivo PNG de cualquier tabla dinámica con confianza, y entenderás cómo adaptar el patrón para múltiples hojas de cálculo o formatos de imagen personalizados.

## Prerrequisitos

Antes de comenzar, asegúrate de tener:

- **Aspose.Cells for .NET** (la versión de prueba gratuita funciona bien para pruebas).  
- **.NET 6.0** o posterior – la API que usamos es totalmente compatible con .NET Standard 2.0+, por lo que los frameworks más antiguos también compilarán.  
- Un proyecto básico en C# (Aplicación de consola, WinForms o ASP.NET – cualquier cosa que pueda referenciar un paquete NuGet).  

Si aún no has instalado Aspose.Cells, ejecuta:

```bash
dotnet add package Aspose.Cells
```

¡Eso es todo – sin interop COM, sin Excel instalado en el servidor!

## Paso 1: Abrir el libro y acceder a la primera hoja de cálculo

Lo primero que haces es cargar el archivo del libro y obtener la hoja que contiene la tabla dinámica. Elegimos deliberadamente la **primera hoja** (`Worksheets[0]`) porque la mayoría de los archivos de demostración colocan la tabla dinámica allí, pero puedes reemplazar el índice por un nombre si lo prefieres.

```csharp
using Aspose.Cells;
using System;

// Load an existing Excel file (replace with your own path)
Workbook wb = new Workbook("YOUR_DIRECTORY/source.xlsx");

// Access the first worksheet – this is where our pivot lives
Worksheet worksheet = wb.Worksheets[0];
```

*¿Por qué es importante esto?* `Worksheet` es el punto de entrada para cualquier operación basada en rangos. Si apuntas a la hoja equivocada, la llamada subsecuente a `PivotTables[0]` lanzará una `IndexOutOfRangeException`.

## Paso 2: Crear rango de referencia de tabla dinámica

Ahora le pedimos a la propia tabla dinámica que nos devuelva un **rango de referencia**. Este rango representa las celdas exactas que forman la tabla dinámica – encabezados, filas de datos y totales. El método `CreateReferenceRange()` realiza el trabajo pesado internamente, manejando celdas combinadas y filas ocultas por ti.

```csharp
// Grab the first pivot table on the worksheet
PivotTable pivot = worksheet.PivotTables[0];

// Build a reference range that covers the whole pivot
Range pivotReferenceRange = pivot.CreateReferenceRange();
```

> **Consejo profesional:** Si tu libro contiene varias tablas dinámicas, recorre `worksheet.PivotTables` y elige la que necesites mediante su propiedad `Name`.

## Paso 3: Renderizar el rango de referencia como una imagen

Aspose.Cells puede renderizar cualquier `Range` a una imagen. El objeto devuelto implementa tanto formatos raster (PNG, JPEG) como vector (SVG). Aquí solicitamos la imagen raster predeterminada, que es un objeto compatible con `System.Drawing.Image`.

```csharp
// Convert the pivot reference range into an image object
ImageOrVector pivotImage = pivotReferenceRange.ToImage();
```

*¿Qué está ocurriendo detrás de escena?* La API captura instantáneamente el diseño visual del rango, respetando estilos de celda, fuentes y formato condicional. Es esencialmente lo mismo que tomar una captura de pantalla, pero de forma programática y sin una interfaz de usuario.

## Paso 4: Guardar la imagen generada en un archivo

Finalmente, persistimos la imagen. El método `Save` elige automáticamente PNG cuando le das una extensión “.png”. También puedes pasar un objeto `SaveOptions` si necesitas controlar DPI o usar otro formato.

```csharp
// Save the image as PNG – the extension drives the format
pivotImage.Save("YOUR_DIRECTORY/pivot.png");
```

Después de ejecutar esta línea, abre `pivot.png` y verás una captura pixel‑perfecta de la tabla dinámica, lista para incrustarse donde sea necesario.

## Ejemplo completo funcional

Juntándolo todo, aquí tienes un programa de consola autocontenido que puedes copiar‑pegar y ejecutar:

```csharp
using Aspose.Cells;
using System;

namespace PivotExportDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load workbook
            Workbook wb = new Workbook("YOUR_DIRECTORY/source.xlsx");

            // 2️⃣ Access first worksheet
            Worksheet worksheet = wb.Worksheets[0];

            // 3️⃣ Get first pivot table
            if (worksheet.PivotTables.Count == 0)
            {
                Console.WriteLine("No pivot tables found on the first sheet.");
                return;
            }
            PivotTable pivot = worksheet.PivotTables[0];

            // 4️⃣ Create a reference range that covers the whole pivot
            Range pivotReferenceRange = pivot.CreateReferenceRange();

            // 5️⃣ Render the range to an image
            ImageOrVector pivotImage = pivotReferenceRange.ToImage();

            // 6️⃣ Save as PNG
            string outputPath = "YOUR_DIRECTORY/pivot.png";
            pivotImage.Save(outputPath);

            Console.WriteLine($"Pivot table image saved to {outputPath}");
        }
    }
}
```

**Salida esperada:** un archivo llamado `pivot.png` ubicado en `YOUR_DIRECTORY`. Ábrelo con cualquier visor de imágenes – deberías ver el diseño exacto de la tabla dinámica original, incluidos los encabezados de columna, filas de datos y totales generales.

## Exportar imagen de tabla dinámica – Personalizar tamaño y DPI

A veces la imagen predeterminada es demasiado pequeña para una diapositiva de presentación. Puedes controlar la resolución pasando un objeto `ImageOrVectorSaveOptions`:

```csharp
using Aspose.Cells.Drawing;

// Define PNG options – 300 DPI for high‑quality print
ImageOrVectorSaveOptions options = new ImageOrVectorSaveOptions
{
    ImageFormat = ImageFormat.Png,
    Resolution = 300 // DPI
};

pivotImage.Save("YOUR_DIRECTORY/pivot_highres.png", options);
```

*¿Por qué ajustar el DPI?* Un DPI más alto produce bordes más nítidos, especialmente cuando el PNG se escala en PowerPoint o un PDF.

## Guardar rango de Excel como PNG – Manejo de múltiples hojas de cálculo

Si necesitas exportar tablas dinámicas de varias hojas, recorre `Workbook.Worksheets` y repite los pasos. Aquí tienes un fragmento conciso:

```csharp
foreach (Worksheet ws in wb.Worksheets)
{
    foreach (PivotTable pt in ws.PivotTables)
    {
        Range refRange = pt.CreateReferenceRange();
        ImageOrVector img = refRange.ToImage();
        string fileName = $"pivot_{ws.Name}_{pt.Name}.png";
        img.Save($"YOUR_DIRECTORY/{fileName}");
        Console.WriteLine($"Saved {fileName}");
    }
}
```

Este patrón **exporta imagen de tabla dinámica** para cada tabla dinámica del libro, y cada archivo lleva el nombre de su hoja y tabla dinámica – perfecto para procesamiento por lotes.

## Problemas comunes y cómo evitarlos

| Problema | Por qué ocurre | Solución |
|----------|----------------|----------|
| `IndexOutOfRangeException` en `PivotTables[0]` | La hoja no tiene tablas dinámicas. | Verifica `worksheet.PivotTables.Count` antes de acceder. |
| Imagen en blanco | La tabla dinámica está filtrada para ocultar todas las filas. | Asegúrate de que la tabla dinámica tenga datos visibles, o llama a `pivot.RefreshData();` antes de crear el rango. |
| PNG de baja resolución | El DPI predeterminado es 96. | Usa `ImageOrVectorSaveOptions.Resolution` como se muestra arriba. |
| Errores de ruta de archivo | Caracteres no válidos en `YOUR_DIRECTORY`. | Usa `Path.Combine` y `Path.GetInvalidPathChars()` para sanitizar. |

## Verificación – Prueba rápida

Después de ejecutar el ejemplo completo:

1. Abre `pivot.png` en el Visor de fotos de Windows.  
2. Verifica que los encabezados de columna, filas de datos y filas totales coincidan con la vista de Excel.  
3. Si notas filas faltantes, verifica que se haya llamado al método **RefreshData** de la tabla dinámica antes de `CreateReferenceRange()`.

## Bonus: Incrustar el PNG en un documento Word

Como la imagen ya es un PNG, puedes enviarla directamente a Aspose.Words:

```csharp
using Aspose.Words;
Document doc = new Document();
DocumentBuilder builder = new DocumentBuilder(doc);
builder.InsertImage("YOUR_DIRECTORY/pivot.png");
doc.Save("YOUR_DIRECTORY/report.docx");
```

Ahora tienes un informe Word que contiene la captura exacta de tu tabla dinámica – sin necesidad de copiar‑pegar manualmente.

## Conclusión

Acabas de aprender cómo **crear rango de referencia de tabla dinámica**, **exportar imagen de tabla dinámica** y **guardar rango de Excel como png** usando Aspose.Cells en C#. Los puntos clave son:

- Usa `PivotTable.CreateReferenceRange()` para aislar el área visual de una tabla dinámica.  
- Convierte ese rango a una imagen con `Range.ToImage()`.  
- Persiste la imagen como PNG, ajustando opcionalmente el DPI para calidad de impresión.  

Desde aquí puedes explorar exportación por lotes, diferentes formatos de imagen (SVG, JPEG) o incluso incrustar el PNG en PDFs o documentos Word. El cielo es el límite una vez que tienes la tabla dinámica capturada como un gráfico estático.

¿Tienes preguntas o un escenario complicado? Deja un comentario abajo, ¡y feliz codificación!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}