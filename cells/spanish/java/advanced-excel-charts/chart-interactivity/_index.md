---
date: 2025-12-06
description: Aprende a cambiar el tipo de gráfico en Excel y crear gráficos interactivos
  con Java usando Aspose.Cells. Añade descripciones emergentes al gráfico, etiquetas
  de datos y desglose para una visualización de datos más rica.
linktitle: Change Excel Chart Type
second_title: Aspose.Cells Java Excel Processing API
title: Cambiar el tipo de gráfico de Excel con Aspose.Cells Java
url: /es/java/advanced-excel-charts/chart-interactivity/
weight: 19
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Cambiar el tipo de gráfico de Excel y agregar interactividad

## Introducción

Los gráficos interactivos le dan a sus informes de Excel un nuevo nivel de visión, permitiendo a los usuarios pasar el cursor, hacer clic y explorar los puntos de datos directamente. En este tutorial **cambiará el tipo de gráfico de Excel** y **creará soluciones de gráficos interactivos en Java** con Aspose.Cells para Java. Revisaremos cómo agregar tooltips al gráfico, etiquetas de datos y un hipervínculo simple de drill‑down para que su audiencia pueda profundizar en los números.

## Respuestas rápidas
- **¿Qué biblioteca se usa?** Aspose.Cells para Java  
- **¿Puedo cambiar el tipo de gráfico?** Sí – simplemente modifique el enum `ChartType` al crear el gráfico.  
- **¿Cómo agrego tooltips a un gráfico?** Use la API de etiquetas de datos (`setHasDataLabels(true)`) y habilite la visualización de valores.  
- **¿Se admite drill‑down?** Puede adjuntar hipervínculos a los puntos de datos para un comportamiento básico de drill‑down.  
- **¿Requisitos previos?** IDE de Java, JAR de Aspose.Cells y un archivo Excel con datos de muestra.

## Requisitos previos

Antes de comenzar, asegúrese de contar con lo siguiente:

- Entorno de desarrollo Java (JDK 8+ recomendado)  
- Biblioteca Aspose.Cells para Java (descárguela desde [aquí](https://releases.aspose.com/cells/java/))  
- Un libro de trabajo de muestra (`data.xlsx`) que contenga los datos que desea visualizar  

## Paso 1: Configurar su proyecto Java

1. Cree un nuevo proyecto Java en su IDE favorito (IntelliJ IDEA, Eclipse, etc.).  
2. Agregue el JAR de Aspose.Cells a la ruta de compilación de su proyecto o a las dependencias de Maven/Gradle.

## Paso 2: Cargar datos

Para trabajar con gráficos primero necesita un libro de trabajo cargado en memoria.

```java
// Load the Excel file
Workbook workbook = new Workbook("data.xlsx");
Worksheet worksheet = workbook.getWorksheets().get(0);
```

## Paso 3: Crear un gráfico (y cambiar su tipo)

Puede elegir cualquier tipo de gráfico que se ajuste a su análisis. A continuación creamos un **gráfico de columnas**, pero puede cambiar fácilmente a un gráfico de líneas, pastel o barras modificando el enum `ChartType`.

```java
// Create a column chart
int chartIndex = worksheet.getCharts().add(ChartType.COLUMN, 5, 0, 15, 5);
Chart chart = worksheet.getCharts().get(chartIndex);
```

> **Consejo:** Para **cambiar el tipo de gráfico de Excel**, reemplace `ChartType.COLUMN` con `ChartType.LINE`, `ChartType.PIE`, etc.

## Paso 4: Agregar interactividad

### 4.1. Agregar tooltips (Agregar tooltips al gráfico)

Los tooltips aparecen cuando el usuario pasa el cursor sobre un punto de datos. El siguiente código habilita las etiquetas de datos y muestra el valor como tooltip.

```java
// Enable tooltips for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowValue(true);
```

### 4.2. Agregar etiquetas de datos

Las etiquetas de datos proporcionan una pista visual permanente en el propio gráfico. Puede mostrarlas como llamadas para una mejor legibilidad.

```java
// Enable data labels for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowLabelAsDataCallout(true);
```

### 4.3. Implementar Drill‑Down (Hipervínculo en un punto de datos)

Una forma sencilla de agregar capacidad de drill‑down es adjuntar un hipervínculo a un punto específico. Al hacer clic en el punto se abre una página web con información detallada.

```java
// Add a hyperlink to a data point
String url = "https://example.com/data-details";
chart.getNSeries().get(0).getPoints().get(0).getHyperlinks().add(url);
```

## Paso 5: Guardar el libro de trabajo

Después de configurar el gráfico, persista el libro de trabajo para que las funciones interactivas se almacenen en el archivo de salida.

```java
// Save the workbook
workbook.save("interactive_chart_output.xlsx");
```

## Problemas comunes y soluciones

| Problema | Solución |
|----------|----------|
| **Los tooltips no se muestran** | Asegúrese de que `setHasDataLabels(true)` se llame antes de configurar `setShowValue(true)`. |
| **El hipervínculo no es clicable** | Verifique que el formato de salida admita hipervínculos (p. ej., XLSX, no CSV). |
| **El tipo de gráfico no cambia** | Revise que haya modificado el enum `ChartType` correcto al agregar el gráfico. |

## Preguntas frecuentes

**Q: ¿Cómo puedo cambiar el tipo de gráfico después de haberlo creado?**  
A: Necesita crear un nuevo gráfico con el `ChartType` deseado. Aspose.Cells no proporciona una conversión in‑place del tipo, por lo que debe eliminar el gráfico antiguo y agregar uno nuevo.

**Q: ¿Puedo personalizar la apariencia de los tooltips?**  
A: Sí. Use las propiedades de `DataLabel` como `setFontSize`, `setFontColor` y `setBackgroundColor` para estilizar el texto del tooltip.

**Q: ¿Cómo manejo las interacciones del usuario en una aplicación web?**  
A: Exporte el libro de trabajo a un archivo HTML o XLSX y use JavaScript del lado del cliente para capturar eventos de clic en los elementos del gráfico.

**Q: ¿Dónde puedo encontrar más ejemplos y documentación?**  
A: Visite la [Referencia de API de Aspose.Cells Java](https://reference.aspose.com/cells/java/) para obtener una lista completa de clases y métodos relacionados con gráficos.

## Conclusión

Ahora sabe cómo **cambiar el tipo de gráfico de Excel**, **crear soluciones de gráficos interactivos en Java** y enriquecerlos con tooltips, etiquetas de datos y hipervínculos de drill‑down usando Aspose.Cells para Java. Estas mejoras hacen que sus informes de Excel sean mucho más atractivos y reveladores para los usuarios finales.

---

**Última actualización:** 2025-12-06  
**Probado con:** Aspose.Cells para Java 24.12  
**Autor:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}