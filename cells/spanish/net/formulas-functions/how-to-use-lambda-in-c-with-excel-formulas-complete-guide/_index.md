---
category: general
date: 2026-03-22
description: Cómo usar lambda en C# para trabajar con fórmulas de Excel. Aprende a
  escribir una fórmula en una celda, convertir un rango a una matriz, mostrar la matriz
  en la consola y calcular la cotangente en Excel.
draft: false
keywords:
- how to use lambda
- display array in console
- convert range to array
- write formula to cell
- calculate cotangent in excel
language: es
og_description: Cómo usar lambda en C# para manipular fórmulas de Excel, convertir
  un rango a matriz, escribir una fórmula en una celda, mostrar la matriz en la consola
  y calcular la cotangente en Excel.
og_title: Cómo usar Lambda en C# con fórmulas de Excel – Paso a paso
tags:
- C#
- Aspose.Cells
- Excel Automation
- Lambda Expressions
title: Cómo usar Lambda en C# con fórmulas de Excel – Guía completa
url: /es/net/formulas-functions/how-to-use-lambda-in-c-with-excel-formulas-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo usar Lambda en C# con fórmulas de Excel – Guía completa

¿Alguna vez te has preguntado **cómo usar lambda** al automatizar Excel desde C#? No estás solo. Muchos desarrolladores se topan con un obstáculo cuando necesitan combinar el poder de las nuevas funciones de matrices dinámicas de Excel con la capacidad `LAMBDA` de C#. ¿La buena noticia? En realidad es bastante sencillo una vez que ves cómo encajan las piezas.

En este tutorial recorreremos **escribir una fórmula en una celda**, **convertir un rango a un array**, **mostrar ese array en la consola**, e incluso **calcular la cotangente en Excel**—todo mientras te mostramos **cómo usar lambda** dentro de una llamada a `REDUCE`. Al final tendrás un fragmento ejecutable que podrás insertar en cualquier proyecto .NET que haga referencia a Aspose.Cells (o una biblioteca similar).

---

## Qué aprenderás

- Cómo **escribir fórmula en celda** usando C#.
- Cómo **convertir rango a array** con la función `EXPAND`.
- Cómo **mostrar array en consola** después del cálculo.
- Cómo **calcular cotangente en Excel** usando `COT` y `COTH`.
- La sintaxis exacta para **cómo usar lambda** dentro de la función `REDUCE` de Excel desde C#.

> **Prerequisite:** Necesitas una versión reciente de .NET (Core 6+ o .NET Framework 4.7+) y la biblioteca Aspose.Cells para .NET instalada vía NuGet.

---

## Paso 1: Configurar el libro y escribir la fórmula en la celda

Lo primero que hacemos es crear un libro nuevo y obtener la primera hoja. Luego **escribimos una fórmula en una celda** – en este caso `A1` contendrá el resultado de una llamada a `EXPAND`.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Write formula to A1 – we’ll expand B1:C2 into a 4‑by‑5 array later
        worksheet.Cells["A1"].Formula = "=EXPAND(B1:C2, 4, 5)";
```

**Por qué es importante:** Escribir la fórmula directamente desde el código te permite generar hojas de cálculo complejas al vuelo sin abrir Excel. Además prepara el escenario para el siguiente paso donde **convertimos rango a array**.

---

## Paso 2: Convertir rango a array con EXPAND

`EXPAND` es la forma que tiene Excel de transformar un rango pequeño en una matriz mayor. Al colocar la fórmula en `A1`, Excel derramará un bloque de 4 × 5 a partir de esa celda. Desde C#, no tenemos que copiar valores manualmente – la biblioteca hará el trabajo pesado cuando llamemos a `Calculate`.

```csharp
        // The EXPAND formula will spill into A1:E4 (4 rows × 5 columns)
        // No extra code needed – the workbook will handle the spill.
```

**Cómo usar lambda:** Aún no, pero espera. Primero necesitamos los datos en la hoja, luego los reduciremos con una lambda.

---

## Paso 3: Usar LAMBDA dentro de REDUCE – El núcleo de “Cómo usar lambda”

Excel 365 introdujo `REDUCE`, que acepta un **valor inicial**, un **rango**, y un **LAMBDA** que indica cómo combinar cada elemento. Desde C# simplemente asignamos la cadena de fórmula; la lambda vive dentro de la fórmula de Excel, no en el código C#.

```csharp
        // Reduce the spilled array by summing all its values.
        // This demonstrates how to use lambda inside REDUCE.
        worksheet.Cells["E1"].Formula = "=REDUCE(0, A1:D4, LAMBDA(acc, x, acc + x))";
```

**Explicación:**  
- `0` es el acumulador inicial (`acc`).  
- `A1:D4` es el rango que queremos procesar (las primeras cuatro columnas del derrame).  
- `LAMBDA(acc, x, acc + x)` le dice a Excel que sume cada celda (`x`) al acumulador.  

Eso es la esencia de **cómo usar lambda** para agregación en el contexto de una hoja de cálculo.

---

## Paso 4: Calcular cotangente en Excel – De grados a hiperbólico

Si necesitas resultados trigonométricos, las funciones `COT` y `COTH` de Excel son muy útiles. Las colocaremos en `G1` y `G2` respectivamente.

```csharp
        // Demonstrate trigonometric functions – cotangent and hyperbolic cotangent
        worksheet.Cells["G1"].Formula = "=COT(PI()/4)";   // Expected result: 1
        worksheet.Cells["G2"].Formula = "=COTH(1)";      // Hyperbolic cotangent of 1
```

**Por qué es útil:** Saber **calcular cotangente en Excel** puede ahorrarte escribir código matemático personalizado, sobre todo cuando el libro será compartido con usuarios que no son desarrolladores.

---

## Paso 5: Forzar el cálculo y obtener el array expandido

Ahora indicamos al libro que evalúe todas las fórmulas y luego extraemos la matriz derramada de `A1`. Aquí es donde **mostramos el array en la consola**.

```csharp
        // Force calculation of all formulas
        workbook.Calculate();

        // Retrieve the spilled array from A1 as a 2‑D object
        var expanded = worksheet.Cells["A1"].Value;

        // Pretty‑print the 2‑D array to the console
        Console.WriteLine("Expanded array from A1 (4×5):");
        if (expanded is object[,] matrix)
        {
            for (int r = 0; r < matrix.GetLength(0); r++)
            {
                for (int c = 0; c < matrix.GetLength(1); c++)
                {
                    Console.Write($"{matrix[r, c]}\t");
                }
                Console.WriteLine();
            }
        }
        else
        {
            Console.WriteLine("Unexpected data type.");
        }

        // Show the result of the REDUCE lambda
        Console.WriteLine($"\nSum of A1:D4 (via REDUCE lambda): {worksheet.Cells["E1"].Value}");

        // Show cotangent results
        Console.WriteLine($"Cotangent of π/4: {worksheet.Cells["G1"].Value}");
        Console.WriteLine($"Hyperbolic cotangent of 1: {worksheet.Cells["G2"].Value}");
    }
}
```

**Lo que verás:**  
- Una matriz 4 × 5 bien formateada impresa línea por línea.  
- La suma calculada por la lambda de `REDUCE`.  
- Los dos valores de cotangente.

Eso completa el flujo desde **escribir fórmula en celda** hasta **mostrar array en consola**.

---

## Ejemplo completo (listo para copiar y pegar)

A continuación tienes el programa completo que puedes colocar en una aplicación de consola. Recuerda agregar primero el paquete NuGet `Aspose.Cells` (`dotnet add package Aspose.Cells`).

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Initialize workbook and worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Step 2: Write EXPAND formula (convert range to array)
        worksheet.Cells["A1"].Formula = "=EXPAND(B1:C2, 4, 5)";

        // Step 3: Use REDUCE with LAMBDA (how to use lambda)
        worksheet.Cells["E1"].Formula = "=REDUCE(0, A1:D4, LAMBDA(acc, x, acc + x))";

        // Step 4: Calculate cotangent values (calculate cotangent in excel)
        worksheet.Cells["G1"].Formula = "=COT(PI()/4)";   // Expected: 1
        worksheet.Cells["G2"].Formula = "=COTH(1)";

        // Step 5: Force calculation
        workbook.Calculate();

        // Step 6: Retrieve and display the expanded array (display array in console)
        var expanded = worksheet.Cells["A1"].Value;
        Console.WriteLine("Expanded array from A1 (4×5):");
        if (expanded is object[,] matrix)
        {
            for (int r = 0; r < matrix.GetLength(0); r++)
            {
                for (int c = 0; c < matrix.GetLength(1); c++)
                {
                    Console.Write($"{matrix[r, c]}\t");
                }
                Console.WriteLine();
            }
        }
        else
        {
            Console.WriteLine("Unexpected data type.");
        }

        // Show REDUCE result
        Console.WriteLine($"\nSum of A1:D4 (via REDUCE lambda): {worksheet.Cells["E1"].Value}");

        // Show cotangent results
        Console.WriteLine($"Cotangent of π/4: {worksheet.Cells["G1"].Value}");
        Console.WriteLine($"Hyperbolic cotangent of 1: {worksheet.Cells["G2"].Value}");
    }
}
```

**Salida esperada en la consola (los valores variarán según el contenido predeterminado de B1:C2, que es 0 por defecto):**

```
Expanded array from A1 (4×5):
0   0   0   0   0
0   0   0   0   0
0   0   0   0   0
0   0   0   0   0

Sum of A1:D4 (via REDUCE lambda): 0
Cotangent of π/4: 1
Hyperbolic cotangent of 1: 1.31303528549933
```

Si lo deseas, rellena `B1:C2` con tus propios números antes de ejecutar – la matriz reflejará esos valores.

---

## Consejos profesionales y errores comunes

- **Consejo:** Si necesitas que el rango derramado empiece en otro lugar, simplemente cambia la celda objetivo (`A1`). La función `EXPAND` respeta el ancla.
- **Cuidado con:** Las celdas vacías en el rango de origen se convierten en `0` en la matriz derramada, lo que puede afectar la suma de `REDUCE`.
- **Caso límite:** Cuando el libro contiene fórmulas que dependen de funciones volátiles (p. ej., `NOW()`), llama a `workbook.Calculate()` después de establecer todas las fórmulas para asegurar que todo esté actualizado.
- **Nota de rendimiento:** Para derrames muy grandes, considera limitar el tamaño en la llamada a `EXPAND`; de lo contrario podrías asignar más memoria de la necesaria.
- **Compatibilidad:** The `

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}