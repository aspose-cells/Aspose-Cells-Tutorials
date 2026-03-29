---
category: general
date: 2026-03-29
description: Aprende cómo copiar rangos, copiar tablas dinámicas, cómo guardar un
  libro de trabajo y cómo cargar un libro de trabajo en C#. Mueve tablas dinámicas
  fácilmente con código paso a paso.
draft: false
keywords:
- how to copy range
- copy pivot tables
- how to save workbook
- how to load workbook
- move pivot table
language: es
og_description: Cómo copiar rangos, copiar tablas dinámicas, cómo guardar un libro
  de trabajo y cómo cargar un libro de trabajo en C#. Mueve las tablas dinámicas sin
  esfuerzo con un código claro.
og_title: Cómo copiar un rango con tablas dinámicas en C# – Guía completa
tags:
- C#
- Aspose.Cells
- Excel automation
title: Cómo copiar un rango con tablas dinámicas en C# – Guía completa
url: /es/net/pivot-tables/how-to-copy-range-with-pivot-tables-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo copiar un rango con tablas dinámicas en C# – Guía completa

¿Alguna vez te has preguntado **cómo copiar un rango** que contiene una tabla dinámica sin romper el vínculo con sus datos de origen? No eres el único. En muchos proyectos del mundo real me he topado con este mismo problema: los archivos de Excel llegan con tablas dinámicas sofisticadas y el requisito es reubicarlas o duplicar los datos en otro lugar.  

¿La buena noticia? La solución es bastante directa una vez que sabes **cómo cargar el libro**, hacer una copia y luego **cómo guardar el libro** nuevamente. En este tutorial recorreremos todo el proceso, incluyendo cómo **copiar tablas dinámicas**, y hasta un consejo rápido sobre **mover tabla dinámica** si la necesitas en otra parte de la misma hoja.

Al final de esta guía tendrás un fragmento de C# totalmente funcional que:

1. Carga un archivo Excel existente.  
2. Copia un rango (incluida la tabla dinámica) a una nueva ubicación.  
3. Guarda el libro modificado en un nuevo archivo.

Sin scripts externos, sin manipulaciones manuales—solo código limpio y reutilizable.

---

## Requisitos previos

- **.NET 6+** (cualquier versión reciente funciona).  
- **Aspose.Cells for .NET** – la biblioteca que proporciona `Workbook`, `WorksheetCopyOptions`, etc. Puedes instalarla vía NuGet:

```bash
dotnet add package Aspose.Cells
```

- Un libro de entrada (`input.xlsx`) que ya contiene una tabla dinámica en el rango `A1:G20`.  
- Familiaridad básica con C# y Visual Studio (o tu IDE favorito).

> **Consejo profesional:** Si utilizas una biblioteca de Excel diferente (p. ej., EPPlus), los conceptos son los mismos—solo cambia las llamadas a la API.

---

## Paso 1 – Cómo cargar el libro (Configuración primaria)

Antes de poder copiar cualquier cosa, necesitamos cargar el archivo Excel en memoria.

```csharp
using Aspose.Cells;

// Step 1: Load the source workbook
var sourceWorkbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");

// Grab the first worksheet – this is where our pivot lives
var sourceWorksheet = sourceWorkbook.Worksheets[0];
```

**Por qué es importante:**  
Cargar el libro te brinda un modelo de objetos que puedes manipular. Sin `cómo cargar el libro` correctamente, cualquier operación de copia posterior lanzará una excepción *FileNotFound* o *InvalidOperation*.  

> **Cuidado:** Si el archivo es grande, considera usar `LoadOptions` con `MemorySetting` para controlar el uso de memoria.

---

## Paso 2 – Cómo copiar el rango (incluida la tabla dinámica)

Ahora llega la estrella del espectáculo: copiar un rango que contiene una tabla dinámica. El método `CopyRange`, combinado con `WorksheetCopyOptions`, realiza el trabajo pesado.

```csharp
// Step 2: Copy a range that includes a pivot table to a new location
sourceWorksheet.CopyRange(
    "A1:G20",                                   // Source range
    new WorksheetCopyOptions { CopyPivotTables = true }, // Ensure pivot tables travel with the data
    sourceWorksheet,                           // Destination worksheet (same sheet in this case)
    "A25");                                     // Upper‑left corner of the destination
```

**Por qué establecemos `CopyPivotTables = true`:**  
Por defecto, copiar un rango solo mueve las celdas crudas. La caché de la tabla dinámica queda atrás, y la tabla copiada se convierte en una tabla estática. Establecer `CopyPivotTables` preserva la conexión en vivo, de modo que la tabla duplicada sigue actualizándose cuando cambian sus datos de origen.

**Caso límite:** Si el rango de destino se superpone al origen, Aspose.Cells lanzará una `ArgumentException`. Siempre elige un objetivo que no se superponga, o crea una nueva hoja primero.

---

## Paso 3 – Cómo guardar el libro (Persistir los cambios)

Después de la copia, querrás escribir los cambios en disco. Aquí es donde entra **cómo guardar el libro**.

```csharp
// Step 3: Save the modified workbook to a new file
sourceWorkbook.Save(@"YOUR_DIRECTORY\output.xlsx");
```

**Qué ocurre bajo el capó:**  
`Save` serializa el libro en memoria, incluida la tabla dinámica recién copiada, en un paquete estándar `.xlsx`. Si necesitas otro formato (CSV, PDF, etc.), simplemente cambia la extensión del archivo o usa la sobrecarga que acepta `SaveFormat`.

> **Consejo:** Usa `Workbook.Save(string, SaveOptions)` si necesitas proteger el archivo con una contraseña o establecer otras opciones de exportación.

---

## Ejemplo completo funcionando

Juntándolo todo, aquí tienes el programa completo listo para ejecutar:

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ How to load workbook
        var sourceWorkbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");
        var sourceWorksheet = sourceWorkbook.Worksheets[0];

        // 2️⃣ How to copy range (including pivot tables)
        sourceWorksheet.CopyRange(
            "A1:G20",
            new WorksheetCopyOptions { CopyPivotTables = true },
            sourceWorksheet,
            "A25");

        // 3️⃣ How to save workbook
        sourceWorkbook.Save(@"YOUR_DIRECTORY\output.xlsx");

        Console.WriteLine("✅ Range copied and workbook saved successfully!");
    }
}
```

**Resultado esperado:**  
Abre `output.xlsx`. Verás la tabla dinámica original todavía en `A1:G20`, y una copia idéntica y totalmente funcional que comienza en `A25`. Ambas tablas apuntan a los mismos datos de origen, por lo que actualizar una refresca a la otra.

---

## Preguntas frecuentes y variaciones

### ¿Puedo **mover tabla dinámica** en lugar de copiarla?

Absolutamente. Después de copiar, simplemente elimina el rango original (o usa `sourceWorksheet.Cells.ClearRange(0, 0, 19, 6)`) y luego renombra el rango de destino si es necesario. Esto efectivamente “mueve” la tabla dinámica.

### ¿Qué pasa si la tabla dinámica usa una fuente de datos externa?

`CopyPivotTables = true` copia solo la definición de la tabla dinámica, no la conexión externa en sí. Asegúrate de que el libro de destino tenga acceso a la misma fuente de datos, o recrea la conexión después de la copia.

### ¿Cómo copio a una **hoja de cálculo diferente**?

Simplemente pasa el objeto de hoja de destino en lugar de `sourceWorksheet`:

```csharp
var destWorksheet = sourceWorkbook.Worksheets.Add("CopiedPivot");
sourceWorksheet.CopyRange("A1:G20", new WorksheetCopyOptions { CopyPivotTables = true }, destWorksheet, "A1");
```

### ¿Existe una forma de copiar **varios rangos** a la vez?

Puedes llamar a `CopyRange` repetidamente o usar `CopyRows`/`CopyColumns` para bloques más grandes. Recorrer una lista de cadenas de direcciones es un enfoque limpio.

---

## Errores comunes y consejos profesionales

- **Tamaño de la caché de la tabla dinámica:** Las cachés grandes pueden inflar el tamaño del libro. Si solo necesitas los datos mostrados, considera `CopyPivotTables = false` y luego usa `PivotTable.RefreshData()` en el destino.
- **Rutas de archivo:** Usa `Path.Combine` para evitar separadores codificados, especialmente en .NET multiplataforma.
- **Rendimiento:** Para libros masivos, envuelve la copia en un `using (var stream = new MemoryStream())` y guarda primero en el flujo, luego escribe en disco. Esto reduce la sobrecarga de I/O.

---

## Conclusión

Ahora sabes **cómo copiar un rango** que contiene una tabla dinámica, cómo **copiar tablas dinámicas**, y los pasos exactos para **cómo cargar el libro** y **cómo guardar el libro** después de la operación. Ya sea que necesites **mover tabla dinámica** dentro de la misma hoja o a otra hoja, el patrón sigue siendo el mismo: cargar, copiar con las opciones correctas y guardar.

Pruébalo con tus propios archivos, ajusta la dirección de destino y experimenta con diferentes configuraciones de tablas dinámicas. Cuanto más practiques, más confianza tendrás al automatizar tareas de Excel en C#.

---

![Diagram showing the source range A1:G20 being copied to A25 in the same worksheet – how to copy range with pivot tables](/images/how-to-copy-range-diagram.png "how to copy range with pivot tables")

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}