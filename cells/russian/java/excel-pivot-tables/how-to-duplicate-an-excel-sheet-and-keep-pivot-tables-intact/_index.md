---
category: general
date: 2026-10-23
description: Узнайте, как дублировать лист Excel в Java, сохраняя сводные таблицы.
  Это руководство также показывает, как копировать сводные таблицы, копировать диапазоны
  Excel и копировать лист с данными сводных таблиц.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- duplicate excel sheet
- how to copy pivot
- copy excel range
- copy sheet with pivot
- copy pivot to workbook
language: ru
lastmod: 2026-10-23
og_description: Создайте копию листа Excel в Java, сохранив сводные таблицы. Следуйте
  этому полному руководству, чтобы копировать сводные таблицы, диапазоны Excel и лист
  со сводными данными.
og_image_alt: Screenshot showing a duplicated Excel sheet with pivot tables preserved
og_title: Дублирование листа Excel с сводными таблицами в Java — пошаговое руководство
schemas:
- author: Aspose
  dateModified: '2026-10-23'
  description: Learn how to duplicate an Excel sheet in Java while preserving pivot
    tables. This guide also shows how to copy pivot tables, copy Excel ranges, and
    copy a sheet with pivot data.
  headline: How to duplicate an Excel sheet and keep pivot tables intact in Java
  type: TechArticle
- description: Learn how to duplicate an Excel sheet in Java while preserving pivot
    tables. This guide also shows how to copy pivot tables, copy Excel ranges, and
    copy a sheet with pivot data.
  name: How to duplicate an Excel sheet and keep pivot tables intact in Java
  steps:
  - name: Expected output
    text: 'Running the program creates `DuplicatedWithPivot.xlsx` in the target directory.
      Open the file in Excel and you will see:'
  - name: How to copy pivot to another workbook without copying the whole sheet?
    text: If you only need the pivot and its underlying data, copy the range that
      contains both the source data and the pivot, then use `setCopyPivotTable(true)`.
      The same code from **Step 4** applies; just ensure the range covers the data
      source.
  - name: What if the source workbook has multiple worksheets with pivots?
    text: 'Repeat **Step 3** for each worksheet you want to duplicate:'
  - name: Does this work with protected worksheets?
    text: 'Aspose.Cells can copy protected sheets, but you must unprotect them first
      if you need to modify the pivot after copying:'
  - name: Can I copy a pivot table to an existing workbook that already contains a
      sheet with the same name?
    text: 'Yes. Use `addCopy` with a unique name:'
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
- Pivot tables
title: Как дублировать лист Excel и сохранить сводные таблицы без изменений в Java
url: /ru/java/excel-pivot-tables/how-to-duplicate-an-excel-sheet-and-keep-pivot-tables-intact/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как дублировать лист Excel и сохранить сводные таблицы неизменными в Java

Если вам нужно **дублировать лист Excel**, сохраняя все сводные таблицы, это руководство покажет, как именно это сделать. Вы увидите лаконичное решение, которое копирует лист, копирует определённый диапазон и даже копирует сводную таблицу в другую книгу — всё на чистом Java с использованием Aspose.Cells.

Дублирование листа Excel — распространённая задача, когда вы генерируете ежемесячные отчёты из шаблона или когда нужен «песочничный» копия для тестирования. Приведённый ниже код работает с Aspose.Cells 25.11 и новее, где была добавлена опция `setCopyPivotTable(true)`.

## Что понадобится

- Java 17 (или любой современный JDK), установленный
- Aspose.Cells for Java 25.11 или новее в вашем проекте (Maven‑координата `com.aspose:aspose-cells:25.11`)
- Исходная рабочая книга (`SourceWithPivot.xlsx`), уже содержащая сводную таблицу
- IDE или система сборки по вашему выбору (IntelliJ IDEA, Eclipse, Maven, Gradle и т.д.)

## Шаг 1: Загрузить исходную рабочую книгу, содержащую сводную таблицу

Первая операция — открыть книгу, в которой находится сводная таблица, которую вы хотите сохранить.

```java
import com.aspose.cells.*;

public class DuplicateExcelSheet {
    public static void main(String[] args) throws Exception {
        // Load the source workbook with the pivot table
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/SourceWithPivot.xlsx");
```

> **Почему этот шаг важен:** загрузка исходной книги даёт доступ к объектам листов, ячейкам и встроенным сводным таблицам. Без этого вы не сможете ссылаться на данные сводной таблицы, которые планируете копировать.

## Шаг 2: Создать пустую целевую рабочую книгу (или загрузить существующую)

Вы можете либо начать с пустой книги, либо открыть существующий файл, который получит дублированный лист.

```java
        // Create a new, empty destination workbook
        Workbook dstWb = new Workbook();
```

> **Подсказка:** если у вас уже есть рабочая книга отчётов, замените строку выше на `new Workbook("ExistingReport.xlsx")`, чтобы добавить дублированный лист в неё.

## Шаг 3: Скопировать весь лист — сводная таблица сохраняется автоматически

Копирование всего листа — самый простой способ **скопировать лист со сводной таблицей**. Aspose.Cells автоматически копирует определение сводной таблицы и её кэш.

```java
        // Access the first worksheet (index 0) from the source workbook
        Worksheet srcWs = srcWb.getWorksheets().get(0);

        // Add a copy of the source worksheet to the destination workbook
        Worksheet dstWs = dstWb.getWorksheets().addCopy(srcWs);
```

> **Почему это работает:** `addCopy` клонирует структуру листа, значения ячеек, стили и любые встроенные сводные таблицы. Новый лист в `dstWb` будет выглядеть идентично оригиналу, включая кэш сводной таблицы.

## Шаг 4: (Опционально) Скопировать только определённый диапазон, включающий сводную таблицу

Иногда вам не нужен весь лист — возможно, требуется только часть, содержащая сводную таблицу. Здесь вы **копируете диапазон Excel** и явно указываете, что нужно скопировать сводную таблицу.

```java
        // Define the source range that covers the pivot table (adjust as needed)
        Range srcRange = srcWs.getCells().createRange("A1:G30");

        // Define the target range in the destination worksheet
        Range dstRange = dstWs.getCells().createRange("A1");

        // Copy the range and tell Aspose.Cells to include the pivot table
        CopyOptions copyOptions = new CopyOptions();
        copyOptions.setCopyPivotTable(true); // new option in 25.11
        dstRange.copy(srcRange, copyOptions);
```

> **Как это помогает:** `setCopyPivotTable(true)` заставляет движок дублировать определение сводной таблицы даже при копировании ограниченного диапазона. Без этого флага копируются только сырые данные, а сводная таблица теряется.

## Шаг 5: Сохранить целевую рабочую книгу

Наконец, запишите дублированное содержимое в новый файл.

```java
        // Save the destination workbook to a new file
        dstWb.save("YOUR_DIRECTORY/DuplicatedWithPivot.xlsx");
    }
}
```

### Ожидаемый результат

Запуск программы создаёт `DuplicatedWithPivot.xlsx` в целевом каталоге. Откройте файл в Excel, и вы увидите:

- Новый лист с именем `Sheet1 (Copy)` (или оригинальное имя с добавлением «Copy»)
- Сводная таблица отображается точно так же, как в исходном листе, полностью функционирует
- Если вы использовали опциональное копирование диапазона, присутствуют только ячейки A1:G30, но сводная таблица всё равно работает, поскольку её кэш был скопирован

## Часто задаваемые вопросы и особые случаи

### Как скопировать сводную таблицу в другую книгу без копирования всего листа?

Если вам нужна только сводная таблица и её исходные данные, скопируйте диапазон, содержащий и исходные данные, и сводную таблицу, затем используйте `setCopyPivotTable(true)`. Применяется тот же код из **Шага 4**; просто убедитесь, что диапазон охватывает источник данных.

### Что делать, если в исходной книге несколько листов со сводными таблицами?

Повторите **Шаг 3** для каждого листа, который хотите дублировать:

```java
for (int i = 0; i < srcWb.getWorksheets().getCount(); i++) {
    Worksheet ws = srcWb.getWorksheets().get(i);
    dstWb.getWorksheets().addCopy(ws);
}
```

### Работает ли это с защищёнными листами?

Aspose.Cells может копировать защищённые листы, но при необходимости изменить сводную таблицу после копирования её нужно сначала снять защиту:

```java
srcWs.unprotect("password");
dstWs.unprotect("password");
```

### Можно ли скопировать сводную таблицу в существующую книгу, где уже есть лист с тем же именем?

Да. Используйте `addCopy` с уникальным именем:

```java
Worksheet dstWs = dstWb.getWorksheets().addCopy(srcWs);
dstWs.setName("PivotCopy_" + System.currentTimeMillis());
```

## Профессиональный совет: проверьте кэш сводной таблицы

После копирования вы можете программно подтвердить наличие кэша сводной таблицы:

```java
PivotTable pt = dstWs.getPivotTables().get(0);
System.out.println("Pivot cache ID: " + pt.getCacheIndex());
```

Если ID кэша выводит неотрицательное число, сводная таблица успешно дублирована.

## Заключение

Теперь вы знаете, как **дублировать лист Excel** в Java, сохраняя каждую сводную таблицу, как **копировать сводные** таблицы напрямую, как **копировать диапазон Excel**, включающий сводную таблицу, и как **копировать лист со сводной** или **копировать сводную в книгу** с помощью Aspose.Cells 25.11+. Применяйте эти шаблоны для автоматизации генерации отчётов, создания клонов шаблонов или построения тестовых окружений, которым нужны идентичные аналитические данные на основе сводных таблиц.

Готовы исследовать дальше? Попробуйте экспортировать дублированную книгу в PDF или программно обновить кэш сводной таблицы после копирования, чтобы отразить актуальные данные. Приятного кодинга!

## Что стоит изучить дальше?

Следующие руководства охватывают тесно связанные темы, которые развивают техники, продемонстрированные в этом руководстве. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, помогая вам освоить дополнительные возможности API и исследовать альтернативные подходы в собственных проектах.

- [Как дублировать лист и сохранить сводные таблицы в Java](/cells/english/java/excel-pivot-tables/how-to-duplicate-worksheet-and-preserve-pivot-tables-in-java/)
- [Как скопировать сводную таблицу в Java — полное руководство Aspose.Cells](/cells/english/java/excel-pivot-tables/how-to-copy-pivot-table-in-java-complete-aspose-cells-guide/)
- [Как скопировать диапазон и сохранить сводную таблицу в Java](/cells/english/java/excel-pivot-tables/how-to-copy-range-and-preserve-a-pivot-table-in-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}