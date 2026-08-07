---
date: '2026-04-11'
description: Aprende automatización de Excel con Java y Aspose.Cells. Este tutorial
  muestra cómo crear un libro de Excel con Java, poblar datos de Excel con Java y
  guardar un archivo de Excel con Java con gráficos.
keywords:
- excel automation java
- create excel workbook java
- save excel file java
- populate excel data java
- aspose cells java
title: 'Automatización de Excel con Java: Crear libros de trabajo y gráficos usando
  Aspose'
url: /es/java/charts-graphs/aspose-cells-java-excel-workbook-charts/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Automatización de Excel con Java: Crear Libros de Trabajo y Gráficos usando Aspose

## Introducción

Automatizar tareas de Excel con Java puede ahorrar horas de trabajo manual, especialmente cuando necesitas generar informes, paneles o gráficos basados en datos al instante. **Excel automation java** con Aspose.Cells te brinda una API limpia y de alto rendimiento que maneja todo, desde la creación del libro de trabajo hasta el estilo sofisticado de los gráficos. En este tutorial aprenderás a configurar Aspose.Cells, **crear un libro de Excel java**, poblarlo con datos, añadir un gráfico, aplicar formato 3‑D y, finalmente, **guardar el archivo Excel java**.

### Respuestas rápidas
- **¿Qué biblioteca simplifica la automatización de Excel en Java?** Aspose.Cells for Java.  
- **¿Puedo añadir gráficos 3‑D programáticamente?** Sí – la API soporta formato 3‑D y efectos de iluminación.  
- **¿Necesito una licencia para desarrollo?** Hay una licencia de prueba gratuita; se requiere una licencia comercial para producción.  
- **¿Qué herramientas de compilación Java son compatibles?** Maven y Gradle están totalmente soportados.  
- **¿Qué formatos de archivo puedo exportar?** XLS, XLSX, CSV, PDF y muchos más.

## ¿Qué es Excel automation java?

Excel automation java se refiere al proceso de generar, modificar y guardar libros de Excel programáticamente usando código Java. Elimina la edición manual de hojas de cálculo, garantiza consistencia y permite la integración con otros sistemas como bases de datos o servicios web.

## ¿Por qué usar Aspose.Cells para Java?

- **Conjunto de funciones amplio** – desde valores simples de celdas hasta gráficos complejos, tablas dinámicas y formato condicional.  
- **Sin dependencia de Microsoft Office** – funciona en cualquier entorno del lado del servidor.  
- **Alto rendimiento** – optimizado para grandes conjuntos de datos y escenarios multihilo.  
- **Amplio soporte de formatos** – leer/escribir XLS, XLSX, ODS, CSV, PDF, HTML y más.

## Requisitos previos

- **Java Development Kit (JDK) 8+**  
- **Maven o Gradle** para la gestión de dependencias  
- **Aspose.Cells for Java 25.3 o posterior** (prueba o con licencia)  

## Configuración de Aspose.Cells para Java

Agrega la biblioteca a tu proyecto usando una de las siguientes configuraciones.

### Maven
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

### Gradle
```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

#### Obtención de licencia

Solicita una licencia de prueba gratuita en el sitio web de Aspose, o compra una licencia completa para uso en producción. Coloca el archivo de licencia en tu proyecto y cárgalo en tiempo de ejecución.

## Inicialización básica y configuración

Una vez resuelta la dependencia, puedes comenzar a codificar.

```java
import com.aspose.cells.Workbook;

public class ExcelDemo {
    public static void main(String[] args) throws Exception {
        String dataDir = "YOUR_DATA_DIRECTORY";
        String outDir = "YOUR_OUTPUT_DIRECTORY";

        // Initialize a new Workbook object
        Workbook book = new Workbook();
        System.out.println("Workbook initialized successfully.");
    }
}
```

## Guía paso a paso

### Paso 1: Cómo crear excel workbook java

Crea una nueva instancia de libro de trabajo que contendrá todas tus hojas.

```java
import com.aspose.cells.Workbook;
// Initialize a new Workbook object
Workbook book = new Workbook();
```

### Paso 2: Añadir hojas de cálculo (incluyendo una hoja de gráfico)

```java
import com.aspose.cells.Worksheet;
Worksheet dataSheet = book.getWorksheets().add("DataSheet");
Worksheet chartSheet = book.getWorksheets().add("MyChart");
System.out.println("Worksheets added successfully.");
```

### Paso 3: Cómo poblar datos excel java

Inserta datos de ejemplo que el gráfico referenciará.

```java
import com.aspose.cells.Cells;
Cells cells = dataSheet.getCells();
cells.get("B1").putValue(1);
cells.get("B2").putValue(2);
cells.get("B3").putValue(3);
cells.get("A1").putValue("A");
cells.get("A2").putValue("B");
cells.get("A3").putValue("C");
System.out.println("Data populated successfully.");
```

### Paso 4: Añadir un gráfico de columnas al libro

```java
import com.aspose.cells.Chart;
import com.aspose.cells.ChartCollection;
import com.aspose.cells.ChartType;
ChartCollection charts = chartSheet.getCharts();
charts.add(ChartType.COLUMN, 5, 0, 25, 15);
Chart chart = book.getWorksheets().get(2).getCharts().get(0);
System.out.println("Chart added successfully.");
```

### Paso 5: Aplicar formato de color al área del gráfico

```java
import com.aspose.cells.Color;
chart.getPlotArea().getArea().setBackgroundColor(Color.getWhite());
chart.getChartArea().getArea().setBackgroundColor(Color.getWhite());
chart.getPlotArea().getArea().setForegroundColor(Color.getWhite());
chart.getChartArea().getArea().setForegroundColor(Color.getWhite());
System.out.println("Color formatting applied successfully.");
```

### Paso 6: Configurar leyenda y series de datos

```java
import com.aspose.cells.Series;
chart.setShowLegend(false);
chart.getNSeries().add("DataSheet!B1:B3", true);
chart.getNSeries().setCategoryData("DataSheet!A1:A3");
Series ser = chart.getNSeries().get(0);
System.out.println("Chart series configured successfully.");
```

### Paso 7: Aplicar formato 3D a la serie

```java
import com.aspose.cells.Bevel;
import com.aspose.cells.BevelPresetType;
import com.aspose.cells.Format3D;
import com.aspose.cells.LightRigType;
import com.aspose.cells.PresetMaterialType;
import com.aspose.cells.ShapePropertyCollection;
ShapePropertyCollection spPr = ser.getShapeProperties();
Format3D fmt3d = spPr.getFormat3D();

Bevel bevel = fmt3d.getTopBevel();
bevel.setType(BevelPresetType.CIRCLE);
bevel.setHeight(5);
bevel.setWidth(9);
fmt3d.setSurfaceMaterialType(PresetMaterialType.WARM_MATTE);
fmt3d.setSurfaceLightingType(LightRigType.THREE_POINT);
fmt3d.setLightingAngle(20);
System.out.println("3D formatting applied successfully.");
```

### Paso 8: Establecer colores de serie para mejor distinción visual

```java
ser.getArea().setBackgroundColor(Color.getMaroon());
ser.getArea().setForegroundColor(Color.getMaroon());
ser.getBorder().setColor(Color.getMaroon());
System.out.println("Series color formatting applied successfully.");
```

### Paso 9: Cómo guardar excel file java

```java
book.save(outDir + "A3DFormat_out.xls");
System.out.println("Workbook saved successfully.");
```

## Aplicaciones prácticas

- **Informes financieros** – Genera estados trimestrales con gráficos dinámicos.  
- **Paneles de análisis de datos** – Construye paneles interactivos que se actualizan automáticamente.  
- **Gestión de inventario** – Exporta niveles de stock y tendencias a Excel para revisión de interesados.  
- **Planificación de proyectos** – Crea gráficos estilo Gantt directamente desde sistemas de programación basados en Java.

## Consejos de rendimiento para Excel Automation Java

- **Reutiliza objetos Workbook** al procesar múltiples hojas para reducir el consumo de memoria.  
- **Actualizaciones masivas de celdas** usando `Cells.importArray` para grandes conjuntos de datos en lugar de llamadas individuales a `putValue`.  
- **Libera recursos** llamando a `book.dispose()` después de guardar archivos grandes.

## Preguntas frecuentes

**P: ¿Puedo generar XLSX en lugar de XLS?**  
R: Sí – simplemente cambia la extensión del archivo en `book.save("output.xlsx")`; Aspose selecciona automáticamente el formato correcto.

**P: ¿Se requiere una licencia para desarrollo?**  
R: Una licencia de prueba gratuita funciona para desarrollo y pruebas. Las implementaciones en producción requieren una licencia comprada.

**P: ¿Cómo añado más tipos de gráficos?**  
R: Usa el enumerado `ChartType` (p. ej., `ChartType.PIE`, `ChartType.LINE`) al llamar a `charts.add(...)`.

**P: ¿Qué pasa si necesito proteger el libro?**  
R: Llama a `book.getSettings().setPassword("yourPassword")` antes de guardar.

**P: ¿Aspose.Cells soporta archivos con macros?**  
R: Sí – puedes crear o conservar macros VBA en libros XLSM.

---

**Última actualización:** 2026-04-11  
**Probado con:** Aspose.Cells 25.3 (Java)  
**Autor:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}