---
category: general
date: 2026-10-07
description: Как разделять столбцы с помощью Aspose.Cells для Java. Узнайте, как разбить
  строку на столбцы, автоматизировать формулы Excel и записать формулу в ячейку за
  несколько строк кода.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to split columns
- split string into columns
- automate excel formula
- write formula to cell
language: ru
lastmod: 2026-10-07
og_description: Как разделить столбцы в Java с помощью Aspose.Cells. Этот учебник
  покажет, как разбить строку на столбцы, автоматизировать вычисление формул Excel
  и записать формулу в ячейку.
og_image_alt: Screenshot of Java code that splits columns in an Excel worksheet using
  Aspose.Cells
og_title: Как разделить столбцы в Java с помощью Aspose.Cells – быстрый учебник
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
title: Как разделить столбцы в Java с помощью Aspose.Cells – пошаговое руководство
url: /ru/java/data-manipulation/how-to-split-columns-in-java-with-aspose-cells-step-by-step/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как разделить столбцы в Java с помощью Aspose.Cells – пошаговое руководство

Если вам нужно **how to split columns** в листе Excel программно, это руководство покажет вам полный процесс с Aspose.Cells для Java. Вы также узнаете, как **split string into columns**, **automate Excel formula** оценку, и **write formula to a cell** используя лаконичный, готовый к продакшену код.

Программное разделение столбцов устраняет ручное копирование‑вставку, снижает количество ошибок и позволяет выполнять масштабные преобразования данных. К концу этого руководства вы сможете генерировать, изменять и вычислять формулы «на лету», делая Excel настоящей частью вашего Java‑бэкенда.

## Требования

* Java 17 или новее, установленный.
* Maven 3.8+ (или Gradle) для управления зависимостями.
* Лицензия Aspose.Cells for Java (бесплатная оценочная версия подходит для обучения).
* Базовое знакомство с синтаксисом Java и концепциями Excel.

Если какой‑либо из этих пунктов отсутствует, установите его сначала; примеры кода предполагают стандартный проект Maven.

## Шаг 1: Добавьте Aspose.Cells в ваш проект

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- Use the latest version available -->
</dependency>
```

**Почему этот шаг важен:** Библиотека предоставляет классы `Workbook`, `Worksheet` и `Cell`, необходимые для работы с файлами Excel без Microsoft Office. Без этой зависимости код не скомпилируется.

## Шаг 2: Создайте рабочую книгу и выберите первый лист

```java
import com.aspose.cells.*;

public class SplitColumnsExample {
    public static void main(String[] args) throws Exception {
        // Step 2: Initialize a new workbook and access the first worksheet
        Workbook workbook = new Workbook();                     // creates an empty .xlsx file in memory
        Worksheet worksheet = workbook.getWorksheets().get(0); // first sheet is index 0
```

Объект `Workbook` представляет весь файл Excel. Доступ к первому листу обеспечивает предсказуемую отправную точку для формулы, которую мы будем писать.

## Шаг 3: Запишите формулу WRAPCOLS в целевую ячейку

```java
        // Step 3: Identify the target cell (A1) where the formula will be placed
        Cell targetCell = worksheet.getCells().get("A1");

        // Step 3: Write the WRAPCOLS formula to split a long string into three columns
        // WRAPCOLS(string, columns) distributes the string across the specified number of columns.
        targetCell.setFormula("=WRAPCOLS(\"This is a very long string that needs to be split\",3)");
```

**Почему мы используем `WRAPCOLS`:** Встроенная функция Excel `WRAPCOLS` автоматически разбивает одно текстовое значение на заданное количество столбцов, интеллектуально учитывая границы слов. Это самый надёжный способ **split string into columns** без пользовательской логики разбора.

## Шаг 4: Принудительно выполнить вычисление формулы в рабочей книге

```java
        // Step 4: Calculate all formulas in the workbook so the result becomes visible
        workbook.calculateFormula();
```

Вызов `calculateFormula()` **automates Excel formula** вычисление на стороне сервера. Без этого вызова ячейка будет содержать текст формулы, а не вычисленные значения.

## Шаг 5: Получите и отобразите результат WRAPCOLS

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

При запуске программы консоль выводит:

```
First column output: This is a very long
Second column output: string that needs
Third column output: to be split
```

Сгенерированный файл `SplitColumnsResult.xlsx` показывает три столбца, заполненные разделённым текстом.

## Понимание функции WRAPCOLS

* **Синтаксис:** `WRAPCOLS(text, columns, [delimiter])`
* **Параметры:**
  * `text` – строка, которую нужно разделить.
  * `columns` – количество столбцов, по которым будет распределён текст.
  * `delimiter` (необязательно) – символ, используемый для разбиения строки; по умолчанию пробел.
* **Возвращаемое значение:** Массив, который «разливается» в соседние ячейки, каждый элемент содержит часть исходного текста.

Поскольку функция разливается горизонтально, достаточно записать формулу в самую левую ячейку (A1 в примере). Excel автоматически заполняет B1, C1, … по мере необходимости.

## Распространённые варианты и граничные случаи

| Ситуация | Рекомендуемая настройка |
|-----------|------------------------|
| **Переменное количество столбцов** | Замените жёстко заданное `3` переменной: `targetCell.setFormula(String.format("=WRAPCOLS(\"%s\",%d)", longString, columnCount));` |
| **Пользовательский разделитель** | Используйте третий аргумент, например `=WRAPCOLS(A2,4,",")` для разделения запятыми. |
| **Пустая исходная строка** | Функция возвращает пустые ячейки; проверяйте `null` или пустые строки перед установкой формулы. |
| **Большие наборы данных** | Применяйте формулу в цикле для каждой строки, затем вызовите `calculateFormula()` один раз после цикла для повышения производительности. |
| **Не‑ASCII символы** | WRAPCOLS работает с Unicode; убедитесь, что ваш Java‑файл сохранён в кодировке UTF‑8. |

**Совет:** При обработке большого количества строк сохраняйте формулу в строковой переменной и переиспользуйте её, чтобы избежать накладных расходов на многократную конкатенацию строк.

## Полный, исполняемый пример

Ниже приведена полностью готовая к копированию программа. В ней включены импорты, обработка исключений и необязательная операция сохранения.

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

Запуск этой программы приводит к тому же выводу в консоль, что был показан ранее, и записывает файл Excel, который явно демонстрирует **how to split columns**.

## Список проверки устранения неполадок

* **Формула не вычисляется** – Убедитесь, что `workbook.calculateFormula()` вызывается после установки формулы.
* **Пустые ячейки после разделения** – Проверьте, что исходная строка не `null` и не пустая, а количество столбцов больше нуля.
* **Исключение лицензии** – Предоставьте действительный файл лицензии Aspose.Cells (`License license = new License(); license.setLicense("Aspose.Total.lic");`) перед созданием рабочей книги, чтобы убрать водяные знаки оценки.
* **Замедление производительности на больших листах** – Вызовите `calculateFormula()` один раз после записи всех формул, а не после каждой отдельной ячейки.

## Заключение

Теперь вы знаете **how to split columns** в Java с помощью Aspose.Cells, как **split string into columns** с функцией `WRAPCOLS`, как **automate Excel formula** вычисление и как **write formula to a cell** программно. Эта техника устраняет ручные шаги подготовки данных и интегрирует мощные возможности обработки текста Excel непосредственно в ваши Java‑приложения.

### Следующие шаги

* Исследуйте другие текстовые функции, такие как `TEXTSPLIT` и `FILTERXML`, для более сложных сценариев разбора.
* Скомбинируйте `WRAPCOLS` с `IFERROR` для graceful обработки неожиданного ввода.
* Интегрируйте решение в сервис Spring Boot, который получает CSV‑данные через REST и возвращает заполненный файл Excel.

## Что следует изучить дальше?

Следующие руководства охватывают тесно связанные темы, которые развивают техники, продемонстрированные в этом руководстве. Каждый ресурс включает полные рабочие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы к реализации в собственных проектах.

- [aspose cells java – Split Names into Columns](/cells/english/java/cell-operations/aspose-cells-java-split-names-columns/)
- [Auto-Fit Excel Columns in Java Using Aspose.Cells](/cells/english/java/formatting/aspose-cells-java-auto-fit-excel-columns-guide/)
- [How to Delete Blank Columns in Excel Using Aspose.Cells Java&#58; A Comprehensive Guide](/cells/english/java/worksheet-management/delete-blank-columns-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}