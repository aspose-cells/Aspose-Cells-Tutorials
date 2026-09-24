---
category: general
date: 2026-09-24
description: Analizar DateTime con el reinado del emperador japonés usando Aspose.Cells
  en C#. Habilitar el calendario de eras japonesas, escribir cadenas de era y obtener
  valores DateTime precisos.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- Parse DateTime with Japanese Emperor Reign
- Aspose.Cells
- C# date parsing
- Japanese era calendar
- Workbook Settings
- DateTimeValue
language: es
lastmod: 2026-09-24
og_description: Analizar DateTime con el reinado del emperador japonés usando Aspose.Cells
  en C#. Este tutorial muestra cómo habilitar el calendario de eras japonesas, escribir
  cadenas de era y leer de nuevo un DateTime correcto.
og_image_alt: Screenshot of C# code parsing a Japanese era date with Aspose.Cells
og_title: Analizar DateTime con el reinado del emperador japonés usando Aspose.Cells
  – Guía C#
schemas:
- author: Aspose
  dateModified: '2026-09-24'
  description: Parse DateTime with Japanese Emperor Reign using Aspose.Cells in C#.
    Enable the Japanese era calendar, write era strings, and retrieve accurate DateTime
    values.
  headline: Parse DateTime with Japanese Emperor Reign using Aspose.Cells
  type: TechArticle
- description: Parse DateTime with Japanese Emperor Reign using Aspose.Cells in C#.
    Enable the Japanese era calendar, write era strings, and retrieve accurate DateTime
    values.
  name: Parse DateTime with Japanese Emperor Reign using Aspose.Cells
  steps:
  - name: Multiple era formats
    text: 'Aspose.Cells recognises several era representations:'
  - name: Invalid strings
    text: 'When the string cannot be parsed (e.g., `"令和99年13月40日"`), `DateTimeValue`
      returns `DateTime.MinValue`. You can check for this condition:'
  - name: Disabling the feature
    text: 'If you later need to store raw era strings without conversion, set the
      flag back to `false`:'
  - name: Performance tip
    text: Enabling the era calendar adds a small overhead to every `PutValue` call
      that involves strings. If you only parse a handful of cells, enable the flag
      right before the operation and disable it afterward to minimise impact.
  type: HowTo
tags:
- Aspose.Cells
- C#
- DateTime
- Japanese era
- .NET
title: Analizar DateTime con el reinado del emperador japonés usando Aspose.Cells
url: /es/net/excel-custom-number-date-formatting/parse-datetime-with-japanese-emperor-reign-using-aspose-cell/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Analizar DateTime con el reinado del emperador japonés usando Aspose.Cells

Si necesitas **analizar DateTime con el reinado del emperador japonés** en una aplicación .NET, esta guía te muestra exactamente cómo hacerlo con Aspose.Cells. Al habilitar el calendario de eras japonesas, escribir una cadena basada en era y leer el valor `DateTime` resultante, obtienes fechas fiables y conscientes de la cultura sin manipular manualmente las cadenas.

Trabajar con fechas de era japonesa es común en finanzas, gobierno y sistemas heredados que aún almacenan fechas como “令和3年5月10日”. Este tutorial cubre el flujo completo, desde la configuración del proyecto hasta la obtención de un objeto `DateTime` que puedes usar en cálculos, registros o visualización en la UI.

## Lo que aprenderás

- Cómo agregar el paquete NuGet Aspose.Cells a un proyecto C#.  
- Cómo activar el **calendario de era japonesa** mediante `Workbook.Settings`.  
- Cómo escribir una cadena de fecha de era japonesa en una celda y dejar que Aspose.Cells la analice automáticamente.  
- Cómo leer el `DateTime` analizado usando la propiedad `DateTimeValue`.  

**Requisitos previos**  
- .NET 6.0 o posterior (el código también funciona con .NET Framework 4.7+).  
- Familiaridad básica con C# y Visual Studio (o cualquier IDE).  
- Acceso a Internet para descargar el paquete Aspose.Cells.

---

## Paso 1: Instalar Aspose.Cells

Abre la carpeta de tu proyecto en una terminal o en la consola del Administrador de paquetes NuGet y ejecuta:

```bash
dotnet add package Aspose.Cells
```

O, en Visual Studio, haz clic derecho en el proyecto → **Manage NuGet Packages** → busca **Aspose.Cells** y haz clic en **Install**.  
Esto agrega el ensamblado `Aspose.Cells`, que proporciona las clases `Workbook`, `Worksheet` y las capacidades de análisis que necesitamos.

## Paso 2: Habilitar el calendario de era japonesa

Aspose.Cells desactiva el análisis de era japonesa de forma predeterminada. Debes activarlo mediante la bandera `Workbook.Settings.UseJapaneseEraCalendar`.

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // Create a new workbook instance
        Workbook workbook = new Workbook();

        // Enable parsing of Japanese era dates (e.g., 令和, 平成)
        workbook.Settings.UseJapaneseEraCalendar = true;
```

Establecer `UseJapaneseEraCalendar` en `true` indica a la biblioteca que interprete las cadenas que contienen nombres de era (`令和`, `平成`, `昭和`, etc.) según las reglas oficiales del calendario japonés.

## Paso 3: Escribir una cadena de fecha de era japonesa en una celda

A continuación, obtén la primera hoja de cálculo y coloca una cadena de fecha de era japonesa en la celda **A1**.

```csharp
        // Access the first worksheet (index 0)
        Worksheet sheet = workbook.Worksheets[0];

        // Write the era‑based date string into cell A1
        sheet.Cells["A1"].PutValue("令和3年5月10日");
```

**Por qué funciona:**  
Cuando `UseJapaneseEraCalendar` está activo, `PutValue` examina la cadena, detecta el prefijo de era (`令和`) y la convierte internamente al año gregoriano correspondiente (2021). La biblioteca almacena entonces el valor como un verdadero objeto `DateTime`, no solo como texto.

## Paso 4: Recuperar el valor `DateTime` analizado

Ahora lee la propiedad `DateTimeValue` de la celda. Aspose.Cells devuelve automáticamente la fecha gregoriana.

```csharp
        // Retrieve the parsed DateTime from cell A1
        DateTime parsedDate = sheet.Cells["A1"].DateTimeValue;

        // Output the result to the console
        Console.WriteLine($"Parsed Gregorian date: {parsedDate:yyyy-MM-dd}");
    }
}
```

Ejecutar el programa muestra:

```
Parsed Gregorian date: 2021-05-10
```

La salida confirma que **Analizar DateTime con el reinado del emperador japonés** convirtió correctamente “令和3年5月10日” a 10 de mayo de 2021.

## Paso 5: Manejar casos límite y variaciones comunes

### Múltiples formatos de era
Aspose.Cells reconoce varias representaciones de era:

| Era (japonés) | Rango de años gregorianos |
|----------------|---------------------------|
| 明治 (Meiji)   | 1868‑1912                 |
| 大正 (Taishō)  | 1912‑1926                 |
| 昭和 (Shōwa)   | 1926‑1989                 |
| 平成 (Heisei)  | 1989‑2019                 |
| 令和 (Reiwa)   | 2019‑presente             |

Si tus datos de origen mezclan caracteres de ancho completo, espacios o usan los kanjis “年”, “月”, “日”, el analizador sigue funcionando. Por ejemplo, `"平成31年4月30日"` se convierte en `2019-04-30`.

### Cadenas inválidas
Cuando la cadena no puede analizarse (p. ej., `"令和99年13月40日"`), `DateTimeValue` devuelve `DateTime.MinValue`. Puedes comprobar esta condición:

```csharp
if (parsedDate == DateTime.MinValue)
{
    Console.WriteLine("The cell does not contain a valid Japanese era date.");
}
```

### Desactivar la función
Si más tarde necesitas almacenar cadenas de era sin conversión, vuelve a establecer la bandera en `false`:

```csharp
workbook.Settings.UseJapaneseEraCalendar = false;
```

### Consejo de rendimiento
Habilitar el calendario de era añade una pequeña sobrecarga a cada llamada `PutValue` que involucre cadenas. Si solo analizas unas pocas celdas, habilita la bandera justo antes de la operación y desactívala después para minimizar el impacto.

## Ejemplo completo, ejecutable

A continuación tienes el programa completo que puedes copiar, pegar y ejecutar al instante.

```csharp
using Aspose.Cells;
using System;

class ParseJapaneseEraDemo
{
    static void Main()
    {
        // 1️⃣ Create a new workbook
        Workbook workbook = new Workbook();

        // 2️⃣ Turn on Japanese era parsing
        workbook.Settings.UseJapaneseEraCalendar = true;

        // 3️⃣ Access the first worksheet
        Worksheet sheet = workbook.Worksheets[0];

        // 4️⃣ Write an era date string into A1
        sheet.Cells["A1"].PutValue("令和3年5月10日");

        // 5️⃣ Retrieve the parsed DateTime
        DateTime parsedDate = sheet.Cells["A1"].DateTimeValue;

        // Verify the result
        Console.WriteLine($"Parsed Gregorian date: {parsedDate:yyyy-MM-dd}");
        // Expected output: Parsed Gregorian date: 2021-05-10
    }
}
```

**Salida esperada**

```
Parsed Gregorian date: 2021-05-10
```

El programa demuestra el flujo de extremo a extremo para **Analizar DateTime con el reinado del emperador japonés** usando Aspose.Cells, desde la creación del libro de trabajo hasta la obtención de un objeto `DateTime` utilizable.

---

## Conclusión

Ahora sabes cómo **Analizar DateTime con el reinado del emperador japonés** en C# mediante:

1. Instalar **Aspose.Cells**.  
2. Habilitar el **calendario de era japonesa** a través de `Workbook.Settings`.  
3. Escribir cadenas basadas en era en celdas.  
4. Leer el `DateTimeValue` resultante.  

Este enfoque elimina la lógica de análisis manual, respeta los límites oficiales de las eras y se integra sin problemas con el manejo de fechas existente en .NET.  

**Próximos pasos**  
- Explora otras funciones específicas de cultura de Aspose.Cells, como el **análisis de fechas C#** para calendarios Hijri o Budista tailandés.  
- Combina esta técnica con configuraciones de `Workbook Settings` como `CalcEngine` para evaluar fórmulas que referencien fechas de era.  
- Utiliza el `DateTime` analizado en informes, almacenamiento en bases de datos o componentes UI que requieran fechas gregorianas.

¡Experimenta con diferentes cadenas de era, maneja entradas inválidas e integra la solución en pipelines de importación de datos más grandes. Feliz codificación!

## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y explicaciones paso a paso para ayudarte a dominar funciones adicionales de la API y explorar enfoques alternativos en tus propios proyectos.

- [Parse Japanese Era Dates in Excel – Full Guide for C# Developers](/cells/english/net/data-loading-and-parsing/parse-japanese-era-dates-in-excel-full-guide-for-c-developer/)
- [How to Parse Japanese Dates in C# – Complete Guide](/cells/english/net/data-loading-and-parsing/how-to-parse-japanese-dates-in-c-complete-guide/)
- [How to Implement Date Validation in .NET Using Aspose.Cells: A Comprehensive Guide](/cells/english/net/data-validation/implement-date-validation-net-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}