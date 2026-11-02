---
category: general
date: 2026-10-10
description: Aprende cómo eliminar una fila completa en un libro de Excel con C#.
  Esta guía paso a paso también cubre cómo eliminar una fila por índice y eliminar
  una fila por índice usando Aspose.Cells.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- delete entire row
- how to delete row
- remove row by index
- delete row excel
- delete row c#
language: es
lastmod: 2026-10-10
og_description: Eliminar una fila completa en un libro de Excel usando C#. Sigue esta
  guía para aprender cómo eliminar una fila por índice, quitar una fila por índice
  y guardar el archivo de forma segura.
og_image_alt: Screenshot of an Excel worksheet before and after deleting an entire
  row with C# code
og_title: Eliminar fila completa en Excel con C# – guía completa de programación
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: Learn how to delete entire row in an Excel workbook with C#. This step‑by‑step
    guide also covers how to delete row by index and remove row by index using Aspose.Cells.
  headline: How to delete entire row in an Excel file using C#
  type: TechArticle
tags:
- Excel
- C#
- Aspose.Cells
title: Cómo eliminar una fila completa en un archivo de Excel usando C#
url: /es/net/row-and-column-management/how-to-delete-entire-row-in-an-excel-file-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Delete entire row in an Excel file using C#

Si necesitas **delete entire row** en un libro de Excel, esta guía te muestra exactamente cómo hacerlo con C#. Ya sea que estés limpiando datos importados o construyendo una herramienta de informes, los pasos a continuación te permiten eliminar una fila por su índice y guardar el resultado sin perder otros datos.

También verás cómo el mismo enfoque responde a la pregunta **how to delete row** por índice, cómo **remove row by index**, y por qué funciona para escenarios de **delete row excel** en C#.

## Requisitos previos

* .NET 6.0 o posterior (el código funciona también con .NET Framework 4.6+)  
* La biblioteca **Aspose.Cells for .NET** (disponible vía NuGet: `Install-Package Aspose.Cells`)  
* Familiaridad básica con proyectos de consola o de escritorio en C#  

No se requieren componentes adicionales de interop de Excel o COM, lo que mantiene la solución ligera y segura para la ejecución del lado del servidor.

## Paso 1: Configurar el proyecto e importar espacios de nombres

Crea una nueva aplicación de consola (o agrega el código a un proyecto existente) y añade las directivas `using` requeridas:

```csharp
using System;
using Aspose.Cells;

namespace ExcelRowDeletion
{
    class Program
    {
        static void Main(string[] args)
        {
            // The rest of the tutorial code lives here.
        }
    }
}
```

*Por qué es importante*: Importar `Aspose.Cells` te brinda acceso a `Workbook`, `Worksheet` y al método `DeleteRows` que realiza la eliminación real de la fila.

## Paso 2: Cargar el libro de trabajo y seleccionar la hoja de cálculo

Debes cargar el archivo fuente (`input.xlsx`) y obtener la hoja de cálculo que deseas modificar. La primera hoja se accede con el índice `0`.

```csharp
// Load the workbook from disk
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

// Get the first worksheet (you can also use workbook.Worksheets["SheetName"])
Worksheet ws = workbook.Worksheets[0];
```

> **Consejo**: Si necesitas trabajar con una hoja específica, reemplaza el índice por el nombre de la hoja: `workbook.Worksheets["Data"]`.

## Paso 3: Eliminar la fila completa por su índice basado en cero

Aspose.Cells utiliza indexación basada en cero, por lo que la primera fila es `0`. Para eliminar la fila 5 (la sexta fila visual), llama a `DeleteRows` con `DeleteOptions.DeleteEntireRow`.

```csharp
// Delete one row starting at index 5 (zero‑based) and remove the whole row
ws.Cells[5, 0].DeleteRows(1, DeleteOptions.DeleteEntireRow);
```

*Explicación*:

* `ws.Cells[5, 0]` apunta a la primera celda de la fila que deseas eliminar.  
* `DeleteRows(1, DeleteOptions.DeleteEntireRow)` indica a Aspose.Cells que elimine **1** fila, y la bandera `DeleteEntireRow` asegura que **toda la fila** desaparezca, desplazando las filas inferiores hacia arriba.

### Cómo eliminar fila por índice en otros escenarios

* **Delete multiple consecutive rows** – cambia el primer argumento al número de filas que deseas eliminar:

  ```csharp
  // Remove rows 5, 6 and 7 (three rows total)
  ws.Cells[5, 0].DeleteRows(3, DeleteOptions.DeleteEntireRow);
  ```

* **Delete the last row** – usa `ws.Cells.MaxDataRow` para obtener el índice de la fila más baja poblada:

  ```csharp
  int lastRow = ws.Cells.MaxDataRow;
  ws.Cells[lastRow, 0].DeleteRows(1, DeleteOptions.DeleteEntireRow);
  ```

Estos fragmentos responden al requisito de **remove row by index** mientras mantienen el código fácil de leer.

## Paso 4: Guardar el libro de trabajo con la fila eliminada

Después de la eliminación, escribe el libro de trabajo modificado de nuevo en el disco. Puedes sobrescribir el archivo original o crear uno nuevo.

```csharp
// Save the workbook to a new file (or overwrite the original)
workbook.Save("YOUR_DIRECTORY/output.xlsx");
```

Si necesitas mantener el archivo original sin cambios, simplemente cambia la ruta de salida. El método `Save` admite muchos formatos (`.xls`, `.csv`, `.pdf`, etc.) – solo cambia la extensión del archivo.

## Ejemplo completo en funcionamiento

Juntando todo, aquí tienes un programa completo y listo para ejecutar:

```csharp
using System;
using Aspose.Cells;

namespace ExcelRowDeletion
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the workbook
            Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

            // 2️⃣ Select the first worksheet
            Worksheet ws = workbook.Worksheets[0];

            // 3️⃣ Delete the entire row at index 5 (sixth visual row)
            ws.Cells[5, 0].DeleteRows(1, DeleteOptions.DeleteEntireRow);

            // 4️⃣ Save the result
            workbook.Save("YOUR_DIRECTORY/output.xlsx");

            Console.WriteLine("Row deleted successfully. Output saved to output.xlsx");
        }
    }
}
```

**Salida esperada**: Después de ejecutar el programa, `output.xlsx` contendrá todas las filas originales excepto la que comenzaba en la fila visual 6. Todos los datos debajo de la fila eliminada se desplazan hacia arriba automáticamente, preservando fórmulas y formato.

## Errores comunes y cómo evitarlos

| Problema | Por qué ocurre | Solución |
|----------|----------------|----------|
| **Índice fuera de rango** | Intentar eliminar un índice de fila que no existe (p.ej., `ws.Cells[1000,0]` en una hoja de 200 filas) | Utiliza `ws.Cells.MaxDataRow` para verificar el índice válido más alto antes de llamar a `DeleteRows`. |
| **Eliminación parcial de fila** | Omitir `DeleteOptions.DeleteEntireRow` hace que solo se borren los contenidos de las celdas | Siempre pasa `DeleteOptions.DeleteEntireRow` cuando necesites eliminar toda la fila. |
| **Cambios inesperados en fórmulas** | Eliminar filas que forman parte de un rango de fórmula puede romper referencias | Re‑evalúa las fórmulas después de la eliminación (`workbook.CalculateFormula()`) si tu libro depende de rangos dinámicos. |
| **Guardar en una ubicación de solo lectura** | La llamada `Save` lanza una excepción si la carpeta está protegida | Asegúrate de que el directorio de destino sea escribible o ejecuta el programa con los permisos adecuados. |

Abordar estas preocupaciones hace que la solución sea robusta para uso en producción y satisface las consultas **delete row excel** y **delete row c#**.

## Avanzado: Eliminar filas basadas en una condición

A veces necesitas eliminar filas que cumplen un cierto criterio (p.ej., filas donde la columna A está vacía). El siguiente bucle demuestra una forma segura de escanear de abajo hacia arriba y eliminar las filas coincidentes:

```csharp
int lastRow = ws.Cells.MaxDataRow;
for (int row = lastRow; row >= 0; row--)
{
    // Check if column A (index 0) is empty
    if (ws.Cells[row, 0].StringValue == string.Empty)
    {
        ws.Cells[row, 0].DeleteRows(1, DeleteOptions.DeleteEntireRow);
    }
}
workbook.Save("YOUR_DIRECTORY/cleaned.xlsx");
```

Escanear de abajo hacia arriba evita el problema de desplazamiento de índices que ocurre al eliminar filas mientras se itera hacia adelante.

## Conclusión

Ahora sabes cómo **delete entire row** en un libro de Excel usando C#. La guía cubrió:

* Cargar un libro de trabajo y seleccionar una hoja de cálculo  
* Usar `DeleteRows` con `DeleteOptions.DeleteEntireRow` para **how to delete row** por índice  
* Guardar el archivo modificado de forma segura  
* Manejo de casos límite, consejos de rendimiento y un ejemplo de eliminación condicional  

Con este conocimiento puedes implementar con confianza la funcionalidad **remove row by index**, automatizar la limpieza de datos y integrar la manipulación de Excel en cualquier aplicación C#.  

**Próximos pasos**: explora otras funciones de Aspose.Cells como insertar filas, copiar rangos o convertir el libro a PDF—cada una de las cuales se basa en los mismos objetos `Workbook` y `Worksheet` que acabas de dominar. ¡Feliz codificación!

## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que se basan en las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y funcionales con explicaciones paso a paso para ayudarte a dominar funciones adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Cómo eliminar una fila de Excel usando Aspose.Cells .NET: Guía completa](/cells/english/net/worksheet-management/delete-excel-row-aspose-cells-net-tutorial/)
- [Aspose Cells Delete Rows – Proteger la fila de encabezado en Excel](/cells/english/net/row-and-column-management/aspose-cells-delete-rows-protect-header-row-in-excel/)
- [Gestión eficiente de filas en Excel usando Aspose.Cells para Java: Insertar y eliminar filas](/cells/english/java/worksheet-management/aspose-cells-java-row-operations-excel/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}