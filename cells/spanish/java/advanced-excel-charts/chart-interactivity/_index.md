---
date: 2025-11-28
description: Aprenda cómo agregar información sobre herramientas, etiquetas de datos
  y funciones de desglose para crear un gráfico interactivo en Java usando Aspose.Cells.
language: es
linktitle: How to Add Tooltips in Interactive Charts
second_title: Aspose.Cells Java Excel Processing API
title: Cómo agregar información sobre herramientas en gráficos interactivos (Aspose.Cells
  Java)
url: /java/advanced-excel-charts/chart-interactivity/
weight: 19
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Cómo agregar información sobre herramientas (tooltips) en gráficos interactivos (Aspose.Cells Java)

## Introducción

Los gráficos interactivos permiten a los usuarios explorar los datos al pasar el cursor, hacer clic o profundizar en los detalles. En este tutorial aprenderás **cómo agregar información sobre herramientas** a un gráfico, así como **cómo agregar etiquetas de datos**, e implementar la navegación de **profundización** (drill‑down), todo con Aspose.Cells para Java. Al final, podrás crear un gráfico interactivo y completo que haga tus presentaciones de datos más atractivas y reveladoras.

## Respuestas rápidas
- **¿Qué biblioteca se necesita?** Aspose.Cells para Java (última versión).  
- **¿Qué característica principal cubre esta guía?** Agregar información sobre herramientas a los gráficos.  
- **¿Puedo también agregar etiquetas de datos?** Sí – consulta la sección “Agregar etiquetas de datos”.  
- **¿Se admite la profundización?** Sí, mediante hipervínculos en los puntos de datos.  
- **¿Qué formato de archivo se genera?** Un libro de Excel (`.xlsx`) con un gráfico interactivo.

## ¿Qué es agregar información sobre herramientas?

Una información sobre herramientas es una pequeña ventana emergente que aparece cuando el usuario pasa el cursor sobre un elemento del gráfico, mostrando información adicional como el valor exacto o un mensaje personalizado. Las herramientas mejoran la legibilidad de los datos sin saturar el diseño visual.

## ¿Por qué crear gráficos interactivos en Java?

- **Mejor toma de decisiones:** Los usuarios pueden ver instantáneamente valores precisos.  
- **Informes profesionales:** Los elementos interactivos hacen que los paneles se vean modernos.  
- **Componentes reutilizables:** Una vez domines la API, podrás aplicarla a cualquier solución de informes basada en Excel.

## Requisitos previos

Antes de comenzar, asegúrate de contar con:

- Un entorno de desarrollo Java (JDK 8 o superior).  
- La biblioteca Aspose.Cells para Java (descárgala desde [aquí](https://releases.aspose.com/cells/java/)).  
- Un archivo Excel de ejemplo llamado **data.xlsx** que contenga los datos que deseas visualizar.

## Paso 1: Configurar tu proyecto Java

1. Crea un nuevo proyecto Java en tu IDE preferido (IntelliJ IDEA, Eclipse, etc.).  
2. Añade el JAR de Aspose.Cells al classpath de tu proyecto.

## Paso 2: Cargar datos

Para crear un gráfico interactivo primero necesitas una hoja de cálculo con datos. El código a continuación carga la primera hoja de **data.xlsx**.

```java
// Load the Excel file
Workbook workbook = new Workbook("data.xlsx");
Worksheet worksheet = workbook.getWorksheets().get(0);
```

## Paso 3: Crear un gráfico

Ahora añadiremos un gráfico de columnas a la hoja. El gráfico ocupará las celdas F6 a K16.

```java
// Create a column chart
int chartIndex = worksheet.getCharts().add(ChartType.COLUMN, 5, 0, 15, 5);
Chart chart = worksheet.getCharts().get(chartIndex);
```

## Paso 4: Agregar interactividad

### 4.1. Cómo agregar información sobre herramientas

El siguiente fragmento habilita las herramientas para la primera serie del gráfico. Cada punto de datos mostrará su valor al pasar el cursor.

```java
// Enable tooltips for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowValue(true);
```

### 4.2. Agregar etiquetas de datos al gráfico

Si también deseas etiquetas visibles junto a cada columna, usa el enfoque **add data labels chart** que se muestra a continuación. Esto satisface la palabra clave secundaria *add data labels chart*.

```java
// Enable data labels for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowLabelAsDataCallout(true);
```

### 4.3. Cómo profundizar (Implementar drill‑down)

La profundización permite a los usuarios hacer clic en un punto de datos y saltar a una vista detallada (por ejemplo, una página web). Aquí adjuntamos un hipervínculo al primer punto de la serie.

```java
// Add a hyperlink to a data point
String url = "https://example.com/data-details";
chart.getNSeries().get(0).getPoints().get(0).getHyperlinks().add(url);
```

> **Consejo profesional:** Puedes generar la URL de forma dinámica basándote en el valor del punto para crear una experiencia de drill‑down realmente impulsada por los datos.

## Paso 5: Guardar el libro

Después de configurar el gráfico, guarda el libro. El archivo resultante contiene un gráfico interactivo listo para abrirse en Excel.

```java
// Save the workbook
workbook.save("interactive_chart_output.xlsx");
```

## Problemas comunes y soluciones

| Problema | Causa | Solución |
|----------|-------|----------|
| Las herramientas no aparecen | Las etiquetas de datos no están habilitadas | Asegúrate de que `setHasDataLabels(true)` se llame antes de establecer `ShowValue`. |
| El hipervínculo no es clicable | Índice de punto incorrecto | Verifica que estés referenciando el punto correcto (`get(0)` es el primer punto). |
| El gráfico parece descolocado | Rango de celdas incorrecto | Ajusta los índices de fila/columna en `add(ChartType.COLUMN, row1, col1, row2, col2)`. |

## Preguntas frecuentes

**P: ¿Cómo puedo cambiar el tipo de gráfico?**  
R: Reemplaza `ChartType.COLUMN` por otro valor del enum, como `ChartType.LINE` o `ChartType.PIE`, al llamar a `worksheet.getCharts().add(...)`.

**P: ¿Puedo personalizar la apariencia de las herramientas?**  
R: Sí. Utiliza las propiedades de formato del objeto `DataLabel` (tamaño de fuente, color de fondo, etc.) para estilizar el texto de la herramienta.

**P: ¿Cómo manejo interacciones de usuario en una aplicación web?**  
R: Exporta el libro a un formato compatible con la web (por ejemplo, HTML) y usa JavaScript para capturar eventos de clic en los elementos del gráfico.

**P: ¿Dónde puedo encontrar más ejemplos y documentación?**  
R: Explora la referencia oficial de la API en [Aspose.Cells Java API Reference](https://reference.aspose.com/cells/java/).

**P: ¿Es posible agregar varios enlaces de drill‑down en el mismo gráfico?**  
R: Absolutamente. Recorre los puntos de la serie y asigna una URL única a la colección `Hyperlinks` de cada punto.

## Conclusión

En esta guía aprendiste **cómo agregar información sobre herramientas**, **agregar etiquetas de datos** y **implementar drill‑down** para crear una **solución de gráfico interactivo java** usando Aspose.Cells. Estas funcionalidades convierten los gráficos estáticos de Excel en visualizaciones dinámicas y fáciles de usar que ayudan a los interesados a explorar los datos con facilidad.

---

**Última actualización:** 2025-11-28  
**Probado con:** Aspose.Cells para Java 24.12  
**Autor:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}