---
category: general
date: 2026-07-03
description: Incluye la exportación de fórmulas en Java para convertir celdas de Excel
  a texto usando Aspose.Cells. Aprende a imprimir un rango de Excel y obtener la cadena
  de valores de las celdas de manera eficiente.
draft: false
keywords:
- include formulas export
- convert excel cells text
- print excel range
- export table options
- get cell values string
language: es
og_description: Incluir exportación de fórmulas en Java para convertir celdas de Excel
  a texto. Guía paso a paso que muestra cómo imprimir un rango de Excel y obtener
  los valores de las celdas como una cadena.
og_title: Incluir exportación de fórmulas en Java – Convertir celdas de Excel a texto
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: Include formulas export in Java to convert Excel cells to text using
    Aspose.Cells. Learn how to print Excel range and get cell values string efficiently.
  headline: Include Formulas Export in Java – Convert Excel Cells to Text
  type: TechArticle
- description: Include formulas export in Java to convert Excel cells to text using
    Aspose.Cells. Learn how to print Excel range and get cell values string efficiently.
  name: Include Formulas Export in Java – Convert Excel Cells to Text
  steps:
  - name: Prerequisites
    text: '- Java 17 or newer (the code compiles with older versions but we’ll stick
      to the latest LTS). - Aspose.Cells for Java 23.10 (or any recent release)—you
      can grab it from Maven Central. - A sample `input.xlsx` placed in a folder you
      control (the path is hard‑coded in the example for clarity).'
  - name: Optional Tweaks
    text: '- `eto.setExportHiddenRows(true);` – include rows hidden in Excel. - `eto.setExportHiddenColumns(true);`
      – same for columns. - `eto.setExportAsHTML(true);` – get HTML instead of plain
      text.'
  - name: Expected Output (sample)
    text: '``` =SUM(A2:A3) 42 Hello =IF(B1>10,"Yes","No") =AVERAGE(C1:C3) =VLOOKUP(A1,Sheet2!A:B,2,FALSE)
      ```'
  - name: What if the range contains merged cells?
    text: Merged cells are treated as the value of the top‑left cell. The rest of
      the merged area will appear as empty strings. If you need the merged region’s
      address, query `Cell.getMergedRange()` before export.
  - name: Can I export a massive sheet (hundreds of thousands of rows)?
    text: Yes, but beware of memory consumption. Use `Workbook.getSettings().setMemorySetting(MemorySetting.MEMORY_PREFERENCE)`
      to let Aspose.Cells stream data to disk. Also, consider exporting in chunks
      (e.g., 10 000 rows at a time) to keep the string manageable.
  - name: How do I change the column delimiter?
    text: '`ExportTableOptions` exposes `setSeparator(char separator)`. For CSV‑style
      output, set it to `'',''`:'
  - name: Do formulas respect external references?
    text: If a formula points to another workbook, Aspose.Cells will keep the reference
      text (`='[Other.xlsx]Sheet1'!A1`). It won’t evaluate the external value unless
      you load that workbook as well.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel
- Export
title: Incluir exportación de fórmulas en Java – Convertir celdas de Excel a texto
url: /es/java/excel-import-export/include-formulas-export-in-java-convert-excel-cells-to-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Incluir exportación de fórmulas en Java – Convertir celdas de Excel a texto

¿Alguna vez necesitó **incluir exportación de fórmulas** al extraer datos de un libro de Excel? Tal vez esté construyendo un servicio de informes que debe preservar las fórmulas originales mientras entrega un bloque de texto ordenado. En ese caso, está en el lugar correcto. Esta guía le muestra cómo convertir celdas de Excel a texto plano—*incluyendo* cualquier fórmula incrustada—usando Aspose.Cells para Java.

También abordaremos cómo **imprimir rango de Excel**, ajustar **opciones de exportación de tabla**, y finalmente **obtener cadena de valores de celda** que puede registrar, enviar a través de una API o almacenar en una base de datos. Al final tendrá un fragmento completamente ejecutable y una comprensión sólida del porqué de cada llamada.

## Lo que obtendrá al final

- Un programa Java completo, listo para copiar y pegar, que lee un archivo `.xlsx`, selecciona un rango y lo exporta como una cadena formateada.
- Una comprensión de la clase `ExportTableOptions` y por qué es importante alternar `setExportAsString` y `setIncludeFormula`.
- Consejos para manejar hojas de cálculo grandes, tratar diferentes tipos de datos y personalizar el formato de salida.
- Una lista de verificación rápida de problemas comunes (piense en celdas combinadas, filas ocultas y formatos numéricos específicos de la configuración regional).

### Requisitos previos

- Java 17 o superior (el código compila con versiones anteriores pero utilizaremos la última LTS).
- Aspose.Cells para Java 23.10 (o cualquier versión reciente)—puede obtenerlo de Maven Central.
- Un archivo de muestra `input.xlsx` colocado en una carpeta que controle (la ruta está codificada en el ejemplo para mayor claridad).

Si ya los tiene, vamos a sumergirnos.

## Paso 1: Configurar el proyecto y agregar dependencias

Primero, cree un proyecto Maven (o Gradle, si lo prefiere). Agregue la dependencia de Aspose.Cells a su `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.10</version>
    <classifier>jdk17</classifier>
</dependency>
```

> **Consejo profesional:** Si está usando un proxy corporativo, asegúrese de que el repositorio sea accesible; de lo contrario la compilación fallará con un error “Could not resolve dependencies”.

Una vez que Maven termine de descargar, estará listo para escribir Java.

## Paso 2: Cargar el libro de trabajo y obtener la hoja de cálculo deseada

La primera línea del ejemplo de código muestra cómo abrir un libro de trabajo existente:

```java
// Step 1: Load the workbook
Workbook wb = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

Reemplace `YOUR_DIRECTORY` con la ruta absoluta o relativa a su archivo. El constructor `Workbook` detecta automáticamente el formato del archivo (XLS, XLSX, CSV, etc.), por lo que no necesita especificarlo.

A continuación, obtenemos la primera hoja:

```java
// Step 2: Get the first worksheet
Worksheet ws = wb.getWorksheets().get(0);
```

¿Por qué la primera hoja? En muchas plantillas los datos están en la primera pestaña, pero puede pasar cualquier índice o incluso usar `get("SheetName")` si prefiere un enfoque por nombre.

## Paso 3: Definir el rango que desea exportar

Ahora llega el corazón de la operación **convert excel cells text**. Le indica a Aspose.Cells qué celdas extraer creando un objeto `Range`:

```java
// Step 3: Create a range covering cells A1 to C3
Range rng = ws.getCells().createRange("A1:C3");
```

La cadena `"A1:C3"` es una dirección clásica estilo A1. También puede construirse programáticamente:

```java
int firstRow = 0, firstCol = 0, totalRows = 3, totalCols = 3;
Range rng = ws.getCells().createRange(firstRow, firstCol, totalRows, totalCols);
```

Esa flexibilidad ayuda cuando el tamaño del rango es dinámico—por ejemplo, si lee la última fila utilizada con `ws.getCells().getMaxDataRow()`.

## Paso 4: Configurar ExportTableOptions para incluir fórmulas

Aquí es donde vive la magia de **include formulas export**. Por defecto, Aspose.Cells devuelve los valores *mostrados*. Si una celda contiene `=SUM(A1:A3)`, obtendrá el número calculado, no el texto de la fórmula. Para cambiar eso, configure `ExportTableOptions`:

```java
// Step 4: Set up export options to return the range as a string and include formulas
ExportTableOptions eto = new ExportTableOptions();
eto.setExportAsString(true);      // Forces the result to be a single string
eto.setIncludeFormula(true);      // Includes the underlying formula instead of the evaluated value
```

¿Por qué ambas banderas? `setExportAsString(true)` indica a la API que concatene las celdas usando el delimitador predeterminado (tabulación para columnas, salto de línea para filas). `setIncludeFormula(true)` cambia la fuente del valor de “valor mostrado” a “fórmula cruda”. Si solo desea valores, déjelo `false`.

### Ajustes opcionales

- `eto.setExportHiddenRows(true);` – incluye filas ocultas en Excel.
- `eto.setExportHiddenColumns(true);` – lo mismo para columnas.
- `eto.setExportAsHTML(true);` – obtener HTML en lugar de texto plano.

Siéntase libre de experimentar; la clase de opciones es un patio de juegos de **export table options**.

## Paso 5: Recuperar el rango como una cadena formateada

Ahora extraemos los datos:

```java
// Step 5: Retrieve the range values as a formatted string using the options
String txt = rng.getValueAsString(eto);
```

El `txt` devuelto se ve algo así (asumiendo que A1:C3 contiene una mezcla de valores y fórmulas):

```
=SUM(A2:A3)	42	"Hello"
=IF(B1>10,"Yes","No")	=AVERAGE(C1:C3)	=VLOOKUP(A1,Sheet2!A:B,2,FALSE)
```

Observe la tabulación (`\t`) que separa columnas y el salto de línea (`\n`) que separa filas. Puede dividir la cadena más tarde si necesita una matriz 2‑D:

```java
String[] rows = txt.split("\n");
for (String row : rows) {
    String[] cells = row.split("\t");
    // Process each cell...
}
```

## Paso 6: Imprimir el resultado – “Print Excel Range” simplificado

Finalmente, volcamos la cadena a la consola:

```java
// Step 6: Print the resulting string
System.out.println(txt);
```

Ejecutar el programa imprime la salida exacta mostrada arriba. Desde aquí podría escribir la cadena en un archivo de registro, enviarla por HTTP o almacenarla en un documento NoSQL.

## Ejemplo completo, listo para ejecutar

Juntándolo todo, aquí está el programa completo. Copie, pegue y presione **Run**—sin importaciones faltantes.

```java
import com.aspose.cells.*;

public class ExportFormulaRange {
    public static void main(String[] args) throws Exception {
        // Load the workbook
        Workbook wb = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // Grab the first worksheet
        Worksheet ws = wb.getWorksheets().get(0);

        // Define the range A1:C3 (adjust as needed)
        Range rng = ws.getCells().createRange("A1:C3");

        // Configure export options: string output + include formulas
        ExportTableOptions eto = new ExportTableOptions();
        eto.setExportAsString(true);
        eto.setIncludeFormula(true);

        // Get the string representation of the range
        String txt = rng.getValueAsString(eto);

        // Print the resulting text
        System.out.println(txt);
    }
}
```

### Salida esperada (ejemplo)

```
=SUM(A2:A3)	42	Hello
=IF(B1>10,"Yes","No")	=AVERAGE(C1:C3)	=VLOOKUP(A1,Sheet2!A:B,2,FALSE)
```

Si su libro de trabajo contiene números formateados como fechas, aparecerán en el formato específico de la configuración regional (p.ej., `2026‑07‑03`). Para forzar fechas ISO, puede ajustar `ExportTableOptions` con un `NumberFormat` personalizado.

## Manejo de casos límite y preguntas comunes

### ¿Qué pasa si el rango contiene celdas combinadas?

Las celdas combinadas se tratan como el valor de la celda superior‑izquierda. El resto del área combinada aparecerá como cadenas vacías. Si necesita la dirección de la región combinada, consulte `Cell.getMergedRange()` antes de exportar.

### ¿Puedo exportar una hoja masiva (cientos de miles de filas)?

Sí, pero tenga cuidado con el consumo de memoria. Use `Workbook.getSettings().setMemorySetting(MemorySetting.MEMORY_PREFERENCE)` para permitir que Aspose.Cells transmita datos al disco. Además, considere exportar en fragmentos (p.ej., 10 000 filas a la vez) para mantener la cadena manejable.

### ¿Cómo cambio el delimitador de columna?

`ExportTableOptions` expone `setSeparator(char separator)`. Para salida estilo CSV, configúrelo a `','`:

```java
eto.setSeparator(',');
```

### ¿Las fórmulas respetan referencias externas?

Si una fórmula apunta a otro libro de trabajo, Aspose.Cells mantendrá el texto de referencia (`='[Other.xlsx]Sheet1'!A1`). No evaluará el valor externo a menos que también cargue ese libro de trabajo.

## Consejos profesionales para código listo para producción

- **Cache el libro de trabajo** si está leyendo el

## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y funcionales con explicaciones paso a paso para ayudarle a dominar características adicionales de la API y explorar enfoques de implementación alternativos en sus propios proyectos.

- [Cómo crear y exportar Excel a HTML usando Aspose.Cells Java \| Guía de operaciones de libro de trabajo](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)
- [Cómo convertir Excel a PDF en Java usando Aspose.Cells: Guía paso a paso](/cells/english/java/workbook-operations/convert-excel-to-pdf-aspose-cells-java/)
- [Exportar libro de Excel como imagen usando Aspose.Cells para Java: Guía paso a paso](/cells/english/java/import-export/export-excel-workbook-as-image-using-aspose-cells-for-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}