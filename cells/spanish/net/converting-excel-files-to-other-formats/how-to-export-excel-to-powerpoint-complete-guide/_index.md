---
category: general
date: 2026-07-03
description: Cómo exportar archivos de Excel a PowerPoint con cuadros de texto editables
  usando Aspose.Cells – guía paso a paso para convertir XLSX a PPTX.
draft: false
keywords:
- how to export excel
- create powerpoint from excel
- editable text boxes
- convert xlsx to pptx
- presentation export options
language: es
og_description: Cómo exportar Excel a PowerPoint con cuadros de texto editables. Aprende
  a convertir XLSX a PPTX usando PresentationExportOptions en C#.
og_title: Cómo exportar Excel a PowerPoint – Guía completa
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: How to export Excel files to PowerPoint with editable text boxes using
    Aspose.Cells – step‑by‑step guide for converting XLSX to PPTX.
  headline: How to Export Excel to PowerPoint – Complete Guide
  type: TechArticle
- description: How to export Excel files to PowerPoint with editable text boxes using
    Aspose.Cells – step‑by‑step guide for converting XLSX to PPTX.
  name: How to Export Excel to PowerPoint – Complete Guide
  steps:
  - name: Navigate to a slide that originated from a worksheet.
    text: Navigate to a slide that originated from a worksheet.
  - name: Click on a text box—notice you can edit the text directly.
    text: Click on a text box—notice you can edit the text directly.
  - name: Adjust the shape’s size or color; the changes persist.
    text: Adjust the shape’s size or color; the changes persist.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Office Automation
title: Cómo exportar Excel a PowerPoint – Guía completa
url: /es/net/converting-excel-files-to-other-formats/how-to-export-excel-to-powerpoint-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo exportar Excel a PowerPoint – Guía completa

¿Alguna vez te has preguntado **cómo exportar excel** datos directamente a una presentación de PowerPoint sin perder la editabilidad? No estás solo. En este tutorial te mostraremos una forma práctica de **crear PowerPoint desde Excel** manteniendo los cuadros de texto y las formas totalmente editables.

Recorreremos cada línea de código, explicaremos por qué cada configuración es importante y terminaremos con un archivo PowerPoint que podrás abrir y ajustar de inmediato. Al final, podrás **convertir XLSX a PPTX** en una sola llamada de método, y comprenderás cómo las **presentation export options** controlan el resultado.

## Lo que necesitarás

- **.NET 6.0** (o cualquier versión reciente de .NET) instalado en tu máquina.  
- Una **licencia** para **Aspose.Cells for .NET** (la prueba gratuita funciona para pruebas).  
- Un conocimiento básico de C#—nada sofisticado, solo la capacidad de crear una aplicación de consola o una pequeña biblioteca.  
- Un libro de Excel (`input.xlsx`) que quieras convertir en una presentación de diapositivas.

Eso es todo. Sin herramientas extra, sin interop COM, solo código administrado puro.

![Diagrama de cómo exportar excel a PowerPoint](https://example.com/placeholder.png "Diagrama que muestra el flujo de cómo exportar datos de Excel a PowerPoint")

## Paso 1: Instalar Aspose.Cells y configurar el proyecto

Para **how to export excel** primero necesitas la biblioteca que lo hace posible. Abre una terminal en la carpeta de tu proyecto y ejecuta:

```bash
dotnet add package Aspose.Cells
```

Esto descarga el paquete más reciente de Aspose.Cells desde NuGet. La biblioteca incluye todo lo que necesitas para **presentation export options**, por lo que no tendrás que referenciar los ensamblados de Office Interop.

> **Consejo profesional:** Si estás apuntando a .NET Framework, usa la versión adecuada de NuGet (por ejemplo, `Aspose.Cells.NET`) para evitar sorpresas de compatibilidad.

## Paso 2: Cargar el libro de Excel

Ahora que la biblioteca está en su lugar, carguemos el archivo fuente. La clase `Workbook` representa todo el documento de Excel.

```csharp
using Aspose.Cells;

// Step 2: Load the Excel workbook
Workbook workbook = new Workbook(@"C:\Data\input.xlsx");
```

*Por qué es importante:* Cargar el libro de trabajo es el primer paso en cualquier flujo de trabajo de **convert XLSX to PPTX**. El objeto `Workbook` contiene hojas, gráficos y formato de celdas, todo lo cual puede mapearse a objetos de PowerPoint más adelante.

## Paso 3: Configurar Presentation Export Options (Cuadros de texto editables)

Aquí es donde ocurre la magia. Por defecto, Aspose.Cells exporta las formas como imágenes estáticas. Para mantenerlas como **cuadros de texto editables**, debes habilitar la bandera correcta.

```csharp
// Step 3: Create presentation export options and enable editable shapes
PresentationExportOptions exportOptions = new PresentationExportOptions
{
    ExportEditableObjects = true // Makes text boxes and shapes editable in the PPTX
};
```

> **¿Por qué habilitar `ExportEditableObjects`?**  
> Cuando esta propiedad es `true`, Aspose.Cells traduce cada forma de Excel en una forma nativa de PowerPoint. Eso significa que puedes abrir el `.pptx` resultante en PowerPoint y editar el texto, cambiar el tamaño del cuadro o modificar los colores—exactamente lo que esperas al **create PowerPoint from Excel**.

## Paso 4: Exportar el libro a PowerPoint

Con el libro cargado y las opciones configuradas, la línea final guarda el archivo como una presentación de PowerPoint.

```csharp
// Step 4: Export the workbook to a PowerPoint file using the configured options
workbook.Save(@"C:\Data\output.pptx", SaveFormat.Pptx, exportOptions);
```

*Lo que verás:* El archivo `output.pptx` contendrá una diapositiva por hoja de cálculo (por defecto). Cada diapositiva refleja el diseño de la hoja original, y cada cuadro de texto que colocaste en Excel ahora será un **editable text box** en PowerPoint.

## Paso 5: Verificar el resultado y ajustar si es necesario

Abre `output.pptx` en Microsoft PowerPoint:

1. Navega a una diapositiva que se originó a partir de una hoja de cálculo.  
2. Haz clic en un cuadro de texto—observa que puedes editar el texto directamente.  
3. Ajusta el tamaño o color de la forma; los cambios persisten.

Si algo parece incorrecto, considera estos ajustes:

- **Exportar solo hojas específicas:** Usa `workbook.Worksheets.RemoveAt(index)` antes de guardar.  
- **Controlar el diseño de la diapositiva:** Establece `exportOptions.ExportAllSheetsAsSlide = false` y agrega diapositivas manualmente.  
- **Preservar el formato de los gráficos:** Asegúrate de que los gráficos estén colocados en la hoja antes de la exportación; se convertirán automáticamente en gráficos de PowerPoint.

## Problemas comunes y cómo evitarlos

| Problema | Por qué ocurre | Solución |
|----------|----------------|----------|
| Las formas se convierten en imágenes | `ExportEditableObjects` dejado en su valor predeterminado (`false`) | Establecer `ExportEditableObjects = true` como se muestra en el Paso 3. |
| Hojas de cálculo faltantes | `Save` llamado antes de eliminar hojas no deseadas | Elimina u oculta las hojas que no necesitas antes de la exportación. |
| Tamaño de archivo grande | Imágenes de alta resolución incrustadas junto a las formas | Usa `exportOptions.ImageResolution = 150` para reducir DPI si es necesario. |
| Advertencias de compatibilidad en PowerPoint | Uso de una versión antigua de Aspose.Cells | Actualiza al último paquete NuGet (soporta PPTX 2016+). |

## Ejemplo completo funcionando

A continuación se muestra el programa completo que puedes copiar y pegar en una aplicación de consola. Incluye todos los pasos, manejo de errores y comentarios.

```csharp
using System;
using Aspose.Cells;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            try
            {
                // 1️⃣ Load the Excel workbook (convert XLSX to PPTX starts here)
                string inputPath = @"C:\Data\input.xlsx";
                Workbook workbook = new Workbook(inputPath);
                Console.WriteLine("Workbook loaded successfully.");

                // 2️⃣ Configure export options – make text boxes editable
                PresentationExportOptions exportOptions = new PresentationExportOptions
                {
                    ExportEditableObjects = true,
                    // Optional: tweak image resolution to keep file size reasonable
                    ImageResolution = 150
                };
                Console.WriteLine("Export options configured (editable text boxes enabled).");

                // 3️⃣ Save as PowerPoint
                string outputPath = @"C:\Data\output.pptx";
                workbook.Save(outputPath, SaveFormat.Pptx, exportOptions);
                Console.WriteLine($"File saved as PowerPoint: {outputPath}");
            }
            catch (Exception ex)
            {
                Console.WriteLine($"Error during conversion: {ex.Message}");
                // In a real app you might log the stack trace or rethrow.
            }
        }
    }
}
```

**Salida esperada en la consola:**

```
Workbook loaded successfully.
Export options configured (editable text boxes enabled).
File saved as PowerPoint: C:\Data\output.pptx
```

Abre el `output.pptx` generado—verás cada hoja de cálculo convertida en una diapositiva, y cada forma que agregaste en Excel ahora es un **editable text box** que puedes ajustar al instante.

## Recapitulación: Cómo exportar Excel rápida y limpiamente

Hemos cubierto todo el proceso de **how to export excel**, desde la instalación de Aspose.Cells, pasando por la configuración de **presentation export options**, hasta finalmente **convert XLSX to PPTX** con contenido totalmente editable. Los puntos clave son:

- Usa `PresentationExportOptions.ExportEditableObjects = true` para mantener las formas editables.  
- El método `Workbook.Save` realiza el trabajo pesado; no necesitas ningún interop COM.  
- Ajusta configuraciones opcionales (resolución de imagen, selección de hoja) para afinar el resultado.

## ¿Qué sigue?

Si disfrutaste convertir hojas de cálculo en diapositivas, también podrías explorar:

- **Incrustar gráficos** como gráficos nativos de PowerPoint (`exportOptions.ExportChartAsShape = false`).  
- **Aplicar una diapositiva maestra personalizada** después de la exportación para coincidir con la identidad corporativa.  
- **Automatizar conversiones por lotes** para decenas de archivos usando un simple bucle `foreach`.  

Todos estos temas se basan en los mismos fundamentos que acabamos de cubrir, así que ya estás en una base sólida.

No dudes en dejar un comentario si encuentras algún problema, o compartir cómo has extendido este patrón en tus propios proyectos. ¡Feliz codificación y disfruta del puente sin fisuras entre Excel y PowerPoint!

## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que se basan en las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos con explicaciones paso a paso para ayudarte a dominar funciones adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Cómo convertir Excel a PowerPoint usando Aspose.Cells para .NET: Guía completa](/cells/english/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)
- [Cómo agregar y acceder a cuadros de texto en Excel usando Aspose.Cells .NET | Guía paso a paso](/cells/english/net/images-shapes/aspose-cells-net-add-text-boxes-excel/)
- [Cómo exportar archivos Excel en .NET usando Aspose.Cells: Guía completa](/cells/english/net/workbook-operations/export-excel-files-net-aspose-cells-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}