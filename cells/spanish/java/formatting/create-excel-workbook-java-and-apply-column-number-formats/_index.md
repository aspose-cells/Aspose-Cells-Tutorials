---
category: general
date: 2026-09-27
description: Crear libro de Excel en Java, importar datos de SQL, establecer formato
  numérico en la columna y guardar el libro como XLSX usando Aspose.Cells en Java.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook java
- save workbook as xlsx
- import sql data excel
- add number format excel
- set number format column
language: es
lastmod: 2026-09-27
og_description: Crear libro de Excel en Java, importar datos de SQL, establecer formato
  numérico en una columna y guardar el libro como XLSX con un ejemplo Java totalmente
  funcional.
og_image_alt: Screenshot of a Java program creating an Excel workbook with styled
  numeric columns
og_title: Crear libro de Excel en Java – importar datos SQL y establecer formatos
  numéricos de columnas
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Create Excel workbook java, import SQL data, set number format column,
    and save workbook as XLSX using Aspose.Cells in Java.
  headline: Create Excel workbook java and apply column number formats
  type: TechArticle
tags:
- Java
- Aspose.Cells
- Excel automation
- Data import
title: Crear libro de Excel en Java y aplicar formatos numéricos a columnas
url: /es/java/formatting/create-excel-workbook-java-and-apply-column-number-formats/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crear Excel workbook java y aplicar formatos numéricos a columnas

Si necesitas **create Excel workbook java** y dar estilo a columnas numéricas, esta guía te muestra exactamente cómo. Aprenderás a importar datos SQL a Excel, establecer un formato numérico para cada columna y **save workbook as XLSX** usando la biblioteca Aspose.Cells.

Trabajar con hojas de cálculo desde Java a menudo se siente fragmentado—los desarrolladores copian y pegan fragmentos, olvidan formatear los números o terminan con archivos CSV en lugar de verdaderos archivos Excel. Este tutorial elimina esa fricción al proporcionar una solución única, de extremo a extremo, que puedes incorporar en cualquier proyecto Java.

Al final del artículo podrás:

* Conectar a una base de datos y recuperar un `DataTable` (o `ResultSet`)  
* Crear un nuevo workbook con Aspose.Cells  
* Aplicar un estilo consistente **add number format excel** a cada columna  
* **Save workbook as XLSX** a una ubicación de tu elección  

El único requisito previo es un entorno de desarrollo Java (se recomienda JDK 8+ ) y el JAR de Aspose.Cells for Java en tu classpath.

---

## Prerequisitos

| Requisito | Por qué es importante |
|-------------|----------------|
| JDK 8 o superior | Proporciona las características del lenguaje usadas en el ejemplo. |
| Aspose.Cells for Java (última versión) | Gestiona la creación, estilo y guardado de Excel sin necesidad de Office instalado. |
| Una base de datos compatible con JDBC (p.ej., MySQL, PostgreSQL) | Proporciona los datos SQL que importaremos. |
| Maven o Gradle (opcional) | Simplifica la gestión de dependencias. |

Agrega Aspose.Cells a tu `pom.xml` de Maven:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- use the latest stable version -->
</dependency>
```

O descarga el JAR directamente desde el sitio web de Aspose y agrégalo al classpath de tu proyecto.

---

## Paso 1: Crear Excel workbook java

El primer bloque lógico es instanciar un nuevo `Workbook`. Este objeto representa todo el archivo Excel en memoria y te brinda acceso a hojas de cálculo, celdas y estilos.

```java
// Step 1: Create a new workbook instance
Workbook workbook = new Workbook();
```

Crear el workbook al inicio también nos proporciona una fábrica `Style` que necesitaremos más adelante cuando **set number format column**.

---

## Paso 2: Recuperar datos de SQL (import sql data excel)

A continuación abrimos una conexión JDBC, ejecutamos una simple sentencia `SELECT` y cargamos el conjunto de resultados en un `DataTable` de Aspose. La clase `DataTable` imita al `DataTable` de .NET y funciona sin problemas con el método `importDataTable`.

```java
// Step 2: Pull data from a database and fill a DataTable
private static DataTable getDataTableFromDb() throws SQLException {
    // Replace with your actual connection string, user, and password
    String url = "jdbc:mysql://localhost:3306/yourdb";
    String user = "your_user";
    String password = "your_password";

    try (Connection conn = DriverManager.getConnection(url, user, password);
         Statement stmt = conn.createStatement();
         ResultSet rs = stmt.executeQuery("SELECT Id, Amount, CreatedDate FROM Payments")) {

        // Aspose.Cells provides a utility to convert ResultSet → DataTable
        return CellsHelper.getDataTableFromResultSet(rs);
    }
}
```

> **Consejo:** Si ya tienes un `DataTable` de otra fuente (p.ej., análisis de CSV), puedes omitir el código JDBC y devolver esa tabla directamente.

---

## Paso 3: Preparar un estilo reutilizable (add number format excel)

Queremos que cada columna numérica muestre los números con dos decimales y un separador de miles. En lugar de dar estilo a cada celda individualmente, creamos un objeto `Style` una vez por columna y lo reutilizamos durante la importación. Esta es la forma más eficiente de **add number format excel**.

```java
// Step 3: Build a style array – one style per column
private static Style[] buildColumnStyles(Workbook workbook, int columnCount) {
    Style[] styles = new Style[columnCount];
    for (int i = 0; i < columnCount; i++) {
        styles[i] = workbook.createStyle();
        // "0.00" = two decimal places; "#,##0.00" adds thousands separator
        styles[i].setNumber("#,##0.00");
    }
    return styles;
}
```

Puedes adaptar la cadena de formato (`"#,##0.00"`) a cualquier formato numérico de Excel que necesites. Para fechas, usa `styles[i].setCustom("mm-dd-yyyy")`, etc.

---

## Paso 4: Importar el DataTable y aplicar los estilos de columna

Ahora juntamos todo. La sobrecarga `importDataTable` nos permite pasar el `DataTable`, especificar si la primera fila debe tratarse como encabezados de columna y proporcionar el arreglo de estilos. Esto automáticamente **set number format column** para cada celda en la columna correspondiente.

```java
// Step 4: Import data with styles into the first worksheet
private static void importDataWithStyles(Workbook workbook, DataTable dataTable) {
    // Build a style for each column based on the number of columns in the DataTable
    Style[] columnStyles = buildColumnStyles(workbook, dataTable.getColumns().size());

    // Import the DataTable starting at cell A1 (row 0, column 0)
    workbook.getWorksheets().get(0).getCells()
            .importDataTable(dataTable, true, 0, 0, columnStyles);
}
```

Como pasamos `true` para la bandera `importColumnNames`, la primera fila de la hoja contiene los nombres de columna del `DataTable`. Cada fila subsecuente recibe los datos, ya formateados según el estilo que definimos.

---

## Paso 5: Guardar workbook como xlsx

El paso final es persistir el workbook en memoria a un archivo físico. Aspose.Cells soporta muchos formatos; usaremos el formato XLSX moderno, que es lo que la mayoría de aplicaciones esperan hoy.

```java
// Step 5: Save the workbook to an .xlsx file
private static void saveWorkbook(Workbook workbook, String filePath) throws IOException {
    workbook.save(filePath, com.aspose.cells.SaveFormat.XLSX);
}
```

Puedes cambiar `filePath` a cualquier ubicación válida en tu sistema. El método lanza `IOException` si el directorio no existe o no tienes permiso de escritura.

---

## Ejemplo completo y ejecutable

Unir todas las piezas produce un programa autónomo que puedes compilar y ejecutar inmediatamente.

```java
import com.aspose.cells.*;
import java.sql.*;

public class CreateExcelWorkbookJava {
    public static void main(String[] args) {
        try {
            // 1️⃣ Obtain data from the database
            DataTable dataTable = getDataTableFromDb();

            // 2️⃣ Create a new workbook that will hold the imported data
            Workbook workbook = new Workbook();

            // 3️⃣ Import the DataTable with a numeric style per column
            importDataWithStyles(workbook, dataTable);

            // 4️⃣ Save the workbook as XLSX
            String outputPath = "DataTableWithNumberFormat.xlsx";
            saveWorkbook(workbook, outputPath);

            System.out.println("Workbook created successfully at: " + outputPath);
        } catch (Exception e) {
            e.printStackTrace();
        }
    }

    // ---- Helper methods (see earlier sections) ----
    private static DataTable getDataTableFromDb() throws SQLException {
        String url = "jdbc:mysql://localhost:3306/yourdb";
        String user = "your_user";
        String password = "your_password";

        try (Connection conn = DriverManager.getConnection(url, user, password);
             Statement stmt = conn.createStatement();
             ResultSet rs = stmt.executeQuery("SELECT Id, Amount, CreatedDate FROM Payments")) {

            return CellsHelper.getDataTableFromResultSet(rs);
        }
    }

    private static Style[] buildColumnStyles(Workbook workbook, int columnCount) {
        Style[] styles = new Style[columnCount];
        for (int i = 0; i < columnCount; i++) {
            styles[i] = workbook.createStyle();
            styles[i].setNumber("#,##0.00"); // two decimals with thousands separator
        }
        return styles;
    }

    private static void importDataWithStyles(Workbook workbook, DataTable dataTable) {
        Style[] columnStyles = buildColumnStyles(workbook, dataTable.getColumns().size());
        workbook.getWorksheets().get(0).getCells()
                .importDataTable(dataTable, true, 0, 0, columnStyles);
    }

    private static void saveWorkbook(Workbook workbook, String filePath) throws IOException {
        workbook.save(filePath, SaveFormat.XLSX);
    }
}
```

### Resultado esperado

Ejecutar el programa crea un archivo llamado **DataTableWithNumberFormat.xlsx** en el directorio de trabajo. Ábrelo con Microsoft Excel, LibreOffice Calc o cualquier visor compatible con XLSX y verás:

| Id | Cantidad | FechaCreación |
|----|----------|----------------|
| 1  | 1,234.56 | 2023‑01‑15 |
| 2  | 78,900.00 | 2023‑02‑20 |
| …  | … | … |

*La columna **Amount** muestra los números con dos decimales y un separador de miles, gracias al estilo **add number format excel** que aplicamos.*

---

## Preguntas comunes y manejo de casos límite

| Pregunta | Respuesta |
|----------|-----------|
| **¿Qué pasa si mi consulta no devuelve filas?** | El `DataTable` estará vacío pero seguirá conteniendo las definiciones de columnas. El workbook contendrá solo la fila de encabezado, lo cual a menudo es suficiente para procesos posteriores. |
| **¿Cómo aplico diferentes formatos por columna?** | Modifica `buildColumnStyles` para inspeccionar el nombre de la columna o el tipo de datos y asignar un formato personalizado (p.ej., fechas, porcentajes). |
| **¿Puedo escribir directamente a un `ByteArrayOutputStream`?** | Sí. Reemplaza `workbook.save(filePath, SaveFormat.XLSX);` con

## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que se basan en las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y funcionales con explicaciones paso a paso para ayudarte a dominar características adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Cómo crear y guardar un libro de Excel como SVG usando Aspose.Cells for Java](/cells/english/java/workbook-operations/create-save-workbook-svg-aspose-cells-java/)
- [Crear y guardar libro de Excel Aspose Cells Java](/cells/hindi/java/workbook-operations/create-save-excel-workbook-aspose-cells-java/)
- [Crear y guardar libro de Excel Aspose Cells Java](/cells/german/java/workbook-operations/create-save-excel-workbook-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}