---
category: general
date: 2026-03-30
description: Crear libro de Excel en C# con formato de moneda. Aprende cómo importar
  una DataTable, agregar formato numérico en Excel y aplicar formato de moneda a una
  columna en minutos.
draft: false
keywords:
- create excel workbook c#
- format cells currency
- import datatable to excel
- add number format excel
- apply currency format column
language: es
og_description: Crea un libro de Excel en C# y formatea instantáneamente las celdas
  como moneda. Este tutorial paso a paso muestra cómo importar una DataTable a Excel
  y agregar formato numérico de Excel a una columna.
og_title: Crear libro de Excel en C# – Guía de formato de moneda
tags:
- Aspose.Cells
- C#
- Excel automation
title: Crear libro de Excel C# – Aplicar formato de moneda e importar DataTable
url: /es/net/excel-data-import-export/create-excel-workbook-c-apply-currency-format-and-import-dat/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crear libro de Excel C# – Aplicar formato de moneda e importar DataTable

¿Alguna vez necesitaste **create Excel workbook C#** que ya tenga el aspecto de un informe pulido? Tal vez estés extrayendo números de ventas de una base de datos y quieras que la columna de precio se muestre en dólares sin tener que manipular Excel manualmente. ¿Te suena? No estás solo—la mayoría de los desarrolladores se topan con este problema cuando automatizan exportaciones a Excel por primera vez.

En esta guía recorreremos una solución completa, lista‑para‑ejecutar que **creates an Excel workbook C#**, importa un `DataTable` y **formats the Price column as currency**. Al final tendrás un archivo llamado `StyledTable.xlsx` que podrás abrir y ver números con formato agradable. No se requiere procesamiento adicional.

> **Qué aprenderás**
> - How to set up Aspose.Cells in a .NET project  
> - How to **import datatable to excel** with a style array  
> - How to **add number format excel** for a specific column  
> - Tips for handling more columns or different locales  

> **Prerequisitos**  
> - .NET 6+ (o .NET Framework 4.6+) instalado  
> - Aspose.Cells for .NET NuGet package (`Install-Package Aspose.Cells`)  
> - Familiaridad básica con C# y DataTables  

---

## Paso 1: Preparar el DataTable (import datatable to excel)

Primero, necesitamos algunos datos de ejemplo. En una aplicación real probablemente rellenarías esta tabla a partir de una consulta a la base de datos, pero un ejemplo codificado mantiene las cosas simples.

```csharp
using System.Data;

// Create a DataTable with two columns: Product (string) and Price (double)
DataTable dataTable = new DataTable();
dataTable.Columns.Add("Product", typeof(string));
dataTable.Columns.Add("Price", typeof(double));

// Add a few rows – you can add as many as you like
dataTable.Rows.Add("Apple", 1.23);
dataTable.Rows.Add("Banana", 0.78);
dataTable.Rows.Add("Cherry", 2.50);
```

*Por qué es importante*: El `DataTable` es el puente entre tus datos de negocio y el archivo Excel. Aspose.Cells puede importarlo directamente, preservando los nombres de columnas y los tipos de datos.

---

## Paso 2: Crear un nuevo Workbook (create excel workbook c#)

Ahora creamos el objeto real del archivo Excel. Piensa en él como el lienzo en blanco sobre el que pintarás.

```csharp
using Aspose.Cells;

// Instantiate a fresh workbook – this is the core of create excel workbook c#
Workbook workbook = new Workbook();

// Grab the first worksheet (index 0). You could also add more sheets later.
Worksheet worksheet = workbook.Worksheets[0];
```

> **Consejo:** Si necesitas varias hojas, llama a `workbook.Worksheets.Add()` y asigna a cada una un nombre significativo.

---

## Paso 3: Definir un estilo de moneda (format cells currency)

Aspose.Cells te permite crear un objeto `Style` que describe cómo deben verse las celdas. Para moneda usamos el formato numérico incorporado ID 164 (`"$#,##0.00"`).

```csharp
// Create a new style object for the price column
Style priceStyle = workbook.CreateStyle();
priceStyle.Number = 164; // Built‑in currency format "$#,##0.00"
```

*¿Por qué no simplemente establecer la cadena de formato?* Usar el ID incorporado garantiza compatibilidad entre versiones de Excel y evita peculiaridades específicas de la configuración regional.

---

## Paso 4: Construir la matriz de estilos (apply currency format column)

Al importar un `DataTable`, puedes pasar una matriz de objetos `Style`—uno por columna. `null` significa “usar el estilo predeterminado”. Aquí aplicamos `priceStyle` solo a la segunda columna.

```csharp
// Column 0 (Product) gets the default style, Column 1 (Price) gets the currency style
Style[] columnStyles = { null, priceStyle };
```

Si más adelante añades más columnas, simplemente extiende la matriz en consecuencia. La longitud de `columnStyles` debe coincidir con el número de columnas que estás importando, de lo contrario Aspose lanzará una excepción.

---

## Paso 5: Importar el DataTable con estilos (import datatable to excel)

Ahora ocurre la magia—nuestro `DataTable` se coloca en la hoja de cálculo, y la columna de precio se muestra instantáneamente como moneda.

```csharp
// Parameters:
//  - dataTable: source data
//  - true: include column headers
//  - startRow: 0 (top of sheet)
//  - startColumn: 0 (first column)
//  - columnStyles: style array defined above
worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);
```

*¿Qué pasa si tienes más de dos columnas?* Simplemente expande `columnStyles` para que cada columna reciba el estilo apropiado (o `null` para el predeterminado). Esta es la forma más limpia de **add number format excel** de manera selectiva.

---

## Paso 6: Guardar el Workbook (create excel workbook c#)

Finalmente, escribimos el archivo en disco. Elige cualquier carpeta a la que tengas permiso de escritura.

```csharp
// Save the workbook as an XLSX file
workbook.Save("YOUR_DIRECTORY/StyledTable.xlsx");
```

Abre `StyledTable.xlsx` en Excel y deberías ver:

| Product | Price |
|---------|-------|
| Apple   | $1.23 |
| Banana  | $0.78 |
| Cherry  | $2.50 |

La columna **Price** ya está formateada como moneda—no se necesitan pasos adicionales.

---

## Casos límite y variaciones

### Más columnas, diferentes formatos

Si necesitas **format cells currency** para varias columnas (p.ej., Cost, Tax, Total), crea un `Style` separado para cada una y rellena `columnStyles` en consecuencia:

```csharp
Style costStyle = workbook.CreateStyle();
costStyle.Number = 164; // currency

Style taxStyle = workbook.CreateStyle();
taxStyle.Number = 164;

// Assuming columns: Product, Cost, Tax, Total
Style[] styles = { null, costStyle, taxStyle, priceStyle };
worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, styles);
```

### Moneda específica de la configuración regional

Para Euro o Libra esterlina, usa diferentes IDs incorporados (p.ej., 165 para `€#,##0.00`). Alternativamente, establece una cadena de formato personalizada:

```csharp
priceStyle.Custom = "€#,##0.00";
```

### Conjuntos de datos grandes

Aspose.Cells puede manejar millones de filas, pero el consumo de memoria crece con los objetos de estilo. Reutiliza una única instancia de `Style` para todas las columnas de moneda para mantener bajo el uso de memoria.

### Estilos faltantes

Si `columnStyles` es más corto que el número de columnas, Aspose aplicará el estilo predeterminado a las columnas restantes. Esto es útil cuando solo te importan unas pocas columnas.

---

## Ejemplo completo (todos los pasos combinados)

A continuación se muestra el programa completo que puedes copiar y pegar en una aplicación de consola. Incluye todas las piezas que discutimos, más algunos comentarios útiles.

```csharp
using Aspose.Cells;
using System;
using System.Data;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Build sample DataTable (import datatable to excel)
        // -------------------------------------------------
        DataTable dataTable = new DataTable();
        dataTable.Columns.Add("Product", typeof(string));
        dataTable.Columns.Add("Price", typeof(double));
        dataTable.Rows.Add("Apple", 1.23);
        dataTable.Rows.Add("Banana", 0.78);
        dataTable.Rows.Add("Cherry", 2.50);
        // You can add as many rows as you like here.

        // -------------------------------------------------
        // Step 2: Create a new workbook (create excel workbook c#)
        // -------------------------------------------------
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // -------------------------------------------------
        // Step 3: Define a currency style (format cells currency)
        // -------------------------------------------------
        Style priceStyle = workbook.CreateStyle();
        priceStyle.Number = 164; // "$#,##0.00" – built‑in currency format

        // -------------------------------------------------
        // Step 4: Build the style array (apply currency format column)
        // -------------------------------------------------
        // First column gets default style (null), second column uses priceStyle.
        Style[] columnStyles = { null, priceStyle };

        // -------------------------------------------------
        // Step 5: Import the DataTable with the style array
        // -------------------------------------------------
        worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);

        // -------------------------------------------------
        // Step 6: Save the workbook to disk
        // -------------------------------------------------
        string outputPath = @"YOUR_DIRECTORY\StyledTable.xlsx";
        workbook.Save(outputPath);

        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

**Resultado esperado:** Al abrir `StyledTable.xlsx` se muestra la columna `Price` con el símbolo de dólar y dos decimales, exactamente como lo exige la instrucción `format cells currency`.

---

## Preguntas frecuentes

**P: ¿Esto funciona con .NET Core?**  
R: Absolutamente. Aspose.Cells es compatible con .NET‑standard, por lo que puedes apuntar a .NET 5, .NET 6 o versiones posteriores sin cambios.

**P: ¿Qué pasa si mi DataTable tiene 10 columnas pero solo quiero formatear la columna 5?**  
R: Crea un `Style[]` de longitud 10, rellena las posiciones 0‑4 y 6‑9 con `null`, y coloca tu estilo personalizado en el índice 4 (basado en cero). Aspose respetará cada entrada.

**P: ¿Puedo ocultar la fila de encabezado?**  
R: Después de la importación, establece `worksheet.Cells.Rows[0].Hidden = true;` o simplemente pasa `false` para el parámetro `includeColumnNames` en `ImportDataTable`.

---

## Conclusión

Acabamos de **create an Excel workbook C#**, importar un `DataTable` y **apply a currency format column** usando Aspose.Cells. Los pasos principales—preparar los datos, definir un estilo, construir una matriz de estilos, importar con `ImportDataTable` y guardar—cubren el núcleo de la mayoría de las tareas de automatización de Excel.

Desde aquí podrías explorar:

- **add number format excel** para fechas o porcentajes  
- Exportar varias hojas de cálculo en un solo archivo  
- Usar **format cells currency** con símbolos específicos de la configuración regional  
- Automatizar la creación de gráficos basados en los mismos datos  

Pruébalos, y pronto te convertirás en la persona de referencia para los informes de Excel en tu equipo. ¿Tienes una variante que te gustaría compartir? Deja un comentario abajo—¡feliz codificación!

![create excel workbook c# screenshot](image.png "create excel workbook c#")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}