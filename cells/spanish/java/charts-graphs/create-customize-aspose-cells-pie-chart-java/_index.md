---
date: '2026-09-27'
description: Aprenda cómo crear un gráfico de pastel en Java usando Aspose.Cells.
  Guía paso a paso para personalizar el gráfico de pastel de Excel, configurar la
  dependencia Maven y generar gráficos profesionales.
keywords:
- create pie chart java
- customize excel pie chart
- maven dependency aspose cells
lastmod: '2026-09-27'
og_description: Cree un gráfico de pastel en Java usando Aspose.Cells para Java. Aprenda
  a personalizar el gráfico de pastel de Excel, añadir la dependencia Maven y generar
  gráficos profesionales en minutos.
og_image_alt: Java code generating a customized pie chart in Excel with Aspose.Cells
og_title: Crear gráfico de pastel en Java con Aspose.Cells – Guía completa de Java
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Learn how to create pie chart java using Aspose.Cells. Step‑by‑step
    guide to customize Excel pie chart, set up Maven dependency, and generate professional
    charts.
  headline: How to create pie chart java with Aspose.Cells
  type: TechArticle
- questions:
  - answer: Yes, repeat the chart‑creation steps for each data range; each chart is
      independent.
    question: Can I generate multiple pie charts in the same workbook?
  - answer: It does; set the chart type to `ChartType.PIE_3D` when adding the chart.
    question: Does Aspose.Cells support 3‑D pie charts?
  - answer: Use the `Workbook.setDefaultTheme` method before creating any charts.
    question: How do I apply a custom theme to all charts?
  - answer: Over 30 formats, including XLSX, CSV, PDF, and HTML.
    question: What file formats can I export the workbook to?
  - answer: Yes, a valid license removes evaluation watermarks and unlocks full functionality.
    question: Is a license required for commercial deployment?
  type: FAQPage
tags:
- Aspose.Cells
- Java charting
- Excel automation
- data visualization
title: Cómo crear un gráfico de pastel en Java con Aspose.Cells
url: /es/java/charts-graphs/create-customize-aspose-cells-pie-chart-java/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo crear un gráfico circular java con Aspose.Cells

## Introducción
Crear un **pie chart** programáticamente a menudo se siente como un rompecabezas, especialmente cuando necesitas un control fino sobre colores, leyendas y títulos. En esta guía aprenderás a **create pie chart java** usando Aspose.Cells, y luego personalizar el **pie chart** de Excel para que coincida con tu marca o estilo de informes. Recorreremos la configuración del entorno, la población de datos, la generación del gráfico y ajustes visuales, todo sin salir de tu IDE de Java.

**Lo que aprenderás**
- Agregar la **Maven dependency Aspose.Cells** a tu proyecto.
- Crear un workbook, rellenar celdas con datos y generar un **pie chart**.
- Aplicar colores personalizados, títulos y leyendas al gráfico.
- Exportar el workbook a un archivo XLSX listo para compartir.

Antes de comenzar, deberías estar cómodo con la sintaxis básica de Java y tener Maven o Gradle instalados.

## Respuestas rápidas
- **¿Qué biblioteca crea pie charts en Java?** Aspose.Cells for Java.
- **¿Necesito una licencia?** Una prueba gratuita funciona para desarrollo; se requiere una licencia de pago para producción.
- **¿Qué coordenadas Maven son necesarias?** `com.aspose:aspose-cells:24.10`.
- **¿Puedo cambiar los colores de las porciones?** Sí, mediante el método `setAreaColor` en cada serie.
- **¿Se puede exportar el gráfico a XLSX?** Absolutamente—simplemente llama a `workbook.save("output.xlsx")`.

## ¿Qué es un pie chart en Excel?
Un **pie chart** visualiza una única serie de datos como porciones proporcionales de un círculo, facilitando la comparación de partes de un todo. El ángulo de cada porción corresponde a su valor relativo al total, permitiendo una visión rápida de la distribución entre categorías como participación de mercado, asignación presupuestaria o porcentajes demográficos.

## ¿Por qué usar Aspose.Cells para crear un pie chart java?
Aspose.Cells admite más de 50 tipos de gráficos y puede manejar hojas de cálculo con hasta un millón de filas sin cargar todo el archivo en memoria. Esta ventaja de rendimiento te permite generar informes grandes en hardware modesto, al tiempo que ofrece un control fino sobre la apariencia del gráfico, el enlace de datos y los formatos de exportación, convirtiéndolo en una opción superior frente a muchas bibliotecas de código abierto.

## Requisitos previos
- **Java Development Kit (JDK)** 8 o superior.
- **IDE** como IntelliJ IDEA o Eclipse.
- **Maven** o **Gradle** para la gestión de dependencias.
- Una **licencia de prueba o comprada de Aspose.Cells**.

### Bibliotecas y dependencias requeridas
Agrega el artefacto Maven de Aspose.Cells a tu `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

O el equivalente en Gradle:

```gradle
implementation 'com.aspose:aspose-cells:25.3'
```

### Pasos para obtener la licencia
Aspose.Cells for Java es comercial, pero puedes comenzar con una prueba gratuita. Visita la [purchase page](https://purchase.aspose.com/buy) para obtener una clave de licencia temporal.

## Configuración de Aspose.Cells para Java
Primero, asegúrate de que la biblioteca esté en tu classpath. Después de agregar la dependencia, puedes inicializar la API como se muestra a continuación.

```java
import com.aspose.cells.Workbook;

// Initialize a new workbook instance
Workbook workbook = new Workbook();
```

## Guía de implementación

### Crear y configurar un workbook
La clase `Workbook` representa un archivo Excel completo en memoria.

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;
import com.aspose.cells.Cells;
import com.aspose.cells.ChartType;
import com.aspose.cells.Chart;
import com.aspose.cells.Series;
import com.aspose.cells.Color;
import com.aspose.cells.LegendPositionType;
import com.aspose.cells.SaveFormat;
```

#### Paso 1: instanciar un workbook
```java
// Creates an empty workbook instance to work with.
Workbook workbook = new Workbook();
```  
Esto crea un nuevo workbook vacío que puedes comenzar a rellenar de inmediato.

### Acceder o modificar celdas de la hoja de cálculo
Una `Worksheet` representa una sola hoja dentro del workbook, que contiene celdas, filas y columnas.  
Escribirás los datos que alimentan el **pie chart** en una hoja de cálculo.

#### Paso 2: obtener la primera worksheet y sus celdas
```java
// Access the first worksheet in the workbook.
Worksheet worksheet = workbook.getWorksheets().get(0);
Cells cells = worksheet.getCells();

// Put sample values used for a pie chart into specific cells.
cells.get("C3").putValue("India");
cells.get("C4").putValue("China");
cells.get("C5").parseNumber("United States", true, null);
cells.get("C6").setValue("Russia");
cells.get("C7").setValue("United Kingdom");
cells.get("C8").setValue("Others");

// Put percentage values for a pie chart into specific cells.
cells.get("D2").putValue("% of world population");
cells.get("D3").putValue(25);
cells.get("D4").putValue(30);
cells.get("D5").putValue(10);
cells.get("D6").putValue(13);
cells.get("D7").putValue(9);
cells.get("D8").putValue(13);
```  
Rellena las celdas con nombres de categorías y valores que el gráfico consumirá.

### Crear un pie chart
Los objetos `Chart` visualizan datos en una worksheet y admiten varios tipos como pie, column y line.

#### Paso 3: agregar un pie chart a la worksheet
```java
// Create a pie chart in the worksheet.
int pieIdx = worksheet.getCharts().add(ChartType.PIE, 1, 6, 15, 14);
Chart pie = worksheet.getCharts().get(pieIdx);
```  

### Configurar series y datos del pie chart
`Series` define el rango de datos y el formato para un gráfico, vinculando celdas de la worksheet a elementos visuales.

#### Paso 4: establecer la series para el gráfico
```java
// Configure the series data range for the chart.
pie.getNSeries().add("D3:D8", true);
pie.getNSeries().setCategoryData("=Sheet1!$C$3:$C$8");

// Link the pie chart title to a cell containing the title text.
pie.getTitle().setLinkedSource("D2");
```  

### Configurar la apariencia de la leyenda y el título del gráfico
Una `Legend` del gráfico muestra los nombres de las series y los colores, ayudando a los lectores a identificar cada porción.

#### Paso 5: personalizar la leyenda y el título del gráfico
```java
// Set legend position at bottom of the chart.
pie.getLegend().setPosition(LegendPositionType.BOTTOM);

// Set font properties for the chart title.
pie.getTitle().getFont().setName("Calibri");
pie.getTitle().getFont().setSize(18);
```  

### Personalizar colores de las series del gráfico
`setAreaColor` establece el color de relleno de una porción de la serie del gráfico usando un valor RGB.

#### Paso 6: cambiar los colores de los segmentos del pie
```java
import com.aspose.cells.Color;

// Access and customize colors of individual pie chart segments.
Series srs = pie.getNSeries().get(0);
srs.getPoints().get(0).getArea().setForegroundColor(Color.fromArgb(0, 246, 22, 219));
srs.getPoints().get(1).getArea().setForegroundColor(Color.fromArgb(0, 51, 34, 84));
srs.getPoints().get(2).getArea().setForegroundColor(Color.fromArgb(0, 46, 74, 44));
srs.getPoints().get(3).getArea().setForegroundColor(Color.fromArgb(0, 19, 99, 44));
srs.getPoints().get(4).getArea().setForegroundColor(Color.fromArgb(0, 208, 223, 7));
srs.getPoints().get(5).getArea().setForegroundColor(Color.fromArgb(0, 222, 69, 8));
```  

### Ajustar columnas automáticamente y guardar el workbook
`autoFitColumns` ajusta automáticamente el ancho de las columnas para que se adapten al contenido de las celdas.

#### Paso 7: ajustar el ancho de las columnas y guardar el archivo
```java
// Autofit all columns.
worksheet.autoFitColumns();

// Define output directory placeholder path for saving the workbook.
String outDir = "YOUR_OUTPUT_DIRECTORY";

// Save the modified workbook to an Excel file in the specified directory.
workbook.save(outDir + "/CSOrSColorsPieChart_out.xlsx", SaveFormat.XLSX);
```  

## Casos de uso comunes
- **Análisis demográfico:** Mostrar la distribución de la población entre regiones.
- **Informe de participación de mercado:** Visualizar la cuota de cada competidor de un vistazo.
- **Asignación presupuestaria:** Resaltar cómo se distribuyen los fondos entre departamentos.

## Consideraciones de rendimiento
- Liberar objetos (`workbook.dispose()`) cuando ya no se necesiten para liberar memoria nativa.
- Para conjuntos de datos masivos, usa `WorkbookDesigner` para transmitir datos en lugar de cargar todo de una vez.
- Perfila con Java Flight Recorder para detectar cuellos de botella en la generación del gráfico.

## Preguntas frecuentes

**Q: ¿Puedo generar varios pie charts en el mismo workbook?**  
A: Sí, repite los pasos de creación del gráfico para cada rango de datos; cada gráfico es independiente.

**Q: ¿Aspose.Cells admite gráficos de pie 3‑D?**  
A: Sí; establece el tipo de gráfico a `ChartType.PIE_3D` al agregar el gráfico.

**Q: ¿Cómo aplico un tema personalizado a todos los gráficos?**  
A: Usa el método `Workbook.setDefaultTheme` antes de crear cualquier gráfico.

**Q: ¿A qué formatos de archivo puedo exportar el workbook?**  
A: Más de 30 formatos, incluidos XLSX, CSV, PDF y HTML.

**Q: ¿Se requiere una licencia para el despliegue comercial?**  
A: Sí, una licencia válida elimina las marcas de agua de evaluación y desbloquea la funcionalidad completa.

## Conclusión
Ahora tienes una receta completa, de extremo a extremo, para **create pie chart java** con Aspose.Cells. Siguiendo los pasos anteriores puedes generar gráficos circulares de Excel pulidos, personalizar colores y títulos, e integrarlos en cualquier flujo de informes. Explora otros tipos de gráficos—column, line, radar—para ampliar tu conjunto de herramientas de visualización de datos.

---

**Last Updated:** 2026-09-27  
**Tested with:** Aspose.Cells 24.10 for Java  
**Author:** Aspose

## Tutoriales relacionados

- [Personalizar etiquetas de datos de gráficos de Excel usando Aspose.Cells para Java&#58; Guía paso a paso](/cells/java/charts-graphs/customize-chart-data-labels-aspose-cells-java/)
- [Crear gráficos dinámicos de Excel con Aspose.Cells Java&#58; Guía completa para desarrolladores](/cells/java/charts-graphs/aspose-cells-java-dynamic-excel-charts/)
- [Crear y personalizar libros de Excel usando Aspose.Cells Java&#58; Guía paso a paso](/cells/java/workbook-operations/create-customize-excel-workbooks-aspose-cells-java/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}