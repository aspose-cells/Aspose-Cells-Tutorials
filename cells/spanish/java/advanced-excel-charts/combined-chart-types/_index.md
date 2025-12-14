---
date: 2025-12-06
description: Aprenda cómo agregar series de datos, crear tipos de gráficos combinados,
  guardar el libro de trabajo de Excel y exportar el gráfico a PNG con Aspose.Cells
  para Java.
linktitle: Add data series to create combined chart using Aspose.Cells
second_title: Aspose.Cells Java Excel Processing API
title: Agregar series de datos para crear un gráfico combinado usando Aspose.Cells
url: /es/java/advanced-excel-charts/combined-chart-types/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Agregar series de datos para crear un gráfico combinado usando Aspose.Cells

En este tutorial **agregarás series de datos** a un libro de Excel y aprenderás cómo **crear tipos de gráficos combinados** con Aspose.Cells para Java. Recorreremos cada paso—desde configurar el libro, agregar series, personalizar la leyenda, hasta **guardar archivos Excel** del libro y exportar el **gráfico a PNG**. Al final, tendrás un gráfico combinado listo para usar que podrás incrustar en informes o paneles.

## Respuestas rápidas
- **¿Qué biblioteca crea gráficos combinados?** Aspose.Cells for Java  
- **¿Cómo agrego una serie de datos?** Use `chart.getNSeries().add(...)`  
- **¿Puedo exportar el gráfico como una imagen?** Sí, con `chart.toImage(...)` (PNG)  
- **¿En qué formato de archivo puedo guardar el libro?** Standard `.xlsx` (Excel)  
- **¿Necesito una licencia para producción?** Se requiere una licencia válida de Aspose.Cells  

## Qué es **add data series** en Aspose.Cells?
Agregar una serie de datos indica al gráfico qué celdas contienen los valores que deseas trazar. Cada serie puede representar una línea, columna u otro tipo de gráfico, y puedes combinarlas para crear un **gráfico combinado**.

## ¿Por qué crear un **gráfico combinado**?
Un gráfico combinado te permite mostrar diferentes conjuntos de datos con representaciones visuales distintas (por ejemplo, una serie de línea sobre una serie de columnas) en una sola vista. Esto es perfecto para comparar tendencias con totales, resaltar correlaciones o ofrecer insights más ricos en un formato compacto.

## Requisitos previos
- Java Development Kit (JDK) 8 o superior  
- Biblioteca Aspose.Cells para Java (descargar desde el enlace a continuación)  
- Familiaridad básica con la sintaxis de Java y conceptos de Excel  

## Comenzando

Primero, descarga la biblioteca Aspose.Cells para Java desde el sitio oficial:

[Download Aspose.Cells for Java](https://releases.aspose.com/cells/java/)

Una vez que el JAR se agrega al classpath de tu proyecto, puedes comenzar a construir el gráfico.

### Paso 1: Importar clases de Aspose.Cells
```java
import com.aspose.cells.*;
```

### Paso 2: Crear un nuevo libro de trabajo
```java
Workbook workbook = new Workbook();
```

### Paso 3: Acceder a la primera hoja de cálculo
```java
Worksheet worksheet = workbook.getWorksheets().get(0);
```

### Paso 4: Agregar un objeto de gráfico combinado  
Comenzaremos con un gráfico de líneas y luego agregaremos otras series para lograr un efecto de **gráfico combinado**.
```java
int chartIndex = worksheet.getCharts().add(ChartType.LINE, 0, 0, 20, 10);
Chart chart = worksheet.getCharts().get(chartIndex);
```

## Agregar datos al gráfico

Ahora que el contenedor del gráfico existe, necesitamos alimentarlo con datos.

### Paso 5: Definir los rangos de datos y **add data series**
```java
Cells cells = worksheet.getCells();
chart.getNSeries().add("A1:A5", true);
chart.getNSeries().add("B1:B5", true);
```
> **Pro tip:** El primer parámetro (`"A1:A5"`) es el rango para la primera serie, y el segundo (`"B1:B5"`) crea una segunda serie que se combinará con la primera.

### Paso 6: Establecer los datos de la categoría (eje X)
```java
chart.getNSeries().setCategoryData("C1:C5");
```

## Personalizando el gráfico

Un buen gráfico cuenta una historia. Démosle títulos, etiquetas de ejes y una leyenda clara.

### Paso 7: Establecer el título del gráfico y las etiquetas de los ejes
```java
chart.getTitle().setText("Combined Chart Example");
chart.getCategoryAxis().getTitle().setText("Categories");
chart.getValueAxis().getTitle().setText("Values");
```

### Paso 8: **Add legend chart** y ajustar su posición
```java
chart.getLegend().setPosition(LegendPositionType.BOTTOM);
chart.getLegend().setOverlay(true);
```

## Guardando y exportando el gráfico

Después de personalizar, querrás **guardar archivos Excel** y también generar una imagen.

### Paso 9: Guardar el libro de trabajo como archivo Excel
```java
workbook.save("CombinedChart.xlsx");
```

### Paso 10: Exportar el **chart to PNG**
```java
chart.toImage("CombinedChart.png", ImageFormat.getPng());
```
> El método `chart.toImage` **generates excel chart** imágenes que pueden usarse en páginas web, informes o correos electrónicos.

## Problemas comunes y solución de problemas

| Problema | Solución |
|----------|----------|
| **No aparecen datos** | Verifica que los rangos de celdas (`A1:A5`, `B1:B5`, `C1:C5`) realmente contengan datos antes de crear el gráfico. |
| **La leyenda se superpone al gráfico** | Configura `chart.getLegend().setOverlay(false)` o mueve la leyenda a una posición diferente (p. ej., `RIGHT`). |
| **El archivo de imagen está en blanco** | Asegúrate de que el gráfico tenga al menos una serie y que `chart.toImage` se llame después de todas las personalizaciones. |
| **Al guardar se lanza una excepción** | Comprueba que tienes permisos de escritura en el directorio de destino y que el archivo no esté abierto en Excel. |

## Preguntas frecuentes

**P: ¿Cómo instalo Aspose.Cells para Java?**  
R: Descarga el JAR desde el sitio oficial y agrégalo al classpath de tu proyecto. El enlace de descarga es: [Download Aspose.Cells for Java](https://releases.aspose.com/cells/java/).

**P: ¿Puedo crear otros tipos de gráficos además de línea y columna?**  
R: Sí, Aspose.Cells admite gráficos de barras, pastel, dispersión, área y muchos más tipos de gráficos. Consulta la documentación de la API para la lista completa.

**P: ¿Se requiere una licencia para uso en producción?**  
R: Se requiere una licencia válida de Aspose.Cells para implementaciones en producción. Hay una prueba gratuita disponible para evaluación.

**P: ¿Cómo puedo cambiar los colores de cada serie?**  
R: Usa `chart.getNSeries().get(i).setAreaColor(Color.getRed())` (o similar) después de agregar la serie.

**P: ¿Dónde puedo encontrar más ejemplos de código?**  
R: La documentación completa y ejemplos adicionales están disponibles en el sitio de referencia de Aspose: [here](https://reference.aspose.com/cells/java/).

---

**Last Updated:** 2025-12-06  
**Tested With:** Aspose.Cells for Java 24.12  
**Author:** Aspose

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
