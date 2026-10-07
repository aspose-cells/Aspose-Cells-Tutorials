---
category: general
date: 2026-10-07
description: Aprende a duplicar tablas dinámicas en Excel usando Java y Aspose.Cells.
  Copia una tabla dinámica copiando su rango entre libros de trabajo rápidamente.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to duplicate pivot
- copy pivot table
- copy excel range
- copy range between workbooks
- how to copy pivot table
language: es
lastmod: 2026-10-07
og_description: Cómo duplicar tablas dinámicas en Excel usando Java y Aspose.Cells.
  Sigue esta guía para copiar una tabla dinámica copiando su rango entre libros de
  trabajo.
og_image_alt: Illustration of copying an Excel pivot table from one workbook to another
og_title: Cómo duplicar tablas dinámicas en Excel con Java – tutorial completo
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: Learn how to duplicate pivot tables in Excel using Java and Aspose.Cells.
    Copy a pivot table by copying its range between workbooks quickly.
  headline: How to duplicate pivot tables in Excel with Java – step‑by‑step guide
  type: TechArticle
- description: Learn how to duplicate pivot tables in Excel using Java and Aspose.Cells.
    Copy a pivot table by copying its range between workbooks quickly.
  name: How to duplicate pivot tables in Excel with Java – step‑by‑step guide
  steps:
  - name: Explanation of each step
    text: '| Step | What the code does | Why it matters for **copy pivot table** |
      |------|-------------------|----------------------------------------| | **1️⃣
      Load source workbook** | `new Workbook(srcPath)` reads `Source.xlsx`. | The
      source file is the only place where the original pivot exists. | | **2️⃣ D'
  - name: 1️⃣ Copying a pivot that spans multiple sheets
    text: 'If the pivot’s source data lives on a different sheet than the pivot itself,
      include both sheets in the copy operation. The simplest approach is to copy
      the entire source sheet first, then copy the pivot sheet:'
  - name: 2️⃣ Dealing with named ranges
    text: 'Aspose.Cells preserves named ranges when you copy a range. However, if
      the destination workbook already contains a name with the same identifier, a
      `CellsException` is thrown. Resolve this by renaming the conflicting name before
      the copy:'
  - name: 3️⃣ Large workbooks and performance
    text: 'Copying very large ranges (hundreds of thousands of rows) can be memory‑intensive.
      Enable **memory optimization**:'
  - name: 4️⃣ Keeping formulas intact
    text: If the source range contains formulas that reference cells outside the copied
      area, those references become broken after the copy. To avoid this, expand the
      range to include all dependent cells, or use `copyRange` with the `CopyOptions`
      flag `CopyOptions.COPY_FORMULA`.
  type: HowTo
tags:
- Excel
- Java
- Aspose.Cells
- PivotTable
- Data manipulation
title: Cómo duplicar tablas dinámicas en Excel con Java – guía paso a paso
url: /es/java/excel-pivot-tables/how-to-duplicate-pivot-tables-in-excel-with-java-step-by-ste/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo duplicar tablas dinámicas en Excel con Java – guía paso a paso

Si necesita **cómo duplicar tabla dinámica** en un libro de Excel, este tutorial le muestra una solución completa y lista para ejecutar. Usando Aspose.Cells para Java puede copiar una tabla dinámica junto con sus datos de origen copiando el rango subyacente y luego guardando el resultado como un nuevo libro.

Duplicar una tabla dinámica a menudo parece complicado porque la caché de la tabla dinámica está oculta dentro de la hoja. Al copiar todo el rango que contiene la tabla dinámica, Aspose.Cells recrea automáticamente la caché en el libro de destino, de modo que obtiene una copia totalmente funcional sin manipular XML manualmente.

En esta guía usted:

* Cargará un libro de origen que contiene una tabla dinámica.  
* Definirá el rango exacto que contiene la tabla dinámica.  
* Copiará ese rango a un libro nuevo, preservando la definición de la tabla dinámica.  
* Guardará el nuevo archivo y verificará que la tabla dinámica funciona.  

Los pasos funcionan con cualquier versión de Excel compatible con Aspose.Cells (2007‑2024) y requieren solo unas pocas líneas de código Java.

## Prerequisites

| Requisito | Por qué es importante |
|-------------|----------------|
| **Java 8 o superior** | Aspose.Cells está construido para Java 8+. |
| **Aspose.Cells for Java** (última versión) | Proporciona las APIs `Workbook`, `Range` y `CopyRange` usadas en el ejemplo. |
| **Libro de origen** con una tabla dinámica (p. ej., `Source.xlsx`) | La tabla dinámica que desea duplicar. |
| **Permiso de escritura** en el directorio de destino | Necesario para guardar `CopyWithPivot.xlsx`. |

Agregue la dependencia de Aspose.Cells Maven a su `pom.xml` (o descargue el JAR manualmente):

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version>   <!-- use the latest stable version -->
</dependency>
```

## Cómo duplicar tablas dinámicas – implementación completa

A continuación se muestra un programa Java autónomo que demuestra **cómo duplicar tablas dinámicas** copiando el rango que contiene la tabla dinámica. El código incluye manejo de errores, comentarios y un paso de verificación.

```java
// File: DuplicatePivot.java
import com.aspose.cells.*;

public class DuplicatePivot {
    public static void main(String[] args) {
        // 1️⃣ Load the source workbook that holds the pivot table.
        String srcPath = "YOUR_DIRECTORY/Source.xlsx";
        Workbook srcWb;
        try {
            srcWb = new Workbook(srcPath);
        } catch (Exception e) {
            System.err.println("Failed to load source workbook: " + e.getMessage());
            return;
        }

        // 2️⃣ Identify the range that encloses the pivot table.
        // Adjust the sheet index (0‑based) and address as needed.
        Worksheet srcSheet = srcWb.getWorksheets().get(0);
        // Example address "A1:G20" – includes the pivot and its data source.
        String pivotRangeAddress = "A1:G20";
        Range srcRange = srcSheet.getCells().createRange(pivotRangeAddress);

        // 3️⃣ Create a destination workbook and copy the identified range.
        Workbook destWb = new Workbook(); // starts with a blank workbook
        Worksheet destSheet = destWb.getWorksheets().get(0);
        try {
            // copyRange copies both values and the internal pivot cache.
            destSheet.getCells().copyRange(srcRange, "A1");
        } catch (Exception e) {
            System.err.println("Failed to copy range: " + e.getMessage());
            return;
        }

        // 4️⃣ (Optional) Refresh the pivot so it reflects the copied data.
        // Aspose.Cells automatically rebuilds the cache, but calling refresh
        // guarantees up‑to‑date results if the source data has changed.
        for (int i = 0; i < destSheet.getPivotTables().getCount(); i++) {
            destSheet.getPivotTables().get(i).refresh();
        }

        // 5️⃣ Save the new workbook that now contains the duplicated pivot.
        String destPath = "YOUR_DIRECTORY/CopyWithPivot.xlsx";
        try {
            destWb.save(destPath);
            System.out.println("Pivot table duplicated successfully to: " + destPath);
        } catch (Exception e) {
            System.err.println("Failed to save destination workbook: " + e.getMessage());
        }
    }
}
```

### Explicación de cada paso

| Paso | Qué hace el código | Por qué es importante para **copiar tabla dinámica** |
|------|-------------------|----------------------------------------|
| **1️⃣ Cargar libro de origen** | `new Workbook(srcPath)` lee `Source.xlsx`. | El archivo de origen es el único lugar donde existe la tabla dinámica original. |
| **2️⃣ Definir el rango** | `createRange("A1:G20")` crea un objeto `Range` que cubre la tabla dinámica y sus datos. | Una tabla dinámica se almacena junto con su caché; copiar todo el rango garantiza que la caché también se traslade. |
| **3️⃣ Copiar el rango** | `copyRange(srcRange, "A1")` escribe el rango en la hoja de destino. | Este es el núcleo de **copiar rango entre libros** – la API maneja los objetos ocultos automáticamente. |
| **4️⃣ Actualizar tabla dinámica** | `pivotTable.refresh()` fuerza a la tabla dinámica a recalcular. | Garantiza que la tabla dinámica duplicada muestre los mismos valores que la original, especialmente después de modificaciones. |
| **5️⃣ Guardar libro** | `destWb.save(destPath)` escribe el archivo en disco. | Produce el resultado final de **copiar rango de Excel** que puede abrir en Excel. |

#### Salida esperada

Después de ejecutar el programa, abra `CopyWithPivot.xlsx`. Verá una hoja de cálculo que se ve idéntica a la hoja de origen, y la tabla dinámica funciona exactamente como la original – puede expandir filas, filtrar campos y actualizar datos sin errores.

## Variaciones comunes y casos límite

### 1️⃣ Copiar una tabla dinámica que abarca varias hojas

Si los datos de origen de la tabla dinámica están en una hoja diferente a la propia tabla dinámica, incluya ambas hojas en la operación de copia. El enfoque más sencillo es copiar primero la hoja de origen completa y luego copiar la hoja de la tabla dinámica:

```java
// Copy source data sheet
Workbook temp = new Workbook(); // temporary workbook for the data sheet
temp.getWorksheets().addCopy(srcWb.getWorksheets().get(0));
Workbook dest = new Workbook();
dest.getWorksheets().addCopy(temp.getWorksheets().get(0));

// Then copy the pivot sheet as shown earlier
```

### 2️⃣ Manejo de rangos con nombre

Aspose.Cells preserva los rangos con nombre cuando copia un rango. Sin embargo, si el libro de destino ya contiene un nombre con el mismo identificador, se lanza una `CellsException`. Resuelva esto renombrando el nombre conflictivo antes de la copia:

```java
if (destWb.getWorksheets().get(0).getNames().containsKey("MyRange")) {
    destWb.getWorksheets().get(0).getNames().remove("MyRange");
}
```

### 3️⃣ Libros grandes y rendimiento

Copiar rangos muy grandes (cientos de miles de filas) puede consumir mucha memoria. Active **optimización de memoria**:

```java
LoadOptions loadOptions = new LoadOptions(LoadFormat.XLSX);
loadOptions.setMemorySetting(MemorySetting.MEMORY_PREFERENCE);
Workbook largeSrc = new Workbook(srcPath, loadOptions);
```

### 4️⃣ Mantener fórmulas intactas

Si el rango de origen contiene fórmulas que hacen referencia a celdas fuera del área copiada, esas referencias se romperán después de la copia. Para evitarlo, amplíe el rango para incluir todas las celdas dependientes, o use `copyRange` con la bandera `CopyOptions` `CopyOptions.COPY_FORMULA`.

```java
CopyOptions options = new CopyOptions();
options.setCopyFormula(true);
destSheet.getCells().copyRange(srcRange, "A1", options);
```

## Consejos profesionales para un **copiar rango entre libros** confiable

* **Siempre use direcciones absolutas** (`$A$1:$G$20`) cuando la hoja de origen pueda ser renombrada.  
* **Actualizar después de copiar** – aunque Aspose.Cells reconstruye la caché, llamar a `refresh()` elimina advertencias ocasionales de caché obsoleta en Excel.  
* **Validar la tabla dinámica**: después de guardar, abra el archivo programáticamente y llame a `pivotTable.validate()` para asegurar que no haya referencias rotas.  
* **Compatibilidad de versiones**: el código funciona con archivos Excel 2007‑2024 (`.xlsx`, `.xlsm`). Para archivos `.xls` heredados, establezca `LoadOptions.setLoadFormat(LoadFormat.XLS)`.

## Listado completo del código fuente (listo para compilar)



## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y funcionales con explicaciones paso a paso para ayudarle a dominar funciones adicionales de la API y explorar enfoques de implementación alternativos en sus propios proyectos.

- [Cómo copiar tabla dinámica en Java – Guía completa de Aspose.Cells](/cells/english/java/excel-pivot-tables/how-to-copy-pivot-table-in-java-complete-aspose-cells-guide/)
- [Cómo crear tablas dinámicas en Excel usando Aspose.Cells para Java: Guía completa](/cells/english/java/data-analysis/create-pivot-tables-excel-aspose-cells-java/)
- [Cómo actualizar la fuente de una tabla dinámica de Excel con Aspose.Cells para Java: Guía completa](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}