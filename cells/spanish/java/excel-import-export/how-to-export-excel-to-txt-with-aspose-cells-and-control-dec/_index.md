---
category: general
date: 2026-08-20
description: Aprende a exportar Excel a TXT limitando los decimales, conservando los
  dígitos significativos y guardando el libro de trabajo como TXT usando Java.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel to txt
- limit decimal places
- keep significant digits
- save workbook as txt
language: es
lastmod: 2026-08-20
og_description: Exportar Excel a TXT con Aspose.Cells. Esta guía muestra cómo limitar
  los decimales, mantener los dígitos significativos y guardar el libro de trabajo
  como TXT en Java.
og_image_alt: Result of export excel to txt showing limited decimal places and kept
  significant digits
og_title: Exportar Excel a TXT en Java – controlar los decimales y los dígitos significativos
schemas:
- author: Aspose
  dateModified: '2026-08-20'
  description: Learn to export Excel to TXT while limiting decimal places, keeping
    significant digits, and saving workbook as TXT using Java.
  headline: How to export Excel to TXT with Aspose.Cells and control decimal precision
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel
- Text export
title: Cómo exportar Excel a TXT con Aspose.Cells y controlar la precisión decimal
url: /es/java/excel-import-export/how-to-export-excel-to-txt-with-aspose-cells-and-control-dec/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo exportar Excel a TXT con Aspose.Cells y controlar la precisión decimal

Si necesita **exportar Excel a TXT** y garantizar que la salida respete un número específico de decimales, esta guía le ofrece una solución completa. Verá cómo limitar los decimales, conservar los dígitos significativos y **guardar el libro de trabajo como TXT** usando la biblioteca Aspose.Cells para Java.

El tutorial recorre la creación de un libro de trabajo, la inserción de un valor de alta precisión, la configuración de las opciones de guardado TXT y la escritura del archivo en disco. Al final podrá generar un archivo de texto que contenga exactamente la precisión que necesita, sin procesamiento manual posterior.

## Lo que necesitará

- Java 17 (o cualquier JDK compatible)
- Aspose.Cells for Java 23.10 o más reciente
- Un IDE o herramienta de compilación (Maven/Gradle) para gestionar dependencias
- Permiso de escritura en el directorio de salida

## Paso 1: Crear un libro de trabajo y acceder a la primera hoja de cálculo

Crear un libro de trabajo es el primer paso cuando desea **exportar Excel a TXT**. La clase `Workbook` representa todo el archivo Excel, y `Worksheet` le brinda acceso a las celdas.

```java
import com.aspose.cells.*;

public class ExportExcelToTxtDemo {
    public static void main(String[] args) throws Exception {
        // Initialize a new workbook
        Workbook workbook = new Workbook();

        // Get the first worksheet (index 0)
        Worksheet sheet = workbook.getWorksheets().get(0);
```

*Por qué es importante*: El objeto workbook contiene todos los datos, estilos y metadatos. Comenzar con un libro de trabajo nuevo garantiza que ningún formato oculto interfiera con la exportación a texto.

## Paso 2: Añadir un valor numérico y limitar los decimales

Inserte un número que tenga muchos decimales para poder demostrar cómo **limitar los decimales** durante la exportación.

```java
        // Put a high‑precision number into cell A1
        sheet.getCells().putValue("A1", 0.000123456789);
```

*Por qué es importante*: Excel almacena la precisión completa, pero cuando exporte más adelante, puede que desee truncar o redondear el valor. La configuración `limit decimal places` manejará esto automáticamente.

## Paso 3: Configurar las opciones de guardado TXT para conservar los dígitos significativos

Aspose.Cells proporciona `TxtSaveOptions`. Configurar `significantDigits` indica al exportador que conserve solo el número necesario de dígitos significativos, ignorando los ceros iniciales.

```java
        // Configure TXT export options
        TxtSaveOptions txtOptions = new TxtSaveOptions();

        // Keep exactly 5 significant digits (e.g., 0.00012346)
        txtOptions.setSignificantDigits(5);
```

*Por qué es importante*: La opción **keep significant digits** garantiza que el archivo de salida contenga una cantidad predecible de precisión, lo cual es esencial para los sistemas posteriores que esperan un formato numérico de ancho fijo.

## Paso 4: Guardar el libro de trabajo como TXT

Finalmente, escriba el libro de trabajo en un archivo de texto. El método `save` respeta las opciones que configuró, por lo que el archivo resultante contendrá la representación decimal limitada.

```java
        // Define the output path (replace with your own directory)
        String outputPath = "output/SignificantDigits.txt";

        // Export the workbook to TXT using the configured options
        workbook.save(outputPath, txtOptions);

        System.out.println("Export completed: " + outputPath);
    }
}
```

*Por qué es importante*: Usar **save workbook as txt** con el `TxtSaveOptions` preparado garantiza que el archivo exportado cumpla con las restricciones de precisión que estableció en el paso anterior.

### Contenido esperado de `SignificantDigits.txt`

```
0.00012346
```

El valor muestra cinco dígitos significativos (`12346`) después del redondeo, y los ceros iniciales se conservan según el formato TXT.

## Variaciones y casos límite

| Escenario | Ajuste |
|----------|------------|
| **Different number of significant digits** | Call `txtOptions.setSignificantDigits(n)` where `n` is 1‑15. |
| **Exporting a range instead of the whole sheet** | Use `txtOptions.setExportRange("A1:B10")` before saving. |
| **Preserving column separators** | Set `txtOptions.setSeparator('\t')` for tab‑delimited output. |
| **Large worksheets** | Increase `txtOptions.setMemorySetting(MemorySetting.MEMORY_PREFERENCES)` to avoid `OutOfMemoryError`. |

## Errores comunes y consejos profesionales

- **No confunda los dígitos significativos con los decimales**. Los ceros iniciales no se cuentan como significativos; use `setSignificantDigits` para precisión significativa y `setDecimalPlaces` si necesita un número fijo de dígitos después del punto decimal.
- **Siempre especifique una ruta de salida absoluta** al ejecutar desde un IDE para evitar errores de permisos.
- **Valide el archivo generado** con una llamada simple `java.nio.file.Files.readAllLines(Paths.get(outputPath))` para asegurarse de que el contenido coincida con lo esperado antes de enviarlo a procesos posteriores.

## Código fuente completo de referencia

```java
import com.aspose.cells.*;

public class ExportExcelToTxtDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.getWorksheets().get(0);

        // Step 2: Insert a high‑precision number (will be limited later)
        sheet.getCells().putValue("A1", 0.000123456789);

        // Step 3: Set TXT options – keep 5 significant digits
        TxtSaveOptions txtOptions = new TxtSaveOptions();
        txtOptions.setSignificantDigits(5);   // keep significant digits

        // Step 4: Save the workbook as TXT
        String outputPath = "output/SignificantDigits.txt";
        workbook.save(outputPath, txtOptions);

        System.out.println("Export completed: " + outputPath);
    }
}
```

Ejecutar el programa genera `SignificantDigits.txt` que contiene la única línea `0.00012346`, demostrando que el proceso de **export excel to txt** respeta tanto los requisitos de **limit decimal places** como de **keep significant digits**.

## Conclusión

Ahora sabe cómo **exportar Excel a TXT** usando Aspose.Cells para Java mientras controla la precisión numérica. Configurando `TxtSaveOptions` puede **limit decimal places**, **keep significant digits**, y de forma fiable **save workbook as txt** sin procesamiento posterior adicional.

A continuación, podría explorar:

- Exportar varias hojas a archivos TXT separados (`save workbook as txt` por hoja)
- Usar `setSeparator` para crear salida compatible con CSV
- Automatizar conversiones por lotes para grandes conjuntos de datos

Siéntase libre de experimentar con diferentes cantidades de dígitos y separadores para ajustarse a las necesidades exactas de su proyecto. ¡Feliz codificación!

## ¿Qué debería aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y funcionales con explicaciones paso a paso para ayudarle a dominar características adicionales de la API y explorar enfoques de implementación alternativos en sus propios proyectos.

- [Cómo crear y exportar Excel a HTML usando Aspose.Cells Java | Guía de operaciones de libro de trabajo](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)
- [Guardar Excel como texto – Guía completa en C# para exportar Excel a TXT](/cells/english/net/converting-excel-files-to-other-formats/save-excel-as-text-complete-c-guide-to-export-excel-to-txt/)
- [Exportar libro de Excel como imagen usando Aspose.Cells para Java&#58; Guía paso a paso](/cells/english/java/import-export/export-excel-workbook-as-image-using-aspose-cells-for-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}