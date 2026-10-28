---
category: general
date: 2026-08-17
description: Exportar Excel a TXT limitando los dígitos significativos – aprenda cómo
  establecer los dígitos y convertir Excel a texto en Java con un ejemplo completo
  de Aspose.Cells.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel to txt
- how to set digits
- convert excel to text
- how to limit decimals
- limit significant digits
language: es
lastmod: 2026-08-17
og_description: Exportar Excel a TXT limitando los dígitos significativos. Este tutorial
  muestra cómo establecer los dígitos y convertir Excel a texto usando Aspose.Cells
  para Java.
og_image_alt: Java code exporting Excel to TXT with 4 significant digits
og_title: Exportar Excel a TXT con dígitos significativos limitados – Guía de Java
schemas:
- author: Aspose
  dateModified: '2026-08-17'
  description: Export Excel to TXT while limiting significant digits – learn how to
    set digits and convert Excel to text in Java with a complete Aspose.Cells example.
  headline: How to export Excel to TXT with limited significant digits using Java
  type: TechArticle
- description: Export Excel to TXT while limiting significant digits – learn how to
    set digits and convert Excel to text in Java with a complete Aspose.Cells example.
  name: How to export Excel to TXT with limited significant digits using Java
  steps:
  - name: Prerequisites
    text: '- Java 17 or later (the code compiles with Java 8 as well). - Aspose.Cells
      for Java 25.10 or newer. Download the JAR from the [Aspose website](https://products.aspose.com/cells/java)
      and add it to your project’s classpath. - An IDE or a simple text editor and
      command‑line build tool (Maven/Gradle).'
  - name: How the setting differs from “limit decimals”
    text: '- **limit decimals** (`setDecimalPlaces`) trims digits *after* the decimal
      point, regardless of the integer part. - **significant digits** (`setSignificantDigits`)
      counts digits from the first non‑zero digit, which is useful when numbers vary
      in magnitude.'
  - name: Expected output
    text: '| Cell | Original value | Exported (4 significant digits) | |------|----------------|---------------------------------|
      | A1 | 123.456789 | 123.5 |'
  - name: Exporting a whole range
    text: 'If you want to export more than one cell, simply fill the range before
      saving:'
  - name: Handling locale‑specific decimal separators
    text: 'Aspose.Cells respects the system locale when writing text. To force a dot
      (`.`) as the decimal separator, set the `TxtSaveOptions` culture:'
  - name: Overwriting existing files
    text: 'The `save` method overwrites the target file by default. If you need to
      avoid accidental data loss, check for file existence first:'
  - name: Large workbooks and memory usage
    text: 'When exporting very large worksheets, consider streaming the output:'
  - name: Next steps
    text: "- Explore other `TxtSaveOptions` properties such as `setDelimiter('\t')`
      to customize column separators. - Combine the exporter with `CsvSaveOptions`
      if you need comma‑separated values instead of plain text. - Integrate the routine
      into a web service that accepts uploaded Excel files and returns tri"
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel export
- TXT conversion
title: Cómo exportar Excel a TXT con dígitos significativos limitados usando Java
url: /es/java/excel-import-export/how-to-export-excel-to-txt-with-limited-significant-digits-u/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Exportar Excel a TXT con dígitos significativos limitados usando Java

Si necesita **exportar Excel a TXT** mientras controla la cantidad de dígitos significativos, esta guía le proporciona una solución lista para ejecutar. Verá cómo establecer los dígitos, convertir Excel a texto y mantener la salida ordenada con un único cambio de configuración.

El ejemplo utiliza Aspose.Cells for Java 25.10, que introduce la opción `setSignificantDigits`. Al final del tutorial podrá generar un archivo TXT que contenga solo los dígitos que desea, sin código adicional de redondeo.

## Lo que logrará

- Crear un libro de trabajo programáticamente.
- Insertar un valor numérico en una celda.
- Configurar las opciones de guardado TXT para limitar los dígitos significativos.
- Guardar el libro de trabajo como un archivo de texto plano.
- Comprender cómo funciona la configuración `significantDigits` y cómo adaptarla a otros escenarios.

### Requisitos previos

- Java 17 o posterior (el código también se compila con Java 8).
- Aspose.Cells for Java 25.10 o más reciente. Descargue el JAR desde el [sitio web de Aspose](https://products.aspose.com/cells/java) y agréguelo al classpath de su proyecto.
- Un IDE o un editor de texto simple y una herramienta de compilación por línea de comandos (Maven/Gradle).

## Paso 1: Configurar el proyecto e importar Aspose.Cells

Cree un nuevo proyecto Java y agregue el JAR de Aspose.Cells a la ruta de compilación. Si usa Maven, añada la siguiente dependencia a `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.10</version>
    <classifier>jdk17</classifier>
</dependency>
```

> **Consejo profesional:** Use el clasificador `jdk17` para el runtime de Java más reciente; reduce el riesgo de advertencias de compatibilidad.

## Paso 2: Crear un libro de trabajo y escribir un valor

El libro de trabajo representa un archivo Excel en memoria. Puede agregar datos a cualquier celda usando el método `putValue`.

```java
import com.aspose.cells.*;

public class SignificantDigitsDemo {
    public static void main(String[] args) throws Exception {
        // Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // Put a numeric value into cell A1
        Cell cell = worksheet.getCells().get("A1");
        cell.putValue(123.456789);
```

El número `123.456789` será la fuente para nuestra exportación a TXT. Por defecto, Aspose.Cells escribiría todos los decimales, lo que a menudo produce archivos de texto ruidosos.

## Paso 3: Configurar las opciones de guardado TXT para limitar los dígitos significativos

Aspose.Cells proporciona `TxtSaveOptions` para un control fino sobre la salida de texto plano. El método `setSignificantDigits` indica al exportador cuántos dígitos conservar **en total**, no solo después del punto decimal.

```java
        // Configure TXT save options to keep only 4 significant digits
        TxtSaveOptions saveOptions = new TxtSaveOptions();
        saveOptions.setSignificantDigits(4); // new option in 25.10
```

Cuando `significantDigits` se establece en `4`, el exportador redondea el valor `123.456789` a `123.5`. Este comportamiento coincide con la definición matemática de cifras significativas: se conservan los primeros cuatro dígitos distintos de cero.

### Cómo difiere esta configuración de “limitar decimales”

- **limitar decimales** (`setDecimalPlaces`) recorta los dígitos *después* del punto decimal, sin importar la parte entera.
- **dígitos significativos** (`setSignificantDigits`) cuenta los dígitos a partir del primer dígito distinto de cero, lo que es útil cuando los números varían en magnitud.

Si necesita un número fijo de lugares decimales en su lugar, reemplace la línea anterior por:

```java
saveOptions.setDecimalPlaces(2); // keeps two digits after the decimal point
```

## Paso 4: Guardar el libro de trabajo como archivo TXT

Ahora escriba el libro de trabajo en disco usando las opciones configuradas.

```java
        // Save the workbook as a TXT file using the configured options
        workbook.save("significant_digits.txt", saveOptions);
    }
}
```

Ejecutar el programa crea `significant_digits.txt` en el directorio de trabajo. El archivo contiene una sola línea:

```
123.5
```

### Salida esperada

| Celda | Valor original | Exportado (4 dígitos significativos) |
|------|----------------|---------------------------------------|
| A1   | 123.456789     | 123.5                                 |

Si cambia `setSignificantDigits(4)` a `6`, la salida se convierte en `123.457`. Experimente con diferentes valores para ver cómo se adapta el redondeo.

## Paso 5: Variaciones comunes y casos límite

### Exportar un rango completo

Si desea exportar más de una celda, simplemente llene el rango antes de guardar:

```java
worksheet.getCells().get("B1").putValue(0.0012345);
worksheet.getCells().get("C1").putValue(98765.4321);
```

La misma configuración `significantDigits` se aplica a cada celda numérica, garantizando una precisión consistente en todo el archivo.

### Manejo de separadores decimales específicos de la configuración regional

Aspose.Cells respeta la configuración regional del sistema al escribir texto. Para forzar un punto (`.`) como separador decimal, establezca la cultura en `TxtSaveOptions`:

```java
saveOptions.setCultureInfo(java.util.Locale.US);
```

Esto es útil cuando la aplicación de destino espera un formato específico, como analizadores CSV que solo aceptan `.`.

### Sobrescribir archivos existentes

El método `save` sobrescribe el archivo de destino por defecto. Si necesita evitar la pérdida accidental de datos, verifique primero la existencia del archivo:

```java
java.io.File outFile = new java.io.File("significant_digits.txt");
if (outFile.exists()) {
    throw new IllegalStateException("File already exists. Choose a different name or delete the existing file.");
}
workbook.save(outFile.getPath(), saveOptions);
```

### Libros de trabajo grandes y uso de memoria

Al exportar hojas de cálculo muy grandes, considere transmitir la salida:

```java
saveOptions.setEnableMemorySaving(true);
```

## Ejemplo completo en funcionamiento

A continuación se muestra el programa completo que puede copiar, pegar y ejecutar de inmediato:

```java
import com.aspose.cells.*;

public class SignificantDigitsDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook and access the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // Step 2: Put numeric values into cells
        worksheet.getCells().get("A1").putValue(123.456789);
        worksheet.getCells().get("B1").putValue(0.0012345);
        worksheet.getCells().get("C1").putValue(98765.4321);

        // Step 3: Configure TXT save options
        TxtSaveOptions saveOptions = new TxtSaveOptions();
        saveOptions.setSignificantDigits(4);          // limit to 4 significant digits
        saveOptions.setCultureInfo(java.util.Locale.US); // enforce dot as decimal separator
        saveOptions.setEnableMemorySaving(true);      // optional for large files

        // Step 4: Save the workbook as a TXT file
        workbook.save("significant_digits.txt", saveOptions);
    }
}
```

Ejecutar este código produce `significant_digits.txt` con el siguiente contenido (columnas separadas por tabulaciones):

```
123.5	0.001235	98770
```

Cada número respeta la regla de **4 dígitos significativos**, demostrando que la configuración funciona en diferentes magnitudes.

## Conclusión

Ahora sabe cómo **exportar Excel a TXT** mientras controla la cantidad de dígitos significativos. Al usar `TxtSaveOptions.setSignificantDigits`, puede **establecer dígitos**, **limitar decimales** y **limitar dígitos significativos** en una única línea de código mantenible. El enfoque funciona tanto para celdas individuales, rangos completos y libros de trabajo grandes.

### Próximos pasos

- Explore otras propiedades de `TxtSaveOptions` como `setDelimiter('\t')` para personalizar los separadores de columnas.
- Combine el exportador con `CsvSaveOptions` si necesita valores separados por comas en lugar de texto plano.
- Integre la rutina en un servicio web que acepte archivos Excel cargados y devuelva una salida TXT recortada al instante.

Siéntase libre de experimentar con diferentes límites de dígitos y configuraciones regionales. Si encuentra un escenario donde las opciones integradas no satisfacen un requisito especial, siempre puede post‑procesar el archivo TXT generado con utilidades estándar de I/O de Java.

¡Feliz codificación!

## ¿Qué debería aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que se basan en las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos con explicaciones paso a paso para ayudarle a dominar funciones adicionales de la API y explorar enfoques de implementación alternativos en sus propios proyectos.

- [Cómo convertir texto a números en Excel usando Aspose.Cells for Java](/cells/english/java/cell-operations/convert-text-to-numbers-excel-aspose-cells-java/)
- [Cómo crear y exportar Excel a HTML usando Aspose.Cells Java | Guía de operaciones de libro de trabajo](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)
- [Cómo exportar propiedades personalizadas de Excel a PDF usando Aspose.Cells for Java](/cells/english/java/workbook-operations/export-excel-custom-properties-pdf-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}