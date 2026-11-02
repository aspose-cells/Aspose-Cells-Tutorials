---
category: general
date: 2026-09-27
description: Aprende cómo eliminar filas de una tabla de Excel en C# con una guía
  paso a paso que también muestra cómo cargar rápidamente un libro de Excel en C#.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- delete rows from Excel table
- load Excel workbook C#
language: es
lastmod: 2026-09-27
og_description: Eliminar filas de una tabla de Excel en C# con un ejemplo claro. Este
  tutorial también cubre cómo cargar un libro de Excel en C# y manejar casos límite
  comunes.
og_image_alt: Screenshot illustrating delete rows from Excel table using C# code
og_title: Eliminar filas de una tabla de Excel en C# – guía completa de código
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Learn how to delete rows from Excel table in C# with a step‑by‑step
    guide that also shows how to load Excel workbook C# quickly.
  headline: How to delete rows from Excel table using C#
  type: TechArticle
- description: Learn how to delete rows from Excel table in C# with a step‑by‑step
    guide that also shows how to load Excel workbook C# quickly.
  name: How to delete rows from Excel table using C#
  steps:
  - name: What if the table has a different name or position?
    text: '* **Named table:** Use `ws.ListObjects["MyTableName"]` instead of the index.
      * **Multiple tables:** Loop through `ws.ListObjects` and pick the one that matches
      a condition (e.g., column header names). * **Dynamic row count:** You can compute
      `rowCount` at runtime by inspecting `ws.ListObjects[0].Dat'
  - name: Edge‑case handling
    text: '| Situation | Recommended code change | |----------------------------------------|--------------------------------------------------------------|
      | Table is empty or has fewer rows | Check `ws.ListObjects[0].DataRange.RowCount`
      before deleting. | | Rows to delete exceed table size | Clamp `rowCount`'
  - name: How do I delete rows from **all** tables in a workbook?
    text: '```csharp foreach (Worksheet sheet in workbook.Worksheets) { foreach (ListObject
      tbl in sheet.ListObjects) { // Example: delete the first data row of each table
      if (tbl.DataRange.RowCount > 1) tbl.DeleteRows(1, 1); } } ```'
  - name: Can I delete rows based on a **cell value**?
    text: 'Yes. Scan the `DataRange` for matching cells, collect their zero‑based
      indices, then delete in descending order:'
  - name: What if I need to **preserve formatting**?
    text: '`DeleteRows` removes the entire row from the table but retains the table’s
      style for remaining rows. If you need to keep specific formatting on a row you’re
      deleting, copy the style to another row before deletion.'
  - name: Does this work with **.xls** (Excel 97‑2003) files?
    text: Yes. Aspose.Cells automatically detects the file format, so the same code
      works with `.xls`. Just change the file extension in the `Workbook` constructor.
  - name: Next steps
    text: '* Explore **ClosedXML** or **EPPlus** if you prefer a fully open‑source
      stack. * Combine row deletion with **data validation** to clean spreadsheets
      before importing into a database. * Automate the process for a folder of workbooks
      using `Directory.GetFiles` and a loop.'
  type: HowTo
tags:
- Excel
- C#
- .NET
title: Cómo eliminar filas de una tabla de Excel usando C#
url: /es/net/row-and-column-management/how-to-delete-rows-from-excel-table-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Eliminar filas de una tabla de Excel en C# – guía completa de programación

Si necesitas **eliminar filas de una tabla de Excel** en un archivo .xlsx, este tutorial te muestra exactamente cómo hacerlo con C#. Verás un ejemplo conciso y ejecutable que carga un libro de Excel, elimina filas específicas de la primera tabla y guarda el resultado. El enfoque funciona con la popular biblioteca Aspose.Cells y puede adaptarse a otras API de Excel para .NET.

Eliminar filas de una tabla es una tarea común al limpiar datos importados, recortar secciones de informes o automatizar actualizaciones de hojas de cálculo. Al final de esta guía podrás **cargar un libro de Excel con C#**, localizar una tabla (ListObject), eliminar las filas que desees y escribir el archivo modificado de nuevo en el disco.

## Requisitos previos

Antes de comenzar, asegúrate de tener:

* .NET 6.0 o posterior instalado (el código también funciona con .NET Framework 4.7+).
* Una referencia al paquete NuGet **Aspose.Cells** (o cualquier biblioteca compatible que exponga los tipos `Workbook`, `Worksheet` y `ListObject`).
* Un archivo de entrada llamado `input.xlsx` colocado en una carpeta que puedas referenciar desde tu proyecto.
* Familiaridad básica con la sintaxis de C# y Visual Studio (o tu IDE preferido).

> **Consejo profesional:** Si prefieres una alternativa de código abierto, la misma lógica se puede aplicar con **ClosedXML** – simplemente reemplaza las clases específicas de Aspose por `XLWorkbook`, `IXLWorksheet` y `IXLTable`.

## Paso 1: Cargar el libro de Excel en C#

La primera operación es leer el archivo fuente en memoria. Cargar el libro es poco costoso para tamaños típicos de hojas de cálculo y te brinda acceso completo a hojas de trabajo, tablas y valores de celdas.

```csharp
using Aspose.Cells;

// Step 1: Load the workbook
// Replace YOUR_DIRECTORY with the actual folder path, e.g. @"C:\Data"
Workbook workbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");
```

*Por qué es importante:* `Workbook` analiza la estructura Open XML del archivo .xlsx, exponiendo una colección de objetos `Worksheet`. Si el archivo no se encuentra, Aspose lanza una `FileNotFoundException`, así que asegúrate de que la ruta sea correcta.

## Paso 2: Acceder a la hoja de trabajo objetivo

La mayoría de las hojas de cálculo contienen varias pestañas; necesitas seleccionar la que contiene la tabla que deseas modificar. Aquí usamos la primera hoja (`Worksheets[0]`), que es un valor predeterminado seguro para archivos simples.

```csharp
// Step 2: Access the first worksheet
Worksheet ws = workbook.Worksheets[0];
```

*Por qué es importante:* `Worksheet` es el contenedor de tablas (`ListObjects`). Acceder a la hoja correcta evita cambios accidentales en datos no relacionados.

## Paso 3: Eliminar filas de una tabla de Excel

Las tablas de Excel se representan mediante objetos `ListObject`. La primera tabla en la hoja es `ListObjects[0]`. El método `DeleteRows(startIndex, rowCount)` elimina filas **relativas al área de datos de la tabla**, no a los números de fila absolutos de la hoja.  

En este ejemplo eliminamos la segunda y tercera fila de la tabla (el encabezado es la fila 0, por lo que comenzamos en el índice 1).

```csharp
// Step 3: Delete rows 1 and 2 from the first table (ListObject)
// The first row (index 0) is the header, so we start at index 1
ws.ListObjects[0].DeleteRows(1, 2);
```

### ¿Qué pasa si la tabla tiene un nombre o posición diferente?

* **Tabla con nombre:** Usa `ws.ListObjects["MyTableName"]` en lugar del índice.  
* **Múltiples tablas:** Recorre `ws.ListObjects` y elige la que coincida con una condición (p. ej., nombres de encabezados de columna).  
* **Recuento de filas dinámico:** Puedes calcular `rowCount` en tiempo de ejecución inspeccionando `ws.ListObjects[0].DataRange.RowCount`.

### Manejo de casos límite

| Situación                              | Cambio de código recomendado                                      |
|----------------------------------------|-------------------------------------------------------------------|
| La tabla está vacía o tiene menos filas      | Check `ws.ListObjects[0].DataRange.RowCount` before deleting. |
| Las filas a eliminar exceden el tamaño de la tabla       | Clamp `rowCount` to `DataRange.RowCount - startIndex`.       |
| Necesitas eliminar filas basadas en una condición (p. ej., valor en la columna C) | Iterate `DataRange.Rows` and collect matching indices, then delete in reverse order to keep indices stable. |

## Paso 4: Guardar el libro modificado

Después de la eliminación, escribe el libro de nuevo en un archivo nuevo (o sobrescribe el original si lo prefieres). Guardar crea un .xlsx nuevo que refleja la tabla actualizada.

```csharp
// Step 4: Save the modified workbook
workbook.Save(@"YOUR_DIRECTORY\output.xlsx");
```

*Por qué es importante:* `Save` serializa la representación en memoria al disco. Si necesitas preservar el archivo original, siempre escribe en una ruta diferente.

## Ejemplo completo y ejecutable

Unir todos los pasos te brinda un programa autónomo que puedes copiar, pegar y ejecutar.

```csharp
using System;
using Aspose.Cells;

class ExcelRowDeletion
{
    static void Main()
    {
        // Adjust the folder path as needed
        const string folder = @"YOUR_DIRECTORY";

        // Load the workbook (load Excel workbook C#)
        Workbook workbook = new Workbook($"{folder}\\input.xlsx");

        // Access the first worksheet
        Worksheet ws = workbook.Worksheets[0];

        // Ensure the worksheet contains at least one table
        if (ws.ListObjects.Count == 0)
        {
            Console.WriteLine("No tables found on the first worksheet.");
            return;
        }

        // Delete rows 1 and 2 from the first table (skip header)
        ListObject table = ws.ListObjects[0];
        int rowsToDelete = Math.Min(2, table.DataRange.RowCount - 1); // guard against short tables
        if (rowsToDelete > 0)
        {
            table.DeleteRows(1, rowsToDelete);
            Console.WriteLine($"Deleted {rowsToDelete} row(s) from table \"{table.Name}\".");
        }
        else
        {
            Console.WriteLine("Table does not have enough rows to delete.");
        }

        // Save the result
        workbook.Save($"{folder}\\output.xlsx");
        Console.WriteLine("Workbook saved as output.xlsx");
    }
}
```

**Salida esperada** (consola):

```
Deleted 2 row(s) from table "Table1".
Workbook saved as output.xlsx
```

Abre `output.xlsx` – la primera tabla ahora carece de las filas que eliminaste, mientras que la fila de encabezado permanece intacta.

## Preguntas frecuentes y variaciones

### ¿Cómo elimino filas de **todas** las tablas en un libro de trabajo?

```csharp
foreach (Worksheet sheet in workbook.Worksheets)
{
    foreach (ListObject tbl in sheet.ListObjects)
    {
        // Example: delete the first data row of each table
        if (tbl.DataRange.RowCount > 1)
            tbl.DeleteRows(1, 1);
    }
}
```

### ¿Puedo eliminar filas basadas en un **valor de celda**?

Sí. Escanea el `DataRange` en busca de celdas coincidentes, recopila sus índices basados en cero y luego elimina en orden descendente:

```csharp
var rowsToRemove = new List<int>();
for (int i = 0; i < table.DataRange.RowCount; i++)
{
    var cell = table.DataRange[i, 2]; // column C (zero‑based)
    if (cell.StringValue == "Obsolete")
        rowsToRemove.Add(i);
}

// Delete rows from bottom to top to keep indices valid
rowsToRemove.Sort((a, b) => b.CompareTo(a));
foreach (int rowIdx in rowsToRemove)
    table.DeleteRows(rowIdx, 1);
```

### ¿Qué pasa si necesito **preservar el formato**?

`DeleteRows` elimina la fila completa de la tabla pero conserva el estilo de la tabla para las filas restantes. Si necesitas mantener un formato específico en una fila que vas a eliminar, copia el estilo a otra fila antes de la eliminación.

### ¿Esto funciona con archivos **.xls** (Excel 97‑2003)?

Sí. Aspose.Cells detecta automáticamente el formato del archivo, por lo que el mismo código funciona con `.xls`. Simplemente cambia la extensión del archivo en el constructor de `Workbook`.

## Consejos de rendimiento

* **Eliminaciones por lotes:** Eliminar muchas filas una por una puede ser más lento. Usa una única llamada `DeleteRows(start, count)` cuando sea posible.  
* **Evita bloquear el hilo de UI:** Si integras esto en una aplicación de escritorio, ejecuta la manipulación del libro en un hilo en segundo plano para mantener la UI responsiva.  
* **Liberar recursos correctamente:** Aunque Aspose.Cells usa memoria gestionada, envuelve el `Workbook` en un bloque `using` si trabajas con archivos grandes para liberar recursos rápidamente.

## Conclusión

Ahora tienes un ejemplo completo y listo para producción que **elimina filas de una tabla de Excel** usando C#. La guía cubrió cómo **cargar un libro de Excel con C#**, localizar el `ListObject` deseado, eliminar filas de forma segura y guardar el archivo actualizado. Con el manejo de casos límite y los consejos de rendimiento incluidos, puedes adaptar este patrón a escenarios más complejos como eliminaciones condicionales, múltiples tablas o bibliotecas alternativas de Excel para .NET.

### Próximos pasos

* Explora **ClosedXML** o **EPPlus** si prefieres una pila completamente de código abierto.  
* Combina la eliminación de filas con **validación de datos** para limpiar hojas de cálculo antes de importarlas a una base de datos.  
* Automatiza el proceso para una carpeta de libros usando `Directory.GetFiles` y un bucle.

¡Siéntete libre de experimentar con diferentes rangos de filas, nombres de tablas y lógica condicional. ¡Feliz codificación!

## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y funcionales con explicaciones paso a paso para ayudarte a dominar funciones adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Cargar archivo Excel C# – Cómo eliminar filas y quitar filas específicas](/cells/english/net/row-and-column-management/load-excel-file-c-how-to-delete-rows-and-remove-specific-row/)
- [Cómo insertar y eliminar filas en Excel con Aspose.Cells para .NET: Guía completa](/cells/english/net/data-manipulation/aspose-cells-net-insert-delete-excel-rows/)
- [Cómo eliminar filas en blanco en Excel usando Aspose.Cells .NET para limpieza de datos](/cells/english/net/data-manipulation/delete-blank-rows-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}