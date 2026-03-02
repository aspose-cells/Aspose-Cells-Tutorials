---
category: general
date: 2026-03-01
description: Importa datos con formato a Excel usando C#. Aprende cómo importar DataTable
  a Excel y agregar color de fondo a las celdas en solo unos pocos pasos.
draft: false
keywords:
- import data with formatting
- how to import datatable into excel
- add background color to excel cells
language: es
og_description: Importar datos con formato en Excel usando C#. Guía paso a paso que
  muestra cómo importar una DataTable y agregar color de fondo a las celdas.
og_title: Importar datos con formato a Excel – Guía de C#
tags:
- C#
- Excel
- DataTable
- Formatting
title: Importar datos con formato a Excel usando C#
url: /es/net/excel-data-import-export/import-data-with-formatting-into-excel-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Importar datos con formato en Excel usando C#

¿Alguna vez necesitaste **importar datos con formato** en un libro de Excel pero seguías obteniendo una hoja simple y aburrida? No estás solo. La mayoría de los desarrolladores se topan con ese problema cuando descubren que la importación predeterminada elimina todos los colores y estilos que cuidadosamente configuraron en sus datos de origen.

En este tutorial recorreremos una solución completa, lista‑para‑ejecutar que **importa un DataTable a Excel** y **agrega color de fondo a las celdas de Excel** al mismo tiempo. No se requiere procesamiento posterior; tu hoja de cálculo se verá exactamente como deseas desde el principio.

## Lo que aprenderás

- Cómo obtener datos en un `DataTable`.
- Cómo definir una matriz de objetos `Style` que contienen colores de fondo.
- Cómo llamar a `ImportDataTable` con esos estilos para que la importación preserve el formato.
- Un ejemplo completo y ejecutable que puedes insertar en una aplicación de consola y ver el resultado al instante.
- Consejos, trampas y variaciones para proyectos del mundo real.

### Requisitos previos

- .NET 6.0 o posterior (el código también funciona con .NET Framework 4.6+).
- La biblioteca **GemBox.Spreadsheet** (la versión gratuita es suficiente para la demostración).
- Familiaridad básica con C# y conceptos de Excel.

Si te preguntas *¿por qué GemBox?* es porque ofrece un método de una sola línea `ImportDataTable` que acepta matrices de estilos —exactamente lo que necesitamos para **importar datos con formato** sin escribir un bucle.

---

## Paso 1: Configurar el proyecto y agregar GemBox.Spreadsheet

Para comenzar, crea una nueva aplicación de consola:

```bash
dotnet new console -n ExcelImportDemo
cd ExcelImportDemo
dotnet add package GemBox.Spreadsheet
```

> **Consejo profesional:** La versión gratuita limita las hojas de cálculo a 150 k celdas, lo cual es suficiente para demostraciones. Si alcanzas el límite, actualiza o cambia a EPPlus, pero la API se verá ligeramente diferente.

## Paso 2: Recuperar los datos de origen como un `DataTable`

Lo primero que necesitamos es un `DataTable` que imite los datos que normalmente extraerías de una base de datos. Aquí tienes un pequeño asistente que crea uno en memoria:

```csharp
using System;
using System.Data;
using System.Drawing;
using GemBox.Spreadsheet;

class Program
{
    static void Main()
    {
        // Register the free license (remove for paid version).
        SpreadsheetInfo.SetLicense("FREE-LIMITED-KEY");

        // 1️⃣ Retrieve the source data as a DataTable.
        DataTable dataTable = GetSampleData();

        // Remaining steps will follow...
    }

    /// <summary>
    /// Generates a sample DataTable with three columns and five rows.
    /// In a real app you’d replace this with a DB call.
    /// </summary>
    static DataTable GetSampleData()
    {
        var table = new DataTable("Report");
        table.Columns.Add("ID", typeof(int));
        table.Columns.Add("Name", typeof(string));
        table.Columns.Add("Score", typeof(double));

        table.Rows.Add(1, "Alice", 93.5);
        table.Rows.Add(2, "Bob", 78.0);
        table.Rows.Add(3, "Charlie", 85.2);
        table.Rows.Add(4, "Diana", 91.3);
        table.Rows.Add(5, "Ethan", 67.8);

        return table;
    }
}
```

**Por qué es importante:** Al separar la obtención de datos en su propio método, puedes cambiar a cualquier origen —SQL, CSV, servicio web— sin tocar la lógica de importación. Esto mantiene el código limpio y hace que el tutorial **cómo importar datatable a excel** sea reutilizable.

## Paso 3: Definir los estilos que deseas aplicar

Ahora llega la parte divertida: crearemos una matriz de objetos `Style`, cada uno con un `ForegroundColor` distinto. GemBox te permite establecer `BackgroundPatternColor` (el relleno de la celda) y `ForegroundColor` (el color del texto). Para esta demostración colorearemos de forma diferente las dos primeras columnas.

```csharp
        // 2️⃣ Define the styles to apply to the imported cells.
        Style[] importStyles = new Style[]
        {
            new Style() { BackgroundPatternColor = Color.LightBlue },   // Column 0 – Light blue fill
            new Style() { BackgroundPatternColor = Color.LightGreen }   // Column 1 – Light green fill
            // No style for column 2 – it will keep the default look.
        };
```

**Explicación:**  
- Los objetos `Style` son contenedores ligeros; no necesitas crear uno nuevo para cada celda.  
- Al alinear el orden de la matriz con el orden de las columnas, GemBox aplica automáticamente el estilo correspondiente durante la importación.  
- Esta es la clave para **importar datos con formato** —el formato viaja con los datos, no después.

## Paso 4: Importar el `DataTable` en la hoja de cálculo con estilos

Con los datos y estilos listos, ahora podemos crear un libro de trabajo, seleccionar la primera hoja y llamar a `ImportDataTable`. La firma del método se ve así:

```csharp
public void ImportDataTable(
    DataTable dataTable,
    bool includeColumnNames,
    int startRow,
    int startColumn,
    Style[] columnStyles = null);
```

Así es como lo usamos:

```csharp
        // 3️⃣ Create a new workbook and import the DataTable.
        var workbook = new ExcelFile();
        var worksheet = workbook.Worksheets.Add("Report");

        // Import, include column headers, start at A1 (0,0), apply our styles.
        worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, importStyles);

        // Save the file to disk.
        workbook.Save("Report.xlsx");

        Console.WriteLine("Excel file 'Report.xlsx' created with formatted data.");
```

**¿Qué está sucediendo bajo el capó?**  
- `true` indica a GemBox que escriba los nombres de columna como la primera fila.  
- `0, 0` posiciona la importación en la celda A1.  
- `importStyles` vincula cada columna con los colores que definimos anteriormente.  

Cuando abras *Report.xlsx*, verás la columna **ID** con un sombreado azul claro, la columna **Name** con un sombreado verde claro, y la columna **Score** sin cambios. Eso es **importar datos con formato** en una sola llamada.

## Paso 5: Verificar el resultado (Salida esperada)

Abre el `Report.xlsx` generado. Deberías ver algo como esto:

| ID (azul claro) | Name (verde claro) | Score |
|-----------------|--------------------|-------|
| 1               | Alice              | 93.5 |
| 2               | Bob                | 78.0 |
| 3               | Charlie            | 85.2 |
| 4               | Diana              | 91.3 |
| 5               | Ethan              | 67.8 |

- Las celdas de la columna **ID** tienen un fondo azul claro.  
- Las celdas de la columna **Name** tienen un fondo verde claro.  
- La columna **Score** permanece con el fondo blanco predeterminado.

Esa pista visual hace que el informe sea instantáneamente escaneable, un pequeño detalle que puede mejorar drásticamente la experiencia del usuario.

![Hoja de Excel que muestra importación de datos con formato – columna ID azul claro, columna Name verde claro](excel-screenshot.png "ejemplo de importación de datos con formato")

*El texto alternativo de la imagen incluye la palabra clave principal para SEO.*

## Preguntas frecuentes y casos límite

### ¿Puedo aplicar algo más que colores de fondo?

Absolutamente. `Style` te permite establecer fuentes, bordes, formatos numéricos e incluso formato condicional. Por ejemplo, para que las puntuaciones superiores a 90 sean negritas y rojas:

```csharp
Style highScoreStyle = new Style()
{
    FontColor = Color.Red,
    FontBold = true
};
worksheet.Cells["C2:C6"].ConditionalFormatting.Add(
    ConditionalFormattingCondition.GreaterThan, "90", highScoreStyle);
```

### ¿Qué pasa si mi DataTable tiene más columnas que estilos?

GemBox aplicará estilos solo a las columnas que tengan una entrada coincidente en la matriz. Las columnas extra volverán al estilo predeterminado —no se lanza error.

### ¿Esto funciona con conjuntos de datos grandes?

Sí, pero vigila el límite de celdas de la versión gratuita (150 k celdas). Para informes masivos, considera la licencia de pago o transmite los datos fila por fila con `worksheet.Cells[row, col].Value = …` —aunque perderás la comodidad de una sola línea.

### ¿Cómo importo datos con formato desde una plantilla de Excel existente?

Puedes cargar primero un libro de trabajo de plantilla:

```csharp
var template = ExcelFile.Load("Template.xlsx");
var targetSheet = template.Worksheets[0];
targetSheet.Cells.ImportDataTable(dataTable, true, 5, 2, importStyles);
template.Save("FilledReport.xlsx");
```

Esto te permite conservar logotipos de encabezado, pies de página y cualquier estilo preexistente mientras aún **importas datos con formato** para la parte dinámica.

## Ejemplo completo y funcional (listo para copiar y pegar)

```csharp
using System;
using System.Data;
using System.Drawing;
using GemBox.Spreadsheet;

class Program
{
    static void Main()
    {
        // Register free license key.
        SpreadsheetInfo.SetLicense("FREE-LIMITED-KEY");

        // 1️⃣ Get the source data.
        DataTable dataTable = GetSampleData();

        // 2️⃣ Define column styles (background colors).
        Style[] importStyles = new Style[]
        {
            new Style() { BackgroundPatternColor = Color.LightBlue },   // ID column
            new Style() { BackgroundPatternColor = Color.LightGreen }   // Name column
            // Score column gets default style.
        };

        // 3️⃣ Create workbook and import with styles.
        var workbook = new ExcelFile();
        var worksheet = workbook.Worksheets.Add("Report");

        worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, importStyles);

        // Save the result.
        workbook.Save("Report.xlsx");

        Console.WriteLine("Report.xlsx created – import data with formatting complete.");
    }

    static DataTable GetSampleData()
    {
        var table = new DataTable("Report");
        table.Columns.Add("ID", typeof(int));
        table.Columns.Add("Name", typeof(string));
        table.Columns.Add("Score", typeof(double));

        table.Rows.Add(1, "Alice", 93.5);
        table.Rows.Add(2, "Bob", 78.0);
        table.Rows.Add(3, "Charlie", 85.2);
        table.Rows.Add(4, "Diana", 91.3);
        table.Rows.Add(5, "Ethan", 67.8);

        return table;
    }
}
```

Ejecuta el programa (`dotnet run`) y abre el *Report.xlsx* generado para ver los colores aplicados al instante.

## Conclusión

Ahora tienes una base sólida, end

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}