---
category: general
date: 2026-02-15
description: Cómo usar WRAPCOLS para crear un diseño de dos columnas, agregar una
  fórmula y generar una matriz de secuencia en hojas de cálculo C# – guía paso a paso.
draft: false
keywords:
- how to use wrapcols
- create two column layout
- how to add formula
- how to create columns
- generate sequence array
language: es
og_description: Cómo usar WRAPCOLS para crear un diseño de dos columnas, agregar fórmulas
  y generar una matriz de secuencia en una hoja de cálculo C# – guía completa.
og_title: 'Cómo usar WRAPCOLS: diseño de dos columnas en C#'
tags:
- CSharp
- ExcelAutomation
- WorksheetFormula
title: 'Cómo usar WRAPCOLS: crear un diseño de dos columnas en C#'
url: /es/net/row-and-column-management/how-to-use-wrapcols-create-a-two-column-layout-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo usar WRAPCOLS: Crear un diseño de dos columnas en C#

¿Alguna vez te has preguntado **cómo usar WRAPCOLS** cuando necesitas una vista rápida de dos columnas dentro de una hoja de cálculo al estilo Excel? No estás solo. Muchos desarrolladores se topan con un obstáculo al intentar dividir una lista generada en columnas ordenadas sin escribir un bucle para cada celda. ¿La buena noticia? Con la función `WRAPCOLS` puedes colocar una única fórmula en `A1` y dejar que Excel (o un motor compatible) haga el trabajo pesado.

En este tutorial recorreremos **cómo agregar una fórmula** que crea un **diseño de dos columnas**, te mostraremos **cómo crear columnas** dinámicamente, e incluso **generar una matriz de secuencia** de valores al instante. Al final tendrás un fragmento de C# completamente ejecutable que puedes pegar en tu proyecto, ejecutar y ver aparecer instantáneamente un bloque ordenado de dos columnas.

## Lo que aprenderás

- El propósito de `WRAPCOLS` y por qué es una alternativa mejor que los bucles manuales.  
- Cómo **agregar una fórmula** a una celda de hoja de cálculo usando C#.  
- Cómo generar una matriz de secuencia con `SEQUENCE` y pasarla a `WRAPCOLS`.  
- Consejos para recalcular la hoja para que la fórmula se resuelva de inmediato.  
- Manejo de casos límite (p. ej., hojas vacías, recuentos de columnas personalizados).

No se requieren bibliotecas externas más allá de un paquete estándar de procesamiento de Excel; utilizaremos **ClosedXML** por su API sencilla, pero los conceptos se aplican a EPPlus, SpreadsheetGear o incluso Google Sheets a través de su API.

---

## Requisitos previos

- .NET 6.0 o posterior (el código compila en .NET Core y .NET Framework).  
- Una referencia a **ClosedXML** (`dotnet add package ClosedXML`).  
- Conocimientos básicos de C# – deberías estar cómodo con las sentencias `using` y la inicialización de objetos.  

Si ya tienes un libro de trabajo abierto, puedes omitir la parte de creación de archivo y pasar directamente a la sección de la fórmula.

---

## Paso 1: Configurar la hoja de cálculo (Cómo crear columnas)

Primero necesitamos un objeto `Worksheet` con el que trabajar. En ClosedXML lo obtienes de un `XLWorkbook`. El fragmento a continuación crea un nuevo libro de trabajo, agrega una hoja llamada *Demo* y obtiene una referencia llamada `worksheet` para mayor claridad.

```csharp
using ClosedXML.Excel;

namespace WrapColsDemo
{
    class Program
    {
        static void Main()
        {
            // Create a fresh workbook and add a worksheet named "Demo"
            using var workbook = new XLWorkbook();
            var ws = workbook.Worksheets.Add("Demo");

            // Rename for clarity – this is the worksheet we’ll manipulate
            var worksheet = ws;   // <-- same object, just a clearer name

            // --------------------------------------------------------------
            // Next step: write the WRAPCOLS formula
            // --------------------------------------------------------------
```

> **¿Por qué renombrar?**  
> Mantener el nombre de la variable corto (`worksheet`) hace que el código posterior sea más fácil de leer, especialmente cuando encadenas múltiples operaciones. También refleja el estilo de nomenclatura que verás en la mayoría de la documentación, reduciendo la carga cognitiva.

---

## Paso 2: Escribir la fórmula (Cómo agregar fórmula + generar matriz de secuencia)

Ahora llega la línea mágica. Colocaremos una fórmula en la celda **A1** que hace dos cosas:

1. **Generar una matriz de secuencia** de seis números (`SEQUENCE(6)` → 1,2,3,4,5,6).  
2. **Envolver esos números en dos columnas** (`WRAPCOLS(..., 2)`).

```csharp
            // Write the WRAPCOLS formula into A1
            worksheet.Cell("A1").FormulaA1 = "=WRAPCOLS(SEQUENCE(6), 2)";

            // --------------------------------------------------------------
            // Finally, force the engine to evaluate the formula
            // --------------------------------------------------------------
```

> **¿Qué está pasando?**  
> `SEQUENCE(6)` crea una matriz vertical `{1;2;3;4;5;6}`. `WRAPCOLS` luego toma esa matriz y la “envuelve” en el número especificado de columnas—en este caso **2**. El resultado es un bloque de 3 filas × 2 columnas que se ve así:

| A | B |
|---|---|
| 1 | 4 |
| 2 | 5 |
| 3 | 6 |

Si cambias el segundo argumento a **3**, obtendrías un diseño de tres columnas en su lugar. Ese es el núcleo de **cómo crear columnas** al vuelo sin bucles manuales.

---

## Paso 3: Recalcular la hoja de cálculo (Asegurando que la fórmula se evalúe)

ClosedXML no evaluará automáticamente las fórmulas cuando las escribas. Necesitas llamar a `Calculate()` en el libro de trabajo (o en la hoja de cálculo específica) para forzar la evaluación.

```csharp
            // Recalculate so the formula is evaluated immediately
            worksheet.Calculate();

            // Optional: save the workbook to inspect the result
            workbook.SaveAs("WrapColsDemo.xlsx");
        }
    }
}
```

> **Consejo profesional:** Si trabajas con libros de trabajo grandes, llama a `Calculate()` solo en las hojas que realmente cambiaron. Esto ahorra memoria y acelera el procesamiento.

Cuando abras `WrapColsDemo.xlsx` verás el diseño de dos columnas poblado ordenadamente en **A1:B3**. No se requirió código adicional para iterar filas o columnas – `WRAPCOLS` manejó todo.

---

## Paso 4: Verificar la salida (Qué esperar)

Después de ejecutar el programa, abre el archivo generado. Deberías ver:

| A | B |
|---|---|
| 1 | 4 |
| 2 | 5 |
| 3 | 6 |

Si los números aparecen verticalmente (es decir, todos en la columna A), verifica que hayas llamado a `worksheet.Calculate()` **después** de establecer la fórmula. Algunos motores también necesitan `workbook.Calculate()`; el fragmento anterior funciona con el evaluador incorporado de ClosedXML.

---

## Variaciones comunes y casos límite

### Cambiar el número de columnas

Para **crear un diseño de dos columnas** con un recuento de filas diferente, simplemente ajusta el tamaño de `SEQUENCE` o el segundo argumento de `WRAPCOLS`:

```csharp
worksheet.Cell("A1").FormulaA1 = "=WRAPCOLS(SEQUENCE(12), 3)";
```

Esto produce un bloque de 4 filas × 3 columnas (12 números divididos en tres columnas).

### Usar un recuento de columnas dinámico

Si el recuento de columnas proviene de una variable, insértalo con interpolación de cadenas:

```csharp
int colCount = 4;
worksheet.Cell("A1").FormulaA1 = $"=WRAPCOLS(SEQUENCE(8), {colCount})";
```

Ahora tienes **cómo agregar una fórmula** que se adapta en tiempo de ejecución.

### Hojas de cálculo vacías

Si la hoja de cálculo está vacía, `Calculate()` aún funciona – la fórmula poblará celdas comenzando en A1. Sin embargo, si luego eliminas filas/columnas que intersectan el rango de salida, podrías ver errores `#REF!`. Para evitarlo, limpia primero el rango de destino:

```csharp
worksheet.Range("A1:Z100").Clear(); // wipes any leftovers
```

### Compatibilidad

`WRAPCOLS` y `SEQUENCE` forman parte de las funciones de **Matriz dinámica** de Excel, introducidas en Office 365. Si apuntas a versiones anteriores de Excel, esas funciones no existirán y necesitarás un bucle manual. El evaluador de ClosedXML refleja el comportamiento más reciente de Excel, por lo que es seguro para entornos modernos.

---

## Ejemplo completo funcional (Listo para copiar y pegar)

```csharp
using ClosedXML.Excel;

namespace WrapColsDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create workbook & worksheet
            using var workbook = new XLWorkbook();
            var ws = workbook.Worksheets.Add("Demo");
            var worksheet = ws;   // clearer name

            // 2️⃣ Write WRAPCOLS formula that generates a sequence array
            worksheet.Cell("A1").FormulaA1 = "=WRAPCOLS(SEQUENCE(6), 2)";

            // 3️⃣ Force calculation so the formula resolves immediately
            worksheet.Calculate();

            // 4️⃣ Save the file (optional, but handy for verification)
            workbook.SaveAs("WrapColsDemo.xlsx");
        }
    }
}
```

**Resultado esperado:** Al abrir *WrapColsDemo.xlsx* se muestra un diseño ordenado de dos columnas con los números del 1 al 6 organizados como se describió anteriormente.

---

## Conclusión

Hemos cubierto **cómo usar WRAPCOLS** para **crear un diseño de dos columnas**, demostrado **cómo agregar una fórmula** programáticamente, y visto cómo `SEQUENCE` te permite **generar una matriz de secuencia** de valores sin un bucle. Al aprovechar las funciones de matrices dinámicas de Excel desde C#, puedes mantener tu código conciso, legible y mantenible.

A continuación, podrías explorar:

- **Crear recuentos de filas dinámicos** con `ROWS` o `COUNTA`.  
- **Estilizar la salida** (bordes, formatos numéricos) usando la API de estilos de ClosedXML.  
- **Exportar a CSV** después de que el diseño esté construido, para procesamiento posterior.

Pruébalo, ajusta el recuento de columnas y observa qué rápido puedes crear prototipos de hojas de cálculo complejas. ¡Feliz codificación!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}