---
category: general
date: 2026-05-23
description: Crea una tabla dinámica de Excel usando una plantilla y datos JSON. Aprende
  a cargar la plantilla de Excel, automatizar el informe de Excel y rellenar Excel
  a partir de JSON rápidamente.
draft: false
keywords:
- create dynamic excel table
- load excel template
- automate excel report
- populate excel from json
- generate excel report json
language: es
og_description: Crea una tabla de Excel dinámica en minutos con una plantilla y JSON.
  Este tutorial muestra cómo cargar una plantilla de Excel, automatizar un informe
  de Excel y poblar Excel a partir de JSON.
og_title: Crear tabla dinámica de Excel – Guía de Smart Marker
schemas:
- author: Aspose
  dateModified: '2026-05-23'
  description: Create dynamic excel table using a template and JSON data. Learn how
    to load excel template, automate excel report, and populate excel from json quickly.
  headline: Create Dynamic Excel Table – Smart Marker Guide
  type: TechArticle
tags:
- Excel
- Smart Markers
- JSON
- .NET
title: Crear tabla dinámica de Excel – Guía de marcador inteligente
url: /es/net/smart-markers-dynamic-data/create-dynamic-excel-table-smart-marker-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crear tabla dinámica de Excel – Guía de Smart Marker

¿Alguna vez necesitaste **crear tabla dinámica de Excel** que se expanda automáticamente para cada registro en tu conjunto de datos? No eres el único. Ya sea que estés construyendo un panel de ventas mensual o un paquete de facturas por cliente, la capacidad de **poblar Excel desde JSON** sin escribir bucles interminables puede ahorrar horas.

En este tutorial recorreremos una solución completa y práctica que te muestra cómo **cargar plantilla de Excel**, incrustar un Smart Marker, alimentarlo con JSON y, finalmente, **automatizar la generación de informes de Excel**. Al final tendrás un proyecto .NET listo para ejecutar que produce un libro de Excel pulido a partir de una única carga JSON.

---

## Lo que necesitarás

- **Aspose.Cells for .NET** (o cualquier biblioteca que soporte Smart Markers). El ejemplo usa la versión 24.5, pero cualquier versión reciente funciona.
- Visual Studio 2022 (o tu IDE de C# favorito).
- Un archivo de plantilla de Excel simple (`template.xlsx`) ubicado en una carpeta que controles.
- Una cadena JSON que contiene una colección llamada `Customers`.

Eso es todo—sin servicios adicionales, sin conexiones a bases de datos, solo código puro.

---

## Paso 1: Crear un libro de trabajo de plantilla – Cargar plantilla de Excel

Lo primero que hacemos es **cargar la plantilla de Excel** en memoria. Piensa en la plantilla como un lienzo donde un marcador de posición especial indica al procesador dónde repetir filas.

```csharp
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

// Load the template workbook (make sure the path is correct)
Workbook workbook = new Workbook(@"C:\Reports\template.xlsx");

// Grab the first worksheet – this is where our Smart Marker lives
Worksheet worksheet = workbook.Worksheets[0];
```

> **Por qué es importante:** Cargar la plantilla una sola vez mantiene el I/O de archivos al mínimo y te permite reutilizar el mismo diseño para muchos informes. También aísla la lógica del Smart Marker del resto de tu código, lo que constituye una separación limpia de responsabilidades.

---

## Paso 2: Insertar un Smart Marker – Crear tabla dinámica de Excel

Ahora incrustamos un **Smart Marker** que repetirá una tabla por cada entrada en la colección `Customers`. La sintaxis `${Customers.RepeatWorksheet}` indica a Aspose.Cells que clone la hoja completa para cada cliente.

```csharp
// Place the Smart Marker in cell A1 (top‑left corner)
worksheet.Cells[0, 0].PutValue("${Customers.RepeatWorksheet}");
```

> **Consejo profesional:** Si solo necesitas repetir filas en lugar de hojas completas, usa `${Customers.Repeat}` en la primera fila de la tabla. La repetición a nivel de hoja es útil cuando cada cliente obtiene su propia pestaña.

---

## Paso 3: Preparar el SmartMarkerProcessor – Automatizar informe de Excel

Con el marcador en su lugar, creamos un `SmartMarkerProcessor`. Este objeto orquesta el enlace de datos entre JSON y la plantilla de Excel.

```csharp
// Initialize the processor with the workbook that contains the marker
SmartMarkerProcessor processor = new SmartMarkerProcessor(workbook);
```

El procesador es liviano; puedes reutilizarlo para múltiples cargas JSON si lo deseas.

---

## Paso 4: Alimentar datos JSON – Poblar Excel desde JSON

Aquí es donde ocurre la magia. Alimentamos una cadena JSON que contiene un arreglo de clientes. Cada cliente puede tener campos como `Name`, `Email` y `Total`.

```csharp
// Sample JSON data – in a real scenario you might read this from a file or API
string customersJson = @"
{
  ""Customers"": [
    { ""Name"": ""Acme Corp"", ""Email"": ""contact@acme.com"", ""Total"": 12500 },
    { ""Name"": ""Globex"", ""Email"": ""sales@globex.com"", ""Total"": 9800 },
    { ""Name"": ""Initech"", ""Email"": ""info@initech.com"", ""Total"": 15400 }
  ]
}";

// Apply the JSON to the processor – this populates the workbook
processor.ApplyJson(customersJson);
```

> **¿Por qué JSON?** JSON es independiente del lenguaje y fácil de generar a partir de APIs, bases de datos o incluso entradas manuales. Usar `ApplyJson` significa que no tienes que mapear objetos manualmente; el procesador hace el trabajo pesado.

---

## Paso 5: Guardar el resultado – Generar informe de Excel JSON

Finalmente, escribimos el libro de trabajo poblado en disco. El archivo de salida ahora contiene una hoja separada para cada cliente, cada una llena con los datos de nuestro JSON.

```csharp
// Save the filled workbook – choose a path that makes sense for your app
workbook.Save(@"C:\Reports\output.xlsx");
```

### Resultado esperado

- **output.xlsx** tendrá tres hojas de cálculo nombradas `Sheet1`, `Sheet2`, `Sheet3` (o cualquier convención de nombres que use tu plantilla).
- Cada hoja mostrará los valores `Name`, `Email` y `Total` para un solo cliente.
- El diseño que creaste en `template.xlsx` (encabezados, estilo, fórmulas) se conserva en todas las hojas generadas.

---

## Ejemplo completo funcionando

A continuación se muestra el programa completo, listo para ejecutar. Copia‑pégalo en una aplicación de consola, ajusta las rutas de archivo y pulsa **F5**.

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

namespace DynamicExcelDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load the template workbook
            string templatePath = @"C:\Reports\template.xlsx";
            Workbook workbook = new Workbook(templatePath);
            Worksheet worksheet = workbook.Worksheets[0];

            // 2️⃣ Insert the Smart Marker that repeats the worksheet per customer
            worksheet.Cells[0, 0].PutValue("${Customers.RepeatWorksheet}");

            // 3️⃣ Create the SmartMarkerProcessor
            SmartMarkerProcessor processor = new SmartMarkerProcessor(workbook);

            // 4️⃣ JSON data containing a collection of customers
            string customersJson = @"
            {
                ""Customers"": [
                    { ""Name"": ""Acme Corp"", ""Email"": ""contact@acme.com"", ""Total"": 12500 },
                    { ""Name"": ""Globex"", ""Email"": ""sales@globex.com"", ""Total"": 9800 },
                    { ""Name"": ""Initech"", ""Email"": ""info@initech.com"", ""Total"": 15400 }
                ]
            }";

            // Apply the JSON – this populates the workbook dynamically
            processor.ApplyJson(customersJson);

            // 5️⃣ Save the generated report
            string outputPath = @"C:\Reports\output.xlsx";
            workbook.Save(outputPath);

            Console.WriteLine($"✅ Dynamic Excel report generated at: {outputPath}");
        }
    }
}
```

Ejecuta el programa, abre `output.xlsx` y verás una **creación de tabla dinámica de Excel** en acción—cada cliente obtiene su propia hoja, totalmente formateada como la diseñaste.

---

## Preguntas frecuentes y casos límite

| Pregunta | Respuesta |
|----------|-----------|
| *¿Qué pasa si mi JSON tiene objetos anidados?* | Los Smart Markers admiten notación con puntos (`${Customers.Address.City}`) siempre que la jerarquía JSON coincida. |
| *¿Puedo nombrar las hojas generadas con el nombre del cliente?* | Sí—agrega un marcador como `${Customers.Name}` en la celda del nombre de la hoja o usa `processor.ApplyJson(customersJson, "Customers")` con un patrón de nombres. |
| *¿Qué pasa con conjuntos de datos grandes (más de 10 k filas)?* | El procesador transmite datos de manera eficiente, pero vigila la memoria. Considera dividir el informe en varios archivos si alcanzas límites de rendimiento. |
| *¿Necesito una licencia para Aspose.Cells?* | Una evaluación gratuita funciona para pruebas, pero una versión con licencia elimina las marcas de agua de evaluación y brinda todas las funciones. |
| *¿Puedo usar este enfoque con .NET Core?* | Absolutamente—Aspose.Cells soporta .NET 6/7/8. Solo referencia el paquete NuGet y el código permanece igual. |

---

## Consejos para implementaciones listas para producción

- **Validar JSON** antes de alimentarlo a `ApplyJson`. Una carga malformada lanzará una `JsonParseException`.
- **Cachear la plantilla** si generas muchos informes en poco tiempo; cargar desde disco repetidamente es I/O innecesario.
- **Bloquear el libro** durante el procesamiento si lo ejecutas en un servicio web multihilo para evitar condiciones de carrera.
- **Agregar manejo de errores** alrededor de `workbook.Save` para manejar de forma elegante problemas de permisos o archivos bloqueados.
- **Personalizar el estilo** en la plantilla (formato condicional, fórmulas) para que las hojas generadas mantengan la lógica de negocio sin código adicional.

---

## Conclusión

Ahora tienes un patrón sólido de extremo a extremo para **crear tabla dinámica de Excel** usando una plantilla, Smart Markers y datos JSON. Al **cargar la plantilla de Excel**, insertar un marcador de repetición y **poblar Excel desde JSON**, puedes **automatizar la generación de informes de Excel** con solo unas pocas líneas de C#.

¿Próximos pasos? Intenta agregar gráficos que referencien las tablas dinámicas, o exporta el mismo JSON a PDF usando Aspose.Words. También podrías experimentar con **generar informe de Excel JSON** a partir de una consulta a base de datos para cerrar el ciclo.

## Tutoriales relacionados

- [Crear una tabla dinámica en Excel usando Aspose.Cells para .NET](/cells/english/net/pivot-tables/create-pivot-table/)
- [Crear gráficos de líneas dinámicos en Excel usando Aspose.Cells para .NET: Guía paso a paso](/cells/english/net/charts-graphs/create-line-charts-excel-aspose-cells-dotnet/)
- [Cómo crear casillas de verificación en Excel usando Aspose.Cells para .NET | Tutorial de validación de datos](/cells/english/net/data-validation/create-checkboxes-net-excel-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}