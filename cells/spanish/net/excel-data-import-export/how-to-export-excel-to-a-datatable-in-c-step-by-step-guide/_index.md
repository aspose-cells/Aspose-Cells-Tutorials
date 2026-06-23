---
category: general
date: 2026-03-18
description: Cómo exportar datos de Excel a un DataTable en C# con código que maneja
  celdas específicas, convierte Excel a DataTable y formatea números. Aprende a exportar
  celdas específicas y más.
draft: false
keywords:
- how to export excel
- convert excel to datatable
- export specific cells
- excel to datatable c#
- excel range to datatable
language: es
og_description: Cómo exportar datos de Excel a un DataTable en C#. Este tutorial muestra
  cómo exportar celdas específicas, convertir Excel a DataTable y formatear números
  con facilidad.
og_title: Cómo exportar Excel a un DataTable en C# – Guía completa
tags:
- C#
- Excel
- DataTable
- Aspose.Cells
title: Cómo exportar Excel a una DataTable en C# – Guía paso a paso
url: /es/net/excel-data-import-export/how-to-export-excel-to-a-datatable-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo exportar Excel a un DataTable en C# – Guía paso a paso

¿Alguna vez te has preguntado **cómo exportar Excel** a un `DataTable` sin perder el formato? No eres el único—los desarrolladores necesitan constantemente extraer una parte de una hoja de cálculo a la memoria para informes, validaciones o operaciones de inserción masiva. ¿La buena noticia? Con unas pocas líneas de C# puedes exportar un rango preciso (por ejemplo *A1:F11*), forzar que cada celda se trate como una cadena y hasta aplicar un formato numérico personalizado.

En este tutorial cubriremos todo lo que necesitas saber: desde cargar el libro de trabajo, configurar **export specific cells**, convertir el rango a un `DataTable`, y manejar casos límite como filas vacías o números dependientes de la configuración regional. Al final tendrás un método reutilizable que funciona con escenarios **excel to datatable c#** en código de producción.

> **Prerequisitos** – Necesitarás la biblioteca Aspose.Cells para .NET (o cualquier API similar que ofrezca `ExportDataTable`). El ejemplo asume .NET 6+, pero los conceptos se aplican también a versiones anteriores.

## Lo que aprenderás

- Cómo **convertir Excel a DataTable** usando Aspose.Cells.
- Exportar un rango personalizado (`excel range to datatable`) tratando todos los valores como cadenas.
- Aplicar un formato numérico de dos decimales (`#,#00.00`) durante la exportación.
- Problemas comunes (filas nulas, columnas ocultas) y cómo evitarlos.
- Un ejemplo de código listo para copiar y ejecutar completamente.

## Prerrequisitos y configuración

Antes de sumergirnos en el código, asegúrate de tener:

1. **Aspose.Cells for .NET** instalado vía NuGet:

   ```bash
   dotnet add package Aspose.Cells
   ```

2. Un archivo Excel (`input.xlsx`) colocado en una carpeta que puedas referenciar, por ejemplo `YOUR_DIRECTORY/input.xlsx`.

3. Un proyecto que apunte a .NET 6 o posterior (las sentencias `using` mostradas a continuación funcionan de inmediato).

> **Consejo profesional:** Si estás usando una biblioteca diferente (p.ej., EPPlus o ClosedXML), el concepto sigue siendo el mismo—carga el libro de trabajo, selecciona un rango y llama a un método que devuelva un `DataTable`.

## Paso 1: Cargar el libro de trabajo y obtener la primera hoja

Lo primero que necesitas es un objeto `Workbook` que represente tu archivo Excel. Una vez lo tengas, puedes acceder a cualquier hoja por índice o nombre.

```csharp
using Aspose.Cells;
using System.Data;

namespace ExcelExportDemo
{
    class Program
    {
        static void Main()
        {
            // Load the workbook from disk
            Workbook workbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");

            // Grab the first worksheet (index 0)
            Worksheet worksheet = workbook.Worksheets[0];

            // Continue with export options...
        }
    }
}
```

**Por qué es importante:** Cargar el libro de trabajo temprano te permite inspeccionar su estructura (hojas ocultas, protección) antes de decidir qué celdas exportar. Si el archivo es grande, considera usar `LoadOptions` para transmitir solo las partes necesarias.

## Paso 2: Configurar opciones de exportación – Tratar todos los valores como cadenas

Cuando exportas datos para procesamiento posterior (p.ej., inserción masiva en SQL), a menudo deseas una **representación de cadena consistente**. Esto evita errores de incompatibilidad de tipos más adelante.

```csharp
// Configure export behavior
ExportTableOptions exportOptions = new ExportTableOptions
{
    // Force every cell to be returned as a string, regardless of its original type
    ExportAsString = true,

    // Apply a two‑decimal‑place format to numeric cells
    NumberFormat = "#,##0.00"
};
```

**Explicación:**  
- `ExportAsString = true` indica a Aspose.Cells que ignore el tipo nativo de la celda y devuelva el texto formateado.  
- `NumberFormat = "#,##0.00"` asegura que números como `1234.5` se conviertan en `"1,234.50"`—útil para informes financieros.

Si necesitas los tipos de datos originales, simplemente establece `ExportAsString` a `false` y maneja la conversión tú mismo.

## Paso 3: Exportar un rango específico (A1:F11) a un DataTable

Ahora llega el núcleo de **export specific cells**. El método `ExportDataTable` toma índices de fila/columna de inicio y fin (basados en cero) más una bandera para la inclusión de encabezados.

```csharp
// Export cells A1:F11 (rows 0‑10, columns 0‑5) including the header row
DataTable table = worksheet.ExportDataTable(
    startRow: 0,
    startColumn: 0,
    endRow: 10,
    endColumn: 5,
    includeColumnNames: true,
    exportOptions: exportOptions);
```

**Qué obtienes:** Un `DataTable` con 11 filas (incluyendo el encabezado) y 6 columnas (`A`‑`F`). Todos los valores son cadenas formateadas según `exportOptions`.

## Paso 4: Verificar el resultado – Imprimir en la consola

Siempre es una buena idea validar la salida antes de pasar la tabla a otro componente.

```csharp
// Simple console dump
foreach (DataRow row in table.Rows)
{
    foreach (var item in row.ItemArray)
    {
        Console.Write($"{item}\t");
    }
    Console.WriteLine();
}
```

You should see something like:

```
Id      Name        Qty     Price   Total   Date
1       Widget A    10      2.50    25.00   2026-01-01
2       Widget B    5       3.75    18.75   2026-01-02
...
```

Observa cómo las columnas numéricas muestran dos decimales, exactamente como especificamos.

## Ejemplo completo funcional (listo para copiar y pegar)

A continuación se muestra el programa completo que une todo. Colócalo en un nuevo proyecto de consola, ajusta la ruta del archivo y ejecútalo—no se necesita configuración adicional.

```csharp
using Aspose.Cells;
using System;
using System.Data;

namespace ExcelExportDemo
{
    class Program
    {
        static void Main()
        {
            // -------------------------------------------------
            // 1️⃣ Load workbook and select worksheet
            // -------------------------------------------------
            string filePath = @"YOUR_DIRECTORY\input.xlsx";
            Workbook workbook = new Workbook(filePath);
            Worksheet worksheet = workbook.Worksheets[0];

            // -------------------------------------------------
            // 2️⃣ Set export options – strings + number format
            // -------------------------------------------------
            ExportTableOptions exportOptions = new ExportTableOptions
            {
                ExportAsString = true,
                NumberFormat = "#,##0.00"
            };

            // -------------------------------------------------
            // 3️⃣ Export range A1:F11 (rows 0‑10, cols 0‑5)
            // -------------------------------------------------
            DataTable table = worksheet.ExportDataTable(
                startRow: 0,
                startColumn: 0,
                endRow: 10,
                endColumn: 5,
                includeColumnNames: true,
                exportOptions: exportOptions);

            // -------------------------------------------------
            // 4️⃣ Output to console for verification
            // -------------------------------------------------
            Console.WriteLine("=== Exported DataTable ===");
            foreach (DataRow row in table.Rows)
            {
                foreach (var cell in row.ItemArray)
                {
                    Console.Write($"{cell}\t");
                }
                Console.WriteLine();
            }

            // Keep console window open
            Console.WriteLine("\nPress any key to exit...");
            Console.ReadKey();
        }
    }
}
```

**Conclusiones clave del código:**

- El objeto `ExportTableOptions` es reutilizable; puedes pasarlo a múltiples llamadas `ExportDataTable` si necesitas exportar varios rangos.
- La indexación comienza en **0**, por lo que `A1` corresponde a `(0,0)`.
- Establecer `includeColumnNames` a `true` usa automáticamente la primera fila como encabezados de columna—ideal para operaciones posteriores con `DataTable`.

## Manejo de casos límite y preguntas frecuentes

### ¿Qué pasa si la hoja tiene filas o columnas ocultas?

Aspose.Cells respeta la visibilidad por defecto. Si necesitas exportar datos ocultos, establece `exportOptions.ExportHiddenRows = true` y `ExportHiddenColumns = true`.

### Mi archivo Excel contiene fórmulas—¿obtendré los valores calculados?

Sí. Por defecto `ExportDataTable` devuelve el **valor mostrado** (el resultado de la fórmula). Si deseas el texto bruto de la fórmula, establece `exportOptions.ExportFormulas = true`.

### ¿Cómo omito filas completamente vacías?

After the export, you can prune the `DataTable`:

```csharp
foreach (DataRow row in table.Rows.Cast<DataRow>()
                                   .Where(r => r.ItemArray.All(c => c == DBNull.Value || string.IsNullOrWhiteSpace(c.ToString()))).ToList())
{
    table.Rows.Remove(row);
}
```

### ¿Puedo exportar un rango no contiguo (p.ej., A1:B5 y D1:E5)?

Aspose.Cells no soporta rangos disjuntos en una sola llamada. En su lugar, exporta cada bloque por separado y luego combina manualmente los `DataTable` resultantes.

## Consejos de rendimiento

- **Reutiliza `ExportTableOptions`** para múltiples exportaciones; crear una nueva instancia cada vez agrega una sobrecarga insignificante pero desordena el código.
- **Transmite archivos grandes** con `LoadOptions` para evitar cargar todo el libro de trabajo en memoria.
- **Evita `DataTable`** si solo necesitas una exportación rápida a CSV—`ExportDataTable` es conveniente pero no es la más eficiente en memoria para hojas masivas.

## Conclusión

Hemos recorrido **cómo exportar Excel** a un `DataTable` mientras controlamos el formato, manejamos rangos de celdas específicos y aseguramos que cada valor llegue como cadena. El ejemplo completo muestra un enfoque limpio y listo para producción que puedes adaptar para **convert excel to datatable**, **export specific cells**, o cualquier escenario **excel range to datatable** que encuentres.

Siéntete libre de experimentar: cambia el rango, alterna `ExportAsString`, o canaliza el `DataTable` directamente a Entity Framework para inserciones masivas. El cielo es el límite una vez que tienes esta base sólida.

### Próximos pasos y temas relacionados

- **Importar DataTable de vuelta a Excel** – aprende la operación inversa con `ImportDataTable`.
- **Inserción masiva de un DataTable en SQL Server** – usa `SqlBulkCopy` para cargas ultrarrápidas.
- **Trabajar con EPPlus o ClosedXML** – observa cómo se ve la misma tarea con bibliotecas alternativas.
- **Formatear celdas al exportar** – explora más `ExportTableOptions` para formatos de fecha, configuraciones culturales personalizadas y más.

¿Tienes preguntas o un caso de uso diferente? Deja un comentario y mantengamos la conversación. ¡Feliz codificación!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}