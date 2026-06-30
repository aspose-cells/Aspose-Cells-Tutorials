---
category: general
date: 2026-06-30
description: Exporta el gráfico como PNG mientras conviertes Excel a HTML usando Aspose.Cells.
  Aprende a incrustar imágenes como Base64 y a guardar el libro de trabajo como HTML
  en minutos.
draft: false
keywords:
- export chart as png
- convert excel to html
- embed images as base64
- save workbook as html
- export excel chart to png
language: es
og_description: Exporta el gráfico como PNG e incrusta imágenes como Base64 mientras
  conviertes Excel a HTML. Sigue este tutorial paso a paso en C# para guardar el libro
  de trabajo como HTML sin esfuerzo.
og_title: Exportar gráfico como PNG – Convertir Excel a HTML con Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Export chart as PNG while you convert Excel to HTML using Aspose.Cells.
    Learn to embed images as Base64 and save workbook as HTML in minutes.
  headline: Export Chart as PNG – Complete Guide to Convert Excel to HTML with Aspose.Cells
  type: TechArticle
- description: Export chart as PNG while you convert Excel to HTML using Aspose.Cells.
    Learn to embed images as Base64 and save workbook as HTML in minutes.
  name: Export Chart as PNG – Complete Guide to Convert Excel to HTML with Aspose.Cells
  steps:
  - name: Open Visual Studio and create a new **Console App** (`dotnet new console`).
    text: Open Visual Studio and create a new **Console App** (`dotnet new console`).
  - name: 'Add the Aspose.Cells NuGet package:'
    text: 'Add the Aspose.Cells NuGet package:'
  - name: '(Optional) If you have a license file, place it in the project root and
      activate it at runtime:'
    text: '(Optional) If you have a license file, place it in the project root and
      activate it at runtime:'
  - name: Open the generated HTML in Chrome. Right‑click the chart image and select
      **Open image in new tab**. The URL will still start with `data:image/png;base64,`.
    text: Open the generated HTML in Chrome. Right‑click the chart image and select
      **Open image in new tab**. The URL will still start with `data:image/png;base64,`.
  - name: 'If the image appears blurry, consider increasing the chart’s resolution
      before saving:'
    text: 'If the image appears blurry, consider increasing the chart’s resolution
      before saving:'
  - name: 'For charts that rely on external data sources, make sure the workbook is
      fully refreshed before saving:'
    text: 'For charts that rely on external data sources, make sure the workbook is
      fully refreshed before saving:'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: Exportar gráfico como PNG – Guía completa para convertir Excel a HTML con Aspose.Cells
url: /es/net/chart-rendering-and-conversion/export-chart-as-png-complete-guide-to-convert-excel-to-html/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Exportar gráfico como PNG – Guía completa para convertir Excel a HTML con Aspose.Cells

¿Alguna vez te has preguntado cómo **exportar gráfico como PNG** directamente desde un libro de Excel mientras conviertes toda la hoja en HTML limpio y adaptable? No eres el único. Muchos desarrolladores se topan con un obstáculo cuando necesitan un informe listo para la web que muestre gráficos sin tener que manejar archivos de imagen separados. La buena noticia es que Aspose.Cells lo hace muy fácil.

En este tutorial recorreremos paso a paso los pasos exactos para **convertir Excel a HTML**, **incrustar imágenes como Base64**, y finalmente **guardar el libro como HTML**, asegurándonos de que cada gráfico se guarde como una imagen PNG. Al final tendrás un único archivo HTML que puedes colocar en cualquier página web, y cada gráfico aparecerá instantáneamente, sin activos adicionales requeridos.

## Lo que aprenderás

- Cómo cargar un libro existente que ya contiene gráficos.  
- Qué banderas de `HtmlSaveOptions` controlan la exportación de imágenes, el formato del gráfico y la adaptabilidad.  
- El código exacto necesario para **exportar gráfico como PNG** e incrustar esos PNG como cadenas Base64.  
- Cómo **guardar el libro como HTML** con una sola llamada de método.  
- Consejos para solucionar problemas comunes, como imágenes de gráficos que faltan o cadenas Base64 demasiado grandes.  

**Requisitos previos:**  
- .NET 6+ (o .NET Framework 4.6+) instalado.  
- Una licencia válida de Aspose.Cells (o una clave de evaluación temporal).  
- Familiaridad básica con C# y Visual Studio (o tu IDE favorito).  

Si alguno de estos puntos te resulta desconocido, detente un momento y configúralo; el resto de la guía asume que ya están listos.

---

## Paso 1: Configura tu proyecto e instala Aspose.Cells

Antes de que podamos **exportar gráfico como PNG**, necesitamos un proyecto C# que haga referencia a la biblioteca Aspose.Cells.

1. Abre Visual Studio y crea una nueva **Console App** (`dotnet new console`).  
2. Añade el paquete NuGet de Aspose.Cells:

```bash
dotnet add package Aspose.Cells
```

3. (Opcional) Si tienes un archivo de licencia, colócalo en la raíz del proyecto y actívalo en tiempo de ejecución:

```csharp
// Activate license – skip this line if you’re using the trial version
Aspose.Cells.License license = new Aspose.Cells.License();
license.SetLicense("Aspose.Cells.lic");
```

> **Consejo profesional:** Mantén el archivo de licencia fuera del control de versiones. Usa variables de entorno o almacenes seguros de secretos para producción.

---

## Paso 2: Carga el libro que contiene el gráfico

Ahora cargaremos el archivo Excel que ya tiene el gráfico que queremos **exportar gráfico como PNG**.

```csharp
using Aspose.Cells;
using System.Drawing.Imaging;   // Needed for ImageFormat enum

// Path to the source workbook – change this to your actual file location
string sourcePath = @"C:\Reports\ReportWithChart.xlsx";

// Load the workbook
Workbook workbook = new Workbook(sourcePath);
```

> **Por qué es importante:** Cargar el libro al principio nos da acceso a todas las hojas, gráficos y objetos incrustados. Si el libro no se carga, el paso posterior de **exportar gráfico a PNG** nunca se ejecutará.

---

## Paso 3: Configura las opciones de guardado HTML

El corazón de la solución vive en `HtmlSaveOptions`. Al alternar algunas propiedades podemos:

- **ExportChartImageFormat = ImageFormat.Png** → garantiza que cada gráfico se convierta en PNG.  
- **ExportImagesAsBase64 = true** → incrusta los datos PNG directamente en el HTML, eliminando archivos externos.  
- **IsResponsive = true** → hace que las tablas generadas se adapten a pantallas móviles.  
- **ExportPrintingHeadersFooters = false** → elimina metadatos de impresión innecesarios.  

Aquí tienes la configuración completa:

```csharp
// Create HTML save options and fine‑tune them
HtmlSaveOptions htmlOptions = new HtmlSaveOptions
{
    // 1️⃣ Embed PNG/JPEG images directly as Base64 strings
    ExportImagesAsBase64 = true,

    // 2️⃣ Force chart images to be saved as PNG files
    ExportChartImageFormat = ImageFormat.Png,

    // 3️⃣ Omit printing headers/footers for a cleaner web view
    ExportPrintingHeadersFooters = false,

    // 4️⃣ Generate responsive tables for mobile friendliness
    IsResponsive = true,

    // 5️⃣ Target modern browsers with HTML5
    HtmlVersion = HtmlVersion.Html5
};
```

### ¿Por qué estas configuraciones?

- **ExportChartImageFormat = ImageFormat.Png** es la única forma de garantizar una imagen de gráfico sin pérdida y segura para la web.  
- **ExportImagesAsBase64 = true** significa que puedes **incrustar imágenes como Base64**, lo cual es perfecto para informes por correo electrónico o implementaciones de un solo archivo.  
- **IsResponsive = true** resuelve una queja frecuente: tablas que se desbordan en smartphones.  
- **ExportPrintingHeadersFooters = false** mantiene el HTML ligero—sin información de impresión oculta que nunca se usa en la web.  

---

## Paso 4: Guarda el libro como HTML

Con las opciones configuradas, la línea final es una única llamada que tanto **convierte Excel a HTML** como **exporta gráfico como PNG** en segundo plano.

```csharp
// Destination HTML file – adjust the folder as needed
string outputPath = @"C:\Reports\Report.html";

// Save the workbook using the configured options
workbook.Save(outputPath, htmlOptions);
```

Cuando esta línea finalice, tendrás un archivo llamado `Report.html`. Ábrelo en cualquier navegador y verás:

- Todos los datos de la hoja renderizados como tablas HTML limpias.  
- Cada gráfico mostrado como una imagen PNG en línea (gracias a la incrustación Base64).  
- Ningún archivo de imagen extra junto al HTML.  

### Resultado esperado

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8">
    <title>Report</title>
    <style>
        /* Aspose.Cells generated responsive CSS */
    </style>
</head>
<body>
    <table class="aspose">
        <!-- Table rows here -->
    </table>

    <!-- Example of an embedded chart image -->
    <img src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAA..." alt="Chart 1" />
</body>
</html>
```

Observa el atributo `src="data:image/png;base64,..."`—esa es la magia de **incrustar imágenes como base64** en acción. No se crean archivos `.png` separados en el disco.

---

## Paso 5: Verifica la exportación PNG y ajusta si es necesario

A veces un gráfico puede verse ligeramente distorsionado después de la conversión, especialmente si usa fuentes personalizadas o degradados complejos. Así puedes comprobarlo:

1. Abre el HTML generado en Chrome. Haz clic derecho sobre la imagen del gráfico y selecciona **Abrir imagen en una nueva pestaña**. La URL seguirá comenzando con `data:image/png;base64,`.  
2. Si la imagen aparece borrosa, considera aumentar la resolución del gráfico antes de guardarlo:

```csharp
htmlOptions.ImageResolution = 300; // DPI – higher values = sharper PNGs
```

3. Para los gráficos que dependen de fuentes de datos externas, asegúrate de que el libro esté completamente actualizado antes de guardar:

```csharp
workbook.CalculateFormula(); // Force recalculation
```

Estos ajustes garantizan que el paso **exportar gráfico de Excel a PNG** produzca gráficos nítidos y listos para producción.

---

## Paso 6: Despliega el HTML donde quieras

Como todas las imágenes están incrustadas, ahora puedes:

- Enviar el HTML como un único archivo adjunto por correo.  
- Pegar el HTML en un CMS que acepte código sin procesar.  
- Alojarlo en un sitio estático sin preocuparte por archivos PNG faltantes.  

Si alguna vez necesitas los archivos PNG como activos separados (quizá para un PDF más adelante), puedes cambiar `ExportImagesAsBase64` a `false` y señalar `HtmlSaveOptions` a una carpeta de salida para imágenes.

```csharp
htmlOptions.ExportImagesAsBase64 = false;
htmlOptions.ImageFolder = @"C:\Reports\Images";
```

Ahora el HTML hará referencia a archivos PNG externos, manteniendo **exportar gráfico como PNG** pero dándote archivos de imagen individuales para otros usos.

---

## Problemas comunes y cómo evitarlos

| Síntoma | Causa probable | Solución |
|---------|----------------|----------|
| Gráfico ausente en el HTML | `ExportChartImageFormat` dejó el valor predeterminado (`Jpeg`) y el navegador bloquea contenido mixto. | Establece `ExportChartImageFormat = ImageFormat.Png`. |
| Archivo HTML muy grande (varios MB) | Gráficos grandes o muchas imágenes de alta resolución incrustadas como Base64. | Reduce `htmlOptions.ImageResolution` o comprime el gráfico en Excel antes de la conversión. |
| Tablas se desbordan en móvil | `IsResponsive` no está habilitado. | Asegúrate de que `IsResponsive = true` en `HtmlSaveOptions`. |
| Cadenas Base64 contienen saltos de línea | Versiones antiguas de .NET pueden envolver cadenas largas. | Actualiza a .NET 6+ o establece `htmlOptions.ExportBase64StringInOneLine = true`. |

---

## Bonus: Encapsúlalo en un método reutilizable

Si vas a realizar esta conversión con frecuencia, encapsula la lógica:

```csharp
public static void ConvertExcelToHtmlWithPngCharts(string excelPath, string htmlPath)
{
    // Load workbook
    Workbook wb = new Workbook(excelPath);

    // Prepare options
    HtmlSaveOptions opts = new HtmlSaveOptions
    {
        ExportImagesAsBase64 = true,
        ExportChartImageFormat = ImageFormat.Png,
        ExportPrintingHeadersFooters = false,
        IsResponsive = true,
        HtmlVersion = HtmlVersion.Html5,
        ImageResolution = 150 // reasonable default DPI
    };

    // Force recalculation for up‑to‑date charts
    wb.CalculateFormula();

    // Save as HTML
    wb.Save(htmlPath, opts);
}
```

Ahora puedes llamar a `ConvertExcelToHtmlWithPngCharts(@"C:\Reports\MyFile.xlsx", @"C:\Reports\MyFile.html");` desde cualquier parte de tu código.

---

## Conclusión

Acabas de dominar cómo **exportar gráfico como PNG** mientras **conviertes Excel a HTML**, **incrustas imágenes como Base64**, y **guardas el libro como HTML** usando Aspose.Cells. La clave es que unas pocas configuraciones bien elegidas de `HtmlSaveOptions` te dan un archivo HTML único y autocontenido que funciona en cualquier dispositivo—sin archivos PNG extra, sin carpetas desordenadas.

¿Listo para el siguiente desafío? Prueba combinar este enfoque con **exportar gráfico de Excel a PNG** para generación de PDF, o experimenta con CSS personalizado para estilizar más las tablas. El cielo es el límite cuando controlas tanto los datos como la presentación de forma programática.

¡No dudes en dejar un comentario si encuentras algún obstáculo, o compartir cómo has adaptado este patrón en tus propios proyectos! ¡Feliz codificación!

## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y explicaciones paso a paso para ayudarte a dominar funciones adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Export Excel to HTML Using Aspose.Cells for .NET: A Complete Guide](/cells/english/net/workbook-operations/export-excel-html-aspose-cells-net/)
- [Export Excel to HTML Without Frame Scripts Using Aspose.Cells for .NET](/cells/english/net/workbook-operations/export-excel-to-html-aspose-cells-net/)
- [How to Export an Excel Worksheet to PNG Using Aspose.Cells Java](/cells/english/java/workbook-operations/export-excel-to-png-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}