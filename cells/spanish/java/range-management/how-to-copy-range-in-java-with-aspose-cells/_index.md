---
category: general
date: 2026-09-08
description: Cómo copiar un rango en Java usando Aspose.Cells – aprende a copiar tabla
  dinámica, duplicar tabla dinámica y exportar tabla dinámica manteniendo el formato.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy range
- copy pivot table
- duplicate pivot table
- export pivot table
- copy range with formatting
language: es
lastmod: 2026-09-08
og_description: Cómo copiar un rango en Java con Aspose.Cells. Este tutorial le muestra
  cómo copiar una tabla dinámica, duplicar una tabla dinámica y exportar una tabla
  dinámica manteniendo el formato.
og_image_alt: Screenshot of Java code copying a pivot table range in Aspose.Cells
og_title: Cómo copiar un rango en Java – guía completa de Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-09-08'
  description: How to copy range in Java using Aspose.Cells – learn to copy pivot
    table, duplicate pivot table, and export pivot table while preserving formatting.
  headline: How to copy range in Java with Aspose.Cells
  type: TechArticle
- description: How to copy range in Java using Aspose.Cells – learn to copy pivot
    table, duplicate pivot table, and export pivot table while preserving formatting.
  name: How to copy range in Java with Aspose.Cells
  steps:
  - name: Copy pivot table to an existing workbook
    text: 'If you need to **duplicate pivot table** inside a workbook that already
      has data, use the same `copyRange` call but point to a different destination
      address:'
  - name: Export pivot table only (without surrounding data)
    text: 'Sometimes you want just the pivot table, not the source data. Identify
      the pivot table’s display range via its `getPivotTable` method:'
  - name: Preserve conditional formatting
    text: 'Conditional formatting rules are part of the style collection. The `PasteType.ALL`
      flag already copies them, but you can be explicit:'
  - name: Edge cases and troubleshooting
    text: '| Situation | What to watch for | Recommended fix | |-----------|-------------------|-----------------|
      | Source and destination workbooks use different Excel versions | Some newer
      pivot features (e.g., data model) may not render correctly | Use the latest
      Aspose.Cells version and set `Workbook.setF'
  - name: Next steps
    text: '- Explore **copy range with formatting** for charts and images (use `PasteType.PICTURES`).
      - Automate batch processing: loop over multiple source files and consolidate
      their pivot tables into a summary workbook. - Combine this technique with Aspose.Slides
      to generate PowerPoint reports that embed th'
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: Cómo copiar un rango en Java con Aspose.Cells
url: /es/java/range-management/how-to-copy-range-in-java-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo copiar un rango en Java con Aspose.Cells

Si necesitas **how to copy range** en Java, Aspose.Cells hace la tarea sencilla. Ya sea que estés moviendo un bloque de celdas regular o una tabla dinámica completa, la biblioteca maneja la operación de copia manteniendo fórmulas, estilos y la caché de la tabla dinámica intactos. En esta guía aprenderás a **copy pivot table**, **duplicate pivot table**, e incluso **export pivot table** a un nuevo libro de trabajo con formato completo.

El tutorial cubre todo, desde la configuración del proyecto hasta el paso final de verificación, para que puedas ejecutar el código inmediatamente después de leerlo. No se requieren herramientas externas más allá del JAR de Aspose.Cells para Java.

## Requisitos previos

Antes de comenzar, asegúrate de tener:

- Java 17 (o cualquier JDK compatible) instalado y configurado en tu IDE.
- Maven o Gradle para la gestión de dependencias (los ejemplos usan Maven).
- Un archivo Excel fuente (`source.xlsx`) que contiene una tabla dinámica en el rango `A1:H20`.
- Familiaridad básica con la programación en Java.

## Paso 1: Añadir Aspose.Cells a tu proyecto

Aspose.Cells es una biblioteca comercial, pero está disponible una versión de evaluación gratuita. Añade la dependencia a tu `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- Use the latest version -->
</dependency>
```

> **Consejo profesional:** Si prefieres Gradle, la entrada equivalente es:
> ```gradle
> implementation 'com.aspose:aspose-cells:24.9'
> ```

Añadir el JAR te da acceso a las clases `Workbook`, `Worksheet`, `Range` y `CopyOptions` usadas a lo largo de esta guía.

## Paso 2: Cargar el libro de trabajo fuente y seleccionar la primera hoja

La primera parte de **how to copy range** es abrir el libro de trabajo que contiene los datos que deseas mover.

```java
import com.aspose.cells.*;

public class CopyRangeDemo {
    public static void main(String[] args) throws Exception {
        // Load the source workbook
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/source.xlsx");
        // Select the first worksheet (index 0)
        Worksheet sourceSheet = sourceWorkbook.getWorksheets().get(0);
```

> **Por qué es importante:** Abrir el libro de trabajo crea una representación en memoria que la API puede manipular sin tocar el archivo original en disco.

## Paso 3: Definir el rango que contiene la tabla dinámica

Una tabla dinámica vive dentro de un bloque rectangular. Debes especificar ese bloque para que Aspose.Cells sepa qué copiar.

```java
        // Define the range that holds the pivot table and its source data
        Range sourceRange = sourceSheet.getCells().createRange("A1:H20");
```

> **Nota:** El método `createRange` **no** copia nada todavía; solo crea un objeto `Range` que apunta a las celdas que pretendes duplicar.

## Paso 4: Crear un nuevo libro de trabajo y obtener su primera hoja

Ahora crea el libro de trabajo de destino donde residirá el rango copiado.

```java
        // Create an empty workbook for the destination
        Workbook destWorkbook = new Workbook();
        // Get its first (and only) worksheet
        Worksheet destSheet = destWorkbook.getWorksheets().get(0);
```

> **¿Por qué un nuevo libro de trabajo?** Usar un archivo nuevo garantiza que no haya estilos ocultos o rangos con nombre que interfieran con la operación de copia, lo cual es especialmente importante cuando **export pivot table** a un archivo separado.

## Paso 5: Copiar el rango (incluida la tabla dinámica) a la hoja de destino

Este es el núcleo de **how to copy range with formatting**. El objeto `CopyOptions` indica a Aspose.Cells que preserve todo: valores, fórmulas, estilos y caché de la tabla dinámica.

```java
        // Prepare copy options – preserve formatting and pivot cache
        CopyOptions copyOptions = new CopyOptions();
        copyOptions.setPasteType(PasteType.ALL); // copies everything
        copyOptions.setSkipBlanks(false);        // keep blank cells

        // Copy the defined range to cell A1 of the destination sheet
        destSheet.getCells().copyRange(sourceRange, "A1", copyOptions);
```

> **Copy pivot table:** Como el rango de origen incluye la tabla dinámica, la API duplica automáticamente la caché de la tabla dinámica, de modo que la nueva hoja contiene una tabla dinámica totalmente funcional que se comporta exactamente como la original.

## Paso 6: Guardar el libro de trabajo de destino

Finalmente, escribe el resultado en disco.

```java
        // Save the destination workbook
        destWorkbook.save("YOUR_DIRECTORY/dest.xlsx");
    }
}
```

Cuando abras `dest.xlsx`, verás una réplica exacta de la tabla dinámica original, completa con su formato, segmentadores y campos calculados.

## Resultado esperado

- `dest.xlsx` contiene una hoja de cálculo llamada **Sheet1**.
- Las celdas `A1:H20` contienen los mismos datos y tabla dinámica que el origen.
- Todos los estilos de celda (fuentes, colores, bordes) se conservan.
- La tabla dinámica es totalmente interactiva; al actualizarla refleja los datos subyacentes en el rango copiado.

## Cómo copiar rango con formato – inmersión profunda

El ejemplo anterior muestra el escenario más simple, pero puedes encontrar variaciones que requieran un enfoque ligeramente diferente.

### Copiar tabla dinámica a un libro de trabajo existente

Si necesitas **duplicate pivot table** dentro de un libro de trabajo que ya tiene datos, usa la misma llamada `copyRange` pero apunta a una dirección de destino diferente:

```java
// Assume destWorkbook already contains other sheets
Worksheet targetSheet = destWorkbook.getWorksheets().get(2);
targetSheet.getCells().copyRange(sourceRange, "B5", copyOptions);
```

### Exportar solo la tabla dinámica (sin los datos circundantes)

A veces solo deseas la tabla dinámica, no los datos fuente. Identifica el rango de visualización de la tabla dinámica mediante su método `getPivotTable`:

```java
PivotTable pt = sourceSheet.getPivotTables().get(0);
String ptArea = pt.getDisplayRange(); // e.g., "C5:G15"
Range pivotOnly = sourceSheet.getCells().createRange(ptArea);
destSheet.getCells().copyRange(pivotOnly, "A1", copyOptions);
```

### Conservar el formato condicional

Las reglas de formato condicional forman parte de la colección de estilos. La bandera `PasteType.ALL` ya las copia, pero puedes ser explícito:

```java
copyOptions.setPasteType(PasteType.FORMATS);
copyOptions.setPasteType(PasteType.ALL); // overrides previous, ensures everything
```

### Casos límite y solución de problemas

| Situación | Qué observar | Solución recomendada |
|-----------|--------------|----------------------|
| Los libros de trabajo origen y destino usan diferentes versiones de Excel | Algunas funciones más nuevas de tabla dinámica (p. ej., modelo de datos) pueden no renderizarse correctamente | Utiliza la última versión de Aspose.Cells y establece `Workbook.setFileFormatType(FileFormatType.XLSX)` para ambos libros de trabajo |
| Tablas dinámicas muy grandes ( > 10 000 filas) generan presión de memoria | Errores de falta de memoria durante la copia | Habilita `Workbook.setMemorySetting(MemorySetting.MEMORY_PREFERENCE)` antes de cargar |
| La hoja de destino ya contiene un rango con nombre con el mismo nombre que el origen | La colisión de nombres provoca un fallo de `CopyOptions` | Llama a `copyOptions.setIgnoreNameConflicts(true)` |

## Ejemplo completo y ejecutable

A continuación tienes el programa completo que puedes copiar‑pegar en una clase Java. Incluye todas las importaciones, manejo de errores y comentarios.

```java
import com.aspose.cells.*;

public class CopyRangeDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load the source workbook
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/source.xlsx");
        Worksheet sourceSheet = sourceWorkbook.getWorksheets().get(0);

        // 2️⃣ Define the range that includes the pivot table
        Range sourceRange = sourceSheet.getCells().createRange("A1:H20");

        // 3️⃣ Create a new destination workbook
        Workbook destWorkbook = new Workbook();
        Worksheet destSheet = destWorkbook.getWorksheets().get(0);

        // 4️⃣ Configure copy options to keep everything (values, formulas, formatting, pivot cache)
        CopyOptions copyOptions = new CopyOptions();
        copyOptions.setPasteType(PasteType.ALL);
        copyOptions.setSkipBlanks(false);
        copyOptions.setIgnoreNameConflicts(true); // avoid name collisions

        // 5️⃣ Perform the copy
        destSheet.getCells().copyRange(sourceRange, "A1", copyOptions);

        // 6️⃣ Save the result
        destWorkbook.save("YOUR_DIRECTORY/dest.xlsx");
        System.out.println("Copy completed – dest.xlsx now contains the duplicated pivot table.");
    }
}
```

Ejecuta el programa, luego abre `dest.xlsx` para verificar que la tabla dinámica funciona exactamente como la original.

## Conclusión

Ahora sabes **how to copy range** en Java usando Aspose.Cells, incluido cómo **copy pivot table**, **duplicate pivot table** y **export pivot table** mientras preservas todo el formato. La biblioteca abstrae los detalles de bajo nivel de la estructura XML de Excel, permitiéndote centrarte en la lógica de negocio.

### Próximos pasos

- Explora **copy range with formatting** para gráficos e imágenes (usa `PasteType.PICTURES`).
- Automatiza el procesamiento por lotes: recorre varios archivos fuente y consolida sus tablas dinámicas en un libro de trabajo resumen.
- Combina esta técnica con Aspose.Slides para generar informes PowerPoint que incrusten la tabla dinámica copiada

## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y funcionales con explicaciones paso a paso para ayudarte a dominar características adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Cómo actualizar la fuente de la tabla dinámica de Excel con Aspose.Cells para Java: una guía completa](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [Optimizar la carga de tablas dinámicas en Java usando Aspose.Cells – una guía completa](/cells/english/java/data-analysis/optimize-pivot-table-loading-aspose-cells-java/)
- [Cómo copiar tabla dinámica en C# – Convertir Excel a PPTX, copiar rango y crear cuadro de texto](/cells/english/net/pivot-tables/how-to-copy-pivot-table-in-c-convert-excel-to-pptx-copy-rang/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}