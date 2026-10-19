---
category: general
date: 2026-03-30
description: Aprende cómo dar formato a números con separador usando Aspose.Cells
  en C#. Incluye establecer un formato numérico personalizado, agregar separador de
  miles, formatear decimales y cómo dar formato a una celda.
draft: false
keywords:
- format number with separator
- set custom number format
- add thousands separator
- format decimal places
- how to format cell
language: es
og_description: Formatear número con separador en C#. Esta guía muestra cómo establecer
  un formato numérico personalizado, agregar separador de miles, formatear decimales
  y cómo formatear una celda usando Aspose.Cells.
og_title: Formato de número con separador en C# – Tutorial de Aspose.Cells
tags:
- C#
- Aspose.Cells
- Number Formatting
title: Formatear número con separador en C# – Guía completa de Aspose.Cells
url: /es/net/excel-custom-number-date-formatting/format-number-with-separator-in-c-complete-aspose-cells-guid/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Formato de número con separador en C# – Guía completa de Aspose.Cells

¿Alguna vez necesitaste **formatear número con separador** en una hoja de cálculo pero no estabas seguro de qué llamada API usar? No eres el único—los desarrolladores luchan constantemente con separadores de miles, decimales y patrones personalizados al exportar datos.  

Buenas noticias: Aspose.Cells lo hace muy fácil. En este tutorial recorreremos un ejemplo del mundo real que **establece un formato numérico personalizado**, **agrega un separador de miles**, **formatea los decimales**, y muestra **cómo formatear una celda** para obtener la salida como una cadena. Al final tendrás un fragmento listo para ejecutar que puedes insertar en cualquier proyecto .NET.

## Qué cubre esta guía

* El paquete NuGet exacto que necesitas y cómo instalarlo.  
* Código paso a paso que crea un libro de trabajo, escribe un valor numérico y aplica un formato personalizado.  
* Por qué `ExportTableOptions.ExportAsString` es la forma preferida de obtener un valor formateado.  
* Errores comunes—como olvidar habilitar `ExportAsString` o usar la máscara de formato incorrecta.  
* Cómo ajustar la máscara de formato si necesitas un número diferente de decimales o un estilo de separador distinto.

No se requieren enlaces a documentación externa; todo lo que necesitas está aquí. Vamos a sumergirnos.

---

## Requisitos previos

| Requisito | Razón |
|-------------|--------|
| .NET 6.0 or later | Aspose.Cells 23.10+ se dirige a .NET Standard 2.0+, por lo que .NET 6 es seguro y actual. |
| Visual Studio 2022 (or any C# IDE) | Facilita la depuración y la gestión de paquetes. |
| Aspose.Cells for .NET NuGet package | Proporciona las clases `Workbook`, `Worksheet` y `ExportTableOptions` que utilizaremos. |

Puedes instalar el paquete mediante la consola del Administrador de paquetes:

```powershell
Install-Package Aspose.Cells
```

Eso es todo—sin DLLs adicionales, sin interop COM, solo una referencia NuGet.

## Paso 1: Inicializar un nuevo Workbook (Cómo formatear una celda)

Lo primero que hacemos es crear una nueva instancia de `Workbook`. Piensa en ella como un archivo de Excel vacío listo para recibir datos.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Create a new workbook – this is where we’ll format the cell.
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];
```

> **Por qué es importante:** `Workbook` es el punto de entrada para cada operación en Aspose.Cells. Al obtener la primera hoja de cálculo (`Worksheets[0]`) conseguimos un lienzo limpio sin necesidad de nombrar una hoja.

## Paso 2: Escribir un valor numérico en la celda objetivo

A continuación, colocamos un número bruto en la celda **A1**. El valor aún no está formateado—es simplemente un double.

```csharp
        // Step 2: Insert a raw numeric value.
        worksheet.Cells["A1"].PutValue(12345.6789);
```

> **Consejo profesional:** Usa `PutValue` en lugar de `PutString` cuando planeas aplicar formato numérico más adelante. Esto preserva el tipo de datos subyacente, permitiendo cálculos compatibles con Excel.

## Paso 3: Establecer formato numérico personalizado (Agregar separador de miles y formatear decimales)

Ahora llega el corazón del tutorial: definir una máscara de formato que indica a Aspose.Cells cómo mostrar el número. La máscara `#,##0.00` hace tres cosas:

1. **`#,##0`** – agrega un separador de miles (coma por defecto).  
2. **`.00`** – fuerza exactamente dos lugares decimales.  

Si necesitas un número diferente de decimales, simplemente cambia la cantidad de `0`s después del punto decimal.

```csharp
        // Step 3: Configure the custom number format.
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,          // Return the value as a formatted string.
            NumberFormat = "#,##0.00"       // Add thousands separator and fix to 2 decimals.
        };
```

> **Por qué usamos `ExportAsString`**: Por defecto, `ExportString` devuelve el valor bruto. Establecer `ExportAsString = true` obliga a la API a aplicar la máscara `NumberFormat` antes de convertir a texto. Esto es esencial cuando necesitas la representación exacta en cadena para informes, cargas JSON o visualización en UI.

## Paso 4: Exportar el texto formateado (Cómo formatear una celda)

Con las opciones listas, llamamos a `ExportString` en la misma celda. El método respeta la máscara que acabamos de definir y devuelve una cadena bien formateada.

```csharp
        // Step 4: Export the formatted value.
        string formattedCellText = worksheet.Cells["A1"].ExportString(exportOptions);

        // Step 5: Show the result.
        Console.WriteLine(formattedCellText); // Expected output: 12,345.68
    }
}
```

Ejecutar el programa imprime **`12,345.68`** en la consola—exactamente el formato que solicitamos.

> **Caso límite:** Si el número origen tiene más de dos decimales, la máscara lo redondea. Si necesitas truncamiento en lugar de redondeo, deberás pre‑procesar el valor con `Math.Truncate` antes de llamar a `PutValue`.

## Paso 5: Ajustar el formato – Variaciones comunes

### 5.1 Cambiar precisión decimal

¿Quieres tres decimales? Simplemente reemplaza la máscara:

```csharp
NumberFormat = "#,##0.000"   // → 12,345.679
```

### 5.2 Usar un separador de miles diferente

Algunas configuraciones regionales prefieren un espacio o un punto. Puedes incrustar el carácter directamente:

```csharp
NumberFormat = "# ##0.00"    // Uses a non‑breaking space as separator.
```

O confiar en la configuración cultural del libro de trabajo:

```csharp
workbook.Settings.CultureInfo = new System.Globalization.CultureInfo("de-DE");
NumberFormat = "#.##0,00";   // German style: 12.345,68
```

### 5.3 Prefijo o sufijo (Moneda, Porcentaje)

Agrega un signo de dólar o un signo de porcentaje directamente en la máscara:

```csharp
NumberFormat = "$#,##0.00";   // → $12,345.68
NumberFormat = "0.00%";       // → 1,234,568.00%
```

> **Nota:** La máscara distingue entre mayúsculas y minúsculas. `$` y `%` son símbolos literales; no afectan el valor numérico subyacente.

## Paso 6: Ejemplo completo (listo para copiar y pegar)

A continuación se muestra el programa completo que puedes copiar en una nueva aplicación de consola. Incluye todos los pasos, comentarios y la verificación de salida final.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialise workbook and worksheet.
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // 2️⃣ Write raw numeric value to A1.
        worksheet.Cells["A1"].PutValue(12345.6789);

        // 3️⃣ Define custom format: thousands separator + two decimals.
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,
            NumberFormat = "#,##0.00"
        };

        // 4️⃣ Export the formatted string.
        string result = worksheet.Cells["A1"].ExportString(exportOptions);

        // 5️⃣ Display the outcome.
        Console.WriteLine(result); // Output: 12,345.68

        // Optional: keep console open.
        Console.WriteLine("Press any key to exit...");
        Console.ReadKey();
    }
}
```

Ejecuta el programa (`dotnet run` desde la terminal o presiona F5 en Visual Studio) y verás el número formateado impreso exactamente como se muestra.

## Preguntas frecuentes (FAQ)

**P: ¿Esto funciona con versiones antiguas de Excel?**  
R: Sí. La máscara de formato sigue la sintaxis nativa de formato numérico de Excel, por lo que cualquier versión que entienda `#,##0.00` mostrará la misma cadena.

**P: ¿Qué pasa si necesito formatear un rango de celdas?**  
R: Recorre el rango deseado y aplica el mismo `ExportTableOptions` a cada celda, o establece la propiedad `Style.Custom` en el rango y luego llama a `ExportString` en una sola celda.

**P: ¿Puedo exportar directamente a CSV con estos formatos aplicados?**  
R: Por supuesto. Usa `Workbook.Save("output.csv", SaveFormat.CSV);` después de establecer el formato en cada celda. Aspose.Cells respeta el `Style` de la celda al generar CSV.

## Conclusión

Acabamos de mostrar cómo **formatear número con separador** en C# usando Aspose.Cells, cubriendo todo desde **establecer formato numérico personalizado** hasta **agregar separador de miles**, **formatear decimales**, y lo esencial **cómo formatear una celda** para exportar como cadena. El código es completamente autónomo, funciona con .NET 6+ y puede adaptarse a cualquier configuración regional o requisito de precisión.

A continuación, podrías explorar:

* Aplicar la misma técnica a fechas y horas (`NumberFormat = "dd‑MMM‑yyyy"`).  
* Automatizar exportaciones masivas donde cada columna necesita una máscara diferente.  
* Integrar las cadenas formateadas en informes PDF con Aspose.Words.

Prueba eso, y pronto serás la persona de referencia para el formateo de hojas de cálculo en tu equipo. ¡Feliz codificación!   (Image: ![Screenshot showing formatted number with separator in Aspose.Cells](image-placeholder.png){alt="Número formateado con separador mostrado en la salida de Aspose.Cells"} )

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}