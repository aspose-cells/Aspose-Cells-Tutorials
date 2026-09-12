---
category: general
date: 2026-09-11
description: Crear una nueva hoja de cálculo y copiar un rango de Excel usando Aspose.Cells.
  Aprende cómo copiar un rango entre hojas manteniendo las tablas dinámicas.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create new worksheet
- copy excel range
- copy range between sheets
- copy range aspose.cells
language: es
lastmod: 2026-09-11
og_description: Crear una nueva hoja de cálculo y copiar un rango de Excel con Aspose.Cells.
  Este tutorial muestra los pasos exactos para copiar un rango entre hojas y mantener
  intactas las tablas dinámicas.
og_image_alt: Screenshot of a Java IDE showing code that creates a new worksheet and
  copies an Excel range
og_title: Crear una nueva hoja de cálculo y copiar rango de Excel – Guía de Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-09-11'
  description: Create new worksheet and copy Excel range using Aspose.Cells. Learn
    how to copy range between sheets while preserving pivot tables.
  headline: Create new worksheet and copy Excel range with Aspose.Cells
  type: TechArticle
- questions:
  - answer: The `copy` method also copies merge information, so merged cells appear
      unchanged on the destination sheet.
    question: What if the source range contains merged cells?
  - answer: Yes. Load a second `Workbook` instance, create a destination range in
      that workbook, and call `sourceRange.copy(destinationRange)`. The method handles
      cross‑workbook copying automatically.
    question: Can I copy to a different workbook?
  - answer: The copy operation overwrites any existing cells that intersect the destination
      range. To avoid data loss, ensure the destination area is empty or use a different
      start cell (e.g., `"B2"`).
    question: What if the destination sheet already has data?
  - answer: Aspose.Cells reuses the original pivot cache, which means the new pivot
      table remains linked to the same source data. If you need an independent cache,
      you must recreate the pivot table after copying.
    question: Is the pivot cache duplicated?
  type: FAQPage
tags:
- Aspose.Cells
- Excel automation
- Java
title: Crear una nueva hoja de cálculo y copiar un rango de Excel con Aspose.Cells
url: /es/java/range-management/create-new-worksheet-and-copy-excel-range-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crear nueva hoja de cálculo y copiar rango de Excel con Aspose.Cells

Si necesita **crear nueva hoja de cálculo** y mover datos dentro de un archivo Excel, Aspose.Cells lo hace sencillo. Esta guía muestra exactamente cómo copiar un rango de Excel de una hoja a otra mientras se preservan las tablas dinámicas dentro del rango.

Aprenderá cómo **copiar rango de excel**, cómo **copiar rango entre hojas**, y por qué el método `copy` de Aspose.Cells mantiene intactas las definiciones de las tablas dinámicas. No se requieren herramientas externas, solo un proyecto Java con la biblioteca Aspose.Cells.

## Requisitos previos

Antes de comenzar, asegúrese de tener:

- Java 17 o posterior instalado
- Aspose.Cells para Java (versión 23.12 o más reciente) añadido al classpath de su proyecto
- Un libro de origen (`input.xlsx`) que contiene una tabla dinámica en el rango que desea copiar
- Familiaridad básica con la sintaxis de Java y la gestión de dependencias Maven/Gradle

## Paso 1: Configurar el proyecto e importar Aspose.Cells

Cree un proyecto Maven sencillo (o Gradle, si lo prefiere) y añada la dependencia de Aspose.Cells:

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version>
</dependency>
```

Luego importe las clases requeridas en su archivo fuente Java:

```java
import com.aspose.cells.*;
import java.io.IOException;
```

*Por qué este paso es importante*: Importar las clases correctas le brinda acceso a `Workbook`, `Worksheet`, `Range` y al método `copy` que manejará la transferencia del rango.

## Paso 2: Cargar el libro de origen

Abra el libro que contiene los datos que desea copiar. El siguiente código carga `input.xlsx` desde un directorio que usted especifica:

```java
public class ExcelRangeCopy {
    public static void main(String[] args) throws IOException {
        // Load the source workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

*Explicación*: `Workbook` representa todo el archivo Excel. Cargarlo una vez le brinda acceso de lectura/escritura a cada hoja y colección de celdas.

## Paso 3: Identificar el rango de origen que incluye la tabla dinámica

Seleccione la hoja que contiene la tabla dinámica y defina el bloque exacto de celdas que desea copiar. En este ejemplo copiamos las celdas A1 a D20:

```java
        // Get the first worksheet (index 0) that contains the pivot table
        Worksheet sourceSheet = workbook.getWorksheets().get(0);

        // Define the source range – this range includes the pivot table
        Range sourceRange = sourceSheet.getCells().createRange("A1:D20");
```

*Por qué es importante*: Al crear un objeto `Range`, le indica a Aspose.Cells exactamente qué celdas (incluidos los objetos incrustados como tablas dinámicas) deben duplicarse.

## Paso 4: **Crear nueva hoja de cálculo** que recibirá los datos copiados

Ahora añadimos una hoja nueva al mismo libro. Este es el punto donde aparece la palabra clave principal:

```java
        // Create a new worksheet named "Copy"
        Worksheet destinationSheet = workbook.getWorksheets().add("Copy");

        // Define the top‑left cell of the destination range
        Range destinationRange = destinationSheet.getCells().createRange("A1");
```

*Explicación*: Añadir una nueva hoja aísla los datos copiados, facilitando la verificación de que la operación **copy excel range** se completó con éxito sin afectar la hoja original.

## Paso 5: Copiar el rango – la tabla dinámica se preserva automáticamente

Utilice el método `copy` para mover el rango de la hoja de origen a la hoja de destino. Aspose.Cells copia fórmulas, formato y definiciones de tablas dinámicas:

```java
        // Copy the range – the pivot table inside the range is preserved
        sourceRange.copy(destinationRange);
```

*Por qué funciona*: El método `copy` realiza una copia profunda de las celdas de origen. No solo copia valores; replica toda la estructura de la celda, lo que incluye la caché de la tabla dinámica. Por eso puede **copy range aspose.cells** y aún ver una tabla dinámica funcional en la nueva hoja.

## Paso 6: Guardar el libro con la nueva hoja de cálculo

Finalmente, escriba el libro modificado en disco:

```java
        // Save the workbook with the copied data
        workbook.save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

*Resultado*: `output.xlsx` ahora contiene la hoja original más una nueva hoja llamada **Copy** que contiene exactamente el mismo rango, incluida la tabla dinámica.

## Ejemplo completo funcional

Uniendo todas las piezas, aquí está el programa completo y ejecutable:

```java
import com.aspose.cells.*;
import java.io.IOException;

public class ExcelRangeCopy {
    public static void main(String[] args) throws IOException {
        // Step 1: Load the source workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // Step 2: Get the worksheet that contains the pivot table and define the source range
        Worksheet sourceSheet = workbook.getWorksheets().get(0);
        Range sourceRange = sourceSheet.getCells().createRange("A1:D20");

        // Step 3: Create a new worksheet that will receive the copied range
        Worksheet destinationSheet = workbook.getWorksheets().add("Copy");
        Range destinationRange = destinationSheet.getCells().createRange("A1");

        // Step 4: Copy the range – the pivot table inside the range is preserved
        sourceRange.copy(destinationRange);

        // Step 5: Save the workbook with the copied data
        workbook.save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

**Salida esperada**: Abra `output.xlsx` en Excel. Verá una hoja llamada **Copy** cuyas celdas A1:D20 contienen los mismos datos, formato y una tabla dinámica activa idéntica a la original.

## Preguntas comunes y casos límite

- **¿Qué pasa si el rango de origen contiene celdas combinadas?**  
  El método `copy` también copia la información de combinación, por lo que las celdas combinadas aparecen sin cambios en la hoja de destino.

- **¿Puedo copiar a un libro de trabajo diferente?**  
  Sí. Cargue una segunda instancia de `Workbook`, cree un rango de destino en ese libro y llame a `sourceRange.copy(destinationRange)`. El método maneja automáticamente la copia entre libros.

- **¿Qué pasa si la hoja de destino ya tiene datos?**  
  La operación de copia sobrescribe cualquier celda existente que intersecte el rango de destino. Para evitar pérdida de datos, asegúrese de que el área de destino esté vacía o use una celda de inicio diferente (p. ej., `"B2"`).

- **¿Se duplica la caché de la tabla dinámica?**  
  Aspose.Cells reutiliza la caché de tabla dinámica original, lo que significa que la nueva tabla dinámica sigue vinculada a los mismos datos de origen. Si necesita una caché independiente, debe recrear la tabla dinámica después de copiar.

## Consejos y mejores prácticas

- **Consejo profesional**: Use `Workbook.setForceFormulaRecalculation(true)` antes de guardar si su rango contiene fórmulas que dependen de datos fuera del bloque copiado.
- **Cuidado con** rangos grandes: copiar hojas masivas puede consumir mucha memoria. Considere copiar en fragmentos más pequeños si se produce `OutOfMemoryError`.
- **Consejo de rendimiento**: Desactive la actualización de pantalla (`workbook.getSettings().setCalculateFormulaOnOpen(false)`) al trabajar con archivos muy grandes para acelerar el proceso de copia.

## Conclusión

Ahora sabe cómo **crear nueva hoja de cálculo** y **copiar rango de excel** entre hojas usando Aspose.Cells, preservando tablas dinámicas y todos los atributos de las celdas. Esta técnica le permite duplicar programáticamente bloques de datos, crear plantillas de informes o reestructurar libros de trabajo sin copiar‑pegar manualmente.

A continuación, explore temas relacionados como **copy range aspose.cells** para operaciones entre libros, automatizar la actualización de tablas dinámicas o exportar la hoja copiada a PDF. Experimente con diferentes rangos de origen y nombres de hoja para adaptarse a su escenario de automatización específico. ¡Feliz codificación!

## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos con explicaciones paso a paso para ayudarle a dominar funciones adicionales de la API y explorar enfoques de implementación alternativos en sus propios proyectos.

- [Copiar formas entre hojas de Excel usando Aspose.Cells para .NET: Guía completa](/cells/english/net/images-shapes/copy-shapes-between-sheets-aspose-cells-dotnet/)
- [Copiar imágenes entre hojas en Excel usando Aspose.Cells para Java: Guía completa](/cells/english/java/images-shapes/copy-images-between-sheets-excel-aspose-cells-java/)
- [Excel Aspose Cells .NET Copiar datos de rango](/cells/hindi/net/range-management/excel-aspose-cells-dotnet-copy-range-data/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}