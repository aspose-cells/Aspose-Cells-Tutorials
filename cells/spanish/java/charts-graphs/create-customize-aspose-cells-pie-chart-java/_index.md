---
"date": "2025-04-08"
"description": "Aprenda a crear y personalizar gráficos circulares con Aspose.Cells para Java. Una guía paso a paso con ejemplos de código para desarrolladores."
"title": "Dominando Aspose.Cells&#58; Crea y personaliza gráficos circulares en Java"
"url": "/es/java/charts-graphs/create-customize-aspose-cells-pie-chart-java/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}


# Dominando Aspose.Cells: Crea y personaliza gráficos circulares en Java

## Introducción
Crear gráficos visualmente atractivos es un requisito común al visualizar datos en Excel. Ya sea para presentar información demográfica o analizar tendencias del mercado, los gráficos circulares ofrecen una forma clara de representar datos proporcionales. Sin embargo, configurarlos mediante programación puede ser complejo. Este tutorial le guía en la creación y personalización de un gráfico circular Aspose.Cells con Java, simplificando el proceso para los desarrolladores.

**Lo que aprenderás:**
- Configure su entorno con Aspose.Cells para Java.
- Cree un nuevo libro de trabajo y acceda a las celdas de la hoja de trabajo.
- Complete datos en celdas específicas para preparar la creación del gráfico.
- Genere un gráfico circular a partir de estos datos.
- Personalice la apariencia de su gráfico circular, incluidos colores, títulos y leyendas.

Antes de comenzar, asegúrate de tener conocimientos básicos de programación en Java y de gestión de dependencias en Maven o Gradle. ¡Configuremos nuestro entorno!

## Prerrequisitos
Para seguir este tutorial, necesitarás:
- **Kit de desarrollo de Java (JDK)**:Versión 8 o superior.
- **Entorno de desarrollo integrado (IDE)**:Como IntelliJ IDEA o Eclipse.
- **Gestión de dependencias**:Utilice Maven o Gradle para administrar sus dependencias.

### Bibliotecas y dependencias requeridas
Asegúrese de incluir Aspose.Cells para Java en su proyecto utilizando Maven o Gradle.

**Experto**
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

**Gradle**
```gradle
implementation 'com.aspose:aspose-cells:25.3'
```

### Pasos para la adquisición de la licencia
Aspose.Cells para Java es una biblioteca comercial, pero puedes empezar con una prueba gratuita o solicitar una licencia temporal. Visita [página de compra](https://purchase.aspose.com/buy) para explorar las opciones de licencia.

## Configuración de Aspose.Cells para Java
En primer lugar, asegúrese de que el entorno de su proyecto incluya las bibliotecas necesarias agregándolas mediante Maven o Gradle, como se muestra arriba. Una vez incluidas, puede inicializar Aspose.Cells:

```java
import com.aspose.cells.Workbook;

// Inicializar una nueva instancia de libro de trabajo
Workbook workbook = new Workbook();
```

## Guía de implementación

### Crear y configurar un libro de trabajo
Crear un libro de trabajo es el paso inicial en el que configurarás tus datos.

#### Importar bibliotecas
Asegúrese de que estas importaciones estén incluidas en la parte superior de su archivo:

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;
import com.aspose.cells.Cells;
import com.aspose.cells.ChartType;
import com.aspose.cells.Chart;
import com.aspose.cells.Series;
import com.aspose.cells.Color;
import com.aspose.cells.LegendPositionType;
import com.aspose.cells.SaveFormat;
```

#### Paso 1: Crear una instancia de libro de trabajo
```java
// Crea una instancia de libro de trabajo vacía con la que trabajar.
Workbook workbook = new Workbook();
```
Este paso inicializa su archivo Excel programáticamente, lo que le permite manipularlo utilizando las funcionalidades de Aspose.Cells.

### Acceder o modificar celdas de la hoja de cálculo
A continuación, complete con datos las celdas de la hoja de cálculo que se utilizarán para el gráfico circular.

#### Paso 2: Acceder a una hoja de cálculo y sus celdas
```java
// Acceda a la primera hoja de trabajo del libro.
Worksheet worksheet = workbook.getWorksheets().get(0);
Cells cells = worksheet.getCells();

// Coloque valores de muestra utilizados para un gráfico circular en celdas específicas.
cells.get("C3").putValue("India");
cells.get("C4").putValue("China");
cells.get("C5").parseNumber("United States", true, null);
cells.get("C6").setValue("Russia");
cells.get("C7").setValue("United Kingdom");
cells.get("C8").setValue("Others");

// Coloque valores porcentuales para un gráfico circular en celdas específicas.
cells.get("D2").putValue("% of world population");
cells.get("D3").putValue(25);
cells.get("D4").putValue(30);
cells.get("D5").putValue(10);
cells.get("D6").putValue(13);
cells.get("D7").putValue(9);
cells.get("D8").putValue(13);
```
Aquí, rellena la hoja de trabajo con datos que representarán diferentes segmentos de un gráfico circular.

### Crear un gráfico circular

#### Paso 3: Agregue un gráfico circular a la hoja de trabajo
```java
// Cree un gráfico circular en la hoja de trabajo.
int pieIdx = worksheet.getCharts().add(ChartType.PIE, 1, 6, 15, 14);
Chart pie = worksheet.getCharts().get(pieIdx);
```
Este paso agrega un nuevo gráfico circular a su hoja de cálculo en posiciones y dimensiones específicas.

### Configurar series y datos de gráficos circulares

#### Paso 4: Establezca la serie para el gráfico
```java
// Configure el rango de datos de la serie para el gráfico.
pie.getNSeries().add("D3:D8", true);
pie.getNSeries().setCategoryData("=Sheet1!$C$3:$C$8");

// Vincula el título del gráfico circular a una celda que contenga el texto del título.
pie.getTitle().setLinkedSource("D2");
```
Este código vincula su rango de datos y configura la serie para el gráfico circular.

### Configurar la apariencia de la leyenda y el título del gráfico

#### Paso 5: Personalizar la leyenda y el título del gráfico
```java
// Establecer la posición de la leyenda en la parte inferior del gráfico.
pie.getLegend().setPosition(LegendPositionType.BOTTOM);

// Establecer las propiedades de fuente para el título del gráfico.
pie.getTitle().getFont().setName("Calibri");
pie.getTitle().getFont().setSize(18);
```
Personalizar la apariencia mejora la legibilidad y el atractivo visual.

### Personalizar los colores de la serie de gráficos

#### Paso 6: Cambiar los colores de los segmentos del gráfico circular
```java
import com.aspose.cells.Color;

// Acceda y personalice los colores de segmentos individuales del gráfico circular.
Series srs = pie.getNSeries().get(0);
srs.getPoints().get(0).getArea().setForegroundColor(Color.fromArgb(0, 246, 22, 219));
srs.getPoints().get(1).getArea().setForegroundColor(Color.fromArgb(0, 51, 34, 84));
srs.getPoints().get(2).getArea().setForegroundColor(Color.fromArgb(0, 46, 74, 44));
srs.getPoints().get(3).getArea().setForegroundColor(Color.fromArgb(0, 19, 99, 44));
srs.getPoints().get(4).getArea().setForegroundColor(Color.fromArgb(0, 208, 223, 7));
srs.getPoints().get(5).getArea().setForegroundColor(Color.fromArgb(0, 222, 69, 8));
```
Estas configuraciones personalizan su gráfico para adaptarse a esquemas de colores específicos.

### Ajustar automáticamente columnas y guardar libro de trabajo

#### Paso 7: Ajuste el ancho de las columnas y guarde el archivo
```java
// Ajustar automáticamente todas las columnas.
worksheet.autoFitColumns();

// Define la ruta de marcador de posición del directorio de salida para guardar el libro de trabajo.
String outDir = "YOUR_OUTPUT_DIRECTORY";

// Guarde el libro modificado en un archivo Excel en el directorio especificado.
workbook.save(outDir + "/CSOrSColorsPieChart_out.xlsx", SaveFormat.XLSX);
```
Por último, ajuste automáticamente las columnas y guarde su libro de trabajo.

## Aplicaciones prácticas
1. **Análisis demográfico**:Utilice gráficos circulares para mostrar distribuciones de población en diferentes países o regiones.
2. **Informes de participación de mercado**:Ilustrar la cuota de mercado de diferentes empresas en un sector.
3. **Asignación de presupuesto**:Visualice cómo se asignan los presupuestos en los distintos departamentos dentro de una organización.

Estas aplicaciones demuestran la versatilidad y utilidad de Aspose.Cells en escenarios del mundo real.

## Consideraciones de rendimiento
Para optimizar el rendimiento al utilizar Aspose.Cells:
- Minimice el uso de memoria eliminando objetos que ya no necesita.
- Utilice estructuras de datos eficientes para procesar grandes conjuntos de datos.
- Perfile su aplicación para identificar cuellos de botella.

Adherirse a las mejores prácticas garantiza aplicaciones fluidas y con capacidad de respuesta.

## Conclusión
Este tutorial te guió por los pasos para crear y personalizar un gráfico circular con Aspose.Cells en Java. Con este conocimiento, podrás aplicar estas técnicas a diversas tareas de visualización de datos en tus proyectos. Para una exploración más profunda, considera explorar otros tipos de gráficos y las opciones de personalización avanzadas disponibles con Aspose.Cells.


{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}