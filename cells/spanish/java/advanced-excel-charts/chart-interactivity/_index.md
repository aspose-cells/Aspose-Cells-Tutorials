---
date: 2026-08-21
description: Aprenda cómo agregar tooltips, data labels y cambiar el tipo de gráfico
  en los gráficos de Excel usando Aspose.Cells for Java – guía paso a paso con ejemplos
  interactivos.
keywords:
- how to add tooltips
- how to change chart type
- how to add data labels
lastmod: 2026-08-21
linktitle: Cambiar tipo de gráfico de Excel
og_description: Aprenda cómo agregar tooltips, data labels y cambiar el tipo de gráfico
  en los gráficos de Excel usando Aspose.Cells for Java – guía paso a paso con ejemplos
  interactivos.
og_image_alt: 'Developer guide: Adding tooltips and data labels to Excel charts with
  Aspose.Cells for Java'
og_title: Cómo agregar tooltips y data labels a los gráficos de Excel en Java
schemas:
- author: Aspose
  dateModified: '2026-08-21'
  description: Learn how to add tooltips, data labels, and change chart type in Excel
    charts using Aspose.Cells for Java – step‑by‑step guide with interactive examples.
  headline: How to add tooltips and data labels to Excel charts in Java
  type: TechArticle
- questions:
  - answer: You need to create a new chart with the desired `ChartType`. Aspose.Cells
      does not provide an in‑place type conversion, so remove the old chart and add
      a new one.
    question: How can I change the chart type after it’s created?
  - answer: Yes. Use the `DataLabel` properties such as `setFontSize`, `setFontColor`,
      and `setBackgroundColor` to style the tooltip text.
    question: Can I customize the appearance of tooltips?
  - answer: Export the workbook to an HTML or XLSX file and use JavaScript on the
      client side to capture click events on chart elements.
    question: How do I handle user interactions in a web application?
  - answer: Visit the [Aspose.Cells Java API Reference](https://reference.aspose.com/cells/java/)
      for a full list of chart‑related classes and methods.
    question: Where can I find more examples and documentation?
  type: FAQPage
second_title: Aspose.Cells Java Excel Processing API
tags:
- Aspose.Cells
- Java chart
- Excel interactivity
- tooltips
- data labels
title: Cómo agregar tooltips y data labels a los gráficos de Excel en Java
url: /es/java/advanced-excel-charts/chart-interactivity/
weight: 19
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Agregar etiquetas de datos al gráfico de Excel y cambiar el tipo de gráfico – Aspose.Cells Java

Los gráficos interactivos brindan a sus informes de Excel un nuevo nivel de información, y **cómo agregar tooltips** hace que la información sea instantáneamente legible. En este tutorial aprenderá a **agregar etiquetas de datos al gráfico de Excel**, **cambiar el tipo de gráfico**, y crear soluciones interactivas en Java con Aspose.Cells. También le mostraremos cómo agregar tooltips y un hipervínculo de profundización simple para que su audiencia pueda explorar los datos en profundidad.

## Respuestas rápidas
- **¿Qué biblioteca se usa?** Aspose.Cells for Java  
- **¿Puedo cambiar el tipo de gráfico?** Sí – simplemente modifique el enum `ChartType` cuando cree el gráfico.  
- **¿Cómo agrego tooltips a un gráfico?** Use la API de etiquetas de datos (`setHasDataLabels(true)`) y habilite la visualización de valores.  
- **¿Se admite la profundización?** Puede adjuntar hipervínculos a los puntos de datos para un comportamiento básico de profundización.  
- **¿Requisitos previos?** IDE de Java, Aspose.Cells JAR y un archivo Excel con datos de muestra.

## Qué es cómo agregar tooltips?
**Cómo agregar tooltips** se refiere al proceso de habilitar texto emergente que muestra el valor de un punto de datos o información personalizada en un gráfico de Excel. En Aspose.Cells esto se logra mediante la configuración de etiquetas de datos del gráfico. Los tooltips ayudan a los usuarios a comprender rápidamente los datos sin saturar el gráfico, y pueden personalizarse en fuente, color y formato.

## Por qué usar gráficos interactivos con Aspose.Cells?
Aspose.Cells admite **más de 50 formatos de entrada y salida**—incluidos XLSX, CSV, PDF y HTML—y puede procesar libros de trabajo con **más de 1 000 hojas** sin cargar todo el archivo en memoria, ofreciendo una generación rápida de gráficos del lado del servidor para informes empresariales. Los gráficos interactivos también permiten incrustar hipervínculos, actualizaciones dinámicas de datos y exportación a formatos web‑amigables, lo que los hace ideales para paneles de control y portales de informes.

## Requisitos previos

Antes de comenzar, asegúrese de tener lo siguiente:

- Entorno de desarrollo Java (JDK 8+ recomendado)  
- Biblioteca Aspose.Cells for Java (descargue desde la [página de descarga de Aspose.Cells for Java](https://releases.aspose.com/cells/java/))  
- Un libro de trabajo de muestra (`data.xlsx`) que contenga los datos que desea visualizar  

## Paso 1: configurar su proyecto Java

1. Cree un nuevo proyecto Java en su IDE favorito (IntelliJ IDEA, Eclipse, etc.).  
2. Añada el JAR de Aspose.Cells a la ruta de compilación de su proyecto o a las dependencias de Maven/Gradle.

## Paso 2: cargar datos

Para trabajar con gráficos primero necesita un libro de trabajo cargado en memoria.

La clase `Workbook` representa un archivo Excel, y `Worksheet` representa una hoja única dentro de ese archivo.

```java
// Load the Excel file
Workbook workbook = new Workbook("data.xlsx");
Worksheet worksheet = workbook.getWorksheets().get(0);
```

## Cómo cambiar el tipo de gráfico en Aspose.Cells?

Cree un nuevo gráfico con el enum `ChartType` deseado; Aspose.Cells no modifica el tipo de un gráfico existente en‑sitio, por lo que debe agregar un gráfico nuevo del tipo correcto y, opcionalmente, eliminar el anterior. Este enfoque garantiza que todas las series y ejes se reconstruyan correctamente para la nueva representación visual.

## Paso 3: crear un gráfico (y cambiar su tipo)

Puede elegir cualquier tipo de gráfico que se ajuste a su análisis. A continuación creamos un **gráfico de columnas**, pero puede cambiar fácilmente a un gráfico de líneas, pastel o barras modificando el enum `ChartType`.

El objeto `Chart` proporciona métodos para configurar la representación visual de los datos en la hoja de cálculo.

```java
// Create a column chart
int chartIndex = worksheet.getCharts().add(ChartType.COLUMN, 5, 0, 15, 5);
Chart chart = worksheet.getCharts().get(chartIndex);
```

> **Consejo profesional:** Para **cambiar el tipo de gráfico de Excel**, reemplace `ChartType.COLUMN` por `ChartType.LINE`, `ChartType.PIE`, etc.

## Cómo agregar tooltips a un gráfico de Excel?

Cargue su gráfico, habilite las etiquetas de datos y establezca la bandera `showValue`. El tooltip mostrará entonces el valor de la celda subyacente siempre que un usuario pase el cursor sobre un punto de datos en el archivo Excel renderizado o en la vista HTML. También puede personalizar la fuente, el color y el fondo del tooltip para que coincidan con el estilo de su informe.

La clase `DataLabel` controla la apariencia y el contenido de las etiquetas de datos, que también sirven como tooltips.

```java
// Enable tooltips for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowValue(true);
```

## Paso 4: agregar interactividad

### 4.1. Agregar tooltips (agregar tooltips al gráfico)

Los tooltips aparecen cuando el usuario pasa el cursor sobre un punto de datos. El siguiente código habilita las etiquetas de datos y muestra el valor como tooltip.

```java
// Enable data labels for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowLabelAsDataCallout(true);
```

### 4.2. Agregar etiquetas de datos – **agregar etiquetas de datos al gráfico de excel**

Las etiquetas de datos proporcionan una pista visual permanente en el propio gráfico. Puede mostrarlas como llamadas de texto para una mejor legibilidad.

La clase `DataLabel` controla la apariencia de las etiquetas en cada serie. Al llamar a `setHasDataLabels(true)` y configurar propiedades como `setShowValue(true)`, incrusta el valor numérico directamente en el gráfico, haciéndolo visible instantáneamente sin interacción. Opciones adicionales le permiten mostrar nombres de series, porcentajes o texto personalizado para un contexto más rico.

> **¿Por qué agregar etiquetas de datos?** Incluir etiquetas de datos directamente en el gráfico elimina la necesidad de que los usuarios pasen el cursor o adivinen valores, mejorando la claridad del informe.

### 4.3. Implementar profundización (hipervínculo en un punto de datos)

Una forma sencilla de agregar capacidad de profundización es adjuntar un hipervínculo a un punto específico. Al hacer clic en el punto se abre una página web con información detallada.

La clase `Hyperlink` adjunta un enlace clicable a un elemento del gráfico, habilitando la navegación de profundización.

```java
// Add a hyperlink to a data point
String url = "https://example.com/data-details";
chart.getNSeries().get(0).getPoints().get(0).getHyperlinks().add(url);
```

## Cómo agregar etiquetas de datos a un gráfico de Excel?

La clase `DataLabel` controla la apariencia de las etiquetas en cada serie. Al llamar a `setHasDataLabels(true)` y configurar propiedades como `setShowValue(true)`, incrusta el valor numérico directamente en el gráfico, haciéndolo visible instantáneamente sin interacción. Opciones adicionales le permiten mostrar nombres de series, porcentajes o texto personalizado para un contexto más rico.

## Paso 5: guardar el libro de trabajo

Después de configurar el gráfico, guarde el libro de trabajo para que las funciones interactivas se almacenen en el archivo de salida.

Llamar a `workbook.save` escribe el libro de trabajo modificado en un archivo en el formato elegido.

```java
// Save the workbook
workbook.save("interactive_chart_output.xlsx");
```

## Problemas comunes y soluciones

| Problema | Solución |
|----------|----------|
| **Tooltips no se muestran** | Asegúrese de que `setHasDataLabels(true)` se llame antes de configurar `setShowValue(true)`. |
| **Hipervínculo no clicable** | Verifique que el formato de salida admita hipervínculos (p.ej., XLSX, no CSV). |
| **El tipo de gráfico no cambia** | Verifique que haya modificado el enum `ChartType` correcto al agregar el gráfico. |

## Preguntas frecuentes

**P: ¿Cómo puedo cambiar el tipo de gráfico después de crearlo?**  
R: Necesita crear un nuevo gráfico con el `ChartType` deseado. Aspose.Cells no ofrece una conversión de tipo en‑sitio, por lo que debe eliminar el gráfico antiguo y agregar uno nuevo.

**P: ¿Puedo personalizar la apariencia de los tooltips?**  
R: Sí. Use las propiedades de `DataLabel` como `setFontSize`, `setFontColor` y `setBackgroundColor` para dar estilo al texto del tooltip.

**P: ¿Cómo manejo las interacciones de usuario en una aplicación web?**  
R: Exporte el libro de trabajo a un archivo HTML o XLSX y use JavaScript del lado del cliente para capturar eventos de clic en los elementos del gráfico.

**P: ¿Dónde puedo encontrar más ejemplos y documentación?**  
R: Visite la [Referencia de API de Aspose.Cells Java](https://reference.aspose.com/cells/java/) para obtener una lista completa de clases y métodos relacionados con gráficos.

## Conclusión

Ahora sabe cómo **agregar etiquetas de datos a un gráfico de Excel**, **cambiar el tipo de gráfico de Excel**, **crear soluciones de gráficos interactivos en Java**, y enriquecerlos con tooltips, etiquetas de datos y hipervínculos de profundización usando Aspose.Cells para Java. Estas mejoras hacen que sus informes de Excel sean mucho más atractivos y reveladores para los usuarios finales.

---

**Última actualización:** 2026-08-21  
**Probado con:** Aspose.Cells for Java 24.12  
**Autor:** Aspose

## Tutoriales relacionados

- [Cómo modificar gráficos de Excel y etiquetas de datos usando Aspose.Cells para Java](/cells/java/charts-graphs/aspose-cells-java-modify-excel-charts-data-labels/)
- [Extraer etiquetas de eje de gráficos de Excel usando Aspose.Cells Java: Guía completa](/cells/java/charts-graphs/aspose-cells-java-excel-chart-axis-labels/)
- [Crear gráficos de burbujas en Excel usando Aspose.Cells para Java: Guía paso a paso](/cells/java/charts-graphs/aspose-cells-java-create-bubble-charts/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}