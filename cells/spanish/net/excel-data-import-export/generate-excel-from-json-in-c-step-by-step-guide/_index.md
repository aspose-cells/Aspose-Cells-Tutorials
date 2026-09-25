---
category: general
date: 2026-03-18
description: Aprende a generar Excel a partir de JSON con C#, permite nombres de hoja
  duplicados, crea una hoja de detalle y guarda el libro de trabajo en C# en minutos.
draft: false
keywords:
- generate excel from json
- allow duplicate sheet names
- how to create detail sheet
- save workbook c#
- smartmarker options
- aspnet cells integration
language: es
og_description: Genera Excel a partir de JSON usando C#. Esta guía muestra cómo permitir
  nombres de hoja duplicados, crear una hoja de detalle y guardar el libro de trabajo
  en C# con Aspose.Cells.
og_title: Generar Excel a partir de JSON en C# – Tutorial completo
tags:
- C#
- Excel automation
- JSON
- Aspose.Cells
title: Generar Excel a partir de JSON en C# – Guía paso a paso
url: /es/net/excel-data-import-export/generate-excel-from-json-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Generar Excel a partir de JSON en C# – Guía paso a paso

¿Alguna vez necesitaste **generar Excel a partir de JSON** pero no estabas seguro de qué biblioteca podía encargarse del trabajo pesado? No eres el único. En muchas aplicaciones empresariales recibimos cargas útiles como JSON y debemos volcar esos datos en hojas de cálculo bien formateadas —piensa en informes de ventas, volcados de inventario o registros de auditoría. ¿La buena noticia? Con el motor SmartMarker de Aspose.Cells puedes convertir una cadena JSON en un archivo Excel completamente funcional con solo unas pocas líneas.

En este tutorial recorreremos todo el proceso: desde preparar la carga JSON, configurar SmartMarker para **permitir nombres de hoja duplicados**, crear una **hoja de detalle**, y finalmente **guardar el libro de trabajo en C#**. Al final tendrás un fragmento reutilizable que puedes insertar en cualquier proyecto .NET.

> **Resumen rápido:**  
> • Objetivo principal – generar Excel a partir de JSON.  
> • Objetivos secundarios – permitir nombres de hoja duplicados, crear hoja de detalle, guardar libro de trabajo en C#.  

## Requisitos previos

Antes de sumergirnos, asegúrate de tener:

- .NET 6.0 SDK (o cualquier versión reciente de .NET).  
- Visual Studio 2022 o VS Code con la extensión C#.  
- Una licencia activa o una prueba gratuita de **Aspose.Cells for .NET** (el paquete NuGet es `Aspose.Cells`).  
- Un archivo de plantilla Excel (`template.xlsx`) que ya contiene etiquetas SmartMarker como `&=Name` y un marcador de posición de tabla de detalle.

Si alguno de esos conceptos te resulta desconocido, no te alarmes—instalar el paquete NuGet es un solo comando, y la plantilla puede ser un libro de trabajo simple con algunas celdas de marcador.

## Visión general de la solución

A alto nivel, haremos:

1. Definir una cadena JSON que refleje los datos que queremos en la hoja.  
2. Configurar `SmartMarkerOptions` para que se permitan nombres de hoja duplicados y que una **hoja de detalle** obtenga un nombre predecible.  
3. Cargar la plantilla Excel que contiene las etiquetas SmartMarker.  
4. Ejecutar el procesador SmartMarker para combinar los datos JSON en el libro de trabajo.  
5. Guardar el archivo final con `workbook.Save(...)`.

Cada paso se explica a continuación, con fragmentos de código completos y por qué el paso es importante.

---

## Paso 1 – Preparar la carga JSON que fusionarás

Lo primero que necesitas es un documento JSON que coincida con las etiquetas SmartMarker dentro de tu plantilla. Piensa en el JSON como la fuente de la verdad; cada clave se convierte en un marcador de posición en el archivo Excel.

```csharp
// Step 1: Define the JSON data that will be merged into the worksheet
string jsonData = @"{
    ""Name"": ""John"",
    ""Date"": ""2023-01-01"",
    ""Orders"": [
        { ""Item"": ""Laptop"", ""Qty"": 2, ""Price"": 1200 },
        { ""Item"": ""Mouse"",  ""Qty"": 5, ""Price"": 25 }
    ]
}";
```

**Por qué es importante:**  
SmartMarker lee la jerarquía JSON y expande automáticamente las tablas para colecciones como `Orders`. Si la estructura de tu JSON no coincide con las etiquetas, la fusión producirá silenciosamente filas vacías—un error común.

---

## Paso 2 – Configurar SmartMarker para permitir nombres de hoja duplicados y nombrar la hoja de detalle

Por defecto, Aspose.Cells prohíbe nombres de hoja duplicados, lo que puede ser un obstáculo cuando generas una hoja de detalle para cada registro maestro. La clase `SmartMarkerOptions` te permite relajar esa regla y también especificar un patrón de nomenclatura para las hojas de detalle recién creadas.

```csharp
// Step 2: Create SmartMarker options and allow duplicate base names for detail sheets
var smartMarkerOptions = new Aspose.Cells.SmartMarker.SmartMarkerOptions
{
    // When a detail sheet is generated, it will be named "Detail", "Detail (2)", etc.
    DetailSheetNewName = "Detail",

    // This flag tells the engine that duplicate sheet names are acceptable.
    // Useful when you generate multiple detail sheets from a loop.
    AllowDuplicateSheetNames = true
};
```

**Por qué es importante:**  
Si estás iterando sobre varios clientes y cada iteración crea una nueva hoja, el motor normalmente lanzaría una excepción. Configurar `AllowDuplicateSheetNames` a `true` indica a Aspose.Cells que añada automáticamente un sufijo numérico, manteniendo el proceso fluido.

---

## Paso 3 – Cargar la plantilla Excel que contiene etiquetas SmartMarker

Tu plantilla es el lienzo donde SmartMarker pintará los datos. Puede contener cualquier formato—colores, fórmulas, gráficos—para que no tengas que recrear esa lógica programáticamente.

```csharp
// Step 3: Load the workbook that contains SmartMarker tags
using var workbook = new Aspose.Cells.Workbook(@"C:\MyProjects\ExcelDemo\template.xlsx");
```

**Consejo:**  
Mantén la plantilla en una carpeta que forme parte de la salida de tu proyecto (p.ej., `Content\Templates`). De esa forma puedes referenciarla con una ruta relativa y evitar codificar rutas absolutas.

---

## Paso 4 – Ejecutar el procesador SmartMarker con el JSON y las opciones

Ahora ocurre la magia. El `SmartMarkerProcessor` lee el JSON, respeta las opciones que configuraste y rellena el libro de trabajo en consecuencia.

```csharp
// Step 4: Process the SmartMarker tags using the JSON data and the configured options
workbook.SmartMarkerProcessor.Process(jsonData, smartMarkerOptions);
```

**¿Qué ocurre bajo el capó?**  
- El procesador escanea cada celda en busca de marcadores como `&=Name` o `&=Orders.Item`.  
- Reemplaza los marcadores simples con valores escalares (`Name`, `Date`).  
- Para colecciones (`Orders`), crea una nueva hoja de detalle (llamada “Detail”) y rellena una fila de tabla por cada elemento.  
- Como permitimos nombres de hoja duplicados, si la plantilla ya tenía una hoja llamada “Detail”, el motor creará “Detail (2)”.

---

## Paso 5 – Guardar el libro de trabajo fusionado en disco

Finalmente, escribe el libro de trabajo poblado en un archivo. Puedes elegir cualquier formato compatible con Aspose.Cells—XLSX, CSV, PDF, etc. Aquí nos quedaremos con el moderno XLSX.

```csharp
// Step 5: Save the workbook with the merged data
workbook.Save(@"C:\MyProjects\ExcelDemo\output.xlsx");
```

**Por qué es importante:**  
Guardar es donde realmente **guardas el libro de trabajo en C#**. Si necesitas transmitir el archivo de vuelta a un cliente web, puedes usar `workbook.Save(Stream, SaveFormat.Xlsx)` en su lugar.

---

## Ejemplo completo funcional

Juntando todo, aquí tienes una aplicación de consola completa y lista para ejecutar. Asegúrate de haber instalado el paquete NuGet `Aspose.Cells` (`dotnet add package Aspose.Cells`) antes de compilar.

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.SmartMarker;

namespace ExcelFromJsonDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Define the JSON payload
            string jsonData = @"{
                ""Name"": ""John"",
                ""Date"": ""2023-01-01"",
                ""Orders"": [
                    { ""Item"": ""Laptop"", ""Qty"": 2, ""Price"": 1200 },
                    { ""Item"": ""Mouse"",  ""Qty"": 5, ""Price"": 25 }
                ]
            }";

            // 2️⃣ Configure SmartMarker options – allow duplicate sheet names & set detail sheet name
            var smartMarkerOptions = new SmartMarkerOptions
            {
                DetailSheetNewName = "Detail",
                AllowDuplicateSheetNames = true
            };

            // 3️⃣ Load the template workbook (ensure the path is correct)
            var workbookPath = @"C:\MyProjects\ExcelDemo\template.xlsx";
            using var workbook = new Workbook(workbookPath);

            // 4️⃣ Merge JSON data into the workbook
            workbook.SmartMarkerProcessor.Process(jsonData, smartMarkerOptions);

            // 5️⃣ Save the result
            var outputPath = @"C:\MyProjects\ExcelDemo\output.xlsx";
            workbook.Save(outputPath);

            Console.WriteLine($"✅ Excel file generated successfully at: {outputPath}");
        }
    }
}
```

### Resultado esperado

- **Hoja 1** (la hoja maestra) mostrará “John” en la celda `Name` y “2023‑01‑01` en la celda `Date`.  
- Una nueva hoja **Detail** aparecerá, conteniendo una tabla con dos filas: una para el pedido de Laptop y otra para el pedido de Mouse.  
- Si la plantilla ya tenía una hoja llamada “Detail”, la nueva hoja se nombrará “Detail (2)”, gracias al indicador `AllowDuplicateSheetNames`.

![Salida de Excel mostrando la hoja maestra con nombre y fecha, más una hoja Detail con filas de pedidos](excel-output.png "generate excel from json result")

*Texto alternativo de la imagen:* **generar excel a partir de json – libro de ejemplo con hojas maestra y detalle**

---

## Preguntas comunes y casos límite

### ¿Qué pasa si mi JSON contiene colecciones anidadas?

SmartMarker puede manejar matrices anidadas, pero deberás añadir hojas de detalle adicionales o usar marcadores jerárquicos. Por ejemplo, `&=Orders.SubItems.Product` generaría automáticamente una hoja de tercer nivel.

### ¿Cómo personalizo el patrón de nombres para hojas duplicadas?

En lugar de un `DetailSheetNewName` estático, puedes asignar una función de devolución de llamada mediante `smartMarkerOptions.DetailSheetNameGenerator`. Esto te permite incrustar marcas de tiempo o IDs únicos en el nombre de la hoja.

```csharp
smartMarkerOptions.DetailSheetNameGenerator = (baseName, index) =>
    $"{baseName}_{DateTime.Now:yyyyMMdd}_{index}";
```

### ¿Puedo generar CSV en lugar de XLSX?

Absolutamente. Reemplaza la llamada final a `Save` con:

```csharp
workbook.Save(outputPath, SaveFormat.Csv);
```

El resto del flujo permanece idéntico.

### ¿Esto funciona en ASP.NET Core?

Sí. El mismo código puede ejecutarse dentro de una acción de controlador. Simplemente transmite el libro de trabajo a la respuesta:

```csharp
using var ms = new MemoryStream();
workbook.Save(ms, SaveFormat.Xlsx);
ms.Position = 0;
return File(ms, "application/vnd.openxmlformats-officedocument.spreadsheetml.sheet", "report.xlsx");
```

---

## Consejos profesionales y trampas

- **Consejo pro:** Mantén tus etiquetas SmartMarker en una hoja “Template” separada. Así puedes proteger la hoja de ediciones accidentales mientras permites que el procesador la lea.  
- **Cuidado con:** claves JSON que contengan espacios o caracteres especiales. Aspose.Cells espera identificadores JavaScript válidos; renómbralas o usa el atributo `JsonProperty` si estás deserializando desde un POCO.  
- **Consejo de rendimiento:** Si procesas miles de filas, configura `smartMarkerOptions.EnableCache = true` para reutilizar marcadores compilados.  
- **Verificación de versión:** El código anterior está dirigido a Aspose.Cells 23.9+. Versiones anteriores pueden no soportar `AllowDuplicateSheetNames`.

---

## Conclusión

Ahora tienes una receta completa, de extremo a extremo, para **generar Excel a partir de JSON** en C#. Configurando `SmartMarkerOptions` demostramos cómo **permitir nombres de hoja duplicados**, controlar la nomenclatura de la **hoja de detalle**, y finalmente **guardar el libro de trabajo en C#**. El enfoque es totalmente autónomo—sin servicios externos, solo un único paquete NuGet.

¿Próximos pasos? Intenta sustituir la fuente JSON por una API real

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}