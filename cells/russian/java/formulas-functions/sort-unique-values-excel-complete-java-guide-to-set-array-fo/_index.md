---
category: general
date: 2026-06-30
description: Сортировка уникальных значений в Excel с помощью Java. Узнайте, как задать
  формулу, пересчитать формулы и создать уникальный список в Excel с Aspose.Cells.
draft: false
keywords:
- sort unique values excel
- how to set formula
- how to recalculate formulas
- generate unique list excel
- set array formula
language: ru
og_description: Сортировка уникальных значений в Excel с помощью Java. Это руководство
  показывает, как задать формулу, пересчитать формулы и за несколько минут создать
  уникальный список в Excel.
og_title: Сортировка уникальных значений в Excel – Java‑урок по массивным формулам
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
title: Сортировка уникальных значений в Excel – Полное руководство по Java по установке
  массивных формул
url: /ru/java/formulas-functions/sort-unique-values-excel-complete-java-guide-to-set-array-fo/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Сортировка уникальных значений в Excel – Полное руководство по Java для **set array formula**

Когда‑то задавались вопросом, как **sort unique values Excel** без перетаскивания формул? Вы не одиноки. Во многих отчетных сценариях нужен чистый, отсортированный по алфавиту список уникальных записей, а делать это вручную — боль.

Хорошая новость? Пара строк Java‑кода позволяют **set array formula** на листе, а затем **recalculate formulas**, чтобы диапазон автоматически заполнился. В этом руководстве мы пройдем всё — от создания книги до генерации уникального списка в стиле Excel — чтобы вы могли сразу внедрить решение в своё приложение.

## Что покрывает это руководство

- Настройка Java‑проекта с Aspose.Cells (библиотека, используемая в коде).  
- Использование функций `SORT` и `UNIQUE` вместе для **generate unique list Excel**.  
- Программное применение **array formula** к ячейке.  
- Запуск расчёта, чтобы шаг **how to recalculate formulas** выполнился мгновенно.  
- Проверка результата и доработка решения для граничных случаев, таких как пустые ячейки или разрозненные диапазоны.

К концу этого руководства вы сможете добавить готовый метод в любой Java‑сервис, который экспортирует чистые Excel‑файлы.

> **Pro tip:** Если вы уже используете Maven, добавление Aspose.Cells в зависимости избавит вас от ручного управления JAR‑файлами.

---

## Предварительные требования

| Требование | Почему это важно |
|------------|------------------|
| Java 8 или новее | Aspose.Cells поддерживает Java 8+. |
| Maven (или Gradle) | Упрощает управление зависимостями. |
| Aspose.Cells for Java | Предоставляет `Workbook`, `Worksheet` и API формул, которые мы будем использовать. |
| Базовое знакомство с функциями Excel | Понимание `SORT` и `UNIQUE` поможет адаптировать код. |

> *Если у вас ещё нет Aspose.Cells, добавьте следующее в ваш `pom.xml`*:

```xml
<!-- Aspose.Cells for Java -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version> <!-- latest as of June 2026 -->
</dependency>
```

---

## Шаг 1: Создать новую книгу (здесь начинается **How to Set Formula**)

Сначала нам нужна пустая книга. Представьте её как чистый холст, где позже **set array formula** будет применена к ячейке `A1`.

```java
import com.aspose.cells.*;

public class UniqueSortExample {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook
        Workbook workbook = new Workbook();

        // The rest of the steps follow...
```

> *Зачем создавать новую книгу?*  
> Это гарантирует чистую среду, без скрытых формул, которые могли бы помешать нашим тестовым данным.

---

## Шаг 2: Заполнить примерными данными (необязательно, но полезно)

Чтобы чётко увидеть результат, заполним столбец **B** некоторыми дублирующимися записями.

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

> *Почему столбец B?*  
> Формула, которую мы напишем, ссылается на `B1:B10`, поэтому размещение данных здесь повторяет классический пример Excel.

---

## Шаг 3: Установить **array formula**, которое **Sort Unique Values Excel**

Теперь происходит магия. Мы комбинируем `UNIQUE` (удаление дубликатов) с `SORT` (сортировка по алфавиту). Получившееся выражение — **array formula**, т.е. оно «разольётся» в соседние ячейки автоматически.

```java
        // Step 3: Set an array formula that sorts the unique values from B1:B10
        // This is the core of “how to set formula” for our scenario.
        cells.get("A1").setFormulaArray("=SORT(UNIQUE(B1:B10))");
```

### Как это работает

- `UNIQUE(B1:B10)` сканирует диапазон и возвращает вертикальный массив уникальных строк.  
- `SORT(...)` берёт этот массив и упорядочивает его по возрастанию.  
- Оборачивание всего в `=` и вызов `setFormulaArray` сообщает Aspose.Cells трактовать результат как **spilled array**, как в Excel.

> **Примечание:** Если вы используете более старую версию Excel без `SORT` или `UNIQUE`, можно вернуться к `SORT(UNIQUE(...))` с функцией **LET** или использовать устаревшие массивные формулы (`=INDEX(...)`). В данном руководстве мы сосредоточены на современном подходе динамических массивов, потому что он самый простой способ **generate unique list Excel** сегодня.

---

## Шаг 4: Пересчитать формулы, чтобы заполнился разлитый диапазон

После установки формулы книга не вычисляет её автоматически. Здесь вступает в действие шаг **how to recalculate formulas**.

```java
        // Step 4: Recalculate formulas so the spilled range is populated automatically
        workbook.calculateFormula();
```

Вызов `calculateFormula()` заставляет Aspose.Cells запустить движок Excel, заполняя ячейки `A1`, `A2`, … отсортированными уникальными значениями.

> *Почему не полагаться на ленивое вычисление?*  
> В серверном контексте часто требуется, чтобы данные были готовы к экспорту (CSV, PDF и т.д.) сразу после расчёта, поэтому явный вызов гарантирует согласованность.

---

## Шаг 5: Проверить результат (необязательно, отладка)

Всегда полезно вывести разлитые значения в консоль — особенно когда вы только осваиваете новый API.

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

Запуск программы выводит:

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

Откройте `SortedUniqueValues.xlsx`, и вы увидите те же данные, «разлитыми» от `A1` вниз.

---

## Обработка граничных случаев

### Пустые ячейки в исходном диапазоне

Если `B1:B10` содержит пустые ячейки, `UNIQUE` будет рассматривать их как отдельный элемент. Чтобы игнорировать пустоты, оберните диапазон в `FILTER`:

```java
cells.get("A1").setFormulaArray("=SORT(UNIQUE(FILTER(B1:B10, B1:B10<>\"\")))");
```

### Разрозненные данные

Когда данные находятся в нескольких столбцах, их можно объединить с помощью `CHOOSE` или `TEXTJOIN` перед применением `UNIQUE`. Например:

```java
cells.get("A1").setFormulaArray(
    "=SORT(UNIQUE(CHOOSE({1,2}, B1:B10, C1:C10)))"
);
```

Эти доработки демонстрируют гибкость **how to set formula** для более сложных сценариев.

---

## Полный рабочий пример (все шаги вместе)

Ниже полностью готовая к запуску Java‑программа. Скопируйте её в IDE, добавьте зависимость Aspose.Cells и нажмите *Run*.

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

**Ожидаемый вывод** (в консоли) соответствует отсортированному, дедуплицированному списку, о котором шла речь. Открывая сгенерированный Excel‑файл, вы увидите те же значения, «разлитыми» от `A1` вниз.

---

## Часто задаваемые вопросы

**В: Работает ли это со старыми версиями Excel (pre‑Office 365)?**  
О: Функции `SORT` и `UNIQUE` входят в движок Dynamic Array, появившийся в Excel 365. Для более старых файлов придётся использовать классические массивные формулы вроде `{=INDEX(..., MATCH(0, COUNTIF($A$1:A1, $B$1:$B$10), 0))}`. Aspose.Cells может их вычислять, но синтаксис более громоздкий.

**В: Можно ли установить массивную формулу в диапазон, отличный от `A1`?**  
О: Конечно. Просто измените адрес в `cells.get("A1")`. Разлитый массив всегда начнётся с указанной ячейки и расширится вправо и вниз по необходимости.

**В: Что если мой исходный диапазон больше, чем `B1:B10`?**  
О: Замените статический диапазон на динамический, например `B:B` или именованный диапазон. Формула станет `=SORT(UNIQUE(B:B))`. Будьте осторожны с ссылками на весь столбец в очень больших листах — это может сказаться на производительности.

---

## Заключение

Мы рассмотрели, как **how to set formula** в Java для **sort unique values Excel**, как **recalculate formulas**, и как **generate unique list Excel** с помощью мощного API Aspose.Cells. Шаги просты: создать книгу, заполнить данными, применить массивную формулу, запустить расчёт и проверить результат.  

Отсюда вы можете расширять функциональность — добавить условное форматирование, экспорт в PDF или интегрировать метод в веб‑сервис, генерирующий готовые отчёты. Основная идея остаётся прежней: позволить функциям Excel выполнять тяжёлую работу, а Java — управлять процессом.

Готовы поднять автоматизацию Excel на новый уровень? Попробуйте заменить `SORT` на `SORTBY` для сортировки по второму столбцу или поэкспериментировать с `FILTER`, чтобы исключать строки, не соответствующие бизнес‑правилам. Возможностей практически бесконечно много.

---

###

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}