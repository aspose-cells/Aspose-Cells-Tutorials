---
category: general
date: 2026-05-23
description: Cómo usar marcadores con Aspose.Cells para lograr nombres de hoja dinámicos
  en la automatización de Excel. Aprenda marcadores inteligentes, enlace de datos
  JSON y creación de hojas en minutos.
draft: false
keywords:
- how to use markers
- dynamic sheet naming excel
- aspose.cells smart markers
language: es
og_description: Cómo usar marcadores en Aspose.Cells para generar archivos Excel con
  nombres de hoja dinámicos. Guía completa paso a paso con ejemplo completo en C#.
og_title: Cómo usar marcadores – Nomenclatura dinámica de hojas en Excel con Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-05-23'
  description: How to use markers with Aspose.Cells to achieve dynamic sheet naming
    Excel automation. Learn smart markers, JSON data binding, and sheet creation in
    minutes.
  headline: How to Use Markers in Aspose.Cells for Dynamic Sheet Naming in Excel
  type: TechArticle
- description: How to use markers with Aspose.Cells to achieve dynamic sheet naming
    Excel automation. Learn smart markers, JSON data binding, and sheet creation in
    minutes.
  name: How to Use Markers in Aspose.Cells for Dynamic Sheet Naming in Excel
  steps:
  - name: What Happens Under the Hood?
    text: 1. The processor reads the `Orders` array. 2. For each order it creates
      a **master sheet** (using `${Orders.MasterSheetName}`) and a **detail sheet**
      (using the `DetailSheetNewName` pattern). 3. Cell values are replaced with the
      corresponding JSON fields, so the master sheet’s first cell ends up con
  - name: What if I need more than two levels of hierarchy?
    text: You can nest markers inside the newly created detail sheets. Just place
      additional `${...}` tags in the template sheet before processing. The processor
      will cascade through each level automatically.
  - name: Can I use a DataTable instead of JSON?
    text: Absolutely. `SmartMarkerProcessor` has overloads for `DataSet`, `DataTable`,
      and even custom objects. The only change is the call to `ApplyJson` – you’d
      use `ApplyDataSet(myDataSet)` instead.
  - name: How do I control the order of sheet creation?
    text: The order follows the sequence of the source collection. If you need a custom
      sort, simply sort the JSON array (or DataTable) before passing it to the processor.
  - name: Is there a way to hide the template sheet after processing?
    text: Yes. Set `sm.Options.RemoveTemplateSheets = true;` before calling `ApplyJson`.
      The original sheet (index 0) will be removed from the final workbook.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: Cómo usar marcadores en Aspose.Cells para nombrar hojas de forma dinámica en
  Excel
url: /es/net/smart-markers-dynamic-data/how-to-use-markers-in-aspose-cells-for-dynamic-sheet-naming/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo usar marcadores en Aspose.Cells para nombrado dinámico de hojas en Excel

¿Alguna vez te has preguntado **cómo usar marcadores** para convertir una plantilla estática de Excel en un libro maestro‑detalle completamente funcional? No estás solo. Muchos desarrolladores se topan con un obstáculo cuando necesitan capacidades de *dynamic sheet naming excel*, especialmente cuando los nombres de las hojas deben reflejar valores de datos provenientes de JSON o una base de datos.  

En este tutorial recorreremos un ejemplo completo y listo para ejecutar en C# que muestra **cómo usar marcadores** con los **smart markers** de **Aspose.Cells**, enlazar datos JSON y permitir que el procesador cree hojas cuyos nombres cambien al instante. Sin rodeos, solo el código exacto que puedes pegar en Visual Studio y ver los resultados al instante.

## Qué aprenderás

- El concepto de **smart markers** y por qué son perfectos para escenarios maestro‑detalle.  
- Cómo incrustar etiquetas de marcador en un libro de trabajo que luego serán reemplazadas por nombres reales de hojas.  
- Configurar **dynamic sheet naming excel** usando la opción `DetailSheetNewName`.  
- Ejecutar el `SmartMarkerProcessor` con datos JSON para generar múltiples hojas automáticamente.  
- Verificar la salida y algunos consejos útiles para evitar errores comunes.

> **Prerequisitos** – Necesitas un runtime reciente de .NET (≥ .NET 6 está bien), la biblioteca Aspose.Cells para .NET (puedes obtener una prueba gratuita de Aspose) y un conocimiento básico de C#.  

---

![ejemplo de cómo usar marcadores en Aspose.Cells](example.png "ejemplo de cómo usar marcadores en Aspose.Cells")

## Cómo usar marcadores para crear nombrado dinámico de hojas (Paso 1)

Lo primero que necesitamos es un libro de trabajo en blanco que actuará como nuestra plantilla. En un proyecto real probablemente comenzarías con un archivo `.xlsx` existente que ya contiene el diseño, formato y celdas de marcador de posición. Para mayor claridad crearemos todo programáticamente.

```csharp
using Aspose.Cells;
using Aspose.Cells.SmartMarker;

// Step 1: Create a new workbook and get the first worksheet
Workbook wb = new Workbook();                // fresh workbook, no sheets yet
Worksheet ws = wb.Worksheets[0];             // default first sheet
```

*Por qué es importante*: El objeto `Worksheet` es donde colocaremos nuestras etiquetas de **smart marker**. Piensa en las etiquetas como pequeños marcadores de posición que el procesador reemplazará más tarde con valores reales provenientes de JSON.  

## Insertar etiquetas de Smart Marker (Paso 2)

Ahora colocamos las etiquetas de marcador directamente en las celdas. La sintaxis `${...}` le indica a Aspose.Cells “esto es un marcador”. En nuestro ejemplo necesitamos dos marcadores: uno para el nombre de la hoja maestra y otro para el nombre de la hoja de detalle.

```csharp
// Step 2: Insert Smart Marker tags that will be replaced with sheet names
ws.Cells[0, 0].PutValue("${Orders.MasterSheetName}");   // master sheet placeholder
ws.Cells[1, 0].PutValue("${Orders.DetailSheetName}");   // detail sheet placeholder
```

> **Consejo profesional** – Mantén los nombres de los marcadores cortos y significativos; se convierten en las claves que usarás en tu carga JSON.

## Preparar los datos JSON (Paso 3)

El procesador funciona con cualquier fuente de datos que pueda representarse como JSON, un `DataSet` o incluso un objeto simple. Aquí tienes una cadena JSON mínima que contiene una colección maestro‑detalle. Observa que cada pedido lleva tanto un `MasterSheetName` como un `DetailSheetName`.

```csharp
// Step 3: Prepare the JSON data that contains the master‑detail information
string jsonOrders = @"{
    ""Orders"": [
        {
            ""OrderId"": 1,
            ""MasterSheetName"": ""Master_1"",
            ""DetailSheetName"": ""Detail_1""
        },
        {
            ""OrderId"": 2,
            ""MasterSheetName"": ""Master_2"",
            ""DetailSheetName"": ""Detail_2""
        }
    ]
}";
```

*¿Por qué JSON?* Es liviano, legible por humanos y funciona muy bien con APIs web. También podrías obtener estos datos de una consulta SQL y serializarlos con `Newtonsoft.Json`.

## Inicializar el SmartMarkerProcessor (Paso 4)

El `SmartMarkerProcessor` es el motor que escanea el libro de trabajo, encuentra los marcadores y realiza el enlace de datos. Instanciarlo es una sola línea.

```csharp
// Step 4: Initialise the SmartMarkerProcessor with the workbook
SmartMarkerProcessor sm = new SmartMarkerProcessor(wb);
```

## Definir nombrado dinámico de hojas (Paso 5)

Aquí es donde **dynamic sheet naming excel** realmente brilla. Al establecer `DetailSheetNewName`, indicamos al procesador que cree una nueva hoja de detalle para cada pedido y la nombre según el `OrderId`. El marcador `${OrderId}` se resuelve a partir del registro actual durante el procesamiento.

```csharp
// Step 5: Define how new detail sheets should be named during processing
sm.Options.DetailSheetNewName = "Detail_${OrderId}";
```

> **Cuidado** – Si olvidas incluir la sintaxis `${}`, la hoja se nombrará literalmente “Detail_${OrderId}” en lugar de “Detail_1”, “Detail_2”, etc.

## Aplicar JSON y generar hojas (Paso 6)

Ahora dejamos que el procesador haga el trabajo pesado. Leerá el JSON, reemplazará los marcadores y creará nuevas hojas de cálculo según sea necesario.

```csharp
// Step 6: Apply the JSON data to populate the smart markers and generate sheets
sm.ApplyJson(jsonOrders);
```

### ¿Qué ocurre bajo el capó?

1. El procesador lee la matriz `Orders`.  
2. Por cada pedido crea una **hoja maestra** (usando `${Orders.MasterSheetName}`) y una **hoja de detalle** (usando el patrón `DetailSheetNewName`).  
3. Los valores de las celdas se reemplazan con los campos JSON correspondientes, de modo que la primera celda de la hoja maestra termina conteniendo “Master_1”, “Master_2”, etc.  

## Guardar y verificar el resultado (Opcional)

Finalmente, escribe el libro de trabajo en disco. Abre el archivo en Excel y deberías ver dos hojas maestras (`Master_1`, `Master_2`) y dos hojas de detalle nombradas dinámicamente (`Detail_1`, `Detail_2`).  

```csharp
// (Optional) Save the result to verify the output
wb.Save("output.xlsx");
```

**Salida esperada** – Después de abrir `output.xlsx` verás:

- Hoja **Master_1** con la celda A1 = “Master_1”.  
- Hoja **Detail_1** con la celda A1 = “Detail_1”.  
- Hoja **Master_2** con la celda A1 = “Master_2”.  
- Hoja **Detail_2** con la celda A1 = “Detail_2”.  

Ese es el ciclo completo de **cómo usar marcadores** para lograr **dynamic sheet naming excel** con **smart markers** de **Aspose.Cells**.

---

## Preguntas comunes y casos límite

### ¿Qué pasa si necesito más de dos niveles de jerarquía?

Puedes anidar marcadores dentro de las hojas de detalle recién creadas. Simplemente coloca etiquetas `${...}` adicionales en la hoja plantilla antes del procesamiento. El procesador recorrerá cada nivel automáticamente.

### ¿Puedo usar un DataTable en lugar de JSON?

Absolutamente. `SmartMarkerProcessor` tiene sobrecargas para `DataSet`, `DataTable` e incluso objetos personalizados. El único cambio es la llamada a `ApplyJson`; en su lugar usarías `ApplyDataSet(myDataSet)`.

### ¿Cómo controlo el orden de creación de las hojas?

El orden sigue la secuencia de la colección origen. Si necesitas un orden personalizado, simplemente ordena la matriz JSON (o DataTable) antes de pasarla al procesador.

### ¿Hay una forma de ocultar la hoja plantilla después del procesamiento?

Sí. Configura `sm.Options.RemoveTemplateSheets = true;` antes de llamar a `ApplyJson`. La hoja original (índice 0) será eliminada del libro final.

---

## Ejemplo completo (todos los pasos combinados)

A continuación se muestra el programa completo que puedes copiar y pegar en un nuevo proyecto de consola C#. Asegúrate de haber referenciado el paquete NuGet `Aspose.Cells`.

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.SmartMarker;

namespace DynamicSheetNamingDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Create a new workbook and get the first worksheet
            Workbook wb = new Workbook();
            Worksheet ws = wb.Worksheets[0];

            // Step 2: Insert Smart Marker tags that will be replaced with sheet names
            ws.Cells[0, 0].PutValue("${Orders.MasterSheetName}");
            ws.Cells[1, 0].PutValue("${Orders.DetailSheetName}");

            // Step 3: Prepare the JSON data that contains the master‑detail information
            string jsonOrders = @"{
                ""Orders"": [
                    {
                        ""OrderId"": 1,
                        ""MasterSheetName"": ""Master_1"",
                        ""DetailSheetName"": ""Detail_1""
                    },
                    {
                        ""OrderId"": 2,
                        ""MasterSheetName"": ""Master_2"",
                        ""DetailSheetName"": ""Detail_2""
                    }
                ]
            }";

            // Step 4: Initialise the SmartMarkerProcessor with the workbook
            SmartMarkerProcessor sm = new SmartMarkerProcessor(wb);

            // Step 5: Define how new detail sheets should be named during processing
            sm.Options.DetailSheetNewName = "Detail_${OrderId}";

            // (Optional) Remove the original template sheet after processing
            // sm.Options.RemoveTemplateSheets = true;

            // Step 6: Apply the JSON data to populate the smart markers and generate sheets
            sm.ApplyJson(jsonOrders);

            // Save the result
            wb.Save("output.xlsx");
            Console.WriteLine("Workbook generated successfully. Check output.xlsx.");
        }
    }
}
```

Ejecuta el programa, abre `output.xlsx` y verás las hojas dinámicas exactamente como se describió anteriormente.

---

## Conclusión

Acabamos de cubrir **cómo usar marcadores** en Aspose.Cells para convertir un libro de trabajo sencillo en una solución maestro‑detalle con **dynamic sheet naming excel**. Los puntos clave son:

1. Coloca marcadores inteligentes `${...}` donde deseas que aparezcan los datos.  
2. Alimenta JSON (o cualquier fuente de datos compatible) al `SmartMarkerProcessor`.  
3. Usa `DetailSheetNewName` para que el procesador nombre nuevas hojas al instante.  

A partir de aquí puedes explorar escenarios más avanzados—agregar tablas, dar estilo a celdas o incluso incrustar gráficos—todo impulsado

## Tutoriales relacionados

- [Cómo implementar Smart Markers de Aspose.Cells en C# para informes dinámicos de Excel](/cells/english/net/automation-batch-processing/implement-aspose-cells-smart-markers-with-csharp/)
- [Generar informes dinámicos de Excel usando Smart Markers de Aspose.Cells .NET](/cells/english/net/templates-reporting/generate-excel-reports-aspose-cells-net-smart-markers/)
- [Dominar Aspose.Cells .NET: Implementar Smart Markers y etiquetas personalizadas para informes dinámicos de Excel](/cells/english/net/advanced-features/aspose-cells-net-smart-markers-custom-labels/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}