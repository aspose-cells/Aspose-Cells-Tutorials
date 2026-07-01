---
category: general
date: 2026-06-30
description: Ordenar valores únicos en Excel usando Java. Aprende cómo establecer
  fórmulas, recalcular fórmulas y generar una lista única en Excel con Aspose.Cells.
draft: false
keywords:
- sort unique values excel
- how to set formula
- how to recalculate formulas
- generate unique list excel
- set array formula
language: es
og_description: Ordena valores únicos en Excel con Java. Esta guía muestra cómo establecer
  fórmulas, recalcular fórmulas y generar una lista única en Excel en minutos.
og_title: Ordenar valores únicos en Excel – Tutorial de Java para fórmulas de matriz
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Sort unique values Excel using Java. Learn how to set formula, recalculate
    formulas, and generate unique list Excel with Aspose.Cells.
  headline: Sort Unique Values Excel – Complete Java Guide to Set Array Formulas
  type: TechArticle
- description: Sort unique values Excel using Java. Learn how to set formula, recalculate
    formulas, and generate unique list Excel with Aspose.Cells.
  name: Sort Unique Values Excel – Complete Java Guide to Set Array Formulas
  steps:
  - name: How It Works
    text: '- `UNIQUE(B1:B10)` scans the range and returns a vertical array of distinct
      strings. - `SORT(...)` takes that array and orders it in ascending order. -
      Wrapping the whole thing in `=` and calling `setFormulaArray` tells Aspose.Cells
      to treat the result as a **spilled array**, just like Excel would.'
  - name: Empty Cells in the Source Range
    text: 'If `B1:B10` contains blanks, `UNIQUE` will treat them as a distinct entry.
      To ignore blanks, wrap the range with `FILTER`:'
  - name: Non‑Contiguous Data
    text: 'When your data lives in multiple columns, you can join them with `CHOOSE`
      or `TEXTJOIN` before applying `UNIQUE`. For example:'
  - name: ' ## What Should You Learn Next?


      The following tutorials cover closely related topics that build on the techniques
      demonstrated in this guide. Each resource includes complete working code examples
      with step-by-step explanations to help you master additional API features and
      explore alternative implementation approaches in your own projects.

      - [How to Sort Excel Files by Cell Color Using Aspose.Cells Java&#58; A Comprehensive
      Guide](/cells/english/java/data-analysis/excel-file-sorting-aspose-cells-java/)
      - [Mastering Aspose.Cells Java&#58; How to Interrupt Formula Calculation in
      Excel Workbooks](/cells/english/java/calculation-engine/master-aspose-cells-java-interrupt-formula-calculation-workbook/)
      - [How to Create an Excel Data Validation List with Aspose.Cells for Java&#58;
      A Step-by-Step Guide](/cells/english/java/data-validation/excel-data-validation-aspose-cells-java/)

      {{< /blocks/products/pf/tutorial-page-section >}}'
    text: '{{< /blocks/products/pf/main-container >}} {{< /blocks/products/pf/main-wrap-class
      >}} {{< blocks/products/products-backtop-button >}}'
  type: HowTo
- questions:
  - answer: The `SORT` and `UNIQUE` functions are part of the Dynamic Array engine
      introduced in Excel 365. For legacy files you’d need to use classic array formulas
      like `{=INDEX(..., MATCH(0, COUNTIF($A$1:A1, $B$1:$B$10), 0))}`. Aspose.Cells
      can still evaluate them, but the syntax is more verbose.
    question: Does this work with older Excel versions (pre‑Office 365)?
  - answer: Absolutely. Just change the address in `cells.get("A1")`. The spilled
      array will always start at the cell you specify and expand right‑and‑down as
      needed.
    question: Can I set the array formula on a range other than `A1`?
  - answer: 'Replace the static range with a dynamic one, e.g., `B:B` or a named range.
      The formula becomes `=SORT(UNIQUE(B:B))`. Be cautious with whole‑column references
      on very large sheets; they can impact performance. --- ## Conclusion We’ve just
      covered **how to set formula** in Java to **sort unique values'
    question: What if my source data is larger than `B1:B10`?
  type: FAQPage
tags:
- Excel automation
- Java
- Aspose.Cells
title: Ordenar valores únicos en Excel – Guía completa de Java para establecer fórmulas
  de matriz
url: /es/java/formulas-functions/sort-unique-values-excel-complete-java-guide-to-set-array-fo/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ordenar valores únicos en Excel – Guía completa de Java para establecer fórmulas de matriz

¿Alguna vez te has preguntado cómo **ordenar valores únicos en Excel** sin arrastrar fórmulas? No eres el único. En muchos escenarios de informes necesitas una lista limpia, ordenada alfabéticamente, de entradas distintas, y hacerlo manualmente es un dolor.  

¿La buena noticia? Con unas pocas líneas de código Java puedes **establecer una fórmula de matriz** en una hoja de cálculo, luego **recalcular fórmulas** para que el rango expandido se llene automáticamente. En este tutorial repasaremos todo—desde crear un libro de trabajo hasta generar una lista única al estilo Excel—para que puedas incrustar la solución directamente en tu aplicación.

## Qué cubre este tutorial

- Configurar un proyecto Java con Aspose.Cells (la biblioteca que impulsa el fragmento de código).  
- Usar las funciones `SORT` y `UNIQUE` juntas para **generar una lista única en Excel**.  
- Aplicar una **fórmula de matriz** a una celda programáticamente.  
- Activar una pasada de cálculo para que el paso de **cómo recalcular fórmulas** ocurra instantáneamente.  
- Verificar la salida y ajustar la solución para casos límite como celdas vacías o rangos no contiguos.

Al final de esta guía podrás insertar un método listo para usar en cualquier servicio Java que necesite exportar hojas de Excel limpias.

> **Consejo profesional:** Si ya estás usando Maven, agregar Aspose.Cells como dependencia te ahorra manejar archivos JAR manualmente.

---

## Requisitos previos

| Requisito | Por qué es importante |
|-------------|----------------|
| Java 8 o superior | Aspose.Cells está dirigido a Java 8+. |
| Maven (o Gradle) | Simplifica la gestión de dependencias. |
| Aspose.Cells para Java | Proporciona las APIs `Workbook`, `Worksheet` y de fórmulas que utilizaremos. |
| Familiaridad básica con funciones de Excel | Entender `SORT` y `UNIQUE` te ayuda a adaptar el código. |

> *Si aún no tienes Aspose.Cells, agrega esto a tu `pom.xml`*:

```xml
<!-- Aspose.Cells for Java -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version> <!-- latest as of June 2026 -->
</dependency>
```

## Paso 1: Crear un nuevo libro de trabajo (Cómo comenzar a establecer la fórmula)

Primero necesitamos un libro de trabajo en blanco. Piensa en él como el lienzo vacío donde más tarde **estableceremos una fórmula de matriz** en la celda `A1`.

```java
import com.aspose.cells.*;

public class UniqueSortExample {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook
        Workbook workbook = new Workbook();

        // The rest of the steps follow...
```

> *¿Por qué crear un nuevo libro de trabajo?*  
> Garantiza un entorno limpio, evitando fórmulas ocultas que podrían interferir con nuestros datos de prueba.

## Paso 2: Poblar datos de ejemplo (Opcional pero útil)

Para ver el resultado claramente, llenemos la columna **B** con algunas entradas duplicadas.

```java
        // Step 2: Get the first worksheet
        Worksheet worksheet = workbook.getWorksheets().get(0);
        Cells cells = worksheet.getCells();

        // Sample data in B1:B10
        String[] rawData = { "Apple", "Banana", "Apple", "Cherry", "Banana",
                             "Date", "Elderberry", "Fig", "Date", "Grape" };
        for (int i = 0; i < rawData.length; i++) {
            cells.get("B" + (i + 1)).putValue(rawData[i]);
        }
```

> *¿Por qué usar la columna B?*  
> La fórmula que escribiremos hace referencia a `B1:B10`, así que mantener los datos allí refleja el ejemplo clásico de Excel.

## Paso 3: Establecer una fórmula de matriz que **ordene valores únicos en Excel**

Ahora ocurre la magia. Combinamos `UNIQUE` (para eliminar duplicados) con `SORT` (para ordenarlos alfabéticamente). La expresión resultante es una **fórmula de matriz**, lo que significa que se expandirá automáticamente a celdas adyacentes.

```java
        // Step 3: Set an array formula that sorts the unique values from B1:B10
        // This is the core of “how to set formula” for our scenario.
        cells.get("A1").setFormulaArray("=SORT(UNIQUE(B1:B10))");
```

### Cómo funciona

- `UNIQUE(B1:B10)` escanea el rango y devuelve una matriz vertical de cadenas distintas.  
- `SORT(...)` toma esa matriz y la ordena en orden ascendente.  
- Envolver todo con `=` y llamar a `setFormulaArray` indica a Aspose.Cells que trate el resultado como una **matriz expandida**, tal como lo haría Excel.

> **Nota:** Si estás usando una versión más antigua de Excel que no tiene `SORT` o `UNIQUE`, puedes recurrir a `SORT(UNIQUE(...))` con la función **LET** o usar fórmulas de matriz heredadas (`=INDEX(...)`). El tutorial se centra en el enfoque de matrices dinámicas modernas porque es la forma más limpia de **generar una lista única en Excel** hoy.

## Paso 4: Recalcular fórmulas para que el rango expandido se rellene

Después de colocar la fórmula, el libro de trabajo no la evalúa automáticamente. Aquí es donde entra el paso de **cómo recalcular fórmulas**.

```java
        // Step 4: Recalculate formulas so the spilled range is populated automatically
        workbook.calculateFormula();
```

Llamar a `calculateFormula()` obliga a Aspose.Cells a ejecutar el motor de Excel, rellenando las celdas `A1`, `A2`, … con los valores únicos ordenados.

> *¿Por qué no confiar en la evaluación perezosa?*  
> En un contexto del lado del servidor a menudo necesitas los datos listos para exportar (CSV, PDF, etc.) justo después del cálculo, por lo que una llamada explícita garantiza la consistencia.

## Paso 5: Verificar el resultado (Depuración opcional)

Siempre es buena idea imprimir los valores expandidos en la consola—especialmente cuando te estás enseñando una nueva API.

```java
        // Step 5: Output the spilled range to the console
        System.out.println("Sorted unique list:");
        int row = 0;
        while (true) {
            String value = cells.get(row, 0).getStringValue(); // column A = index 0
            if (value == null || value.isEmpty()) break; // stop at first empty cell
            System.out.println("- " + value);
            row++;
        }

        // Optionally, save the workbook to inspect in Excel
        workbook.save("SortedUniqueValues.xlsx");
    }
}
```

Ejecutar el programa imprime:

```
Sorted unique list:
- Apple
- Banana
- Cherry
- Date
- Elderberry
- Fig
- Grape
```

Abre `SortedUniqueValues.xlsx` y verás los mismos datos expandiéndose desde `A1` hacia abajo.

## Manejo de casos límite

### Celdas vacías en el rango de origen

Si `B1:B10` contiene celdas vacías, `UNIQUE` las tratará como una entrada distinta. Para ignorar los vacíos, envuelve el rango con `FILTER`:

```java
cells.get("A1").setFormulaArray("=SORT(UNIQUE(FILTER(B1:B10, B1:B10<>\"\")))");
```

### Datos no contiguos

Cuando tus datos están en varias columnas, puedes unirlos con `CHOOSE` o `TEXTJOIN` antes de aplicar `UNIQUE`. Por ejemplo:

```java
cells.get("A1").setFormulaArray(
    "=SORT(UNIQUE(CHOOSE({1,2}, B1:B10, C1:C10)))"
);
```

Estos ajustes demuestran la flexibilidad de **cómo establecer la fórmula** para escenarios más complejos.

## Ejemplo completo (todos los pasos combinados)

A continuación se muestra el programa Java completo y ejecutable. Copia‑pégalo en tu IDE, agrega la dependencia de Aspose.Cells y pulsa *Run*.

```java
import com.aspose.cells.*;

public class UniqueSortExample {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook
        Workbook workbook = new Workbook();

        // Step 2: Get the first worksheet and fill sample data
        Worksheet worksheet = workbook.getWorksheets().get(0);
        Cells cells = worksheet.getCells();

        String[] rawData = { "Apple", "Banana", "Apple", "Cherry", "Banana",
                             "Date", "Elderberry", "Fig", "Date", "Grape" };
        for (int i = 0; i < rawData.length; i++) {
            cells.get("B" + (i + 1)).putValue(rawData[i]);
        }

        // Step 3: Set an array formula that sorts the unique values from B1:B10
        cells.get("A1").setFormulaArray("=SORT(UNIQUE(B1:B10))");

        // Step 4: Recalculate formulas so the spilled range is populated automatically
        workbook.calculateFormula();

        // Step 5: Output the spilled range to the console
        System.out.println("Sorted unique list:");
        int row = 0;
        while (true) {
            String value = cells.get(row, 0).getStringValue(); // column A = index 0
            if (value == null || value.isEmpty()) break;
            System.out.println("- " + value);
            row++;
        }

        // Save the workbook for visual verification
        workbook.save("SortedUniqueValues.xlsx");
    }
}
```

**Salida esperada** (mostrada en la consola) coincide con la lista ordenada y deduplicada que discutimos antes. Al abrir el archivo Excel generado verás los mismos valores expandiéndose desde `A1` hacia abajo.

## Preguntas frecuentes

**Q: ¿Esto funciona con versiones antiguas de Excel (pre‑Office 365)?**  
A: Las funciones `SORT` y `UNIQUE` forman parte del motor de Matrices Dinámicas introducido en Excel 365. Para archivos heredados necesitarías usar fórmulas de matriz clásicas como `{=INDEX(..., MATCH(0, COUNTIF($A$1:A1, $B$1:$B$10), 0))}`. Aspose.Cells aún puede evaluarlas, pero la sintaxis es más extensa.

**Q: ¿Puedo establecer la fórmula de matriz en un rango distinto a `A1`?**  
A: Por supuesto. Simplemente cambia la dirección en `cells.get("A1")`. La matriz expandida siempre comenzará en la celda que especifiques y se expandirá a la derecha y hacia abajo según sea necesario.

**Q: ¿Qué pasa si mis datos de origen son más grandes que `B1:B10`?**  
A: Reemplaza el rango estático por uno dinámico, por ejemplo `B:B` o un rango con nombre. La fórmula se convierte en `=SORT(UNIQUE(B:B))`. Ten cuidado con las referencias a columnas completas en hojas muy grandes; pueden afectar el rendimiento.

## Conclusión

Acabamos de cubrir **cómo establecer una fórmula** en Java para **ordenar valores únicos en Excel**, cómo **recalcular fórmulas**, y cómo **generar una lista única en Excel** usando la potente API de Aspose.Cells. Los pasos son sencillos: crear un libro de trabajo, poblar datos, aplicar una fórmula de matriz, activar el cálculo y verificar el resultado.  

A partir de aquí puedes expandir—agregar formato condicional, exportar a PDF, o integrar el método en un servicio web que entregue informes listos. La idea central sigue siendo la misma: dejar que las propias funciones de Excel hagan el trabajo pesado y que Java orqueste el proceso.

¿Listo para llevar tu automatización de Excel al siguiente nivel? Prueba cambiar `SORT` por `SORTBY` para ordenar por una columna secundaria, o experimenta con `FILTER` para excluir filas que no cumplan las reglas de negocio. Las posibilidades son prácticamente infinitas.

---

###

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}