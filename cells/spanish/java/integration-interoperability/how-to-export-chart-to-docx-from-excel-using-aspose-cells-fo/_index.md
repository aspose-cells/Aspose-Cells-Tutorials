---
category: general
date: 2026-08-20
description: Aprenda cómo exportar un gráfico a docx y convertir un libro de Excel
  a docx con Aspose.Cells en Java. Guía paso a paso con código completo.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export chart to docx
- convert excel workbook to docx
- Aspose.Cells Java
- editable chart DOCX
- Excel to Word conversion
language: es
lastmod: 2026-08-20
og_description: Exporta el gráfico a docx y convierte el libro de Excel a docx usando
  Aspose.Cells para Java. Sigue este tutorial completo y ejecutable.
og_image_alt: Screenshot showing a Java code editor exporting an Excel chart to a
  DOCX file
og_title: Exportar gráfico a docx con Aspose.Cells – Guía de Java
schemas:
- author: Aspose
  dateModified: '2026-08-20'
  description: Learn how to export chart to docx and convert Excel workbook to docx
    with Aspose.Cells in Java. Step‑by‑step guide with complete code.
  headline: How to export chart to docx from Excel using Aspose.Cells for Java
  type: TechArticle
tags:
- Aspose.Cells
- Java
- DOCX
- Excel
title: Cómo exportar un gráfico a docx desde Excel usando Aspose.Cells para Java
url: /es/java/integration-interoperability/how-to-export-chart-to-docx-from-excel-using-aspose-cells-fo/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Exportar gráfico a docx desde un libro de Excel usando Java

Si necesita **exportar gráfico a docx** directamente desde un archivo de Excel, este tutorial le muestra una solución lista para ejecutar. Al final de la guía también sabrá cómo **convertir libro de Excel a docx** conservando un gráfico editable, de modo que el documento Word resultante pueda modificarse sin perder fidelidad.

Exportar gráficos es común cuando genera informes que combinan cálculos de hojas de cálculo con diseños ricos de Word. Aspose.Cells for Java hace que la conversión sea sencilla, y la API le permite mantener el gráfico editable—no se requiere una imagen estática.

## Qué cubre este tutorial

* Cargar un libro existente que contiene un gráfico.  
* Configurar `ImageOrPrintOptions` para dirigirse al formato DOCX.  
* Habilitar la bandera `ExportEditableCharts` (disponible a partir de la versión 25.10).  
* Guardar el libro como un archivo DOCX que conserva un gráfico editable.  

No se necesitan herramientas externas más allá del JAR de Aspose.Cells. El código funciona con Java 8+ y cualquier versión reciente de Aspose.Cells.

## Requisitos previos

| Requirement | Why it matters |
|-------------|----------------|
| **Aspose.Cells for Java** (v25.10 or later) | La característica `setExportEditableCharts` se introdujo en esta versión. |
| **Java Development Kit (JDK) 8 or newer** | Proporciona el tiempo de ejecución para compilar y ejecutar el ejemplo. |
| **An Excel workbook (`.xlsx`) that contains at least one chart** | Un libro de Excel (`.xlsx`) que contiene al menos un gráfico. |
| **A Java IDE or build tool (e.g., Maven, Gradle)** | Un IDE de Java o herramienta de compilación (p. ej., Maven, Gradle) simplifica la gestión de dependencias y la ejecución. |

Puede descargar el último JAR de Aspose.Cells desde el [sitio web de Aspose](https://products.aspose.com/cells/java/).

## Paso 1: Configurar el proyecto y agregar la dependencia de Aspose.Cells

Si usa Maven, agregue la siguiente dependencia a su `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.10</version> <!-- use the latest version -->
</dependency>
```

Para Gradle, agregue:

```gradle
implementation 'com.aspose:aspose-cells:25.10'
```

> **Consejo profesional:** Use la versión exacta que introdujo `ExportEditableCharts` (25.10) o cualquier versión más reciente. Las versiones anteriores ignorarán la bandera y producirán una imagen estática.

## Paso 2: Cargar el libro que contiene el gráfico

La clase `Workbook` representa todo el archivo de Excel. Cargarlo es una operación de una sola línea:

```java
import com.aspose.cells.*;

public class ExportEditableChartToDocx {
    public static void main(String[] args) throws Exception {
        // Load the workbook with the chart you want to export
        Workbook workbook = new Workbook("YOUR_DIRECTORY/ChartWorkbook.xlsx");
```

> **Por qué es importante:** El libro debe estar completamente cargado antes de que pueda aplicar cualquier opción de exportación. Si la ruta del archivo es incorrecta, Aspose.Cells lanza una `FileNotFoundException`.

## Paso 3: Configurar las opciones de imagen/impresión para la salida DOCX

`ImageOrPrintOptions` controla cómo se renderiza el libro. Establecer el formato de guardado a `DOCX` indica a Aspose.Cells que produzca un documento Word en lugar de una imagen.

```java
        // Create options and specify DOCX as the target format
        ImageOrPrintOptions options = new ImageOrPrintOptions();
        options.setSaveFormat(SaveFormat.DOCX);
```

También puede ajustar el tamaño de página, DPI o calidad de imagen aquí, pero son opcionales para la exportación del gráfico.

## Paso 4: Habilitar la exportación de gráficos editables

A partir de la versión 25.10, Aspose.Cells puede incrustar gráficos como objetos de gráfico nativos de Word. Esto los hace totalmente editables en Microsoft Word.

```java
        // Turn on the editable chart export flag
        options.setExportEditableCharts(true);
```

> **Caso límite:** Si establece esta bandera a `false` (o la omite), el gráfico se renderizará como una imagen estática. Use `true` solo cuando la audiencia objetivo necesite editar el gráfico después de la conversión.

## Paso 5: Guardar el libro como un archivo DOCX

Finalmente, invoque `Workbook.save` con las opciones configuradas:

```java
        // Save the workbook as a DOCX document that contains an editable chart
        workbook.save("YOUR_DIRECTORY/ChartEditable.docx", options);
    }
}
```

Cuando el programa termine, abra `ChartEditable.docx` en Microsoft Word. Debería ver el gráfico original y, si hace clic derecho sobre él, la opción **Edit Data** estará disponible—confirmando que el gráfico es realmente editable.

## Ejemplo completo y ejecutable

A continuación se muestra el archivo fuente completo. Cópialo en su IDE, reemplace `YOUR_DIRECTORY` con una ruta absoluta o relativa, y ejecútelo.

```java
import com.aspose.cells.*;

public class ExportEditableChartToDocx {
    public static void main(String[] args) throws Exception {
        // Step 1: Load the workbook that contains the chart
        Workbook workbook = new Workbook("YOUR_DIRECTORY/ChartWorkbook.xlsx");

        // Step 2: Create image/print options and set the target format to DOCX
        ImageOrPrintOptions options = new ImageOrPrintOptions();
        options.setSaveFormat(SaveFormat.DOCX);

        // Step 3: Enable exporting of editable charts (available from version 25.10)
        options.setExportEditableCharts(true);

        // Step 4: Save the workbook as a DOCX document with the configured options
        workbook.save("YOUR_DIRECTORY/ChartEditable.docx", options);
    }
}
```

**Salida esperada**

* Un archivo llamado `ChartEditable.docx` en el directorio especificado.  
* Al abrir el archivo en Word se muestra el gráfico exactamente como apareció en Excel, y puede hacer doble clic en el gráfico para editar sus series de datos.

## Problemas comunes y cómo evitarlos

| Symptom | Cause | Fix |
|---------|-------|-----|
| Word muestra una **imagen estática** en lugar de un gráfico editable | `setExportEditableCharts` no se llamó o se está usando una versión < 25.10 | Asegúrese de que la bandera esté establecida en `true` y que esté usando Aspose.Cells 25.10 o una versión más reciente. |
| El DOCX generado está **en blanco** | Ruta de archivo incorrecta para el libro fuente o permisos insuficientes | Verifique la ruta del libro y que la aplicación tenga acceso de lectura/escritura. |
| El diseño del gráfico se ve **distorsionado** | Configuración de página en Excel (p. ej., filas/columnas ocultas) difiere de los valores predeterminados de Word | Ajuste `ImageOrPrintOptions` (p. ej., `setOnePagePerSheet(true)`) para controlar el escalado. |
| **Rendimiento** disminuye en libros grandes | Exportar muchos gráficos o conjuntos de datos grandes | Exporte solo las hojas necesarias o use `setSheetIndex` para limitar el procesamiento. |

## Extender la solución

* **Múltiples gráficos:** Iterar sobre todas las hojas de cálculo y llamar a `worksheet.getCharts()` para exportar cada gráfico individualmente.  
* **Estilizado personalizado de DOCX:** Después de guardar, use Aspose.Words para aplicar encabezados, pies de página o estilos al documento generado.  
* **Conversión por lotes:** Encapsular el código en un bucle que procese un directorio de archivos `.xlsx`, produciendo un DOCX para cada uno.

## Conclusión

Ahora tiene un método fiable para **exportar gráfico a docx** y **convertir libro de Excel a docx** mientras preserva la plena editabilidad del gráfico. Los pasos clave son cargar el libro, configurar `ImageOrPrintOptions` para DOCX, habilitar `ExportEditableCharts` y guardar el resultado.

Experimente con opciones adicionales—como establecer márgenes de página o incrustar las fórmulas del libro—para adaptar la salida a su flujo de trabajo de informes. Cuando necesite generar informes Word a partir de datos de Excel de forma programática, este enfoque ofrece una solución limpia y mantenible.

--- 

*¿Listo para probarlo? Clone el ejemplo, actualice las rutas de los archivos y ejecute el programa. Si encuentra algún problema, consulte la documentación de Aspose.Cells for Java o explore los temas relacionados a continuación.*  

### Temas relacionados que podría explorar a continuación

* **convert excel workbook to pdf** – generar informes PDF a partir del mismo libro.  
* **Aspose.Cells chart formatting** – personalizar colores, marcadores y ejes antes de la exportación.  
* **Embedding images in DOCX with Aspose.Words** – combinar gráficos con otro contenido de Word.  

¡Feliz codificación!

## ¿Qué debería aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que se basan en las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y funcionales con explicaciones paso a paso para ayudarle a dominar funciones adicionales de la API y explorar enfoques de implementación alternativos en sus propios proyectos.

- [Cómo crear un gráfico de Excel con línea de tendencia y exportarlo a imagen usando Aspose.Cells for Java](/cells/english/java/advanced-excel-charts/trendline-analysis/)
- [Automatizar el acceso a gráficos de Excel usando Aspose.Cells Java: Guía paso a paso](/cells/english/java/charts-graphs/excel-charts-access-aspose-cells-java/)
- [Personalizar etiquetas de datos de gráficos de Excel usando Aspose.Cells for Java: Guía paso a paso](/cells/english/java/charts-graphs/customize-chart-data-labels-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}