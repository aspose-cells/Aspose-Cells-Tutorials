---
category: general
date: 2026-03-22
description: Tutorial de formato de número personalizado en Excel que muestra cómo
  importar una tabla de datos a Excel, establecer el color de fondo de la columna,
  formatear la columna como moneda y guardar el libro de trabajo como xlsx.
draft: false
keywords:
- custom number format excel
- import datatable to excel
- set column background color
- format column as currency
- save workbook as xlsx
language: es
og_description: Tutorial de Excel sobre formato de número personalizado que te guía
  a través de la importación de una DataTable, la configuración del color de fondo
  de una columna, el formato de una columna como moneda y el guardado del libro de
  trabajo como xlsx.
og_title: Formato de número personalizado en Excel con C# – Guía paso a paso
tags:
- C#
- Excel automation
- Aspose.Cells
- Data export
title: Formato de número personalizado en Excel con C# – Guía completa
url: /es/net/excel-custom-number-date-formatting/custom-number-format-excel-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Formato de número personalizado en Excel – Tutorial Full‑Stack C#

¿Alguna vez te has preguntado cómo aplicar un estilo de **custom number format excel** directamente desde C#? Tal vez hayas intentado volcar un DataTable en una hoja de cálculo solo para ver números simples, sin colores y sin formato de moneda. Ese es un punto de dolor común, especialmente cuando necesitas un informe pulido para los interesados.

En esta guía resolveremos ese problema juntos: aprenderás a **import datatable to excel**, **set column background color**, **format column as currency**, y finalmente **save workbook as xlsx** con un formato de número personalizado que hará que tus cifras resalten. Sin referencias vagas, solo una solución completa y ejecutable que puedes copiar‑pegar en tu proyecto.

---

## Lo que construirás

Al final de este tutorial tendrás una aplicación de consola C# autosuficiente que:

1. Recupera un `DataTable` (puedes reemplazar el stub con tu propia consulta).  
2. Crea un nuevo libro de Excel usando Aspose.Cells (o cualquier biblioteca compatible).  
3. Aplica una fuente azul y en negrita a la primera columna, un fondo amarillo claro a la segunda, y un formato de moneda (`$#,##0.00`) a la tercera.  
4. Guarda el archivo como `DataTableWithStyleArray.xlsx` en la carpeta que elijas.

Verás exactamente cómo cada línea contribuye al archivo Excel final, y discutiremos por qué esas decisiones importan para el mantenimiento y el rendimiento.

---

## Requisitos previos

- .NET 6.0 o posterior (el código también funciona con .NET Framework 4.7+).  
- Aspose.Cells para .NET (versión de prueba gratuita o con licencia). Instálalo vía NuGet:

```bash
dotnet add package Aspose.Cells
```

- Familiaridad básica con `DataTable` y aplicaciones de consola C#.

---

## Paso 1: Recuperar los datos de origen como DataTable

Primero, necesitamos algunos datos para exportar. En un escenario real probablemente llames a un repositorio o ejecutes una consulta SQL. Para ilustrar crearemos una tabla simple en memoria.

```csharp
using System;
using System.Data;
using Aspose.Cells;

static DataTable GetSampleData()
{
    var table = new DataTable("Sales");
    table.Columns.Add("Product", typeof(string));
    table.Columns.Add("Quantity", typeof(int));
    table.Columns.Add("Revenue", typeof(decimal));

    table.Rows.Add("Widget A", 120, 3450.75m);
    table.Rows.Add("Widget B", 85, 2190.00m);
    table.Rows.Add("Widget C", 60, 1580.40m);

    return table;
}
```

> **Por qué es importante:** Usar un `DataTable` te brinda una fuente tabular, consciente del esquema, que se mapea limpiamente a filas y columnas de Excel. Además, te permite reutilizar la misma lógica de exportación para cualquier conjunto de datos sin reescribir código.

---

## Paso 2: Crear un nuevo Workbook y obtener la primera hoja

Ahora iniciamos un libro de Excel. La clase `Workbook` representa todo el archivo; su `Worksheets[0]` es la hoja predeterminada donde depositaremos nuestros datos.

```csharp
// Initialize a fresh workbook
Workbook workbook = new Workbook();

// Grab the first (and only) worksheet
Worksheet worksheet = workbook.Worksheets[0];
```

> **Consejo profesional:** Si necesitas varias hojas, simplemente llama a `workbook.Worksheets.Add("SheetName")` y repite los pasos de estilo para cada una.

---

## Paso 3: Definir estilos de columna – Fuente, fondo y formato de número

El estilo en Aspose.Cells se maneja mediante objetos `Style`. Construiremos un arreglo donde cada elemento corresponde a una columna del DataTable.

```csharp
// Prepare an array to hold three distinct styles
Style[] columnStyles = new Style[3];

// 1️⃣ First column – blue, bold font
columnStyles[0] = workbook.CreateStyle();
columnStyles[0].Font.Color = System.Drawing.Color.Blue;
columnStyles[0].Font.IsBold = true;

// 2️⃣ Second column – light‑yellow background
columnStyles[1] = workbook.CreateStyle();
columnStyles[1].ForegroundColor = System.Drawing.Color.LightYellow;
columnStyles[1].Pattern = BackgroundType.Solid;

// 3️⃣ Third column – custom currency format (custom number format excel)
columnStyles[2] = workbook.CreateStyle();
columnStyles[2].Custom = "$#,##0.00";
```

> **¿Por qué un arreglo de estilos?** Pasar un arreglo a `ImportDataTable` te permite aplicar un estilo distinto a cada columna en una sola llamada, lo que es conciso y eficiente. Además garantiza que el formato permanezca sincronizado con el orden de los datos.

---

## Paso 4: Importar el DataTable aplicando los estilos

Aquí está el corazón de la operación: alimentamos el `DataTable` a la hoja, indicamos a Aspose que incluya la fila de encabezado y entregamos nuestro arreglo `columnStyles`.

```csharp
// Import data starting at cell A1 (row 0, column 0)
worksheet.Cells.ImportDataTable(
    GetSampleData(),   // source DataTable
    true,              // include column names as header
    0, 0,              // start row, start column
    columnStyles);     // apply the style array
```

> **¿Qué ocurre bajo el capó?** Aspose recorre cada columna, escribe el encabezado y luego escribe cada valor de fila. Mientras lo hace, aplica el `Style` correspondiente del arreglo, de modo que terminas con un encabezado azul para “Product”, una columna “Quantity” con fondo amarillo y una columna “Revenue” formateada como moneda.

---

## Paso 5: Guardar el Workbook como archivo XLSX

Finalmente, persistimos el libro en disco. El método `Save` elige automáticamente el formato XLSX según la extensión del archivo.

```csharp
// Choose a folder that exists on your machine
string outputPath = @"C:\Temp\DataTableWithStyleArray.xlsx";

// Ensure the directory exists (optional safety check)
System.IO.Directory.CreateDirectory(System.IO.Path.GetDirectoryName(outputPath)!);

// Save the workbook
workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to {outputPath}");
```

> **Consejo:** Si necesitas transmitir el archivo (p. ej., para una API web), usa `workbook.Save(stream, SaveFormat.Xlsx)` en lugar de una ruta de archivo.

---

## Ejemplo completo funcionando

A continuación tienes el programa completo que puedes pegar en un nuevo proyecto de consola. Compila y se ejecuta tal cual, generando un archivo Excel con estilo.

```csharp
using System;
using System.Data;
using Aspose.Cells;

namespace ExcelExportDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1 – Get data
            DataTable dataTable = GetSampleData();

            // Step 2 – Create workbook & worksheet
            Workbook workbook = new Workbook();
            Worksheet worksheet = workbook.Worksheets[0];

            // Step 3 – Prepare column styles
            Style[] columnStyles = new Style[3];

            // Font style for first column (blue, bold)
            columnStyles[0] = workbook.CreateStyle();
            columnStyles[0].Font.Color = System.Drawing.Color.Blue;
            columnStyles[0].Font.IsBold = true;

            // Background style for second column (light yellow)
            columnStyles[1] = workbook.CreateStyle();
            columnStyles[1].ForegroundColor = System.Drawing.Color.LightYellow;
            columnStyles[1].Pattern = BackgroundType.Solid;

            // Currency format for third column (custom number format excel)
            columnStyles[2] = workbook.CreateStyle();
            columnStyles[2].Custom = "$#,##0.00";

            // Step 4 – Import data with styles
            worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);

            // Step 5 – Save as XLSX
            string outputPath = @"C:\Temp\DataTableWithStyleArray.xlsx";
            System.IO.Directory.CreateDirectory(System.IO.Path.GetDirectoryName(outputPath)!);
            workbook.Save(outputPath);

            Console.WriteLine($"Workbook saved to {outputPath}");
        }

        // Helper method to build a demo DataTable
        static DataTable GetSampleData()
        {
            var table = new DataTable("Sales");
            table.Columns.Add("Product", typeof(string));
            table.Columns.Add("Quantity", typeof(int));
            table.Columns.Add("Revenue", typeof(decimal));

            table.Rows.Add("Widget A", 120, 3450.75m);
            table.Rows.Add("Widget B", 85, 2190.00m);
            table.Rows.Add("Widget C", 60, 1580.40m);

            return table;
        }
    }
}
```

### Resultado esperado

Al abrir `DataTableWithStyleArray.xlsx` verás:

| **Producto** (azul, negrita) | **Cantidad** (amarillo claro) | **Ingresos** (moneda) |
|------------------------------|-------------------------------|-----------------------|
| Widget A                     | 120                           | $3,450.75             |
| Widget B                     | 85                            | $2,190.00             |
| Widget C                     | 60                            | $1,580.40             |

El **custom number format excel** que especificaste (`$#,##0.00`) asegura que cada celda de ingresos muestre el signo de dólar, separador de miles y dos decimales, exactamente lo que los equipos financieros esperan.

---

## Preguntas frecuentes y casos límite

### ¿Puedo usar esto con otra biblioteca de Excel?

Absolutamente. El concepto—crear un estilo por columna y aplicarlo durante la importación—se traduce a EPPlus, ClosedXML o NPOI. Las llamadas a la API difieren, pero el patrón se mantiene.

### ¿Qué pasa si mi DataTable tiene más columnas que estilos?

Aspose aplicará el estilo predeterminado a cualquier columna que no tenga una entrada correspondiente en el arreglo `columnStyles`. Para evitar sorpresas, dimensiona el arreglo a `dataTable.Columns.Count` o genera estilos dinámicamente en un bucle.

### ¿Cómo establezco un formato de número personalizado para fechas?

Simplemente asigna `style.Custom = "dd‑mm‑yyyy"` (o cualquier cadena de formato válida de Excel). El mismo enfoque basado en arreglos funciona para fechas, porcentajes o notación científica.

### ¿Hay forma de auto‑ajustar el ancho de columnas después de la importación?

Sí—llama a `worksheet.AutoFitColumns();` después de la importación. Ejecuta un cálculo rápido del ancho basado en el contenido de las celdas.

### ¿Qué pasa con conjuntos de datos muy grandes (¡100 k+ filas!)?

`ImportDataTable` está optimizado para operaciones masivas, pero podrías alcanzar límites de memoria. En ese caso, considera transmitir filas manualmente con `Cells[i, j].PutValue(...)` y reutilizar un solo objeto `Style` para reducir la sobrecarga.

---

## Consejos profesionales y errores comunes

- **Evita codificar rutas** de forma rígida en código de producción; usa `Environment.GetFolderPath` o configuraciones.  
- **Descarta el workbook** si estás en un servicio de larga duración—envuélvelo en un bloque `using` para liberar recursos nativos.  
- **Cuidado con los separadores específicos de cultura**. El formato personalizado `$#,##0.00` fuerza un punto como separador decimal sin importar la configuración regional del SO, lo cual suele ser lo que deseas para informes financieros.  
- **Recuerda referenciar System.Drawing** (o `System.Drawing.Common` en .NET Core) para las estructuras de color usadas en el estilo.  
- **Prueba la salida en diferentes versiones de Excel**; versiones antiguas pueden interpretar algunos formatos personalizados de forma ligeramente distinta.

---

## Conclusión

Hemos cubierto todo lo que necesitas para **custom number format excel** archivos desde C#: obtener datos de un `DataTable`, **import datatable to excel**, aplicar un **set column background color**, usar **format column as currency**, y finalmente **save workbook as x

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}