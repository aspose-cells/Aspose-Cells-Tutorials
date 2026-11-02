---
category: general
date: 2026-04-07
description: Aprende cómo actualizar la tabla dinámica, insertar una imagen en Excel
  y guardar el libro de Excel con un marcador de posición de imagen en solo unos pocos
  pasos.
draft: false
keywords:
- how to refresh pivot
- insert image into excel
- save excel workbook
- add picture placeholder
- refresh pivot table
language: es
og_description: Cómo actualizar una tabla dinámica en Excel, insertar una imagen en
  Excel y guardar el libro de Excel usando C# con un marcador de posición de imagen.
  Ejemplo de código paso a paso.
og_title: Cómo actualizar la tabla dinámica e insertar una imagen en Excel – Guía
  completa
tags:
- Aspose.Cells
- C#
- Excel automation
title: Cómo actualizar la tabla dinámica e insertar una imagen en Excel – Guía completa
url: /es/net/pivot-tables/how-to-refresh-pivot-and-insert-image-into-excel-complete-gu/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo actualizar una tabla dinámica e insertar una imagen en Excel – Guía completa

¿Alguna vez te has preguntado **cómo actualizar una tabla dinámica** cuando los datos de origen cambian, y luego colocar una nueva imagen de gráfico o tabla directamente en la misma hoja? No eres el único. En muchos flujos de informes los datos viven en una base de datos, la tabla dinámica los extrae, y el archivo Excel final necesita mostrar los últimos números como una imagen, de modo que los usuarios posteriores no puedan editar accidentalmente el origen.  

En este tutorial recorreremos exactamente eso: **cómo actualizar una tabla dinámica**, **insertar una imagen en Excel**, y finalmente **guardar el libro de Excel** usando un **marcador de posición de imagen**. Al final tendrás un único programa C# ejecutable que lo hace todo, y comprenderás por qué cada línea es importante.

> **Consejo profesional:** El enfoque funciona con Aspose.Cells 2024 o posterior, lo que significa que no necesitas Excel instalado en el servidor.

---

## Lo que necesitarás

- **Aspose.Cells for .NET** (paquete NuGet `Aspose.Cells`).  
- SDK .NET 6.0 o posterior (el código también compila con .NET 8).  
- Un archivo Excel básico (`input.xlsx`) que ya contiene una tabla dinámica y un marcador de posición de imagen (el primer objeto picture en la hoja).  
- Un poco de curiosidad sobre los modelos de objetos de Excel.

Sin interop COM adicional, sin instalación de Office, solo C# puro.

---

## Cómo actualizar la tabla dinámica y capturar los datos más recientes

Lo primero que debes hacer es indicarle a Excel (o mejor dicho, a Aspose.Cells) que la tabla dinámica debe recalcularse basándose en el rango de origen más reciente. Omitir este paso te deja con números obsoletos, lo que anula todo el propósito de la automatización.

```csharp
using Aspose.Cells;
using System.Drawing.Imaging;

// 1️⃣ Load the workbook and grab the first worksheet
Workbook workbook = new Workbook(@"C:\MyProjects\ExcelDemo\input.xlsx");
Worksheet worksheet = workbook.Worksheets[0];

// 2️⃣ Refresh the first pivot table so it reflects the latest data
worksheet.PivotTables[0].Refresh();
```

**Por qué esto es importante:**  
Cuando llamas a `Refresh()`, el motor de la tabla dinámica vuelve a ejecutar su lógica de agregación. Si luego exportas la tabla dinámica como una imagen, la picture mostrará los totales *actuales*, no los que estaban cuando el archivo se guardó por última vez.

---

## Insertar imagen en Excel usando un marcador de posición de picture

Ahora que la tabla dinámica está actualizada, necesitamos convertirla en una imagen estática. Esto es útil cuando deseas bloquear la visualización para su distribución o incrustarla más tarde en una diapositiva de PowerPoint.

```csharp
// 3️⃣ Set up image options – we want a PNG image
ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
{
    ImageFormat = ImageFormat.Png
};

// 4️⃣ Render the refreshed pivot table to an image using the options
Image pivotImage = worksheet.PivotTables[0].ToImage(imageOptions);
```

El objeto `ImageOrPrintOptions` te permite controlar la resolución, el fondo y el formato. PNG es sin pérdida y funciona muy bien para la mayoría de los informes empresariales.

---

## Añadir marcador de posición de picture a una hoja de cálculo

La mayoría de las plantillas de Excel ya contienen una forma o imagen que actúa como un “espacio” para gráficos dinámicos. Si no tienes una, simplemente inserta una imagen en blanco en Excel y guarda la plantilla—Aspose.Cells la expondrá como `Pictures[0]`.

```csharp
// 5️⃣ Place the rendered image into the first picture placeholder on the sheet
worksheet.Pictures[0].Image = pivotImage;
```

**¿Qué pasa si tienes varios marcadores de posición?**  
Simplemente cambia el índice (`Pictures[1]`, `Pictures[2]`, …) o recorre `worksheet.Pictures` para encontrar uno por nombre.

---

## Guardar el libro de Excel después de las modificaciones

Finalmente, guardamos los cambios. El libro ahora contiene una tabla dinámica actualizada, un PNG recién generado y el marcador de posición de picture actualizado con esa imagen.

```csharp
// 6️⃣ Save the workbook to see the result
workbook.Save(@"C:\MyProjects\ExcelDemo\output.xlsx");
```

Al abrir `output.xlsx` verás el espacio de picture rellenado con la instantánea más reciente de la tabla dinámica. No se requieren pasos manuales.

---

## Ejemplo completo (todos los pasos juntos)

A continuación se muestra el programa completo, listo para copiar y pegar. Incluye las declaraciones `using` necesarias, manejo de errores y comentarios que explican cada línea no obvia.

```csharp
using Aspose.Cells;
using System;
using System.Drawing.Imaging;

namespace ExcelPivotImageDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Paths – adjust to your environment
            string inputPath = @"C:\MyProjects\ExcelDemo\input.xlsx";
            string outputPath = @"C:\MyProjects\ExcelDemo\output.xlsx";

            try
            {
                // Load workbook
                Workbook workbook = new Workbook(inputPath);
                Worksheet sheet = workbook.Worksheets[0];

                // -------------------------------------------------
                // Refresh pivot table – this is the core of "how to refresh pivot"
                // -------------------------------------------------
                if (sheet.PivotTables.Count == 0)
                {
                    Console.WriteLine("No pivot tables found on the first worksheet.");
                    return;
                }
                sheet.PivotTables[0].Refresh();

                // -------------------------------------------------
                // Convert refreshed pivot to PNG image
                // -------------------------------------------------
                ImageOrPrintOptions imgOpts = new ImageOrPrintOptions
                {
                    ImageFormat = ImageFormat.Png,
                    // Optional: higher DPI for sharper images
                    HorizontalResolution = 150,
                    VerticalResolution = 150
                };
                Image pivotImg = sheet.PivotTables[0].ToImage(imgOpts);

                // -------------------------------------------------
                // Insert the image into the first picture placeholder
                // -------------------------------------------------
                if (sheet.Pictures.Count == 0)
                {
                    // If the template lacks a placeholder, we create one on the fly
                    int picIdx = sheet.Pictures.Add(0, 0, pivotImg);
                    sheet.Pictures[picIdx].Name = "PivotSnapshot";
                }
                else
                {
                    sheet.Pictures[0].Image = pivotImg;
                }

                // -------------------------------------------------
                // Save the updated workbook – this fulfills "save excel workbook"
                // -------------------------------------------------
                workbook.Save(outputPath);
                Console.WriteLine($"Workbook saved successfully to {outputPath}");
            }
            catch (Exception ex)
            {
                Console.WriteLine($"Error: {ex.Message}");
                // In production you might log the stack trace or rethrow
            }
        }
    }
}
```

**Resultado esperado:**  
Abre `output.xlsx`. El primer objeto picture ahora muestra un PNG de la tabla dinámica actualizada. Si cambias los datos de origen en `input.xlsx` y ejecutas el programa de nuevo, la imagen se actualiza automáticamente—no se necesita copiar‑pegar manualmente.

---

## Variaciones comunes y casos límite

| Situación | Qué cambiar |
|-----------|-------------|
| **Multiple pivot tables** | Recorre `sheet.PivotTables` y actualiza cada una, luego elige la que necesitas para la imagen. |
| **Different image format** | Establece `ImageFormat = ImageFormat.Jpeg` (o `Bmp`) en `ImageOrPrintOptions`. |
| **Dynamic placeholder selection** | Usa `sheet.Pictures["MyPlaceholderName"]` en lugar de un índice. |
| **Large workbooks** | Incrementa `Workbook.Settings.CalculateFormulaEngine` a `EngineType.Fast` para actualizaciones más rápidas. |
| **Running on a headless server** | Aspose.Cells funciona completamente sin UI, por lo que no se requiere configuración adicional. |

---

## Preguntas frecuentes

**Q: ¿Funciona esto con libros habilitados para macros (`.xlsm`)?**  
A: Sí. Aspose.Cells los trata como cualquier otro libro; las macros se conservan pero no se ejecutan durante la actualización.

**Q: ¿Qué pasa si la tabla dinámica usa una fuente de datos externa?**  
A: Debes asegurarte de que la cadena de conexión sea válida en la máquina que ejecuta el código. Llama a `pivotTable.CacheDefinition.ConnectionInfo` para ajustarla programáticamente.

**Q: ¿Puedo colocar la imagen en un rango de celdas específico en lugar de un marcador de posición de picture?**  
A: Por supuesto. Usa `sheet.Pictures.Add(row, column, pivotImg)` donde `row` y `column` son índices basados en cero.

---

## Conclusión

Hemos cubierto **cómo actualizar una tabla dinámica**, **insertar una imagen en Excel**, **añadir un marcador de posición de picture**, y finalmente **guardar el libro de Excel**—todo en un fragmento de C# ordenado. Al actualizar la tabla dinámica primero, garantizas que la imagen refleje los últimos números, y al usar un marcador de posición mantienes tus plantillas limpias y reutilizables.

A continuación, podrías explorar:

- Exportar la misma imagen a un informe PDF (`PdfSaveOptions`).  
- Automatizar un lote de archivos con diferentes datos de origen.  
- Usar Aspose.Slides para pegar el PNG directamente en una diapositiva de PowerPoint.

Siéntete libre de experimentar—cambiar el PNG por un JPEG, modificar el DPI, o añadir múltiples imágenes. La idea central sigue siendo la misma: mantener los datos actualizados, capturarlos como una imagen y incrustarlos donde los necesites.

¡Feliz codificación! 🚀

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}