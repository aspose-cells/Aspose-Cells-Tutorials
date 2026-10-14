---
category: general
date: 2026-10-13
description: Aprende cómo guardar Excel como TXT con Aspose.Cells. Esta guía cubre
  la exportación de Excel a TXT, escribir valores en una celda y establecer dígitos
  significativos en solo unos pocos pasos.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- save excel as txt
- export excel to txt
- write value to cell
- set significant digits
- export spreadsheet as txt
language: es
lastmod: 2026-10-13
og_description: Guarda Excel como TXT con Aspose.Cells. Aprende cómo exportar Excel
  a TXT, escribir valores en una celda y establecer dígitos significativos en solo
  unas pocas líneas de código C#.
og_image_alt: Screenshot showing a workbook saved as a TXT file using save excel as
  txt
og_title: Guardar Excel como TXT – guía paso a paso para desarrolladores .NET
schemas:
- author: Aspose
  dateModified: '2026-10-13'
  description: Learn how to save Excel as TXT with Aspose.Cells. This guide covers
    export Excel to TXT, write value to cell, and set significant digits in just a
    few steps.
  headline: How to save Excel as TXT using Aspose.Cells in C#
  type: TechArticle
- questions:
  - answer: It rounds to the nearest value based on the specified number of significant
      digits, ensuring the output is mathematically accurate to that precision.
    question: Does `SignificantDigits` round or truncate?
  - answer: 'Yes. Replace the file path with a `MemoryStream` instance: `workbook.Save(stream,
      txtOptions);`. This is handy for web APIs that need to return the TXT content
      without touching the file system.'
    question: Can I export directly to a memory stream?
  - answer: 'Use `txtOptions.ExportFormattedValues = true`. This forces Aspose.Cells
      to write the cell’s displayed text rather than the raw value. ## Conclusion
      You now know how to **save Excel as TXT** with full control over precision,
      formatting, and output location. By following the four steps—create a workbo'
    question: What if I need to keep the original formatting (e.g., dates)?
  type: FAQPage
tags:
- Excel
- TXT
- Aspose.Cells
- .NET
title: Cómo guardar Excel como TXT usando Aspose.Cells en C#
url: /es/net/converting-excel-files-to-other-formats/how-to-save-excel-as-txt-using-aspose-cells-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo guardar Excel como TXT usando Aspose.Cells en C#

Si necesitas **guardar Excel como TXT** rápidamente, este tutorial muestra el proceso completo en menos de cinco minutos. Verás cómo exportar Excel a TXT, escribir un valor en una celda y establecer los dígitos significativos para que el archivo de texto contenga exactamente los datos que esperas.

Exportar una hoja de cálculo como TXT es útil cuando los sistemas posteriores solo aceptan entrada de texto plano, cuando necesitas generar registros o cuando deseas un volcado legible por humanos de los cálculos. El ejemplo a continuación funciona con Aspose.Cells v25.10 o posterior y se ejecuta en cualquier entorno .NET 6+.

## Requisitos previos

Antes de comenzar, asegúrate de tener:

* Una copia con licencia de **Aspose.Cells for .NET** (la prueba gratuita sirve para pruebas).
* SDK de .NET 6 o posterior instalado.
* Un IDE como Visual Studio 2022, VS Code o Rider.
* Conocimientos básicos de C#—no se requiere experiencia avanzada en automatización de Excel.

Puedes instalar el paquete NuGet de Aspose.Cells con:

```bash
dotnet add package Aspose.Cells
```

## Paso 1: Crear un libro y acceder a su primera hoja (save excel as txt)

Lo primero que haces cuando quieres **save Excel as TXT** es crear un objeto `Workbook`. Este objeto representa todo el archivo Excel en memoria.

```csharp
using Aspose.Cells;

// Create a new workbook (an empty Excel file)
Workbook workbook = new Workbook();

// Access the first worksheet (index 0)
Worksheet worksheet = workbook.Worksheets[0];
```

> **Por qué es importante:** La clase `Workbook` es el punto de entrada para todas las operaciones de hoja de cálculo. Al comenzar con un libro nuevo evitas cualquier formato oculto que pueda afectar la salida de texto plano.

## Paso 2: Escribir un número de alta precisión en una celda (write value to cell)

Ahora necesitas **write value to cell** A1. El método `PutValue` detecta automáticamente el tipo de datos y lo almacena como un valor numérico.

```csharp
// Write a high‑precision number into cell A1
worksheet.Cells["A1"].PutValue(12345.6789012345);
```

> **Consejo:** Si más adelante necesitas escribir cadenas, fechas o fórmulas, el mismo método `PutValue` funciona—solo pasa el tipo .NET correspondiente.

## Paso 3: Configurar las opciones de exportación para mantener solo la precisión necesaria (set significant digits)

Al exportar a un archivo TXT, a menudo deseas limitar la cantidad de dígitos para mantener el tamaño del archivo pequeño o para cumplir con una especificación posterior. La clase `TxtSaveOptions` proporciona la propiedad `SignificantDigits` para este propósito.

```csharp
// Configure TXT save options to retain only 6 significant digits
TxtSaveOptions txtSaveOptions = new TxtSaveOptions(SaveFormat.Txt)
{
    SignificantDigits = 6   // New option in v25.10
};
```

> **Por qué debes establecer dígitos significativos:** Sin esta configuración, Aspose.Cells escribe el valor de doble precisión completo, lo que puede producir cadenas largas como `12345.6789012345`. Establecer `SignificantDigits = 6` recorta la salida a `12345.7`, cumpliendo la mayoría de los requisitos de informes.

## Paso 4: Exportar el libro como archivo TXT (export excel to txt)

Finalmente, **export Excel to TXT** llamando a `Workbook.Save` con las opciones configuradas previamente.

```csharp
// Save the workbook as a TXT file using the configured options
string outputPath = @"C:\Temp\LimitedDigits.txt";
workbook.Save(outputPath, txtSaveOptions);
```

Cuando el código termina, `LimitedDigits.txt` contiene:

```
12345.7
```

> **Verificación del resultado:** Abre el archivo en cualquier editor de texto (Notepad, VS Code) para confirmar que solo aparecen seis dígitos significativos y que no aparecen comas extra ni delimitadores de tabulación.

## Ejemplo completo y ejecutable

A continuación tienes una aplicación de consola autocontenida que puedes copiar, pegar y ejecutar de inmediato.

```csharp
using System;
using Aspose.Cells;

namespace ExcelToTxtDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create workbook and get the first worksheet
            Workbook workbook = new Workbook();
            Worksheet worksheet = workbook.Worksheets[0];

            // 2️⃣ Write a high‑precision number to cell A1
            worksheet.Cells["A1"].PutValue(12345.6789012345);

            // 3️⃣ Set up TXT save options with 6 significant digits
            TxtSaveOptions txtOptions = new TxtSaveOptions(SaveFormat.Txt)
            {
                SignificantDigits = 6
            };

            // 4️⃣ Save as TXT
            string path = @"C:\Temp\LimitedDigits.txt";
            workbook.Save(path, txtOptions);

            Console.WriteLine($"Workbook exported to TXT at: {path}");
        }
    }
}
```

**Explicación de cada bloque**

| Bloque | Propósito |
|-------|-----------|
| `using Aspose.Cells;` | Importa el espacio de nombres Aspose.Cells necesario para `Workbook`, `Worksheet` y `TxtSaveOptions`. |
| `Workbook workbook = new Workbook();` | Instancia un libro de Excel vacío en memoria. |
| `worksheet.Cells["A1"].PutValue(...);` | **write value to cell** A1 con un número de doble precisión. |
| `TxtSaveOptions` | Configura el comportamiento **set significant digits** para la exportación TXT. |
| `workbook.Save(..., txtOptions);` | Ejecuta la operación **export excel to txt**, creando el archivo de texto plano. |

## Casos límite y consejos adicionales

| Escenario | Cómo manejarlo |
|----------|----------------|
| **Hojas de cálculo grandes** (muchas filas/columnas) | Usa `txtOptions.Encoding = Encoding.UTF8` si necesitas soporte Unicode, y considera transmitir el archivo con `Workbook.Save(Stream, txtOptions)` para evitar un alto consumo de memoria. |
| **Delimitadores personalizados** (valores separados por comas) | `TxtSaveOptions` también expone `Separator`—establece `','` para producir una salida estilo CSV manteniendo el formato TXT. |
| **Preservar fórmulas** | Establece `txtOptions.ExportFormulas = true` para escribir el texto de la fórmula en lugar del valor calculado. |
| **Separadores decimales específicos de la localidad** | Ajusta `txtOptions.DecimalSeparator` a `','` para configuraciones europeas. |
| **Múltiples hojas** | Recorre `workbook.Worksheets` y llama a `Save` para cada una, añadiendo el nombre de la hoja al nombre del archivo. |

## Preguntas frecuentes

**P: ¿`SignificantDigits` redondea o trunca?**  
R: Redondea al valor más cercano según la cantidad de dígitos significativos especificada, garantizando que la salida sea matemáticamente precisa a esa precisión.

**P: ¿Puedo exportar directamente a un flujo de memoria?**  
R: Sí. Reemplaza la ruta del archivo con una instancia de `MemoryStream`: `workbook.Save(stream, txtOptions);`. Esto es útil para APIs web que necesitan devolver el contenido TXT sin tocar el sistema de archivos.

**P: ¿Qué pasa si necesito conservar el formato original (p. ej., fechas)?**  
R: Usa `txtOptions.ExportFormattedValues = true`. Esto obliga a Aspose.Cells a escribir el texto mostrado en la celda en lugar del valor bruto.

## Conclusión

Ahora sabes cómo **save Excel as TXT** con control total sobre precisión, formato y ubicación de salida. Siguiendo los cuatro pasos—crear un libro, **write value to cell**, **set significant digits** y **export Excel to TXT**—puedes integrar la exportación a texto plano en cualquier aplicación .NET.

A continuación, explora temas relacionados como **export spreadsheet as TXT with custom delimiters**, **convert Excel to CSV**, o **use Aspose.Cells to generate JSON reports**. Cada uno de ellos se basa en los mismos conceptos centrales demostrados aquí, ofreciéndote un conjunto de herramientas versátil para el intercambio de datos entre plataformas.

¡Feliz codificación!

## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y funcionales con explicaciones paso a paso para ayudarte a dominar características adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Save Excel as Text – Complete C# Guide to Export Excel to TXT](/cells/english/net/converting-excel-files-to-other-formats/save-excel-as-text-complete-c-guide-to-export-excel-to-txt/)
- [Create New Workbook and Export Excel to TXT with Precision](/cells/english/net/excel-data-export-retrieval/create-new-workbook-and-export-excel-to-txt-with-precision/)
- [Create new workbook – Export Excel to TXT with Full Precision](/cells/english/net/converting-excel-files-to-other-formats/create-new-workbook-export-excel-to-txt-with-full-precision/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}