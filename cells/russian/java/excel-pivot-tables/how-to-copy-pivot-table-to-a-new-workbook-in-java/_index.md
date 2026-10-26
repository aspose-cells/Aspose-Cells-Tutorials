---
category: general
date: 2026-10-26
description: Узнайте, как скопировать сводную таблицу в новую книгу с помощью Java,
  сохранив форматирование и определение сводной таблицы, при копировании диапазона
  Excel с форматированием через Aspose.Cells.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy pivot table
- how to copy pivot
- copy excel range
- create empty workbook
- copy range with formatting
language: ru
lastmod: 2026-10-26
og_description: Копировать сводную таблицу в новую книгу в Java с Aspose.Cells. Это
  руководство показывает, как копировать диапазон Excel, сохранять форматирование
  и эффективно создавать пустую книгу.
og_image_alt: Screenshot of a Java program that copies a pivot table to a new Excel
  workbook
og_title: Копировать сводную таблицу в новую книгу в Java – пошаговое руководство
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Learn how to copy pivot table to a new workbook using Java, preserving
    formatting and the pivot definition while you copy excel range with formatting
    via Aspose.Cells.
  headline: How to copy pivot table to a new workbook in Java
  type: TechArticle
- description: Learn how to copy pivot table to a new workbook using Java, preserving
    formatting and the pivot definition while you copy excel range with formatting
    via Aspose.Cells.
  name: How to copy pivot table to a new workbook in Java
  steps:
  - name: Prerequisites
    text: '* Java 17 or later. * Aspose.Cells for Java (version 23.10 or newer). *
      Basic familiarity with Java IDEs (IntelliJ IDEA, Eclipse, etc.).'
  - name: Why this works
    text: '* `new Workbook()` **creates empty workbook** with a default sheet, avoiding
      the need to delete existing data. * `CopyOptions` tells Aspose.Cells to copy
      **pivot table** metadata, not just raw values. The `PASTE_ALL` mode also carries
      cell styles, number formats, and conditional formatting—fulfillin'
  - name: Edge cases to consider
    text: '| Situation | Recommended handling | |----------------------------------------|----------------------|
      | Source workbook has multiple pivots | Copy each pivot’s range separately or
      copy the whole sheet. | | Destination already contains data | Choose a non‑conflicting
      start cell (e.g., "H1") when cal'
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: Как скопировать сводную таблицу в новую рабочую книгу в Java
url: /ru/java/excel-pivot-tables/how-to-copy-pivot-table-to-a-new-workbook-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как скопировать сводную таблицу в новую книгу Excel на Java

Если вам нужно **скопировать сводную таблицу** из одного файла Excel в другой, это руководство покажет полное, готовое к запуску решение. Вы увидите, как сохранить определение сводной таблицы, сохранить всё форматирование и избежать распространённых подводных камней при копировании диапазона Excel.

Копирование сводной таблицы часто вызывает вопросы вроде *как скопировать сводную* без разрушения источника данных или потери стилей. К концу этого урока у вас будет автономная Java‑программа, которая создаёт пустую книгу, копирует нужный диапазон и сохраняет результат со сводной таблицей в неизменном виде.

## Что вы достигнете

* Загрузить исходную книгу, содержащую сводную таблицу.  
* **Create empty workbook**, которая получит скопированные данные.  
* **Copy excel range**, включающий сводную таблицу, используя параметры, сохраняющие сводную и форматирование.  
* Сохранить файл назначения и убедиться, что сводная работает точно так же, как оригинал.

### Предварительные требования

* Java 17 или новее.  
* Aspose.Cells for Java (версия 23.10 или новее).  
* Базовое знакомство с Java‑IDE (IntelliJ IDEA, Eclipse и т.п.).  

> **Pro tip:** Используйте бесплатную оценочную лицензию Aspose.Cells для быстрой проверки; замените её полной лицензией перед использованием в продакшене.

## Копирование сводной таблицы в новую книгу

Первый шаг — настроить исходную и целевую книги. Целевая начинается как вызов **create empty workbook**, который даёт чистый файл с единственным листом.

```java
import com.aspose.cells.*;

public class CopyPivotExample {
    public static void main(String[] args) throws Exception {
        // Load the source workbook that holds the pivot table
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/source.xlsx");

        // Create an empty workbook that will receive the copied range
        Workbook destWb = new Workbook();

        // Get the first worksheet from each workbook
        Worksheet srcSheet = srcWb.getWorksheets().get(0);
        Worksheet destSheet = destWb.getWorksheets().get(0);

        // Configure copy options to preserve the pivot table and formatting
        CopyOptions copyOptions = new CopyOptions();
        copyOptions.setPasteType(PasteType.PASTE_ALL); // ensures pivot and styles are kept

        // Copy the range that contains the pivot table
        srcSheet.getCells().copyRange("A1:D20", destSheet.getCells(), "A1", copyOptions);

        // Save the destination workbook
        destWb.save("YOUR_DIRECTORY/destination.xlsx");
    }
}
```

### Почему это работает

* `new Workbook()` **creates empty workbook** с листом по умолчанию, избегая необходимости удалять существующие данные.  
* `CopyOptions` указывает Aspose.Cells копировать метаданные **pivot table**, а не только сырые значения. Режим `PASTE_ALL` также переносит стили ячеек, числовые форматы и условное форматирование — удовлетворяя требование **copy range with formatting**.  
* `copyRange` выполняет операцию **copy excel range**, учитывающую внутренние структуры источника, поэтому сводная остаётся функциональной после копирования.

## Как скопировать сводную таблицу без потери форматирования

Если использовать только параметры по умолчанию `CopyOptions`, часть информации о стиле может быть опущена в старых версиях Aspose.Cells. Явное указание типа вставки гарантирует, что **copy range with formatting** будет соблюдено.

```java
CopyOptions copyOptions = new CopyOptions();
copyOptions.setPasteType(PasteType.PASTE_ALL);          // copy values, formulas, formats
copyOptions.setPasteSpecialType(PasteSpecialType.ALL); // include column widths and row heights
```

Добавление `setPasteSpecialType` гарантирует, что ширины столбцов, высоты строк и даже правила проверки данных перейдут вместе с диапазоном. Это особенно полезно, когда сводная таблица охватывает несколько столбцов с пользовательскими ширинами.

## Создание пустой книги перед копированием

Иногда разработчики пытаются копировать в уже существующую книгу, содержащую данные. Это может привести к перекрытию диапазонов или неожиданным перезаписям. Начало с вызова **create empty workbook** изолирует операцию:

```java
Workbook destWb = new Workbook(); // fresh file with one sheet
Worksheet destSheet = destWb.getWorksheets().get(0); // reference the clean sheet
```

Если вам нужно более одного листа в целевом файле, их можно добавить после копирования:

```java
destWb.getWorksheets().add("Summary");
```

## Копирование диапазона Excel с форматированием с помощью CopyOptions

Помимо сводных таблиц, тот же шаблон работает для любого **copy excel range**, требующего сохранения форматирования — диаграмм, таблиц или условных форматов.

```java
// Example: copy a styled table from A1 to G15
srcSheet.getCells().copyRange("A1:G15", destSheet.getCells(), "A1", copyOptions);
```

Экземпляр `CopyOptions` остаётся тем же, поэтому вы получаете согласованное поведение для разных диапазонов.

### Пограничные случаи, которые следует учитывать

| Ситуация                              | Рекомендованное решение |
|----------------------------------------|--------------------------|
| В исходной книге несколько сводных таблиц   | Скопировать диапазон каждой сводной таблицы отдельно или скопировать весь лист. |
| В целевой книге уже есть данные      | Выберите непересекающуюся начальную ячейку (например, "H1") при вызове `copyRange`. |
| Источник данных сводной таблицы внешний (например, БД) | Убедитесь, что целевая книга ссылается на тот же внешний источник данных, или обновите сводную таблицу после копирования. |
| Большая книга (> 10 МБ )             | Увеличьте размер кучи Java (`-Xmx2g`), чтобы избежать `OutOfMemoryError`. |

## Проверка результата

После запуска программы откройте `destination.xlsx`. Вы должны увидеть:

* Тот же макет сводной таблицы, что и в `source.xlsx`.  
* Все цвета ячеек, числовые форматы и ширины столбцов сохранены.  
* Источник данных сводной таблицы по‑прежнему указывает на оригинальный диапазон внутри нового файла, поэтому обновление сводной корректно пересчитывает значения.

Если сводная отображается как статическая таблица, проверьте, что установлен `CopyOptions.setPasteType(PasteType.PASTE_ALL)`. Без этой опции Aspose.Cells рассматривает сводную как обычные данные.

## Заключение

Теперь вы знаете, как **copy pivot table** в новую книгу Excel на Java, сохраняя форматирование, соединения данных и макет листа. Полное решение демонстрирует загрузку исходного файла, **create empty workbook**, настройку параметров **copy excel range** и сохранение результата.  

Отсюда вы можете изучать связанные темы, такие как **how to copy pivot** между разными листами, встраивание диаграмм рядом со сводными таблицами или автоматизацию пакетной обработки нескольких книг. Экспериментируйте с настройками `CopyOptions`, чтобы они соответствовали вашим конкретным задачам автоматизации, и у вас будет надёжный набор инструментов для работы с Excel под рукой.

## Что следует изучить дальше?

Следующие учебные материалы охватывают тесно связанные темы, построенные на техниках, продемонстрированных в этом руководстве. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, помогающими освоить дополнительные возможности API и исследовать альтернативные подходы к реализации в ваших проектах.

- [Создание новой книги в Java – Полное руководство по копированию сводной таблицы](/cells/english/java/excel-pivot-tables/create-new-workbook-in-java-full-guide-to-copy-pivot-table/)
- [Копирование сводной таблицы между книгами – Пошаговое руководство на Java](/cells/english/java/excel-pivot-tables/copy-pivot-table-between-workbooks-step-by-step-java-guide/)
- [Как скопировать диапазон и сохранить сводную таблицу в Java](/cells/english/java/excel-pivot-tables/how-to-copy-range-and-preserve-a-pivot-table-in-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}