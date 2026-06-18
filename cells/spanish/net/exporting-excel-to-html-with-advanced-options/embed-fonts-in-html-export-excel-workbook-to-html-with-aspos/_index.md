---
category: general
date: 2026-06-17
description: Incrusta fuentes en HTML mientras guardas el libro de trabajo como HTML.
  Aprende cómo convertir el libro de trabajo a HTML y exportar HTML de Excel con fuentes
  incrustadas en unos pocos pasos.
draft: false
keywords:
- embed fonts in html
- save workbook as html
- convert workbook to html
- how to export excel html
language: es
og_description: Incrusta fuentes en HTML cuando guardas el libro de trabajo como HTML.
  Sigue esta guía para convertir el libro de trabajo a HTML y aprende cómo exportar
  HTML de Excel con soporte completo de fuentes.
og_title: Incrustar fuentes en HTML – Exportar libro de Excel a HTML
schemas:
- author: Aspose
  dateModified: '2026-06-17'
  description: Embed fonts in HTML while you save workbook as HTML. Learn how to convert
    workbook to HTML and export Excel HTML with embedded fonts in a few steps.
  headline: Embed Fonts in HTML – Export Excel Workbook to HTML with Aspose.Cells
  type: TechArticle
tags:
- Aspose.Cells
- Excel
- HTML export
title: Incrustar fuentes en HTML – Exportar libro de Excel a HTML con Aspose.Cells
url: /es/net/exporting-excel-to-html-with-advanced-options/embed-fonts-in-html-export-excel-workbook-to-html-with-aspos/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Incrustar fuentes en HTML – Exportar libro de Excel a HTML con Aspose.Cells

¿Alguna vez te has preguntado cómo **incrustar fuentes en HTML** al exportar una hoja de Excel? No eres el único. Muchos desarrolladores se topan con un problema cuando el HTML generado muestra una fuente genérica sans‑serif en lugar del estilo original de Excel. ¿La buena noticia? Con un par de líneas de código puedes **guardar el libro como HTML** y mantener todas las fuentes intactas.

En este tutorial recorreremos todo el proceso de **convertir un libro a HTML** usando Aspose.Cells para .NET, explicaremos por qué es importante incrustar fuentes y te mostraremos exactamente **cómo exportar Excel a HTML** para que el resultado se vea idéntico a la hoja de cálculo original. Sin herramientas externas, sin procesamiento manual posterior—solo código C# limpio y ejecutable.

## Requisitos previos

- .NET 6.0 o posterior (el ejemplo funciona en .NET Core, .NET Framework y .NET 5+)
- Paquete NuGet Aspose.Cells para .NET (`Install-Package Aspose.Cells`)
- Un conocimiento básico de C# y manejo de archivos Excel
- Opcional: un archivo de fuente TrueType personalizado que deseas incrustar (p.ej., `MyFont.ttf`)

¿Tienes todo eso? Genial—¡vamos a sumergirnos!

## Paso 1: Configurar el proyecto y cargar un libro de Excel

Primero necesitamos un objeto workbook. Puedes crear uno desde cero o cargar un `.xlsx` existente. Aquí tienes una configuración mínima que también agrega una fuente personalizada a la colección de estilos del libro.

```csharp
using Aspose.Cells;
using System.IO;

// Load an existing workbook (replace with your own path)
Workbook wb = new Workbook("SampleData.xlsx");

// OPTIONAL: Register a custom font if your sheet uses one that isn’t standard
string fontPath = Path.Combine(Directory.GetCurrentDirectory(), "MyFont.ttf");
if (File.Exists(fontPath))
{
    // Register the font with the font manager – this ensures Aspose knows about it
    FontConfigs.AddFontFile(fontPath);
}
```

*¿Por qué este paso?* Al cargar el libro primero le damos a Aspose.Cells la oportunidad de inspeccionar todos los estilos de celda. Registrar una fuente personalizada garantiza que la fuente se encontrará cuando más adelante la incrustemos en el archivo HTML.

## Paso 2: Configurar las opciones de guardado HTML para **incrustar fuentes en HTML**

La magia está en `HtmlSaveOptions`. Configurar `EmbedFonts = true` indica a la biblioteca que incruste cada fuente utilizada como una regla `@font-face` codificada en Base64 dentro del archivo HTML generado.

```csharp
// Configure HTML save options – this is where we embed fonts in HTML
HtmlSaveOptions saveOptions = new HtmlSaveOptions
{
    // Embed all referenced fonts directly into the HTML output
    EmbedFonts = true,

    // Optional: keep the original layout (useful for complex sheets)
    ExportActiveWorksheetOnly = true,

    // Optional: produce a single HTML file (no external CSS or images)
    ExportImagesAsBase64 = true
};
```

*¿Por qué habilitar `EmbedFonts`?* Sin ello, el HTML de salida hace referencia a fuentes del sistema, y cualquiera que abra el archivo en una máquina que no tenga esas fuentes verá una fuente de reemplazo. Incrustar garantiza la fidelidad visual en todos los navegadores y dispositivos.

## Paso 3: **Guardar el libro como HTML** con las opciones configuradas

Ahora finalmente escribimos el archivo. El método `Save` recibe tres argumentos: la ruta de destino, el formato (`SaveFormat.Html`) y las opciones que acabamos de configurar.

```csharp
// Define the output HTML file path
string outputPath = Path.Combine(Directory.GetCurrentDirectory(), "with-fonts.html");

// Save the workbook as HTML with embedded fonts
wb.Save(outputPath, SaveFormat.Html, saveOptions);
```

Si todo funciona sin problemas, terminarás con un único archivo `with-fonts.html` que contiene todo el diseño de la hoja de cálculo *y* los datos de la fuente codificados directamente en el marcado.

## Resultado esperado

Abre `with-fonts.html` en cualquier navegador moderno (Chrome, Edge, Firefox). Deberías ver:

- Los mismos valores de celda, colores y bordes que en el archivo Excel original.
- Texto renderizado con la fuente exacta que usaste en Excel, incluso si esa fuente no está instalada en tu computadora.
- Sin archivos externos `.css` o de imagen—todo reside dentro del archivo HTML.

A continuación se muestra un pequeño extracto de cómo podría verse el bloque `<style>` generado (la cadena Base64 está truncada por brevedad):

```html
<style type="text/css">
@font-face{
    font-family:'MyCustomFont';
    src:url(data:font/truetype;charset=utf-8;base64,AAEAAAALAIAAAwAwT1Mv... ) format('truetype');
}
...
</style>
```

## Paso 4: Problemas comunes y cómo solucionarlos

| Problema | Por qué ocurre | Solución |
|------|----------------|-----|
| **Fuente faltante en el HTML** | El archivo de fuente no se registró con `FontConfigs` antes de guardar. | Llama a `FontConfigs.AddFontFile` *antes* de crear `HtmlSaveOptions`. |
| **Tamaño enorme del archivo HTML** | Incrustar muchas fuentes grandes puede inflar el archivo. | Incrusta solo las fuentes que realmente necesitas; usa `saveOptions.FontEmbeddingMode = FontEmbeddingMode.Subset` para incrustar solo los glifos usados (disponible en versiones más recientes de Aspose). |
| **Caracteres incorrectos (p.ej., glifos asiáticos)** | La fuente no contiene los rangos Unicode requeridos. | Asegúrate de que la fuente origen soporte los caracteres, o incrusta una fuente de respaldo adicional. |
| **Ralentización del rendimiento en libros grandes** | Incrustar fuentes añade sobrecarga de procesamiento. | Exporta solo la hoja activa (`ExportActiveWorksheetOnly = true`) o divide el libro en partes más pequeñas. |

## Paso 5: Extender la solución – Exportar múltiples hojas de cálculo

Si necesitas **convertir un libro a HTML** para todas las hojas, simplemente desactiva `ExportActiveWorksheetOnly`:

```csharp
saveOptions.ExportActiveWorksheetOnly = false; // Export every sheet
wb.Save("all-sheets.html", SaveFormat.Html, saveOptions);
```

Cada hoja aparecerá como un `<div>` separado en el mismo archivo HTML, aún con fuentes incrustadas.

## Consejo profesional: combinar con personalización CSS

A veces deseas un control más estricto sobre el marcado generado. `HtmlSaveOptions` ofrece una propiedad `CssClassPrefix` para evitar colisiones de nombres de clase al combinar múltiples exportaciones HTML:

```csharp
saveOptions.CssClassPrefix = "myExcel_";
```

Ahora cada clase CSS generada comenzará con `myExcel_`, lo que facilita aplicar tu propia hoja de estilos más adelante.

## Recapitulación

- **Incrustar fuentes en HTML** estableciendo `HtmlSaveOptions.EmbedFonts = true`.
- Usa **guardar libro como HTML** (`wb.Save(..., SaveFormat.Html, ...)`) para producir un archivo único y autónomo.
- Este método **convierte un libro a HTML** preservando cada detalle visual, respondiendo la clásica pregunta **cómo exportar Excel a HTML** con plena fidelidad.
- Registra fuentes personalizadas con `FontConfigs.AddFontFile` para asegurar que estén disponibles para incrustar.
- Ajusta opciones como `ExportImagesAsBase64` y `ExportActiveWorksheetOnly` para adaptarlas a las necesidades de tu proyecto.

## ¿Qué sigue?

- Intenta exportar a **MHTML** (`SaveFormat.Mhtml`) para un paquete aún más portátil.
- Explora la **conversión a PDF** (`SaveFormat.Pdf`) si necesitas un formato listo para imprimir.
- Integra la exportación HTML en una API web para que los usuarios puedan descargar hojas de cálculo con estilo al instante.

Siéntete libre de experimentar—cambiar fuentes, modificar la selección de hojas, o combinar múltiples formatos de exportación. La flexibilidad de Aspose.Cells te permite adaptar la salida a cualquier escenario, desde paneles de informes automatizados hasta fragmentos HTML listos para correo electrónico.

¡Feliz codificación, y que tu HTML siempre se vea exactamente como la hoja de Excel original!

## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y funcionales con explicaciones paso a paso para ayudarte a dominar características adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [How to Create and Export Excel to HTML Using Aspose.Cells Java | Workbook Operations Guide](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)
- [Set Default Font in Excel-to-HTML Conversion with Aspose.Cells for .NET | Workbook Operations Guide](/cells/english/net/workbook-operations/excel-html-conversion-default-font-aspose-cells-net/)
- [How to Export Excel to HTML with Grid Lines Using Aspose.Cells for .NET](/cells/english/net/workbook-operations/export-excel-to-html-grid-lines-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}