---
date: 2026-08-21
description: Aprenda a exportar gráficos como imágenes y crear gráficos circulares
  3D en Java con Aspose.Cells. Genere gráficos de barras 3D, añada gráficos 3D a Excel
  y guarde libros de trabajo como XLSX.
keywords:
- export chart as image
- 3d pie chart java
- 3d bar chart java
- save workbook as xlsx
- add 3d chart excel
lastmod: 2026-08-21
linktitle: Crear gráfico circular 3D Java
og_description: Exportar gráfico como imagen y crear gráficos circulares 3D en Java
  usando Aspose.Cells. Guía paso a paso para generar gráficos de barras y circulares
  3D, personalizarlos y guardar libros de trabajo como XLSX.
og_image_alt: Developer guide showing how to export a 3D chart as an image with Aspose.Cells
  for Java
og_title: Exportar gráfico como imagen y crear gráfico circular 3D en Java
schemas:
- author: Aspose
  dateModified: '2026-08-21'
  description: Learn how to export chart as image and create 3D pie charts in Java
    with Aspose.Cells. Generate 3D bar charts, add 3D charts to Excel, and save workbooks
    as XLSX.
  headline: How to export chart as image and create 3D pie chart in Java
  type: TechArticle
- questions:
  - answer: Use `chart.getNSeries().add()` for each series range and ensure the chart
      type remains 3‑D (e.g., `ChartType.BAR_3_D` or `ChartType.PIE_3_D`).
    question: How can I add multiple data series to a 3D chart?
  - answer: Yes, you can save the chart as PNG, JPEG, or PDF by calling the appropriate
      `chart.toImage()` overload or `workbook.save()` with an image or PDF format,
      satisfying the **convert chart png** requirement.
    question: Can I export 3D charts created with Aspose.Cells for Java to other formats?
  - answer: Aspose.Cells focuses on static Excel charts. For interactive web‑based
      3‑D visualizations, consider coupling Excel data with JavaScript libraries such
      as Three.js.
    question: Is it possible to create interactive 3D charts with Aspose.Cells for
      Java?
  - answer: Absolutely. Load new data into the worksheet programmatically and refresh
      the chart range; the next time the workbook is opened, the chart reflects the
      updated values.
    question: Can I automate the process of updating data in my 3D charts?
  - answer: 'You can find comprehensive documentation and resources for Aspose.Cells
      for Java at the website: [Aspose.Cells for Java Documentation](https://reference.aspose.com/cells/java/).'
    question: Where can I find more resources and documentation for Aspose.Cells for
      Java?
  type: FAQPage
second_title: Aspose.Cells Java Excel Processing API
tags:
- export chart as image
- 3d pie chart
- Aspose.Cells Java
- Excel chart automation
title: Cómo exportar gráfico como imagen y crear gráfico circular 3D en Java
url: /es/java/advanced-excel-charts/3d-charts/
weight: 13
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Crear gráfico de pastel 3D Java

## Introducción a los gráficos 3D

Aspose.Cells for Java es una poderosa API Java para trabajar con archivos Excel, y facilita la **creación de gráfico de pastel 3D** así como visualizaciones clásicas de barras 3‑D. En este tutorial verá exactamente cómo **exportar gráfico como imagen**, generar un gráfico de barras 3‑D, adaptar el mismo enfoque para un gráfico de pastel 3‑D, personalizar la apariencia y, finalmente, **agregar archivos de gráfico 3D a Excel** a sus informes. Ya sea que esté creando un panel financiero, una hoja de desempeño de ventas o visualizando datos científicos, los pasos a continuación le proporcionarán una base sólida.

## Respuestas rápidas
- **¿Qué biblioteca necesito?** Aspose.Cells for Java (última versión)  
- **¿Puedo generar un gráfico de barras 3D?** Sí – use `ChartType.BAR_3_D`  
- **¿Necesito una licencia?** Una licencia válida elimina los límites de evaluación  
- **¿Qué versiones de Excel son compatibles?** Todas las versiones principales de 2003 a 2023  
- **¿Es posible exportar el gráfico como una imagen?** Sí – llame a `chart.toImage()` después de crear el gráfico  

## ¿Qué son los gráficos 3D?
Los gráficos 3D añaden profundidad a las visualizaciones 2D tradicionales, ayudando a los espectadores a comprender relaciones multidimensionales de forma más intuitiva. Son especialmente útiles cuando necesita comparar varias categorías lado a lado manteniendo una jerarquía visual clara. Al agregar una tercera dimensión, estos gráficos pueden resaltar diferencias de magnitud que podrían pasar desapercibidas en representaciones planas, facilitando la interpretación de datos complejos para los interesados del negocio.

## ¿Por qué usar Aspose.Cells for Java para generar un gráfico de barras 3D?
Aspose.Cells for Java ofrece más de 150 tipos de gráficos incorporados y soporta más de 100 funciones de Excel, brindándole un motor completo que funciona en todas las versiones de Excel desde 2003 hasta 2023 sin requerir Microsoft Office. Esto significa que puede **generar gráficos de barras 3D** de forma programática con resultados predecibles y una sobrecarga mínima.

## Configuración de Aspose.Cells for Java

### Descarga e instalación
Puede descargar la biblioteca Aspose.Cells for Java desde el sitio web oficial. Siga las instrucciones proporcionadas para Maven/Gradle o agregue el JAR directamente al classpath de su proyecto.

### Inicialización de la licencia
La clase `License` se utiliza para aplicar su licencia de Aspose.Cells y desbloquear la funcionalidad completa.  
```java
// Initialize Aspose.Cells license
License license = new License();
license.setLicense("path_to_license_file.xml");
```

## Creación de un gráfico 3D básico

### Importación de bibliotecas necesarias
Primero, traiga las clases requeridas al alcance:  
```java
import com.aspose.cells.*;
```

### Inicialización de un libro de trabajo
Cree un libro de trabajo nuevo que alojará el gráfico:  
```java
Workbook workbook = new Workbook();
```

### Agregar datos al gráfico
Complete la hoja de cálculo con datos de ejemplo que el gráfico referenciará:  
```java
Worksheet worksheet = workbook.getWorksheets().get(0);

// Adding data to cells
worksheet.getCells().get("A1").putValue("Category");
worksheet.getCells().get("A2").putValue("A");
worksheet.getCells().get("A3").putValue("B");
worksheet.getCells().get("A4").putValue("C");

worksheet.getCells().get("B1").putValue("Value");
worksheet.getCells().get("B2").putValue(10);
worksheet.getCells().get("B3").putValue(20);
worksheet.getCells().get("B4").putValue(30);
```

## Cómo generar un gráfico de barras 3D en Java
Para crear un gráfico de barras 3D, añada un objeto de gráfico a la hoja, establezca su tipo a `ChartType.BAR_3_D` y luego vincule la serie de datos a las celdas que contienen sus valores. Después de configurar la apariencia del gráfico, puede renderizarlo o exportarlo según sea necesario.  
```java
int chartIndex = worksheet.getCharts().add(ChartType.BAR_3_D, 5, 0, 15, 5);
Chart chart = worksheet.getCharts().get(chartIndex);

// Setting the data range for the chart
chart.getNSeries().add("A2:B4", true);

// Customizing chart attributes
chart.getChartArea().getBorder().setVisible(false);
chart.getChartTitle().setText("3D Bar Chart");
```

## Guardar el gráfico en un archivo
Finalmente, escriba el libro de trabajo (que ahora contiene el gráfico 3‑D) en disco. Esto también **guarda el libro de trabajo xlsx** en el formato estándar de Excel:  
```java
workbook.save("3D_Chart.xlsx");
```

## Cómo crear un gráfico de pastel 3D con Aspose.Cells for Java
Si necesita una visualización tipo pastel, el flujo de trabajo es casi idéntico—solo cambia el enum `ChartType`. Reemplace `ChartType.BAR_3_D` por `ChartType.PIE_3_D` al agregar el gráfico y apunte la serie al mismo rango de datos. Después de crear el gráfico, puede establecer un título descriptivo, ajustar los colores de las porciones y exportar el resultado como una imagen. Este enfoque le permite reutilizar el mismo código de preparación de datos mientras ofrece una perspectiva visual diferente.

## Cómo exportar el gráfico como imagen en Java
El método `toImage` del objeto `Chart` guarda el gráfico como un archivo de imagen. Puede exportar cualquier gráfico 3D a una imagen raster con una sola llamada: `chart.toImage("myChart.png", ImageFormat.getPng())`. Este método renderiza el gráfico exactamente como aparece en Excel, preservando la profundidad 3‑D, colores y leyendas, y escribe la salida en la ruta de archivo especificada. Use PNG para calidad sin pérdidas o JPEG para tamaños de archivo menores al incrustar la imagen en informes web.

## Diferentes tipos de gráficos 3D
Aspose.Cells for Java soporta varias variedades de gráficos 3D que puede **agregar archivos de gráfico 3D a Excel** con:

- **Gráficos de barras** – ideales para comparar categorías.  
- **Gráficos de pastel** – muestran contribuciones proporcionales (incluido el pastel 3D).  
- **Gráficos de líneas** – ilustran tendencias a lo largo del tiempo.  
- **Gráficos de áreas** – enfatizan la magnitud del cambio.

Puede cambiar el enum `ChartType` a cualquiera de los anteriores manteniendo el mismo patrón de creación.

## Personalización avanzada de gráficos

### Agregar títulos y etiquetas
Proporcione contexto a su gráfico estableciendo un título descriptivo y etiquetas de ejes.

### Ajustar colores y estilos
Utilice el método `chart.getSeries().get(i).getArea().setForegroundColor(Color.getRGB(...))` para que coincida con la identidad corporativa.

### Trabajar con los ejes del gráfico
Ajuste finamente las escalas de los ejes, intervalos y marcas de graduación para mejorar la legibilidad.

### Agregar leyendas
Habilite leyendas con `chart.getLegend().setVisible(true)` para que los espectadores puedan identificar cada serie de datos.

### Exportar gráficos como imágenes
Cuando necesite una imagen estática para un informe web, llame a `chart.toImage("chart.png", ImageFormat.getPng())`. Esto satisface el caso de uso **convertir gráfico png** sin salir del libro de trabajo.

## Integración de datos
Aspose.Cells for Java puede extraer datos de bases de datos, archivos CSV o APIs en vivo. Simplemente rellene las celdas de la hoja de cálculo con los datos obtenidos antes de vincular el rango al gráfico. Esto mantiene su flujo de trabajo **agregar gráfico 3D a Excel** dinámico y actualizado.

## Conclusión
En esta guía recorrimos cómo **crear gráfico de pastel 3D** y **crear gráfico de barras 3D** desde el inicio hasta el final—configurando la biblioteca, agregando datos, generando un gráfico de barras 3‑D, adaptando los mismos pasos para un gráfico de pastel 3‑D y aplicando estilos avanzados. Con Aspose.Cells for Java dispone de una forma fiable y agnóstica de versión para incrustar visualizaciones 3‑D ricas directamente en libros de trabajo Excel e incluso **exportar gráfico como imagen** para su uso en paneles o informes.

## Preguntas frecuentes

**P: ¿Cómo puedo agregar múltiples series de datos a un gráfico 3D?**  
R: Use `chart.getNSeries().add()` para cada rango de serie y asegúrese de que el tipo de gráfico siga siendo 3‑D (por ejemplo, `ChartType.BAR_3_D` o `ChartType.PIE_3_D`).

**P: ¿Puedo exportar los gráficos 3D creados con Aspose.Cells for Java a otros formatos?**  
R: Sí, puede guardar el gráfico como PNG, JPEG o PDF llamando a la sobrecarga adecuada de `chart.toImage()` o a `workbook.save()` con un formato de imagen o PDF, cumpliendo el requisito **convertir gráfico png**.

**P: ¿Es posible crear gráficos 3D interactivos con Aspose.Cells for Java?**  
R: Aspose.Cells se centra en gráficos estáticos de Excel. Para visualizaciones 3‑D interactivas basadas en la web, considere combinar los datos de Excel con bibliotecas JavaScript como Three.js.

**P: ¿Puedo automatizar el proceso de actualización de datos en mis gráficos 3D?**  
R: Absolutamente. Cargue nuevos datos en la hoja de cálculo de forma programática y actualice el rango del gráfico; la próxima vez que se abra el libro de trabajo, el gráfico reflejará los valores actualizados.

**P: ¿Dónde puedo encontrar más recursos y documentación para Aspose.Cells for Java?**  
R: Puede encontrar documentación y recursos completos para Aspose.Cells for Java en el sitio web: [Aspose.Cells for Java Documentation](https://reference.aspose.com/cells/java/).

---

**Última actualización:** 2026-08-21  
**Probado con:** Aspose.Cells for Java 24.12 (última)  
**Autor:** Aspose

## Tutoriales relacionados

- [Crear gráficos de pastel en Excel usando Aspose.Cells for Java: Guía completa](/cells/java/charts-graphs/master-pie-chart-creation-excel-aspose-cells-java/)
- [aspose cells java – Crear gráfico de Excel con anotaciones](/cells/java/advanced-excel-charts/chart-annotations/)
- [Agregar etiquetas de datos a un gráfico de Excel con Aspose.Cells Java](/cells/java/advanced-excel-charts/chart-interactivity/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}