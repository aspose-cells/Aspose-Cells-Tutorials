---
category: general
date: 2026-02-15
description: Crear un nuevo libro de trabajo y exportar Excel a TXT mientras se establece
  la precisión numérica. Aprende a establecer dígitos significativos y a limitar los
  dígitos significativos en C#.
draft: false
keywords:
- create new workbook
- export excel to txt
- set significant digits
- limit significant digits
- set numeric precision
language: es
og_description: Crear un nuevo libro de trabajo y exportar Excel a TXT, estableciendo
  dígitos significativos para la precisión numérica. Guía paso a paso en C#.
og_title: Crear nuevo libro de trabajo – Exportar Excel a TXT con precisión
tags:
- C#
- Aspose.Cells
- Excel automation
title: Crear nuevo libro de trabajo y exportar Excel a TXT con precisión
url: /es/net/excel-data-export-retrieval/create-new-workbook-and-export-excel-to-txt-with-precision/
---

.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crear nuevo libro de trabajo – Exportar Excel a TXT con formato numérico preciso

¿Alguna vez te has preguntado cómo **create new workbook** objetos en C# y volcarlos instantáneamente a un archivo de texto plano? No eres el único. En muchos escenarios de canalización de datos necesitamos **export Excel to TXT** manteniendo los números legibles, lo que significa limitar la cantidad de dígitos que aparecen después del punto decimal.  

En este tutorial recorreremos todo el proceso: desde crear un libro de trabajo nuevo, hasta configurar la exportación para que **sets significant digits** (también conocido como limitar dígitos significativos), y finalmente escribir el archivo en disco. Al final tendrás un fragmento listo‑para‑ejecutar que respeta tus requisitos de **numeric precision**—sin bibliotecas adicionales, sin trucos.

> **Pro tip:** Si ya estás usando Aspose.Cells, las clases mostradas a continuación forman parte de esa biblioteca. Si estás en una plataforma diferente, los conceptos siguen siendo válidos; simplemente intercambia las llamadas a la API.

---

## Qué necesitarás

- .NET 6+ (el código se compila en .NET Core y .NET Framework por igual)  
- Aspose.Cells para .NET (versión de prueba gratuita o con licencia) – instala vía NuGet: `dotnet add package Aspose.Cells`  
- Cualquier IDE que prefieras (Visual Studio, Rider, VS Code)  

Eso es todo. No hay archivos de configuración adicionales, ni pasos ocultos.

---

## Paso 1: Crear un nuevo libro de trabajo

Lo primero es **create new workbook**. Piensa en la clase `Workbook` como un archivo Excel vacío esperando hojas, celdas y datos.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Instantiate a fresh workbook – this is the core of create new workbook logic
        Workbook workbook = new Workbook();

        // (Optional) Add some sample data so you can see the effect of numeric precision later
        Worksheet sheet = workbook.Worksheets[0];
        sheet.Cells["A1"].PutValue(12345.678901);
        sheet.Cells["A2"].PutValue(0.000123456);
        sheet.Cells["A3"].PutValue(Math.PI);
```

> **Why this matters:** Al comenzar con un libro de trabajo limpio evitas cualquier formato oculto que pueda interferir con la configuración de precisión más adelante.

---

## Paso 2: Configurar opciones de guardado de texto – Establecer dígitos significativos

Ahora indicamos a Aspose.Cells cuántos **significant digits** queremos al escribir a un archivo `.txt`. La clase `TxtSaveOptions` expone una propiedad `SignificantDigits` que hace exactamente eso.

```csharp
        // Step 2: Prepare save options – limit numeric precision to 5 significant digits
        TxtSaveOptions txtOptions = new TxtSaveOptions
        {
            // This limits the output to 5 digits that matter, rounding the rest
            SignificantDigits = 5
        };
```

> **Explanation:** `SignificantDigits = 5` significa que el exportador mantendrá los cinco dígitos más importantes de cualquier número, sin importar dónde se encuentre el punto decimal. Es una forma práctica de **set numeric precision** sin formatear manualmente cada celda.

---

## Paso 3: Guardar el libro de trabajo como archivo de texto plano

Con el libro de trabajo y las opciones listas, finalmente **export Excel to txt**. El método `Save` recibe la ruta del archivo y el objeto de opciones que acabamos de configurar.

```csharp
        // Step 3: Write the workbook out as a TXT file using our precision settings
        string outputPath = @"C:\Temp\numbers.txt";
        workbook.Save(outputPath, txtOptions);

        System.Console.WriteLine($"Workbook exported to {outputPath} with 5 significant digits.");
    }
}
```

Ejecutar el programa produce un archivo que se ve así:

```
12346
0.00012346
3.1416
```

Observa cómo cada número respeta la regla de **limit significant digits** que establecimos antes.

---

## Paso 4: Verificar el resultado (Opcional pero recomendado)

Es fácil abrir el `numbers.txt` generado en cualquier editor, pero quizás quieras automatizar el paso de verificación, especialmente en pipelines de CI.

```csharp
        // Quick verification – read back the file and print each line
        foreach (var line in System.IO.File.ReadAllLines(outputPath))
        {
            System.Console.WriteLine($"Line: {line}");
        }
```

Si la consola muestra las tres líneas anteriores, has configurado correctamente **set significant digits** y la exportación funciona como se esperaba.

---

## Errores comunes y cómo evitarlos

| Problema | Por qué ocurre | Solución |
|----------|----------------|----------|
| Los números aparecen con demasiados decimales | `SignificantDigits` se dejó en el valor predeterminado (0) | Establece explícitamente `SignificantDigits` al recuento deseado |
| Se crea un archivo vacío | El libro de trabajo nunca recibió datos antes de guardarse | Pobla las celdas **before** llamando a `Save` |
| La ruta del archivo lanza `UnauthorizedAccessException` | Intentar escribir en una carpeta protegida | Usa una carpeta donde tengas permisos de escritura (p.ej., `C:\Temp` o `%USERPROFILE%\Documents`) |
| La precisión parece incorrecta para números muy pequeños | El recuento de dígitos significativos incluye ceros iniciales después del decimal | Recuerda que “significant” ignora los ceros iniciales; 0.000123456 con 5 dígitos se convierte en `0.00012346` |

---

## Ejemplo completo funcional (listo para copiar‑pegar)

A continuación se muestra el programa completo y autónomo. Pégalo en un nuevo proyecto de consola y pulsa **Run**.

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new workbook
        Workbook workbook = new Workbook();

        // Populate with sample numbers
        Worksheet sheet = workbook.Worksheets[0];
        sheet.Cells["A1"].PutValue(12345.678901);
        sheet.Cells["A2"].PutValue(0.000123456);
        sheet.Cells["A3"].PutValue(Math.PI);

        // 2️⃣ Set up export options – limit significant digits to 5
        TxtSaveOptions txtOptions = new TxtSaveOptions
        {
            SignificantDigits = 5
        };

        // 3️⃣ Export to TXT
        string outputPath = @"C:\Temp\numbers.txt";
        workbook.Save(outputPath, txtOptions);

        Console.WriteLine($"✅ Export completed: {outputPath}");
        Console.WriteLine("🔎 Verifying content:");
        foreach (var line in System.IO.File.ReadAllLines(outputPath))
        {
            Console.WriteLine($"   {line}");
        }
    }
}
```

**Salida esperada en la consola**

```
✅ Export completed: C:\Temp\numbers.txt
🔎 Verifying content:
   12346
   0.00012346
   3.1416
```

Y el archivo `numbers.txt` contendrá las tres líneas mostradas arriba.

---

## Próximos pasos: Ir más allá de lo básico

- **Export other formats** – Aspose.Cells también soporta CSV, HTML y PDF. Cambia `TxtSaveOptions` por `CsvSaveOptions` o `PdfSaveOptions` según sea necesario.  
- **Dynamic precision** – puedes calcular `SignificantDigits` en tiempo de ejecución basándote en la entrada del usuario o archivos de configuración.  
- **Multiple worksheets** – itera sobre `workbook.Worksheets` y exporta cada una a su propio archivo `.txt`.  
- **Localization** – controla el separador decimal (`.` vs `,`) mediante `CultureInfo` si necesitas coincidir con la configuración regional.  

Todas estas extensiones siguen basándose en la idea central que cubrimos: **create new workbook**, configurar la exportación y **set numeric precision** para que coincida con los requisitos de tus informes.

---

## Resumen

Hemos tomado una nueva instancia de **create new workbook**, la hemos rellenado con datos y demostrado cómo **export Excel to TXT** mientras **setting significant digits** para limitar la precisión de salida. El ejemplo completo funciona listo para usar, y la explicación cubrió el *por qué* detrás de cada línea para que puedas adaptarlo a tus propios proyectos.

Siéntete libre de experimentar—cambia el valor de `SignificantDigits`, agrega más hojas o cambia el formato de salida. Si encuentras algún problema, consulta la documentación de Aspose.Cells o deja un comentario abajo. ¡Feliz codificación!

---

![Ejemplo de crear nuevo libro de trabajo](/images/create-new-workbook.png "Captura de pantalla que muestra un IDE C# con el código de crear nuevo libro de trabajo")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}