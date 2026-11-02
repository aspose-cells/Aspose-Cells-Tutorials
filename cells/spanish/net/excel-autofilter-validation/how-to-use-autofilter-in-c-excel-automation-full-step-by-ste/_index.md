---
category: general
date: 2026-05-30
description: Cómo usar AutoFilter en la automatización de Excel con C#. Aprende a
  crear un libro de Excel, filtrar filas por valor y optimizar tus tareas de hoja
  de cálculo.
draft: false
keywords:
- how to use autofilter
- create excel workbook
- filter rows by value
- filter column b
- excel automation c#
language: es
og_description: Cómo usar AutoFilter en la automatización de Excel con C#. Domina
  la creación de libros de Excel, el filtrado de filas por valor y la automatización
  de hojas de cálculo con facilidad.
og_title: Cómo usar AutoFilter en la automatización de Excel con C# – Guía completa
schemas:
- author: Aspose
  dateModified: '2026-05-30'
  description: How to use AutoFilter in C# Excel automation. Learn how to create Excel
    workbook, filter rows by value, and streamline your spreadsheet tasks.
  headline: How to Use AutoFilter in C# Excel Automation – Full Step‑by‑Step Guide
  type: TechArticle
- description: How to use AutoFilter in C# Excel automation. Learn how to create Excel
    workbook, filter rows by value, and streamline your spreadsheet tasks.
  name: How to Use AutoFilter in C# Excel Automation – Full Step‑by‑Step Guide
  steps:
  - name: '**Creating the workbook** – `new Workbook()` gives you a clean file; `Worksheets[0]`
      grabs the default sheet.'
    text: '**Creating the workbook** – `new Workbook()` gives you a clean file; `Worksheets[0]`
      grabs the default sheet.'
  - name: '**Filling sample data** – We write a tiny dataset so you can see the filter
      in action.'
    text: '**Filling sample data** – We write a tiny dataset so you can see the filter
      in action.'
  - name: '**Adding a table** – `ListObjects.Add` converts the range into an Excel
      table, which automatically supports filtering and styling.'
    text: '**Adding a table** – `ListObjects.Add` converts the range into an Excel
      table, which automatically supports filtering and styling.'
  - name: '**Applying AutoFilter** – `table.AutoFilter.Filter(1, "Apple")` tells the
      engine: “Show only rows where the second column (B) equals *Apple*.”'
    text: '**Applying AutoFilter** – `table.AutoFilter.Filter(1, "Apple")` tells the
      engine: “Show only rows where the second column (B) equals *Apple*.”'
  - name: '**Saving files** – Two files are written: one filtered, one with the filter
      removed, proving that `RemoveAutoFilter()` works as expected.'
    text: '**Saving files** – Two files are written: one filtered, one with the filter
      removed, proving that `RemoveAutoFilter()` works as expected.'
  type: HowTo
- questions:
  - answer: Yes. Aspose.Cells can save to both `.xlsx` and `.xls` by changing the
      file extension or using `SaveOptions`.
    question: Does this work with older .xls files?
  - answer: Load the file with `new Workbook("path.xlsx")`, apply the filter, then
      `Save` again.
    question: What if I need to filter *after* the workbook is already saved?
  - answer: 'Absolutely. Use `worksheet.AutoFilter.Range = "A1:C5";` and then `worksheet.AutoFilter.ApplyFilter();`.
      However, tables give you built‑in styling and easier column referencing. ---
      ## Image – Visual Confirmation ![Screenshot showing AutoFilter applied to column
      B in an Excel workbook created with C#'
    question: Can I apply a filter to a *range* that isn’t a table?
  type: FAQPage
tags:
- C#
- Excel
- Automation
title: Cómo usar AutoFilter en la automatización de Excel con C# – Guía completa paso
  a paso
url: /es/net/excel-autofilter-validation/how-to-use-autofilter-in-c-excel-automation-full-step-by-ste/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo usar AutoFilter en la automatización de Excel con C# – Guía completa

¿Alguna vez te has preguntado **cómo usar AutoFilter** cuando generas archivos Excel desde código C#? No estás solo—muchos desarrolladores se encuentran con ese problema cuando necesitan ocultar filas que no coinciden con un criterio determinado.  

En este tutorial recorreremos un ejemplo concreto y ejecutable que **crea un libro de Excel**, agrega una tabla y luego **filtra filas por valor** en la columna B. Al final tendrás un fragmento limpio y reutilizable que puedes insertar en cualquier proyecto C# que necesite automatización de Excel.

## Lo que aprenderás

- Configurar un proyecto C# con la biblioteca Aspose.Cells (o Microsoft.Office.Interop).  
- **Crear un libro de Excel** programáticamente y agregar una tabla con estilo.  
- Aplicar **AutoFilter** para mostrar solo las filas donde **la columna B** sea igual a una cadena específica.  
- Eliminar el filtro por completo, restaurando el conjunto de datos completo.  
- Consejos para manejar casos límite como columnas faltantes o múltiples criterios de filtro.

No se requiere experiencia previa en Excel‑VBA; solo una comprensión básica de C# y paquetes NuGet.

---

## Prerequisites

| Requisito | Por qué es importante |
|-----------|-----------------------|
| .NET 6.0 o posterior (o .NET Framework 4.7+) | Los entornos modernos ofrecen mejor rendimiento y una gestión de paquetes más sencilla. |
| Aspose.Cells para .NET (o Microsoft.Office.Interop.Excel) instalado vía NuGet | Esta biblioteca nos proporciona los objetos `Workbook`, `Worksheet` y `Table` usados en el código. |
| Un editor de código (Visual Studio, VS Code, Rider, etc.) | Necesitarás compilar y ejecutar el ejemplo. |
| Conocimientos básicos de C# | El tutorial explica *por qué* existe cada línea, no solo *qué* hace. |

Puedes instalar Aspose.Cells con:

```bash
dotnet add package Aspose.Cells
```

---

## Cómo usar AutoFilter con Aspose.Cells en C#

A continuación se muestra el programa completo y autónomo. Guárdalo como `Program.cs` en un proyecto de consola y ejecútalo – obtendrás `FilteredWorkbook.xlsx` en la carpeta de salida.

```csharp
using System;
using Aspose.Cells;

namespace ExcelAutoFilterDemo
{
    class Program
    {
        static void Main()
        {
            // -------------------------------------------------
            // Step 1: Create an Excel workbook and grab the first worksheet
            // -------------------------------------------------
            Workbook workbook = new Workbook();               // creates a new, empty workbook
            Worksheet sheet = workbook.Worksheets[0];         // the default sheet is named "Sheet1"

            // Populate the sheet with sample data (A‑C columns, 5 rows)
            sheet.Cells["A1"].PutValue("ID");
            sheet.Cells["B1"].PutValue("Fruit");
            sheet.Cells["C1"].PutValue("Quantity");

            sheet.Cells["A2"].PutValue(1);
            sheet.Cells["B2"].PutValue("Apple");
            sheet.Cells["C2"].PutValue(10);

            sheet.Cells["A3"].PutValue(2);
            sheet.Cells["B3"].PutValue("Banana");
            sheet.Cells["C3"].PutValue(15);

            sheet.Cells["A4"].PutValue(3);
            sheet.Cells["B4"].PutValue("Apple");
            sheet.Cells["C4"].PutValue(7);

            sheet.Cells["A5"].PutValue(4);
            sheet.Cells["B5"].PutValue("Cherry");
            sheet.Cells["C5"].PutValue(20);

            // -------------------------------------------------
            // Step 2: Convert the range into a ListObject (Excel table)
            // -------------------------------------------------
            // Parameters: firstRow, firstColumn, totalRows, totalColumns, hasHeaders
            int tableIdx = sheet.ListObjects.Add(0, 0, 5, 3, true);
            ListObject table = sheet.ListObjects[tableIdx];
            table.TableStyleType = TableStyleType.TableStyleMedium2; // nice built‑in styling

            // -------------------------------------------------
            // Step 3: Apply an AutoFilter to show only rows where column B = "Apple"
            // -------------------------------------------------
            // The AutoFilter is attached to the table’s range automatically.
            // We target column B (index 1) and set the criteria.
            table.AutoFilter.Filter(1, "Apple"); // 1 = zero‑based column index for B

            // -------------------------------------------------
            // Step 4: Save the filtered workbook to disk
            // -------------------------------------------------
            workbook.Save("FilteredWorkbook.xlsx");

            // -------------------------------------------------
            // Step 5: (Optional) Remove the AutoFilter completely
            // -------------------------------------------------
            // This demonstrates that you can revert to the full dataset without re‑loading.
            table.RemoveAutoFilter();   // clears the filter
            workbook.Save("UnfilteredWorkbook.xlsx");

            Console.WriteLine("Workbook created and filtered successfully.");
        }
    }
}
```

### Cómo funciona el código

1. **Crear el libro** – `new Workbook()` te da un archivo limpio; `Worksheets[0]` obtiene la hoja predeterminada.  
2. **Rellenar datos de muestra** – Escribimos un pequeño conjunto de datos para que puedas ver el filtro en acción.  
3. **Agregar una tabla** – `ListObjects.Add` convierte el rango en una tabla de Excel, que soporta filtrado y estilo automáticamente.  
4. **Aplicar AutoFilter** – `table.AutoFilter.Filter(1, "Apple")` indica al motor: “Mostrar solo filas donde la segunda columna (B) sea *Apple*.”  
5. **Guardar archivos** – Se escriben dos archivos: uno filtrado, otro con el filtro eliminado, demostrando que `RemoveAutoFilter()` funciona como se espera.

> **Consejo profesional:** Si necesitas filtrar por múltiples criterios (p. ej., “Apple” *o* “Banana”), usa la sobrecarga `Filter(int columnIndex, string criteria1, string criteria2)` o pasa un arreglo de strings.

---

## Filtrar filas por valor – Variaciones comunes

Si bien el ejemplo anterior se centra en **filtrar la columna B**, puede que quieras filtrar otras columnas o usar criterios numéricos. Aquí tienes una hoja de referencia rápida:

| Filtro deseado | Fragmento de código |
|----------------|----------------------|
| Coincidencia de texto en la columna C | `table.AutoFilter.Filter(2, "Cherry");` |
| Números mayores que 10 en la columna C | `table.AutoFilter.CustomFilter(2, "10", OperatorType.GreaterThan);` |
| Múltiples valores en la columna B | `table.AutoFilter.Filter(1, new[] { "Apple", "Banana" });` |

**Caso límite:** Si el encabezado de la columna está mal escrito o el índice de columna está fuera de rango, Aspose.Cells lanza una `ArgumentException`. Protege contra esto verificando `table.ListColumns.Count` antes de aplicar el filtro.

---

## Eliminar AutoFilter – Cuándo restablecer

A veces necesitas presentar de nuevo el conjunto de datos completo (p. ej., después de que un usuario borra un cuadro de búsqueda). Llamar a `table.RemoveAutoFilter()` lo logra en una sola línea. Si estás usando Microsoft.Office.Interop, deberías llamar a `worksheet.AutoFilterMode = false;`.

---

## Recapitulación del ejemplo completo

A continuación está el programa *completo* nuevamente, sin comentarios para quienes prefieren una vista concisa:

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        Workbook wb = new Workbook();
        Worksheet ws = wb.Worksheets[0];

        ws.Cells["A1"].PutValue("ID");
        ws.Cells["B1"].PutValue("Fruit");
        ws.Cells["C1"].PutValue("Quantity");

        ws.Cells["A2"].PutValue(1); ws.Cells["B2"].PutValue("Apple");  ws.Cells["C2"].PutValue(10);
        ws.Cells["A3"].PutValue(2); ws.Cells["B3"].PutValue("Banana"); ws.Cells["C3"].PutValue(15);
        ws.Cells["A4"].PutValue(3); ws.Cells["B4"].PutValue("Apple");  ws.Cells["C4"].PutValue(7);
        ws.Cells["A5"].PutValue(4); ws.Cells["B5"].PutValue("Cherry"); ws.Cells["C5"].PutValue(20);

        int idx = ws.ListObjects.Add(0, 0, 5, 3, true);
        ListObject tbl = ws.ListObjects[idx];
        tbl.TableStyleType = TableStyleType.TableStyleMedium2;

        tbl.AutoFilter.Filter(1, "Apple");
        wb.Save("FilteredWorkbook.xlsx");

        tbl.RemoveAutoFilter();
        wb.Save("UnfilteredWorkbook.xlsx");
    }
}
```

Ejecutar esto genera dos archivos:

- **FilteredWorkbook.xlsx** – solo filas con *Apple* visibles.  
- **UnfilteredWorkbook.xlsx** – los datos originales restaurados.

---

## Preguntas frecuentes

**P: ¿Esto funciona con archivos .xls antiguos?**  
R: Sí. Aspose.Cells puede guardar tanto en `.xlsx` como en `.xls` cambiando la extensión del archivo o usando `SaveOptions`.

**P: ¿Qué pasa si necesito filtrar *después* de que el libro ya está guardado?**  
R: Carga el archivo con `new Workbook("path.xlsx")`, aplica el filtro y luego `Save` nuevamente.

**P: ¿Puedo aplicar un filtro a un *rango* que no sea una tabla?**  
R: Por supuesto. Usa `worksheet.AutoFilter.Range = "A1:C5";` y luego `worksheet.AutoFilter.ApplyFilter();`. Sin embargo, las tablas proporcionan estilo incorporado y una referencia de columnas más sencilla.

---

## Imagen – Confirmación visual

![Captura de pantalla que muestra AutoFilter aplicado a la columna B en un libro de Excel creado con C#](/images/autofilter-column-b.png "AutoFilter en la columna B")

*(La imagen ilustra la vista filtrada donde solo permanecen las filas que contienen “Apple”.)*

---

## Conclusión

Acabamos de cubrir **cómo usar AutoFilter** en un escenario de automatización de Excel impulsado por C#, desde **crear un libro de Excel** hasta **filtrar filas por valor** en **la columna B**, y finalmente **eliminar el filtro** cuando ya no se necesita. Los pasos clave—inicializar, agregar una tabla, aplicar el filtro y limpiar—son reutilizables en cualquier proyecto que necesite **excel automation c#**.

¿Listo para el siguiente desafío? Prueba:

- Agregar formato condicional para resaltar filas filtradas.  
- Exportar los datos filtrados a un CSV para procesamiento posterior.  
- Combinar múltiples filtros (p. ej., “Apple” *y* cantidad > 8).

Experimenta, rompe cosas y luego arréglalas—

## ¿Qué deberías aprender a continuación?

- [Cómo implementar AutoFilter en Excel usando Aspose.Cells para .NET (Guía de análisis de datos)](/cells/english/net/data-analysis/implement-autofilter-excel-aspose-cells-dotnet/)
- [Cómo usar Autofilter No contiene en Aspose.Cells .NET para análisis de datos de Excel](/cells/english/net/data-analysis/master-autofilter-not-contains-aspose-cells-net/)
- [Cómo implementar Excel Autofilter 'EndsWith' usando Aspose.Cells para .NET](/cells/english/net/data-analysis/implement-autofilter-endswith-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}