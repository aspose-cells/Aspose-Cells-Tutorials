---
date: 2025-12-10
description: Aprende a crear un gráfico de cascada en Java usando Aspose.Cells. Guía
  paso a paso para agregar el gráfico a la hoja de cálculo, personalizarlo y guardar
  el libro como XLSX.
linktitle: Waterfall Charts
second_title: Aspose.Cells Java Excel Processing API
title: Cómo crear un gráfico de cascada con Aspose.Cells para Java
url: /es/java/advanced-excel-charts/waterfall-charts/
weight: 18
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Gráficos de Cascada

## Introducción a los Gráficos de Cascada usando Aspose.Cells para Java

En este tutorial aprenderás a **crear un gráfico de cascada** con Aspose.Cells para Java. Los gráficos de cascada son una herramienta esencial en la visualización de datos porque permiten ver el efecto acumulativo de una serie de valores positivos y negativos. Ya sea que estés preparando un estado financiero, un informe de rendimiento de ventas o cualquier otro análisis basado en datos, un gráfico de cascada puede convertir números crudos en ideas claras y accionables.

## Respuestas rápidas
- **¿Qué es un gráfico de cascada?** Una visualización que muestra cómo un valor inicial se incrementa y disminuye mediante una serie de valores intermedios, terminando con un total final.  
- **¿Qué biblioteca se utiliza?** Aspose.Cells para Java.  
- **¿Necesito una licencia?** Una prueba gratuita funciona para desarrollo; se requiere una licencia comercial para producción.  
- **¿Puedo guardar el archivo como XLSX?** Sí – usa `workbook.save("FileName.xlsx")`.  
- **¿Es adecuado para la visualización de datos en Java?** Absolutamente; Aspose.Cells ofrece funciones de gráficos avanzados sin necesidad de Office instalado.

## ¿Qué es un gráfico de cascada?
Un gráfico de cascada muestra contribuciones positivas y negativas secuenciales a un valor inicial, ayudándote a comprender cómo cada componente impacta el resultado global.

## ¿Por qué usar Aspose.Cells para Java para agregar un gráfico de cascada?
- **No se requiere Microsoft Excel** – genera gráficos en cualquier servidor o pipeline CI.  
- **Control total sobre el formato** – colores, etiquetas de datos y ejes pueden personalizarse programáticamente.  
- **Soporta múltiples formatos de salida** – XLSX, PDF, HTML y más.  
- **Alto rendimiento** – ideal para libros de trabajo grandes y generación automática de informes.

## Requisitos previos

Antes de sumergirnos en el código, asegúrate de contar con los siguientes requisitos:

- Aspose.Cells para Java: Necesitarás tener Aspose.Cells para Java instalado. Puedes descargarlo desde [aquí](https://releases.aspose.com/cells/java/).

- Entorno de desarrollo Java: Asegúrate de tener Java instalado en tu sistema.

Ahora, comencemos a crear el gráfico de cascada paso a paso.

## Cómo crear un gráfico de cascada en Java

### Paso 1: Importar Aspose.Cells

```java
import com.aspose.cells.*;
```

Primero, debes importar la biblioteca Aspose.Cells a tu proyecto Java. Esta biblioteca proporciona una funcionalidad extensa para trabajar con archivos Excel, incluida la creación de gráficos.

### Paso 2: Inicializar Workbook y Worksheet

```java
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.getWorksheets().get(0);
```

Crea un nuevo workbook y agrega una worksheet. Usaremos esta hoja para ingresar nuestros datos y **agregar el gráfico a la hoja**.

### Paso 3: Ingresar datos

Ahora, vamos a poblar la worksheet con los datos que queremos representar en el gráfico de cascada.

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

En este ejemplo, tenemos categorías en la columna A y valores correspondientes en la columna B. Puedes reemplazar estos datos con tu propio conjunto de datos.

### Paso 4: Crear el gráfico de cascada

```java
int chartIndex = worksheet.getCharts().add(ChartType.WATERFALL, 5, 0, 15, 5);
Chart waterfallChart = worksheet.getCharts().get(chartIndex);
waterfallChart.getNSeries().add("B2:B6", true);
waterfallChart.getNSeries().setCategoryData("A2:A6");
```

Hemos añadido un gráfico de cascada a nuestra worksheet, especificado la serie de datos y los datos de categoría. Este es el paso central que **agrega el gráfico de cascada** a tu hoja. Puedes personalizar aún más la apariencia del gráfico (colores, etiquetas de datos, etc.) usando las propiedades del objeto `Chart`.

### Paso 5: Guardar el Workbook

```java
workbook.save("WaterfallChart.xlsx");
```

Guarda el workbook en un archivo. El ejemplo utiliza el formato XLSX, pero Aspose.Cells también permite exportar a PDF, CSV y muchos otros formatos. Esto satisface el requisito de **guardar el workbook en xlsx**.

## Problemas comunes y soluciones

- **El gráfico aparece en blanco** – Verifica que las referencias del rango de datos (`B2:B6` y `A2:A6`) coincidan con las celdas reales que contienen tus valores y categorías.  
- **Los valores negativos no se muestran correctamente** – Asegúrate de que el tipo de serie esté configurado a `ChartType.WATERFALL`; otros tipos de gráfico tratan los negativos de manera diferente.  
- **El archivo no se abre en Excel** – Comprueba que estés usando una versión reciente de Aspose.Cells (la última versión) y que la extensión del archivo coincida con el formato (`.xlsx` para Excel).

## Preguntas frecuentes

### ¿Cómo puedo personalizar la apariencia de mi gráfico de cascada?

Puedes personalizar la apariencia de tu gráfico de cascada modificando propiedades como colores, etiquetas de datos y etiquetas de eje. Consulta la documentación de Aspose.Cells para obtener una guía detallada.

### ¿Puedo crear varios gráficos de cascada en la misma worksheet?

Sí, puedes crear varios gráficos de cascada en la misma worksheet siguiendo los mismos pasos con diferentes rangos de datos.

### ¿Aspose.Cells es compatible con diferentes entornos de desarrollo Java?

Sí, Aspose.Cells para Java es compatible con varios entornos de desarrollo Java, incluidos Eclipse, IntelliJ IDEA y NetBeans.

### ¿Puedo añadir series de datos adicionales a mi gráfico de cascada?

Por supuesto, puedes añadir más series de datos a tu gráfico de cascada para representar escenarios de datos complejos de manera eficaz.

### ¿Dónde puedo encontrar más recursos y ejemplos para Aspose.Cells para Java?

Puedes explorar la documentación de Aspose.Cells para Java en [reference.aspose.com/cells/java/](https://reference.aspose.com/cells/java/) para obtener información profunda y ejemplos de código.

---

**Última actualización:** 2025-12-10  
**Probado con:** Aspose.Cells para Java 24.12 (última)  
**Autor:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}