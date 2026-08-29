---
category: general
date: 2026-07-23
description: Crea un nuevo libro de trabajo en Java y aprende cómo copiar una tabla
  dinámica, copiar un rango de Excel y exportar la tabla dinámica con Aspose.Cells
  en minutos.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create new workbook
- copy pivot table
- how to copy pivot
- copy excel range
- export pivot table
language: es
lastmod: 2026-07-23
og_description: Crea un nuevo libro de trabajo en Java y copia instantáneamente la
  tabla dinámica, copia el rango de Excel y luego exporta la tabla dinámica usando
  Aspose.Cells. Sigue este tutorial completo.
og_image_alt: Screenshot of Java code copying a pivot table from one workbook to another
og_title: Crear nuevo libro de trabajo en Java – Copiar tabla dinámica paso a paso
schemas:
- author: Aspose
  dateModified: '2026-07-23'
  description: Create new workbook in Java and learn how to copy pivot table, copy
    excel range, and export pivot table with Aspose.Cells in minutes.
  headline: Create New Workbook in Java – Full Guide to Copy Pivot Table
  type: TechArticle
- questions:
  - answer: You’ll need to copy each relevant range separately, then recreate the
      pivot on the destination sheet using `PivotTable` APIs.
    question: What if the source pivot spans more than one worksheet?
  - answer: Set `sourceRange.setCopyDataOnly(false)` before the copy. This tells Aspose
      to keep the cache but not the underlying source data.
    question: Can I copy only the pivot layout without the data?
  - answer: CSV doesn’t support pivots, but you can export the pivot’s *result* by
      calling `pivotTable.calculate()` and then saving the sheet as CSV.
    question: Is there a way to copy the pivot to a CSV file?
  - answer: Formatting lives in the style collection. After copying, you can call
      `destinationSheet.getCells().applyStyle(sourceSheet.getCells().getStyle())`
      to transfer styles.
    question: Why does the copied pivot lose its formatting?
  type: FAQPage
tags:
- Java
- Aspose.Cells
- Excel Automation
title: Crear nuevo libro de trabajo en Java – Guía completa para copiar tabla dinámica
url: /es/java/excel-pivot-tables/create-new-workbook-in-java-full-guide-to-copy-pivot-table/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crear nuevo libro de trabajo en Java – Guía completa para copiar tabla dinámica

¿Alguna vez te has preguntado cómo **create new workbook** en Java mientras preservas una tabla dinámica compleja? No eres el único rascándote la cabeza por esto. En muchas aplicaciones de informes necesitas mover una tabla dinámica de un archivo fuente a un libro de trabajo nuevo, tal vez para enviarlo a un cliente o para ejecutar cálculos adicionales. ¿La buena noticia? Con unas pocas líneas puedes hacer exactamente eso—sin necesidad de copiar‑pegar manualmente.

En este tutorial recorreremos todo el proceso: cargar el archivo fuente, definir el rango que contiene la tabla dinámica, **copying the Excel range**, crear un **new workbook**, y finalmente **exporting the pivot table** a un archivo nuevo. Al final tendrás un programa Java autónomo y ejecutable que responde a la pregunta “**how to copy pivot**” sin conjeturas.

## Prerequisites

Antes de sumergirnos, asegúrate de tener:

- Java 17 o posterior (el código funciona con cualquier JDK reciente)
- Biblioteca Aspose.Cells for Java (prueba gratuita o versión con licencia)
- Un archivo de ejemplo `source.xlsx` que contiene una tabla dinámica en el rango `A1:G20`
- Un IDE o herramienta de compilación (Maven/Gradle) para gestionar el JAR de Aspose.Cells

¿Los tienes? Genial—¡comencemos.

## Step 1: Set Up the Project and Import Aspose.Cells

Lo primero es añadir Aspose.Cells a tu proyecto. Si usas Maven, inserta esta dependencia en tu `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.8</version> <!-- check for the latest version -->
</dependency>
```

Si prefieres Gradle, el equivalente es:

```groovy
implementation 'com.aspose:aspose-cells:24.8'
```

Una vez que la biblioteca está en el classpath, importa las clases que necesitarás:

```java
import com.aspose.cells.*;
import java.io.IOException;
```

> **Consejo profesional:** Aspose.Cells es una biblioteca comercial, pero ofrece una evaluación totalmente funcional de 30 días que coloca una marca de agua en la salida—perfecta para probar esto.

## Step 2: Load the Source Workbook

Ahora crearemos objetos **create new workbook**, pero primero necesitamos la fuente que contiene la tabla dinámica. Este paso es la base para cualquier operación **copy excel range** porque el objeto rango sabe exactamente qué celdas (incluyendo la caché de la tabla dinámica) transferir.

```java
// Load the source workbook that contains the pivot table
Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/source.xlsx");

// Grab the first worksheet (index 0) – adjust if your pivot lives elsewhere
Worksheet sourceSheet = sourceWorkbook.getWorksheets().get(0);
```

¿por qué no leer directamente el rango? Porque los metadatos de la tabla dinámica viven en la caché de pivote de la hoja, y Aspose.Cells los agrupa automáticamente al copiar el rango.

## Step 3: Define the Range That Holds the Pivot Table

En muchos archivos del mundo real la tabla dinámica ocupa un bloque rectangular. Para este ejemplo asumiremos que está en `A1:G20`. Por supuesto, puedes ajustar la dirección para que coincida con tu diseño real.

```java
// Define the exact area that includes the pivot table
Range sourceRange = sourceSheet.getCells().createRange("A1:G20");
```

Si no estás seguro de la dirección exacta, puedes usar `sourceSheet.getCells().getMaxDataRow()` y `getMaxDataColumn()` para calcular los límites de forma dinámica. Es un truco útil cuando el tamaño de la tabla dinámica cambia con el tiempo.

## Step 4: **Create New Workbook** and Destination Worksheet

Este es el momento en que realmente **create new workbook** que recibirá el contenido copiado. Piensa en ello como el lienzo en blanco donde pegarás la tabla dinámica.

```java
// Create an empty workbook – this is our destination
Workbook destinationWorkbook = new Workbook();

// By default a new workbook comes with one worksheet
Worksheet destinationSheet = destinationWorkbook.getWorksheets().get(0);
```

¿Por qué comenzar con un libro de trabajo vacío? Garantiza que no haya estilos ocultos o pivotes anteriores que interfieran con la copia, dándote un resultado limpio listo para **export pivot table**.

## Step 5: Copy the Pivot Table (and Its Underlying Range)

Ahora el núcleo del tutorial: **copy pivot table**. Aspose.Cells trata la copia de un rango como una copia profunda, lo que significa que la caché de pivote viaja con las celdas. Por eso esta única línea realiza el trabajo pesado.

```java
// Copy the defined range (including the pivot) to the destination sheet at A1
sourceRange.copy(destinationSheet.getCells().createRange("A1"));
```

Si alguna vez te preguntaste **how to copy pivot** sin perder su funcionalidad, esta es la respuesta. La hoja de destino ahora contiene una tabla dinámica totalmente funcional que puedes actualizar, modificar o simplemente exportar.

### Edge Case: Preserving Refresh Settings

A veces la tabla dinámica fuente está configurada para actualizarse al abrir. Para mantener ese comportamiento, puedes copiar explícitamente las opciones de la tabla dinámica:

```java
// Optional: retain the original pivot's refresh settings
PivotTable srcPivot = sourceSheet.getPivotTables().get(0);
PivotTable destPivot = destinationSheet.getPivotTables().get(0);
destPivot.setRefreshOnFileOpen(srcPivot.isRefreshOnFileOpen());
```

Ese fragmento asegura que la tabla dinámica copiada se comporte exactamente como la original.

## Step 6: Save the Destination Workbook – **Export Pivot Table**

Finalmente, **export pivot table** guardando el nuevo libro de trabajo en disco. Puedes elegir cualquier formato que Aspose admita: XLSX, XLS, CSV, PDF, etc. Para esta guía nos quedaremos con XLSX.

```java
// Save the workbook that now contains the copied pivot
destinationWorkbook.save("YOUR_DIRECTORY/copied_with_pivot.xlsx", SaveFormat.XLSX);
```

Si necesitas enviar el archivo a través de un servicio web, puedes escribirlo en un `ByteArrayOutputStream` en lugar de una ruta de archivo—Aspose lo hace trivial.

## Full Working Example

Juntándolo todo, aquí tienes un programa completo, listo para ejecutar. Siéntete libre de copiar, pegar y ejecutarlo en tu IDE.

```java
import com.aspose.cells.*;

public class CopyPivotExample {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load the source workbook
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/source.xlsx");
        Worksheet sourceSheet = sourceWorkbook.getWorksheets().get(0);
        Range sourceRange = sourceSheet.getCells().createRange("A1:G20");

        // 2️⃣ Create a new workbook that will receive the copied range
        Workbook destinationWorkbook = new Workbook();
        Worksheet destinationSheet = destinationWorkbook.getWorksheets().get(0);

        // 3️⃣ Copy the range (pivot table included) to the destination sheet
        sourceRange.copy(destinationSheet.getCells().createRange("A1"));

        // Optional: Preserve refresh settings if needed
        if (!sourceSheet.getPivotTables().isEmpty()) {
            PivotTable srcPivot = sourceSheet.getPivotTables().get(0);
            PivotTable destPivot = destinationSheet.getPivotTables().get(0);
            destPivot.setRefreshOnFileOpen(srcPivot.isRefreshOnFileOpen());
        }

        // 4️⃣ Save the result – this effectively **export pivot table**
        destinationWorkbook.save("YOUR_DIRECTORY/copied_with_pivot.xlsx", SaveFormat.XLSX);

        System.out.println("Pivot table copied successfully!");
    }
}
```

### Expected Output

Al ejecutar el programa, la consola muestra:

```
Pivot table copied successfully!
```

Y el archivo `copied_with_pivot.xlsx` aparece en `YOUR_DIRECTORY`. Ábrelo en Excel y verás la tabla dinámica intacta, lista para actualizarse o editarse.

## Common Questions & Troubleshooting

- **¿Qué pasa si la tabla dinámica fuente abarca más de una hoja?**  
  Necesitarás copiar cada rango relevante por separado, y luego recrear la tabla dinámica en la hoja de destino usando las APIs `PivotTable`.

- **¿Puedo copiar solo el diseño de la tabla dinámica sin los datos?**  
  Configura `sourceRange.setCopyDataOnly(false)` antes de la copia. Esto indica a Aspose que mantenga la caché pero no los datos subyacentes.

- **¿Hay una forma de copiar la tabla dinámica a un archivo CSV?**  
  CSV no admite tablas dinámicas, pero puedes exportar el *resultado* de la tabla dinámica llamando a `pivotTable.calculate()` y luego guardando la hoja como CSV.

- **¿Por qué la tabla dinámica copiada pierde su formato?**  
  El formato reside en la colección de estilos. Después de copiar, puedes llamar a `destinationSheet.getCells().applyStyle(sourceSheet.getCells().getStyle())` para transferir los estilos.

## Conclusion

Acabamos de mostrarte cómo **create new workbook** en Java, **copy pivot table**, y **export pivot table**—todo con un ejemplo de código limpio y reproducible. Definiendo el **copy excel range** exacto, aprovechando la semántica de copia profunda de Aspose.Cells y preservando configuraciones opcionales, puedes automatizar prácticamente cualquier tarea de migración de tablas dinámicas.

¿Listo para el siguiente paso? Prueba cambiar el formato de salida a PDF, o recorre varios archivos fuente para procesar en lote decenas de tablas dinámicas. El mismo patrón se aplica—solo ajusta las rutas de archivo y las direcciones de rango.

Si encuentras algún problema, deja un comentario abajo o consulta la documentación de Aspose.Cells para manipulación avanzada de tablas dinámicas. ¡Feliz codificación, y disfruta del tiempo que ahorraste al automatizar esas tediosas tareas de copiar‑pegar!

## What Should You Learn Next?

Los siguientes tutoriales cubren temas estrechamente relacionados que se basan en las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y funcionales con explicaciones paso a paso para ayudarte a dominar características adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [How to Create Pivot Tables in Excel Using Aspose.Cells for Java: A Comprehensive Guide](/cells/english/java/data-analysis/create-pivot-tables-excel-aspose-cells-java/)
- [How to Update Excel Pivot Table Source with Aspose.Cells for Java: A Comprehensive Guide](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [How to Create and Export Excel to HTML Using Aspose.Cells Java | Workbook Operations Guide](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}