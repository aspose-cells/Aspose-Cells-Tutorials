---
date: 2026-09-02
description: Aprenda cómo crear un gráfico de cascada de excel en Java con Aspose.Cells,
  establezca el rango de datos del gráfico, personalice las etiquetas y exporte a
  XLSX.
keywords:
- create excel waterfall chart
- waterfall chart data labels
- Aspose.Cells Java chart
lastmod: 2026-09-02
linktitle: Gráficos de cascada
og_description: Crear gráfico de cascada de excel usando Aspose.Cells para Java –
  establezca el rango de datos del gráfico, añada etiquetas de datos y exporte a XLSX
  en unos pocos pasos.
og_image_alt: 'Tutorial: create excel waterfall chart with Aspose.Cells Java'
og_title: Crear gráfico de cascada de excel con Aspose.Cells para Java
schemas:
- author: Aspose
  dateModified: '2026-09-02'
  description: Learn how to create excel waterfall chart in Java with Aspose.Cells,
    set the chart data range, customize labels and export to XLSX.
  headline: Create excel waterfall chart with Aspose.Cells for Java
  type: TechArticle
- description: Learn how to create excel waterfall chart in Java with Aspose.Cells,
    set the chart data range, customize labels and export to XLSX.
  name: Create excel waterfall chart with Aspose.Cells for Java
  steps:
  - name: import Aspose.Cells
    text: The `com.aspose.cells` package contains all classes required for Excel manipulation,
      including workbook creation, worksheet handling, and chart generation.
  - name: initialize workbook and worksheet
    text: A **Workbook** represents an Excel file, and a **Worksheet** is a single
      sheet within that file. Creating these objects provides the canvas for both
      raw data and the chart.
  - name: enter data
    text: Column A holds category labels, while column B contains the numeric values
      for the waterfall. This layout matches the typical profit‑and‑loss flow used
      in financial analysis.
  - name: create the waterfall chart
    text: The **Chart** object creates a visual representation; setting its type to
      `ChartType.WATERFALL` configures it as a waterfall chart. Use the `add` method
      to set the chart data range for the series (`"B2:B6"`), and link the category
      axis to `"A2:A6"`.
  - name: save the workbook
    text: Saving the workbook writes the chart and data to the specified file format.
      Call `workbook.save("WaterfallChart.xlsx")` to generate an XLSX file, or change
      the format parameter to export to PDF, CSV, or HTML.
  type: HowTo
- questions:
  - answer: Use the `add` method on the chart’s series, passing the cell range that
      contains your values, e.g., `"B2:B6"`.
    question: How do I set the chart data range for a financial waterfall chart?
  - answer: Yes, call `workbook.save("WaterfallChart.pdf", SaveFormat.PDF);` to generate
      a PDF version.
    question: Can I export the workbook to PDF instead of XLSX?
  - answer: Extend the data range in both the values column and the category column,
      then update the `add` and `setCategoryData` calls accordingly.
    question: What if I need to create a waterfall chart with more categories?
  - answer: Iterate through the `Series` collection and set the `FillFormat` color
      based on each value’s sign; Aspose.Cells lets you apply conditional formatting
      programmatically.
    question: Is there a way to automatically format positive and negative bars?
  - answer: Yes. After modifying cell values, simply re‑save the workbook—the chart
      will reflect the new data automatically.
    question: Does Aspose.Cells support dynamic data updates for charts?
  type: FAQPage
second_title: Aspose.Cells Java Excel Processing API
tags:
- waterfall chart
- Aspose.Cells
- java excel charts
- excel automation
title: Crear gráfico de cascada de excel con Aspose.Cells para Java
url: /es/java/advanced-excel-charts/waterfall-charts/
weight: 18
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Gráficos de cascada

## Introducción a los gráficos de cascada usando Aspose.Cells for Java

En este tutorial aprenderá cómo **crear un gráfico de cascada de Excel** y **establecer el rango de datos del gráfico** con Aspose.Cells for Java. Los gráficos de cascada convierten una serie de números positivos y negativos en una historia visual clara, lo que los hace ideales para estados financieros, revisiones de desempeño de ventas y cualquier escenario donde necesite ver cómo los elementos individuales contribuyen a un total.

## Respuestas rápidas
- **¿Qué es un gráfico de cascada?** Una visual que muestra cómo un valor inicial se incrementa y disminuye mediante una serie de valores intermedios, terminando con un total final.  
- **¿Qué biblioteca se utiliza?** Aspose.Cells for Java.  
- **¿Necesito una licencia?** Una prueba gratuita funciona para desarrollo; se requiere una licencia comercial para producción.  
- **¿Puedo guardar el archivo como XLSX?** Sí – use `workbook.save("FileName.xlsx")`.  
- **¿Es adecuado para la visualización de datos en Java?** Absolutamente; Aspose.Cells proporciona funciones de gráficos avanzadas sin necesidad de Office instalado.

## Qué es un gráfico de cascada
Un gráfico de cascada muestra contribuciones positivas y negativas secuenciales a un valor inicial, ayudándole a comprender cómo cada componente impacta el resultado total. Al visualizar ganancias y pérdidas lado a lado, hace que los flujos financieros complejos sean instantáneamente legibles.

## Por qué usar Aspose.Cells for Java para agregar un gráfico de cascada
Aspose.Cells le permite generar gráficos de Excel en cualquier servidor, canal de CI o escritorio sin necesidad de Microsoft Excel. Soporta **más de 15 formatos de salida** (XLSX, PDF, HTML, CSV y más), procesa libros de trabajo con **más de 500 filas** en menos de un segundo, y brinda control programático sobre cada elemento del gráfico, desde colores hasta etiquetas de datos.

## Requisitos previos

Antes de sumergirnos en el código, asegúrese de que tenga los siguientes requisitos previos:

- Aspose.Cells for Java: Necesitará tener Aspose.Cells for Java instalado. Puede descargarlo desde la página de lanzamientos de Aspose.Cells for Java: [Aspose.Cells for Java releases](https://releases.aspose.com/cells/java/).
- Entorno de desarrollo Java: Asegúrese de tener Java instalado en su sistema y una herramienta de compilación (Maven/Gradle) lista.

Ahora, comencemos a crear el gráfico de cascada paso a paso.

## Cómo establecer el rango de datos del gráfico para un gráfico de cascada en Java
Cargue un nuevo libro de trabajo, pueblelo con datos, agregue un objeto `Chart`, defina el rango de la serie y, finalmente, guarde el archivo. Este proceso es sencillo: crea un libro de trabajo, llena celdas con categorías y valores, crea un gráfico, enlaza los rangos de datos y luego exporta el libro de trabajo. El resultado es un gráfico de cascada totalmente funcional listo para usar en informes o paneles.

### Paso 1: importar Aspose.Cells
El paquete `com.aspose.cells` contiene todas las clases necesarias para la manipulación de Excel, incluyendo la creación de libros de trabajo, el manejo de hojas de cálculo y la generación de gráficos.

### Paso 2: inicializar libro de trabajo y hoja de cálculo
Un **Workbook** representa un archivo de Excel, y una **Worksheet** es una hoja única dentro de ese archivo. Crear estos objetos proporciona el lienzo tanto para los datos sin procesar como para el gráfico.

### Paso 3: ingresar datos
La columna A contiene las etiquetas de categoría, mientras que la columna B contiene los valores numéricos para el gráfico de cascada. Este diseño coincide con el flujo típico de ganancias y pérdidas utilizado en el análisis financiero.

### Paso 4: crear el gráfico de cascada
El objeto **Chart** crea una representación visual; establecer su tipo a `ChartType.WATERFALL` lo configura como un gráfico de cascada. Use el método `add` para establecer el rango de datos del gráfico para la serie (`"B2:B6"`), y vincule el eje de categorías a `"A2:A6"`.

### Paso 5: guardar el libro de trabajo
Guardar el libro de trabajo escribe el gráfico y los datos en el formato de archivo especificado. Llame a `workbook.save("WaterfallChart.xlsx")` para generar un archivo XLSX, o cambie el parámetro de formato para exportar a PDF, CSV o HTML.

## Problemas comunes y soluciones

- **El gráfico aparece en blanco** – Verifique que las referencias del rango de datos (`B2:B6` y `A2:A6`) coincidan con las celdas reales que contienen sus valores y categorías.  
- **Los valores negativos no se muestran correctamente** – Asegúrese de que el tipo de serie esté configurado a `ChartType.WATERFALL`; otros tipos de gráfico tratan los negativos de forma diferente.  
- **El archivo no se abre en Excel** – Use la última versión de Aspose.Cells y confirme que la extensión del archivo coincida con el formato (`.xlsx` para Excel).

## Preguntas frecuentes

### ¿Cómo puedo personalizar la apariencia de mi gráfico de cascada?
Puede modificar propiedades como `Chart.getSeries().get(0).getFillFormat().setColor(Color.getRed())` para cambiar los colores de las barras, habilitar etiquetas de datos con `setShowDataLabels(true)`, y ajustar los títulos de los ejes mediante `getCategoryAxis().setTitle("Stage")`. La referencia de la API de Aspose.Cells proporciona una lista completa de opciones personalizables.

### ¿Puedo crear varios gráficos de cascada en la misma hoja de cálculo?
Sí. Después de agregar el primer gráfico, repita los pasos de creación del gráfico con un rango de datos diferente y un nuevo objeto `Chart`. Cada gráfico es independiente y puede posicionarse en cualquier parte de la hoja.

### ¿Aspose.Cells es compatible con diferentes entornos de desarrollo Java?
Absolutamente. La biblioteca funciona con Eclipse, IntelliJ IDEA, NetBeans y cualquier sistema de compilación que soporte Maven o Gradle. No se requieren complementos adicionales.

### ¿Puedo agregar series de datos adicionales a mi gráfico de cascada?
Puede agregar más series llamando a `chart.getNSeries().add("C2:C6", true)` y configurando cada serie por separado. Esto le permite comparar varios escenarios lado a lado.

### ¿Dónde puedo encontrar más recursos y ejemplos para Aspose.Cells for Java?
Explore la documentación completa en la referencia de la API de Aspose.Cells Java: [Aspose.Cells Java API reference](https://reference.aspose.com/cells/java/).

## Preguntas frecuentes

**Q: ¿Cómo establezco el rango de datos del gráfico para un gráfico de cascada financiero?**  
A: Use el método `add` en la serie del gráfico, pasando el rango de celdas que contiene sus valores, por ejemplo, `"B2:B6"`.

**Q: ¿Puedo exportar el libro de trabajo a PDF en lugar de XLSX?**  
A: Sí, llame a `workbook.save("WaterfallChart.pdf", SaveFormat.PDF);` para generar una versión PDF.

**Q: ¿Qué pasa si necesito crear un gráfico de cascada con más categorías?**  
A: Amplíe el rango de datos tanto en la columna de valores como en la columna de categorías, luego actualice las llamadas `add` y `setCategoryData` en consecuencia.

**Q: ¿Hay una forma de formatear automáticamente las barras positivas y negativas?**  
A: Itere a través de la colección `Series` y establezca el color `FillFormat` según el signo de cada valor; Aspose.Cells le permite aplicar formato condicional programáticamente.

**Q: ¿Aspose.Cells admite actualizaciones dinámicas de datos para los gráficos?**  
A: Sí. Después de modificar los valores de las celdas, simplemente vuelva a guardar el libro de trabajo; el gráfico reflejará los nuevos datos automáticamente.

---

**Última actualización:** 2026-09-02  
**Probado con:** Aspose.Cells for Java (última)  
**Autor:** Aspose  









```java
import com.aspose.cells.*;
```

```java
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.getWorksheets().get(0);
```

```java
Cells cells = worksheet.getCells();

// Insert data
cells.get("A1").putValue("Categories");
cells.get("A2").putValue("Start");
cells.get("A3").putValue("Positive Value 1");
cells.get("A4").putValue("Negative Value 1");
cells.get("A5").putValue("Positive Value 2");
cells.get("A6").putValue("End");

cells.get("B1").putValue("Values");
cells.get("B2").putValue(0);
cells.get("B3").putValue(20);
cells.get("B4").putValue(-10);
cells.get("B5").putValue(15);
cells.get("B6").putValue(25);
```

```java
int chartIndex = worksheet.getCharts().add(ChartType.WATERFALL, 5, 0, 15, 5);
Chart waterfallChart = worksheet.getCharts().get(chartIndex);
waterfallChart.getNSeries().add("B2:B6", true);
waterfallChart.getNSeries().setCategoryData("A2:A6");
```

```java
workbook.save("WaterfallChart.xlsx");
```

## Tutoriales relacionados

- [Personalizar etiquetas de datos de gráficos de Excel usando Aspose.Cells for Java: Guía paso a paso](/cells/java/charts-graphs/customize-chart-data-labels-aspose-cells-java/)
- [Agregar etiquetas de datos a un gráfico de Excel con Aspose.Cells Java](/cells/java/advanced-excel-charts/chart-interactivity/)
- [Cómo crear y exportar gráficos en Java usando Aspose.Cells: Guía completa](/cells/java/charts-graphs/aspose-cells-java-create-export-charts/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}