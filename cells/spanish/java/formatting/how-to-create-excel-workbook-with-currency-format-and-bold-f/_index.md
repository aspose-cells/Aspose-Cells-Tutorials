---
category: general
date: 2026-08-20
description: Crear un libro de Excel en Java usando Aspose.Cells, establecer formato
  de moneda, agregar fuente en negrita e importar una matriz de estilos para celdas
  con estilo.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook
- set currency format
- format cells currency
- how to import style
- add bold font
language: es
lastmod: 2026-08-20
og_description: Crear un libro de Excel en Java, establecer formato de moneda, agregar
  fuente en negrita y aprender cómo importar estilo usando Aspose.Cells.
og_image_alt: Screenshot of an excel workbook created with currency format and bold
  font using Aspose.Cells
og_title: Crear libro de Excel con celdas de moneda con estilo en Java
schemas:
- author: Aspose
  dateModified: '2026-08-20'
  description: Create excel workbook in Java using Aspose.Cells, set currency format,
    add bold font, and import style array for styled cells.
  headline: How to create excel workbook with currency format and bold font in Java
  type: TechArticle
- description: Create excel workbook in Java using Aspose.Cells, set currency format,
    add bold font, and import style array for styled cells.
  name: How to create excel workbook with currency format and bold font in Java
  steps:
  - name: Initialise the workbook and worksheet
    text: Creating a fresh workbook gives you a clean container for all subsequent
      formatting.
  - name: Build a DataTable with numeric data
    text: A `DataTable` mimics a database table, making it easy to import rows in
      bulk.
  - name: Define a style – currency format and bold font
    text: Here we **set currency format** and **add bold font** to a `Style` object.
  - name: Configure import options to use the style array
    text: Aspose.Cells lets you pass a `Style[]` via `ImportTableOptions`. This is
      the official **how to import style** method.
  - name: Import the DataTable into the worksheet
    text: Now we bring the data into the sheet at cell `A1`, applying the style array
      automatically.
  - name: Save the workbook to disk
    text: Finally, write the in‑memory workbook to a physical file.
  - name: Expected output
    text: 'When you open `DataTableWithStyleArray.xlsx` in Microsoft Excel, you should
      see:'
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel
- Formatting
title: Cómo crear un libro de Excel con formato de moneda y fuente en negrita en Java
url: /es/java/formatting/how-to-create-excel-workbook-with-currency-format-and-bold-f/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo crear un libro de Excel con formato de moneda y fuente en negrita en Java

Si necesitas **crear un libro de Excel** programáticamente, esta guía te muestra exactamente cómo. Recorreremos la creación de un libro, la aplicación de un formato de moneda, la adición de una fuente en negrita y el uso de la función **how to import style** de Aspose.Cells para que cada celda importada tenga un aspecto consistente.

Terminarás con un archivo `DataTableWithStyleArray.xlsx` listo para usar que muestra los números como dólares y los resalta en negrita. No se requiere formateo manual en Excel.

## Requisitos previos

Antes de comenzar, asegúrate de tener:

- Java 17 o posterior instalado.
- Una licencia de Aspose.Cells for Java (o una clave de evaluación gratuita).
- Maven o Gradle para gestionar la dependencia `aspose-cells`.
- Familiaridad básica con colecciones de Java y `DataTable`.

```xml
<!-- Maven dependency -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version>
</dependency>
```

> **Consejo profesional:** Si te encuentras con una `LicenseException`, coloca tu archivo de licencia en el classpath y llama a `License license = new License(); license.setLicense("Aspose.Total.Java.lic");` antes de crear el libro.

## Cómo crear un libro de Excel con celdas de moneda con estilo

Esta sección contiene los pasos principales. Cada paso explica **por qué** es importante, no solo **qué** escribir.

### Paso 1: Inicializar el libro y la hoja de cálculo

Crear un libro nuevo te brinda un contenedor limpio para todo el formateo posterior.

```java
// Step 1: Create a new workbook and get the first worksheet
Workbook workbook = new Workbook();                     // creates an empty .xlsx file in memory
Worksheet worksheet = workbook.getWorksheets().get(0); // first sheet is index 0
Cells cells = worksheet.getCells();                     // shortcut to work with cells
```

> **Por qué:** El objeto `Workbook` representa todo el archivo Excel. Acceder a la primera `Worksheet` te permite comenzar a rellenar datos de inmediato.

### Paso 2: Construir un DataTable con datos numéricos

Un `DataTable` imita una tabla de base de datos, lo que facilita la importación masiva de filas.

```java
// Step 2: Build a DataTable with sample numeric data
DataTable dataTable = new DataTable();
dataTable.getColumns().add("Amount", DataType.DOUBLE); // column type DOUBLE ensures numeric handling
dataTable.getRows().add(new Object[]{1234.56});
dataTable.getRows().add(new Object[]{7890.12});
```

> **Por qué:** Usar `DOUBLE` garantiza que los valores mantengan su precisión decimal, lo cual es esencial cuando más adelante **format cells currency**.

### Paso 3: Definir un estilo – formato de moneda y fuente en negrita

Aquí **establecemos el formato de moneda** y **añadimos fuente en negrita** a un objeto `Style`.

```java
// Step 3: Define a style (currency format and bold font) for the imported cells
Style currencyStyle = workbook.createStyle();                // create a reusable style instance
currencyStyle.getNumber().setFormat("$#,##0.00");            // set currency format (e.g., $1,234.56)
currencyStyle.getFont().setBold(true);                      // make the font bold
Style[] styleArray = new Style[] { currencyStyle };          // style array required by ImportTableOptions
```

> **Por qué:** La cadena de formato `Number` `$#,##0.00` indica a Excel que trate la celda como un valor monetario, mientras que `setBold(true)` llama la atención sobre los números. Colocar el estilo en un arreglo nos prepara para el paso **how to import style**.

### Paso 4: Configurar opciones de importación para usar el arreglo de estilos

Aspose.Cells permite pasar un `Style[]` mediante `ImportTableOptions`. Este es el método oficial de **how to import style**.

```java
// Step 4: Set up import options to use the style array
ImportTableOptions importOptions = new ImportTableOptions();
importOptions.setStyleArray(styleArray); // tells the importer to apply our currencyStyle to every column
```

> **Por qué:** Sin `ImportTableOptions`, las celdas importadas heredarían el estilo predeterminado, perdiendo el formato de moneda y la negrita que definimos.

### Paso 5: Importar el DataTable en la hoja de cálculo

Ahora llevamos los datos a la hoja en la celda `A1`, aplicando el arreglo de estilos automáticamente.

```java
// Step 5: Import the DataTable into the worksheet at A1, applying the style
cells.importDataTable(dataTable, true, "A1", importOptions);
```

- `true` indica que la primera fila del `DataTable` contiene encabezados de columna.
- `"A1"` es la esquina superior izquierda donde comienza la importación.

> **Por qué:** Importar con el arreglo de estilos garantiza que cada celda importada reciba el estilo **format cells currency** que preparamos anteriormente.

### Paso 6: Guardar el libro en disco

Finalmente, escribe el libro en memoria a un archivo físico.

```java
// Step 6: Save the workbook to a file
String outputPath = "YOUR_DIRECTORY/DataTableWithStyleArray.xlsx";
workbook.save(outputPath);
System.out.println("Workbook saved to: " + outputPath);
```

> **Por qué:** Guardar persiste el formateo, permitiendo que tú o procesos posteriores abran el archivo en Excel con la apariencia deseada.

## Código fuente completo

A continuación se muestra la clase Java completa y lista para ejecutar. Cópiala en tu IDE, reemplaza `YOUR_DIRECTORY` por una carpeta existente y ejecútala.

```java
import com.aspose.cells.*;

public class StyleArrayImportTutorial {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.getWorksheets().get(0);
        Cells cells = worksheet.getCells();

        // Step 2: Build a DataTable with sample numeric data
        DataTable dataTable = new DataTable();
        dataTable.getColumns().add("Amount", DataType.DOUBLE);
        dataTable.getRows().add(new Object[]{1234.56});
        dataTable.getRows().add(new Object[]{7890.12});

        // Step 3: Define a style (currency format and bold font) for the imported cells
        Style currencyStyle = workbook.createStyle();
        currencyStyle.getNumber().setFormat("$#,##0.00");   // set currency format
        currencyStyle.getFont().setBold(true);             // add bold font
        Style[] styleArray = new Style[] { currencyStyle };

        // Step 4: Set up import options to use the style array
        ImportTableOptions importOptions = new ImportTableOptions();
        importOptions.setStyleArray(styleArray);           // how to import style

        // Step 5: Import the DataTable into the worksheet at A1, applying the style
        cells.importDataTable(dataTable, true, "A1", importOptions);

        // Step 6: Save the workbook to a file
        workbook.save("YOUR_DIRECTORY/DataTableWithStyleArray.xlsx");
        System.out.println("Workbook created successfully.");
    }
}
```

### Resultado esperado

Al abrir `DataTableWithStyleArray.xlsx` en Microsoft Excel, deberías ver:

| Cantidad |
|----------|
| **$1,234.56** |
| **$7,890.12** |

- Los números se muestran con un **formato de moneda** (signo `$`, dos decimales).
- La fuente de ambas celdas es **negrita**, lo que las hace resaltar.

## Variaciones comunes y casos límite

| Escenario | Qué cambiar | Razón |
|-----------|-------------|-------|
| **Moneda diferente** | `currencyStyle.getNumber().setFormat("€#,##0.00");` | Utiliza el símbolo del euro o cualquier formato específico de localidad. |
| **Múltiples columnas con estilos diferentes** | Create multiple `Style` objects, populate `styleArray` in the same order as columns. | Cada columna puede tener su propio formato numérico, fuente, fondo, etc. |
| **Conjuntos de datos grandes** | Use `cells.importDataTable(dataTable, false, "A1", importOptions);` and set `importOptions.setImportDataOptions(ImportDataOptions.DATA_ONLY);` | Mejora el rendimiento al omitir filas de encabezado o metadatos innecesarios. |
| **Aplicar estilo después de la importación** | Call `cells.get("A2").setStyle(currencyStyle);` for individual cells. | Útil cuando solo un subconjunto de filas necesita un formato especial. |

## Consejos para uso en producción

- **Licencia temprana**: Registra tu licencia de Aspose.Cells antes de crear el libro para evitar la marca de agua de evaluación.
- **Seguridad de subprocesos**: Las instancias de `Workbook` **no** son seguras para subprocesos. Crea una instancia separada por subproceso si generas muchos archivos simultáneamente.
- **Gestión de memoria**: Para hojas muy grandes, considera usar la API de streaming de `Workbook` (`Workbook` → `WorkbookDesigner`) para mantener bajo el uso de memoria.
- **Pruebas**: Incluye una prueba unitaria que abra el archivo guardado con Apache POI y verifique que el formato numérico del estilo de celda coincida con `"$#,##0.00"`.

## Conclusión

Ahora sabes cómo **crear un libro de Excel** en Java, **establecer el formato de moneda**, **añadir fuente en negrita**, y usar correctamente **how to import style** mediante `ImportTableOptions` de Aspose.Cells. Esta solución de extremo a extremo elimina los pasos manuales en Excel y garantiza que cada celda importada siga el mismo estilo **format cells currency**.

¿Listo para el siguiente desafío? Prueba a añadir formato condicional, incrustar gráficos o exportar el libro a PDF, todo reutilizando la misma técnica de arreglo de estilos. ¡Feliz codificación!

## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y funcionales con explicaciones paso a paso para ayudarte a dominar características adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Crear un libro de Excel usando Aspose.Cells en Java: Guía paso a paso](/cells/english/java/getting-started/create-excel-workbook-aspose-cells-java/)
- [Cómo crear y formatear celdas de Excel usando Aspose.Cells para Java: Guía paso a paso](/cells/english/java/formatting/aspose-cells-java-excel-automation-guide/)
- [Cómo dar estilo a celdas de Excel y añadir hipervínculos usando Aspose.Cells para Java](/cells/english/java/formatting/style-excel-cells-hyperlinks-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}