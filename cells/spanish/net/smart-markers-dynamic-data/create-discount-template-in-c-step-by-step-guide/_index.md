---
category: general
date: 2026-02-14
description: Crea una plantilla de descuento rápidamente y aprende cómo aplicar el
  descuento en una hoja de cálculo, inyectar datos en la plantilla y definir un prefijo
  variable para los marcadores inteligentes.
draft: false
keywords:
- create discount template
- apply discount in spreadsheet
- inject data into template
- define variable prefix
language: es
og_description: Crea una plantilla de descuento con C#. Aprende a aplicar descuentos
  en una hoja de cálculo, inyectar datos en la plantilla y definir un prefijo variable
  para los marcadores inteligentes.
og_title: Crear plantilla de descuento – Recorrido completo en C#
tags:
- C#
- SmartMarker
- Spreadsheet Automation
title: Crear plantilla de descuento en C# – Guía paso a paso
url: /es/net/smart-markers-dynamic-data/create-discount-template-in-c-step-by-step-guide/
---

produce final content.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crear plantilla de descuento – Guía completa en C#

¿Alguna vez necesitaste **crear plantilla de descuento** para un informe de ventas pero no estabas seguro de cómo introducir los números en una hoja de cálculo automáticamente? No estás solo. En este tutorial te mostraremos exactamente cómo **crear plantilla de descuento**, luego **aplicar descuento en la hoja de cálculo** en celdas, **inyectar datos en la plantilla**, e incluso **definir prefijo de variable** para tus marcadores inteligentes, todo con código C# limpio.

Comenzaremos describiendo el problema, y luego pasaremos directamente a una solución funcional que puedes copiar y pegar. Al final tendrás un patrón reutilizable que funciona tanto si estás generando facturas, listas de precios o cualquier hoja de cálculo que necesite descuentos dinámicos.

---

## Lo que aprenderás

- Cómo diseñar una plantilla de hoja de cálculo consciente de descuentos.
- Cómo configurar un `VariablePrefix` / `VariableSuffix` personalizado para que los marcadores sean fáciles de identificar.
- Cómo pasar un objeto anónimo (`discountData`) al `SmartMarkerProcessor`.
- Cómo la fórmula resultante (`=IF(#Discount#>0, A1*(1-#Discount#), A1)`) calcula automáticamente el precio final.
- Consejos para manejar casos extremos como filas sin descuento o múltiples niveles de descuento.

**Requisitos previos** – un runtime .NET reciente (≥ .NET 6), una referencia a la biblioteca `Aspose.Cells` (o similar) que proporciona `SmartMarkerProcessor`, y una comprensión básica de la sintaxis de C#. Nada exótico.

---

## Paso 1: Crear una plantilla de descuento en tu hoja de cálculo

Primero, abre un nuevo libro de trabajo (o usa uno existente) y coloca un marcador de posición donde se aplicará el descuento. Piensa en la plantilla como un archivo Excel sencillo con “marcadores inteligentes” que el procesador reemplazará.

```csharp
using Aspose.Cells;          // SmartMarkerProcessor lives here
using System;

// Step 1: Load or create a workbook
Workbook wb = new Workbook();               // creates an empty .xlsx in memory
Worksheet ws = wb.Worksheets[0];
ws.Name = "Pricing";

// Put a header
ws.Cells["A1"].PutValue("Original Price");
ws.Cells["B1"].PutValue("Discounted Price");

// Sample data row – the formula will be injected later
ws.Cells["A2"].PutValue(100);               // original price = 100
ws.Cells["B2"].Formula = "=IF(#Discount#>0, A2*(1-#Discount#), A2)";
```

**Por qué es importante:** Al incrustar `#Discount#` dentro de la fórmula le indicamos al procesador exactamente dónde pertenece el valor del descuento. El `SmartMarkerProcessor` reemplazará `#Discount#` con el número que proporciones más adelante, dejando el resto de la fórmula sin cambios.

---

## Paso 2: Definir prefijo de variable para los marcadores inteligentes

De fábrica, muchas bibliotecas buscan `${Variable}` o `{{Variable}}`. En nuestro caso queremos un marcador limpio y legible, por lo que **definimos explícitamente el prefijo y sufijo de variable**.

```csharp
// Step 2: Configure how markers are identified
var smartMarkerOptions = new SmartMarkerOptions
{
    VariablePrefix = "#",   // start marker
    VariableSuffix = "#"    // end marker
};
```

**Consejo profesional:** Usar `#` mantiene los marcadores cortos y fáciles de detectar en la barra de fórmulas de Excel. Si alguna vez necesitas evitar conflictos con funciones existentes de Excel, elige un par diferente (p. ej., `[[` y `]]`).

---

## Paso 3: Inyectar datos en la plantilla usando SmartMarkerProcessor

Ahora introducimos el valor real del descuento. El procesador escaneará la hoja de cálculo, encontrará cada `#Discount#` y lo reemplazará con el valor del objeto anónimo que pasamos.

```csharp
// Step 3: Prepare the data that will be injected
var discountData = new { Discount = 0.10, Total = 100 };

// Run the processor – it mutates the workbook in‑place
ws.SmartMarkerProcessor.StartSmartMarkerProcessing(discountData, smartMarkerOptions);
```

Después de esta llamada, la fórmula en `B2` se convierte en:

```
=IF(0.1>0, A2*(1-0.1), A2)
```

Cuando el libro de trabajo calcula, `B2` muestra **90**, es decir, un descuento del 10 % aplicado al precio original de 100.

**Por qué funciona:** `StartSmartMarkerProcessing` recorre cada celda, busca el token `#Discount#` y sustituye el valor numérico. Como el token está dentro de una instrucción `IF`, la hoja de cálculo sigue manejando los casos en que el descuento pueda ser cero.

---

## Paso 4: Aplicar descuento en la hoja de cálculo – Verificar el resultado

Activemos el cálculo y mostremos el precio final en la consola. Este paso demuestra que el flujo de trabajo de **aplicar descuento en la hoja de cálculo** se completó con éxito.

```csharp
// Step 4: Force calculation and read the result
wb.CalculateFormula();                     // ensures all formulas are up‑to‑date
double discountedPrice = ws.Cells["B2"].DoubleValue;

Console.WriteLine($"Original: {ws.Cells["A2"].DoubleValue}");
Console.WriteLine($"Discounted (10%): {discountedPrice}");
```

**Salida esperada**

```
Original: 100
Discounted (10%): 90
```

Si cambias `discountData.Discount` a `0.25` y vuelves a ejecutar el procesador, la salida reflejará automáticamente un descuento del 25 % — sin código adicional.

---

## Paso 5: Manejo de casos extremos y descuentos múltiples

### Filas sin descuento

A veces un producto no está en oferta. Para mantener la fórmula robusta, el `IF` que colocaste antes ya cubre este escenario: cuando `#Discount#` es `0`, el precio original pasa sin cambios.

```csharp
var noDiscountData = new { Discount = 0.0 };
ws.SmartMarkerProcessor.StartSmartMarkerProcessing(noDiscountData, smartMarkerOptions);
wb.CalculateFormula();
Console.WriteLine($"No discount applied: {ws.Cells["B2"].DoubleValue}");
```

### Columnas de descuento múltiple

Si necesitas descuentos separados por fila, asigna a cada fila su propio marcador, p. ej., `#Discount1#`, `#Discount2#`, y pasa una colección:

```csharp
var multiDiscountData = new[]
{
    new { Discount = 0.05 },   // row 2
    new { Discount = 0.15 }    // row 3
};

ws.SmartMarkerProcessor.StartSmartMarkerProcessing(multiDiscountData, smartMarkerOptions);
```

El procesador coincide con los marcadores de forma secuencial, por lo que cada fila recibe el valor correcto.

---

## Ejemplo completo y funcional

A continuación tienes el programa completo, listo para copiar, que incorpora cada paso anterior. Guárdalo como `Program.cs`, agrega una referencia a `Aspose.Cells` y ejecútalo.

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // 1️⃣ Create workbook & template
        Workbook wb = new Workbook();
        Worksheet ws = wb.Worksheets[0];
        ws.Name = "Pricing";
        ws.Cells["A1"].PutValue("Original Price");
        ws.Cells["B1"].PutValue("Discounted Price");
        ws.Cells["A2"].PutValue(100);
        ws.Cells["B2"].Formula = "=IF(#Discount#>0, A2*(1-#Discount#), A2)";

        // 2️⃣ Define marker delimiters
        var smartMarkerOptions = new SmartMarkerOptions
        {
            VariablePrefix = "#",
            VariableSuffix = "#"
        };

        // 3️⃣ Inject a 10 % discount
        var discountData = new { Discount = 0.10 };
        ws.SmartMarkerProcessor.StartSmartMarkerProcessing(discountData, smartMarkerOptions);

        // 4️⃣ Calculate and display result
        wb.CalculateFormula();
        double original = ws.Cells["A2"].DoubleValue;
        double discounted = ws.Cells["B2"].DoubleValue;

        Console.WriteLine($"Original: {original}");
        Console.WriteLine($"Discounted (10%): {discounted}");

        // Optional: Save the workbook to verify manually
        wb.Save("DiscountedPricing.xlsx");
    }
}
```

Al ejecutar esto se imprimen los números esperados y se genera un archivo `DiscountedPricing.xlsx` que puedes abrir en Excel para ver la fórmula ya resuelta.

---

## Conclusión

Ahora sabes cómo **crear plantilla de descuento**, **aplicar descuento en la hoja de cálculo**, **inyectar datos en la plantilla**, y **definir prefijo de variable** para los marcadores inteligentes, todo con unas pocas líneas concisas de C#. El patrón escala — simplemente cambia el objeto anónimo o suministra una colección para actualizaciones masivas, y la misma plantilla manejará cualquier escenario de descuento que le presentes.

¿Listo para el siguiente nivel? Prueba:

- Agregar cálculos de impuestos junto con los descuentos.
- Obtener los porcentajes de descuento desde una base de datos en lugar de codificarlos directamente.
- Usar formato condicional para resaltar filas con descuentos altos.

Estas extensiones mantienen la idea central intacta mientras amplían la utilidad de tu plantilla de descuento.

¿Tienes preguntas o un caso de uso interesante? Deja un comentario abajo, ¡y feliz codificación!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}