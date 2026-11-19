---
category: general
date: 2026-11-19
description: Cómo repetir la hoja de cálculo al poblar Excel con datos de matriz.
  Aprende a generar múltiples hojas de cálculo y a poblar una hoja a partir de una
  lista en unos pocos pasos.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to repeat worksheet
- populate excel with array
- generate multiple worksheets
- populate worksheet from list
language: es
lastmod: 2026-11-19
og_description: Cómo repetir una hoja de cálculo usando SmartMarkerProcessor. Sigue
  esta guía para rellenar Excel con datos de matriz, generar múltiples hojas de cálculo
  y rellenar una hoja a partir de una lista.
og_image_alt: Screenshot showing repeated worksheets in an Excel workbook after processing
og_title: Cómo repetir una hoja de cálculo en Excel – guía paso a paso
schemas:
- author: GroupDocs
  dateModified: '2026-11-19'
  description: How to repeat worksheet while populating Excel with array data. Learn
    to generate multiple worksheets and populate worksheet from list in a few steps.
  headline: How to repeat worksheet in Excel with SmartMarkerProcessor
  type: TechArticle
- description: How to repeat worksheet while populating Excel with array data. Learn
    to generate multiple worksheets and populate worksheet from list in a few steps.
  name: How to repeat worksheet in Excel with SmartMarkerProcessor
  steps:
  - name: Expected output
    text: 'When you open the resulting workbook, you should see:'
  - name: Empty or null arrays
    text: 'If `Dept` is null or empty, the processor will not create any additional
      worksheets. To avoid a completely blank workbook, you can add a guard:'
  - name: Custom worksheet names
    text: 'The default naming scheme may not suit every reporting requirement. After
      processing, rename each sheet using a loop:'
  - name: Populating additional columns
    text: 'If you need to **populate excel with array** values beyond a single marker,
      extend the data object:'
  type: HowTo
tags:
- Excel automation
- SmartMarkerProcessor
- .NET
title: Cómo repetir la hoja de cálculo en Excel con SmartMarkerProcessor
url: /es/net/smart-markers-dynamic-data/how-to-repeat-worksheet-in-excel-with-smartmarkerprocessor/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo repetir una hoja de cálculo en Excel con SmartMarkerProcessor

Si necesitas **cómo repetir una hoja de cálculo** al generar informes de Excel, esta guía te muestra una solución completa y ejecutable. Al final del tutorial podrás **poblar Excel con array** de datos, **generar múltiples hojas de cálculo** y **poblar hoja de cálculo desde una lista** usando la biblioteca SmartMarkerProcessor.

Repetir una hoja de cálculo es un requisito común cuando cada departamento, región o período de tiempo necesita su propia pestaña. El ejemplo a continuación demuestra los pasos exactos, explica por qué cada configuración es importante y cubre casos límite como listas vacías o nombres personalizados.

## Requisitos previos

Antes de comenzar, asegúrate de tener:

- .NET 6.0 o posterior instalado
- Una referencia al paquete NuGet **GroupDocs.Viewer** (o equivalente) que contiene `SmartMarkerProcessor`
- Un libro de plantillas de Excel (`.xlsx`) con un marcador como `${repeat:Dept}` colocado en la fila que deseas repetir
- Familiaridad básica con C# y LINQ (opcional pero útil)

No se requieren bibliotecas de terceros adicionales.

## Paso 1: Crear la instancia de SmartMarkerProcessor

El procesador orquesta el reemplazo de marcadores y la duplicación de hojas. Instanciarlo sin argumentos usa las opciones predeterminadas.

```csharp
// Step 1: Create a SmartMarkerProcessor instance
SmartMarkerProcessor processor = new SmartMarkerProcessor();
```

Crear el procesador al principio te permite configurar opciones globales antes de aplicar cualquier dato. Esta es la base para **cómo repetir una hoja de cálculo** correctamente.

## Paso 2: Habilitar la repetición de hoja

Por defecto el procesador reemplaza los marcadores solo en la hoja actual. Establecer `RepeatWorksheet` a `true` indica al motor que clone la hoja completa para cada elemento en la colección de datos.

```csharp
// Step 2: Enable worksheet repetition for the ${repeat:Dept} marker
processor.Options.RepeatWorksheet = true;
```

Habilitar esta opción es la clave para **generar múltiples hojas de cálculo**: el procesador creará una nueva pestaña por cada elemento del array `Dept` y mantendrá el formato original.

## Paso 3: Preparar la fuente de datos como array o lista

SmartMarkerProcessor funciona con cualquier enumerable, pero usar un array deja clara la intención cuando deseas **poblar hoja de cálculo desde una lista**. Aquí creamos un objeto anónimo que contiene una propiedad `Dept` que almacena un array de strings.

```csharp
// Step 3: Prepare the data source with a list of departments
var data = new { Dept = new[] { "HR", "IT", "Finance" } };
```

Si ya tienes un `List<string>` puedes pasarlo directamente; el procesador lo tratará de la misma manera. Lo importante es que el nombre de la propiedad (`Dept`) coincida con el marcador `${repeat:Dept}` en la plantilla.

## Paso 4: Cargar la hoja de plantilla

Suponiendo que tienes un `ExcelPackage` (de EPPlus) o un objeto `Workbook`, recupera la hoja que deseas repetir. La variable `ws` representa esa hoja.

```csharp
// Example using EPPlus to load the template workbook
using var package = new OfficeOpenXml.ExcelPackage(new FileInfo("Template.xlsx"));
var ws = package.Workbook.Worksheets[0]; // first worksheet
```

Si prefieres otra biblioteca (p. ej., ClosedXML), el mismo principio se aplica: obtener un objeto hoja que implemente la interfaz requerida.

## Paso 5: Procesar la hoja con los datos

Ahora aplica los datos a la plantilla. El procesador clona la hoja para cada departamento, reemplaza el marcador `${repeat:Dept}` con el nombre real del departamento y deja el resto de la hoja sin cambios.

```csharp
// Step 5: Apply the data to the template worksheet (ws)
processor.Process(ws, data);
```

Una vez que `Process` finaliza, `ws` se convierte en la primera de varias hojas—una por departamento. El nombre de la hoja original se conserva, mientras que los duplicados reciben sufijos incrementales (p. ej., “Sheet1 (1)”, “Sheet1 (2)”). Puedes renombrarlos después si necesitas un esquema de nombres personalizado.

### Resultado esperado

Al abrir el libro resultante, deberías ver:

- **Sheet1** – la plantilla original (a menudo vacía o usada como maestra)
- **Sheet1 (1)** – poblada con “HR”
- **Sheet1 (2)** – poblada con “IT”
- **Sheet1 (3)** – poblada con “Finance”

Cada hoja contiene el mismo diseño pero con el nombre del departamento sustituido donde apareció `${repeat:Dept}`.

## Manejo de casos límite

### Arrays vacíos o nulos

Si `Dept` es nulo o está vacío, el procesador no creará hojas adicionales. Para evitar un libro completamente vacío, puedes añadir una protección:

```csharp
if (data.Dept != null && data.Dept.Any())
{
    processor.Process(ws, data);
}
else
{
    // Optionally write a warning or keep the original sheet unchanged
}
```

### Nombres de hoja personalizados

El esquema de nombres predeterminado puede no adaptarse a todos los requisitos de informes. Después del procesamiento, renombra cada hoja usando un bucle:

```csharp
for (int i = 1; i <= data.Dept.Length; i++)
{
    var sheet = package.Workbook.Worksheets[i]; // index 0 is the original
    sheet.Name = data.Dept[i - 1]; // use department name as tab title
}
```

### Poblar columnas adicionales

Si necesitas **poblar Excel con array** de valores más allá de un solo marcador, amplía el objeto de datos:

```csharp
var data = new
{
    Dept = new[]
    {
        new { Name = "HR", Headcount = 12 },
        new { Name = "IT", Headcount = 25 },
        new { Name = "Finance", Headcount = 8 }
    }
};
```

Luego ajusta los marcadores de la plantilla a `${repeat:Dept.Name}` y `${repeat:Dept.Headcount}`. El procesador repetirá la fila para cada departamento y rellenará ambas columnas.

## Ejemplo completo funcional

A continuación se muestra una aplicación de consola autocontenida que demuestra todo el flujo, desde la carga de la plantilla hasta el guardado del libro final.

```csharp
using System;
using System.IO;
using OfficeOpenXml;               // Install-Package EPPlus
using GroupDocs.Viewer.Markup;    // SmartMarkerProcessor namespace

class Program
{
    static void Main()
    {
        // 1️⃣ Create processor
        SmartMarkerProcessor processor = new SmartMarkerProcessor();

        // 2️⃣ Enable worksheet repetition
        processor.Options.RepeatWorksheet = true;

        // 3️⃣ Define data source (array of departments)
        var data = new { Dept = new[] { "HR", "IT", "Finance" } };

        // 4️⃣ Load template workbook (ensure Template.xlsx exists)
        var fileInfo = new FileInfo("Template.xlsx");
        using var package = new ExcelPackage(fileInfo);
        var ws = package.Workbook.Worksheets[0]; // first sheet contains ${repeat:Dept}

        // 5️⃣ Process template
        processor.Process(ws, data);

        // Optional: rename generated sheets
        for (int i = 1; i <= data.Dept.Length; i++)
        {
            var sheet = package.Workbook.Worksheets[i];
            sheet.Name = data.Dept[i - 1];
        }

        // Save the result
        var output = new FileInfo("Result.xlsx");
        package.SaveAs(output);

        Console.WriteLine("Workbook generated with repeated worksheets.");
    }
}
```

**Explicación de secciones clave**

- **Creación del procesador** – establece el motor que interpretará los marcadores.
- **Opción RepeatWorksheet** – activa la funcionalidad central que responde a *cómo repetir una hoja de cálculo*.
- **Fuente de datos** – usa un array (`new[]`) para satisfacer **poblar Excel con array**.
- **Carga de plantilla** – muestra una forma común de obtener un objeto hoja.
- **Procesamiento** – realiza la duplicación e inserción de datos en una sola llamada.
- **Renombrado** – muestra cómo convertir los nombres genéricos “(1)”, “(2)” en títulos significativos, un requisito típico después de **generar múltiples hojas de cálculo**.

Ejecutar este programa produce `Result.xlsx` con tres pestañas específicas por departamento, cada una poblada a partir del array.

## Errores comunes y consejos profesionales

- **Ortografía del marcador** – el marcador debe coincidir exactamente con el nombre de la propiedad (`${repeat:Dept}`). Un error tipográfico impide la repetición.
- **Índice de hoja** – después del procesamiento, la hoja original permanece en el índice 0; las hojas generadas siguen secuencialmente. Un índice incorrecto puede llevar a renombrar la pestaña equivocada.
- **Conjuntos de datos grandes** – generar cientos de hojas puede aumentar drásticamente el tamaño del archivo. Considera dividir los informes o usar una sola hoja con secciones agrupadas si el rendimiento se vuelve un problema.
- **Seguridad en hilos** – `SmartMarkerProcessor` no es seguro para subprocesos. Crea una instancia separada por hilo si procesas varios libros en paralelo.

## Conclusión

Ahora sabes **cómo repetir una hoja de cálculo** en Excel usando SmartMarkerProcessor, cómo **poblar Excel con array** de datos, cómo **generar múltiples hojas de cálculo** y cómo **poblar hoja de cálculo desde una lista** de manera eficiente. El ejemplo completo une todos los conceptos, y el paso opcional de renombrado te permite producir nombres de pestaña limpios y amigables.

A continuación, podrías explorar:

- Usar **populate worksheet from list** con objetos complejos (colecciones anidadas)
- Aplicar formato condicional después de la duplicación de hojas
- Exportar el libro generado a PDF o CSV para consumo posterior

¡Siéntete libre de adaptar el código a tus propios escenarios de informes y disfruta automatizando libros de Excel con confianza!

## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y explicaciones paso a paso para ayudarte a dominar funciones adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [How to Repeat Worksheets – Complete Guide for Excel Automation](/cells/english/net/smart-markers-dynamic-data/how-to-repeat-worksheets-complete-guide-for-excel-automation/)
- [Create Worksheet Per Item – How to Repeat Worksheet in C#](/cells/english/net/worksheet-operations/create-worksheet-per-item-how-to-repeat-worksheet-in-c/)
- [How to expand array in Excel and populate a template](/cells/english/net/templates-reporting/how-to-expand-array-in-excel-and-populate-a-template/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}