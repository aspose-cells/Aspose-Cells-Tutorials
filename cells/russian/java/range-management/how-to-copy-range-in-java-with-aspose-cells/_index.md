---
category: general
date: 2026-09-08
description: Как копировать диапазон в Java с помощью Aspose.Cells — изучите копирование
  сводной таблицы, дублирование сводной таблицы и экспорт сводной таблицы с сохранением
  форматирования.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy range
- copy pivot table
- duplicate pivot table
- export pivot table
- copy range with formatting
language: ru
lastmod: 2026-09-08
og_description: Как копировать диапазон в Java с помощью Aspose.Cells. Этот учебник
  показывает, как копировать сводную таблицу, дублировать сводную таблицу и экспортировать
  сводную таблицу, сохраняя форматирование.
og_image_alt: Screenshot of Java code copying a pivot table range in Aspose.Cells
og_title: Как скопировать диапазон в Java – полное руководство по Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-09-08'
  description: How to copy range in Java using Aspose.Cells – learn to copy pivot
    table, duplicate pivot table, and export pivot table while preserving formatting.
  headline: How to copy range in Java with Aspose.Cells
  type: TechArticle
- description: How to copy range in Java using Aspose.Cells – learn to copy pivot
    table, duplicate pivot table, and export pivot table while preserving formatting.
  name: How to copy range in Java with Aspose.Cells
  steps:
  - name: Copy pivot table to an existing workbook
    text: 'If you need to **duplicate pivot table** inside a workbook that already
      has data, use the same `copyRange` call but point to a different destination
      address:'
  - name: Export pivot table only (without surrounding data)
    text: 'Sometimes you want just the pivot table, not the source data. Identify
      the pivot table’s display range via its `getPivotTable` method:'
  - name: Preserve conditional formatting
    text: 'Conditional formatting rules are part of the style collection. The `PasteType.ALL`
      flag already copies them, but you can be explicit:'
  - name: Edge cases and troubleshooting
    text: '| Situation | What to watch for | Recommended fix | |-----------|-------------------|-----------------|
      | Source and destination workbooks use different Excel versions | Some newer
      pivot features (e.g., data model) may not render correctly | Use the latest
      Aspose.Cells version and set `Workbook.setF'
  - name: Next steps
    text: '- Explore **copy range with formatting** for charts and images (use `PasteType.PICTURES`).
      - Automate batch processing: loop over multiple source files and consolidate
      their pivot tables into a summary workbook. - Combine this technique with Aspose.Slides
      to generate PowerPoint reports that embed th'
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: Как скопировать диапазон в Java с помощью Aspose.Cells
url: /ru/java/range-management/how-to-copy-range-in-java-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как копировать диапазон в Java с помощью Aspose.Cells

Если вам нужно **скопировать диапазон** в Java, Aspose.Cells делает эту задачу простой. Независимо от того, перемещаете ли вы обычный блок ячеек или полностью функциональную сводную таблицу, библиотека выполняет операцию копирования, сохраняя формулы, стили и кэш сводных таблиц. В этом руководстве вы узнаете, как **скопировать сводную таблицу**, **дублировать сводную таблицу** и даже **экспортировать сводную таблицу** в новую книгу с полным форматированием.

Учебник охватывает всё от настройки проекта до финального шага проверки, поэтому вы сможете запустить код сразу после чтения. Ни какие внешние инструменты не требуются, кроме Aspose.Cells for Java JAR.

## Предварительные требования

Прежде чем начать, убедитесь, что у вас есть:

- Java 17 (или любой поддерживаемый JDK), установленный и настроенный в вашей IDE.
- Maven или Gradle для управления зависимостями (в примерах используется Maven).
- Исходный файл Excel (`source.xlsx`), содержащий сводную таблицу в диапазоне `A1:H20`.
- Базовые знания программирования на Java.

## Шаг 1: Добавьте Aspose.Cells в ваш проект

Aspose.Cells — коммерческая библиотека, но доступна бесплатная оценочная версия. Добавьте зависимость в ваш `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- Use the latest version -->
</dependency>
```

> **Pro tip:** Если вы предпочитаете Gradle, эквивалентная запись выглядит так:
> ```gradle
> implementation 'com.aspose:aspose-cells:24.9'
> ```

Добавление JAR‑файла дает вам доступ к классам `Workbook`, `Worksheet`, `Range` и `CopyOptions`, которые используются в этом руководстве.

## Шаг 2: Загрузите исходную книгу и выберите первый лист

Первая часть **как скопировать диапазон** — открыть книгу, содержащую данные, которые вы хотите переместить.

```java
import com.aspose.cells.*;

public class CopyRangeDemo {
    public static void main(String[] args) throws Exception {
        // Load the source workbook
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/source.xlsx");
        // Select the first worksheet (index 0)
        Worksheet sourceSheet = sourceWorkbook.getWorksheets().get(0);
```

> **Почему это важно:** Открытие книги создаёт представление в памяти, которое API может изменять, не затрагивая оригинальный файл на диске.

## Шаг 3: Определите диапазон, содержащий сводную таблицу

Сводная таблица располагается внутри прямоугольного блока. Необходимо указать этот блок, чтобы Aspose.Cells знала, что копировать.

```java
        // Define the range that holds the pivot table and its source data
        Range sourceRange = sourceSheet.getCells().createRange("A1:H20");
```

> **Примечание:** Метод `createRange` **не** копирует ничего сразу; он лишь создаёт объект `Range`, указывающий на ячейки, которые вы собираетесь дублировать.

## Шаг 4: Создайте новую книгу и получите её первый лист

Теперь создайте целевую книгу, в которой будет находиться скопированный диапазон.

```java
        // Create an empty workbook for the destination
        Workbook destWorkbook = new Workbook();
        // Get its first (and only) worksheet
        Worksheet destSheet = destWorkbook.getWorksheets().get(0);
```

> **Зачем нужна новая книга?** Использование чистого файла гарантирует, что скрытые стили или именованные диапазоны не помешают операции копирования, что особенно важно при **экспорте сводной таблицы** в отдельный файл.

## Шаг 5: Скопируйте диапазон (включая сводную таблицу) на лист назначения

Это ядро **как скопировать диапазон с форматированием**. Объект `CopyOptions` указывает Aspose.Cells сохранять всё: значения, формулы, стили и кэш сводных таблиц.

```java
        // Prepare copy options – preserve formatting and pivot cache
        CopyOptions copyOptions = new CopyOptions();
        copyOptions.setPasteType(PasteType.ALL); // copies everything
        copyOptions.setSkipBlanks(false);        // keep blank cells

        // Copy the defined range to cell A1 of the destination sheet
        destSheet.getCells().copyRange(sourceRange, "A1", copyOptions);
```

> **Копировать сводную таблицу:** Поскольку исходный диапазон включает сводную таблицу, API автоматически дублирует кэш, и новый лист содержит полностью функционирующую сводную таблицу, работающую точно так же, как оригинальная.

## Шаг 6: Сохраните целевую книгу

Наконец, запишите результат на диск.

```java
        // Save the destination workbook
        destWorkbook.save("YOUR_DIRECTORY/dest.xlsx");
    }
}
```

Когда вы откроете `dest.xlsx`, вы увидите точную копию оригинальной сводной таблицы со всем её форматированием, срезами и вычисляемыми полями.

## Ожидаемый результат

- `dest.xlsx` содержит лист с именем **Sheet1**.
- Ячейки `A1:H20` содержат те же данные и сводную таблицу, что и в источнике.
- Все стили ячеек (шрифты, цвета, границы) сохранены.
- Сводная таблица полностью интерактивна; её обновление отражает изменения в скопированных данных.

## Как скопировать диапазон с форматированием — более глубокий разбор

Приведённый пример демонстрирует самый простой сценарий, но могут возникнуть варианты, требующие слегка другого подхода.

### Копировать сводную таблицу в существующую книгу

Если вам нужно **дублировать сводную таблицу** внутри книги, где уже есть данные, используйте тот же вызов `copyRange`, но укажите другой адрес назначения:

```java
// Assume destWorkbook already contains other sheets
Worksheet targetSheet = destWorkbook.getWorksheets().get(2);
targetSheet.getCells().copyRange(sourceRange, "B5", copyOptions);
```

### Экспортировать только сводную таблицу (без окружающих данных)

Иногда требуется лишь сама сводная таблица, без исходных данных. Определите диапазон отображения сводной таблицы через её метод `getPivotTable`:

```java
PivotTable pt = sourceSheet.getPivotTables().get(0);
String ptArea = pt.getDisplayRange(); // e.g., "C5:G15"
Range pivotOnly = sourceSheet.getCells().createRange(ptArea);
destSheet.getCells().copyRange(pivotOnly, "A1", copyOptions);
```

### Сохранить условное форматирование

Правила условного форматирования являются частью коллекции стилей. Флаг `PasteType.ALL` уже копирует их, но можно задать явно:

```java
copyOptions.setPasteType(PasteType.FORMATS);
copyOptions.setPasteType(PasteType.ALL); // overrides previous, ensures everything
```

### Пограничные случаи и устранение неполадок

| Ситуация | На что обратить внимание | Рекомендуемое решение |
|-----------|-------------------|-----------------|
| Исходная и целевая книги используют разные версии Excel | Некоторые новые возможности сводных таблиц (например, модель данных) могут отображаться некорректно | Используйте последнюю версию Aspose.Cells и задайте `Workbook.setFileFormatType(FileFormatType.XLSX)` для обеих книг |
| Очень большие сводные таблицы ( > 10 000 строк) вызывают нагрузку на память | Ошибки Out‑of‑memory во время копирования | Включите `Workbook.setMemorySetting(MemorySetting.MEMORY_PREFERENCE)` перед загрузкой |
| На листе назначения уже существует именованный диапазон с тем же именем, что и в источнике | Конфликт имён приводит к сбою `CopyOptions` | Вызовите `copyOptions.setIgnoreNameConflicts(true)` |

## Полный, готовый к запуску пример

Ниже представлена полная программа, которую можно скопировать и вставить в класс Java. В ней включены все импорты, обработка ошибок и комментарии.

```java
import com.aspose.cells.*;

public class CopyRangeDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load the source workbook
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/source.xlsx");
        Worksheet sourceSheet = sourceWorkbook.getWorksheets().get(0);

        // 2️⃣ Define the range that includes the pivot table
        Range sourceRange = sourceSheet.getCells().createRange("A1:H20");

        // 3️⃣ Create a new destination workbook
        Workbook destWorkbook = new Workbook();
        Worksheet destSheet = destWorkbook.getWorksheets().get(0);

        // 4️⃣ Configure copy options to keep everything (values, formulas, formatting, pivot cache)
        CopyOptions copyOptions = new CopyOptions();
        copyOptions.setPasteType(PasteType.ALL);
        copyOptions.setSkipBlanks(false);
        copyOptions.setIgnoreNameConflicts(true); // avoid name collisions

        // 5️⃣ Perform the copy
        destSheet.getCells().copyRange(sourceRange, "A1", copyOptions);

        // 6️⃣ Save the result
        destWorkbook.save("YOUR_DIRECTORY/dest.xlsx");
        System.out.println("Copy completed – dest.xlsx now contains the duplicated pivot table.");
    }
}
```

Запустите программу, затем откройте `dest.xlsx`, чтобы убедиться, что сводная таблица работает точно так же, как оригинальная.

## Заключение

Теперь вы знаете, **как копировать диапазон** в Java с помощью Aspose.Cells, включая способы **скопировать сводную таблицу**, **дублировать сводную таблицу** и **экспортировать сводную таблицу**, сохраняя всё форматирование. Библиотека абстрагирует низкоуровневые детали XML‑структуры Excel, позволяя сосредоточиться на бизнес‑логике.

### Следующие шаги

- Исследуйте **копирование диапазона с форматированием** для диаграмм и изображений (используйте `PasteType.PICTURES`).
- Автоматизируйте пакетную обработку: перебирайте несколько исходных файлов и консолидируйте их сводные таблицы в сводной книге.
- Скомбинируйте эту технику с Aspose.Slides для создания PowerPoint‑отчётов, в которые встроена скопированная сводная таблица.

## Что изучать дальше?


Следующие учебники охватывают тесно связанные темы, расширяющие техники, продемонстрированные в этом руководстве. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, помогая вам освоить дополнительные возможности API и исследовать альтернативные подходы в собственных проектах.

- [Как обновить источник сводной таблицы Excel с помощью Aspose.Cells для Java: Полное руководство](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [Оптимизация загрузки сводных таблиц в Java с использованием Aspose.Cells – Полное руководство](/cells/english/java/data-analysis/optimize-pivot-table-loading-aspose-cells-java/)
- [Как скопировать сводную таблицу в C# – Конвертировать Excel в PPTX, копировать диапазон и создавать текстовое поле](/cells/english/net/pivot-tables/how-to-copy-pivot-table-in-c-convert-excel-to-pptx-copy-rang/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}