---
category: general
date: 2026-06-27
description: Aprende a analizar fechas de era japonesa en C# y luego formatear datetime
  yyyy‑mm‑dd para salida ISO. Código paso a paso, casos límite y consejos.
draft: false
keywords:
- parse japanese era date
- format datetime yyyy-mm-dd
- C# JapaneseCalendar
- CultureInfo date parsing
- .NET DateTime era handling
language: es
og_description: Analiza fechas de la era japonesa en C# y formatea datetime yyyy‑mm‑dd
  sin esfuerzo. Ejemplo completo con explicaciones y trampas.
og_title: Analizar fecha de era japonesa en C# – Guía completa de programación
schemas:
- author: Aspose
  dateModified: '2026-06-27'
  description: Learn how to parse Japanese era date in C# and then format datetime
    yyyy-mm-dd for ISO output. Step‑by‑step code, edge cases, and tips.
  headline: Parse Japanese era date in C# – Complete Guide
  type: TechArticle
- description: Learn how to parse Japanese era date in C# and then format datetime
    yyyy-mm-dd for ISO output. Step‑by‑step code, edge cases, and tips.
  name: Parse Japanese era date in C# – Complete Guide
  steps:
  - name: Multiple Eras
    text: Japan has gone through several eras (Meiji, Taishō, Shōwa, Heisei, Reiwa).
      The `JapaneseCalendar` automatically maps them, so `"H30-12-31"` (Heisei 30)
      becomes `2018-12-31`. Just keep the same parsing logic; the calendar does the
      heavy lifting.
  - name: Invalid Input
    text: 'If a string doesn’t match the expected pattern, `Parse` throws. Use `TryParseExact`
      as shown earlier, or pre‑validate with a regular expression:'
  - name: Time Zones
    text: '`DateTime` objects are “kind‑agnostic” by default. If you need a UTC timestamp,
      call:'
  type: HowTo
tags:
- C#
- .NET
- DateTime
- Localization
title: Analizar fecha de era japonesa en C# – Guía completa
url: /es/net/data-loading-and-parsing/parse-japanese-era-date-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Analizar fecha de era japonesa en C# – Guía completa

¿Alguna vez necesitaste **parse Japanese era date** en una aplicación .NET y te preguntaste por qué el resultado parece incorrecto? No estás solo. En muchos sistemas heredados, las fechas aparecen en el estilo “R3‑04‑01”, y necesitas convertirlas en una cadena **format datetime yyyy-mm-dd** limpia para APIs o bases de datos.  

En este tutorial recorreremos paso a paso lo necesario para lograrlo, explicaremos por qué cada pieza es importante y te mostraremos cómo manejar los casos límite que a menudo atrapan a los desarrolladores.

> **Nota:** Todo el código está listo para copiar‑pegar en una aplicación de consola dirigida a .NET 6 o posterior.

## Lo que necesitarás

- .NET 6 SDK (o cualquier versión reciente)
- Familiaridad básica con C# y el espacio de nombres `System.Globalization`
- Un IDE o editor – Visual Studio, VS Code, Rider, lo que prefieras

No se requieren paquetes NuGet externos; todo está en la BCL.

## Paso 1: Configurar la cultura japonesa con el calendario imperial

Primero, necesitamos un `CultureInfo` que conozca el calendario imperial japonés. Por defecto, `ja-JP` usa el calendario gregoriano, así que reemplazamos su `DateTimeFormat.Calendar` con una instancia de `JapaneseCalendar`.

```csharp
using System;
using System.Globalization;

class Program
{
    static void Main()
    {
        // Step 1: Create a Japanese culture and switch to the Japanese imperial calendar
        CultureInfo japaneseCulture = new CultureInfo("ja-JP");
        japaneseCulture.DateTimeFormat.Calendar = new JapaneseCalendar();

        // (The rest of the code follows...)
```

> **Por qué es importante:** El `JapaneseCalendar` traduce los símbolos de era (como “R” para Reiwa) al año gregoriano correcto. Sin él, `DateTime.Parse` lanzaría una `FormatException`.

## Paso 2: Analizar la cadena de fecha basada en era

Ahora podemos pasar una cadena como `"R3-04-01"` a `DateTime.Parse`. La cultura que acabamos de configurar indica al analizador cómo interpretar la parte “R3”.

```csharp
        // Step 2: Parse a date string that uses the Japanese era format (e.g., "R3-04-01")
        string eraDate = "R3-04-01";
        DateTime parsedDate = DateTime.Parse(eraDate, japaneseCulture);
```

Si prefieres un enfoque más seguro que evite excepciones con entradas incorrectas, sustituye `Parse` por `TryParseExact`:

```csharp
        // Safer alternative with TryParseExact
        if (DateTime.TryParseExact(
                eraDate,
                "ggy-MM-dd",               // ggy = era+year, MM = month, dd = day
                japaneseCulture,
                DateTimeStyles.None,
                out DateTime safeDate))
        {
            parsedDate = safeDate;
        }
        else
        {
            Console.WriteLine("Unable to parse the Japanese era date.");
            return;
        }
```

> **Consejo profesional:** La cadena de formato personalizada `"ggy-MM-dd"` le dice al analizador exactamente qué esperar. “gg” es el designador de era, “y” el año dentro de esa era.

## Paso 3: Convertir el resultado a ISO 8601 (`format datetime yyyy-mm-dd`)

Finalmente, emitimos el `DateTime` en un formato ISO estándar. El especificador de formato `"yyyy-MM-dd"` hace precisamente eso.

```csharp
        // Step 3: Display the parsed date in a standard ISO format
        string isoDate = parsedDate.ToString("yyyy-MM-dd", CultureInfo.InvariantCulture);
        Console.WriteLine(isoDate); // Expected output: 2021-04-01
    }
}
```

Ejecutar el programa muestra:

```
2021-04-01
```

Ese es el **format datetime yyyy-mm-dd** que buscabas, listo para cargas JSON, inserciones SQL o cualquier sistema descendente.

![parse japanese era date example](placeholder.png){alt="ejemplo de análisis de fecha de era japonesa"}

## Manejo de otras eras y casos límite

### Múltiples eras

Japón ha atravesado varias eras (Meiji, Taishō, Shōwa, Heisei, Reiwa). El `JapaneseCalendar` las asigna automáticamente, de modo que `"H30-12-31"` (Heisei 30) se convierte en `2018-12-31`. Mantén la misma lógica de análisis; el calendario hace el trabajo pesado.

### Entrada no válida

Si una cadena no coincide con el patrón esperado, `Parse` lanza una excepción. Usa `TryParseExact` como se mostró antes, o pre‑valida con una expresión regular:

```csharp
bool IsValidEraDate(string input) =>
    System.Text.RegularExpressions.Regex.IsMatch(
        input, @"^[RHS][0-9]+-\d{2}-\d{2}$", System.Text.RegularExpressions.RegexOptions.IgnoreCase);
```

### Zonas horarias

Los objetos `DateTime` son “agnósticos de tipo” por defecto. Si necesitas una marca de tiempo UTC, llama:

```csharp
DateTime utc = DateTime.SpecifyKind(parsedDate, DateTimeKind.Utc);
```

O usa `DateTimeOffset` para una plena conciencia de zona.

## Ejemplo completo funcionando

Aquí tienes el fragmento completo que puedes colocar en un nuevo proyecto de consola:

```csharp
using System;
using System.Globalization;

class Program
{
    static void Main()
    {
        // Initialize Japanese culture with the imperial calendar
        CultureInfo japaneseCulture = new CultureInfo("ja-JP");
        japaneseCulture.DateTimeFormat.Calendar = new JapaneseCalendar();

        // The era‑based date you want to convert
        string eraDate = "R3-04-01";

        // Try parsing – safer than Parse when input may be malformed
        if (!DateTime.TryParseExact(
                eraDate,
                "ggy-MM-dd",
                japaneseCulture,
                DateTimeStyles.None,
                out DateTime parsedDate))
        {
            Console.WriteLine("Failed to parse the Japanese era date.");
            return;
        }

        // Convert to ISO 8601 (format datetime yyyy-mm-dd)
        string isoDate = parsedDate.ToString("yyyy-MM-dd", CultureInfo.InvariantCulture);
        Console.WriteLine($"Original era date: {eraDate}");
        Console.WriteLine($"Converted ISO date: {isoDate}");
    }
}
```

**Salida esperada en la consola**

```
Original era date: R3-04-01
Converted ISO date: 2021-04-01
```

## Recapitulación

Hemos cubierto cómo **parse Japanese era date** cadenas mediante:

1. Crear un `CultureInfo` para `ja-JP` y sustituir su calendario por `JapaneseCalendar`.
2. Usar `DateTime.Parse` o el más robusto `TryParseExact` con un formato personalizado.
3. Formatear el `DateTime` resultante con `"yyyy-MM-dd"` para obtener el **format datetime yyyy-mm-dd** deseado.

Eso es todo lo que necesitas para conectar datos heredados de era japonesa con sistemas modernos compatibles con ISO.

## ¿Qué sigue?

- **Procesamiento por lotes:** Recorrer un CSV de fechas de era y escribir cadenas ISO en una base de datos.
- **Localización:** Convertir fechas ISO de nuevo al formato de era para la visualización en UI (`ToString("ggyy年MM月dd日", japaneseCulture)`).
- **Calendarios personalizados:** Explorar `TaiwanCalendar` o `HijriCalendar` para otras necesidades regionales.

Siéntete libre de experimentar—cambia la cadena de era, prueba casos límite o integra esta lógica en endpoints de ASP.NET Core. Si encuentras algún problema, deja un comentario abajo; ¡feliz codificación!

## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos con explicaciones paso a paso para ayudarte a dominar funciones adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Cómo implementar validación de fechas en .NET usando Aspose.Cells: Guía completa](/cells/english/net/data-validation/implement-date-validation-net-aspose-cells/)
- [Cambiar el sistema de fechas de Excel a 1904 usando Aspose.Cells .NET](/cells/english/net/calculation-engine/change-excel-date-system-aspose-cells-net/)
- [Cómo implementar y formatear comentarios en Excel usando Aspose.Cells para .NET: Guía paso a paso](/cells/english/net/comments-annotations/implement-format-excel-comments-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}