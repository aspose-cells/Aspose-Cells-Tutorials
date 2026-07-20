---
category: general
date: 2026-07-20
description: Копировать сводную таблицу в Java с помощью Aspose.Cells. Узнайте, как
  скопировать сводную таблицу в другой файл, извлечь диапазон сводной таблицы и скопировать
  диапазон в новую книгу.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy pivot table
- copy pivot table to another file
- copy range to new workbook
- how to copy pivot table
- extract pivot table range
language: ru
lastmod: 2026-07-20
og_description: Копирование сводной таблицы в Java с помощью Aspose.Cells. Следуйте
  этому руководству, чтобы скопировать сводную таблицу в другой файл, извлечь её диапазон
  и скопировать диапазон в новую книгу.
og_image_alt: Diagram illustrating how to copy pivot table from one workbook to another
  using Java
og_title: Копирование сводной таблицы в Java – пошаговое руководство Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-07-20'
  description: Copy pivot table in Java using Aspose.Cells. Learn how to copy pivot
    table to another file, extract pivot table range, and copy range to new workbook.
  headline: Copy Pivot Table in Java with Aspose.Cells – Complete Guide
  type: TechArticle
- description: Copy pivot table in Java using Aspose.Cells. Learn how to copy pivot
    table to another file, extract pivot table range, and copy range to new workbook.
  name: Copy Pivot Table in Java with Aspose.Cells – Complete Guide
  steps:
  - name: Expected Output
    text: '- `CopyWithPivot.xlsx` contains a single worksheet. - The worksheet shows
      the same pivot layout as the source. - All pivot fields, filters, and calculated
      items are intact. - Refreshing the pivot updates totals based on the newly copied
      data.'
  - name: Copying Multiple Pivot Tables
    text: If your source sheet has more than one pivot, repeat the `createRange`/`copy`
      pair for each table, adjusting the address accordingly. You can also loop through
      `sourceWorksheet.getPivotTables()` to automate discovery.
  - name: Preserving Styles and Formatting
    text: The `Range.copy` method copies cell values, formulas, and formatting by
      default. However, if you only need the data without styles, use `sourceRange.copy(destinationRange,
      new CopyOptions());` and tweak the `CopyOptions` flags.
  - name: Working with Large Workbooks
    text: 'For workbooks exceeding a few hundred MB, consider enabling **memory‑efficient
      loading**:'
  - name: Quick Recap
    text: '- Loaded a source workbook containing a pivot table. - Identified the exact
      **extract pivot table range** (`A1:G20`). - Created a fresh workbook and **copied
      range to new workbook**, preserving the pivot. - Saved the result, effectively
      **copying pivot table to another file**.'
  type: HowTo
- questions:
  - answer: Yes. Aspose handles format conversion automatically during `save()`. Just
      specify the desired extension in the output path.
    question: Can I copy a pivot table across different Excel formats (XLSX → XLS)?
  - answer: The copy will overwrite existing cells. To avoid data loss, either clear
      the area first (`destinationSheet.getCells().clearRange("A1:G20")`) or choose
      a different start cell.
    question: What if the destination workbook already contains data in the target
      range?
  - answer: 'The source workbook is opened in read‑write mode by default. If you only
      need to read, pass `LoadOptions` with `setReadOnly(true)`. ## Next Steps & Related
      Topics Now that you know **how to copy pivot table** programmatically, you might
      explore: - **Refreshing pivot caches** after copying (`pivotTab'
    question: Does this work with read‑only source files?
  type: FAQPage
tags:
- Aspose.Cells
- Java
- Excel automation
- Pivot Table
title: Копирование сводной таблицы в Java с Aspose.Cells – полное руководство
url: /ru/java/excel-pivot-tables/copy-pivot-table-in-java-with-aspose-cells-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Копирование сводной таблицы в Java с Aspose.Cells – Полное руководство

Когда‑нибудь вам нужно было **скопировать сводную таблицу** из одного файла Excel в другой, но вы не знали, с чего начать? Вы не одиноки. Во многих конвейерах отчетности нам приходится перемещать сводную‑таблицу из основного рабочего листа в легковесный файл для распространения, а делать это вручную — настоящая головная боль.  

В этом руководстве мы пройдем чистое программное решение, которое позволяет **скопировать сводную таблицу в другой файл**, извлечь её точный диапазон и даже **скопировать диапазон в новую книгу** за один шаг. К концу вы получите переиспользуемый фрагмент кода, работающий с любым Java‑проектом, поддерживающим Aspose.Cells.

## Что покрывает это руководство

- Загрузка исходной книги, уже содержащей сводную таблицу  
- Определение точного **extract pivot table range**, который вам нужен  
- Создание новой книги и вставка диапазона с сохранением логики сводной таблицы  
- Сохранение результата в новый файл, готовый к дальнейшей обработке  

Никаких внешних инструментов, никаких макросов — только чистый Java‑код и несколько вызовов Aspose.Cells. Если вы уже работали с Excel, концепции будут знакомы; если вы новичок в Aspose, библиотека абстрагирует низкоуровневую работу с XML, позволяя сосредоточиться на бизнес‑логике.

> **Prerequisites**  
> - Java 8 или новее  
> - Aspose.Cells for Java (последняя версия на июль 2026)  
> - Базовое знакомство со сводными таблицами Excel  

Теперь давайте погрузимся.

## Шаг 1: Настройте проект и импортируйте Aspose.Cells

Прежде чем работать с любой книгой, убедитесь, что JAR‑файл Aspose.Cells находится в classpath. Если вы используете Maven, добавьте зависимость:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version> <!-- latest as of 2026 -->
</dependency>
```

Если предпочитаете ручную настройку, поместите `aspose-cells-24.10.jar` в папку `libs` и подключите её в IDE.

> **Pro tip:** Держите версию библиотеки синхронной с вашей Java‑runtime, чтобы избежать `UnsupportedClassVersionError`.

## Шаг 2: Загрузите исходную книгу, содержащую сводную таблицу

Первое, что нам нужно — объект `Workbook`, указывающий на файл, где находится сводная таблица. Именно с этого начинается операция **copy pivot table**.

```java
import com.aspose.cells.*;

public class CopyPivotTableDemo {
    public static void main(String[] args) throws Exception {
        // Load the workbook that already has the pivot table
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/SourceWithPivot.xlsx");
```

Почему именно так? Aspose читает весь файл в память, предоставляя полный доступ к листам, ячейкам и скрытому кэшу сводных таблиц. Это гарантирует, что определение сводной (поля, фильтры, источник данных) останется неизменным при последующем копировании.

## Шаг 3: Определите точный диапазон, содержащий сводную таблицу

Сводная таблица — это не просто блок ячеек; за ней стоит скрытый кэш. Однако при копировании визуального диапазона Aspose автоматически переносит кэш. Чтобы быть уверенными, мы явно зададим диапазон — это шаг **extract pivot table range**.

```java
        // Define the range covering the pivot table (adjust as needed)
        Range sourceRange = sourceWorkbook.getWorksheets()
                                          .get(0)                // first worksheet
                                          .getCells()
                                          .createRange("A1:G20"); // typical size; change if larger
```

Если вы не уверены в размерах, можно программно найти сводную таблицу через `Worksheet.getPivotTables()`. Для краткости будем считать, что прямоугольник известен, но та же логика работает и для динамического обнаружения.

## Шаг 4: Создайте новую книгу для получения скопированного диапазона

Теперь создаём чистую книгу, которая станет файлом‑назначением. Здесь происходит **copy range to new workbook**.

```java
        // Create an empty workbook that will receive the copy
        Workbook destinationWorkbook = new Workbook(); // starts with a default sheet
        Worksheet destinationSheet = destinationWorkbook.getWorksheets().get(0);
```

Почему новая книга? Чистый старт гарантирует отсутствие посторонних форматов или скрытых листов, которые могут помешать внутренним ссылкам сводной. Если нужно объединить с существующим файлом, просто загрузите его вместо `new Workbook()`.

## Шаг 5: Выполните копирование — сводная таблица сохраняется

Это сердце руководства: копирование диапазона с сохранением работоспособности сводной. Метод `Range.copy` от Aspose делает всю тяжёлую работу.

```java
        // Copy the source range (including the pivot) to the destination sheet
        sourceRange.copy(destinationSheet.getCells().createRange("A1"));
```

При выполнении этой строки Aspose клонирует визуальные ячейки **и** копирует подлежащий кэш сводной в новую книгу. В результате получаем полностью рабочую сводную таблицу, которую можно обновлять, фильтровать или экспортировать так же, как оригинал.

> **Common question:** *Что если в целевом файле уже есть сводная таблица с тем же именем?*  
> Aspose автоматически переименовывает скопированную сводную, чтобы избежать конфликтов (например, “PivotTable1_1”).

## Шаг 6: Сохраните целевую книгу

Наконец, сохраняем новый файл. Это фактический шаг **copy pivot table to another file** на диске.

```java
        // Save the workbook with the copied pivot table
        destinationWorkbook.save("YOUR_DIRECTORY/CopyWithPivot.xlsx");
    }
}
```

После выполнения программы откройте `CopyWithPivot.xlsx` в Excel. Вы увидите тот же макет сводной, те же фильтры и источник данных (который теперь указывает на скопированный диапазон). Обновление сводной пересчитает итоги на основе нового блока данных.

## Полный рабочий пример

Собирая всё вместе, получаем полностью готовый к запуску класс:

```java
import com.aspose.cells.*;

public class CopyPivotTableDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load the source workbook that contains the pivot table
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/SourceWithPivot.xlsx");

        // 2️⃣ Define the range that includes the pivot table (e.g., A1:G20)
        Range sourceRange = sourceWorkbook.getWorksheets()
                                          .get(0)
                                          .getCells()
                                          .createRange("A1:G20");

        // 3️⃣ Create a new workbook to receive the copied range
        Workbook destinationWorkbook = new Workbook(); // empty workbook
        Worksheet destinationSheet = destinationWorkbook.getWorksheets().get(0);

        // 4️⃣ Copy the range to the destination worksheet; the pivot table is preserved
        sourceRange.copy(destinationSheet.getCells().createRange("A1"));

        // 5️⃣ Save the destination workbook with the copied pivot table
        destinationWorkbook.save("YOUR_DIRECTORY/CopyWithPivot.xlsx");
    }
}
```

### Ожидаемый результат

- `CopyWithPivot.xlsx` содержит один лист.  
- На листе отображается тот же макет сводной, что и в источнике.  
- Все поля, фильтры и вычисляемые элементы сохранены.  
- Обновление сводной обновит итоги на основе только что скопированных данных.

## Обработка особых случаев и вариаций

### Копирование нескольких сводных таблиц

Если на исходном листе более одной сводной, повторите пару `createRange`/`copy` для каждой таблицы, подбирая адрес соответственно. Можно также пройтись в цикле по `sourceWorksheet.getPivotTables()` для автоматического обнаружения.

### Сохранение стилей и форматирования

Метод `Range.copy` по умолчанию копирует значения, формулы и форматирование. Если нужны только данные без стилей, используйте `sourceRange.copy(destinationRange, new CopyOptions());` и настройте флаги `CopyOptions`.

### Работа с большими книгами

Для книг размером более нескольких сотен МБ рассмотрите включение **memory‑efficient loading**:

```java
LoadOptions loadOptions = new LoadOptions(LoadFormat.XLSX);
loadOptions.setMemorySetting(MemorySetting.MEMORY_PREFERENCE);
Workbook sourceWorkbook = new Workbook("bigfile.xlsx", loadOptions);
```

Это уменьшит потребление кучи, но всё равно позволит копировать диапазоны.

## Часто задаваемые вопросы

**Q: Можно ли копировать сводную таблицу между разными форматами Excel (XLSX → XLS)?**  
A: Да. Aspose автоматически обрабатывает конвертацию формата во время `save()`. Просто укажите нужное расширение в пути вывода.

**Q: Что если в целевой книге уже есть данные в целевом диапазоне?**  
A: Копирование перезапишет существующие ячейки. Чтобы избежать потери данных, либо очистите область заранее (`destinationSheet.getCells().clearRange("A1:G20")`), либо выберите другую стартовую ячейку.

**Q: Работает ли это с файлами‑источниками только для чтения?**  
A: По умолчанию исходная книга открывается в режиме чтения‑записи. Если нужен только чтение, передайте `LoadOptions` с `setReadOnly(true)`.

## Следующие шаги и связанные темы

Теперь, когда вы знаете **how to copy pivot table** программно, можете изучить:

- **Обновление кэша сводных** после копирования (`pivotTable.refresh();`)  
- **Экспорт данных сводной в CSV** для дальнейшего анализа  
- **Программное добавление срезов** к скопированной сводной (`PivotTable.addSlicer(...)`)  
- **Копирование диаграмм, связанных со сводными**, с помощью `Chart.copy()`  

Каждый из этих пунктов опирается на основу, которую мы только что построили, позволяя создавать сквозные конвейеры автоматизации Excel в Java.

---

### Краткое резюме

- Загрузили исходную книгу со сводной таблицей.  
- Определили точный **extract pivot table range** (`A1:G20`).  
- Создали новую книгу и **copied range to new workbook**, сохранив сводную.  
- Сохранили результат, эффективно **copying pivot table to another file**.  

Попробуйте на своих файлах, подкорректируйте диапазон и наблюдайте, как сводная мигрирует без проблем. Если возникнут вопросы, оставляйте комментарий ниже — happy coding!

![Диаграмма копирования сводной таблицы, показывающая исходную и целевую книги](https://example.com/images/copy-pivot-table-diagram.png)


## Что изучать дальше?


Следующие руководства охватывают тесно связанные темы, расширяющие техники, продемонстрированные в этом гиде. Каждый ресурс содержит полностью работающие примеры кода с пошаговыми объяснениями, помогающими освоить дополнительные возможности API и исследовать альтернативные подходы в ваших проектах.

- [How to Update Excel Pivot Table Source with Aspose.Cells for Java: A Comprehensive Guide](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [Optimize Pivot Table Loading in Java using Aspose.Cells: A Comprehensive Guide](/cells/english/java/data-analysis/optimize-pivot-table-loading-aspose-cells-java/)
- [Excel Pivot Table Manipulation with Aspose.Cells Java: A Comprehensive Guide](/cells/english/java/data-analysis/excel-pivot-table-manipulation-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}