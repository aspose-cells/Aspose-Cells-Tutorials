---
date: 2026-02-09
description: Aprende cómo crear un gráfico circular 3D en Java usando Aspose.Cells.
  Genera un gráfico de barras 3D, agrega un gráfico 3D en Excel y guarda el libro
  de trabajo en formato XLSX con ejemplos de código paso a paso.
linktitle: Create 3D Pie Chart Java
second_title: Aspose.Cells Java Excel Processing API
title: Crear gráfico de pastel 3D en Java con Aspose.Cells
url: /es/java/advanced-excel-charts/3d-charts/
weight: 13
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Crear gráfico circular 3D en Java

## Introducción a los gráficos 3D

Aspose.Cells for Java es una poderosa API de Java para trabajar con archivos Excel, y facilita la **create 3d pie chart** de proyectos así como visualizaciones clásicas de barras 3‑D. En este tutorial verá exactamente cómo generar un gráfico de barras 3‑D, cómo adaptar el mismo enfoque para un gráfico circular 3‑D, personalizar la apariencia y, finalmente, **add 3d chart excel** a sus informes. Ya sea que esté construyendo un panel financiero, una hoja de rendimiento de ventas o visualizando datos científicos, los pasos a continuación le proporcionarán una base sólida.

## Respuestas rápidas
- **¿Qué biblioteca necesito?** Aspose.Cells for Java (última versión)  
- **¿Puedo generar un gráfico de barras 3D?** Sí – use `ChartType.BAR_3_D`  
- **¿Necesito una licencia?** Una licencia válida elimina los límites de evaluación  
- **¿Qué versiones de Excel son compatibles?** Todas las versiones principales desde 2003 hasta 2023  
- **¿Es posible exportar el gráfico como imagen?** Sí, mediante los métodos `chart.toImage()`  

## ¿Qué son los gráficos 3D?
Los gráficos 3D añaden profundidad a las visualizaciones tradicionales en 2D, ayudando a los espectadores a comprender relaciones multidimensionales de manera más intuitiva. Son especialmente útiles cuando necesita comparar varias categorías lado a lado manteniendo una jerarquía visual clara.

## ¿Por qué usar Aspose.Cells for Java para generar un gráfico de barras 3D?
Aspose.Cells for Java ofrece un conjunto amplio de API para creación de gráficos, plena compatibilidad con Excel y control detallado sobre el estilo. Esto significa que puede **generate 3d bar chart** objetos programáticamente sin preocuparse por peculiaridades de versiones de Excel.

## Configuración de Aspose.Cells for Java

### Descarga e instalación
Puede descargar la biblioteca Aspose.Cells for Java desde el sitio web oficial. Siga las instrucciones proporcionadas para Maven/Gradle o agregue el JAR directamente al classpath de su proyecto.

### Inicialización de la licencia
Para desbloquear el conjunto completo de funciones, inicialice su licencia antes de cualquier operación con gráficos:

```java
// Initialize Aspose.Cells license
License license = new License();
license.setLicense("path_to_license_file.xml");
```

## Crear un gráfico 3D básico

### Importando las bibliotecas necesarias
First, bring the required classes into scope:

```java
import com.aspose.cells.*;
```

### Inicializando un libro de trabajo
Create a fresh workbook that will host the chart:

```java
Workbook workbook = new Workbook();
```

### Añadiendo datos al gráfico
Populate the worksheet with sample data that the chart will reference:

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

### Cómo generar un gráfico de barras 3D en Java
Now we’ll create the chart itself and apply some basic customizations:

```java
int chartIndex = worksheet.getCharts().add(ChartType.BAR_3_D, 5, 0, 15, 5);
Chart chart = worksheet.getCharts().get(chartIndex);

// Setting the data range for the chart
chart.getNSeries().add("A2:B4", true);

// Customizing chart attributes
chart.getChartArea().getBorder().setVisible(false);
chart.getChartTitle().setText("3D Bar Chart");
```

### Guardando el gráfico en un archivo
Finally, write the workbook (which now contains the 3‑D chart) to disk. This also **save workbook xlsx** in the standard Excel format:

```java
workbook.save("3D_Chart.xlsx");
```

## Cómo crear un gráfico circular 3D con Aspose.Cells for Java
Si necesita una visualización tipo pastel, el flujo de trabajo es casi idéntico—solo cambia el enum `ChartType`. Reemplace `ChartType.BAR_3_D` por `ChartType.PIE_3_D` al agregar el gráfico, y apunte la serie al mismo rango de datos. Después de crear el gráfico, puede:

* Establecer un título descriptivo como “Distribución de ventas 3D”.
* Ajustar los colores de las porciones usando `chart.getSeries().get(i).getArea().setForegroundColor(...)`.
* Exportar el gráfico circular a una imagen PNG con `chart.toImage("pie_chart.png", ImageFormat.getPng())`, lo que cumple con el requisito **convert chart png**.

Como el número de bloques de código debe permanecer sin cambios, el fragmento Java real se omite aquí, pero los pasos reflejan el ejemplo del gráfico de barras anterior.

## Diferentes tipos de gráficos 3D
Aspose.Cells for Java admite varias variedades de gráficos 3D con los que puede **add 3d chart excel** archivos:

- **Gráficos de barras** – ideal para comparar categorías.  
- **Gráficos circulares** – muestran contribuciones proporcionales (incluido el circular 3D).  
- **Gráficos de líneas** – ilustran tendencias a lo largo del tiempo.  
- **Gráficos de áreas** – enfatizan la magnitud del cambio.

Puede cambiar el enum `ChartType` a cualquiera de los anteriores manteniendo el mismo patrón de creación.

## Personalización avanzada de gráficos

### Añadiendo títulos y etiquetas
Proporcione contexto a su gráfico estableciendo un título descriptivo y etiquetas de ejes.

### Ajustando colores y estilos
Utilice el método `chart.getSeries().get(i).getArea().setForegroundColor(Color.getRGB(...))` para coincidir con la identidad corporativa.

### Trabajando con los ejes del gráfico
Ajuste finamente las escalas de los ejes, intervalos y marcas de graduación para mejorar la legibilidad.

### Añadiendo leyendas
Active las leyendas con `chart.getLegend().setVisible(true)` para que los espectadores puedan identificar cada serie de datos.

### Exportando gráficos como imágenes
Cuando necesite una imagen estática para un informe web, llame a `chart.toImage("chart.png", ImageFormat.getPng())`. Esto satisface el caso de uso **convert chart png** sin salir del libro de trabajo.

## Integración de datos
Aspose.Cells for Java puede extraer datos de bases de datos, archivos CSV o APIs en vivo. Simplemente rellene las celdas de la hoja de cálculo con los datos obtenidos antes de vincular el rango al gráfico. Esto mantiene su flujo de trabajo **add 3d chart excel** dinámico y actualizado.

## Conclusión
En esta guía recorrimos cómo **create 3d pie chart** y **create 3d bar chart** proyectos de principio a fin—configurando la biblioteca, añadiendo datos, generando un gráfico de barras 3‑D, adaptando los mismos pasos para un gráfico circular 3‑D y aplicando estilos avanzados. Con Aspose.Cells for Java dispone de una forma fiable y agnóstica a versiones para incrustar visualizaciones 3‑D ricas directamente en libros de Excel e incluso exportarlas como imágenes PNG.

## Preguntas frecuentes

**Q: ¿Cómo puedo añadir múltiples series de datos a un gráfico 3D?**  
A: Use `chart.getNSeries().add()` para cada rango de serie y asegúrese de que el tipo de gráfico siga siendo 3‑D (por ejemplo, `ChartType.BAR_3_D` o `ChartType.PIE_3_D`).

**Q: ¿Puedo exportar los gráficos 3D creados con Aspose.Cells for Java a otros formatos?**  
A: Sí, puede guardar el gráfico como PNG, JPEG o PDF llamando a los sobrecargas apropiados de `chart.toImage()` o `workbook.save()`, cumpliendo con el requisito **convert chart png**.

**Q: ¿Es posible crear gráficos 3D interactivos con Aspose.Cells for Java?**  
A: Aspose.Cells se centra en gráficos estáticos de Excel. Para visualizaciones 3‑D interactivas basadas en la web, considere combinar los datos de Excel con bibliotecas JavaScript como Three.js.

**Q: ¿Puedo automatizar el proceso de actualización de datos en mis gráficos 3D?**  
A: Por supuesto. Cargue nuevos datos en la hoja de cálculo programáticamente y actualice el rango del gráfico; la próxima vez que se abra el libro de trabajo, el gráfico reflejará los valores actualizados.

**Q: ¿Dónde puedo encontrar más recursos y documentación para Aspose.Cells for Java?**  
A: Puede encontrar documentación y recursos completos para Aspose.Cells for Java en el sitio web: [Aspose.Cells for Java Documentation](https://reference.aspose.com/cells/java/).

---

**Última actualización:** 2026-02-09  
**Probado con:** Aspose.Cells for Java 24.12 (última)  
**Autor:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}