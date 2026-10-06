---
category: general
date: 2026-05-23
description: Crear un libro de Excel en C# y aprender a aplicar un formato numérico
  personalizado, establecer el estilo de la celda programáticamente, formatear la
  celda en notación científica y luego guardar el libro en formato xlsx.
draft: false
keywords:
- create excel workbook
- apply custom number format
- format cell scientific notation
- set cell style programmatically
- save workbook to xlsx
language: es
og_description: Crea un libro de Excel en C# rápidamente. Aprende a aplicar formatos
  numéricos personalizados, dar estilo a las celdas programáticamente, formatear notación
  científica y guardar en xlsx.
og_title: Crear libro de Excel en C# – Aplicar formato numérico personalizado
schemas:
- author: Aspose
  dateModified: '2026-05-23'
  description: Create excel workbook in C# and learn how to apply custom number format,
    set cell style programmatically, format cell scientific notation, then save workbook
    to xlsx.
  headline: Create Excel Workbook in C# – Apply Custom Number Format
  type: TechArticle
tags:
- C#
- Excel
- Aspose.Cells
- Automation
title: Crear libro de Excel en C# – Aplicar formato numérico personalizado
url: /es/net/excel-custom-number-date-formatting/create-excel-workbook-in-c-apply-custom-number-format/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crear libro de Excel en C# – Aplicar formato numérico personalizado

Crear un libro de Excel en C# es más fácil de lo que podrías pensar. En esta guía te acompañaremos paso a paso para aplicar un formato numérico personalizado, formatear una celda en notación científica, establecer el estilo de la celda mediante código y, finalmente, guardar el libro en un archivo xlsx.

Si alguna vez te has quedado mirando una hoja de cálculo en blanco y te has preguntado cómo automatizar todo—desde rellenar datos hasta que los números se vean exactamente como necesitas—este tutorial es para ti. Al final tendrás un archivo de Excel totalmente funcional que podrás abrir en cualquier programa de hojas de cálculo, y comprenderás **por qué** cada paso es importante, no solo **cómo** escribir el código.

## Qué necesitarás

- **.NET 6+** (o cualquier versión reciente de .NET Framework que admita la biblioteca)  
- **Aspose.Cells for .NET** (u otra API que exponga las clases `Workbook`, `Cell` y `CellFormat`)  
- Un nivel modesto de experiencia en C# – si puedes escribir un `Console.WriteLine`, estás listo.  

Sin archivos de configuración extra, sin interop COM y, por supuesto, sin necesidad de instalar Excel manualmente.

---

## Crear libro de Excel – Inicializar el objeto Workbook

Lo primero que debemos hacer es crear un libro vacío. Piensa en la clase `Workbook` como el lienzo en blanco donde pintarás filas, columnas y estilos.

```csharp
using Aspose.Cells;   // Make sure the Aspose.Cells namespace is referenced

// Step 1: Create a new workbook instance
Workbook workbook = new Workbook();
```

Eso es todo—una sola línea y tienes un nuevo archivo de Excel en memoria. El constructor de `Workbook` crea la colección de hojas de cálculo predeterminada, por lo que puedes comenzar a añadir datos de inmediato.

> **Consejo profesional:** Si necesitas varias hojas, puedes llamar a `workbook.Worksheets.Add()` antes de empezar a rellenar celdas.

![Create excel workbook example](image-placeholder.png "Create excel workbook screenshot")

*Texto alternativo de la imagen: ejemplo de creación de libro de Excel que muestra una hoja en blanco en el IDE.*

## Aplicar formato numérico personalizado a una celda

Ahora que el libro existe, pongamos un número en la celda **A1** y asignémosle un formato personalizado. Los formatos numéricos personalizados te permiten controlar cómo aparecen los números—moneda, porcentajes, fechas o, en nuestro caso, notación científica.

```csharp
// Step 2: Grab the first worksheet and the cell at A1 (row 0, column 0)
Worksheet sheet = workbook.Worksheets[0];
Cell cell = sheet.Cells[0, 0];

// Step 3: Insert a numeric value
cell.PutValue(12345.6789);

// Step 4: Retrieve the current style so we can modify its Number format
Style style = cell.GetStyle();

// Step 5: Define a custom scientific notation format with two decimal places
style.Custom = "0.00E+00";   // This is the “apply custom number format” part

// Step 6: Push the modified style back onto the cell
cell.SetStyle(style);
```

¿Por qué obtener primero el estilo? Porque el objeto `Cell` almacena un objeto **Style** que contiene fuentes, bordes, alineación y formato numérico, todo en un solo lugar. Al editar la propiedad `Custom` le decimos a Excel: “muestra este valor usando notación científica con dos decimales”.

> **Pregunta frecuente:** *¿Puedo usar un formato incorporado en lugar de uno personalizado?*  
> Sí—establece `style.Number = 10` para un formato científico incorporado, pero la cadena personalizada te brinda control preciso sobre los decimales.

## Establecer estilo de celda mediante código (más allá del formato numérico)

Con frecuencia querrás algo más que solo el formato numérico. Añadamos una fuente en negrita y un fondo gris claro para que la celda destaque.

```csharp
// Optional: Enhance the cell appearance
style.Font.IsBold = true;
style.ForegroundColor = System.Drawing.Color.LightGray;
style.Pattern = BackgroundType.Solid;

// Re‑apply the enriched style
cell.SetStyle(style);
```

Observa que reutilizamos el mismo objeto `style` que ajustamos antes. Esa es la ventaja de **establecer estilo de celda mediante código**: obtienes el estilo una sola vez, modificas las propiedades que necesites y lo vuelves a escribir. No es necesario recrear objetos ni perder el formato numérico que ya configuraste.

## Formatear celda en notación científica (manejo de casos extremos)

Si trabajas con números muy grandes o muy pequeños, la notación científica es una salvación. El formato personalizado que usamos (`0.00E+00`) garantiza dos dígitos después del punto decimal y fuerza un signo más para el exponente. Aquí tienes una rápida comprobación de sentido:

```csharp
// Verify the format by inserting another extreme value
Cell extraCell = sheet.Cells[1, 0]; // B2
extraCell.PutValue(0.00001234);
extraCell.SetStyle(style); // Reuse the same style with scientific notation
```

Al abrir el archivo resultante, B2 aparecerá como `1.23E-05`, confirmando que la directiva **format cell scientific notation** funciona tanto para números grandes como diminutos.

## Guardar el libro en XLSX

Toda la diversión termina cuando realmente escribes el archivo en disco. El método `Save` se encarga del trabajo pesado, convirtiendo la representación en memoria en un paquete `.xlsx` adecuado.

```csharp
// Step 7: Persist the workbook
string outputPath = @"C:\Temp\CustomFormatted.xlsx";
workbook.Save(outputPath, SaveFormat.Xlsx);
```

Esa línea cumple el objetivo de **save workbook to xlsx**. Si el directorio no existe, `Save` lanzará una excepción—asegúrate de crear la carpeta antes o envuelve la llamada en un bloque try/catch.

```csharp
try
{
    workbook.Save(outputPath, SaveFormat.Xlsx);
    Console.WriteLine($"Workbook saved successfully to {outputPath}");
}
catch (Exception ex)
{
    Console.Error.WriteLine($"Failed to save workbook: {ex.Message}");
}
```

Ahora tienes un archivo de Excel listo para compartir, con un número científico bien formateado, estilo en negrita y un fondo gris claro.

## Ejemplo completo y funcional

A continuación tienes el programa completo, listo para copiar y pegar, que une todas las piezas. Compila como una aplicación de consola, pero puedes integrar la lógica en cualquier proyecto C#.

```csharp
using System;
using Aspose.Cells;
using System.Drawing;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new workbook
        Workbook workbook = new Workbook();

        // 2️⃣ Access the first worksheet and target cell A1
        Worksheet sheet = workbook.Worksheets[0];
        Cell cell = sheet.Cells[0, 0];

        // 3️⃣ Insert a numeric value
        cell.PutValue(12345.6789);

        // 4️⃣ Retrieve and customize the cell style
        Style style = cell.GetStyle();
        style.Custom = "0.00E+00";               // apply custom number format (scientific)
        style.Font.IsBold = true;               // set cell style programmatically
        style.ForegroundColor = Color.LightGray;
        style.Pattern = BackgroundType.Solid;

        // 5️⃣ Apply the style back to the cell
        cell.SetStyle(style);

        // 6️⃣ Add another example to prove scientific notation works for tiny numbers
        Cell tinyCell = sheet.Cells[1, 0]; // B2
        tinyCell.PutValue(0.00001234);
        tinyCell.SetStyle(style);

        // 7️⃣ Save the workbook to an XLSX file
        string outputPath = @"C:\Temp\CustomFormatted.xlsx";
        try
        {
            workbook.Save(outputPath, SaveFormat.Xlsx);
            Console.WriteLine($"Workbook saved successfully to {outputPath}");
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Failed to save workbook: {ex.Message}");
        }
    }
}
```

**Resultado esperado:** Abre `CustomFormatted.xlsx` y verás:

| A1               | B2            |
|------------------|---------------|
| 1.23E+04         | 1.23E-05      |

Ambas celdas están en negrita, tienen un relleno gris claro y muestran los números en notación científica con dos decimales.

---

## Conclusión

Acabamos de **crear un libro de Excel** desde cero, **aplicar un formato numérico personalizado**, **formatear la celda en notación científica**, **establecer el estilo de la celda mediante código** y **guardar el libro en xlsx**—todo en unas pocas líneas de C#. El enfoque escala: basta con iterar sobre filas, clonar el objeto `style` y tendrás un informe totalmente estilizado en segundos.

### ¿Qué sigue?

- **Formato dinámico:** Cambia el formato según la magnitud del valor (p. ej., moneda vs. porcentaje).  
- **Múltiples hojas:** Usa `workbook.Worksheets.Add("Summary")` para crear paneles de control.  
- **Estilizado avanzado:** Bordes, formato condicional y validación de datos.

## Tutoriales relacionados

- [How to Create and Save an Excel Workbook as ODS Using Aspose.Cells for .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)
- [Create Save Excel Workbook Aspose Cells Dotnet](/cells/hongkong/net/workbook-operations/create-save-excel-workbook-aspose-cells-dotnet/)
- [Create Save Excel Workbook Pdf Aspnet Aspose Cells](/cells/hongkong/net/workbook-operations/create-save-excel-workbook-pdf-aspnet-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}