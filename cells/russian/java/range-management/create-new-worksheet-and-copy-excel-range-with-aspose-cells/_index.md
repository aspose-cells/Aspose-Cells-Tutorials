---
category: general
date: 2026-09-11
description: Создайте новый лист и скопируйте диапазон Excel с помощью Aspose.Cells.
  Узнайте, как копировать диапазон между листами, сохраняя сводные таблицы.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create new worksheet
- copy excel range
- copy range between sheets
- copy range aspose.cells
language: ru
lastmod: 2026-09-11
og_description: Создайте новый лист и скопируйте диапазон Excel с помощью Aspose.Cells.
  Этот учебник показывает точные шаги копирования диапазона между листами и сохранения
  сводных таблиц без изменений.
og_image_alt: Screenshot of a Java IDE showing code that creates a new worksheet and
  copies an Excel range
og_title: Создание нового листа и копирование диапазона Excel – руководство Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-09-11'
  description: Create new worksheet and copy Excel range using Aspose.Cells. Learn
    how to copy range between sheets while preserving pivot tables.
  headline: Create new worksheet and copy Excel range with Aspose.Cells
  type: TechArticle
- questions:
  - answer: The `copy` method also copies merge information, so merged cells appear
      unchanged on the destination sheet.
    question: What if the source range contains merged cells?
  - answer: Yes. Load a second `Workbook` instance, create a destination range in
      that workbook, and call `sourceRange.copy(destinationRange)`. The method handles
      cross‑workbook copying automatically.
    question: Can I copy to a different workbook?
  - answer: The copy operation overwrites any existing cells that intersect the destination
      range. To avoid data loss, ensure the destination area is empty or use a different
      start cell (e.g., `"B2"`).
    question: What if the destination sheet already has data?
  - answer: Aspose.Cells reuses the original pivot cache, which means the new pivot
      table remains linked to the same source data. If you need an independent cache,
      you must recreate the pivot table after copying.
    question: Is the pivot cache duplicated?
  type: FAQPage
tags:
- Aspose.Cells
- Excel automation
- Java
title: Создать новый рабочий лист и скопировать диапазон Excel с помощью Aspose.Cells
url: /ru/java/range-management/create-new-worksheet-and-copy-excel-range-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Создать новый лист и скопировать диапазон Excel с помощью Aspose.Cells

Если вам нужно **create new worksheet** и перемещать данные в файле Excel, Aspose.Cells делает это простым. Это руководство показывает, как точно скопировать диапазон Excel с одного листа на другой, сохраняя любые сводные таблицы внутри диапазона.

Вы узнаете, как **copy excel range**, как **copy range between sheets**, и почему метод `copy` в Aspose.Cells сохраняет определения сводных таблиц. Не требуются внешние инструменты — только Java‑проект с библиотекой Aspose.Cells.

## Предварительные требования

- Установлен Java 17 или новее
- Aspose.Cells for Java (версия 23.12 или новее), добавленная в classpath вашего проекта
- Исходная рабочая книга (`input.xlsx`), содержащая сводную таблицу в диапазоне, который вы хотите скопировать
- Базовое знакомство с синтаксисом Java и управлением зависимостями Maven/Gradle

## Шаг 1: Настройте проект и импортируйте Aspose.Cells

Создайте простой Maven‑проект (или Gradle, если предпочитаете) и добавьте зависимость Aspose.Cells:

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version>
</dependency>
```

Затем импортируйте необходимые классы в ваш Java‑файл:

```java
import com.aspose.cells.*;
import java.io.IOException;
```

*Почему этот шаг важен*: Импорт правильных классов дает доступ к `Workbook`, `Worksheet`, `Range` и методу `copy`, который будет выполнять передачу диапазона.

## Шаг 2: Загрузите исходную рабочую книгу

Откройте рабочую книгу, содержащую данные, которые вы хотите скопировать. Следующий код загружает `input.xlsx` из указанного вами каталога:

```java
public class ExcelRangeCopy {
    public static void main(String[] args) throws IOException {
        // Load the source workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

*Объяснение*: `Workbook` представляет весь файл Excel. Однократная загрузка предоставляет доступ к чтению/записи всех листов и коллекций ячеек.

## Шаг 3: Определите исходный диапазон, включающий сводную таблицу

Выберите лист, содержащий сводную таблицу, и задайте точный блок ячеек, который хотите скопировать. В этом примере мы копируем ячейки A1‑D20:

```java
        // Get the first worksheet (index 0) that contains the pivot table
        Worksheet sourceSheet = workbook.getWorksheets().get(0);

        // Define the source range – this range includes the pivot table
        Range sourceRange = sourceSheet.getCells().createRange("A1:D20");
```

*Почему это важно*: Создавая объект `Range`, вы точно указываете Aspose.Cells, какие ячейки (включая встроенные объекты, такие как сводные таблицы) следует дублировать.

## Шаг 4: **Create new worksheet**, который получит скопированные данные

Теперь мы добавляем новый лист в ту же рабочую книгу. Здесь появляется основной ключевой запрос:

```java
        // Create a new worksheet named "Copy"
        Worksheet destinationSheet = workbook.getWorksheets().add("Copy");

        // Define the top‑left cell of the destination range
        Range destinationRange = destinationSheet.getCells().createRange("A1");
```

*Объяснение*: Добавление нового листа изолирует скопированные данные, упрощая проверку того, что операция **copy excel range** выполнена успешно и не затронула оригинальный лист.

## Шаг 5: Скопировать диапазон — сводная таблица сохраняется автоматически

Используйте метод `copy` для перемещения диапазона с исходного листа на лист назначения. Aspose.Cells копирует формулы, форматирование и определения сводных таблиц:

```java
        // Copy the range – the pivot table inside the range is preserved
        sourceRange.copy(destinationRange);
```

*Почему это работает*: Метод `copy` выполняет глубокое копирование исходных ячеек. Он копирует не только значения, а воспроизводит всю структуру ячеек, включая кэш сводных таблиц. Поэтому вы можете **copy range aspose.cells** и по‑прежнему видеть рабочую сводную таблицу на новом листе.

## Шаг 6: Сохраните рабочую книгу с новым листом

Наконец, запишите изменённую рабочую книгу на диск:

```java
        // Save the workbook with the copied data
        workbook.save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

*Результат*: `output.xlsx` теперь содержит оригинальный лист плюс новый лист под названием **Copy**, в котором находится точно такой же диапазон, включая сводную таблицу.

## Полный рабочий пример

Объединив все части, представляем полный, исполняемый пример программы:

```java
import com.aspose.cells.*;
import java.io.IOException;

public class ExcelRangeCopy {
    public static void main(String[] args) throws IOException {
        // Step 1: Load the source workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // Step 2: Get the worksheet that contains the pivot table and define the source range
        Worksheet sourceSheet = workbook.getWorksheets().get(0);
        Range sourceRange = sourceSheet.getCells().createRange("A1:D20");

        // Step 3: Create a new worksheet that will receive the copied range
        Worksheet destinationSheet = workbook.getWorksheets().add("Copy");
        Range destinationRange = destinationSheet.getCells().createRange("A1");

        // Step 4: Copy the range – the pivot table inside the range is preserved
        sourceRange.copy(destinationRange);

        // Step 5: Save the workbook with the copied data
        workbook.save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

**Ожидаемый результат**: Откройте `output.xlsx` в Excel. Вы увидите лист с именем **Copy**, ячейки A1:D20 которого содержат те же данные, форматирование и активную сводную таблицу, идентичную оригиналу.

## Часто задаваемые вопросы и особые случаи

- **Что если исходный диапазон содержит объединённые ячейки?**  
  Метод `copy` также копирует информацию об объединении, поэтому объединённые ячейки остаются без изменений на листе назначения.

- **Можно ли копировать в другую рабочую книгу?**  
  Да. Загрузите второй экземпляр `Workbook`, создайте диапазон назначения в этой книге и вызовите `sourceRange.copy(destinationRange)`. Метод автоматически обрабатывает копирование между книгами.

- **Что если на листе назначения уже есть данные?**  
  Операция копирования перезапишет любые существующие ячейки, пересекающиеся с диапазоном назначения. Чтобы избежать потери данных, убедитесь, что область назначения пуста, либо используйте другую начальную ячейку (например, `"B2"`).

- **Дублируется ли кэш сводной таблицы?**  
  Aspose.Cells повторно использует оригинальный кэш сводной таблицы, что означает, что новая сводная таблица остаётся связанной с теми же исходными данными. Если нужен независимый кэш, необходимо воссоздать сводную таблицу после копирования.

## Советы и лучшие практики

- **Pro tip**: Используйте `Workbook.setForceFormulaRecalculation(true)` перед сохранением, если ваш диапазон содержит формулы, зависящие от данных за пределами скопированного блока.
- **Watch out for** большие диапазоны: копирование огромных листов может потреблять значительное количество памяти. Рассмотрите возможность копирования небольшими частями, если возникает `OutOfMemoryError`.
- **Performance tip**: Отключите обновление экрана (`workbook.getSettings().setCalculateFormulaOnOpen(false)`) при работе с очень большими файлами, чтобы ускорить процесс копирования.

## Заключение

Теперь вы знаете, как **create new worksheet** и **copy excel range** между листами с помощью Aspose.Cells, сохраняя сводные таблицы и все атрибуты ячеек. Эта техника позволяет программно дублировать блоки данных, создавать шаблоны отчётов или перестраивать рабочие книги без ручного копирования‑вставки.

Далее изучайте связанные темы, такие как **copy range aspose.cells** для операций между книгами, автоматизацию обновления сводных таблиц или экспорт скопированного листа в PDF. Экспериментируйте с различными исходными диапазонами и именами листов, чтобы адаптировать их к вашему сценарию автоматизации. Приятного кодинга!

## Что следует изучить дальше?

Следующие руководства охватывают тесно связанные темы, которые развивают техники, продемонстрированные в этом руководстве. Каждый ресурс включает полные рабочие примеры кода с пошаговыми объяснениями, помогая вам освоить дополнительные возможности API и исследовать альтернативные подходы к реализации в ваших проектах.

- [Копирование фигур между листами Excel с помощью Aspose.Cells для .NET: Полное руководство](/cells/english/net/images-shapes/copy-shapes-between-sheets-aspose-cells-dotnet/)
- [Копирование изображений между листами в Excel с помощью Aspose.Cells для Java: Полное руководство](/cells/english/java/images-shapes/copy-images-between-sheets-excel-aspose-cells-java/)
- [Excel Aspose Cells .NET Копирование данных диапазона](/cells/hindi/net/range-management/excel-aspose-cells-dotnet-copy-range-data/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}