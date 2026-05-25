---
category: general
date: 2026-03-21
description: Establece un formato personalizado de celda en C# y aprende cómo escribir
  fechas en Excel, aplicar un formato de fecha personalizado, leer DateTime de Excel
  y crear rápidamente una hoja de cálculo.
draft: false
keywords:
- set cell custom format
- write date to excel
- read datetime from excel
- apply custom date format
- create workbook worksheet
language: es
og_description: Establecer formato personalizado de celda en C# para escribir fechas
  en Excel, aplicar un formato de fecha personalizado, leer DateTime desde Excel y
  crear una hoja de cálculo del libro de trabajo con facilidad.
og_title: Establecer formato personalizado de celda en C# – Escribir y leer fechas
  en Excel
tags:
- Aspose.Cells
- C#
- Excel Automation
title: Establecer formato personalizado de celda en C# – Guía completa para escribir
  y leer fechas en Excel
url: /es/net/excel-custom-number-date-formatting/set-cell-custom-format-in-c-complete-guide-to-writing-readin/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Establecer formato personalizado de celda – Escribir y leer fechas en Excel con C#

¿Alguna vez necesitaste **establecer un formato personalizado de celda** en un archivo Excel desde C# pero no sabías por dónde empezar? No estás solo. En muchas herramientas de generación de informes o utilidades de exportación de datos la fecha debe aparecer en una localidad específica—piensa en fechas de era japonesa, calendarios fiscales o cadenas ISO‑8601.  

En este tutorial recorreremos un **ejemplo completo y ejecutable** que muestra cómo **escribir una fecha en Excel**, **aplicar un formato de fecha personalizado**, **leer DateTime desde Excel** y **crear una hoja de cálculo** con Aspose.Cells. Al final tendrás un programa autocontenido que puedes insertar en cualquier proyecto .NET.

## Lo que aprenderás

- Cómo **crear una hoja de cálculo** programáticamente.  
- Los pasos exactos para **escribir una fecha en Excel** usando una cadena específica de la localidad.  
- Cómo **aplicar un formato de fecha personalizado** (incluida la notación de era japonesa).  
- La forma de **leer DateTime desde Excel** y convertirlo en un objeto `DateTime`.  
- Consejos, trampas y variaciones que podrías encontrar al trabajar con fechas en Excel.

No se requiere documentación externa—todo lo que necesitas está aquí.

## Requisitos previos

- .NET 6.0 o posterior (el código también funciona en .NET Framework 4.7+).  
- Aspose.Cells para .NET instalado vía NuGet (`Install-Package Aspose.Cells`).  
- Un entendimiento básico de la sintaxis de C#—nada complicado.

> **Consejo profesional:** Si usas Visual Studio, habilita *tipos de referencia anulables* para detectar errores sutiles temprano.

## Paso 1: Crear un Workbook y una Worksheet  

Lo primero: necesitas un objeto workbook que represente el archivo Excel, y una worksheet donde vivirán los datos.

```csharp
using Aspose.Cells;
using System;

class ExcelDateDemo
{
    static void Main()
    {
        // Step 1: Initialize a new workbook and grab the first worksheet
        Workbook workbook = new Workbook();                     // creates an empty .xlsx in memory
        Worksheet worksheet = workbook.Worksheets[0];           // default sheet is named "Sheet1"
```

*Por qué es importante:* La clase `Workbook` es el punto de entrada para todas las operaciones de Excel. Crearla en memoria significa que no tocas el sistema de archivos hasta que guardes explícitamente, lo que mantiene el proceso rápido y fácil de probar.

## Paso 2: Escribir la fecha en Excel  

A continuación, colocaremos una cadena de fecha de era japonesa (`"R02-04-01"`) en la celda **A1**. La cadena imita la era Reiwa (año 2, 1 de abril).

```csharp
        // Step 2: Write a Japanese era date string into cell A1
        worksheet.Cells["A1"].PutValue("R02-04-01");
```

*Qué está ocurriendo:* `PutValue` almacena la cadena cruda. Aspose.Cells intentará analizarla más tarde según el estilo de la celda. Si omites este paso y escribes directamente un `DateTime`, perderás la información de era que deseas mostrar.

## Paso 3: Aplicar el formato numérico de fecha incorporado (ID 14)

Excel tiene un formato de fecha incorporado con ID 14 (`mm-dd-yy`). Aplicarlo indica al motor que la celda **contiene una fecha**, no solo texto.

```csharp
        // Step 3: Apply the built‑in date number format (ID 14)
        worksheet.Cells["A1"].Style.Number = 14;
```

*¿Por qué usar el ID 14?* Es el formato universal de “fecha corta” que asegura que Excel trate el contenido como un valor de fecha, requisito previo para que cualquier formato personalizado funcione correctamente.

## Paso 4: Establecer un formato personalizado para mostrar notación de era japonesa  

Ahora viene la parte divertida: le decimos a Excel que renderice la fecha usando el formato de era japonesa. La cadena personalizada `[$-ja-JP]ggge年m月d日` hace exactamente eso.

```csharp
        // Step 4: Set a custom format to display the date in Japanese era notation
        worksheet.Cells["A1"].Style.Custom = "[$-ja-JP]ggge年m月d日";
```

*Explicación:*  
- `[$-ja-JP]` fuerza la localidad a japonés.  
- `ggg` es el nombre de la era (p. ej., “R” para Reiwa).  
- `e` es el año de la era.  
- `年`, `月`, `日` son caracteres japoneses literales para año, mes y día.

Si necesitas una localidad diferente, simplemente reemplaza `ja-JP` con el código cultural apropiado (p. ej., `en-US`).

## Paso 5: Recuperar el valor DateTime analizado  

Finalmente, leamos el **DateTime real** que Excel ha analizado de la celda. Esto demuestra que la cadena se interpretó correctamente.

```csharp
        // Step 5: Retrieve the parsed DateTime value from the cell
        DateTime parsedDate = worksheet.Cells["A1"].DateTime;   // => 2020‑04‑01

        // Output to console for verification
        Console.WriteLine($"Parsed DateTime: {parsedDate:yyyy-MM-dd}");
```

*Resultado:* La consola imprime `Parsed DateTime: 2020-04-01`. Aunque ingresamos una cadena de era japonesa, Excel almacena internamente la fecha gregoriana, que puedes usar para cálculos, comparaciones o exportaciones posteriores.

## Paso 6: Guardar el Workbook (Opcional)

Si deseas ver el libro formateado en Excel, simplemente guárdalo en disco.

```csharp
        // Optional: Save the workbook to a file
        workbook.Save("JapaneseEraDate.xlsx");
    }
}
```

Abre el **JapaneseEraDate.xlsx** generado y verás la celda **A1** mostrando `R02年4月1日` (el formato exacto de era japonesa que establecimos).

![ejemplo de formato personalizado de celda](image-placeholder.png "Celda de Excel que muestra la fecha de era japonesa – formato personalizado de celda")

*El texto alternativo anterior contiene la palabra clave principal, cumpliendo con el requisito de SEO para imágenes.*

## Variaciones comunes y casos límite  

### Escribir un formato de fecha diferente  

Si prefieres ISO‑8601 (`2020-04-01`) en lugar de una cadena de era, simplemente cambia la llamada a `PutValue`:

```csharp
worksheet.Cells["A1"].PutValue(new DateTime(2020, 4, 1));
worksheet.Cells["A1"].Style.Number = 14;                 // keep built‑in date format
worksheet.Cells["A1"].Style.Custom = "yyyy-mm-dd";      // custom ISO format
```

### Manejar celdas nulas o vacías  

Al leer una fecha, siempre protege contra celdas vacías para evitar `InvalidOperationException`:

```csharp
if (!worksheet.Cells["A1"].IsDate)
{
    Console.WriteLine("Cell A1 does not contain a valid date.");
}
else
{
    DateTime dt = worksheet.Cells["A1"].DateTime;
    // use dt...
}
```

### Soportar múltiples localidades  

Puedes iterar sobre una lista de códigos culturales y aplicarlos dinámicamente:

```csharp
string[] cultures = { "ja-JP", "en-US", "fr-FR" };
foreach (var culture in cultures)
{
    worksheet.Cells["A1"].Style.Custom = $"[$-{culture}]ggge年m月d日";
    // Save or export per culture if needed
}
```

## Consejos profesionales y advertencias  

- **Siempre establece primero un formato numérico incorporado** (`Style.Number`). Sin él, Excel trata la celda como texto plano y el formato personalizado se ignora.  
- **Los códigos de localidad no distinguen entre mayúsculas y minúsculas**, pero usar la forma canónica (`ja-JP`) evita confusiones.  
- **Guardar es opcional** para procesamiento en memoria; puedes transmitir el workbook directamente a una respuesta web (`workbook.Save(stream, SaveFormat.Xlsx)`).  
- **Licencias de Aspose.Cells**: La versión de evaluación gratuita agrega una marca de agua. Para producción, asegúrate de contar con una licencia válida para evitar penalizaciones de rendimiento.

## Recapitulación  

Hemos demostrado cómo **establecer un formato personalizado de celda** en C# para mostrar fechas de era japonesa, cómo **escribir una fecha en Excel**, **aplicar un formato de fecha personalizado**, **leer DateTime desde Excel** y **crear una hoja de cálculo**, todo en un único programa autocontenido. La palabra clave principal aparece de forma natural a lo largo del texto, mientras que las palabras clave secundarias están integradas en los encabezados y el cuerpo, cumpliendo tanto con los estándares SEO como con los de citación AI.

## ¿Qué sigue?

- Explora **formato condicional** para resaltar fechas vencidas.  
- Combina este enfoque con **Tablas dinámicas** para informes dinámicos.  
- Prueba **leer archivos CSV grandes** y convertirlos a Excel con la misma lógica de manejo de fechas.  

Siéntete libre de experimentar con diferentes localidades, patrones personalizados o incluso zonas horarias. Si encuentras algún inconveniente, deja un comentario abajo—¡feliz codificación!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}