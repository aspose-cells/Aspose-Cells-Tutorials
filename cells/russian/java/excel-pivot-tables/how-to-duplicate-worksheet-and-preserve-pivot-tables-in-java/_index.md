---
category: general
date: 2026-08-17
description: Как дублировать рабочий лист в Java с помощью Aspose.Cells, сохраняя
  сводную таблицу, копировать сводную таблицу в новую книгу и создавать книгу из листа.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to duplicate worksheet
- how to copy pivot
- how to preserve pivot
- copy pivot to workbook
- create workbook from sheet
language: ru
lastmod: 2026-08-17
og_description: Как дублировать лист в Java с помощью Aspose.Cells, сохраняя сводную
  таблицу, копировать сводную таблицу в новую книгу и создавать книгу из листа — все
  шаги объяснены.
og_image_alt: Screenshot of Java code duplicating an Excel worksheet with a pivot
  table using Aspose.Cells
og_title: Как дублировать лист и сохранить сводные таблицы – руководство по Java
schemas:
- author: Aspose
  dateModified: '2026-08-17'
  description: How to duplicate worksheet in Java using Aspose.Cells, preserving the
    pivot table, copying pivot to a new workbook, and creating a workbook from a sheet.
  headline: How to duplicate worksheet and preserve pivot tables in Java
  type: TechArticle
- description: How to duplicate worksheet in Java using Aspose.Cells, preserving the
    pivot table, copying pivot to a new workbook, and creating a workbook from a sheet.
  name: How to duplicate worksheet and preserve pivot tables in Java
  steps:
  - name: – Load the workbook that contains the pivot table
    text: '```java import com.aspose.cells.*;'
  - name: – Create a new workbook and duplicate the entire worksheet
    text: '```java // Create an empty destination workbook Workbook destinationWorkbook
      = new Workbook();'
  - name: – Save the new workbook
    text: '```java // Save the duplicated workbook; the pivot remains functional destinationWorkbook.save("YOUR_DIRECTORY/copy_with_pivot.xlsx");
      } } ```'
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel
- Pivot Table
- Workbook
title: Как дублировать лист и сохранять сводные таблицы в Java
url: /ru/java/excel-pivot-tables/how-to-duplicate-worksheet-and-preserve-pivot-tables-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как дублировать лист и сохранять сводные таблицы в Java

Дублирование листа с сохранением его сводной таблицы — частая необходимость при автоматизации отчетности Excel. В этом руководстве показано, как скопировать сводную таблицу в новую книгу с помощью Aspose.Cells for Java, а также как сохранить сводную таблицу при создании книги из листа.

Вы узнаете, как загрузить существующую книгу, дублировать лист, содержащий сводную таблицу, и сохранить результат в новый файл. Руководство предполагает наличие базовой среды разработки Java и действующей лицензии Aspose.Cells (бесплатная оценочная версия подходит для тестирования). Никакие внешние инструменты, кроме JAR‑файла Aspose.Cells, не требуются.

## Prerequisites

Перед началом убедитесь, что у вас есть:

* Java Development Kit (JDK) 8 или новее.  
* Maven или Gradle для управления зависимостью Aspose.Cells.  
* Файл Excel (`source.xlsx`), содержащий как минимум одну сводную таблицу на первом листе.  
* Каталог, в котором вы можете читать исходный файл и записывать дублированную книгу.

Add the Aspose.Cells dependency to your `pom.xml` (Maven) or `build.gradle` (Gradle). For Maven:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version> <!-- use the latest version -->
</dependency>
```

## Как дублировать лист со сводной таблицей

Основная операция состоит из трёх шагов: загрузка, копирование и сохранение. Каждый шаг описан ниже.

### Step 1 – Load the workbook that contains the pivot table

```java
import com.aspose.cells.*;

public class CopyPivotTable {
    public static void main(String[] args) throws Exception {
        // Load the source workbook that holds the pivot table
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/source.xlsx");
        Worksheet sourceWorksheet = sourceWorkbook.getWorksheets().get(0);
```

*Why this step matters*: Объект `Workbook` представляет весь файл Excel. Получая первый лист (`get(0)`), вы нацеливаетесь на лист, содержащий сводную таблицу, которую планируете дублировать.

### Step 2 – Create a new workbook and duplicate the entire worksheet

```java
        // Create an empty destination workbook
        Workbook destinationWorkbook = new Workbook();

        // Duplicate the source worksheet, preserving its pivot table
        destinationWorkbook.getWorksheets().addCopy(sourceWorksheet);
```

`addCopy` клонирует лист **включая** все встроенные объекты, формулы и кэши сводных таблиц. Это рекомендуемый способ **how to copy pivot**, потому что определение сводной таблицы и её источник данных передаются вместе.

### Step 3 – Save the new workbook

```java
        // Save the duplicated workbook; the pivot remains functional
        destinationWorkbook.save("YOUR_DIRECTORY/copy_with_pivot.xlsx");
    }
}
```

После выполнения `copy_with_pivot.xlsx` содержит точную копию оригинального листа, и сводная таблица работает без дополнительной настройки.

**Expected result**: Открывая `copy_with_pivot.xlsx` в Excel, вы видите дублированный лист с тем же макетом сводной таблицы, фильтрами и вычисляемыми полями, что и в исходном файле.

## Как скопировать сводную таблицу в другую книгу

Если нужно переместить сводную таблицу без копирования всего листа, можно извлечь кэш сводной таблицы и присоединить его к новому листу. Ниже показан соответствующий фрагмент кода:

```java
// Assume sourceWorkbook and sourceWorksheet are already loaded
PivotTable pivot = sourceWorksheet.getPivotTables().get(0);

// Create a new workbook and a blank worksheet
Workbook targetWorkbook = new Workbook();
Worksheet targetSheet = targetWorkbook.getWorksheets().add("PivotCopy");

// Import the pivot table definition
targetSheet.getPivotTables().addCopy(pivot);
targetWorkbook.save("YOUR_DIRECTORY/pivot_only_copy.xlsx");
```

Этот код отвечает на **how to copy pivot**, копируя только объект сводной таблицы, а не весь лист. Метод `addCopy` в коллекции `PivotTables` гарантирует дублирование кэша сводной таблицы, удовлетворяя требованиям **how to preserve pivot**.

## Как сохранить сводную таблицу при создании книги из листа

Иногда вы начинаете с листа, который не принадлежит ни одной книге (например, генерируете лист в памяти). Чтобы **create workbook from sheet**, сохранив сводную таблицу, выполните следующие шаги:

```java
// Create a worksheet in memory
Worksheet tempSheet = new Worksheet();
PivotTable pivot = tempSheet.getPivotTables().add("A1", "B10", "MyPivot");

// Configure the pivot source range, rows, columns, data fields, etc.
// (Omitted for brevity – see Aspose.Cells docs for detailed setup)

// Wrap the worksheet in a new workbook
Workbook newWorkbook = new Workbook();
newWorkbook.getWorksheets().addCopy(tempSheet);
newWorkbook.save("YOUR_DIRECTORY/created_from_sheet.xlsx");
```

Добавляя лист в новую `Workbook` после полного определения сводной таблицы, вы гарантируете, что **how to preserve pivot** работает даже тогда, когда лист был создан вне существующего файла.

## Practical tips and common pitfalls

| Совет | Почему это важно |
|------|-------------------|
| Используйте `addCopy` вместо `copy` | `addCopy` клонирует базовый кэш сводных таблиц; простой `copy` может потерять связь с источником данных. |
| Храните исходные и целевые файлы в одной файловой системе | Относительные пути в источнике данных сводной таблицы разрешаются корректно, уменьшая ошибки «source not found». |
| Проверьте кэш сводной таблицы после копирования | Вызовите `pivot.refresh()`, если исходные данные изменились между копированием и сохранением. |
| Освобождайте книги после использования | `sourceWorkbook.dispose();` освобождает нативные ресурсы, что важно для больших файлов. |

## Edge cases you might encounter

* **Несколько листов со взаимозависимыми сводными таблицами** – копируйте каждый лист отдельно; общие кэши дублируются автоматически, но может потребоваться переназначить внешние соединения данных.  
* **Сводные таблицы, основанные на внешних SQL‑запросах** – убедитесь, что целевая среда имеет доступ к той же базе данных; иначе сводная таблица покажет ошибки «#REF!».  
* **Большие книги (>100 MB)** – используйте `WorkbookSettings.setMemorySetting(MemorySetting.MEMORY_PREFERENCE)`, чтобы снизить нагрузку на память во время операции копирования.

## Complete, runnable example

Ниже приведена полная программа, включающая все обсуждаемые шаги. Сохраните её как `CopyPivotTable.java`, скорректируйте пути к файлам и запустите в предпочитаемой IDE или через `javac`/`java`.



## Что стоит изучить дальше?

Следующие руководства охватывают тесно связанные темы, расширяющие техники, продемонстрированные в этом руководстве. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, помогая вам освоить дополнительные возможности API и исследовать альтернативные подходы в собственных проектах.

- [Как создавать сводные таблицы в Excel с помощью Aspose.Cells for Java: Полное руководство](/cells/english/java/data-analysis/create-pivot-tables-excel-aspose-cells-java/)
- [Как обновлять источник данных сводной таблицы Excel с помощью Aspose.Cells for Java: Полное руководство](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [Как реализовать срезы в сводных таблицах с помощью Aspose.Cells for Java: Полное руководство](/cells/english/java/data-analysis/implement-slicers-pivot-tables-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}