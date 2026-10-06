---
category: general
date: 2026-04-07
description: Aplica un formato numérico personalizado a una celda de hoja de cálculo
  y aprende cómo formatear números en la hoja mientras exportas el valor de la celda
  con C#. Guía rápida y completa.
draft: false
keywords:
- apply custom number format
- format number in spreadsheet
- how to format numeric cell
- how to export cell value
language: es
og_description: Aplica un formato numérico personalizado a una celda de la hoja de
  cálculo y expórtala como una cadena formateada. Aprende cómo formatear números en
  la hoja de cálculo y exportar el valor de la celda.
og_title: Aplicar formato de número personalizado – Tutorial completo de exportación
  en C#
tags:
- C#
- Spreadsheet
- Number Formatting
title: Aplicar formato numérico personalizado en la exportación de hojas de cálculo
  C# – Guía paso a paso
url: /es/net/excel-custom-number-date-formatting/apply-custom-number-format-in-c-spreadsheet-export-step-by-s/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aplicar formato numérico personalizado en la exportación de hojas de cálculo C# – Tutorial completo

¿Alguna vez necesitaste **apply custom number format** a una celda y luego extraer esa cadena formateada de una hoja de cálculo? No estás solo. Muchos desarrolladores se topan con un obstáculo cuando descubren que el valor bruto se devuelve en lugar de la cadena bonita y con conciencia de la configuración regional que esperan. En esta guía te mostraremos exactamente cómo **format number in spreadsheet** cells y cómo exportar el valor de la celda como una cadena formateada usando una popular biblioteca de hojas de cálculo C#.

Al final del tutorial podrás **apply custom number format** a cualquier celda numérica, exportar el resultado con `ExportTable` y ver la salida exacta que esperarías mostrar en una UI o un informe. No se necesitan documentos externos—todo está aquí.

## Requisitos previos

- .NET 6.0 o posterior (el código también funciona en .NET Framework 4.7+)
- Una referencia a la biblioteca de hojas de cálculo que proporciona `Workbook`, `Worksheet` y `ExportTableOptions` (p. ej., **Aspose.Cells** o **GemBox.Spreadsheet**; la API mostrada coincide con Aspose.Cells)
- Conocimientos básicos de C#—si puedes escribir un `Console.WriteLine`, estás listo para continuar

> **Consejo profesional:** Si estás usando una biblioteca diferente, los nombres de las propiedades suelen ser similares (`NumberFormat`, `ExportAsString`). Simplemente mapealos en consecuencia.

## Qué cubre el tutorial

1. Crear un libro de trabajo y seleccionar la primera hoja de cálculo.  
2. Insertar un valor numérico en una celda.  
3. Configurar `ExportTableOptions` para **apply custom number format** y devolver una cadena.  
4. Exportar la celda e imprimir el resultado formateado.  
5. Manejo de casos límite – ¿qué pasa si la celda contiene una fórmula o un valor nulo?

Vamos a comenzar.

![ejemplo de aplicar formato numérico personalizado](https://example.com/image.png "aplicar formato numérico personalizado")

## Paso 1 – Crear un libro de trabajo y obtener la primera hoja de cálculo

Lo primero que necesitas es un objeto workbook. Piensa en él como el archivo de Excel que abrirías en la aplicación Office. Una vez que lo tienes, obtén la primera hoja—la mayoría de los tutoriales comienzan allí porque mantiene el ejemplo conciso.

```csharp
// Step 1: Initialize the workbook and fetch the first worksheet
Workbook workbook = new Workbook();                 // creates an in‑memory workbook
Worksheet worksheet = workbook.Worksheets[0];      // first sheet (index 0)
```

**Por qué es importante:** Un libro de trabajo nuevo te brinda una hoja en blanco, asegurando que no haya formato oculto que interfiera con nuestro custom number format más adelante.

## Paso 2 – Insertar un valor numérico en la celda B2 (la celda que exportaremos)

Ahora necesitamos algo que formatear. La celda **B2** es un lugar conveniente—fácil de referenciar y lo suficientemente alejada de la esquina predeterminada A1 para evitar sobrescrituras accidentales.

```csharp
// Step 2: Insert a raw numeric value
worksheet.Cells["B2"].Value = 1234.56;   // raw double, no formatting yet
```

**¿Qué pasa si el valor es una fórmula?**  
Si más adelante reemplazas el valor bruto con una fórmula (p. ej., `=SUM(A1:A10)`), la rutina de exportación seguirá respetando el number format que aplicamos en el siguiente paso, porque el formato está asociado a la celda, no al tipo de valor.

## Paso 3 – Configurar las opciones de exportación para recibir el valor como una cadena formateada

Aquí está el corazón del tutorial: le indicamos a la biblioteca que **apply custom number format** al exportar. La cadena `NumberFormat` sigue el mismo patrón que usarías en la categoría “Custom” de Excel.

```csharp
// Step 3: Set up options for exporting as a formatted string
ExportTableOptions exportOptions = new ExportTableOptions
{
    ExportAsString = true,                         // forces string output
    NumberFormat = "#,##0.00;(#,##0.00)"           // custom format: 1,234.56 or (1,234.56) for negatives
};
```

- `ExportAsString = true` garantiza que el método devuelva un `string` en lugar de un double bruto.  
- `NumberFormat = "#,##0.00;(#,##0.00)"` replica el patrón de Excel: comas para miles, dos decimales y paréntesis para números negativos.

> **¿Por qué usar un formato personalizado?** Garantiza consistencia entre culturas (p. ej., separadores de número EE. UU. vs. europeos) y te permite incorporar estilos específicos del negocio como los paréntesis contables.

## Paso 4 – Exportar la celda usando las opciones configuradas

Ahora realmente extraemos el valor de la hoja de cálculo, dejando que la biblioteca haga el trabajo pesado de aplicar el formato que definimos.

```csharp
// Step 4: Export the formatted value from B2
string formattedResult = worksheet.Cells.ExportTable(
    worksheet.Cells["B2"],   // the source cell
    exportOptions);         // our custom options
```

**Caso límite – celda vacía:** Si `B2` estuviera vacía, `formattedResult` sería `null`. Puedes protegerte de eso con una simple verificación de null antes de imprimir.

## Paso 5 – Mostrar la cadena formateada

Finalmente, escribimos el resultado en la consola. En una aplicación real podrías enviar esta cadena a un PDF, un correo electrónico o una etiqueta de UI.

```csharp
// Step 5: Show the result
Console.WriteLine(formattedResult);   // Expected output: 1,234.56
```

**Salida esperada**

```
1,234.56
```

Si cambias el valor bruto a `-9876.54`, el mismo formato te daría `(9,876.54)`—exactamente lo que muchos informes contables requieren.

## Ejemplo completo y ejecutable

A continuación se muestra el programa completo que puedes copiar y pegar en un nuevo proyecto de consola. Compila y se ejecuta tal cual, asumiendo que has añadido el paquete NuGet apropiado para la biblioteca de hojas de cálculo.

```csharp
using System;
using Aspose.Cells;   // Replace with your library’s namespace if different

class Program
{
    static void Main()
    {
        // 1️⃣ Create workbook and get first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // 2️⃣ Insert numeric value into B2
        worksheet.Cells["B2"].Value = 1234.56;

        // 3️⃣ Set export options – apply custom number format
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,
            NumberFormat = "#,##0.00;(#,##0.00)"   // custom format
        };

        // 4️⃣ Export the cell as a formatted string
        string formattedResult = worksheet.Cells.ExportTable(
            worksheet.Cells["B2"], exportOptions);

        // 5️⃣ Output the result
        Console.WriteLine(formattedResult);   // → 1,234.56
    }
}
```

### Verificación rápida

- **¿Compila?** Sí—solo asegúrate de que la DLL `Aspose.Cells` (o equivalente) esté referenciada.
- **¿Funcionará con otras culturas?** La cadena de formato es independiente de la cultura; la biblioteca respeta el patrón que le das. Si necesitas separadores específicos de la configuración regional, puedes anteponer el manejo de `CultureInfo` antes de la exportación.

## Preguntas frecuentes y variaciones

### Cómo **format number in spreadsheet** usando un patrón diferente?

Reemplaza la cadena `NumberFormat`. Por ejemplo, para mostrar un porcentaje con un decimal:

```csharp
NumberFormat = "0.0%";
```

### ¿Qué pasa si necesito **how to export cell value** como HTML en lugar de texto plano?

La mayoría de las bibliotecas tienen una sobrecarga que acepta un tipo de exportación. Configurarías `ExportAsString = true` y añadirías `ExportHtml = true` (o similar). El principio sigue siendo el mismo: definir el formato y luego elegir la representación de salida.

### ¿Puedo aplicar el formato a un rango completo, no solo a una celda?

Absolutamente. Puedes asignar `NumberFormat` a un objeto `Style` y luego aplicar ese estilo a un `Range`. La llamada de exportación permanece sin cambios; recogerá el estilo automáticamente.

```csharp
Style style = workbook.CreateStyle();
style.Custom = "#,##0.00;(#,##0.00)";
Range range = worksheet.Cells.CreateRange("A1:C10");
range.ApplyStyle(style, new StyleFlag { NumberFormat = true });
```

### ¿Qué ocurre cuando la celda contiene una fórmula?

La rutina de exportación evalúa primero la fórmula y luego formatea el valor numérico resultante. No se necesita código extra—solo asegúrate de que `Calculate` se haya llamado si desactivaste el cálculo automático.

```csharp
worksheet.Cells["B2"].Formula = "=SUM(A1:A5)";
worksheet.Calculate();   // forces evaluation
```

## Conclusión

Ahora sabes cómo **apply custom number format** a una celda de hoja de cálculo, **format number in spreadsheet** en contextos, y **how to export cell value** como una cadena lista para mostrar. El conciso ejemplo de código anterior cubre cada paso—desde la creación del workbook hasta la salida final—para que puedas incorporarlo directamente en un proyecto de producción.

¿Listo para el próximo desafío? Prueba combinar esta técnica con **how to format numeric cell** para fechas, símbolos de moneda o formato condicional. O explora exportar múltiples celdas como CSV manteniendo el formato personalizado de cada celda. El cielo es el límite, y con estos fundamentos tienes una base sólida.

¡Feliz codificación, y no olvides experimentar—a veces las mejores respuestas aparecen cuando ajustas la cadena de formato un poco!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}