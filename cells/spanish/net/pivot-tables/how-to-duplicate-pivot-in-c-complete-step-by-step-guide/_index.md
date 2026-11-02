---
category: general
date: 2026-03-22
description: Aprenda cómo duplicar una tabla dinámica en C# usando Aspose.Cells. Esta
  guía también muestra cómo copiar filas y cargar un libro de Excel en C# para una
  automatización de Excel sin problemas al copiar filas.
draft: false
keywords:
- how to duplicate pivot
- how to copy rows
- load excel workbook c#
- excel automation copy rows
language: es
og_description: ¿Cómo duplicar una tabla dinámica en C#? Sigue este tutorial conciso
  para cargar un libro de Excel en C#, copiar filas y dominar la automatización de
  Excel copiando filas.
og_title: Cómo duplicar Pivot en C# – Guía completa
tags:
- C#
- Excel Automation
- Aspose.Cells
title: Cómo duplicar Pivot en C# – Guía completa paso a paso
url: /es/net/pivot-tables/how-to-duplicate-pivot-in-c-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo duplicar una tabla dinámica en C# – Guía completa paso a paso

¿Alguna vez te has preguntado **cómo duplicar una tabla dinámica** de forma programática sin arrastrarla manualmente en Excel? No eres el único. En muchos flujos de informes se necesita el mismo diseño de tabla dinámica en un nuevo conjunto de filas, y hacerlo a mano es una pérdida de tiempo.  

¿La buena noticia? Con unas pocas líneas de C# puedes cargar un libro de Excel, definir el área que contiene la tabla dinámica y **cómo copiar filas** para que la tabla dinámica aparezca en una nueva ubicación, todo en una ejecución automatizada. En este tutorial también cubriremos los conceptos básicos de **load excel workbook c#** y te daremos una base sólida para tareas de **excel automation copy rows**.

> **Lo que obtendrás**  
> • Un ejemplo completo y ejecutable que duplica una tabla dinámica.  
> • Una explicación de por qué cada línea es importante.  
> • Consejos para manejar casos límite como hojas ocultas o múltiples tablas dinámicas.

---

## Requisitos previos

- **.NET 6.0** (o cualquier versión reciente de .NET) instalado.  
- **Aspose.Cells for .NET** – la biblioteca que usaremos para manipular archivos Excel. Puedes obtenerla vía NuGet:  

```bash
dotnet add package Aspose.Cells
```  

- Un libro de origen (`Source.xlsx`) que ya contiene una tabla dinámica en el rango **A1:J20** (el rango que duplicaremos).  
- Familiaridad básica con la sintaxis de C# – nada sofisticado, solo las habituales sentencias `using` y el método `Main`.

Si alguno de estos conceptos te resulta desconocido, detente un momento e instala el paquete; el resto de la guía asume que la biblioteca está lista para usar.

![Ilustración de cómo duplicar una tabla dinámica en C# usando Aspose.Cells](https://example.com/duplicate-pivot.png "ilustración de cómo duplicar una tabla dinámica en C#")

*Texto alternativo de la imagen: "cómo duplicar una tabla dinámica en C# ejemplo que muestra filas de la tabla dinámica original y duplicada".*

## Paso 1: Cargar libro de Excel C# – Abrir el archivo

Lo primero que necesitas hacer cuando quieres **load excel workbook c#** es crear una instancia de `Workbook` que apunte a tu archivo. Este objeto te brinda acceso a cada hoja, celda y tabla dinámica dentro del archivo.

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // Step 1: Load the source workbook
        string sourcePath = @"C:\Data\Source.xlsx";
        Workbook workbook = new Workbook(sourcePath);

        // From here on we can work with worksheets, ranges, and pivots.
```

**Por qué es importante:**  
`Workbook` abstrae todo el archivo Excel en un modelo en memoria. Sin cargarlo primero no puedes inspeccionar la ubicación de la tabla dinámica ni copiar filas. Además, el constructor detecta automáticamente el formato del archivo (XLS, XLSX, CSV, etc.), por lo que no necesitas código adicional para la detección del formato.

## Paso 2: Cómo copiar filas – Definir el área de la tabla dinámica

Ahora que el libro está en memoria, necesitamos indicarle a Aspose.Cells qué filas contienen la tabla dinámica. En nuestro ejemplo la tabla dinámica está en **A1:J20**, lo que corresponde a las filas **0‑19** (indexado basado en cero). Lo envolveremos en una estructura `CellArea`.

```csharp
        // Step 2: Define the cell area that contains the pivot table (A1:J20)
        // Row indices are zero‑based, column indices are also zero‑based.
        CellArea copyRange = new CellArea(startRow: 0, startColumn: 0, endRow: 19, endColumn: 9);
```

**Por qué usamos `CellArea`:**  
Es una forma ligera de describir un bloque rectangular. Cuando más adelante llames a `CopyRows`, el método lee este objeto para saber exactamente qué filas duplicar. Si alguna vez necesitas ajustar el rango (por ejemplo, que la tabla dinámica crezca hasta la columna K), solo cambias el valor de `endColumn`.

## Paso 3: Acceder a la hoja de destino

La mayoría de los libros tienen una sola hoja, pero la API funciona igual para múltiples hojas. Obtén la primera hoja (índice 0) – allí está la tabla dinámica original.

```csharp
        // Step 3: Get the first worksheet from the workbook
        Worksheet worksheet = workbook.Worksheets[0];
```

**Consejo profesional:**  
Si tienes hojas con nombre, también puedes obtenerlas por nombre: `workbook.Worksheets["Sheet1"]`. Esto ayuda a evitar codificar índices cuando la estructura del libro cambia.

## Paso 4: Cómo copiar filas – Duplicar la tabla dinámica

Este es el núcleo de **how to duplicate pivot**: copiamos las filas que contienen la tabla dinámica a una nueva ubicación. En nuestro caso empezamos en la fila 31 (índice basado en cero 30). El método `CopyRows` copia *tanto* los datos como la caché subyacente de la tabla dinámica, por lo que las nuevas filas se comportan exactamente como las originales.

```csharp
        // Step 4: Copy the rows of the defined range to a new location (starting at row 31)
        // The third argument is the destination start row (zero‑based).
        worksheet.Cells.CopyRows(copyRange.StartRow, copyRange.EndRow, destinationRow: 30);
```

**¿Qué ocurre internamente?**  
`CopyRows` clona cada fila, preservando fórmulas, estilos y definiciones de la tabla dinámica. Como la caché de la tabla dinámica reside a nivel del libro, la tabla duplicada referencia automáticamente la misma fuente de datos – no se necesita configuración adicional.

**Caso límite – filas ocultas:**  
Si alguna de las filas del rango de origen está oculta, permanecerá oculta después de copiar. Si deseas mostrarlas, llama a `worksheet.Rows[destRow].IsHidden = false` después de la copia.

## Paso 5: Guardar el libro – Verificar el duplicado

Finalmente, escribe los cambios de vuelta al disco. Puedes sobrescribir el archivo original o, de forma más segura, guardarlo con un nuevo nombre para poder comparar antes y después.

```csharp
        // Step 5: Save the workbook – the pivot table is now duplicated in the new rows
        string outputPath = @"C:\Data\CopyWithPivot.xlsx";
        workbook.Save(outputPath);

        Console.WriteLine("Pivot duplicated successfully! Check " + outputPath);
    }
}
```

**Resultado que deberías ver:**  
Abre `CopyWithPivot.xlsx`. Encontrarás la tabla dinámica original en **A1:J20** y una copia idéntica que comienza en **A31:J50**. Ambas tablas dinámicas pueden actualizarse de forma independiente, y cualquier segmentador (slicer) asociado a la original seguirá funcionando para la copia porque comparten la misma caché.

## Preguntas frecuentes y variaciones

### ¿Puedo duplicar varias tablas dinámicas a la vez?

Absolutamente. Recorre todas las tablas dinámicas (`worksheet.PivotTables`) y copia el rango de cada una a un destino diferente. Solo asegúrate de que los rangos de destino no se superpongan.

### ¿Qué pasa si el libro de origen está protegido con contraseña?

Aspose.Cells te permite abrir un archivo protegido pasando la contraseña al constructor `Workbook`:

```csharp
Workbook workbook = new Workbook(sourcePath, new LoadOptions { Password = "mySecret" });
```

### ¿Cómo copiar filas sin afectar las fórmulas?

Si solo necesitas los *valores* (sin fórmulas), usa `CopyRows` con la bandera `CopyOptions`:

```csharp
worksheet.Cells.CopyRows(sourceStart, sourceEnd, destStart, new CopyOptions { CopyValues = true });
```

### ¿Hay una forma de copiar filas a un libro *diferente*?

Sí. Después de copiar filas en la hoja de origen, puedes clonar la hoja en otra instancia de `Workbook` mediante `targetWorkbook.Worksheets.AddCopy(worksheet)`.

## Consejos profesionales para una copia de filas fiable en automatización de Excel

- **Validar el rango** antes de copiar. Un rápido `if (copyRange.EndRow >= worksheet.Cells.MaxDataRow)` evita errores fuera de rango.  
- **Desactivar el cálculo** mientras se copian rangos grandes: `workbook.Settings.CalcMode = CalcMode.Manual;` – esto acelera la operación dramáticamente.  
- **Liberar objetos** (`workbook.Dispose()`) si procesas muchos archivos en un bucle para liberar recursos nativos.  
- **Registrar la operación** – especialmente en pipelines de producción – para poder rastrear qué archivos fueron procesados y detectar fallos temprano.

## Conclusión

Ahora sabes **how to duplicate pivot** tablas en C# usando Aspose.Cells, y has visto el flujo completo desde **load excel workbook c#** hasta **excel automation copy rows** y finalmente guardar el resultado. El ejemplo es autónomo, se ejecuta directamente, y puede ampliarse para manejar múltiples tablas dinámicas, archivos protegidos o copias entre libros.

¿Próximos pasos? Prueba adaptar el script para:

- Actualizar la tabla dinámica duplicada programáticamente (`pivotTable.RefreshData();`).  
- Exportar el área duplicada a un CSV para procesamiento posterior.  
- Integrar el código en una API ASP.NET Core para que los usuarios puedan subir un archivo y recibir instantáneamente una versión con la tabla dinámica duplicada.

¡Feliz codificación, y que tu automatización de Excel sea siempre fluida!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}