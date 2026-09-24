---
category: general
date: 2026-03-30
description: Crear libro de Excel en C# usando Aspose.Cells. Aprenda a aplicar la
  función lambda en Excel, la función SEQUENCE en Excel, expandir matrices en Excel
  y guardar el libro como xlsx.
draft: false
keywords:
- create excel workbook c#
- lambda function excel
- save workbook as xlsx
- sequence function excel
- expand array excel
language: es
og_description: Crea rápidamente un libro de Excel con C#. Esta guía muestra cómo
  usar la función lambda en Excel, la función secuencia en Excel, expandir matrices
  en Excel y guardar el libro como xlsx.
og_title: Crear libro de Excel C# – Guía de Lambda, SEQUENCE y EXPAND
tags:
- Aspose.Cells
- C#
- Excel automation
title: Crear libro de Excel en C# – Guía de Lambda, SEQUENCE y EXPAND
url: /es/net/formulas-functions/create-excel-workbook-c-lambda-sequence-expand-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crear Libro de Excel C# – Guía de LAMBDA, SEQUENCE y EXPAND

¿Alguna vez necesitaste **crear libro de Excel C#** para un informe automatizado, pero no estabas seguro de qué llamadas a la API usar? No estás solo: muchos desarrolladores se topan con el mismo obstáculo al adentrarse por primera vez en la generación programática de Excel. En esta guía verás un ejemplo completo y ejecutable que cubre todo, desde la nueva **función SEQUENCE de Excel** hasta la poderosa **función LAMBDA de Excel**, e incluso cómo **expandir matrices en Excel**.  

También te mostraremos los pasos exactos para **guardar el libro como xlsx** y poder entregar el archivo a cualquiera que use Excel. Al final de este tutorial tendrás un fragmento sólido y listo para producción que puedes insertar en cualquier proyecto .NET. Sin enlaces vagos de “ver la documentación”, solo código que funciona hoy.

## Qué Necesitarás

- **.NET 6.0 o posterior** – el ejemplo está dirigido a .NET 6, pero cualquier versión reciente funciona.  
- **Aspose.Cells para .NET** – instálalo vía NuGet (`Install-Package Aspose.Cells`).  
- Un conocimiento básico de la sintaxis de C# (variables, objetos y expresiones lambda).  
- Un IDE con el que te sientas cómodo (Visual Studio, Rider o VS Code).  

Eso es todo. Sin interop COM adicional, sin Office instalado en el servidor—Aspose.Cells maneja todo en memoria.

## Crear Libro de Excel C# – Implementación Paso a Paso

A continuación dividimos el proceso en pasos manejables. Cada paso tiene un encabezado claro, un breve fragmento de código y una explicación de **por qué** lo hacemos. Si lo deseas, copia el bloque completo al final y ejecútalo como una aplicación de consola.

### Paso 1 – Inicializar un Nuevo Libro

Lo primero: necesitamos un objeto de libro en blanco que represente el archivo de Excel en memoria.

```csharp
using Aspose.Cells;

// Step 1: Create a new workbook and get the first worksheet
Workbook workbook = new Workbook();               // empty workbook
Worksheet sheet = workbook.Worksheets[0];         // default first sheet
```

*Por qué es importante:* `Workbook` es el punto de entrada para todas las operaciones de Aspose.Cells. Al obtener la primera `Worksheet` obtenemos un lienzo donde podemos escribir fórmulas, valores o aplicar formato.  

> **Consejo profesional:** Si necesitas varias hojas, simplemente llama a `workbook.Worksheets.Add()` y conserva una referencia a cada una.

### Paso 2 – Usar la función SEQUENCE de Excel para Generar Datos

La **sequence function excel** crea una matriz dinámica de números sin VBA. La colocaremos en la celda `A1` y dejaremos que Excel la expanda automáticamente.

```csharp
// Step 2: Generate a 5‑row, 1‑column array from a SEQUENCE
sheet["A1"].Formula = "EXPAND(SEQUENCE(3),5,1)"; // 1..3 padded with blanks
```

*Por qué es importante:* `SEQUENCE(3)` produce `[1,2,3]`. Envolverla con `EXPAND` fuerza el resultado a un rango de 5 filas, rellenando las filas extra con celdas vacías. Esto demuestra tanto **sequence function excel** como **expand array excel** en una sola operación.

### Paso 3 – Agregar Números con la función LAMBDA de Excel

Ahora mostraremos la capacidad de la **lambda function excel**. Sumaremos los números del 1 al 5 usando la nueva función `REDUCE`, que internamente depende de una lambda.

```csharp
// Step 3: Aggregate a sequence (sum 1..5) using REDUCE/LAMBDA
sheet["B1"].Formula = "REDUCE(0, SEQUENCE(5), LAMBDA(a,b, a+b))"; // result = 15
```

*Por qué es importante:* `REDUCE` itera sobre la matriz producida por `SEQUENCE(5)`, pasando cada elemento (`b`) a la lambda junto con el acumulador (`a`). La lambda `a+b` los suma, dejando `15` en `B1`. Esta es una forma limpia, solo con fórmulas, de realizar reducciones sin bucles en C#.

### Paso 4 – Aplicar Funciones Trigonométricas Directamente en Celdas

Las funciones matemáticas integradas de Excel son útiles para cálculos rápidos. Pondremos una cotangente y una cotangente hiperbólica en celdas adyacentes.

```csharp
// Step 4: Trigonometric functions directly in Excel cells
sheet["C1"].Formula = "COT(PI()/4)";   // evaluates to 1
sheet["D1"].Formula = "COTH(1)";      // hyperbolic cotangent of 1
```

*Por qué es importante:* Demuestra que puedes combinar funciones matemáticas clásicas con las nuevas fórmulas de matriz dinámica. No es necesario calcular estos valores en C# a menos que tengas una razón de rendimiento específica.

### Paso 5 – Calcular Todas las Fórmulas

Aspose.Cells no evalúa automáticamente las fórmulas cuando las asignas. Debes indicarle que calcule.

```csharp
// Step 5: Force calculation so that cells store the results
workbook.CalculateFormula();
```

*Por qué es importante:* Después de esta llamada, la propiedad `Value` de cada celda contiene el resultado evaluado, listo para guardarse o leerse nuevamente.

### Paso 6 – Guardar el Libro como Xlsx

Finalmente, persistimos el libro en disco usando el patrón **save workbook as xlsx**.

```csharp
// Step 6: Save the workbook to an Excel file (XLSX format)
string outputPath = Path.Combine(
    Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
    "NewFunctions.xlsx");

workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to: {outputPath}");
```

*Por qué es importante:* El método `Save` detecta automáticamente la extensión del archivo. Al usar “.xlsx” garantizamos que el archivo sea compatible con las versiones modernas de Excel. La ruta apunta al escritorio para un acceso fácil durante las pruebas.

### Ejemplo Completo Funcional

A continuación tienes el programa completo que puedes pegar en un nuevo proyecto de consola. Incluye todos los pasos anteriores, más un pequeño bloque de verificación que imprime los valores calculados en la consola.

```csharp
using System;
using System.IO;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Initialize workbook
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.Worksheets[0];

        // SEQUENCE + EXPAND
        sheet["A1"].Formula = "EXPAND(SEQUENCE(3),5,1)";

        // REDUCE with LAMBDA
        sheet["B1"].Formula = "REDUCE(0, SEQUENCE(5), LAMBDA(a,b, a+b))";

        // Trig functions
        sheet["C1"].Formula = "COT(PI()/4)";
        sheet["D1"].Formula = "COTH(1)";

        // Calculate formulas
        workbook.CalculateFormula();

        // Verify results (optional)
        Console.WriteLine("A1‑A5 (expanded SEQUENCE):");
        for (int i = 0; i < 5; i++)
        {
            Console.WriteLine($"  Row {i + 1}: {sheet.Cells[i, 0].Value ?? "blank"}");
        }
        Console.WriteLine($"B1 (sum 1‑5): {sheet["B1"].Value}");
        Console.WriteLine($"C1 (cot(π/4)): {sheet["C1"].Value}");
        Console.WriteLine($"D1 (coth(1)): {sheet["D1"].Value}");

        // Save workbook
        string outputPath = Path.Combine(
            Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
            "NewFunctions.xlsx");
        workbook.Save(outputPath);
        Console.WriteLine($"Workbook saved to: {outputPath}");
    }
}
```

**Salida esperada en la consola**

```
A1‑A5 (expanded SEQUENCE):
  Row 1: 1
  Row 2: 2
  Row 3: 3
  Row 4: blank
  Row 5: blank
B1 (sum 1‑5): 15
C1 (cot(π/4)): 1
D1 (coth(1)): 1.31303528549933
Workbook saved to: C:\Users\YourName\Desktop\NewFunctions.xlsx
```

Y cuando abras *NewFunctions.xlsx* verás los mismos números distribuidos en las primeras cuatro columnas.

![captura de pantalla de crear libro de Excel c# del libro de cálculo resultante](/images/create-excel-workbook-csharp.png)

## Casos límite, Consejos y Preguntas Frecuentes

- **¿Qué pasa si necesito más de una hoja?**  
  Simplemente llama a `workbook.Worksheets.Add()` y repite la asignación de fórmulas en cada nuevo objeto `Worksheet`.  

- **¿Puedo usar versiones antiguas de Excel?**  
  Las funciones de matriz dinámica (`SEQUENCE`, `EXPAND`, `REDUCE`) requieren Excel 365 o Excel 2021+. Si apuntas a versiones anteriores, utiliza fórmulas clásicas o calcula los valores en C# antes de escribirlos.  

- **¿Preocupaciones de rendimiento?**  
  Para miles de filas, establecer fórmulas en un rango y luego llamar a `CalculateFormula` suele ser más rápido que iterar y asignar valores uno por uno.  

- **¿Guardar en un stream en lugar de un archivo?**  
  `work

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}