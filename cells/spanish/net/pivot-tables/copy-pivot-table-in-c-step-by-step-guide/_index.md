---
category: general
date: 2026-03-18
description: Copiar tabla dinámica en C# con Aspose.Cells. Aprende cómo copiar un
  rango de Excel, duplicar una tabla dinámica de Excel, copiar un rango a una nueva
  hoja y copiar la tabla dinámica a una hoja en minutos.
draft: false
keywords:
- copy pivot table
- copy excel range
- duplicate excel pivot
- copy range to new
- copy pivot to sheet
language: es
og_description: Copiar tabla dinámica en C# usando Aspose.Cells. Aprende a duplicar
  una tabla dinámica de Excel, copiar un rango de Excel a una nueva ubicación y copiar
  la tabla dinámica a una hoja con ejemplos de código completos.
og_title: Copiar tabla dinámica en C# – Guía completa de programación
tags:
- Aspose.Cells
- C#
- Excel automation
title: Copiar tabla dinámica en C# – Guía paso a paso
url: /es/net/pivot-tables/copy-pivot-table-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Copiar tabla dinámica en C# – Guía completa de programación

¿Alguna vez necesitaste **copy pivot table** de una parte de un libro de trabajo a otra, pero no estabas seguro de cómo hacerlo sin perder las conexiones de datos subyacentes? No estás solo. Muchos desarrolladores se encuentran con este problema al automatizar informes de Excel, especialmente cuando la tabla dinámica está dentro de un bloque de datos más grande. ¿La buena noticia? Con Aspose.Cells puedes copiar la tabla dinámica **exactamente como aparece**, y también aprenderás a **copy excel range**, **duplicate excel pivot**, e incluso **copy pivot to sheet** con solo unas pocas líneas de C#.

En este tutorial recorreremos un escenario del mundo real: mover una tabla dinámica que ocupa *A1:J20* a una nueva área *M1:V20* en la misma hoja de cálculo. Al final tendrás un programa ejecutable, comprenderás por qué cada paso es importante y sabrás cómo adaptar el código para otros rangos o incluso hojas de cálculo separadas. No se necesitan documentos externos—todo está aquí.

---

## Requisitos previos

- **Aspose.Cells for .NET** (versión 23.9 o posterior). Puedes obtenerlo vía NuGet: `Install-Package Aspose.Cells`.
- Un entorno básico de desarrollo C# (Visual Studio 2022, Rider o VS Code con la extensión C#).
- Un archivo Excel (`source.xlsx`) que contiene una tabla dinámica dentro del rango *A1:J20*.

Eso es todo. Si te sientes cómodo creando una aplicación de consola, estás listo para comenzar.

---

## Cómo copiar tabla dinámica en Aspose.Cells

El núcleo de la solución es una única llamada a `Worksheet.Cells.CopyRange`. Este método no solo copia los valores de celda sin procesar, sino que también preserva tablas dinámicas, gráficos y otros objetos enriquecidos automáticamente. Desglosémoslo.

### Paso 1: Cargar el libro de trabajo fuente

Primero necesitamos cargar el libro de trabajo en memoria.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Load the source workbook from disk
        Workbook sourceWorkbook = new Workbook(@"YOUR_DIRECTORY\source.xlsx");
```

> **Por qué es importante:** Cargar el libro de trabajo crea una representación en memoria que Aspose.Cells puede manipular sin iniciar Excel. Es rápido, seguro para subprocesos y funciona en servidores.

### Paso 2: Obtener la primera hoja de cálculo

La mayoría de los ejemplos usan la primera hoja, pero puedes apuntar a cualquier índice o nombre.

```csharp
        // Access the first worksheet (index 0)
        Worksheet worksheet = sourceWorkbook.Worksheets[0];
```

> **Consejo:** Si necesitas **copy pivot to sheet** en lugar de la misma hoja, simplemente cambia la referencia `worksheet` a otro objeto `Worksheet`.

### Paso 3: Definir los rangos de origen y destino

Usaremos estructuras `CellArea` para describir los bloques que estamos moviendo.

```csharp
        // Define the source range (A1:J20) that contains the pivot table
        CellArea sourceRange = new CellArea(0, 0, 19, 9);   // rows 0‑19, columns 0‑9

        // Define the target range (M1:V20) where the data will be copied
        CellArea targetRange = new CellArea(0, 12, 19, 21); // rows 0‑19, columns 12‑21
```

> **Explicación:** Los índices de filas y columnas comienzan en cero. Columna 0 = **A**, columna 12 = **M**, etc. Ajusta estos números si tu tabla dinámica está en otro lugar.

### Paso 4: Ejecutar la operación de copia

Ahora ocurre la magia. Establecer el último parámetro booleano a `true` indica a Aspose.Cells que copie todos los objetos, incluida la tabla dinámica.

```csharp
        // Copy the source range to the target range; pivot tables are copied automatically
        worksheet.Cells.CopyRange(
            sourceRange.StartRow, sourceRange.StartColumn,
            sourceRange.EndRow, sourceRange.EndColumn,
            targetRange.StartRow, targetRange.StartColumn,
            true);
```

> **¿Por qué `true`?** La bandera indica “copiar todos los objetos”. Si la estableces en `false`, solo se moverán los valores de celda simples y la tabla dinámica se perderá.

### Paso 5: Guardar el libro de trabajo

Finalmente, escribe el libro de trabajo modificado de nuevo en disco.

```csharp
        // Save the workbook with the copied range
        sourceWorkbook.Save(@"YOUR_DIRECTORY\copy-pivot.xlsx");
    }
}
```

> **Resultado:** `copy-pivot.xlsx` ahora contiene la tabla dinámica original en *A1:J20* **y** una copia idéntica en *M1:V20*. Abre el archivo en Excel para verificar que ambas tablas dinámicas son funcionales y conservan sus conexiones de datos.

---

## Copiar rango de Excel a una nueva ubicación – una variación rápida

A veces solo necesitas **copy excel range** sin preocuparte por las tablas dinámicas. El mismo método `CopyRange` hace el truco; simplemente establece el último argumento a `false`.

```csharp
worksheet.Cells.CopyRange(
    sourceRange.StartRow, sourceRange.StartColumn,
    sourceRange.EndRow, sourceRange.EndColumn,
    targetRange.StartRow, targetRange.StartColumn,
    false); // plain values only
```

> **Cuándo usar:** Si estás moviendo datos sin procesar para una hoja de cálculo temporal, desactivar la copia de objetos ahorra memoria y acelera la operación.

---

## Duplicar tabla dinámica de Excel en varias hojas

¿Qué pasa si deseas **duplicate excel pivot** en una hoja de cálculo diferente? El patrón sigue siendo el mismo; simplemente haces referencia a otro `Worksheet` para el destino.

```csharp
// Assume we have a second sheet already created
Worksheet destSheet = sourceWorkbook.Worksheets.Add("PivotCopy");

// Copy the pivot (and its data source) to the new sheet starting at A1
destSheet.Cells.CopyRange(
    sourceRange.StartRow, sourceRange.StartColumn,
    sourceRange.EndRow, sourceRange.EndColumn,
    0, 0, // destination at A1
    true);
```

> **Caso límite:** Si la tabla dinámica de origen usa una tabla que está en la hoja original, Aspose.Cells también copiará la definición de tabla subyacente, asegurando que la nueva tabla dinámica funcione de inmediato.

---

## Errores comunes y cómo evitarlos

| Pitfall | Why it happens | Fix |
|---------|----------------|-----|
| **Pivot pierde su caché** | Usar `CopyRange` con `false` o una rutina de copia personalizada que ignora los objetos. | Siempre pasa `true` cuando necesitas la propia tabla dinámica. |
| **Las celdas de destino ya contienen datos** | Sobrescribe silenciosamente, potencialmente corrompiendo fórmulas existentes. | Limpia primero el área de destino: `worksheet.Cells.ClearRange(targetRange.StartRow, targetRange.StartColumn, targetRange.EndRow, targetRange.EndColumn, true);` |
| **El rango de origen no incluye toda la tabla dinámica** | Las tablas dinámicas abarcan más filas/columnas de lo que esperas (p. ej., filas ocultas). | Usa `worksheet.PivotTables[0].DataRange` para obtener programáticamente los límites exactos. |
| **Copiar entre libros de trabajo** | `CopyRange` solo funciona dentro del mismo libro de trabajo. | Usa `sourceWorksheet.Cells.CopyRange` a un rango temporal, luego `destWorkbook.Worksheets.AddCopy(sourceWorksheet);` |

---

## Resultado esperado y verificación

Después de ejecutar el programa:

1. Abre `copy-pivot.xlsx`.
2. Verás dos tablas dinámicas idénticas—una en **A1:J20**, otra en **M1:V20**.
3. Actualiza cualquier tabla dinámica; ambas deberían reflejar los mismos datos subyacentes.
4. Si la duplicaste en otra hoja, la nueva hoja contendrá también una copia funcional.

Una forma rápida de verificar mediante código:

```csharp
int pivotCount = worksheet.PivotTables.Count; // should be 2 after copy
Console.WriteLine($"Pivot tables on the sheet: {pivotCount}");
```

---

## Consejo profesional: Automatizar la detección de rangos

Codificar manualmente `CellArea` funciona para informes estáticos, pero el código de producción a menudo necesita localizar la tabla dinámica de forma dinámica.

```csharp
// Find the first pivot table on the sheet
PivotTable pt = worksheet.PivotTables[0];
CellArea ptRange = pt.DataRange;

// Use the detected range for copying
worksheet.Cells.CopyRange(
    ptRange.StartRow, ptRange.StartColumn,
    ptRange.EndRow, ptRange.EndColumn,
    targetRange.StartRow, targetRange.StartColumn,
    true);
```

> **¿Por qué molestarse?** Esto hace que tu solución sea resistente a cambios de diseño—no más errores de “Ups, la tabla dinámica se movió a B2”.

![copy pivot table example](copy-pivot.png){alt="ejemplo de copiar tabla dinámica"}

*La captura de pantalla (marcador de posición) muestra la tabla dinámica original a la izquierda y la duplicada a la derecha.*

---

## Recapitulación

Acabamos de cubrir cómo **copy pivot table** en C# usando Aspose.Cells, exploramos formas de **copy excel range**, **duplicate excel pivot**, e incluso **copy pivot to sheet** entre hojas de cálculo. Los puntos clave son:

- Usa `Worksheet.Cells.CopyRange` con la bandera `true` para preservar objetos enriquecidos.
- Define objetos `CellArea` de origen y destino con índices basados en cero.
- Ajusta la hoja de destino si necesitas **copy pivot to sheet**.
- Ten en cuenta casos límite como datos existentes, filas ocultas y escenarios entre libros de trabajo.

## ¿Qué sigue?

- **Dynamic pivot discovery**: Construye un asistente que escanee un libro de trabajo en busca de todas las tablas dinámicas y las replique automáticamente.
- **Export to PDF/HTML**: Después de copiar, podrías querer renderizar la hoja a un formato de informe—Aspose.Cells también lo maneja.
- **Performance tuning**: Para libros de trabajo masivos, considera desactivar el cálculo antes de copiar y volver a activarlo después.

Siéntete libre de experimentar: cambia las coordenadas de destino, copia a un libro de trabajo nuevo, o incluso recorre varias hojas de cálculo para crear un informe consolidado. Las posibilidades son infinitas, y con la base que ahora tienes, podrás adaptar el código a prácticamente cualquier tarea de automatización de Excel.

¡Feliz codificación, y que tus tablas dinámicas siempre permanezcan perfectamente sincronizadas!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}