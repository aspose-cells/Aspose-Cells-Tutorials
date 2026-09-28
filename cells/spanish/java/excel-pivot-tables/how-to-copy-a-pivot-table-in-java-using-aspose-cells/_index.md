---
category: general
date: 2026-09-27
description: Copiar tabla dinámica en Java con Aspose.Cells – una guía paso a paso
  que muestra cómo copiar el rango y preservar las definiciones de la tabla dinámica.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy pivot table
- how to copy pivot table
- copy range aspose cells
language: es
lastmod: 2026-09-27
og_description: Copiar tabla dinámica en Java usando Aspose.Cells. Sigue este tutorial
  completo para copiar el rango de Aspose.Cells y mantener intactas las definiciones
  de la tabla dinámica.
og_image_alt: Screenshot of copy pivot table operation in Aspose.Cells Java
og_title: Copiar una tabla dinámica en Java – Guía rápida de Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Copy pivot table in Java with Aspose.Cells – a step‑by‑step guide that
    shows how to copy range and preserve pivot definitions.
  headline: How to copy a pivot table in Java using Aspose.Cells
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel automation
title: Cómo copiar una tabla dinámica en Java usando Aspose.Cells
url: /es/java/excel-pivot-tables/how-to-copy-a-pivot-table-in-java-using-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo copiar una tabla dinámica en Java usando Aspose.Cells

Si necesitas **copiar tabla dinámica** de un libro de trabajo a otro, esta guía te muestra exactamente cómo hacerlo con Aspose.Cells para Java. La solución funciona para cualquier tabla dinámica que hayas creado y conserva la definición de la tabla sin necesidad de recrearla manualmente.

Aprenderás a cargar el archivo fuente, definir el rango que contiene la tabla dinámica, copiar ese rango a un nuevo libro de trabajo y, finalmente, guardar el resultado. El tutorial también cubre problemas comunes, como preservar las fuentes de datos y manejar libros de trabajo grandes.

## Lo que necesitarás

Antes de comenzar, asegúrate de tener:

* Java 17 o posterior (el código también compila con JDK 8+)
* Aspose.Cells para Java 23.9 o más reciente – la última versión ofrece el soporte más fiable de **copy range aspose cells**
* Un archivo Excel fuente que contenga una tabla dinámica (p. ej., `SourceWithPivot.xlsx`)
* Un IDE o herramienta de compilación (Maven/Gradle) que pueda referenciar el JAR de Aspose.Cells

## Paso 1: Cargar el libro de trabajo fuente que contiene la tabla dinámica

La primera acción es abrir el libro de trabajo que contiene la tabla dinámica que deseas duplicar. Cargar el archivo crea una representación en memoria de todas las hojas, celdas y cachés de tabla dinámica.

```java
import com.aspose.cells.*;

public class CopyPivotTable {
    public static void main(String[] args) throws Exception {
        // Load the source workbook
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/SourceWithPivot.xlsx");
        // Access the first worksheet (adjust the index if needed)
        Worksheet srcWs = srcWb.getWorksheets().get(0);
```

**Por qué es importante:**  
Aspose.Cells lee todo el libro de trabajo, incluidas las hojas de caché de tabla dinámica ocultas. Si omites este paso, la operación posterior de **copy pivot table** perdería la fuente de datos subyacente.

## Paso 2: Crear un libro de trabajo de destino vacío

A continuación, instancia un nuevo libro de trabajo que recibirá la tabla dinámica copiada. Comenzar con un libro limpio evita sobrescrituras accidentales.

```java
        // Create an empty destination workbook
        Workbook destWb = new Workbook();
        Worksheet destWs = destWb.getWorksheets().get(0);
```

**Consejo:** El libro de trabajo predeterminado contiene una hoja vacía, lo cual es perfecto para una copia sencilla. Si necesitas copiar a una hoja con nombre específico, renombra `destWs` con `destWs.setName("TargetSheet")`.

## Paso 3: Definir el rango fuente que incluye la tabla dinámica

Una tabla dinámica ocupa un bloque rectangular de celdas. Debes especificar el rango exacto; de lo contrario solo se copiarán los datos sin formato. En este ejemplo asumimos que la tabla dinámica ocupa **A1:G20**, pero puedes ajustar la dirección para que coincida con tu archivo.

```java
        // Define the range that includes the pivot table
        Range srcRange = srcWs.getCells().createRange("A1:G20");
```

**Por qué funciona:**  
Cuando llamas a `createRange` en la colección `Cells` de la hoja, Aspose.Cells incluye la definición de la tabla dinámica, su caché y cualquier formato. Este es el núcleo de **how to copy pivot table** correctamente.

## Paso 4: Copiar el rango definido a la hoja de destino

Ahora usa el método `copy` para duplicar el rango. El método copia todo lo que está dentro del rango, incluida la definición de la tabla dinámica, fórmulas y estilos.

```java
        // Copy the range (pivot table definition is included) to the destination sheet
        srcRange.copy(destWs.getCells().createRange("A1"));
```

**Nota importante:**  
Si solo necesitas los datos sin la tabla dinámica, podrías usar `srcRange.copyData`. Sin embargo, para una verdadera **copy pivot table** debes copiar todo el rango como se muestra arriba.

## Paso 5: Guardar el libro de trabajo de destino

Finalmente, escribe el nuevo libro de trabajo en disco. El archivo resultante contendrá una tabla dinámica totalmente funcional idéntica a la fuente.

```java
        // Save the destination workbook
        destWb.save("YOUR_DIRECTORY/CopyPivotResult.xlsx");
    }
}
```

Ejecutar el programa genera `CopyPivotResult.xlsx` con el mismo diseño, filtros y cálculos de la tabla dinámica original.

## Resultado esperado

Al abrir `CopyPivotResult.xlsx` en Excel:

* La tabla dinámica aparece en **A1:G20** en la primera hoja.
* Todos los campos de fila/columna, filtros y campos de valor están intactos.
* Actualizar la tabla dinámica refresca la misma fuente de datos que el libro de trabajo fuente (si los datos están incrustados).

## Casos límite y consejos prácticos

| Situación | Cómo manejarla |
|-----------|----------------|
| **La tabla dinámica abarca más columnas de lo esperado** | Usa `srcWs.getPivotTables().get(0).getPivotTableArea()` para obtener la dirección exacta de forma programática. |
| **El libro de trabajo fuente contiene varias tablas dinámicas** | Recorre `srcWs.getPivotTables()` y copia cada rango individualmente, ajustando las direcciones de destino. |
| **Libros de trabajo grandes generan presión de memoria** | Habilita `WorkbookSettings.setMemorySetting(MemorySetting.MEMORY_PREFERENCE)` antes de cargar el archivo fuente. |
| **Necesitas copiar solo la definición de la tabla dinámica, no los datos** | Después de copiar, elimina las filas de datos fuente en el destino con `destWs.getCells().deleteRows(startRow, count)`. |
| **El archivo de destino debe conservar el formato original** | Configura `CopyOptions` con `options.setPasteType(PasteType.ALL)` para una copia de fidelidad total. |

**Consejo profesional:** Siempre verifica la tabla dinámica copiada llamando a `destWs.getPivotTables().get(0).refresh()` de forma programática. Esto asegura que la caché esté actualizada, especialmente cuando la fuente de datos reside en una conexión externa.

## Ejemplo completo ejecutable

A continuación tienes el programa completo que puedes copiar‑pegar en tu IDE. Sustituye `YOUR_DIRECTORY` por la ruta real en tu máquina.

```java
import com.aspose.cells.*;

public class CopyPivotTable {
    public static void main(String[] args) throws Exception {
        // Step 1: Load the source workbook that contains the pivot table
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/SourceWithPivot.xlsx");
        Worksheet srcWs = srcWb.getWorksheets().get(0);

        // Step 2: Create an empty destination workbook
        Workbook destWb = new Workbook();
        Worksheet destWs = destWb.getWorksheets().get(0);

        // Step 3: Define the range that includes the pivot table in the source sheet
        // Adjust the address if your pivot occupies a different area
        Range srcRange = srcWs.getCells().createRange("A1:G20");

        // Step 4: Copy the defined range (pivot table definition is included) to the destination sheet
        srcRange.copy(destWs.getCells().createRange("A1"));

        // Step 5: Save the destination workbook with the copied pivot table
        destWb.save("YOUR_DIRECTORY/CopyPivotResult.xlsx");
    }
}
```

Ejecutar este código **copy pivot table** exactamente como se describe, y demuestra la forma más directa de **copy range aspose cells** mientras se conserva la funcionalidad de la tabla dinámica.

## Conclusión

Ahora sabes cómo **copy pivot table** en Java usando Aspose.Cells, desde cargar el libro de trabajo fuente hasta guardar el archivo de destino. La guía cubrió los pasos esenciales, explicó por qué cada paso es importante y abordó casos límite comunes.  

A continuación, podrías explorar:

* **how to copy pivot table** entre diferentes hojas dentro del mismo libro de trabajo
* Usar **copy range aspose cells** para duplicar gráficos o formato condicional
* Automatizar la actualización de la tabla dinámica después de copiarla para mantener los datos al día

¡Siéntete libre de experimentar con rangos más grandes, múltiples tablas dinámicas o integrar esta lógica en una canalización más amplia de procesamiento de Excel! ¡Feliz codificación!

## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y funcionales con explicaciones paso a paso para ayudarte a dominar características adicionales de la API y explorar enfoques alternativos de implementación en tus propios proyectos.

- [Copy Pivot Table in Java – Preserve It, Export to PPTX](/cells/english/java/excel-pivot-tables/copy-pivot-table-in-java-preserve-it-export-to-pptx/)
- [How to Update Excel Pivot Table Source with Aspose.Cells for Java&#58; A Comprehensive Guide](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [Excel Pivot Table Manipulation with Aspose.Cells Java&#58; A Comprehensive Guide](/cells/english/java/data-analysis/excel-pivot-table-manipulation-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}