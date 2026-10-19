---
category: general
date: 2026-08-14
description: Copiar rango entre libros de trabajo con Java usando Aspose.Cells. Aprende
  a copiar la tabla dinámica del libro, exportar una imagen a PowerPoint y eliminar
  el AutoFiltro de la tabla de Excel.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy range between workbooks
- copy pivot table workbook
- export picture to powerpoint
- copy excel range to new workbook
- remove autofilter from excel table
language: es
lastmod: 2026-08-14
og_description: Copiar rango entre libros de trabajo en Java. Esta guía muestra cómo
  copiar el libro de tabla dinámica, exportar una imagen a PowerPoint y eliminar AutoFilter
  de una tabla de Excel.
og_image_alt: Screenshot of Java code copying range between workbooks with Aspose.Cells
og_title: Copiar rango entre libros de trabajo en Java – tutorial completo de Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-08-14'
  description: Copy range between workbooks with Java using Aspose.Cells. Learn to
    copy pivot table workbook, export picture to PowerPoint and remove AutoFilter
    from Excel table.
  headline: Copy range between workbooks in Java – step‑by‑step guide
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel automation
- PowerPoint export
title: Copiar rango entre libros de trabajo en Java – guía paso a paso
url: /es/java/range-management/copy-range-between-workbooks-in-java-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Copiar rango entre libros de trabajo en Java – guía paso a paso

Si necesitas **copiar rango entre libros de trabajo** en Java, Aspose.Cells ofrece una API clara que maneja objetos complejos como tablas dinámicas y imágenes. Este tutorial muestra cómo **copiar el libro de la tabla dinámica**, **exportar una imagen a PowerPoint** y **eliminar AutoFilter de una tabla de Excel** manteniendo el código fácil de leer y mantener.

Aprenderás a:

* Cargar un libro de trabajo origen y definir el rango fuente.  
* Crear un libro de trabajo destino y copiar el rango de modo que la tabla dinámica permanezca intacta.  
* Exportar la primera imagen de la hoja como un objeto editable de PowerPoint.  
* Eliminar un AutoFilter de la primera tabla de Excel.  
* Cargar un libro de trabajo con `SmartMarkerOptions` para tratar arreglos JSON como un único valor de celda.

El ejemplo usa Aspose.Cells 23.10 para Java, pero los conceptos se aplican a versiones anteriores también.

---

## Requisitos previos

| Requisito | Por qué es importante |
|-----------|-----------------------|
| Java 17 o superior | Requerido por la última versión del runtime de Aspose.Cells. |
| Aspose.Cells para Java (artefacto Maven `com.aspose:aspose-cells`) | Proporciona las clases `Workbook`, `Worksheet`, `Range` y relacionadas usadas en el código. |
| Un archivo Excel origen (`src.xlsx`) que contenga una tabla dinámica, una imagen y una tabla con AutoFilter. | El tutorial manipula estos objetos para demostrar cada funcionalidad. |

Agrega la dependencia Maven a tu `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.10</version>
    <classifier>jdk17</classifier>
</dependency>
```

---

## Copiar rango entre libros de trabajo – cargar origen y destino

El primer paso es abrir el libro de trabajo origen, seleccionar el rango que contiene los datos que deseas copiar y crear un libro de trabajo destino vacío.

```java
import com.aspose.cells.*;

public class CopyRangeDemo {
    public static void main(String[] args) throws Exception {
        // Load the source workbook that holds the pivot table, picture, and table.
        Workbook sourceWb = new Workbook("YOUR_DIRECTORY/src.xlsx");
        Worksheet sourceWs = sourceWb.getWorksheets().get(0);

        // Define the range that includes the pivot table (A1:G20 in this example).
        Range sourceRange = sourceWs.getCells().createRange("A1:G20");

        // Create a new workbook that will receive the copied range.
        Workbook destWb = new Workbook();
        Worksheet destWs = destWb.getWorksheets().get(0);
        Range destRange = destWs.getCells().createRange("A1");
```

> **Por qué es importante:** Al usar `Range.copy`, Aspose.Cells copia no solo los valores de celda sin formato sino también la caché subyacente de la tabla dinámica, manteniendo la tabla funcional en el libro de trabajo destino.

---

## Copiar libro de tabla dinámica mientras se copia el rango

Ahora copia el rango definido del libro origen al libro destino. La tabla dinámica se conserva automáticamente porque el rango incluye la caché de la tabla dinámica.

```java
        // Copy the source range to the destination range.
        destRange.copy(sourceRange);

        // Save the intermediate workbook to verify that the pivot table was copied.
        destWb.save("YOUR_DIRECTORY/destination.xlsx");
```

> **Resultado:** Al abrir `destination.xlsx` se muestra el mismo diseño de tabla dinámica que en `src.xlsx`. No se necesita código adicional para reconstruir la caché de la tabla dinámica.

---

## Exportar imagen a PowerPoint

Aspose.Cells puede marcar una imagen para exportarla como un objeto editable de PowerPoint. El siguiente código selecciona la primera imagen en la hoja destino y establece la bandera de exportación.

```java
        // Retrieve the first picture on the destination sheet.
        Shape picture = destWs.getPictures().get(0);

        // Instruct Aspose.Cells to export this picture as a PowerPoint object.
        picture.getPictureFormat().setExportToPptx(true);

        // Optionally, save the workbook as PPTX to see the result.
        destWb.save("YOUR_DIRECTORY/destination.pptx");
```

> **Lo que ves:** Al abrir `destination.pptx` en PowerPoint la imagen aparece como una forma nativa que puedes editar, redimensionar o animar.

---

## Eliminar AutoFilter de la tabla de Excel

Si la hoja origen contiene una tabla con AutoFilter, es posible que desees eliminarlo después de copiar. El código a continuación accede a la primera tabla y quita su filtro.

```java
        // Access the first table on the destination sheet.
        Table table = destWs.getTables().get(0);

        // Remove the AutoFilter by assigning null.
        table.setAutoFilter(null);

        // Save the final workbook.
        destWb.save("YOUR_DIRECTORY/final_output.xlsx");
```

> **Efecto:** La tabla permanece en el libro de trabajo, pero desaparecen las flechas de filtro desplegables, ofreciéndote una vista de datos limpia.

---

## Cargar libro de trabajo con opciones SmartMarker – tratar arreglos JSON como una sola celda

Cuando generas un informe a partir de JSON, Aspose.Cells puede tratar todo un arreglo como un único valor de celda. Esto es útil para incrustar cadenas JSON en una plantilla sin expandirlas en múltiples celdas.

```java
        // Configure LoadOptions to enable SmartMarker array handling.
        LoadOptions loadOptions = new LoadOptions();
        SmartMarkerOptions smOptions = new SmartMarkerOptions();
        smOptions.setArrayAsSingle(true);
        loadOptions.setSmartMarkerOptions(smOptions);

        // Load a template workbook using the configured options.
        Workbook smartMarkerWb = new Workbook("YOUR_DIRECTORY/template.xlsx", loadOptions);

        // Continue processing (e.g., populate markers) as needed.
        // ...

        // Save the processed workbook.
        smartMarkerWb.save("YOUR_DIRECTORY/template_filled.xlsx");
    }
}
```

> **Por qué podrías usar esto:** Si tu carga JSON contiene un arreglo que debe aparecer como una cadena JSON en una sola celda, `setArrayAsSingle(true)` evita que Aspose.Cells expanda el arreglo en filas o columnas separadas.

---

![Copy range between workbooks in Java – Aspose.Cells code example](copy-range-workbooks.png)

*Texto alternativo de la imagen:* **Copiar rango entre libros de trabajo en Java – ejemplo de código Aspose.Cells** (coincide con la palabra clave principal).

---

## Resultado esperado

| Nombre del archivo          | Contenido |
|-----------------------------|-----------|
| `destination.xlsx`          | Rango copiado con tabla dinámica funcional. |
| `destination.pptx`          | Imagen exportada como una forma editable de PowerPoint. |
| `final_output.xlsx`         | Tabla sin flechas de AutoFilter. |
| `template_filled.xlsx`      | Arreglo JSON almacenado como un único valor de celda. |

Abre cada archivo en la aplicación correspondiente (Excel o PowerPoint) para verificar que las operaciones se hayan realizado correctamente.

---

## Conclusión

Ahora sabes cómo **copiar rango entre libros de trabajo** en Java usando Aspose.Cells, preservando una tabla dinámica, exportando una imagen a PowerPoint y eliminando un AutoFilter de una tabla de Excel. El mismo patrón puede ampliarse para copiar cualquier rango de Excel a un nuevo libro, manejar arreglos JSON con SmartMarker o encadenar transformaciones adicionales.

Próximos pasos que podrías explorar:

* **Copiar rango de Excel a un nuevo libro** con varias hojas de cálculo.  
* Usar **exportar imagen a PowerPoint** para extracción masiva de imágenes.  
* Aplicar **eliminar autofilter de tabla de excel** en pipelines de informes más extensos.  
* Combinar estas técnicas con Aspose.Slides para una automatización completa de Excel a PowerPoint.

Siéntete libre de experimentar con diferentes direcciones de rango, múltiples tablas dinámicas o formatos de imagen personalizados. La API de Aspose.Cells está diseñada para flexibilidad programática, por lo que puedes adaptar los patrones mostrados aquí a cualquier escenario empresarial de automatización de Excel.

## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y funcionales con explicaciones paso a paso para ayudarte a dominar características adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Copiar imágenes entre hojas en Excel usando Aspose.Cells para Java: Guía completa](/cells/english/java/images-shapes/copy-images-between-sheets-excel-aspose-cells-java/)
- [Copiar configuración de página entre hojas de cálculo en Excel usando Aspose.Cells Java](/cells/english/java/headers-footers/copy-page-setup-excel-aspose-cells-java/)
- [Copiar hojas de cálculo entre libros de trabajo en Excel](/cells/english/net/excel-copy-worksheet/excel-copy-worksheets-between-workbooks/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}