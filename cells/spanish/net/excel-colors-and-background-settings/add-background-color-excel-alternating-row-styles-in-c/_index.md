---
category: general
date: 2026-04-07
description: Agregar color de fondo a filas de Excel usando C#. Aprende cómo aplicar
  colores alternados a las filas, establecer estilos de fondo sólido e importar una
  datatable a Excel en un solo flujo de trabajo.
draft: false
keywords:
- add background color excel
- apply alternating row colors
- style excel rows
- set solid background
- import datatable to excel
language: es
og_description: Agregar color de fondo a filas de Excel con C#. Esta guía muestra
  cómo aplicar colores alternados a las filas, establecer un fondo sólido e importar
  una tabla de datos a Excel de manera eficiente.
og_title: Añadir color de fondo en Excel – Estilos de filas alternas en C#
tags:
- C#
- Excel
- DataTable
- Styling
title: Agregar color de fondo en Excel – Estilos de filas alternas en C#
url: /es/net/excel-colors-and-background-settings/add-background-color-excel-alternating-row-styles-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Agregar color de fondo a Excel – Estilos de filas alternadas en C#

¿Alguna vez necesitaste **agregar color de fondo a Excel** a filas pero no estabas seguro de cómo hacerlo sin mil líneas de código complicado? No estás solo—la mayoría de los desarrolladores se topan con ese obstáculo cuando intentan por primera vez que sus hojas de cálculo se vean más que un simple volcado de datos.  

¿La buena noticia? En solo unos minutos puedes **aplicar colores de fila alternados**, establecer un **fondo sólido**, e incluso **importar datatable a excel** usando un patrón limpio y reutilizable en C#.  

En este tutorial recorreremos todo el proceso, desde extraer datos a un `DataTable` hasta estilizar cada fila con un patrón de franjas blanco‑amarillo‑claro. No se requieren bibliotecas externas más allá de un paquete sólido de manejo de Excel (como **ClosedXML** o **GemBox.Spreadsheet**), y verás por qué este enfoque es tanto eficiente como fácil de mantener.

## Lo que aprenderás

- Cómo recuperar datos y alimentarlos a una hoja de cálculo de Excel.
- Cómo **estilizar filas de excel** con colores de fondo alternados.
- La mecánica detrás de **establecer fondo sólido** usando el objeto `Style`.
- Cómo **importar datatable a excel** manteniendo los estilos de fila.
- Consejos para manejar casos límite como tablas vacías o esquemas de colores personalizados.

> **Consejo profesional:** Si ya estás usando un objeto de libro de trabajo (`wb`) de una biblioteca que soporta la creación de estilos, puedes reutilizar las mismas instancias de `Style` en múltiples hojas de cálculo—ahorrando memoria y manteniendo tu código ordenado.

---

## Paso 1: Recuperar los datos – Preparando el DataTable

Antes de que pueda ocurrir cualquier estilo, necesitamos una fuente de filas. En la mayoría de los escenarios reales esto proviene de una base de datos, una API o un archivo CSV. Para ilustrar, simplemente crearemos un `DataTable` simple en memoria.

```csharp
using System;
using System.Data;
using System.Drawing;          // For Color
using GemBox.Spreadsheet;      // Or ClosedXML, whichever you prefer

// Simulated data fetch – replace with your own data access logic
DataTable GetData()
{
    var table = new DataTable();
    table.Columns.Add("Id", typeof(int));
    table.Columns.Add("Name", typeof(string));
    table.Columns.Add("Score", typeof(double));

    // Populate with sample rows
    for (int i = 1; i <= 10; i++)
        table.Rows.Add(i, $"Student {i}", Math.Round(new Random().NextDouble() * 100, 2));

    return table;
}
```

**Por qué es importante:** Usar un `DataTable` te brinda un contenedor tabular y consciente del esquema que la biblioteca de Excel puede importar directamente, eliminando la necesidad de escribir bucles celda por celda.

---

## Paso 2: Crear estilos de fila – **Aplicar colores de fila alternados**

Ahora construiremos una matriz de objetos `Style`—uno por fila—para que cada fila pueda recibir su propio fondo. El patrón que usaremos es un clásico amarillo claro para filas pares y blanco para filas impares.

```csharp
// Assume 'wb' is an existing Workbook instance
Workbook wb = new Workbook();

// Retrieve data
DataTable dataTable = GetData();

// Allocate a style for each row
Style[] rowStyles = new Style[dataTable.Rows.Count];

for (int i = 0; i < rowStyles.Length; i++)
{
    // Create a fresh style instance
    rowStyles[i] = wb.CreateStyle();

    // Choose background colour based on row index
    rowStyles[i].ForegroundColor = (i % 2 == 0) ? Color.LightYellow : Color.White;

    // Ensure the colour is actually applied
    rowStyles[i].Pattern = BackgroundType.Solid;   // <-- **set solid background**
}
```

**Explicación:**  
- `wb.CreateStyle()` te brinda un objeto de estilo limpio que puedes ajustar sin afectar a otros.  
- El operador ternario `(i % 2 == 0)` decide si la fila es par (amarillo claro) o impar (blanco).  
- Establecer `Pattern = BackgroundType.Solid` es el paso crucial que **establece fondo sólido**; sin ello el color sería ignorado.

---

## Paso 3: Obtener la hoja de cálculo objetivo

La mayoría de las bibliotecas exponen una colección de hojas de cálculo. Trabajaremos con la primera, pero puedes apuntar a cualquier índice o nombre que prefieras.

```csharp
Worksheet worksheet = wb.Worksheets[0];   // First worksheet in the workbook
```

Si el libro de trabajo es completamente nuevo, la biblioteca suele crear una hoja predeterminada para ti. De lo contrario, puedes agregar una explícitamente:

```csharp
// Alternative: create a new sheet named "Report"
Worksheet worksheet = wb.Worksheets.Add("Report");
```

---

## Paso 4: Importar el DataTable con estilos de fila – **Importar datatable a excel**

Con los estilos listos, el paso final es insertar el `DataTable` en la hoja mientras se aplica el estilo correspondiente a cada fila.

```csharp
// Parameters: (DataTable, includeHeaders, startRow, startColumn, stylesArray)
worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, rowStyles);
```

**¿Qué está ocurriendo bajo el capó?**  
- `true` indica al método que escriba los encabezados de columna como la primera fila.  
- `0, 0` marca la esquina superior izquierda (A1) como punto de inserción.  
- `rowStyles` alinea cada `Style` con la fila de datos correspondiente, dándonos los colores alternados que preparamos antes.

---

## Paso 5: Guardar el libro de trabajo

La última pieza del rompecabezas es persistir el libro de trabajo en un archivo para que puedas abrirlo en Excel y ver el resultado.

```csharp
// Choose a format – XLSX is the modern default
wb.Save("StudentScores.xlsx");

// Optional: open automatically (Windows only)
System.Diagnostics.Process.Start("StudentScores.xlsx");
```

Abre el archivo y deberías ver una hoja ordenadamente formateada:

- Fila de encabezado en negrita (estilo predeterminado de la biblioteca).  
- Filas 1, 3, 5… con un fondo blanco limpio.  
- Filas 2, 4, 6… con un relleno sutil amarillo claro, facilitando la lectura.

### Captura del resultado esperado

| Id | Name      | Score |
|----|-----------|-------|
| 1  | Student 1 | 78.45 |
| 2  | Student 2 | 62.13 |
| 3  | Student 3 | 91.27 |
| …  | …         | …     |

Rows 2, 4, 6, … appear with a light‑yellow background—exactly the **apply alternating row colors** effect we aimed for.

![Ejemplo de agregar color de fondo a Excel](https://example.com/excel-background.png "Ejemplo de agregar color de fondo a Excel")

*(El texto alternativo incluye la palabra clave principal para SEO.)*

---

## Manejo de casos límite y variaciones

### DataTable vacío

Si `dataTable.Rows.Count` es cero, la matriz `rowStyles` estará vacía y `ImportDataTable` aún escribirá la fila de encabezado (si `includeHeaders` es `true`). No se lanza ninguna excepción, pero podrías querer protegerte contra generar un archivo casi vacío:

```csharp
if (dataTable.Rows.Count == 0)
{
    Console.WriteLine("No data to export – workbook will contain only headers.");
}
```

### Esquemas de color personalizados

¿Quieres una franja azul/gris en lugar de amarilla/blanca? Simplemente reemplaza los valores de `Color`:

```csharp
rowStyles[i].ForegroundColor = (i % 2 == 0) ? Color.LightBlue : Color.LightGray;
```

Siéntete libre de obtener los colores de un archivo de configuración para que los no‑desarrolladores puedan ajustar la paleta sin tocar el código.

### Reutilizar estilos en múltiples hojas de cálculo

Si exportas varias tablas al mismo libro de trabajo, puedes generar la matriz de estilos una vez y reutilizarla:

```csharp
Style[] sharedStyles = CreateAlternatingStyles(dataTable.Rows.Count);
worksheet1.Cells.ImportDataTable(dt1, true, 0, 0, sharedStyles);
worksheet2.Cells.ImportDataTable(dt2, true, 0, 0, sharedStyles);
```

Solo ten cuidado de que ambas tablas tengan el mismo número de filas, o genera una nueva matriz por hoja.

---

## Ejemplo completo funcional

Juntando todo, aquí tienes un programa autocontenido que puedes copiar y pegar en una aplicación de consola.

```csharp
using System;
using System.Data;
using System.Drawing;
using GemBox.Spreadsheet;   // Install-Package GemBox.Spreadsheet

class Program
{
    static void Main()
    {
        // License free for small projects – remove for commercial use
        SpreadsheetInfo.SetLicense("FREE-LIMITED-KEY");

        // 1️⃣ Retrieve data
        DataTable dataTable = GetData();

        // 2️⃣ Initialise workbook
        Workbook wb = new Workbook();

        // 3️⃣ Create alternating row styles
        Style[] rowStyles = CreateAlternatingStyles(dataTable.Rows.Count);

        // 4️⃣ Get (or create) the target worksheet
        Worksheet ws = wb.Worksheets.Add("Report");

        // 5️⃣ Import data with styles
        ws.Cells.ImportDataTable(dataTable, true, 0, 0, rowStyles);

        // 6️⃣ Save the file
        wb.Save("Report.xlsx");
        Console.WriteLine("Excel file created – check Report.xlsx");
    }

    // Helper: generate a DataTable with sample data
    static DataTable GetData()
    {
        var dt = new DataTable();
        dt.Columns.Add("Id", typeof(int));
        dt.Columns.Add("Name", typeof(string));
        dt.Columns.Add("Score", typeof(double));

        var rnd = new Random();
        for (int i = 1; i <= 12; i++)
            dt.Rows.Add(i, $"Student {i}", Math.Round(rnd.NextDouble() * 100, 2));

        return dt;
    }

    // Helper: create style array for alternating colors
    static Style[] CreateAlternatingStyles(int rowCount)
    {
        var wb = new Workbook();               // Temporary workbook for style creation
        var styles = new Style[rowCount];
        for (int i = 0; i < rowCount; i++)
        {
            styles[i] = wb.CreateStyle();
            styles[i].ForegroundColor = (i % 2 == 0) ? Color.LightYellow : Color.White;
            styles[i].Pattern = BackgroundType.Solid;   // **set solid background**
        }
        return styles;
    }
}
```

Ejecuta el programa, abre `Report.xlsx`, y verás el fondo alternado exactamente como se describió.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}