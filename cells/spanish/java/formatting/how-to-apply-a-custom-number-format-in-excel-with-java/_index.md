---
category: general
date: 2026-11-22
description: Aprende a usar un formato numérico personalizado para dar formato a una
  columna como moneda en Excel usando Java. Configura el formato numérico de Excel
  rápidamente con un estilo sencillo.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- custom number format
- format column as currency
- set excel number format
- set currency format
- style first column
language: es
lastmod: 2026-11-22
og_description: Aplicar un formato numérico personalizado en Excel con Java. Este
  tutorial muestra cómo establecer el formato numérico en Excel y dar estilo a la
  primera columna como moneda.
og_image_alt: Java code snippet that applies a custom number format to an Excel column
og_title: Aplicar un formato numérico personalizado en Excel con Java – guía paso
  a paso
schemas:
- author: Aspose
  dateModified: '2026-11-22'
  description: Learn how to use a custom number format to format a column as currency
    in Excel using Java. Set Excel number format quickly with a simple style.
  headline: How to apply a custom number format in Excel with Java
  type: TechArticle
tags:
- Java
- Excel
- Apache POI
- Spreadsheet Automation
title: Cómo aplicar un formato de número personalizado en Excel con Java
url: /es/java/formatting/how-to-apply-a-custom-number-format-in-excel-with-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo aplicar un formato numérico personalizado en Excel con Java

Si necesitas **custom number format** una columna en una hoja de cálculo de Excel, esta guía te muestra exactamente cómo hacerlo usando Java. Ya sea que estés generando informes financieros o exportando datos contables, formatear la primera columna como moneda hace que la salida sea instantáneamente legible.

En el ejemplo a continuación **format column as currency**, aplicaremos el estilo a la primera columna y luego importaremos una `DataTable` en la hoja de cálculo. El mismo enfoque funciona para cualquier formato numérico que desees mostrar.

## Lo que aprenderás

* Cómo crear un **custom number format** con el objeto `Style` de Apache POI.  
* Cómo **set Excel number format** para una columna específica, incluido el caso **set currency format**.  
* Cómo **style first column** al importar una `DataTable`.  
* Cómo guardar el libro de trabajo y verificar que el formato aparezca correctamente.

## Requisitos previos

* Java 17 o superior.  
* Apache POI 5.x (la biblioteca que proporciona `Workbook`, `Worksheet` y `Style`).  
* Una implementación de `DataTable` que pueda iterarse como la del ejemplo de código.  
* Familiaridad básica con conceptos de Java y Excel.

---

## Paso 1: Configurar el proyecto e importar los datos

Primero, agrega Apache POI a tu proyecto. Si usas Maven, incluye la siguiente dependencia:

```xml
<!-- pom.xml -->
<dependency>
    <groupId>org.apache.poi</groupId>
    <artifactId>poi-ooxml</artifactId>
    <version>5.2.3</version>
</dependency>
```

A continuación, obtén los datos fuente como una `DataTable`. En un escenario real, esto podría provenir de una consulta a base de datos, un archivo CSV o una respuesta de API.

```java
// Step 1: Obtain the source data as a DataTable
DataTable dataTable = getData();   // replace with your own data‑fetching logic
```

> **Consejo profesional:** Asegúrate de que las columnas de la `DataTable` tengan los tipos Java correctos (`Integer`, `Double`, etc.) porque el formato numérico solo afecta a las celdas numéricas.

---

## Paso 2: Crear un **custom number format** para la primera columna

Un **custom number format** indica a Excel cómo mostrar los valores numéricos. Para mostrar valores como moneda usamos el formato incorporado `CURRENCY`, pero también puedes definir patrones como `"$#,##0.00"`.

```java
// Step 2: Prepare a Style array – one entry per column in the DataTable
Style[] columnStyles = new Style[dataTable.getColumns().size()];

// Step 3: Create a style for the first column and set it to display values as currency
// wb – existing Workbook instance (e.g., XSSFWorkbook for .xlsx files)
Workbook wb = new XSSFWorkbook();
columnStyles[0] = wb.createCellStyle();               // style first column
columnStyles[0].setDataFormat(
        wb.createDataFormat().getFormat(Style.CustomNumberFormat.CURRENCY));
```

**Por qué esto funciona:**  
* `createCellStyle()` devuelve un objeto de estilo reutilizable.  
* `setDataFormat()` adjunta el **set currency format** al estilo, que Excel aplica a cada celda que usa este estilo.  
* Al almacenar el estilo en `columnStyles[0]` garantizamos que solo la primera columna reciba el formato de moneda.

---

## Paso 3: Importar la `DataTable` aplicando los estilos de columna

Ahora importamos los datos en la hoja de cálculo. El método `importDataTable` acepta el arreglo de estilos, lo que nos permite **style first column** y dejar las columnas restantes con el formato predeterminado.

```java
// Step 4: Import the DataTable into the worksheet, applying the column styles
// ws – existing Worksheet instance
Worksheet ws = wb.createSheet("Report");

// true  → import column headers
// 0,0   → start at cell A1
ws.getCells().importDataTable(dataTable, true, 0, 0, columnStyles);
```

La llamada anterior **sets Excel number format** solo para la primera columna. Todas las demás columnas heredan el estilo predeterminado del libro de trabajo, lo que mantiene el código simple y eficiente.

---

## Paso 4: Guardar el libro de trabajo y verificar el resultado

Finalmente, escribe el libro de trabajo a un archivo y ábrelo en Excel para confirmar que la primera columna muestra símbolos de moneda.

```java
// Step 5: Save the workbook to disk
try (FileOutputStream fileOut = new FileOutputStream("FormattedReport.xlsx")) {
    wb.write(fileOut);
}
System.out.println("Workbook saved as FormattedReport.xlsx");
```

**Salida esperada:**  
Cuando abras *FormattedReport.xlsx*, los valores en la columna A aparecen con el símbolo de moneda apropiado (p. ej., `$1,234.00`). Todas las demás columnas conservan su representación numérica original.

---

## Variaciones comunes y casos límite

| Situación | Ajuste |
|-----------|------------|
| **Different currency** (e.g., Euro) | Reemplaza `Style.CustomNumberFormat.CURRENCY` con un patrón personalizado: <br>`wb.createDataFormat().getFormat("\"€\"#,##0.00")` |
| **More than one styled column** | Rellena entradas adicionales en `columnStyles[]` con sus propios objetos `CellStyle`. |
| **Large data sets** | Usa `importDataTable` en lotes o transmite filas para evitar `OutOfMemoryError`. |
| **Locale‑specific separators** | Utiliza `java.text.NumberFormat` para generar un patrón dependiente de la configuración regional y pásalo a `setDataFormat`. |

> **Cuidado con:** Reutilizar un único objeto `CellStyle` en muchas columnas puede causar un formato inesperado porque Excel limita el número de estilos distintos por libro de trabajo. Crea un estilo separado para cada formato único que necesites.

---

## Ejemplo completo ejecutable

A continuación se muestra un programa autocontenido que demuestra todo el flujo de trabajo, desde la creación de datos hasta guardar el libro de trabajo formateado.

```java
import java.io.FileOutputStream;
import java.util.ArrayList;
import java.util.List;

import org.apache.poi.ss.usermodel.*;
import org.apache.poi.xssf.usermodel.XSSFWorkbook;

/* Mock DataTable implementation for demonstration purposes */
class DataTable {
    private final List<String> columns = List.of("Amount", "Description");
    private final List<Object[]> rows = new ArrayList<>();

    public DataTable() {
        rows.add(new Object[]{1234.5, "Consulting"});
        rows.add(new Object[]{5678.9, "Licensing"});
    }

    public List<String> getColumns() { return columns; }
    public List<Object[]> getRows() { return rows; }
}

/* Helper that mimics the importDataTable method used in the original snippet */
class WorksheetHelper {
    private final Sheet sheet;
    private final Workbook wb;

    public WorksheetHelper(Workbook wb, Sheet sheet) {
        this.wb = wb;
        this.sheet = sheet;
    }

    public void importDataTable(DataTable dt, boolean includeHeaders,
                                int startRow, int startCol, Style[] styles) {
        int rowIdx = startRow;
        if (includeHeaders) {
            Row header = sheet.createRow(rowIdx++);
            for (int c = 0; c < dt.getColumns().size(); c++) {
                Cell cell = header.createCell(startCol + c);
                cell.setCellValue(dt.getColumns().get(c));
            }
        }
        for (Object[] rowData : dt.getRows()) {
            Row row = sheet.createRow(rowIdx++);
            for (int c = 0; c < rowData.length; c++) {
                Cell cell = row.createCell(startCol + c);
                Object value = rowData[c];
                if (value instanceof Number) {
                    cell.setCellValue(((Number) value).doubleValue());
                } else {
                    cell.setCellValue(value.toString());
                }
                // Apply custom style if provided
                if (styles != null && c < styles.length && styles[c] != null) {
                    cell.setCellStyle((CellStyle) styles[c]);
                }
            }
        }
    }
}

/* Main class that puts everything together */
public class CustomNumberFormatDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Obtain the source data
        DataTable dataTable = new DataTable();

        // 2️⃣ Create a workbook and a sheet
        Workbook wb = new XSSFWorkbook();
        Sheet ws = wb.createSheet("Report");

        // 3️⃣ Prepare a style array – one entry per column
        Style[] columnStyles = new Style[dataTable.getColumns().size()];

        // 4️⃣ Create a style for the first column (currency)
        CellStyle currencyStyle = wb.createCellStyle();
        DataFormat fmt = wb.createDataFormat();
        currencyStyle.setDataFormat(fmt.getFormat("$#,##0.00"));
        columnStyles[0] = currencyStyle;   // style first column

        // 5️⃣ Import the DataTable, applying the column styles
        WorksheetHelper helper = new WorksheetHelper(wb, ws);
        helper.importDataTable(dataTable, true, 0, 0, columnStyles);

        // 6️⃣ Save the workbook
        try (FileOutputStream out = new FileOutputStream("FormattedReport.xlsx")) {
            wb.write(out);
        }
        System.out.println("Workbook written to FormattedReport.xlsx");
    }
}
```

Ejecutar el programa crea **FormattedReport.xlsx** donde la columna A (la columna “Amount”) se muestra con un **custom number format** que muestra el signo de dólar y dos decimales.

---

## Conclusión

Ahora sabes cómo **custom number format** una hoja de cálculo de Excel desde Java, **format column as currency**, y **style first column** al importar datos. Creando un `CellStyle` reutilizable y pasándolo a `importDataTable`, puedes **set Excel number format** para cualquier columna sin iterar manualmente sobre cada celda.

Next, try:

* Usar `setDataFormat` con patrones específicos de la configuración regional para **set currency format**

## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y funcionales con explicaciones paso a paso para ayudarte a dominar funciones adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Establecer formato numérico en Excel con Java – Guía completa](/cells/english/java/formatting/set-number-format-excel-in-java-complete-guide/)
- [Aplicar formato numérico en Excel con Java – Guía completa de Aspose.Cells](/cells/english/java/formatting/apply-number-format-excel-in-java-complete-aspose-cells-guid/)
- [Cómo crear un libro de Excel con formato de moneda y fuente en negrita en Java](/cells/english/java/formatting/how-to-create-excel-workbook-with-currency-format-and-bold-f/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}