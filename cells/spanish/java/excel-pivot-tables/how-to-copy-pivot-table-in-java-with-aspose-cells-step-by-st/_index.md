---
category: general
date: 2026-10-20
description: Aprende cómo copiar una tabla dinámica usando Aspose.Cells en Java. Este
  tutorial muestra cómo copiar un rango a una nueva hoja y duplicar la hoja de la
  tabla dinámica de forma segura.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy pivot table
- copy range to new sheet
- duplicate pivot table sheet
language: es
lastmod: 2026-10-20
og_description: Cómo copiar una tabla dinámica con Aspose.Cells en Java. Sigue esta
  guía para copiar el rango a una nueva hoja y duplicar la hoja de la tabla dinámica
  sin perder datos.
og_image_alt: Screenshot showing how to copy pivot table from one worksheet to another
  in a Java program
og_title: Cómo copiar una tabla dinámica en Java – tutorial completo de Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-10-20'
  description: Learn how to copy pivot table using Aspose.Cells in Java. This tutorial
    shows how to copy range to new sheet and duplicate pivot table sheet safely.
  headline: How to copy pivot table in Java with Aspose.Cells – step‑by‑step guide
  type: TechArticle
- description: Learn how to copy pivot table using Aspose.Cells in Java. This tutorial
    shows how to copy range to new sheet and duplicate pivot table sheet safely.
  name: How to copy pivot table in Java with Aspose.Cells – step‑by‑step guide
  steps:
  - name: Load the workbook that holds the original pivot table.
    text: Load the workbook that holds the original pivot table.
  - name: Identify the exact range that includes the pivot table.
    text: Identify the exact range that includes the pivot table.
  - name: Create a new worksheet that will receive the copied data.
    text: Create a new worksheet that will receive the copied data.
  - name: Use the `Range.copy` method to transfer the range to the new sheet.
    text: Use the `Range.copy` method to transfer the range to the new sheet.
  - name: Save the workbook to a new file.
    text: Save the workbook to a new file.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: Cómo copiar una tabla dinámica en Java con Aspose.Cells – guía paso a paso
url: /es/java/excel-pivot-tables/how-to-copy-pivot-table-in-java-with-aspose-cells-step-by-st/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo copiar una tabla dinámica en Java con Aspose.Cells – guía paso a paso

Si necesitas **how to copy pivot table** en una aplicación Java, esta guía te muestra los pasos exactos. Ya sea que estés construyendo un motor de informes o automatizando la migración de datos, verás cómo copiar un rango a una nueva hoja manteniendo la definición y los datos de la tabla dinámica.

Copiar una tabla dinámica puede parecer arriesgado porque la caché subyacente y la configuración de los campos a menudo se pierden. Este tutorial demuestra un enfoque fiable usando Aspose.Cells, muestra el código completo ejecutable y explica por qué cada línea es importante. Al final, podrás duplicar la hoja de tabla dinámica en segundos.

## Requisitos previos

* Java 8 o una versión más reciente instalada.
* Aspose.Cells for Java (versión 23.10 o posterior) añadido al classpath de tu proyecto.
* Un libro de trabajo fuente (`source.xlsx`) que contiene una tabla dinámica en el rango `A1:G20`.
* Familiaridad básica con conceptos de Java y Excel.

No se requieren bibliotecas adicionales; Aspose.Cells maneja todas las operaciones de Excel internamente.

## Cómo copiar una tabla dinámica – estrategia general

La idea principal es simple:

1. Cargar el libro de trabajo que contiene la tabla dinámica original.
2. Identificar el rango exacto que incluye la tabla dinámica.
3. Crear una nueva hoja de cálculo que recibirá los datos copiados.
4. Usar el método `Range.copy` para transferir el rango a la nueva hoja.  
   Este método copia automáticamente la caché de la tabla dinámica, por lo que la tabla dinámica sigue funcionando.
5. Guardar el libro de trabajo en un nuevo archivo.

Debido a que la operación de copia funciona a nivel de rango, la **duplicate pivot table sheet** conserva todas las configuraciones de campos, filtros y elementos calculados.

## Paso 1: Cargar el libro de trabajo fuente

```java
// Import Aspose.Cells classes
import com.aspose.cells.*;

public class PivotCopyDemo {
    public static void main(String[] args) throws Exception {
        // Load the source workbook that contains the pivot table
        Workbook workbook = new Workbook("YOUR_DIRECTORY/source.xlsx");
```

*Por qué esto es importante*: Cargar el libro de trabajo te da acceso a sus hojas, celdas y a la caché de la tabla dinámica. Aspose.Cells lee todo el archivo en memoria, por lo que las operaciones posteriores son rápidas y seguras para subprocesos.

## Paso 2: Definir el rango fuente que contiene la tabla dinámica

```java
        // Locate the first worksheet (index 0) and create a range covering the pivot table
        Range sourceRange = workbook.getWorksheets()
                                    .get(0)               // first sheet
                                    .getCells()
                                    .createRange("A1:G20"); // adjust if your pivot table is larger
```

*Por qué esto es importante*: La llamada `createRange` indica a Aspose.Cells exactamente qué celdas copiar. Incluir toda el área de la tabla dinámica asegura que también se transfieran las filas ocultas de la caché. Si omites alguna parte de la caché, la tabla dinámica copiada aparecerá vacía.

## Paso 3: Añadir una hoja de cálculo de destino para los datos copiados

```java
        // Add a new worksheet that will hold the duplicated pivot table
        Worksheet destinationSheet = workbook.getWorksheets().add("CopyResult");
```

*Por qué esto es importante*: Añadir una hoja dedicada aísla la tabla dinámica copiada de la original, facilitando la comparación de resultados o el uso de la hoja como plantilla para procesamiento adicional.

## Paso 4: Copiar el rango a la hoja de cálculo de destino (la tabla dinámica se conserva)

```java
        // Copy the defined range to cell A1 of the new worksheet
        sourceRange.copy(destinationSheet.getCells().createRange("A1"));
```

*Por qué esto es importante*: El método `copy` no solo copia valores y formato de celdas, sino que también replica la caché de la tabla dinámica. Este es el paso clave que te permite **duplicate pivot table sheet** sin perder ninguna funcionalidad.

## Paso 5: Guardar el libro de trabajo con el rango copiado

```java
        // Persist the workbook to a new file
        workbook.save("YOUR_DIRECTORY/result.xlsx");
    }
}
```

*Por qué esto es importante*: Guardar crea un nuevo archivo Excel (`result.xlsx`) que contiene tanto la original como la hoja de tabla dinámica duplicada. Ahora puedes abrir el archivo en Excel para verificar que la tabla dinámica funciona exactamente como antes.

## Ejemplo completo y ejecutable

Juntando todo, aquí tienes el programa completo que puedes copiar y pegar en tu IDE:

```java
import com.aspose.cells.*;

public class PivotCopyDemo {
    public static void main(String[] args) throws Exception {
        // 1. Load the source workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/source.xlsx");

        // 2. Define the source range that contains the pivot table
        Range sourceRange = workbook.getWorksheets()
                                    .get(0)
                                    .getCells()
                                    .createRange("A1:G20");

        // 3. Add a destination worksheet for the copied data
        Worksheet destinationSheet = workbook.getWorksheets().add("CopyResult");

        // 4. Copy the range to the destination worksheet (pivot table is preserved)
        sourceRange.copy(destinationSheet.getCells().createRange("A1"));

        // 5. Save the workbook with the copied range
        workbook.save("YOUR_DIRECTORY/result.xlsx");
    }
}
```

### Resultado esperado

* Abrir `result.xlsx` muestra dos hojas de cálculo:
  * **Sheet1** – los datos originales y la tabla dinámica.
  * **CopyResult** – una duplicación exacta de la tabla dinámica, totalmente funcional.
* Todos los campos de la tabla dinámica, filtros y elementos calculados se comportan idénticamente al origen.

Si modificas la tabla dinámica fuente después de la copia, la hoja duplicada **no** reflejará esos cambios porque la caché se duplicó en el momento de la copia. Este aislamiento suele ser deseable cuando necesitas una instantánea del informe.

## Errores comunes y cómo evitarlos

| Issue | Why it happens | Fix |
|-------|----------------|-----|
| **La tabla dinámica aparece en blanco** | El rango copiado omitió las filas ocultas de la caché. | Asegúrate de que el rango incluya toda la caché (normalmente algunas filas debajo de la tabla visible). |
| **El nombre de la hoja de destino ya existe** | `add("CopyResult")` lanza una excepción si el nombre ya está en uso. | Usa `workbook.getWorksheets().addUniqueName("CopyResult")` o verifica `contains` antes de añadir. |
| **Errores de ruta de archivo** | `YOUR_DIRECTORY` incorrecto provoca `FileNotFoundException`. | Utiliza rutas absolutas o `Paths.get(...).toAbsolutePath()` de Java para resolver ubicaciones. |
| **Ralentización del rendimiento en libros grandes** | Copiar rangos masivos copia celdas innecesarias. | Limita el rango al área exacta de la tabla dinámica, o usa `Range.copy` con `CopyOptions` para omitir el formato si no es necesario. |

## Consejo profesional: Usar `CopyOptions` para un control más fino

Si solo necesitas los datos de la tabla dinámica y deseas omitir el formato de celdas, puedes pasar un objeto `CopyOptions`:

```java
CopyOptions options = new CopyOptions();
options.setCopyStyle(false);        // skip styles
options.setCopyMerged(true);        // keep merged cells
sourceRange.copy(destinationSheet.getCells().createRange("A1"), options);
```

Esto reduce el tamaño del archivo de la hoja duplicada y acelera la operación de copia, especialmente en libros de trabajo grandes.

## Cómo copiar un rango a una nueva hoja sin perder fórmulas

El ejemplo anterior ya copia fórmulas porque `Range.copy` las conserva por defecto. Si solo deseas valores (p.ej., para congelar el estado actual), establece `options.setPasteType(PasteType.VALUES)`.

```java
CopyOptions opt = new CopyOptions();
opt.setPasteType(PasteType.VALUES);
sourceRange.copy(destinationSheet.getCells().createRange("A1"), opt);
```

Ahora la hoja de destino contiene valores estáticos, pero la tabla dinámica seguirá funcionando porque su caché forma parte del rango.

## Resumen de la solución

* **How to copy pivot table** – cargar el libro de trabajo, definir el rango exacto, añadir una nueva hoja de cálculo, copiar el rango y guardar.
* El proceso también demuestra **copy range to new sheet** y cómo **duplicate pivot table sheet** de forma segura.
* Puedes afinar la copia con `CopyOptions` para escenarios de rendimiento o solo valores.

## Próximos pasos y temas relacionados

* **Refresh pivot cache programmatically** – usa `PivotTable.refreshData()` después de actualizar los datos de origen.
* **Export pivot table to PDF** – combina esta técnica de copia con `PdfSaveOptions` para crear informes instantáneos.
* **Automate multi‑sheet duplication** – recorre todas las hojas de cálculo y aplica la misma lógica de copia.

Experimenta con estas variaciones para adaptar el patrón a tu canal de informes específico. Si encuentras casos límite, como fuentes de datos externas o tablas dinámicas impulsadas por VBA, el mismo enfoque de copia de rango funciona, pero puede que necesites copiar también los objetos de conexión subyacentes.

---

*¡Feliz codificación! Si este tutorial te ayudó a aprender **how to copy pivot table**, siéntete libre de compartirlo con tus compañeros o contribuir con mejoras.*

## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y funcionales con explicaciones paso a paso para ayudarte a dominar funciones adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Cómo copiar rango y preservar una tabla dinámica en Java](/cells/english/java/excel-pivot-tables/how-to-copy-range-and-preserve-a-pivot-table-in-java/)
- [Crear nuevo libro de trabajo en Java – Guía completa para copiar tabla dinámica](/cells/english/java/excel-pivot-tables/create-new-workbook-in-java-full-guide-to-copy-pivot-table/)
- [Copiar tabla dinámica entre libros de trabajo – Guía paso a paso en Java](/cells/english/java/excel-pivot-tables/copy-pivot-table-between-workbooks-step-by-step-java-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}