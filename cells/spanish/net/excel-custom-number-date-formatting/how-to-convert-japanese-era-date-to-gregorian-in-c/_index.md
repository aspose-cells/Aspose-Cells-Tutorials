---
category: general
date: 2026-10-01
description: Convierte una fecha de era japonesa a un DateTime gregoriano usando Aspose.Cells
  en C#. Aprende cómo convertir el calendario japonés rápidamente.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert japanese era date
- how to convert japanese calendar
language: es
lastmod: 2026-10-01
og_description: Convertir una fecha de era japonesa a un DateTime gregoriano en C#.
  Este tutorial explica cómo convertir el calendario japonés con precisión usando
  Aspose.Cells.
og_image_alt: Code example converting a Japanese era date string to a Gregorian DateTime
  in a C# console app
og_title: Convertir fecha de era japonesa al calendario gregoriano en C# – guía paso
  a paso
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: convert japanese era date to a Gregorian DateTime using Aspose.Cells
    in C#. Learn how to convert japanese calendar quickly.
  headline: How to convert Japanese era date to Gregorian in C#
  type: TechArticle
- description: convert japanese era date to a Gregorian DateTime using Aspose.Cells
    in C#. Learn how to convert japanese calendar quickly.
  name: How to convert Japanese era date to Gregorian in C#
  steps:
  - name: Why each step matters
    text: '| Step | Purpose | How it helps the conversion | |------|---------|-----------------------------|
      | **Create workbook** | Provides a container that understands Excel formulas
      and date systems. | The library’s internal date engine is activated only inside
      a workbook. | | **Insert era string** | Suppl'
  - name: Handling invalid or ambiguous strings
    text: '* **Invalid era name** – Aspose.Cells throws a `FormatException`. Wrap
      the conversion in `try/catch` to provide a friendly error message. * **Missing
      year/month/day** – The library expects a full “Era Year/Month/Day” pattern.
      If you receive partial data, prepend missing parts or reject the input ear'
  - name: Next steps
    text: '* Explore **formatting options** to write the Gregorian date back into
      the worksheet with a custom number format. * Combine this conversion with **data
      import pipelines** (e.g., reading CSV files that contain era dates). * Review
      other Aspose.Cells features such as **date arithmetic** and **regional'
  type: HowTo
tags:
- Aspose.Cells
- C#
- date conversion
title: Cómo convertir una fecha de era japonesa al calendario gregoriano en C#
url: /es/net/excel-custom-number-date-formatting/how-to-convert-japanese-era-date-to-gregorian-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo convertir una fecha de era japonesa a Gregorian en C#

Si necesitas **convertir fechas de era japonesa** a fechas gregorianas en C#, esta guía te muestra exactamente cómo hacerlo. Ya sea que estés procesando datos heredados, leyendo la entrada del usuario o generando informes, la biblioteca Aspose.Cells hace que la conversión sea sencilla. Además, descubrirás la mejor manera de **cómo convertir el calendario japonés** cuando trabajas con hojas de cálculo.

El tutorial cubre cada paso—desde crear un libro de trabajo hasta obtener un valor `DateTime`—para que puedas copiar‑pegar un programa completo y ejecutable. No se requiere documentación externa; solo sigue el código y las explicaciones a continuación.

## Requisitos previos

Antes de comenzar, asegúrate de tener:

* .NET 6.0 o posterior (el código también funciona con .NET Framework 4.6+)
* Una licencia para **Aspose.Cells** (la prueba gratuita sirve para pruebas)
* Un entorno de desarrollo como Visual Studio 2022 o VS Code
* Familiaridad básica con aplicaciones de consola en C#

## Convertir fecha de era japonesa con Aspose.Cells

El núcleo de la conversión se encuentra en unas pocas llamadas simples a la API. Aspose.Cells interpreta automáticamente cadenas de era japonesa (p. ej., “Reiwa 2/04/01”) y expone el resultado como un objeto `DateTime` una vez que la hoja de cálculo se recalcula.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Create a new workbook and get the first worksheet
        var workbook = new Workbook();                // creates an empty Excel file in memory
        var worksheet = workbook.Worksheets[0];       // the default sheet is at index 0

        // Step 2: Insert a Japanese era date string into cell A1
        // The string follows the Japanese calendar format: Era Year/Month/Day
        worksheet.Cells[0, 0].PutValue("Reiwa 2/04/01");

        // Step 3: Apply a default style to the cell (required for proper calculation)
        // Without a style, Aspose.Cells may treat the content as plain text and skip conversion.
        worksheet.Cells[0, 0].SetStyle(workbook.CreateStyle());

        // Step 4: Recalculate the worksheet so the date string is converted to a Gregorian date
        // The Calculate method parses the era string and updates the cell's internal value.
        worksheet.Calculate();

        // Step 5: Retrieve and display the converted DateTime value (2020‑04‑01)
        DateTime gregorian = worksheet.Cells[0, 0].DateTimeValue;
        Console.WriteLine($"Gregorian date: {gregorian:yyyy-MM-dd}");
    }
}
```

### Por qué cada paso es importante

| Paso | Propósito | Cómo ayuda a la conversión |
|------|-----------|----------------------------|
| **Crear libro de trabajo** | Proporciona un contenedor que entiende fórmulas de Excel y sistemas de fechas. | El motor interno de fechas de la biblioteca se activa solo dentro de un libro de trabajo. |
| **Insertar cadena de era** | Proporciona el texto del calendario japonés que deseas traducir. | Aspose.Cells reconoce nombres de era como *Reiwa*, *Heisei*, *Showa*, etc. |
| **Establecer estilo** | Obliga a que la celda se trate como una celda de valor y no como una cadena literal. | Sin un estilo, el método `Calculate` puede ignorar la celda, dejando el texto sin cambios. |
| **Calcular** | Dispara el análisis de la cadena de era y la conversión al número de serie interno de fecha. | La biblioteca convierte “Reiwa 2/04/01” → número de serie → `DateTime` gregoriano. |
| **Leer `DateTimeValue`** | Devuelve el objeto .NET `DateTime` convertido. | Ahora tienes un `DateTime` estándar que puedes usar en cualquier API de .NET. |

## Cómo convertir el calendario japonés en otros escenarios

El mismo enfoque funciona para cualquier nombre de era japonesa admitido por Aspose.Cells:

```csharp
// Example: converting a Heisei era date
worksheet.Cells[0, 0].PutValue("Heisei 30/12/31"); // corresponds to 2018‑12‑31
worksheet.Calculate();
Console.WriteLine(worksheet.Cells[0, 0].DateTimeValue); // 2018-12-31
```

### Manejo de cadenas inválidas o ambiguas

* **Nombre de era inválido** – Aspose.Cells lanza una `FormatException`. Envuelve la conversión en `try/catch` para proporcionar un mensaje de error amigable.
* **Falta año/mes/día** – La biblioteca espera un patrón completo “Era Año/Mes/Día”. Si recibes datos parciales, antepone las partes faltantes o rechaza la entrada de inmediato.
* **Configuraciones regionales diferentes** – La conversión **no** depende de la cultura del hilo actual; siempre utiliza el mapa de eras japonesas incorporado en Aspose.Cells. Esto hace que el método sea seguro para procesamiento del lado del servidor.

```csharp
try
{
    worksheet.Cells[0, 0].PutValue(userInput);
    worksheet.Calculate();
    DateTime result = worksheet.Cells[0, 0].DateTimeValue;
    // Use result...
}
catch (FormatException ex)
{
    Console.WriteLine($"Unable to parse Japanese era date: {ex.Message}");
}
```

## Consejos prácticos y errores comunes

* **Siempre llama a `SetStyle`** antes de `Calculate`. Omitir este paso es una fuente frecuente de errores porque la celda sigue siendo un contenedor de texto plano.
* **Reutiliza el mismo libro de trabajo** si necesitas convertir muchas fechas. Crear un nuevo libro para cada conversión genera una sobrecarga innecesaria.
* **Conversión por lotes** – Llena una columna con cadenas de era, llama a `worksheet.Calculate()` una vez y luego lee toda la columna de `DateTimeValue`s. Esto es mucho más eficiente que recalcular celda por celda.
* **Compatibilidad de versiones** – La lógica de conversión de eras se introdujo en Aspose.Cells 22.9. Asegúrate de usar esa versión o una posterior; versiones anteriores tratan la cadena como texto plano.

## Ejemplo completo (aplicación de consola)

A continuación tienes un programa autocontenido que puedes compilar y ejecutar de inmediato. Demuestra tanto una conversión de Reiwa como de Heisei, manejando errores de forma elegante.

```csharp
using System;
using Aspose.Cells;

class JapaneseEraConverter
{
    static void Main()
    {
        // Initialize workbook once
        var workbook = new Workbook();
        var sheet = workbook.Worksheets[0];
        var style = workbook.CreateStyle();
        sheet.Cells[0, 0].SetStyle(style);
        sheet.Cells[1, 0].SetStyle(style);

        // Sample inputs
        string[] eraDates = { "Reiwa 2/04/01", "Heisei 30/12/31", "InvalidEra 1/01/01" };

        for (int i = 0; i < eraDates.Length; i++)
        {
            sheet.Cells[i, 0].PutValue(eraDates[i]);
        }

        // Perform conversion for all populated cells
        sheet.Calculate();

        // Output results
        for (int i = 0; i < eraDates.Length; i++)
        {
            try
            {
                DateTime dt = sheet.Cells[i, 0].DateTimeValue;
                Console.WriteLine($"{eraDates[i]} → {dt:yyyy-MM-dd}");
            }
            catch (Exception)
            {
                Console.WriteLine($"{eraDates[i]} → conversion failed");
            }
        }
    }
}
```

**Salida esperada en la consola**

```
Reiwa 2/04/01 → 2020-04-01
Heisei 30/12/31 → 2018-12-31
InvalidEra 1/01/01 → conversion failed
```

Ejecutar este programa confirma que la biblioteca convierte correctamente **fechas de era japonesa** y reporta de forma elegante los valores no compatibles.

## Conclusión

Ahora sabes cómo **convertir fechas de era japonesa** a objetos `DateTime` gregorianos estándar usando Aspose.Cells en C#. El proceso se reduce a insertar el texto de la era, aplicar un estilo, recalcular la hoja y leer `DateTimeValue`. Siguiendo los pasos anteriores también puedes responder a la pregunta más amplia de **cómo convertir el calendario japonés** en bloque, manejar errores y optimizar el rendimiento.

### Próximos pasos

* Explora **opciones de formato** para escribir la fecha gregoriana de vuelta en la hoja con un formato numérico personalizado.
* Combina esta conversión con **pipelines de importación de datos** (p. ej., leyendo archivos CSV que contengan fechas de era).
* Revisa otras funcionalidades de Aspose.Cells como **aritmética de fechas** y **configuraciones regionales** para escenarios de calendario más complejos.

¡Feliz codificación, y siéntete libre de adaptar el ejemplo a tus propios flujos de procesamiento de datos!

## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos con explicaciones paso a paso para ayudarte a dominar funciones adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Parse Japanese Era Date in C# with Aspose.Cells – Full Guide](/cells/english/net/excel-custom-number-date-formatting/parse-japanese-era-date-in-c-with-aspose-cells-full-guide/)
- [Enable Japanese Era Parsing in C# with Aspose.Cells](/cells/english/net/workbook-settings/enable-japanese-era-parsing-in-c-with-aspose-cells/)
- [How to create workbook and convert string to date in C#](/cells/english/net/excel-custom-number-date-formatting/how-to-create-workbook-and-convert-string-to-date-in-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}