---
category: general
date: 2026-02-21
description: Crea estilo de celda en C# rápidamente. Aprende cómo aplicar estilo a
  una celda, centrar texto en la celda, establecer la alineación de la celda y dominar
  el formato de celdas.
draft: false
keywords:
- create cell style
- apply style to cell
- center text in cell
- set cell alignment
- how to center text
language: es
og_description: Crea un estilo de celda en C# y aprende cómo aplicar el estilo a una
  celda, centrar el texto en ella y establecer la alineación con una guía clara paso
  a paso.
og_title: Crear estilo de celda en C# – Aplicar estilo a una celda y centrar el texto
tags:
- C#
- Aspose.Cells
- Excel automation
title: Crear estilo de celda en C# – Cómo aplicar estilo a una celda y centrar el
  texto
url: /es/net/excel-formatting-and-styling/create-cell-style-in-c-how-to-apply-style-to-a-cell-and-cent/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crear estilo de celda en C# – Guía completa para aplicar estilos y centrar texto

¿Alguna vez necesitaste **crear estilo de celda** en una hoja de Excel pero no sabías por dónde empezar? No estás solo. En muchos proyectos de automatización, la capacidad de **aplicar estilo a celda** es la diferencia entre una hoja de cálculo aburrida y un informe pulido.  

En este tutorial recorreremos un ejemplo completo y ejecutable que te muestra **cómo centrar texto** dentro de una celda, establecer la alineación y agregar un borde fino, todo en solo unas pocas líneas de C#. Al final sabrás exactamente por qué cada elemento es importante y cómo ajustarlo para tus propios escenarios.

## Lo que aprenderás

- Una comprensión clara del flujo de trabajo para **crear estilo de celda** usando Aspose.Cells (o cualquier biblioteca similar).
- El código exacto que puedes copiar y pegar en una aplicación de consola para **aplicar estilo a celda**.
- Información sobre **centrar texto en celda**, **establecer alineación de celda**, y manejar casos especiales como celdas combinadas o formatos numéricos personalizados.
- Consejos para ampliar el estilo: diferentes fuentes, colores de fondo o formato condicional.

> **Requisito previo:** Visual Studio 2022 (o cualquier IDE de C#) y el paquete NuGet Aspose.Cells para .NET. No se requieren otras dependencias.

---

## Paso 1: Configura tu proyecto e importa los espacios de nombres

Antes de que podamos **crear estilo de celda**, necesitamos un proyecto que haga referencia a la biblioteca de Excel.

```csharp
// Program.cs – entry point
using System;
using Aspose.Cells;   // Make sure the Aspose.Cells NuGet package is installed

class Program
{
    static void Main()
    {
        // We'll fill in the rest of the steps here.
    }
}
```

*Por qué es importante:* Importar `Aspose.Cells` nos brinda acceso a las clases `Workbook`, `Worksheet`, `Style` y `Border`. Si estás usando una biblioteca diferente (p.ej., EPPlus), los nombres de las clases cambian pero el concepto sigue siendo el mismo.

---

## Paso 2: Crear un libro de trabajo y obtener la primera celda

Ahora **creamos estilo de celda** obteniendo primero una referencia a la celda que queremos formatear.

```csharp
// Inside Main()
Workbook workbook = new Workbook();           // New, empty workbook
Worksheet ws = workbook.Worksheets[0];        // First worksheet (index 0)

// Step 1: Get a reference to the first cell (row 0, column 0) in the worksheet
Cell firstCell = ws.Cells[0, 0];               // A1 in Excel terms
firstCell.PutValue("Hello, styled world!");
```

Observa que usamos `Cell` en lugar del genérico `var`; la tipificación explícita hace que el código sea más claro para los principiantes. La llamada a `PutValue` escribe una cadena para que podamos ver el efecto del estilo más adelante.

---

## Paso 3: Definir el estilo – centrar texto, agregar un borde fino

Aquí está el núcleo de la operación de **crear estilo de celda**. Estableceremos la alineación horizontal, un borde fino y algunos detalles opcionales.

```csharp
// Step 2: Define a style that centers the text and adds a thin border
Style cellStyle = workbook.CreateStyle();          // Create a fresh Style object
cellStyle.HorizontalAlignment = TextAlignmentType.Center; // Center text horizontally
cellStyle.VerticalAlignment = TextAlignmentType.Center;   // Center vertically – often forgotten
cellStyle.Borders[BorderType.TopBorder].LineStyle = CellBorderType.Thin;
cellStyle.Borders[BorderType.BottomBorder].LineStyle = CellBorderType.Thin;
cellStyle.Borders[BorderType.LeftBorder].LineStyle = CellBorderType.Thin;
cellStyle.Borders[BorderType.RightBorder].LineStyle = CellBorderType.Thin;

// Optional: set a light gray background to make the border pop
cellStyle.ForegroundColor = System.Drawing.Color.LightGray;
cellStyle.Pattern = BackgroundType.Solid;
```

*Por qué lo hacemos:*  
- **HorizontalAlignment** y **VerticalAlignment** juntos responden a la pregunta “**cómo centrar texto** en una celda?”.  
- Añadir los cuatro bordes garantiza que la celda se vea como una etiqueta enmarcada, lo cual es útil para encabezados.  
- El color de fondo no es obligatorio, pero demuestra cómo puedes ampliar el estilo más adelante.

---

## Paso 4: Aplicar el estilo definido a la celda seleccionada

Ahora que el estilo existe, **aplicamos estilo a celda** con una única llamada al método.

```csharp
// Step 3: Apply the defined style to the selected cell
firstCell.SetStyle(cellStyle);
```

Eso es todo—Aspose.Cells se encarga de copiar el estilo en la colección interna de estilos de la celda. Si necesitas el mismo formato en un rango, puedes usar `ws.Cells.CreateRange("A1:D1").ApplyStyle(cellStyle, new StyleFlag { All = true });`.

---

## Paso 5: Guardar el libro de trabajo y verificar el resultado

Una guardada rápida te permite abrir el archivo en Excel y confirmar que el texto está realmente centrado y que el borde aparece.

```csharp
// Save the workbook to disk
string outputPath = "StyledCell.xlsx";
workbook.Save(outputPath, SaveFormat.Xlsx);
Console.WriteLine($"Workbook saved to {outputPath}. Open it to see the styled cell.");
```

*Salida esperada:* Cuando abras **StyledCell.xlsx**, la celda **A1** contiene “Hello, styled world!” centrada tanto horizontal como verticalmente, rodeada por un borde gris fino y con un fondo gris claro.

---

## Variaciones comunes y casos límite

### 1. Centrar texto en una región combinada

Si combinas las celdas **A1:C1** y aún deseas que el texto esté centrado, debes aplicar el estilo a la celda superior‑izquierda **después** de combinar:

```csharp
ws.Cells.Merge(0, 0, 1, 3); // Merge A1:C1
firstCell.SetStyle(cellStyle); // Style still works because it’s applied to the anchor cell
```

### 2. Usar un formato numérico

A veces necesitas **establecer alineación de celda** *y* mostrar números con un formato específico:

```csharp
cellStyle.Custom = "#,##0.00"; // Two decimal places
firstCell.PutValue(12345.678);
firstCell.SetStyle(cellStyle);
```

La alineación permanece centrada mientras el número aparece como `12,345.68`.

### 3. Reutilizar estilos de forma eficiente

Crear un nuevo `Style` para cada celda puede afectar el rendimiento. En su lugar, crea un objeto de estilo y reutilízalo en muchas celdas o rangos. La clase `StyleFlag` te permite aplicar solo las partes que te interesan, ahorrando memoria.

```csharp
StyleFlag flag = new StyleFlag { HorizontalAlignment = true, Borders = true };
ws.Cells.CreateRange("B2:B10").ApplyStyle(cellStyle, flag);
```

---

## Consejos profesionales y errores a evitar

- **No olvides la alineación vertical** – centrar solo horizontalmente a menudo se ve mal, especialmente con filas más altas.
- **Tipos de borde**: `CellBorderType.Thin` funciona para la mayoría de los informes, pero puedes cambiar a `Medium` o `Dashed` para crear jerarquía visual.
- **Manejo de colores**: Cuando apuntas a .NET Core, usa `System.Drawing.Color` del paquete `System.Drawing.Common`; de lo contrario tendrás un error en tiempo de ejecución.
- **Formato de guardado**: Si necesitas compatibilidad con versiones antiguas de Excel, cambia `SaveFormat.Xlsx` a `SaveFormat.Xls`.

![Ejemplo de crear estilo de celda](https://example.com/images/create-cell-style.png "Crear estilo de celda en C#")

*Texto alternativo: captura de pantalla que muestra una celda con texto centrado y borde fino creado por el tutorial de crear estilo de celda.*

---

## Ejemplo completo (listo para copiar y pegar)

```csharp
using System;
using Aspose.Cells;
using System.Drawing; // For Color

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize workbook and worksheet
        Workbook workbook = new Workbook();
        Worksheet ws = workbook.Worksheets[0];

        // 2️⃣ Grab the first cell and put a sample value
        Cell firstCell = ws.Cells[0, 0];
        firstCell.PutValue("Hello, styled world!");

        // 3️⃣ Create the style: center text, thin border, light gray background
        Style cellStyle = workbook.CreateStyle();
        cellStyle.HorizontalAlignment = TextAlignmentType.Center;
        cellStyle.VerticalAlignment   = TextAlignmentType.Center;
        cellStyle.Borders[BorderType.TopBorder].LineStyle    = CellBorderType.Thin;
        cellStyle.Borders[BorderType.BottomBorder].LineStyle = CellBorderType.Thin;
        cellStyle.Borders[BorderType.LeftBorder].LineStyle   = CellBorderType.Thin;
        cellStyle.Borders[BorderType.RightBorder].LineStyle  = CellBorderType.Thin;
        cellStyle.ForegroundColor = Color.LightGray;
        cellStyle.Pattern = BackgroundType.Solid;

        // 4️⃣ Apply the style to the cell
        firstCell.SetStyle(cellStyle);

        // 5️⃣ Save the result
        string outputPath = "StyledCell.xlsx";
        workbook.Save(outputPath, SaveFormat.Xlsx);
        Console.WriteLine($"Workbook saved to {outputPath}. Open it to see the styled cell.");
    }
}
```

Ejecuta este programa, abre **StyledCell.xlsx**, y verás el resultado exacto descrito anteriormente. Siéntete libre de cambiar el texto, el estilo del borde o el color de fondo para que coincida con tu marca.

---

## Conclusión

Hemos **creado estilo de celda** desde cero, **aplicado estilo a celda**, y demostrado **cómo centrar texto** tanto horizontal como verticalmente. Al dominar estos bloques de construcción ahora puedes formatear encabezados, resaltar totales o crear plantillas de informes completas sin salir de C#.  

Si tienes curiosidad por los siguientes pasos, prueba:

- **Aplicar el mismo estilo a una fila completa** (`ws.Cells.CreateRange("A2:E2").ApplyStyle(cellStyle, new StyleFlag { All = true });`).
- **Agregar formato condicional** para cambiar el fondo según los valores de la celda.
- **Exportar a PDF** manteniendo el estilo.

Recuerda, el estilo es tanto sobre legibilidad como sobre estética. Experimenta, itera, y pronto tus hojas de cálculo se verán tan profesionales como tu código.

*¡Feliz codificación!*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}