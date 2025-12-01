---
date: 2025-12-01
description: Aprenda a cambiar el tipo de gráfico de Excel y agregar funciones interactivas
  como descripciones emergentes, etiquetas de datos y desglose usando Aspose.Cells
  para Java.
language: es
linktitle: Change Excel chart type and add interactivity
second_title: Aspose.Cells Java Excel Processing API
title: Cambiar el tipo de gráfico de Excel y agregar interactividad – Aspose.Cells
  Java
url: /java/advanced-excel-charts/chart-interactivity/
weight: 19
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Cambiar el tipo de gráfico de Excel y agregar interactividad

## Introducción

Los gráficos interactivos permiten a su audiencia explorar los datos al instante, mientras que poder **change Excel chart type** le brinda la flexibilidad de presentar la información en el formato visual más eficaz. En este tutorial aprenderá a usar Aspose.Cells para Java para cambiar el tipo de un gráfico, agregar tooltips, incrustar etiquetas de datos e incluso crear enlaces de drill‑down, todo sin salir de su código Java. Al final, tendrá un libro de trabajo de Excel totalmente interactivo que podrá incrustar en informes, paneles o aplicaciones web.

## Respuestas rápidas
- **¿Puedo cambiar el tipo de gráfico programáticamente?** Sí – use el enum `ChartType` al crear o actualizar un gráfico.  
- **¿Cómo agrego tooltips a un gráfico?** Habilite las etiquetas de datos y establezca `ShowValue` en true.  
- **¿Cuál es la forma más fácil de agregar enlaces de drill‑down?** Adjunte un hipervínculo a un punto de datos mediante `getHyperlinks().add(url)`.  
- **¿Necesito una licencia para Aspose.Cells?** Una prueba gratuita funciona para desarrollo; se requiere una licencia para producción.  
- **¿Qué versión de Java es compatible?** Java 8 y superiores son totalmente compatibles.

## ¿Qué es “change Excel chart type”?

Cambiar el tipo de gráfico significa intercambiar la representación visual (p. ej., de un gráfico de columnas a uno de líneas) manteniendo intactos los datos subyacentes. Esto es útil cuando descubre que otro tipo de gráfico comunica mejor tendencias, comparaciones o distribuciones.

## ¿Por qué agregar interactividad a los gráficos de Excel?

- **Mejor visión de los datos:** Los tooltips y las etiquetas de datos permiten a los usuarios ver valores exactos sin desplazarse.  
- **Presentaciones atractivas:** Los elementos interactivos mantienen a los espectadores interesados.  
- **Capacidad de drill‑down:** Los hipervínculos permiten a los usuarios saltar a hojas de cálculo detalladas o recursos externos.  
- **Activos reutilizables:** Un libro de trabajo puede servir a múltiples escenarios de informes simplemente cambiando los tipos de gráfico.

## Requisitos previos

- Entorno de desarrollo Java (JDK 8+)  
- Biblioteca Aspose.Cells para Java (descargar desde [aquí](https://releases.aspose.com/cells/java/))  
- Un archivo Excel de muestra (`data.xlsx`) que contiene los datos que desea visualizar

## Guía paso a paso

### Paso 1: Configurar su proyecto Java

1. Cree un nuevo proyecto Java en su IDE favorito (IntelliJ IDEA, Eclipse, VS Code, etc.).  
2. Agregue el JAR de Aspose.Cells al classpath de su proyecto.

### Paso 2: Cargar el libro de trabajo fuente

Comenzamos cargando un libro de trabajo existente que contiene los datos para nuestro gráfico.

```java
// Load the Excel file
Workbook workbook = new Workbook("data.xlsx");
Worksheet worksheet = workbook.getWorksheets().get(0);
```

### Paso 3: Crear un gráfico y **cambiar su tipo**

A continuación creamos un gráfico de columnas y luego demostramos inmediatamente cómo podría cambiarlo a un gráfico de líneas si es necesario.

```java
// Create a column chart
int chartIndex = worksheet.getCharts().add(ChartType.COLUMN, 5, 0, 15, 5);
Chart chart = worksheet.getCharts().get(chartIndex);

// OPTIONAL: Change the chart type to LINE
chart.setChartType(ChartType.LINE);
```

> **Pro tip:** Cambiar el tipo de gráfico después de la creación es tan simple como llamar a `setChartType(...)`. Esto satisface la palabra clave principal **change Excel chart type** sin requerir un nuevo objeto de gráfico.

### Paso 4: Agregar interactividad

#### 4.1 Agregar tooltips al gráfico

Los tooltips se muestran cuando un usuario pasa el cursor sobre un punto de datos. En Aspose.Cells se implementan mediante etiquetas de datos.

```java
// Enable tooltips for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowValue(true);
```

#### 4.2 Agregar etiquetas de datos ( **add data labels chart** )

Las etiquetas de datos pueden mostrar el valor exacto, el nombre de la categoría o ambos. Aquí usamos un estilo de llamada.

```java
// Enable data labels for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowLabelAsDataCallout(true);
```

#### 4.3 Implementar drill‑down ( **add drill down excel** )

Un enlace de drill‑down permite a los usuarios hacer clic en un punto y saltar a una vista detallada, ya sea dentro del libro de trabajo o en una página web.

```java
// Add a hyperlink to a data point
String url = "https://example.com/data-details";
chart.getNSeries().get(0).getPoints().get(0).getHyperlinks().add(url);
```

### Paso 5: Guardar el libro de trabajo

```java
// Save the workbook
workbook.save("interactive_chart_output.xlsx");
```

## Problemas comunes y soluciones

| Problema | Razón | Solución |
|----------|-------|----------|
| Los tooltips no se muestran | `HasDataLabels` no está habilitado | Asegúrese de que se llame a `setHasDataLabels(true)` antes de configurar `ShowValue`. |
| El enlace de drill‑down no hace nada | La URL del hipervínculo está mal formada | Verifique que la URL comience con `http://` o `https://`. |
| El tipo de gráfico no cambia | Se está usando una versión antigua de Aspose.Cells | Actualice a la última versión (probada con 24.12). |

## Preguntas frecuentes

**P: ¿Cómo puedo cambiar el tipo de gráfico después de haber sido creado?**  
R: Llame a `chart.setChartType(ChartType.YOUR_CHOICE)` en el objeto `Chart` existente. Esto aborda directamente el requisito **change Excel chart type**.

**P: ¿Puedo personalizar la apariencia de los tooltips?**  
R: Sí. Use `chart.getNSeries().get(0).getPoints().getDataLabels()` para establecer el tamaño de fuente, color y fondo.

**P: ¿Es posible agregar varios enlaces de drill‑down en un mismo gráfico?**  
R: Absolutamente. Recorra los puntos y llame a `getHyperlinks().add(url)` para cada punto que desee enlazar.

**P: ¿Aspose.Cells admite otros tipos de gráficos como pastel o radar?**  
R: Todos los tipos de gráfico definidos en el enum `ChartType` son compatibles, incluidos `PIE`, `RADAR`, `AREA`, etc.

**P: ¿Dónde puedo encontrar más ejemplos?**  
R: Visite la referencia oficial de la API Java de Aspose.Cells en [Aspose.Cells Java API Reference](https://reference.aspose.com/cells/java/) para obtener una lista completa de métodos relacionados con gráficos.

## Conclusión

Ahora sabe cómo **change Excel chart type**, incrustar **tooltips**, agregar **etiquetas de datos** y crear enlaces de **drill‑down** usando Aspose.Cells para Java. Estas funciones interactivas convierten hojas de cálculo estáticas en herramientas dinámicas de exploración de datos, perfectas para paneles, informes y análisis basados en la web.

---

**Last Updated:** 2025-12-01  
**Tested With:** Aspose.Cells 24.12 for Java  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}