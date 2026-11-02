---
category: general
date: 2026-08-14
description: Cómo establecer el delimitador y guardar como CSV usando Aspose.Cells,
  limitar los dígitos, exportar cadenas CSV y recalcular fórmulas en Java.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to set delimiter
- save as csv
- recalculate formulas
- how to export csv
- how to limit digits
language: es
lastmod: 2026-08-14
og_description: Cómo establecer el delimitador y guardar como CSV con Aspose.Cells,
  limitar los dígitos, exportar cadenas CSV y recalcular fórmulas en Java.
og_image_alt: Screenshot of Java code that sets a CSV delimiter and saves an Excel
  workbook as CSV using Aspose.Cells
og_title: Cómo establecer el delimitador y guardar como CSV – Guía de Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-08-14'
  description: How to set delimiter and save as CSV using Aspose.Cells, limit digits,
    export CSV strings, and recalculate formulas in Java.
  headline: How to set delimiter and save as CSV with Aspose.Cells
  type: TechArticle
- description: How to set delimiter and save as CSV using Aspose.Cells, limit digits,
    export CSV strings, and recalculate formulas in Java.
  name: How to set delimiter and save as CSV with Aspose.Cells
  steps:
  - name: Why this works
    text: "- `CsvSaveOptions.setDelimiter(char)` tells Aspose.Cells which character
      separates fields. By default it’s a comma, but any character (tab `'\t'`, pipe
      `'|'`, etc.) works. - `setSignificantDigits(int)` limits numeric precision,
      satisfying the **how to limit digits** requirement without manually form"
  - name: When to use this
    text: '- Returning CSV from a REST endpoint (`@RestController` in Spring) - Embedding
      CSV data into an email attachment without writing to disk - Performing quick
      sanity checks during unit tests'
  - name: Why recalculate?
    text: '- Formulas may reference external data or volatile functions (`NOW()`,
      `RAND()`) that need fresh values. - Dynamic‑array formulas (e.g., `=SORT(A1:A10)`)
      are evaluated automatically, but calling `calculateFormula()` guarantees consistency
      across all sheets.'
  - name: Verifying the result
    text: 1. Open `output.csv` in a text editor – you should see a semicolon (`;`)
      separating each column. 2. Confirm that numeric columns display at most five
      significant digits. 3. The console output will print the CSV string generated
      in step 4. 4. Open `japan_updated.xlsx` in Excel – any formulas that pre
  type: HowTo
tags:
- Aspose.Cells
- Java
- CSV export
- Excel automation
title: Cómo establecer el delimitador y guardar como CSV con Aspose.Cells
url: /es/java/excel-import-export/how-to-set-delimiter-and-save-as-csv-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo establecer el delimitador y guardar como CSV con Aspose.Cells

Si necesitas **cómo establecer el delimitador** al exportar datos desde un libro de Excel, esta guía te muestra una solución completa, de extremo a extremo, usando Aspose.Cells para Java. Aprenderás a configurar el delimitador CSV, limitar el número de dígitos significativos, exportar una cadena CSV y actualizar las fórmulas de matriz dinámica después de cargar un libro de trabajo.

El tutorial cubre todo lo necesario para ejecutar el código en tu máquina, incluido el manejo de calendarios especiales como el reinado del Emperador japonés. Al final, podrás generar archivos CSV precisos, controlar la precisión numérica y asegurar que las fórmulas estén actualizadas.

## Prerrequisitos

- Java 17 o posterior (el código también compila con JDK 11+)
- Aspose.Cells para Java 23.9 o más reciente – descárgalo desde el [sitio web de Aspose](https://products.aspose.com/cells/java/)
- Familiaridad básica con Maven o Gradle para la gestión de dependencias
- Un IDE (IntelliJ IDEA, Eclipse, VS Code) o un editor de texto simple y la línea de comandos

> **Consejo profesional:** Usa una carpeta `libs` dedicada o Maven Central para mantener el JAR de Aspose.Cells en tu classpath. Los ejemplos a continuación asumen un proyecto Maven.

## Paso 1: Configurar el proyecto Maven

Crea un `pom.xml` con la dependencia de Aspose.Cells:

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0" 
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 
                             http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>com.example</groupId>
    <artifactId>aspose-csv-demo</artifactId>
    <version>1.0.0</version>
    <properties>
        <maven.compiler.source>17</maven.compiler.source>
        <maven.compiler.target>17</maven.compiler.target>
    </properties>

    <dependencies>
        <dependency>
            <groupId>com.aspose</groupId>
            <artifactId>aspose-cells</artifactId>
            <version>23.9</version>
            <classifier>jdk17</classifier>
        </dependency>
    </dependencies>
</project>
```

Ejecuta `mvn clean compile` para descargar la biblioteca y verificar que la compilación sea exitosa.

## Paso 2: Cómo establecer el delimitador y guardar como CSV

El objetivo principal es cambiar el delimitador por defecto (coma) a un carácter personalizado (por ejemplo, punto y coma) al guardar un libro de Excel como CSV. Aspose.Cells proporciona `CsvSaveOptions` para este propósito.

```java
package com.example;

import com.aspose.cells.*;

public class CsvDelimiterDemo {
    public static void main(String[] args) throws Exception {
        // Load an existing workbook (replace the path with your file)
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // Configure CSV save options
        CsvSaveOptions csvOptions = new CsvSaveOptions();
        // Primary requirement: set a custom delimiter
        csvOptions.setDelimiter(';');               // <-- how to set delimiter
        // Optional: limit the number of significant digits
        csvOptions.setSignificantDigits(5);         // <-- how to limit digits

        // Save the workbook as CSV using the configured options
        workbook.save("YOUR_DIRECTORY/output.csv", csvOptions);

        System.out.println("CSV file saved with ';' delimiter and 5‑digit precision.");
    }
}
```

### Por qué funciona

- `CsvSaveOptions.setDelimiter(char)` indica a Aspose.Cells qué carácter separa los campos. Por defecto es una coma, pero cualquier carácter (tab `'\t'`, barra vertical `'|'`, etc.) funciona.
- `setSignificantDigits(int)` limita la precisión numérica, cumpliendo el requisito de **cómo limitar los dígitos** sin formatear manualmente cada celda.

#### Salida esperada

El archivo `output.csv` contendrá filas como:

```
Name;Amount;Date
Alice;123.46;2024-01-15
Bob;78.90;2024-01-16
```

Observa que los números se redondean a cinco dígitos significativos (p. ej., `123.45678` → `123.46`).

## Paso 3: Cómo limitar los dígitos al guardar CSV

Si necesitas un control más estricto sobre el formato numérico, también puedes usar una instancia de `CsvSaveOptions` para especificar una cadena de formato numérico personalizada.

```java
CsvSaveOptions csvOptions = new CsvSaveOptions();
csvOptions.setDelimiter(',');                // standard comma delimiter
csvOptions.setNumberFormat("0.####");        // up to 4 decimal places
csvOptions.setSignificantDigits(6);          // overall significant digits
```

- `setNumberFormat` sigue los patrones al estilo .NET, que Aspose.Cells respeta.
- Combinar `setNumberFormat` y `setSignificantDigits` te brinda un redondeo predecible en diferentes configuraciones regionales.

## Paso 4: Cómo exportar CSV como una cadena con un delimitador personalizado

A veces no deseas un archivo físico; necesitas los datos CSV en memoria (p. ej., para enviarlos como respuesta HTTP). La clase `ExportTableOptions` permite exportar un rango como una cadena.

```java
// Export a range (rows 0‑9, columns 0‑4) as a CSV string
ExportTableOptions exportOptions = new ExportTableOptions();
exportOptions.setExportAsString(true);   // return a string instead of a file
exportOptions.setDelimiter(',');         // <-- how to set delimiter for export
exportOptions.setIncludeColumnNames(true);

String csvData = workbook.getWorksheets()
                         .get(0)                     // first worksheet
                         .getCells()
                         .exportDataTableAsString(0, 0, 10, 5, exportOptions);

System.out.println("Exported CSV string:");
System.out.println(csvData);
```

### Cuándo usar esto

- Devolver CSV desde un endpoint REST (`@RestController` en Spring)
- Incrustar datos CSV en un archivo adjunto de correo electrónico sin escribir en disco
- Realizar comprobaciones rápidas durante pruebas unitarias

## Paso 5: Cómo recalcular fórmulas después de cargar un libro de trabajo

Si tu libro contiene fórmulas—especialmente **fórmulas de matriz dinámica** introducidas en versiones recientes de Excel—debes recalcularlas después de cargar el archivo. Aspose.Cells actualiza automáticamente los resultados de matrices dinámicas, pero aún necesitas invocar `calculateFormula()` para las fórmulas regulares.

```java
// Load a workbook that uses the Japanese Emperor calendar (optional step)
LoadOptions loadOptions = new LoadOptions();
loadOptions.setCalendar(CalendarType.JAPANESE_EMPEROR_REIGN);
Workbook japaneseWorkbook = new Workbook("YOUR_DIRECTORY/japan.xlsx", loadOptions);

// Recalculate all formulas in the workbook
japaneseWorkbook.calculateFormula();   // <-- recalculate formulas

// Save the refreshed workbook (preserves the original calendar)
japaneseWorkbook.save("YOUR_DIRECTORY/japan_updated.xlsx");
System.out.println("Formulas recalculated and workbook saved.");
```

### ¿Por qué recalcular?

- Las fórmulas pueden referenciar datos externos o funciones volátiles (`NOW()`, `RAND()`) que requieren valores frescos.
- Las fórmulas de matriz dinámica (p. ej., `=SORT(A1:A10)`) se evalúan automáticamente, pero llamar a `calculateFormula()` garantiza la consistencia en todas las hojas.

## Paso 6: Ejemplo completo de extremo a extremo

A continuación se muestra una única clase que demuestra **cómo establecer el delimitador**, **guardar como CSV**, **limitar los dígitos**, **exportar una cadena CSV**, **cargar un libro con un calendario especial** y **recalcular fórmulas**. El código está listo para copiar y pegar en tu proyecto.

```java
package com.example;

import com.aspose.cells.*;

public class AsposeCsvFullDemo {
    public static void main(String[] args) throws Exception {
        // -----------------------------------------------------------------
        // 1. Load an existing workbook
        // -----------------------------------------------------------------
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // -----------------------------------------------------------------
        // 2. Configure CSV save options (delimiter + digit limit)
        // -----------------------------------------------------------------
        CsvSaveOptions csvOptions = new CsvSaveOptions();
        csvOptions.setDelimiter(';');          // <-- how to set delimiter
        csvOptions.setSignificantDigits(5);    // <-- how to limit digits

        // -----------------------------------------------------------------
        // 3. Save the workbook as CSV
        // -----------------------------------------------------------------
        workbook.save("YOUR_DIRECTORY/output.csv", csvOptions);
        System.out.println("Saved CSV with ';' delimiter.");

        // -----------------------------------------------------------------
        // 4. Export a range as a CSV string (custom delimiter)
        // -----------------------------------------------------------------
        ExportTableOptions exportOptions = new ExportTableOptions();
        exportOptions.setExportAsString(true);
        exportOptions.setDelimiter(',');       // <-- how to set delimiter for export
        exportOptions.setIncludeColumnNames(true);

        String csvString = workbook.getWorksheets()
                                   .get(0)
                                   .getCells()
                                   .exportDataTableAsString(0, 0, 10, 5, exportOptions);
        System.out.println("CSV string exported:");
        System.out.println(csvString);

        // -----------------------------------------------------------------
        // 5. Load a workbook that uses the Japanese Emperor calendar
        // -----------------------------------------------------------------
        LoadOptions loadOptions = new LoadOptions();
        loadOptions.setCalendar(CalendarType.JAPANESE_EMPEROR_REIGN);
        Workbook japaneseWorkbook = new Workbook("YOUR_DIRECTORY/japan.xlsx", loadOptions);

        // -----------------------------------------------------------------
        // 6. Recalculate formulas (including dynamic‑array formulas)
        // -----------------------------------------------------------------
        japaneseWorkbook.calculateFormula();   // <-- recalculate formulas

        // -----------------------------------------------------------------
        // 7. Save the refreshed workbook
        // -----------------------------------------------------------------
        japaneseWorkbook.save("YOUR_DIRECTORY/japan_updated.xlsx");
        System.out.println("Japanese workbook refreshed and saved.");
    }
}
```

### Verificando el resultado

1. Abre `output.csv` en un editor de texto – deberías ver un punto y coma (`;`) separando cada columna.
2. Confirma que las columnas numéricas muestren como máximo cinco dígitos significativos.
3. La salida de consola imprimirá la cadena CSV generada en el paso 4.
4. Abre `japan_updated.xlsx` en Excel – cualquier fórmula que antes mostrara `#REF!` o valores obsoletos ahora mostrará los resultados correctos.

## Problemas comunes y cómo evitarlos

| Problema | Causa | Solución |
|----------|-------|----------|
| CSV muestra comillas extra | Las celdas contienen comas mientras el delimitador también es una coma | Usa un delimitador diferente (`;` o `\t`) mediante `setDelimiter` |
| Los números se redondean incorrectamente | `setSignificantDigits` se aplicó después del formato numérico personalizado | Aplica `setNumberFormat` **antes** de `setSignificantDigits` |

## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos con explicaciones paso a paso para ayudarte a dominar funciones adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [How to Load and Save Excel as CSV Using Aspose.Cells for Java: A Comprehensive Guide](/cells/english/java/workbook-operations/aspose-cells-java-load-save-excel-csv/)
- [How to Load a CSV File Using Aspose.Cells for Java: A Comprehensive Guide](/cells/english/java/workbook-operations/load-csv-aspose-cells-java-tutorial/)
- [How to Load CSV Files Using Custom Parsers in Java with Aspose.Cells](/cells/english/java/import-export/load-csv-files-custom-parsers-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}