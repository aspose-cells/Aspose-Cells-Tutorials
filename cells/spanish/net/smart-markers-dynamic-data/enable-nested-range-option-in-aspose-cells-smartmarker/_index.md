---
category: general
date: 2026-06-05
description: Habilite la opción de rango anidado en Aspose.Cells SmartMarkerProcessor
  para manejar datos jerárquicos de Excel sin esfuerzo. Aprenda sobre marcadores inteligentes,
  rangos anidados y mejores prácticas.
draft: false
keywords:
- enable nested range option
- SmartMarkerProcessor
- nested range handling
- Excel smart markers
- Aspose.Cells
language: es
og_description: Habilite la opción de rango anidado en Aspose.Cells SmartMarkerProcessor
  para trabajar con datos jerárquicos. Guía completa con código, consejos y trampas.
og_title: Habilitar la opción de rango anidado en Aspose.Cells SmartMarker
schemas:
- author: Aspose
  dateModified: '2026-06-05'
  description: Enable nested range option in Aspose.Cells SmartMarkerProcessor to
    handle hierarchical Excel data effortlessly. Learn smart markers, nested ranges,
    and best practices.
  headline: Enable Nested Range Option in Aspose.Cells SmartMarker
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
- Smart Markers
title: Habilitar la opción de rango anidado en Aspose.Cells SmartMarker
url: /es/net/smart-markers-dynamic-data/enable-nested-range-option-in-aspose-cells-smartmarker/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Habilitar la opción de rango anidado en Aspose.Cells SmartMarker

¿Alguna vez te has preguntado cómo **habilitar la opción de rango anidado** en Aspose.Cells SmartMarkerProcessor? Habilitar esta función te permite trabajar con datos jerárquicos como pedidos y líneas de artículo sin problemas.  

En este tutorial recorreremos un escenario del mundo real: alimentar una lista de pedidos con elementos anidados en una plantilla de Excel usando smart markers. Al final tendrás un libro de trabajo totalmente funcional, comprenderás **SmartMarkerProcessor** y sabrás por qué la bandera de **manejo de rangos anidados** es importante.

Cubriremos:

* Preparar un objeto anónimo en C# que imite datos maestro‑detalle.  
* Activar la bandera **nested range** en el procesador.  
* Ejecutar el procesador contra un libro de trabajo y verificar el resultado.  

No se requieren frameworks sofisticados, solo .NET 6+ y la biblioteca Aspose.Cells para .NET. Si alguna vez has tenido problemas con filas repetidas dentro de filas repetidas, esta guía es para ti.

---

## Preparar datos jerárquicos para los Smart Markers de Excel

Primero, necesitamos una fuente de datos que refleje una relación padre‑hijo. El ejemplo a continuación crea un objeto anónimo con un pedido que contiene dos artículos.

```csharp
// Step 1: Define hierarchical data with orders and their items
var orderData = new
{
    Orders = new[]
    {
        new
        {
            Id = 1,
            Items = new[]
            {
                new { Name = "A" },
                new { Name = "B" }
            }
        }
    }
};
```

**¿Por qué esta forma?**  
Los smart markers leen los nombres de las propiedades (`Orders`, `Items`) y generan automáticamente rangos anidados cuando el procesador está configurado correctamente. Piensa en ello como una mini‑base de datos que la plantilla de Excel iterará.

> **Consejo profesional:** Usa nombres de propiedad significativos que coincidan con los marcadores que colocaste en la plantilla (p. ej., `&=Orders.Id&`, `&=Items.Name&`). Los nombres que no coinciden son una causa frecuente de errores de “sin datos”.

---

## Configurar SmartMarkerProcessor y habilitar el rango anidado

Ahora creamos el procesador y activamos el interruptor **NestedRange**. Esta única línea indica a Aspose.Cells que trate las colecciones hijas como tablas internas.

```csharp
// Step 2: Create a SmartMarkerProcessor and enable nested range handling
SmartMarkerProcessor processor = new SmartMarkerProcessor();
processor.Options.NestedRange = true;   // <‑‑ enable nested range option
```

**¿Qué hace realmente `NestedRange = true`?**  
Cuando está activado, el procesador construye un rango separado para cada colección hija y lo anida dentro del rango padre. Sin ello, solo se renderizaría la colección de nivel superior (`Orders`), y las filas internas de `Items` se ignorarían.

> **Cuidado:** Si habilitas los rangos anidados pero olvidas marcar el rango hijo en la plantilla (usando `&=Items.Start&` / `&=Items.End&`), el procesador lanzará una `SmartMarkerException`. Siempre verifica dos veces la sintaxis de tus marcadores.

---

## Cargar o crear la plantilla del libro de trabajo

Para la demostración generaremos un libro de trabajo simple sobre la marcha, pero en producción normalmente comenzarás a partir de un archivo `.xlsx` existente que ya contiene smart markers.

```csharp
// Step 3: Create a workbook with a simple template
Workbook wb = new Workbook();
Worksheet ws = wb.Worksheets[0];

// Header row
ws.Cells["A1"].PutValue("Order ID");
ws.Cells["B1"].PutValue("Item Name");

// Smart marker row for Orders (parent)
//   &amp;=Orders.Start&amp; and &amp;=Orders.End&amp; define the range for each order.
ws.Cells["A2"].PutValue("&=Orders.Start&");
ws.Cells["A2"].PutValue("&=Orders.Id&");
ws.Cells["B2"].PutValue("&=Orders.End&");

// Smart marker row for Items (child)
//   Nested inside the Orders range.
ws.Cells["A3"].PutValue("&=Items.Start&");
ws.Cells["A3"].PutValue("&=Items.Name&");
ws.Cells["B3"].PutValue("&=Items.End&");
```

Observa los marcadores `&=Orders.Start&` / `&=Orders.End&`: indican al procesador dónde comienza y termina cada bloque de pedido. El mismo patrón se aplica al rango hijo `Items`.

---

## Procesar el libro de trabajo con Smart Markers

Con los datos y el procesador listos, el paso final es una única línea que combina todo.

```csharp
// Step 4: Apply the data to the workbook using smart markers
processor.Process(wb, orderData);
```

Después de esta llamada, el libro de trabajo contendrá:

| Order ID | Item Name |
|----------|-----------|
| 1        | A         |
| 1        | B         |

Puedes guardar el resultado en disco o enviarlo como flujo a un cliente:

```csharp
wb.Save("NestedRangeResult.xlsx");
```

---

## Verificar la salida y manejar problemas comunes

### Resultado esperado

Abre `NestedRangeResult.xlsx` y deberías ver dos filas bajo el encabezado del único pedido, cada fila mostrando el nombre del artículo (`A` y `B`). El ID del pedido se repite para cada fila hija, exactamente lo que los rangos anidados están diseñados para hacer.

### Problemas típicos

| Síntoma | Causa probable | Solución |
|---------|----------------|----------|
| No aparecen filas hijas | `NestedRange` dejado como `false` | Establece `processor.Options.NestedRange = true`. |
| Los marcadores aparecen como texto plano | Error tipográfico en la sintaxis del marcador (`&=Orders.Start&` vs `&=Orders.Start`) | Asegúrate de que tanto `&=` como el `&` final estén presentes. |
| Filas duplicadas para cada pedido | Falta el marcador `&=Orders.End&` | Añade el marcador de cierre para delimitar el rango padre. |

---

## Ejemplo completo (listo para copiar y pegar)

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Define hierarchical data
        var orderData = new
        {
            Orders = new[]
            {
                new
                {
                    Id = 1,
                    Items = new[]
                    {
                        new { Name = "A" },
                        new { Name = "B" }
                    }
                }
            }
        };

        // 2️⃣ Create processor and enable nested range option
        SmartMarkerProcessor processor = new SmartMarkerProcessor();
        processor.Options.NestedRange = true;   // enable nested range option

        // 3️⃣ Build a simple workbook template with smart markers
        Workbook wb = new Workbook();
        Worksheet ws = wb.Worksheets[0];

        ws.Cells["A1"].PutValue("Order ID");
        ws.Cells["B1"].PutValue("Item Name");

        // Parent range markers
        ws.Cells["A2"].PutValue("&=Orders.Start&");
        ws.Cells["A2"].PutValue("&=Orders.Id&");
        ws.Cells["B2"].PutValue("&=Orders.End&");

        // Child range markers (nested)
        ws.Cells["A3"].PutValue("&=Items.Start&");
        ws.Cells["A3"].PutValue("&=Items.Name&");
        ws.Cells["B3"].PutValue("&=Items.End&");

        // 4️⃣ Process the workbook
        processor.Process(wb, orderData);

        // 5️⃣ Save the result
        wb.Save("NestedRangeResult.xlsx");
        Console.WriteLine("Workbook generated – check NestedRangeResult.xlsx");
    }
}
```

Ejecuta el programa, abre el archivo generado y verás las filas anidadas pobladas exactamente como se muestra en la tabla anterior.

---

## Conclusión

Acabas de aprender cómo **habilitar la opción de rango anidado** en Aspose.Cells SmartMarkerProcessor, convirtiendo una plantilla de Excel plana en un potente generador de informes maestro‑detalle. Al activar `processor.Options.NestedRange = true`, la biblioteca crea automáticamente tablas internas para colecciones hijas, ahorrándote bucles manuales de inserción de filas.

¿Qué sigue? Prueba agregar un segundo nivel de anidamiento (p. ej., pedido → artículos → sub‑componentes), experimenta con el estilo de las filas generadas o cambia a una plantilla pre‑diseñada que incluya gráficos y fórmulas. La combinación de **Excel smart markers** y **manejo de rangos anidados** es una base sólida para cualquier solución de generación automática de informes.

¿Tienes preguntas o un escenario complicado? Deja un comentario abajo, ¡y feliz codificación!

## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y explicaciones paso a paso para ayudarte a dominar funciones adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Handle Nested Objects with Smart Markers Aspose.Cells](/cells/english/net/smart-markers-dynamic-data/nested-objects-smart-markers/)
- [Populate Excel with Nested Data Using Aspose.Cells&#58; A Comprehensive Guide](/cells/english/java/data-manipulation/populate-excel-nested-data-aspose-cells-java/)
- [Populate Excel Nested Data Aspose Cells Java](/cells/german/java/data-manipulation/populate-excel-nested-data-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}