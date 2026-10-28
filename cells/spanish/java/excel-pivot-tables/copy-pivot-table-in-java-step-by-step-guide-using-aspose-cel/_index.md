---
category: general
date: 2026-08-04
description: Copiar tabla dinámica con Aspose.Cells para Java. Aprende cómo copiar
  un rango de Excel, duplicar una tabla dinámica y copiar una hoja de cálculo con
  tabla dinámica en solo unas pocas líneas.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy pivot table
- copy excel range
- copy range java
- duplicate pivot table
- copy worksheet with pivot
language: es
lastmod: 2026-08-04
og_description: Copiar tabla dinámica usando Aspose.Cells para Java. Este tutorial
  le guía a través de la copia de un rango de Excel, la duplicación de una tabla dinámica
  y la preservación de todos los datos en una nueva hoja de cálculo.
og_image_alt: Screenshot of a Java program that copies a pivot table to a new worksheet
og_title: Copiar tabla dinámica en Java – tutorial completo de Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-08-04'
  description: Copy pivot table with Aspose.Cells for Java. Learn how to copy excel
    range, duplicate pivot table, and copy worksheet with pivot in just a few lines.
  headline: Copy pivot table in Java – step‑by‑step guide using Aspose.Cells
  type: TechArticle
- description: Copy pivot table with Aspose.Cells for Java. Learn how to copy excel
    range, duplicate pivot table, and copy worksheet with pivot in just a few lines.
  name: Copy pivot table in Java – step‑by‑step guide using Aspose.Cells
  steps:
  - name: '`CopyWithPivot.xlsx` appears in `YOUR_DIRECTORY`.'
    text: '`CopyWithPivot.xlsx` appears in `YOUR_DIRECTORY`.'
  - name: Opening the file in Excel shows a new sheet named **CopySheet**.
    text: Opening the file in Excel shows a new sheet named **CopySheet**.
  - name: '**CopySheet** contains a fully functional pivot table identical to the
      original, ready to refresh.'
    text: '**CopySheet** contains a fully functional pivot table identical to the
      original, ready to refresh.'
  - name: All formatting, filters, and calculated fields are preserved.
    text: All formatting, filters, and calculated fields are preserved.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
- PivotTable
- Data copying
title: Copiar tabla dinámica en Java – guía paso a paso con Aspose.Cells
url: /es/java/excel-pivot-tables/copy-pivot-table-in-java-step-by-step-guide-using-aspose-cel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Copiar tabla dinámica en Java – guía paso a paso usando Aspose.Cells

Si necesitas **copiar una tabla dinámica** de una hoja de cálculo a otra en Java, esta guía te muestra exactamente cómo hacerlo con Aspose.Cells. Ya sea que estés generando informes programáticamente o construyendo una herramienta de migración de datos, verás un ejemplo completo y ejecutable que preserva la definición y los datos de la tabla dinámica.

Copiar una tabla dinámica es más que copiar un rango de celdas; la caché subyacente y la fuente de datos deben permanecer intactas. En este tutorial también cubrimos cómo **copiar rango de Excel**, cómo **duplicar tabla dinámica** entre hojas de cálculo y cómo **copiar hoja de cálculo con tabla dinámica** usando la misma API.

## Requisitos previos

Antes de comenzar, asegúrate de tener:

* Java Development Kit (JDK) 8 o posterior.
* Maven o Gradle para gestionar dependencias.
* Aspose.Cells for Java (la última versión, por ejemplo, 23.12). Añade la siguiente coordenada Maven a tu `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version>
</dependency>
```

* Un libro de trabajo fuente (`Source.xlsx`) que contiene una tabla dinámica en la primera hoja.

## Cómo copiar una tabla dinámica en Java con Aspose.Cells

La idea principal es copiar el *rango fuente* que envuelve la tabla dinámica y luego pegarlo en una nueva hoja de cálculo. Aspose.Cells copia automáticamente la caché de la tabla dinámica, por lo que la hoja resultante contiene una **tabla dinámica duplicada** totalmente funcional.

```java
import com.aspose.cells.*;

public class CopyPivotTableDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Load the workbook that contains the PivotTable
        Workbook workbook = new Workbook("YOUR_DIRECTORY/Source.xlsx");

        // Step 2: Define the source range (including the PivotTable) to be copied
        // The range must cover the entire pivot table area, e.g., A1:G20
        Range sourceRange = workbook.getWorksheets()
                                    .get(0)                 // first worksheet
                                    .getCells()
                                    .createRange("A1:G20");

        // Step 3: Add a new worksheet that will receive the copied range
        Worksheet destinationSheet = workbook.getWorksheets().add("CopySheet");

        // Step 4: Copy the source range to cell A1 of the new worksheet
        sourceRange.copy(destinationSheet.getCells().createRange("A1"));

        // Step 5: Save the workbook with the copied PivotTable intact
        workbook.save("YOUR_DIRECTORY/CopyWithPivot.xlsx");
    }
}
```

### Por qué funciona esto

* **La copia del rango incluye la caché de la tabla dinámica** – Aspose.Cells trata una tabla dinámica como un objeto especial incrustado en el rango de celdas. Cuando llamas a `Range.copy`, la biblioteca copia tanto las celdas visibles como la caché oculta que alimenta la tabla dinámica.
* **No se necesita recreación manual** – No tienes que reconstruir los campos de la tabla dinámica o la fuente de datos; la duplicada está lista para actualizarse al instante.
* **Funciona con cualquier versión de Excel** – El archivo generado sigue el estándar Office Open XML (XLSX), por lo que Excel 2007+ puede abrirlo sin advertencias.

## Copiar rango de Excel – reutilizando el mismo código para datos sin tabla dinámica

Si solo necesitas **copiar rango de Excel** sin una tabla dinámica, se aplica el mismo patrón. Simplemente ajusta la dirección del rango a la región que deseas duplicar.

```java
// Example: copy A1:D10 from Sheet1 to Sheet2
Range dataRange = workbook.getWorksheets()
                          .get(0)
                          .getCells()
                          .createRange("A1:D10");
Worksheet sheet2 = workbook.getWorksheets().add("DataCopy");
dataRange.copy(sheet2.getCells().createRange("A1"));
```

El método `copy` preserva fórmulas, formato y comentarios, convirtiéndolo en una solución universal para cualquier bloque de datos de Excel.

## Duplicar tabla dinámica en varias hojas de cálculo

A veces necesitas **duplicar tabla dinámica** varias veces—p. ej., una por departamento. Recorre las hojas de cálculo de destino y reutiliza la misma llamada `sourceRange.copy`:

```java
String[] departments = {"Sales", "Marketing", "Finance"};
for (String dept : departments) {
    Worksheet ws = workbook.getWorksheets().add(dept + "Pivot");
    sourceRange.copy(ws.getCells().createRange("A1"));
}
```

Cada hoja nueva contiene una tabla dinámica independiente que puede actualizarse por separado. La caché se duplica, por lo que los cambios en una hoja no afectarán a las demás.

## Copiar hoja de cálculo con tabla dinámica – preservando la configuración a nivel de hoja

Si deseas **copiar hoja de cálculo con tabla dinámica** manteniendo también la configuración de página, el ancho de columnas y los rangos nombrados, usa `Worksheet.copy` en lugar de copiar un rango manualmente. Este método clona toda la hoja, incluida la tabla dinámica.

```java
Worksheet original = workbook.getWorksheets().get(0);
Worksheet clone = workbook.getWorksheets().addCopy(original);
clone.setName("FullCopy");
workbook.save("YOUR_DIRECTORY/FullCopy.xlsx");
```

`addCopy` es útil cuando la hoja contiene gráficos, imágenes o estilos personalizados que deben viajar junto con la tabla dinámica.

## Errores comunes y cómo evitarlos

| Problema | Por qué ocurre | Solución |
|----------|----------------|----------|
| **Caché de tabla dinámica perdida después de copiar** | Usar `Cell.copy` en celdas individuales (en lugar de un rango) descarta la caché oculta. | Siempre copia el *rango completo* que envuelve la tabla dinámica, como se muestra en el Paso 2. |
| **Rango fuente demasiado pequeño** | El rango no incluye el área de datos de la tabla dinámica, por lo que la hoja nueva muestra solo valores estáticos. | Amplía la dirección (p. ej., `A1:G20`) para cubrir toda la tabla dinámica más cualquier segmentador o filtro. |
| **Incompatibilidad de versión del libro de destino** | Guardar como XLS (legado) elimina las funciones modernas de tabla dinámica. | Guarda como XLSX (predeterminado) o establece explícitamente `SaveFormat.XLSX`. |
| **Fuente de datos externa rota** | La tabla dinámica apunta a una fuente de datos fuera del libro; al copiar no se incrusta. | Usa `PivotTable.refreshData()` después de copiar, o incrusta los datos fuente en el mismo libro. |

## Resultado esperado

Después de ejecutar el programa:

1. `CopyWithPivot.xlsx` aparece en `YOUR_DIRECTORY`.
2. Al abrir el archivo en Excel se muestra una nueva hoja llamada **CopySheet**.
3. **CopySheet** contiene una tabla dinámica totalmente funcional idéntica a la original, lista para actualizarse.
4. Todo el formato, filtros y campos calculados se conservan.

Si abres `FullCopy.xlsx`, verás una réplica completa de la hoja original, incluidos los gráficos o imágenes que estaban en la hoja fuente.

## Recapitulación

* Aprendiste cómo **copiar tabla dinámica** en Java usando Aspose.Cells.
* El mismo enfoque funciona para un simple **copiar rango de Excel** o escenarios de **copy range java**.
* Para operaciones masivas, puedes **duplicar tabla dinámica** en muchas hojas.
* Cuando necesitas la hoja completa, **copia hoja de cálculo con tabla dinámica** usando `addCopy`.

## Próximos pasos

* Explora **PivotTable.refreshData()** para actualizar programáticamente la caché después de copiar.
* Combina la lógica de copia con **Excel file streaming** para manejar libros grandes sin cargar todo en memoria.
* Revisa el soporte de Aspose.Cells para **pivot slicers** si tus informes dependen de filtros interactivos.

¡Siéntete libre de adaptar el código a la estructura de tu propio proyecto, experimentar con diferentes tamaños de rango o integrarlo en una canalización de procesamiento de datos más grande. ¡Feliz codificación!

## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que se basan en las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y funcionales con explicaciones paso a paso para ayudarte a dominar funciones adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Cómo actualizar la fuente de la tabla dinámica de Excel con Aspose.Cells para Java: Guía completa](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [Manipulación de tablas dinámicas de Excel Aspose Cells Java](/cells/hongkong/java/data-analysis/excel-pivot-table-manipulation-aspose-cells-java/)
- [Crear nuevo libro de Excel – Copiar y duplicar tabla dinámica](/cells/english/net/pivot-tables/create-new-excel-workbook-copy-duplicate-pivot-table/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}