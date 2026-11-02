---
category: general
date: 2026-09-18
description: cómo duplicar una tabla dinámica en Java con Aspose.Cells – copiar una
  tabla dinámica entre libros de trabajo de forma rápida y fiable.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to duplicate pivot
- copy range between workbooks
- how to copy pivot
- copy pivot to workbook
- load excel workbook java
language: es
lastmod: 2026-09-18
og_description: cómo duplicar una tabla dinámica en Java usando Aspose.Cells. Sigue
  este tutorial completo para copiar una tabla dinámica entre libros de trabajo con
  código Java limpio.
og_image_alt: Screenshot showing a Java IDE copying a pivot table between two Excel
  workbooks
og_title: Duplicar una tabla dinámica en Java – guía paso a paso
schemas:
- author: Aspose
  dateModified: '2026-09-18'
  description: how to duplicate pivot in Java with Aspose.Cells – copy a pivot table
    between workbooks quickly and reliably.
  headline: How to duplicate pivot in Java using Aspose.Cells
  type: TechArticle
- description: how to duplicate pivot in Java with Aspose.Cells – copy a pivot table
    between workbooks quickly and reliably.
  name: How to duplicate pivot in Java using Aspose.Cells
  steps:
  - name: '**Load the source workbook** – this gives you access to the worksheet that
      holds the pivot.'
    text: '**Load the source workbook** – this gives you access to the worksheet that
      holds the pivot.'
  - name: '**Define the cell area** that encloses the pivot.'
    text: '**Define the cell area** that encloses the pivot.'
  - name: '**Create a destination workbook** – an empty file that will receive the
      copied range.'
    text: '**Create a destination workbook** – an empty file that will receive the
      copied range.'
  - name: '**Copy the range** – Aspose.Cells automatically duplicates the pivot definition.'
    text: '**Copy the range** – Aspose.Cells automatically duplicates the pivot definition.'
  - name: '**Save the destination workbook** – you now have a separate file with the
      same pivot.'
    text: '**Save the destination workbook** – you now have a separate file with the
      same pivot.'
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: Cómo duplicar una tabla dinámica en Java usando Aspose.Cells
url: /es/java/excel-pivot-tables/how-to-duplicate-pivot-in-java-using-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo duplicar una tabla dinámica en Java usando Aspose.Cells

Si necesitas **duplicar una tabla dinámica** en una aplicación Java, esta guía te muestra los pasos exactos. Al cargar un libro de Excel, definir el área de celdas de la tabla dinámica y copiar ese rango a un nuevo libro, puedes mover una tabla dinámica sin perder su definición ni sus datos.

Copiar una tabla dinámica es un requerimiento común cuando generas informes, archivas análisis o divides un libro grande en piezas modulares. En este tutorial aprenderás cómo **copiar rangos entre libros de trabajo**, cómo **cargar un libro de Excel con Java**, y los matices de **copiar una tabla dinámica** de forma segura.

Terminarás con un programa Java listo para ejecutar que duplica una tabla dinámica de `Source.xlsx` a `PivotCopied.xlsx` usando Aspose.Cells para Java.

## Requisitos previos

Antes de comenzar, asegúrate de tener:

* JDK 8 o superior instalado.
* Maven (u otra herramienta de compilación) para gestionar dependencias.
* Aspose.Cells for Java versión 23.10 o posterior. Añade la siguiente dependencia Maven a tu `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.10</version>
    <classifier>jdk17</classifier> <!-- adjust classifier to your JDK version -->
</dependency>
```

* Un libro de origen (`Source.xlsx`) que contiene una tabla dinámica en el rango **A1:H30**.

## Cómo duplicar una tabla dinámica en Java

La idea principal es sencilla:

1. **Cargar el libro de origen** – esto te da acceso a la hoja que contiene la tabla dinámica.
2. **Definir el área de celdas** que envuelve la tabla dinámica.
3. **Crear un libro de destino** – un archivo vacío que recibirá el rango copiado.
4. **Copiar el rango** – Aspose.Cells duplica automáticamente la definición de la tabla dinámica.
5. **Guardar el libro de destino** – ahora tienes un archivo separado con la misma tabla dinámica.

A continuación se muestra un programa Java completo y ejecutable que sigue esos pasos.

```java
package com.example.excelpivot;

import com.aspose.cells.*;

public class DuplicatePivotExample {

    public static void main(String[] args) throws Exception {
        // ---------- Step 1: Load the source workbook ----------
        // Replace the path with the actual location of your source file.
        String srcPath = "YOUR_DIRECTORY/Source.xlsx";
        Workbook srcWorkbook = new Workbook(srcPath);
        // The first worksheet (index 0) contains the pivot table.
        Worksheet srcWorksheet = srcWorkbook.getWorksheets().get(0);

        // ---------- Step 2: Define the cell area that contains the pivot ----------
        // The pivot occupies A1:H30 in the source sheet.
        CellArea srcRange = CellArea.create("A1", "H30");

        // ---------- Step 3: Create a new workbook for the copy ----------
        Workbook destWorkbook = new Workbook();               // creates a blank workbook
        Worksheet destWorksheet = destWorkbook.getWorksheets().get(0);

        // ---------- Step 4: Copy the range (pivot table is duplicated automatically) ----------
        // CopyOptions can be left default; it ensures that all formatting and pivot objects are preserved.
        srcWorksheet.copyRange(srcRange, destWorksheet, "A1", new CopyOptions());

        // ---------- Step 5: Save the destination workbook ----------
        String destPath = "YOUR_DIRECTORY/PivotCopied.xlsx";
        destWorkbook.save(destPath);

        System.out.println("Pivot table duplicated successfully to " + destPath);
    }
}
```

### Por qué funciona esto

* **Aspose.Cells** trata una tabla dinámica como parte de la colección de celdas de la hoja. Cuando invocas `copyRange`, la biblioteca copia no solo los valores de las celdas sino también la caché y definición subyacentes de la tabla dinámica, de modo que el nuevo libro contiene un duplicado completamente funcional.
* El objeto `CopyOptions` por defecto preserva fórmulas, formatos y objetos incrustados. Puedes personalizarlo (p. ej., `setCopyColumnWidths(true)`) si necesitas un control adicional.

## Copiar rangos entre libros de trabajo – análisis más profundo

Aunque el ejemplo anterior copia un único bloque contiguo, `copyRange` puede manejar cualquier área rectangular. Si tu tabla dinámica abarca rangos no adyacentes, puedes llamar a `copyRange` varias veces o usar `Worksheet.copy` para duplicar la hoja completa.

```java
// Example: copy the whole sheet, preserving all pivots and charts
srcWorksheet.copy(destWorksheet, new CopyOptions());
```

**Consejo:** Al copiar libros grandes, habilita `CopyOptions.setPreserveCellStyle(true)` para evitar la duplicación innecesaria de estilos, lo que puede mejorar el rendimiento.

## Cómo copiar una tabla dinámica a un libro – manejo de múltiples tablas dinámicas

Si la hoja de origen contiene más de una tabla dinámica, puedes iterar sobre las tablas dinámicas de la hoja y copiar cada una individualmente:

```java
for (int i = 0; i < srcWorksheet.getPivotTables().getCount(); i++) {
    PivotTable pt = srcWorksheet.getPivotTables().get(i);
    // Determine the range that the pivot occupies
    CellArea pivotArea = pt.getPivotTableArea();
    srcWorksheet.copyRange(pivotArea, destWorksheet, pt.getName() + "!A1", new CopyOptions());
}
```

Este enfoque garantiza que cada tabla dinámica conserve su nombre y fuente de datos originales.

## Cargar un libro de Excel con Java – errores comunes

* **Separadores de rutas de archivo:** Usa barras diagonales (`/`) o `File.separator` para mantener el código independiente de la plataforma.
* **Licencia ausente:** Aspose.Cells funciona en modo de evaluación, pero la salida contendrá una marca de agua. Registra una licencia con `License license = new License(); license.setLicense("Aspose.Total.Java.lic");` antes de cargar el libro para eliminar la marca de agua.
* **Archivos grandes:** Para libros mayores de 100 MB, considera usar `WorkbookFactory.create(InputStream, new LoadOptions(LoadFormat.XLSX))` con opciones de transmisión para reducir el consumo de memoria.

## Resumen completo del ejemplo de extremo a extremo

Uniendo todo, aquí tienes el programa final que puedes copiar y pegar en tu IDE:

```java
package com.example.excelpivot;

import com.aspose.cells.*;

public class DuplicatePivotExample {
    public static void main(String[] args) throws Exception {
        // Load license (optional, removes evaluation watermark)
        // License lic = new License();
        // lic.setLicense("Aspose.Total.Java.lic");

        // 1️⃣ Load source workbook
        Workbook srcWorkbook = new Workbook("YOUR_DIRECTORY/Source.xlsx");
        Worksheet srcWorksheet = srcWorkbook.getWorksheets().get(0);

        // 2️⃣ Define pivot range (A1:H30)
        CellArea srcRange = CellArea.create("A1", "H30");

        // 3️⃣ Prepare destination workbook
        Workbook destWorkbook = new Workbook();
        Worksheet destWorksheet = destWorkbook.getWorksheets().get(0);

        // 4️⃣ Copy the pivot (Aspose.Cells handles the pivot cache automatically)
        srcWorksheet.copyRange(srcRange, destWorksheet, "A1", new CopyOptions());

        // 5️⃣ Save the result
        destWorkbook.save("YOUR_DIRECTORY/PivotCopied.xlsx");

        System.out.println("Pivot table duplicated successfully.");
    }
}
```

**Salida esperada:** Después de la ejecución, `PivotCopied.xlsx` aparece en el directorio especificado. Al abrirlo en Excel muestra el mismo diseño de tabla dinámica, filtros y datos que en `Source.xlsx`. Todos los campos calculados y el formato se conservan.

## Preguntas frecuentes

* **¿Funciona esto con formatos antiguos de Excel (.xls)?**  
  Sí. Aspose.Cells detecta automáticamente el formato. Usa `new Workbook("file.xls")` y la misma lógica de copia se aplica.

* **¿Qué pasa si la tabla dinámica hace referencia a fuentes de datos externas?**  
  La copia conserva la referencia original a la fuente de datos. Si el entorno de destino no puede acceder a esa fuente, la tabla dinámica mostrará errores `#REF!`. Para evitarlo, actualiza la tabla dinámica después de copiarla o cambia su fuente de datos mediante `PivotTable.setDataSource(...)`.

* **¿Puedo copiar una tabla dinámica a una hoja con nombre específico?**  
  Por supuesto. Después de crear la hoja de destino, renómbrala:

  ```java
  destWorksheet.setName("ReportPivot");
  srcWorksheet.copyRange(srcRange, destWorksheet, "A1", new CopyOptions());
  ```

## Conclusión

Ahora sabes **cómo duplicar tablas dinámicas** en Java usando Aspose.Cells, cómo **copiar rangos entre libros de trabajo**, y las mejores prácticas para **cargar un libro de Excel con Java**. Siguiendo el proceso de cinco pasos—cargar, definir, crear destino, copiar y guardar—puedes automatizar la generación de informes, archivar análisis o dividir libros complejos sin perder la funcionalidad de la tabla dinámica.

A continuación, explora temas relacionados como **copiar tabla dinámica a un libro** con múltiples hojas, o integrar la tabla dinámica duplicada en una canalización de procesamiento de datos más grande usando Apache POI para escenarios sin Aspose. Experimenta con diferentes configuraciones de `CopyOptions` para afinar el rendimiento en libros de trabajo masivos.

¡Feliz codificación!

## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y funcionales con explicaciones paso a paso para ayudarte a dominar características adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Cómo crear tablas dinámicas en Excel usando Aspose.Cells para Java: Guía completa](/cells/english/java/data-analysis/create-pivot-tables-excel-aspose-cells-java/)
- [Cómo actualizar la fuente de una tabla dinámica de Excel con Aspose.Cells para Java: Guía completa](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [Agrupar campos de tabla dinámica en libros de Excel usando Aspose.Cells para Java - Guía completa](/cells/english/java/data-analysis/aspose-cells-java-group-pivot-fields-excel-workbook/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}