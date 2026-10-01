---
category: general
date: 2026-10-01
description: Aprende cómo incrustar fuentes en HTML al convertir Excel a HTML usando
  Aspose.Cells. Exporta Excel como HTML con fuentes incrustadas en unos pocos pasos.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to embed fonts
- convert excel to html
- embed fonts in html
- how to export excel
- export excel as html
language: es
lastmod: 2026-10-01
og_description: Cómo incrustar fuentes en HTML al exportar archivos de Excel. Sigue
  esta guía paso a paso para convertir Excel a HTML con fuentes incrustadas.
og_image_alt: Screenshot of Aspose.Cells code embedding fonts in exported HTML
og_title: Cómo incrustar fuentes en HTML desde Excel – Guía de Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Learn how to embed fonts in HTML while converting Excel to HTML using
    Aspose.Cells. Export Excel as HTML with embedded fonts in a few steps.
  headline: How to embed fonts when converting Excel to HTML with Aspose.Cells
  type: TechArticle
- description: Learn how to embed fonts in HTML while converting Excel to HTML using
    Aspose.Cells. Export Excel as HTML with embedded fonts in a few steps.
  name: How to embed fonts when converting Excel to HTML with Aspose.Cells
  steps:
  - name: 'Edge case: unsupported fonts'
    text: If the workbook uses a font that is not installed on the server, Aspose.Cells
      falls back to a default system font. To avoid this, install the required fonts
      on the server or embed them manually after export.
  - name: Converting multiple worksheets
    text: If you need to **convert Excel to HTML** for all worksheets, set `ExportActiveWorksheetOnly
      = false` (the default). Aspose.Cells will create a separate HTML file for each
      sheet.
  - name: Controlling CSS output
    text: 'You can reduce the HTML size by disabling inline CSS:'
  - name: Using a stream instead of a file
    text: 'When integrating into a web API, write the HTML to a `MemoryStream` and
      return it directly:'
  type: HowTo
tags:
- Aspose.Cells
- .NET
- Excel conversion
title: Cómo incrustar fuentes al convertir Excel a HTML con Aspose.Cells
url: /es/net/exporting-excel-to-html-with-advanced-options/how-to-embed-fonts-when-converting-excel-to-html-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo incrustar fuentes al convertir Excel a HTML con Aspose.Cells

Incrustar fuentes en HTML al convertir un libro de Excel es esencial para preservar el aspecto original en los navegadores. Si necesitas convertir Excel a HTML manteniendo las fuentes personalizadas, esta guía muestra el proceso completo. También verás cómo exportar Excel como HTML y por qué la incrustación de fuentes en HTML es importante para un renderizado consistente.

Este tutorial cubre todo lo que necesitas saber: bibliotecas requeridas, configuración del código y verificación del archivo HTML generado. Al final, podrás exportar Excel como HTML con fuentes incrustadas en solo unas pocas líneas de C#.

## Lo que necesitarás

Antes de comenzar, asegúrate de tener:

* **.NET 6.0 o posterior** – el código está dirigido a .NET 6, pero cualquier versión de .NET que admita Aspose.Cells funciona.
* **Aspose.Cells for .NET** – obtén una licencia o usa la versión de evaluación gratuita desde el sitio web de Aspose.
* Un entorno de desarrollo **C#** (Visual Studio, Rider o VS Code) – cualquier IDE que pueda compilar proyectos .NET.
* Un libro de Excel (`Styled.xlsx`) que utilice fuentes personalizadas que deseas preservar.

## Paso 1: Configurar Aspose.Cells en tu proyecto .NET

Primero, agrega el paquete NuGet Aspose.Cells a tu proyecto:

```bash
dotnet add package Aspose.Cells
```

Luego incluye el espacio de nombres al inicio de tu archivo C#:

```csharp
using Aspose.Cells;
```

Agregar el paquete hace que las clases `Workbook`, `HtmlSaveOptions` y relacionadas estén disponibles.

## Paso 2: Cargar el libro de Excel

Cargar el libro es el primer paso concreto en **cómo exportar datos de Excel**. El constructor `Workbook` lee el archivo desde el disco:

```csharp
// Step 1: Load the Excel workbook
var workbook = new Workbook("YOUR_DIRECTORY/Styled.xlsx");
```

*Por qué es importante:* Aspose.Cells analiza el libro, incluyendo estilos de celda, fórmulas e información de fuentes. Si el archivo no se encuentra, se lanza una excepción, así que verifica que la ruta sea correcta.

## Paso 3: Configurar las opciones de guardado HTML para incrustar fuentes

El núcleo de **incrustar fuentes en html** es la clase `HtmlSaveOptions`. Establece `EmbedFonts` a `true` para que cada fuente usada en el libro se escriba en la salida HTML como una regla `@font-face` codificada en Base64.

```csharp
// Step 2: Set HTML save options to embed fonts in the output
var htmlOptions = new HtmlSaveOptions
{
    EmbedFonts = true,
    // Optional: keep the original worksheet name as the HTML file name
    ExportActiveWorksheetOnly = true
};
```

*Por qué es importante:* Por defecto Aspose.Cells hace referencia a archivos de fuentes externos, que pueden no estar disponibles en la máquina del cliente. Habilitar `EmbedFonts` garantiza que el HTML renderizado se vea idéntico a la hoja de Excel original, sin importar las fuentes instaladas en el visor.

### Caso límite: fuentes no compatibles

Si el libro usa una fuente que no está instalada en el servidor, Aspose.Cells recurre a una fuente del sistema predeterminada. Para evitarlo, instala las fuentes necesarias en el servidor o incrústalas manualmente después de la exportación.

## Paso 4: Guardar el libro como HTML usando las opciones configuradas

Ahora puedes escribir el archivo HTML. El método `Save` recibe la ruta de salida y la instancia de `HtmlSaveOptions`:

```csharp
// Step 3: Save the workbook as an HTML file using the configured options
workbook.Save("YOUR_DIRECTORY/Styled.html", htmlOptions);
```

Después de la ejecución, `Styled.html` contiene los datos de la hoja y un bloque `<style>` con definiciones `@font-face` codificadas en Base64 para cada fuente personalizada.

## Paso 5: Verificar las fuentes incrustadas

Abre `Styled.html` en un navegador. Inspecciona la sección `<head>`; deberías ver algo como:

```html
<style>
@font-face {
    font-family: 'Calibri';
    src: url(data:font/ttf;base64,AAEAAAARAQAABAA...);
}
...
</style>
```

Si las fuentes aparecen correctamente en la tabla renderizada, la incrustación fue exitosa. Si notas glifos faltantes, verifica que los archivos de fuente origen estén instalados en la máquina que ejecuta la conversión.

## Variaciones comunes y opciones adicionales

### Convertir varias hojas de cálculo

Si necesitas **convertir Excel a HTML** para todas las hojas, establece `ExportActiveWorksheetOnly = false` (el valor predeterminado). Aspose.Cells creará un archivo HTML separado para cada hoja.

```csharp
htmlOptions.ExportActiveWorksheetOnly = false;
workbook.Save("YOUR_DIRECTORY/AllSheets.html", htmlOptions);
```

### Controlar la salida CSS

Puedes reducir el tamaño del HTML deshabilitando el CSS en línea:

```csharp
htmlOptions.ExportCssSeparately = true; // Generates a .css file alongside the .html
```

### Usar un stream en lugar de un archivo

Al integrarlo en una API web, escribe el HTML a un `MemoryStream` y devuélvelo directamente:

```csharp
using var stream = new MemoryStream();
workbook.Save(stream, htmlOptions);
stream.Position = 0; // Reset for reading
// Return stream as a file download in ASP.NET Core
```

## Consejo profesional: Licenciar el producto para eliminar marcas de agua de evaluación

Si estás usando la versión de evaluación, el HTML generado puede contener un comentario de marca de agua. Aplica tu licencia de Aspose.Cells antes de cargar el libro para producir una salida limpia:

```csharp
var license = new License();
license.SetLicense("Aspose.Total.lic");
```

## Ejemplo completo funcional

A continuación se muestra un programa completo y ejecutable que demuestra **cómo incrustar fuentes**, **convertir excel a html** y **exportar excel como html** en un solo paso:

```csharp
using System;
using Aspose.Cells;

class ExcelToHtmlWithEmbeddedFonts
{
    static void Main()
    {
        // Apply license if you have one (optional)
        // var license = new License();
        // license.SetLicense("Aspose.Total.lic");

        // 1️⃣ Load the Excel workbook
        var workbookPath = @"YOUR_DIRECTORY/Styled.xlsx";
        var workbook = new Workbook(workbookPath);

        // 2️⃣ Configure HTML save options to embed fonts
        var htmlOptions = new HtmlSaveOptions
        {
            EmbedFonts = true,
            ExportActiveWorksheetOnly = true, // Export only the first sheet
            ExportCssSeparately = false        // Keep CSS inline for a single file
        };

        // 3️⃣ Save as HTML
        var htmlPath = @"YOUR_DIRECTORY/Styled.html";
        workbook.Save(htmlPath, htmlOptions);

        Console.WriteLine($"Excel workbook '{workbookPath}' has been exported to HTML with embedded fonts at '{htmlPath}'.");
    }
}
```

**Salida esperada:** Después de ejecutar el programa, `Styled.html` aparecerá en `YOUR_DIRECTORY`. Abrir el archivo en cualquier navegador moderno muestra la hoja de cálculo con las mismas fuentes que el archivo Excel original, incluso en máquinas que no tengan esas fuentes.

## Conclusión

Ahora sabes **cómo incrustar fuentes** cuando **conviertes Excel a HTML** usando Aspose.Cells, y has visto el flujo completo desde cargar un libro hasta verificar las fuentes incrustadas. Este enfoque garantiza que la fidelidad visual de tus archivos Excel se mantenga en el HTML generado, lo que lo hace ideal para informes web, boletines de correo electrónico o cualquier escenario donde debas **exportar Excel como HTML** con tipografía personalizada.

A continuación, explora temas relacionados como **exportar Excel como PDF**, **estilizar la salida HTML con CSS personalizado**, o **procesar en lote múltiples libros**. Cada uno de estos se basa en el mismo patrón `HtmlSaveOptions`, por lo que puedes adaptar el código con cambios mínimos.

¡Feliz codificación!

## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y explicaciones paso a paso para ayudarte a dominar funciones adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [How to Export Excel to HTML – Step‑by‑Step Guide](/cells/english/net/exporting-excel-to-html-with-advanced-options/how-to-export-excel-to-html-step-by-step-guide/)
- [How to Embed Fonts in HTML – Complete C# Guide](/cells/english/net/exporting-excel-to-html-with-advanced-options/how-to-embed-fonts-in-html-complete-c-guide/)
- [How to embed fonts when converting Excel to PDF – Step‑by‑Step Guide](/cells/english/net/conversion-to-pdf/how-to-embed-fonts-when-converting-excel-to-pdf-step-by-step/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}