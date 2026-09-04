---
category: general
date: 2026-02-09
description: Crea un nuevo libro de Excel y aprende a copiar tablas dinámicas sin
  esfuerzo. Esta guía muestra cómo duplicar una tabla dinámica y guardar el libro
  como nuevo.
draft: false
keywords:
- create new excel workbook
- how to copy pivot
- duplicate pivot table
- save workbook as new
- how to copy worksheet
language: es
og_description: Crea un nuevo libro de Excel en C# y copia una tabla dinámica al instante.
  Aprende cómo duplicar la tabla dinámica y guardar el libro como nuevo con un ejemplo
  de código completo.
og_title: Crear nuevo libro de Excel – Copia paso a paso de tabla dinámica
tags:
- excel
- csharp
- aspose.cells
- automation
title: Crear nuevo libro de Excel – Copiar y duplicar tabla dinámica
url: /es/net/pivot-tables/create-new-excel-workbook-copy-duplicate-pivot-table/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crear nuevo libro de Excel – Copiar y duplicar tabla dinámica

¿Alguna vez necesitaste **create new Excel workbook** que transfiera una tabla dinámica compleja desde un archivo existente? No eres el único—muchos desarrolladores se topan con este obstáculo al automatizar pipelines de informes. La buena noticia es que con unas pocas líneas de C# y la biblioteca Aspose.Cells puedes **how to copy pivot** rápidamente, **duplicate pivot table**, y **save workbook as new** sin abrir Excel manualmente.

En esta guía recorreremos todo el proceso, desde cargar el libro de origen hasta guardar la versión duplicada. Al final tendrás un fragmento listo‑para‑ejecutar que puedes insertar en cualquier proyecto .NET. Sin rodeos, solo una solución práctica que puedes probar hoy.

## Qué cubre este tutorial

* **Prerequisites** – .NET 6+ (o .NET Framework 4.6+), Visual Studio y el paquete NuGet Aspose.Cells para .NET.
* Código paso a paso que **creates new Excel workbook**, copia la tabla dinámica y escribe el resultado en disco.
* Explicaciones de **why** cada línea importa, no solo de **what** hace.
* Consejos para manejar casos límite como hojas de cálculo ocultas o rangos de datos grandes.
* Una mirada rápida a **how to copy worksheet** si alguna vez necesitas la hoja completa en lugar de solo la tabla dinámica.

¿Listo? Vamos a sumergirnos.

![create new excel workbook illustration](image.png "Diagram showing source workbook, pivot copy, and destination workbook")

## Paso 1: Configurar el proyecto e instalar Aspose.Cells

Antes de que podamos **create new Excel workbook**, necesitamos un proyecto que haga referencia a la biblioteca correcta.

```csharp
// Install the Aspose.Cells package via NuGet:
//   dotnet add package Aspose.Cells
using Aspose.Cells;   // Provides Workbook, Worksheet, Range, etc.
using System;        // For basic .NET types
```

*Why this matters:* Aspose.Cells funciona completamente en memoria, por lo que nunca tendrás que lanzar Excel en el servidor. También conserva la información de la caché de la tabla dinámica, lo cual es esencial para una verdadera **duplicate pivot table**.

> **Pro tip:** Si estás apuntando a .NET Core, asegúrate de que el identificador de tiempo de ejecución (RID) de tu proyecto coincida con la plataforma a la que desplegarás; de lo contrario podrías encontrar errores al cargar bibliotecas nativas.

## Paso 2: Cargar el libro de origen que contiene la tabla dinámica

Ahora vamos a **how to copy pivot** desde un archivo existente. El libro de origen puede estar en cualquier ubicación del disco, en un stream o incluso en un array de bytes.

```csharp
// Step 2: Load the source workbook that contains the pivot table
string sourcePath = @"C:\Reports\source.xlsx";
Workbook sourceWorkbook = new Workbook(sourcePath);

// Grab the first worksheet (adjust the index if your pivot lives elsewhere)
Worksheet sourceSheet = sourceWorkbook.Worksheets[0];

// Define the range that encloses the pivot table – A1:D20 in this example
Range sourceRange = sourceSheet.Cells.CreateRange("A1:D20");
```

*Why we pick a range:* Una tabla dinámica reside dentro de un rango de celdas regular, pero también tiene datos de caché ocultos adjuntos a la hoja. Al copiar el rango **including the pivot**, Aspose.Cells asegura que la caché viaja con él, dándote una **duplicate pivot table** funcional en el archivo de destino.

## Paso 3: Crear un nuevo libro de Excel para recibir los datos copiados

Aquí es donde realmente **create new Excel workbook** que contendrá la tabla dinámica duplicada.

```csharp
// Step 3: Create a fresh workbook (empty) for the destination
Workbook destinationWorkbook = new Workbook(); // Starts with a default empty sheet
Worksheet destinationSheet = destinationWorkbook.Worksheets[0];

// Destination starts at A1 – you could offset if you need space for other data
Range destinationRange = destinationSheet.Cells.CreateRange("A1");
```

> **Why a fresh workbook?** Comenzar desde cero garantiza que ningún formato residual u objetos ocultos interfieran con la tabla dinámica copiada. También hace que el archivo resultante sea más pequeño, lo cual es útil para adjuntos de correo electrónico automatizados.

## Paso 4: Copiar el rango de la tabla dinámica al nuevo libro

Ahora realizamos la operación real de **how to copy pivot**.

```csharp
// Step 4: Copy the range (including the pivot) from source to destination
sourceRange.Copy(destinationRange);
```

Esa única línea hace el trabajo pesado:

* Los valores de celda, fórmulas y formato se transfieren.
* La caché de la tabla dinámica se duplica, por lo que la nueva tabla dinámica sigue siendo totalmente funcional.
* Cualquier referencia relativa dentro de la tabla dinámica se ajusta automáticamente a la nueva ubicación.

### Manejo de casos límite

* **Hidden worksheets:** Si la hoja de origen está oculta, la tabla dinámica aún se copia correctamente, pero podrías querer mostrar la hoja de destino para la visibilidad del usuario:
  ```csharp
  destinationSheet.IsVisible = true;
  ```
* **Large data sets:** Para rangos mayores a unos pocos miles de filas, considera usar `CopyTo` con `CopyOptions` para transmitir la operación y reducir la presión de memoria.

## Paso 5: Guardar el libro de destino como un nuevo archivo

Finalmente, **save workbook as new** y verificamos el resultado.

```csharp
// Step 5: Save the destination workbook with the duplicated pivot table
string destPath = @"C:\Reports\copied.xlsx";
destinationWorkbook.Save(destPath, SaveFormat.Xlsx);

// Quick verification – open the file manually or read a cell value
Console.WriteLine($"Workbook saved to {destPath}");
```

Si abres `copied.xlsx` verás una réplica exacta de la tabla dinámica original, lista para manipulación o distribución adicional.

### Opcional: How to Copy Worksheet Instead of Just the Pivot

A veces deseas la hoja completa, no solo la tabla dinámica. La misma API lo hace trivial:

```csharp
// Copy the whole worksheet (including all charts, tables, etc.)
sourceSheet.CopyTo(destinationWorkbook, 0); // Inserts at index 0
destinationWorkbook.Save(@"C:\Reports\full_copy.xlsx");
```

Esto satisface la consulta **how to copy worksheet** y puede ser útil cuando necesitas preservar configuraciones adicionales a nivel de hoja.

## Ejemplo completo funcionando

Juntándolo todo, aquí tienes una aplicación de consola auto‑contenida que puedes compilar y ejecutar:

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // 1️⃣ Load source workbook
        string sourcePath = @"C:\Reports\source.xlsx";
        Workbook sourceWorkbook = new Workbook(sourcePath);
        Worksheet sourceSheet = sourceWorkbook.Worksheets[0];
        Range sourceRange = sourceSheet.Cells.CreateRange("A1:D20");

        // 2️⃣ Create destination workbook
        Workbook destinationWorkbook = new Workbook();
        Worksheet destinationSheet = destinationWorkbook.Worksheets[0];
        Range destinationRange = destinationSheet.Cells.CreateRange("A1");

        // 3️⃣ Copy the pivot (range)
        sourceRange.Copy(destinationRange);

        // 4️⃣ Save as new file
        string destPath = @"C:\Reports\copied.xlsx";
        destinationWorkbook.Save(destPath, SaveFormat.Xlsx);

        Console.WriteLine($"✅ Successfully created new Excel workbook with duplicated pivot table at {destPath}");
    }
}
```

**Expected output:** La consola imprime un mensaje de éxito, y `copied.xlsx` aparece en `C:\Reports` con una tabla dinámica funcional idéntica a la de `source.xlsx`.

## Preguntas comunes y trampas

* **Will formulas inside the pivot break?** No—porque la caché de la tabla dinámica viaja con el rango, todos los campos calculados permanecen intactos.
* **What if the source pivot uses external data connections?** Esas conexiones *no* se copian. Necesitarás volver a establecerlas en el libro de destino o convertir la tabla dinámica a una tabla estática primero.
* **Can I copy multiple pivots at once?** Absolutamente—simplemente define un rango más grande que abarque todas las tablas dinámicas, o itera a través de cada objeto `PivotTable` en `sourceSheet.PivotTables` y cópialas individualmente.
* **Do I need to dispose of the `Workbook` objects?** Implementan `IDisposable`, por lo que envolverlos en sentencias `using` es una buena práctica, especialmente en servicios de alto rendimiento.

## Conclusión

Ahora sabes **how to create new Excel workbook**, copiar una tabla dinámica, **duplicate pivot table**, y **save workbook as new** usando C# y Aspose.Cells. Los pasos son sencillos: cargar, crear, copiar y guardar. Con el fragmento opcional **how to copy worksheet** también tienes una alternativa para duplicar la hoja completa.

A continuación, podrías explorar:

* Añadir formato personalizado a la tabla dinámica duplicada.
* Actualizar la caché de la tabla dinámica programáticamente después de cambios en los datos.
* Exportar el libro a PDF o CSV para sistemas posteriores.

¡Pruébalo, ajusta el rango, y deja que la automatización elimine el trabajo pesado de tu flujo de informes! ¡Feliz codificación!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}