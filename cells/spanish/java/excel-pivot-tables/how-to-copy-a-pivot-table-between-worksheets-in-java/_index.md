---
category: general
date: 2026-10-16
description: Cómo copiar una tabla dinámica en Java con Aspose.Cells – aprende a copiar
  un rango a otra hoja y a copiar rangos entre hojas de cálculo de manera eficiente.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy pivot table
- copy range to another sheet
- copy range between worksheets
language: es
lastmod: 2026-10-16
og_description: Cómo copiar una tabla dinámica en Java usando Aspose.Cells. Este tutorial
  le muestra cómo copiar un rango a otra hoja y copiar un rango entre hojas de cálculo
  con el código completo.
og_image_alt: Diagram illustrating how to copy pivot table from one worksheet to another
  in Java
og_title: Cómo copiar una tabla dinámica entre hojas de cálculo en Java – guía paso
  a paso
schemas:
- author: Aspose
  dateModified: '2026-10-16'
  description: How to copy pivot table in Java with Aspose.Cells – learn to copy range
    to another sheet and copy range between worksheets efficiently.
  headline: How to copy a pivot table between worksheets in Java
  type: TechArticle
- description: How to copy pivot table in Java with Aspose.Cells – learn to copy range
    to another sheet and copy range between worksheets efficiently.
  name: How to copy a pivot table between worksheets in Java
  steps:
  - name: Load the workbook
    text: '```java import com.aspose.cells.*;'
  - name: Locate the source range that contains the pivot table
    text: '```java // The first worksheet (index 0) holds the pivot table. Worksheet
      sourceSheet = workbook.getWorksheets().get(0);'
  - name: Define the destination range on another sheet
    text: '```java // The second worksheet (index 1) will receive the copied pivot
      table. Worksheet destSheet = workbook.getWorksheets().get(1);'
  - name: Copy the source range while preserving the pivot table
    text: '```java // Configure copy options to keep all formatting, formulas, and
      pivot data. CopyOptions copyOptions = new CopyOptions(); copyOptions.setPasteType(PasteType.PASTE_ALL);
      // copies everything copyOptions.setSkipEmptyRows(false); copyOptions.setSkipEmptyColumns(false);'
  - name: Save the workbook and verify the result
    text: '```java // Save the modified workbook to a new file. workbook.save("output.xlsx");
      System.out.println("Pivot table copied successfully."); } } ```'
  type: HowTo
tags:
- Aspose.Cells
- Java
- PivotTable
- Excel automation
title: Cómo copiar una tabla dinámica entre hojas de cálculo en Java
url: /es/java/excel-pivot-tables/how-to-copy-a-pivot-table-between-worksheets-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo copiar una tabla dinámica entre hojas de cálculo en Java

Si necesita **how to copy pivot table** de una hoja a otra en el mismo libro de trabajo, esta guía proporciona una solución completa y lista para ejecutar. Verá cómo copiar el rango de origen que contiene la tabla dinámica, preservar su funcionalidad y verificar el resultado, todo usando Aspose.Cells para Java.

Copiar una tabla dinámica es una tarea común cuando genera informes programáticamente, y hacerlo correctamente evita perder la caché de la tabla dinámica o romper fórmulas. Al final de este tutorial podrá **copy range to another sheet** y **copy range between worksheets** sin pasos manuales.

## Lo que aprenderá

* Cargar un archivo Excel existente con una tabla dinámica.
* Definir el rango de origen que contiene la tabla dinámica.
* Definir un rango de destino en una hoja de cálculo diferente.
* Usar `CopyOptions` para mantener la tabla dinámica intacta.
* Verificar que la tabla dinámica copiada funcione como se espera.

**Requisitos previos**

* Java 17 o posterior.
* Aspose.Cells for Java (versión 23.12 o más reciente).  
* Un archivo Excel (`input.xlsx`) que contiene una tabla dinámica en la primera hoja.

---

## Cómo copiar una tabla dinámica con Aspose.Cells

El núcleo de la operación es un proceso de cuatro pasos: cargar el libro de trabajo, localizar el rango de origen, establecer el rango de destino y realizar la copia. A continuación, cada paso se explica en detalle.

### Paso 1: Cargar el libro de trabajo

```java
import com.aspose.cells.*;

public class CopyPivotTableExample {
    public static void main(String[] args) throws Exception {
        // Load the workbook that contains the original pivot table
        Workbook workbook = new Workbook("input.xlsx");
```

*¿Por qué este paso?*  
Cargar el libro de trabajo trae todo el archivo a la memoria, dándole acceso a hojas de cálculo, celdas y la caché de la tabla dinámica. Aspose.Cells lee el formato del archivo automáticamente, por lo que no necesita preocuparse por `.xls` vs `.xlsx`.

### Paso 2: Localizar el rango de origen que contiene la tabla dinámica

```java
        // The first worksheet (index 0) holds the pivot table.
        Worksheet sourceSheet = workbook.getWorksheets().get(0);

        // Define the exact area that includes the pivot table.
        // Adjust the address if your pivot table spans a different range.
        Range sourceRange = sourceSheet.getCells().createRange("A1:G20");
```

*¿Por qué este paso?*  
Una tabla dinámica se almacena en un bloque de celdas que también hace referencia a una caché oculta. Al seleccionar el rango exacto (`A1:G20` en este ejemplo), se asegura de que la caché permanezca vinculada cuando se copie el rango.

### Paso 3: Definir el rango de destino en otra hoja

```java
        // The second worksheet (index 1) will receive the copied pivot table.
        Worksheet destSheet = workbook.getWorksheets().get(1);

        // Destination starts at cell A1 of the second sheet.
        Range destRange = destSheet.getCells().createRange("A1");
```

*¿Por qué este paso?*  
Elegir un destino en una hoja de cálculo diferente le permite **copy range to another sheet**. La celda superior izquierda (`A1`) es un punto de partida común, pero puede colocarla en cualquier lugar cambiando la dirección.

### Paso 4: Copiar el rango de origen preservando la tabla dinámica

```java
        // Configure copy options to keep all formatting, formulas, and pivot data.
        CopyOptions copyOptions = new CopyOptions();
        copyOptions.setPasteType(PasteType.PASTE_ALL); // copies everything
        copyOptions.setSkipEmptyRows(false);
        copyOptions.setSkipEmptyColumns(false);

        // Perform the copy operation.
        sourceRange.copy(destRange, copyOptions);
```

*¿Por qué este paso?*  
`CopyOptions` controla lo que se transfiere. Usar `PasteType.PASTE_ALL` garantiza que la tabla dinámica, su formato y las fórmulas subyacentes se dupliquen. Sin estas opciones, solo se podrían copiar valores sin formato, rompiendo la funcionalidad de la tabla dinámica.

### Paso 5: Guardar el libro de trabajo y verificar el resultado

```java
        // Save the modified workbook to a new file.
        workbook.save("output.xlsx");
        System.out.println("Pivot table copied successfully.");
    }
}
```

Abra `output.xlsx` en Excel y confirme que:

* La segunda hoja contiene una tabla dinámica totalmente funcional idéntica a la original.
* Actualizar la tabla dinámica actualiza los datos, demostrando que la caché está intacta.

---

## Copiar rango a otra hoja usando Java

Si su objetivo es simplemente **copy range to another sheet** sin una tabla dinámica, el mismo código funciona con un rango de celdas regular. El único cambio es la dirección de origen. La configuración de `CopyOptions` permanece igual, asegurando que las fórmulas y el formato se conserven.

```java
// Example: copy a plain data table from Sheet1!B2:D10 to Sheet3!A1
Range plainSource = workbook.getWorksheets().get(0)
                            .getCells().createRange("B2:D10");
Range plainDest = workbook.getWorksheets().get(2)
                          .getCells().createRange("A1");
plainSource.copy(plainDest, copyOptions);
```

Este fragmento demuestra la flexibilidad de la API para escenarios con y sin tabla dinámica.

---

## Copiar rango entre hojas de cálculo sin perder fórmulas

Cuando **copy range between worksheets**, las fórmulas que hacen referencia a otras hojas pueden romperse si cambian las referencias relativas. Para evitarlo:

1. Use `CopyOptions.setPasteType(PasteType.PASTE_FORMULAS)` si solo necesita fórmulas.
2. Mantenga la hoja de destino en el mismo libro de trabajo para que las referencias internas sigan siendo válidas.
3. Después de copiar, llame a `workbook.calculateFormula();` para forzar un recálculo.

```java
copyOptions.setPasteType(PasteType.PASTE_FORMULAS);
sourceRange.copy(destRange, copyOptions);
workbook.calculateFormula();
```

Estos pasos adicionales garantizan que un rango copiado se comporte exactamente como el original, incluso cuando abarca varias hojas de cálculo.

---

## Consejos profesionales y errores comunes

| Situation | Tip |
|-----------|-----|
| **Pivot cache not updating** | Después de copiar, llame a `destSheet.getPivotTables().get(0).refresh();` para actualizar la caché. |
| **Copying to a different workbook** | Utilice `Workbook destWorkbook = new Workbook();` y luego `sourceRange.copy(destWorkbook.getWorksheets().get(0).getCells().createRange("A1"), copyOptions);`. Recuerde copiar la caché de la tabla dinámica por separado si es necesario. |
| **Large pivot tables** | Aumente el tamaño del heap de Java (`-Xmx2g`) para evitar `OutOfMemoryError` durante la copia. |
| **Preserving styles** | Establezca `copyOptions.setPasteType(PasteType.PASTE_ALL)`; de lo contrario, solo se copian los valores. |

---

## Resultado esperado

Ejecutar el programa completo produce `output.xlsx`. Cuando se abre en Excel:

* **Sheet2!A1:G20** muestra la misma tabla dinámica que **Sheet1!A1:G20**.
* La lista de campos de la tabla dinámica, las etiquetas de fila/columna y los valores de datos coinciden con el origen.
* Actualizar la tabla dinámica actualiza los números, confirmando que la caché funciona.

The console will print:

```
Pivot table copied successfully.
```

---

## Conclusión

En este tutorial aprendió **how to copy pivot table** de una hoja de cálculo a otra usando Aspose.Cells para Java. Al cargar el libro de trabajo, seleccionar el rango de origen correcto, definir un destino y configurar `CopyOptions`, puede copiar de forma fiable **copy range to another sheet** y **copy range between worksheets** mientras preserva toda la funcionalidad de la tabla dinámica.  

A continuación, podría explorar:

* Exportar la tabla dinámica copiada a PDF o HTML.
* Automatizar la actualización de tablas dinámicas en varios libros de trabajo.
* Usar `CopyOptions` para copiar solo elementos específicos (p. ej., valores, formatos).

Siéntase libre de experimentar con diferentes direcciones de rango, estructuras de libros de trabajo o incluso copias entre libros. ¡Feliz codificación!

## ¿Qué debería aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que se basan en las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y funcionales con explicaciones paso a paso para ayudarle a dominar funciones adicionales de la API y explorar enfoques de implementación alternativos en sus propios proyectos.

- [Cómo copiar rango en Java – Copiar tabla dinámica con Aspose.Cells](/cells/english/java/excel-pivot-tables/how-to-copy-range-in-java-copy-pivot-table-with-aspose-cells/)
- [Cómo copiar tabla dinámica en Java – Guía completa de Aspose.Cells](/cells/english/java/excel-pivot-tables/how-to-copy-pivot-table-in-java-complete-aspose-cells-guide/)
- [Copiar tabla dinámica Excel – Guía paso a paso usando Java](/cells/english/java/excel-pivot-tables/copy-pivot-table-excel-step-by-step-guide-using-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}