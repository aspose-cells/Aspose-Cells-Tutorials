---
category: general
date: 2026-06-27
description: Copiar tabla dinámica a otra hoja en C# usando Aspose.Cells. Aprende
  paso a paso cómo preservar los datos y el formato de la tabla dinámica.
draft: false
keywords:
- copy pivot table to another sheet
- Aspose.Cells copy pivot
- Excel pivot duplication
- preserve pivot formatting
- copy range with pivot
language: es
og_description: Copiar tabla dinámica a otra hoja en C# con Aspose.Cells. Este tutorial
  muestra exactamente cómo duplicar una tabla dinámica manteniendo su formato intacto.
og_title: Copiar tabla dinámica a otra hoja – Guía completa de C#
schemas:
- author: Aspose
  dateModified: '2026-06-27'
  description: Copy pivot table to another sheet in C# using Aspose.Cells. Learn step‑by‑step
    how to preserve pivot data and formatting.
  headline: Copy Pivot Table to Another Sheet – Complete C# Guide
  type: TechArticle
tags:
- Excel automation
- C#
- Aspose.Cells
title: Copiar tabla dinámica a otra hoja – Guía completa de C#
url: /es/net/pivot-tables/copy-pivot-table-to-another-sheet-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Copiar tabla dinámica a otra hoja – Guía completa en C#

¿Alguna vez necesitaste **copiar tabla dinámica a otra hoja** pero temías perder los segmentadores, campos calculados o el formato? No estás solo. Muchos desarrolladores se encuentran con ese problema al automatizar informes de Excel, y la frustración es real. En esta guía recorreremos una solución limpia, de extremo a extremo, que **preserva la tabla dinámica** tal como aparece.

Utilizaremos **Aspose.Cells for .NET**, una biblioteca potente que permite manipular archivos de Excel sin abrir Excel. Al final de este tutorial tendrás un fragmento de C# listo para ejecutar que copia una tabla dinámica de una hoja a otra, manteniendo todas las conexiones de datos subyacentes intactas.

## Qué cubre este tutorial

- Configurar un proyecto .NET y agregar el paquete NuGet de Aspose.Cells.  
- Cargar un libro de trabajo existente que ya contiene una tabla dinámica.  
- Definir tanto el rango de origen (la tabla dinámica original) como el rango de destino en una hoja diferente.  
- Usar `CopyOptions` para **preservar la tabla dinámica** al copiar.  
- Guardar el resultado y verificar que la tabla dinámica funciona en su nueva ubicación.  

Sin herramientas externas, sin copiar‑pegar manual, y sin trucos ocultos—solo código sencillo que puedes insertar en cualquier aplicación o servicio de consola C#.

> **Por qué deberías importarte:** Automatizar la duplicación de tablas dinámicas ahorra horas de trabajo manual, especialmente en pipelines de informes nocturnos donde decenas de libros de trabajo necesitan estructuras de tabla dinámica idénticas en múltiples hojas.

---

## Paso 1: Configurar el proyecto y agregar Aspose.Cells

Lo primero. Si aún no lo has hecho, crea un nuevo proyecto de consola .NET:

```bash
dotnet new console -n PivotCopyDemo
cd PivotCopyDemo
```

Ahora agrega el paquete Aspose.Cells:

```bash
dotnet add package Aspose.Cells
```

> **Consejo profesional:** Usa la última versión estable (a partir de junio 2026 v23.12). Incluye correcciones de errores para el manejo de `CopyPivotTable`.

## Paso 2: Cargar el libro de trabajo y acceder a las hojas

Abre el libro de trabajo que contiene la tabla dinámica de origen. En la mayoría de los escenarios reales el archivo está en una unidad compartida, pero para esta demostración asumiremos que está en una carpeta local llamada `YOUR_DIRECTORY`.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Load the workbook containing the source pivot table
        Workbook workbook = new Workbook("YOUR_DIRECTORY/source.xlsx");

        // Step 2: Access the first worksheet (source sheet)
        Worksheet sourceSheet = workbook.Worksheets[0];

        // We'll also create (or reference) a destination sheet
        Worksheet destSheet = workbook.Worksheets.Add("CopyDestination");
```

Aquí creamos una nueva hoja llamada **CopyDestination** donde se colocará la tabla dinámica. Si ya tienes una hoja de destino, simplemente obténla por índice o nombre.

## Paso 3: Definir los rangos de origen y destino

Una tabla dinámica reside dentro de un bloque rectangular de celdas. Necesitas indicar a Aspose.Cells qué bloque copiar. En este ejemplo la tabla dinámica ocupa las filas 0‑20 y columnas 0‑10 (indexación basada en cero).

```csharp
        // Step 3: Define the source range that includes the pivot table (rows 0‑20, columns 0‑10)
        CellArea sourceRange = new CellArea(0, 0, 20, 10);

        // Step 4: Define the destination start cell (row 30, column 0) on the destination sheet
        // and calculate the target area size to match the source dimensions
        CellArea destinationRange = new CellArea(
            30,                                 // start row on destination sheet
            0,                                  // start column
            30 + sourceRange.RowCount - 1,     // end row (same height as source)
            sourceRange.ColumnCount - 1        // end column (same width as source)
        );
```

Observa cómo calculamos la fila y columna final de forma dinámica. De esta manera, incluso si más adelante cambias el tamaño del rango de origen, el destino se ajustará automáticamente.

## Paso 4: Realizar la copia preservando la tabla dinámica

Ahora ocurre la magia. Al pasar un objeto `CopyOptions` con `CopyPivotTable = true`, Aspose.Cells sabe mantener la definición de la tabla dinámica intacta.

```csharp
        // Step 5: Copy the range, preserving the pivot table
        destSheet.Cells.CopyRange(
            sourceRange,
            destinationRange,
            new CopyOptions { CopyPivotTable = true }
        );
```

Internamente, Aspose.Cells recrea la caché de la tabla dinámica, actualiza la referencia de la fuente de datos y vuelve a aplicar cualquier formato. Esta es la **duplicación de tabla dinámica en Excel** que estabas buscando.

## Paso 5: Guardar y verificar el resultado

Finalmente, escribe el libro de trabajo de nuevo en disco. Puedes mantener el archivo original sin tocar guardándolo con un nuevo nombre.

```csharp
        // Step 6: Save the workbook with the copied pivot table
        workbook.Save("YOUR_DIRECTORY/copy-pivot.xlsx");

        // Optional: open the file automatically (Windows only)
        System.Diagnostics.Process.Start(new System.Diagnostics.ProcessStartInfo
        {
            FileName = "YOUR_DIRECTORY/copy-pivot.xlsx",
            UseShellExecute = true
        });
    }
}
```

Abre el `copy-pivot.xlsx` resultante y verás la tabla dinámica replicada perfectamente en la hoja **CopyDestination**, completa con segmentadores, campos calculados y formato. La fuente de datos subyacente sigue apuntando a la tabla original, por lo que la actualización funciona exactamente como antes.

> **¿Qué pasa si la tabla dinámica de origen abarca un rango dinámico?**  
> Usa `Worksheet.PivotTables[0].CacheDefinition.SourceData` para obtener los límites reales, luego construye `sourceRange` a partir de esa información. Esto maneja casos donde filas o columnas pueden expandirse con el tiempo.

## Bonus: Preservar el formato de la tabla dinámica al copiar

A veces la copia predeterminada pierde el formato condicional o los formatos de número personalizados. Para evitarlo, amplía el `CopyOptions`:

```csharp
        var options = new CopyOptions
        {
            CopyPivotTable = true,
            CopyFormatting = true,      // copies cell styles, colors, fonts
            CopyConditionalFormatting = true
        };
        destSheet.Cells.CopyRange(sourceRange, destinationRange, options);
```

Habilitar `CopyFormatting` garantiza que se cumpla el requisito de **preservar el formato de la tabla dinámica**, dándote un duplicado pixel‑perfecto.

## Resultado esperado

Al ejecutar el programa, la consola terminará silenciosamente (a menos que agregues registro). Al abrir `copy-pivot.xlsx` deberías ver:

- Hoja 1: Datos originales y tabla dinámica sin cambios.  
- **CopyDestination**: Una réplica exacta de la tabla dinámica, posicionada a partir de la fila 31 (ya que las filas son basadas en 1 en la interfaz de Excel).  
- Todos los segmentadores y filtros funcionales; al hacer clic en “Refresh” se actualizan ambas tablas dinámicas simultáneamente.

## Conclusión

Acabamos de demostrar cómo **copiar tabla dinámica a otra hoja** usando Aspose.Cells en C#. Los pasos—configurar el proyecto, cargar el libro de trabajo, definir los rangos, copiar con `CopyPivotTable = true` y guardar—forman un patrón fiable que puedes reutilizar en cualquier pipeline de automatización.

Si quieres ir más allá, considera:

- **Duplicación de tabla dinámica en Excel** entre varios libros de trabajo (recorrer archivos).  
- Usar la opción **Aspose.Cells copy range with pivot** para mover tablas dinámicas entre diferentes libros de trabajo.  
- Automatizar actualizaciones con `PivotTable.RefreshData()` después de copiar.

Siéntete libre de experimentar con diferentes rangos de origen, o combinar esta técnica con generación de gráficos para paneles de informes totalmente automatizados. ¿Tienes preguntas? Deja un comentario, ¡y feliz codificación!

---

![Captura de pantalla que muestra la tabla dinámica copiada en una nueva hoja](copy-pivot-screenshot.png "ejemplo de copiar tabla dinámica a otra hoja")

## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que se basan en las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y funcionales con explicaciones paso a paso para ayudarte a dominar características adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Cómo cambiar los datos de origen de una tabla dinámica usando Aspose.Cells para .NET | Guía de análisis de datos](/cells/english/net/data-analysis/change-pivot-table-source-aspose-cells-net/)
- [Dominar el formato de tablas dinámicas en .NET usando Aspose.Cells](/cells/english/net/formatting/format-pivot-tables-dotnet-aspose-cells/)
- [Acceder a fuentes de datos externas de tablas dinámicas en .NET usando Aspose.Cells](/cells/english/net/data-analysis/access-pivot-table-data-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}