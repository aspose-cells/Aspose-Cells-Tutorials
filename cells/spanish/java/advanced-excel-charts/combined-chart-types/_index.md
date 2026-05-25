---
date: 2026-02-14
description: Aprenda a exportar un gráfico a PNG, añadir series de datos, combinar
  un gráfico de líneas y columnas, guardar el libro de trabajo como XLSX y añadir
  una leyenda al gráfico usando Aspose.Cells para Java.
linktitle: Export chart to PNG and add data series for combined chart
second_title: Aspose.Cells Java Excel Processing API
title: Exportar gráfico a PNG y agregar series de datos para gráfico combinado
url: /es/java/advanced-excel-charts/combined-chart-types/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Exportar gráfico a PNG y agregar series de datos para gráfico combinado

En este tutorial **agregarás series de datos** a un libro de Excel, **combinarás elementos de gráfico de líneas y columnas**, y aprenderás cómo **exportar el gráfico a PNG** usando Aspose.Cells for Java. Recorreremos cada paso—desde configurar el libro, agregar el gráfico a una hoja de cálculo, personalizar la leyenda, hasta **guardar el libro como xlsx** y generar una imagen PNG del gráfico. Al final, tendrás un gráfico combinado listo para usar que podrás incrustar en informes o paneles.

## Respuestas rápidas
- **¿Qué biblioteca crea gráficos combinados?** Aspose.Cells for Java  
- **¿Cómo agrego una serie de datos?** Use `chart.getNSeries().add(...)`  
- **¿Cómo puedo exportar el gráfico a png?** Call `chart.toImage("file.png", ImageFormat.getPng())`  
- **¿En qué formato de archivo puedo guardar el libro?** Standard `.xlsx` (save workbook as xlsx)  
- **¿Necesito una licencia para producción?** A valid Aspose.Cells license is required  

## Qué es **exportar gráfico a PNG** en Aspose.Cells?
Exportar un gráfico a PNG crea una imagen raster del gráfico de Excel que puede mostrarse en páginas web, informes o correos electrónicos sin requerir la aplicación Excel.

## ¿Por qué crear un **gráfico combinado de línea y columna**?
Un gráfico combinado te permite mostrar diferentes conjuntos de datos con representaciones visuales distintas (por ejemplo, una serie de línea sobre una serie de columnas) en una sola vista. Esto es perfecto para comparar tendencias con totales, resaltar correlaciones o ofrecer información más rica en un formato compacto.

## Requisitos previos
- Java Development Kit (JDK) 8 o superior  
- Biblioteca Aspose.Cells for Java (descargar desde el enlace a continuación)  
- Familiaridad básica con la sintaxis de Java y conceptos de Excel  

## Comenzando

Primero, descarga la biblioteca Aspose.Cells for Java desde el sitio oficial:

[Download Aspose.Cells for Java](https://releases.aspose.com/cells/java/)

Una vez que el JAR se agrega al classpath de tu proyecto, puedes comenzar a crear el gráfico.

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

### Paso 4: Agregar un objeto de gráfico combinado a la hoja de cálculo  
Comenzaremos con un gráfico de líneas y luego agregaremos una serie de columnas para lograr un efecto de **gráfico combinado de línea y columna**.
```java
int chartIndex = worksheet.getCharts().add(ChartType.LINE, 0, 0, 20, 10);
Chart chart = worksheet.getCharts().get(chartIndex);
```

## Agregar datos al gráfico

Ahora que el contenedor del gráfico existe, necesitamos alimentarlo con datos.

### Paso 5: Definir los rangos de datos y **agregar series de datos**
```java
Cells cells = worksheet.getCells();
chart.getNSeries().add("A1:A5", true);
chart.getNSeries().add("B1:B5", true);
```
> **Consejo profesional:** El primer parámetro (`"A1:A5"`) es el rango para la primera serie, y el segundo (`"B1:B5"`) crea una segunda serie que se combinará con la primera.

### Paso 6: Establecer los datos de la categoría (eje X)
```java
chart.getNSeries().setCategoryData("C1:C5");
```

## Personalizando el gráfico

Un buen gráfico cuenta una historia. Démosle títulos, etiquetas de ejes y una leyenda clara.

### Paso 7: **Establecer etiquetas de los ejes del gráfico** y título
```java
chart.getTitle().setText("Combined Chart Example");
chart.getCategoryAxis().getTitle().setText("Categories");
chart.getValueAxis().getTitle().setText("Values");
```

### Paso 8: **Agregar leyenda al gráfico** y ajustar su posición
```java
chart.getLegend().setPosition(LegendPositionType.BOTTOM);
chart.getLegend().setOverlay(true);
```

## Guardar y exportar el gráfico

Después de personalizar, querrás **guardar el libro como xlsx** y también generar una imagen.

### Paso 9: Guardar el libro como archivo Excel (xlsx)
```java
workbook.save("CombinedChart.xlsx");
```

### Paso 10: **Exportar gráfico a PNG**
```java
chart.toImage("CombinedChart.png", ImageFormat.getPng());
```
> El método `chart.toImage` **genera imágenes de gráficos de Excel** que pueden usarse en páginas web, informes o correos electrónicos.

## Problemas comunes y solución de problemas

| Problema | Solución |
|----------|----------|
| **No aparecen datos** | Verifica que los rangos de celdas (`A1:A5`, `B1:B5`, `C1:C5`) realmente contengan datos antes de crear el gráfico. |
| **La leyenda se superpone al gráfico** | Establece `chart.getLegend().setOverlay(false)` o mueve la leyenda a una posición diferente (p. ej., `RIGHT`). |
| **El archivo de imagen está vacío** | Asegúrate de que el gráfico tenga al menos una serie y que `chart.toImage` se llame después de todas las personalizaciones. |
| **Al guardar se lanza una excepción** | Comprueba que tienes permisos de escritura en el directorio de destino y que el archivo no esté abierto en Excel. |

## Preguntas frecuentes

**Q: ¿Cómo instalo Aspose.Cells for Java?**  
A: Descarga el JAR del sitio oficial y agrégalo al classpath de tu proyecto. El enlace de descarga es: [Download Aspose.Cells for Java](https://releases.aspose.com/cells/java/).

**Q: ¿Puedo crear otros tipos de gráficos además de línea y columna?**  
A: Sí, Aspose.Cells soporta gráficos de barras, pastel, dispersión, área y muchos más tipos. Consulta la documentación de la API para la lista completa.

**Q: ¿Se requiere una licencia para uso en producción?**  
A: Se requiere una licencia válida de Aspose.Cells para despliegues en producción. Hay una prueba gratuita disponible para evaluación.

**Q: ¿Cómo puedo cambiar los colores de cada serie?**  
A: Usa `chart.getNSeries().get(i).setAreaColor(Color.getRed())` (o similar) después de agregar la serie.

**Q: ¿Dónde puedo encontrar más ejemplos de código?**  
A: La documentación completa y ejemplos adicionales están disponibles en el sitio de referencia de Aspose: [here](https://reference.aspose.com/cells/java/).

---

**Última actualización:** 2026-02-14  
**Probado con:** Aspose.Cells for Java última versión  
**Autor:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}