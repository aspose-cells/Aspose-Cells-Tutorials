---
category: general
date: 2026-10-01
description: Aprende cómo agregar propiedades personalizadas a un libro de Excel usando
  Aspose.Cells. Esta guía también muestra cómo agregar el ID del proyecto y leer propiedades
  personalizadas.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add custom properties
- how to add custom
- excel custom properties
- add project id
- read custom properties
language: es
lastmod: 2026-10-01
og_description: Agrega propiedades personalizadas a un libro de Excel con Aspose.Cells.
  Sigue este tutorial completo para añadir un ID de proyecto, establecer la información
  del revisor y leer las propiedades personalizadas programáticamente.
og_image_alt: Screenshot of an Excel worksheet displaying custom properties added
  via Aspose.Cells
og_title: Agregar propiedades personalizadas al libro de Excel – guía paso a paso
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Learn how to add custom properties to an Excel workbook using Aspose.Cells.
    This guide also shows how to add project ID and read custom properties.
  headline: How to add custom properties to an Excel workbook
  type: TechArticle
- description: Learn how to add custom properties to an Excel workbook using Aspose.Cells.
    This guide also shows how to add project ID and read custom properties.
  name: How to add custom properties to an Excel workbook
  steps:
  - name: Open the saved `DataWithProps.xlsb` file in Microsoft Excel.
    text: Open the saved `DataWithProps.xlsb` file in Microsoft Excel.
  - name: Go to **File → Info → Properties → Advanced Properties**.
    text: Go to **File → Info → Properties → Advanced Properties**.
  - name: Select the **Custom** tab.
    text: Select the **Custom** tab.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: Cómo agregar propiedades personalizadas a un libro de Excel
url: /es/net/document-properties/how-to-add-custom-properties-to-an-excel-workbook/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo agregar propiedades personalizadas a un libro de Excel

Si necesita **agregar propiedades personalizadas** a un libro de Excel, esta guía le muestra exactamente cómo hacerlo con Aspose.Cells for .NET. También aprenderá cómo agregar un ID de proyecto, establecer un nombre de revisor y, más adelante, **leer propiedades personalizadas** del archivo.

Trabajar con metadatos personalizados le permite incrustar información específica del negocio directamente dentro de la hoja de cálculo, facilitando el seguimiento de la propiedad, la versión o cualquier otro contexto sin mantener una base de datos separada. Los pasos a continuación cubren el flujo de trabajo completo de extremo a extremo, desde la creación del libro hasta la persistencia de las nuevas propiedades.

## Requisitos previos

* .NET 6.0 o posterior instalado  
* Una licencia válida de Aspose.Cells for .NET (o una prueba gratuita)  
* Visual Studio 2022 (o cualquier IDE de C#)  

No se requieren paquetes NuGet adicionales más allá de `Aspose.Cells`.

## Paso 1: Configurar el proyecto e importar espacios de nombres

Cree una nueva aplicación de consola y agregue la referencia a Aspose.Cells:

```csharp
using System;
using Aspose.Cells;

namespace ExcelCustomPropertiesDemo
{
    class Program
    {
        static void Main()
        {
            // The rest of the code lives here
        }
    }
}
```

El espacio de nombres `Aspose.Cells` contiene las clases `Workbook`, `Worksheet` y `CustomPropertyCollection` que utilizaremos.

## Paso 2: Cargar un libro existente (o crear uno nuevo)

Puede comenzar con un archivo `.xlsb` existente o generar un nuevo libro. El ejemplo a continuación carga un archivo llamado **Data.xlsb** ubicado en una carpeta llamada `YOUR_DIRECTORY`.

```csharp
// Load the existing workbook
var workbookPath = @"YOUR_DIRECTORY\Data.xlsb";
var workbook = new Workbook(workbookPath);
```

Si el archivo no existe, reemplace el código con `new Workbook();` para crear un libro en blanco.

## Paso 3: Agregar propiedades personalizadas a la primera hoja de cálculo

La operación principal es **agregar propiedades personalizadas** a una hoja de cálculo. Aspose.Cells almacena las propiedades personalizadas en una colección que se comporta como un diccionario.

```csharp
// Get the first worksheet (index 0)
var worksheet = workbook.Worksheets[0];

// Add a numeric ProjectId property
worksheet.CustomProperties.Add("ProjectId", 12345);

// Add a string Reviewer property
worksheet.CustomProperties.Add("Reviewer", "John Doe");

// Optional: add a DateTime property for the creation timestamp
worksheet.CustomProperties.Add("CreatedOn", DateTime.UtcNow);
```

Usamos `CustomProperties.Add` en lugar de `CustomProperties["Name"] = value` porque el método `Add` crea la entrada si no existe y garantiza que se almacene el tipo de datos correcto. Este enfoque evita desajustes de tipo accidentales que podrían causar errores en tiempo de ejecución al leer los valores más tarde.

## Paso 4: Guardar el libro con las nuevas propiedades

Después de haber inyectado los metadatos, persista los cambios en un archivo nuevo para que el original permanezca intacto.

```csharp
// Save the workbook with the custom properties
var outputPath = @"YOUR_DIRECTORY\DataWithProps.xlsb";
workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to {outputPath}");
```

En este punto, el archivo de Excel contiene los metadatos personalizados que definió. Puede verificar las propiedades utilizando los pasos en la siguiente sección.

## Paso 5: Leer propiedades personalizadas de un libro

Leer **propiedades personalizadas de Excel** sigue el mismo patrón de colección. Este fragmento muestra cómo recuperar los valores que acabamos de almacenar.

```csharp
// Load the workbook that contains custom properties
var loadedWorkbook = new Workbook(outputPath);
var loadedWorksheet = loadedWorkbook.Worksheets[0];
var props = loadedWorksheet.CustomProperties;

// Retrieve each property safely
int projectId = props["ProjectId"] != null ? (int)props["ProjectId"].Value : -1;
string reviewer = props["Reviewer"] != null ? props["Reviewer"].Value.ToString() : "Unknown";
DateTime createdOn = props["CreatedOn"] != null ? (DateTime)props["CreatedOn"].Value : DateTime.MinValue;

Console.WriteLine($"ProjectId: {projectId}");
Console.WriteLine($"Reviewer: {reviewer}");
Console.WriteLine($"CreatedOn (UTC): {createdOn:u}");
```

El indexador `CustomPropertyCollection` devuelve un objeto `CustomProperty`; acceder a su propiedad `Value` le brinda los datos almacenados en su tipo original. Verificar `null` antes de convertir evita `NullReferenceException` si falta una propiedad.

### Salida esperada en la consola

```
ProjectId: 12345
Reviewer: John Doe
CreatedOn (UTC): 2026-10-01 12:34:56Z
```

La marca de tiempo reflejará el momento exacto en que llamó a `Add` en el paso 3.

## Consejo profesional: Actualizar una propiedad personalizada existente

Si necesita **agregar información personalizada** más tarde (por ejemplo, cambiar el revisor), use el setter de `CustomPropertyCollection`:

```csharp
// Change the reviewer name
if (props["Reviewer"] != null)
{
    props["Reviewer"].Value = "Jane Smith";
}
else
{
    // Property does not exist; add it
    props.Add("Reviewer", "Jane Smith");
}
```

Este patrón garantiza que la propiedad se actualice o se cree, lo cual es útil en flujos de trabajo iterativos como la generación automática de informes.

## Paso 6: Verificar las propiedades dentro de Excel (opcional)

También puede ver las propiedades personalizadas directamente en Excel:

1. Abra el archivo guardado `DataWithProps.xlsb` en Microsoft Excel.  
2. Vaya a **Archivo → Información → Propiedades → Propiedades avanzadas**.  
3. Seleccione la pestaña **Personalizado**.  

Verá las entradas `ProjectId`, `Reviewer` y `CreatedOn` listadas con sus respectivos valores.

## Ejemplo completo de trabajo

A continuación se muestra el programa completo y autónomo que combina todos los fragmentos anteriores. Copie el código en `Program.cs` y ejecútelo; la consola mostrará los valores recuperados.

```csharp
using System;
using Aspose.Cells;

namespace ExcelCustomPropertiesDemo
{
    class Program
    {
        static void Main()
        {
            // Paths (adjust to your environment)
            var sourcePath = @"YOUR_DIRECTORY\Data.xlsb";
            var resultPath = @"YOUR_DIRECTORY\DataWithProps.xlsb";

            // Load or create workbook
            var workbook = new Workbook(sourcePath);
            var worksheet = workbook.Worksheets[0];

            // Add custom properties
            worksheet.CustomProperties.Add("ProjectId", 12345);
            worksheet.CustomProperties.Add("Reviewer", "John Doe");
            worksheet.CustomProperties.Add("CreatedOn", DateTime.UtcNow);

            // Save the workbook
            workbook.Save(resultPath);
            Console.WriteLine($"Saved workbook with custom properties to {resultPath}");

            // Load the saved workbook to read properties
            var loadedWorkbook = new Workbook(resultPath);
            var loadedWorksheet = loadedWorkbook.Worksheets[0];
            var props = loadedWorksheet.CustomProperties;

            // Read properties
            int projectId = props["ProjectId"] != null ? (int)props["ProjectId"].Value : -1;
            string reviewer = props["Reviewer"] != null ? props["Reviewer"].Value.ToString() : "Unknown";
            DateTime createdOn = props["CreatedOn"] != null ? (DateTime)props["CreatedOn"].Value : DateTime.MinValue;

            Console.WriteLine($"ProjectId: {projectId}");
            Console.WriteLine($"Reviewer: {reviewer}");
            Console.WriteLine($"CreatedOn (UTC): {createdOn:u}");
        }
    }
}
```

Ejecutar este programa produce la salida de consola mostrada anteriormente y crea `DataWithProps.xlsb` que contiene los metadatos incrustados.

## Preguntas frecuentes y casos límite

| Pregunta | Respuesta |
|---|---|
| **¿Puedo almacenar tipos no primitivos?** | Aspose.Cells admite `string`, `int`, `double`, `DateTime` y `bool`. Para objetos complejos, sérialícelos a JSON o XML primero y almacene la cadena. |
| **¿Qué pasa si el libro está protegido con contraseña?** | Abra el libro con una contraseña (`new Workbook(path, password)`) antes de acceder a `CustomProperties`. Las propiedades siguen siendo accesibles después de la descifrado. |
| **¿Las propiedades personalizadas sobreviven a la conversión de formato?** | Al guardar en un formato diferente (p. ej., `.xlsx`), Aspose.Cells conserva las propiedades personalizadas siempre que el formato de destino las admita. |
| **¿Cómo eliminar una propiedad personalizada?** | Utilice `worksheet.CustomProperties.Remove("PropertyName");`. Esto elimina la entrada de la colección. |

## Próximos pasos

Ahora que sabe **agregar propiedades personalizadas**, podría explorar temas relacionados como:

* **excel custom properties** para el versionado de documentos  
* **read custom properties** de múltiples hojas de cálculo en un solo libro  
* Usar **Aspose.Cells** para crear tablas dinámicas que referencien metadatos personalizados  
* Exportar el libro a PDF mientras se preservan las propiedades personalizadas  

Experimente con diferentes tipos de datos, combine propiedades personalizadas con comentarios de celdas, o integre los metadatos en un sistema de gestión documental más amplio.

---

**¿Listo para automatizar sus informes de Excel?** Agregue el código anterior a su proyecto, ajuste los nombres de las propiedades para que coincidan con sus necesidades empresariales, y tendrá una hoja de cálculo auto‑descriptiva lista para el procesamiento posterior.

## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que se basan en las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y funcionales con explicaciones paso a paso para ayudarle a dominar funciones adicionales de la API y explorar enfoques de implementación alternativos en sus propios proyectos.

- [Crear libro de Excel – Agregar propiedades personalizadas y guardar como XLSB](/cells/english/net/document-properties/create-excel-workbook-add-custom-properties-and-save-as-xlsb/)
- [Cómo acceder a propiedades de documento personalizadas en Excel usando Aspose.Cells para .NET](/cells/english/net/workbook-operations/access-custom-excel-properties-aspose-cells-net/)
- [Dominar las propiedades personalizadas de Excel usando Aspose.Cells .NET para una gestión de datos mejorada](/cells/english/net/data-manipulation/excel-custom-properties-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}