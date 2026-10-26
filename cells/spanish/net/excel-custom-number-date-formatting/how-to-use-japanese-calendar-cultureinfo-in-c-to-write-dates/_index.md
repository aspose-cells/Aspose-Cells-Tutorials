---
category: general
date: 2026-10-26
description: Aprende a usar CultureInfo del calendario japonés en C# al analizar fechas
  de era e insertarlas en una hoja de Excel con NPOI.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- use japanese calendar cultureinfo
- japanese era date parsing
- cultureinfo with japanese calendar
- datetime parse with cultureinfo
- npoi excel cultureinfo
language: es
lastmod: 2026-10-26
og_description: Utiliza CultureInfo del calendario japonés en C# para analizar fechas
  de la era Reiwa y escribirlas en una hoja de Excel. Código completo y ejecutable
  con explicaciones.
og_image_alt: Screenshot of C# code parsing a Japanese era date and inserting it into
  an Excel cell
og_title: Usar CultureInfo del calendario japonés en C# – ejemplo completo de Excel
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Learn how to use Japanese calendar CultureInfo in C# when parsing era
    dates and inserting them into an Excel worksheet with NPOI.
  headline: How to use Japanese calendar CultureInfo in C# to write dates to Excel
  type: TechArticle
tags:
- C#
- CultureInfo
- Excel
- NPOI
- Internationalization
title: Cómo usar CultureInfo del calendario japonés en C# para escribir fechas en
  Excel
url: /es/net/excel-custom-number-date-formatting/how-to-use-japanese-calendar-cultureinfo-in-c-to-write-dates/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo usar CultureInfo del calendario japonés en C# para escribir fechas en Excel

Si necesitas **usar CultureInfo del calendario japonés** al trabajar con fechas en C#, esta guía te muestra exactamente cómo. Aprenderás a analizar una cadena de fecha que contiene un nombre de era japonesa (por ejemplo, *Reiwa 2/5/1*) y luego escribir el `DateTime` resultante en la primera celda de una hoja de cálculo de Excel usando la biblioteca NPOI.

Analizar fechas basadas en eras sin el `CultureInfo` correcto conduce a `FormatException` o valores de mes/día incorrectos. Al configurar `CultureInfo` al calendario japonés, garantizas que el tiempo de ejecución de .NET interprete la era correctamente y que el valor que almacenes en Excel coincida con la notación japonesa original.

En este tutorial aprenderás:

* Crear un objeto `CultureInfo` que use el calendario japonés.
* Analizar una cadena de fecha de era japonesa con `DateTime.Parse`.
* Insertar el `DateTime` analizado en una celda de hoja de cálculo NPOI.
* Ver el programa completo, ejecutable y la salida esperada.

> **Requisitos previos** – .NET 6.0+ (o .NET Core 3.1+), el paquete NuGet **NPOI**, y una comprensión básica de C# y el manejo de archivos de Excel.

---

## Lo que necesitarás

| Item | Reason |
|------|--------|
| **.NET SDK** (6.0 or later) | Proporciona el tiempo de ejecución y las bibliotecas para `CultureInfo`. |
| **NPOI** (`NPOI` NuGet package) | Permite crear y manipular archivos de Excel sin necesidad de Office instalado. |
| **Visual Studio Code**, **Visual Studio**, or any C# IDE | Para compilar y ejecutar el ejemplo. |
| **Japanese era date string** (e.g., `"Reiwa 2/5/1"`) | Demuestra el uso del calendario japonés. |

---

## Paso 1: Instalar NPOI

Abre una terminal en la carpeta de tu proyecto y ejecuta:

```bash
dotnet add package NPOI --version 2.6.1
```

El paquete proporciona los tipos `IWorkbook`, `ISheet` y `ICell` que se usarán más adelante.

---

## Paso 2: Crear un CultureInfo que use el calendario japonés

El calendario japonés es un calendario basado en eras. Debes solicitar la variante *Japanese* de la configuración regional `ja-JP` y establecer explícitamente el calendario a `JapaneseCalendar`.

```csharp
using System;
using System.Globalization;

// Create a CultureInfo based on Japanese locale and switch its calendar.
CultureInfo japaneseCulture = new CultureInfo("ja-JP");
japaneseCulture.DateTimeFormat.Calendar = new JapaneseCalendar();
```

> **Por qué es importante** – La cultura predeterminada `ja-JP` usa el calendario gregoriano. Reasignar la propiedad `Calendar` asegura que los nombres de era como *Reiwa* sean reconocidos durante el análisis.

---

## Paso 3: Analizar una cadena de fecha de era japonesa

Ahora que el `CultureInfo` está configurado, puedes analizar de forma segura una cadena que contiene un nombre de era.

```csharp
// Example Japanese era date: Reiwa 2 (2020) year, May 1st.
string eraDate = "Reiwa 2/5/1";

// Parse using the Japanese CultureInfo created earlier.
DateTime reiwaDate = DateTime.Parse(eraDate, japaneseCulture);
Console.WriteLine($"Parsed DateTime (UTC): {reiwaDate:u}");
```

**Salida**

```
Parsed DateTime (UTC): 2020-05-01 00:00:00Z
```

El método `Parse` interpreta *Reiwa 2* como el año gregoriano 2020, mes 5, día 1.

### Caso límite: manejo de eras inválidas

Si un usuario proporciona una era no soportada (p.ej., `"Heisei 31/4/30"` después de que terminó la era Heisei), `DateTime.Parse` lanza una `FormatException`. Envuelve la llamada en un bloque try‑catch para proporcionar un mensaje de error amigable:

```csharp
try
{
    DateTime parsed = DateTime.Parse(input, japaneseCulture);
}
catch (FormatException)
{
    Console.Error.WriteLine($"'{input}' is not a valid Japanese era date.");
}
```

---

## Paso 4: Escribir el DateTime analizado en una hoja de cálculo de Excel

Con el objeto `DateTime` listo, puedes almacenarlo en una celda de Excel. NPOI formatea automáticamente los valores `DateTime` como fechas de Excel.

```csharp
using NPOI.SS.UserModel;
using NPOI.XSSF.UserModel;
using System.IO;

// Create a new workbook and a sheet.
IWorkbook workbook = new XSSFWorkbook();
ISheet sheet = workbook.CreateSheet("Japanese Dates");

// Write the DateTime into cell A1 (row 0, column 0).
IRow row = sheet.CreateRow(0);
ICell cell = row.CreateCell(0);
cell.SetCellValue(reiwaDate);

// Optionally apply a date style that shows the era (Excel does not have a built‑in era format,
// so we keep the Gregorian representation).
ICellStyle dateStyle = workbook.CreateCellStyle();
short dateFormatId = workbook.CreateDataFormat().GetFormat("yyyy-mm-dd");
dateStyle.DataFormat = dateFormatId;
cell.CellStyle = dateStyle;

// Save the workbook to a file.
using (FileStream fs = new FileStream("JapaneseEraDate.xlsx", FileMode.Create, FileAccess.Write))
{
    workbook.Write(fs);
}
Console.WriteLine("Excel file 'JapaneseEraDate.xlsx' created successfully.");
```

**Resultado** – Al abrir *JapaneseEraDate.xlsx* se muestra la fecha **2020‑05‑01** en la celda A1.

### ¿Por qué usar NPOI?

*Funciona en cualquier plataforma* (Windows, Linux, macOS) y **no** requiere Microsoft Office. Esto hace que la solución sea adecuada para pipelines de CI, contenedores Docker o procesamiento del lado del servidor.

---

## Paso 5: Programa completo y ejecutable

Juntando todo, aquí tienes una aplicación de consola completa que demuestra todo el flujo:

```csharp
// File: Program.cs
using System;
using System.Globalization;
using System.IO;
using NPOI.SS.UserModel;
using NPOI.XSSF.UserModel;

class Program
{
    static void Main()
    {
        // 1️⃣ Configure CultureInfo for the Japanese calendar.
        CultureInfo japaneseCulture = new CultureInfo("ja-JP");
        japaneseCulture.DateTimeFormat.Calendar = new JapaneseCalendar();

        // 2️⃣ Parse a Japanese era date string.
        string eraDate = "Reiwa 2/5/1";
        DateTime reiwaDate;
        try
        {
            reiwaDate = DateTime.Parse(eraDate, japaneseCulture);
            Console.WriteLine($"Parsed DateTime: {reiwaDate:u}");
        }
        catch (FormatException)
        {
            Console.Error.WriteLine($"'{eraDate}' is not a valid Japanese era date.");
            return;
        }

        // 3️⃣ Create an Excel workbook and write the date.
        IWorkbook workbook = new XSSFWorkbook();
        ISheet sheet = workbook.CreateSheet("Japanese Dates");
        IRow row = sheet.CreateRow(0);
        ICell cell = row.CreateCell(0);
        cell.SetCellValue(reiwaDate);

        // Apply a simple Gregorian date format.
        ICellStyle style = workbook.CreateCellStyle();
        short fmt = workbook.CreateDataFormat().GetFormat("yyyy-mm-dd");
        style.DataFormat = fmt;
        cell.CellStyle = style;

        // 4️⃣ Save the workbook.
        const string fileName = "JapaneseEraDate.xlsx";
        using (FileStream fs = new FileStream(fileName, FileMode.Create, FileAccess.Write))
        {
            workbook.Write(fs);
        }

        Console.WriteLine($"Excel file '{fileName}' created successfully.");
    }
}
```

**Cómo ejecutar**

```bash
dotnet run
```

Después de la ejecución, encontrarás `JapaneseEraDate.xlsx` en la carpeta del proyecto con la fecha analizada correctamente.

---

## Errores comunes y consejos de buenas prácticas

| Pitfall | Fix / Recommendation |
|---------|----------------------|
| Forgetting to set `japaneseCulture.DateTimeFormat.Calendar` | Siempre asigna una instancia de `JapaneseCalendar`; de lo contrario el nombre de era no será reconocido. |
| Using `DateTime.TryParse` without the custom `CultureInfo` | Pasa el mismo `japaneseCulture` a `TryParse` para mantener el comportamiento consistente. |
| Expecting Excel to display the era name | Los formatos de fecha incorporados de Excel son solo gregorianos. Si necesitas que se muestre la era, guarda la cadena original en una columna separada o crea un formato de texto personalizado. |
| Not disposing the `FileStream` | Usa un bloque `using` (como se muestra) para asegurar que el manejador del archivo se libere rápidamente. |
| Mixing `CultureInfo` objects across threads | `CultureInfo` es seguro para hilos en operaciones de solo lectura, pero evita modificar su propiedad `Calendar` después de la configuración inicial. |

---

## Conclusión

Ahora sabes cómo **usar CultureInfo del calendario japonés** en C# para analizar con precisión fechas de era japonesa y escribir el `DateTime` resultante en una hoja de cálculo de Excel con NPOI. El ejemplo completo cubre configuración, análisis, manejo de errores y salida a Excel, dándote una base sólida para cualquier escenario de informes internacionalizados o intercambio de datos.

A continuación, podrías explorar:

* **Formatear fechas con texto personalizado** para conservar el nombre de la era dentro de Excel.
* **Leer fechas desde Excel** usando `cell.DateCellValue` respetando el calendario japonés.
* **Aplicar la misma técnica** a otros calendarios basados en eras (p.ej., calendario budista tailandés) sustituyendo `JapaneseCalendar` por la subclase `Calendar` correspondiente.

¡Siéntete libre de experimentar con diferentes cadenas de era, conjuntos de datos más grandes o integrar esta lógica en APIs ASP.NET Core que generen informes de Excel al vuelo! ¡Feliz codificación!

## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y funcionales con explicaciones paso a paso para ayudarte a dominar características adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Crear libro de Excel con fechas del calendario japonés – Guía completa](/cells/english/net/excel-custom-number-date-formatting/create-excel-workbook-with-japanese-calendar-dates-full-guid/)
- [Analizar fechas de era japonesa en Excel – Guía completa para desarrolladores C#](/cells/english/net/data-loading-and-parsing/parse-japanese-era-dates-in-excel-full-guide-for-c-developer/)
- [Cómo crear un libro de Excel y analizar fechas japonesas en C#](/cells/english/net/excel-custom-number-date-formatting/how-to-create-excel-workbook-and-parse-japanese-dates-in-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}