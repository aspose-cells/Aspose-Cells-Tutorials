---
category: general
date: 2026-07-16
description: Establezca un separador de celdas personalizado al exportar una tabla
  de Excel a TXT usando Aspose.Cells. Aprenda cómo exportar fórmulas de Excel a texto
  y guardar la hoja de cálculo como archivo txt.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- set custom cell separator
- export excel table to txt
- export excel formulas to text
- save worksheet as txt file
- export excel data as plain text
language: es
lastmod: 2026-07-16
og_description: Establecer un separador de celdas personalizado en Aspose.Cells le
  permite exportar la tabla de Excel a TXT con formato exacto. Exporte fórmulas de
  Excel a texto y guarde la hoja de cálculo como archivo txt fácilmente.
og_image_alt: Screenshot showing set custom cell separator option in Aspose.Cells
  export settings
og_title: Establecer separador de celda personalizado – Exportar tabla de Excel a
  TXT
schemas:
- author: Aspose
  dateModified: '2026-07-16'
  description: Set custom cell separator when exporting Excel table to TXT using Aspose.Cells.
    Learn how to export Excel formulas to text and save worksheet as txt file.
  headline: Set Custom Cell Separator – Export Excel Table to TXT
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel Export
title: Establecer separador de celdas personalizado – Exportar tabla de Excel a TXT
url: /es/java/excel-import-export/set-custom-cell-separator-export-excel-table-to-txt/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Establecer Separador de Celda Personalizado – Exportar Tabla de Excel a TXT

Establecer un separador de celda personalizado es la salsa secreta que necesitas cuando quieres obtener un volcado de texto ordenado desde una hoja de Excel. ¿Alguna vez te has preguntado cómo **exportar tabla de excel a txt** sin terminar con un desastre de comas y saltos de línea? En este tutorial recorreremos todo el proceso usando Aspose.Cells para Java, desde cargar un libro de trabajo hasta **guardar hoja de cálculo como archivo txt** con el delimitador que elijas.

## Lo que aprenderás

- Cómo **establecer separador de celda personalizado** para exportaciones de texto.  
- Los pasos exactos para **exportar fórmulas de excel a texto** de modo que los valores evaluados viajen contigo.  
- Formas de **exportar datos de excel como texto plano** manteniendo el diseño.  
- Un ejemplo de código completo, listo para ejecutar, que puedes copiar y pegar en tu proyecto.

Al final de esta guía podrás tomar cualquier libro de Excel, elegir una barra vertical (`|`), una tabulación (`\t`) o cualquier carácter que prefieras, y producir un archivo de texto delimitado limpio que los sistemas posteriores adorarán.

### Requisitos previos

- Java 8 o superior instalado.  
- Maven (o cualquier herramienta de compilación) para obtener la biblioteca Aspose.Cells para Java.  
- Un libro de muestra (`TableDemo.xlsx`) que contenga una tabla con fórmulas.

Si ya tienes todo eso, vamos al grano—sin rodeos, solo pasos prácticos.

## Paso 1: Añadir Aspose.Cells a tu proyecto

Antes de poder **establecer separador de celda personalizado**, necesitas el JAR de Aspose.Cells en el classpath. La forma más sencilla es mediante Maven:

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version> <!-- Check Maven Central for the latest version -->
</dependency>
```

Si prefieres Gradle, sustituye el XML por el equivalente `implementation 'com.aspose:aspose-cells:24.10'`. Una vez resuelta la dependencia, estarás listo para escribir código Java que interactúe con archivos Excel.

## Paso 2: Cargar el libro de trabajo – Preparando la exportación de tabla de Excel a TXT

La primera línea de código real siempre es la misma: abrir el libro que contiene la tabla que deseas exportar.

```java
import com.aspose.cells.*;

public class ExportTableWithOptions {
    public static void main(String[] args) throws Exception {
        // Load the workbook containing the table
        Workbook workbook = new Workbook("YOUR_DIRECTORY/TableDemo.xlsx");
        Worksheet worksheet = workbook.getWorksheets().get(0);
```

Aquí obtenemos la primera hoja (`get(0)`). Si tus datos están en otra hoja, simplemente cambia el índice o usa `get("SheetName")`. Esta parte es esencial para **exportar tabla de excel a txt** porque el exportador funciona a nivel de hoja de cálculo.

## Paso 3: Establecer separador de celda personalizado – El núcleo de la exportación

Ahora llega la estrella del espectáculo: configurar `ExportTableOptions`. Este objeto te permite decidir exactamente cómo aparecerá cada celda en el archivo de texto final.

```java
        // Define how the table should be exported
        ExportTableOptions exportTableOptions = new ExportTableOptions();

        // 1️⃣ Export cell contents as plain strings (no rich formatting)
        exportTableOptions.setExportAsString(true);

        // 2️⃣ Include the evaluated formula result, not the formula itself
        exportTableOptions.setFormulaValueInCell(true);

        // 3️⃣ Set the custom separator – this is where we set custom cell separator
        exportTableOptions.setCellValueSeparator("|"); // you can use any char you like
```

¿Por qué **establecemos separador de celda personalizado**? Porque el separador predeterminado es una tabulación, lo que puede entrar en conflicto con datos que ya contienen tabs. Al elegir una barra vertical (`|`) o un punto y coma, garantizas que cada columna permanezca distinta cuando un analizador posterior lea el archivo.

### Exportar fórmulas de Excel a texto

La línea `setFormulaValueInCell(true)` indica a Aspose.Cells que escriba las **exportar fórmulas de excel a texto** como el *resultado* de la fórmula, no como la cadena de la fórmula. Si omites esto, una celda que contiene `=SUM(A1:A5)` aparecería como `=SUM(A1:A5)` en el TXT, lo cual rara vez es lo que deseas.

## Paso 4: Adjuntar opciones de exportación a las opciones de guardado TXT

Ahora vinculamos esas opciones de tabla a la configuración general de exportación TXT.

```java
        // Attach the table export options to TXT save options
        TxtSaveOptions txtSaveOptions = new TxtSaveOptions();
        txtSaveOptions.setExportTableOptions(exportTableOptions);
```

`TxtSaveOptions` es el objeto paraguas que controla cómo se escribe toda la hoja. Al conectar `exportTableOptions` a él, aseguras que cada tabla en la hoja respete la regla de **establecer separador de celda personalizado**.

## Paso 5: Guardar la hoja como archivo TXT – Finalizando la exportación

Finalmente, escribimos el archivo en disco.

```java
        // Save the worksheet as a TXT file using the configured options
        workbook.save("YOUR_DIRECTORY/TableExported.txt", txtSaveOptions);
    }
}
```

Al ejecutar este programa se crea `TableExported.txt`. Cada fila de la tabla original de Excel aparecerá ahora como una línea de valores separados por barras verticales, por ejemplo:

```
Name|Quantity|Price|Total
Apple|10|0.50|5.00
Banana|5|0.30|1.50
```

Observa cómo la fórmula en la columna **Total** se evaluó antes de ser escrita—gracias a `setFormulaValueInCell(true)`. Esa es la esencia de **exportar datos de excel como texto plano** mientras se conservan los resultados calculados.

## Paso 6: Verificar la salida – ¿Se ve bien?

Abre el `TableExported.txt` generado en cualquier editor de texto. Deberías ver:

- Una línea por cada fila de Excel.  
- Columnas separadas por el carácter de barra vertical que configuraste con `setCellValueSeparator`.  
- No hay comas o tabs inesperados, a menos que formaran parte de los valores originales de las celdas.  
- Resultados de fórmulas, no las propias fórmulas.

Si detectas caracteres inesperados, revisa el separador que elegiste. Algunos caracteres (como la barra vertical) son seguros para la mayoría de los analizadores estilo CSV, pero si tus datos ya contienen barras verticales, considera usar otro delimitador como `~` o una tabulación (`\t`).

## Consejos, casos límite y buenas prácticas – Exportar datos de Excel como texto plano

| Situación | Qué hacer |
|-----------|-----------|
| **Los datos ya contienen el separador que elegiste** | Cambia a un carácter menos común (`^`, `~` o caracteres Unicode no imprimibles). |
| **Necesitas codificación UTF‑8** |  |

## ¿Qué deberías aprender a continuación?

Los tutoriales siguientes cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y funcionales con explicaciones paso a paso para ayudarte a dominar características adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Guardar Excel como Archivo de Texto con Separador Personalizado usando Aspose.Cells](/cells/english/net/workbook-operations/save-excel-text-custom-separator-aspose-cells-net/)
- [Guardar Excel como Archivo de Texto con Separador Personalizado usando Aspose.Cells](/cells/german/net/workbook-operations/save-excel-text-custom-separator-aspose-cells-net/)
- [Guardar Excel como Archivo de Texto con Separador Personalizado usando Aspose.Cells](/cells/french/net/workbook-operations/save-excel-text-custom-separator-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}