---
category: general
date: 2026-10-23
description: Aprende cómo duplicar una hoja de Excel en Java manteniendo las tablas
  dinámicas. Esta guía también muestra cómo copiar tablas dinámicas, copiar rangos
  de Excel y copiar una hoja con datos de tabla dinámica.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- duplicate excel sheet
- how to copy pivot
- copy excel range
- copy sheet with pivot
- copy pivot to workbook
language: es
lastmod: 2026-10-23
og_description: Duplica una hoja de Excel en Java manteniendo las tablas dinámicas.
  Sigue este tutorial completo para copiar tablas dinámicas, copiar rangos de Excel
  y copiar una hoja con datos de tabla dinámica.
og_image_alt: Screenshot showing a duplicated Excel sheet with pivot tables preserved
og_title: Duplicar una hoja de Excel con tablas dinámicas en Java – guía paso a paso
schemas:
- author: Aspose
  dateModified: '2026-10-23'
  description: Learn how to duplicate an Excel sheet in Java while preserving pivot
    tables. This guide also shows how to copy pivot tables, copy Excel ranges, and
    copy a sheet with pivot data.
  headline: How to duplicate an Excel sheet and keep pivot tables intact in Java
  type: TechArticle
- description: Learn how to duplicate an Excel sheet in Java while preserving pivot
    tables. This guide also shows how to copy pivot tables, copy Excel ranges, and
    copy a sheet with pivot data.
  name: How to duplicate an Excel sheet and keep pivot tables intact in Java
  steps:
  - name: Expected output
    text: 'Running the program creates `DuplicatedWithPivot.xlsx` in the target directory.
      Open the file in Excel and you will see:'
  - name: How to copy pivot to another workbook without copying the whole sheet?
    text: If you only need the pivot and its underlying data, copy the range that
      contains both the source data and the pivot, then use `setCopyPivotTable(true)`.
      The same code from **Step 4** applies; just ensure the range covers the data
      source.
  - name: What if the source workbook has multiple worksheets with pivots?
    text: 'Repeat **Step 3** for each worksheet you want to duplicate:'
  - name: Does this work with protected worksheets?
    text: 'Aspose.Cells can copy protected sheets, but you must unprotect them first
      if you need to modify the pivot after copying:'
  - name: Can I copy a pivot table to an existing workbook that already contains a
      sheet with the same name?
    text: 'Yes. Use `addCopy` with a unique name:'
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
- Pivot tables
title: Cómo duplicar una hoja de Excel y mantener intactas las tablas dinámicas en
  Java
url: /es/java/excel-pivot-tables/how-to-duplicate-an-excel-sheet-and-keep-pivot-tables-intact/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo duplicar una hoja de Excel y mantener intactas las tablas dinámicas en Java

Si necesitas **duplicar una hoja de Excel** mientras mantienes todas las tablas dinámicas activas, esta guía te muestra exactamente cómo hacerlo. Verás una solución concisa que copia una hoja, copia un rango específico e incluso copia una tabla dinámica a otro libro, todo en Java puro usando Aspose.Cells.

Duplicar una hoja de Excel es una tarea común cuando generas informes mensuales a partir de una plantilla o cuando necesitas una copia de pruebas para experimentar. El código a continuación funciona con Aspose.Cells 25.11 o posterior, que introdujo la opción `setCopyPivotTable(true)`.

## Lo que necesitarás

Antes de comenzar, asegúrate de tener:

- Java 17 (o cualquier JDK reciente) instalado
- Aspose.Cells for Java 25.11 o una versión más nueva en tu proyecto (coordenada Maven `com.aspose:aspose-cells:25.11`)
- Un libro de origen (`SourceWithPivot.xlsx`) que ya contenga una tabla dinámica
- Un IDE o herramienta de compilación de tu elección (IntelliJ IDEA, Eclipse, Maven, Gradle, etc.)

## Paso 1: Cargar el libro de origen que contiene la tabla dinámica

La primera operación es abrir el libro que contiene la tabla dinámica que deseas preservar.

```java
import com.aspose.cells.*;

public class DuplicateExcelSheet {
    public static void main(String[] args) throws Exception {
        // Load the source workbook with the pivot table
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/SourceWithPivot.xlsx");
```

> **Por qué este paso es importante:** Cargar el libro de origen te brinda acceso a los objetos de hoja, celdas y a las tablas dinámicas incrustadas. Sin esto, no puedes referenciar los datos de la tabla dinámica que planeas copiar.

## Paso 2: Crear un libro de destino vacío (o cargar uno existente)

Puedes comenzar con un libro en blanco o abrir un archivo existente que recibirá la hoja duplicada.

```java
        // Create a new, empty destination workbook
        Workbook dstWb = new Workbook();
```

> **Consejo:** Si ya tienes un libro de informes, reemplaza la línea anterior con `new Workbook("ExistingReport.xlsx")` para añadir la hoja duplicada a ese libro.

## Paso 3: Copiar toda la hoja – la tabla dinámica se conserva automáticamente

Copiar la hoja completa es la forma más sencilla de **copiar hoja con tabla dinámica**. Aspose.Cells copia la definición de la tabla dinámica y su caché automáticamente.

```java
        // Access the first worksheet (index 0) from the source workbook
        Worksheet srcWs = srcWb.getWorksheets().get(0);

        // Add a copy of the source worksheet to the destination workbook
        Worksheet dstWs = dstWb.getWorksheets().addCopy(srcWs);
```

> **Por qué funciona:** `addCopy` clona la estructura de la hoja, los valores de celda, estilos y cualquier tabla dinámica incrustada. La nueva hoja en `dstWb` será idéntica a la original, incluido el caché de la tabla dinámica.

## Paso 4: (Opcional) Copiar solo un rango específico que incluya la tabla dinámica

A veces no necesitas toda la hoja—quizá solo requieras una porción que contenga la tabla dinámica. Aquí es donde **copias un rango de Excel** y solicitas explícitamente que la tabla dinámica se copie.

```java
        // Define the source range that covers the pivot table (adjust as needed)
        Range srcRange = srcWs.getCells().createRange("A1:G30");

        // Define the target range in the destination worksheet
        Range dstRange = dstWs.getCells().createRange("A1");

        // Copy the range and tell Aspose.Cells to include the pivot table
        CopyOptions copyOptions = new CopyOptions();
        copyOptions.setCopyPivotTable(true); // new option in 25.11
        dstRange.copy(srcRange, copyOptions);
```

> **Cómo ayuda:** `setCopyPivotTable(true)` obliga al motor a duplicar la definición de la tabla dinámica incluso cuando copias un rango limitado. Sin esta bandera, solo se copiarían los datos sin formato y la tabla dinámica se perdería.

## Paso 5: Guardar el libro de destino

Finalmente, escribe el contenido duplicado en un nuevo archivo.

```java
        // Save the destination workbook to a new file
        dstWb.save("YOUR_DIRECTORY/DuplicatedWithPivot.xlsx");
    }
}
```

### Resultado esperado

Al ejecutar el programa se crea `DuplicatedWithPivot.xlsx` en el directorio de destino. Abre el archivo en Excel y verás:

- Una nueva hoja llamada `Sheet1 (Copy)` (o el nombre original con “Copy” añadido)
- La tabla dinámica aparece exactamente como en la hoja de origen, totalmente funcional
- Si utilizaste la copia de rango opcional, solo estarán presentes las celdas A1:G30, pero la tabla dinámica sigue funcionando porque su caché fue copiado

## Preguntas frecuentes y casos especiales

### ¿Cómo copiar una tabla dinámica a otro libro sin copiar toda la hoja?

Si solo necesitas la tabla dinámica y sus datos subyacentes, copia el rango que contiene tanto los datos de origen como la tabla dinámica, luego usa `setCopyPivotTable(true)`. El mismo código del **Paso 4** se aplica; solo asegúrate de que el rango cubra la fuente de datos.

### ¿Qué pasa si el libro de origen tiene varias hojas con tablas dinámicas?

Repite el **Paso 3** para cada hoja que quieras duplicar:

```java
for (int i = 0; i < srcWb.getWorksheets().getCount(); i++) {
    Worksheet ws = srcWb.getWorksheets().get(i);
    dstWb.getWorksheets().addCopy(ws);
}
```

### ¿Esto funciona con hojas protegidas?

Aspose.Cells puede copiar hojas protegidas, pero debes desprotegerlas primero si necesitas modificar la tabla dinámica después de copiar:

```java
srcWs.unprotect("password");
dstWs.unprotect("password");
```

### ¿Puedo copiar una tabla dinámica a un libro existente que ya contiene una hoja con el mismo nombre?

Sí. Usa `addCopy` con un nombre único:

```java
Worksheet dstWs = dstWb.getWorksheets().addCopy(srcWs);
dstWs.setName("PivotCopy_" + System.currentTimeMillis());
```

## Consejo profesional: verificar el caché de la tabla dinámica

Después de copiar, puedes confirmar programáticamente que el caché de la tabla dinámica existe:

```java
PivotTable pt = dstWs.getPivotTables().get(0);
System.out.println("Pivot cache ID: " + pt.getCacheIndex());
```

Si el ID del caché imprime un número no negativo, la tabla dinámica se duplicó con éxito.

## Conclusión

Ahora sabes cómo **duplicar una hoja de Excel** en Java manteniendo cada tabla dinámica, cómo **copiar tablas dinámicas** directamente, cómo **copiar un rango de Excel** que incluya una tabla dinámica, y cómo **copiar hoja con tabla dinámica** o **copiar tabla dinámica a un libro** usando Aspose.Cells 25.11+. Aplica estos patrones para automatizar la generación de informes, crear clones de plantillas o construir entornos de prueba que necesiten análisis idénticos basados en tablas dinámicas.

¿Listo para explorar más? Prueba exportar el libro duplicado a PDF, o refresca programáticamente el caché de la tabla dinámica después de copiar para asegurar que los datos más recientes se reflejen. ¡Feliz codificación!

## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos con explicaciones paso a paso para ayudarte a dominar funciones adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [How to duplicate worksheet and preserve pivot tables in Java](/cells/english/java/excel-pivot-tables/how-to-duplicate-worksheet-and-preserve-pivot-tables-in-java/)
- [How to Copy Pivot Table in Java – Complete Aspose.Cells Guide](/cells/english/java/excel-pivot-tables/how-to-copy-pivot-table-in-java-complete-aspose-cells-guide/)
- [How to copy range and preserve a pivot table in Java](/cells/english/java/excel-pivot-tables/how-to-copy-range-and-preserve-a-pivot-table-in-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}