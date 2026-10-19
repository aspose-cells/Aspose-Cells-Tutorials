---
category: general
date: 2026-09-21
description: Configure SmartMarkerOptions ArrayAsSingle en C# para exportar matrices
  JSON como un único valor de celda en un libro de Excel.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- configure smartmarkeroptions arrayassingle
- Aspose.Cells smart markers
- export JSON array
- C# DataTable
- Workbook ProcessSmartMarkers
language: es
lastmod: 2026-09-21
og_description: Configura SmartMarkerOptions ArrayAsSingle en C# para exportar matrices
  JSON como un único valor de celda. Aprende la solución completa paso a paso.
og_image_alt: Screenshot of an Excel sheet showing a JSON array stored in a single
  cell after using SmartMarkerOptions
og_title: Configura SmartMarkerOptions ArrayAsSingle en C# – guía completa
schemas:
- author: Aspose
  dateModified: '2026-09-21'
  description: Configure SmartMarkerOptions ArrayAsSingle in C# to export JSON arrays
    as a single cell value in an Excel workbook.
  headline: Configure SmartMarkerOptions ArrayAsSingle in C# for JSON arrays
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
title: Configurar SmartMarkerOptions ArrayAsSingle en C# para arreglos JSON
url: /es/net/smart-markers-dynamic-data/configure-smartmarkeroptions-arrayassingle-in-c-for-json-arr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Configurar SmartMarkerOptions ArrayAsSingle en C# para matrices JSON

Si necesita **configurar SmartMarkerOptions ArrayAsSingle** al generar archivos Excel con Aspose.Cells, esta guía le muestra exactamente cómo hacerlo. Verá cómo mantener una matriz JSON intacta en una sola celda en lugar de distribuir sus elementos en varias filas.

Trabajar con datos JSON en hojas de cálculo a menudo implica elegir entre una vista aplanada y una representación compacta. En muchos escenarios de informes —como almacenar una lista de etiquetas o un conjunto de identificadores— desea que la cadena JSON completa permanezca en una sola celda. La bandera **ArrayAsSingle** en `SmartMarkerOptions` hace eso posible.

En este tutorial usted:

* Crear un `DataTable` que contenga una matriz JSON en una columna.
* Colocar Smart Markers en una hoja de cálculo Excel.
* **Configurar SmartMarkerOptions ArrayAsSingle** para que la matriz JSON se trate como un valor de celda único.
* Procesar los marcadores y guardar el libro de trabajo.
* Verificar la salida.

> **Requisitos previos** – Necesita la biblioteca Aspose.Cells para .NET (v23.12 o posterior) y un entorno de desarrollo .NET (se recomienda Visual Studio 2022). Se asume conocimiento básico de C# y DataTables.

---

## Paso 1: Preparar la fuente de datos con una matriz JSON

Primero, cree un `DataTable` que imite los datos que recibiría de un servicio o una base de datos. La columna **Names** contiene una cadena codificada en JSON que representa una matriz de nombres.

```csharp
using System;
using System.Data;
using Aspose.Cells;

DataTable dataTable = new DataTable();
dataTable.Columns.Add("Id", typeof(int));
dataTable.Columns.Add("Names", typeof(string));

// Store the JSON array as a plain string
dataTable.Rows.Add(1, "[\"Alice\",\"Bob\"]");
```

*¿Por qué este paso?*  
Los Smart Markers leen datos directamente de objetos .NET. Al colocar la matriz JSON en una columna de tipo cadena, conserva la sintaxis JSON exacta, que luego puede escribirse en una celda sin cambios.

---

## Paso 2: Insertar Smart Markers en un nuevo libro de trabajo

Cree un libro de trabajo nuevo, seleccione la primera hoja de cálculo y escriba Smart Markers que hagan referencia a toda la tabla y a la columna **Names** específica.

```csharp
// Create a new workbook and get the first worksheet
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.Worksheets[0];

// Smart marker for the entire table (optional, shown for completeness)
worksheet.Cells["A1"].PutValue("&=dataTable");

// Smart marker that targets only the Names column
worksheet.Cells["A2"].PutValue("&=dataTable.Names");
```

El marcador `&=dataTable.Names` indica a Aspose.Cells que reemplace la celda con el valor de la columna **Names** para cada fila en `dataTable`. Como solo tenemos una fila, el marcador se procesará una vez.

---

## Paso 3: **Configurar SmartMarkerOptions ArrayAsSingle**

Por defecto, Aspose.Cells expande una cadena similar a una matriz en filas separadas. Establecer `ArrayAsSingle` en `true` anula ese comportamiento, obligando a que la cadena JSON completa permanezca en una sola celda.

```csharp
SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions
{
    // Export the JSON array as a single cell value
    ArrayAsSingle = true
};
```

*¿Por qué habilitar `ArrayAsSingle`?*  
Cuando `ArrayAsSingle` es `false`, el motor interpreta `["Alice","Bob"]` como dos valores separados y los escribe en filas adyacentes. Establecerlo en `true` trata la cadena como un valor atómico, lo cual es esencial para preservar el formato JSON dentro de Excel.

---

## Paso 4: Procesar los Smart Markers con las opciones configuradas

Ahora ejecute el motor Smart Marker, pasando el objeto de opciones que acaba de configurar.

```csharp
// Process smart markers using the custom options
workbook.ProcessSmartMarkers(smartMarkerOptions);
```

Durante el procesamiento, Aspose.Cells lee el `dataTable`, aplica los marcadores y respeta la bandera `ArrayAsSingle`, dejando la matriz JSON sin modificar.

---

## Paso 5: Guardar el libro de trabajo y verificar el resultado

Finalmente, escriba el libro de trabajo en disco. Abra el archivo generado en Excel o cualquier visor de hojas de cálculo para confirmar que la celda **A2** contiene la cadena JSON exacta.

```csharp
// Save the resulting workbook
string outputPath = @"C:\Temp\SmartMarkerJson.xlsx";
workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to {outputPath}");
```

### Resultado esperado

| A   |
|-----|
| **["Alice","Bob"]** |

La celda **A2** muestra la matriz JSON como un valor de texto único, exactamente como está almacenada en el `DataTable`. No se crean filas adicionales.

---

## Variaciones comunes y manejo de casos límite

| Situación | Cómo adaptar |
|-----------|--------------|
| **Múltiples filas con matrices JSON** | La misma configuración `ArrayAsSingle` funciona; la matriz JSON de cada fila permanece en su propia celda. |
| **Diferentes estructuras JSON (objetos, matrices anidadas)** | Mientras el JSON sea una cadena, `ArrayAsSingle` lo mantendrá intacto. Para objetos complejos puede que necesite escapar comillas. |
| **Usar una fuente de datos diferente (p.ej., List\<T\>)** | Reemplace el `DataTable` por cualquier colección enumerable; la sintaxis del marcador (`&=myList.Property`) sigue siendo la misma. |
| **Exportar a CSV en lugar de XLSX** | `ArrayAsSingle` sigue aplicándose, pero recuerde que CSV no conserva el formato de celda; puede que necesite envolver el JSON entre comillas. |

**Consejo profesional:** Siempre establezca `ArrayAsSingle` *antes* de llamar a `ProcessSmartMarkers`. Cambiar la bandera después del procesamiento no tiene efecto sobre las celdas ya generadas.

---

## Ejemplo completo y ejecutable

A continuación se muestra el programa completo que puede copiar y pegar en una aplicación de consola. Incluye todas las directivas `using` y comentarios para mayor claridad.

```csharp
using System;
using System.Data;
using Aspose.Cells;

namespace SmartMarkerDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create the data source with a JSON array
            DataTable dataTable = new DataTable();
            dataTable.Columns.Add("Id", typeof(int));
            dataTable.Columns.Add("Names", typeof(string));
            dataTable.Rows.Add(1, "[\"Alice\",\"Bob\"]");

            // 2️⃣ Build a workbook and place smart markers
            Workbook workbook = new Workbook();
            Worksheet worksheet = workbook.Worksheets[0];
            worksheet.Cells["A1"].PutValue("&=dataTable");          // whole table (optional)
            worksheet.Cells["A2"].PutValue("&=dataTable.Names");   // Names column

            // 3️⃣ Configure SmartMarkerOptions to treat arrays as single values
            SmartMarkerOptions options = new SmartMarkerOptions
            {
                ArrayAsSingle = true
            };

            // 4️⃣ Process the markers with the custom options
            workbook.ProcessSmartMarkers(options);

            // 5️⃣ Save the file
            string path = @"C:\Temp\SmartMarkerJson.xlsx";
            workbook.Save(path);
            Console.WriteLine($"Workbook saved to {path}");
        }
    }
}
```

Ejecute el programa, abra `SmartMarkerJson.xlsx` y verá la matriz JSON preservada en la celda **A2**.

---

## Conclusión

Ahora sabe cómo **configurar SmartMarkerOptions ArrayAsSingle** en C# para mantener una matriz JSON como un valor de celda único al usar los smart markers de Aspose.Cells. Los pasos —preparar un `DataTable`, insertar marcadores, establecer la bandera `ArrayAsSingle`, procesar y guardar— forman un patrón repetible que puede aplicar a cualquier escenario donde se requiera una representación compacta de JSON dentro de Excel.

A continuación, podría explorar:

* **Smart markers de Aspose.Cells** para iterar sobre colecciones.
* Exportar **objetos JSON anidados** personalizando el formato de celda.
* Combinar **formato condicional** con smart markers para informes más ricos.

¡Siéntase libre de experimentar con diferentes estructuras de datos y compartir sus hallazgos! ¡Feliz codificación!

## ¿Qué debería aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que se basan en las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y funcionales con explicaciones paso a paso para ayudarle a dominar características adicionales de la API y explorar enfoques de implementación alternativos en sus propios proyectos.

- [Crear libro de Excel desde JSON – Guía completa de Aspose.Cells](/cells/english/net/data-loading-and-parsing/create-excel-workbook-from-json-complete-aspose-cells-guide/)
- [Crear y configurar libro de Excel Aspose Cells .NET](/cells/hindi/net/getting-started/create-configure-excel-workbook-aspose-cells-net/)
- [Crear y configurar libro de Excel Aspose Cells .NET](/cells/german/net/getting-started/create-configure-excel-workbook-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}