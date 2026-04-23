---
category: general
date: 2026-02-09
description: Cómo crear un libro de trabajo en C# con un fondo azul claro e importar
  datos con encabezados. Aprende a añadir un fondo azul claro, usar el estilo predeterminado
  de Excel e importar una tabla de datos.
draft: false
keywords:
- how to create workbook
- add light blue background
- import data with headers
- excel import datatable c#
- use default style excel
language: es
og_description: Cómo crear un libro de trabajo en C# con un fondo azul claro, importar
  datos con encabezados y aplicar el estilo predeterminado de Excel, todo en una guía
  concisa.
og_title: Cómo crear un libro de trabajo – Fondo azul claro, importación de datos
tags:
- C#
- Excel
- Aspose.Cells
title: Cómo crear un libro de trabajo – Fondo azul claro, importación de datos
url: /es/net/excel-data-import-export/how-to-create-workbook-light-blue-background-data-import/
---

content.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo crear Workbook – Fondo azul claro, importación de datos

¿Alguna vez te has preguntado **cómo crear workbook** en C# que se vea un poco más atractivo directamente al abrirlo? Tal vez hayas extraído una `DataTable` de una base de datos y estés cansado de las celdas blancas y sin estilo por defecto. En este tutorial recorreremos la creación de un nuevo workbook, la adición de un fondo azul claro a una columna y la importación de datos con encabezados, todo ello usando el estilo predeterminado que Excel proporciona.

También incluiremos algunos escenarios “qué‑pasaría si”, como el manejo de valores nulos o la personalización de más de una columna. Al final, tendrás un archivo Excel totalmente estilizado que podrás entregar a los interesados sin necesidad de procesamiento adicional.

## Prerrequisitos

Antes de comenzar, asegúrate de contar con:

* **.NET 6+** (el código también funciona en .NET Framework 4.6+)  
* **Aspose.Cells for .NET** – la biblioteca que potencia las llamadas a `Workbook`, `Style` e `ImportDataTable`. Instálala vía NuGet:  

  ```bash
  dotnet add package Aspose.Cells
  ```

* Una fuente `DataTable` – la simularemos en el ejemplo, pero puedes reemplazarla con cualquier consulta ADO.NET.

¿Los tienes? Perfecto, vamos a empezar.

## Paso 1: Inicializar un nuevo Workbook (Palabra clave principal)

Lo primero que debes hacer es **how to create workbook** – literalmente. La clase `Workbook` representa todo el archivo Excel, y su constructor te brinda una hoja en blanco.

```csharp
using Aspose.Cells;
using System;
using System.Data;
using System.Drawing;

namespace ExcelStylingDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Create a new workbook (or obtain an existing one)
            Workbook workbook = new Workbook();   // <-- this is how to create workbook
```

> **Por qué es importante:** Comenzar con un `Workbook` nuevo garantiza que controles cada estilo desde el principio. Si abrieras un archivo existente, heredarías los estilos que el autor original dejó, lo que puede generar un formato inconsistente.

## Paso 2: Preparar la DataTable que importarás

Para ilustrar, vamos a crear una `DataTable` sencilla. En escenarios reales probablemente llamarías a un procedimiento almacenado o a un método de un ORM.

```csharp
            // Step 2: Retrieve the data you want to import (e.g., from a database)
            DataTable dataTable = GetSampleData(); // replace with your own GetData()
```

```csharp
        // Helper method that returns a dummy DataTable
        static DataTable GetSampleData()
        {
            DataTable table = new DataTable("Employees");
            table.Columns.Add("ID", typeof(int));
            table.Columns.Add("Name", typeof(string));
            table.Columns.Add("HireDate", typeof(DateTime));
            table.Columns.Add("Salary", typeof(decimal));

            table.Rows.Add(1, "Alice Johnson", new DateTime(2020, 5, 12), 72000);
            table.Rows.Add(2, "Bob Smith", new DateTime(2019, 3, 4), 68000);
            table.Rows.Add(3, "Carol White", DBNull.Value, 75000); // demonstrates a null value
            return table;
        }
```

> **Consejo:** Si necesitas conservar el orden de columnas exactamente como aparece en la base de datos, establece el parámetro `importColumnNames` de `ImportDataTable` a `true`. Esto indica a Aspose.Cells que escriba los encabezados de columna por ti.

## Paso 3: Definir estilos de columna – Predeterminado + Fondo azul claro

Ahora respondemos a la parte **add light blue background** del rompecabezas. Aspose.Cells te permite pasar un arreglo de objetos `Style` que corresponden a cada columna que importas. La primera entrada es el estilo para la columna 0, la segunda para la columna 1, y así sucesivamente. Si tienes menos estilos que columnas, las columnas restantes usan el estilo predeterminado.

```csharp
            // Step 3: Define column styles – the default style and a custom style with a light‑blue foreground
            Style defaultStyle = workbook.DefaultStyle; // this is the use default style excel
            Style lightBlueStyle = workbook.CreateStyle();
            lightBlueStyle.ForegroundColor = Color.LightBlue;
            lightBlueStyle.Pattern = BackgroundType.Solid; // make sure the color shows

            // Apply default style to the first column, light blue to the second column
            Style[] columnStyles = { defaultStyle, lightBlueStyle };
```

> **¿Por qué solo dos estilos?** En nuestro ejemplo tenemos cuatro columnas, pero solo queremos que la segunda columna (Name) destaque. La longitud del arreglo no necesita coincidir con el número de columnas; cualquier entrada faltante hereda automáticamente el estilo predeterminado del workbook.

## Paso 4: Importar la DataTable con encabezados y estilos

Aquí es donde combinamos **excel import datatable c#** y **import data with headers**. El método `ImportDataTable` hace el trabajo pesado: escribe los nombres de columna, las filas y aplica el arreglo de estilos que acabamos de crear.

```csharp
            // Step 4: Import the DataTable into the first worksheet starting at cell A1, applying the styles
            Worksheet sheet = workbook.Worksheets[0];
            sheet.Cells.ImportDataTable(dataTable, // the source DataTable
                                        true,       // import column names as headers
                                        0,          // start row (0‑based)
                                        0,          // start column (0‑based)
                                        columnStyles);
```

### Resultado esperado

Después de ejecutar el programa, `workbook` contendrá una sola hoja que se verá así:

| **ID** | **Name** (light‑blue) | **HireDate** | **Salary** |
|-------|------------------------|--------------|------------|
| 1     | Alice Johnson          | 5/12/2020    | 72000      |
| 2     | Bob Smith              | 3/4/2019     | 68000      |
| 3     | Carol White            | *(blank)*    | 75000      |

* La columna **Name** muestra un fondo azul claro, demostrando que el arreglo de estilos funciona.
* Los encabezados de columna se generan automáticamente porque pasamos `true` para `importColumnNames`.
* Los valores nulos aparecen como celdas vacías, que es el comportamiento predeterminado de Aspose.Cells.

## Paso 5: Guardar el Workbook (Opcional pero útil)

Probablemente querrás escribir el archivo en disco o enviarlo como stream a un cliente web. Guardar es sencillo:

```csharp
            // Step 5: Save the workbook to a file
            string outputPath = "StyledEmployees.xlsx";
            workbook.Save(outputPath, SaveFormat.Xlsx);
            Console.WriteLine($"Workbook saved to {outputPath}");
        }
    }
}
```

> **Pro tip:** Si estás orientado a versiones antiguas de Excel, cambia `SaveFormat.Xlsx` a `SaveFormat.Xls`. La API se encarga de la conversión por ti.

## Casos límite y variaciones

### Múltiples columnas con estilo

Si necesitas más de una columna con estilo, simplemente amplía el arreglo `columnStyles`:

```csharp
Style[] columnStyles = { defaultStyle, lightBlueStyle, defaultStyle, lightBlueStyle };
```

Ahora tanto **Name** como **Salary** tendrán fondo azul claro.

### Formato condicional en lugar de estilos fijos

A veces deseas que una columna se vuelva roja cuando un valor supera un umbral. Ahí es donde **use default style excel** se combina con formato condicional:

```csharp
int salaryColIdx = 3; // zero‑based index for Salary column
FormatCondition condition = sheet.ConditionalFormattings[0]
    .AddCondition(FormatConditionType.CellValue, OperatorType.GreaterThan, "70000");
condition.Style.ForegroundColor = Color.LightCoral;
condition.Style.Pattern = BackgroundType.Solid;
```

### Importar sin encabezados

Si tu sistema downstream ya provee sus propios encabezados, solo pasa `false` al argumento `importColumnNames`. Los datos comenzarán en `A1` y podrás escribir encabezados personalizados después.

```csharp
sheet.Cells.ImportDataTable(dataTable, false, 1, 0); // start at row 2 (index 1)
```

## Ejemplo completo funcionando (All

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}