---
category: general
date: 2026-02-14
description: Crea un objeto de datos maestro en C# y genera la hoja de detalle sin
  esfuerzo. Aprende el flujo de trabajo completo de SmartMarker con ejemplos de código
  prácticos.
draft: false
keywords:
- create master data object
- generate detail sheet
- smartmarker processing
- worksheet automation
- c# data binding
language: es
og_description: Crea un objeto de datos maestros en C# y genera una hoja de detalle
  con SmartMarker. Sigue nuestro tutorial detallado para una solución lista para ejecutar.
og_title: Crear objeto de datos maestros – Guía completa
tags:
- C#
- SmartMarker
- Excel Automation
title: Crear objeto de datos maestros – Guía paso a paso para generar la hoja de detalle
url: /es/net/smart-markers-dynamic-data/create-master-data-object-step-by-step-guide-to-generate-det/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crear objeto de datos maestro – Tutorial completo

¿Alguna vez necesitaste **crear objeto de datos maestro** para una hoja de cálculo de Excel pero no sabías cómo enlazarlo a una hoja de detalle SmartMarker? No estás solo. En muchos escenarios de informes, el objeto maestro impulsa una hoja de detalle dinámica, y lograr la conexión correcta puede sentirse como armar un rompecabezas sin la imagen.  

En esta guía recorreremos todo el proceso: construir el objeto de datos maestro, configurar las opciones de SmartMarker para **generar hoja de detalle**, y finalmente ejecutar el procesador. Al final tendrás un fragmento ejecutable que puedes pegar en cualquier proyecto .NET que use la biblioteca GrapeCity Documents for Excel (GcExcel).

## Lo que necesitarás

- .NET 6+ (o .NET Framework 4.7.2) con una referencia a `GcExcel.dll`
- Familiaridad básica con C# (variables, tipos anónimos, inicializadores de objetos)
- Un libro de Excel que ya contenga etiquetas SmartMarker como `{{OrderId}}` y una tabla para los artículos de línea
- Visual Studio, Rider o cualquier editor que prefieras

Eso es todo—no se requieren paquetes NuGet adicionales más allá de la distribución principal de GcExcel.

## Paso 1: Crear el objeto de datos maestro

Lo primero que debes hacer es **crear objeto de datos maestro** que refleje la estructura esperada por las etiquetas SmartMarker. Piensa en él como un pequeño modelo de informe en memoria.

```csharp
// Step 1: Build the master data object that feeds the SmartMarkers.
// It contains an OrderId and a collection of line items.
var orderData = new
{
    OrderId = 1,
    Items = new[]
    {
        new { Product = "A", Quantity = 2 },
        new { Product = "B", Quantity = 5 }
    }
};
```

¿Por qué usar un tipo anónimo aquí? Porque te permite definir un contenedor ligero sin declarar una clase completa—perfecto para demostraciones rápidas o cuando la forma es poco probable que cambie. Si más adelante necesitas un modelo reutilizable, simplemente reemplaza `var` por un POCO adecuado.

> **Consejo profesional:** Mantén los nombres de las propiedades (`OrderId`, `Product`, `Quantity`) idénticos a los marcadores de posición en tu hoja; SmartMarker los compara sin distinguir mayúsculas y minúsculas.

## Paso 2: Configurar opciones de SmartMarker para generar una hoja de detalle

Ahora indicamos a SmartMarker que queremos una hoja de cálculo separada para la tabla de artículos de línea. Aquí es donde entra en juego la palabra clave **generate detail sheet**.

```csharp
// Step 2: Set up SmartMarker options.
// Enabling DetailSheet creates a new sheet for each master record.
var smartMarkerOptions = new SmartMarkerOptions
{
    DetailSheet = true,
    // The new sheet will be named using the OrderId value.
    DetailSheetNewName = "Order_{OrderId}"
};
```

El patrón `DetailSheetNewName` usa marcadores de posición entre llaves que se reemplazan en tiempo de ejecución. En nuestro ejemplo la hoja se llamará `Order_1`. Si más adelante iteras sobre varios pedidos, cada uno obtendrá su propia pestaña—exactamente lo que la mayoría de los contadores esperan.

## Paso 3: Ejecutar el procesador SmartMarker

Con los datos y las opciones listos, el paso final es invocar el procesador sobre la hoja de cálculo objetivo.

```csharp
// Step 3: Execute SmartMarker processing on the worksheet.
// 'worksheet' is an IWorksheet instance that points to the template sheet.
worksheet.SmartMarkerProcessor.StartSmartMarkerProcessing(orderData, smartMarkerOptions);
```

Detrás de escena, SmartMarker escanea la hoja en busca de etiquetas, inserta los valores de `orderData` y, como `DetailSheet` está en `true`, clona la plantilla en una nueva hoja llamada `Order_1`. Todos los artículos de línea aparecen en el área de detalle, conservando cualquier formato que hayas aplicado en la plantilla.

### Ejemplo completo funcionando

A continuación tienes un programa de consola autocontenido que abre un libro de plantilla (`Template.xlsx`), ejecuta los tres pasos y guarda el resultado como `Result.xlsx`. Puedes copiar‑pegar esto en un nuevo proyecto de consola y pulsar **F5**.

```csharp
using System;
using GrapeCity.Documents.Excel;

class Program
{
    static void Main()
    {
        // Load the Excel template that contains SmartMarker tags.
        var workbook = new Workbook();
        workbook.Open("Template.xlsx");

        // -------------------------------------------------
        // Step 1: Create the master data object.
        // -------------------------------------------------
        var orderData = new
        {
            OrderId = 1,
            Items = new[]
            {
                new { Product = "A", Quantity = 2 },
                new { Product = "B", Quantity = 5 }
            }
        };

        // -------------------------------------------------
        // Step 2: Configure SmartMarker options to generate detail sheet.
        // -------------------------------------------------
        var smartMarkerOptions = new SmartMarkerOptions
        {
            DetailSheet = true,
            DetailSheetNewName = "Order_{OrderId}"
        };

        // -------------------------------------------------
        // Step 3: Process the worksheet.
        // -------------------------------------------------
        // Assume the first sheet holds the master template.
        var worksheet = workbook.Worksheets[0];
        worksheet.SmartMarkerProcessor.StartSmartMarkerProcessing(orderData, smartMarkerOptions);

        // Save the populated workbook.
        workbook.Save("Result.xlsx");
        Console.WriteLine("Done! Check Result.xlsx – a new sheet named Order_1 should exist.");
    }
}
```

#### Salida esperada

- **Result.xlsx** contiene una hoja llamada `Order_1`.
- La celda `A1` (o donde hayas colocado `{{OrderId}}`) ahora muestra `1`.
- Una tabla que comienza en el bloque SmartMarker lista dos filas:
  | Product | Quantity |
  |---------|----------|
  | A       | 2        |
  | B       | 5        |

Si abres el archivo, verás que se preserva el formato de la plantilla—bordes, fuentes, formato condicional—todo intacto.

## Preguntas frecuentes y casos límite

### ¿Qué pasa si tengo varios pedidos?

Envuelve el objeto maestro en una colección y deja que SmartMarker itere automáticamente:

```csharp
var orders = new[]
{
    new {
        OrderId = 1,
        Items = new[] { new { Product = "A", Quantity = 2 } }
    },
    new {
        OrderId = 2,
        Items = new[] { new { Product = "C", Quantity = 3 } }
    }
};

worksheet.SmartMarkerProcessor.StartSmartMarkerProcessing(orders, smartMarkerOptions);
```

Cada pedido genera su propia hoja (`Order_1`, `Order_2`, …). El procesador trata la matriz externa como la colección maestra.

### ¿Cómo controlo la posición de la hoja?

Establece `smartMarkerOptions.DetailSheetInsertIndex = 2;` para colocar la nueva hoja después de la segunda pestaña, o usa `DetailSheetInsertAfter = "Summary"` para insertarla después de una hoja con nombre.

### ¿Puedo desactivar la hoja de detalle para una ejecución concreta?

Simplemente cambia `DetailSheet = false;`. SmartMarker entonces escribirá los artículos de línea en la misma hoja donde se encuentran las etiquetas maestras.

### ¿Qué ocurre con conjuntos de datos muy grandes?

SmartMarker transmite los datos de forma eficiente, pero si superas unas cuantas cientos de miles de filas podrías alcanzar el límite de 1 048 576 filas de Excel. En ese caso divide los datos en varios registros maestros o considera exportar a CSV.

## Visión general visual

![Diagrama que ilustra cómo crear objeto de datos maestro y generar hoja de detalle usando SmartMarker](/images/smartmarker-flow.png)

*La ilustración muestra el flujo desde el objeto maestro en C# → opciones de SmartMarker → procesamiento de la hoja de cálculo → nueva hoja de detalle.*

## Conclusión

Ahora sabes cómo **crear objeto de datos maestro** en C# y configurar SmartMarker para **generar hoja de detalle** automáticamente. El patrón de tres pasos—datos, opciones, procesador—cubre la mayoría de los escenarios de automatización de Excel con GcExcel.  

A partir de aquí podrías explorar:

- Añadir datos de encabezado/pie de página a cada hoja de detalle
- Usar formato condicional basado en el estado del pedido
- Exportar el libro generado a PDF con `workbook.SaveAsPdf(...)`

Siéntete libre de experimentar, romper cosas y luego volver a ensamblarlas. Esa es la forma más rápida de dominar la automatización de hojas de cálculo. ¡Feliz codificación!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}