---
category: general
date: 2026-03-01
description: El tutorial de lectura y escritura de Excel en C# muestra cómo leer el
  valor de una celda de Excel y escribir una fecha y hora en Excel usando C# y Aspose.Cells
  en unos pocos pasos fáciles.
draft: false
keywords:
- read write excel c#
- read excel cell value
- write datetime to excel
- c# excel interop
- aspnet excel automation
language: es
og_description: El tutorial de lectura y escritura de Excel en C# explica cómo leer
  el valor de una celda de Excel y escribir una fecha y hora en Excel, con ejemplos
  de código claros y buenas prácticas.
og_title: Leer y escribir Excel C# – Guía paso a paso
tags:
- C#
- Excel
- Aspose.Cells
title: Leer y escribir Excel C# – Guía completa para leer y escribir celdas de Excel
url: /es/net/cell-operations/read-write-excel-c-complete-guide-to-reading-and-writing-exc/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Leer y escribir Excel C# – Guía completa para leer y escribir celdas de Excel

¿Alguna vez intentaste **leer escribir Excel C#** y terminaste con una excepción críptica o una fecha desajustada? No estás solo. Muchos desarrolladores tropiezan cuando necesitan extraer una fecha de era japonesa de una hoja de cálculo y luego almacenar un `DateTime` correcto de nuevo en la misma celda.  

En esta guía recorreremos paso a paso cómo **read excel cell value** y **write datetime to excel** usando C# y la poderosa biblioteca Aspose.Cells. Al final tendrás un ejemplo autocontenido y ejecutable que podrás incorporar a cualquier proyecto .NET.

## Lo que aprenderás

- Cómo instalar y referenciar Aspose.Cells en un proyecto .NET 6+ .  
- El código exacto necesario para obtener una celda que contiene una cadena de era japonesa como `"R3/5/12"`.  
- Cómo analizar esa cadena a un `DateTime` usando la cultura `"ja-JP"`.  
- Los pasos para volver a colocar el `DateTime` resultante en la misma celda de la hoja de cálculo.  
- Consejos para manejar casos límite como celdas vacías o formatos de era inesperados.  

No se requiere experiencia previa con interop de Excel, solo un entendimiento básico de C# y .NET. ¡Comencemos!

![Captura de pantalla de la operación leer escribir Excel C# que muestra la celda B2 antes y después de la conversión](read-write-excel-csharp.png "read write excel c# example")

## Paso 1: Configurar el proyecto – Fundamentos de leer y escribir Excel C#

Antes de sumergirnos en el código, necesitamos una base sólida.

1. **Crea una nueva aplicación de consola** (o cualquier proyecto .NET) que apunte a .NET 6 o superior:

   ```bash
   dotnet new console -n ExcelEraDemo
   cd ExcelEraDemo
   ```

2. **Agrega el paquete NuGet Aspose.Cells**. Es una biblioteca totalmente gestionada que funciona sin interop COM:

   ```bash
   dotnet add package Aspose.Cells
   ```

3. **Copia un archivo Excel** (`EraDates.xlsx`) en la raíz del proyecto. Este libro debe contener una hoja llamada `"Sheet1"` con la celda **B2** que tenga un valor como `"R3/5/12"` (Reiwa 3, 12 de mayo).

Eso es todo el andamiaje que necesitas. El resto del tutorial se centra en la lógica real de **read excel cell value** y **write datetime to excel**.

## Paso 2: Leer el valor de una celda de Excel con C#

Ahora que el proyecto está listo, obtengamos la cadena de la hoja de cálculo. El siguiente fragmento muestra la cadena de llamadas exacta:

```csharp
using Aspose.Cells;
using System;
using System.Globalization;

class Program
{
    static void Main()
    {
        // Load the workbook (adjust the path as needed)
        Workbook wb = new Workbook("EraDates.xlsx");
        Worksheet ws = wb.Worksheets["Sheet1"];   // assumes the sheet is named Sheet1

        // Step 2: Get the cell that holds the Japanese era date string
        // B2 contains something like "R3/5/12"
        Cell dateCell = ws.Cells["B2"];  

        // Step 3: Read the string representation from the cell
        string eraDateString = dateCell.StringValue;  

        Console.WriteLine($"Original cell value: {eraDateString}");
        // -------------------------------------------------
        // From here we’ll convert the era string to a DateTime.
        // -------------------------------------------------
    }
}
```

**Por qué funciona:** `Cell.StringValue` siempre devuelve el texto mostrado, sin importar el formato numérico subyacente. Eso garantiza que trabajemos con la cadena exacta `"R3/5/12"` que ve el usuario.

### Errores comunes

- **Celdas vacías** – `StringValue` devuelve una cadena vacía. Protege contra ello antes de analizar.  
- **Formatos inesperados** – Si la celda contiene `"2023/05/12"` el analizador de era lanzará una excepción; puede que necesites un método alternativo.

## Paso 3: Escribir DateTime a Excel con C#

Con la cadena de era en mano, ahora la analizamos usando `DateTime.ParseExact`. El formato `"ggyy/MM/dd"` indica a .NET que espere una era japonesa (`gg`), un año de dos dígitos (`yy`) y los componentes de mes/día.

```csharp
        // Step 4: Convert the era date string to a DateTime using the Japanese culture
        DateTime parsedDate;
        try
        {
            parsedDate = DateTime.ParseExact(
                eraDateString,
                "ggyy/MM/dd",
                new CultureInfo("ja-JP"));
        }
        catch (FormatException)
        {
            Console.WriteLine("The cell value does not match the expected Japanese era format.");
            return;
        }

        Console.WriteLine($"Parsed DateTime (UTC): {parsedDate:u}");

        // Step 5: Store the resulting DateTime back into the same cell
        dateCell.PutValue(parsedDate);

        // Optional: Apply a standard date format so Excel shows it nicely
        dateCell.SetStyle(new Style { Number = 14 }); // 14 = "m/d/yyyy"

        // Save the workbook to a new file so we don’t overwrite the original
        wb.Save("EraDates_Converted.xlsx");
        Console.WriteLine("Workbook saved as EraDates_Converted.xlsx");
```

**Por qué usamos `PutValue`**: Aspose.Cells detecta automáticamente el tipo .NET y escribe el tipo de celda de Excel apropiado. Pasar un `DateTime` produce una verdadera fecha de Excel, que puede formatearse o usarse en fórmulas posteriores.

### Casos límite y consejos

- **Zonas horarias** – Los objetos `DateTime` se almacenan sin información de zona. Si necesitas UTC, llama a `DateTime.SpecifyKind`.  
- **Alternativa cultural** – Si anticipas otras culturas, envuelve el análisis en un helper que pruebe varios objetos `CultureInfo`.  
- **Rendimiento** – Al procesar miles de filas, reutiliza una única instancia de `CultureInfo` en lugar de crear una nueva en cada iteración.

## Paso 4: Ejemplo completo – Todo junto

A continuación tienes el programa completo, listo para ejecutarse. Copia‑pega en `Program.cs`, asegúrate de que `EraDates.xlsx` esté junto al binario compilado y ejecuta `dotnet run`.

```csharp
using Aspose.Cells;
using System;
using System.Globalization;

class Program
{
    static void Main()
    {
        // Load workbook
        Workbook wb = new Workbook("EraDates.xlsx");
        Worksheet ws = wb.Worksheets["Sheet1"];   // Change if your sheet has a different name

        // -------------------------------------------------
        // 1️⃣ Read the Japanese era string from B2
        // -------------------------------------------------
        Cell dateCell = ws.Cells["B2"];
        string eraDateString = dateCell.StringValue?.Trim();

        if (string.IsNullOrEmpty(eraDateString))
        {
            Console.WriteLine("Cell B2 is empty. Nothing to convert.");
            return;
        }

        Console.WriteLine($"Original cell value: {eraDateString}");

        // -------------------------------------------------
        // 2️⃣ Parse the era string into a DateTime
        // -------------------------------------------------
        DateTime parsedDate;
        try
        {
            parsedDate = DateTime.ParseExact(
                eraDateString,
                "ggyy/MM/dd",
                new CultureInfo("ja-JP"));
        }
        catch (FormatException)
        {
            Console.WriteLine("The value does not match the expected Japanese era format (ggyy/MM/dd).");
            return;
        }

        Console.WriteLine($"Parsed DateTime: {parsedDate:u}");

        // -------------------------------------------------
        // 3️⃣ Write the DateTime back into the same cell
        // -------------------------------------------------
        dateCell.PutValue(parsedDate);

        // Apply a friendly date format (e.g., 2023/05/12)
        Style style = wb.CreateStyle();
        style.Number = 14; // Built‑in date format
        dateCell.SetStyle(style);

        // Save the updated workbook
        wb.Save("EraDates_Converted.xlsx");
        Console.WriteLine("Conversion complete – saved as EraDates_Converted.xlsx");
    }
}
```

**Salida esperada**

```
Original cell value: R3/5/12
Parsed DateTime: 2021-05-12 00:00:00Z
Conversion complete – saved as EraDates_Converted.xlsx
```

Cuando abras `EraDates_Converted.xlsx`, la celda **B2** mostrará una fecha normal (p. ej., `5/12/2021`) y podrá usarse en cálculos de Excel como cualquier otro valor de fecha.

## Consejos profesionales para un código robusto de leer y escribir Excel C#

- **Validar antes de escribir** – Usa `Cell.IsFormula` o `Cell.Type` para evitar sobrescribir fórmulas accidentalmente.  
- **Procesamiento por lotes** – Si necesitas convertir una columna completa, recorre `ws.Cells.Columns[1]` (columna B) y aplica la misma lógica.  
- **Seguridad en hilos** – Los objetos Aspose.Cells no son seguros para hilos; crea instancias separadas de `Workbook` por hilo cuando paralelices.  
- **Registro** – Para scripts de producción, reemplaza `Console.WriteLine` por un logger adecuado (p. ej., Serilog) para capturar fallos de análisis.  
- **Pruebas** – Escribe pruebas unitarias que alimenten cadenas de era conocidas a un método helper y verifiquen los valores `DateTime` resultantes.

## Conclusión

Acabas de dominar **read write Excel C#** aprendiendo a **read excel cell value**, analizar una cadena de era japonesa y **write datetime to excel** con confianza. El ejemplo completo muestra un flujo limpio de extremo a extremo que puedes adaptar a operaciones masivas, diferentes culturas o incluso pipelines de Excel a base de datos.

¿Qué sigue? Prueba a extender el script para procesar una columna entera de fechas de era, o explora las amplias opciones de formato de Aspose.Cells para dar estilo a las celdas de salida. También puedes experimentar con otras bibliotecas como EPPlus o ClosedXML—la mayor parte de la lógica permanece igual, solo cambian las llamadas a la API.

¿Tienes preguntas o un escenario complicado de Excel? Deja un comentario abajo, ¡y feliz codificación!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}