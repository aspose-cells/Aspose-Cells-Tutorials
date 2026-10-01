---
category: general
date: 2026-02-23
description: Actualizar tabla dinámica de Excel en C# y exportarla como imagen PNG.
  Aprende a cargar un libro de Excel en C#, actualizar la tabla dinámica y guardar
  el resultado.
draft: false
keywords:
- refresh excel pivot table
- load excel workbook c#
- export pivot as image
- export excel pivot image
language: es
og_description: Actualizar tabla dinámica de Excel en C# y exportarla como imagen
  PNG. Guía paso a paso con código completo y consejos prácticos.
og_title: Actualizar tabla dinámica de Excel en C# – Exportar como imagen PNG
tags:
- C#
- Excel
- Aspose.Cells
- Data Automation
title: Actualizar tabla dinámica de Excel en C# – Exportar como imagen PNG
url: /es/net/pivot-tables/refresh-excel-pivot-table-in-c-export-as-png-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Actualizar tabla dinámica de Excel en C# – Exportar como imagen PNG

¿Alguna vez necesitaste **refresh an Excel pivot table** desde una aplicación C# y luego convertirla en una imagen? No eres el único que se ha quedado perplejo. En este tutorial veremos paso a paso cómo **refresh Excel pivot table**, **load Excel workbook C#**, y finalmente **export pivot as image**, todo en un fragmento de código limpio y ejecutable.

Al final obtendrás un archivo PNG que se ve exactamente como la tabla dinámica que verías en Excel, listo para incrustarse en informes, correos electrónicos o paneles. Sin copiar‑pegar manual, sin complicados interop COM, solo código .NET directo.

## Requisitos previos

- .NET 6+ (or .NET Framework 4.7+)
- Aspose.Cells for .NET (prueba gratuita o versión con licencia) – puedes obtenerlo de NuGet con `Install-Package Aspose.Cells`.
- Un `input.xlsx` existente que contenga al menos una tabla dinámica.
- Una carpeta donde tengas permiso de escritura para la imagen de salida.

> **Consejo profesional:** Si estás usando Visual Studio, habilita **nullable reference types** (`<Nullable>enable</Nullable>`) para detectar errores relacionados con null temprano.

---

## Paso 1: Cargar libro de Excel en C#

Lo primero que necesitamos es un objeto `Workbook` que apunte a nuestro archivo fuente. Piensa en esto como abrir el archivo de Excel programáticamente.

```csharp
using System;
using Aspose.Cells;

class PivotExportDemo
{
    static void Main()
    {
        // 👉 Step 1: Load the workbook and obtain the first worksheet
        string inputPath = @"YOUR_DIRECTORY\input.xlsx";
        Workbook wb = new Workbook(inputPath);
        Worksheet worksheet = wb.Worksheets[0];

        // The rest of the steps follow…
```

**Por qué es importante:** Cargar el libro nos da acceso a las hojas de cálculo, celdas y—lo más importante—las tablas dinámicas que has creado. Si el archivo no se encuentra, Aspose lanza una clara `FileNotFoundException`, que puedes capturar para un manejo elegante.

---

## Paso 2: Configurar opciones de exportación de imagen (Export Pivot as Image)

Aspose.Cells te permite definir cómo se debe renderizar la tabla dinámica. Aquí solicitamos un PNG porque es sin pérdida y ampliamente compatible.

```csharp
        // 👉 Step 2: Configure image export options to use PNG format
        ImageOrPrintOptions imgOptions = new ImageOrPrintOptions
        {
            ImageFormat = ImageFormat.Png,
            // Optional: set resolution for sharper output
            HorizontalResolution = 300,
            VerticalResolution = 300
        };
```

**¿Por qué PNG?** A diferencia de JPEG, PNG conserva las líneas de cuadrícula nítidas y el sombreado de texto del que dependen las tablas dinámicas. Si necesitas un archivo más pequeño, podrías cambiar a `ImageFormat.Jpeg` y ajustar la calidad, pero perderás algo de claridad.

---

## Paso 3: Actualizar la tabla dinámica

Antes de capturar la visual, debemos asegurarnos de que la tabla dinámica refleje los datos más recientes. Este es el núcleo de **refresh excel pivot table**.

```csharp
        // 👉 Step 3: Refresh the first pivot table so it reflects the latest data
        PivotTable pivot = worksheet.PivotTables[0];
        pivot.Refresh();
```

**¿Qué ocurre internamente?** `Refresh()` recalcula la tabla dinámica basándose en el rango de origen. Si has añadido filas a los datos de origen después de guardar el libro, esta llamada las incorpora. Omitir este paso produce una imagen obsoleta que no coincide con los datos actuales.

---

## Paso 4: Renderizar la tabla dinámica a PNG (Export Excel Pivot Image)

Ahora que todo está actualizado, podemos renderizar la tabla dinámica directamente a un archivo de imagen.

```csharp
        // 👉 Step 4: Export the refreshed pivot table as a PNG image
        string outputPath = @"YOUR_DIRECTORY\pivot.png";
        pivot.RenderToImage(imgOptions, outputPath);

        Console.WriteLine($"Pivot table exported successfully to: {outputPath}");
    }
}
```

**Resultado:** Abre `pivot.png` y verás una captura pixel‑perfecta de la tabla dinámica actualizada. Este archivo puede adjuntarse a un correo electrónico, incrustarse en una página web o alimentarse a un motor de informes.

### Salida esperada

```
Pivot table exported successfully to: YOUR_DIRECTORY\pivot.png
```

Si navegas a la carpeta, el PNG debería mostrar las mismas filas, columnas y filtros que verías en Excel.

---

## Manejo de casos comunes

| Situación | Qué hacer |
|-----------|------------|
| **Multiple pivot tables** | Loop through `worksheet.PivotTables` and call `Refresh()` / `RenderToImage()` for each. |
| **Dynamic sheet names** | Use `wb.Worksheets[wb.Worksheets.IndexOf("SheetName")]` or search by `worksheet.Name`. |
| **Large datasets** | Increase `imgOptions.OnePagePerSheet = false` and set `imgOptions.PageWidth`/`PageHeight` to control paging. |
| **Missing Aspose.Cells license** | The free trial adds a watermark. Acquire a license and call `License license = new License(); license.SetLicense("Aspose.Total.NET.lic");` before loading the workbook. |
| **File‑path issues** | Use `Path.Combine(Environment.CurrentDirectory, "input.xlsx")` to avoid hard‑coded separators. |

---

## Consejos profesionales y buenas prácticas

- **Dispose properly** – Envuelve el `Workbook` en un bloque `using` o llama a `wb.Dispose()` cuando termines para liberar recursos nativos.
- **Cache rendered images** – Si necesitas la misma imagen de tabla dinámica repetidamente, almacena en caché el PNG en disco y reutilízalo en lugar de volver a renderizar cada vez.
- **Thread safety** – Cada hilo debe trabajar con su propia instancia de `Workbook`; los objetos de Aspose.Cells no son seguros para subprocesos.
- **Performance** – Renderizar tablas dinámicas grandes puede consumir mucha memoria. Ajusta `imgOptions.ImageFormat` a `Bmp` para mayor velocidad pero archivos más grandes, o reduce el DPI para renders más rápidos.

---

## Ejemplo completo funcional (listo para copiar y pegar)

```csharp
using System;
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Rendering;

class PivotExportDemo
{
    static void Main()
    {
        // 👉 Step 1: Load the workbook and obtain the first worksheet
        string inputPath = Path.Combine(Environment.CurrentDirectory, "input.xlsx");
        if (!File.Exists(inputPath))
        {
            Console.Error.WriteLine($"File not found: {inputPath}");
            return;
        }

        Workbook wb = new Workbook(inputPath);
        Worksheet worksheet = wb.Worksheets[0];

        // 👉 Step 2: Configure image export options to use PNG format
        ImageOrPrintOptions imgOptions = new ImageOrPrintOptions
        {
            ImageFormat = ImageFormat.Png,
            HorizontalResolution = 300,
            VerticalResolution = 300
        };

        // 👉 Step 3: Refresh the first pivot table so it reflects the latest data
        if (worksheet.PivotTables.Count == 0)
        {
            Console.Error.WriteLine("No pivot tables found on the first worksheet.");
            return;
        }

        PivotTable pivot = worksheet.PivotTables[0];
        pivot.Refresh();

        // 👉 Step 4: Export the refreshed pivot table as a PNG image
        string outputPath = Path.Combine(Environment.CurrentDirectory, "pivot.png");
        pivot.RenderToImage(imgOptions, outputPath);

        Console.WriteLine($"Pivot table exported successfully to: {outputPath}");

        // Clean up
        wb.Dispose();
    }
}
```

Ejecuta el programa, abre `pivot.png` y verás la tabla dinámica actualizada exactamente como aparece en Excel.

---

## Preguntas frecuentes

**P: ¿Esto funciona con archivos .xlsx creados por LibreOffice?**  
R: Sí. Aspose.Cells lee el formato Open XML sin importar la aplicación de origen, por lo que puedes **load excel workbook c#** desde LibreOffice, exportaciones de Google Sheets o cualquier otra fuente.

**P: ¿Puedo exportar varias hojas de cálculo a la vez?**  
R: Por supuesto. Recorre `wb.Worksheets` y aplica la misma lógica `RenderToImage` por hoja. Solo recuerda dar a cada salida un nombre de archivo único.

**P: ¿Qué pasa si la tabla dinámica usa una fuente de datos externa?**  
R: Aspose.Cells puede actualizar conexiones externas si están incrustadas en el archivo, pero deberás proporcionar la cadena de conexión y credenciales programáticamente. Consulta la documentación de Aspose para `DataSourceOptions`.

---

## Conclusión

Ahora tienes una solución sólida de extremo a extremo para **refresh excel pivot table** desde C# y **export excel pivot image** como PNG. El código muestra cómo **load excel workbook c#**, configurar las opciones de imagen, asegurar que la tabla dinámica refleje los datos más recientes y, finalmente, renderizarla a un archivo.

A continuación, podrías explorar **export pivot as image** en otros formatos (PDF, SVG) o automatizar el proceso para varios libros en un trabajo por lotes. ¿Quieres incrustar el PNG en un informe Word? La misma clase `ImageOrPrintOptions` funciona con Aspose.Words.

¡Siéntete libre de experimentar, romper cosas y hacer preguntas en los comentarios—feliz codificación!

![Refresh Excel pivot table screenshot](image.png)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}