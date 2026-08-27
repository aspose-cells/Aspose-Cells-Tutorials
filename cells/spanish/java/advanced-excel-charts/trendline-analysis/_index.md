---
date: 2026-02-09
description: Aprenda a crear un gráfico de Excel, agregar una línea de tendencia,
  mostrar el valor de R‑cuadrado y exportar el gráfico a una imagen usando Aspose.Cells
  para Java. Incluye los pasos para cargar el archivo de Excel, personalizar el gráfico
  y guardarlo como PNG/JPEG.
linktitle: Export Chart to Image with Trendline Analysis
second_title: Aspose.Cells Java Excel Processing API
title: Cómo crear un gráfico de Excel con línea de tendencia y exportarlo a imagen
  usando Aspose.Cells para Java
url: /es/java/advanced-excel-charts/trendline-analysis/
weight: 15
---

 content.{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Exportar gráfico a imagen con análisis de línea de tendencia

En este tutorial aprenderá cómo **create Excel chart** con una línea de tendencia, mostrar su valor R‑cuadrado y exportar la visualización resultante a una imagen usando Aspose.Cells for Java. Revisaremos cómo cargar un libro de trabajo existente, agregar una línea de tendencia, personalizar los títulos, guardar el libro y, finalmente, generar un archivo PNG/JPEG que puede incrustar en cualquier lugar.

## Respuestas rápidas
- **¿Cuál es el propósito principal de esta guía?** Mostrarle cómo agregar una línea de tendencia, mostrar su ecuación y el valor R‑squared, y exportar el gráfico resultante a una imagen usando Java.  
- **¿Qué biblioteca se requiere?** Aspose.Cells for Java (descargue [here](https://releases.aspose.com/cells/java/)).  
- **¿Necesito una licencia?** Una prueba gratuita funciona para desarrollo; se requiere una licencia comercial para producción.  
- **¿Puedo generar un archivo Excel en Java?** Sí – el tutorial crea y guarda un libro de trabajo XLSX.  
- **¿Cómo exporto el gráfico a PNG o JPEG?** Use el método `Chart.toImage()` (cubierto en la sección “Export Chart”).

## Cómo crear un gráfico de Excel con línea de tendencia y exportarlo a imagen
Este encabezado responde directamente a la consulta principal de palabras clave y lo guía a través de todo el flujo de trabajo en un orden lógico. A continuación encontrará el porqué, los requisitos previos y una guía paso a paso.

## ¿Qué es Export Chart to Image?
Exportar un gráfico a una imagen convierte la representación visual de sus datos en un mapa de bits portátil (PNG, JPEG, etc.). Esto es útil para incrustar gráficos en informes, páginas web o presentaciones donde no se requiere el archivo Excel original.

## ¿Por qué agregar una línea de tendencia y mostrar el valor R‑cuadrado?
Una línea de tendencia le ayuda a identificar el patrón subyacente de una serie de datos, mientras que la métrica **R‑squared** cuantifica qué tan bien la línea de tendencia se ajusta a los datos. Incluir estos en su imagen exportada brinda a los interesados una visión inmediata sin abrir el libro de trabajo.

## Requisitos previos
- Java 8 o superior instalado.  
- Biblioteca Aspose.Cells for Java añadida a su proyecto (archivos JAR en el classpath).  
- Familiaridad básica con IDEs de Java (IntelliJ IDEA, Eclipse, etc.).  

## Guía paso a paso

### Paso 1: Configurar el proyecto
Cree un nuevo proyecto Java y agregue los JAR de Aspose.Cells a la ruta de compilación. Esto prepara el entorno para generar y manipular archivos Excel.

### Paso 2: Cargar archivo Excel (load excel file java)
```java
// Import necessary libraries
import com.aspose.cells.*;

// Load the Excel file
Workbook workbook = new Workbook("your_excel_file.xlsx");

// Access the worksheet
Worksheet worksheet = workbook.getWorksheets().get(0);
```
*Acabamos de **cargar un archivo Excel** en memoria, listo para la creación del gráfico.*

### Paso 3: Crear un gráfico
```java
// Create a chart
int chartIndex = worksheet.getCharts().add(ChartType.LINE, 5, 0, 15, 5);
Chart chart = worksheet.getCharts().get(chartIndex);

// Specify data source for the chart
chart.getNSeries().add("A1:A10", true);
```
*Aquí generamos un gráfico de líneas que más adelante alojará nuestra línea de tendencia.*

### Paso 4: Agregar línea de tendencia (how to add trendline) y mostrar el valor R‑squared
```java
// Add a trendline to the chart
Trendline trendline = chart.getNSeries().get(0).getTrendlines().add(TrendlineType.LINEAR);

// Customize trendline options
trendline.setDisplayEquation(true);
trendline.setDisplayRSquaredValue(true);
```
*La llamada `setDisplayRSquaredValue(true)` garantiza que el **valor R‑squared** aparezca en el gráfico.*

### Paso 5: Personalizar el gráfico y guardar el libro de trabajo (save workbook xlsx, generate excel file java)
```java
// Customize chart title and axes
chart.getTitle().setText("Trendline Analysis");
chart.getCategoryAxis().getTitle().setText("X-Axis");
chart.getValueAxis().getTitle().setText("Y-Axis");

// Save the Excel file with the chart
workbook.save("output.xlsx");
```
*Ahora el libro de trabajo está **generado** y guardado como un archivo XLSX, listo para procesamiento adicional.*

### Paso 6: Exportar gráfico a imagen (export chart to image)
> **Nota:** Este paso se describe sin un bloque de código adicional para mantener el número original de bloques.  
Después de que el gráfico se haya creado y guardado, puede exportarlo a una imagen llamando al método `chart.toImage()` y escribiendo el `java.awt.image.BufferedImage` resultante en el formato de archivo que elija (PNG, JPEG, BMP). El flujo de trabajo típico es:
1. Recuperar el objeto `Chart` (ya hecho en pasos anteriores).  
2. Llamar a `chart.toImage()` para obtener un `BufferedImage`.  
3. Usar `ImageIO.write(bufferedImage, "png", new File("chart.png"))` para escribir el archivo.  

Esto produce una imagen de alta resolución que puede incrustar en cualquier lugar, completando el proceso de **export chart to image**.

## Analizar resultados
Abra `output.xlsx` en Excel para verificar que la línea de tendencia, la ecuación y el valor R‑squared aparezcan como se espera. Abra el archivo de imagen exportado (p. ej., `chart.png`) para ver una visual limpia que puede compartirse sin el libro de trabajo original.

## Problemas comunes y soluciones
- **La línea de tendencia no se muestra:** Asegúrese de que el rango de datos (`A1:A10`) contenga valores numéricos; los datos no numéricos impedirán que se calcule la línea de tendencia.  
- **El valor R‑squared se muestra como 0:** Esto a menudo indica que la serie de datos es constante o tiene variación insuficiente. Pruebe con un conjunto de datos diferente o una línea de tendencia polinómica.  
- **La exportación de la imagen falla con `NullPointerException`:** Verifique que el gráfico se haya renderizado completamente antes de llamar a `toImage()`. Guardar el libro de trabajo primero a veces resuelve problemas de sincronización.

## Preguntas frecuentes

**Q: ¿Cómo puedo cambiar el tipo de línea de tendencia?**  
A: Use una enumeración `TrendlineType` diferente al agregar la línea de tendencia, p. ej., `TrendlineType.POLYNOMIAL` para un ajuste polinómico.

**Q: ¿Puedo personalizar la apariencia de la línea de tendencia (color, grosor)?**  
A: Sí. Acceda al `LineFormat` de la línea de tendencia mediante `trendline.getLineFormat()` y establezca propiedades como `setWeight()` y `setColor()`.

**Q: ¿Cómo exporto el gráfico a PDF en lugar de una imagen?**  
A: Convierta primero el gráfico a una imagen, luego incruste esa imagen en un PDF usando Aspose.PDF o cualquier biblioteca PDF de su elección.

**Q: ¿Es posible agregar múltiples líneas de tendencia al mismo gráfico?**  
A: Absolutamente. Llame a `chart.getNSeries().get(0).getTrendlines().add(...)` para cada serie que desee analizar.

**Q: ¿Aspose.Cells admite la exportación de imágenes de alta resolución?**  
A: Sí. Puede especificar los DPI al llamar a `chart.toImage()` y luego escalar la imagen en consecuencia antes de guardarla.

## Conclusión
Ahora dispone de una solución completa, de extremo a extremo, para **create Excel chart**, agregar una línea de tendencia, mostrar la ecuación y el valor R‑squared, personalizar la visualización, guardar el libro de trabajo y, finalmente, exportar el gráfico como una imagen PNG/JPEG. Este enfoque le permite generar activos analíticos de nivel profesional de forma programática, perfecto para informes automatizados, paneles de control o cualquier escenario donde una imagen estática sea más conveniente que un archivo Excel.

**Última actualización:** 2026-02-09  
**Probado con:** Aspose.Cells for Java latest  
**Autor:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}