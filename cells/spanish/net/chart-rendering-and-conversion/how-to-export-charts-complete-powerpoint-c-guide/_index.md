---
category: general
date: 2026-06-05
description: Cómo exportar gráficos desde PowerPoint usando C#. Incluye la exportación
  de objetos OLE y hace que los gráficos sean editables en el PPTX resultante, paso
  a paso.
draft: false
keywords:
- how to export charts
- export ole objects
- how to export ole
- make charts editable
language: es
og_description: Cómo exportar gráficos de PowerPoint usando C#. Aprende a exportar
  objetos OLE y a hacer que los gráficos sean editables en el PPTX guardado, paso
  a paso.
og_title: Cómo exportar gráficos – Guía completa de PowerPoint en C#
schemas:
- author: Aspose
  dateModified: '2026-06-05'
  description: How to export charts from PowerPoint using C#. Includes export OLE
    objects and make charts editable in the resulting PPTX – step‑by‑step.
  headline: How to Export Charts – Complete PowerPoint C# Guide
  type: TechArticle
- description: How to export charts from PowerPoint using C#. Includes export OLE
    objects and make charts editable in the resulting PPTX – step‑by‑step.
  name: How to Export Charts – Complete PowerPoint C# Guide
  steps:
  - name: Full Working Example
    text: Below is the complete, self‑contained program you can compile and run. It
      includes `using` statements, proper disposal, and comments that explain each
      line.
  - name: What if the source file has no charts?
    text: The code will still run; `ExportEditableCharts` simply has no effect because
      there’s nothing to convert. No error is thrown.
  - name: Can I export only specific charts?
    text: Yes. Instead of using the global `ExportEditableCharts` flag, you can iterate
      through `presentation.Slides` and set `Chart.IsEditable = true` on individual
      chart objects before saving. This gives you granular control.
  - name: Does enabling OLE export increase file size?
    text: A little. The binary OLE streams are stored verbatim, so the resulting PPTX
      can be a few kilobytes larger. In most business scenarios the trade‑off is worth
      it because you retain full editability.
  - name: Which PowerPoint versions can open the resulting file?
    text: Any version that supports the OOXML standard (PowerPoint 2007 and later).
      The editable chart feature relies on the native chart editor introduced in Office
      2007, so older binaries like `.ppt` won’t benefit.
  type: HowTo
tags:
- PowerPoint
- C#
- Aspose.Slides
- OLE
- Charts
title: How to Export Charts – Complete PowerPoint C# Guide
url: /es/net/chart-rendering-and-conversion/how-to-export-charts-complete-powerpoint-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo exportar gráficos – Guía completa de PowerPoint en C#

¿Alguna vez te has preguntado **cómo exportar gráficos** de una presentación de PowerPoint sin perder la capacidad de editarlos después? No eres el único. En muchos flujos de trabajo de informes los datos del gráfico viven dentro del PPTX, y una vez que entregas el archivo, el destinatario a menudo necesita ajustar un valor o cambiar una etiqueta. La buena noticia es que con unas pocas líneas de C# puedes preservar la editabilidad, e incluso exportar objetos OLE incrustados al mismo tiempo.

En este tutorial recorreremos un ejemplo práctico, listo‑para‑ejecutar, que muestra **cómo exportar gráficos**, cómo **exportar objetos OLE**, y cómo **hacer que los gráficos sean editables** en el archivo de salida. Al final tendrás un fragmento reutilizable que puedes insertar en cualquier proyecto .NET que use la biblioteca Aspose.Slides.

> **Consejo profesional:** Si eres nuevo en Aspose.Slides, asegúrate de haber añadido el paquete NuGet `Aspose.Slides.NET` a tu proyecto—de lo contrario el código no compilará.

## Qué necesitarás

| Requisito | Por qué es importante |
|-----------|-----------------------|
| .NET 6+ (o .NET Framework 4.7+) | Los runtimes modernos ofrecen mejor rendimiento y una gestión de paquetes más sencilla. |
| Aspose.Slides for .NET (última versión) | Esta biblioteca proporciona las clases `Presentation` y `PptxSaveOptions` que utilizaremos. |
| Un archivo PowerPoint de ejemplo con al menos un gráfico | La demo funciona con cualquier `.pptx` que contenga un gráfico; verás la editabilidad después de la exportación. |
| Un IDE (Visual Studio, Rider o VS Code) | Útil para depurar rápidamente y ver el archivo generado. |

No se requieren herramientas de terceros adicionales—todo es manejado por la API de Aspose.

## Paso 1 – Cargar la presentación de origen

Primero necesitamos cargar el PPTX original en memoria. Piensa en esto como abrir un documento en Word antes de comenzar a editar.

```csharp
using Aspose.Slides;

// Step 1: Load the source presentation
Presentation presentation = new Presentation(@"C:\MyProjects\input.pptx");
```

> **Por qué es importante:** El objeto `Presentation` es el punto de entrada para todas las operaciones posteriores. Analiza el archivo, construye un modelo de objetos de diapositivas, formas, gráficos y objetos OLE, y mantiene todo en un estado mutable.

## Paso 2 – Crear opciones de guardado y habilitar gráficos editables

Por defecto, cuando llamas a `Save` la biblioteca aplana los gráficos en imágenes estáticas. Para mantenerlos editables debes activar la bandera `ExportEditableCharts`.

```csharp
// Step 2: Create PPTX save options and enable editable charts
PptxSaveOptions saveOptions = new PptxSaveOptions
{
    // This tells Aspose to keep chart data in a format PowerPoint can edit.
    ExportEditableCharts = true
};
```

> **Cómo funciona:** Cuando `ExportEditableCharts` es `true`, la biblioteca escribe la definición XML del gráfico (`chart.xml`) dentro del PPTX en lugar de rasterizarlo. PowerPoint entonces lee ese XML y permite al usuario abrir el editor de gráficos.

## Paso 3 – Activar la exportación de objetos OLE incrustados

Muchas presentaciones incrustan hojas de Excel, diagramas de Visio o incluso archivos PDF como objetos OLE. Si deseas que esos objetos sobrevivan al proceso de ida y vuelta, habilita `ExportOLEObjects`.

```csharp
// Step 3: Enable export of embedded OLE objects
saveOptions.ExportOLEObjects = true;
```

> **Qué significa realmente “exportar objetos OLE”:** El paquete OLE se almacena como un blob binario dentro del PPTX. Al establecer esta bandera se preserva el binario original, permitiendo al destinatario hacer doble clic en el objeto y abrirlo en su aplicación nativa (p. ej., Excel). Sin ella, el objeto OLE sería eliminado, rompiendo enlaces y perdiendo datos.

## Paso 4 – Guardar la presentación con las opciones configuradas

Ahora que hemos preparado las opciones, simplemente indicamos a Aspose que escriba el archivo.

```csharp
// Step 4: Save the presentation with the configured options
presentation.Save(@"C:\MyProjects\editable.pptx", saveOptions);
```

> **Resultado:** `editable.pptx` contiene las mismas diapositivas que `input.pptx`, pero cualquier gráfico puede editarse directamente en PowerPoint, y los objetos OLE incrustados permanecen intactos.

### Ejemplo completo y funcional

A continuación tienes el programa completo, autocontenido, que puedes compilar y ejecutar. Incluye sentencias `using`, la correcta liberación de recursos y comentarios que explican cada línea.

```csharp
using System;
using Aspose.Slides;

namespace ExportChartsDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Path to the source PPTX
            string sourcePath = @"C:\MyProjects\input.pptx";
            // Path where the edited PPTX will be saved
            string destPath = @"C:\MyProjects\editable.pptx";

            // Load the presentation
            using (Presentation presentation = new Presentation(sourcePath))
            {
                // Configure save options
                PptxSaveOptions options = new PptxSaveOptions
                {
                    ExportEditableCharts = true,   // make charts editable
                    ExportOLEObjects = true        // export OLE objects such as embedded Excel sheets
                };

                // Save the new file
                presentation.Save(destPath, options);
            }

            Console.WriteLine("Presentation saved with editable charts and OLE objects.");
        }
    }
}
```

**Salida esperada:** Después de ejecutar el programa, abre `editable.pptx` en PowerPoint. Haz clic derecho en cualquier gráfico → *Edit Data* → se abrirá el editor de gráficos, confirmando que **hacer gráficos editables** funcionó. Haz doble clic en una hoja de Excel incrustada y se abrirá en Excel, demostrando que **exportar objetos OLE** funcionó.

![how to export charts diagram](https://example.com/images/export-charts.png "how to export charts – PowerPoint after export")

*(Texto alternativo: cómo exportar gráficos – captura de pantalla de PowerPoint con gráfico editable y objeto OLE)*

## Preguntas frecuentes y casos límite

### ¿Qué pasa si el archivo de origen no tiene gráficos?

El código seguirá ejecutándose; `ExportEditableCharts` simplemente no tendrá efecto porque no hay nada que convertir. No se lanza ningún error.

### ¿Puedo exportar solo gráficos específicos?

Sí. En lugar de usar la bandera global `ExportEditableCharts`, puedes iterar a través de `presentation.Slides` y establecer `Chart.IsEditable = true` en los objetos de gráfico individuales antes de guardar. Esto te brinda control granular.

```csharp
foreach (ISlide slide in presentation.Slides)
{
    foreach (IChart chart in slide.Shapes.OfType<IChart>())
    {
        chart.IsEditable = true; // enable editability only for this chart
    }
}
```

### ¿Activar la exportación OLE aumenta el tamaño del archivo?

Un poco. Los flujos binarios OLE se almacenan tal cual, por lo que el PPTX resultante puede ser unos pocos kilobytes más grande. En la mayoría de los escenarios empresariales el intercambio vale la pena porque conservas la editabilidad completa.

### ¿Qué versiones de PowerPoint pueden abrir el archivo resultante?

Cualquier versión que soporte el estándar OOXML (PowerPoint 2007 y posteriores). La función de gráfico editable depende del editor nativo introducido en Office 2007, por lo que versiones más antiguas como `.ppt` no se beneficiarán.

## Consejos para código listo para producción

| Consejo | Razón |
|---------|-------|
| Usa bloques `using` (como se muestra) para disponer de los objetos `Presentation`. | Evita fugas de memoria, especialmente al procesar muchos archivos en lote. |
| Valida las rutas de archivo antes de cargarlas. | Previene `FileNotFoundException` que podría bloquear un servicio en segundo plano. |
| Registra los valores de `ExportEditableCharts` y `ExportOLEObjects`. | Útil para depurar cuando un usuario informa que los gráficos no son editables. |
| Captura `Aspose.Slides.Exception` por separado. | Proporciona mensajes de error más claros de la biblioteca (p. ej., tipos de gráfico no compatibles). |
| Considera `PptxCompressionLevel` si el tamaño del archivo es crítico. | Puedes comprimir la salida manteniendo la editabilidad. |

## Recapitulación – Lo que logramos

Comenzamos con una pregunta clara: **cómo exportar gráficos** de un archivo PowerPoint manteniéndolos editables y preservando los objetos OLE incrustados. Al cargar la presentación, configurar `PptxSaveOptions` (`ExportEditableCharts = true` y `ExportOLEObjects = true`) y guardar el archivo, ahora disponemos de un PPTX que satisface ambos requisitos. El mismo patrón puede reutilizarse para conversiones por lotes, pipelines CI o cualquier herramienta de generación de informes automatizada.

## ¿Qué explorar a continuación?

- **Exportar gráficos como imágenes** para informes estáticos (`saveOptions.ExportEditableCharts = false`).  
- **Convertir PPTX a PDF** manteniendo gráficos vectoriales (`PdfSaveOptions`).  
- **Manipular datos de gráficos programáticamente** (p. ej., actualizar valores de series antes de exportar).  
- **Integrar con Azure Functions** para ofrecer una API de exportación de gráficos bajo demanda.

¡Experimenta, y cuéntanos qué casos límite encuentras! Feliz codificación, y que todos tus gráficos permanezcan editables.

## ¿Qué deberías aprender después?

Los siguientes tutoriales cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos con explicaciones paso a paso para ayudarte a dominar funcionalidades adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [How to Export Excel Charts to PDF Using Aspose.Cells for .NET: A Step-by-Step Guide](/cells/english/net/workbook-operations/export-excel-charts-pdf-aspose-cells-net/)
- [How to Convert Excel Charts to SVG Using Aspose.Cells for .NET (Step-by-Step Guide)](/cells/english/net/charts-graphs/convert-excel-chart-to-svg-aspose-cells-net/)
- [How to Apply Themes to Excel Charts Using Aspose.Cells .NET: A Step-by-Step Guide](/cells/english/net/charts-graphs/apply-themes-charts-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}