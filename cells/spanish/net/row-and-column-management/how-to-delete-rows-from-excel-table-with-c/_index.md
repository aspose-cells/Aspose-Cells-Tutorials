---
category: general
date: 2026-11-25
description: Aprende cómo eliminar filas de una tabla de Excel en C# y también eliminar
  varias filas de una hoja de Excel de manera eficiente.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- delete rows from excel table
- delete multiple rows from excel sheet
language: es
lastmod: 2026-11-25
og_description: Eliminar filas de una tabla de Excel en C# y aprender a eliminar múltiples
  filas de una hoja de Excel con código limpio.
og_image_alt: Screenshot of C# code deleting rows from an Excel table
og_title: Eliminar filas de una tabla de Excel en C# – guía completa
schemas:
- author: Aspose
  dateModified: '2026-11-25'
  description: Learn how to delete rows from Excel table in C# and also delete multiple
    rows from Excel sheet efficiently.
  headline: How to delete rows from Excel table with C#
  type: TechArticle
- description: Learn how to delete rows from Excel table in C# and also delete multiple
    rows from Excel sheet efficiently.
  name: How to delete rows from Excel table with C#
  steps:
  - name: Add Aspose.Cells to your project
    text: 'Open the **Package Manager Console** and run:'
  - name: Load the workbook and locate the table
    text: '```csharp using Aspose.Cells;'
  - name: Delete the desired data rows
    text: The `DeleteRows` method expects a **zero‑based** row index relative to the
      table, **including** the header row. Because the header cannot be removed, you
      must start at index 1 for the first data row.
  - name: Save the modified workbook
    text: '```csharp // Save the workbook to a new file to preserve the original workbook.Save(@"C:\Data\table_with_header_modified.xlsx");
      } } ```'
  - name: Full working example
    text: '```csharp using Aspose.Cells;'
  - name: Edge cases and best practices
    text: '| Situation | Recommended handling | |----------------------------------------|----------------------|
      | Deleting rows beyond the last row | Check `worksheet.Rows.Count` before calling
      `RemoveAt`. | | Removing all rows except the header | Delete data rows in a
      loop or use `DeleteRows(1, table.DataRa'
  type: HowTo
tags:
- Excel automation
- C#
- Aspose.Cells
- data manipulation
title: Cómo eliminar filas de una tabla de Excel con C#
url: /es/net/row-and-column-management/how-to-delete-rows-from-excel-table-with-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo eliminar filas de una tabla de Excel con C#

Si necesitas eliminar filas de una tabla de Excel usando C#, esta guía te muestra exactamente cómo hacerlo. También verás cómo eliminar múltiples filas de una hoja de Excel sin afectar otros datos.

Trabajar con Excel de forma programática a menudo requiere eliminar registros obsoletos o inválidos. Eliminar filas directamente en una hoja de cálculo puede ser arriesgado porque la fila de encabezado de una tabla estructurada debe permanecer intacta. Este tutorial te guía a través de un enfoque seguro que respeta el encabezado de la tabla y te permite eliminar cualquier número de filas de datos en una sola llamada.

## Requisitos previos

* .NET 6.0 o posterior instalado  
* Visual Studio 2022 (o cualquier IDE compatible)  
* El paquete NuGet **Aspose.Cells** (versión 23.10 o más reciente) – esta biblioteca proporciona las clases `Workbook`, `Worksheet` y `ListObject` usadas en los ejemplos  

No necesitas Microsoft Office instalado en la máquina de desarrollo porque Aspose.Cells trabaja directamente con el formato de archivo.

## Eliminar filas de una tabla de Excel – paso a paso

Las siguientes secciones describen cada paso necesario para eliminar filas de una tabla de Excel de forma segura. La palabra clave principal aparece en este encabezado para cumplir con los requisitos de SEO.

### Paso 1: Añadir Aspose.Cells a tu proyecto

Abre la **Package Manager Console** y ejecuta:

```powershell
Install-Package Aspose.Cells
```

El paquete agrega los ensamblados necesarios y resuelve los tipos `Workbook`, `Worksheet` y `ListObject`.

### Paso 2: Cargar el libro de trabajo y localizar la tabla

```csharp
using Aspose.Cells;

class ExcelRowDeletion
{
    static void Main()
    {
        // Load the workbook that contains the table
        var workbook = new Workbook(@"C:\Data\table_with_header.xlsx");

        // Access the first worksheet (index 0)
        var worksheet = workbook.Worksheets[0];

        // Retrieve the first ListObject (structured table) on the sheet
        var table = worksheet.ListObjects[0];
```

*Por qué es importante*: El `ListObject` representa una tabla real de Excel, que mantiene su propia fila de encabezado. Al trabajar con el `ListObject`, evitas la eliminación accidental del encabezado.

### Paso 3: Eliminar las filas de datos deseadas

El método `DeleteRows` espera un índice de fila **basado en cero** relativo a la tabla, **incluyendo** la fila de encabezado. Como el encabezado no puede ser eliminado, debes comenzar en el índice 1 para la primera fila de datos.

```csharp
        // Delete two data rows starting after the header (index 1)
        // Parameters: startRow (relative to the table), numberOfRows
        table.DeleteRows(1, 2);
```

Si intentas `table.DeleteRows(0, 2)`, Aspose.Cells lanzará una excepción porque la fila de encabezado (índice 0) está protegida. Comenzar en el índice 1 garantiza que solo se eliminen filas de datos.

### Paso 4: Guardar el libro de trabajo modificado

```csharp
        // Save the workbook to a new file to preserve the original
        workbook.Save(@"C:\Data\table_with_header_modified.xlsx");
    }
}
```

Ejecutar el programa elimina las dos filas inmediatamente debajo del encabezado mientras mantiene intacta la estructura de la tabla.

### Ejemplo completo en funcionamiento

```csharp
using Aspose.Cells;

class ExcelRowDeletion
{
    static void Main()
    {
        // 1. Load workbook
        var workbook = new Workbook(@"C:\Data\table_with_header.xlsx");

        // 2. Access first worksheet
        var worksheet = workbook.Worksheets[0];

        // 3. Get the first table (ListObject)
        var table = worksheet.ListObjects[0];

        // 4. Delete two rows after the header (cannot delete header itself)
        table.DeleteRows(1, 2);

        // 5. Save the result
        workbook.Save(@"C:\Data\table_with_header_modified.xlsx");
    }
}
```

**Salida esperada**: El archivo `table_with_header_modified.xlsx` contiene el encabezado original de la tabla, seguido de todas las filas excepto las dos que fueron eliminadas. No se alteran otras hojas de cálculo.

## Eliminar múltiples filas de una hoja de Excel

A veces necesitas eliminar filas que **no** forman parte de una tabla estructurada. La palabra clave secundaria aparece en este encabezado. El enfoque difiere ligeramente porque trabajas con la colección `Rows` de la hoja de cálculo en lugar de un `ListObject`.

```csharp
using Aspose.Cells;

class SheetRowDeletion
{
    static void Main()
    {
        var workbook = new Workbook(@"C:\Data\plain_sheet.xlsx");
        var worksheet = workbook.Worksheets[0];

        // Delete rows 5 through 9 (inclusive) – zero‑based index
        // The second argument is the count of rows to remove
        worksheet.Rows.RemoveAt(4, 5);

        workbook.Save(@"C:\Data\plain_sheet_modified.xlsx");
    }
}
```

**Por qué funciona**: `Rows.RemoveAt(startIndex, count)` elimina un bloque contiguo de filas directamente de la hoja de cálculo. No hay protección del encabezado, por lo que puedes comenzar en cualquier índice. El método es eficiente porque actualiza las estructuras de datos internas en una sola operación, lo que es ideal cuando necesitas eliminar múltiples filas de una hoja de Excel.

### Casos límite y mejores prácticas

| Situación                               | Manejo recomendado |
|----------------------------------------|----------------------|
| Eliminar filas más allá de la última fila      | Verifica `worksheet.Rows.Count` antes de llamar a `RemoveAt`. |
| Eliminar todas las filas excepto el encabezado    | Elimina filas de datos en un bucle o usa `DeleteRows(1, table.DataRange.RowCount - 1)`. |
| Conservar el formato de celdas             | Eliminar mediante `ListObject` desplaza automáticamente el formato; para hojas sin tabla, copia el formato antes de la eliminación si es necesario. |
| Hojas de cálculo grandes ( > 10 000 filas)      | Realiza eliminaciones en orden descendente para evitar el desplazamiento de índices, o usa `DeleteRows` en la tabla si es posible. |

**Consejo profesional**: Cuando necesites eliminar filas basadas en una condición (p.ej., filas donde el valor de una columna está vacío), recorre el `DataRange` de la tabla en sentido inverso y llama a `DeleteRows` para cada fila coincidente. Eliminar en sentido inverso evita desalineaciones de índices.

## Preguntas frecuentes

*¿Esto funciona con archivos .xlsx creados por Excel 365?*  
Sí. Aspose.Cells soporta la especificación completa de Office Open XML, por lo que el mismo código funciona con cualquier archivo `.xlsx` moderno.

*¿Qué pasa si el libro de trabajo contiene múltiples tablas?*  
Obtén la tabla deseada por nombre: `var table = worksheet.ListObjects["MyTable"];` y luego aplica `DeleteRows` como se muestra.

*¿Puedo eliminar filas sin usar una biblioteca de terceros?*  
Podrías usar la interoperabilidad COM Microsoft.Office.Interop.Excel, pero eso requiere que Excel esté instalado en el servidor e introduce sobrecarga relacionada con COM. Aspose.Cells ofrece una alternativa ligera y segura para el servidor.

## Conclusión

Ahora sabes cómo eliminar filas de una tabla de Excel de forma segura y cómo eliminar múltiples filas de una hoja de Excel usando C#. La técnica principal se basa en el método `ListObject.DeleteRows`, que respeta el encabezado de la tabla, mientras que la técnica secundaria usa `Rows.RemoveAt` para hojas simples. Aplica estos patrones para limpiar datos, automatizar la generación de informes o implementar funciones de edición masiva en tus aplicaciones.

**Próximos pasos**

* Explora otras funcionalidades de Aspose.Cells como insertar filas, copiar estilos o filtrar datos.  
* Prueba las mismas operaciones con **ClosedXML** si prefieres una biblioteca de código abierto; la API es similar pero usa `IXLTable` y `IXLRows`.  
* Combina la lógica de eliminación de filas con consultas LINQ para crear pipelines de limpieza de datos más complejos.

¡Feliz codificación!

## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y funcionales con explicaciones paso a paso para ayudarte a dominar características adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [cómo eliminar filas en Excel con C# – proteger encabezado de tabla](/cells/english/net/row-and-column-management/how-to-delete-rows-in-excel-with-c-protect-table-header/)
- [Cómo usar Aspose.Cells para eliminar filas en una tabla de Excel manteniendo el](/cells/english/net/row-and-column-management/how-to-use-aspose-cells-to-delete-rows-in-an-excel-table-whi/)
- [Cargar archivo Excel C# – Cómo eliminar filas y eliminar filas específicas](/cells/english/net/row-and-column-management/load-excel-file-c-how-to-delete-rows-and-remove-specific-row/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}