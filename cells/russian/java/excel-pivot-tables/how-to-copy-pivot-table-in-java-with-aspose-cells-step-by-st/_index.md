---
category: general
date: 2026-10-20
description: Узнайте, как копировать сводную таблицу с помощью Aspose.Cells в Java.
  Этот учебник показывает, как скопировать диапазон на новый лист и безопасно дублировать
  лист со сводной таблицей.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy pivot table
- copy range to new sheet
- duplicate pivot table sheet
language: ru
lastmod: 2026-10-20
og_description: Как скопировать сводную таблицу с помощью Aspose.Cells в Java. Следуйте
  этому руководству, чтобы скопировать диапазон на новый лист и дублировать лист со
  сводной таблицей без потери данных.
og_image_alt: Screenshot showing how to copy pivot table from one worksheet to another
  in a Java program
og_title: Как скопировать сводную таблицу в Java — полный учебник по Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-10-20'
  description: Learn how to copy pivot table using Aspose.Cells in Java. This tutorial
    shows how to copy range to new sheet and duplicate pivot table sheet safely.
  headline: How to copy pivot table in Java with Aspose.Cells – step‑by‑step guide
  type: TechArticle
- description: Learn how to copy pivot table using Aspose.Cells in Java. This tutorial
    shows how to copy range to new sheet and duplicate pivot table sheet safely.
  name: How to copy pivot table in Java with Aspose.Cells – step‑by‑step guide
  steps:
  - name: Load the workbook that holds the original pivot table.
    text: Load the workbook that holds the original pivot table.
  - name: Identify the exact range that includes the pivot table.
    text: Identify the exact range that includes the pivot table.
  - name: Create a new worksheet that will receive the copied data.
    text: Create a new worksheet that will receive the copied data.
  - name: Use the `Range.copy` method to transfer the range to the new sheet.
    text: Use the `Range.copy` method to transfer the range to the new sheet.
  - name: Save the workbook to a new file.
    text: Save the workbook to a new file.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: Как скопировать сводную таблицу в Java с помощью Aspose.Cells – пошаговое руководство
url: /ru/java/excel-pivot-tables/how-to-copy-pivot-table-in-java-with-aspose-cells-step-by-st/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как скопировать сводную таблицу в Java с помощью Aspose.Cells – пошаговое руководство

Если вам нужно **скопировать сводную таблицу** в Java‑приложении, это руководство проведёт вас через все необходимые шаги. Независимо от того, создаёте ли вы движок отчётности или автоматизируете миграцию данных, вы увидите, как скопировать диапазон на новый лист, сохранив определение и данные сводной таблицы.

Копирование сводной таблицы может показаться рискованным, потому что скрытый кэш и настройки полей часто теряются. В этом учебнике демонстрируется надёжный подход с использованием Aspose.Cells, показан полностью готовый к запуску код и объяснено, почему каждая строка важна. К концу вы сможете дублировать лист со сводной таблицей за считанные секунды.

## Предварительные требования

* Установлен Java 8 или новее.
* Aspose.Cells for Java (версия 23.10 или новее) добавлен в classpath вашего проекта.
* Исходный рабочий файл (`source.xlsx`), содержащий сводную таблицу в диапазоне `A1:G20`.
* Базовое знакомство с Java и концепциями Excel.

Дополнительные библиотеки не требуются; Aspose.Cells обрабатывает все операции с Excel внутри.

## Как скопировать сводную таблицу – общая стратегия

Основная идея проста:

1. Загрузить рабочую книгу, содержащую оригинальную сводную таблицу.
2. Определить точный диапазон, включающий сводную таблицу.
3. Создать новый лист, который получит скопированные данные.
4. Использовать метод `Range.copy` для переноса диапазона на новый лист.  
   Этот метод автоматически копирует кэш сводной таблицы, поэтому она остаётся рабочей.
5. Сохранить рабочую книгу в новый файл.

Поскольку операция копирования происходит на уровне диапазона, **лист с дублированной сводной таблицей** сохраняет все конфигурации полей, фильтры и вычисляемые элементы.

## Шаг 1: Загрузить исходную рабочую книгу

```java
// Import Aspose.Cells classes
import com.aspose.cells.*;

public class PivotCopyDemo {
    public static void main(String[] args) throws Exception {
        // Load the source workbook that contains the pivot table
        Workbook workbook = new Workbook("YOUR_DIRECTORY/source.xlsx");
```

*Почему это важно*: Загрузка рабочей книги даёт доступ к её листам, ячейкам и кэшу сводной таблицы. Aspose.Cells читает весь файл в память, поэтому последующие операции быстры и потокобезопасны.

## Шаг 2: Определить исходный диапазон, содержащий сводную таблицу

```java
        // Locate the first worksheet (index 0) and create a range covering the pivot table
        Range sourceRange = workbook.getWorksheets()
                                    .get(0)               // first sheet
                                    .getCells()
                                    .createRange("A1:G20"); // adjust if your pivot table is larger
```

*Почему это важно*: Вызов `createRange` указывает Aspose.Cells точно, какие ячейки копировать. Включение всей области сводной таблицы гарантирует, что скрытые строки кэша также будут перенесены. Если пропустить любую часть кэша, скопированная сводная таблица окажется пустой.

## Шаг 3: Добавить лист назначения для скопированных данных

```java
        // Add a new worksheet that will hold the duplicated pivot table
        Worksheet destinationSheet = workbook.getWorksheets().add("CopyResult");
```

*Почему это важно*: Добавление отдельного листа изолирует скопированную сводную таблицу от оригинала, упрощая сравнение результатов или использование листа в качестве шаблона для дальнейшей обработки.

## Шаг 4: Скопировать диапазон на лист назначения (сводная таблица сохраняется)

```java
        // Copy the defined range to cell A1 of the new worksheet
        sourceRange.copy(destinationSheet.getCells().createRange("A1"));
```

*Почему это важно*: Метод `copy` копирует не только значения ячеек и форматирование, но и воспроизводит кэш сводной таблицы. Это ключевой шаг, позволяющий **дублировать лист со сводной таблицей** без потери любой функциональности.

## Шаг 5: Сохранить рабочую книгу с скопированным диапазоном

```java
        // Persist the workbook to a new file
        workbook.save("YOUR_DIRECTORY/result.xlsx");
    }
}
```

*Почему это важно*: Сохранение создаёт новый файл Excel (`result.xlsx`), содержащий как оригинальный, так и дублированный лист со сводной таблицей. Теперь вы можете открыть файл в Excel, чтобы убедиться, что сводная таблица работает точно так же, как и прежде.

## Полный, готовый к запуску пример

Объединив всё вместе, представляем полный код программы, который вы можете скопировать и вставить в свою IDE:

```java
import com.aspose.cells.*;

public class PivotCopyDemo {
    public static void main(String[] args) throws Exception {
        // 1. Load the source workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/source.xlsx");

        // 2. Define the source range that contains the pivot table
        Range sourceRange = workbook.getWorksheets()
                                    .get(0)
                                    .getCells()
                                    .createRange("A1:G20");

        // 3. Add a destination worksheet for the copied data
        Worksheet destinationSheet = workbook.getWorksheets().add("CopyResult");

        // 4. Copy the range to the destination worksheet (pivot table is preserved)
        sourceRange.copy(destinationSheet.getCells().createRange("A1"));

        // 5. Save the workbook with the copied range
        workbook.save("YOUR_DIRECTORY/result.xlsx");
    }
}
```

### Ожидаемый результат

* При открытии `result.xlsx` отображаются два листа:
  * **Sheet1** – оригинальные данные и сводная таблица.
  * **CopyResult** – точный дубликат сводной таблицы, полностью функциональный.
* Все поля сводной таблицы, фильтры и вычисляемые элементы ведут себя идентично исходным.

Если вы измените исходную сводную таблицу после копирования, дублированный лист **не** отразит эти изменения, поскольку кэш был продублирован во время копирования. Такая изоляция часто желательна, когда нужен снимок отчёта.

## Распространённые подводные камни и как их избежать

| Проблема | Почему происходит | Решение |
|----------|-------------------|---------|
| **Сводная таблица отображается пустой** | Скопированный диапазон не включил скрытые строки кэша. | Убедитесь, что диапазон включает весь кэш (обычно несколько строк ниже видимой таблицы). |
| **Имя листа назначения уже существует** | `add("CopyResult")` бросает исключение, если имя уже занято. | Используйте `workbook.getWorksheets().addUniqueName("CopyResult")` или проверьте `contains` перед добавлением. |
| **Ошибки пути к файлу** | Неправильный `YOUR_DIRECTORY` приводит к `FileNotFoundException`. | Используйте абсолютные пути или `Paths.get(...).toAbsolutePath()` в Java для определения местоположения. |
| **Замедление производительности при больших книгах** | Копирование огромных диапазонов переносит ненужные ячейки. | Ограничьте диапазон точной областью сводной таблицы или используйте `Range.copy` с `CopyOptions`, чтобы пропустить форматирование, если оно не требуется. |

## Профессиональный совет: использование `CopyOptions` для более тонкого управления

Если вам нужны только данные сводной таблицы и вы хотите пропустить форматирование ячеек, можно передать объект `CopyOptions`:

```java
CopyOptions options = new CopyOptions();
options.setCopyStyle(false);        // skip styles
options.setCopyMerged(true);        // keep merged cells
sourceRange.copy(destinationSheet.getCells().createRange("A1"), options);
```

## Как скопировать диапазон на новый лист без потери формул

Приведённый выше пример уже копирует формулы, поскольку `Range.copy` сохраняет их по умолчанию. Если нужны только значения (например, чтобы зафиксировать текущее состояние), установите `options.setPasteType(PasteType.VALUES)`.

```java
CopyOptions opt = new CopyOptions();
opt.setPasteType(PasteType.VALUES);
sourceRange.copy(destinationSheet.getCells().createRange("A1"), opt);
```

Теперь лист назначения содержит статические значения, но сводная таблица всё равно будет работать, поскольку её кэш является частью диапазона.

## Краткое резюме решения

* **Как скопировать сводную таблицу** – загрузить рабочую книгу, определить точный диапазон, добавить новый лист, скопировать диапазон и сохранить.
* Процесс также демонстрирует **копирование диапазона на новый лист** и как безопасно **дублировать лист со сводной таблицей**.
* Вы можете точно настроить копирование с помощью `CopyOptions` для повышения производительности или сценариев только со значениями.

## Следующие шаги и связанные темы

* **Обновление кэша сводной таблицы программно** – используйте `PivotTable.refreshData()` после обновления исходных данных.
* **Экспорт сводной таблицы в PDF** – комбинируйте эту технику копирования с `PdfSaveOptions` для создания отчётов‑снимков.
* **Автоматизация дублирования нескольких листов** – пройдитесь по всем листам и примените ту же логику копирования.

Экспериментируйте с этими вариантами, чтобы адаптировать шаблон к вашему конкретному конвейеру отчётности. Если вы столкнётесь с особенными случаями, например внешними источниками данных или сводными таблицами, управляемыми VBA, тот же подход копирования диапазона работает, но может потребоваться также копировать базовые объекты соединения.

---

*Счастливого кодинга! Если этот учебник помог вам узнать **как скопировать сводную таблицу**, смело делитесь им с коллегами или вносите улучшения.*

## Что стоит изучить дальше?

Следующие учебники охватывают тесно связанные темы, построенные на техниках, продемонстрированных в этом руководстве. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы к реализации в ваших проектах.

- [Как скопировать диапазон и сохранить сводную таблицу в Java](/cells/english/java/excel-pivot-tables/how-to-copy-range-and-preserve-a-pivot-table-in-java/)
- [Создание новой рабочей книги в Java – Полное руководство по копированию сводной таблицы](/cells/english/java/excel-pivot-tables/create-new-workbook-in-java-full-guide-to-copy-pivot-table/)
- [Копирование сводной таблицы между рабочими книгами – Пошаговое руководство Java](/cells/english/java/excel-pivot-tables/copy-pivot-table-between-workbooks-step-by-step-java-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}