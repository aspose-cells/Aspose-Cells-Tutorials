---
date: 2026-08-27
description: Aprenda cómo agregar una trendline al chart, mostrar su valor R‑squared
  y exportar el chart como una imagen PNG o JPEG usando Aspose.Cells for Java.
keywords:
- add trendline to chart
- save chart as image
- export excel chart image
- java create excel workbook
- convert chart to png
lastmod: 2026-08-27
linktitle: Exportar chart a imagen con análisis de trendline
og_description: Agregar trendline al chart, ver R‑squared y exportar el resultado
  como PNG/JPEG usando Aspose.Cells for Java – una solución rápida y de 50 formatos.
og_image_alt: Guide showing Java code to add a trendline to an Excel chart and export
  it as an image
og_title: Agregar trendline al chart y exportarlo como imagen con Aspose.Cells for
  Java
schemas:
- author: Aspose
  dateModified: '2026-08-27'
  description: Learn how to add trendline to chart, display its R‑squared value, and
    export the chart as a PNG or JPEG image using Aspose.Cells for Java.
  headline: How to add trendline to chart and export as image in Java
  type: TechArticle
- description: Learn how to add trendline to chart, display its R‑squared value, and
    export the chart as a PNG or JPEG image using Aspose.Cells for Java.
  name: How to add trendline to chart and export as image in Java
  steps:
  - name: set up the project
    text: Create a new Java project and place the Aspose.Cells JARs on the build path.
      This prepares the environment for generating and manipulating Excel files.
  - name: load excel file (load excel file java)
    text: '*We’ve just **loaded an Excel file** into memory, ready for chart creation.*'
  - name: create a chart
    text: '*Here we generate a line chart that will later host our trendline.*'
  - name: add trendline (how to add trendline) and display R‑squared value
    text: '*The `setDisplayRSquaredValue(true)` call ensures the **R‑squared value**
      appears on the chart.*'
  - name: customize chart and save workbook (save workbook xlsx, generate excel file
      java)
    text: '*Now the workbook is **generated** and saved as an XLSX file, ready for
      further processing.*'
  - name: export chart to image (export chart to image)
    text: '> **Note:** This step is described without an additional code block to
      keep the original block count unchanged. After the chart is created and saved,
      you can export it to an image by calling the `chart.toImage()` method and writing
      the resulting `java.awt.image.BufferedImage` to a file format of you'
  type: HowTo
- questions:
  - answer: Use a different `TrendlineType` enumeration when adding the trendline,
      e.g., `TrendlineType.POLYNOMIAL` for a polynomial fit.
    question: How can I change the trendline type?
  - answer: Yes. Access the trendline’s `LineFormat` via `trendline.getLineFormat()`
      and set properties such as `setWeight()` and `setColor()`.
    question: Can I customize the trendline appearance (color, thickness)?
  - answer: Convert the chart to an image first, then embed that image into a PDF
      using Aspose.PDF or any other PDF library.
    question: How do I export the chart to PDF instead of an image?
  - answer: Absolutely. Call `chart.getNSeries().get(0).getTrendlines().add(...)`
      for each series you wish to analyze.
    question: Is it possible to add multiple trendlines to the same chart?
  - answer: Yes. You can specify the DPI when calling `chart.toImage()` and then scale
      the image before saving, ensuring crisp output for print or high‑density screens.
    question: Does Aspose.Cells support high‑resolution image export?
  type: FAQPage
second_title: Aspose.Cells Java Excel Processing API
tags:
- Aspose.Cells
- Java charting
- Excel automation
- trendline analysis
title: Cómo agregar una trendline al chart y exportarlo como imagen en Java
url: /es/java/advanced-excel-charts/trendline-analysis/
weight: 15
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Agregar línea de tendencia al gráfico y exportarlo como una imagen

En este tutorial aprenderá cómo **agregar una línea de tendencia al gráfico**, mostrar el valor R‑cuadrado y exportar la visualización a un archivo PNG o JPEG usando Aspose.Cells for Java. Verá por qué las líneas de tendencia son importantes, cómo preparar el libro de trabajo y los pasos exactos para generar una imagen de alta resolución que se pueda incrustar en informes, correos electrónicos o páginas web.

## Respuestas rápidas
- **¿Cuál es el objetivo principal de esta guía?** Mostrarle cómo agregar una línea de tendencia al gráfico, mostrar su ecuación y el valor R‑cuadrado, y exportar el gráfico como una imagen con Java.  
- **¿Qué biblioteca necesito?** Aspose.Cells for Java – descárguela desde la [página de lanzamiento de Aspose.Cells for Java](https://releases.aspose.com/cells/java/).  
- **¿Necesito una licencia para desarrollo?** Una prueba gratuita funciona para desarrollo; se requiere una licencia comercial para implementaciones en producción.  
- **¿Puedo generar el libro de trabajo de Excel programáticamente?** Sí – el tutorial crea y guarda un libro de trabajo XLSX desde cero.  
- **¿Cómo se exporta el gráfico a PNG o JPEG?** Llame al método `Chart.toImage()` y escriba el `BufferedImage` devuelto con `ImageIO.write(...)`.

## ¿Cómo crear un gráfico de Excel con una línea de tendencia y exportarlo como imagen?
Cargue el libro de trabajo, agregue un gráfico de líneas, adjunte una línea de tendencia que muestre la ecuación y el valor R‑cuadrado, guarde el libro de trabajo y luego llame a `chart.toImage()` y escriba el `BufferedImage` resultante en un archivo PNG o JPEG. Este flujo de extremo a extremo requiere solo unas pocas líneas de código Java y produce una imagen perfecta a nivel de píxel adecuada para cualquier aplicación posterior.

## ¿Qué es exportar un gráfico a imagen?
Exportar un gráfico a una imagen convierte la representación visual de sus datos en un mapa de bits portátil (PNG, JPEG, BMP, etc.). Este formato es ideal para incrustar gráficos en informes, páginas web o presentaciones donde no se requiere el archivo Excel original.

## ¿Por qué agregar una línea de tendencia y mostrar el valor R‑cuadrado?
Una línea de tendencia revela el patrón subyacente de una serie de datos, mientras que la métrica **R‑cuadrado** cuantifica qué tan bien la línea de tendencia se ajusta a los datos. Incluir ambos en la imagen exportada brinda a los interesados una visión inmediata sin abrir el libro de trabajo. Ayuda a los tomadores de decisiones a evaluar rápidamente la fuerza de la correlación y a pronosticar tendencias sin necesidad de abrir Excel.

## Requisitos previos
- Java 8 o superior instalado en su máquina de desarrollo.  
- Biblioteca Aspose.Cells for Java añadida al classpath del proyecto (archivos JAR).  
- Familiaridad con un IDE de Java como IntelliJ IDEA o Eclipse.  

## Guía paso a paso

### Paso 1: configurar el proyecto
Cree un nuevo proyecto Java y coloque los JAR de Aspose.Cells en la ruta de compilación. Esto prepara el entorno para generar y manipular archivos Excel.

### Paso 2: cargar archivo Excel (cargar archivo excel java)
```java
// Import necessary libraries
import com.aspose.cells.*;

// Load the Excel file
Workbook workbook = new Workbook("your_excel_file.xlsx");

// Access the worksheet
Worksheet worksheet = workbook.getWorksheets().get(0);
```
*Acabamos de **cargar un archivo Excel** en memoria, listo para crear el gráfico.*

### Paso 3: crear un gráfico
```java
// Create a chart
int chartIndex = worksheet.getCharts().add(ChartType.LINE, 5, 0, 15, 5);
Chart chart = worksheet.getCharts().get(chartIndex);

// Specify data source for the chart
chart.getNSeries().add("A1:A10", true);
```
*Aquí generamos un gráfico de líneas que más adelante alojará nuestra línea de tendencia.*

### Paso 4: agregar línea de tendencia (cómo agregar línea de tendencia) y mostrar el valor R‑cuadrado
```java
// Add a trendline to the chart
Trendline trendline = chart.getNSeries().get(0).getTrendlines().add(TrendlineType.LINEAR);

// Customize trendline options
trendline.setDisplayEquation(true);
trendline.setDisplayRSquaredValue(true);
```
*La llamada `setDisplayRSquaredValue(true)` garantiza que el **valor R‑cuadrado** aparezca en el gráfico.*

### Paso 5: personalizar el gráfico y guardar el libro de trabajo (guardar libro de trabajo xlsx, generar archivo excel java)
```java
// Customize chart title and axes
chart.getTitle().setText("Trendline Analysis");
chart.getCategoryAxis().getTitle().setText("X-Axis");
chart.getValueAxis().getTitle().setText("Y-Axis");

// Save the Excel file with the chart
workbook.save("output.xlsx");
```
*Ahora el libro de trabajo está **generado** y guardado como un archivo XLSX, listo para procesamiento adicional.*

### Paso 6: exportar gráfico a imagen (exportar gráfico a imagen)
> **Nota:** Este paso se describe sin un bloque de código adicional para mantener el recuento original de bloques.  
Después de que el gráfico se haya creado y guardado, puede exportarlo a una imagen llamando al método `chart.toImage()` y escribiendo el `java.awt.image.BufferedImage` resultante en el formato de archivo que elija (PNG, JPEG, BMP). El flujo de trabajo típico es:
1. Obtener el objeto `Chart` (ya hecho en pasos anteriores).  
2. Llamar a `chart.toImage()` para obtener un `BufferedImage`.  
3. Usar `ImageIO.write(bufferedImage, "png", new File("chart.png"))` para escribir el archivo.  

El objeto `Chart` representa un gráfico en el libro de trabajo y proporciona métodos para modificar su apariencia y datos. `BufferedImage` es una clase Java que almacena una imagen en memoria, permitiendo guardarla en un archivo. `ImageIO` es una clase de utilidad para leer y escribir imágenes en Java. `setDisplayRSquaredValue` permite mostrar la estadística R‑cuadrado en la línea de tendencia.

### Analizar resultados
Abra `output.xlsx` en Excel para verificar que la línea de tendencia, la ecuación y el valor R‑cuadrado aparezcan como se espera. Abra el archivo de imagen exportado (p. ej., `chart.png`) para ver una visualización limpia que se puede compartir sin el libro de trabajo original.

## Problemas comunes y soluciones
- **La línea de tendencia no se muestra:** Asegúrese de que el rango de datos (`A1:A10`) contenga valores numéricos; los datos no numéricos impiden el cálculo de la línea de tendencia.  
- **El valor R‑cuadrado se muestra como 0:** Esto a menudo indica que la serie de datos es constante o carece de variación. Pruebe con un conjunto de datos diferente o use una línea de tendencia polinómica.  
- **La exportación de la imagen falla con `NullPointerException`:** Verifique que el gráfico se haya renderizado completamente antes de llamar a `toImage()`. Guardar el libro de trabajo primero a veces puede resolver problemas de sincronización.

## Preguntas frecuentes

**P: ¿Cómo puedo cambiar el tipo de línea de tendencia?**  
R: Use una enumeración `TrendlineType` diferente al agregar la línea de tendencia, por ejemplo, `TrendlineType.POLYNOMIAL` para un ajuste polinómico.

**P: ¿Puedo personalizar la apariencia de la línea de tendencia (color, grosor)?**  
R: Sí. Acceda al `LineFormat` de la línea de tendencia mediante `trendline.getLineFormat()` y establezca propiedades como `setWeight()` y `setColor()`.

**P: ¿Cómo exporto el gráfico a PDF en lugar de una imagen?**  
R: Convierta el gráfico a una imagen primero, luego incruste esa imagen en un PDF usando Aspose.PDF o cualquier otra biblioteca PDF.

**P: ¿Es posible agregar múltiples líneas de tendencia al mismo gráfico?**  
R: Absolutamente. Llame a `chart.getNSeries().get(0).getTrendlines().add(...)` para cada serie que desee analizar.

**P: ¿Aspose.Cells admite la exportación de imágenes de alta resolución?**  
R: Sí. Puede especificar los DPI al llamar a `chart.toImage()` y luego escalar la imagen antes de guardarla, garantizando una salida nítida para impresión o pantallas de alta densidad.

---

**Última actualización:** 2026-08-27  
**Probado con:** Aspose.Cells for Java latest (soporta más de 50 formatos de archivo y procesa libros de trabajo con hasta 2 millones de filas sin cargar toda la memoria)  
**Autor:** Aspose

## Tutoriales relacionados

- [Agregar etiquetas de datos al gráfico de Excel con Aspose.Cells Java](/cells/java/advanced-excel-charts/chart-interactivity/)
- [Cómo exportar gráficos de Excel como SVG usando Aspose.Cells Java para gráficos vectoriales escalables](/cells/java/charts-graphs/export-excel-charts-svg-aspose-cells-java/)
- [Exportar gráficos de Excel a PDF usando Aspose.Cells for Java&#58; Guía de tamaños de página personalizados](/cells/java/charts-graphs/export-excel-charts-pdf-aspose-cells-java/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}