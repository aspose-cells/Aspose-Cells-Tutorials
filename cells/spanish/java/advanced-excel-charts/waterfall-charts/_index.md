---
date: 2026-02-16
description: Aprende cómo establecer el rango de datos del gráfico y crear un gráfico
  de cascada en Java usando Aspose.Cells. Guía paso a paso para agregar un gráfico
  de series de datos, personalizarlo y exportarlo a XLSX.
linktitle: Waterfall Charts
second_title: Aspose.Cells Java Excel Processing API
title: Establecer rango de datos del gráfico – Gráfico de cascada de Aspose.Cells
  para Java
url: /es/java/advanced-excel-charts/waterfall-charts/
weight: 18
---

 final answer.{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Gráficos de Cascada

## Introducción a los Gráficos de Cascada usando Aspose.Cells para Java

En este tutorial aprenderá cómo **establecer el rango de datos del gráfico** y crear un **gráfico de cascada** con Aspose.Cells para Java. Los gráficos de cascada son una herramienta esencial en la visualización de datos porque le permiten ver el efecto acumulativo de una serie de valores positivos y negativos. Ya sea que esté preparando un estado financiero, un informe de desempeño de ventas o cualquier otro análisis basado en datos, un gráfico de cascada puede convertir números crudos en ideas claras y accionables.

## Respuestas Rápidas
- **¿Qué es un gráfico de cascada?** Una visualización que muestra cómo un valor inicial se incrementa y disminuye mediante una serie de valores intermedios, terminando con un total final.  
- **¿Qué biblioteca se utiliza?** Aspose.Cells para Java.  
- **¿Necesito una licencia?** Una prueba gratuita funciona para desarrollo; se requiere una licencia comercial para producción.  
- **¿Puedo guardar el archivo como XLSX?** Sí – use `workbook.save("FileName.xlsx")`.  
- **¿Es adecuado para la visualización de datos en Java?** Absolutamente; Aspose.Cells ofrece funciones de gráficos avanzadas sin necesidad de Office instalado.

## ¿Qué es un Gráfico de Cascada?
Un gráfico de cascada muestra contribuciones positivas y negativas secuenciales a un valor inicial, ayudándole a comprender cómo cada componente impacta el resultado total.

## ¿Por Qué Usar Aspose.Cells para Java para Añadir un Gráfico de Cascada?
- **No se requiere Microsoft Excel** – genere gráficos en cualquier servidor o canal de CI.  
- **Control total sobre el formato** – colores, etiquetas de datos y ejes pueden personalizarse programáticamente.  
- **Soporta múltiples formatos de salida** – XLSX, PDF, HTML y más.  
- **Alto rendimiento** – ideal para libros de trabajo grandes y reportes automatizados.

## Requisitos Previos

Antes de sumergirnos en el código, asegúrese de que tiene los siguientes requisitos:

- Aspose.Cells para Java: Necesitará tener Aspose.Cells para Java instalado. Puede descargarlo desde [aquí](https://releases.aspose.com/cells/java/).

- Entorno de Desarrollo Java: Asegúrese de que Java esté instalado en su sistema.

Ahora, comencemos a crear el gráfico de cascada paso a paso.

## Cómo Establecer el Rango de Datos del Gráfico para un Gráfico de Cascada en Java

### Paso 1: Importar Aspose.Cells

```java
import com.aspose.cells.*;
```

Primero, necesita importar la biblioteca Aspose.Cells a su proyecto Java. Esta biblioteca ofrece una funcionalidad extensa para trabajar con archivos Excel, incluida la creación de gráficos.

### Paso 2: Inicializar Libro de Trabajo y Hoja de Cálculo

```java
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.getWorksheets().get(0);
```

Cree un nuevo libro de trabajo y añada una hoja de cálculo. Usaremos esta hoja para ingresar nuestros datos y **añadir el gráfico a la hoja**.

### Paso 3: Ingresar Datos

Ahora, vamos a poblar la hoja con los datos que queremos representar en el gráfico de cascada.

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

En este ejemplo, tenemos categorías en la columna A y valores correspondientes en la columna B. Puede reemplazar estos datos con su propio conjunto de datos.

### Paso 4: Crear el Gráfico de Cascada

```java
int chartIndex = worksheet.getCharts().add(ChartType.WATERFALL, 5, 0, 15, 5);
Chart waterfallChart = worksheet.getCharts().get(chartIndex);
waterfallChart.getNSeries().add("B2:B6", true);
waterfallChart.getNSeries().setCategoryData("A2:A6");
```

Hemos añadido un gráfico de cascada a nuestra hoja, especificado la serie de datos y los datos de categoría. Este es el paso central que **añade el gráfico de cascada** a su hoja. Observe cómo el método `add` usa el rango `"B2:B6"` – aquí es donde **establecemos el rango de datos del gráfico** para la serie. Puede personalizar aún más la apariencia del gráfico (colores, etiquetas de datos, etc.) usando las propiedades del objeto `Chart`.

### Paso 5: Guardar el Libro de Trabajo

```java
workbook.save("WaterfallChart.xlsx");
```

Guarde el libro de trabajo en un archivo. El ejemplo usa el formato XLSX, pero Aspose.Cells también le permite **exportar excel pdf java**‑compatible archivos como PDF, CSV y muchos otros formatos. Esto satisface el requisito de **guardar libro de trabajo xlsx**.

## Problemas Comunes y Soluciones

- **El gráfico aparece en blanco** – Verifique que las referencias del rango de datos (`B2:B6` y `A2:A6`) coincidan con las celdas reales que contienen sus valores y categorías.  
- **Los valores negativos no se muestran correctamente** – Asegúrese de que el tipo de serie esté configurado a `ChartType.WATERFALL`; otros tipos de gráfico tratan los negativos de manera diferente.  
- **El archivo no se abre en Excel** – Asegúrese de estar usando una versión reciente de Aspose.Cells (la última versión) y que la extensión del archivo coincida con el formato (`.xlsx` para Excel).

## Preguntas Frecuentes

### ¿Cómo puedo personalizar la apariencia de mi gráfico de cascada?

Puede personalizar la apariencia de su gráfico de cascada modificando propiedades como colores, etiquetas de datos y etiquetas de eje. Consulte la documentación de Aspose.Cells para obtener una guía detallada.

### ¿Puedo crear varios gráficos de cascada en la misma hoja?

Sí, puede crear varios gráficos de cascada en la misma hoja siguiendo los mismos pasos con diferentes rangos de datos.

### ¿Aspose.Cells es compatible con diferentes entornos de desarrollo Java?

Sí, Aspose.Cells para Java es compatible con varios entornos de desarrollo Java, incluidos Eclipse, IntelliJ IDEA y NetBeans.

### ¿Puedo añadir series de datos adicionales a mi gráfico de cascada?

Por supuesto, puede añadir más series de datos a su gráfico de cascada para representar escenarios de datos complejos de manera eficaz. Este es un ejemplo de cómo puede **añadir series de datos al gráfico** programáticamente.

### ¿Dónde puedo encontrar más recursos y ejemplos para Aspose.Cells para Java?

Puede explorar la documentación de Aspose.Cells para Java en [reference.aspose.com/cells/java/](https://reference.aspose.com/cells/java/) para obtener información detallada y ejemplos de código.

## Preguntas Frecuentes

**P: ¿Cómo establezco el rango de datos del gráfico para un gráfico de cascada financiero?**  
R: Use el método `add` en la serie del gráfico, pasando el rango de celdas que contiene sus valores, por ejemplo, `"B2:B6"`.

**P: ¿Puedo exportar el libro a PDF en lugar de XLSX?**  
R: Sí, llame a `workbook.save("WaterfallChart.pdf", SaveFormat.PDF);` para una salida **exportar excel pdf java**‑compatible.

**P: ¿Qué pasa si necesito crear un gráfico de cascada financiero con más categorías?**  
R: Amplíe el rango de datos tanto en la columna de valores como en la columna de categorías, y luego actualice las llamadas a `add` y `setCategoryData` en consecuencia.

**P: ¿Hay una forma de formatear automáticamente las barras positivas y negativas?**  
R: Puede iterar a través de la colección `Series` y establecer el color `FillFormat` según el signo de cada valor.

**P: ¿Aspose.Cells admite actualizaciones dinámicas de datos para los gráficos?**  
R: Sí, puede modificar los valores de las celdas después de crear el gráfico; el gráfico reflejará los cambios cuando se guarde el libro.

---

**Última actualización:** 2026-02-16  
**Probado con:** Aspose.Cells para Java (última)  
**Autor:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}