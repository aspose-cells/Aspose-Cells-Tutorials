---
category: general
date: 2026-08-17
description: Guardar Excel como PowerPoint con C# – guía paso a paso para convertir
  archivos XLSX, hacer que los cuadros de texto sean editables y generar salida PPTX.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- save excel as powerpoint
- convert excel to powerpoint
- how to convert xlsx
- make textbox editable
- how to edit textboxes
language: es
lastmod: 2026-08-17
og_description: Guardar Excel como PowerPoint en C# con un ejemplo de código completo.
  Aprende cómo convertir XLSX, hacer que los cuadros de texto sean editables y exportar
  a PPTX.
og_image_alt: Screenshot showing Excel data saved as a PowerPoint slide
og_title: Guardar Excel como PowerPoint en C# – guía completa de conversión
schemas:
- author: Aspose
  dateModified: '2026-08-17'
  description: Save Excel as PowerPoint with C# – step‑by‑step guide to convert XLSX
    files, make textboxes editable, and generate PPTX output.
  headline: How to save Excel as PowerPoint using C# and Aspose.Cells
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel-to-PowerPoint
title: Cómo guardar Excel como PowerPoint usando C# y Aspose.Cells
url: /es/net/converting-excel-files-to-other-formats/how-to-save-excel-as-powerpoint-using-c-and-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo guardar Excel como PowerPoint usando C# y Aspose.Cells

Si necesitas **guardar Excel como PowerPoint** en un proyecto .NET, esta guía te muestra una solución completa, lista‑para‑ejecutar. Verás cómo cargar un libro de trabajo XLSX, hacer que cada cuadro de texto en la hoja sea editable y exportar el resultado a un archivo PPTX, todo con solo unas pocas líneas de C#.

Convertir Excel a PowerPoint es un requisito común para paneles de informes, presentaciones o generación automática de diapositivas. Este tutorial también cubre **cómo editar cuadros de texto** programáticamente, para que puedas personalizar el contenido de la diapositiva antes de guardarla.

## Requisitos previos

* SDK .NET 6.0 (o posterior) instalado  
* Un entorno de desarrollo como Visual Studio 2022 o VS Code  
* Una licencia de Aspose.Cells para .NET (o una clave de evaluación gratuita) – descárgala desde el [sitio web de Aspose](https://products.aspose.com/cells/net/)  
* El archivo `input.xlsx` que deseas convertir  

> **Consejo profesional:** Si utilizas la versión de evaluación gratuita, el PPTX de salida contendrá una marca de agua. Una versión con licencia la elimina.

## Paso 1: Instalar el paquete NuGet Aspose.Cells

Abre una terminal en la carpeta de tu proyecto y ejecuta:

```bash
dotnet add package Aspose.Cells
```

Esto agrega el ensamblado `Aspose.Cells`, que proporciona las clases `Workbook`, `Worksheet` y `Shape` necesarias para la conversión.

## Paso 2: Crear la estructura básica de una aplicación de consola

Crea un nuevo proyecto de consola (si aún no tienes uno):

```bash
dotnet new console -n ExcelToPptxDemo
cd ExcelToPptxDemo
```

Reemplaza el `Program.cs` generado con el código que se muestra en los siguientes pasos.

## Paso 3: Cargar el libro de trabajo y seleccionar la primera hoja

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Drawing;

class Program
{
    static void Main()
    {
        // Load the workbook from a file – adjust the path to your environment
        string inputPath = @"YOUR_DIRECTORY\input.xlsx";
        Workbook workbook = new Workbook(inputPath);

        // Get the first worksheet in the workbook
        Worksheet worksheet = workbook.Worksheets[0];
```

**Por qué es importante:**  
`Workbook` lee el archivo Excel en memoria, mientras que `Worksheet` te brinda acceso a las celdas, gráficos y formas de la hoja. La primera hoja suele ser el informe predeterminado que deseas presentar.

## Paso 4: Hacer que cada cuadro de texto en la hoja sea editable

```csharp
        // Iterate through all shapes on the worksheet
        foreach (Shape shapeItem in worksheet.Shapes)
        {
            // Check if the shape is a textbox (ShapeType.TextBox)
            if (shapeItem.Type == ShapeType.TextBox)
            {
                // The IsEditable property was added in Aspose.Cells 25.11
                shapeItem.TextBox.IsEditable = true;
            }
        }
```

**Por qué lo necesitas:**  
Por defecto, los cuadros de texto importados desde Excel son de solo lectura cuando se renderizan en PowerPoint. Establecer `IsEditable = true` permite que tú (o usuarios posteriores de PowerPoint) modifiquen el texto directamente en la diapositiva.

## Paso 5: Guardar el libro de trabajo como una presentación PowerPoint

```csharp
        // Define the output path for the PPTX file
        string outputPath = @"YOUR_DIRECTORY\output.pptx";

        // Save the workbook as a PowerPoint presentation
        workbook.Save(outputPath, SaveFormat.Pptx);

        Console.WriteLine($"Conversion complete. PPTX saved to: {outputPath}");
    }
}
```

**Qué ocurre internamente:**  
`Workbook.Save` detecta el valor enum `SaveFormat.Pptx` y traduce el diseño de la hoja de Excel —incluyendo filas, columnas, gráficos y los cuadros de texto ahora editables— en objetos de diapositiva de PowerPoint.

## Código fuente completo (ejecutable)

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Drawing;

class Program
{
    static void Main()
    {
        // Step 1: Load the workbook from a file
        string inputPath = @"YOUR_DIRECTORY\input.xlsx";
        Workbook workbook = new Workbook(inputPath);

        // Step 2: Get the first worksheet in the workbook
        Worksheet worksheet = workbook.Worksheets[0];

        // Step 3: Make every textbox on the sheet editable (property added in version 25.11)
        foreach (Shape shapeItem in worksheet.Shapes)
        {
            if (shapeItem.Type == ShapeType.TextBox)
            {
                shapeItem.TextBox.IsEditable = true;
            }
        }

        // Step 4: Save the workbook as a PowerPoint presentation
        string outputPath = @"YOUR_DIRECTORY\output.pptx";
        workbook.Save(outputPath, SaveFormat.Pptx);

        Console.WriteLine($"Conversion complete. PPTX saved to: {outputPath}");
    }
}
```

### Salida esperada

Al ejecutar el programa (`dotnet run`), deberías ver:

```
Conversion complete. PPTX saved to: YOUR_DIRECTORY\output.pptx
```

Al abrir `output.pptx` en Microsoft PowerPoint se mostrará una diapositiva que replica la hoja de Excel original. Todos los cuadros de texto pueden editarse directamente haciendo doble clic sobre ellos.

## Preguntas frecuentes y casos límite

| Pregunta | Respuesta |
|----------|-----------|
| **¿Puedo convertir una hoja específica en lugar de la primera?** | Sí. Reemplaza `workbook.Worksheets[0]` con `workbook.Worksheets["SheetName"]` o cualquier índice que necesites. |
| **¿Qué pasa si el libro de trabajo contiene varias hojas?** | Llama a `workbook.Save` una vez por hoja, proporcionando un nombre de archivo PPTX distinto para cada una, o combínalas en una sola presentación usando objetos `Presentation` de Aspose.Slides. |
| **¿Se conservarán los gráficos?** | Aspose.Cells convierte los gráficos de Excel en objetos de gráfico de PowerPoint automáticamente. No se requiere código adicional. |
| **¿Cómo cambio el tamaño de la diapositiva?** | Después de `workbook.Save`, puedes cargar el PPTX generado con Aspose.Slides y ajustar `Presentation.SlideSize`. |
| **¿Qué pasa si necesito editar el texto del cuadro de texto antes de guardar?** | Accede a `shapeItem.TextBox.Text` dentro del bucle, modifícalo y luego establece `IsEditable = true`. Ejemplo: `shapeItem.TextBox.Text = "New title";` |

## Consejos de solución de problemas

* **“ShapeType.TextBox” no encontrado** – Asegúrate de estar usando Aspose.Cells versión 25.11 o posterior; las versiones anteriores no tienen la propiedad `IsEditable`.  
* **Errores de archivo no encontrado** – Verifica que `YOUR_DIRECTORY` sea una ruta absoluta o que la ruta relativa apunte a la ubicación correcta.  
* **Licencia no aplicada** – Llama a `License license = new License(); license.SetLicense("Aspose.Total.NET.lic");` antes de cargar el libro de trabajo para eliminar las marcas de agua de evaluación.

## Conclusión

Ahora sabes cómo **guardar Excel como PowerPoint** con C# cargando un libro de trabajo XLSX, haciendo que cada cuadro de texto sea editable y exportando a PPTX. Este método maneja gráficos, imágenes y formato de celdas automáticamente, proporcionándote una presentación lista para usar.

A continuación, explora temas relacionados como **convertir Excel a PowerPoint con Aspose.Slides**, **cómo editar cuadros de texto programáticamente después de la conversión**, o **procesar por lotes varios libros de trabajo**. Cada uno de estos se basa en los pasos principales cubiertos aquí y puede automatizar aún más tu flujo de trabajo de informes.

## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que se basan en las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y funcionales con explicaciones paso a paso para ayudarte a dominar funciones adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Cómo convertir Excel a PowerPoint usando Aspose.Cells para .NET: Guía completa](/cells/english/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)
- [Cómo copiar tabla dinámica en C# – Convertir Excel a PPTX, copiar rango y crear cuadro de texto](/cells/english/net/pivot-tables/how-to-copy-pivot-table-in-c-convert-excel-to-pptx-copy-rang/)
- [Cómo guardar archivos Excel en múltiples formatos usando Aspose.Cells .NET (Guía 2023)](/cells/english/net/workbook-operations/aspose-cells-net-save-excel-formats/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}