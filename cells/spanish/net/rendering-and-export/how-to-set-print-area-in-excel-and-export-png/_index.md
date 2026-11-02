---
category: general
date: 2026-09-27
description: Establecer el área de impresión en Excel y aprender cómo exportar imágenes
  PNG de celdas seleccionadas. Esta guía también cubre cómo guardar un rango como
  imagen y añadir una imagen a la hoja de cálculo.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- set print area excel
- how to export png
- save range as image
- add picture to worksheet
- export selected cells image
language: es
lastmod: 2026-09-27
og_description: Establece el área de impresión en Excel y exporta PNG con Aspose.Cells.
  Sigue esta guía paso a paso para guardar el rango como imagen y añadirla a la hoja
  de cálculo.
og_image_alt: Screenshot showing set print area excel and exported PNG file
og_title: Establecer el área de impresión en Excel – exportar PNG en C#
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Set print area in Excel and learn how to export PNG images of selected
    cells. This guide also covers saving range as image and adding picture to worksheet.
  headline: How to set print area in Excel and export PNG
  type: TechArticle
tags:
- Excel automation
- C#
- Aspose.Cells
title: Cómo establecer el área de impresión en Excel y exportar a PNG
url: /es/net/rendering-and-export/how-to-set-print-area-in-excel-and-export-png/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo establecer el área de impresión en Excel y exportar PNG

Si necesitas **establecer el área de impresión en Excel** antes de crear una imagen, esta guía te muestra exactamente cómo hacerlo. También aprenderás **cómo exportar PNG** desde un rango específico, **guardar rango como imagen**, y **agregar imagen a la hoja de cálculo** en un flujo de trabajo único y repetible.

Trabajar con Excel de forma programática a menudo significa que solo deseas un subconjunto de celdas —por ejemplo, una tabla dinámica o un gráfico— para convertirlo en una imagen. Al definir primero un área de impresión, garantizas que el PNG exportado contenga exactamente las celdas que esperas, ni más ni menos. Este tutorial te lleva paso a paso, desde cargar el libro de trabajo hasta guardar el archivo PNG final, y explica por qué cada configuración es importante.

## Requisitos previos

Antes de comenzar, asegúrate de tener:

* .NET 6.0 o posterior instalado  
* Visual Studio 2022 (o cualquier IDE de C#)  
* El paquete NuGet **Aspose.Cells for .NET** (`Install-Package Aspose.Cells`)  
* Un archivo Excel (`input.xlsx`) ubicado en un directorio conocido  

Estos requisitos garantizan que el código se ejecute sin configuraciones adicionales.

## Paso 1: Cargar el libro de trabajo con el que deseas trabajar

```csharp
using Aspose.Cells;
using System.Drawing.Imaging;

// Load the workbook from disk
Workbook workbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");
```

La clase `Workbook` representa todo el archivo Excel. Cargarlo primero te da acceso a hojas, celdas y opciones de configuración de página.

## Paso 2: **Establecer el área de impresión en Excel** para el rango objetivo

```csharp
// Define the range you want to capture
string printArea = "A1:G20";

// Apply the range as the print area on the first worksheet
workbook.Worksheets[0].PageSetup.PrintArea = printArea;
```

Definir el **área de impresión** indica a Excel (y a Aspose.Cells) qué celdas pertenecen a la página imprimible. Cuando luego exportes la hoja como imagen, solo se renderizará esta zona, lo cual es esencial para una **exportación de celdas seleccionadas como imagen** limpia.

## Paso 3: Configurar las opciones de exportación de imagen — **cómo exportar PNG**

```csharp
ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
{
    ImageFormat = ImageFormat.Png,   // PNG ensures lossless quality
    OnePagePerSheet = true           // Export the defined print area as a single page
};
```

`ImageOrPrintOptions` controla el formato de salida. Al elegir `ImageFormat.Png`, garantizas una imagen de alta resolución y con fondo transparente que funciona bien en contextos web y de escritorio.

## Paso 4: Crear una imagen a partir del rango definido y **agregar imagen a la hoja de cálculo**

```csharp
// Create a picture object from the selected range
Picture picture = workbook.Worksheets[0].Pictures.Add(
    0,                                     // top‑left row index where the picture will be placed
    0,                                     // top‑left column index where the picture will be placed
    workbook.Worksheets[0].Cells.CreateRange(printArea));
```

El método `Pictures.Add` inserta una nueva imagen en la hoja. Al pasar el rango creado en el Paso 2, **guardas el rango como imagen** directamente en la hoja, lo cual es útil si luego necesitas referenciar la imagen en otras partes del libro.

## Paso 5: **Guardar la imagen como archivo** — completando el flujo de trabajo de **exportar celdas seleccionadas como imagen**

```csharp
// Save the picture to disk as a PNG file
picture.Save(@"YOUR_DIRECTORY\selected_range.png", imageOptions);
```

Llamar a `Save` escribe la imagen en el sistema de archivos usando las opciones definidas en el Paso 3. El archivo resultante `selected_range.png` contiene exactamente las celdas definidas por el comando **establecer el área de impresión en Excel**.

## Ejemplo completo y ejecutable

Unir todas las piezas te brinda un programa compacto que puedes colocar en cualquier aplicación de consola:

```csharp
using System;
using Aspose.Cells;
using System.Drawing.Imaging;

class ExportExcelRangeAsPng
{
    static void Main()
    {
        // 1️⃣ Load the workbook
        Workbook workbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");

        // 2️⃣ Set print area excel
        string printArea = "A1:G20";
        workbook.Worksheets[0].PageSetup.PrintArea = printArea;

        // 3️⃣ Configure how to export png
        ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
        {
            ImageFormat = ImageFormat.Png,
            OnePagePerSheet = true
        };

        // 4️⃣ Add picture to worksheet (save range as image)
        Picture picture = workbook.Worksheets[0].Pictures.Add(
            0,
            0,
            workbook.Worksheets[0].Cells.CreateRange(printArea));

        // 5️⃣ Export selected cells image
        picture.Save(@"YOUR_DIRECTORY\selected_range.png", imageOptions);

        Console.WriteLine("PNG exported successfully to YOUR_DIRECTORY\\selected_range.png");
    }
}
```

### Salida esperada

Al ejecutar el programa se muestra:

```
PNG exported successfully to YOUR_DIRECTORY\selected_range.png
```

Y encontrarás un archivo `selected_range.png` que muestra solo las celdas A1 a G20 de `input.xlsx`.

## Problemas comunes y cómo evitarlos

| Problema | Por qué ocurre | Solución |
|----------|----------------|----------|
| La imagen exportada contiene toda la hoja | No se definió un área de impresión | Asegúrate de **establecer el área de impresión en Excel** antes de crear la imagen |
| PNG borroso | El DPI predeterminado es bajo | Establece `imageOptions.DpiX` y `imageOptions.DpiY` a un valor mayor (p. ej., 300) |
| Error de archivo no encontrado | Ruta del directorio incorrecta | Usa `Path.Combine` o verifica que la carpeta exista |
| La imagen aparece desplazada | Índices de fila/columna incorrectos | Los dos primeros parámetros de `Pictures.Add` son la celda superior‑izquierda donde se coloca la imagen; mantenlos en `0,0` para una exportación limpia |

## Consejo profesional: Exportar varios rangos en una sola ejecución

Si necesitas **exportar celdas seleccionadas como imagen** para varias áreas, repite los Pasos 2‑5 dentro de un bucle, cambiando `printArea` en cada iteración. Recuerda dar a cada imagen un nombre de archivo único; de lo contrario, la guardada posteriormente sobrescribirá la anterior.

## Conclusión

Ahora sabes cómo **establecer el área de impresión en Excel**, configurar **cómo exportar PNG**, **guardar rango como imagen**, y **agregar imagen a la hoja de cálculo** usando Aspose.Cells. Esta solución de extremo a extremo te permite convertir cualquier bloque de celdas en un PNG de alta calidad con solo unas pocas líneas de código C#.

A continuación, podrías explorar:

* Añadir bordes o marcas de agua al PNG exportado (busca *add picture to worksheet* con estilo)
* Exportar directamente a PDF para informes imprimibles (*export selected cells image* → flujo de trabajo PDF)
* Automatizar el proceso para varios libros de trabajo en un trabajo por lotes

Siéntete libre de experimentar con diferentes rangos, configuraciones de DPI o formatos de imagen para adaptarlos a las necesidades de tu proyecto. ¡Feliz codificación!

## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y explicaciones paso a paso para ayudarte a dominar funciones adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Set Print Area in Excel and Export to PowerPoint – Step‑by‑Step Guide](/cells/english/net/converting-excel-files-to-other-formats/set-print-area-in-excel-and-export-to-powerpoint-step-by-ste/)
- [Export Excel Print Area to HTML with Aspose.Cells Java](/cells/english/java/workbook-operations/export-excel-print-area-html-aspose-cells-java/)
- [How to Set a Print Area in Excel Using Aspose.Cells for .NET](/cells/english/net/headers-footers/set-print-area-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}