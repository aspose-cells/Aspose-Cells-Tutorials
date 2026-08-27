---
category: general
date: 2026-02-14
description: 'Automatiza la generación de facturas con SmartMarker: aprende a repetir
  hojas de cálculo, nombrarlas dinámicamente y dominar la nomenclatura dinámica de
  hojas en minutos.'
draft: false
keywords:
- automate invoice generation
- how to name worksheets
- how to repeat worksheet
- dynamic worksheet naming
language: es
og_description: Automatiza la generación de facturas con SmartMarker. Esta guía muestra
  cómo repetir hojas de cálculo, nombrarlas dinámicamente y dominar la nomenclatura
  dinámica de hojas.
og_title: Automatizar la generación de facturas – Nomenclatura dinámica de hojas de
  cálculo y repetición
tags:
- C#
- SmartMarker
- Excel Automation
title: Automatizar la generación de facturas – Nomenclatura dinámica de hojas de cálculo
  y repetición en C#
url: /es/net/smart-markers-dynamic-data/automate-invoice-generation-dynamic-worksheet-naming-repeati/
---

with bold formatting and code formatting.

Proceed.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Automatizar la generación de facturas – Nomenclatura dinámica de hojas y repetición en C#

¿Alguna vez te has preguntado cómo **automatizar la generación de facturas** sin copiar manualmente hojas para cada pedido? No estás solo. Muchos desarrolladores se topan con un obstáculo cuando necesitan una hoja separada por factura pero también quieren que el nombre de la hoja refleje el número de pedido. En este tutorial resolveremos ese problema usando `SmartMarkerProcessor` de SmartMarker y te mostraremos **cómo nombrar hojas** de forma dinámica mientras también cubrimos **cómo repetir una hoja** para cada registro. Al final tendrás un ejemplo listo‑para‑ejecutar en C# que produce un libro donde cada factura vive en su propia pestaña con un nombre adecuado.

Recorreremos cada paso—desde obtener los pedidos de una fuente de datos hasta configurar `SmartMarkerOptions` para la nomenclatura dinámica de hojas. No se requieren documentos externos; todo lo que necesitas está aquí. Solo un conocimiento básico de C# y una referencia a la biblioteca Aspose.Cells (o cualquier motor compatible con SmartMarker) será suficiente.

---

## Qué vas a construir

- Recuperar una colección de objetos **Order**.
- Configurar SmartMarker para **repetir una hoja** por cada pedido.
- Aplicar **nomenclatura dinámica de hojas** usando el marcador `{OrderId}`.
- Generar un archivo Excel donde cada pestaña se llame `Invoice_12345`, `Invoice_67890`, etc.
- Verificar la salida abriendo el libro de trabajo.

---

## Requisitos previos

- .NET 6.0 o posterior (el código también compila con .NET 5+).
- Aspose.Cells para .NET (o cualquier biblioteca que implemente SmartMarker). Instálalo vía NuGet:

```bash
dotnet add package Aspose.Cells
```

- Una clase básica `Order` (puedes reemplazarla con tu propio DTO).

---

## Paso 1: Configurar el proyecto y el modelo

Primero, crea una nueva aplicación de consola y define el modelo de datos que representa un pedido.

```csharp
using System;
using System.Collections.Generic;
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

namespace InvoiceAutomation
{
    // Simple POCO representing an order – replace fields as needed
    public class Order
    {
        public int OrderId { get; set; }
        public string Customer { get; set; }
        public DateTime Date { get; set; }
        public decimal Total { get; set; }
    }

    class Program
    {
        static void Main()
        {
            // Retrieve orders (in real life this could be a DB call)
            var orders = GetOrders();

            // The rest of the tutorial continues here...
        }

        // Mock method – in production pull from EF Core, Dapper, etc.
        private static List<Order> GetOrders()
        {
            return new List<Order>
            {
                new Order { OrderId = 1001, Customer = "Acme Corp", Date = DateTime.Today, Total = 1234.56m },
                new Order { OrderId = 1002, Customer = "Beta Ltd.", Date = DateTime.Today.AddDays(-1), Total = 789.00m },
                new Order { OrderId = 1003, Customer = "Gamma LLC", Date = DateTime.Today.AddDays(-2), Total = 456.78m }
            };
        }
    }
}
```

> **Consejo profesional:** Mantén el modelo ligero para la demostración; siempre puedes enriquecerlo más adelante con líneas de detalle, impuestos, etc.

---

## Paso 2: Preparar la plantilla de Excel

SmartMarker trabaja contra un libro de trabajo plantilla. Crea un archivo llamado `InvoiceTemplate.xlsx` con una sola hoja llamada `InvoiceTemplate`. En la celda **A1** coloca un marcador SmartMarker como:

```
{{OrderId}} – {{Customer}} – {{Date}} – ${{Total}}
```

Puedes dar formato a las celdas como prefieras—encabezados en negrita, formato de moneda, etc. Guarda el archivo en la carpeta raíz del proyecto.

> **¿Por qué una plantilla?** Separa el diseño del código, permitiendo que los diseñadores ajusten la apariencia sin tocar la lógica.

---

## Paso 3: Configurar las opciones de SmartMarker – Repetir y nombrar hojas

Ahora indicaremos a SmartMarker que *repita* la hoja plantilla para cada pedido y que le asigne a cada copia un nombre que incluya el ID del pedido. Este es el núcleo de la **nomenclatura dinámica de hojas**.

```csharp
// Inside Main() after retrieving orders
// Load the template workbook
Workbook wb = new Workbook("InvoiceTemplate.xlsx");

// Set up SmartMarker options
var smartMarkerOptions = new SmartMarkerOptions
{
    // Instructs SmartMarker to create a new worksheet per data item
    RepeatWorksheet = true,

    // Naming pattern – {OrderId} will be replaced with the actual value
    RepeatWorksheetName = "Invoice_{OrderId}"
};

// Run the processor
wb.SmartMarkerProcessor.StartSmartMarkerProcessing(orders, smartMarkerOptions);

// Save the result
string outputPath = "GeneratedInvoices.xlsx";
wb.Save(outputPath);

Console.WriteLine($"✅ Invoices generated: {outputPath}");
```

### Cómo funciona

- **`RepeatWorksheet = true`** indica al motor que duplique la hoja origen para cada elemento de la colección `orders`. Esto satisface el requisito de **cómo repetir una hoja**.
- **`RepeatWorksheetName = "Invoice_{OrderId}"`** es una cadena de plantilla donde `{OrderId}` es un marcador que SmartMarker reemplaza con el ID del pedido actual. Esa es la respuesta a **cómo nombrar hojas** y a la **nomenclatura dinámica de hojas**.
- El procesador combina los campos de cada pedido (`{{OrderId}}`, `{{Customer}}`, etc.) en la hoja duplicada, produciendo una factura completamente rellenada.

---

## Paso 4: Ejecutar la aplicación y verificar la salida

Compila y ejecuta la aplicación de consola:

```bash
dotnet run
```

Deberías ver el mensaje de éxito en la consola. Abre `GeneratedInvoices.xlsx` y encontrarás tres pestañas:

- **Invoice_1001**
- **Invoice_1002**
- **Invoice_1003**

Cada hoja contiene los datos del pedido sustituidos en los marcadores. El diseño que creaste en la plantilla se conserva, demostrando que **automatizar la generación de facturas** funciona de extremo a extremo.

### Captura de pantalla esperada (texto alternativo para SEO)

![automate invoice generation example showing three dynamically named worksheets](/images/invoice-automation.png)

> *El texto alternativo de la imagen incluye la palabra clave principal para cumplir con SEO.*

---

## Paso 5: Casos límite y variaciones comunes

### ¿Qué pasa si un OrderId contiene caracteres no permitidos?

Los nombres de hojas de Excel no pueden contener `\ / ? * [ ] :`. Si tus IDs pueden incluir esos caracteres, debes sanitizarlos:

```csharp
RepeatWorksheetName = "Invoice_{SanitizedOrderId}"
```

Agrega una propiedad calculada a `Order`:

```csharp
public string SanitizedOrderId => OrderId.ToString().Replace("/", "-").Replace("\\", "-");
```

### ¿Necesitas conservar la hoja plantilla original?

Establece `smartMarkerOptions.RemoveTemplate = false;` (el valor predeterminado es `true`). Así la hoja `InvoiceTemplate` original queda intacta como referencia.

### ¿Quieres agrupar facturas por cliente?

Puedes anidar **grupos de repetición**. Primero repite por cliente y luego por pedidos dentro de cada hoja de cliente. La sintaxis se vuelve un poco más compleja, pero el principio sigue siendo el mismo: usa `RepeatWorksheet` y un patrón de nombre que refleje la jerarquía.

---

## Ejemplo completo (todo el código en un solo lugar)

```csharp
using System;
using System.Collections.Generic;
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

namespace InvoiceAutomation
{
    public class Order
    {
        public int OrderId { get; set; }
        public string Customer { get; set; }
        public DateTime Date { get; set; }
        public decimal Total { get; set; }

        // Helper for safe sheet names
        public string SanitizedOrderId => OrderId.ToString();
    }

    class Program
    {
        static void Main()
        {
            var orders = GetOrders();

            // Load template
            Workbook wb = new Workbook("InvoiceTemplate.xlsx");

            // Configure SmartMarker for repeating and naming worksheets
            var smartMarkerOptions = new SmartMarkerOptions
            {
                RepeatWorksheet = true,
                RepeatWorksheetName = "Invoice_{OrderId}" // dynamic worksheet naming
                // RemoveTemplate = true; // default behavior
            };

            // Process the data
            wb.SmartMarkerProcessor.StartSmartMarkerProcessing(orders, smartMarkerOptions);

            // Save the final workbook
            string outputPath = "GeneratedInvoices.xlsx";
            wb.Save(outputPath);

            Console.WriteLine($"✅ Invoices generated: {outputPath}");
        }

        private static List<Order> GetOrders()
        {
            return new List<Order>
            {
                new Order { OrderId = 1001, Customer = "Acme Corp", Date = DateTime.Today, Total = 1234.56m },
                new Order { OrderId = 1002, Customer = "Beta Ltd.", Date = DateTime.Today.AddDays(-1), Total = 789.00m },
                new Order { OrderId = 1003, Customer = "Gamma LLC", Date = DateTime.Today.AddDays(-2), Total = 456.78m }
            };
        }
    }
}
```

Copia‑pega esto en `Program.cs`, coloca `InvoiceTemplate.xlsx` al lado y estarás listo para ejecutar.

---

## Preguntas frecuentes

**P: ¿Este enfoque funciona con conjuntos de datos grandes (miles de facturas)?**  
R: Sí. SmartMarker transmite los datos de forma eficiente, pero vigila el uso de memoria. Si alcanzas límites, considera procesar en lotes y escribir cada lote en un libro de trabajo separado.

**P: ¿Puedo añadir un logotipo a cada factura automáticamente?**  
R: Por supuesto. Coloca la imagen del logotipo en la hoja plantilla. Como la hoja se duplica, el logotipo aparecerá en cada factura generada sin código adicional.

**P: ¿Qué pasa si necesito proteger las hojas?**  
R: Después del procesamiento, recorre `wb.Worksheets` y llama a `ws.Protect(Password, ProtectionType.All)`.

---

## Conclusión

Acabamos de **automatizar la generación de facturas** aprovechando la función de repetición de hojas de SmartMarker y un patrón de nombres ingenioso. El tutorial cubrió **cómo nombrar hojas**, demostró **cómo repetir una hoja** para cada pedido y mostró **nomenclatura dinámica de hojas** que mantiene tu libro ordenado y fácil de buscar.  

Desde la obtención de datos, la configuración de una plantilla, la configuración de `SmartMarkerOptions`, hasta el manejo de casos límite, ahora dispones de una solución completa y ejecutable. Como siguiente paso, prueba añadir tablas de líneas de detalle, aplicar formato condicional o exportar los mismos datos a PDF para crear una cadena de facturación totalmente automatizada.

¿Listo para subir de nivel? Explora temas relacionados como “exportación masiva a Excel con Aspose.Cells”, “conversión a PDF de hojas” o “envío de facturas generadas por correo electrónico directamente desde C#”. El cielo es el límite—¡feliz codificación!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}