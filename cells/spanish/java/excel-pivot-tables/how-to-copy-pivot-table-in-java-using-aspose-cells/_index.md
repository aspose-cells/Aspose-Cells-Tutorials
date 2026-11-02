---
category: general
date: 2026-07-06
description: Cómo copiar una tabla dinámica en Java con Aspose.Cells – guía paso a
  paso para duplicar tablas dinámicas de Excel programáticamente.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy pivot
- duplicate excel pivot
language: es
lastmod: 2026-07-06
og_description: Cómo copiar una tabla dinámica en Java usando Aspose.Cells le permite
  duplicar tablas dinámicas de Excel de forma rápida y fiable.
og_image_alt: Screenshot of Java code copying an Excel pivot table with Aspose.Cells
og_title: Cómo copiar una tabla dinámica en Java – Guía completa de Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-07-06'
  description: How to copy pivot table in Java with Aspose.Cells – step‑by‑step guide
    to duplicate Excel pivot tables programmatically.
  headline: How to copy pivot table in Java using Aspose.Cells
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel
- Pivot Table
title: Cómo copiar una tabla dinámica en Java usando Aspose.Cells
url: /es/java/excel-pivot-tables/how-to-copy-pivot-table-in-java-using-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo copiar una tabla dinámica en Java usando Aspose.Cells

¿Alguna vez te has preguntado **cómo copiar tablas dinámicas** dentro de un archivo Excel sin abrir el libro manualmente? No eres el único. En muchos flujos de informes necesitas **duplicar tablas dinámicas de Excel** al vuelo—quizás para crear una instantánea, moverla a una nueva hoja o generar una plantilla para usuarios posteriores.

En este tutorial recorreremos un ejemplo completo y ejecutable que muestra exactamente eso. Usando la biblioteca Aspose.Cells for Java cargaremos un libro, localizaremos el rango de la tabla dinámica origen, lo copiaremos a una nueva ubicación y guardaremos el resultado. Sin referencias vagas, solo una solución concreta que puedes incorporar a tu proyecto hoy.

---

## Requisitos previos

* **Java Development Kit (JDK) 8+** – el código se compila con cualquier JDK reciente.
* **Aspose.Cells for Java** versión 25.11 o más reciente – el método `Range.copy` que soporta tablas dinámicas se introdujo en esta versión.
* Un archivo **input.xlsx** que ya contiene una tabla dinámica (puedes crear una en Excel para probar).
* Una herramienta de compilación de tu elección (Maven, Gradle o simple `javac`). Mostraremos la dependencia de Maven para un inicio rápido.

```xml
<!-- Add this to your pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.12</version> <!-- Use the latest stable -->
</dependency>
```

---

## Paso 1: Cargar el libro de origen

Lo primero que hacemos es abrir el archivo Excel que contiene la tabla dinámica original. Aspose.Cells trata el libro como un objeto en memoria, por lo que puedes manipularlo sin lanzar Excel.

```java
// Load the workbook from disk
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

> **Por qué es importante:** Cargar el libro nos da acceso a las hojas de cálculo, celdas y, crucialmente, a la caché de la tabla dinámica que la respalda. Sin este paso la biblioteca no tiene nada que copiar.

---

## Paso 2: Obtener la hoja que contiene la tabla dinámica

Si tu libro tiene varias hojas, necesitas apuntar a la correcta. Aquí simplemente obtenemos la primera hoja, pero también puedes usar `get("SheetName")` para buscar por nombre.

```java
// Obtain the first worksheet (index 0)
Worksheet worksheet = workbook.getWorksheets().get(0);
```

> **Consejo profesional:** Cuando trabajas con muchas hojas, almacena el índice o nombre en un archivo de configuración para evitar codificar números directamente.

---

## Paso 3: Definir el rango de origen que incluye la tabla dinámica

A partir de la versión 25.11 Aspose.Cells permite tratar una tabla dinámica como un rango de celdas normal. Especifica las celdas superior‑izquierda e inferior‑derecha que encierran toda la tabla dinámica.

```java
// The range A1:D20 covers the whole pivot table in this example
Range sourceRange = worksheet.getCells().createRange("A1:D20");
```

> **Caso límite:** Si tu tabla dinámica se expande dinámicamente (p. ej., se añaden filas después), considera usar `worksheet.getPivotTables().get(0).getDataRange()` para obtener el rango exacto de forma programática.

---

## Paso 4: Definir el rango de destino donde se copiará la tabla dinámica

Elige cualquier celda vacía donde quieras que aparezca la tabla dinámica duplicada. En esta demostración empezamos en **F1**, dejando un espacio entre el original y la copia.

```java
// Destination starts at cell F1 – adjust as needed
Range destinationRange = worksheet.getCells().createRange("F1");
```

> **¿Por qué no una hoja nueva?** También puedes crear una hoja nueva (`workbook.getWorksheets().add("Copy")`) y usar sus celdas como destino. El mismo método `copy` funciona entre hojas.

---

## Paso 5: Copiar la tabla dinámica a la nueva ubicación

Ahora ocurre la magia. El método `copy` clona la tabla dinámica, su caché, formato e incluso cualquier segmentador asociado (a partir de la última versión).

```java
// Perform the copy – the pivot is now duplicated at the destination
sourceRange.copy(destinationRange);
```

> **Importante:** La operación de copia es *profunda*; **no** crea una referencia al pivote original. Puedes modificar la nueva tabla dinámica de forma independiente sin afectar la fuente.

---

## Paso 6: Guardar el libro con la tabla dinámica duplicada

Finalmente, escribe el libro modificado de nuevo en disco. Puedes sobrescribir el original o crear un nuevo archivo; aquí elegimos lo último para mantener la fuente intacta.

```java
// Save the workbook – the duplicated pivot lives in output.xlsx
workbook.save("YOUR_DIRECTORY/output.xlsx");
```

Cuando abras **output.xlsx** en Excel, verás la tabla dinámica original en las columnas A‑D y una copia perfecta que comienza en la columna F. Ambas tablas dinámicas pueden actualizarse por separado.

---

## Ejemplo completo de trabajo

Juntando todo, aquí tienes la clase Java completa que puedes compilar y ejecutar directamente:

```java
import com.aspose.cells.*;

public class ExportPivotTableExample {
    public static void main(String[] args) throws Exception {
        // Step 1: Load the source workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // Step 2: Get the worksheet that contains the pivot table
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // Step 3: Define the source range that includes the pivot table (supported from version 25.11)
        // Adjust the range to match your actual pivot dimensions
        Range sourceRange = worksheet.getCells().createRange("A1:D20");

        // Step 4: Define the destination range where the pivot table will be copied
        // Change "F1" to any starting cell you prefer
        Range destinationRange = worksheet.getCells().createRange("F1");

        // Step 5: Copy the pivot table to the new location
        sourceRange.copy(destinationRange);

        // Step 6: Save the workbook with the copied pivot table
        workbook.save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

**Resultado esperado:** Al abrir `output.xlsx` se muestra la tabla dinámica original (A1:D20) y una tabla idéntica que comienza en F1. Ambas tablas conservan sus filtros, estilos y campos calculados.

---

## Manejo de variaciones comunes

| Situación | Qué ajustar |
|-----------|-------------|
| **Múltiples tablas dinámicas** en la misma hoja | Recorre `worksheet.getPivotTables()` y copia cada una con su propio rango de destino. |
| **Rango de datos dinámico** | Usa `worksheet.getPivotTables().get(0).getDataRange()` para detectar automáticamente el área de origen. |
| **Copiar a otro libro** | Carga una segunda instancia de `Workbook`, crea una hoja de destino, luego llama a `sourceRange.copy(destWorksheet.getCells().createRange("A1"))`. |
| **Preservar segmentadores** | A partir de la 25.12, los segmentadores se copian automáticamente cuando el rango los incluye. Verifica en Excel después de guardar. |

---

## Consejos profesionales y trampas

* **Comprobación de versión:** El método `copy` que soporta tablas dinámicas se añadió en **Aspose.Cells 25.11**. Si usas una versión anterior obtendrás una excepción. Siempre verifica la versión de `aspose-cells` en tu `pom.xml`.
* **Rendimiento:** Copiar tablas dinámicas grandes puede consumir mucha memoria. Si solo necesitas los datos, considera exportar la tabla dinámica a una tabla plana en lugar de clonar todo el objeto.
* **Comportamiento de actualización:** La tabla dinámica duplicada conserva su propia caché. Si modificas los datos subyacentes, llama a `pivotTable.refresh()` en la nueva tabla para recalcular.
* **Detalles de formato:** Algunos formatos numéricos personalizados pueden no sobrevivir la copia en versiones muy antiguas de Excel (<2007). Prueba con la versión de Excel de tu público objetivo.

---

## Conclusión

Ahora tienes una respuesta sólida y completa a **cómo copiar tablas dinámicas** usando Aspose.Cells for Java, y has visto cómo **duplicar tablas dinámicas de Excel** en unas pocas líneas de código. El enfoque funciona para una o varias tablas dinámicas, entre hojas de cálculo e incluso entre libros.

Los siguientes pasos podrían incluir:

* Automatizar la copia de cada tabla dinámica en un trabajo por lotes.
* Añadir código para renombrar la tabla dinámica duplicada (p. ej., `pivotTable.setName("Copy_of_Sales")`).
* Integrar la rutina en un servicio de informes más amplio que genere PDFs o exportaciones CSV.

¡Pruébalo, ajusta los rangos para que coincidan con tus datos reales y deja que la biblioteca haga el trabajo pesado. ¡Feliz codificación!

## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que se basan en las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y funcionales con explicaciones paso a paso para ayudarte a dominar funciones adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Cómo crear tablas dinámicas en Excel usando Aspose.Cells para Java: Guía completa](/cells/english/java/data-analysis/create-pivot-tables-excel-aspose-cells-java/)
- [Manipulación de tablas dinámicas de Excel con Aspose.Cells Java: Guía completa](/cells/english/java/data-analysis/excel-pivot-table-manipulation-aspose-cells-java/)
- [Cómo actualizar la fuente de una tabla dinámica de Excel con Aspose.Cells para Java: Guía completa](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}