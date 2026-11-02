---
category: general
date: 2026-07-13
description: Crea un libro de Excel en C# y aprende cómo agregar un rango con nombre,
  asignar un nombre a una tabla y manejar conflictos de nombres, todo en un ejemplo
  claro.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook
- add named range
- assign name to table
- set table name
- how to add range
language: es
lastmod: 2026-07-13
og_description: Crear libro de Excel en C# con Aspose.Cells. Aprende cómo agregar
  un rango con nombre, establecer el nombre de la tabla y resolver conflictos de nombres
  en una guía concisa y ejecutable.
og_image_alt: Screenshot showing an Excel workbook with a named range and a table
  name set using C# code
og_title: Crear libro de Excel en C# – Añadir rango con nombre y establecer nombre
  de tabla
schemas:
- author: Aspose
  dateModified: '2026-07-13'
  description: Create Excel Workbook in C# and learn how to add named range, assign
    name to table, and handle naming conflicts—all in one clear example.
  headline: Create Excel Workbook in C# – Add Named Range & Set Table Name
  type: TechArticle
- description: Create Excel Workbook in C# and learn how to add named range, assign
    name to table, and handle naming conflicts—all in one clear example.
  name: Create Excel Workbook in C# – Add Named Range & Set Table Name
  steps:
  - name: '**Use a consistent prefix** (`tbl_`, `rng_`, etc.) – it instantly tells
      you what the object is.'
    text: '**Use a consistent prefix** (`tbl_`, `rng_`, etc.) – it instantly tells
      you what the object is.'
  - name: '**Stay within 255 characters** – Excel’s limit for names.'
    text: '**Stay within 255 characters** – Excel’s limit for names.'
  - name: '**Avoid spaces and special characters** – only letters, numbers, and underscores
      are safe.'
    text: '**Avoid spaces and special characters** – only letters, numbers, and underscores
      are safe.'
  - name: '**Validate before assigning** – a quick `if (!sheet.Names.Contains(name))`
      check prevents the clash we demonstrated.'
    text: '**Validate before assigning** – a quick `if (!sheet.Names.Contains(name))`
      check prevents the clash we demonstrated.'
  type: HowTo
- questions:
  - answer: Yes, but you must qualify the address with the sheet name, e.g., `"Sheet1!A1:B5"`.
      The `Names.Add` method accepts that format.
    question: Can I add a named range that spans multiple worksheets?
  - answer: Absolutely. You can pass a formula string instead of a static address,
      such as `"=OFFSET(Sheet1!$A$1,0,0,COUNT(Sheet1!$A:$A),2)"`.
    question: Does Aspose.Cells support dynamic named ranges (like OFFSET formulas)?
  - answer: 'Just set `table.Name = " ## What Should You Learn Next?


      The following tutorials cover closely related topics that build on the techniques
      demonstrated in this guide. Each resource includes complete working code examples
      with step-by-step explanations to help you master additional API features and
      explore alternative implementation approaches in your own projects.

      - [How to Create Workbook Scoped Named Ranges in Excel Using Aspose.Cells .NET](/cells/english/net/range-management/excel-workbook-scoped-named-ranges-aspose-cells-net/)
      - [How to Implement a Named Range with Workbook Scope in Aspose.Cells Java for
      Enhanced Excel Data Management](/cells/english/java/tables-structured-references/implement-named-range-workbook-scope-aspose-cells-java/)
      - [Excel Automation&#58; Create a Workbook and Add a ListBox Using Aspose.Cells
      for .NET](/cells/english/net/automation-batch-processing/excel-automation-create-workbook-add-listbox-aspose-cells/)

      {{< /blocks/products/pf/tutorial-page-section >}} {{< /blocks/products/pf/main-container
      >}} {{< /blocks/products/pf/main-wrap-class >}} {{< blocks/products/products-backtop-button
      >}}'
    question: What if I need to rename an existing table?
  type: FAQPage
tags:
- C#
- Aspose.Cells
- Excel Automation
- .NET
title: Crear libro de Excel en C# – Añadir rango con nombre y establecer nombre de
  tabla
url: /es/net/excel-advanced-named-ranges/create-excel-workbook-in-c-add-named-range-set-table-name/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crear libro de Excel en C# – Guía completa para agregar rangos con nombre y establecer nombres de tabla

¿Alguna vez necesitaste **crear un libro de Excel** desde cero y te preguntaste dónde colocar un rango con nombre o cómo darle a una tabla su propio identificador? No eres el único. En muchos escenarios de informes o exportación de datos, te encontrarás manejando rangos, tablas y el ocasional conflicto de nombres.  

En este tutorial recorreremos un ejemplo completamente ejecutable que **crea un libro de Excel**, **agrega un rango con nombre**, y luego **asigna un nombre a una tabla**—mostrándote exactamente qué hacer cuando los nombres chocan. Al final conocerás el “cómo” y el “por qué” detrás de cada paso, además de algunos consejos para mantener tu código limpio.

> **Ventaja rápida:** El código usa la biblioteca **Aspose.Cells**, que funciona con .NET 6+ y no requiere instalación de Excel en el servidor.

---

## Lo que necesitarás

- **.NET 6 SDK** (o cualquier versión reciente de .NET)  
- **Aspose.Cells for .NET** paquete NuGet  
- Un IDE decente (Visual Studio, Rider o VS Code)  
- Conocimientos básicos de C#—nada elegante, solo las habituales sentencias `using`

Si tienes eso, podemos pasar directamente al proceso de **crear libro de Excel**.

---

## ## Crear libro de Excel – Visión general paso a paso

A continuación tienes el programa completo, listo para copiar y pegar. Demuestra todo, desde la creación del libro hasta el manejo de un conflicto de nombres cuando intentas **asignar nombre a tabla**.

```csharp
using System;
using Aspose.Cells;

namespace ExcelNamingDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Create a new workbook
            Workbook workbook = new Workbook();

            // Step 2: Add some sample data so we have a table to work with
            Worksheet sheet = workbook.Worksheets[0];
            sheet.Cells["A1"].PutValue("Product");
            sheet.Cells["B1"].PutValue("Price");
            sheet.Cells["A2"].PutValue("Apple");
            sheet.Cells["B2"].PutValue(0.99);
            sheet.Cells["A3"].PutValue("Banana");
            sheet.Cells["B3"].PutValue(0.59);
            sheet.Cells["A4"].PutValue("Cherry");
            sheet.Cells["B4"].PutValue(2.99);
            sheet.Cells["A5"].PutValue("Date");
            sheet.Cells["B5"].PutValue(3.49);

            // Step 3: Convert the data range into a table (default name Table1)
            int tableIndex = sheet.Tables.Add(sheet.Cells.CreateRange("A1:B5"), true);
            ListObject table = sheet.Tables[tableIndex];
            // At this point the table name is "Table1"

            // Step 4: Add a named range that covers the same cells
            // This is the "add named range" part of the tutorial
            sheet.Names.Add("MyRange", "A1:B5");

            // Step 5: Try to give the table the same name – this will cause a conflict
            try
            {
                table.Name = "MyRange"; // <-- assign name to table
            }
            catch (Exception ex)
            {
                // Step 6: Handle the naming conflict by outputting the error message
                Console.WriteLine("Naming conflict detected:");
                Console.WriteLine(ex.Message);
            }

            // Optional: Save the workbook to verify everything works
            workbook.Save("DemoWorkbook.xlsx");
        }
    }
}
```

**Salida esperada** al ejecutar el programa:

```
Naming conflict detected:
A name with the same text already exists.
```

Y si abres *DemoWorkbook.xlsx* verás una tabla llamada **Table1** y un rango con nombre llamado **MyRange**—exactamente lo que pretendíamos, sin el choque.

---

## ## Add Named Range – Why It Matters

Un **named range** es esencialmente un alias para un bloque de celdas. En lugar de referirte constantemente a `A1:B5`, puedes escribir `MyRange` en fórmulas, validaciones de datos o incluso en código. Esto mejora la legibilidad y reduce la probabilidad de errores por tipado.

En el fragmento anterior llamamos:

```csharp
sheet.Names.Add("MyRange", "A1:B5");
```

- El primer argumento es el **nombre** que usarás más adelante.  
- El segundo argumento es la **dirección** (relativa a la hoja).  

Si alguna vez necesitas **how to add range** dinámicamente, puedes construir la cadena de dirección con `Cell.GetRefersTo()` o usar `Range refRange = sheet.Cells.CreateRange(startRow, startCol, totalRows, totalCols)`.

---

## ## Assign Name to Table – Handling Conflicts

Las tablas (también llamadas *list objects*) ya poseen una propiedad de nombre incorporada. Por defecto Aspose.Cells las nombra `Table1`, `Table2`, etc. Cuando intentas dar a una tabla el mismo identificador que a un rango con nombre existente, la biblioteca lanza una excepción—exactamente como lo hace Excel.

¿Por qué ocurre esto?

- El alcance de nombres de Excel es **a nivel de libro** tanto para rangos como para tablas.  
- Los nombres duplicados harían que las fórmulas fueran ambiguas, por lo que el motor lo bloquea.

### Pro tip

Si realmente necesitas que una tabla comparta un nombre lógico con un rango, considera **añadir un prefijo** a uno de ellos, por ejemplo:

```csharp
table.Name = "tbl_MyRange";   // safe, no conflict
```

O renombra el rango primero:

```csharp
sheet.Names["MyRange"].Name = "DataRange";
```

Ambas aproximaciones mantienen ordenado el espacio de nombres y evitan errores en tiempo de ejecución.

---

## ## Set Table Name – Best Practices

Cuando **set table name** programáticamente, ten en cuenta estas directrices:

1. **Usa un prefijo consistente** (`tbl_`, `rng_`, etc.) – indica instantáneamente qué objeto es.  
2. **Mantente dentro de 255 caracteres** – límite de Excel para nombres.  
3. **Evita espacios y caracteres especiales** – solo letras, números y guiones bajos son seguros.  
4. **Valida antes de asignar** – una rápida comprobación `if (!sheet.Names.Contains(name))` evita el conflicto que demostramos.  

Aquí tienes un método auxiliar que puedes incorporar a cualquier proyecto:

```csharp
static void SafeSetTableName(Worksheet sheet, ListObject table, string desiredName)
{
    string finalName = desiredName;
    int suffix = 1;
    while (sheet.Names.Contains(finalName) || sheet.Tables.Contains(finalName))
    {
        finalName = $"{desiredName}_{suffix}";
        suffix++;
    }
    table.Name = finalName;
}
```

Llamar a `SafeSetTableName(sheet, table, "MyRange")` convertirá automáticamente `MyRange` en `MyRange_1` si existe un conflicto, asegurando que la operación de **create excel workbook** nunca se aborta inesperadamente.

---

## ## Full Working Example – Putting It All Together

A continuación tienes una versión compacta que puedes copiar directamente a una aplicación de consola. Incluye la rutina de seguridad y demuestra el flujo de extremo a extremo.

```csharp
using System;
using Aspose.Cells;

namespace ExcelNamingDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create the workbook
            Workbook wb = new Workbook();
            Worksheet ws = wb.Worksheets[0];

            // Populate a simple dataset
            ws.Cells["A1"].PutValue("Item");
            ws.Cells["B1"].PutValue("Quantity");
            ws.Cells["A2"].PutValue("Pen");
            ws.Cells["B2"].PutValue(10);
            ws.Cells["A3"].PutValue("Notebook");
            ws.Cells["B3"].PutValue(5);

            // Turn data into a table
            int tblIdx = ws.Tables.Add(ws.Cells.CreateRange("A1:B3"), true);
            ListObject tbl = ws.Tables[tblIdx];

            // Add a named range covering the same cells
            ws.Names.Add("MyRange", "A1:B3");

            // Safely assign a name to the table
            SafeSetTableName(ws, tbl, "MyRange");

            // Save to verify
            wb.Save("FinalDemo.xlsx");
            Console.WriteLine($"Table name set to: {tbl.Name}");
        }

        static void SafeSetTableName(Worksheet sheet, ListObject table, string desiredName)
        {
            string candidate = desiredName;
            int i = 1;
            while (sheet.Names.Contains(candidate) || sheet.Tables.Contains(candidate))
            {
                candidate = $"{desiredName}_{i}";
                i++;
            }
            table.Name = candidate;
        }
    }
}
```

Ejecutar este script produce `FinalDemo.xlsx` donde la tabla se llama `MyRange_1` (u otro sufijo único) y el rango permanece `MyRange`. Sin excepción, sin misterio—solo nombres limpios y determinísticos.

---

## ## Frequently Asked Questions (FAQ)

**Q: ¿Puedo agregar un rango con nombre que abarque varias hojas de cálculo?**  
A: Sí, pero debes calificar la dirección con el nombre de la hoja, por ejemplo, `"Sheet1!A1:B5"`. El método `Names.Add` acepta ese formato.

**Q: ¿Aspose.Cells admite rangos con nombre dinámicos (como fórmulas OFFSET)?**  
A: Absolutamente. Puedes pasar una cadena de fórmula en lugar de una dirección estática, como `"=OFFSET(Sheet1!$A$1,0,0,COUNT(Sheet1!$A:$A),2)"`.

**Q: ¿Qué pasa si necesito renombrar una tabla existente?**  
A: Simplemente establece `table.Name = "

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}