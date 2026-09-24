---
category: general
date: 2026-03-30
description: Crea PowerPoint a partir de Excel rápidamente usando Aspose.Cells y Aspose.Slides.
  Aprende cómo exportar la hoja de cálculo como imagen y guardar la presentación como
  PPTX en C#.
draft: false
keywords:
- create powerpoint from excel
- convert excel to powerpoint
- export worksheet as image
- save presentation as pptx
- export excel chart as picture
language: es
og_description: Crear PowerPoint a partir de Excel en C# con Aspose. Exportar la hoja
  de cálculo como imagen, mantener las formas editables y guardar el resultado como
  PPTX.
og_title: Crear PowerPoint desde Excel – Tutorial completo de C#
tags:
- Aspose
- C#
- Office Automation
title: Crear PowerPoint desde Excel – Guía paso a paso en C#
url: /es/net/converting-excel-files-to-other-formats/create-powerpoint-from-excel-step-by-step-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crear PowerPoint desde Excel – Tutorial completo en C#

¿Alguna vez necesitaste **crear PowerPoint desde Excel** pero no estabas seguro de qué biblioteca podía mantener tus gráficos editables? No estás solo. En muchos escenarios de informes querrás convertir una hoja de cálculo en una presentación sin perder la capacidad de ajustar los cuadros de texto más tarde. Esta guía te muestra exactamente cómo **convertir Excel a PowerPoint** usando Aspose.Cells y Aspose.Slides, además de cubrir cómo **exportar la hoja de cálculo como imagen** y finalmente **guardar la presentación como PPTX**.

Recorreremos cada línea de código, explicaremos *por qué* cada configuración es importante e incluso discutiremos qué hacer si tu libro de trabajo contiene gráficos complejos que prefieres exportar como una imagen. Al final tendrás una aplicación de consola C# lista para ejecutar que toma `ShapesDemo.xlsx` y genera `Result.pptx`, todo con cuadros de texto editables e imágenes nítidas.

## Lo que necesitarás

- .NET 6.0 o posterior (la API funciona también con .NET Framework, pero .NET 6 es el punto óptimo).  
- Paquetes NuGet **Aspose.Cells** y **Aspose.Slides** (las licencias de prueba gratuitas sirven para pruebas).  
- Familiaridad básica con la sintaxis de C# – si puedes escribir un `Console.WriteLine`, estás listo para continuar.  

Sin interop COM adicional, sin Office instalado en el servidor, y sin copiar‑pegar manual de imágenes. Todo se maneja programáticamente.

---

## Crear PowerPoint desde Excel – Cargar el libro y establecer opciones de exportación

Lo primero que hacemos es abrir el archivo Excel y decirle a Aspose.Cells cómo queremos que se renderice la hoja. El objeto `ImageOrPrintOptions` es donde ocurre la magia: habilitamos `ExportShapes` y `ExportEditableTextBoxes` para que cualquier forma (incluidos los gráficos) se convierta en parte de la diapositiva **y** permanezca editable después de la conversión.

```csharp
using Aspose.Cells;
using Aspose.Slides;

// 1️⃣ Load the Excel workbook
string excelPath = "YOUR_DIRECTORY/ShapesDemo.xlsx";
Workbook workbook = new Workbook(excelPath);
Worksheet worksheet = workbook.Worksheets[0];   // Grab the first sheet

// 2️⃣ Configure image export – keep shapes editable
ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
{
    OnePagePerSheet = true,          // Export the whole sheet as one slide
    ExportShapes = true,             // Include shapes (charts, drawings)
    ExportEditableTextBoxes = true   // Make text boxes editable in PPTX
};
```

**¿Por qué estas banderas?**  
- `OnePagePerSheet` evita que la hoja se divida en varias diapositivas; obtienes una única imagen a tamaño completo.  
- `ExportShapes` indica a Aspose.Cells que rasterice los gráficos *y* las formas vectoriales, preservando su apariencia.  
- `ExportEditableTextBoxes` es la clave secreta que te permite hacer doble clic en un cuadro de texto en PowerPoint y editar el texto sin volver a abrir Excel.

> **Consejo profesional:** Si solo necesitas una imagen estática de un gráfico, establece `ExportShapes = false` y usa el método `ExportExcelChartAsPicture` más adelante (ver la sección final).

---

## Convertir Excel a PowerPoint – Generar imagen desde la hoja de cálculo

Con las opciones listas, ahora convertimos la hoja de cálculo en un `System.Drawing.Image`. El `WorksheetToImageConverter` realiza el trabajo pesado, aplicando la configuración que acabamos de definir.

```csharp
// 3️⃣ Convert the worksheet to an image using the options above
WorksheetToImageConverter converter = new WorksheetToImageConverter(worksheet);
System.Drawing.Image sheetImage = converter.ConvertToImage(0, imageOptions);
```

El argumento `0` indica la primera página (solo tenemos una debido a `OnePagePerSheet`). La `sheetImage` resultante conserva la DPI original, por lo que tu diapositiva no se verá pixelada incluso en pantallas de alta resolución.

---

## Guardar presentación como PPTX – Insertar imagen en una diapositiva

Ahora creamos un nuevo archivo PowerPoint, añadimos una diapositiva y colocamos el mapa de bits en ella. Aspose.Slides trata la imagen como una forma de *marco de imagen*, que puedes redimensionar o mover más tarde como cualquier objeto nativo de PowerPoint.

```csharp
// 4️⃣ Create a new PowerPoint presentation
Presentation presentation = new Presentation();
ISlide slide = presentation.Slides[0];   // The default blank slide

// Add the Excel‑derived image as a picture frame
slide.Shapes.AddPictureFrame(
    ShapeType.Rectangle,                 // Simple rectangle container
    0, 0,                                // Top‑left corner (0,0)
    sheetImage.Width,                    // Width of the picture
    sheetImage.Height,                   // Height of the picture
    sheetImage);                         // The bitmap we generated
```

> **¿Qué pasa si la imagen es más grande que el tamaño de la diapositiva?**  
> PowerPoint recortará automáticamente cualquier cosa que exceda las dimensiones de la diapositiva. Una solución rápida es escalar la imagen antes de insertarla:

```csharp
float scale = Math.Min(presentation.SlideSize.Size.Width / (float)sheetImage.Width,
                       presentation.SlideSize.Size.Height / (float)sheetImage.Height);
int newWidth  = (int)(sheetImage.Width * scale);
int newHeight = (int)(sheetImage.Height * scale);
```

Luego puedes pasar `newWidth` y `newHeight` a `AddPictureFrame`.

---

## Exportar hoja de cálculo como imagen – Guardar el archivo PPTX

Finalmente guardamos la presentación en disco. La bandera `SaveFormat.Pptx` garantiza el formato OpenXML moderno, que funciona en todas las versiones recientes de PowerPoint.

```csharp
// 5️⃣ Save the presentation as a PPTX file
string pptxPath = "YOUR_DIRECTORY/Result.pptx";
presentation.Save(pptxPath, SaveFormat.Pptx);
```

Cuando abras `Result.pptx` verás una única diapositiva que se ve exactamente como tu hoja de Excel, pero aún podrás hacer clic en cualquier cuadro de texto y editar su contenido directamente en PowerPoint.

---

## Exportar gráfico de Excel como imagen – Cuando se prefieren imágenes rasterizadas

A veces no necesitas formas editables; un PNG de alta calidad de un gráfico es suficiente. Aspose.Cells puede exportar un gráfico específico a una imagen sin convertir toda la hoja:

```csharp
// Example: Export the first chart on the sheet as a PNG
int chartIndex = 0; // Adjust if you have multiple charts
Chart chart = worksheet.Charts[chartIndex];
ImageOrPrintOptions chartOptions = new ImageOrPrintOptions
{
    ImageFormat = ImageFormat.Png,
    OnePagePerSheet = false
};
chart.ToImage("chart.png", chartOptions);
```

Luego puedes incrustar `chart.png` en una diapositiva de la misma manera que añadimos `sheetImage`. Este enfoque reduce el tamaño del archivo PPTX y es útil cuando los datos circundantes no son necesarios en la diapositiva.

---

## Problemas comunes y cómo evitarlos

| Problema | Por qué ocurre | Solución |
|----------|----------------|----------|
| **El texto se ve borroso** | Exportado con DPI bajo (predeterminado 96). | Establece `imageOptions.Dpi = 300;` antes de la conversión. |
| **Las formas desaparecen** | `ExportShapes` quedó en `false`. | Asegúrate de que `ExportShapes = true` cuando necesites gráficos editables. |
| **Desajuste de tamaño de diapositiva** | Imagen más grande que las dimensiones de la diapositiva. | Escala la imagen (ver fragmento de código) o cambia el tamaño de la diapositiva mediante `presentation.SlideSize`. |
| **Excepción de licencia** | Uso de la versión de prueba sin la activación adecuada. | Llama a `License license = new License(); license.SetLicense("Aspose.Total.lic");` al inicio de `Main`. |

---

## Ejemplo completo (listo para copiar‑pegar)

A continuación se muestra el programa completo, listo para insertar en un nuevo proyecto de consola. Reemplaza `YOUR_DIRECTORY` con la carpeta que contiene tu archivo Excel.

```csharp
using System;
using Aspose.Cells;
using Aspose.Slides;
using System.Drawing;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -----------------------------------------------------------------
            // 1️⃣ Load the Excel workbook
            // -----------------------------------------------------------------
            string excelPath = "YOUR_DIRECTORY/ShapesDemo.xlsx";
            Workbook workbook = new Workbook(excelPath);
            Worksheet worksheet = workbook.Worksheets[0];

            // -----------------------------------------------------------------
            // 2️⃣ Set up export options – keep shapes editable
            // -----------------------------------------------------------------
            ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
            {
                OnePagePerSheet = true,
                ExportShapes = true,
                ExportEditableTextBoxes = true,
                Dpi = 300                 // High‑resolution output
            };

            // -----------------------------------------------------------------
            // 3️⃣ Convert worksheet to an image
            // -----------------------------------------------------------------
            WorksheetToImageConverter converter = new WorksheetToImageConverter(worksheet);
            Image sheetImage = converter.ConvertToImage(0, imageOptions);

            // -----------------------------------------------------------------
            // 4️⃣ Create PowerPoint and add the image as a slide
            // -----------------------------------------------------------------
            Presentation presentation = new Presentation();
            ISlide slide = presentation.Slides[0];
            slide.Shapes.AddPictureFrame(
                ShapeType.Rectangle,
                0, 0,
                sheetImage.Width,
                sheetImage.Height,
                sheetImage);

            // -----------------------------------------------------------------
            // 5️⃣ Save the PPTX file
            // -----------------------------------------------------------------
            string pptxPath = "YOUR_DIRECTORY/Result.pptx";
            presentation.Save(pptxPath, SaveFormat.Pptx);

            Console.WriteLine("✅ PowerPoint created successfully at: " + pptxPath);
        }
    }
}
```

**Salida esperada:**  
Al ejecutar el programa se imprime `✅ PowerPoint created successfully at: YOUR_DIRECTORY/Result.pptx`. Al abrir el PPTX se muestra una única diapositiva que refleja la hoja de Excel original, con cuadros de texto editables.

---

## Resumen y próximos pasos

Ahora sabes cómo **crear PowerPoint desde Excel** usando las potentes APIs de Aspose, cómo **exportar la hoja de cálculo como imagen**, y cómo **guardar la presentación como PPTX** preservando la editabilidad. El mismo patrón funciona para libros de trabajo con varias hojas: simplemente recorre `workbook.Worksheets` y agrega una nueva diapositiva por cada una.

**¿Qué explorar a continuación?**  

- **Conversión por lotes:** Recorrer una carpeta de archivos Excel y generar una presentación por archivo.  
- **Diseños dinámicos:** Usa `slide.LayoutSlide` para aplicar plantillas de PowerPoint pre‑diseñadas.  
- **Exportación solo de gráficos:** Combina el fragmento “Export Excel chart as picture” con marcadores de posición en la diapositiva para una presentación más ligera.  
- **Estilizado avanzado:** Aplica fondos de diapositiva personalizados, transiciones o animaciones mediante Aspose.Slides.

Siéntete libre de experimentar: cambia la DPI, sustituye `ShapeType.Ellipse` por un marco de imagen circular, o incluso incrusta múltiples imágenes por diapositiva. El cielo es el límite cuando tienes control programático sobre

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}