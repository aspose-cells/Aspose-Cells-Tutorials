---
category: general
date: 2026-11-19
description: Aprende cómo copiar una tabla dinámica en Java preservando sus datos
  y su diseño. Esta guía paso a paso también muestra cómo copiar tablas dinámicas
  de Excel de manera eficiente.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy pivot table
- how to copy pivot
- how to preserve pivot
- preserve pivot table
- copy excel pivot
language: es
lastmod: 2026-11-19
og_description: Copiar tabla dinámica en Java con Aspose.Cells. Sigue esta guía para
  aprender cómo preservar las tablas dinámicas y copiar los datos de tabla dinámica
  de Excel con precisión.
og_image_alt: Illustration of the copy pivot table workflow in Java
og_title: Copiar tabla dinámica en Java – guía completa de Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-11-19'
  description: Learn how to copy pivot table in Java while preserving its data and
    layout. This step‑by‑step guide also shows how to copy excel pivot tables efficiently.
  headline: How to copy pivot table in Java with Aspose.Cells
  type: TechArticle
tags:
- Java
- Aspose.Cells
- Excel automation
- Pivot tables
title: Cómo copiar una tabla dinámica en Java con Aspose.Cells
url: /es/java/excel-pivot-tables/how-to-copy-pivot-table-in-java-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo copiar una tabla dinámica en Java con Aspose.Cells

Si necesitas **copiar una tabla dinámica** de un libro a otro, esta guía te muestra exactamente cómo hacerlo en Java. Ya sea que estés construyendo un motor de informes o migrando datos, verás una forma fiable de preservar la caché, los campos y el formato de la tabla dinámica.

Copiar una tabla dinámica puede ser complicado porque una simple copia de rango a menudo pierde la fuente de datos subyacente. En este tutorial usaremos Aspose.Cells para **copiar tablas dinámicas** manteniendo intactos todos los cálculos, y también cubriremos **cómo preservar tablas dinámicas** cuando el libro de destino está vacío.

## Requisitos previos

Antes de comenzar, asegúrate de tener:

* Java 17 o superior instalado.  
* Aspose.Cells for Java (versión 23.9 o posterior) añadido al classpath de tu proyecto.  
* Dos archivos Excel: un libro origen que contiene la tabla dinámica y un libro destino vacío (o un libro en el que quieras fusionar).

No necesitas ninguna licencia especial para el ejemplo de código, pero una licencia válida de Aspose.Cells elimina las marcas de agua de evaluación.

## Paso 1: Cargar el libro origen que contiene la tabla dinámica

El primer paso es abrir el libro que contiene la tabla dinámica original. Cargar el archivo te da acceso a la hoja, a las celdas y a la caché de la tabla dinámica.

```java
// Step 1: Load the source workbook that contains the pivot table
Workbook srcWb = new Workbook("YOUR_DIRECTORY/source.xlsx");
```

*Por qué es importante*: Aspose.Cells lee todo el libro, incluida la caché oculta que alimenta la tabla dinámica. Sin cargar el archivo completo, la operación de copia perdería la definición de la tabla dinámica.

## Paso 2: Preparar el libro destino

Crea un libro nuevo (o abre uno existente) y obtén su primera hoja. Aquí es donde se colocará la tabla dinámica.

```java
// Step 2: Create a new destination workbook and get its first worksheet
Workbook destWb = new Workbook();                     // empty workbook
Worksheet destWs = destWb.getWorksheets().get(0);    // first sheet
```

*Consejo*: Si ya tienes un libro objetivo, reemplaza la llamada `new Workbook()` por `new Workbook("target.xlsx")`. Esto te permite **copiar una tabla dinámica de Excel** en un libro ya poblado.

## Paso 3: Definir el área de celdas que engloba la tabla dinámica

Debes especificar el rango exacto que cubre la tabla dinámica. El rango incluye la tabla, la lista de campos y cualquier dato circundante que quieras conservar.

```java
// Step 3: Define the cell area that covers the pivot table in the source sheet
CellArea area = CellArea.createCellArea("A1", "H30"); // adjust as needed
```

*Por qué es importante*: El `CellArea` le indica a Aspose.Cells qué copiar. Si el área es demasiado pequeña, la tabla dinámica se truncará; si es demasiado grande, copiarás datos innecesarios. Ajusta las coordenadas según el tamaño real de tu tabla dinámica.

## Paso 4: Ejecutar la operación de copia con CopyOptions

Utiliza el método `copy` de la colección de celdas de la hoja origen. Pasar un nuevo objeto `CopyOptions()` garantiza que se transfieran todos los formatos, fórmulas y la caché de la tabla dinámica.

```java
// Step 4: Copy the defined range (including the pivot table) to the destination worksheet
srcWb.getWorksheets().get(0).getCells().copy(area, destWs.getCells(), new CopyOptions());
```

### Por qué `CopyOptions` preserva la tabla dinámica

`CopyOptions` indica a Aspose.Cells que trate el rango como un *objeto completo* en lugar de un conjunto plano de valores. Esta es la clave para **cómo preservar tablas dinámicas**: la caché subyacente se duplica, de modo que el libro destino puede recalcular la tabla dinámica sin intervención manual.

## Paso 5: Guardar el libro destino

Finalmente, escribe el archivo destino en disco. El archivo guardado contendrá una copia totalmente funcional de la tabla dinámica original.

```java
// Step 5: Save the destination workbook – the pivot table is preserved
destWb.save("YOUR_DIRECTORY/copied_with_pivot.xlsx");
```

*Resultado esperado*: Al abrir `copied_with_pivot.xlsx` en Excel se muestra la tabla dinámica idéntica, completa con segmentadores, filtros y campos calculados. Puedes actualizarla y la fuente de datos apuntará al rango copiado dentro del mismo libro.

---

![Diagrama que muestra el proceso de copiar una tabla dinámica](/images/copy-pivot-table-workflow.png){.align-center width=600 alt="Diagrama que ilustra el flujo de copiar una tabla dinámica del libro origen al libro destino"}

## Cómo copiar tablas dinámicas en varias hojas de cálculo

Si necesitas **copiar tablas dinámicas de Excel** de varias hojas, repite los Pasos 3‑4 para cada hoja origen. También puedes iterar sobre `srcWb.getWorksheets()` y copiar cada tabla dinámica en la hoja correspondiente de `destWb`. Aquí tienes un ejemplo de bucle conciso:

```java
for (int i = 0; i < srcWb.getWorksheets().getCount(); i++) {
    Worksheet srcWs = srcWb.getWorksheets().get(i);
    Worksheet newDestWs = destWb.getWorksheets().add();
    // Assume each pivot occupies A1:H30 – adjust per sheet if needed
    CellArea area = CellArea.createCellArea("A1", "H30");
    srcWs.getCells().copy(area, newDestWs.getCells(), new CopyOptions());
}
destWb.save("YOUR_DIRECTORY/multi_sheet_copy.xlsx");
```

*Pro tip*: Usa `srcWs.getPivotTables().getCount()` para detectar si una hoja realmente contiene una tabla dinámica antes de copiar. Así evitas copiar datos irrelevantes.

## Problemas comunes y cómo evitarlos

| Problema | Por qué ocurre | Solución |
|----------|----------------|----------|
| **La tabla dinámica pierde su caché** | Usar `Worksheet.copy()` sin `CopyOptions` copia solo los valores de las celdas. | Siempre usa `srcWs.getCells().copy(..., new CopyOptions())`. |
| **El destino muestra errores #REF!** | La tabla dinámica copiada sigue referenciando la fuente de datos externa del libro original. | Después de copiar, llama `destWs.getPivotTables().get(0).refresh();` para volver a enlazar la caché al nuevo rango. |
| **Los segmentadores desaparecen** | Los segmentadores se almacenan fuera del área principal de celdas. | Amplía `CellArea` para incluir los rangos de los segmentadores, o copia la hoja completa (`srcWs.copy(destWs, new CopyOptions())`). |
| **Ralentización del rendimiento en tablas dinámicas grandes** | Copiar rangos enormes con formato puede ser lento. | Usa `CopyOptions.setOnlyData(true)` si no necesitas formato, y luego reaplica los estilos manualmente. |

## Cómo preservar el formato de la tabla dinámica al actualizar datos

A veces necesitas **preservar el diseño de la tabla dinámica** después de que cambien los datos de origen. Después de copiar, puedes bloquear el estilo de la tabla dinámica:

```java
PivotTable pt = destWs.getPivotTables().get(0);
pt.setPreserveFormatting(true);   // keeps colors, fonts, and layout
pt.refresh();                     // recalculates with new data
```

Establecer `PreserveFormatting` garantiza que cualquier estilo personalizado que aplicaste en el origen sobreviva a la copia.

## Verificando la copia

Una forma rápida de confirmar que la copia se realizó correctamente es comparar las definiciones de las tablas dinámicas:

```java
PivotTable srcPt = srcWb.getWorksheets().get(0).getPivotTables().get(0);
PivotTable destPt = destWs.getPivotTables().get(0);

System.out.println("Source fields: " + srcPt.getFields().size());
System.out.println("Destination fields: " + destPt.getFields().size());
// Both numbers should match
```

Si los recuentos coinciden y el libro destino se abre sin errores, has **copiado la tabla dinámica** con éxito.

## Conclusión

Ahora sabes cómo **copiar una tabla dinámica** de un libro Excel a otro usando Aspose.Cells para Java, y has visto los pasos exactos para **copiar tablas dinámicas** asegurando que la caché, el formato y los segmentadores permanezcan intactos. El mismo patrón funciona para escenarios de **copiar tablas dinámicas de Excel** en múltiples hojas, y puedes adaptar el código para casos especiales como preservar el formato o manejar conjuntos de datos grandes.

### Próximos pasos

* Explora opciones de **preservar tabla dinámica** como `setPreserveFormatting` y `refresh` para fuentes de datos dinámicas.  
* Prueba copiar tablas dinámicas entre libros con diferentes órdenes de columnas—ajusta el `CellArea` según corresponda.  
* Combina esta técnica con Aspose.Slides para incrustar instantáneas de tablas dinámicas en presentaciones PowerPoint.

¡Feliz codificación, y siéntete libre de experimentar con variaciones que se ajusten a tu canal de automatización específico!

## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y explicaciones paso a paso para ayudarte a dominar funciones adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [How to copy range and preserve a pivot table in Java](/cells/english/java/excel-pivot-tables/how-to-copy-range-and-preserve-a-pivot-table-in-java/)
- [How to copy a pivot table between worksheets in Java](/cells/english/java/excel-pivot-tables/how-to-copy-a-pivot-table-between-worksheets-in-java/)
- [How to copy pivot table to a new workbook in Java](/cells/english/java/excel-pivot-tables/how-to-copy-pivot-table-to-a-new-workbook-in-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}