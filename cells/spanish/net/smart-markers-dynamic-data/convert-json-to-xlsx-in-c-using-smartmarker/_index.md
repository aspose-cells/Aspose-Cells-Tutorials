---
category: general
date: 2026-10-10
description: Convertir JSON a XLSX en C# con SmartMarker – aprende cómo importar JSON
  a Excel y rellenar un libro de trabajo programáticamente.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert json to xlsx
- how to import json into excel
- populate excel from json
- create excel workbook c#
- import json into worksheet
language: es
lastmod: 2026-10-10
og_description: Convierte JSON a XLSX en C# con SmartMarker. Sigue esta guía para
  importar JSON a Excel, crear un libro de Excel en C# y rellenar Excel a partir de
  JSON.
og_image_alt: Diagram showing JSON data being converted to an XLSX workbook using
  C#
og_title: Convertir JSON a XLSX en C# – guía paso a paso
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: Convert JSON to XLSX in C# with SmartMarker – learn how to import JSON
    into Excel and populate a workbook programmatically.
  headline: Convert JSON to XLSX in C# using SmartMarker
  type: TechArticle
- description: Convert JSON to XLSX in C# with SmartMarker – learn how to import JSON
    into Excel and populate a workbook programmatically.
  name: Convert JSON to XLSX in C# using SmartMarker
  steps:
  - name: '**Create an Excel workbook** in memory.'
    text: '**Create an Excel workbook** in memory.'
  - name: '**Load JSON data** that represents a simple list of people.'
    text: '**Load JSON data** that represents a simple list of people.'
  - name: '**Configure SmartMarker** to treat the JSON array as a single record (`ArrayAsSingle
      = true`).'
    text: '**Configure SmartMarker** to treat the JSON array as a single record (`ArrayAsSingle
      = true`).'
  - name: '**Process the worksheet**, letting SmartMarker replace markers with the
      JSON values.'
    text: '**Process the worksheet**, letting SmartMarker replace markers with the
      JSON values.'
  - name: '**Save the workbook** as an `.xlsx` file.'
    text: '**Save the workbook** as an `.xlsx` file.'
  type: HowTo
tags:
- JSON
- Excel
- C#
- Aspose.Cells
title: Convertir JSON a XLSX en C# usando SmartMarker
url: /es/net/smart-markers-dynamic-data/convert-json-to-xlsx-in-c-using-smartmarker/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Convertir JSON a XLSX en C# usando SmartMarker

Si necesitas **convertir JSON a XLSX en C#**, esta guía te muestra cómo **importar JSON a Excel** y **poblar Excel desde JSON** con solo unas pocas líneas de código. Verás cómo **crear un libro de Excel C#**, configurar el procesador SmartMarker y, finalmente, **importar JSON a celdas de la hoja de cálculo**.

> **Lo que obtendrás** – un ejemplo completamente ejecutable que lee un arreglo JSON, lo trata como un solo registro y escribe los datos en un archivo `.xlsx` listo para informes o análisis posteriores.

## Convertir JSON a XLSX – visión general

SmartMarker es parte de la biblioteca Aspose.Cells y te permite vincular JSON, XML o cualquier objeto .NET directamente a una plantilla de Excel. En este tutorial nosotros:

1. **Crear un libro de Excel** en memoria.
2. **Cargar datos JSON** que representan una lista simple de personas.
3. **Configurar SmartMarker** para tratar el arreglo JSON como un solo registro (`ArrayAsSingle = true`).
4. **Procesar la hoja de cálculo**, permitiendo que SmartMarker reemplace los marcadores con los valores JSON.
5. **Guardar el libro** como un archivo `.xlsx`.

Todo el flujo se ejecuta en .NET 6+ y solo requiere el paquete NuGet `Aspose.Cells`.

## Paso 1: Crear un libro de Excel en C#

Primero, agrega el paquete Aspose.Cells a tu proyecto:

```bash
dotnet add package Aspose.Cells
```

Ahora puedes instanciar un nuevo `Workbook`. El libro comienza vacío, pero puedes agregar una hoja de cálculo y colocar etiquetas SmartMarker donde deberían aparecer los datos JSON.

```csharp
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

namespace JsonToXlsxDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Create a new workbook (this also creates the default first worksheet)
            Workbook workbook = new Workbook();

            // Optional: give the first sheet a friendly name
            Worksheet sheet = workbook.Worksheets[0];
            sheet.Name = "People";
```

> **Por qué creamos el libro primero** – SmartMarker funciona contra un objeto `Worksheet` existente; el libro proporciona el contenedor para todas las operaciones posteriores.

## Paso 2: Definir datos JSON y configurar SmartMarker

Usaremos una pequeña carga JSON que enumera dos personas. La opción `ArrayAsSingle` indica a SmartMarker que trate todo el arreglo como un único registro lógico, lo cual es ideal cuando deseas una tabla simple sin bucles anidados.

```csharp
            // Step 2: Define the JSON data to populate the worksheet
            string jsonData = "[{'Name':'John','Age':30},{'Name':'Anna','Age':25}]";

            // Step 3: Initialise the SmartMarker processor
            SmartMarkerProcessor processor = new SmartMarkerProcessor();

            // Important: treat the JSON array as a single record
            processor.Options.ArrayAsSingle = true;
```

> **Consejo:** Si omites `ArrayAsSingle`, SmartMarker intentará crear un registro separado para cada elemento del arreglo, lo que puede generar filas duplicadas o un diseño inesperado.

## Paso 3: Insertar etiquetas SmartMarker en la hoja de cálculo

Las etiquetas SmartMarker son marcadores de posición de texto plano rodeados por `&`. Colócalas en las celdas donde deseas que aparezcan los valores JSON. En este ejemplo escribimos las etiquetas directamente mediante código, pero también podrías diseñar una plantilla en Excel primero.

```csharp
            // Step 4: Write SmartMarker tags into the first row (header) and second row (data)
            sheet.Cells["A1"].PutValue("Name");                // Header
            sheet.Cells["B1"].PutValue("Age");                 // Header
            sheet.Cells["A2"].PutValue("&=Name&");             // Data placeholder
            sheet.Cells["B2"].PutValue("&=Age&");              // Data placeholder
```

> **Explicación:** `&=Name&` indica a SmartMarker que reemplace la celda con el campo `Name` del objeto JSON, mientras que `&=Age&` hace lo mismo para `Age`.

## Paso 4: Procesar la hoja de cálculo – poblar Excel desde JSON

Ahora permite que SmartMarker lea la cadena JSON y rellene los marcadores.

```csharp
            // Step 5: Apply the JSON data to the worksheet
            processor.Process(sheet, jsonData);
```

Detrás de escena, SmartMarker analiza `jsonData`, asigna cada propiedad del objeto a la etiqueta correspondiente y expande las filas automáticamente porque `ArrayAsSingle` es `true`. Después del procesamiento, la hoja de cálculo se ve así:

| Nombre | Edad |
|--------|------|
| John | 30 |
| Anna | 25 |

## Paso 5: Guardar el archivo XLSX

Finalmente, escribe el libro poblado en disco.

```csharp
            // Step 6: Save the populated workbook as an .xlsx file
            string outputPath = Path.Combine(
                Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
                "SmartMarkerJson.xlsx");

            workbook.Save(outputPath, SaveFormat.Xlsx);
            Console.WriteLine($"Workbook saved to {outputPath}");
        }
    }
}
```

Ejecutar el programa crea `SmartMarkerJson.xlsx` en tu escritorio. Abrir el archivo en Excel muestra una tabla limpia con los datos JSON importados correctamente.

## Problemas comunes al importar JSON en la hoja de cálculo

| Problema | Por qué ocurre | Cómo evitarlo |
|----------|----------------|---------------|
| **Etiquetas SmartMarker faltantes** | SmartMarker solo reemplaza celdas que contienen `&=...&`. | Verifica dos veces la ortografía exacta de la etiqueta y su capitalización. |
| **Formato JSON incorrecto** | Las comillas simples (`'`) no son JSON válido para el analizador incorporado. | Usa comillas dobles (`"` ) o permite que Aspose.Cells maneje el formato flexible como se muestra. |
| **Arreglo tratado como múltiples registros** | El valor predeterminado de `ArrayAsSingle` es `false`. | Establece `processor.Options.ArrayAsSingle = true` cuando deseas una tabla plana. |
| **Guardando en una carpeta de solo lectura** | `workbook.Save` lanza una excepción. | Elige un directorio con permisos de escritura (p.ej., Escritorio o una carpeta temporal). |

## Extender la solución

- **Múltiples hojas de cálculo:** Crea hojas adicionales y llama a `processor.Process` en cada una con diferentes fuentes JSON.
- **Estilos:** Después del procesamiento, aplica estilos a las celdas (fuentes, bordes) como cualquier operación regular de Aspose.Cells.
- **Grandes conjuntos de datos:** Para miles de filas, considera transmitir el libro para reducir el uso de memoria (`WorkbookDesigner` o `SaveOptions` con `EnableMemoryOptimization`).

## Conclusión

Ahora sabes cómo **convertir JSON a XLSX en C#** usando Aspose.Cells SmartMarker. El flujo de trabajo completo—**crear libro de Excel C#**, agregar etiquetas SmartMarker, configurar el procesador, **poblar Excel desde JSON**, y guardar el archivo—te permite **importar JSON en celdas de la hoja de cálculo** con código mínimo.

Siéntete libre de experimentar con estructuras JSON más complejas, agregar fórmulas o generar gráficos directamente a partir de los datos poblados. Si disfrutaste esta guía, prueba el siguiente tutorial sobre **cómo importar JSON a Excel** para crear gráficos o sobre **crear libro de Excel C#** con formato avanzado.

---


## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que se basan en las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y funcionales con explicaciones paso a paso para ayudarte a dominar funciones adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Convertir JSON a Excel con C# – Guía paso a paso](/cells/english/net/smart-markers-dynamic-data/convert-json-to-excel-with-c-step-by-step-guide/)
- [Cómo insertar JSON en una plantilla de Excel – Paso a paso](/cells/english/net/data-loading-and-parsing/how-to-insert-json-into-excel-template-step-by-step/)
- [Crear libro de Excel C# – Insertar JSON y guardar como XLSX](/cells/english/net/excel-data-import-export/create-excel-workbook-c-insert-json-and-save-as-xlsx/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}