---
category: general
date: 2026-06-08
description: Analiza la fecha de era japonesa en C# usando Aspose.Cells. Aprende cómo
  CultureInfo ja-JP y el formato de era japonesa permiten una conversión precisa de
  fechas en Excel.
draft: false
keywords:
- parse japanese era date
- Aspose.Cells
- CultureInfo ja-JP
- Japanese era format
- Excel date conversion
- C# DateTime parsing
language: es
og_description: Analiza rápidamente fechas de era japonesa en C#. Este tutorial muestra
  cómo CultureInfo ja-JP y Aspose.Cells convierten cadenas de era en objetos DateTime
  adecuados.
og_title: Analizar fecha de era japonesa en C# – Guía de Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: Parse Japanese era date in C# using Aspose.Cells. Learn how CultureInfo
    ja-JP and Japanese era format enable accurate Excel date conversion.
  headline: Parse Japanese Era Date in C# with Aspose.Cells – Full Guide
  type: TechArticle
- description: Parse Japanese era date in C# using Aspose.Cells. Learn how CultureInfo
    ja-JP and Japanese era format enable accurate Excel date conversion.
  name: Parse Japanese Era Date in C# with Aspose.Cells – Full Guide
  steps:
  - name: 5.1 Invalid or Empty Strings
    text: '```csharp string maybeDate = workbook.Worksheets[0].Cells["B1"].GetString();
      // could be empty if (string.IsNullOrWhiteSpace(maybeDate)) { Console.WriteLine("Cell
      B1 is empty – skipping."); } else { // Attempt to parse; catch format exceptions
      try { DateTime dt = DateTime.Parse(maybeDate, new Cultur'
  - name: 5.2 Older Eras (Showa, Taisho)
    text: 'The same `CultureInfo ja-JP` works for older eras automatically:'
  - name: 5.3 Using `DateTime.ParseExact` for Strict Validation
    text: 'If you want to enforce the exact Japanese era pattern, use a custom format
      string:'
  type: HowTo
- questions:
  - answer: Yes. As long as the workbook’s `Settings.CultureInfo` is set to `ja-JP`
      *before* you call `GetDateTime()`, Aspose.Cells will interpret the existing
      strings correctly.
    question: Does this work with .xlsx files that already contain era dates?
  - answer: The parsing returns a `DateTime` with `Kind = Unspecified`. If you need
      UTC or local time, apply `DateTime.SpecifyKind` or convert after parsing.
    question: What about time zones?
  - answer: Absolutely. Loop through the desired range and call `GetDateTime()` on
      each cell—just remember to handle exceptions for malformed entries.
    question: Can I parse multiple cells at once?
  type: FAQPage
tags:
- C#
- Excel
- DateTime
- Localization
title: Analizar fechas de era japonesa en C# con Aspose.Cells – Guía completa
url: /es/net/excel-custom-number-date-formatting/parse-japanese-era-date-in-c-with-aspose-cells-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Analizar fechas de era japonesa en C# con Aspose.Cells – Guía completa

¿Alguna vez necesitaste **parse japanese era date** cadenas directamente desde una hoja de Excel? Tal vez estés extrayendo datos de un sistema heredado que aún usa “令和3年5月12日” y quieras un `DateTime` limpio para generar informes. En este tutorial recorreremos un ejemplo completo, listo para ejecutar, que convierte esas cadenas con formato de era en fechas C# correctas, sin conjeturas.

Usaremos **Aspose.Cells**, la poderosa biblioteca .NET para manipular Excel, junto con la configuración **CultureInfo ja-JP** que sabe leer eras japonesas. Al final tendrás un fragmento reutilizable que maneja “令和”, “平成”, y incluso eras más antiguas sin esfuerzo.

## Requisitos previos

- .NET 6.0 o posterior (el código también funciona en .NET Framework 4.6+)
- Aspose.Cells para .NET (puedes obtener un paquete de prueba gratuito de NuGet: `Install-Package Aspose.Cells`)
- Conocimientos básicos de C#—nada complicado, basta con una aplicación de consola
- Un IDE de tu elección (Visual Studio, Rider, VS Code, etc.)

Eso es todo. Sin servicios adicionales, sin analizadores de terceros obscuros.

## Paso 1: Configurar el proyecto y agregar Aspose.Cells

Primero, crea un nuevo proyecto de consola:

```bash
dotnet new console -n JapaneseEraParser
cd JapaneseEraParser
dotnet add package Aspose.Cells
```

Ahora abre **Program.cs** y agrega los espacios de nombres requeridos:

```csharp
using System;
using System.Globalization;
using Aspose.Cells;
```

> **Pro tip:** Si usas Visual Studio, el IDE sugerirá agregar las declaraciones `using` automáticamente después de escribir los nombres de clase.

## Paso 2: Crear un Workbook y aplicar la cultura japonesa

La clave para **parse japanese era date** correctamente es indicar a Aspose.Cells qué cultura usar. Configurar `CultureInfo` a `ja-JP` activa el análisis sensible a eras.

```csharp
// Step 2: Initialize a new workbook and set Japanese culture
Workbook workbook = new Workbook();
workbook.Settings.CultureInfo = new CultureInfo("ja-JP");
```

¿Por qué importa esto? El calendario japonés tiene múltiples eras (p. ej., *Reiwa* (令和), *Heisei* (平成)). El objeto `CultureInfo` contiene un `JapaneseCalendar` que conoce las fechas de inicio de cada era, de modo que cualquier cadena que siga el formato de era japonesa pueda interpretarse correctamente.

## Paso 3: Escribir una cadena de fecha de era japonesa en una celda

Vamos a colocar una fecha de era de ejemplo en la celda **A1**. Siéntete libre de cambiar la cadena para probar diferentes eras.

```csharp
// Step 3: Put a Japanese era date string into A1
string japaneseDate = "令和3年5月12日"; // Reiwa 3, May 12, 2021
workbook.Worksheets[0].Cells["A1"].PutValue(japaneseDate);
```

Si prefieres trabajar con un libro existente, puedes cargarlo con `new Workbook("path/to/file.xlsx")` y omitir el paso de creación.

## Paso 4: Recuperar el valor como un objeto C# DateTime

Ahora ocurre la magia. Al llamar a `GetDateTime()`, Aspose.Cells lee la celda usando el `CultureInfo` previamente establecido y devuelve un `DateTime` correcto.

```csharp
// Step 4: Parse the cell value into a DateTime
DateTime parsedDate = workbook.Worksheets[0].Cells["A1"].GetDateTime();
Console.WriteLine($"Parsed DateTime: {parsedDate:yyyy-MM-dd}");
```

**Salida esperada**

```
Parsed DateTime: 2021-05-12
```

Ese es todo el flujo de **parse japanese era date**—cuatro líneas concisas de código.

## Paso 5: Manejo de casos límite y eras alternativas

Los datos del mundo real no siempre están limpios. Aquí tienes algunos escenarios que podrías encontrar y cómo manejarlos.

### 5.1 Cadenas inválidas o vacías

```csharp
string maybeDate = workbook.Worksheets[0].Cells["B1"].GetString(); // could be empty
if (string.IsNullOrWhiteSpace(maybeDate))
{
    Console.WriteLine("Cell B1 is empty – skipping.");
}
else
{
    // Attempt to parse; catch format exceptions
    try
    {
        DateTime dt = DateTime.Parse(maybeDate, new CultureInfo("ja-JP"));
        Console.WriteLine($"B1 parsed as {dt:yyyy-MM-dd}");
    }
    catch (FormatException)
    {
        Console.WriteLine($"Unable to parse '{maybeDate}' as a Japanese era date.");
    }
}
```

### 5.2 Eras más antiguas (Showa, Taisho)

El mismo `CultureInfo ja-JP` funciona automáticamente para eras más antiguas:

```csharp
string showaDate = "昭和45年12月31日"; // Showa 45 = 1970-12-31
DateTime showaParsed = DateTime.Parse(showaDate, new CultureInfo("ja-JP"));
Console.WriteLine(showaParsed.ToString("yyyy-MM-dd")); // 1970-12-31
```

### 5.3 Usar `DateTime.ParseExact` para validación estricta

Si deseas imponer el patrón exacto de era japonesa, usa una cadena de formato personalizada:

```csharp
string pattern = "ggggy年M月d日"; // gggg = era name, y = year in era
DateTime strictDate = DateTime.ParseExact(japaneseDate, pattern, new CultureInfo("ja-JP"));
Console.WriteLine(strictDate); // 2021-05-12 00:00:00
```

Este enfoque lanza una `FormatException` cuando la cadena se desvía, lo que puede ser útil para verificaciones de calidad de datos.

## Ejemplo completo funcionando

A continuación tienes el programa completo que puedes copiar‑pegar en **Program.cs** y ejecutar.

```csharp
using System;
using System.Globalization;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Create workbook and set Japanese culture
        Workbook workbook = new Workbook();
        workbook.Settings.CultureInfo = new CultureInfo("ja-JP");

        // 2️⃣ Insert a Japanese era date string
        string japaneseDate = "令和3年5月12日";
        workbook.Worksheets[0].Cells["A1"].PutValue(japaneseDate);

        // 3️⃣ Parse the cell value into DateTime
        DateTime parsedDate = workbook.Worksheets[0].Cells["A1"].GetDateTime();
        Console.WriteLine($"Parsed DateTime: {parsedDate:yyyy-MM-dd}");

        // 4️⃣ Demonstrate handling an older era
        string showaDate = "昭和45年12月31日";
        DateTime showaParsed = DateTime.Parse(showaDate, new CultureInfo("ja-JP"));
        Console.WriteLine($"Showa parsed: {showaParsed:yyyy-MM-dd}");

        // 5️⃣ Strict parsing with ParseExact
        string pattern = "gggy年M月d日";
        try
        {
            DateTime strict = DateTime.ParseExact(japaneseDate, pattern, new CultureInfo("ja-JP"));
            Console.WriteLine($"Strict parse: {strict:yyyy-MM-dd}");
        }
        catch (FormatException ex)
        {
            Console.WriteLine($"Strict parse failed: {ex.Message}");
        }
    }
}
```

Ejecuta con `dotnet run` y deberías ver:

```
Parsed DateTime: 2021-05-12
Showa parsed: 1970-12-31
Strict parse: 2021-05-12
```

¡Listo—**parse japanese era date** completado, y tienes una plantilla para cualquier era que puedas encontrar!

![Flujo de análisis de fecha de era japonesa – muestra creación de libro, configuración de cultura, escritura de celda y llamada GetDateTime](parse-japanese-era-date.png "Diagrama que ilustra cómo analizar fechas de era japonesa usando Aspose.Cells y CultureInfo ja-JP")

## Preguntas frecuentes respondidas

- **¿Esto funciona con archivos .xlsx que ya contienen fechas de era?**  
  Sí. Mientras la `Settings.CultureInfo` del libro esté establecida en `ja-JP` *antes* de llamar a `GetDateTime()`, Aspose.Cells interpretará correctamente las cadenas existentes.

- **¿Qué pasa con las zonas horarias?**  
  El análisis devuelve un `DateTime` con `Kind = Unspecified`. Si necesitas UTC o hora local, aplica `DateTime.SpecifyKind` o convierte después del análisis.

- **¿Puedo analizar varias celdas a la vez?**  
  Absolutamente. Recorre el rango deseado y llama a `GetDateTime()` en cada celda—solo recuerda manejar excepciones para entradas mal formadas.

## Conclusión

Hemos cubierto todo lo que necesitas para **parse japanese era date** cadenas en C# usando Aspose.Cells y el `CultureInfo ja-JP` incorporado. Desde configurar el libro, escribir cadenas con formato de era, obtener un `DateTime` limpio, hasta manejar casos límite como eras antiguas y validación estricta—esta guía te brinda una solución lista para producción.

A continuación, podrías explorar **Excel date conversion** para fechas numéricas en serie, o profundizar en **C# DateTime parsing** con calendarios personalizados para otras localidades. El mismo patrón funciona para el calendario budista tailandés, el calendario hebreo y más—solo cambia el `CultureInfo`.

¿Tienes alguna variante que te esté dando problemas? Deja un comentario y solucionemos juntos. ¡Feliz codificación!

## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y funcionales con explicaciones paso a paso para ayudarte a dominar funciones adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Cómo implementar validación de fechas en .NET usando Aspose.Cells: Guía completa](/cells/english/net/data-validation/implement-date-validation-net-aspose-cells/)
- [Cambiar el sistema de fechas de Excel a 1904 usando Aspose.Cells .NET](/cells/english/net/calculation-engine/change-excel-date-system-aspose-cells-net/)
- [Convertir eficientemente Excel a PDF con formatos de fecha personalizados usando Aspose.Cells para Java](/cells/english/java/workbook-operations/render-excel-custom-date-formats-pdf-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}