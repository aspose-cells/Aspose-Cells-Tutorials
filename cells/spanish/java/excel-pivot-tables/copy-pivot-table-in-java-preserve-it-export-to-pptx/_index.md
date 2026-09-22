---
category: general
date: 2026-03-01
description: 'Copiar tabla dinámica en Java manteniendo la pivote, luego exportar
  Excel a PPTX, desactivar el AutoFiltro de Excel y usar Smart Marker para matrices
  JSON: guía completa paso a paso.'
draft: false
keywords:
- copy pivot table
- preserve pivot table
- use smart marker
- disable excel autofilter
- export excel to pptx
language: es
og_description: 'Copiar tabla dinámica en Java, preservar la definición de la tabla
  dinámica, exportar a PPTX, desactivar AutoFilter y usar Smart Marker: guía completa
  para desarrolladores.'
og_title: Copiar tabla dinámica en Java – Preservarla, exportarla a PPTX
tags:
- Aspose.Cells
- Java
- Excel Automation
title: Copiar tabla dinámica en Java – Preservarla, exportar a PPTX
url: /es/java/excel-pivot-tables/copy-pivot-table-in-java-preserve-it-export-to-pptx/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Copiar tabla dinámica en Java – Preservarla, Exportar a PPTX

¿Alguna vez necesitaste **copy pivot table** de un libro de trabajo a otro sin perder la definición subyacente de la tabla dinámica? No eres el único rascándote la cabeza por esto. En muchos proyectos del mundo real te encontrarás moviendo datos, y lo último que deseas es una tabla dinámica rota que genere errores en tiempo de ejecución.  

En este tutorial recorreremos una solución completa que no solo **copy pivot table** sino que también te muestra cómo **preserve pivot table** al copiar, **export Excel to PPTX**, **disable Excel AutoFilter**, y **use smart marker** para insertar un array JSON en una sola celda. Al final tendrás un único programa Java ejecutable que cubre los cuatro escenarios.

## Requisitos previos

- Java 8 o superior (el código también funciona con Java 11)  
- Biblioteca Aspose.Cells for Java (versión 23.9 o posterior) – puedes obtenerla de Maven Central  
- Familiaridad básica con conceptos de Excel como pivot tables, tables y text boxes  

Si te falta el JAR de Aspose.Cells, agrega esto a tu `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.9</version>
</dependency>
```

Ahora, vamos a sumergirnos.

## Paso 1: Copiar tabla dinámica – Preservando la definición de la tabla dinámica

Cuando simplemente copias el rango de celdas que contiene una tabla dinámica, los metadatos de la tabla a menudo quedan atrás. Aspose.Cells nos ofrece una forma práctica de mantener la definición intacta usando `copyRange` con una instancia de `CopyOptions`.

```java
import com.aspose.cells.*;

public class PivotCopyDemo {

    public static void main(String[] args) throws Exception {
        // 1️⃣ Load the source workbook that contains the pivot table
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/src.xlsx");
        Worksheet sourceSheet = sourceWorkbook.getWorksheets().get(0);

        // 2️⃣ Define the range that includes the pivot (A1:G20 is just an example)
        Range pivotRange = sourceSheet.getCells().createRange("A1:G20");

        // 3️⃣ Prepare the destination workbook
        Workbook destWorkbook = new Workbook();
        Worksheet destSheet = destWorkbook.getWorksheets().get(0);

        // 4️⃣ Copy the range – the pivot definition travels with it
        destSheet.getCells().copyRange(pivotRange,
                new CellArea(0, 0, 19, 6), // destination area (rows 0‑19, cols 0‑6)
                new CopyOptions());

        // 5️⃣ Save the result
        destWorkbook.save("YOUR_DIRECTORY/dest.xlsx");
    }
}
```

**Por qué funciona:** `CopyOptions` indica a Aspose.Cells que copie todo, incluyendo la caché de la tabla dinámica y la configuración de campos. Sin ella, terminarías con valores simples y perderías la capacidad de actualizar la tabla dinámica.

**Caso límite:** Si tu tabla dinámica de origen abarca más que el rango codificado `A1:G20`, ajusta el rango en consecuencia o usa `sourceSheet.getPivotTables().get(0).getDataRange()` para obtenerlo dinámicamente.

![Ejemplo de copiar tabla dinámica](image.png "Copiar tabla dinámica en Java")

*Texto alternativo de la imagen: diagrama de copiar tabla dinámica en Java*

## Paso 2: Exportar una hoja de cálculo con un TextBox editable a PPTX

A menudo necesitas convertir una hoja de Excel en una diapositiva de PowerPoint—piensa en paneles semanales que deben presentarse. Aspose.Cells puede guardar directamente una hoja de cálculo como un archivo PPTX mientras preserva formas como los text boxes.

```java
import com.aspose.cells.*;

public class ExportToPptxDemo {

    public static void main(String[] args) throws Exception {
        // Load workbook that contains a TextBox shape
        Workbook wb = new Workbook("YOUR_DIRECTORY/textbox.xlsx");

        // Export the first worksheet to PPTX
        wb.save("YOUR_DIRECTORY/output.pptx", SaveFormat.PPTX);

        System.out.println("Worksheet exported to PPTX successfully.");
    }
}
```

**Qué está sucediendo:** El método `save` con `SaveFormat.PPTX` convierte toda la hoja, incluido cualquier TextBox editable, en una diapositiva de PowerPoint. El texto dentro del cuadro permanece editable al abrir el PPTX en PowerPoint.

**Consejo:** Si tienes varias hojas y solo deseas una específica, llama a `wb.getWorksheets().removeAt(index)` para las demás antes de guardar.

## Paso 3: Desactivar AutoFilter de Excel en una tabla

AutoFilter es útil para los usuarios finales, pero a veces necesitas desactivarlo programáticamente—quizás antes de exportar datos o al generar un informe limpio. Aquí se muestra cómo **disable excel autofilter** en una tabla de Excel.

```java
import com.aspose.cells.*;

public class DisableAutoFilterDemo {

    public static void main(String[] args) throws Exception {
        Workbook wb = new Workbook("YOUR_DIRECTORY/textbox.xlsx");
        Worksheet sheet = wb.getWorksheets().get(0);

        // Assume the first table in the sheet is the target
        Table table = sheet.getTables().get(0);

        // Turn off the AutoFilter arrows
        table.setShowAutoFilter(false);

        // Save the modified workbook
        wb.save("YOUR_DIRECTORY/noFilter.xlsx");
        System.out.println("AutoFilter disabled and workbook saved.");
    }
}
```

**Por qué podrías necesitar esto:** Exportar a formatos que no admiten AutoFilter (como CSV o PDF) puede hacer que aparezcan íconos de filtro sobrantes. Desactivarlo garantiza una salida limpia.

**Trampa común:** Si la hoja no tiene tablas, `getTables().get(0)` lanzará una `IndexOutOfBoundsException`. Siempre verifica `sheet.getTables().size()` primero en el código de producción.

## Paso 4: Usar Smart Marker – Insertar un array JSON como valor de una sola celda

Smart Marker es el motor de plantillas de Aspose. Un truco útil es tratar un array JSON completo como un valor de una sola celda, lo cual es perfecto para registrar o pasar datos estructurados aguas abajo. Vamos a **use smart marker** para lograr esto.

```java
import com.aspose.cells.*;

public class SmartMarkerDemo {

    public static void main(String[] args) throws Exception {
        Workbook wb = new Workbook("YOUR_DIRECTORY/textbox.xlsx");

        // Initialise the SmartMarker processor with the workbook
        SmartMarkerProcessor processor = new SmartMarkerProcessor(wb);

        // JSON array we want to embed
        String jsonArray = "[{\"Name\":\"John\",\"Age\":30},{\"Name\":\"Anna\",\"Age\":28}]";

        // Configure the processor to treat arrays as a single cell
        processor.setOptions(SmartMarkerOptions.ArrayAsSingle);

        // Apply the marker – assume cell A1 contains the marker ${json}
        processor.apply(jsonArray);

        // Save the result
        wb.save("YOUR_DIRECTORY/smartMarkerResult.xlsx");
        System.out.println("JSON array inserted via Smart Marker.");
    }
}
```

**Cómo funciona:** El marcador `${json}` en el libro de trabajo se reemplaza por la cadena JSON completa porque configuramos `ArrayAsSingle`. Sin esta opción, Aspose intentaría expandir cada elemento del array en filas separadas.

**Variación:** Si necesitas que el array se divida en filas, simplemente omite `ArrayAsSingle` y deja que Smart Marker maneje la expansión automáticamente.

## Ejemplo completo en funcionamiento – Todos los pasos combinados

A continuación se muestra una única clase Java que encadena todas las operaciones que hemos cubierto. Ejecútala como un método `main` regular; solo ajusta las rutas de archivo para que coincidan con tu entorno.

```java
import com.aspose.cells.*;

public class CompleteExcelAutomation {

    public static void main(String[] args) throws Exception {
        // ----------- Step 1: Copy Pivot Table -----------
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/src.xlsx");
        Worksheet srcSheet = srcWb.getWorksheets

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}