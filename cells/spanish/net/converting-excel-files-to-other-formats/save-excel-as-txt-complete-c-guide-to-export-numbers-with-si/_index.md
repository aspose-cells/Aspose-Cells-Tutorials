---
category: general
date: 2026-02-21
description: Guarda Excel como txt con control preciso de los dígitos significativos.
  Exporta Excel a txt en C# y establece los dígitos significativos fácilmente.
draft: false
keywords:
- save excel as txt
- export excel to txt
- set significant digits
- save workbook as text
- export numbers to txt
language: es
og_description: Guarda Excel como txt rápidamente. Aprende cómo exportar Excel a txt,
  establecer dígitos significativos y controlar la salida de texto usando C#.
og_title: Guardar Excel como txt – Exportar números con dígitos significativos en
  C#
tags:
- C#
- Aspose.Cells
- Excel automation
title: Guardar Excel como txt – Guía completa de C# para exportar números con dígitos
  significativos
url: /es/net/converting-excel-files-to-other-formats/save-excel-as-txt-complete-c-guide-to-export-numbers-with-si/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Guardar Excel como txt – Guía completa de C# para exportar números con dígitos significativos

¿Alguna vez necesitaste **save Excel as txt** pero temías que los números perdieran su precisión? No estás solo. Muchos desarrolladores se topan con un obstáculo al intentar exportar Excel a txt y terminan con demasiados decimales o con un desorden redondeado.  

En este tutorial te mostraremos una forma directa de **export Excel to txt** mientras **estableces dígitos significativos** para que la salida se vea exactamente como deseas. Al final tendrás un fragmento de C# listo para ejecutar que guarda un libro como texto, exporta números a txt y te brinda control total sobre el formato numérico.

## What You’ll Learn

- Cómo crear un nuevo workbook y escribir datos numéricos.  
- La forma correcta de **set significant digits** usando `TxtSaveOptions`.  
- Cómo **save workbook as text** y verificar el resultado.  
- Manejo de casos límite (números grandes, valores negativos, problemas de configuración regional).  
- Consejos rápidos para ajustar aún más la salida (cambio de delimitador, codificación).

### Prerequisites

- .NET 6.0 o superior (el código también funciona en .NET Framework 4.6+).  
- El paquete NuGet **Aspose.Cells** (`Install-Package Aspose.Cells`).  
- Un conocimiento básico de la sintaxis de C#—no se requiere un conocimiento profundo de interop con Excel.

> **Pro tip:** Si usas Visual Studio, habilita *nullable reference types* (`<Nullable>enable</Nullable>`) para detectar posibles errores de null temprano.

---

## Step 1: Initialize the Workbook and Write a Number

First, we need a workbook object. Think of it as the in‑memory representation of an Excel file.  

```csharp
using Aspose.Cells;
using System;

// Create a new workbook (starts with one worksheet by default)
var workbook = new Workbook();
var worksheet = workbook.Worksheets[0];

// Write a numeric value into cell A1 (row 0, column 0)
worksheet.Cells[0, 0].PutValue(12345.6789);
```

**Why this matters:**  
Creating the workbook programmatically avoids the overhead of COM interop, and `PutValue` automatically detects the data type, ensuring the cell is treated as a number—not a string.

---

## Step 2: Configure TxtSaveOptions to Control Significant Digits

The `TxtSaveOptions` class is where the magic happens. By setting `SignificantDigits`, you tell Aspose.Cells how many meaningful digits to keep when the file is written out.

```csharp
// Configure text save options – keep only 4 significant digits
var txtSaveOptions = new TxtSaveOptions
{
    // 4 significant digits means 12345.6789 becomes 12350
    SignificantDigits = 4,

    // Optional: change delimiter if you need CSV‑style output
    // Delimiter = ',',

    // Optional: force UTF‑8 encoding for broader character support
    // Encoding = System.Text.Encoding.UTF8
};
```

**Why you should set this:**  
When you **export numbers to txt**, you often need a concise representation (e.g., for reporting systems that only accept a certain precision). The `SignificantDigits` property guarantees consistent rounding regardless of the original number’s length.

---

## Step 3: Save the Workbook as a Text File

Now we write the workbook to disk using the options we just defined.

```csharp
// Define the output path – adjust to your environment
string outputPath = @"C:\Temp\Numbers.txt";

// Save the workbook as a .txt file with the configured options
workbook.Save(outputPath, txtSaveOptions);

Console.WriteLine($"Workbook saved as txt at: {outputPath}");
```

**What you’ll see:**  
Open `Numbers.txt` and you’ll get a single line:

```
12350
```

The original `12345.6789` has been rounded to **four significant digits**, exactly as requested.

---

## Step 4: Verify the Output (Optional but Recommended)

Automated tests are a great habit. Here’s a quick check you can run right after saving:

```csharp
// Read back the file to confirm the content
string fileContent = System.IO.File.ReadAllText(outputPath).Trim();

if (fileContent == "12350")
{
    Console.WriteLine("✅ Export succeeded – significant digits applied correctly.");
}
else
{
    Console.WriteLine($"⚠️ Unexpected output: {fileContent}");
}
```

Running this block will print a green checkmark if everything lines up, giving you confidence that the **save excel as txt** operation behaved as intended.

---

## Common Variations & Edge Cases

### Exporting Multiple Cells or Ranges

If you need to **export excel to txt** for a whole range, just fill more cells before saving:

```csharp
worksheet.Cells[0, 1].PutValue(0.000123456);
worksheet.Cells[0, 2].PutValue(-98765.4321);
```

The same `TxtSaveOptions` will apply the 4‑digit rule to each value, producing:

```
12350
0.0001235
-98800
```

### Changing the Delimiter

Some downstream systems expect tab‑separated values. Adjust the delimiter like so:

```csharp
txtSaveOptions.Delimiter = '\t'; // Tab character
```

Now each cell in a row appears separated by a tab.

### Handling Locale‑Specific Decimal Separators

If your audience uses commas for decimals, set the culture:

```csharp
txtSaveOptions.CultureInfo = new System.Globalization.CultureInfo("fr-FR");
```

The output will respect the locale, turning `12350` into `12 350` (space as thousands separator in French).

---

## Full Working Example (Copy‑Paste Ready)

```csharp
using Aspose.Cells;
using System;
using System.IO;

class Program
{
    static void Main()
    {
        // 1️⃣ Create workbook and write numbers
        var workbook = new Workbook();
        var sheet = workbook.Worksheets[0];
        sheet.Cells[0, 0].PutValue(12345.6789);
        sheet.Cells[0, 1].PutValue(0.000123456);
        sheet.Cells[0, 2].PutValue(-98765.4321);

        // 2️⃣ Configure save options – 4 significant digits
        var txtOptions = new TxtSaveOptions
        {
            SignificantDigits = 4,
            // Delimiter = '\t',               // Uncomment for TSV
            // Encoding = System.Text.Encoding.UTF8,
            // CultureInfo = new System.Globalization.CultureInfo("en-US")
        };

        // 3️⃣ Save to text file
        string path = Path.Combine(Environment.GetFolderPath(Environment.SpecialFolder.Desktop), "Numbers.txt");
        workbook.Save(path, txtOptions);
        Console.WriteLine($"File saved to {path}");

        // 4️⃣ Verify result (optional)
        string result = File.ReadAllText(path).Trim();
        Console.WriteLine($"File content: {result}");
    }
}
```

**Expected `Numbers.txt` content (default delimiter, 4 significant digits):**

```
12350	0.0001235	-98800
```

The tab (`\t`) appears because we left the delimiter at its default (tab) in the example; change it to a comma if you prefer CSV.

---

## Conclusion

You now know exactly **how to save Excel as txt** while controlling the number of significant digits. The steps—creating a workbook, setting `TxtSaveOptions.SignificantDigits`, and saving—are all you need to **export excel to txt** reliably.  

From here you can:

- **Export numbers to txt** for larger data sets.  
- Tweak delimiters, encoding, or culture settings to match any downstream system.  
- Combine this approach with other Aspose.Cells features (styles, formulas) before export.

Give it a spin, adjust the `SignificantDigits` to 2 or 6, and see how the output changes. The flexibility of **save workbook as text** makes it a handy tool in any data‑exchange pipeline.

---

### Related Topics You Might Explore Next

- **Export Excel to CSV** with custom column ordering.  
- **Read txt files back into a workbook** (`Workbook.Load` with `LoadOptions`).  
- **Batch processing** multiple worksheets and consolidating them into one txt file.  
- **Performance tuning** for large‑scale exports (streaming vs. in‑memory).

Feel free to drop a comment if you hit any snags, or share how you’ve customized the export for your own projects. Happy coding!  

---  

*Image: A screenshot of the generated `Numbers.txt` file showing rounded values.*  
*Alt text: “Archivo Numbers.txt que muestra 12350, 0.0001235 y -98800 después de guardar Excel como txt con 4 dígitos significativos.”*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}