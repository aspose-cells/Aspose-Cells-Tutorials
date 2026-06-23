---
category: general
date: 2026-02-26
description: Exportar gráfico a PowerPoint desde Excel usando C#. Aprende cómo convertir
  Excel a PowerPoint, guardar Excel como PowerPoint y mantener las formas editables.
draft: false
keywords:
- export chart to powerpoint
- convert excel to powerpoint
- save excel as powerpoint
- how to convert excel to ppt
- save workbook as pptx
language: es
og_description: Exportar gráfico a PowerPoint desde Excel usando C#. Esta guía muestra
  cómo convertir Excel a PowerPoint, guardar el libro de trabajo como PPTX y mantener
  las formas editables.
og_title: Exportar gráfico a PowerPoint con C# – Tutorial completo de programación
tags:
- Aspose.Cells
- C#
- Office Automation
title: Exportar gráfico a PowerPoint con C# – Guía completa paso a paso
url: /es/net/chart-rendering-and-conversion/export-chart-to-powerpoint-with-c-complete-step-by-step-guid/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Exportar gráfico a PowerPoint – Tutorial completo de programación

¿Alguna vez te has preguntado cómo **exportar un gráfico a PowerPoint** sin perder la capacidad de edición? En muchos escenarios de informes necesitas un gráfico en vivo dentro de una presentación, pero copiar y pegar manualmente es un dolor. La buena noticia es que puedes hacerlo programáticamente con unas pocas líneas de C#.

En esta guía recorreremos todo el proceso: desde cargar un libro de Excel que contiene un gráfico con un cuadro de texto, configurar la exportación para que los cuadros de texto y las formas permanezcan editables, y finalmente guardar el resultado como un archivo **PowerPoint**. Al final también sabrás cómo **convertir Excel a PowerPoint**, **guardar Excel como PowerPoint**, y ajustar las opciones para escenarios de borde.

## Lo que necesitarás

- **Aspose.Cells for .NET** (versión 23.10 o posterior). Es la biblioteca que hace que la conversión sea sencilla.
- **.NET 6+** runtime – cualquier SDK reciente funciona.
- Un archivo Excel sencillo (`ChartWithTextbox.xlsx`) que contenga al menos un gráfico y un cuadro de texto.
- Visual Studio o tu IDE favorito.

No se requieren paquetes NuGet adicionales más allá de Aspose.Cells, pero tener una comprensión básica de la sintaxis de C# ciertamente ayuda.

## Exportar gráfico a PowerPoint – Paso a paso

A continuación dividimos la solución en pasos discretos y fáciles de seguir. Cada paso incluye el código exacto que necesitas, más un breve párrafo “por qué” que explica la razón detrás de él.

### Paso 1: Cargar el libro de Excel que contiene el gráfico

Primero necesitamos cargar el archivo fuente en memoria. Usar `Workbook` de Aspose.Cells lee toda la hoja de cálculo, incluidos gráficos, imágenes y objetos incrustados.

```csharp
using Aspose.Cells;

// Step 1: Load the Excel workbook that contains the chart with a textbox
Workbook workbook = new Workbook(@"C:\Samples\ChartWithTextbox.xlsx");

// Verify that the workbook actually contains a chart
if (workbook.Worksheets[0].Charts.Count == 0)
{
    throw new InvalidOperationException("No chart found in the first worksheet.");
}
```

*Por qué es importante:* Si el libro se abre sin especificar correctamente la ruta, obtendrás una `FileNotFoundException`. Esta rápida comprobación evita que exportes una diapositiva vacía más adelante.

### Paso 2: Preparar las opciones de presentación para mantener las formas editables

Aspose.Cells te permite decidir si los cuadros de texto, formas y hasta el propio gráfico permanecen **editables** después de la exportación. Configurar `ExportTextBoxes` y `ExportShapes` a `true` preserva esos objetos como elementos nativos de PowerPoint en lugar de aplanarlos en una imagen estática.

```csharp
using Aspose.Cells.Drawing;

// Step 2: Set up presentation options to keep textboxes and shapes editable in the output
PresentationOptions presentationOptions = new PresentationOptions
{
    ExportTextBoxes = true, // Preserve editable textboxes
    ExportShapes    = true  // Preserve shapes such as the chart itself
};
```

*Por qué es importante:* Si dejas estas banderas en sus valores predeterminados (`false`), la diapositiva resultante contendrá un mapa de bits del gráfico, lo que imposibilita editar las series o cambiar el título más tarde. Habilitar ambas opciones te brinda un verdadero gráfico de PowerPoint que se comporta exactamente como uno que dibujarías manualmente.

### Paso 3: Convertir Excel a PowerPoint y guardar el archivo

Ahora invocamos el método `Save`, pasando el enumerado `SaveFormat.Pptx` y las opciones que acabamos de configurar. La biblioteca se encarga de traducir el objeto de gráfico de Excel en una forma de gráfico de PowerPoint.

```csharp
// Step 3: Save the workbook as a PowerPoint presentation using the configured options
workbook.Save(@"C:\Samples\Result.pptx", SaveFormat.Pptx, presentationOptions);
```

*Por qué es importante:* La llamada a `Save` realiza todo el trabajo pesado: mapear series de Excel a series de PowerPoint, preservar el formato de los ejes y copiar cualquier cuadro de texto vinculado. Después de ejecutar esta línea, tendrás un archivo `.pptx` totalmente editable listo para abrir en Microsoft PowerPoint.

### Verificar el resultado

Abre `Result.pptx` en PowerPoint. Deberías ver una diapositiva que contiene:

- El gráfico original, todavía vinculado a sus datos (puedes hacer doble clic para editar las series).
- Cualquier cuadro de texto que estaba en la hoja de Excel, ahora un cuadro de texto nativo de PowerPoint.
- La disposición de la diapositiva se elige automáticamente (normalmente una diapositiva en blanco).

Si notas elementos faltantes, verifica que el libro fuente realmente tenía objetos visibles y que `ExportTextBoxes` / `ExportShapes` estaban configurados en `true`.

### Convertir Excel a PowerPoint: manejo de varias hojas de cálculo

A menudo un libro contiene más de una hoja, cada una con su propio gráfico. Por defecto Aspose.Cells exportará **todos** los gráficos de **todas** las hojas en diapositivas separadas. Si solo necesitas un subconjunto, puedes filtrarlos antes de guardar:

```csharp
// Example: Export only charts from the first worksheet
Worksheet firstSheet = workbook.Worksheets[0];
foreach (Chart chart in firstSheet.Charts)
{
    chart.IsVisible = true; // Ensure visibility
}

// Hide charts from other sheets
for (int i = 1; i < workbook.Worksheets.Count; i++)
{
    foreach (Chart chart in workbook.Worksheets[i].Charts)
    {
        chart.IsVisible = false;
    }
}
```

*Consejo profesional:* Establecer `chart.IsVisible = false` es más barato que eliminar el gráfico por completo, y te permite alternar su inclusión sin modificar el archivo fuente.

### Guardar Excel como PowerPoint – Personalizar el tamaño de la diapositiva

PowerPoint usa por defecto una diapositiva de 10 pulgadas por 5.63 pulgadas. Si tu gráfico se ve apretado, puedes cambiar las dimensiones de la diapositiva mediante el objeto `PresentationOptions`:

```csharp
presentationOptions.SlideSize = new SizeF(13.33f, 7.5f); // 16:9 widescreen
```

Ahora el gráfico exportado tendrá más espacio y cualquier cuadro de texto conservará su diseño original.

### Cómo convertir Excel a PPT: manejo de objetos ocultos

Filas, columnas o formas ocultas pueden colarse en la exportación. Para eliminarlas, ejecuta una rápida limpieza antes de guardar:

```csharp
// Remove hidden rows/columns that might affect chart layout
foreach (Worksheet sheet in workbook.Worksheets)
{
    sheet.Cells.HideRows = false;
    sheet.Cells.HideColumns = false;
}
```

Este paso no siempre es necesario, pero evita huecos inesperados en tu presentación final.

### Guardar libro como PPTX – Ejemplo completo funcionando

Juntando todo, aquí tienes un programa de consola listo para ejecutar que demuestra todo el flujo:

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing; // For SizeF

class ExportChartDemo
{
    static void Main()
    {
        // Load workbook (Step 1)
        string sourcePath = @"C:\Samples\ChartWithTextbox.xlsx";
        Workbook workbook = new Workbook(sourcePath);

        // Verify chart existence
        if (workbook.Worksheets[0].Charts.Count == 0)
        {
            Console.WriteLine("No chart found. Exiting.");
            return;
        }

        // Configure presentation options (Step 2)
        PresentationOptions options = new PresentationOptions
        {
            ExportTextBoxes = true,
            ExportShapes    = true,
            SlideSize       = new SizeF(13.33f, 7.5f) // optional widescreen
        };

        // Optional: export only first worksheet charts
        for (int i = 1; i < workbook.Worksheets.Count; i++)
        {
            foreach (Chart c in workbook.Worksheets[i].Charts)
                c.IsVisible = false;
        }

        // Save as PowerPoint (Step 3)
        string targetPath = @"C:\Samples\Result.pptx";
        workbook.Save(targetPath, SaveFormat.Pptx, options);

        Console.WriteLine($"Export complete! File saved to {targetPath}");
    }
}
```

Ejecutar este programa creará `Result.pptx` con un gráfico y un cuadro de texto editables, exactamente lo que esperarías al **guardar libro como pptx** manualmente.

![Ejemplo de exportación de gráfico a PowerPoint](/images/export-chart-to-powerpoint.png "Exportar gráfico a PowerPoint – diapositiva editable")

## Preguntas frecuentes y casos límite

**¿Qué pasa si el archivo Excel contiene un gráfico con una fuente de datos externa vinculada?**  
Aspose.Cells copia los valores *actuales* de los datos al gráfico de PowerPoint. **No** preserva el vínculo externo, porque PowerPoint no puede referenciar una conexión de datos de Excel de la misma manera. Si necesitas actualizaciones en tiempo real, considera incrustar el archivo Excel original en el PPTX como un objeto OLE.

**¿Puedo exportar un gráfico que usa un tema personalizado?**  
Sí. La biblioteca intenta mapear los colores del tema de Excel a los slots del tema de PowerPoint. Para paletas muy personalizadas podrías necesitar ajustar los colores después de la exportación usando la propia API de PowerPoint (p. ej., Aspose.Slides).

**¿Existe un límite en la cantidad de gráficos?**  
Prácticamente ninguno—Aspose.Cells transmite los datos, de modo que incluso un libro con docenas de gráficos se exportará, aunque el tamaño del PPTX resultante crecerá linealmente.

**¿Necesito una licencia para Aspose.Cells?**  
Una evaluación gratuita funciona, pero añade una marca de agua en la primera diapositiva. Para uso en producción, adquiere una licencia adecuada para eliminar la marca de agua y desbloquear el rendimiento completo.

## Resumen

Hemos cubierto cómo **exportar un gráfico a PowerPoint** usando C#, demostrado el código exacto para cargar un libro de Excel, configurar `PresentationOptions` para mantener los cuadros de texto y las formas editables, y finalmente guardar el resultado como un `.pptx`. También aprendiste a **convertir Excel a PowerPoint**, **guardar Excel como PowerPoint**, y a responder la pregunta “**cómo convertir Excel a ppt**” con un ejemplo completo y ejecutable.

## ¿Qué sigue?

- **Guardar libro como PPTX** con múltiples diapositivas: recorre cada hoja de cálculo y llama a `Save` con `PresentationOptions` para cada una.
- Explora **Aspose.Slides** si necesitas modificar programáticamente el PPTX generado (añadir transiciones, notas del orador, etc.).
- Prueba exportar **gráficos dinámicos** o **gráficos 3‑D**—las mismas opciones se aplican, aunque quizá necesites ajustar el formato de los ejes después.

Si encuentras algún inconveniente, deja un comentario abajo o consulta la documentación oficial de Aspose.Cells para ver los últimos cambios de la API. ¡Feliz codificación y disfruta convirtiendo esos gráficos de Excel en presentaciones pulidas de PowerPoint con solo unas líneas de C#!

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}