---
category: general
date: 2026-07-03
description: Cómo usar SEQUENCE en C# para generar números incrementales en Excel.
  Aprende a crear un libro de Excel con C# y ASP.NET y a crear un archivo Excel con
  unas pocas líneas de código.
draft: false
keywords:
- how to use sequence
- create excel workbook c#
- asp.net create excel file
- generate incremental numbers excel
language: es
og_description: Cómo usar SEQUENCE en C# para generar números incrementales en Excel.
  Guía paso a paso para crear un libro de Excel con C# y ASP.NET y generar un archivo
  Excel.
og_title: Cómo usar SEQUENCE en C# – Crear un libro de Excel
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: How to use SEQUENCE in C# to generate incremental numbers in Excel.
    Learn to create Excel workbook C# and ASP.NET create Excel file with a few lines
    of code.
  headline: How to Use SEQUENCE in C# – Create Excel Workbook
  type: TechArticle
- description: How to use SEQUENCE in C# to generate incremental numbers in Excel.
    Learn to create Excel workbook C# and ASP.NET create Excel file with a few lines
    of code.
  name: How to Use SEQUENCE in C# – Create Excel Workbook
  steps:
  - name: Why Use SEQUENCE Instead of a Loop?
    text: '- **Performance** – Excel does the math on its own engine, which is highly
      optimized. - **Maintainability** – The formula is self‑documenting; anyone opening
      the sheet instantly knows the intent. - **Dynamic resizing** – Change the `rows`
      argument and the spill range expands automatically.'
  - name: Pro Tip
    text: 'If you need the workbook in memory (e.g., to send it over a web API), use
      a `MemoryStream`:'
  - name: What If the Client Uses an Older Excel Version?
    text: 'Dynamic arrays (including `SEQUENCE`) were introduced in Excel 365/2019.
      If you need backward compatibility, fall back to a manual fill:'
  type: HowTo
- questions:
  - answer: No. `SEQUENCE` is a non‑iterative function; a simple `CalculateFormula()`
      call is enough.
    question: Do I need to enable iterative calculation?
  - answer: 'Change the second argument: `=SEQUENCE(1,5,10,2)` spills across B1:F1.'
    question: What if I want a horizontal spill?
  - answer: Absolutely. For example, `=INDEX(A:A, SEQUENCE(5,1,10,2))` can pull rows
      from another column.
    question: Can I combine SEQUENCE with other functions?
  - answer: The file size impact of a formula is negligible. Only when you start populating
      millions of cells manually does size become an issue.
    question: Is the workbook size a concern?
  type: FAQPage
tags:
- C#
- Excel
- Aspose.Cells
- ASP.NET
title: Cómo usar SEQUENCE en C# – Crear libro de Excel
url: /es/net/formulas-functions/how-to-use-sequence-in-c-create-excel-workbook/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo usar SEQUENCE en C# – Crear un libro de Excel

¿Alguna vez te has preguntado **cómo usar SEQUENCE** para generar una lista de números en una hoja de Excel desde C#? No eres el único. Ya sea que estés construyendo un panel de informes, alimentando una cuadrícula de datos, o simplemente necesites una forma rápida de generar IDs, dominar este truco te ahorra tener que lidiar con bucles.

En este tutorial **crearemos un libro de Excel en C#**, insertaremos una fórmula de matriz dinámica `SEQUENCE` en la celda A1, y obtendremos una bonita columna de números incrementales. También veremos cómo servir ese archivo desde un controlador ASP.NET—sí, también se cubre **ASP.NET crear archivo Excel**. Al final podrás **generar números incrementales al estilo Excel** con una sola línea de código.

## Qué necesitarás

- .NET 6+ (el código también funciona en .NET Framework 4.6+)  
- El paquete NuGet **Aspose.Cells for .NET** (o cualquier biblioteca que exponga objetos `Workbook`/`Worksheet`)  
- Un proyecto básico de ASP.NET Core o MVC si quieres probar la parte de descarga web  

Eso es todo. No se requiere COM interop adicional, ni instalación de Office.

---

## Cómo usar SEQUENCE para generar números incrementales

La función de Excel `SEQUENCE(filas, [columnas], [inicio], [paso])` devuelve un rango **spill**. En nuestro caso queremos 5 filas, 1 columna, iniciar en 10, paso 2. La fórmula se ve así:

```excel
=SEQUENCE(5,1,10,2)
```

Cuando Excel la evalúa, las celdas A1:A5 contendrán **10, 12, 14, 16, 18**. Lo hermoso es que no necesitamos escribir bucles en C#—la fórmula hace el trabajo pesado.

A continuación el fragmento completo de C# que crea un libro, inserta la fórmula, fuerza el cálculo y guarda el archivo.

```csharp
using Aspose.Cells;
using System.IO;

// 1️⃣ Create a new workbook
Workbook workbook = new Workbook();

// 2️⃣ Grab the first worksheet (Aspose creates one by default)
Worksheet sheet = workbook.Worksheets[0];

// 3️⃣ Insert the SEQUENCE formula – this will spill a 5‑row column starting at 10, step 2
sheet.Cells["A1"].Formula = "=SEQUENCE(5,1,10,2)";

// 4️⃣ Force calculation so the spilled range is materialized
workbook.CalculateFormula();

// 5️⃣ Save to disk (you can change the path as needed)
workbook.Save("DynamicArray.xlsx");
```

**Salida esperada** – abre *DynamicArray.xlsx* y verás:

| A |
|---|
| 10 |
| 12 |
| 14 |
| 16 |
| 18 |

Esa es toda la historia de **cómo usar SEQUENCE** en C#. Simple, ¿verdad? Pero profundicemos un poco más.

### ¿Por qué usar SEQUENCE en lugar de un bucle?

- **Rendimiento** – Excel realiza los cálculos con su propio motor, altamente optimizado.  
- **Mantenibilidad** – La fórmula se auto‑documenta; cualquiera que abra la hoja entiende al instante la intención.  
- **Redimensionamiento dinámico** – Cambia el argumento `filas` y el rango spill se expande automáticamente.

---

## Crear un libro de Excel en C# – Paso a paso

Si eres nuevo en **create excel workbook c#**, la siguiente lista de verificación te ayuda a evitar errores comunes.

1. **Agregar el paquete Aspose.Cells**  
   ```bash
   dotnet add package Aspose.Cells
   ```
   (También puedes usar ClosedXML o EPPlus, pero la API mostrada coincide con el código anterior.)

2. **Establecer una licencia** (opcional para la versión de prueba).  
   ```csharp
   var license = new Aspose.Cells.License();
   license.SetLicense("Aspose.Total.NET.lic");
   ```

3. **Instanciar `Workbook`** – esto te da un libro nuevo y vacío.

4. **Referenciar la hoja de cálculo** – `workbook.Worksheets[0]` es la hoja predeterminada llamada *Sheet1*.

5. **Aplicar la fórmula SEQUENCE** – como se mostró antes.

6. **Calcular** – `workbook.CalculateFormula()` fuerza el spill; de lo contrario el archivo solo contendría la fórmula.

7. **Guardar** – puedes escribir en disco, en un `MemoryStream`, o directamente en una respuesta HTTP.

### Consejo profesional

Si necesitas el libro en memoria (p. ej., para enviarlo a través de una API web), usa un `MemoryStream`:

```csharp
using var ms = new MemoryStream();
workbook.Save(ms, SaveFormat.Xlsx);
byte[] excelBytes = ms.ToArray(); // ready to return or attach
```

---

## ASP.NET crear archivo Excel – Transmitir al navegador

Ahora que sabemos **create excel workbook c#**, integremoslo en un controlador ASP.NET Core para que los usuarios descarguen el archivo al instante.

```csharp
using Aspose.Cells;
using Microsoft.AspNetCore.Mvc;
using System.IO;

[Route("api/[controller]")]
public class ExcelController : ControllerBase
{
    [HttpGet("download")]
    public IActionResult Download()
    {
        // 1️⃣ Build the workbook (same steps as before)
        var workbook = new Workbook();
        var sheet = workbook.Worksheets[0];
        sheet.Cells["A1"].Formula = "=SEQUENCE(5,1,10,2)";
        workbook.CalculateFormula();

        // 2️⃣ Save to a memory stream
        using var ms = new MemoryStream();
        workbook.Save(ms, SaveFormat.Xlsx);
        ms.Position = 0; // reset stream position

        // 3️⃣ Return the file as a download
        const string fileName = "DynamicArray.xlsx";
        return File(ms, 
                    "application/vnd.openxmlformats-officedocument.spreadsheetml.sheet", 
                    fileName);
    }
}
```

Cuando un usuario accede a `/api/excel/download`, el navegador muestra el cuadro de descarga de *DynamicArray.xlsx*. El archivo ya contiene la columna **números incrementales generados en Excel** gracias a la fórmula `SEQUENCE`.

### ¿Y si el cliente usa una versión anterior de Excel?

Las matrices dinámicas (incluyendo `SEQUENCE`) se introdujeron en Excel 365/2019. Si necesitas compatibilidad hacia atrás, recurre a un relleno manual:

```csharp
// Alternative for older Excel: write numbers directly
for (int i = 0; i < 5; i++)
{
    sheet.Cells[i, 0].PutValue(10 + i * 2); // column 0 = A
}
```

Ese fragmento muestra el enfoque clásico para **generar números incrementales en Excel** sin depender de la nueva función.

---

## Preguntas frecuentes y casos límite

- **¿Necesito habilitar cálculo iterativo?**  
  No. `SEQUENCE` es una función no iterativa; basta con una llamada simple a `CalculateFormula()`.

- **¿Qué pasa si quiero un spill horizontal?**  
  Cambia el segundo argumento: `=SEQUENCE(1,5,10,2)` se extiende de B1 a F1.

- **¿Puedo combinar SEQUENCE con otras funciones?**  
  Por supuesto. Por ejemplo, `=INDEX(A:A, SEQUENCE(5,1,10,2))` puede extraer filas de otra columna.

- **¿El tamaño del libro es un problema?**  
  El impacto en el tamaño del archivo por una fórmula es insignificante. Solo cuando empiezas a rellenar manualmente millones de celdas el tamaño se vuelve relevante.

---

## Conclusión

Hemos recorrido **cómo usar SEQUENCE** en C# para **create excel workbook c#**, servir ese libro mediante **ASP.NET create excel file**, y demostrar una forma limpia de **generar números incrementales en Excel** sin escribir bucles. La clave: deja que el motor de matrices dinámicas de Excel haga el conteo y que tu código .NET se encargue de la orquestación.

Siéntete libre de experimentar—cambia los argumentos `filas`, `inicio` o `paso`, genera spills horizontales, o combina la fórmula con `IF` o `FILTER` para informes más sofisticados. Cuando estés listo, prueba encadenar varias hojas o exportar el libro como CSV para sistemas downstream.

¿Tienes un truco que quieras compartir? Deja un comentario abajo, o envíame un mensaje en GitHub. ¡Feliz codificación!

## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos con explicaciones paso a paso para ayudarte a dominar funciones adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [How to Create and Configure Excel Workbooks with Aspose.Cells .NET: A Step-by-Step Guide](/cells/english/net/getting-started/create-configure-excel-workbook-aspose-cells-net/)
- [How to Create and Save Excel Files with Aspose.Cells for .NET: A Complete Guide](/cells/english/net/workbook-operations/create-save-excel-file-aspose-cells-dotnet/)
- [How to Create and Style Excel Workbooks Using Aspose.Cells for .NET (2023 Guide)](/cells/english/net/formatting/create-style-excel-workbooks-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}