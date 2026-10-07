---
category: general
date: 2026-10-07
description: Aprende cómo crear PNG a partir de un rango y exportar datos como PNG
  en Java. Esta guía te muestra cómo guardar la imagen de un rango de Excel usando
  Aspose.Cells.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create png from range
- export data as png
- save excel range image
- convert worksheet to png
- save cells as png
language: es
lastmod: 2026-10-07
og_description: Crea PNG a partir de un rango en Java y exporta los datos como PNG
  con Aspose.Cells. Sigue este tutorial completo para guardar la imagen del rango
  de Excel al instante.
og_image_alt: Screenshot of Java code that creates a PNG from an Excel range
og_title: Crear PNG a partir de un rango en Java – guía paso a paso de Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: Learn how to create PNG from range and export data as PNG in Java.
    This guide shows you how to save Excel range image using Aspose.Cells.
  headline: How to create PNG from range in Java with Aspose.Cells
  type: TechArticle
- description: Learn how to create PNG from range and export data as PNG in Java.
    This guide shows you how to save Excel range image using Aspose.Cells.
  name: How to create PNG from range in Java with Aspose.Cells
  steps:
  - name: Maven dependency
    text: '```xml <dependency> <groupId>com.aspose</groupId> <artifactId>aspose-cells</artifactId>
      <version>23.12</version> </dependency> ```'
  - name: Expected output
    text: '* A file named `PivotImage.png` located in `YOUR_DIRECTORY`. * The image
      shows the exact layout, fonts, colors, and borders from the selected range.
      * If the source range contains a pivot table, the rendered image includes the
      same styling and calculated values as displayed in Excel.'
  - name: Exporting a non‑contiguous range
    text: Aspose.Cells does not render disjoint ranges in a single image. To export
      multiple areas, create separate images for each range and combine them later
      with an image‑processing library (e.g., ImageIO).
  - name: Saving a large worksheet as PNG
    text: 'Rendering an entire sheet that spans thousands of rows can consume significant
      memory. Mitigate this by:'
  - name: Preserving cell formulas
    text: A PNG image is a raster format; formulas are not retained. If downstream
      consumers need the raw data, also export the range as CSV or JSON using `Range.exportDataTable()`.
  - name: Next steps
    text: '* Experiment with different `Resolution` values to balance quality and
      file size. * Use `ImageOrPrintOptions.setTransparent(true)` if you need a PNG
      with a transparent background. * Combine multiple range images into a single
      PDF using `PdfSaveOptions` for multi‑page reports. * Explore exporting to '
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: Cómo crear PNG a partir de un rango en Java con Aspose.Cells
url: /es/java/images-shapes/how-to-create-png-from-range-in-java-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo crear PNG a partir de un rango en Java con Aspose.Cells

Si necesitas **crear PNG a partir de un rango** en un libro de Excel, este tutorial te muestra exactamente cómo hacerlo. Al final de la guía podrás **exportar datos como PNG**, guardar una imagen de un rango de Excel y reutilizar el archivo en informes o páginas web.

Verás un programa Java completo y ejecutable que carga un libro, selecciona las celdas deseadas, las renderiza como PNG y guarda el resultado en disco. No se requieren herramientas externas—Aspose.Cells maneja todo internamente.

## Qué cubre este tutorial

* Requisitos previos y configuración de Maven para Aspose.Cells
* Cargar un libro que contiene una tabla dinámica o cualquier rango de datos
* Definir el rango de celdas exacto que deseas convertir
* Configurar opciones de imagen para la salida PNG
* Renderizar el rango y guardar el archivo PNG
* Problemas comunes y consejos para imágenes de alta calidad

Después de completar estos pasos podrás **convertir una hoja de cálculo a PNG** para cualquier rango, ya sea una tabla simple o un gráfico dinámico complejo.

## Requisitos previos

* Java 17 o posterior (el código compila con JDK 11+)
* Maven 3.6+ (o Gradle si lo prefieres)
* Aspose.Cells for Java 23.12 o más reciente – agrega la dependencia que se muestra a continuación
* Un archivo Excel existente (`PivotWithStyle.xlsx`) que contiene el rango que deseas capturar

> **Consejo profesional:** Si no tienes una licencia, puedes solicitar una clave de evaluación temporal a Aspose. La biblioteca funciona en modo de evaluación sin configuración adicional.

### Dependencia Maven

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version>
</dependency>
```

## Paso 1: Cargar el libro que contiene el rango objetivo

La primera operación es abrir el archivo Excel. Aspose.Cells lee el archivo en memoria sin requerir Microsoft Office.

```java
import com.aspose.cells.*;

public class PivotRangeToPng {
    public static void main(String[] args) throws Exception {
        // Load the workbook containing the data you want to export
        Workbook workbook = new Workbook("YOUR_DIRECTORY/PivotWithStyle.xlsx");
```

*Por qué es importante*: Cargar el libro te da acceso a hojas de cálculo, celdas y propiedades de configuración de página necesarias para el renderizado.

## Paso 2: Acceder a la hoja que contiene el rango

La mayoría de los libros tienen una hoja predeterminada en el índice 0, pero también puedes usar el nombre de la hoja.

```java
        // Retrieve the first worksheet (index 0)
        Worksheet worksheet = workbook.getWorksheets().get(0);
```

Si tus datos están en una hoja diferente, reemplaza `0` con el índice apropiado o usa `workbook.getWorksheets().get("SheetName")`.

## Paso 3: Definir el rango de celdas que deseas convertir

Puedes especificar cualquier área rectangular usando la notación A1. En este ejemplo capturamos `A1:D15`, que podría ser una tabla dinámica o un bloque de datos regular.

```java
        // Create a range object for cells A1:D15
        Range pivotRange = worksheet.getCells().createRange("A1:D15");
```

*Caso límite*: Cuando el rango incluye celdas combinadas, Aspose.Cells expande automáticamente la imagen para incluir el área combinada.

## Paso 4: Preparar las opciones de imagen PNG

`ImageOrPrintOptions` te permite controlar el formato, la resolución y otros detalles de renderizado. Establecer el formato de guardado a PNG garantiza calidad sin pérdidas.

```java
        // Configure image options – we want a PNG file
        ImageOrPrintOptions imageOptions = new ImageOrPrintOptions();
        imageOptions.setSaveFormat(SaveFormat.PNG);
        // Optional: increase DPI for sharper output (default is 96)
        imageOptions.setImageFormat(ImageFormat.getPng());
        imageOptions.setResolution(150); // 150 DPI for clearer text
```

Aumentar el DPI es útil cuando las celdas de origen contienen fuentes pequeñas o gráficos detallados.

## Paso 5: Limitar el área de renderizado al rango seleccionado

Al asignar el rango como área de impresión, Aspose.Cells renderiza solo esas celdas e ignora el resto de la hoja.

```java
        // Set the print area so only the defined range is rendered
        worksheet.getPageSetup().setPrintArea(pivotRange.getRefersTo());
```

Si omites este paso, toda la hoja se rasterizará, lo que puede consumir memoria y producir una imagen más grande.

## Paso 6: Renderizar el rango y agregar la imagen a la hoja (opcional)

Si deseas incrustar el PNG generado de nuevo en el libro (para propósitos de vista previa), puedes agregarlo como una imagen. Este paso es opcional para escenarios de exportación pura.

```java
        // Add the rendered image back to the worksheet at cell (0,0) – optional
        worksheet.getPictures().add(0, 0, imageOptions);
```

*Por qué podrías hacerlo*: Algunos flujos de trabajo requieren que la imagen sea parte del libro antes de la distribución, como crear un informe imprimible que mezcle celdas nativas e imágenes.

## Paso 7: Guardar el archivo PNG en disco

Finalmente, escribe la imagen en un archivo. El método `save` respeta el formato especificado en `imageOptions`.

```java
        // Save the rendered PNG image to the specified path
        workbook.save("YOUR_DIRECTORY/PivotImage.png", SaveFormat.PNG);
    }
}
```

Cuando el programa termine, `PivotImage.png` contendrá una captura pixel‑perfecta de las celdas `A1:D15`.

### Resultado esperado

* Un archivo llamado `PivotImage.png` ubicado en `YOUR_DIRECTORY`.
* La imagen muestra el diseño exacto, fuentes, colores y bordes del rango seleccionado.
* Si el rango de origen contiene una tabla dinámica, la imagen renderizada incluye el mismo estilo y los valores calculados tal como se muestran en Excel.

## Manejo de escenarios comunes

### Exportar un rango no contiguo

Aspose.Cells no renderiza rangos disjuntos en una sola imagen. Para exportar múltiples áreas, crea imágenes separadas para cada rango y combínalas después con una biblioteca de procesamiento de imágenes (p. ej., ImageIO).

```java
Range first = worksheet.getCells().createRange("A1:B10");
Range second = worksheet.getCells().createRange("D1:E10");
// Render each range individually using the same ImageOrPrintOptions
```

### Guardar una hoja grande como PNG

Renderizar una hoja completa que abarca miles de filas puede consumir mucha memoria. Mitígualo mediante:

* Reducir el DPI (`imageOptions.setResolution(72)`) para un archivo más pequeño.
* Usar `setPageCount` para limitar la cantidad de páginas renderizadas.
* Exportar una página imprimible a la vez mediante `worksheet.getPageSetup().setPrintArea(...)`.

### Preservar fórmulas de celdas

Una imagen PNG es un formato raster; las fórmulas no se conservan. Si los consumidores posteriores necesitan los datos sin procesar, también exporta el rango como CSV o JSON usando `Range.exportDataTable()`.

## Ejemplo completo y ejecutable

A continuación se muestra la clase Java completa que puedes copiar y pegar en tu IDE. Reemplaza `YOUR_DIRECTORY` con una ruta absoluta o relativa en tu máquina.

```java
import com.aspose.cells.*;

public class PivotRangeToPng {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load the workbook containing the data
        Workbook workbook = new Workbook("YOUR_DIRECTORY/PivotWithStyle.xlsx");

        // 2️⃣ Access the first worksheet (adjust index or name as needed)
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // 3️⃣ Define the exact cell range you want to convert (A1:D15 in this case)
        Range pivotRange = worksheet.getCells().createRange("A1:D15");

        // 4️⃣ Prepare PNG image options – set format and optional resolution
        ImageOrPrintOptions imageOptions = new ImageOrPrintOptions();
        imageOptions.setSaveFormat(SaveFormat.PNG);
        imageOptions.setResolution(150); // sharper output

        // 5️⃣ Restrict rendering to the selected range
        worksheet.getPageSetup().setPrintArea(pivotRange.getRefersTo());

        // 6️⃣ (Optional) Add the rendered image back to the worksheet for preview
        worksheet.getPictures().add(0, 0, imageOptions);

        // 7️⃣ Save the PNG file – this creates the final image on disk
        workbook.save("YOUR_DIRECTORY/PivotImage.png", SaveFormat.PNG);
    }
}
```

Ejecuta el programa con `mvn compile exec:java` (o tu herramienta de compilación preferida). Después de la ejecución, abre `PivotImage.png` para verificar el resultado.

## Conclusión

Ahora sabes cómo **crear PNG a partir de un rango** en Java usando Aspose.Cells, efectivamente **exportar datos como PNG** y **guardar la imagen del rango de Excel** para cualquier escenario de informes o compartición. Los pasos—cargar el libro, definir el rango, configurar las opciones de imagen, establecer el área de impresión y guardar el archivo—cubren todo el flujo de trabajo para **convertir una hoja a PNG** y **guardar celdas como PNG**.

### Próximos pasos

* Experimenta con diferentes valores de `Resolution` para equilibrar calidad y tamaño de archivo.
* Usa `ImageOrPrintOptions.setTransparent(true)` si necesitas un PNG con fondo transparente.
* Combina múltiples imágenes de rango en un solo PDF usando `PdfSaveOptions` para informes de varias páginas.
* Explora la exportación a otros formatos raster (JPEG, BMP) cambiando `setSaveFormat`.

¡Siéntete libre de adaptar este patrón a gráficos, tablas o incluso hojas completas. ¡Feliz codificación!

## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que se basan en las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y funcionales con explicaciones paso a paso para ayudarte a dominar funciones adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Cómo exportar una hoja de Excel a PNG usando Aspose.Cells Java](/cells/english/java/workbook-operations/export-excel-to-png-aspose-cells-java/)
- [Convertir Excel a PNG usando Aspose.Cells para Java: Guía paso a paso](/cells/english/java/workbook-operations/convert-excel-to-png-aspose-cells-java/)
- [Crear rango de unión en Excel usando Aspose.Cells Java: Guía completa](/cells/english/java/range-management/create-union-range-excel-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}