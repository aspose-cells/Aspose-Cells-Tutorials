---
category: general
date: 2026-05-30
description: Cambiar el tamaño de fuente del cuadro de texto en Excel usando C#. Aprende
  a modificar la fuente del cuadro de texto de Excel rápidamente con código paso a
  paso.
draft: false
keywords:
- change textbox font size
- modify excel textbox font
language: es
og_description: Cambiar el tamaño de fuente del cuadro de texto en Excel usando C#.
  Esta guía muestra cómo modificar la fuente del cuadro de texto de Excel de forma
  segura y eficiente.
og_title: Cambiar el tamaño de fuente del cuadro de texto en Excel con C# – Tutorial
  completo
schemas:
- author: Aspose
  dateModified: '2026-05-30'
  description: Change textbox font size in Excel using C#. Learn how to modify excel
    textbox font quickly with step‑by‑step code.
  headline: Change Textbox Font Size in Excel with C# – Complete Guide
  type: TechArticle
- description: Change textbox font size in Excel using C#. Learn how to modify excel
    textbox font quickly with step‑by‑step code.
  name: Change Textbox Font Size in Excel with C# – Complete Guide
  steps:
  - name: Why this matters
    text: Opening the workbook via COM gives us a live object model—meaning any change
      we make reflects instantly in the file. Setting `Visible = false` speeds things
      up and avoids popping windows during automation.
  - name: Why we use `TextFrame2`
    text: '`TextFrame2` is the newer object model introduced with Office 2007. It
      supports advanced typographic features and is generally more reliable than the
      older `TextFrame`. Using it ensures our **change textbox font size** operation
      works across modern Excel versions.'
  - name: 1. Change *all* textboxes on a sheet
    text: '```csharp foreach (Excel.Shape s in xlWorksheet.Shapes) { if (s.Type.HasFlag(Excel.MsoShapeType.msoTextBox))
      { var tr = s.TextFrame2.TextRange; tr.Font.Name = fontName; tr.Font.Size = newSize;
      } } ```'
  - name: 2. Identify a textbox by its **Name** instead of index
    text: 'If you gave your textbox a meaningful name (e.g., “TitleBox”), you can
      fetch it directly:'
  type: HowTo
tags:
- Excel Interop
- C#
- Office Automation
title: Cambiar el tamaño de fuente del cuadro de texto en Excel con C# – Guía completa
url: /es/net/excel-shape-text-modifications/change-textbox-font-size-in-excel-with-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cambiar el tamaño de fuente del cuadro de texto en Excel con C# – Guía completa

¿Necesitas **cambiar el tamaño de fuente del cuadro de texto** en una hoja de Excel desde C#? Estás en el lugar correcto. Ya sea que estés generando informes, construyendo un panel de control o simplemente ajustando una plantilla, modificar la apariencia de un cuadro de texto puede hacer que tu hoja de cálculo se vea mucho más profesional.

En este tutorial también **modificaremos la fuente del cuadro de texto en Excel** más allá del tamaño: familia de fuente, negrita e incluso el manejo de múltiples formas. Al final tendrás un fragmento listo‑para‑ejecutar que cubre cada rincón del proceso, desde abrir el libro hasta limpiar los objetos COM. Sin rodeos, solo código práctico que puedes incorporar a tu proyecto hoy.

## Requisitos previos — Lo que necesitarás

Antes de sumergirnos, asegúrate de que tienes lo siguiente en tu máquina:

| Requisito | Por qué es importante |
|-----------|-----------------------|
| **.NET 6+** (o .NET Framework 4.7.2+) | Proporciona el compilador y tiempo de ejecución de C#. |
| **Microsoft.Office.Interop.Excel** paquete NuGet | Nos brinda los tipos de interop COM necesarios para comunicarnos con Excel. |
| **Excel instalado** (cualquier versión reciente) | La capa Interop solo funciona cuando la aplicación Office está presente. |
| **Conocimientos básicos de C#** | Podrás seguir el tutorial sin problemas, pero explicaremos cada línea. |

Si falta alguno de estos, detente ahora e instálalo; el resto de la guía asume que están disponibles.

## Paso 1: Configurar el proyecto e importar los espacios de nombres

Lo primero: crea una nueva aplicación de consola (o intégrala en una existente) y agrega el espacio de nombres de interop.

```csharp
using System;
using Excel = Microsoft.Office.Interop.Excel;

namespace ExcelTextboxDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // We'll call the helper method that does the heavy lifting.
            ChangeTextboxFontSize(@"C:\Temp\Sample.xlsx", "Sheet1", 0, 14, "Calibri");
        }
    }
}
```

> **Consejo profesional:** Si apuntas a .NET 6+, agrega el paquete `Microsoft.Office.Interop.Excel` mediante `dotnet add package Microsoft.Office.Interop.Excel`. Así garantizas que el alias `Excel` se resuelva correctamente.

## Paso 2: Abrir el libro y obtener la hoja de trabajo objetivo

Ahora debemos iniciar Excel, abrir el archivo y apuntar a la hoja que contiene el cuadro de texto. Envolver esto en un bloque `try/finally` garantiza que los objetos COM se liberen incluso si algo falla.

```csharp
static void ChangeTextboxFontSize(string workbookPath,
                                  string sheetName,
                                  int textboxIndex,
                                  double newSize,
                                  string fontName)
{
    Excel.Application xlApp = null;
    Excel.Workbook xlWorkbook = null;
    Excel.Worksheet xlWorksheet = null;

    try
    {
        xlApp = new Excel.Application
        {
            // Keep Excel hidden; set to true if you want to watch the changes.
            Visible = false,
            DisplayAlerts = false
        };

        xlWorkbook = xlApp.Workbooks.Open(workbookPath);
        xlWorksheet = xlWorkbook.Worksheets[sheetName] as Excel.Worksheet;
        if (xlWorksheet == null)
            throw new ArgumentException($"Worksheet '{sheetName}' not found.");
```

### Por qué es importante

Abrir el libro vía COM nos da un modelo de objetos en vivo—lo que significa que cualquier cambio se refleja instantáneamente en el archivo. Establecer `Visible = false` acelera el proceso y evita que se abran ventanas durante la automatización.

## Paso 3: Recuperar la forma del cuadro de texto

Excel trata los cuadros de texto como objetos `Shape` dentro de la colección `Shapes`, no como una colección dedicada `TextBox`. Por eso el código a continuación se ve un poco diferente al fragmento que quizá hayas visto en línea.

```csharp
        // Excel stores all drawing objects (including textboxes) in the Shapes collection.
        Excel.Shapes shapes = xlWorksheet.Shapes;

        // Guard against an out‑of‑range index.
        if (textboxIndex < 0 || textboxIndex >= shapes.Count)
            throw new IndexOutOfRangeException("Textbox index is out of range.");

        // Grab the specific shape; we assume it’s a textbox.
        Excel.Shape textboxShape = shapes.Item(textboxIndex + 1); // COM collections are 1‑based.
        if (!textboxShape.Type.HasFlag(Excel.MsoShapeType.msoTextBox))
            throw new InvalidOperationException("Selected shape is not a textbox.");
```

> **Cuidado:** La colección `Shapes` está basada en 1, así que añadimos `+1` al `textboxIndex` basado en 0 que pasas. Olvidar esto genera errores de “índice fuera de rango” que pueden ser frustrantes de depurar.

## Paso 4: Cambiar el tamaño de fuente del cuadro de texto (y el nombre)

Aquí es donde finalmente **cambiamos el tamaño de fuente del cuadro de texto**. La propiedad `TextFrame2` nos da acceso a las opciones de formato de texto enriquecido, que incluyen `Font.Name` y `Font.Size`.

```csharp
        // Access the text range inside the textbox.
        Excel.TextRange2 textRange = textboxShape.TextFrame2.TextRange;

        // Change the font name – this also “modifies excel textbox font”.
        textRange.Font.Name = fontName;

        // Change the font size – the core of our tutorial.
        textRange.Font.Size = newSize;

        // Optional: make the text bold for extra emphasis.
        // textRange.Font.Bold = Microsoft.Office.Core.MsoTriState.msoTrue;
```

### Por qué usamos `TextFrame2`

`TextFrame2` es el modelo de objetos más reciente introducido con Office 2007. Soporta funciones tipográficas avanzadas y es generalmente más fiable que el antiguo `TextFrame`. Usarlo asegura que nuestra operación de **cambiar el tamaño de fuente del cuadro de texto** funcione en versiones modernas de Excel.

## Paso 5: Guardar, limpiar y verificar

Después de ajustar la fuente, necesitamos persistir los cambios y liberar cada referencia COM. Omitir la limpieza puede dejar procesos de Excel huérfanos ejecutándose en segundo plano.

```csharp
        // Save the workbook – you can also use SaveAs to create a copy.
        xlWorkbook.Save();

        Console.WriteLine($"Successfully changed textbox font size to {newSize} pt and font to '{fontName}'.");
    }
    catch (Exception ex)
    {
        Console.Error.WriteLine($"Error: {ex.Message}");
    }
    finally
    {
        // Release COM objects in reverse order of creation.
        if (xlWorksheet != null) System.Runtime.InteropServices.Marshal.ReleaseComObject(xlWorksheet);
        if (xlWorkbook != null)
        {
            xlWorkbook.Close(false);
            System.Runtime.InteropServices.Marshal.ReleaseComObject(xlWorkbook);
        }
        if (xlApp != null)
        {
            xlApp.Quit();
            System.Runtime.InteropServices.Marshal.ReleaseComObject(xlApp);
        }

        // Force garbage collection to clean up any remaining RCWs.
        GC.Collect();
        GC.WaitForPendingFinalizers();
    }
}
```

> **Consejo profesional:** Si necesitas **modificar la fuente del cuadro de texto en Excel** en muchas hojas, envuelve la lógica interna en un bucle que itere sobre `Workbook.Worksheets`. Sólo recuerda reiniciar `textboxIndex` para cada hoja.

## Manejo de casos especiales — Múltiples cuadros de texto y formas ausentes

Las hojas de cálculo del mundo real rara vez contienen solo un cuadro de texto. A continuación tienes dos estrategias rápidas que puedes adoptar sin reescribir todo el método.

### 1. Cambiar *todos* los cuadros de texto en una hoja

```csharp
foreach (Excel.Shape s in xlWorksheet.Shapes)
{
    if (s.Type.HasFlag(Excel.MsoShapeType.msoTextBox))
    {
        var tr = s.TextFrame2.TextRange;
        tr.Font.Name = fontName;
        tr.Font.Size = newSize;
    }
}
```

### 2. Identificar un cuadro de texto por su **Nombre** en lugar de por índice

Si le asignaste a tu cuadro de texto un nombre significativo (p. ej., “TitleBox”), puedes obtenerlo directamente:

```csharp
Excel.Shape namedBox = xlWorksheet.Shapes.Item("TitleBox");
namedBox.TextFrame2.TextRange.Font.Size = newSize;
```

Ambos enfoques te permiten **modificar la fuente del cuadro de texto en Excel** con precisión, sin importar cómo esté estructurado el libro.

## Visión general visual (Opcional)

Si prefieres una pista visual rápida, imagina el siguiente diagrama:

![Captura de pantalla que muestra una hoja de Excel con un cuadro de texto resaltado – demuestra cómo cambiar el tamaño de fuente del cuadro de texto](change-textbox-font-size.png)

*Texto alternativo:* *cambiar tamaño de fuente del cuadro de texto en Excel – cuadro de texto resaltado listo para la modificación de la fuente.*

## Ejemplo completo funcional

Juntando todo, aquí tienes un único archivo que puedes copiar‑pegar en un proyecto de consola y ejecutar de inmediato (solo actualiza la ruta del archivo y el nombre de la hoja).

```csharp
using System;
using Excel = Microsoft.Office.Interop.Excel;

namespace ExcelTextboxDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Ajusta estos parámetros a tu entorno.
            string workbookPath = @"C:\Temp\Sample.xlsx";
            string sheetName = "Sheet1";
            int textboxIndex = 0;          // Primer cuadro de texto en la hoja.
            double newFontSize = 14;       // Tamaño de fuente deseado.
            string newFontName = "Calibri";

            ChangeTextboxFontSize(workbookPath, sheetName, textboxIndex, newFontSize, newFontName);
        }

        static void ChangeTextboxFontSize(string workbookPath,
                                          string sheetName,
                                          int textboxIndex,
                                          double newSize,
                                          string fontName)
        {
            Excel.Application xlApp = null;
            Excel.Workbook xlWorkbook = null;
            Excel.Worksheet xlWorksheet = null;

            try
            {
                xlApp = new Excel.Application { Visible = false, DisplayAlerts = false };
                xlWorkbook = xlApp.Workbooks.Open(workbookPath);
                xlWorksheet = xlWorkbook.Worksheets[sheetName] as Excel.Worksheet;

                if (xlWorksheet == null)


## ¿Qué deberías aprender a continuación?

- [Changing Font Size in Excel](/cells/english/net/working-with-fonts-in-excel/changing-font-size/)
- [How to Customize Font Size in Excel Cells Using Aspose.Cells .NET | Complete Guide](/cells/english/net/formatting/customize-font-size-excel-aspose-cells-dotnet/)
- [How to Set Font Styles in Excel Using Aspose.Cells for .NET (Step-by-Step Guide)](/cells/english/net/formatting/aspose-cells-dotnet-set-font-styles-excel/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}