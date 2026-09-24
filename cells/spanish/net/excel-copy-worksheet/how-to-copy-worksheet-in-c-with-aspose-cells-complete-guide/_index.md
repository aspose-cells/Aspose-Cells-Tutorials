---
category: general
date: 2026-03-30
description: Cómo copiar una hoja de cálculo en C# usando Aspose.Cells – guía paso
  a paso que cubre copiar rango de celdas, copiar columnas entre hojas, copiar tabla
  dinámica de la hoja y agregar código para una nueva hoja.
draft: false
keywords:
- how to copy worksheet
- copy cell range
- copy columns between sheets
- copy worksheet pivot table
- add new worksheet code
language: es
og_description: Aprende cómo copiar una hoja de cálculo en C# con Aspose.Cells. Esta
  guía muestra cómo copiar un rango de celdas, preservar tablas dinámicas, copiar
  columnas entre hojas y agregar código para una nueva hoja.
og_title: Cómo copiar una hoja de cálculo en C# – Tutorial completo de Aspose.Cells
tags:
- Aspose.Cells
- C#
- Excel Automation
title: Cómo copiar una hoja de cálculo en C# con Aspose.Cells – Guía completa
url: /es/net/excel-copy-worksheet/how-to-copy-worksheet-in-c-with-aspose-cells-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo copiar una hoja de cálculo en C# con Aspose.Cells – Guía completa

¿Alguna vez te has preguntado **cómo copiar worksheet** en C# sin perder ni una sola tabla dinámica o fórmula? No estás solo—muchos desarrolladores se topan con un obstáculo cuando necesitan duplicar una hoja manteniendo todas sus ventajas intactas. En este tutorial recorreremos una solución práctica, de extremo a extremo, que no solo copia los datos sino que también preserva la **copy worksheet pivot table**, maneja **copy cell range**, y muestra el **add new worksheet code** que necesitarás.

Cubrirémos todo, desde cargar el libro de trabajo fuente hasta guardar el archivo de destino, para que puedas copy columns between sheets, preservar objetos y mantener tu código limpio. Sin referencias vagas, solo un ejemplo completo y ejecutable que puedes incorporar a tu proyecto hoy.

## Qué cubre este tutorial

- Cargar un archivo Excel existente con Aspose.Cells  
- Usar **add new worksheet code** para crear una hoja de destino  
- Definir un **copy cell range** que incluya una tabla dinámica  
- Configurar **CopyOptions** para mantener gráficos, fórmulas y tablas dinámicas intactas  
- Ejecutar **copy columns between sheets** con precisión por filas  
- Guardar el resultado y verificar que la hoja de cálculo se haya copiado correctamente  

Al final de esta guía podrás responder con confianza a la pregunta “how to copy worksheet”, ya sea que estés automatizando informes o construyendo una interfaz basada en hojas de cálculo.

## Cómo copiar una hoja de cálculo – Visión general

Antes de sumergirnos en el código, describamos el flujo a alto nivel. Piensa en ello como una receta:

1. **Load** el libro de trabajo fuente (`Source.xlsx`).  
2. **Add** una nueva hoja de cálculo para contener la copia (`add new worksheet code`).  
3. **Define** el área que deseas duplicar (`copy cell range`).  
4. **Configure** las opciones de copia para que la tabla dinámica sobreviva (`copy worksheet pivot table`).  
5. **Copy** filas y columnas (`copy columns between sheets`).  
6. **Save** el nuevo libro de trabajo (`Destination.xlsx`).  

Eso es todo—seis pasos, sin magia. Cada paso se explica a continuación con fragmentos de código y la lógica detrás de ellos.

## Paso 1 – Cargar el libro de trabajo fuente

Lo primero: necesitas una instancia de `Workbook` que apunte al archivo que deseas duplicar. Este paso es esencial porque Aspose.Cells trabaja directamente con el sistema de archivos, no con la interfaz de Office.

```csharp
using Aspose.Cells;

// Path to the original file
string sourcePath = "YOUR_DIRECTORY/Source.xlsx";
string destinationPath = "YOUR_DIRECTORY/Destination.xlsx";

// Load the workbook – this is the starting point for how to copy worksheet
Workbook workbook = new Workbook(sourcePath);
```

*Why this matters:* Cargar el archivo crea una representación en memoria de cada hoja, celda y objeto. Sin esto, no hay nada que copiar, y cualquier intento de `add new worksheet code` más adelante fallará porque los datos fuente no están presentes.

## Paso 2 – Añadir una nueva hoja de cálculo (add new worksheet code)

Ahora necesitamos un lugar para pegar los datos copiados. Aquí es donde el **add new worksheet code** brilla. Puedes nombrar la hoja como quieras; aquí la llamamos `"Copy"`.

```csharp
// Grab the first worksheet (the one we want to copy)
Worksheet sourceSheet = workbook.Worksheets[0];

// Add a fresh worksheet to receive the copy
Worksheet copySheet = workbook.Worksheets.Add("Copy");
```

*Pro tip:* Si planeas copiar varias hojas, llama a `Worksheets.Add` dentro de un bucle y asigna a cada hoja un nombre único. Así evitarás colisiones de nombres y mantendrás tu libro de trabajo ordenado.

## Paso 3 – Definir el rango de celdas a copiar

Un **copy cell range** indica a Aspose.Cells exactamente qué filas y columnas duplicar. En muchos escenarios reales el rango incluye una tabla dinámica, por lo que debemos ser precisos.

```csharp
// Define the area that contains the pivot table (A1:G20)
CellArea sourceRange = new CellArea
{
    StartRow = 0,      // Row 1 (zero‑based)
    StartColumn = 0,   // Column A
    EndRow = 19,       // Row 20
    EndColumn = 6      // Column G
};

// Destination range – we start at the same top‑left corner
CellArea destinationRange = new CellArea
{
    StartRow = 0,
    StartColumn = 0,
    EndRow = 19,
    EndColumn = 6
};
```

*Why we need this:* Al especificar explícitamente el rango, evitas copiar toda la hoja (lo que puede ser derrochador) y garantizas que la tabla dinámica quede dentro del área copiada. Este es el núcleo de **how to copy worksheet** cuando solo necesitas una parte de la hoja.

## Paso 4 – Configurar opciones de copia (preserve copy worksheet pivot table)

Aspose.Cells ofrece un objeto `CopyOptions` que controla lo que se pega. Para mantener la tabla dinámica, los gráficos y las fórmulas, configuramos `PasteType.All` y habilitamos `PasteSpecial`.

```csharp
CopyOptions copyOptions = new CopyOptions
{
    PasteType = PasteType.All,   // Copy everything: values, formats, objects
    PasteSpecial = true          // Enable special paste to retain pivot tables
};
```

*Explanation:* `PasteType.All` es la opción más inclusiva, mientras que `PasteSpecial` indica al motor que trate correctamente los objetos complejos—como tablas dinámicas. Omitir este paso es una trampa común; la hoja copiada perdería sus características interactivas.

## Paso 5 – Copiar filas y columnas (copy columns between sheets)

Ahora llega la parte pesada: mover realmente los datos. Usaremos `CopyRows` y `CopyColumns` para manejar **copy columns between sheets**. Hacer ambos garantiza que las celdas combinadas y los anchos de columna se conserven.

```csharp
// Copy rows from the source to the destination sheet
sourceSheet.Cells.CopyRows(
    sourceRange.StartRow,
    sourceRange.EndRow,
    copySheet.Cells,
    destinationRange.StartRow,
    copyOptions);

// Copy columns from the source to the destination sheet
sourceSheet.Cells.CopyColumns(
    sourceRange.StartColumn,
    sourceRange.EndColumn,
    copySheet.Cells,
    destinationRange.StartColumn,
    copyOptions);
```

*What’s happening:* `CopyRows` mueve los datos fila por fila, mientras que `CopyColumns` hace lo mismo columna por columna. Ejecutar ambos garantiza que todo el bloque rectangular se duplique, lo cual es esencial cuando necesitas **copy columns between sheets** que tienen diferentes anchos de columna o columnas ocultas.

## Paso 6 – Guardar el libro de trabajo

Finalmente, escribe los cambios de vuelta al disco. Este paso completa el proceso de **how to copy worksheet**.

```csharp
// Save the workbook with the newly copied sheet
workbook.Save(destinationPath);
```

*Verification tip:* Abre `Destination.xlsx` y verifica que la hoja `"Copy"` sea idéntica a la original, que las tablas dinámicas funcionen y que los anchos de columna coincidan. Si algo parece incorrecto, revisa la configuración de `CopyOptions`.

## Casos límite y variaciones comunes

### Copiar múltiples hojas de cálculo

Si necesitas duplicar varias hojas, envuelve la lógica anterior en un bucle `foreach`:

```csharp
foreach (Worksheet ws in workbook.Worksheets)
{
    Worksheet newWs = workbook.Worksheets.Add(ws.Name + "_Copy");
    // Re‑use sourceRange/destinationRange or calculate per sheet
    // Then call CopyRows/CopyColumns as shown earlier
}
```

### Preservar fórmulas entre diferentes libros de trabajo

Cuando los libros de trabajo fuente y destino tienen rangos nombrados diferentes, establece `copyOptions` a `PasteType.Formulas` además de `All`:

```csharp
copyOptions.PasteType = PasteType.All | PasteType.Formulas;
```

### Grandes rangos y rendimiento

Para conjuntos de datos masivos (cientos de miles de filas), considera usar solo `CopyRows` y omitir `CopyColumns` si los anchos de columna no son críticos. Esto puede ahorrar unos segundos.

## Ejemplo completo y funcional

Abajo está el programa completo, listo para ejecutar, que incorpora todo lo que hemos discutido. Pégalo en una aplicación de consola, ajusta las rutas de archivo y pulsa **F5**.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // ---------- Step 1: Load the source workbook ----------
        string sourcePath = "YOUR_DIRECTORY/Source.xlsx";
        string destinationPath = "YOUR_DIRECTORY/Destination.xlsx";
        Workbook workbook = new Workbook(sourcePath);

        // ---------- Step 2: Add a new worksheet (add new worksheet code) ----------
        Worksheet sourceSheet = workbook.Worksheets[0];
        Worksheet copySheet = workbook.Worksheets.Add("Copy");

        // ---------- Step 3: Define the copy cell range ----------
        CellArea sourceRange = new CellArea
        {
            StartRow = 0,
            StartColumn = 0,
            EndRow = 19,
            EndColumn = 6
        };
        CellArea destinationRange = new CellArea
        {
            StartRow = 0,
            StartColumn = 0,
            EndRow = 19,
            EndColumn = 6
        };

        // ---------- Step 4: Set copy options (preserve copy worksheet pivot table) ----------
        CopyOptions copyOptions = new CopyOptions
        {
            PasteType = PasteType.All,
            PasteSpecial = true
        };

        // ---------- Step 5: Copy rows and columns (copy columns between sheets) ----------
        sourceSheet.Cells.CopyRows(
            sourceRange.StartRow,
            sourceRange.EndRow,
            copySheet.Cells,
            destinationRange.StartRow,
            copyOptions);

        sourceSheet.Cells.CopyColumns(
            sourceRange.StartColumn,
            sourceRange.EndColumn,
            copySheet.Cells,
            destinationRange.StartColumn,
            copyOptions);

        // ---------- Step 6: Save the workbook ----------
        workbook.Save(destinationPath);
    }
}
```

**Expected result:** Al abrir `Destination.xlsx` se muestra una hoja llamada **Copy** que refleja la primera hoja de `Source.xlsx`—incluyendo cualquier tabla dinámica, formato y anchos de columna. El archivo original permanece intacto.

## Preguntas frecuentes

**Q: ¿Esto funciona con archivos .xlsx creados por Excel 2019?**  
A: Absolutamente. Aspose.Cells soporta todos los formatos modernos de Excel, por lo que el mismo código funciona para `.xlsx`, `.xlsm`, e incluso archivos `.xls` más antiguos.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}