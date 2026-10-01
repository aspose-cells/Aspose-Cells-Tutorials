---
category: general
date: 2026-02-23
description: Crear un nuevo libro de trabajo programáticamente en C# y añadir una
  fórmula a una celda. Aprende a usar EXPAND y luego guarda el libro de Excel sin
  esfuerzo.
draft: false
keywords:
- create new workbook
- add formula to cell
- save excel workbook
- how to use expand
- create excel file programmatically
language: es
og_description: Crea un nuevo libro de trabajo programáticamente en C#. Añade una
  fórmula a una celda, aprende a usar EXPAND y guarda el libro de Excel en segundos.
og_title: Crear nuevo libro de trabajo en C# – Añadir fórmula y guardar archivo de
  Excel
tags:
- C#
- Excel Automation
- Aspose.Cells
title: Crear nuevo libro de trabajo en C# – Añadir fórmula y guardar archivo de Excel
url: /es/net/excel-workbook/create-new-workbook-in-c-add-formula-and-save-excel-file/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crear nuevo libro de trabajo en C# – Añadir fórmula y guardar archivo Excel

¿Alguna vez te has preguntado cómo **crear nuevos objetos workbook** desde código sin abrir Excel? No eres el único. Muchos desarrolladores se quedan atascados cuando necesitan generar una hoja de cálculo al vuelo—quizá para un informe, una exportación o un volcado rápido de datos.  

¿La buena noticia? En esta guía verás exactamente cómo **crear un nuevo workbook**, insertar una **fórmula en una celda**, y luego **guardar el libro de Excel** con solo unas pocas líneas de C#. También profundizaremos en **cómo usar expand** para generar matrices dinámicas sin copiar manualmente. Al final, podrás **crear archivos Excel programáticamente** y enviarlos a usuarios o servicios downstream.

## Requisitos previos

- .NET 6.0 o posterior (cualquier runtime reciente de .NET funciona)
- Aspose.Cells para .NET (versión de prueba o con licencia) – esta biblioteca nos proporciona las clases `Workbook` y `Worksheet` usadas a continuación.
- Un entendimiento básico de la sintaxis de C#—no se requiere un conocimiento profundo de Excel.

Si ya los tienes, ¡genial! Si no, obtén Aspose.Cells desde NuGet (`Install-Package Aspose.Cells`) y estarás listo para comenzar.

---

## Paso 1: Crear nuevo Workbook – La base

Para empezar, necesitamos instanciar un nuevo objeto workbook. Piensa en ello como abrir un archivo Excel completamente vacío.

```csharp
using Aspose.Cells;

public class ExcelGenerator
{
    public void Generate()
    {
        // Step 1: Create a new workbook (this is the core of create new workbook)
        Workbook workbook = new Workbook();
```

> **Por qué es importante:** La clase `Workbook` es el punto de entrada para cualquier manipulación de Excel. Al crear una nueva instancia, reservamos memoria para hojas, estilos y fórmulas—todo sin tocar el sistema de archivos.

---

## Paso 2: Acceder a la primera hoja de cálculo

Cada nuevo workbook viene con una hoja de cálculo predeterminada (llamada *Sheet1*). La obtendremos para poder colocar datos y fórmulas.

```csharp
        // Step 2: Access the first worksheet
        Worksheet worksheet = workbook.Worksheets[0];
```

> **Consejo profesional:** Si necesitas varias hojas, simplemente llama a `workbook.Worksheets.Add("MySheet")` y trabaja con el objeto `Worksheet` devuelto.

---

## Paso 3: Añadir fórmula a la celda – Usando EXPAND

Ahora viene la parte divertida: insertar una fórmula. La función `EXPAND` es perfecta cuando deseas convertir una matriz estática en un rango más grande y autollenado.

```csharp
        // Step 3: Add formula to cell A1 using EXPAND
        // This creates a 5‑row array from the constant {1,2,3}
        worksheet.Cells["A1"].Formula = "EXPAND({1,2,3},5,1)";
```

### Cómo funciona la fórmula EXPAND

| Argumento | Significado |
|----------|-------------|
| `{1,2,3}` | La matriz origen (una lista horizontal de tres números) |
| `5`       | Número deseado de filas en el resultado |
| `1`       | Número deseado de columnas (déjalo en 1 para mantenerlo vertical) |

Cuando Excel evalúa esto, produce una lista **vertical**:

```
A1: 1
A2: 2
A3: 3
A4: 0   (filled with zeros)
A5: 0
```

> **¿Por qué usar EXPAND?** Elimina la necesidad de copiar manualmente o de bucles VBA. La función remodela datos dinámicamente, haciendo que tus hojas de cálculo sean más robustas y fáciles de mantener.

---

## Paso 4: Guardar el libro de Excel – Persistir el resultado

Con la fórmula en su lugar, el paso final es escribir el workbook en disco. Puedes elegir cualquier carpeta a la que tengas permiso de escritura.

```csharp
        // Step 4: Save the workbook to view the result
        string outputPath = @"C:\Temp\ExpandFormula.xlsx";
        workbook.Save(outputPath);
    }
}
```

> **Lo que verás:** Abre `ExpandFormula.xlsx` en Excel, y la celda `A1` mostrará la matriz expandida. La fórmula permanece en la celda, de modo que si editas la matriz origen, la salida se actualiza automáticamente.

---

## Opcional: Verificar la salida programáticamente

Si prefieres no abrir Excel manualmente, puedes leer de nuevo los valores para confirmar que coinciden con lo esperado.

```csharp
        // Verify values without opening Excel
        for (int row = 0; row < 5; row++)
        {
            var value = worksheet.Cells[row, 0].Value; // column 0 = A
            Console.WriteLine($"Row {row + 1}: {value}");
        }
```

Ejecutar lo anterior imprimirá:

```
Row 1: 1
Row 2: 2
Row 3: 3
Row 4: 0
Row 5: 0
```

---

## Preguntas frecuentes y casos límite

| Pregunta | Respuesta |
|----------|-----------|
| **¿Puedo usar EXPAND con una matriz origen más grande?** | Claro. Simplemente cambia `{1,2,3}` por cualquier constante o rango de celdas, por ejemplo `EXPAND(A1:C1,10,1)`. |
| **¿Qué pasa si necesito un resultado horizontal?** | Intercambia los argumentos de fila/columna: `EXPAND({1,2,3},1,5)` producirá una expansión de 1 fila y 5 columnas. |
| **¿Funcionará esto en versiones antiguas de Excel?** | `EXPAND` está disponible a partir de Excel 365/2021. En versiones anteriores, tendrías que simular la matriz con `INDEX`/`SEQUENCE`. |
| **¿Necesito llamar a `workbook.CalculateFormula()`?** | No. Aspose.Cells evalúa automáticamente las fórmulas al guardar, por lo que los valores aparecen de inmediato. |
| **¿Cómo añadir más de una hoja antes de guardar?** | Llama a `workbook.Worksheets.Add("SecondSheet")` y repite los pasos de manipulación de celdas en la nueva hoja. |

---

## Ejemplo completo y funcional

A continuación tienes el programa completo, listo para ejecutar. Copia‑pega en una aplicación de consola, ajusta la ruta de salida y pulsa **F5**.

```csharp
using System;
using Aspose.Cells;

namespace ExcelAutomationDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Create new workbook
            Workbook workbook = new Workbook();

            // Access first worksheet
            Worksheet worksheet = workbook.Worksheets[0];

            // Add EXPAND formula to A1
            worksheet.Cells["A1"].Formula = "EXPAND({1,2,3},5,1)";

            // Optional: verify values in console
            workbook.CalculateFormula(); // ensures formulas are evaluated now
            for (int i = 0; i < 5; i++)
            {
                Console.WriteLine($"A{i + 1} = {worksheet.Cells[i, 0].Value}");
            }

            // Save the workbook
            string filePath = @"C:\Temp\ExpandFormula.xlsx";
            workbook.Save(filePath);
            Console.WriteLine($"Workbook saved to {filePath}");
        }
    }
}
```

**Salida esperada en la consola:**

```
A1 = 1
A2 = 2
A3 = 3
A4 = 0
A5 = 0
Workbook saved to C:\Temp\ExpandFormula.xlsx
```

Abre el archivo generado y verás los mismos números poblados en la columna **A**.

---

## Resumen visual

![Crear nuevo libro de trabajo ejemplo](create-new-workbook.png "Captura de pantalla que muestra un nuevo libro de trabajo creado con crear nuevo libro de trabajo en C#")

*La imagen ilustra el libro de trabajo recién generado con el resultado de EXPAND.*

---

## Conclusión

Ahora sabes cómo **crear un nuevo workbook**, **añadir una fórmula a una celda**, y **guardar el libro de Excel** usando C#. Al dominar **cómo usar expand**, puedes generar matrices dinámicas sin esfuerzo manual, y todo el proceso te permite **crear archivos Excel programáticamente** para cualquier escenario de automatización.

¿Qué sigue? Prueba a sustituir la matriz constante por una referencia a un rango, experimenta con diferentes dimensiones de `EXPAND`, o encadena múltiples fórmulas entre hojas. El mismo patrón funciona para gráficos, estilos e incluso tablas dinámicas—así que sigue explorando.

Si encontraste algún problema, deja un comentario abajo. ¡Feliz codificación y disfruta del poder de Excel programático!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}