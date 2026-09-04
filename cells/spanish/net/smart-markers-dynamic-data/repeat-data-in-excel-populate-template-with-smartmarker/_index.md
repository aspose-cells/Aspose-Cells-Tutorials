---
category: general
date: 2026-02-21
description: Repite datos en Excel rápidamente usando SmartMarker—aprende cómo rellenar
  una plantilla de Excel y repetir filas sin esfuerzo.
draft: false
keywords:
- repeat data in excel
- populate excel template
- how to repeat rows
- repeat rows in excel
- populate excel from data
language: es
og_description: Repetir datos en Excel usando SmartMarker. Aprende cómo rellenar una
  plantilla de Excel, repetir filas y automatizar tus hojas de cálculo.
og_title: repetir datos en Excel – Rellenar plantilla con SmartMarker
tags:
- excel
- csharp
- smartmarker
- automation
title: Repetir datos en Excel – Rellenar plantilla con SmartMarker
url: /es/net/smart-markers-dynamic-data/repeat-data-in-excel-populate-template-with-smartmarker/
---

with shortcodes unchanged.

Proceed.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# repetir datos en excel – Poblar plantilla con SmartMarker

¿Alguna vez necesitaste **repetir datos en Excel** pero no sabías cómo evitar el copiar‑pegar manual? No estás solo. En muchos escenarios de informes tienes una lista de elementos que debe expandirse en filas automáticamente, y hacerlo a mano es una receta para errores.

La cuestión es que, usando el **SmartMarkerProcessor** de la biblioteca **GemBox.Spreadsheet**, puedes **poblar una plantilla de Excel** con una sola línea de C# y hacer que las filas se repitan por cada elemento de tu colección. En esta guía recorreremos los pasos exactos, te mostraremos el código completo y explicaremos por qué cada pieza es importante, para que puedas repetir filas en Excel sin sudar.

## Lo que aprenderás

* Cómo definir la estructura de datos que impulsa la operación de repetición.  
* Cómo conectar un `SmartMarkerProcessor` a un libro que contiene una hoja de plantilla oculta.  
* Cómo el marcador `${Repeat:Item}` se expande en múltiples filas automáticamente.  
* Consejos para manejar casos límite como colecciones vacías o formato personalizado.  

Al final de este tutorial podrás **poblar excel desde datos** de una manera escalable, fácil de mantener y que funciona con cualquier proyecto .NET.

---

## Requisitos previos

* .NET 6.0 o posterior (el código usa características modernas de C#).  
* El paquete NuGet **GemBox.Spreadsheet** (la versión gratuita funciona hasta 150 filas).  
* Un archivo de plantilla de Excel básico (`Template.xlsx`) con una hoja oculta llamada `HiddenTemplate`.  
* Familiaridad con objetos C# y LINQ es útil pero no obligatoria.

---

## Paso 1 – Definir la estructura de datos para la repetición

Primero, necesitas una fuente de datos que el motor SmartMarker pueda iterar. En la mayoría de las aplicaciones reales esto provendrá de una base de datos, una API o un archivo CSV. Para mayor claridad usaremos un tipo anónimo con una única propiedad llamada `Item` que contiene un arreglo de cadenas.

```csharp
// Step 1: Define the data that will be repeated in the template
var repeatData = new { Item = new[] { "A", "B", "C" } };
```

> **Por qué es importante:** El marcador `${Repeat:Item}` dentro de la plantilla de Excel busca una propiedad llamada `Item`. Si cambias el nombre de la propiedad, actualiza el marcador en consecuencia. Este acoplamiento estrecho garantiza que la plantilla permanezca sincronizada con tu código, facilitando **poblar la plantilla de excel** sin adivinar nombres de columnas.

### Variaciones comunes

* **Objetos complejos:** En lugar de un simple arreglo de cadenas puedes proporcionar una lista de objetos (`new[] { new { Name = "A", Qty = 10 } }`). El marcador repetirá filas y podrás referenciar `${Item.Name}` y `${Item.Qty}` en la hoja.  
* **Colecciones vacías:** Si `Item` está vacío, SmartMarker simplemente elimina el bloque de repetición, dejando la plantilla intacta—ideal para secciones opcionales.

---

## Paso 2 – Crear el SmartMarkerProcessor para la hoja de plantilla oculta

A continuación, carga tu libro y crea una instancia de `SmartMarkerProcessor`. Señálalo al libro que contiene la hoja de plantilla oculta; SmartMarker copiará esa hoja a una visible y expandirá los marcadores de repetición.

```csharp
using GemBox.Spreadsheet;

// Load the workbook that holds the hidden template sheet.
var wb = ExcelFile.Load("Template.xlsx");

// Step 2: Create a SmartMarkerProcessor for the workbook that holds the hidden template sheet
var processor = new SmartMarkerProcessor(wb);
```

> **Consejo profesional:** Si tienes varias plantillas en el mismo archivo, puedes especificar el nombre de la hoja origen al llamar a `processor.Process`. Esto ayuda cuando necesitas **repetir filas en excel** para diferentes secciones de un informe.

### Manejo de casos límite

* **Hoja de plantilla ausente:** Envuelve la carga en un try/catch y registra un error claro—esto evita fallos silenciosos cuando la ruta del archivo es incorrecta.  
* **Conjuntos de datos grandes:** Para miles de filas, considera transmitir la salida a un archivo (`processor.Save`) en lugar de mantener todo en memoria.

---

## Paso 3 – Aplicar los datos y expandir el marcador `${Repeat:Item}`

Ahora llega la línea mágica que realmente repite las filas. Pasa el objeto que creaste en el Paso 1 a `processor.Process`. SmartMarker localizará cada marcador `${Repeat:Item}`, duplicará la fila por cada elemento y reemplazará los marcadores de posición con los valores reales.

```csharp
// Step 3: Apply the data to the template, expanding the ${Repeat:Item} marker
processor.Process(repeatData);

// Save the resulting workbook.
wb.Save("Result.xlsx");
```

### Lo que deberías ver

Al abrir `Result.xlsx`, la hoja de plantilla oculta se ha copiado a una nueva hoja visible (por defecto llamada `Sheet1`). La fila que contenía `${Repeat:Item}` ahora aparece tres veces, con las celdas mostrando **A**, **B** y **C** respectivamente.

| Item |
|------|
| A    |
| B    |
| C    |

Si añadiste más columnas como `${Item.Price}`, esas se rellenarían automáticamente desde la fuente de datos.

---

## Cómo repetir filas en Excel sin SmartMarker (comparación rápida)

| Enfoque                | Complejidad del código | Mantenimiento | Rendimiento |
|------------------------|------------------------|---------------|-------------|
| Copiar‑pegar manual    | Alta                   | Baja          | Pobre       |
| Macro VBA              | Media                  | Media         | Buena       |
| **SmartMarkerProcessor**| Baja                   | Alta          | Excelente   |

Como puedes observar, usar SmartMarker para **repetir datos en excel** te brinda la separación más limpia entre el diseño de la plantilla y la lógica de negocio. Además, es independiente del lenguaje—existen conceptos similares en bibliotecas de Java, Python y JavaScript.

---

## Consejos avanzados y errores comunes

### 1. Formatear las filas repetidas

SmartMarker copia la fila completa—incluidos estilos de celda, bordes y formato condicional. Si necesitas un estilo diferente para la primera o última fila, añade marcadores extra como `${If:Item.IsFirst}` y usa fórmulas condicionales dentro de Excel.

### 2. Trabajar con conjuntos de datos grandes

Al manejar > 10 000 filas, desactiva el cálculo automático de Excel antes del procesamiento:

```csharp
wb.WorkbookOptions = new WorkbookOptions { RecalculateAllFormulas = false };
```

Vuelve a activarlo después de guardar para mantener el rendimiento ágil.

### 3. Poblar Excel desde datos en una base de datos real

```csharp
var orders = dbContext.Orders
    .Where(o => o.Date >= start && o.Date <= end)
    .Select(o => new { o.OrderId, o.CustomerName, o.Total })
    .ToArray();

processor.Process(new { Order = orders });
```

Luego usa `${Repeat:Order}` en la plantilla para listar cada pedido. Este patrón muestra lo fácil que es **poblar excel desde datos** directamente desde Entity Framework.

### 4. Usar varios bloques de repetición

Puedes tener varios marcadores `${Repeat:...}` en la misma hoja o en hojas diferentes. SmartMarker los procesa secuencialmente, por lo que el orden solo importa si un bloque depende del resultado de otro.

---

## Ejemplo completo ejecutable

A continuación tienes una aplicación de consola autocontenida que puedes pegar en Visual Studio y ejecutar de inmediato. Demuestra los tres pasos más el guardado del archivo.

```csharp
using System;
using GemBox.Spreadsheet;

class Program
{
    static void Main()
    {
        // License free version (up to 150 rows). For production use, set your license key.
        SpreadsheetInfo.SetLicense("FREE-LIMITED-KEY");

        // 1️⃣ Define the data to repeat.
        var repeatData = new { Item = new[] { "A", "B", "C" } };

        // 2️⃣ Load the template workbook (ensure Template.xlsx exists next to the exe).
        var wb = ExcelFile.Load("Template.xlsx");

        // Create processor bound to the workbook.
        var processor = new SmartMarkerProcessor(wb);

        // 3️⃣ Process the data – this expands the ${Repeat:Item} marker.
        processor.Process(repeatData);

        // Save the populated workbook.
        wb.Save("Result.xlsx");

        Console.WriteLine("Excel file generated successfully – check Result.xlsx");
    }
}
```

**Salida esperada:** `Result.xlsx` contiene una hoja donde la fila con `${Repeat:Item}` aparece tres veces, mostrando A, B y C. No se requieren ajustes manuales.

---

## Conclusión

Ahora sabes cómo **repetir datos en excel** de manera eficiente aprovechando el SmartMarkerProcessor. Definiendo un objeto de datos sencillo, cargando una plantilla de libro y llamando a `Process`, puedes **poblar la plantilla de excel**, **repetir filas en excel**, y en general **

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}