---
category: general
date: 2026-08-08
description: Cómo copiar una tabla dinámica en Aspose.Cells y copiar un rango a un
  libro de trabajo usando Java. Aprende los pasos exactos para duplicar una tabla
  dinámica con CopyOptions.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy pivot
- copy range to workbook
- aspose.cells copy range
language: es
lastmod: 2026-08-08
og_description: Cómo copiar una tabla dinámica en Aspose.Cells y copiar un rango a
  un libro de trabajo con Java. Sigue esta guía completa para duplicar una tabla dinámica
  usando CopyOptions.
og_image_alt: Diagram showing how to copy pivot in Aspose.Cells
og_title: Cómo copiar una tabla dinámica en Aspose.Cells – copiar rango al libro de
  trabajo
schemas:
- author: Aspose
  dateModified: '2026-08-08'
  description: How to copy pivot in Aspose.Cells and copy range to workbook using
    Java. Learn the exact steps to duplicate a pivot table with CopyOptions.
  headline: How to copy pivot in Aspose.Cells – copy range to workbook
  type: TechArticle
- description: How to copy pivot in Aspose.Cells and copy range to workbook using
    Java. Learn the exact steps to duplicate a pivot table with CopyOptions.
  name: How to copy pivot in Aspose.Cells – copy range to workbook
  steps:
  - name: Add Aspose.Cells to your project
    text: 'If you use Maven, add the following dependency to your `pom.xml`:'
  - name: Load the source workbook
    text: '```java import com.aspose.cells.*;'
  - name: Configure copy options to include the pivot table
    text: '```java // Define copy options to include the pivot table in the copied
      range CopyOptions copyOptions = new CopyOptions() .setCopyPivotTable(true);
      ```'
  - name: Copy the desired range with the pivot table
    text: '```java // Copy the range A1:H20, preserving the pivot table workbook.getWorksheets().get(0).getCells()
      .copyRange("A1:H20", copyOptions); ```'
  - name: Save the modified workbook
    text: '```java // Save the workbook with the copied pivot table workbook.save("YOUR_DIRECTORY/output.xlsx");
      } } ```'
  - name: Expected result
    text: '* `output.xlsx` contains the same data as `input.xlsx`. * The pivot table
      that originally occupied the source range appears in the destination cells,
      fully functional (filters, refresh capability, etc.). * All cell formatting,
      formulas, and column widths are preserved because `copyRange` copies the '
  type: HowTo
tags:
- Aspose.Cells
- Java
- PivotTable
- CopyRange
title: Cómo copiar una tabla dinámica en Aspose.Cells – copiar rango al libro de trabajo
url: /es/java/excel-pivot-tables/how-to-copy-pivot-in-aspose-cells-copy-range-to-workbook/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo copiar una tabla dinámica en Aspose.Cells – copiar rango a libro de trabajo

Si necesitas **cómo copiar una tabla dinámica** en un archivo Excel usando Aspose.Cells, esta guía te muestra el proceso exacto. Al final del tutorial podrás **copiar rango a libro de trabajo** conservando la definición de la tabla dinámica.

El ejemplo usa Java, pero los mismos conceptos se aplican a cualquier lenguaje .NET que funcione con Aspose.Cells. No se requieren herramientas externas—solo la biblioteca Aspose.Cells para Java y un entorno de desarrollo básico.

## Requisitos previos

Antes de comenzar, asegúrate de tener:

* Java Development Kit (JDK) 8 o posterior.
* Maven o Gradle para gestionar dependencias (el ejemplo usa Maven).
* Aspose.Cells for Java 23.9 (o la última versión) añadido a tu proyecto.
* Un libro de trabajo de entrada (`input.xlsx`) que contenga al menos una tabla dinámica en la primera hoja.

Tener estos elementos listos evita errores en tiempo de ejecución cuando el código accede al libro de trabajo.

## Cómo copiar una tabla dinámica con Aspose.Cells

Esta sección recorre cada paso necesario para **cómo copiar una tabla dinámica** de una parte de una hoja a otra, usando la clase `CopyOptions`.

### Paso 1: Añadir Aspose.Cells a tu proyecto

Si usas Maven, agrega la siguiente dependencia a tu `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.9</version>
    <classifier>jdk17</classifier> <!-- adjust JDK version as needed -->
</dependency>
```

*Por qué este paso es importante*: La biblioteca proporciona las clases `Workbook`, `CopyOptions` y otras necesarias para operaciones de **aspose.cells copy range**. Sin la dependencia el compilador no puede resolver esos tipos.

### Paso 2: Cargar el libro de trabajo de origen

```java
import com.aspose.cells.*;

public class CopyPivotTableRange {
    public static void main(String[] args) throws Exception {
        // Load the workbook that contains the pivot table
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

Cargar el archivo crea una representación en memoria de la hoja de cálculo. El objeto `Workbook` te brinda acceso a hojas, celdas y tablas dinámicas.

### Paso 3: Configurar las opciones de copia para incluir la tabla dinámica

```java
        // Define copy options to include the pivot table in the copied range
        CopyOptions copyOptions = new CopyOptions()
                .setCopyPivotTable(true);
```

`CopyOptions.setCopyPivotTable(true)` indica a Aspose.Cells que la operación debe preservar los metadatos de la tabla dinámica. Si omites este indicador, la tabla dinámica se reducirá a datos estáticos, perdiendo su interactividad.

### Paso 4: Copiar el rango deseado con la tabla dinámica

```java
        // Copy the range A1:H20, preserving the pivot table
        workbook.getWorksheets().get(0).getCells()
                .copyRange("A1:H20", copyOptions);
```

El método `copyRange` copia celdas, formato y—gracias a las opciones establecidas en el paso anterior—cualquier tabla dinámica que intersecte el rango. Este es el núcleo de la funcionalidad de **copy range to workbook**.

### Paso 5: Guardar el libro de trabajo modificado

```java
        // Save the workbook with the copied pivot table
        workbook.save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

Guardar escribe los cambios en un nuevo archivo (`output.xlsx`). Ahora puedes abrir este archivo en Excel y ver que la tabla dinámica se ha duplicado exactamente donde se copió el rango.

## Ejemplo completo y ejecutable

Juntando todas las piezas, aquí tienes el programa completo que puedes compilar y ejecutar:

```java
import com.aspose.cells.*;

public class CopyPivotTableRange {
    public static void main(String[] args) throws Exception {
        // 1. Load the workbook that contains the pivot table
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // 2. Define copy options to include the pivot table
        CopyOptions copyOptions = new CopyOptions()
                .setCopyPivotTable(true);

        // 3. Copy the range A1:H20 with the specified options
        workbook.getWorksheets().get(0).getCells()
                .copyRange("A1:H20", copyOptions);

        // 4. Save the modified workbook
        workbook.save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

### Resultado esperado

* `output.xlsx` contiene los mismos datos que `input.xlsx`.
* La tabla dinámica que originalmente ocupaba el rango de origen aparece en las celdas de destino, totalmente funcional (filtros, capacidad de actualización, etc.).
* Todo el formato de celdas, fórmulas y anchos de columna se conservan porque `copyRange` copia todo el bloque de celdas.

## Preguntas comunes y casos límite

**¿Qué pasa si el rango de destino se superpone con una tabla dinámica existente?**  
Aspose.Cells sobrescribirá las celdas de destino. Para evitar pérdida de datos, asegúrate de que el área de destino esté vacía o mueve primero la tabla dinámica existente.

**¿Puedo copiar una tabla dinámica entre hojas de cálculo?**  
Sí. Usa `workbook.getWorksheets().get(targetSheetIndex).getCells().copyRange(sourceRange, copyOptions);` donde `targetSheetIndex` apunta a la hoja de destino.

**¿`setCopyPivotTable(true)` copia la fuente de datos subyacente?**  
El método copia solo la referencia a la caché de la tabla dinámica. Si los datos de origen están en el mismo libro, la tabla dinámica de destino apuntará a la misma caché. Para duplicar la caché, debes crear una nueva caché de tabla dinámica manualmente.

**¿Cómo copiar un rango grande de manera eficiente?**  
Al copiar rangos muy grandes, considera usar `CopyOptions.setCopyFormula(true)` y `setCopyDataValidation(true)` solo si es necesario. Reducir la cantidad de opciones puede mejorar el rendimiento.

## Consejos para un uso fiable de **aspose.cells copy range**

* **Consejo profesional:** Siempre llama a `workbook.calculateFormula()` después de copiar si el rango contiene fórmulas que dependen de la caché de la tabla dinámica.
* **Cuidado con:** Hojas ocultas. `copyRange` funciona solo en hojas visibles a menos que referencias explícitamente la hoja oculta por índice.
* **Verificación de versión:** El indicador `setCopyPivotTable` está disponible a partir de Aspose.Cells 20.9. Asegúrate de que tu versión de la biblioteca lo soporte.

## Conclusión

Ahora sabes **cómo copiar una tabla dinámica** en Aspose.Cells y cómo **copiar rango a libro de trabajo** conservando la funcionalidad completa de la tabla dinámica. Los pasos—añadir la biblioteca, cargar el libro, configurar `CopyOptions`, realizar la copia y guardar—forman un patrón repetible que puedes adaptar a otros escenarios de copiar‑y‑pegar.

A continuación, explora temas relacionados como **aspose.cells copy range** para gráficos, formato condicional y validación de datos. Experimenta copiando entre diferentes formatos de archivo (XLSX → XLS) para ampliar tus capacidades de automatización. ¡Feliz codificación!

## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y funcionales con explicaciones paso a paso para ayudarte a dominar características adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Cómo crear tablas dinámicas en Excel usando Aspose.Cells para Java: Guía completa](/cells/english/java/data-analysis/create-pivot-tables-excel-aspose-cells-java/)
- [Cómo actualizar la fuente de la tabla dinámica de Excel con Aspose.Cells para Java: Guía completa](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [Cómo implementar segmentadores en tablas dinámicas usando Aspose.Cells para Java: Guía completa](/cells/english/java/data-analysis/implement-slicers-pivot-tables-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}