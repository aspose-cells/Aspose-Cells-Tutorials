---
category: general
date: 2026-06-17
description: Establecer formato de fecha en Excel usando C# y también establecer el
  fondo de la celda, aplicar color de primer plano y colorear la columna de Excel
  durante la importación. Aprende paso a paso.
draft: false
keywords:
- set date format
- set cell background
- apply foreground color
- color excel column
- excel import formatting
language: es
og_description: Establecer formato de fecha en Excel con C# mientras se configura
  el fondo de la celda, se aplica color de primer plano y se colorea la columna de
  Excel durante la importación. Tutorial completo.
og_title: Establecer formato de fecha en Excel con C# – Guía completa
schemas:
- author: Aspose
  dateModified: '2026-06-17'
  description: Set date format in Excel using C# and also set cell background, apply
    foreground color, and color Excel column during import. Learn step‑by‑step.
  headline: Set date format in Excel with C# – Full Import Formatting Guide
  type: TechArticle
- description: Set date format in Excel using C# and also set cell background, apply
    foreground color, and color Excel column during import. Learn step‑by‑step.
  name: Set date format in Excel with C# – Full Import Formatting Guide
  steps:
  - name: 2.1 Set Date Format for the First Column
    text: The first column (`OrderDate`) should display as “MM/dd/yyyy”. Aspose uses
      the built‑in number format index 14 for the short date, but you can also supply
      a custom format string if you prefer.
  - name: 2.2 Set Cell Background for the Second Column
    text: Let’s give the `CustomerName` column a light blue background. This is where
      **set cell background** comes into play.
  - name: 2.3 Apply Foreground (Text) Color – Optional Extra
    text: 'If you also want the text itself to be a contrasting color, you can tweak
      the same style:'
  - name: 3.1 Save the Workbook
    text: '```csharp // Save to a file – change path as needed wb.Save("FormattedReport.xlsx",
      SaveFormat.Xlsx); Console.WriteLine("Excel file created with date format and
      colors."); ```'
  - name: What if I have more than two columns?
    text: Just expand the `columnStyles` array and assign a `Style` to each index
      you care about. Unassigned indexes will fall back to the default style, which
      is perfectly fine.
  - name: How do I format a column as currency?
    text: '```csharp columnStyles[3] = wb.CreateStyle(); columnStyles[3].Number =
      164; // Built‑in currency format (e.g., $#,##0.00) ```'
  - name: Can I change the header row style separately?
    text: 'Yes. After the import, you can grab the first row and apply a distinct
      style:'
  - name: What if the DataTable contains null dates?
    text: 'Aspose will leave those cells blank. If you prefer a placeholder like “N/A”,
      you can preprocess the table:'
  type: HowTo
tags:
- excel
- csharp
- aspnet
- data-import
title: Establecer formato de fecha en Excel con C# – Guía completa de formato de importación
url: /es/net/excel-custom-number-date-formatting/set-date-format-in-excel-with-c-full-import-formatting-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Establecer formato de fecha en Excel con C# – Guía completa de formato de importación

¿Alguna vez necesitaste **establecer el formato de fecha** en una hoja de Excel generada desde código C#, pero también querías que la columna tuviera un fondo o color de texto personalizado? No eres el único. En muchos escenarios de generación de informes extraes un `DataTable` de una base de datos, lo insertas en una hoja de cálculo y luego te apresuras a que las fechas se vean bien y las columnas resalten con los colores correctos.  

En este tutorial recorreremos una solución limpia, de extremo a extremo, que **establece el formato de fecha**, **establece el fondo de la celda**, **aplica color de primer plano**, e incluso **colorea una columna de Excel** mientras importas datos. Al final tendrás un patrón reutilizable que maneja **excel import formatting** sin el habitual ensayo y error.

> **Lo que necesitarás**  
> * .NET 6+ (o .NET Framework 4.7+)  
> * Aspose.Cells for .NET (la prueba gratuita funciona para pruebas)  
> * Una fuente `DataTable` – cualquier consulta ADO.NET servirá  
> * Visual Studio o tu IDE favorito  

Vamos a comenzar.

---

## Visión general de la solución

Dividiremos el problema en tres bloques lógicos:

1. **Recuperar los datos de origen** – un `DataTable` con las filas que deseas exportar.  
2. **Crear estilos específicos por columna** – un estilo para la columna de fecha, otro para una columna de texto, más cualquier estilo adicional que desees.  
3. **Importar la tabla con estilos** – usa `Worksheet.Cells.ImportDataTable` para que cada columna herede el estilo que preparaste.

¿Por qué este enfoque? Porque Aspose.Cells te permite adjuntar una matriz `Style` directamente a la llamada `ImportDataTable`, lo que significa que no necesitas una segunda pasada para volver a aplicar el formato. Es más rápido, menos propenso a errores y mantiene tu código ordenado.

---

## Paso 1: Recuperar los datos para exportar

Lo primero – necesitas un `DataTable`. En un proyecto real probablemente llamarías a un procedimiento almacenado o usarías Entity Framework para llenarlo, pero para ilustrar simularemos una tabla simple con una columna de fecha y una de texto.

```csharp
using System;
using System.Data;
using Aspose.Cells;

DataTable GetData()
{
    var table = new DataTable();
    table.Columns.Add("OrderDate", typeof(DateTime));
    table.Columns.Add("CustomerName", typeof(string));

    // Sample rows – replace with your DB call
    table.Rows.Add(DateTime.Today.AddDays(-2), "Acme Corp");
    table.Rows.Add(DateTime.Today.AddDays(-1), "Globex Inc");
    table.Rows.Add(DateTime.Today, "Soylent Co");

    return table;
}
```

> **Consejo profesional:** Si tu origen usa fechas anulables, asegúrate de que el tipo de columna sea `typeof(DateTime?)` – Aspose respetará el formato que asignes después.

---

## Paso 2: Preparar una matriz de estilos – Uno por columna

Ahora creamos un `Style[]` cuya longitud coincida con el número de columnas en el `DataTable`. Cada entrada contendrá el formato para su respectiva columna.

```csharp
// Create a new workbook and get the first worksheet
Workbook wb = new Workbook();
Worksheet ws = wb.Worksheets[0];

// Pull the data
DataTable dataTable = GetData();

// Allocate the style array
Style[] columnStyles = new Style[dataTable.Columns.Count];
```

### 2.1 Establecer formato de fecha para la primera columna

La primera columna (`OrderDate`) debe mostrarse como “MM/dd/yyyy”. Aspose usa el índice de formato numérico incorporado 14 para la fecha corta, pero también puedes proporcionar una cadena de formato personalizada si lo prefieres.

```csharp
// Style for the date column (index 0)
columnStyles[0] = wb.CreateStyle();
columnStyles[0].Number = 14;               // Built‑in short date format
// Or a custom pattern:
// columnStyles[0].Custom = "mm/dd/yyyy";
```

**Por qué es importante:** Excel almacena las fechas como números de serie. Al asignar un formato numérico, le indicas a Excel que renderice esos números como fechas legibles en lugar de valores crudos.

### 2.2 Establecer fondo de celda para la segunda columna

Démosle a la columna `CustomerName` un fondo azul claro. Aquí es donde entra en juego **set cell background**.

```csharp
// Style for the text column (index 1)
columnStyles[1] = wb.CreateStyle();
columnStyles[1].ForegroundColor = System.Drawing.Color.LightBlue;
columnStyles[1].Pattern = BackgroundType.Solid; // Needed to show the color
```

> **Nota:** Sin establecer `Pattern` a `Solid`, el color de primer plano no aparecerá porque el patrón predeterminado es “None”.

### 2.3 Aplicar color de primer plano (texto) – Extra opcional

Si también deseas que el texto tenga un color contrastante, puedes ajustar el mismo estilo:

```csharp
columnStyles[1].Font.Color = System.Drawing.Color.DarkBlue; // apply foreground color
```

Esto satisface el requisito de **apply foreground color** mientras mantiene intacto el fondo de la columna.

---

## Paso 3: Importar el DataTable con los estilos definidos

Con los estilos listos, el paso final es una sola línea que importa los datos y aplica los estilos columna por columna.

```csharp
// Import the DataTable starting at cell A1 (row 0, column 0)
// includeColumnNames = true to add a header row
ws.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);
```

**Cómo funciona:** Aspose lee la matriz `columnStyles` y asigna cada `Style` al índice de columna correspondiente. La fila de encabezado hereda el estilo predeterminado a menos que proporciones un estilo separado para la fila 0.

### 3.1 Guardar el libro de trabajo

```csharp
// Save to a file – change path as needed
wb.Save("FormattedReport.xlsx", SaveFormat.Xlsx);
Console.WriteLine("Excel file created with date format and colors.");
```

Ejecuta el programa, abre *FormattedReport.xlsx*, y deberías ver:

- La columna **OrderDate** mostrada como fechas (p. ej., `06/15/2026`).  
- La columna **CustomerName** con un relleno azul claro y texto azul oscuro.  

Ese es todo el flujo de trabajo de **excel import formatting** en menos de 30 líneas de C#.

---

## Recapitulación paso a paso (con por qué)

| Paso | Qué haces | Por qué es importante |
|------|-----------|-----------------------|
| **Recuperar datos** | Llamar a `GetData()` para llenar un `DataTable`. | Proporciona una fuente estructurada que Aspose puede ingerir directamente. |
| **Crear matriz de estilos** | Asignar `Style[]` con la cantidad de columnas. | Permite el estilo por columna en una única llamada de importación. |
| **Establecer formato de fecha** | `columnStyles[0].Number = 14;` | Garantiza que las fechas se rendericen correctamente en Excel. |
| **Establecer color de fondo** | `ForegroundColor = LightBlue; Pattern = Solid;` | Resalta la columna, cumpliendo **set cell background**. |
| **Aplicar color de primer plano** | `Font.Color = DarkBlue;` | Mejora la legibilidad y satisface **apply foreground color**. |
| **Importar con estilos** | `ImportDataTable(..., columnStyles);` | Importación de una sola pasada que respeta todo el formato. |
| **Guardar libro de trabajo** | `wb.Save(...);` | Persiste el resultado para los usuarios posteriores. |

---

## Manejo de casos límite y preguntas frecuentes

### ¿Qué pasa si tengo más de dos columnas?

Simplemente amplía la matriz `columnStyles` y asigna un `Style` a cada índice que te interese. Los índices no asignados volverán al estilo predeterminado, lo cual está perfectamente bien.

```csharp
columnStyles[2] = wb.CreateStyle();
columnStyles[2].Number = 0; // General format for numeric columns
```

### ¿Cómo formateo una columna como moneda?

```csharp
columnStyles[3] = wb.CreateStyle();
columnStyles[3].Number = 164; // Built‑in currency format (e.g., $#,##0.00)
```

### ¿Puedo cambiar el estilo de la fila de encabezado por separado?

Sí. Después de la importación, puedes obtener la primera fila y aplicar un estilo distinto:

```csharp
Style headerStyle = wb.CreateStyle();
headerStyle.Font.IsBold = true;
headerStyle.ForegroundColor = System.Drawing.Color.Gold;
headerStyle.Pattern = BackgroundType.Solid;

ws.Cells.Rows[0].ApplyStyle(headerStyle, new StyleFlag { All = true });
```

### ¿Qué ocurre si el DataTable contiene fechas nulas?

Aspose dejará esas celdas en blanco. Si prefieres un marcador como “N/A”, puedes preprocesar la tabla:

```csharp
foreach (DataRow row in dataTable.Rows)
{
    if (row.IsNull("OrderDate"))
        row["OrderDate"] = DateTime.MinValue; // or any sentinel
}
```

Luego ajusta el estilo para que muestre un formato personalizado que muestre “N/A” para el valor centinela.

---

## Ejemplo completo funcionando

A continuación tienes el programa completo, listo para copiar y pegar. Ejecútalo como una aplicación de consola y obtendrás un archivo Excel bien formateado.

```csharp
using System;
using System.Data;
using System.Drawing;
using Aspose.Cells;

class ExcelExportDemo
{
    static void Main()
    {
        // 1️⃣ Retrieve data
        DataTable dataTable = GetData();

        // 2️⃣ Create workbook & style array
        Workbook wb = new Workbook();
        Worksheet ws = wb.Worksheets[0];
        Style[] columnStyles = new Style[dataTable.Columns.Count];

        // 2a️⃣ Date column – set date format
        columnStyles[0] = wb.CreateStyle();
        columnStyles[0].Number = 14; // short date (MM/dd/yyyy)

        // 2b️⃣ Text column – set background & foreground colors
        columnStyles[1] = wb.CreateStyle();
        columnStyles[1].ForegroundColor = Color.LightBlue;
        columnStyles[1].Pattern = BackgroundType.Solid;
        columnStyles[1].Font.Color = Color.DarkBlue; // apply foreground color

        // 3️⃣ Import with formatting
        ws.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);

        // Optional: style header row
        Style headerStyle = wb.CreateStyle();
        headerStyle.Font.IsBold = true;
        headerStyle.ForegroundColor = Color.Gold;
        headerStyle.Pattern = BackgroundType.Solid;
        ws.Cells


## ¿Qué deberías aprender a continuación?


Los siguientes tutoriales cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos con explicaciones paso a paso para ayudarte a dominar características adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Establecer color de fuente en celdas de Excel usando Aspose.Cells para .NET](/cells/english/net/formatting/setting-font-color/)
- [Establecer color de fuente en Excel .NET con Aspose.Cells](/cells/english/net/formatting/set-font-color-net-excel-aspose-cells/)
- [Establecer anchura de columnas de Excel en píxeles usando Aspose.Cells para .NET | Guía paso a paso](/cells/english/net/formatting/set-excel-column-width-pixels-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}