---
category: general
date: 2026-02-15
description: Cómo copiar la fuente y aplicar el estilo de celda en C# con un ejemplo
  sencillo. Aprende a obtener el estilo de celda y a usar el formato de celda para
  establecer el tamaño de fuente del cuadro de texto.
draft: false
keywords:
- how to copy font
- apply cell style
- get cell style
- use cell formatting
- set textbox font size
language: es
og_description: cómo copiar la fuente de una celda de la hoja de cálculo y aplicar
  el estilo de celda a un cuadro de texto. Esta guía muestra cómo obtener el estilo
  de celda, usar el formato de celda y establecer el tamaño de fuente del cuadro de
  texto.
og_title: cómo copiar la fuente de una celda de Excel – Tutorial completo de C#
tags:
- C#
- EPPlus
- UI‑grid
- Excel‑interop
title: Cómo copiar la fuente de una celda de Excel a un TextBox – Guía paso a paso
url: /es/net/working-with-fonts-in-excel/how-to-copy-font-from-an-excel-cell-to-a-textbox-step-by-ste/
---

preserve code placeholders.

Now produce final content.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo copiar la fuente de una celda de Excel a un TextBox – Tutorial completo de C#

¿Alguna vez necesitaste **copiar la fuente** de una celda de hoja de cálculo y hacer que un cuadro de texto de la UI se vea exactamente igual? No eres el único. En muchas herramientas de informes o paneles personalizados, terminarás extrayendo datos de Excel y luego intentando mantener la fidelidad visual —familia de fuente, tamaño y color— intacta.  

La buena noticia es que con solo unas pocas líneas de C# puedes **obtener el estilo de la celda**, leer sus propiedades de fuente y **aplicar el estilo de la celda** a cualquier control de cuadro de texto. En este tutorial recorreremos un ejemplo completo y ejecutable que muestra cómo **usar el formato de celdas** e incluso **establecer el tamaño de fuente del textbox** de forma programática.

---

## Lo que aprenderás

- Cómo obtener un objeto `TextBox` de un componente de cuadrícula (`gridJs` en nuestro ejemplo)
- Cómo leer la familia de fuente, el tamaño y el color de una celda específica de Excel (`B2`)
- Cómo copiar esos atributos de fuente al cuadro de texto para que la UI refleje la hoja de cálculo
- Problemas comunes (p. ej., conversión de color) y algunos **consejos profesionales** para mantener tu código robusto
- Un fragmento de código listo‑para‑ejecutar que puedes insertar en una aplicación de consola o proyecto WinForms

**Prerequisites**  
You should have:

1. .NET 6+ (or .NET Framework 4.8) installed  
2. The EPPlus NuGet package (for Excel handling)  
3. A grid control that exposes a `TextBoxes` dictionary (the example uses a fictional `gridJs` but the idea works with any UI library)

Now, let’s get our hands dirty.

---

## Paso 1: Configurar el proyecto y cargar la hoja de cálculo

First, create a new console or WinForms project and add EPPlus:

```bash
dotnet add package EPPlus --version 6.*
```

Then, load the workbook and grab the cell whose style you want to copy.

```csharp
using OfficeOpenXml;
using OfficeOpenXml.Style;
using System.Drawing;

// ...

// Load the Excel file (make sure the file exists at the given path)
var fileInfo = new FileInfo(@"C:\Data\Sample.xlsx");
using var package = new ExcelPackage(fileInfo);
ExcelWorksheet ws = package.Workbook.Worksheets["Sheet1"]; // adjust sheet name if needed

// Retrieve the style of cell B2
ExcelStyle cellStyle = ws.Cells["B2"].Style;
```

**Por qué es importante:** EPPlus te brinda acceso directo al objeto `Style`, que contiene el sub‑objeto `Font`. Desde allí puedes leer `Name`, `Size` y `Color`. Este es el núcleo de la operación **obtener estilo de celda**.

---

## Paso 2: Obtener el TextBox objetivo de tu cuadrícula

Assuming your UI grid (`gridJs`) stores text boxes in a dictionary keyed by column name, you can retrieve the one you want like so:

```csharp
// Fake grid class for illustration – replace with your actual grid component
var gridJs = new MyGrid(); // MyGrid is a placeholder for your UI control

// Step 1: Retrieve the "Notes" text box from the grid
var notesTextBox = gridJs.TextBoxes["Notes"];
```

If you’re using WinForms, `notesTextBox` could be a `TextBox` control; for WPF it might be a `TextBox` element, and for a web‑based grid it could be a JavaScript interop object. The key point is that you have a reference you can manipulate.

---

## Paso 3: Transferir la familia de fuente

Now that we have both the source style and the destination control, copy the font family.

```csharp
// Apply the cell's font family to the text box
notesTextBox.FontFamily = cellStyle.Font.Name;
```

**Consejo profesional:** No todos los frameworks UI exponen una propiedad `FontFamily` que acepte una cadena simple. En WinForms establecerías `notesTextBox.Font = new Font(cellStyle.Font.Name, notesTextBox.Font.Size);`. Ajusta según corresponda.

---

## Paso 4: Transferir el tamaño de fuente

Font size is stored as a `float` in EPPlus. Apply it directly:

```csharp
// Apply the cell's font size to the text box
notesTextBox.FontSize = cellStyle.Font.Size;
```

If your control uses points (which most do), you can assign the value without conversion. For CSS‑based grids you might need to append `"pt"`.

---

## Paso 5: Transferir el color de fuente

Colour conversion is the trickiest part because EPPlus stores colours as ARGB integers, while many UI frameworks expect a `System.Drawing.Color` or a CSS hex string.

```csharp
// Apply the cell's font colour to the text box
// EPPlus stores colour as a System.Drawing.Color when using .Color property
var excelColor = cellStyle.Font.Color?.GetColor();

// Fallback to black if the cell has no explicit colour
var safeColor = excelColor ?? Color.Black;

// Convert to the format your UI expects (example for WinForms)
notesTextBox.FontColor = safeColor;
```

> **Why this works:** `GetColor()` resolves theme‑based colours and returns a concrete `System.Drawing.Color`. If the cell uses the default colour (no explicit setting), we default to black to avoid null reference exceptions.

---

## Ejemplo completo

Putting everything together, here’s a minimal console app that reads an Excel file, extracts the font from **B2**, and applies it to a mock text box.

```csharp
using OfficeOpenXml;
using OfficeOpenXml.Style;
using System;
using System.Collections.Generic;
using System.Drawing;

namespace FontCopyDemo
{
    // Mock grid control – replace with your real UI component
    public class MyGrid
    {
        public Dictionary<string, TextBoxMock> TextBoxes { get; } = new()
        {
            { "Notes", new TextBoxMock() }
        };
    }

    // Simple text box representation for demonstration
    public class TextBoxMock
    {
        public string FontFamily { get; set; }
        public float FontSize { get; set; }
        public Color FontColor { get; set; }

        public override string ToString()
        {
            return $"FontFamily: {FontFamily}, FontSize: {FontSize}, FontColor: {FontColor.Name}";
        }
    }

    class Program
    {
        static void Main()
        {
            // 1️⃣ Load Excel worksheet
            var fileInfo = new FileInfo(@"C:\Data\Sample.xlsx");
            using var package = new ExcelPackage(fileInfo);
            var ws = package.Workbook.Worksheets["Sheet1"];
            var cellStyle = ws.Cells["B2"].Style;

            // 2️⃣ Grab the target TextBox from the grid
            var gridJs = new MyGrid();
            var notesTextBox = gridJs.TextBoxes["Notes"];

            // 3️⃣ Apply font family
            notesTextBox.FontFamily = cellStyle.Font.Name;

            // 4️⃣ Apply font size
            notesTextBox.FontSize = cellStyle.Font.Size;

            // 5️⃣ Apply font colour (with safety net)
            var excelColor = cellStyle.Font.Color?.GetColor();
            notesTextBox.FontColor = excelColor ?? Color.Black;

            // Output the result for verification
            Console.WriteLine("TextBox after copying font:");
            Console.WriteLine(notesTextBox);
        }
    }
}
```

**Expected output (assuming B2 uses Arial, 12 pt, blue):**

```
TextBox after copying font:
FontFamily: Arial, FontSize: 12, FontColor: Blue
```

Run the program, open your UI, and you’ll see the “Notes” text box now mirrors the exact font styling of cell **B2**. No manual tweaking required.

---

## Preguntas frecuentes y casos límite

### ¿Qué pasa si la celda usa un color de tema en lugar de un valor RGB explícito?

EPPlus’s `GetColor()` automatically resolves theme colours to a concrete `System.Drawing.Color`. However, if you’re using an older library that only returns the theme index, you’ll need to map that index to a colour palette yourself.

### ¿Puedo copiar otros atributos de estilo (p. ej., negrita, cursiva)?

Absolutely. The `ExcelStyle.Font` object also exposes `Bold`, `Italic`, `Underline`, and `Strike`. Just set the corresponding properties on your UI control:

```csharp
notesTextBox.FontBold = cellStyle.Font.Bold;
notesTextBox.FontItalic = cellStyle.Font.Italic;
```

### ¿Qué pasa si el control de cuadrícula no expone una propiedad `FontColor`?

Most modern UI frameworks do, but if yours only accepts a CSS string, convert the `Color` to hex:

```csharp
string hex = $"#{notesTextBox.FontColor.R:X2}{notesTextBox.FontColor.G:X2}{notesTextBox.FontColor.B:X2}";
notesTextBox.Style["color"] = hex; // for web‑based grids
```

### ¿Cómo manejo varias celdas a la vez?

Loop over the desired range, fetch each cell’s style, and apply it to the corresponding text box. Remember to cache the style objects if you’re processing many rows to avoid performance hits.

---

## Consejos profesionales y errores comunes

- **Cachea el ExcelPackage** – abrir y cerrar el archivo para cada celda es costoso. Carga el libro de trabajo una vez y luego reutiliza el objeto `ExcelWorksheet`.
- **Cuidado con los colores nulos** – una celda que hereda el color predeterminado devuelve `null`. Siempre proporciona un valor de respaldo (negro o el predeterminado del control).
- **Ten en cuenta la escala DPI** – si apuntas a monitores de alta DPI, los tamaños de fuente pueden aparecer ligeramente más grandes. Ajusta usando `Graphics.DpiX` si es necesario.
- **Seguridad de hilos** – EPPlus no es seguro para hilos. Si procesas muchas hojas en paralelo, crea un `ExcelPackage` separado por hilo.

---

## Conclusión

You now know **how to copy font** from an Excel cell and **apply cell style** to any text‑box control using C#. By retrieving the cell’s `Style`, extracting its `Font` properties, and assigning them to the UI element, you preserve visual consistency without manual copying.  

The complete solution—loading the workbook, getting the cell style, and setting the textbox’s font family, size, and colour—covers the core of **use cell formatting** and demonstrates how to **set textbox font size** correctly.  

Next, try extending the example to copy background colours, borders, or even entire cell contents. If you’re working with a data‑grid library that supports rich cell rendering, you can now feed it the exact same styling information you pulled from Excel, keeping your UI and reports perfectly in sync.

Got more questions? Drop a comment or explore related topics such as “dynamic Excel‑to‑UI binding” and “theme‑aware colour conversion”. Happy coding!

---

![ejemplo de cómo copiar la fuente](placeholder-image.jpg "cómo copiar la fuente de una celda de Excel a un TextBox")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}