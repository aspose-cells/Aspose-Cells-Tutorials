---
category: general
date: 2026-03-18
description: Crear un nuevo libro de trabajo y exportar Excel a TXT manteniendo la
  precisión numérica. Aprende cómo guardar la hoja de cálculo como TXT y convertir
  la hoja de cálculo a TXT de manera eficiente.
draft: false
keywords:
- create new workbook
- export excel to txt
- save excel as txt
- save worksheet as txt
- convert worksheet to txt
language: es
og_description: Crear un nuevo libro de trabajo y exportar Excel a TXT con precisión.
  Este tutorial muestra cómo guardar la hoja de cálculo como TXT y convertir la hoja
  de cálculo a TXT usando C#.
og_title: Crear nuevo libro de trabajo – Guía para exportar Excel a TXT
tags:
- Aspose.Cells
- C#
- Excel automation
title: Crear nuevo libro de trabajo – Exportar Excel a TXT con precisión total
url: /es/net/converting-excel-files-to-other-formats/create-new-workbook-export-excel-to-txt-with-full-precision/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crear nuevo libro – Exportar Excel a TXT con Precisión Completa

¿Alguna vez necesitaste **crear nuevo libro** en C# solo para volcar algunos datos a un archivo de texto plano? Tal vez estés extrayendo un informe de un sistema heredado y la herramienta downstream solo acepte un feed `.txt`. ¿La buena noticia? No tienes que sacrificar la precisión numérica, y ciertamente no necesitas crear manualmente cadenas CSV.

En esta guía recorreremos todo el proceso de **export excel to txt**, cubriendo desde la inicialización del libro hasta la preservación de ceros finales cuando **save worksheet as txt**. Al final tendrás un fragmento listo para ejecutar que podrás insertar en cualquier proyecto .NET—sin utilidades adicionales.

## Lo que Necesitarás

- **ASP.NET/ .NET 6+** (el código también funciona en .NET Framework 4.6+)  
- **Aspose.Cells for .NET** – la biblioteca que impulsa las clases `Workbook`, `Worksheet` y `TxtSaveOptions`. Puedes obtenerla desde NuGet con `Install-Package Aspose.Cells`.  
- Un conocimiento básico de C# (si te sientes cómodo con las sentencias `using`, ya estás listo).  

Eso es todo—sin interop de Excel, sin objetos COM y, definitivamente, sin concatenación manual de cadenas.  

---

## Paso 1: Inicializar un Nuevo Libro (Palabra Clave Principal)

Lo primero que debes hacer es **create new workbook**. Piensa en el libro como el lienzo en blanco donde luego pegarás números, texto o fórmulas.

```csharp
using System;
using Aspose.Cells;

namespace ExcelToTxtDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1: Create a new workbook and get the first worksheet
            Workbook workbook = new Workbook();                 // <‑‑ creates new workbook
            Worksheet worksheet = workbook.Worksheets[0];       // first sheet (index 0)
```

> **Por qué importa:** Instanciar `Workbook` sin cargar un archivo te brinda una hoja limpia. Luego puedes añadir datos programáticamente, lo cual es perfecto para escenarios de **convert worksheet to txt** donde no dispones de un `.xlsx` existente.

---

## Paso 2: Poblar Celdas – Mantener esos Ceros Finales

Una trampa común al volcar números a texto es perder los ceros finales (`123.45000` se convierte en `123.45`). Si los sistemas downstream dependen de campos de ancho fijo, esa pérdida puede romper todo.

```csharp
            // Step 2: Write a numeric value that contains trailing zeros
            // PutValue respects the data type; we’ll later tell the saver to keep precision.
            worksheet.Cells[0, 0].PutValue(123.45000);
```

> **Consejo profesional:** `PutValue` infiere automáticamente el tipo de dato. Si necesitas una cadena que parezca un número, usa `PutValue("123.45000")` en su lugar.

---

## Paso 3: Configurar Opciones de Guardado TXT – Preservar la Precisión Numérica

Aquí es donde ocurre la magia. Al activar `PreserveNumericPrecision`, le indicas a Aspose.Cells que escriba el valor exacto que ingresaste, incluidos los ceros finales insignificantes.

```csharp
            // Step 3: Configure TXT save options to keep the original numeric precision
            TxtSaveOptions txtSaveOptions = new TxtSaveOptions(SaveFormat.Txt)
            {
                PreserveNumericPrecision = true   // retain all digits, even trailing zeros
            };
```

> **¿Por qué habilitarlo?** Cuando **save excel as txt**, el comportamiento predeterminado recorta decimales innecesarios. Establecer `PreserveNumericPrecision = true` garantiza que la salida refleje el valor mostrado en la celda, lo cual es crítico para informes financieros o datos científicos.

---

## Paso 4: Guardar la Hoja como TXT – La Exportación Final

Ahora realmente **save worksheet as txt**. Puedes indicar cualquier ruta donde tengas permiso de escritura; el ejemplo usa una carpeta relativa llamada `output`.

```csharp
            // Step 4: Save the worksheet as a TXT file using the configured options
            string outputPath = "output/num-preserve.txt";
            worksheet.Save(outputPath, txtSaveOptions);

            Console.WriteLine($"File saved to {outputPath}");
        }
    }
}
```

> **Salida esperada** (`num-preserve.txt`):

```
123.45000
```

Observa que los ceros finales permanecen intactos—exactamente lo que solicitaste.

---

## Paso 5: Verificar el Resultado – Chequeo rápido de sanidad

Después de ejecutar el programa, abre `num-preserve.txt` en cualquier editor de texto. Deberías ver la única línea `123.45000`. Si ves `123.45` en su lugar, verifica que `PreserveNumericPrecision` esté configurado en `true` y que estés usando una versión reciente de Aspose.Cells (v23.10+).

---

## Variaciones Comunes y Casos Límite

### Exportar Múltiples Celdas o Rangos

Si necesitas **export excel to txt** para un rango completo, simplemente rellena más celdas antes de guardar:

```csharp
worksheet.Cells["A1"].PutValue(100);
worksheet.Cells["A2"].PutValue(200.500);
worksheet.Cells["A3"].PutValue(300.00);
```

Aspose escribirá cada celda en una nueva línea por defecto. También puedes cambiar el delimitador (tabulación, coma) mediante `txtSaveOptions.Separator`.

### Convertir Hoja a TXT con Codificaciones Diferentes

A veces los sistemas downstream requieren UTF‑8 BOM o ASCII. Ajusta la codificación así:

```csharp
txtSaveOptions.Encoding = System.Text.Encoding.UTF8;
```

### Manejo de Libros Grandes

Al trabajar con hojas masivas (cientos de miles de filas), considera transmitir la salida:

```csharp
txtSaveOptions.EnableCache = true; // writes data in chunks to reduce memory footprint
```

---

## Consejos Profesionales y Trucos

- **No olvides crear el directorio de salida** antes de llamar a `Save`, de lo contrario obtendrás una `DirectoryNotFoundException`.  
- **Cuidado con los separadores decimales específicos de la configuración regional**. Si tu entorno usa comas (`1,23`), establece `txtSaveOptions.DecimalSeparator = '.'` para forzar un punto.  
- **Compatibilidad de versiones**: la bandera `PreserveNumericPrecision` se introdujo en Aspose.Cells 20.6. Si usas una versión anterior, la bandera no existirá y tendrás que formatear la celda como texto antes de guardar.

---

![Crear nuevo libro de ejemplo](excel-to-txt.png "Crear nuevo libro")

*Texto alternativo de la imagen: "Crear nuevo libro y exportar Excel a TXT con precisión numérica preservada"*

---

## Recapitulación – Lo que Cubrimos

- **Create new workbook** usando Aspose.Cells.  
- Poblar una celda con un número que incluye ceros finales.  
- Establecer `TxtSaveOptions.PreserveNumericPrecision = true` para **save excel as txt** sin perder precisión.  
- Escribir el archivo en disco, verificando que la salida coincida con el valor original.  

Ese es el flujo completo de **convert worksheet to txt** en menos de 50 líneas de C#.

---

## Próximos Pasos y Temas Relacionados

Ahora que puedes **export excel to txt** con precisión perfecta, quizá quieras explorar:

- **Exportar a CSV** con delimitadores personalizados (`TxtSaveOptions.Separator`).  
- **Guardar como otros formatos de texto plano** como TSV (`SaveFormat.TabDelimited`).  
- **Procesamiento por lotes** de múltiples libros en una carpeta usando `Directory.GetFiles`.  
- **Integración con Azure Functions** para conversiones bajo demanda en la nube.

Cada uno de estos se basa en el mismo patrón `Workbook` → `Worksheet` → `TxtSaveOptions`, así que te sentirás como en casa.

---

### Reflexión Final

Si has seguido los pasos, ahora sabes exactamente cómo **create new workbook**, poblarlo y **save worksheet as txt** manteniendo cada dígito decimal que te importa. Es un pequeño fragmento de código, pero resuelve un dolor de cabeza sorprendentemente común cuando los pipelines heredados exigen entradas de texto plano.

Pruébalo, ajusta las opciones y deja que los datos fluyan exactamente como necesitas. ¡Feliz codificación!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}