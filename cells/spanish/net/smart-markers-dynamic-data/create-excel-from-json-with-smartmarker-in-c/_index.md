---
category: general
date: 2026-11-16
description: Crea Excel a partir de JSON usando SmartMarker. Aprende cómo convertir
  JSON a Excel, incrustar JSON en Excel y guardar el libro de trabajo xlsx en minutos.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel from json
- convert json to excel
- embed json in excel
- save workbook xlsx
language: es
lastmod: 2026-11-16
og_description: Crea Excel a partir de JSON rápidamente. Este tutorial muestra cómo
  convertir JSON a Excel, incrustar JSON en Excel y guardar el libro de trabajo xlsx
  con Aspose.Cells.
og_image_alt: Screenshot of an Excel worksheet showing JSON data inserted into a single
  cell
og_title: Crear Excel a partir de JSON con SmartMarker – guía paso a paso en C#
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: Create Excel from JSON using SmartMarker. Learn how to convert JSON
    to Excel, embed JSON in Excel, and save workbook xlsx in minutes.
  headline: Create Excel from JSON with SmartMarker in C#
  type: TechArticle
- description: Create Excel from JSON using SmartMarker. Learn how to convert JSON
    to Excel, embed JSON in Excel, and save workbook xlsx in minutes.
  name: Create Excel from JSON with SmartMarker in C#
  steps:
  - name: Build and run the console app (`dotnet run`).
    text: Build and run the console app (`dotnet run`).
  - name: Verify the console prints the full path to the generated file.
    text: Verify the console prints the full path to the generated file.
  - name: Open the file in Excel or any spreadsheet viewer.
    text: Open the file in Excel or any spreadsheet viewer.
  - name: Confirm that cell A1 holds the JSON array string exactly as shown above.
    text: Confirm that cell A1 holds the JSON array string exactly as shown above.
  type: HowTo
tags:
- SmartMarker
- Aspose.Cells
- C#
- JSON
title: Crear Excel a partir de JSON con SmartMarker en C#
url: /es/net/smart-markers-dynamic-data/create-excel-from-json-with-smartmarker-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crear Excel a partir de JSON con SmartMarker en C#

Si necesitas **crear Excel a partir de JSON** en un proyecto .NET, esta guía muestra una solución completa y ejecutable. Usando el procesador Smart Marker de Aspose.Cells puedes **convertir JSON a Excel**, incrustar la cadena JSON directamente en una celda y **guardar el libro xlsx** sin escribir código de análisis manual.

Verás cómo registrar una fuente de datos JSON, insertar un Smart Marker que genera todo el arreglo como una única cadena JSON, procesar la hoja de cálculo y, finalmente, escribir el archivo en disco. Al final del tutorial podrás generar un archivo Excel que contiene la carga JSON original en la celda A1, listo para procesamiento posterior o generación de informes.

## Requisitos previos

- .NET 6.0 o posterior (el código también funciona con .NET Framework 4.7+)
- Aspose.Cells para .NET (paquete NuGet `Aspose.Cells`)
- Conocimientos básicos de C# y formato JSON
- Un IDE como Visual Studio o VS Code

## Paso 1: Configurar el proyecto e importar espacios de nombres

Crea una nueva aplicación de consola y agrega el paquete Aspose.Cells:

```bash
dotnet new console -n JsonToExcelDemo
cd JsonToExcelDemo
dotnet add package Aspose.Cells
```

Luego incluye los espacios de nombres requeridos al inicio de `Program.cs`:

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;
```

**¿Por qué?**  
`Aspose.Cells` proporciona el modelo del libro, mientras que `Aspose.Cells.SmartMarkers` contiene la clase `SmartMarkerProcessor` que interpreta los marcadores `&=` en la hoja de cálculo.

## Paso 2: Definir la fuente de datos JSON

Coloca la cadena JSON en una variable. En este ejemplo tenemos un arreglo de órdenes:

```csharp
// Step 2: Define the JSON data source
string json = @"{
    ""Orders"": [
        { ""Id"": 1, ""Amount"": 100 },
        { ""Id"": 2, ""Amount"": 150 }
    ]
}";
```

**¿Por qué?**  
Smart Marker funciona con cualquier JSON bien formado. Mantener el JSON en una cadena permite registrarlo directamente sin necesidad de un archivo en disco.

## Paso 3: Registrar el JSON con SmartMarkerProcessor

Crea una instancia de `SmartMarkerProcessor` y asocia la cadena JSON con un nombre que referenciarás más adelante en la hoja:

```csharp
// Step 3: Register the JSON data with the Smart Marker processor
SmartMarkerProcessor processor = new SmartMarkerProcessor();
processor.RegisterJsonDataSource("OrdersJson", json);
```

**¿Por qué?**  
`RegisterJsonDataSource` analiza el JSON y pone su jerarquía a disposición de los Smart Markers. El nombre `"OrdersJson"` se convierte en el objeto raíz en las expresiones del marcador.

## Paso 4: Crear un libro e insertar el Smart Marker

Instancia un nuevo libro, obtén su primera hoja y escribe un Smart Marker en la celda A1 que generará todo el arreglo `Orders` como una única cadena JSON:

```csharp
// Step 4: Create a workbook and get the first worksheet
Worksheet ws = new Workbook().Worksheets[0];

// Insert a Smart Marker that outputs the whole array as a single JSON string
ws.Cells["A1"].PutValue("&=OrdersJson.Orders.ArrayAsSingle");
```

**¿Por qué?**  
La expresión `OrdersJson.Orders.ArrayAsSingle` indica a Smart Marker que tome el arreglo `Orders` y lo serialice nuevamente a JSON, colocando el resultado en la celda de destino. Esta es la forma más directa de **incrustar JSON en Excel**.

## Paso 5: Procesar la hoja de cálculo

Ejecuta el procesador para que reemplace el marcador con la cadena JSON real:

```csharp
// Step 5: Process the worksheet – the marker is replaced with the JSON array string
processor.Process(ws);
```

**¿Por qué?**  
El procesamiento examina cada celda en busca de marcadores `&=`, los evalúa contra las fuentes de datos registradas y escribe el valor evaluado de vuelta en la hoja.

## Paso 6: Guardar el libro como archivo .xlsx

Finalmente, escribe el libro en disco. Ajusta la ruta a una carpeta donde tengas permisos de escritura:

```csharp
// Step 6: Save the workbook
string outputPath = Path.Combine(
    Environment.CurrentDirectory,
    "JsonArraySingleCell.xlsx");

ws.Workbook.Save(outputPath, SaveFormat.Xlsx);
Console.WriteLine($"Workbook saved to: {outputPath}");
```

**¿Por qué?**  
`SaveFormat.Xlsx` garantiza que el archivo se almacene en el formato moderno Office Open XML, cumpliendo con el requisito de **guardar libro xlsx**.

## Código fuente completo

Uniendo todas las piezas, aquí tienes el programa completo y listo para ejecutarse:

```csharp
using System;
using System.IO;
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

class Program
{
    static void Main()
    {
        // Step 2: Define the JSON data source
        string json = @"{
            ""Orders"": [
                { ""Id"": 1, ""Amount"": 100 },
                { ""Id"": 2, ""Amount"": 150 }
            ]
        }";

        // Step 3: Register the JSON data with the Smart Marker processor
        SmartMarkerProcessor processor = new SmartMarkerProcessor();
        processor.RegisterJsonDataSource("OrdersJson", json);

        // Step 4: Create a workbook and get the first worksheet
        Worksheet ws = new Workbook().Worksheets[0];

        // Insert a Smart Marker that will output the whole array as a single JSON string
        ws.Cells["A1"].PutValue("&=OrdersJson.Orders.ArrayAsSingle");

        // Step 5: Process the worksheet – the marker is replaced with the JSON array string
        processor.Process(ws);

        // Step 6: Save the workbook
        string outputPath = Path.Combine(
            Environment.CurrentDirectory,
            "JsonArraySingleCell.xlsx");
        ws.Workbook.Save(outputPath, SaveFormat.Xlsx);

        Console.WriteLine($"Workbook saved to: {outputPath}");
    }
}
```

### Resultado esperado en Excel

Abre `JsonArraySingleCell.xlsx`. La celda A1 contendrá:

```
[{"Id":1,"Amount":100},{"Id":2,"Amount":150}]
```

La cadena JSON es una representación compacta del arreglo `Orders` original, lo que facilita su transporte o consumo en flujos de trabajo posteriores basados en Excel.

## Variaciones comunes y casos límite

| Situación | Ajuste |
|-----------|--------|
| **Múltiples objetos JSON** | Registra cada objeto con un nombre distinto (p. ej., `processor.RegisterJsonDataSource("CustomerJson", customerJson);`) y haz referencia a ellos con marcadores separados. |
| **JSON con formato legible en una celda** | Usa la opción `ArrayAsSinglePretty`: `ws.Cells["A1"].PutValue("&=OrdersJson.Orders.ArrayAsSinglePretty");` |
| **Cargas JSON muy grandes** | Considera escribir el JSON en una hoja oculta o usar la conversión a `DataTable` para mejorar el rendimiento. |
| **Incrustar JSON en varias celdas** | Coloca diferentes marcadores en otras celdas, por ejemplo, `&=OrdersJson.Orders[0].Id` para extraer campos individuales. |

**Consejo profesional:** Cuando trabajes con JSON muy grande, incrementa el búfer de memoria del libro (`WorkbookSettings.MemorySetting`) para evitar `OutOfMemoryException`.

## Probar la solución

1. Compila y ejecuta la aplicación de consola (`dotnet run`).  
2. Verifica que la consola imprima la ruta completa del archivo generado.  
3. Abre el archivo en Excel o cualquier visor de hojas de cálculo.  
4. Confirma que la celda A1 contiene la cadena JSON del arreglo exactamente como se muestra arriba.

Si la celda muestra el texto del marcador (`&=OrdersJson...`) en lugar del JSON, verifica que el procesador se haya invocado **después** de colocar el marcador y que la cadena JSON sea válida.

## Conclusión

Ahora sabes cómo **crear Excel a partir de JSON** usando Smart Markers de Aspose.Cells, cómo **convertir JSON a Excel**, incrustar la carga JSON directamente en una celda y **guardar libro xlsx** con una sola línea de código. Este enfoque elimina el análisis manual, funciona con cualquier estructura JSON y produce un archivo Excel limpio y conforme a estándares.

### Próximos pasos

- Explora los **bucles Smart Marker** (`&=OrdersJson.Orders`) para generar una fila por cada orden en lugar de una única cadena JSON.  
- Combina esta técnica con **fórmulas de Excel** para calcular totales a partir de los datos incrustados.  
- Investiga la **lectura de JSON desde Excel** usando `Workbook.Load` y `SmartMarkerProcessor` en sentido inverso.

¡Siéntete libre de experimentar con diferentes formas de JSON, múltiples hojas de cálculo o exportar a otros formatos como CSV o PDF. Feliz codificación!

## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y explicaciones paso a paso para ayudarte a dominar funciones adicionales de la API y explorar enfoques alternativos en tus propios proyectos.

- [Create Excel from JSON with Aspose.Cells Smart Marker](/cells/english/net/smart-markers-dynamic-data/create-excel-from-json-with-aspose-cells-smart-marker/)
- [Create Excel Workbook from JSON – Complete Aspose.Cells Guide](/cells/english/net/data-loading-and-parsing/create-excel-workbook-from-json-complete-aspose-cells-guide/)
- [Save Excel Workbook from JSON – Complete Guide](/cells/english/net/templates-reporting/save-excel-workbook-from-json-complete-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}