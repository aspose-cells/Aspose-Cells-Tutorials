---
date: '2026-04-08'
description: Aprende cómo crear un gráfico de líneas con marcadores usando Aspose.Cells
  para Java, agregar el gráfico a la hoja de cálculo y personalizar los gráficos de
  Excel para informes automatizados.
keywords:
- line chart with markers
- add chart to worksheet
- automate excel chart creation
- populate data for chart
- export styled chart excel
title: Crear un gráfico de líneas con marcadores usando Aspose.Cells para Java
url: /es/java/charts-graphs/aspose-cells-java-excel-charts-creation/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Creación y Estilizado de Gráficos de Excel con Aspose.Cells Java

## Introducción

En el mundo actual impulsado por los datos, un **gráfico de líneas con marcadores** es una de las formas más efectivas de visualizar tendencias y valores atípicos. Ya sea que estés creando informes automatizados o un panel que se actualiza diariamente, poder agregar programáticamente un gráfico de líneas con marcadores a una hoja de cálculo ahorra innumerables pasos manuales. Este tutorial te guía a través del uso de Aspose.Cells para Java para crear, estilizar y exportar dichos gráficos, de modo que puedas concentrarte en los insights en lugar de en la tediosa manipulación de Excel.

**Lo que aprenderás**
- Inicializar un libro de trabajo y poblarlo con datos usando Aspose.Cells.  
- **Cómo agregar un gráfico de líneas con marcadores a una hoja de cálculo** y configurar su apariencia.  
- Personalizar colores de series, marcadores y otras opciones de estilo.  
- Guardar el libro de trabajo como un archivo Excel que incluya tu gráfico estilizado.

## Respuestas Rápidas
- **¿Cuál es la clase principal para comenzar?** `Workbook` inicializa un nuevo archivo Excel.  
- **¿Qué tipo de gráfico crea un gráfico de líneas con marcadores?** `ChartType.LINE_WITH_DATA_MARKERS`.  
- **¿Cómo establezco colores personalizados para los puntos de la serie?** Usa `chart.getNSeries().setColorVaried(true)` y define los colores del área del marcador.  
- **¿Necesito una licencia para la funcionalidad completa?** Sí, una licencia paga o temporal de Aspose.Cells elimina las limitaciones de evaluación.  
- **¿Puedo exportar el resultado como XLSX?** Absolutamente—`workbook.save("StyledChart.xlsx")` crea un archivo XLSX.

## Requisitos Previos

Antes de crear y estilizar gráficos usando Aspose.Cells para Java, asegúrate de tener la siguiente configuración:

### Bibliotecas Requeridas
Incluye Aspose.Cells como dependencia en tu proyecto. Aquí tienes instrucciones para usuarios de Maven y Gradle:

**Maven:**
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

**Gradle:**
```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

### Requisitos de Configuración del Entorno
- Java Development Kit (JDK) instalado en tu sistema.  
- Un Entorno de Desarrollo Integrado (IDE) como IntelliJ IDEA o Eclipse para codificar y probar.

### Conocimientos Previos
Se requiere una comprensión básica de la programación en Java, junto con familiaridad con libros de trabajo de Excel y conceptos de gráficos. 

### Adquisición de Licencia
Aspose.Cells es un producto comercial que requiere una licencia para la funcionalidad completa. Puedes obtener una prueba gratuita para evaluar sus características, solicitar una licencia temporal para pruebas extendidas o comprar el producto para uso a largo plazo.

- **Prueba Gratuita:** [Download Free Trial](https://releases.aspose.com/cells/java/)  
- **Licencia Temporal:** [Request Temporary License](https://purchase.aspose.com/temporary-license/)  
- **Compra:** [Buy Aspose.Cells](https://purchase.aspose.com/buy)

## Configuración de Aspose.Cells para Java

Una vez que hayas instalado las dependencias necesarias, configura tu entorno de desarrollo para usar Aspose.Cells. Comienza importando la biblioteca e inicializando un objeto `Workbook` en tu aplicación Java:

```java
import com.aspose.cells.*;

public class SetupAsposeCells {
    public static void main(String[] args) throws Exception {
        // Initialize a new workbook instance
        Workbook workbook = new Workbook();
        
        System.out.println("Workbook initialized successfully!");
    }
}
```

## Guía de Implementación

En esta sección, desglosaremos la implementación en características distintas: Inicialización del Libro de Trabajo y Población de Datos, Creación y Configuración del Gráfico, Personalización de Series y Guardado del Libro de Trabajo.

### Funcionalidad 1: Inicialización del Libro de Trabajo y Población de Datos

**Visión general:** Esta funcionalidad se centra en crear un nuevo libro de trabajo, acceder a su primera hoja y poblarla con datos para la creación del gráfico.

#### Paso 1: Inicializar el Libro de Trabajo
Comienza instanciando un objeto `Workbook`:

```java
import com.aspose.cells.*;

public class FeatureWorkbookInitialization {
    public static void main(String[] args) throws Exception {
        // Instantiate a workbook
        Workbook workbook = new Workbook();
        
        // Access first worksheet
        Worksheet worksheet = workbook.getWorksheets().get(0);
```

#### Paso 2: Establecer los Títulos de las Columnas y Poblar los Datos
Define los encabezados de columna y rellena filas con datos de ejemplo:

```java
        // Set columns title 
        worksheet.getCells().get(0, 0).setValue("X");
        worksheet.getCells().get(0, 1).setValue("Y");

        // Create random data for series 1
        for (int i = 1; i < 21; i++) {
            worksheet.getCells().get(i, 0).setValue(i);
            worksheet.getCells().get(i, 1).setValue(0.8);
        }

        // Create random data for series 2
        for (int i = 21; i < 41; i++) {
            worksheet.getCells().get(i, 0).setValue(i - 20);
            worksheet.getCells().get(i, 1).setValue(0.9);
        }
    }
}
```

### Funcionalidad 2: Creación y Configuración del Gráfico

**Visión general:** Esta funcionalidad muestra cómo agregar un gráfico a la hoja del libro de trabajo, establecer su estilo y configurar propiedades básicas.

#### Paso 3: Añadir un Gráfico a la Hoja de Cálculo
Agrega un gráfico de líneas con marcadores de datos:

```java
import com.aspose.cells.*;

public class FeatureChartCreation {
    public static void main(String[] args) throws Exception {
        // Instantiate a workbook
        Workbook workbook = new Workbook();
        
        // Access first worksheet
        Worksheet worksheet = workbook.getWorksheets().get(0);
        
        // Add chart to the worksheet
        int idx = worksheet.getCharts().add(ChartType.LINE_WITH_DATA_MARKERS, 1, 3, 20, 20);

        // Access and configure the chart
        Chart chart = worksheet.getCharts().get(idx);
        chart.setStyle(3); // Set a predefined style
        chart.setAutoScaling(true);
        chart.getTitle().setText("Sample Chart");
        chart.getCategoryAxis().getTitle().setText("Units");
    }
}
```

### Funcionalidad 3: Configuración y Personalización de Series

**Visión general:** Mejora el atractivo visual de tus gráficos personalizando la configuración de series, como colores variados y estilos de marcadores.

#### Paso 4: Personalizar la Configuración de Series
Configura los datos de la serie, aplica formato personalizado y ajusta los marcadores:

```java
import com.aspose.cells.*;

public class FeatureSeriesConfiguration {
    public static void main(String[] args) throws Exception {
        // Instantiate a workbook
        Workbook workbook = new Workbook();
        
        // Access first worksheet
        Worksheet worksheet = workbook.getWorksheets().get(0);
        
        // Add series to the chart
        Chart chart = worksheet.getCharts().add(ChartType.LINE_WITH_DATA_MARKERS, 1, 3, 20, 20).get(0);

        int s2_idx = chart.getNSeries().add("A2: A21", true);
        int s3_idx = chart.getNSeries().add("A22: A41", true);

        // Enable varied colors for series points
        chart.getNSeries().setColorVaried(true);

        // Customize first series marker styles and colors
        chart.getNSeries().get(s2_idx).getArea().setFormatting(FormattingType.CUSTOM);
        chart.getNSeries().get(s2_idx).getMarker().getArea().setForegroundColor(Color.getYellow());
        chart.getNSeries().get(s2_idx).getMarker().getBorder().setVisible(false);

        // Set X and Y values for the first series
        chart.getNSeries().get(s2_idx).setXValues("A2: A21");
        chart.getNSeries().get(s2_idx).setValues("B2: B21");

        // Customize second series marker styles and colors
        chart.getNSeries().get(s3_idx).getArea().setFormatting(FormattingType.CUSTOM);
        chart.getNSeries().get(s3_idx).getMarker().getArea().setForegroundColor(Color.getGreen());
        chart.getNSeries().get(s3_idx).getMarker().getBorder().setVisible(false);

        // Set X and Y values for the second series
        chart.getNSeries().get(s3_idx).setXValues("A22: A41");
        chart.getNSeries().get(s3_idx).setValues("B22: B41");
    }
}
```

### Funcionalidad 4: Guardado del Libro de Trabajo

**Visión general:** Finalmente, guarda el libro de trabajo para preservar tus cambios y asegurar que el gráfico se incluya en el archivo Excel.

#### Paso 5: Guardar el Libro de Trabajo
Guarda tu libro de trabajo con los gráficos recién creados:

```java
import com.aspose.cells.*;

public class FeatureWorkbookSaving {
    public static void main(String[] args) throws Exception {
        // Instantiate a workbook
        Workbook workbook = new Workbook();
        
        // Access first worksheet and add data, chart configuration as per previous steps...
        Worksheet worksheet = workbook.getWorksheets().get(0);
        // (Implementation of adding data and configuring the chart would be here)

        // Save the workbook to an Excel file
        workbook.save("StyledChart.xlsx");
    }
}
```

### Problemas Comunes y Solución de Problemas

- **El gráfico aparece vacío:** Verifica que los rangos de celdas usados en `setXValues` y `setValues` referencien correctamente celdas pobladas.  
- **Los colores no se aplican:** Asegúrate de que `chart.getNSeries().setColorVaried(true)` se llame antes de personalizar series individuales.  
- **Errores de licencia:** Una licencia de prueba puede limitar el número de gráficos; instala una licencia completa para eliminar restricciones.

## Preguntas Frecuentes

**Q: ¿Puedo crear otros tipos de gráficos (p. ej., barra, pastel) con Aspose.Cells?**  
A: Sí, Aspose.Cells admite una amplia gama de tipos de gráficos; simplemente reemplaza `ChartType.LINE_WITH_DATA_MARKERS` por el valor de enumeración deseado.

**Q: ¿Necesito cerrar el libro de trabajo o liberar recursos?**  
A: La clase `Workbook` gestiona los recursos automáticamente, pero puedes llamar a `workbook.dispose()` en aplicaciones de larga duración para liberar memoria.

**Q: ¿Es posible agregar varios gráficos a la misma hoja de cálculo?**  
A: Absolutamente—llama a `worksheet.getCharts().add(...)` por cada gráfico que desees insertar.

**Q: ¿Cómo exporto el archivo a un formato Excel más antiguo (XLS)?**  
A: Usa `workbook.save("StyledChart.xls", SaveFormat.EXCEL_97_TO_2003);`.

**Q: ¿El gráfico mantendrá su estilo al abrirse en Microsoft Excel?**  
A: Sí, Aspose.Cells escribe objetos de gráfico nativos de Excel, por lo que todos los estilos, colores y marcadores aparecen exactamente como se definieron.

---

**Última actualización:** 2026-04-08  
**Probado con:** Aspose.Cells 25.3 for Java  
**Autor:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}