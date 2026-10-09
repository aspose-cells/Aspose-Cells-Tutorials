---
category: general
date: 2026-06-21
description: Importa JSON a Excel rápidamente y aprende a convertir JSON a XLSX, generar
  Excel a partir de JSON y exportar JSON a una hoja de cálculo en unos pocos pasos
  sencillos.
draft: false
keywords:
- import json to excel
- convert json to xlsx
- generate excel from json
- save json as excel
- export json to spreadsheet
language: es
og_description: Importa JSON a Excel sin esfuerzo. Esta guía te muestra cómo convertir
  JSON a XLSX, generar Excel a partir de JSON y exportar JSON a una hoja de cálculo
  usando C#.
og_title: Importar JSON a Excel con Aspose.Cells – Guía completa
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Import JSON to Excel quickly and learn how to convert JSON to XLSX,
    generate Excel from JSON, and export JSON to spreadsheet in a few easy steps.
  headline: Import JSON to Excel with Aspose.Cells – Complete Programming Guide
  type: TechArticle
- description: Import JSON to Excel quickly and learn how to convert JSON to XLSX,
    generate Excel from JSON, and export JSON to spreadsheet in a few easy steps.
  name: Import JSON to Excel with Aspose.Cells – Complete Programming Guide
  steps:
  - name: Expected Output
    text: 'Running the program prints:'
  - name: 1. Import Multiple JSON Arrays into Different Sheets
    text: 'If you have several arrays—say `"Employees"` and `"Departments"`—you can
      import each into its own worksheet:'
  - name: 2. Styling the Generated Table
    text: 'You can apply a style after the data expands:'
  - name: 3. Using a JSON File Instead of a String
    text: 'If your JSON lives on disk, just read it first:'
  type: HowTo
tags:
- Aspose.Cells
- C#
- JSON
- Excel automation
title: Importar JSON a Excel con Aspose.Cells – Guía completa de programación
url: /es/net/excel-data-import-export/import-json-to-excel-with-aspose-cells-complete-programming/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Importar JSON a Excel – Guía Completa de Programación

¿Alguna vez te has preguntado **cómo importar JSON a Excel** sin escribir un analizador personalizado? No estás solo. Muchos desarrolladores se encuentran con un obstáculo cuando necesitan convertir una carga JSON en una hoja de cálculo ordenada para informes o tareas de análisis de datos. ¿La buena noticia? Con Aspose.Cells puedes **convertir JSON a XLSX** en solo unas pocas líneas, y todo el proceso es rápido y seguro en cuanto a tipos.

En este tutorial recorreremos cada paso necesario para **generar Excel a partir de JSON**, guardar el resultado como un archivo `.xlsx` e incluso exploraremos algunas variaciones útiles, como exportar JSON a una hoja que se actualiza automáticamente cuando cambias los datos de origen. Al final, tendrás un fragmento reutilizable que podrás insertar en cualquier proyecto .NET.

## Requisitos previos

Antes de profundizar, asegúrate de contar con:

- .NET 6.0 o posterior (el código también funciona en .NET Framework)
- Una licencia válida de Aspose.Cells for .NET o una clave de evaluación temporal
- Visual Studio 2022 (o cualquier IDE de C# que prefieras)
- Familiaridad básica con estructuras JSON y sintaxis C#

No se necesitan paquetes NuGet adicionales más allá de **Aspose.Cells**, lo que mantiene la configuración ligera.

## Paso 1: Instalar Aspose.Cells y Configurar el Proyecto

Lo primero, agrega la biblioteca Aspose.Cells a tu proyecto. Abre la consola del Administrador de paquetes y ejecuta:

```powershell
Install-Package Aspose.Cells
```

Si utilizas la CLI de .NET, el equivalente es:

```bash
dotnet add package Aspose.Cells
```

> **Consejo profesional:** Después de la instalación, agrega tu archivo de licencia (`Aspose.Cells.lic`) a la raíz del proyecto y cárgalo al iniciar:

```csharp
// Load the Aspose.Cells license (optional but removes evaluation watermark)
var license = new Aspose.Cells.License();
license.SetLicense("Aspose.Cells.lic");
```

Ahora estás listo para comenzar a **importar JSON a Excel**.

## Paso 2: Preparar la Carga JSON

Para la demostración, usaremos una matriz simple de objetos persona. En un escenario real podrías leer esta cadena desde un archivo, una respuesta de API o una base de datos.

```csharp
// Step 2: Define the JSON data to be imported
string json = "[{\"Name\":\"John\",\"Age\":30},{\"Name\":\"Anna\",\"Age\":28}]";
```

Observa cómo el JSON es una matriz plana, la forma que mejor funciona con los marcadores inteligentes de Aspose.Cells.

## Paso 3: Configurar las Opciones de Carga de JSON

Aspose.Cells te permite tratar toda la matriz JSON como una *única* fuente de datos. Esto es crucial cuando deseas que las filas se expandan automáticamente dentro de la hoja.

```csharp
// Step 3: Configure JSON loading options to treat the whole array as a single data source
var loadOptions = new Aspose.Cells.JsonLoadOptions
{
    // When true, the whole array becomes one data source (e.g., "People")
    ArrayAsSingle = true
};
```

Establecer `ArrayAsSingle = true` indica a la biblioteca **generar un marcador inteligente que se repita por cada elemento** de la matriz, que es el núcleo del flujo de trabajo **convertir JSON a XLSX**.

## Paso 4: Crear el Workbook e Importar el JSON

Ahora creamos una nueva instancia de `Workbook` e importamos el JSON usando un marcador inteligente llamado `"People"`.

```csharp
// Step 4: Create a new workbook and import the JSON using a smart marker named "People"
var workbook = new Aspose.Cells.Workbook();
workbook.ImportJson(json, loadOptions, new Aspose.Cells.SmartMarkerOptions
{
    DataSourceName = "People"
});
```

Detrás de escena, Aspose.Cells analiza el JSON, asigna cada propiedad (`Name`, `Age`) a una columna y prepara un marcador de posición que luego se expandirá en filas.

## Paso 5: Colocar el Marcador Inteligente en la Hoja

Un marcador inteligente se ve así `{{People}}`. Cuando se guarda el workbook, Aspose.Cells reemplaza este marcador con una tabla que contiene todos los datos de la matriz JSON.

```csharp
// Step 5: Put the smart marker in cell A1 so the data expands when saved
workbook.Worksheets[0].Cells["A1"].PutValue("{{People}}");
```

Puedes mover el marcador a cualquier lugar; la esquina superior izquierda es una opción común porque permite que la tabla crezca hacia abajo y hacia la derecha.

## Paso 6: Guardar el Workbook como Archivo XLSX

Finalmente, escribe el workbook en disco. Aquí es donde **guardamos JSON como Excel** y obtenemos un verdadero archivo `.xlsx` que puedes abrir en Excel, Google Sheets o cualquier otra aplicación de hojas de cálculo.

```csharp
// Step 6: Save the workbook to a file (convert JSON to XLSX)
string outputPath = Path.Combine(Environment.CurrentDirectory, "JsonSingleCell.xlsx");
workbook.Save(outputPath, Aspose.Cells.SaveFormat.Xlsx);
Console.WriteLine($"Workbook saved to {outputPath}");
```

Al abrir `JsonSingleCell.xlsx`, verás algo como:

| Name | Age |
|------|-----|
| John | 30  |
| Anna | 28  |

Ese es el resultado de **generar Excel a partir de JSON** en acción.

## Ejemplo Completo Funcional

Juntando todo, aquí tienes el programa completo, listo para ejecutar:

```csharp
using System;
using System.IO;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Load license (optional)
        // var license = new License();
        // license.SetLicense("Aspose.Cells.lic");

        // Step 1: Define JSON data
        string json = "[{\"Name\":\"John\",\"Age\":30},{\"Name\":\"Anna\",\"Age\":28}]";

        // Step 2: Configure loading options
        var loadOptions = new JsonLoadOptions { ArrayAsSingle = true };

        // Step 3: Create workbook and import JSON
        var workbook = new Workbook();
        workbook.ImportJson(json, loadOptions, new SmartMarkerOptions { DataSourceName = "People" });

        // Step 4: Insert smart marker
        workbook.Worksheets[0].Cells["A1"].PutValue("{{People}}");

        // Step 5: Save as XLSX (export JSON to spreadsheet)
        string outputPath = Path.Combine(Environment.CurrentDirectory, "JsonSingleCell.xlsx");
        workbook.Save(outputPath, SaveFormat.Xlsx);

        Console.WriteLine($"Excel file generated successfully at: {outputPath}");
    }
}
```

### Salida Esperada

Ejecutar el programa imprime:

```
Excel file generated successfully at: C:\YourProject\JsonSingleCell.xlsx
```

Abrir el archivo muestra una tabla de dos filas con los encabezados **Name** y **Age**, coincidiendo exactamente con la matriz JSON original.

## Variaciones Avanzadas

### 1. Importar Múltiples Matrices JSON en Hojas Diferentes

Si tienes varias matrices —por ejemplo `"Employees"` y `"Departments"`— puedes importar cada una a su propia hoja:

```csharp
// Load a more complex JSON with two arrays
string complexJson = @"
{
  ""Employees"": [{""Name"":""John"",""Age"":30}],
  ""Departments"": [{""Dept"":""HR"",""Count"":5}]
}";
var options = new JsonLoadOptions { ArrayAsSingle = false };
var wb = new Workbook();
wb.ImportJson(complexJson, options, new SmartMarkerOptions());

// Place markers
wb.Worksheets[0].Cells["A1"].PutValue("{{Employees}}");
wb.Worksheets.Add();
wb.Worksheets[1].Cells["A1"].PutValue("{{Departments}}");
wb.Save("MultipleSheets.xlsx");
```

Ahora has **exportado JSON a una hoja de cálculo** con varias pestañas, cada una reflejando un conjunto de datos distinto.

### 2. Aplicar Estilo a la Tabla Generada

Puedes aplicar un estilo después de que los datos se expandan:

```csharp
var table = workbook.Worksheets[0].Cells["A1"].GetSmartMarkerTable();
var style = workbook.CreateStyle();
style.Font.IsBold = true;
style.ForegroundColor = System.Drawing.Color.LightBlue;
style.Pattern = BackgroundType.Solid;
table.ApplyStyle(style);
```

Este pequeño ajuste hace que la fila de encabezado destaque, lo cual es útil para paneles de informes.

### 3. Usar un Archivo JSON en Lugar de una Cadena

Si tu JSON está en disco, simplemente léelo primero:

```csharp
string jsonFromFile = File.ReadAllText(@"C:\Data\people.json");
workbook.ImportJson(jsonFromFile, loadOptions, new SmartMarkerOptions { DataSourceName = "People" });
```

El resto de los pasos permanece exactamente igual, por lo que puedes **guardar JSON como Excel** desde cualquier origen.

## Problemas Comunes y Cómo Evitarlos

- **Falta `ArrayAsSingle`** – Olvidar esta bandera hará que cada objeto se trate como una fuente de datos separada, resultando en celdas vacías. Siempre configúrala cuando tu JSON sea una matriz de nivel superior.
- **Nombre de Marcador Inteligente Incorrecto** – El marcador (`{{People}}`) debe coincidir con el `DataSourceName` que pasaste (`"People"`). Un error tipográfico dejará el marcador sin reemplazar.
- **Licencia No Cargada** – En modo de evaluación, el archivo de salida contiene una marca de agua. Carga tu licencia al inicio para mantener el workbook limpio.
- **Permisos de Ruta de Archivo** – Intentar guardar en una carpeta protegida lanza una excepción. Usa `Environment.CurrentDirectory` o una ruta escribible por el usuario.

## Probar el Resultado Programáticamente

Si deseas verificar que la exportación se realizó correctamente sin abrir Excel, puedes leer la primera celda de vuelta:

```csharp
var wbCheck = new Workbook("JsonSingleCell.xlsx");
string firstName = wbCheck.Worksheets[0].Cells["A2"].StringValue; // Should be "John"
Console.WriteLine($"First imported name: {firstName}");
```

Una rápida comprobación en consola como esta confirma que **convertir JSON a XLSX** funcionó como se esperaba.

## Conclusión

Acabamos de cubrir todo lo que necesitas para **importar JSON a Excel** usando Aspose.Cells: desde la instalación de la biblioteca, la preparación del JSON, la configuración de marcadores inteligentes, hasta finalmente **guardar JSON como Excel**. Ya sea que necesites **convertir JSON a XLSX**, **generar Excel a partir de JSON**, o **exportar JSON a hoja de cálculo** para análisis, el patrón sigue siendo el mismo — los marcadores inteligentes hacen el trabajo pesado.

Siéntete libre de experimentar con estilos, múltiples hojas o incluso actualizaciones dinámicas reimportando JSON en tiempo de ejecución. El siguiente paso lógico es integrar este código en una API web que sirva informes Excel bajo demanda — simplemente reemplaza la línea de guardado de archivo por un stream devuelto al cliente.

¿Tienes preguntas sobre casos especiales, como objetos JSON anidados o conjuntos de datos muy grandes? Deja un comentario abajo, ¡y feliz codificación!

## ¿Qué Deberías Aprender a Continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos con explicaciones paso a paso para ayudarte a dominar funciones adicionales de la API y explorar enfoques alternativos de implementación en tus propios proyectos.

- [Efficiently Import JSON to Excel Using Aspose.Cells for Java: A Comprehensive Guide](/cells/english/java/import-export/import-json-to-excel-aspose-cells-java/)
- [Import JSON Data into Excel Using Aspose.Cells Java: A Comprehensive Guide](/cells/english/java/import-export/import-json-data-excel-aspose-cells-java/)
- [Effortlessly Import JSON into Excel using Aspose.Cells for .NET](/cells/english/net/import-export/import-json-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}