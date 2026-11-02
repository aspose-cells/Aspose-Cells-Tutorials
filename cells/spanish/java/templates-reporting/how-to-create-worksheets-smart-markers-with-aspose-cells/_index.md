---
category: general
date: 2026-08-20
description: Cree marcadores inteligentes de hojas de cálculo en Java usando Aspose.Cells
  y controle el nombrado de las hojas de detalle con SmartMarkerOptions.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create worksheets smart markers
- Aspose.Cells Java
- smart marker options
- duplicate sheet names
- detail sheet naming
language: es
lastmod: 2026-08-20
og_description: Crea marcadores inteligentes de hojas de cálculo en Java con Aspose.Cells.
  Aprende cómo nombrar hojas de detalle dinámicamente usando SmartMarkerOptions.
og_image_alt: create worksheets smart markers example diagram
og_title: Crear marcadores inteligentes de hojas de cálculo – Guía de Java con Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-08-20'
  description: Create worksheets smart markers in Java using Aspose.Cells and control
    detail sheet naming with SmartMarkerOptions.
  headline: How to create worksheets smart markers with Aspose.Cells
  type: TechArticle
- description: Create worksheets smart markers in Java using Aspose.Cells and control
    detail sheet naming with SmartMarkerOptions.
  name: How to create worksheets smart markers with Aspose.Cells
  steps:
  - name: Set up the Maven project and add Aspose.Cells
    text: 'Create a new Maven module (or Gradle project) and add the Aspose.Cells
      dependency:'
  - name: Load the master workbook that contains smart markers
    text: '```java import com.aspose.cells.*;'
  - name: Configure SmartMarkerOptions for custom detail sheet names
    text: '```java // Define naming pattern for detail sheets. SmartMarkerOptions
      smartMarkerOptions = new SmartMarkerOptions(); // {0} is automatically replaced
      by the row index (starting at 1). smartMarkerOptions.setDetailSheetNewName("DetailSheet_{0}");
      ```'
  - name: Build a DataTable that matches the smart marker fields
    text: '```java // Build a simple DataTable with two columns. DataTable data =
      new DataTable(); data.getColumns().add("Id", DataType.INTEGER); data.getColumns().add("Value",
      DataType.STRING); // Add sample rows. data.getRows().add(new Object[] { 1, "A"
      }); data.getRows().add(new Object[] { 2, "B" }); ```'
  - name: Apply the data to the smart markers with the naming options
    text: '```java // Apply the data to the first worksheet (index 0). workbook.getWorksheets().get(0).getSmartMarkers().apply(data,
      smartMarkerOptions); ```'
  - name: Save the workbook and verify the result
    text: '```java // Save the expanded workbook. workbook.save("YOUR_DIRECTORY/MasterDetailDuplicatedNames.xlsx");
      } } ```'
  - name: Multiple master sheets
    text: 'If your template contains more than one master sheet, iterate over each
      sheet’s smart markers:'
  - name: Custom naming beyond the row index
    text: 'You can embed any data column into the sheet name by using placeholders
      like `{ColumnName}`:'
  - name: Preventing overly long sheet names
    text: 'Excel limits sheet names to 31 characters. If your naming pattern risks
      exceeding this limit, truncate or hash the value:'
  type: HowTo
tags:
- Java
- Aspose.Cells
- Smart Markers
- Excel Automation
title: Cómo crear marcadores inteligentes en hojas de cálculo con Aspose.Cells
url: /es/java/templates-reporting/how-to-create-worksheets-smart-markers-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo crear marcadores inteligentes en hojas de cálculo con Aspose.Cells

Si necesita **crear marcadores inteligentes en hojas de cálculo** en un libro de Java, esta guía le muestra los pasos exactos para hacerlo con Aspose.Cells. Verá cómo configurar `SmartMarkerOptions` para que cada hoja de detalle reciba un nombre único y predecible.

Generar informes de Excel que expanden una plantilla maestro‑detalle es un requisito común en finanzas, inventario y sistemas de reportes. El uso de marcadores inteligentes elimina la duplicación manual de hojas y le permite centrarse en los datos en lugar de la infraestructura.

## Lo que aprenderá

* Cómo cargar un libro maestro que contiene marcadores inteligentes.  
* Cómo establecer `SmartMarkerOptions` para controlar el nombrado de las hojas de detalle generadas.  
* Cómo proporcionar un `DataTable` con datos de ejemplo y aplicarlo a los marcadores inteligentes.  
* Cómo guardar el resultado para que cada hoja de detalle tenga un nombre distinto, evitando nombres de hoja duplicados.

**Prerequisitos**  
* Java 17 o posterior (el código también compila con JDK 8+).  
* Aspose.Cells for Java 23.9 o más reciente – la biblioteca proporciona `Workbook`, `SmartMarkerOptions` y clases relacionadas.  
* Un IDE como IntelliJ IDEA, Eclipse o VS Code.

Los conceptos secundarios que encontrará incluyen **Aspose.Cells Java**, **smart marker options**, y el manejo de **duplicate sheet names** cuando la plantilla se expande.

## Crear marcadores inteligentes en hojas de cálculo – guía paso a paso

Las siguientes secciones desglosan el proceso en pasos discretos y reutilizables. Cada paso incluye un fragmento de código, una explicación de por qué es importante y consejos prácticos para evitar errores comunes.

### Paso 1: Configurar el proyecto Maven y agregar Aspose.Cells

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.9</version>
</dependency>
```

**Por qué este paso es importante** – La biblioteca proporciona la clase `Workbook` que lee y escribe archivos Excel, además del motor de smart‑marker que expande su plantilla automáticamente. Sin la dependencia correcta, el compilador no puede resolver las llamadas a la API usadas más adelante.

> **Consejo profesional:** Si trabaja detrás de un proxy corporativo, configure `settings.xml` de Maven para obtener el repositorio de Aspose de forma segura.

### Paso 2: Cargar el libro maestro que contiene marcadores inteligentes

```java
import com.aspose.cells.*;

public class DuplicateDetailSheetNames {
    public static void main(String[] args) throws Exception {
        // Load the template that holds the smart marker tags.
        Workbook workbook = new Workbook("YOUR_DIRECTORY/MasterDetailTemplate.xlsx");
```

**Por qué este paso es importante** – El libro maestro define el diseño, las fórmulas y las etiquetas de marcador de posición (`«SmartMarker»`) que el motor reemplazará. Cargar el archivo una sola vez mantiene bajo el uso de memoria y le permite reutilizar el mismo libro para varios conjuntos de datos.

### Paso 3: Configurar SmartMarkerOptions para nombres personalizados de hojas de detalle

```java
        // Define naming pattern for detail sheets.
        SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions();
        // {0} is automatically replaced by the row index (starting at 1).
        smartMarkerOptions.setDetailSheetNewName("DetailSheet_{0}");
```

**Por qué este paso es importante** – Por defecto Aspose.Cells crea hojas de detalle con nombres genéricos como “DetailSheet”. Cuando la plantilla se expande para muchas filas, esos nombres entran en conflicto, lo que genera **duplicate sheet names** y una excepción en tiempo de ejecución. El patrón `"DetailSheet_{0}"` garantiza un nombre único por fila, resolviendo el problema de duplicación.

### Paso 4: Construir un DataTable que coincida con los campos de los marcadores inteligentes

```java
        // Build a simple DataTable with two columns.
        DataTable data = new DataTable();
        data.getColumns().add("Id", DataType.INTEGER);
        data.getColumns().add("Value", DataType.STRING);
        // Add sample rows.
        data.getRows().add(new Object[] { 1, "A" });
        data.getRows().add(new Object[] { 2, "B" });
```

**Por qué este paso es importante** – El `DataTable` suministra los valores reales que reemplazan los marcadores inteligentes. Los nombres de columna deben coincidir con los nombres de los marcadores en la plantilla; de lo contrario, el motor omite la sustitución silenciosamente.

> **Error común:** Usar un nombre de columna que difiere en mayúsculas/minúsculas (p.ej., “id” vs “Id”) provoca datos faltantes en las hojas generadas.

### Paso 5: Aplicar los datos a los marcadores inteligentes con las opciones de nombrado

```java
        // Apply the data to the first worksheet (index 0).
        workbook.getWorksheets().get(0).getSmartMarkers().apply(data, smartMarkerOptions);
```

**Por qué este paso es importante** – El método `apply` activa el motor de smart‑marker. Lee cada fila, crea una nueva hoja de detalle usando el patrón de nombrado de `SmartMarkerOptions` y rellena la hoja con los datos de la fila. Esta única llamada reemplaza decenas de líneas de clonación manual de hojas y llenado de celdas.

### Paso 6: Guardar el libro y verificar el resultado

```java
        // Save the expanded workbook.
        workbook.save("YOUR_DIRECTORY/MasterDetailDuplicatedNames.xlsx");
    }
}
```

Después de la ejecución, abra `MasterDetailDuplicatedNames.xlsx`. Debería ver:

* La hoja maestra original sin cambios.  
* Dos nuevas hojas de cálculo nombradas `DetailSheet_1` y `DetailSheet_2`.  
* Cada hoja de detalle contiene los valores de la fila correspondiente del `DataTable`.

**Por qué este paso es importante** – Persistir el libro finaliza la expansión de los smart‑markers. El archivo ahora puede enviarse a sistemas posteriores, adjuntarse a correos electrónicos o abrirse en Excel para un análisis adicional.

## Manejo de casos límite y variaciones

### Múltiples hojas maestras

Si su plantilla contiene más de una hoja maestra, itere sobre los marcadores inteligentes de cada hoja:

```java
for (int i = 0; i < workbook.getWorksheets().getCount(); i++) {
    workbook.getWorksheets().get(i).getSmartMarkers().apply(data, smartMarkerOptions);
}
```

### Nomenclatura personalizada más allá del índice de fila

Puede incrustar cualquier columna de datos en el nombre de la hoja usando marcadores como `{ColumnName}`:

```java
smartMarkerOptions.setDetailSheetNewName("Order_{OrderId}");
```

Asegúrese de que la columna `OrderId` exista en el `DataTable` suministrado.

### Evitar nombres de hoja excesivamente largos

Excel limita los nombres de hoja a 31 caracteres. Si su patrón de nombrado corre el riesgo de superar este límite, trunque o aplique un hash al valor:

```java
String pattern = "Detail_{0}_{1}";
smartMarkerOptions.setDetailSheetNewName(pattern);
```

Luego procese el nombre generado con `StringUtils.abbreviate` antes de pasarlo a Aspose.

## Ejemplo completo ejecutable

A continuación se muestra el archivo fuente completo que puede copiar, ajustar las rutas de archivo y ejecutar directamente:

```java
import com.aspose.cells.*;

public class DuplicateDetailSheetNames {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load the master workbook that contains smart markers
        Workbook workbook = new Workbook("YOUR_DIRECTORY/MasterDetailTemplate.xlsx");

        // 2️⃣ Define how detail sheets will be named when they are created
        SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions();
        // {0} is replaced by the row index (starting at 1)
        smartMarkerOptions.setDetailSheetNewName("DetailSheet_{0}");

        // 3️⃣ Prepare sample data to populate the smart markers
        DataTable data = new DataTable();
        data.getColumns().add("Id", DataType.INTEGER);
        data.getColumns().add("Value", DataType.STRING);
        data.getRows().add(new Object[] { 1, "A" });
        data.getRows().add(new Object[] { 2, "B" });

        // 4️⃣ Apply the data to the smart markers using the naming options
        workbook.getWorksheets().get(0).getSmartMarkers().apply(data, smartMarkerOptions);

        // 5️⃣ Save the workbook – each detail sheet now has a unique name
        workbook.save("YOUR_DIRECTORY/MasterDetailDuplicatedNames.xlsx");
    }
}
```

**Salida esperada**

* `MasterDetailDuplicatedNames.xlsx` contiene:

## ¿Qué debería aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que se basan en las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y funcionales con explicaciones paso a paso para ayudarle a dominar funciones adicionales de la API y explorar enfoques de implementación alternativos en sus propios proyectos.

- [Dominar Aspose.Cells Java: Utilizar Smart Markers para datos dinámicos en hojas de cálculo](/cells/english/java/worksheet-management/aspose-cells-java-smart-markers-worksheets/)
- [Crear gráficos dinámicos con Smart Markers en Aspose.Cells para Java | Guía paso a paso](/cells/english/java/charts-graphs/dynamic-charts-smart-markers-aspose-cells-java/)
- [Hojas de cálculo con Smart Markers de Aspose Cells Java](/cells/german/java/worksheet-management/aspose-cells-java-smart-markers-worksheets/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}