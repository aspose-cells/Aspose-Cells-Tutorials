---
category: general
date: 2026-08-17
description: Cómo duplicar una hoja de cálculo en Java usando Aspose.Cells, preservando
  la tabla dinámica, copiando la tabla dinámica a un nuevo libro de trabajo y creando
  un libro de trabajo a partir de una hoja.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to duplicate worksheet
- how to copy pivot
- how to preserve pivot
- copy pivot to workbook
- create workbook from sheet
language: es
lastmod: 2026-08-17
og_description: Cómo duplicar una hoja de cálculo en Java usando Aspose.Cells, preservando
  la tabla dinámica, copiando la tabla dinámica a un nuevo libro de trabajo y creando
  un libro de trabajo a partir de una hoja, todo explicado paso a paso.
og_image_alt: Screenshot of Java code duplicating an Excel worksheet with a pivot
  table using Aspose.Cells
og_title: Cómo duplicar una hoja de cálculo y mantener las tablas dinámicas – Guía
  de Java
schemas:
- author: Aspose
  dateModified: '2026-08-17'
  description: How to duplicate worksheet in Java using Aspose.Cells, preserving the
    pivot table, copying pivot to a new workbook, and creating a workbook from a sheet.
  headline: How to duplicate worksheet and preserve pivot tables in Java
  type: TechArticle
- description: How to duplicate worksheet in Java using Aspose.Cells, preserving the
    pivot table, copying pivot to a new workbook, and creating a workbook from a sheet.
  name: How to duplicate worksheet and preserve pivot tables in Java
  steps:
  - name: – Load the workbook that contains the pivot table
    text: '```java import com.aspose.cells.*;'
  - name: – Create a new workbook and duplicate the entire worksheet
    text: '```java // Create an empty destination workbook Workbook destinationWorkbook
      = new Workbook();'
  - name: – Save the new workbook
    text: '```java // Save the duplicated workbook; the pivot remains functional destinationWorkbook.save("YOUR_DIRECTORY/copy_with_pivot.xlsx");
      } } ```'
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel
- Pivot Table
- Workbook
title: Cómo duplicar una hoja de cálculo y preservar las tablas dinámicas en Java
url: /es/java/excel-pivot-tables/how-to-duplicate-worksheet-and-preserve-pivot-tables-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo duplicar una hoja de cálculo y preservar tablas dinámicas en Java

Duplicar una hoja de cálculo manteniendo su tabla dinámica intacta es una necesidad frecuente cuando automatizas la generación de informes en Excel. Esta guía muestra cómo copiar una tabla dinámica a un nuevo libro de trabajo usando Aspose.Cells para Java, y también cubre cómo preservar la tabla dinámica al crear un libro de trabajo a partir de una hoja.

Aprenderás a cargar un libro de trabajo existente, duplicar la hoja que contiene una tabla dinámica y guardar el resultado como un archivo nuevo. El tutorial asume que tienes un entorno básico de desarrollo Java y una licencia válida de Aspose.Cells (la evaluación gratuita funciona para pruebas). No se requieren herramientas externas más allá del JAR de Aspose.Cells.

## Requisitos previos

Antes de comenzar, asegúrate de tener:

* Java Development Kit (JDK) 8 o superior.
* Maven o Gradle para gestionar la dependencia de Aspose.Cells.
* Un archivo Excel (`source.xlsx`) que contenga al menos una tabla dinámica en la primera hoja.
* Un directorio donde puedas leer el archivo origen y escribir el libro de trabajo duplicado.

Agrega la dependencia de Aspose.Cells a tu `pom.xml` (Maven) o `build.gradle` (Gradle). Para Maven:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version> <!-- use the latest version -->
</dependency>
```

## Cómo duplicar una hoja de cálculo con una tabla dinámica

La operación principal es un proceso de tres pasos: cargar, copiar y guardar. Cada paso se explica a continuación.

### Paso 1 – Cargar el libro de trabajo que contiene la tabla dinámica

```java
import com.aspose.cells.*;

public class CopyPivotTable {
    public static void main(String[] args) throws Exception {
        // Load the source workbook that holds the pivot table
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/source.xlsx");
        Worksheet sourceWorksheet = sourceWorkbook.getWorksheets().get(0);
```

*Por qué es importante este paso*: El objeto `Workbook` representa todo el archivo Excel. Al obtener la primera hoja (`get(0)`), apuntas a la hoja que contiene la tabla dinámica que deseas duplicar.

### Paso 2 – Crear un nuevo libro de trabajo y duplicar la hoja completa

```java
        // Create an empty destination workbook
        Workbook destinationWorkbook = new Workbook();

        // Duplicate the source worksheet, preserving its pivot table
        destinationWorkbook.getWorksheets().addCopy(sourceWorksheet);
```

`addCopy` clona la hoja **incluyendo** todos los objetos incrustados, fórmulas y cachés de tabla dinámica. Esta es la forma recomendada de **cómo copiar una tabla dinámica** porque la definición de la tabla y su origen de datos se transfieren juntos.

### Paso 3 – Guardar el nuevo libro de trabajo

```java
        // Save the duplicated workbook; the pivot remains functional
        destinationWorkbook.save("YOUR_DIRECTORY/copy_with_pivot.xlsx");
    }
}
```

Después de la ejecución, `copy_with_pivot.xlsx` contiene una copia exacta de la hoja original, y la tabla dinámica funciona sin configuración adicional.

**Resultado esperado**: Al abrir `copy_with_pivot.xlsx` en Excel se muestra la hoja duplicada con el mismo diseño de tabla dinámica, filtros y campos calculados que el archivo origen.

## Cómo copiar una tabla dinámica a otro libro de trabajo

Si necesitas mover una tabla dinámica sin copiar toda la hoja, puedes extraer la caché de la tabla y adjuntarla a una nueva hoja. El siguiente fragmento demuestra ese enfoque:

```java
// Assume sourceWorkbook and sourceWorksheet are already loaded
PivotTable pivot = sourceWorksheet.getPivotTables().get(0);

// Create a new workbook and a blank worksheet
Workbook targetWorkbook = new Workbook();
Worksheet targetSheet = targetWorkbook.getWorksheets().add("PivotCopy");

// Import the pivot table definition
targetSheet.getPivotTables().addCopy(pivot);
targetWorkbook.save("YOUR_DIRECTORY/pivot_only_copy.xlsx");
```

Este código responde a **cómo copiar una tabla dinámica** copiando solo el objeto de tabla dinámica, no la hoja completa. El método `addCopy` en la colección `PivotTables` asegura que la caché de la tabla se duplique, cumpliendo con los requisitos de **cómo preservar una tabla dinámica**.

## Cómo preservar la tabla dinámica al crear un libro de trabajo a partir de una hoja

A veces comienzas con una hoja que no pertenece a un libro de trabajo (por ejemplo, generas una hoja en memoria). Para **crear un libro de trabajo a partir de una hoja** manteniendo la tabla dinámica, sigue estos pasos:

```java
// Create a worksheet in memory
Worksheet tempSheet = new Worksheet();
PivotTable pivot = tempSheet.getPivotTables().add("A1", "B10", "MyPivot");

// Configure the pivot source range, rows, columns, data fields, etc.
// (Omitted for brevity – see Aspose.Cells docs for detailed setup)

// Wrap the worksheet in a new workbook
Workbook newWorkbook = new Workbook();
newWorkbook.getWorksheets().addCopy(tempSheet);
newWorkbook.save("YOUR_DIRECTORY/created_from_sheet.xlsx");
```

Al agregar la hoja a un `Workbook` nuevo después de que la tabla dinámica esté totalmente definida, garantizas que **cómo preservar una tabla dinámica** funciona incluso cuando la hoja se originó fuera de un archivo existente.

## Consejos prácticos y errores comunes

| Consejo | Por qué es importante |
|-----|----------------|
| Usa `addCopy` en lugar de `copy` | `addCopy` clona la caché subyacente de la tabla dinámica; un simple `copy` puede perder la conexión al origen de datos. |
| Mantén los archivos origen y destino en el mismo sistema de archivos | Las rutas relativas en el origen de datos de la tabla dinámica se resuelven correctamente, reduciendo errores de “origen no encontrado”. |
| Verifica la caché de la tabla después de copiar | Llama a `pivot.refresh()` si los datos de origen cambiaron entre la copia y la operación de guardado. |
| Libera los libros de trabajo cuando termines | `sourceWorkbook.dispose();` libera recursos nativos, lo cual es importante para archivos grandes. |

## Casos límite que podrías encontrar

* **Múltiples hojas con tablas dinámicas interdependientes** – Copia cada hoja individualmente; las cachés compartidas se duplican automáticamente, pero puede que necesites reasignar conexiones de datos externas.
* **Tablas dinámicas basadas en consultas SQL externas** – Asegúrate de que el entorno de destino pueda acceder a la misma base de datos; de lo contrario la tabla mostrará errores “#REF!”. 
* **Libros de trabajo grandes (>100 MB)** – Usa `WorkbookSettings.setMemorySetting(MemorySetting.MEMORY_PREFERENCE)` para reducir la presión de memoria durante la operación de copia.

## Ejemplo completo y ejecutable

A continuación se muestra el programa completo que incorpora todos los pasos discutidos. Guárdalo como `CopyPivotTable.java`, ajusta las rutas de archivo y ejecútalo con tu IDE preferido o mediante `javac`/`java`.



## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y funcionales con explicaciones paso a paso para ayudarte a dominar características adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Cómo crear tablas dinámicas en Excel usando Aspose.Cells para Java: Guía completa](/cells/english/java/data-analysis/create-pivot-tables-excel-aspose-cells-java/)
- [Cómo actualizar el origen de una tabla dinámica de Excel con Aspose.Cells para Java: Guía completa](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [Cómo implementar segmentaciones en tablas dinámicas usando Aspose.Cells para Java: Guía completa](/cells/english/java/data-analysis/implement-slicers-pivot-tables-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}