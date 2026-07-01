---
category: general
date: 2026-06-30
description: Rellene la plantilla de Excel con datos usando SmartMarkerProcessor y
  aprenda cómo crear un informe de Excel a partir de una plantilla en Java – guía
  paso a paso.
draft: false
keywords:
- populate excel template with data
- create excel report from template
- smartmarkerprocessor java
- excel automation java
- java data source excel
language: es
og_description: Rellene la plantilla de Excel con datos usando SmartMarkerProcessor.
  Esta guía muestra cómo crear un informe de Excel a partir de una plantilla en Java,
  con código incluido.
og_title: Rellenar plantilla de Excel con datos – Crear informe de Excel a partir
  de la plantilla
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Populate Excel template with data using SmartMarkerProcessor and learn
    how to create Excel report from template in Java – step‑by‑step guide.
  headline: Populate Excel Template with Data – Create Excel Report from Template
  type: TechArticle
- description: Populate Excel template with data using SmartMarkerProcessor and learn
    how to create Excel report from template in Java – step‑by‑step guide.
  name: Populate Excel Template with Data – Create Excel Report from Template
  steps:
  - name: Instantiate the SmartMarkerProcessor
    text: The processor is the engine that scans your workbook, finds Smart Markers,
      and replaces them with real values.
  - name: '(Optional): Rename the Detail Sheet'
    text: Smart Markers often generate a hidden “detail” sheet that holds intermediate
      data. Renaming it makes the final workbook easier to navigate.
  - name: Load the Template Workbook
    text: This is where you point the processor at the Excel file that contains the
      markers.
  - name: Prepare a Data Source
    text: SmartMarkerProcessor expects an `IDataSource` implementation that knows
      how to fetch values for each marker. Below is a minimal **in‑memory** data source
      that uses a `Map<String, Object>`.
  - name: Apply the Data to the Workbook
    text: Now the magic happens—Smart Markers are replaced with the values from your
      `IDataSource`.
  - name: Save the Processed Workbook
    text: Finally, write the populated workbook to disk (or stream it directly to
      HTTP response if you’re in a web app).
  - name: 'H3: Handling Collections (Tables)'
    text: If your template contains a repeating block like a sales table, replace
      the marker with an array in your data source.
  - name: 'H3: Formatting Dates and Numbers'
    text: 'Smart Markers respect cell formatting. If you pre‑format a cell as *Currency*
      in the template, the numeric value you push through will automatically display
      with the correct symbol and decimal places. No extra code needed—just make sure
      the data type you return (`Double`, `BigDecimal`, `LocalDate`) '
  - name: 'H3: Performance Considerations'
    text: '- **Reuse the processor** if you generate dozens of reports in a batch;
      just call `processor.clear()` between runs. - **Turn off calculation** (`workbook.getSettings().setRecalcOnLoad(false)`)
      when you only need to write values, not recalculate formulas. - **Stream the
      output** to avoid large tempor'
  type: HowTo
tags:
- excel
- java
- reporting
- smartmarker
title: Rellenar plantilla de Excel con datos – Crear informe de Excel a partir de
  la plantilla
url: /es/java/templates-reporting/populate-excel-template-with-data-create-excel-report-from-t/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Poblar plantilla de Excel con datos – Crear informe de Excel a partir de una plantilla

¿Alguna vez necesitaste **poblar una plantilla de Excel con datos** pero no estabas seguro de qué biblioteca podía encargarse del trabajo pesado? No eres el único. Cuando estás creando paneles mensuales, facturas o cualquier tipo de hoja de cálculo basada en datos, hacerlo a mano rápidamente se vuelve una pesadilla.  

La buena noticia es que el SmartMarkerProcessor de Aspose.Cells lo hace sin esfuerzo: solo alimenta una plantilla y una fuente de datos, y tendrás un informe de Excel pulido en segundos. En este tutorial también te mostraremos **cómo crear un informe de Excel a partir de una plantilla** usando Java puro, para que puedas incorporar la solución directamente en tu proyecto.

## Requisitos previos (Lo que necesitarás)

- Java 17 o superior (el código compila con versiones anteriores, pero 17 te brinda las últimas mejoras del lenguaje).  
- Aspose.Cells para Java (el artefacto Maven `com.aspose:aspose-cells` versión 24.9 o posterior).  
- Un archivo Excel que contenga Smart Markers (por ejemplo, `input.xlsx`).  
- Una fuente de datos simple que implemente `IDataSource` (crearemos una para ti).  

No se requiere un IDE especial; cualquier editor que pueda compilar Java servirá.  

---

## Poblar plantilla de Excel con datos – Paso a paso

A continuación dividimos el proceso en seis pasos lógicos. Cada paso incluye **por qué** es importante, no solo **qué** escribir.

### Paso 1: Instanciar el SmartMarkerProcessor  

El procesador es el motor que escanea tu libro de trabajo, encuentra Smart Markers y los reemplaza con valores reales.

```java
// Step 1: Create a SmartMarkerProcessor instance
SmartMarkerProcessor processor = new SmartMarkerProcessor();
```

*¿Por qué?*  
Crear un procesador nuevo garantiza que comiences con un estado limpio. Si reutilizas una instancia antigua, la configuración residual podría filtrarse en la siguiente ejecución, algo que definitivamente deseas evitar en un trabajo de producción.

### Paso 2 (Opcional): Renombrar la hoja de detalle  

Los Smart Markers a menudo generan una hoja oculta de “detalle” que contiene datos intermedios. Renombrarla hace que el libro de trabajo final sea más fácil de navegar.

```java
// Step 2: (Optional) Set a new name for the detail sheet that will be generated
processor.setDetailSheetNewName("CopyOfDetail");
```

*Consejo profesional:*  
Si tu plantilla ya contiene una hoja llamada “Detail”, asigna a la hoja generada un sufijo único (p. ej., `CopyOfDetail_2024`) para evitar colisiones de nombres.

### Paso 3: Cargar el libro de trabajo de la plantilla  

Aquí es donde indicas al procesador el archivo Excel que contiene los marcadores.

```java
// Step 3: Load the workbook that contains Smart Markers
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

*¿Por qué?*  
Cargar el libro de trabajo en memoria permite que Aspose.Cells lo manipule sin tocar el archivo original en disco. Puedes reutilizar de forma segura el mismo archivo de plantilla para varios informes.

### Paso 4: Preparar una fuente de datos  

SmartMarkerProcessor espera una implementación de `IDataSource` que sepa cómo obtener valores para cada marcador. A continuación se muestra una fuente de datos **en memoria** mínima que utiliza un `Map<String, Object>`.

```java
// Step 4: Prepare the data source that provides values for the markers
class MapDataSource implements IDataSource {
    private final Map<String, Object> data;

    public MapDataSource(Map<String, Object> data) {
        this.data = data;
    }

    @Override
    public Object getValue(String key) {
        return data.get(key);
    }

    @Override
    public boolean isArray(String key) {
        // For this simple example we never return arrays
        return false;
    }

    @Override
    public int getLength(String key) {
        return 0; // not an array
    }

    @Override
    public Object getValue(String key, int index) {
        return null; // not an array
    }
}

// Example data that matches the markers in input.xlsx
Map<String, Object> values = new HashMap<>();
values.put("EmployeeName", "Jane Doe");
values.put("Department", "Engineering");
values.put("Salary", 95000);
values.put("ReportDate", LocalDate.now().toString());

IDataSource dataSource = new MapDataSource(values);
```

*¿Por qué esta implementación?*  
Es ligera, no requiere una base de datos externa y es perfecta para demostraciones o pruebas unitarias. En un escenario real reemplazarías `MapDataSource` por algo que obtenga datos de un conjunto de resultados JDBC, una API REST o una entidad ORM.

### Paso 5: Aplicar los datos al libro de trabajo  

Ahora ocurre la magia: los Smart Markers se reemplazan con los valores de tu `IDataSource`.

```java
// Step 5: Apply the data to the workbook, generating the detail sheet
processor.apply(workbook, dataSource);
```

*¿Qué ocurre detrás de escena?*  
Aspose.Cells itera sobre cada celda que contiene un marcador como `${EmployeeName}`. Para cada marcador, llama a `IDataSource.getValue("EmployeeName")` y escribe el valor devuelto en la celda. Si tuvieras un marcador de tabla (`${Employees}`), el procesador expandiría automáticamente las filas según la longitud del arreglo.

### Paso 6: Guardar el libro de trabajo procesado  

Finalmente, escribe el libro de trabajo poblado en disco (o envíalo directamente a la respuesta HTTP si estás en una aplicación web).

```java
// Step 6: Save the processed workbook
workbook.save("YOUR_DIRECTORY/output.xlsx");
```

*Consejo:*  
Utiliza la sobrecarga `workbook.save(OutputStream, SaveFormat.XLSX)` cuando necesites enviar el archivo a un cliente sin tocar el sistema de archivos.

---

## Crear informe de Excel a partir de una plantilla – Consejos avanzados

Ahora que el flujo básico funciona, exploremos un par de mejoras comunes que hacen que tu **informe de Excel a partir de una plantilla** esté listo para producción.

### H3: Manejo de colecciones (Tablas)

Si tu plantilla contiene un bloque repetitivo como una tabla de ventas, reemplaza el marcador con un arreglo en tu fuente de datos.

```java
class ListDataSource implements IDataSource {
    private final Map<String, List<Map<String, Object>>> tables = new HashMap<>();

    public void addTable(String name, List<Map<String, Object>> rows) {
        tables.put(name, rows);
    }

    @Override
    public boolean isArray(String key) {
        return tables.containsKey(key);
    }

    @Override
    public int getLength(String key) {
        List<Map<String, Object>> rows = tables.get(key);
        return rows == null ? 0 : rows.size();
    }

    @Override
    public Object getValue(String key, int index) {
        List<Map<String, Object>> rows = tables.get(key);
        return rows != null ? rows.get(index) : null;
    }

    @Override
    public Object getValue(String key) {
        // Not used for arrays
        return null;
    }
}

// Sample table data
List<Map<String, Object>> sales = new ArrayList<>();
sales.add(Map.of("Product", "Widget A", "Qty", 120, "Revenue", 4800));
sales.add(Map.of("Product", "Widget B", "Qty", 75,  "Revenue", 3375));

ListDataSource listSource = new ListDataSource();
listSource.addTable("SalesData", sales);

// Apply as before
processor.apply(workbook, listSource);
```

En la plantilla tendrías marcadores como `${SalesData.Product}`, `${SalesData.Qty}`, etc., dentro de una fila que Aspose replicará para cada entrada.

### H3: Formateo de fechas y números

Los Smart Markers respetan el formato de la celda. Si preformateas una celda como *Moneda* en la plantilla, el valor numérico que envíes se mostrará automáticamente con el símbolo y los decimales correctos. No se necesita código adicional; solo asegúrate de que el tipo de datos que devuelvas (`Double`, `BigDecimal`, `LocalDate`) coincida con el formato esperado.

### H3: Consideraciones de rendimiento

- **Reutiliza el procesador** si generas decenas de informes en lote; simplemente llama a `processor.clear()` entre ejecuciones.  
- **Desactiva el cálculo** (`workbook.getSettings().setRecalcOnLoad(false)`) cuando solo necesitas escribir valores, no recalcular fórmulas.  
- **Transmite la salida** para evitar archivos temporales grandes al ejecutarse en un entorno con recursos limitados.

---

## Resultado esperado

Después de ejecutar el ejemplo de seis pasos, `output.xlsx` contendrá:

| A               | B          | C            |
|-----------------|------------|--------------|
| EmployeeName    | Jane Doe   |              |
| Department      | Engineering|              |
| Salary          | 95,000     |              |
| ReportDate      | 2026‑06‑30 |              |
| …               | …          | …            |

Si añadiste el ejemplo de tabla, verás una tabla de ventas completamente poblada justo debajo de las filas de encabezado. Todo el formato que aplicaste en `input.xlsx` (símbolos de moneda, patrones de fecha, encabezados en negrita) permanece intacto.

---

## Conclusión

Acabamos de repasar cómo **poblar una plantilla de Excel con datos** usando `SmartMarkerProcessor` de Aspose.Cells, y ahora conoces los pasos exactos para **crear un informe de Excel a partir de una plantilla** en Java. La idea central es simple: define Smart Markers en un libro reutilizable, proporciona un `IDataSource` compatible y deja que la biblioteca se encargue del trabajo pesado.  

Desde aquí puedes:

- Conectar una base de datos real en lugar de `MapDataSource`.  
- Agregar gráficos que reflejen automáticamente los nuevos datos.  
- Desplegar el código como un microservicio que devuelva el archivo Excel generado bajo demanda.  

Pruébalo, ajusta los marcadores y observa cómo tu flujo de generación de informes se reduce drásticamente. ¿Tienes preguntas o un escenario de marcador complicado? Deja un comentario abajo—¡feliz codificación!

## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y funcionales con explicaciones paso a paso para ayudarte a dominar características adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Poblar Excel con datos anidados usando Aspose.Cells para Java: Guía completa](/cells/english/java/data-manipulation/populate-excel-nested-data-aspose-cells-java/)
- [Exportar datos XML desde Excel usando Aspose.Cells en Java: Guía paso a paso](/cells/english/java/import-export/export-excel-xml-data-aspose-cells-java/)
- [Cómo crear y formatear celdas de Excel usando Aspose.Cells para Java: Guía paso a paso](/cells/english/java/formatting/aspose-cells-java-excel-automation-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}