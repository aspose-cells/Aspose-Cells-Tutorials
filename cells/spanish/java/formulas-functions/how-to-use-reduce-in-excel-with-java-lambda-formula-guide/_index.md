---
category: general
date: 2026-06-08
description: Cómo usar reduce en Excel con Java usando Aspose.Cells. Aprende la fórmula
  lambda en Excel, matrices dinámicas en Java, cómo escribir lambda y sumar con reduce
  en un tutorial claro paso a paso.
draft: false
keywords:
- how to use reduce
- lambda formula excel
- dynamic arrays java
- how to write lambda
- sum with reduce
language: es
og_description: Cómo usar reduce en Excel con Java. Domina la fórmula lambda en Excel,
  los arrays dinámicos en Java y la suma con reduce usando un ejemplo completo y ejecutable.
og_title: Cómo usar Reduce en Excel con Java – Guía de fórmulas Lambda
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: How to use reduce in Excel with Java using Aspose.Cells. Learn lambda
    formula Excel, dynamic arrays java, how to write lambda, and sum with reduce in
    a clear step‑by‑step tutorial.
  headline: How to Use Reduce in Excel with Java – Lambda Formula Guide
  type: TechArticle
- description: How to use reduce in Excel with Java using Aspose.Cells. Learn lambda
    formula Excel, dynamic arrays java, how to write lambda, and sum with reduce in
    a clear step‑by‑step tutorial.
  name: How to Use Reduce in Excel with Java – Lambda Formula Guide
  steps:
  - name: What if I need a horizontal array instead of vertical?
    text: 'Swap the column/row arguments in `EXPAND`. For a horizontal spill across
      B1:F1:'
  - name: Can I use REDUCE to multiply instead of sum?
    text: 'Absolutely. Just change the lambda body:'
  - name: Does Aspose.Cells support custom LAMBDA functions?
    text: Yes, you can define named LAMBDA functions via the workbook’s `Names` collection,
      then call them like any built‑in formula. That’s a deeper dive for a later tutorial
      on **how to write lambda** functions that live beyond a single cell.
  - name: What about older Excel versions that don’t recognize REDUCE?
    text: If you target Excel 2019 or earlier, the engine will return `#NAME?`. In
      such cases
  type: HowTo
tags:
- Excel
- Java
- Aspose.Cells
title: Cómo usar Reduce en Excel con Java – Guía de fórmulas Lambda
url: /es/java/formulas-functions/how-to-use-reduce-in-excel-with-java-lambda-formula-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo usar Reduce en Excel con Java – Guía de Fórmulas Lambda

¿Alguna vez te has preguntado **cómo usar reduce** en Excel cuando estás escribiendo código Java? No estás solo. Muchos desarrolladores se topan con un obstáculo al intentar combinar las nuevas funciones de matrices dinámicas de Excel con la automatización basada en Java, y la respuesta no es tan críptica como parece al principio.

En este tutorial recorreremos un ejemplo concreto que muestra **cómo usar reduce** junto con una **lambda formula Excel**, todo impulsado por la biblioteca Aspose.Cells for Java. Al final podrás generar matrices dinámicas en Java, escribir funciones lambda y calcular una **suma con reduce**, sin necesidad de manipular manualmente la hoja de cálculo.

---

## Lo que construirás

- Un libro nuevo creado completamente desde Java.  
- Una matriz dinámica **EXPAND** que llena las celdas A1:A5 con los números 1‑5.  
- Una fórmula **REDUCE** que suma esos números usando una **lambda formula Excel**.  
- Un archivo `.xlsx` guardado que puedes abrir en cualquier programa de hojas de cálculo para verificar el resultado.

Sin macros externas, sin VBA—solo código Java puro y las funciones modernas de Excel.

---

## Requisitos previos

- Java 17 (o cualquier JDK reciente) – versiones anteriores funcionan pero perderás la azúcar de `var`.  
- Aspose.Cells for Java (la prueba gratuita funciona bien para esta demo).  
- Familiaridad básica con la sintaxis de Java y las fórmulas de Excel.  

Si eres nuevo en **dynamic arrays java**, no te preocupes—esta guía explica cada pieza.

---

## Paso 1: Configura tu proyecto e importa Aspose.Cells

Lo primero, añade la dependencia de Aspose.Cells en tu `pom.xml` (o descarga el JAR manualmente).

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- latest as of June 2026 -->
</dependency>
```

> **Consejo profesional:** Mantén tus dependencias actualizadas; las versiones más recientes mejoran la velocidad de evaluación de fórmulas, lo que importa cuando estás **how to use reduce** en hojas grandes.

---

## Paso 2: Crea un Workbook y accede a la primera Worksheet

Ahora crearemos un libro totalmente nuevo. Esta es la base para aprender **how to use reduce** porque el objeto workbook nos brinda un sandbox donde colocar fórmulas.

```java
// Step 2: Initialize a new workbook and grab the first sheet
Workbook workbook = new Workbook();                     // creates an empty .xlsx in memory
Worksheet worksheet = workbook.getWorksheets().get(0); // first (and only) sheet by default
```

*Por qué importa:* La clase `Workbook` abstrae todo el archivo Excel, mientras que `Worksheet` representa una sola pestaña. Más adelante verás cómo **dynamic arrays java** pueden llenar muchas celdas a partir de una única fórmula colocada en A1.

---

## Paso 3: Genera una matriz vertical con EXPAND

La función `EXPAND` de Excel puede derramar valores en un rango. La usaremos para crear los números 1 hasta 5 en la columna A.

```java
// Step 3: Write an EXPAND formula to produce 1‑5 vertically
Cell expandCell = worksheet.getCells().get("A1");
expandCell.setFormula("=EXPAND({1},5,1)"); // {1} is the seed, 5 rows, 1 column
expandCell.calculate(); // forces the engine to evaluate the formula now
```

Si abres el libro resultante, las celdas A1:A5 mostrarán 1, 2, 3, 4, 5. Esta es la parte de **dynamic arrays java**—una fórmula que rellena todo un rango.

---

## Paso 4: Escribe una lambda REDUCE para sumar la matriz

Aquí respondemos la pregunta central: **how to use reduce** en Excel desde Java. La función `REDUCE` itera sobre una matriz, aplicando una lambda que tú proporcionas. En nuestro caso sumaremos los números.

```java
// Step 4: Use REDUCE with a LAMBDA to compute the sum of A1:A5
Cell reduceCell = worksheet.getCells().get("B1");
reduceCell.setFormula(
    "=REDUCE(0, A1:A5, LAMBDA(acc, x, acc + x))"
);
reduceCell.calculate(); // forces evaluation immediately
```

Desglosemos:

- `0` – el valor inicial del acumulador (`acc`).  
- `A1:A5` – la matriz que generamos con **EXPAND**.  
- `LAMBDA(acc, x, acc + x)` – la **lambda formula Excel** que suma cada elemento (`x`) al acumulador (`acc`).  

Cuando la fórmula se ejecuta, `B1` termina conteniendo **15**, la **sum with reduce** de los números 1‑5.

> **¿Cómo escribir lambda** en Excel? Piensa en ella como una función anónima donde los primeros argumentos son los parámetros y la expresión final es el valor de retorno. En Java simplemente incrustamos el texto; el motor de Excel hace el trabajo pesado.

---

## Paso 5: Guarda el Workbook

Finalmente, persistimos el libro en disco para que puedas abrirlo en Excel, Google Sheets o cualquier visor que soporte `.xlsx`.

```java
// Step 5: Persist the workbook
String outputPath = "YOUR_DIRECTORY/new-functions.xlsx";
workbook.save(outputPath);
System.out.println("Workbook saved to " + outputPath);
```

Abre el archivo y verás:

| A | B |
|---|---|
| 1 | 15 |
| 2 |   |
| 3 |   |
| 4 |   |
| 5 |   |

La **sum with reduce** aparece en B1, confirmando que hemos demostrado con éxito **how to use reduce** junto con una **lambda formula Excel** desde Java.

---

## Ejemplo completo y funcional

A continuación tienes el programa Java completo, listo para ejecutar. Copia‑pega en tu IDE, ajusta el directorio de salida y pulsa **Run**.

```java
import com.aspose.cells.*;

public class ReduceLambdaDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Create workbook & get first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // 2️⃣ EXPAND – generate vertical array 1‑5 in A1:A5
        Cell expandCell = worksheet.getCells().get("A1");
        expandCell.setFormula("=EXPAND({1},5,1)");
        expandCell.calculate(); // evaluate now

        // 3️⃣ REDUCE – sum the values using a lambda
        Cell reduceCell = worksheet.getCells().get("B1");
        reduceCell.setFormula("=REDUCE(0, A1:A5, LAMBDA(acc, x, acc + x))");
        reduceCell.calculate(); // evaluate now

        // 4️⃣ Save the workbook
        String outPath = "new-functions.xlsx";
        workbook.save(outPath);
        System.out.println("Workbook created at: " + outPath);
    }
}
```

**Salida esperada** al abrir `new-functions.xlsx`:

- Las celdas **A1:A5** contienen `1, 2, 3, 4, 5`.  
- La celda **B1** muestra `15`, confirmando la **sum with reduce**.

---

## Preguntas frecuentes y casos límite

### ¿Qué pasa si necesito una matriz horizontal en lugar de vertical?

Intercambia los argumentos de columna/fila en `EXPAND`. Para un derrame horizontal en B1:F1:

```java
expandCell.setFormula("=EXPAND({1},1,5)");
```

### ¿Puedo usar REDUCE para multiplicar en lugar de sumar?

Claro. Sólo cambia el cuerpo de la lambda:

```java
reduceCell.setFormula("=REDUCE(1, A1:A5, LAMBDA(acc, x, acc * x))");
```

Ahora B1 mostrará `120` (5 ! = 120).

### ¿Aspose.Cells admite funciones LAMBDA personalizadas?

Sí, puedes definir funciones LAMBDA nombradas mediante la colección `Names` del libro, y luego llamarlas como cualquier fórmula incorporada. Eso es un tema más profundo para un tutorial futuro sobre **how to write lambda** functions que vivan más allá de una sola celda.

### ¿Qué ocurre con versiones antiguas de Excel que no reconocen REDUCE?

Si apuntas a Excel 2019 o anterior, el motor devolverá `#NAME?`. En esos casos


## ¿Qué deberías aprender a continuación?


Los tutoriales siguientes cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos con explicaciones paso a paso para ayudarte a dominar características adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Mastering Aspose.Cells Java: How to Interrupt Formula Calculation in Excel Workbooks](/cells/english/java/calculation-engine/master-aspose-cells-java-interrupt-formula-calculation-workbook/)
- [How to Convert Excel Cell Names to Indices Using Aspose.Cells for Java: A Step-by-Step Guide](/cells/english/java/cell-operations/convert-excel-cell-names-to-indices-aspose-cells-java/)
- [How to Create & Format Excel Cells Using Aspose.Cells for Java: A Step-by-Step Guide](/cells/english/java/formatting/aspose-cells-java-excel-automation-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}