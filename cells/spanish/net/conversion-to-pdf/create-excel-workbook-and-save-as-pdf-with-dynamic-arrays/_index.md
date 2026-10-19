---
category: general
date: 2026-09-15
description: Crear un libro de Excel en C# y aprender a guardar el libro como PDF
  mientras se expanden matrices dinámicas usando la función EXPAND.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook
- save workbook as pdf
- spill dynamic array
- use expand function
- how to create dynamic array in excel
language: es
lastmod: 2026-09-15
og_description: Crea un libro de Excel en C# y guarda rápidamente el libro como PDF
  mientras utilizas la función EXPAND para expandir una matriz dinámica.
og_image_alt: Create Excel workbook screenshot showing dynamic array and PDF output
og_title: Crear libro de Excel y guardarlo como PDF con matrices dinámicas
schemas:
- author: Aspose
  dateModified: '2026-09-15'
  description: Create Excel workbook in C# and learn how to save workbook as PDF while
    spilling dynamic arrays using the EXPAND function.
  headline: Create Excel workbook and save as PDF with dynamic arrays
  type: TechArticle
tags:
- excel
- csharp
- aspose-cells
- pdf
- dynamic-array
title: Crear libro de Excel y guardarlo como PDF con matrices dinámicas
url: /es/net/conversion-to-pdf/create-excel-workbook-and-save-as-pdf-with-dynamic-arrays/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crear libro de Excel y guardarlo como PDF con matrices dinámicas

Si necesitas **crear un libro de Excel** programáticamente y luego **guardar el libro como PDF**, esta guía te muestra una solución completa, de extremo a extremo, en C#. También verás cómo **desbordar una matriz dinámica** usando la **función EXPAND**, que es la forma moderna de generar matrices sin VBA.  

Ya sea que estés construyendo un servicio de informes, una función de exportación para un sistema ERP, o un panel de control basado en datos, los pasos a continuación te permiten generar un libro, rellenarlo con datos de smart‑marker y producir un PDF que conserva características tipográficas avanzadas.

## Requisitos previos

Antes de comenzar, asegúrate de tener:

* .NET 6.0 o posterior (el código también funciona con .NET Framework 4.8)
* Una versión reciente de **Aspose.Cells for .NET** (v25.8 o más reciente) – proporciona `Workbook`, `PdfSaveOptions` y `SmartMarkerProcessor`.
* Un IDE como Visual Studio 2022 (cualquier editor que pueda compilar C# funciona).

Añade el paquete NuGet a tu proyecto:

```bash
dotnet add package Aspose.Cells --version 25.8
```

## Paso 1: Crear libro de Excel y configurar la primera hoja de cálculo

La primera tarea es **crear un libro de Excel** y obtener una referencia a la hoja de cálculo predeterminada. Esta hoja alojará la matriz dinámica y la plantilla de Smart Marker.

```csharp
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;
using System;

class Program
{
    static void Main()
    {
        // Create a new workbook in memory
        Workbook wb = new Workbook();

        // Get the first (default) worksheet
        Worksheet ws = wb.Worksheets[0];
```

*Por qué es importante*: Instanciar `Workbook` asigna la estructura interna del libro, mientras que acceder a `Worksheets[0]` te brinda una hoja lista para usar sin necesidad de añadir una manualmente.

## Paso 2: Desbordar una matriz dinámica usando la función EXPAND

La **función EXPAND** de Excel puede convertir un literal de matriz estática en un rango de desbordamiento de cualquier tamaño. Aquí le pedimos a Excel que expanda `{1,2,3}` a un rango de 5 filas × 1 columna que comienza en `A1`.

```csharp
        // Write the EXPAND formula into A1
        ws.Cells["A1"].Formula = "=EXPAND({1,2,3},5,1)";

        // Force calculation so the spill occurs immediately
        ws.Calculate();
```

*Por qué es importante*: Usar `EXPAND` evita bucles manuales en C#. El motor calcula el rango de desbordamiento y almacena los valores directamente en la hoja, que luego aparecen en el PDF.

## Paso 3: Guardar el libro como PDF preservando los selectores de variación de fuente

Cuando necesitas **guardar el libro como PDF**, también puedes habilitar características tipográficas avanzadas como los selectores de variación de fuente (disponibles a partir de Aspose.Cells v25.8). Esto garantiza que los PDFs rendericen correctamente scripts complejos.

```csharp
        // Configure PDF options
        PdfSaveOptions pdfOpts = new PdfSaveOptions
        {
            FontVariationSelectors = true   // keeps variation selectors for OpenType fonts
        };

        // Save the current workbook (with the spilled array) as PDF
        wb.Save(@"YOUR_DIRECTORY\VarSelector.pdf", pdfOpts);
```

*Por qué es importante*: Configurar `FontVariationSelectors` a `true` es esencial para idiomas que dependen de la variación de glifos (p. ej., chino, japonés, emoji). El PDF generado refleja la vista de Excel en pantalla.

## Paso 4: Insertar una plantilla Smart Marker que haga referencia a una fuente de datos anidada

Los Smart Markers te permiten incrustar marcadores de posición directamente en la hoja. La plantilla a continuación generará una lista de pedidos y sus artículos.

```csharp
        // Define a Smart Marker template in cell A1
        string template = "${Orders.OrderId}\n${Orders.Items:ItemName}\n";
        ws.Cells["A1"].PutValue(template);
```

*Por qué es importante*: Al colocar la plantilla en `A1`, le indicas a Aspose.Cells dónde comenzar a expandir los datos. La sintaxis `:` (`Items:ItemName`) indica al procesador que itere sobre una colección anidada.

## Paso 5: Definir la fuente de datos anidada (pedidos que contienen artículos)

Creamos una matriz anónima de pedidos, cada uno con su propia colección de objetos de artículo. Esto refleja un escenario típico maestro‑detalle.

```csharp
        // Sample nested data source
        var orders = new[]
        {
            new
            {
                OrderId = 1,
                Items = new[]
                {
                    new { ItemName = "Apple" },
                    new { ItemName = "Banana" }
                }
            },
            new
            {
                OrderId = 2,
                Items = new[]
                {
                    new { ItemName = "Carrot" }
                }
            }
        };
```

*Por qué es importante*: La estructura anidada demuestra **cómo crear una matriz dinámica en Excel** mediante Smart Markers, sin escribir VBA ni bucles manuales de celdas.

## Paso 6: Procesar los Smart Markers y guardar el archivo Excel final

Ahora entregamos el libro y la fuente de datos a `SmartMarkerProcessor`. Después del procesamiento, los marcadores de posición se reemplazan por filas reales, y guardamos el resultado como un archivo `.xlsx` normal.

```csharp
        // Process the Smart Markers
        SmartMarkerProcessor processor = new SmartMarkerProcessor();
        processor.Process(wb, orders);

        // Save the populated workbook
        wb.Save(@"YOUR_DIRECTORY\NestedSmartMarker.xlsx");
    }
}
```

*Por qué es importante*: `SmartMarkerProcessor` expande automáticamente la plantilla, crea las filas necesarias y las rellena con datos. El libro final puede abrirse en Excel para verificar que cada pedido y sus artículos aparecen correctamente.

## Resultado esperado

* **VarSelector.pdf** – un archivo PDF que muestra los números 1‑3 desbordándose en cinco filas, renderizado con cualquier variación de fuente OpenType que hayas habilitado.
* **NestedSmartMarker.xlsx** – un archivo Excel con las siguientes filas (comenzando en `A1`):

| OrderId | ItemName |
|---------|----------|
| 1       | Apple    |
| 1       | Banana   |
| 2       | Carrot   |

La versión PDF conserva el mismo desbordamiento numérico porque el estado de la hoja se guardó antes del procesamiento de Smart Marker; puedes volver a guardar el PDF después del procesamiento si también necesitas los datos finales en PDF.

## Consejos y errores comunes

| Consejo | Explicación |
|-----|-------------|
| **Reutilizar el mismo `PdfSaveOptions`** | Crear el objeto de opciones una vez y reutilizarlo evita sutiles diferencias en el renderizado (p. ej., selectores de variación ausentes). |
| **Llamar a `ws.Calculate()` después de establecer fórmulas** | Sin un cálculo explícito, el rango de desbordamiento puede quedar vacío al inspeccionar el libro programáticamente. |
| **Colocar plantillas Smart Marker en una hoja limpia** | Mezclar plantillas con datos existentes puede causar inserciones de filas inesperadas. Usa una hoja dedicada si es posible. |
| **Prestar atención a las rutas de archivo** | Usa `Path.Combine(Environment.CurrentDirectory, "output.pdf")` para evitar directorios codificados en duro en diferentes máquinas. |
| **Comprobar la versión** | `FontVariationSelectors` solo está disponible a partir de la versión 25.8; versiones anteriores ignorarán la propiedad sin lanzar una excepción. |

## Próximos pasos

Ahora que sabes cómo **crear un libro de Excel**, **desbordar una matriz dinámica** y **guardar el libro como PDF**, puedes explorar:

* Agregar gráficos o imágenes antes de la conversión a PDF.
* Exportar el mismo libro a otros formatos (p. ej., HTML, CSV) usando sobrecargas de `Save`.
* Usar **expresiones Smart Marker** (`${Orders.Total:SUM(Items.Price)}`) para calcular agregados al vuelo.
* Integrar este código en una API ASP.NET Core para que los usuarios puedan descargar el PDF generado directamente desde un endpoint web.

---

**Resumen** – Este tutorial te mostró cómo **crear un libro de Excel**, usar la **función EXPAND** para **desbordar una matriz dinámica**, incrustar un **Smart Marker** que funciona con una fuente de datos anidada y, finalmente, **guardar el libro como PDF** preservando características tipográficas avanzadas. El ejemplo completo y ejecutable puede copiarse en cualquier proyecto C# y adaptarse a tus propias estructuras de datos. ¡Feliz codificación!

## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que se basan en las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y funcionales con explicaciones paso a paso para ayudarte a dominar características adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Create and Save Excel Workbook as PDF in ASP.NET Using Aspose.Cells](/cells/english/net/workbook-operations/create-save-excel-workbook-pdf-aspnet-aspose-cells/)
- [How to Create and Save an Excel Workbook as ODS Using Aspose.Cells for .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)
- [How to Create and Save an Excel Workbook as SVG using Aspose.Cells for Java](/cells/english/java/workbook-operations/create-save-workbook-svg-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}