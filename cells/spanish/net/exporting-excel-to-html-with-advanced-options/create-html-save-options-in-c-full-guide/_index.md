---
category: general
date: 2026-06-08
description: Crear opciones de guardado HTML en C# para incrustar todas las fuentes
  y guardar el libro de trabajo como HTML. Aprende cómo exportar un libro de trabajo
  de Excel a HTML con un ejemplo simple y completo.
draft: false
keywords:
- create html save options
- save workbook as html
- export excel workbook to html
- embed all fonts in html
language: es
og_description: Crea opciones de guardado en HTML en C# para incrustar todas las fuentes
  y exportar el libro de Excel a HTML. Esta guía te lleva paso a paso por una solución
  completa y lista para ejecutar.
og_title: Crear opciones de guardado HTML en C# – Tutorial completo
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: Create HTML save options in C# to embed all fonts and save workbook
    as HTML. Learn how to export Excel workbook to HTML with a simple, complete example.
  headline: Create HTML Save Options in C# – Full Guide
  type: TechArticle
- description: Create HTML save options in C# to embed all fonts and save workbook
    as HTML. Learn how to export Excel workbook to HTML with a simple, complete example.
  name: Create HTML Save Options in C# – Full Guide
  steps:
  - name: Expected Output
    text: Running the program produces `EmbeddedWorkbook.html` in the execution folder.
      Open it in any modern browser and you’ll see the text **“Hello, Aspose.Cells!”**
      rendered in **Comic Sans MS**, even if your system doesn’t have that font installed.
      Inspect the HTML source and you’ll notice a `<style>` bl
  - name: What if the workbook contains many different fonts?
    text: Embedding *all* fonts can inflate the HTML size dramatically (each font
      is Base64‑encoded). If file size becomes a concern, consider setting `EmbedAllFonts
      = false` and manually embedding only the critical fonts via `htmlOptions.FontEmbeddingMode
      = FontEmbeddingMode.Custom;`.
  - name: Does this work with older Excel files (`.xls`)?
    text: Absolutely. Aspose.Cells abstracts the source format, so whether you load
      an `.xlsx`, `.xls`, or even a CSV, the **export excel workbook to html** step
      behaves the same.
  - name: Can I control the output folder dynamically?
    text: 'Sure thing—just replace the hard‑coded `outputPath` with something like:'
  - name: What about images or charts inside the workbook?
    text: '`HtmlSaveOptions` also handles images, charts, and even formulas. By default
      they’re rendered as PNGs embedded in the HTML. If you prefer external files,
      toggle `htmlOptions.ExportImagesAsBase64 = false`.'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel Export
- HTML Export
title: Crear opciones de guardado HTML en C# – Guía completa
url: /es/net/exporting-excel-to-html-with-advanced-options/create-html-save-options-in-c-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crear opciones de guardado HTML en C# – Tutorial completo

¿Alguna vez te has preguntado cómo **crear opciones de guardado HTML** que mantengan cada fuente exactamente como aparece en Excel? No estás solo. Muchos desarrolladores se topan con el problema de que el HTML exportado pierde las fuentes personalizadas, dejando la página sin estilo. ¿La buena noticia? Con un par de líneas de C# puedes **incrustar todas las fuentes en HTML** y **guardar el libro de trabajo como HTML** sin inconvenientes.

En esta guía recorreremos todo el proceso de **exportar libro de Excel a HTML** usando Aspose.Cells. Al final tendrás un programa autónomo y ejecutable que no solo crea las opciones correctas, sino que también explica *por qué* cada configuración es importante. Sin piezas faltantes, sin desvíos a “ver la documentación”, solo una solución clara de principio a fin.

## Requisitos previos

Antes de comenzar, asegúrate de tener:

* .NET 6.0 SDK (o cualquier versión reciente de .NET) – el código funciona tanto en .NET Core como en .NET Framework.  
* El paquete NuGet **Aspose.Cells** – `dotnet add package Aspose.Cells`.  
* Un conocimiento básico de la sintaxis de C# – si puedes escribir un `Console.WriteLine`, estás listo.  

Eso es todo. Sin herramientas extra, sin archivos de configuración obscuros.

## Paso 1: Configurar el proyecto y cargar un libro de trabajo

Lo primero: necesitamos un proyecto de consola y un libro de trabajo con el que trabajar. Si ya tienes un archivo Excel, genial; de lo contrario, el ejemplo crea uno al vuelo.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Create a new workbook or load an existing one
        Workbook wb = new Workbook(); // starts with a default sheet

        // Populate the sheet with some styled text so we can see font embedding in action
        var sheet = wb.Worksheets[0];
        var cell = sheet.Cells["A1"];
        cell.PutValue("Hello, Aspose.Cells!");
        var style = cell.GetStyle();
        style.Font.Name = "Comic Sans MS";   // a non‑system font to test embedding
        style.Font.Size = 14;
        cell.SetStyle(style);

        // Continue with HTML export...
```

**Por qué hacemos esto:** Cargar un libro de trabajo nos da algo que exportar. Añadir una fuente personalizada (`Comic Sans MS`) hace visible la configuración *incrustar todas las fuentes* en el HTML generado.

## Paso 2: **Crear opciones de guardado HTML** – El núcleo de la tarea

Ahora llegamos al corazón del asunto: configurar `HtmlSaveOptions`. Este objeto indica a Aspose.Cells exactamente cómo debe escribirse el HTML.

```csharp
        // Step 2: Create HTML save options and embed all fonts in the output
        HtmlSaveOptions htmlOptions = new HtmlSaveOptions
        {
            // Setting this to true forces every used font to be base‑64 encoded
            // and placed directly inside the HTML file. No external .ttf files.
            EmbedAllFonts = true,

            // Optional but handy: keep the original Excel formatting
            ExportColumnHeaders = true,
            ExportRowHeaders = true
        };
```

**Por qué `EmbedAllFonts = true` es importante:** Cuando abres el HTML resultante en un navegador, las fuentes personalizadas ya están integradas en el archivo. Eso significa que la página se ve idéntica al origen de Excel, incluso en máquinas que no tengan la fuente instalada.

## Paso 3: **Guardar libro de trabajo como HTML** usando las opciones configuradas

Con nuestras opciones listas, finalmente podemos **guardar el libro de trabajo como HTML**. La firma del método acepta la ruta del archivo, el formato deseado y el objeto de opciones que acabamos de crear.

```csharp
        // Step 3: Save the workbook as an HTML file using the configured options
        string outputPath = "EmbeddedWorkbook.html";
        wb.Save(outputPath, SaveFormat.Html, htmlOptions);

        Console.WriteLine($"Workbook successfully exported to {outputPath}");
    }
}
```

**¿Qué ocurre tras bambalinas?** Aspose.Cells renderiza cada celda, convierte las definiciones de fuente a Base64 y las inserta en un bloque `<style>`. El `EmbeddedWorkbook.html` resultante es un único archivo autónomo—sin archivos `.css` ni fuentes externas.

## Ejemplo completo funcional

Juntando todo, aquí tienes el programa completo que puedes copiar‑pegar en `Program.cs` y ejecutar:

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Create or load a workbook
        Workbook wb = new Workbook();
        var sheet = wb.Worksheets[0];
        var cell = sheet.Cells["A1"];
        cell.PutValue("Hello, Aspose.Cells!");
        var style = cell.GetStyle();
        style.Font.Name = "Comic Sans MS"; // non‑standard font for testing
        style.Font.Size = 14;
        cell.SetStyle(style);

        // 2️⃣ Create HTML save options – embed all fonts
        HtmlSaveOptions htmlOptions = new HtmlSaveOptions
        {
            EmbedAllFonts = true,
            ExportColumnHeaders = true,
            ExportRowHeaders = true
        };

        // 3️⃣ Save workbook as HTML
        string outputPath = "EmbeddedWorkbook.html";
        wb.Save(outputPath, SaveFormat.Html, htmlOptions);

        Console.WriteLine($"Workbook successfully exported to {outputPath}");
    }
}
```

### Salida esperada

Al ejecutar el programa se genera `EmbeddedWorkbook.html` en la carpeta de ejecución. Ábrelo en cualquier navegador moderno y verás el texto **“Hello, Aspose.Cells!”** renderizado en **Comic Sans MS**, aunque tu sistema no tenga esa fuente instalada. Si inspeccionas el código fuente HTML notarás un bloque `<style>` con una regla `@font-face` que contiene una enorme cadena Base64—esa es la fuente incrustada.

![Create HTML Save Options diagram](image.png "Diagrama que muestra el flujo de exportación HTML"){: alt="Diagrama de creación de opciones de guardado HTML"}

*El texto alternativo incluye la palabra clave principal para SEO.*

## Preguntas frecuentes y casos límite

### ¿Qué pasa si el libro contiene muchas fuentes diferentes?

Incrustar *todas* las fuentes puede inflar el tamaño del HTML de forma drástica (cada fuente se codifica en Base64). Si el tamaño del archivo se vuelve un problema, considera establecer `EmbedAllFonts = false` y incrustar manualmente solo las fuentes críticas mediante `htmlOptions.FontEmbeddingMode = FontEmbeddingMode.Custom;`.

### ¿Funciona con archivos Excel antiguos (`.xls`)?

Absolutamente. Aspose.Cells abstrae el formato de origen, de modo que ya sea que cargues un `.xlsx`, `.xls` o incluso un CSV, el paso de **exportar libro de Excel a HTML** se comporta de la misma manera.

### ¿Puedo controlar la carpeta de salida de forma dinámica?

Claro—simplemente reemplaza el `outputPath` codificado por algo como:

```csharp
string outputPath = Path.Combine(Environment.CurrentDirectory, "Reports", "MyExport.html");
Directory.CreateDirectory(Path.GetDirectoryName(outputPath));
```

Así podrás **guardar el libro de trabajo como HTML** donde necesites.

### ¿Qué ocurre con imágenes o gráficos dentro del libro?

`HtmlSaveOptions` también gestiona imágenes, gráficos e incluso fórmulas. Por defecto se renderizan como PNG incrustados en el HTML. Si prefieres archivos externos, desactiva `htmlOptions.ExportImagesAsBase64 = false`.

## Consejos profesionales

* **Consejo de rendimiento:** Reutiliza una única instancia de `HtmlSaveOptions` si vas a exportar muchos libros en un bucle—generas menos basura.  
* **Consejo de pruebas:** Usa un navegador sin cabeza (por ejemplo, Puppeteer) para verificar automáticamente que las fuentes incrustadas se renderizan correctamente.  
* **Revisión de versión:** La bandera `EmbedAllFonts` se introdujo en Aspose.Cells 20.9. Asegúrate de que tu paquete NuGet esté actualizado.

## Conclusión

Ahora sabes exactamente cómo **crear opciones de guardado HTML** en C# que **incrusten todas las fuentes en HTML**, y has visto una forma práctica de **guardar el libro de trabajo como HTML** para cualquier archivo Excel. Este ejemplo completo, listo para ejecutar, cubre el *qué*, *por qué* y *cómo* de **exportar libro de Excel a HTML**, dándote una base sólida para escenarios más avanzados como procesamiento por lotes o estilos personalizados.

¿Listo para el siguiente paso? Prueba exportar un libro que contenga gráficos, o experimenta con diferentes propiedades de `HtmlSaveOptions` como `ExportImagesAsBase64` o `CssClassPrefix`. El mismo patrón se aplica—crea las opciones, ajusta los flags y llama a `wb.Save`. ¡Feliz codificación, y que tus exportaciones HTML siempre se vean exactamente como las hojas de Excel originales!

## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos con explicaciones paso a paso para ayudarte a dominar funciones adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Prefijar estilos de elementos de tabla con Html Save Options](/cells/english/net/exporting-excel-to-html-with-advanced-options/prefixing-table-elements-styles/)
- [Establecer fuente predeterminada en la conversión de Excel a HTML con Aspose.Cells para .NET | Guía de operaciones de libro](/cells/english/net/workbook-operations/excel-html-conversion-default-font-aspose-cells-net/)
- [Exportar propiedades de libro y hoja de cálculo a HTML usando Aspose.Cells para .NET](/cells/english/net/workbook-operations/export-excel-properties-to-html-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}