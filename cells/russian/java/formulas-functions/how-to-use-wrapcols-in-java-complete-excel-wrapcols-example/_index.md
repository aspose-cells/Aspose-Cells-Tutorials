---
category: general
date: 2026-06-21
description: Как использовать WRAPCOLS в Aspose.Cells Java для преобразования массива
  в строки, записи формулы в ячейку и заполнения ячеек формулой — пошаговое руководство.
draft: false
keywords:
- how to use wrapcols
- convert array to rows
- write formula to cell
- excel wrapcols example
- populate cells with formula
language: ru
og_description: Как использовать WRAPCOLS в Java с Aspose.Cells для преобразования
  массива в строки, записи формулы в ячейку и заполнения ячеек формулой — всё в одном
  руководстве.
og_title: Как использовать WRAPCOLS в Java – Полный пример WRAPCOLS в Excel
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: How to use WRAPCOLS with Aspose.Cells Java to convert array to rows,
    write formula to cell, and populate cells with formula – step‑by‑step guide.
  headline: How to Use WRAPCOLS in Java – Complete Excel WRAPCOLS Example
  type: TechArticle
- description: How to use WRAPCOLS with Aspose.Cells Java to convert array to rows,
    write formula to cell, and populate cells with formula – step‑by‑step guide.
  name: How to Use WRAPCOLS in Java – Complete Excel WRAPCOLS Example
  steps:
  - name: What the Formula Does
    text: '- `{1,2,3}` – a literal array containing three numbers. - `2` – the number
      of columns per row. - Result: - **A1** = 1, **B1** = 2 - **A2** = 3, **B2**
      = (blank)'
  - name: 1. Empty Arrays
    text: 'If the array literal is empty (`{}`), `WRAPCOLS` returns a `#VALUE!` error.
      To avoid breaking your sheet, guard the formula generation:'
  - name: 2. Non‑Numeric Data
    text: '`WRAPCOLS` works with text as well. For example, `WRAPCOLS({"A","B","C","D"},2)`
      produces a two‑column layout of strings. Just remember to quote strings inside
      the array literal.'
  - name: 3. Compatibility
    text: The `WRAPCOLS` function is available in Excel 365 and Excel 2019+ (Office
      2019, Excel for the web). If you need to support older versions, you’ll have
      to fall back to manual looping or use a different spill‑compatible function.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel formulas
- WRAPCOLS
title: Как использовать WRAPCOLS в Java – Полный пример WRAPCOLS в Excel
url: /ru/java/formulas-functions/how-to-use-wrapcols-in-java-complete-excel-wrapcols-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как использовать WRAPCOLS в Java – Полный пример Excel WRAPCOLS

Когда‑нибудь задавались вопросом **как использовать WRAPCOLS**, когда нужно преобразовать простой массив в аккуратную таблицу в Excel? Вы не одиноки. Многие разработчики сталкиваются с трудностями, впервые увидев функцию `WRAPCOLS` и подумав: «Как же записать эту формулу в ячейку из Java?» Хорошая новость? Всё довольно просто, как только вы знаете правильные шаги.

В этом руководстве мы пройдём полностью исполняемый пример Aspose.Cells для Java, который **преобразует массив в строки**, записывает формулу напрямую в ячейку и показывает, как **заполнять ячейки формулой** в реальных сценариях. К концу вы получите чёткое представление о **excel wrapcols example** и сможете адаптировать его под свои проекты.

## Prerequisites

Прежде чем начать, убедитесь, что у вас есть:

- Java 17 или новее (код работает с любой современной JDK).
- Библиотека Aspose.Cells для Java (можно взять последнюю JAR‑ку из Maven Central).
- Базовое понимание синтаксиса Java и формул Excel.
- IDE или простой текстовый редактор — никакие специальные инструменты не требуются.

Всё готово? Отлично, приступим.

## Step 1: Set Up the Project and Load a Workbook

Сначала — создайте новый проект Maven (или Gradle) и добавьте зависимость Aspose.Cells:

```xml
<!-- pom.xml snippet -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version> <!-- check for the latest version -->
</dependency>
```

Теперь мы можем загрузить существующую книгу (или создать новую) и получить первый лист:

```java
import com.aspose.cells.*;

public class WrapColsDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Load the workbook (or create a new one)
        Workbook wb = new Workbook();               // creates a blank workbook
        // Alternatively, load an existing file:
        // Workbook wb = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // Step 2: Access the first worksheet
        Worksheet ws = wb.getWorksheets().get(0);
```

> **Why we load a workbook** – Aspose.Cells работает с представлением Excel‑файла в памяти. Загрузив (или создав) книгу, мы получаем доступ к ячейкам, строкам и формулам, что необходимо для любой операции **write formula to cell**.

## Step 2: Insert the WRAPCOLS Formula into a Cell

Суть урока заключается в функции `WRAPCOLS`. Она принимает одномерный массив и «оборачивает» его в указанное количество столбцов, автоматически распределяя остаток по новым строкам. Вот синтаксис, который мы будем использовать:

```java
// Step 3: Set a formula that wraps a collection into rows of 2 columns
// The formula WRAPCOLS({1,2,3},2) will produce:
//   Row 1: 1, 2
//   Row 2: 3
ws.getCells().get("A1").setFormula("=WRAPCOLS({1,2,3},2)");
```

Обратите внимание, что формула передаётся как обычная строка в `setFormula`. Aspose.Cells делает всю тяжёлую работу — парсит формулу, вычисляет её и «разливает» результаты по листу. Это самый прямой способ **populate cells with formula** без ручного перебора строк и столбцов.

### What the Formula Does

- `{1,2,3}` – буквальный массив, содержащий три числа.
- `2` – количество столбцов в каждой строке.
- Результат:
  - **A1** = 1, **B1** = 2
  - **A2** = 3, **B2** = (пусто)

Если вам нужны три столбца, просто измените второй аргумент на `3`, и массив заполнит одну строку.

## Step 3: Save the Workbook and Verify the Output

Теперь, когда формула находится в **A1**, сохраним книгу на диск, чтобы вы могли открыть её в Excel и увидеть результат:

```java
        // (Optional) Save the workbook to see the result
        wb.save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

Откройте `output.xlsx`, и вы увидите именно то, о чём говорилось в комментарии — два столбца в первой строке и оставшееся значение во второй строке. Это суть **excel wrapcols example**.

## Step 4: Extending the Example – Converting Larger Arrays

В реальных проектах редко работают только с тремя числами. Предположим, у вас есть более крупная коллекция, например `{10,20,30,40,50,60,70}`, и вам нужны три столбца в каждой строке. Вот как нужно изменить код:

```java
String largeArray = "{10,20,30,40,50,60,70}";
int columnsPerRow = 3;
String formula = String.format("=WRAPCOLS(%s,%d)", largeArray, columnsPerRow);
ws.getCells().get("C5").setFormula(formula);
```

Теперь «разливание» начинается с **C5**, получая:

| C5 | D5 | E5 |
|----|----|----|
|10  |20  |30  |
|40  |50  |60  |
|70  |    |    |

Это демонстрирует, как можно **convert array to rows** динамически, просто изменив строку формулы. Без циклов, без ручных назначений ячеек — Aspose.Cells делает всё остальное.

## Step 5: Handling Edge Cases and Common Gotchas

### 1. Empty Arrays

Если литерал массива пуст (`{}`), `WRAPCOLS` возвращает ошибку `#VALUE!`. Чтобы не ломать лист, защитите генерацию формулы:

```java
if (arrayContent.isEmpty()) {
    ws.getCells().get("F1").setValue("No data");
} else {
    ws.getCells().get("F1").setFormula(formula);
}
```

### 2. Non‑Numeric Data

`WRAPCOLS` работает и с текстом. Например, `WRAPCOLS({"A","B","C","D"},2)` создаёт двухстолбцовое расположение строк. Просто не забудьте заключать строки в кавычки внутри литерала массива.

### 3. Compatibility

Функция `WRAPCOLS` доступна в Excel 365 и Excel 2019+ (Office 2019, Excel для веба). Если нужно поддерживать более старые версии, придётся использовать ручные циклы или другую функцию, совместимую с «spill».

## Step 6: Practical Tips and Pro Tricks

- **Pro tip:** Используйте `Cell.setFormulaLocal`, если нужен разделитель, зависящий от локали (запятая vs точка с запятой) в зависимости от региональных настроек пользователя.
- **Watch out for:** Перезапись существующих данных. Область «spill» заменит любой контент, уже находящийся в целевом диапазоне.
- **Performance note:** Установка формулы дешёва; основная нагрузка появляется при **save** или **recalculate** книги. Если генерируете тысячи формул, рассмотрите отключение автоматических вычислений (`wb.calculateFormula()` позже), чтобы ускорить обработку.

## Full Working Example

Ниже приведён полностью готовый к запуску Java‑класс, включающий всё, о чём мы говорили:

```java
import com.aspose.cells.*;

public class WrapColsDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Create a new workbook
        Workbook wb = new Workbook();

        // 2️⃣ Grab the first worksheet
        Worksheet ws = wb.getWorksheets().get(0);

        // 3️⃣ Simple WRAPCOLS formula – basic excel wrapcols example
        ws.getCells().get("A1").setFormula("=WRAPCOLS({1,2,3},2)");

        // 4️⃣ Larger array with three columns per row
        String largeArray = "{10,20,30,40,50,60,70}";
        int cols = 3;
        String largeFormula = String.format("=WRAPCOLS(%s,%d)", largeArray, cols);
        ws.getCells().get("C5").setFormula(largeFormula);

        // 5️⃣ Text array demonstration
        ws.getCells().get("G1").setFormula("=WRAPCOLS({\"Apple\",\"Banana\",\"Cherry\",\"Date\"},2)");

        // 6️⃣ Save the result
        wb.save("output.xlsx");
    }
}
```

**Expected output:** Откройте `output.xlsx`, и вы увидите три отдельные области «spill»:

- **A1:B2** — числа 1‑3, распределённые по двум столбцам.
- **C5:E7** — числа 10‑70, распределённые по трём столбцам.
- **G1:H2** — названия фруктов, распределённые по двум столбцам.

## Conclusion

Мы только что рассмотрели, **как использовать WRAPCOLS** с Aspose.Cells для Java, показав, как **convert array to rows**, **write formula to cell** и **populate cells with formula** чистым, повторяемым способом. Такой подход устраняет утомительные циклы, использует нативное «spill»‑поведение Excel и делает код лаконичным.

Готовы к следующему вызову? Попробуйте комбинировать `WRAPCOLS` с динамическими источниками данных — например, извлекать значения из базы, формировать строку массива «на лету» и позволять Excel заниматься раскладкой. Вы также можете поэкспериментировать с другими «spill»‑функциями, такими как `SEQUENCE` или `FILTER`, чтобы создавать ещё более богатые отчёты.

Если возникнут проблемы, оставьте комментарий ниже или изучите обширную документацию Aspose. Счастливого кодинга и наслаждайтесь мощью современных формул Excel прямо из Java! 

![how to use wrapcols example](/images/wrapcols-demo.png "how to use wrapcols in Java – screenshot of spilled data")


## What Should You Learn Next?

Следующие руководства охватывают тесно связанные темы, построенные на техниках, продемонстрированных в этом пособии. Каждый ресурс содержит полностью рабочие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы в своих проектах.

- [Как выбрать диапазоны ячеек в Excel с помощью Aspose.Cells для Java (руководство 2023)](/cells/english/java/range-management/aspose-cells-java-select-cell-ranges-excel/)
- [Как установить активную ячейку в Excel с помощью Aspose.Cells для Java: Полное руководство](/cells/english/java/cell-operations/aspose-cells-java-set-active-cell-excel/)
- [Как вставлять строки в рабочие книги Excel с помощью Aspose.Cells для Java](/cells/english/java/worksheet-management/aspose-cells-java-insert-rows-excel-workbooks/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}