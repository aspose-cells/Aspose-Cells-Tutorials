---
category: general
date: 2026-02-26
description: cómo exportar Excel a un archivo txt delimitado por tabulaciones usando
  C#. Aprende a exportar Excel como tab, convertir Excel a txt y exportar Excel con
  delimitador en tres pasos fáciles.
draft: false
keywords:
- how to export excel
- export excel as tab
- convert excel to txt
- export excel with delimiter
- export excel range
language: es
og_description: cómo exportar Excel a un archivo txt delimitado por tabulaciones usando
  C#. Este tutorial muestra exportar Excel como tabulación, convertir Excel a txt
  y exportar Excel con delimitador.
og_title: cómo exportar Excel – Guía de texto delimitado por tabulaciones
tags:
- csharp
- excel
- file-conversion
title: Cómo exportar Excel – Guía de texto delimitado por tabulaciones
url: /es/net/converting-excel-files-to-other-formats/how-to-export-excel-tab-delimited-text-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# cómo exportar excel – Tutorial completo de C#

¿Alguna vez te has preguntado **cómo exportar excel** datos a un archivo de texto plano sin perder el formato? Tal vez necesites un TSV rápido (valores separados por tabulaciones) para una canalización de datos, o estés alimentando un sistema heredado que solo lee `.txt`. De cualquier manera, no estás solo—los desarrolladores se topan constantemente con este obstáculo al mover datos fuera de las hojas de cálculo.

¡Buenas noticias! En solo tres pasos sencillos puedes **exportar excel como texto** delimitado por tabulaciones, **convertir excel a txt**, e incluso elegir un delimitador personalizado si cambias de opinión más tarde. A continuación verás un ejemplo completo de C# ejecutable, por qué cada línea es importante y algunos consejos para evitar los problemas habituales.

> **Pro tip:** Este enfoque funciona con la popular biblioteca Aspose.Cells, pero los conceptos se trasladan a cualquier API de Excel para .NET que ofrezca un método estilo `ExportTable`.

## Lo que necesitarás

- **.NET 6+** (o .NET Framework 4.6+). El código se compila en cualquier runtime reciente.
- **Aspose.Cells for .NET** (prueba gratuita o con licencia). Instálalo vía NuGet: `dotnet add package Aspose.Cells`.
- Un libro de trabajo de entrada llamado `input.xlsx` ubicado en una carpeta que controles.
- Un poco de curiosidad—no se requieren conocimientos profundos de Excel.

Si ya tienes todo eso, pasemos directamente a la solución.

## Paso 1 – Cargar el Workbook que deseas exportar

Primero creamos un objeto `Workbook` que apunta al archivo fuente. Este objeto representa todo el archivo Excel, incluidas todas las hojas, rangos con nombre y formato.

```csharp
using Aspose.Cells;

// Step 1: Load the workbook that contains the data to export
Workbook workbook = new Workbook(@"C:\Data\input.xlsx");
```

*Por qué es importante:*  
Cargar el workbook te da acceso a la colección de hojas (`workbook.Worksheets`). Sin este objeto no puedes referenciar celdas, rangos o configuraciones de exportación.

> **Nota:** Si tu archivo está en un recurso compartido de red, antepone `\\` o usa una ruta UNC—Aspose.Cells lo maneja sin problemas.

## Paso 2 – Configurar opciones de exportación (valores como cadena y delimitador de tabulación)

Ahora indicamos a la biblioteca cómo queremos que se escriban los datos. Al establecer `ExportAsString = true` obligamos a que cada celda se trate como una cadena simple, lo que elimina los formatos numéricos específicos de la configuración regional de Excel. La parte `Delimiter = "\t"` es el corazón de **exportar excel como tab**.

```csharp
// Step 2: Configure the export options – export values as strings and use a tab delimiter
ExportTableOptions exportOptions = new ExportTableOptions
{
    ExportAsString = true,   // ensures numbers become plain text, not scientific notation
    Delimiter = "\t"         // tab character – perfect for TSV files
};
```

*Por qué es importante:*  
Si omites `ExportAsString`, una celda que contiene `12345` podría convertirse en `12,345` en algunas configuraciones regionales, rompiendo los analizadores posteriores. El delimitador puede cambiarse por comas, barras verticales u otro carácter si luego decides **exportar excel con delimitador** distinto a una tabulación.

## Paso 3 – Exportar un rango específico a un archivo de texto

Finalmente, elegimos el rango que nos interesa (`A1:D10` en este ejemplo) y lo escribimos en `out.txt`. El método `ExportTable` hace todo el trabajo pesado: lee las celdas, aplica las opciones y envía el resultado al disco.

```csharp
// Step 3: Export the range A1:D10 from the first worksheet to a text file
Worksheet sheet = workbook.Worksheets[0]; // first worksheet (index 0)
sheet.Cells.ExportTable("A1", "D10", @"C:\Data\out.txt", exportOptions);
```

Después de ejecutar esto, encontrarás `out.txt` con contenido similar a:

```
Name    Age    City    Score
Alice   30     NY      85
Bob     25     LA      90
...
```

Cada columna está separada por una **tabulación**, listo para `awk`, `PowerShell` o cualquier herramienta compatible con CSV que respete las tabulaciones.

### Verificación rápida

Abre el archivo generado en un editor de texto plano (Notepad, VS Code) y confirma:

1. Las columnas se alinean cuando activas “Mostrar espacios en blanco”.
2. No aparecen comillas ni comas extra.
3. Todas las celdas numéricas aparecen exactamente como en Excel (gracias a `ExportAsString`).

Si algo parece incorrecto, verifica que el workbook de origen no oculte filas/columnas y que hayas referenciado el índice de hoja correcto.

## Variaciones comunes y casos límite

### Exportar una hoja completa

Si deseas **exportar excel rango** que cubra toda la hoja, puedes usar `sheet.Cells.MaxDisplayRange`:

```csharp
var maxRange = sheet.Cells.MaxDisplayRange;
sheet.Cells.ExportTable(maxRange.FirstRow, maxRange.FirstColumn,
                       maxRange.RowCount, maxRange.ColumnCount,
                       @"C:\Data\fullSheet.txt", exportOptions);
```

### Usar un delimitador diferente

Cambiar de tabulación a barra vertical (`|`) es tan fácil como modificar una línea:

```csharp
exportOptions.Delimiter = "|"; // now we have a pipe‑delimited file
```

Esto satisface el escenario **exportar excel con delimitador** sin reescribir otro código.

### Manejar archivos grandes (> 100 MB)

Para libros de trabajo masivos, transmite la exportación para evitar cargar todo en memoria:

```csharp
using (FileStream fs = new FileStream(@"C:\Data\largeOut.txt", FileMode.Create, FileAccess.Write))
{
    sheet.Cells.ExportTable("A1", "Z5000", fs, exportOptions);
}
```

### Convertir varias hojas en una sola pasada

Si necesitas **convertir excel a txt** para varias hojas, recórrelas en un bucle:

```csharp
for (int i = 0; i < workbook.Worksheets.Count; i++)
{
    string outPath = $@"C:\Data\Sheet{i + 1}.txt";
    workbook.Worksheets[i].Cells.ExportTable("A1", "D10", outPath, exportOptions);
}
```

Cada hoja genera su propio archivo TSV—útil para trabajos por lotes.

## Ejemplo completo (listo para copiar y pegar)

A continuación tienes el programa completo, listo para compilar. Solo reemplaza las rutas de archivo por las tuyas.

```csharp
using System;
using Aspose.Cells;

namespace ExcelToTxtDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load the workbook
            string inputPath = @"C:\Data\input.xlsx";
            Workbook workbook = new Workbook(inputPath);

            // 2️⃣ Set export options – strings + tab delimiter
            ExportTableOptions exportOptions = new ExportTableOptions
            {
                ExportAsString = true,
                Delimiter = "\t"
            };

            // 3️⃣ Export range A1:D10 from the first worksheet
            Worksheet sheet = workbook.Worksheets[0];
            string outputPath = @"C:\Data\out.txt";
            sheet.Cells.ExportTable("A1", "D10", outputPath, exportOptions);

            Console.WriteLine($"Export complete! Check {outputPath}");
        }
    }
}
```

**Salida esperada:** Un archivo llamado `out.txt` donde cada columna está separada por un carácter de tabulación y cada valor de celda aparece exactamente como en Excel.

## Preguntas frecuentes

- **¿Funciona esto con archivos .xls?**  
  Sí. Aspose.Cells detecta automáticamente el formato, por lo que puedes apuntar `Workbook` a un `.xls` antiguo y el mismo código funciona.

- **¿Qué pasa si mis datos contienen tabulaciones?**  
  Las tabulaciones dentro de una celda se conservarán, lo que puede romper los analizadores TSV. En ese caso, considera cambiar a un delimitador de barra vertical (`|`) actualizando `exportOptions.Delimiter`.

- **¿Puedo exportar fórmulas en lugar de valores?**  
  Establece `exportOptions.ExportAsString = false` y usa la sobrecarga de `ExportTableOptions` que incluye `ExportFormula = true`. La salida contendrá el texto bruto de la fórmula.

- **¿Hay forma de omitir filas ocultas?**  
  Sí. Configura `exportOptions.ExportHiddenRows = false` (el valor predeterminado es `true`). Las filas ocultas se excluirán del archivo de texto final.

## Conclusión

Ahora tienes una receta sólida y lista para producción sobre **cómo exportar excel** datos como archivo de texto delimitado por tabulaciones, cómo **exportar excel como tab** y cómo **convertir excel a txt** con control total sobre delimitadores y selección de rangos. Al aprovechar el método `ExportTable` de Aspose.Cells evitas construir CSV manualmente, preservas la fidelidad de los datos y mantienes tu base de código limpia.

¿Listo para el siguiente reto? Prueba:

- Exportar directamente a un `MemoryStream` para APIs web.  
- Añadir una fila de encabezado dinámicamente basada en el contenido de la primera fila.  
- Integrar esta rutina en una Azure Function que vigile un bucket de almacenamiento en busca de nuevas cargas de Excel.

Pruébalo, ajusta el delimitador y deja que los datos fluyan donde los necesites. ¡Feliz codificación!  

<img src="export-excel.png" alt="how to export excel example" style="max-width:100%; height:auto;" />

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}