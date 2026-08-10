---
category: general
date: 2026-08-07
description: Crear Excel a partir de JSON usando Aspose.Cells Smart Marker – aprende
  cómo rellenar una plantilla de Excel, aplicar nombres de hoja dinámicos y generar
  múltiples hojas de cálculo.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel from json
- populate excel template
- dynamic sheet naming
- generate multiple worksheets
- aspose.cells smart marker
language: es
lastmod: 2026-08-07
og_description: Crea Excel a partir de JSON con Aspose.Cells Smart Marker para rellenar
  rápidamente plantillas, usar nombres de hoja dinámicos y generar múltiples hojas
  de cálculo.
og_image_alt: Screenshot of generated Excel workbook with multiple dynamically named
  sheets
og_title: Crear Excel a partir de JSON – Guía de Smart Marker de Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-08-07'
  description: Create Excel from JSON using Aspose.Cells Smart Marker – learn how
    to populate an Excel template, apply dynamic sheet naming, and generate multiple
    worksheets.
  headline: Create Excel from JSON with Aspose.Cells Smart Marker
  type: TechArticle
- description: Create Excel from JSON using Aspose.Cells Smart Marker – learn how
    to populate an Excel template, apply dynamic sheet naming, and generate multiple
    worksheets.
  name: Create Excel from JSON with Aspose.Cells Smart Marker
  steps:
  - name: Define the JSON‑compatible source data
    text: '```csharp // Step 1: Define the source data that will be merged into the
      workbook var ordersData = new { Orders = new[] { new { Id = 1, Items = new[]
      { "Apple", "Banana" } }, new { Id = 2, Items = new[] { "Orange" } } } }; ```'
  - name: Prepare the workbook template and insert a Smart Marker
    text: '```csharp // Step 2: Create a new workbook and place a Smart Marker that
      references the data collection var workbook = new Workbook(); // creates an
      empty workbook workbook.Worksheets[0].Cells["A1"].PutValue("{{Orders}}"); ```'
  - name: Configure dynamic sheet naming
    text: '```csharp // Step 3: Configure how duplicated detail sheets should be named
      during processing var smartMarkerOptions = new SmartMarkerOptions { // {0} will
      be replaced by an incremental index (DetailSheet_1, DetailSheet_2, …) DetailSheetNewName
      = "DetailSheet_{0}" }; ```'
  - name: Process the template with the data and naming options
    text: '```csharp // Step 4: Process the workbook with the data and the naming
      options var smartMarkerProcessor = new SmartMarkerProcessor(workbook, smartMarkerOptions);
      smartMarkerProcessor.Process(ordersData); ```'
  - name: Save the resulting workbook
    text: '```csharp // Step 5: Save the resulting workbook – the detail sheets are
      created automatically workbook.Save("YOUR_DIRECTORY/SmartMarkerDupSheets.xlsx");
      ```'
  - name: Populate Excel template with additional fields
    text: 'If your JSON includes more properties (e.g., `CustomerName`, `TotalAmount`),
      add corresponding markers to the template:'
  - name: Generate multiple worksheets from nested collections
    text: 'You can create a second level of duplication by placing a marker inside
      the detail sheet that references a nested collection, such as `Items`:'
  - name: Custom naming with data from the record
    text: '```csharp var smartMarkerOptions = new SmartMarkerOptions { DetailSheetNewName
      = "Order_{Id}" }; ```'
  - name: Next steps
    text: '* Explore **conditional formatting** inside the detail sheet to highlight
      high‑value orders. * Replace the anonymous object with a strongly typed model
      deserialized via `System.Text.Json`. * Combine Smart Markers with **PivotTable**
      generation for advanced reporting.'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: Crear Excel a partir de JSON con Smart Marker de Aspose.Cells
url: /es/net/smart-markers-dynamic-data/create-excel-from-json-with-aspose-cells-smart-marker/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crear Excel a partir de JSON con Aspose.Cells Smart Marker

Si necesitas **crear Excel a partir de JSON**, este tutorial muestra una solución completa y lista para producción. Verás cómo **poblar una plantilla de Excel**, configurar **nombres de hoja dinámicos** y **generar múltiples hojas** automáticamente con el motor **Aspose.Cells Smart Marker**.

La guía te lleva paso a paso por cada etapa requerida, desde definir el objeto fuente similar a JSON hasta guardar el libro final. No se necesitan scripts externos, y el código se ejecuta en .NET 6 o superior.

## Lo que lograrás

* Cargar un objeto de datos estilo JSON en memoria.  
* Insertar un marcador Smart Marker en una plantilla de libro.  
* Aplicar un patrón de nombres para que cada hoja de detalle duplicada reciba un nombre único.  
* Procesar la plantilla para crear una hoja separada por cada pedido en la colección.  
* Guardar el resultado como un archivo `.xlsx` listo para su consumo posterior.

Requisitos previos: Visual Studio 2022 (o cualquier IDE de C#), .NET 6+, y el paquete NuGet **Aspose.Cells**. El ejemplo usa C#; los mismos conceptos se aplican a VB.NET u otros lenguajes .NET.

## Crear Excel a partir de JSON – flujo de trabajo general

Las siguientes secciones dividen el flujo de trabajo en cinco pasos lógicos. Cada paso incluye el código exacto que necesitas, una explicación de por qué es importante y consejos para escalar la solución.

### Paso 1: Definir los datos de origen compatibles con JSON

```csharp
// Step 1: Define the source data that will be merged into the workbook
var ordersData = new
{
    Orders = new[]
    {
        new { Id = 1, Items = new[] { "Apple", "Banana" } },
        new { Id = 2, Items = new[] { "Orange" } }
    }
};
```

**Por qué es importante** – El objeto `ordersData` refleja la estructura que recibirías de una API JSON real. Aspose.Cells Smart Marker lee propiedades públicas, por lo que un tipo anónimo funciona siempre que los nombres de las propiedades coincidan con las etiquetas del marcador (`{{Orders}}`). Cuando luego sustituyas el tipo anónimo por un objeto JSON deserializado, no será necesario cambiar el código.

### Paso 2: Preparar la plantilla del libro e insertar un Smart Marker

```csharp
// Step 2: Create a new workbook and place a Smart Marker that references the data collection
var workbook = new Workbook();                     // creates an empty workbook
workbook.Worksheets[0].Cells["A1"].PutValue("{{Orders}}");
```

**Por qué es importante** – El marcador `{{Orders}}` indica al procesador que itere sobre la colección `Orders`. Colocar el marcador en la celda `A1` de la primera hoja convierte esa hoja en la hoja *maestra*. El procesador clonará esta hoja para cada pedido, conservando cualquier formato que añadas después.

> **Consejo:** Si dispones de una plantilla pre‑diseñada (p. ej., con encabezados, fórmulas o estilos), cárgala con `new Workbook("Template.xlsx")` en lugar de crear un libro vacío.

### Paso 3: Configurar nombres de hoja dinámicos

```csharp
// Step 3: Configure how duplicated detail sheets should be named during processing
var smartMarkerOptions = new SmartMarkerOptions
{
    // {0} will be replaced by an incremental index (DetailSheet_1, DetailSheet_2, …)
    DetailSheetNewName = "DetailSheet_{0}"
};
```

**Por qué es importante** – Por defecto Aspose.Cells nombra las hojas duplicadas como `Sheet1`, `Sheet2`, etc. El patrón `DetailSheetNewName` inserta un índice incremental (`{0}`) para que cada hoja reciba un nombre significativo. Puedes incrustar marcadores adicionales (p. ej., `{Id}`) para incluir datos del registro actual.

> **Pro tip:** Usa `DetailSheetNewName = "Order_{Id}"` para nombrar las hojas con el identificador del pedido, lo que facilita la navegación en libros grandes.

### Paso 4: Procesar la plantilla con los datos y las opciones de nombrado

```csharp
// Step 4: Process the workbook with the data and the naming options
var smartMarkerProcessor = new SmartMarkerProcessor(workbook, smartMarkerOptions);
smartMarkerProcessor.Process(ordersData);
```

**Por qué es importante** – El `SmartMarkerProcessor` combina `ordersData` con el libro, crea una nueva hoja por cada elemento en `Orders` y aplica el patrón de nombres definido anteriormente. El procesador también expande cualquier colección anidada (p. ej., `Items`) si añades marcadores adicionales dentro de la hoja de detalle.

### Paso 5: Guardar el libro resultante

```csharp
// Step 5: Save the resulting workbook – the detail sheets are created automatically
workbook.Save("YOUR_DIRECTORY/SmartMarkerDupSheets.xlsx");
```

**Por qué es importante** – El método `Save` escribe el libro completamente poblado en disco. El archivo ahora contiene una hoja maestra (que puede ocultarse o eliminarse) y una serie de hojas de detalle nombradas `DetailSheet_1`, `DetailSheet_2`, …, cada una con los datos de un solo pedido.

#### Salida esperada

| Nombre de hoja    | Contenido (simplificado)                     |
|-------------------|----------------------------------------------|
| DetailSheet_1     | Orden Id = 1, Artículos: Apple, Banana       |
| DetailSheet_2     | Orden Id = 2, Artículos: Orange              |

Todas las hojas conservan cualquier formato que hayas aplicado a la hoja maestra antes del procesamiento.

## Variaciones avanzadas

### Poblar la plantilla de Excel con campos adicionales

Si tu JSON incluye más propiedades (p. ej., `CustomerName`, `TotalAmount`), agrega los marcadores correspondientes a la plantilla:

```csharp
workbook.Worksheets[0].Cells["B1"].PutValue("{{CustomerName}}");
workbook.Worksheets[0].Cells["C1"].PutValue("{{TotalAmount}}");
```

El procesador reemplazará cada marcador con el valor de la propiedad coincidente.

### Generar múltiples hojas a partir de colecciones anidadas

Puedes crear un segundo nivel de duplicación colocando un marcador dentro de la hoja de detalle que haga referencia a una colección anidada, como `Items`:

```csharp
// Inside the detail sheet (e.g., cell A2)
workbook.Worksheets[0].Cells["A2"].PutValue("{{Items}}");

// Inside the same sheet, cell B2 will list each item
workbook.Worksheets[0].Cells["B2"].PutValue("{{Items}}");
```

Durante el procesamiento, Aspose.Cells crea una fila por cada elemento del arreglo `Items`, permitiéndote generar listas detalladas por pedido.

### Nomenclatura personalizada con datos del registro

```csharp
var smartMarkerOptions = new SmartMarkerOptions
{
    DetailSheetNewName = "Order_{Id}"
};
```

Ahora las hojas se nombran `Order_1`, `Order_2`, lo que alinea el nombre de la hoja con el identificador comercial.

## Problemas comunes y cómo evitarlos

| Problema                                                            | Solución |
|---------------------------------------------------------------------|----------|
| El texto del marcador no coincide con el nombre de la propiedad (distinción entre mayúsculas y minúsculas) | Asegúrate de que el marcador (`{{Orders}}`) coincida exactamente con la propiedad, incluida la capitalización. |
| La plantilla contiene celdas combinadas que abarcan la región del marcador | Descombina las celdas o coloca el marcador en una única celda sin combinar para evitar cambios inesperados en el diseño. |
| Colecciones JSON grandes generan presión de memoria | Procesa los datos en lotes o transmite el JSON a un `DataTable` y usa `SmartMarkerProcessor` con `DataSource`. |
| La ruta del archivo guardado es inválida | Usa `Path.Combine(Environment.CurrentDirectory, "output.xlsx")` o verifica los permisos de escritura. |

## Ejemplo completo funcional

```csharp
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

class Program
{
    static void Main()
    {
        // 1️⃣ Define JSON‑compatible data
        var ordersData = new
        {
            Orders = new[]
            {
                new { Id = 1, Items = new[] { "Apple", "Banana" } },
                new { Id = 2, Items = new[] { "Orange" } }
            }
        };

        // 2️⃣ Create workbook and add master Smart Marker
        var workbook = new Workbook();
        workbook.Worksheets[0].Cells["A1"].PutValue("{{Orders}}");

        // 3️⃣ Set up dynamic sheet naming
        var smartMarkerOptions = new SmartMarkerOptions
        {
            DetailSheetNewName = "DetailSheet_{0}"
        };

        // 4️⃣ Process template with data
        var processor = new SmartMarkerProcessor(workbook, smartMarkerOptions);
        processor.Process(ordersData);

        // 5️⃣ Save the result
        string outputPath = Path.Combine(
            Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
            "SmartMarkerDupSheets.xlsx");
        workbook.Save(outputPath);
    }
}
```

Ejecutar el programa genera un archivo Excel en el escritorio que contiene dos hojas de detalle (`DetailSheet_1` y `DetailSheet_2`). Cada hoja refleja el registro de pedido correspondiente.

## Conclusión

Ahora sabes cómo **crear Excel a partir de JSON** usando **Aspose.Cells Smart Marker**, cómo **poblar una plantilla de Excel**, aplicar **nombres de hoja dinámicos** y **generar múltiples hojas** automáticamente. El mismo patrón escala a decenas o miles de registros, soporta colecciones anidadas e integra sin problemas cualquier biblioteca de deserialización JSON de .NET.

### Próximos pasos

* Explora **formato condicional** dentro de la hoja de detalle para resaltar pedidos de alto valor.  
* Sustituye el objeto anónimo por un modelo fuertemente tipado deserializado mediante `System.Text.Json`.  
* Combina Smart Markers con la generación de **PivotTable** para informes avanzados.  

Experimenta con el patrón de nombres, agrega más marcadores e integra este flujo de trabajo en tus pipelines de exportación de datos existentes. ¡Feliz codificación!

## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos con explicaciones paso a paso para ayudarte a dominar funcionalidades adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Generar informes dinámicos de Excel usando Aspose.Cells .NET Smart Markers](/cells/english/net/templates-reporting/generate-excel-reports-aspose-cells-net-smart-markers/)
- [Poblar Excel con datos usando Aspose.Cells y Smart Markers](/cells/english/java/cell-operations/populate-excel-aspose-cells-smart-markers/)
- [Cómo crear y combinar libros de Excel usando Aspose.Cells para Java | Guía completa](/cells/english/java/workbook-operations/create-merge-excel-workbooks-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}