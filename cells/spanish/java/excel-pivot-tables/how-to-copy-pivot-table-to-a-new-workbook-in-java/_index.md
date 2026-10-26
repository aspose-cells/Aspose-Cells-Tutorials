---
category: general
date: 2026-10-26
description: Aprende a copiar una tabla dinámica a un nuevo libro de trabajo usando
  Java, preservando el formato y la definición de la tabla dinámica mientras copias
  un rango de Excel con formato mediante Aspose.Cells.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy pivot table
- how to copy pivot
- copy excel range
- create empty workbook
- copy range with formatting
language: es
lastmod: 2026-10-26
og_description: Copiar tabla dinámica a un nuevo libro de trabajo en Java con Aspose.Cells.
  Esta guía muestra cómo copiar un rango de Excel, conservar el formato y crear un
  libro de trabajo vacío de manera eficiente.
og_image_alt: Screenshot of a Java program that copies a pivot table to a new Excel
  workbook
og_title: Copiar tabla dinámica a un nuevo libro de trabajo en Java – guía paso a
  paso
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Learn how to copy pivot table to a new workbook using Java, preserving
    formatting and the pivot definition while you copy excel range with formatting
    via Aspose.Cells.
  headline: How to copy pivot table to a new workbook in Java
  type: TechArticle
- description: Learn how to copy pivot table to a new workbook using Java, preserving
    formatting and the pivot definition while you copy excel range with formatting
    via Aspose.Cells.
  name: How to copy pivot table to a new workbook in Java
  steps:
  - name: Prerequisites
    text: '* Java 17 or later. * Aspose.Cells for Java (version 23.10 or newer). *
      Basic familiarity with Java IDEs (IntelliJ IDEA, Eclipse, etc.).'
  - name: Why this works
    text: '* `new Workbook()` **creates empty workbook** with a default sheet, avoiding
      the need to delete existing data. * `CopyOptions` tells Aspose.Cells to copy
      **pivot table** metadata, not just raw values. The `PASTE_ALL` mode also carries
      cell styles, number formats, and conditional formatting—fulfillin'
  - name: Edge cases to consider
    text: '| Situation | Recommended handling | |----------------------------------------|----------------------|
      | Source workbook has multiple pivots | Copy each pivot’s range separately or
      copy the whole sheet. | | Destination already contains data | Choose a non‑conflicting
      start cell (e.g., "H1") when cal'
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: Cómo copiar una tabla dinámica a un nuevo libro de trabajo en Java
url: /es/java/excel-pivot-tables/how-to-copy-pivot-table-to-a-new-workbook-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo copiar una tabla dinámica a un nuevo libro de trabajo en Java

Si necesitas **copy pivot table** de un archivo Excel a otro, esta guía te muestra una solución completa y ejecutable. Verás cómo preservar la definición de la tabla dinámica, mantener todo el formato y evitar problemas comunes al copiar un rango de Excel.

Copiar una tabla dinámica a menudo genera preguntas como *how to copy pivot* sin romper la fuente de datos o perder estilos. Al final de este tutorial tendrás un programa Java autocontenido que crea un libro de trabajo vacío, copia el rango deseado y guarda el resultado con la tabla dinámica intacta.

## Lo que lograrás

* Cargar un libro de trabajo fuente que contiene una tabla dinámica.  
* **Create empty workbook** que recibirá los datos copiados.  
* **Copy excel range** que incluye la tabla dinámica, usando opciones que mantienen la tabla dinámica y el formato.  
* Guardar el archivo de destino y verificar que la tabla dinámica funciona exactamente como la original.

### Requisitos previos

* Java 17 o posterior.  
* Aspose.Cells for Java (versión 23.10 o más reciente).  
* Familiaridad básica con IDEs de Java (IntelliJ IDEA, Eclipse, etc.).  

> **Consejo profesional:** Usa la licencia de evaluación gratuita de Aspose.Cells para pruebas rápidas; reemplázala con una licencia completa antes de usar en producción.

## Copiar tabla dinámica a un nuevo libro de trabajo

El primer paso es configurar los libros de trabajo fuente y de destino. El destino comienza con una llamada **create empty workbook**, lo que te brinda un archivo limpio con una sola hoja de cálculo.

```java
import com.aspose.cells.*;

public class CopyPivotExample {
    public static void main(String[] args) throws Exception {
        // Load the source workbook that holds the pivot table
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/source.xlsx");

        // Create an empty workbook that will receive the copied range
        Workbook destWb = new Workbook();

        // Get the first worksheet from each workbook
        Worksheet srcSheet = srcWb.getWorksheets().get(0);
        Worksheet destSheet = destWb.getWorksheets().get(0);

        // Configure copy options to preserve the pivot table and formatting
        CopyOptions copyOptions = new CopyOptions();
        copyOptions.setPasteType(PasteType.PASTE_ALL); // ensures pivot and styles are kept

        // Copy the range that contains the pivot table
        srcSheet.getCells().copyRange("A1:D20", destSheet.getCells(), "A1", copyOptions);

        // Save the destination workbook
        destWb.save("YOUR_DIRECTORY/destination.xlsx");
    }
}
```

### Por qué funciona esto

* `new Workbook()` **creates empty workbook** con una hoja predeterminada, evitando la necesidad de eliminar datos existentes.  
* `CopyOptions` indica a Aspose.Cells que copie los metadatos de **pivot table**, no solo los valores sin procesar. El modo `PASTE_ALL` también transporta estilos de celda, formatos numéricos y formato condicional, cumpliendo con el requisito de **copy range with formatting**.  
* `copyRange` realiza una operación de **copy excel range** que respeta las estructuras internas de la fuente, por lo que la tabla dinámica sigue funcional después de la copia.

## Cómo copiar una tabla dinámica sin perder el formato

Si solo utilizas el `CopyOptions` predeterminado, alguna información de estilo puede omitirse en versiones antiguas de Aspose.Cells. Configurar explícitamente el tipo de pegado garantiza que se respete **copy range with formatting**.

```java
CopyOptions copyOptions = new CopyOptions();
copyOptions.setPasteType(PasteType.PASTE_ALL);          // copy values, formulas, formats
copyOptions.setPasteSpecialType(PasteSpecialType.ALL); // include column widths and row heights
```

Agregar `setPasteSpecialType` asegura que los anchos de columna, alturas de fila e incluso las reglas de validación de datos viajen con el rango. Esto es especialmente útil cuando la tabla dinámica abarca varias columnas con anchos personalizados.

## Crear un libro de trabajo vacío antes de copiar

A veces los desarrolladores intentan copiar en un libro de trabajo existente que ya contiene datos. Eso puede causar rangos superpuestos o sobrescrituras inesperadas. Comenzar con una llamada **create empty workbook** aísla la operación:

```java
Workbook destWb = new Workbook(); // fresh file with one sheet
Worksheet destSheet = destWb.getWorksheets().get(0); // reference the clean sheet
```

Si necesitas más de una hoja en el destino, puedes agregarlas después de la copia:

```java
destWb.getWorksheets().add("Summary");
```

## Copiar rango de Excel con formato usando CopyOptions

Más allá de las tablas dinámicas, el mismo patrón funciona para cualquier **copy excel range** que requiera preservación de formato—gráficos, tablas o formatos condicionales.

```java
// Example: copy a styled table from A1 to G15
srcSheet.getCells().copyRange("A1:G15", destSheet.getCells(), "A1", copyOptions);
```

La instancia de `CopyOptions` permanece igual, por lo que obtienes un comportamiento consistente en diferentes rangos.

### Casos límite a considerar

| Situación                              | Manejo recomendado |
|----------------------------------------|----------------------|
| El libro de trabajo fuente tiene múltiples tablas dinámicas   | Copy each pivot’s range separately or copy the whole sheet. |
| El destino ya contiene datos      | Choose a non‑conflicting start cell (e.g., "H1") when calling `copyRange`. |
| La fuente de datos de la tabla dinámica es externa (p.ej., BD) | Ensure the destination workbook points to the same external data source, or refresh the pivot after copy. |
| Libro de trabajo grande ( > 10 MB )             | Increase Java heap size (`-Xmx2g`) to avoid `OutOfMemoryError`. |

## Verificar el resultado

Después de ejecutar el programa, abre `destination.xlsx`. Deberías ver:

* El mismo diseño de tabla dinámica que en `source.xlsx`.  
* Todos los colores de celda, formatos numéricos y anchos de columna preservados.  
* La fuente de datos de la tabla dinámica sigue apuntando al rango de datos original dentro del nuevo archivo, por lo que actualizar la tabla dinámica actualiza los valores correctamente.

Si la tabla dinámica aparece como una tabla estática, verifica que `CopyOptions.setPasteType(PasteType.PASTE_ALL)` esté configurado. Sin esta opción Aspose.Cells trata la tabla dinámica como datos simples.

## Conclusión

Ahora sabes cómo **copy pivot table** a un nuevo libro de trabajo en Java mientras preservas el formato, las conexiones de datos y el diseño de la hoja. La solución completa muestra cómo cargar un archivo fuente, **create empty workbook**, configurar opciones de **copy excel range**, y guardar el resultado.  

Desde aquí puedes explorar temas relacionados como **how to copy pivot** entre diferentes hojas de cálculo, incrustar gráficos junto a tablas dinámicas, o automatizar el procesamiento por lotes de varios libros de trabajo. Experimenta con la configuración de `CopyOptions` para adaptarla a tus necesidades específicas de automatización, y tendrás un robusto conjunto de herramientas para manipular Excel al alcance de tu mano.

## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que se basan en las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y funcionales con explicaciones paso a paso para ayudarte a dominar características adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Crear nuevo libro de trabajo en Java – Guía completa para copiar tabla dinámica](/cells/english/java/excel-pivot-tables/create-new-workbook-in-java-full-guide-to-copy-pivot-table/)
- [Copiar tabla dinámica entre libros de trabajo – Guía paso a paso en Java](/cells/english/java/excel-pivot-tables/copy-pivot-table-between-workbooks-step-by-step-java-guide/)
- [Cómo copiar rango y preservar una tabla dinámica en Java](/cells/english/java/excel-pivot-tables/how-to-copy-range-and-preserve-a-pivot-table-in-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}