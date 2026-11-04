---
category: general
date: 2026-10-01
description: Aprende cómo crear un libro de Excel en C#, aplicar un formato numérico
  personalizado, establecer los decimales de la celda y guardar el libro como XLSX
  en una guía completa paso a paso.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook c#
- apply custom number format
- how to format numbers excel
- set cell decimal places
- save workbook as xlsx
language: es
lastmod: 2026-10-01
og_description: Crear libro de Excel en C# con formato numérico personalizado, establecer
  los decimales de la celda y guardar el libro como XLSX. Sigue esta guía completa
  para obtener una salida numérica precisa.
og_image_alt: Screenshot of an Excel sheet showing numbers rounded to four significant
  digits
og_title: Crear libro de Excel en C# – formato numérico personalizado y exportación
  a XLSX
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Learn how to create Excel workbook C# and apply custom number format,
    set cell decimal places, and save workbook as XLSX in a complete step‑by‑step
    guide.
  headline: How to create Excel workbook C# with custom number formatting
  type: TechArticle
- description: Learn how to create Excel workbook C# and apply custom number format,
    set cell decimal places, and save workbook as XLSX in a complete step‑by‑step
    guide.
  name: How to create Excel workbook C# with custom number formatting
  steps:
  - name: Run the program (`dotnet run`).
    text: Run the program (`dotnet run`).
  - name: Open `SigDigits.xlsx`.
    text: Open `SigDigits.xlsx`.
  - name: Confirm that **A1** reads `123.5`.
    text: Confirm that **A1** reads `123.5`.
  - name: If you open the file’s XML (`.xlsx` is a zip archive), you’ll see the custom
      format `"0.######"` stored in the `<c>` element’s `s` attribute.
    text: If you open the file’s XML (`.xlsx` is a zip archive), you’ll see the custom
      format `"0.######"` stored in the `<c>` element’s `s` attribute.
  type: HowTo
tags:
- Excel
- C#
- Aspose.Cells
title: Cómo crear un libro de Excel en C# con formato numérico personalizado
url: /es/net/excel-custom-number-date-formatting/how-to-create-excel-workbook-c-with-custom-number-formatting/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo crear un libro de Excel en C# con formato numérico personalizado

Si necesitas **crear excel workbook c#** que muestre los números exactamente como deseas, esta guía te muestra cómo hacerlo en unos pocos pasos claros. Aprenderás a aplicar un formato numérico personalizado, establecer los decimales de una celda y, finalmente, **guardar el libro como xlsx** para su consumo posterior.

Trabajar con datos numéricos a menudo implica equilibrar precisión y legibilidad. Al final de este tutorial tendrás un patrón reutilizable que limita los dígitos mostrados a un número específico de cifras significativas mientras preserva el valor original en el archivo. No se requieren scripts externos—solo C# y la biblioteca Aspose.Cells.

## Requisitos previos

Antes de comenzar, asegúrate de tener:

* .NET 6.0 SDK o posterior instalado  
* Visual Studio 2022 (o cualquier IDE de C#)  
* El paquete NuGet **Aspose.Cells for .NET** (`Install-Package Aspose.Cells`) – esta biblioteca proporciona las clases `Workbook`, `Worksheet` y `ExportTableOptions` usadas en los ejemplos.  

Estos requisitos son mínimos; el mismo código funciona en .NET Core, .NET Framework e incluso en Azure Functions.

## Paso 1: Crear Excel workbook C# – inicializar el archivo

La primera operación es instanciar un nuevo objeto `Workbook`. Este objeto representa todo el archivo Excel en memoria y contiene automáticamente una hoja de cálculo predeterminada.

```csharp
using Aspose.Cells;

namespace ExcelDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Create a new workbook and get the first worksheet
            Workbook workbook = new Workbook();               // creates an empty .xlsx container
            Worksheet sheet = workbook.Worksheets[0];         // reference to the default sheet
```

**Por qué es importante:**  
Crear el libro de trabajo al inicio te brinda un lienzo limpio. La hoja predeterminada (`Worksheets[0]`) está lista para la entrada de datos, por lo que no necesitas agregar una nueva hoja a menos que tu escenario requiera varias pestañas.

## Paso 2: Escribir un valor numérico en una celda

Ahora coloca un número de ejemplo en la celda **A1**. El valor que usamos (`123.456789`) contiene más decimales de los que eventualmente queremos mostrar, lo que nos permite demostrar el redondeo más adelante.

```csharp
            // Step 2: Write a numeric value to cell A1
            sheet.Cells[0, 0].PutValue(123.456789); // row 0, column 0 = A1
```

**Consejo:** `PutValue` detecta automáticamente el tipo de dato, por lo que no tienes que convertir el número a cadena.

## Paso 3: Aplicar formato numérico personalizado – limitar decimales visibles

Para controlar cómo Excel muestra el número, creamos un `Style` con un **formato numérico personalizado**. El patrón `"0.######"` indica a Excel que muestre hasta seis decimales pero omita los ceros finales.

```csharp
            // Step 3: Define a custom number format (up to 6 decimal places) and apply it
            Style customStyle = workbook.CreateStyle();
            customStyle.Custom = "0.######";               // up to 6 decimals, no trailing zeros
            sheet.Cells[0, 0].SetStyle(customStyle);
```

**Cómo funciona:**  
La cadena de formato sigue la sintaxis de formato personalizado de Excel. `0` obliga a un dígito, mientras que `#` muestra un dígito solo si es significativo. Al combinarlos obtienes una visualización flexible que aún respeta la precisión original.

## Paso 4: Establecer decimales de celda – usando ExportTableOptions

Si necesitas **set cell decimal places** para datos exportados (p. ej., al convertir a un DataTable), Aspose.Cells te permite especificar el número de **cifras significativas**. Este paso asegura que el CSV o DataTable exportado respete las mismas reglas de redondeo que aplicaste en el libro.

```csharp
            // Step 4: Configure export options to limit the output to 4 significant digits
            ExportTableOptions exportOptions = new ExportTableOptions();
            exportOptions.SignificantDigits = 4;           // round to 4 significant figures
```

**¿Por qué usar `SignificantDigits`?**  
A diferencia de un recuento decimal fijo, las cifras significativas preservan la magnitud del número mientras limitan la precisión, lo que a menudo es lo que los analistas esperan al resumir datos.

## Paso 5: Exportar los datos de la hoja y **save workbook as xlsx**

Finalmente, exporta los datos (si necesitas un DataTable) y persiste el libro en disco. La llamada `ExportDataTable` respeta las `ExportTableOptions` que configuramos, y `workbook.Save` escribe un archivo XLSX estándar.

```csharp
            // Step 5: Export the worksheet data using the configured options and save the workbook
            sheet.ExportDataTable(sheet.Cells.MaxDisplayRange, true, exportOptions);
            workbook.Save("SigDigits.xlsx");               // saves to the application’s working folder
        }
    }
}
```

**Resultado esperado:**  
Al abrir *SigDigits.xlsx* en Excel, la celda **A1** muestra `123.5`. El valor subyacente sigue siendo `123.456789`, pero el número mostrado respeta la regla de 4 cifras significativas. Si exportas la hoja a un DataTable, el valor en la tabla también quedará redondeado a `123.5`.

---

## Aplicar formato numérico personalizado a celdas adicionales

Si necesitas formatear un rango en lugar de una sola celda, reutiliza el objeto `Style`:

```csharp
// Apply the same custom style to B2:C5
Range range = sheet.Cells.CreateRange("B2:C5");
range.ApplyStyle(customStyle, new StyleFlag { NumberFormat = true });
```

**Pro tip:** Re‑usar un objeto de estilo reduce la sobrecarga de memoria y garantiza un formato consistente en toda la hoja.

## Cómo formatear números en Excel usando C# – variaciones comunes

| Escenario | Cadena de formato | Resultado |
|----------|-------------------|-----------|
| Dos decimales fijos | `"0.00"` | `123.46` |
| Moneda (EE. UU.) | `"$#,##0.00"` | `$123.46` |
| Porcentaje con un decimal | `"0.0%"` | `12,346.0%` |
| Notación científica | `"0.00E+00"` | `1.23E+02` |

Elige el patrón que coincida con los requisitos de tu informe. Todos los patrones son compatibles con la propiedad `Style.Custom` demostrada anteriormente.

## Establecer decimales de celda dinámicamente según la entrada del usuario

A veces la precisión requerida no se conoce en tiempo de compilación. Puedes construir la cadena de formato en tiempo de ejecución:

```csharp
int decimals = 3; // could come from a UI textbox
string format = "0." + new string('#', decimals);
customStyle.Custom = format;
sheet.Cells["A2"].PutValue(987.654321);
sheet.Cells["A2"].SetStyle(customStyle);
```

**Caso límite:** Si `decimals` es cero, el formato se convierte en `"0"` (visualización entera). Siempre valida la entrada del usuario para evitar cadenas de formato mal formadas.

## Guardar el libro como XLSX – buenas prácticas

* **Usa rutas absolutas** al escribir en un directorio conocido (`Path.Combine(Environment.CurrentDirectory, "output.xlsx")`).  
* **Dispose** el `Workbook` si lo envuelves en una sentencia `using` para liberar recursos no administrados rápidamente:

```csharp
using (Workbook wb = new Workbook())
{
    // ...populate workbook...
    wb.Save(Path.Combine(@"C:\Exports", "Report.xlsx"));
}
```

* **Compatibilidad de versiones:** Aspose.Cells escribe archivos compatibles con Excel 2010‑2023, por lo que los usuarios posteriores no encontrarán problemas de formato.

---

## Ejemplo completo

A continuación tienes el programa completo que puedes copiar, pegar y ejecutar de inmediato. Incluye todas las directivas `using` necesarias, comentarios y manejo de errores.

```csharp
using System;
using System.IO;
using Aspose.Cells;

namespace ExcelDemo
{
    class Program
    {
        static void Main()
        {
            try
            {
                // 1️⃣ Create workbook and get the first worksheet
                Workbook workbook = new Workbook();
                Worksheet sheet = workbook.Worksheets[0];

                // 2️⃣ Write a high‑precision number to A1
                sheet.Cells[0, 0].PutValue(123.456789);

                // 3️⃣ Apply a custom number format (up to 6 decimals)
                Style customStyle = workbook.CreateStyle();
                customStyle.Custom = "0.######";
                sheet.Cells[0, 0].SetStyle(customStyle);

                // 4️⃣ Configure export options for 4 significant digits
                ExportTableOptions exportOptions = new ExportTableOptions
                {
                    SignificantDigits = 4
                };

                // 5️⃣ Export data (optional) and save the workbook as XLSX
                sheet.ExportDataTable(sheet.Cells.MaxDisplayRange, true, exportOptions);
                string outputPath = Path.Combine(Environment.CurrentDirectory, "SigDigits.xlsx");
                workbook.Save(outputPath);

                Console.WriteLine($"Workbook saved successfully at: {outputPath}");
                Console.WriteLine("Cell A1 displays: " + sheet.Cells["A1"].StringValue);
            }
            catch (Exception ex)
            {
                Console.Error.WriteLine($"Error creating workbook: {ex.Message}");
            }
        }
    }
}
```

**Pasos de verificación**

1. Ejecuta el programa (`dotnet run`).  
2. Abre `SigDigits.xlsx`.  
3. Confirma que **A1** muestra `123.5`.  
4. Si abres el XML del archivo (`.xlsx` es un archivo zip), verás el formato personalizado `"0.######"` almacenado en el atributo `s` del elemento `<c>`.

---

## Conclusión

En este tutorial aprendiste a **create excel workbook c#**, **apply custom number format**, **set cell decimal places** y **save workbook as xlsx** usando Aspose.Cells. La solución muestra tanto el formato visual dentro de Excel como el redondeo de exportación de datos mediante `ExportTableOptions`.  

A partir de aquí puedes:

* Extender el enfoque a rangos o tablas completas.  
* Combinar múltiples estilos (fuentes, bordes) con `StyleFlag`.  
* Automatizar la generación de informes iterando sobre fuentes de datos y aplicando la misma lógica de formato.  

¡Siéntete libre de experimentar con diferentes cadenas de formato, conteos decimales u opciones de exportación para adaptarlas a tus necesidades específicas de reporte. ¡Feliz codificación!

## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos con explicaciones paso a paso para ayudarte a dominar características adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Create Excel Workbook C# – Apply Currency Format and Import DataTable](/cells/english/net/excel-data-import-export/create-excel-workbook-c-apply-currency-format-and-import-dat/)
- [Create Excel Workbook C# – Step‑by‑Step Guide with Conditional Formatting](/cells/english/net/excel-conditional-formatting/create-excel-workbook-c-step-by-step-guide-with-conditional/)
- [Create Excel Workbook C# – Add Comment & Save as XLSX](/cells/english/net/excel-comment-annotation/create-excel-workbook-c-add-comment-save-as-xlsx/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}