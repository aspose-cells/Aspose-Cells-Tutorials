---
category: general
date: 2026-03-22
description: Crear libro de Excel, agregar propiedades personalizadas, establecer
  el nombre de la hoja de cálculo y guardar como archivo binario XLSB usando C#.
draft: false
keywords:
- create excel workbook
- add custom properties
- save as xlsb
- set worksheet name
- write binary excel file
language: es
og_description: Crear un libro de Excel, agregar propiedades personalizadas, establecer
  el nombre de la hoja de cálculo y guardar como archivo binario XLSB usando C#.
og_title: Crear libro de Excel – Añadir propiedades personalizadas y guardar como
  XLSB
tags:
- C#
- Aspose.Cells
- Excel automation
title: Crear libro de Excel – Añadir propiedades personalizadas y guardar como XLSB
url: /es/net/document-properties/create-excel-workbook-add-custom-properties-and-save-as-xlsb/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crear libro de Excel – Añadir propiedades personalizadas y guardar como XLSB

¿Alguna vez necesitaste **crear un libro de Excel** programáticamente pero también mantener algunos metadatos adjuntos? Tal vez estés construyendo un motor de informes que etiqueta cada archivo con un ID de informe, el nombre del autor o el número de versión. En ese caso, aprender a **añadir propiedades personalizadas** mientras **estableces el nombre de la hoja** y finalmente **guardas como XLSB** te ahorrará mucho procesamiento manual posterior.

En este tutorial recorreremos un ejemplo completo y ejecutable que muestra exactamente cómo **escribir un archivo Excel binario** usando C#. Verás por qué el formato XLSB es la elección correcta para transportar propiedades personalizadas, cómo evitar los errores más comunes y qué hacer si necesitas soportar versiones antiguas de Excel.

---

## Lo que necesitarás

- **.NET 6+** (o .NET Framework 4.6+). El código funciona en cualquier runtime reciente.
- **Aspose.Cells for .NET** (prueba gratuita o con licencia). Proporciona las clases `Workbook`, `Worksheet` y `CustomProperties` utilizadas a continuación.
- Un IDE con el que te sientas cómodo – Visual Studio, Rider o incluso VS Code sirve.
- Acceso de escritura a una carpeta donde se guardará el archivo generado.

No se requieren otras bibliotecas de terceros.

---

## Paso 1: Instalar Aspose.Cells

Para comenzar, agrega el paquete NuGet de Aspose.Cells a tu proyecto:

```bash
dotnet add package Aspose.Cells
```

> **Consejo profesional:** Si estás en un servidor CI, almacena la clave de licencia en una variable de entorno y cárgala en tiempo de ejecución – esto evita que la marca de agua de “evaluación” se infiltre en tu salida.

---

## Paso 2: Crear libro de Excel – Visión general

La primera acción real es **crear un libro de Excel**. Este objeto representa todo el archivo en memoria y te brinda acceso a hojas de cálculo, estilos y propiedades personalizadas.

```csharp
using Aspose.Cells;

namespace ExcelDemo
{
    class Program
    {
        static void Main()
        {
            // Step 2.1: Instantiate a new workbook (empty by default)
            Workbook workbook = new Workbook();

            // The rest of the steps follow...
```

¿Por qué instanciar un `Workbook` nuevo en lugar de cargar una plantilla? Un libro en blanco garantiza que no haya estilos ocultos ni propiedades personalizadas residuales, lo cual es especialmente importante cuando pretendes **escribir un archivo Excel binario** para sistemas posteriores que esperan una hoja limpia.

---

## Paso 3: Establecer el nombre de la hoja (y por qué es importante)

Las hojas de Excel por defecto se llaman “Sheet1”, “Sheet2”, etc. Dar a una hoja un nombre significativo facilita mucho la lectura del procesamiento posterior—como Power Query o macros VBA.

```csharp
            // Step 3.1: Grab the first worksheet (index 0) and rename it
            Worksheet worksheet = workbook.Worksheets[0];
            worksheet.Name = "Data"; // clear, concise, and self‑describing
```

Si intentas asignar un nombre duplicado, Aspose.Cells lanzará una `ArgumentException`. Para estar seguro, puedes comprobar `Worksheets.Exists("Data")` antes de renombrar.

---

## Paso 4: Añadir propiedades personalizadas

Las propiedades personalizadas se almacenan en el XML interno del libro y viajan con el archivo sin importar el formato. Son perfectas para incrustar elementos como `ReportId` o `GeneratedBy`.

```csharp
            // Step 4.1: Add a numeric property
            workbook.CustomProperties.Add("ReportId", 12345);

            // Step 4.2: Add a string property
            workbook.CustomProperties.Add("GeneratedBy", "MyApp");
```

> **¿Por qué usar propiedades personalizadas?**  
> • Son accesibles a través del panel “Archivo → Información → Propiedades” de Excel.  
> • El código que consume el libro puede leerlas sin escanear el contenido de las celdas.  
> • Sobreviven a conversiones de formato (XLSX ↔ XLSB) porque forman parte de los metadatos del archivo.

También puedes almacenar fechas, booleanos o incluso blobs binarios, pero mantén la carga pequeña—Excel no es una base de datos.

---

## Paso 5: Guardar como XLSB (Escribir archivo Excel binario)

El formato XLSB almacena los datos en una estructura binaria, lo que hace que el archivo sea más pequeño y rápido de abrir. Más importante para este tutorial, **las propiedades personalizadas están integradas en el flujo binario**, garantizando que viajen con el archivo.

```csharp
            // Step 5.1: Define the output path
            string outputPath = Path.Combine(
                Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
                "WithCustomProps.xlsb");

            // Step 5.2: Save the workbook as a binary XLSB file
            workbook.Save(outputPath, SaveFormat.Xlsb);

            Console.WriteLine($"Workbook saved to {outputPath}");
        }
    }
}
```

### Resultado esperado

Después de ejecutar el programa, encontrarás `WithCustomProps.xlsb` en tu escritorio. Ábrelo en Excel, ve a **Archivo → Información → Propiedades**, y verás `ReportId` y `GeneratedBy` listados bajo *Personalizado*.

---

## Paso 6: Casos límite y preguntas frecuentes

### ¿Qué pasa si la carpeta de destino es de solo lectura?

Envuelve la llamada `Save` en un bloque `try/catch` y recurre a una ubicación escribible por el usuario, como `%TEMP%`. Esto evita que la aplicación se bloquee por errores de permisos.

```csharp
try
{
    workbook.Save(outputPath, SaveFormat.Xlsb);
}
catch (UnauthorizedAccessException)
{
    string fallback = Path.GetTempFileName().Replace(".tmp", ".xlsb");
    workbook.Save(fallback, SaveFormat.Xlsb);
    Console.WriteLine($"Saved to fallback location: {fallback}");
}
```

### ¿Puedo **guardar como XLSX** y seguir manteniendo las propiedades personalizadas?

Sí—simplemente cambia `SaveFormat.Xlsb` a `SaveFormat.Xlsx`. Las propiedades se almacenan en la misma parte XML, por lo que sobreviven al cambio de formato. Sin embargo, los archivos XLSX son más grandes porque son XML comprimido, mientras que XLSB ofrece mejor rendimiento para conjuntos de datos grandes.

### ¿Cómo leo las propiedades personalizadas más tarde?

```csharp
Workbook loaded = new Workbook(outputPath);
foreach (CustomProperty prop in loaded.CustomProperties)
{
    Console.WriteLine($"{prop.Name} = {prop.Value}");
}
```

Este fragmento imprime cada propiedad personalizada, facilitando que los servicios posteriores verifiquen la procedencia del archivo.

---

## Ejemplo completo

A continuación se muestra el programa completo que puedes copiar y pegar en un nuevo proyecto de consola. No falta ninguna pieza—todo, desde las declaraciones `using` hasta el `Console.WriteLine` final, está incluido.

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
            // 1️⃣ Create a new workbook instance
            Workbook workbook = new Workbook();

            // 2️⃣ Access the first worksheet and give it a meaningful name
            Worksheet worksheet = workbook.Worksheets[0];
            worksheet.Name = "Data";

            // 3️⃣ Add custom properties (they travel with the file)
            workbook.CustomProperties.Add("ReportId", 12345);
            workbook.CustomProperties.Add("GeneratedBy", "MyApp");

            // 4️⃣ Define where to save the binary XLSB file
            string outputPath = Path.Combine(
                Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
                "WithCustomProps.xlsb");

            // 5️⃣ Save the workbook as a binary XLSB file
            try
            {
                workbook.Save(outputPath, SaveFormat.Xlsb);
                Console.WriteLine($"✅ Workbook saved to {outputPath}");
            }
            catch (Exception ex)
            {
                Console.WriteLine($"❌ Failed to save workbook: {ex.Message}");
            }
        }
    }
}
```

Ejecuta el programa, abre el archivo resultante y verifica las propiedades personalizadas. Ese es todo el proceso de **crear un libro de Excel**, **añadir propiedades personalizadas**, **establecer el nombre de la hoja** y **guardar como xlsb** en un flujo ordenado.

---

## Conclusión

Ahora sabes exactamente cómo **crear un libro de Excel**, darle a su hoja un claro **establecer nombre de hoja**, incrustar metadatos útiles con **añadir propiedades personalizadas**, y finalmente **guardar como XLSB** para producir un archivo Excel compacto y binario. Este flujo de trabajo es fiable, funciona en distintas versiones de .NET y escala bien tanto si generas un informe como mil.

¿Qué sigue? Intenta añadir una tabla de datos a la hoja “Data”, experimenta con diferentes tipos de propiedades (fechas, booleanos), o cambia la salida a **guardar como xlsb** para conjuntos de datos masivos. También podrías explorar proteger el libro con una contraseña—Aspose.Cells lo hace con una sola línea.

¡No dudes en dejar un comentario si encuentras algún problema, o compartir cómo has ampliado este patrón en tus propios proyectos! ¡Feliz codificación!  

---  

![Captura de pantalla de crear libro de Excel](image.png){alt="Crear libro de Excel con propiedades personalizadas"}

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}