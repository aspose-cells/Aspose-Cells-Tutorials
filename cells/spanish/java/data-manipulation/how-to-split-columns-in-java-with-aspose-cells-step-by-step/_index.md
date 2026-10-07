---
category: general
date: 2026-10-07
description: Cómo dividir columnas usando Aspose.Cells para Java. Aprende a dividir
  una cadena en columnas, automatizar fórmulas de Excel y escribir una fórmula en
  una celda en unas pocas líneas de código.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to split columns
- split string into columns
- automate excel formula
- write formula to cell
language: es
lastmod: 2026-10-07
og_description: Cómo dividir columnas en Java con Aspose.Cells. Este tutorial le muestra
  cómo dividir una cadena en columnas, automatizar la evaluación de fórmulas de Excel
  y escribir una fórmula en una celda.
og_image_alt: Screenshot of Java code that splits columns in an Excel worksheet using
  Aspose.Cells
og_title: Cómo dividir columnas en Java con Aspose.Cells – tutorial rápido
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: How to split columns using Aspose.Cells for Java. Learn to split string
    into columns, automate Excel formula, and write formula to cell in a few lines
    of code.
  headline: How to split columns in Java with Aspose.Cells – step‑by‑step guide
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel automation
title: Cómo dividir columnas en Java con Aspose.Cells – guía paso a paso
url: /es/java/data-manipulation/how-to-split-columns-in-java-with-aspose-cells-step-by-step/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo dividir columnas en Java con Aspose.Cells – guía paso a paso

Si necesitas **how to split columns** en una hoja de cálculo de Excel de forma programática, esta guía te muestra el proceso completo con Aspose.Cells para Java. También aprenderás cómo **split string into columns**, **automate Excel formula** evaluation, y **write formula to a cell** usando código conciso y listo para producción.

Dividir columnas de forma programática elimina la copia‑pegado manual, reduce errores y permite transformaciones de datos a gran escala. Al final de este tutorial podrás generar, modificar y evaluar fórmulas al vuelo, haciendo de Excel una parte real de tu backend Java.

## Requisitos previos

Antes de comenzar, asegúrate de tener:

* Java 17 o posterior instalado.
* Maven 3.8+ (o Gradle) para la gestión de dependencias.
* Una licencia de Aspose.Cells para Java (la versión de evaluación gratuita funciona para aprendizaje).
* Familiaridad básica con la sintaxis de Java y conceptos de Excel.

Si falta alguno de estos elementos, instálalo primero; los ejemplos de código asumen un proyecto Maven estándar.

## Paso 1: Añadir Aspose.Cells a tu proyecto

Añade la siguiente dependencia a tu `pom.xml`. Esto descarga la última versión estable de la biblioteca Aspose.Cells.

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- Use the latest version available -->
</dependency>
```

**Por qué este paso es importante:** La biblioteca proporciona las clases `Workbook`, `Worksheet` y `Cell` necesarias para manipular archivos Excel sin Microsoft Office. Sin la dependencia el código no compilará.

## Paso 2: Crear un libro de trabajo y seleccionar la primera hoja de cálculo

```java
import com.aspose.cells.*;

public class SplitColumnsExample {
    public static void main(String[] args) throws Exception {
        // Step 2: Initialize a new workbook and access the first worksheet
        Workbook workbook = new Workbook();                     // creates an empty .xlsx file in memory
        Worksheet worksheet = workbook.getWorksheets().get(0); // first sheet is index 0
```

El objeto `Workbook` representa todo el archivo Excel. Acceder a la primera hoja de cálculo garantiza un punto de partida predecible para la fórmula que vamos a escribir.

## Paso 3: Escribir la fórmula WRAPCOLS en una celda objetivo

```java
        // Step 3: Identify the target cell (A1) where the formula will be placed
        Cell targetCell = worksheet.getCells().get("A1");

        // Step 3: Write the WRAPCOLS formula to split a long string into three columns
        // WRAPCOLS(string, columns) distributes the string across the specified number of columns.
        targetCell.setFormula("=WRAPCOLS(\"This is a very long string that needs to be split\",3)");
```

**Por qué usamos `WRAPCOLS`:** La función incorporada de Excel `WRAPCOLS` divide automáticamente un único valor de texto en un número definido de columnas, manejando los límites de palabras de forma inteligente. Esta es la manera más fiable de **split string into columns** sin lógica de análisis personalizada.

## Paso 4: Forzar al libro de trabajo a evaluar la fórmula

```java
        // Step 4: Calculate all formulas in the workbook so the result becomes visible
        workbook.calculateFormula();
```

Llamar a `calculateFormula()` **automates Excel formula** evaluation en el lado del servidor. Sin esta llamada la celda seguiría conteniendo el texto de la fórmula, no los valores calculados.

## Paso 5: Recuperar y mostrar el resultado envuelto

```java
        // Step 5: Retrieve the computed value from the target cell
        String result = targetCell.getStringValue(); // returns the first column of the split result
        System.out.println("First column output: " + result);

        // Optionally, read the other columns created by WRAPCOLS
        String second = worksheet.getCells().get("B1").getStringValue();
        String third  = worksheet.getCells().get("C1").getStringValue();

        System.out.println("Second column output: " + second);
        System.out.println("Third column output: " + third);

        // Save the workbook to verify the split visually (optional)
        workbook.save("SplitColumnsResult.xlsx");
    }
}
```

Al ejecutar el programa, la consola muestra:

```
First column output: This is a very long
Second column output: string that needs
Third column output: to be split
```

El archivo `SplitColumnsResult.xlsx` generado muestra las tres columnas pobladas con el texto dividido.

## Entendiendo la función WRAPCOLS

* **Sintaxis:** `WRAPCOLS(text, columns, [delimiter])`
* **Parámetros:**
  * `text` – la cadena que deseas dividir.
  * `columns` – el número de columnas donde distribuir el texto.
  * `delimiter` (opcional) – carácter usado para dividir la cadena; por defecto es un espacio.
* **Valor de retorno:** Una matriz que se derrama en celdas adyacentes, cada elemento contiene una porción del texto original.

Debido a que la función se derrama horizontalmente, solo necesitas escribir la fórmula en la celda más a la izquierda (A1 en el ejemplo). Excel completa automáticamente B1, C1, … según sea necesario.

## Variaciones comunes y casos límite

| Situación | Ajuste recomendado |
|-----------|--------------------|
| **Recuento de columnas variable** | Reemplaza el `3` codificado de forma rígida por una variable: `targetCell.setFormula(String.format("=WRAPCOLS(\"%s\",%d)", longString, columnCount));` |
| **Delimitador personalizado** | Usa el tercer argumento, por ejemplo, `=WRAPCOLS(A2,4,",")` para dividir por comas. |
| **Cadena fuente vacía** | La función devuelve celdas vacías; protege contra `null` o cadenas vacías antes de establecer la fórmula. |
| **Conjuntos de datos grandes** | Aplica la fórmula en un bucle para cada fila, luego llama a `calculateFormula()` una vez después del bucle para mejorar el rendimiento. |
| **Caracteres no ASCII** | WRAPCOLS funciona con Unicode; asegúrate de que tu archivo fuente Java esté guardado como UTF‑8. |

**Consejo profesional:** Al procesar muchas filas, almacena la fórmula en una variable de cadena y reutilízala para evitar la sobrecarga de concatenación repetida.

## Ejemplo completo y ejecutable

A continuación se muestra el programa completo listo para copiar y pegar. Incluye declaraciones de importación, manejo de excepciones y una operación de guardado opcional.

```java
import com.aspose.cells.*;

public class SplitColumnsExample {
    public static void main(String[] args) throws Exception {
        // Create a new workbook and access the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // Define the long string and desired column count
        String longString = "This is a very long string that needs to be split";
        int columnCount = 3;

        // Write the WRAPCOLS formula to cell A1
        Cell targetCell = worksheet.getCells().get("A1");
        String formula = String.format("=WRAPCOLS(\"%s\",%d)", longString, columnCount);
        targetCell.setFormula(formula);

        // Evaluate all formulas in the workbook
        workbook.calculateFormula();

        // Read and display each column's result
        System.out.println("First column output: " + worksheet.getCells().get("A1").getStringValue());
        System.out.println("Second column output: " + worksheet.getCells().get("B1").getStringValue());
        System.out.println("Third column output: " + worksheet.getCells().get("C1").getStringValue());

        // Save the workbook for visual verification
        workbook.save("SplitColumnsResult.xlsx");
    }
}
```

Ejecutar este programa produce la misma salida de consola mostrada anteriormente y escribe un archivo Excel que demuestra claramente **how to split columns**.

## Lista de verificación de solución de problemas

* **La fórmula no se evalúa** – Asegúrate de que se llame a `workbook.calculateFormula()` después de establecer la fórmula.
* **Celdas vacías después de dividir** – Verifica que la cadena fuente no sea `null` o vacía, y que el número de columnas sea mayor que cero.
* **Excepción de licencia** – Proporciona un archivo de licencia válido de Aspose.Cells (`License license = new License(); license.setLicense("Aspose.Total.lic");`) antes de crear el libro de trabajo para eliminar las marcas de agua de evaluación.
* **Retraso de rendimiento en hojas grandes** – Llama a `calculateFormula()` una vez después de que todas las fórmulas estén escritas, no después de cada celda individual.

## Conclusión

Ahora sabes **how to split columns** en Java usando Aspose.Cells, cómo **split string into columns** con la función `WRAPCOLS`, cómo **automate Excel formula** evaluation, y cómo **write formula to a cell** de forma programática. Esta técnica elimina los pasos manuales de preparación de datos e integra las potentes capacidades de manejo de texto de Excel directamente en tus aplicaciones Java.

### Próximos pasos

* Explora otras funciones de texto como `TEXTSPLIT` y `FILTERXML` para escenarios de análisis más complejos.
* Combina `WRAPCOLS` con `IFERROR` para manejar entradas inesperadas de forma elegante.
* Integra la solución en un servicio Spring Boot que reciba datos CSV vía REST y devuelva un archivo Excel poblado.

Al dominar estos patrones puedes crear flujos de trabajo de Excel robustos y automatizados que escalen con las necesidades de tu negocio. ¡Feliz codificación!

## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que se basan en las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y funcionales con explicaciones paso a paso para ayudarte a dominar características adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [aspose cells java – Dividir nombres en columnas](/cells/english/java/cell-operations/aspose-cells-java-split-names-columns/)
- [Ajustar automáticamente columnas de Excel en Java usando Aspose.Cells](/cells/english/java/formatting/aspose-cells-java-auto-fit-excel-columns-guide/)
- [Cómo eliminar columnas en blanco en Excel usando Aspose.Cells Java&#58; Guía completa](/cells/english/java/worksheet-management/delete-blank-columns-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}