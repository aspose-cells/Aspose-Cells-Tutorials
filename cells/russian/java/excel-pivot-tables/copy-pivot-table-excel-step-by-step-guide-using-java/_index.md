---
category: general
date: 2026-06-27
description: Копировать сводную таблицу Excel с помощью Java за несколько минут —
  узнайте, как скопировать диапазон в другую книгу и откройте эффективные способы
  копирования сводной таблицы.
draft: false
keywords:
- copy pivot table excel
- copy range to another workbook
- how to copy pivot table
language: ru
og_description: Копировать сводную таблицу Excel с помощью Java. Это руководство показывает,
  как скопировать диапазон в другую книгу и объясняет, как скопировать сводную таблицу,
  с полным примером.
og_title: Копировать сводную таблицу Excel – учебник по Java
schemas:
- author: Aspose
  dateModified: '2026-06-27'
  description: Copy pivot table excel with Java in minutes – learn how to copy range
    to another workbook and discover how to copy pivot table efficiently.
  headline: Copy Pivot Table Excel – Step‑by‑Step Guide Using Java
  type: TechArticle
- description: Copy pivot table excel with Java in minutes – learn how to copy range
    to another workbook and discover how to copy pivot table efficiently.
  name: Copy Pivot Table Excel – Step‑by‑Step Guide Using Java
  steps:
  - name: Expected Result
    text: '- Opening `destination.xlsx` shows a sheet named **CopiedPivot**. - The
      sheet contains a pivot table that can be refreshed, filtered, and rearranged
      just like the original. - No error messages appear in the console, confirming
      that **copy pivot table excel** succeeded.'
  - name: What if the source workbook has multiple pivot tables?
    text: 'You can repeat the range‑selection logic for each pivot table, or you can
      copy the entire worksheet:'
  - name: How to handle external data connections?
    text: 'If your pivot table pulls data from an external database, the destination
      workbook will retain the connection string. To avoid broken links, update the
      connection after copying:'
  - name: Does this work with .xls files?
    text: Yes. Aspose.Cells abstracts the file format, so the same code works for
      `.xls`, `.xlsx`, `.xlsb`, and even `.ods`. Just change the file extension in
      the `Workbook` constructors.
  type: HowTo
tags:
- pivot-table
- excel
- java
- aspose-cells
title: Копирование сводной таблицы в Excel – пошаговое руководство с использованием
  Java
url: /ru/java/excel-pivot-tables/copy-pivot-table-excel-step-by-step-guide-using-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Копирование сводной таблицы Excel – руководство на Java

Когда‑нибудь задумывались, как **copy pivot table excel** файлы без потери исходных соединений данных? Вы не одиноки. Многие разработчики сталкиваются с проблемой, когда пытаются переместить сводную таблицу из одной книги в другую, в результате получая статический диапазон или сломанную ссылку.  

Хорошие новости? С несколькими строками кода на Java и правильной библиотекой вы можете чисто **copy pivot table excel** книги, сохраняя каждое поле, фильтр и макет. В этом руководстве мы также покажем, как **how to copy pivot table** с помощью API Aspose.Cells for Java, и добавим советы по **copy range to another workbook** для редких сценариев.

> **What you’ll walk away with:** полностью исполняемую программу, которая загружает исходную книгу, копирует диапазон, содержащий сводную таблицу, и сохраняет новую книгу, выглядящую точно так же, как оригинал.

## Необходимые условия

- Java 17 или новее (код компилируется на любой современной JDK).
- Aspose.Cells for Java 23.10 или новее — бесплатная пробная версия подходит для тестирования.
- Исходный файл Excel (`source.xlsx`), уже содержащий сводную таблицу на первом листе.
- IDE или простая настройка сборки через командную строку (Maven/Gradle).

Других внешних зависимостей не требуется.

## Шаг 1: Настройка проекта и импорт классов

Сначала создайте Maven‑проект (или Gradle, если предпочитаете) и добавьте зависимость Aspose.Cells:

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.10</version>
    <classifier>jdk17</classifier>
</dependency>
```

Теперь импортируйте необходимые классы:

```java
import com.aspose.cells.*;
import java.io.IOException;
```

> **Pro tip:** держите папку `src/main/resources` в порядке; разместите `source.xlsx` там и обращайтесь к ней через относительный путь, чтобы избежать жёстко заданных абсолютных каталогов.

## Шаг 2: Загрузка исходной книги, содержащей сводную таблицу

Первая строка любой операции **copy pivot table excel** — загрузить книгу, в которой находится сводная таблица, которую вы хотите дублировать.

```java
// Step 2: Load the source workbook that contains the pivot table
Workbook srcWb = new Workbook("src/main/resources/source.xlsx");
```

Почему мы загружаем всю книгу, а не только лист? Потому что кэш сводной таблицы находится на уровне книги; копирование только листа разрушит кэш, и ваша сводная таблица превратится в обычный диапазон.

## Шаг 3: Получение листа и определение диапазона сводной таблицы

Далее мы находим лист и точный блок ячеек, охватывающий сводную таблицу. В большинстве случаев сводная таблица начинается с `A1`, но вам следует скорректировать диапазон под ваш файл.

```java
// Step 3: Access the worksheet where the pivot table resides
Worksheet srcWs = srcWb.getWorksheets().get(0);

// Define the range that includes the pivot table (e.g., A1:E20)
Range srcRange = srcWs.getCells().createRange("A1:E20");
```

Если вы не уверены в диапазоне, можете позволить Aspose.Cells вычислить используемые ячейки:

```java
int maxRow = srcWs.getCells().getMaxDataRow();
int maxCol = srcWs.getCells().getMaxDataColumn();
String autoRange = String.format("A1:%s%d",
        CellsHelper.columnIndexToName(maxCol), maxRow + 1);
Range srcRange = srcWs.getCells().createRange(autoRange);
```

Этот небольшой фрагмент полезен, когда нужно **copy range to another workbook** без жёсткого указания адреса.

## Шаг 4: Создание целевой книги

Теперь мы создаём новую книгу, которая получит скопированную сводную таблицу. Это суть **how to copy pivot table** — вы создаёте чистый лист и затем вставляете диапазон.

```java
// Step 4: Create a new destination workbook (or load an existing one)
Workbook dstWb = new Workbook(); // empty workbook by default
```

Если у вас уже есть шаблонный файл, который нужно дополнить, просто замените конструктор на `new Workbook("template.xlsx")`.

## Шаг 5: Добавление листа в целевую книгу

Хотя новая `Workbook` уже содержит один лист по умолчанию, мы добавим второй лист, чтобы продемонстрировать процесс копирования в определённое место.

```java
// Step 5: Add a new worksheet to the destination workbook
Worksheet dstWs = dstWb.getWorksheets().add();
```

Вы можете переименовать лист для ясности:

```java
dstWs.setName("CopiedPivot");
```

## Шаг 6: Копирование диапазона — сводная таблица сохраняется

Вот волшебная строка, которая действительно **copy range to another workbook**, сохраняя сводную таблицу нетронутой. Объект `CopyOptions` указывает Aspose.Cells сохранять всё, включая кэш сводной таблицы.

```java
// Step 6: Copy the range—pivot table is preserved—to the new worksheet at A1
CopyOptions copyOptions = new CopyOptions();
copyOptions.setPasteType(PasteType.PASTE_ALL);
dstWs.getCells().copyRange(srcRange, "A1", copyOptions);
```

Зачем мы устанавливаем `PasteType.PASTE_ALL`? Потому что операция вставки по умолчанию копирует только значения и форматирование, отбрасывая кэш сводной таблицы. Явно запрашивая `PASTE_ALL`, мы гарантируем, что целевая книга получит полностью функциональную сводную таблицу.

## Шаг 7: Сохранение целевой книги

Наконец, запишите новый файл на диск. После этого шага вы можете открыть `destination.xlsx` в Excel и увидеть сводную таблицу точно такой же, как в исходном файле.

```java
// Step 7: Save the destination workbook with the copied pivot table
dstWb.save("src/main/resources/destination.xlsx");
```

### Ожидаемый результат

- При открытии `destination.xlsx` отображается лист с именем **CopiedPivot**.
- На листе находится сводная таблица, которую можно обновлять, фильтровать и перестраивать, как оригинал.
- В консоли не появляется сообщений об ошибках, подтверждая успешное выполнение **copy pivot table excel**.

## Часто задаваемые вопросы и особые случаи

### Что делать, если в исходной книге несколько сводных таблиц?

Вы можете повторить логику выбора диапазона для каждой сводной таблицы, либо скопировать весь лист:

```java
srcWs.getCells().copy(dstWs.getCells());
```

Копирование всего листа также переносит все кэши сводных таблиц, что делает его быстрым способом **copy range to another workbook**, когда у вас много таблиц.

### Как работать с внешними соединениями данных?

Если ваша сводная таблица получает данные из внешней базы, целевая книга сохранит строку соединения. Чтобы избежать разорванных ссылок, обновите соединение после копирования:

```java
PivotTable pt = dstWs.getPivotTables().get(0);
pt.getPivotCache().setExternalDataSource("newConnectionString");
```

### Работает ли это с файлами .xls?

Да. Aspose.Cells абстрагирует формат файла, поэтому тот же код работает с `.xls`, `.xlsx`, `.xlsb` и даже `.ods`. Просто измените расширение файла в конструкторах `Workbook`.

## Полный рабочий пример

Объединив всё вместе, представляем готовый к запуску класс Java, демонстрирующий **how to copy pivot table** из одной книги в другую:

```java
import com.aspose.cells.*;

public class CopyPivotTableExcel {
    public static void main(String[] args) throws Exception {
        // Load source workbook containing the pivot table
        Workbook srcWb = new Workbook("src/main/resources/source.xlsx");
        Worksheet srcWs = srcWb.getWorksheets().get(0);

        // Determine the used range automatically (covers the pivot table)
        int maxRow = srcWs.getCells().getMaxDataRow();
        int maxCol = srcWs.getCells().getMaxDataColumn();
        String rangeAddress = String.format("A1:%s%d",
                CellsHelper.columnIndexToName(maxCol), maxRow + 1);
        Range srcRange = srcWs.getCells().createRange(rangeAddress);

        // Create destination workbook and add a sheet
        Workbook dstWb = new Workbook();
        Worksheet dstWs = dstWb.getWorksheets().add();
        dstWs.setName("CopiedPivot");

        // Copy the range with all pivot information preserved
        CopyOptions opts = new CopyOptions();
        opts.setPasteType(PasteType.PASTE_ALL);
        dstWs.getCells().copyRange(srcRange, "A1", opts);

        // Save the result
        dstWb.save("src/main/resources/destination.xlsx");
        System.out.println("Pivot table copied successfully!");
    }
}
```

Запустите класс, откройте `destination.xlsx`, и вы увидите точную копию оригинальной сводной таблицы. 🎉

## Заключение

Мы только что прошли полный процесс **copy pivot table excel** с использованием Java. Загрузив исходную книгу, определив диапазон сводной таблицы и применив `CopyOptions` с `PASTE_ALL`, вы можете надёжно **copy range to another workbook**, сохраняя все возможности сводной таблицы.  

Если вам интересно, как **how to copy pivot table** в других языках, те же концепции применимы — просто замените Aspose.Cells SDK на соответствующую платформу. Далее вы можете исследовать программное обновление скопированной сводной таблицы или экспорт её в PDF для отчётности.  

Есть свои варианты этого сценария? Возможно, вам нужно скопировать график, привязанный к сводной таблице, или обработать пакетно десятки файлов. Эти темы являются естественными продолжениями того, что мы рассмотрели сегодня.  

Попробуйте код, подкорректируйте диапазон, и пусть ваши приключения по автоматизации Excel начнутся. Счастливого кодинга!

## Что стоит изучить дальше?

Следующие руководства охватывают тесно связанные темы, построенные на техниках, продемонстрированных в этом руководстве. Каждый ресурс включает полные рабочие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы к реализации в ваших проектах.

- [How to Update Excel Pivot Table Source with Aspose.Cells for Java: A Comprehensive Guide](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [Automate Excel Pivot Table Styling and Saving with Aspose.Cells for Java: A Comprehensive Guide](/cells/english/java/data-analysis/excel-pivot-table-styling-saving-aspose-cells-java/)
- [Excel Pivot Table Manipulation with Aspose.Cells Java: A Comprehensive Guide](/cells/english/java/data-analysis/excel-pivot-table-manipulation-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}