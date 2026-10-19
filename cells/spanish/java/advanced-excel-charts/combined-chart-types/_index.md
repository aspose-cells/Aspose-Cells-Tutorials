---
date: 2026-09-02
description: Aprenda cómo exportar un gráfico a PNG, agregar series de datos, combinar
  gráfico de líneas y columnas, guardar el libro de trabajo como XLSX y agregar una
  leyenda al gráfico usando Aspose.Cells for Java.
keywords:
- export chart to png
- combine line and column chart
- save workbook as xlsx
- generate chart image java
lastmod: 2026-09-02
linktitle: Exportar gráfico a PNG y agregar series de datos para gráfico combinado
og_description: Exportar gráfico a PNG con Aspose.Cells for Java, combinar gráfico
  de líneas y columnas, agregar series de datos y guardar el libro de trabajo como
  XLSX en un solo tutorial.
og_image_alt: Developer guide showing combined line‑column chart export to PNG using
  Aspose.Cells for Java
og_title: Exportar gráfico a PNG y agregar series de datos para gráfico combinado
schemas:
- author: Aspose
  dateModified: '2026-09-02'
  description: Learn how to export chart to PNG, add data series, combine line column
    chart, save workbook as XLSX and add legend chart using Aspose.Cells for Java.
  headline: Export chart to PNG and add data series for combined chart
  type: TechArticle
- description: Learn how to export chart to PNG, add data series, combine line column
    chart, save workbook as XLSX and add legend chart using Aspose.Cells for Java.
  name: Export chart to PNG and add data series for combined chart
  steps:
  - name: import aspose.cells classes
    text: '`Workbook` is Aspose.Cells’ core object that represents an entire Excel
      file in memory.'
  - name: create a new workbook
    text: '`Worksheet` represents a single sheet inside a `Workbook` and provides
      access to cells, rows, and charts.'
  - name: access the first worksheet
    text: '`Chart` is the object that holds all chart‑related settings, series, and
      rendering options.'
  - name: add a combined chart object to the worksheet
    text: We’ll start with a line chart and later add a column series to achieve a
      **combined line column chart** effect.
  - name: define the data ranges and add data series
    text: '`NSeries` is the collection that stores each data series for a chart. Adding
      a series links a range of cells to the chart. > **Pro tip:** The first parameter
      (`"A1:A5"`) is the range for the first series, and the second (`"B1:B5"`) creates
      a second series that will be combined with the first.'
  - name: set the category (X‑axis) data
    text: '`CategoryAxis` represents the horizontal axis of the chart, controlling
      the labels displayed along the X‑axis.'
  - name: set chart axis labels and title
    text: '`Title` sets the main title of the chart, and `Axis` objects represent
      the X and Y axes.'
  - name: add legend chart and adjust its position
    text: '`Legend` controls the placement and appearance of the series legend in
      the chart.'
  - name: save the workbook as an Excel file (XLSX)
    text: '`Workbook.save` writes the in‑memory workbook to a file in the specified
      format.'
  - name: export chart to PNG
    text: '`Chart.toImage` renders the chart as an image file in the chosen format.
      > The `chart.toImage` method **generates Excel chart** images that can be used
      in web pages, reports, or emails.'
  type: HowTo
- questions:
  - answer: 'Download the JAR from the official site and add it to your project’s
      classpath. The download link is: [Download Aspose.Cells for Java](https://releases.aspose.com/cells/java/).'
    question: How do I install Aspose.Cells for Java?
  - answer: Yes, Aspose.Cells supports bar, pie, scatter, area, and many more chart
      types. Refer to the API documentation for the full list.
    question: Can I create other chart types besides line and column?
  - answer: A valid Aspose.Cells license is required for production deployments. A
      free trial is available for evaluation.
    question: Is a license required for production use?
  - answer: Use `chart.getNSeries().get(i).setAreaColor(Color.getRed())` (or similar)
      after adding the series.
    question: How can I change the colors of each series?
  - answer: 'Comprehensive documentation and additional samples are available at the
      Aspose reference site: [Aspose Cells Java reference documentation](https://reference.aspose.com/cells/java/).'
    question: Where can I find more code examples?
  type: FAQPage
second_title: Aspose.Cells Java Excel Processing API
tags:
- export chart to png
- Aspose.Cells
- Java Excel charts
title: Exportar gráfico a PNG y agregar series de datos para gráfico combinado
url: /es/java/advanced-excel-charts/combined-chart-types/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Exportar gráfico a PNG y agregar series de datos para gráfico combinado

En este tutorial **agregarás series de datos** a un libro de Excel, **combinarás elementos de gráfico de líneas y columnas**, y aprenderás cómo **exportar el gráfico a PNG** usando Aspose.Cells for Java. Recorreremos cada paso—desde configurar el libro, agregar el gráfico a una hoja de cálculo, personalizar la leyenda, hasta **guardar el libro como XLSX** y generar una imagen PNG del gráfico. Al final, tendrás un gráfico combinado listo para usar que podrás incrustar en informes o paneles.

## Respuestas rápidas
- **¿Qué biblioteca crea gráficos combinados?** Aspose.Cells for Java.  
- **¿Cómo agrego una serie de datos?** Llama a `chart.getNSeries().add(...)` con el rango apropiado.  
- **¿Cómo puedo exportar el gráfico a PNG?** Usa `chart.toImage("chart.png", ImageFormat.getPng())`.  
- **¿En qué formato de archivo puedo guardar el libro?** `.xlsx` estándar (guardar libro como XLSX).  
- **¿Necesito una licencia para producción?** Sí – se requiere una licencia válida de Aspose.Cells para implementaciones en producción.

## Qué es exportar gráfico a PNG en Aspose.Cells?
Exportar un gráfico a PNG crea una imagen rasterizada del gráfico de Excel que puede mostrarse en páginas web, informes o correos electrónicos sin requerir la aplicación Excel. Este método captura el diseño visual exacto, los colores y los marcadores de datos, produciendo un archivo de imagen portátil.

## ¿Por qué crear un gráfico combinado de línea y columna?
Un gráfico combinado de línea y columna te permite mostrar diferentes conjuntos de datos con representaciones visuales distintas (p. ej., una serie de línea sobre una serie de columnas) en una sola vista. Este enfoque es ideal para comparar tendencias con totales, resaltar correlaciones o ofrecer información más rica manteniendo una huella visual pequeña.

## Requisitos previos
- Java Development Kit (JDK) 8 o superior  
- Aspose.Cells for Java library (descargar desde el enlace a continuación)  
- Familiaridad básica con la sintaxis de Java y conceptos de Excel  

## Getting started

Primero, descarga la biblioteca Aspose.Cells for Java desde el sitio oficial:

[Download Aspose.Cells for Java](https://releases.aspose.com/cells/java/)

Una vez que el JAR se agrega al classpath de tu proyecto, puedes comenzar a crear el gráfico.

### Paso 1: importar clases de aspose.cells
`Workbook` es el objeto central de Aspose.Cells que representa un archivo Excel completo en memoria.  
```java
import com.aspose.cells.*;
```

### Paso 2: crear un nuevo libro de trabajo
`Worksheet` representa una hoja única dentro de un `Workbook` y brinda acceso a celdas, filas y gráficos.  
```java
Workbook workbook = new Workbook();
```

### Paso 3: acceder a la primera hoja de cálculo
`Chart` es el objeto que contiene todas las configuraciones relacionadas con el gráfico, series y opciones de renderizado.  
```java
Worksheet worksheet = workbook.getWorksheets().get(0);
```

### Paso 4: agregar un objeto de gráfico combinado a la hoja de cálculo  
Comenzaremos con un gráfico de líneas y luego agregaremos una serie de columnas para lograr un efecto de **gráfico combinado de línea y columna**.  
```java
int chartIndex = worksheet.getCharts().add(ChartType.LINE, 0, 0, 20, 10);
Chart chart = worksheet.getCharts().get(chartIndex);
```

## Agregar datos al gráfico

Ahora que el contenedor del gráfico existe, necesitamos alimentarlo con datos.

### Paso 5: definir los rangos de datos y agregar series de datos
`NSeries` es la colección que almacena cada serie de datos para un gráfico. Agregar una serie vincula un rango de celdas al gráfico.  
```java
Cells cells = worksheet.getCells();
chart.getNSeries().add("A1:A5", true);
chart.getNSeries().add("B1:B5", true);
```
> **Consejo profesional:** El primer parámetro (`"A1:A5"`) es el rango para la primera serie, y el segundo (`"B1:B5"`) crea una segunda serie que se combinará con la primera.

### Paso 6: establecer los datos de la categoría (eje X)
`CategoryAxis` representa el eje horizontal del gráfico, controlando las etiquetas mostradas a lo largo del eje X.  
```java
chart.getNSeries().setCategoryData("C1:C5");
```

## Personalizar el gráfico

Un buen gráfico cuenta una historia. Démosle títulos, etiquetas de ejes y una leyenda clara.

### Paso 7: establecer etiquetas de ejes y título del gráfico
`Title` establece el título principal del gráfico, y los objetos `Axis` representan los ejes X y Y.  
```java
chart.getTitle().setText("Combined Chart Example");
chart.getCategoryAxis().getTitle().setText("Categories");
chart.getValueAxis().getTitle().setText("Values");
```

### Paso 8: agregar la leyenda del gráfico y ajustar su posición
`Legend` controla la ubicación y apariencia de la leyenda de series en el gráfico.  
```java
chart.getLegend().setPosition(LegendPositionType.BOTTOM);
chart.getLegend().setOverlay(true);
```

## Guardar y exportar el gráfico

Después de personalizar, querrás **guardar el libro como XLSX** y también generar una imagen.

### Paso 9: guardar el libro como archivo Excel (XLSX)
`Workbook.save` escribe el libro en memoria a un archivo en el formato especificado.  
```java
workbook.save("CombinedChart.xlsx");
```

### Paso 10: exportar el gráfico a PNG
`Chart.toImage` renderiza el gráfico como un archivo de imagen en el formato elegido.  
```java
chart.toImage("CombinedChart.png", ImageFormat.getPng());
```
> El método `chart.toImage` **genera imágenes de gráficos de Excel** que pueden usarse en páginas web, informes o correos electrónicos.

## Problemas comunes y solución de problemas

| Problema | Solución |
|----------|----------|
| **No aparecen datos** | Verifica que los rangos de celdas (`A1:A5`, `B1:B5`, `C1:C5`) realmente contengan datos antes de crear el gráfico. |
| **La leyenda se superpone al gráfico** | Establece `chart.getLegend().setOverlay(false)` o mueve la leyenda a una posición diferente (p. ej., `RIGHT`). |
| **El archivo de imagen está vacío** | Asegúrate de que el gráfico tenga al menos una serie y que `chart.toImage` se llame después de todas las personalizaciones. |
| **Al guardar se lanza una excepción** | Comprueba que tienes permisos de escritura en el directorio de destino y que el archivo no esté abierto en Excel. |

## Preguntas frecuentes

**P: ¿Cómo instalo Aspose.Cells for Java?**  
R: Descarga el JAR del sitio oficial y agrégalo al classpath de tu proyecto. El enlace de descarga es: [Download Aspose.Cells for Java](https://releases.aspose.com/cells/java/).

**P: ¿Puedo crear otros tipos de gráficos además de línea y columna?**  
R: Sí, Aspose.Cells admite gráficos de barras, pastel, dispersión, área y muchos más tipos de gráficos. Consulta la documentación de la API para la lista completa.

**P: ¿Se requiere una licencia para uso en producción?**  
R: Se requiere una licencia válida de Aspose.Cells para implementaciones en producción. Hay una prueba gratuita disponible para evaluación.

**P: ¿Cómo puedo cambiar los colores de cada serie?**  
R: Usa `chart.getNSeries().get(i).setAreaColor(Color.getRed())` (o similar) después de agregar la serie.

**P: ¿Dónde puedo encontrar más ejemplos de código?**  
R: La documentación completa y ejemplos adicionales están disponibles en el sitio de referencia de Aspose: [Aspose Cells Java reference documentation](https://reference.aspose.com/cells/java/).

**Última actualización:** 2026-09-02  
**Probado con:** la última versión de Aspose.Cells for Java  
**Autor:** Aspose

## Tutoriales relacionados

- [Cómo agregar etiquetas a los gráficos de Excel usando Aspose.Cells for Java](/cells/java/charts-graphs/adding-labels-to-charts-aspose-cells-java-tutorial/)
- [Cómo crear un gráfico de Excel con línea de tendencia y exportarlo a imagen usando Aspose.Cells for Java](/cells/java/advanced-excel-charts/trendline-analysis/)
- [Exportar gráficos de Excel a PDF usando Aspose.Cells for Java: Guía de tamaños de página personalizados](/cells/java/charts-graphs/export-excel-charts-pdf-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}