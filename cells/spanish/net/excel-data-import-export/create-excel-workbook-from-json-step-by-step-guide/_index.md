---
category: general
date: 2026-03-25
description: Crear un libro de Excel a partir de JSON y guardarlo como xlsx. Aprende
  cómo exportar JSON a xlsx, generar Excel desde JSON y rellenar Excel con JSON en
  minutos.
draft: false
keywords:
- create excel workbook
- export json to xlsx
- generate excel from json
- populate excel from json
- save workbook as xlsx
language: es
og_description: Crea un libro de Excel a partir de JSON al instante. Esta guía muestra
  cómo exportar JSON a XLSX, generar Excel desde JSON y rellenar Excel con JSON usando
  Aspose.Cells.
og_title: Crear libro de Excel a partir de JSON – Tutorial completo de C#
tags:
- Aspose.Cells
- C#
- JSON
- Excel automation
title: Crear libro de Excel a partir de JSON – Guía paso a paso
url: /es/net/excel-data-import-export/create-excel-workbook-from-json-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crear libro de Excel a partir de JSON – Tutorial completo de C#

¿Alguna vez necesitaste **crear libro de Excel** a partir de una carga JSON pero no sabías por dónde empezar? No estás solo; muchos desarrolladores se topan con ese obstáculo cuando intentan convertir datos de una API en una hoja de cálculo ordenada. ¿La buena noticia? Con unas pocas líneas de C# y Aspose.Cells puedes **exportar json a xlsx**, **generar Excel a partir de json**, y **poblar Excel a partir de json** sin lidiar con convertidores de terceros.

En esta guía recorreremos todo el proceso—comenzando con una cadena JSON cruda, insertándola en un SmartMarker, y finalmente **guardar libro como xlsx** en disco. Al final tendrás un archivo Excel listo para usar que se ve así:

| Name | Score |
|------|-------|
| John | 90    |
| Anna | 85    |

> **Consejo profesional:** Si ya estás usando Aspose.Cells en otra parte de tu proyecto, puedes reutilizar la misma instancia `Workbook` para múltiples importaciones de JSON—ideal para procesamiento por lotes.

---

## Lo que necesitarás

- **.NET 6+** (o cualquier .NET Framework reciente que soporte C# 10)
- **Aspose.Cells for .NET** – instalar vía NuGet: `dotnet add package Aspose.Cells`
- Un conocimiento básico de la sintaxis de C# (no se requiere conocimiento profundo de Excel)

Eso es todo. Sin servicios externos, sin interop COM, solo código administrado puro.

---

## Paso 1: Inicializar un nuevo libro de Excel

Lo primero que hacemos es crear un nuevo objeto workbook. Piensa en ello como abrir un archivo Excel en blanco donde más tarde insertaremos nuestros datos.

```csharp
using Aspose.Cells;

// Step 1: Create a new workbook and grab the first worksheet
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.Worksheets[0];
```

¿Por qué comenzar con un nuevo workbook? Garantiza una hoja limpia, evita estilos residuales de ejecuciones anteriores y mantiene el tamaño del archivo al mínimo—perfecto para canalizaciones automatizadas.

---

## Paso 2: Preparar los datos JSON que deseas importar

Para la demostración usaremos una pequeña matriz JSON, pero puedes sustituirla por cualquier JSON válido que recibas de un servicio web, un archivo o una consulta a base de datos.

```csharp
// Step 2: JSON string representing a simple collection of records
string jsonData = "[{\"Name\":\"John\",\"Score\":90},{\"Name\":\"Anna\",\"Score\":85}]";
```

Observa las comillas doblemente escapadas (`\"`)—eso es solo la sintaxis de literal de cadena en C#. En un escenario real probablemente leerías esto desde un archivo:

```csharp
// string jsonData = File.ReadAllText("data.json");
```

---

## Paso 3: Indicar a SmartMarker que trate toda la matriz como un solo registro

El motor SmartMarker de Aspose.Cells puede iterar sobre colecciones automáticamente. Al habilitar **ArrayAsSingle**, tratamos toda la matriz JSON como un solo registro, que es exactamente lo que necesitamos para una tabla plana.

```csharp
// Step 3: Configure SmartMarker options – array‑as‑single mode
SmartMarkerOptions options = new SmartMarkerOptions
{
    ArrayAsSingle = true   // This makes the whole JSON array behave like one record
};
```

Si olvidas esta bandera, SmartMarker intentará crear una hoja separada para cada elemento—definitivamente no es lo que deseas al generar una tabla simple.

---

## Paso 4: Colocar un token SmartMarker en la hoja de cálculo

Los tokens SmartMarker se ven como `${jsonArray}`. Cuando el procesador se ejecuta, reemplaza el token con los datos de la fuente JSON. Colocaremos el token en la celda **A1** para que la salida comience en la esquina superior izquierda.

```csharp
// Step 4: Insert the SmartMarker token into cell A1
worksheet.Cells["A1"].PutValue("${jsonArray}");
```

También puedes pre‑formatear la fila de encabezado antes del procesamiento. Por ejemplo, establecer fuente en negrita en la primera fila:

```csharp
Cell headerCell = worksheet.Cells["A1"];
headerCell.Style.Font.IsBold = true;
```

---

## Paso 5: Ejecutar el procesador SmartMarker

Ahora ocurre la magia. El procesador lee el JSON, asigna cada propiedad a una columna y escribe las filas debajo del token.

```csharp
// Step 5: Process the SmartMarker with our JSON data and options
worksheet.SmartMarkerProcessor.Process(jsonData, options);
```

Detrás de escena, Aspose.Cells:

1. Analiza el JSON a un objeto .NET.
2. Coincide los nombres de propiedades (`Name`, `Score`) con los encabezados de columna.
3. Escribe cada elemento de la matriz como una nueva fila.

Si tu JSON contiene objetos anidados, puedes referenciarlos con notación de punto (`${parent.child}`) – una característica útil para informes más complejos.

---

## Paso 6: Guardar el libro como archivo XLSX

Finalmente, persiste el workbook en disco. La extensión de archivo `.xlsx` indica a Excel (y a la mayoría de las aplicaciones de hojas de cálculo) que se trata de un libro OpenXML.

```csharp
// Step 6: Save the workbook to a file
string outputPath = Path.Combine(Environment.CurrentDirectory, "json-single.xlsx");
workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to {outputPath}");
```

Por supuesto, puedes transmitir el workbook directamente a una respuesta HTTP si estás construyendo una API web:

```csharp
// Example for ASP.NET Core
using (var stream = new MemoryStream())
{
    workbook.Save(stream, SaveFormat.Xlsx);
    stream.Position = 0;
    return File(stream, "application/vnd.openxmlformats-officedocument.spreadsheetml.sheet", "data.xlsx");
}
```

---

## Ejemplo completo en funcionamiento

A continuación se muestra el programa completo, listo para ejecutar, que incorpora cada paso anterior. Copia‑pega en un nuevo proyecto de consola y pulsa **F5**.

```csharp
using System;
using System.IO;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // 2️⃣ JSON data to be merged into the sheet
        string jsonData = "[{\"Name\":\"John\",\"Score\":90},{\"Name\":\"Anna\",\"Score\":85}]";

        // 3️⃣ Enable array‑as‑single mode so the whole array is one record
        SmartMarkerOptions options = new SmartMarkerOptions
        {
            ArrayAsSingle = true
        };

        // 4️⃣ Put a SmartMarker token in A1 that points to the JSON array
        worksheet.Cells["A1"].PutValue("${jsonArray}");

        // Optional: make the header bold for better readability
        worksheet.Cells["A1"].Style.Font.IsBold = true;

        // 5️⃣ Process the SmartMarker with the JSON payload
        worksheet.SmartMarkerProcessor.Process(jsonData, options);

        // 6️⃣ Save the result as an XLSX file
        string outputPath = Path.Combine(Environment.CurrentDirectory, "json-single.xlsx");
        workbook.Save(outputPath);

        Console.WriteLine($"✅ Workbook created and saved to: {outputPath}");
    }
}
```

**Resultado esperado:** Al abrir `json-single.xlsx` se muestran dos filas bajo el encabezado en negrita—`John` con una puntuación de `90` y `Anna` con `85`. Los nombres de columna se infieren automáticamente a partir de los nombres de propiedades del JSON.

---

## Preguntas frecuentes y casos límite

### ¿Qué pasa si mis claves JSON contienen espacios o caracteres especiales?

SmartMarker espera nombres de identificador válidos. Reemplaza los espacios con guiones bajos o usa un mapeo personalizado:

```csharp
// Example JSON: {"First Name":"John"}
string jsonData = "[{\"First_Name\":\"John\",\"Score\":90}]";
// Token stays the same – Aspose.Cells will map "First_Name" to column header "First_Name"
```

### ¿Cómo exportar una gran matriz JSON (miles de filas)?

El procesador transmite datos internamente, por lo que el uso de memoria se mantiene moderado. Sin embargo, podrías querer:

- Incrementar el límite `MaxRows` de la hoja (`worksheet.Cells.MaxRow = 1_048_576;` – el máximo de Excel).
- Desactivar las líneas de cuadrícula para mejorar el rendimiento (`worksheet.IsGridlinesVisible = false;`).

### ¿Puedo añadir varias tablas JSON al mismo libro?

Claro. Simplemente coloca diferentes tokens SmartMarker en rangos separados (p.ej., `${orders}` en `A10`, `${customers}` en `D1`) y llama a `Process` una vez por token o una vez con un objeto JSON compuesto que contenga ambas matrices.

---

## Bonus: Añadir un gráfico simple (Opcional)

Si deseas visualizar las puntuaciones, añade un gráfico de columnas rápido después de que los datos se hayan poblado:

```csharp
// Insert a column chart starting at cell E1
int chartIndex = worksheet.Charts.Add(ChartType.Column, 0, 4, 15, 10);
Chart chart = worksheet.Charts[chartIndex];
chart.NSeries.Add("B2:B3", true);
chart.NSeries[0].Name = "Score";
chart.Title.Text = "Scores by Name";
```

---

## Conclusión

Ahora sabes **how to create excel workbook** a partir de una cadena JSON, **export json to xlsx**, **generate excel from json**, y **populate excel from json** usando la función SmartMarker de Aspose.Cells. La solución completa—inicializar un workbook, configurar SmartMarker, procesar JSON y guardar el archivo—cabe en unas pocas líneas, pero escala a conjuntos de datos masivos.

¿Próximos pasos? Prueba a sustituir el JSON estático por una llamada a una API, añade formato condicional basado en las puntuaciones, o genera múltiples hojas para diferentes dominios de datos. El mismo patrón funciona para CSV, XML o incluso conjuntos de resultados de bases de datos—solo cambia la cadena de origen y ajusta el token SmartMarker.

¡Feliz codificación, y que tus hojas de cálculo siempre estén ordenadas!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}