---
category: general
date: 2026-06-30
description: Crea una línea sparkline en Excel con C# rápidamente. Aprende cómo agregar
  sparkline, crear un libro de Excel con C# y añadir sparkline a una celda en unos
  pocos pasos.
draft: false
keywords:
- create line sparkline
- how to add sparkline
- add line sparkline
- create excel workbook c#
- add sparkline to cell
language: es
og_description: Crear una sparkline de línea en Excel con C#. Este tutorial muestra
  cómo agregar una sparkline, crear un libro de Excel con C# e incrustar la sparkline
  en una celda.
og_title: Crear sparkline de línea en Excel con C# – Guía paso a paso
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Create line sparkline in Excel with C# quickly. Learn how to add sparkline,
    create Excel workbook C#, and add sparkline to cell in a few steps.
  headline: Create line sparkline in Excel with C# – Complete Programming Guide
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
title: Crear sparkline de línea en Excel con C# – Guía completa de programación
url: /es/net/charts/create-line-sparkline-in-excel-with-c-complete-programming-g/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crear sparkline de línea en Excel con C# – Guía completa de programación

¿Alguna vez te has preguntado cómo **crear sparkline de línea** en un archivo Excel usando C#? No eres el único—los desarrolladores preguntan constantemente, “¿cómo añado un sparkline a un informe sin abrir Excel manualmente?” La buena noticia es que con unas pocas líneas de código puedes generar un elegante sparkline de línea directamente dentro del libro, sin necesidad de UI.

En este tutorial repasaremos todo lo que necesitas saber: desde los conceptos básicos de **create Excel workbook C#**, pasando por la población de datos, hasta los pasos exactos para **add line sparkline** y **add sparkline to cell**. Al final tendrás un archivo *.xlsx* listo para usar que visualiza las tendencias de ventas mensuales de un vistazo. Sin rodeos, solo una solución práctica y ejecutable.

---

## Qué vas a construir

- Un nuevo libro de Excel llamado *KPI_Sparklines.xlsx*  
- Una hoja de cálculo llamada **KPI** que contiene números de ventas de muestra  
- Un **sparkline de línea** colocado en la celda **D2** que hace referencia al rango de datos **B2:B13**  
- Formato básico (color, grosor de línea) para que el sparkline destaque  

¿Requisitos previos? Solo el .NET SDK (3.1+ o .NET 6) y la biblioteca gratuita Aspose.Cells for .NET (disponible vía NuGet). Si nunca has usado Aspose.Cells, piénsalo como un motor de Excel potente que puedes invocar desde código—sin interop COM, sin necesidad de instalar Excel.

---

![ejemplo de código para crear sparkline de línea en Excel usando C#](https://example.com/images/create-line-sparkline.png "Crear sparkline de línea en Excel con C#")

*Texto alternativo de la imagen: ejemplo de código para crear sparkline de línea en Excel usando C#*

---

## Paso 1: **Create Excel workbook C#** – Configura el archivo y la hoja de cálculo

Lo primero. Necesitamos un objeto workbook y una hoja de cálculo donde vivirán los datos. Esta es la base para cualquier automatización de Excel, ya sea que después **add line sparkline** o escribas fórmulas.

```csharp
using Aspose.Cells;
using System.Drawing;

// Initialize a new workbook
Workbook workbook = new Workbook();

// Grab the first worksheet (index 0) and give it a meaningful name
Worksheet worksheet = workbook.Worksheets[0];
worksheet.Name = "KPI";   // “KPI” will hold our key performance indicators
```

> **Por qué es importante:** La clase `Workbook` representa todo el archivo, mientras que `Worksheet` es el lienzo para filas, columnas y, eventualmente, nuestro sparkline. Nombrar la hoja desde el principio mantiene el archivo ordenado y auto‑documentado.

---

## Paso 2: Poblar datos – El rango de origen para el sparkline

Un sparkline necesita datos para trazarse. Simularemos 12 meses de cifras de ventas. Podrías obtenerlos de una base de datos, pero para mayor claridad los generaremos al vuelo.

```csharp
// Fill column B (index 1) with monthly sales numbers
for (int month = 0; month < 12; month++)
{
    // Example pattern: start at 5,000 and increase by 750 each month
    worksheet.Cells[month + 1, 1].PutValue(5000 + month * 750);
}
```

> **Consejo:** `PutValue` detecta automáticamente el tipo de dato, así que no necesitas convertir a `double` o `int`. Si alguna vez necesitas formatear las celdas (moneda, separadores de miles), puedes aplicar un objeto `Style` más adelante.

---

## Paso 3: **Create line sparkline** – Añade el sparkline a una celda específica

Ahora llega la estrella del espectáculo: el **sparkline de línea**. Aspose.Cells agrupa los sparklines, así que primero creamos un `SparklineGroup` de tipo `Line`, y luego indicamos dónde colocar la visualización.

```csharp
// Add a new SparklineGroup of type Line
int groupIndex = worksheet.SparklineGroups.Add(SparklineType.Line);
SparklineGroup sparklineGroup = worksheet.SparklineGroups[groupIndex];

// Add a sparkline that lives in D2 (row 1, column 3) and reads data from B2:B13
// Parameters: firstRow, firstColumn, lastRow, lastColumn, firstDataRow, lastDataRow
sparklineGroup.Add(1, 3, 1, 3, 1, 12);   // D2 ↔ B2:B13
```

> **Cómo funciona:**  
> - `firstRow/firstColumn` y `lastRow/lastColumn` definen la *celda objetivo* (donde aparece el sparkline).  
> - `firstDataRow/lastDataRow` apuntan al rango de origen.  
> Como estamos usando un **sparkline de línea**, la visual será una simple línea delgada que sigue la tendencia de los números.

### Opcional: **How to add sparkline** con estilo personalizado

Si deseas que el sparkline destaque, ajusta un par de propiedades:

```csharp
sparklineGroup.LineWeight = 1.0;               // Thickness of the line
sparklineGroup.SeriesColor = Color.DarkBlue;  // Color of the sparkline line
sparklineGroup.ShowMarkers = true;             // Show data markers (optional)
sparklineGroup.MarkerColor = Color.OrangeRed;  // Marker color
```

> **¿Por qué estilizarlo?** Una línea azul oscuro sobre fondo blanco es fácil para la vista, mientras que los marcadores dan una pista rápida sobre los puntos de datos individuales—útil para presentaciones.

---

## Paso 4: Guardar el libro – Verifica el resultado

Con el sparkline en su lugar, solo necesitamos escribir el archivo en disco. Elige una carpeta donde tengas permiso de escritura; el ejemplo usa una ruta de marcador de posición que deberás reemplazar.

```csharp
// Save the workbook as an .xlsx file
string outputPath = @"C:\Temp\KPI_Sparklines.xlsx";
workbook.Save(outputPath);
```

> **Verificación:** Abre el archivo generado en Excel (o cualquier visor que soporte .xlsx). Deberías ver un **sparkline de línea** en la celda **D2** que refleja el aumento de las ventas en la columna **B**. Al pasar el cursor sobre el sparkline aparecerá una información emergente con los valores subyacentes.

---

## Paso 5: Problemas comunes al **add sparkline to cell**

Incluso un ejemplo sencillo puede causar tropiezos a los principiantes. Aquí tienes algunas cosas a vigilar:

| Problema | Por qué ocurre | Solución |
|----------|----------------|----------|
| Coordenadas de celda incorrectas | El objetivo del sparkline usa índice de columna basado en cero pero índice de fila basado en uno. | Recuerda `Cells[row, column]` donde `row` es basado en cero y `column` también basado en cero. En `SparklineGroup.Add`, filas y columnas son **basadas en 1**. |
| No se muestra datos | El rango de origen está vacío o contiene valores no numéricos. | Asegúrate de que el rango (p. ej., `B2:B13`) contenga números. Usa `PutValue` con tipos numéricos. |
| El sparkline desaparece después de guardar | Incompatibilidad de versión de la biblioteca o licencia faltante. | Usa la última versión del paquete Aspose.Cells y proporciona una licencia válida si superas los límites de evaluación. |
| El formato no se aplica | Los cambios de estilo se hicieron antes de añadir el sparkline. | Aplica el estilo **después** de crear el grupo, como se muestra arriba. |

---

## Código fuente completo – Copia‑pega todo en uno

A continuación tienes el programa completo, listo para ejecutar. Pégalo en un nuevo proyecto de consola, agrega el paquete NuGet Aspose.Cells y pulsa **F5**.

```csharp
using Aspose.Cells;
using System.Drawing;

namespace SparklineDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // Step 1: Create Excel workbook C#
            // -------------------------------------------------
            Workbook workbook = new Workbook();
            Worksheet worksheet = workbook.Worksheets[0];
            worksheet.Name = "KPI";

            // -------------------------------------------------
            // Step 2: Populate monthly sales data (B2:B13)
            // -------------------------------------------------
            for (int month = 0; month < 12; month++)
            {
                worksheet.Cells[month + 1, 1].PutValue(5000 + month * 750);
            }

            // -------------------------------------------------
            // Step 3: Create line sparkline and add it to D2
            // -------------------------------------------------
            int groupIdx = worksheet.SparklineGroups.Add(SparklineType.Line);
            SparklineGroup sparklineGroup = worksheet.SparklineGroups[groupIdx];
            sparklineGroup.Add(1, 3, 1, 3, 1, 12); // D2 ↔ B2:B13

            // -------------------------------------------------
            // Step 4: Optional formatting (how to add sparkline with style)
            // -------------------------------------------------
            sparklineGroup.LineWeight = 1.0;
            sparklineGroup.SeriesColor = Color.DarkBlue;
            sparklineGroup.ShowMarkers = true;
            sparklineGroup.MarkerColor = Color.OrangeRed;

            // -------------------------------------------------
            // Step 5: Save the workbook
            // -------------------------------------------------
            string outputPath = @"C:\Temp\KPI_Sparklines.xlsx";
            workbook.Save(outputPath);

            System.Console.WriteLine($"Workbook saved to {outputPath}");
        }
    }
}
```

**Salida esperada:** Al abrir *KPI_Sparklines.xlsx*, la columna **B** muestra doce números (5,000 → 13,250) y la celda **D2** contiene un suave sparkline de línea azul oscuro que sube de forma constante. Los marcadores aparecen como pequeños puntos naranja‑rojo si activaste `ShowMarkers`.

---

## ¿Qué sigue? Amplía tus habilidades con sparklines

Ahora que dominas **create line sparkline** con Aspose.Cells, considera explorar estos temas relacionados:

- **Add column sparkline** – perfecto para mostrar datos apilados.  
- **Create multi‑sparkline groups** en la misma hoja para comparaciones lado a lado.  
- **Export to PDF** manteniendo los sparklines (Aspose.Cells soporta conversión a PDF).  
- **Dynamic data sources** – extrae cifras reales de ventas desde una base de datos SQL en lugar de valores codificados.  

Cada uno de estos se basa en los mismos conceptos centrales: **create Excel workbook C#**, poblar datos y **add sparkline to cell** con el estilo deseado.

---

### TL;DR

Mostramos cómo **create line sparkline** en un libro de Excel usando C#. Los pasos—*crear libro, rellenar datos, añadir sparkline, estilizar y guardar*—están todos encapsulados en un único programa autocontenido. Siéntete libre de ajustar colores, grosor de línea o rango de origen para que coincidan con tus necesidades de reporte.

¿Tienes alguna variante que quieras compartir? Deja un comentario abajo, ¡y feliz codificación!

## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y explicaciones paso a paso para ayudarte a dominar funciones adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Excel Automation: Create a Workbook and Add a ListBox Using Aspose.Cells for .NET](/cells/english/net/automation-batch-processing/excel-automation-create-workbook-add-listbox-aspose-cells/)
- [Excel Automation Create Workbook Add Listbox Aspose Cells](/cells/german/net/automation-batch-processing/excel-automation-create-workbook-add-listbox-aspose-cells/)
- [Excel Automation Create Workbook Add Listbox Aspose Cells](/cells/french/net/automation-batch-processing/excel-automation-create-workbook-add-listbox-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}