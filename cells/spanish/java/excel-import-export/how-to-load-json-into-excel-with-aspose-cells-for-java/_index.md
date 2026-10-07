---
category: general
date: 2026-10-07
description: Aprende cómo cargar JSON en Excel y generar XLSX a partir de JSON usando
  Aspose.Cells. Esta guía paso a paso también muestra cómo rellenar Excel desde JSON
  y guardar el libro de trabajo como XLSX.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- load json into excel
- generate xlsx from json
- populate excel from json
- save workbook as xlsx
- create workbook from json
language: es
lastmod: 2026-10-07
og_description: Cargue JSON en Excel y genere XLSX a partir de JSON usando Aspose.Cells
  para Java. Siga esta guía para poblar Excel con JSON y guardar el libro de trabajo
  como XLSX.
og_image_alt: Screenshot of an Excel workbook that was loaded with JSON data using
  Aspose.Cells
og_title: Cargar JSON en Excel con Aspose.Cells – guía completa de Java
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: Learn how to load JSON into Excel and generate XLSX from JSON using
    Aspose.Cells. This step‑by‑step guide also shows how to populate Excel from JSON
    and save workbook as XLSX.
  headline: How to load JSON into Excel with Aspose.Cells for Java
  type: TechArticle
- description: Learn how to load JSON into Excel and generate XLSX from JSON using
    Aspose.Cells. This step‑by‑step guide also shows how to populate Excel from JSON
    and save workbook as XLSX.
  name: How to load JSON into Excel with Aspose.Cells for Java
  steps:
  - name: 'Compile the program:'
    text: 'Compile the program:'
  - name: 'Run it:'
    text: 'Run it:'
  - name: Verify that `JsonSingleCell.xlsx` appears in the working directory and opens
      without errors.
    text: Verify that `JsonSingleCell.xlsx` appears in the working directory and opens
      without errors.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: Cómo cargar JSON en Excel con Aspose.Cells para Java
url: /es/java/excel-import-export/how-to-load-json-into-excel-with-aspose-cells-for-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cargar JSON en Excel con Aspose.Cells para Java

Si necesitas **cargar JSON en Excel**, este tutorial te muestra una forma fiable de hacerlo con Aspose.Cells para Java. Verás cómo generar XLSX a partir de JSON, poblar Excel desde JSON y, finalmente, **guardar el libro de trabajo como XLSX**—todo en un único programa autocontenido.

Trabajar con JSON en hojas de cálculo es común cuando exportas datos de servicios web, APIs o almacenes NoSQL. Al final de esta guía tendrás una clase Java lista para ejecutar que crea un libro de trabajo a partir de JSON y escribe el resultado en un archivo en disco.

## Requisitos previos

Antes de comenzar, asegúrate de tener:

* Java 8 o superior instalado (el código usa características estándar de Java).
* Biblioteca Aspose.Cells para Java (versión 23.10 o posterior). Puedes obtenerla desde el [Aspose website](https://downloads.aspose.com/cells/java) o mediante Maven Central.
* Un IDE o un editor de texto simple y una terminal para compilar y ejecutar código Java.
* Familiaridad básica con la sintaxis JSON y conceptos de Excel.

> **Consejo profesional:** Si utilizas Maven, agrega la siguiente dependencia a tu `pom.xml` para evitar la gestión manual de JARs:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.10</version>
</dependency>
```

## Paso 1: Configurar el proyecto e importar las clases necesarias

Crea una nueva clase Java llamada `JsonToExcelDemo`. Importa las clases de Aspose.Cells que necesitarás para la creación del libro de trabajo, el manejo de hojas de cálculo y el procesamiento de Smart Markers.

```java
package com.example.exceljson;

import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;
import com.aspose.cells.SmartMarkerProcessor;
import com.aspose.cells.SaveFormat;

public class JsonToExcelDemo {
    public static void main(String[] args) throws Exception {
        // The full implementation starts in the next step.
    }
}
```

*Por qué este paso es importante:* Importar las clases correctas garantiza que el compilador pueda localizar las APIs de Aspose.Cells. La clase `Workbook` representa el archivo Excel, mientras que `SmartMarkerProcessor` impulsa la conversión de JSON a Excel.

## Paso 2: Definir la fuente JSON que se cargará en Excel

Para este ejemplo usamos una pequeña matriz JSON que contiene dos objetos. En un escenario real podrías leer el JSON desde un archivo, un endpoint REST o una base de datos.

```java
// Step 2: Define the JSON data that will be used as the smart‑marker source
String jsonData = "[{\"Name\":\"John\",\"Age\":30},{\"Name\":\"Anna\",\"Age\":25}]";
```

*Por qué este paso es importante:* La cadena JSON es la fuente de datos para la operación de **poblar Excel desde JSON**. Mantener el JSON en una variable `String` facilita pasarlo al `SmartMarkerProcessor`.

## Paso 3: Crear un nuevo libro de trabajo y obtener la primera hoja de cálculo

Un libro de trabajo nuevo te brinda una hoja en blanco. La primera hoja de cálculo (índice 0) es donde insertaremos el Smart Marker.

```java
// Step 3: Create a new workbook and get the first worksheet
Workbook workbook = new Workbook();               // creates an empty XLSX workbook
Worksheet worksheet = workbook.getWorksheets().get(0);
```

*Por qué este paso es importante:* Aspose.Cells trabaja con un objeto `Workbook` que puede guardarse posteriormente como archivo XLSX. Acceder a la primera `Worksheet` nos permite colocar el marcador en una dirección de celda conocida.

## Paso 4: Insertar un Smart Marker que indique a Aspose.Cells cómo tratar el JSON

Los Smart Markers son marcadores de posición que Aspose.Cells reemplaza con datos de una fuente. El marcador `&=JSONData.ArrayAsSingle` indica a la biblioteca que trate toda la matriz JSON como un único valor de celda.

```java
// Step 4: Insert a smart‑marker that tells Aspose.Cells to treat the JSON array as a single cell
worksheet.getCells().putValue(0, 0, "&=JSONData.ArrayAsSingle");
```

*Por qué este paso es importante:* Usar `ArrayAsSingle` evita el comportamiento predeterminado de expandir cada elemento de la matriz en filas separadas. Esto es útil cuando deseas que el texto JSON aparezca literalmente en una celda, o cuando planeas dividirlo más tarde con fórmulas.

## Paso 5: Configurar el SmartMarkerProcessor con la fuente de datos JSON

Ahora enlaza la cadena JSON con el nombre lógico `JSONData`. El procesador reemplazará el marcador con los datos reales.

```java
// Step 5: Configure the SmartMarkerProcessor with the JSON data source
SmartMarkerProcessor processor = new SmartMarkerProcessor(workbook);
processor.setDataSource("JSONData", jsonData);
processor.process();   // expands the marker and writes JSON into the worksheet
```

*Por qué este paso es importante:* `setDataSource` vincula el nombre usado en el marcador (`JSONData`) con la carga útil JSON real. `process()` realiza el trabajo pesado: analiza el JSON, aplica la lógica del marcador y escribe el resultado en la hoja de cálculo.

## Paso 6: Guardar el libro de trabajo resultante como archivo XLSX

Finalmente, escribe el libro de trabajo en disco. La constante `SaveFormat.XLSX` garantiza el formato correcto de Office Open XML.

```java
// Step 6: Save the resulting workbook
String outputPath = "JsonSingleCell.xlsx";   // adjust the path as needed
workbook.save(outputPath, SaveFormat.XLSX);
System.out.println("Workbook saved to " + outputPath);
```

*Por qué este paso es importante:* Guardar el archivo completa el flujo de trabajo de **generar XLSX a partir de JSON**. El archivo generado puede abrirse en Excel, LibreOffice o cualquier otro programa de hojas de cálculo que admita XLSX.

### Código fuente completo

Juntando todas las piezas, aquí tienes el programa completo y ejecutable que **crea un libro de trabajo a partir de JSON**, **puebla Excel desde JSON**, y **guarda el libro de trabajo como XLSX**.

```java
package com.example.exceljson;

import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;
import com.aspose.cells.SmartMarkerProcessor;
import com.aspose.cells.SaveFormat;

public class JsonToExcelDemo {
    public static void main(String[] args) throws Exception {
        // 1. JSON source – replace with your own data if needed
        String jsonData = "[{\"Name\":\"John\",\"Age\":30},{\"Name\":\"Anna\",\"Age\":25}]";

        // 2. Create a fresh workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // 3. Place a smart‑marker that treats the JSON array as a single cell
        worksheet.getCells().putValue(0, 0, "&=JSONData.ArrayAsSingle");

        // 4. Bind the JSON string to the marker name and process it
        SmartMarkerProcessor processor = new SmartMarkerProcessor(workbook);
        processor.setDataSource("JSONData", jsonData);
        processor.process();

        // 5. Save the workbook as an XLSX file
        String outputPath = "JsonSingleCell.xlsx";
        workbook.save(outputPath, SaveFormat.XLSX);
        System.out.println("Workbook saved to " + outputPath);
    }
}
```

### Resultado esperado

Cuando abras `JsonSingleCell.xlsx` verás la matriz JSON mostrada en la celda **A1** exactamente como la cadena original:

```
[{"Name":"John","Age":30},{"Name":"Anna","Age":25}]
```

Si prefieres cada objeto en una fila separada, reemplaza el marcador con `&=JSONData` (sin `.ArrayAsSingle`). El procesador entonces expandirá la matriz en filas individuales, demostrando una técnica diferente de **poblar Excel desde JSON**.

## Variaciones comunes y casos límite

| Situación | Ajuste |
|-----------|------------|
| **Gran carga JSON ( > 10 MB )** | Aumenta el tamaño del heap de la JVM (`-Xmx2g`) y considera transmitir el JSON para evitar `OutOfMemoryError`. |
| **Objetos anidados** | Utiliza marcadores jerárquicos como `&=JSONData.Name` y `&=JSONData.Age` dentro de una tabla para mapear cada propiedad a una columna. |
| **Archivo JSON en lugar de una cadena** | Lee el archivo en una `String` con `java.nio.file.Files.readString(Path.of("data.json"))` y pásalo a `setDataSource`. |
| **Necesidad de mantener el formato JSON original** | Mantén el sufijo `.ArrayAsSingle`, o envuelve el JSON en CDATA si planeas usar fórmulas de Excel que analicen JSON más adelante. |
| **Múltiples hojas de cálculo** | Crea hojas de cálculo adicionales (`workbook.getWorksheets().add("Sheet2")`) y repite la inserción del marcador en cada hoja. |

> **Advertencia:** Los Smart Markers distinguen mayúsculas y minúsculas. Asegúrate de que el nombre lógico (`JSONData`) coincida exactamente entre el marcador y `setDataSource`.

## Probando la solución

1. Compila el programa:

   ```bash
   javac -cp ".:aspose-cells-23.10.jar" com/example/exceljson/JsonToExcelDemo.java
   ```

2. Ejecuta el programa:

   ```bash
   java -cp ".:aspose-cells-23.10.jar" com.example.exceljson.JsonToExcelDemo
   ```

3. Verifica que `JsonSingleCell.xlsx` aparezca en el directorio de trabajo y se abra sin errores.

## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que se basan en las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y funcionales con explicaciones paso a paso para ayudarte a dominar características adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Crear libro de Excel a partir de JSON – Guía completa de Aspose.Cells](/cells/english/net/data-loading-and-parsing/create-excel-workbook-from-json-complete-aspose-cells-guide/)
- [Crear libro de Excel C# – Insertar JSON y Guardar como XLSX](/cells/english/net/excel-data-import-export/create-excel-workbook-c-insert-json-and-save-as-xlsx/)
- [Guardar libro de Excel desde JSON – Guía completa](/cells/english/net/templates-reporting/save-excel-workbook-from-json-complete-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}