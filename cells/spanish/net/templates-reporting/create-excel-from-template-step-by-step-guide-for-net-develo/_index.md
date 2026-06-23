---
category: general
date: 2026-05-04
description: Crear Excel a partir de una plantilla y mapear JSON a Excel con nombres
  de hoja dinámicos. Aprende cómo rellenar Excel desde JSON y generar Excel usando
  JSON en minutos.
draft: false
keywords:
- create excel from template
- map json to excel
- populate excel from json
- dynamic worksheet naming excel
- generate excel using json
language: es
og_description: Crea Excel a partir de una plantilla rápidamente. Esta guía muestra
  cómo mapear JSON a Excel, rellenar Excel desde JSON, usar nombres de hoja dinámicos
  y generar Excel usando JSON.
og_title: Crear Excel a partir de una plantilla – Tutorial completo de .NET
tags:
- C#
- Aspose.Cells
- SmartMarker
- JSON
title: Crear Excel a partir de una plantilla – Guía paso a paso para desarrolladores
  .NET
url: /es/net/templates-reporting/create-excel-from-template-step-by-step-guide-for-net-develo/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crear Excel a partir de una plantilla – Tutorial completo de .NET

¿Alguna vez necesitaste **crear Excel a partir de una plantilla** pero te sentiste atascado manejando datos JSON y nombres de hojas de cálculo? No eres el único. En muchos proyectos de informes la plantilla contiene el diseño mientras que la carga JSON impulsa los valores reales, y lograr que se comuniquen puede ser un dolor de cabeza.  

¿La buena noticia? Con unas pocas líneas de C# y el motor SmartMarker de Aspose Cells puedes **poblar Excel desde JSON**, renombrar hojas de detalle al vuelo y, finalmente, **generar Excel usando JSON** sin tocar nunca la interfaz de usuario.  

En este tutorial recorreremos todo el proceso: cargar una plantilla, mapear JSON a Excel, configurar la nomenclatura dinámica de hojas de cálculo y guardar el libro final. Al final tendrás un fragmento reutilizable que puedes insertar en cualquier servicio .NET. Sin herramientas externas, solo código puro.

---

## Lo que necesitarás

- **Aspose.Cells for .NET** (v24.10 o posterior) – la biblioteca que impulsa SmartMarker.  
- Un archivo **template.xlsx** que contenga etiquetas SmartMarker como `{Master:Name}` y `{Detail:Item}`.  
- Un archivo **data.json** que coincida con la estructura maestro‑detalle.  
- Visual Studio 2022 (o cualquier IDE que prefieras) dirigido a .NET 6 o posterior.

¡Eso es todo! Si ya tienes esos componentes, estás listo para comenzar.

---

## Crear Excel a partir de una plantilla – Visión general

La idea central es simple: trata el archivo Excel como una *plantilla* y deja que SmartMarker reemplace los marcadores de posición con los valores de tu JSON. La biblioteca también permite renombrar la hoja de detalle basándose en un campo maestro, que es donde **la nomenclatura dinámica de hojas de cálculo** brilla.

A continuación tienes el código completo, listo para ejecutar. Siéntete libre de copiar‑pegarlo en una aplicación de consola y apuntar las rutas a tus propios archivos.

```csharp
// ------------------------------------------------------------
// Full example: create Excel from template using JSON data
// ------------------------------------------------------------
using System;
using System.IO;
using Aspose.Cells;

namespace ExcelTemplateDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load the workbook that contains SmartMarker tags
            //    (e.g., {Master:Name} in the master sheet and {Detail:Item} in the detail sheet)
            string templatePath = @"C:\MyProject\Templates\template.xlsx";
            Workbook wb = new Workbook(templatePath);

            // 2️⃣ Read the JSON data that will populate the markers
            //    The JSON should match the structure expected by the template.
            string jsonPath = @"C:\MyProject\Data\data.json";
            string json = File.ReadAllText(jsonPath);

            // 3️⃣ Configure the SmartMarker processor to rename the detail sheet
            //    dynamically based on the master record’s Name field.
            //    This demonstrates dynamic worksheet naming excel.
            wb.SmartMarkerProcessor.Options.DetailSheetNewName = "Detail_{Master.Name}";

            // 4️⃣ Execute the SmartMarker processing using the JSON data.
            //    This step maps JSON to Excel and populates every marker.
            wb.SmartMarkerProcessor.Execute(json);

            // 5️⃣ Save the processed workbook – now it’s a brand‑new file.
            string outputPath = @"C:\MyProject\Output\output.xlsx";
            wb.Save(outputPath);

            Console.WriteLine("✅ Excel file generated successfully at: " + outputPath);
        }
    }
}
```

> **Resultado esperado:**  
> - La hoja maestra mostrará el nombre de `Master.Name`.  
> - La hoja de detalle será renombrada a algo como `Detail_JohnDoe`.  
> - Todas las filas `{Detail:Item}` se rellenarán con el arreglo de items del JSON.

---

## Mapear JSON a Excel – Cargar datos

Antes de que el motor SmartMarker pueda hacer su magia, el JSON debe estar **bien formado** y reflejar la jerarquía usada en la plantilla. Un JSON típico maestro‑detalle se ve así:

```json
{
  "Master": {
    "Name": "John Doe",
    "Date": "2026-05-04"
  },
  "Detail": [
    { "Item": "Widget A", "Qty": 10, "Price": 2.5 },
    { "Item": "Widget B", "Qty": 5,  "Price": 5.0 }
  ]
}
```

**Por qué es importante:**  
- Las claves `Master` y `Detail` corresponden directamente a las etiquetas `{Master:…}` y `{Detail:…}`.  
- Si la estructura del JSON diverge, SmartMarker no encontrará coincidencias y las celdas permanecerán vacías.  

**Consejo:** Valida tu JSON con un validador en línea rápido o con `System.Text.Json.JsonDocument.Parse(json)` para detectar errores de sintaxis temprano.

---

## Poblar Excel desde JSON – Configuración de SmartMarker

SmartMarker funciona escaneando el libro en busca de etiquetas y luego inyectando los datos. El paso **populate excel from json** es esencialmente la llamada `Execute` que vimos antes, pero hay algunas configuraciones opcionales que vale la pena mencionar:

| Configuración | Qué hace | Cuándo usarla |
|---------------|----------|----------------|
| `Options.CaseSensitive` | Trata los nombres de etiqueta como sensibles a mayúsculas/minúsculas. | Si tu plantilla mezcla mayúsculas y necesitas coincidencia estricta. |
| `Options.RemoveEmptyRows` | Elimina filas que no recibieron datos. | Para mantener la hoja final ordenada cuando algunos ítems de detalle son opcionales. |
| `Options.EnableHyperlink` | Permite que los hipervínculos dentro del JSON se vuelvan clicables. | Cuando necesitas URLs clicables en el informe. |

Puedes encadenarlas así:

```csharp
wb.SmartMarkerProcessor.Options.CaseSensitive = true;
wb.SmartMarkerProcessor.Options.RemoveEmptyRows = true;
```

---

## Nomenclatura dinámica de hojas de cálculo – Configurar el nombre de la hoja de detalle

Uno de los requisitos más complicados que muchos proyectos tienen es **la nomenclatura dinámica de hojas de cálculo**. En lugar de una hoja “Detail” estática, podrías querer que cada informe lleve el nombre del cliente o un número de orden.

La línea:

```csharp
wb.SmartMarkerProcessor.Options.DetailSheetNewName = "Detail_{Master.Name}";
```

hace exactamente eso. El marcador `{Master.Name}` se reemplaza *después* de procesar el JSON, por lo que el nuevo nombre de la hoja se convierte en `Detail_JohnDoe`.  

**Caso límite:** Si el nombre contiene caracteres ilegales en nombres de hoja (`:`, `\`, `/`, `?`, `*`, `[`, `]`), Aspose los sanitiza automáticamente, pero puedes limpiar la cadena en el JSON si necesitas un formato específico.

---

## Generar Excel usando JSON – Ejecutar y Guardar

Las dos últimas líneas del código (`Execute` y `Save`) son donde ocurre la magia de **generate excel using json**. Bajo el capó, Aspose analiza el JSON en una tabla de datos, itera sobre la plantilla y escribe el archivo de salida.

Si necesitas generar varios libros en un bucle (p. ej., uno por cliente), simplemente mueve la instanciación de `Workbook` dentro del bucle y cambia el nombre del archivo de salida en consecuencia:

```csharp
foreach (var customerJson in customers)
{
    Workbook wb = new Workbook(templatePath);
    wb.SmartMarkerProcessor.Options.DetailSheetNewName = $"Detail_{customerJson.Master.Name}";
    wb.SmartMarkerProcessor.Execute(customerJson);
    wb.Save($@"C:\Reports\Report_{customerJson.Master.Name}.xlsx");
}
```

Ese patrón es común en servicios de informes por lotes.

---

## Problemas comunes y consejos profesionales

- **Etiquetas faltantes:** Si una celda aún muestra `{Master:Name}`, la etiqueta no fue reconocida. Verifica la ortografía y que la etiqueta esté dentro de una celda, no en un comentario.  
- **Carga JSON grande:** Para conjuntos de datos masivos, considera transmitir el JSON o usar `DataTable` en lugar de una cadena cruda para reducir la presión de memoria.  
- **Seguridad en hilos:** Las instancias de `Workbook` no son seguras para hilos. Crea una nueva instancia por hilo si ejecutas trabajos en paralelo.  
- **Bloqueos de archivo:** Asegúrate de que la plantilla no esté abierta en Excel mientras tu código se ejecuta; de lo contrario obtendrás una `IOException`.  

> **Consejo profesional:** Mantén una copia de la plantilla original en una carpeta de solo lectura. Esto evita sobrescrituras accidentales durante la depuración.

---

## Recapitulación del ejemplo completo

Aquí tienes el programa completo nuevamente, esta vez con comentarios en línea para cada línea no obvia:

```csharp
using System;
using System.IO;
using Aspose.Cells;

namespace ExcelTemplateDemo
{
    class Program
    {
        static void Main()
        {
            // Path to the Excel template that contains SmartMarker tags.
            string templatePath = @"C:\MyProject\Templates\template.xlsx";

            // Load the workbook – this is the "create excel from template" step.
            Workbook wb = new Workbook(templatePath);

            // Read JSON data that maps directly to the template's tags.
            string jsonPath = @"C:\MyProject\Data\data.json";
            string json = File.ReadAllText(jsonPath);

            // OPTIONAL: tweak SmartMarker behavior (case‑sensitivity, empty rows, etc.).
            wb.SmartMarkerProcessor.Options.CaseSensitive = false;
            wb.SmartMarkerProcessor.Options.RemoveEmptyRows = true;

            // Set up dynamic worksheet naming based on the master record's Name field.
            wb.SmartMarkerProcessor.Options.DetailSheetNewName = "Detail_{Master.Name}";

            // Run the SmartMarker engine – this is where we "populate excel from json".
            wb.SmartMarkerProcessor.Execute(json);

            // Save the newly generated workbook – the final "generate excel using json" step.
            string outputPath = @"C:\MyProject\Output\output.xlsx";
            wb.Save(outputPath);

            Console.WriteLine("✅ Workbook created at: " + outputPath);
        }
    }
}
```

Ejecutar esta aplicación de consola producirá `output.xlsx` con la hoja de detalle renombrada y todos los datos rellenados.

---

## Próximos pasos y temas relacionados

- **Exportar a PDF:** Después de generar el libro, puedes llamar a `wb.Save("report.pdf", SaveFormat.Pdf);` para entregar una versión PDF.  
- **Población de gráficos:** SmartMarker también admite fuentes de datos de gráficos; solo enlaza el arreglo JSON al rango de series del gráfico.  
- **Formato condicional:** Usa las reglas integradas de Excel en la plantilla; permanecerán después del reemplazo de SmartMarker.  
- **Optimización de rendimiento:** Para escenarios de alto volumen, reutiliza una sola instancia de `Workbook` con `Clone` para evitar I/O de archivo repetido.  

Siéntete libre de experimentar con diferentes estructuras JSON, patrones de renombrado o incluso combinar múltiples plantillas en una sola ejecución. La flexibilidad de **create excel from template** usando Aspose.Cells te permite adaptar la solución a facturas, paneles de control o cualquier necesidad de informes.

---

## Resumen visual

![Flujo de crear Excel a partir de una plantilla mostrando JSON → SmartMarker → Nomenclatura dinámica de hoja](/images/create-excel-from-template-workflow.png "Diagrama del flujo de crear Excel a partir de una plantilla")

*(El texto alternativo incluye la palabra clave principal para SEO)*

---

### Conclusión

Hemos cubierto todo lo que necesitas para **create excel from template**, **map JSON to Excel**, **populate Excel from JSON**, usar **dynamic worksheet naming excel**, y finalmente **generate Excel using JSON**. El código está completo, las explicaciones te indican *por qué* cada línea es importante, y ahora tienes una base sólida para construir pipelines de informes más grandes.

¿Tienes alguna variante que estás intentando implementar? Deja un comentario abajo y solucionemoslo juntos. ¡Feliz codificación!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}