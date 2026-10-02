---
category: general
date: 2026-06-05
description: Crea un libro de Excel en C# rápidamente y aprende cómo establecer el
  formato numérico de la celda, exportar la celda de Excel y convertir el valor de
  la celda a cadena con precisión de dos decimales.
draft: false
keywords:
- create excel workbook
- set cell number format
- format number with two decimals
- how to export excel cell
- convert cell value to string
language: es
og_description: Crear un libro de Excel en C# y dominar la configuración del formato
  numérico de las celdas, exportar una celda de Excel como cadena y formatear números
  con dos decimales.
og_title: Crear libro de Excel en C# – Guía completa paso a paso
schemas:
- author: Aspose
  dateModified: '2026-06-05'
  description: Create Excel workbook in C# quickly and learn how to set cell number
    format, export Excel cell, and convert cell value to string with two‑decimal precision.
  headline: Create Excel Workbook in C# – Complete Programming Guide
  type: TechArticle
- description: Create Excel workbook in C# quickly and learn how to set cell number
    format, export Excel cell, and convert cell value to string with two‑decimal precision.
  name: Create Excel Workbook in C# – Complete Programming Guide
  steps:
  - name: What if the cell already has a style?
    text: The `GetStyle` method returns a copy of the existing style, so any previous
      formatting (font, color, etc.) is retained. You only overwrite the `Custom`
      property, leaving everything else untouched.
  - name: How does culture affect the decimal separator?
    text: 'Aspose.Cells respects the thread’s `CultureInfo`. If you need a comma instead
      of a dot, set:'
  - name: Can I export a range of cells at once?
    text: Yes—use `Worksheet.ExportDataTable` or `Worksheet.ExportString` with a range
      address. The `ExportTableOptions` you defined for a single cell can be reused
      for the whole range.
  - name: What if I don’t want the value rounded but truncated?
    text: 'Change the custom format to `"0.00"` with a rounding mode, or manually
      truncate before putting the value:'
  type: HowTo
tags:
- C#
- Excel
- Aspose.Cells
title: Crear libro de Excel en C# – Guía completa de programación
url: /es/net/excel-workbook/create-excel-workbook-in-c-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crear Excel Workbook en C# – Guía completa de programación

¿Alguna vez te has preguntado cómo **create Excel workbook** en C# sin luchar con la interoperabilidad COM o trucos desordenados de CSV? No estás solo. Muchos desarrolladores necesitan una forma limpia y nativa de .NET para generar un archivo .xlsx, colocar un número en una celda y luego exportar ese valor como una cadena con buen formato.  

En este tutorial recorreremos exactamente eso—comenzando con un libro vacío, estableciendo el formato numérico de la celda, formateando el número con dos decimales y, finalmente, aprendiendo **how to export Excel cell** datos como una cadena. Al final también verás cómo **convert cell value to string** sin perder precisión.

> **Consejo profesional:** El enfoque a continuación utiliza la biblioteca **Aspose.Cells for .NET**, que es una API probada en batalla y de nivel comercial. Si buscas una alternativa gratuita, EPPlus o ClosedXML funcionan de manera similar, pero los fragmentos de código diferirán ligeramente.

## Requisitos previos

- .NET 6.0 SDK (o cualquier versión reciente de .NET) instalado.
- Visual Studio 2022 o VS Code con la extensión C#.
- El paquete NuGet **Aspose.Cells** (`Install-Package Aspose.Cells`).

No se requieren otras dependencias—todo lo demás está dentro de la biblioteca.

## Paso 1: Instalar Aspose.Cells y configurar el proyecto

Abre tu terminal (o la Consola del Administrador de paquetes) y ejecuta:

```powershell
dotnet new console -n ExcelDemo
cd ExcelDemo
dotnet add package Aspose.Cells
```

Esto crea una nueva aplicación de consola llamada `ExcelDemo` y agrega la ensambladura `Aspose.Cells`.  

Por qué este paso es importante: sin la biblioteca, no puedes **create Excel workbook** objetos ni manipular celdas de forma segura en cuanto a tipos.

## Paso 2: Crear el Workbook y obtener la primera Worksheet

Ahora abre `Program.cs` y reemplaza el código predeterminado con el fragmento a continuación. Muestra lo primero que haces cuando **create Excel workbook**—instanciar la clase `Workbook` y obtener una referencia a la hoja predeterminada.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 2: Create a workbook and get the first worksheet
        Workbook workbook = new Workbook();               // creates a new .xlsx in memory
        Worksheet ws = workbook.Worksheets[0];           // first (default) sheet

        // The rest of the steps will follow here...
```

> **¿Por qué?** El objeto `Workbook` es la representación en memoria de un archivo Excel. Por defecto contiene una hoja de cálculo, a la que accedemos mediante el índice basado en cero.

## Paso 3: Insertar un valor numérico en una celda específica

Apuntemos a la fila 5, columna 2 (índices basados en cero) e insertemos un número decimal. Esto demuestra **format number with two decimals** más adelante.

```csharp
        // Step 3: Access the cell at row 5, column 2 (zero‑based) and insert a number
        Cell cell = ws.Cells[5, 2];          // corresponds to cell C6 in Excel UI
        cell.PutValue(12345.6789);          // raw value with many decimal places
```

El método `PutValue` almacena el double sin procesar. En este punto, Excel mostraría la precisión completa a menos que apliquemos un formato.

## Paso 4: Establecer el formato numérico de la celda (dos decimales)

Aquí es donde **set cell number format**. Usaremos el objeto `Style` para definir un formato numérico personalizado `"0.00"`—exactamente dos decimales.

```csharp
        // Step 4: Apply a number format to show only two decimal places
        Style style = cell.GetStyle();               // clone existing style
        style.Custom = "0.00";                       // forces two digits after the dot
        cell.SetStyle(style);                        // apply the style back to the cell
```

¿Por qué usar un estilo en lugar de una conversión a cadena? Mantener la celda como tipo numérico preserva su naturaleza calculable (todavía puedes sumar, promediar, etc.) mientras muestra exactamente lo que necesitas.

## Paso 5: Exportar el valor de la celda como una cadena formateada

A veces necesitas el valor **how to export excel cell** como texto plano—quizás para escribirlo en un archivo de registro o enviarlo a través de una API web. Aspose.Cells te permite adjuntar opciones de exportación a una celda, indicando a la biblioteca que renderice el valor como una cadena usando el mismo formato numérico.

```csharp
        // Step 5: Configure export options to get the formatted string
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,          // forces string output
            NumberFormat = "0.00"           // matches the style we set earlier
        };
        cell.ExportOptions = exportOptions; // attach options to the cell
```

## Paso 6: Recuperar la cadena formateada (Convert Cell Value to String)

Vamos a realizar realmente la exportación y ver el resultado. El método `ExportString` devuelve el contenido de la celda como una cadena, aplicando cualquier `ExportTableOptions` que hayamos adjuntado.

```csharp
        // Step 6: Export the cell as a formatted string
        string formattedValue = cell.ExportString();
        Console.WriteLine($"Formatted cell value: {formattedValue}");
```

Al ejecutar el programa, la consola imprime:

```
Formatted cell value: 12345.68
```

Observa el redondeo de `12345.6789` a `12345.68`—ese es el efecto de **format number with two decimals**.

## Paso 7: (Opcional) Guardar el Workbook en disco

Si también deseas ver el resultado dentro de un archivo `.xlsx` real, simplemente llama a `Save`:

```csharp
        // Optional: write the workbook to a file so you can open it in Excel
        workbook.Save("DemoWorkbook.xlsx");
    }
}
```

Abrir `DemoWorkbook.xlsx` muestra el mismo número en la celda **C6**, formateado con dos decimales.

## Casos límite y preguntas comunes

### ¿Qué pasa si la celda ya tiene un estilo?

El método `GetStyle` devuelve una copia del estilo existente, por lo que cualquier formato previo (fuente, color, etc.) se conserva. Sólo sobrescribes la propiedad `Custom`, dejando todo lo demás intacto.

### ¿Cómo afecta la cultura al separador decimal?

Aspose.Cells respeta el `CultureInfo` del hilo. Si necesitas una coma en lugar de un punto, establece:

```csharp
System.Threading.Thread.CurrentThread.CurrentCulture = new System.Globalization.CultureInfo("fr-FR");
```

### ¿Puedo exportar un rango de celdas de una vez?

Sí—usa `Worksheet.ExportDataTable` o `Worksheet.ExportString` con una dirección de rango. Las `ExportTableOptions` que definiste para una sola celda pueden reutilizarse para todo el rango.

### ¿Qué pasa si no quiero que el valor se redondee sino que se trunque?

Cambia el formato personalizado a `"0.00"` con un modo de redondeo, o trunca manualmente antes de insertar el valor:

```csharp
double raw = Math.Truncate(12345.6789 * 100) / 100; // yields 12345.67
cell.PutValue(raw);
```

## Ejemplo completo funcional (listo para copiar y pegar)

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 2: Create a workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet ws = workbook.Worksheets[0];

        // Step 3: Access the cell at row 5, column 2 (zero‑based) and insert a number
        Cell cell = ws.Cells[5, 2];
        cell.PutValue(12345.6789);

        // Step 4: Apply a number format to show only two decimal places
        Style style = cell.GetStyle();
        style.Custom = "0.00";
        cell.SetStyle(style);

        // Step 5: Configure export options to get the formatted string
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,
            NumberFormat = "0.00"
        };
        cell.ExportOptions = exportOptions;

        // Step 6: Export the cell as a formatted string
        string formattedValue = cell.ExportString();
        Console.WriteLine($"Formatted cell value: {formattedValue}");

        // Optional: save the workbook for visual verification
        workbook.Save("DemoWorkbook.xlsx");
    }
}
```

**Salida esperada en la consola**

```
Formatted cell value: 12345.68
```

Abre `DemoWorkbook.xlsx` → ve a la celda **C6** → verás el mismo número con dos decimales.

## Conclusión

Acabamos de cubrir todo lo que necesitas para **create Excel workbook** en C#, **set cell number format**, **format number with two decimals**, entender **how to export Excel cell** datos, y **convert cell value to string** para procesamiento posterior.  

Los puntos clave son:

1. Utiliza `Workbook` y `Worksheet` para crear un archivo Excel en memoria.  
2. Aplica un estilo personalizado (`"0.00"`) para forzar la visualización con dos decimales.  
3. Adjunta `ExportTableOptions` a una celda cuando necesites una representación en cadena que respete el mismo formato.  

Desde aquí puedes experimentar—añadir más celdas, aplicar formato condicional o incluso generar gráficos. Si tienes curiosidad sobre el estilo de fuentes o agregar fórmulas, consulta la documentación de Aspose.Cells sobre **cell styling** y **formula evaluation**.

¿Tienes más preguntas sobre la automatización de Excel en C#? Deja un comentario, ¡y feliz codificación!

## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que se basan en las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y funcionales con explicaciones paso a paso para ayudarte a dominar funciones adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Dominar operaciones de libros de trabajo en Aspose.Cells .NET: cargar archivos Excel y rastrear precedentes de celdas de manera eficaz](/cells/english/net/workbook-operations/aspose-cells-net-master-workbook-operations/)
- [Dominar el formato de celdas Excel y la gestión de libros de trabajo con Aspose.Cells para .NET](/cells/english/net/formatting/excel-formatting-aspose-cells-net/)
- [Dominar Aspose.Cells para .NET: gestión avanzada de libros de trabajo y celdas Excel](/cells/english/net/advanced-features/excel-aspose-cells-net-create-manage/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}