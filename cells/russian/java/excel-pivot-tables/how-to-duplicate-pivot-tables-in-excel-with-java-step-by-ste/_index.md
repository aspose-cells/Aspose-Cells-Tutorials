---
category: general
date: 2026-10-07
description: Узнайте, как дублировать сводные таблицы в Excel с помощью Java и Aspose.Cells.
  Быстро скопируйте сводную таблицу, копируя её диапазон между книгами.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to duplicate pivot
- copy pivot table
- copy excel range
- copy range between workbooks
- how to copy pivot table
language: ru
lastmod: 2026-10-07
og_description: Как дублировать сводные таблицы в Excel с помощью Java и Aspose.Cells.
  Следуйте этому руководству, чтобы скопировать сводную таблицу, копируя её диапазон
  между рабочими книгами.
og_image_alt: Illustration of copying an Excel pivot table from one workbook to another
og_title: Как дублировать сводные таблицы в Excel с помощью Java – полный учебник
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: Learn how to duplicate pivot tables in Excel using Java and Aspose.Cells.
    Copy a pivot table by copying its range between workbooks quickly.
  headline: How to duplicate pivot tables in Excel with Java – step‑by‑step guide
  type: TechArticle
- description: Learn how to duplicate pivot tables in Excel using Java and Aspose.Cells.
    Copy a pivot table by copying its range between workbooks quickly.
  name: How to duplicate pivot tables in Excel with Java – step‑by‑step guide
  steps:
  - name: Explanation of each step
    text: '| Step | What the code does | Why it matters for **copy pivot table** |
      |------|-------------------|----------------------------------------| | **1️⃣
      Load source workbook** | `new Workbook(srcPath)` reads `Source.xlsx`. | The
      source file is the only place where the original pivot exists. | | **2️⃣ D'
  - name: 1️⃣ Copying a pivot that spans multiple sheets
    text: 'If the pivot’s source data lives on a different sheet than the pivot itself,
      include both sheets in the copy operation. The simplest approach is to copy
      the entire source sheet first, then copy the pivot sheet:'
  - name: 2️⃣ Dealing with named ranges
    text: 'Aspose.Cells preserves named ranges when you copy a range. However, if
      the destination workbook already contains a name with the same identifier, a
      `CellsException` is thrown. Resolve this by renaming the conflicting name before
      the copy:'
  - name: 3️⃣ Large workbooks and performance
    text: 'Copying very large ranges (hundreds of thousands of rows) can be memory‑intensive.
      Enable **memory optimization**:'
  - name: 4️⃣ Keeping formulas intact
    text: If the source range contains formulas that reference cells outside the copied
      area, those references become broken after the copy. To avoid this, expand the
      range to include all dependent cells, or use `copyRange` with the `CopyOptions`
      flag `CopyOptions.COPY_FORMULA`.
  type: HowTo
tags:
- Excel
- Java
- Aspose.Cells
- PivotTable
- Data manipulation
title: Как дублировать сводные таблицы в Excel с помощью Java — пошаговое руководство
url: /ru/java/excel-pivot-tables/how-to-duplicate-pivot-tables-in-excel-with-java-step-by-ste/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как дублировать сводные таблицы в Excel с помощью Java – пошаговое руководство

Если вам нужно **how to duplicate pivot** таблицы в рабочей книге Excel, этот учебник покажет вам полное готовое решение. С помощью Aspose.Cells for Java вы можете скопировать сводную таблицу вместе с её исходными данными, скопировав базовый диапазон, а затем сохранив результат как новую рабочую книгу.

Дублирование сводной таблицы часто кажется сложным, потому что кэш сводной таблицы скрыт внутри листа. Копируя весь диапазон, содержащий сводную таблицу, Aspose.Cells автоматически воссоздаёт кэш в целевой рабочей книге, поэтому вы получаете полностью функциональную копию без ручного вмешательства в XML.

В этом руководстве вы:

* Загрузите исходную рабочую книгу, содержащую сводную таблицу.  
* Определите точный диапазон, в котором находится сводная таблица.  
* Скопируете этот диапазон в новую рабочую книгу, сохранив определение сводной таблицы.  
* Сохраните новый файл и проверите, что сводная таблица работает.  

Шаги работают с любой версией Excel, поддерживаемой Aspose.Cells (2007‑2024), и требуют всего несколько строк кода на Java.

## Prerequisites

| Требование | Почему это важно |
|-------------|----------------|
| **Java 8 or newer** | Aspose.Cells построен для Java 8+. |
| **Aspose.Cells for Java** (latest version) | Предоставляет API `Workbook`, `Range` и `CopyRange`, используемые в примере. |
| **Source workbook** with a pivot table (e.g., `Source.xlsx`) | Сводная таблица, которую вы хотите дублировать. |
| **Write permission** to the target directory | Необходимо для сохранения `CopyWithPivot.xlsx`. |

Добавьте зависимость Aspose.Cells Maven в ваш `pom.xml` (или загрузите JAR вручную):

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version>   <!-- use the latest stable version -->
</dependency>
```

## Как дублировать сводные таблицы – полная реализация

Ниже приведена автономная Java‑программа, демонстрирующая **how to duplicate pivot** таблицы путем копирования диапазона, содержащего сводную таблицу. Код включает обработку ошибок, комментарии и шаг проверки.

```java
// File: DuplicatePivot.java
import com.aspose.cells.*;

public class DuplicatePivot {
    public static void main(String[] args) {
        // 1️⃣ Load the source workbook that holds the pivot table.
        String srcPath = "YOUR_DIRECTORY/Source.xlsx";
        Workbook srcWb;
        try {
            srcWb = new Workbook(srcPath);
        } catch (Exception e) {
            System.err.println("Failed to load source workbook: " + e.getMessage());
            return;
        }

        // 2️⃣ Identify the range that encloses the pivot table.
        // Adjust the sheet index (0‑based) and address as needed.
        Worksheet srcSheet = srcWb.getWorksheets().get(0);
        // Example address "A1:G20" – includes the pivot and its data source.
        String pivotRangeAddress = "A1:G20";
        Range srcRange = srcSheet.getCells().createRange(pivotRangeAddress);

        // 3️⃣ Create a destination workbook and copy the identified range.
        Workbook destWb = new Workbook(); // starts with a blank workbook
        Worksheet destSheet = destWb.getWorksheets().get(0);
        try {
            // copyRange copies both values and the internal pivot cache.
            destSheet.getCells().copyRange(srcRange, "A1");
        } catch (Exception e) {
            System.err.println("Failed to copy range: " + e.getMessage());
            return;
        }

        // 4️⃣ (Optional) Refresh the pivot so it reflects the copied data.
        // Aspose.Cells automatically rebuilds the cache, but calling refresh
        // guarantees up‑to‑date results if the source data has changed.
        for (int i = 0; i < destSheet.getPivotTables().getCount(); i++) {
            destSheet.getPivotTables().get(i).refresh();
        }

        // 5️⃣ Save the new workbook that now contains the duplicated pivot.
        String destPath = "YOUR_DIRECTORY/CopyWithPivot.xlsx";
        try {
            destWb.save(destPath);
            System.out.println("Pivot table duplicated successfully to: " + destPath);
        } catch (Exception e) {
            System.err.println("Failed to save destination workbook: " + e.getMessage());
        }
    }
}
```

### Пояснение каждого шага

| Шаг | Что делает код | Почему это важно для **copy pivot table** |
|------|-------------------|----------------------------------------|
| **1️⃣ Load source workbook** | `new Workbook(srcPath)` reads `Source.xlsx`. | Исходный файл — единственное место, где находится оригинальная сводная таблица. |
| **2️⃣ Define the range** | `createRange("A1:G20")` creates a `Range` object that covers the pivot and its data. | Сводная таблица хранится вместе со своим кэшем; копирование всего диапазона гарантирует перемещение кэша. |
| **3️⃣ Copy the range** | `copyRange(srcRange, "A1")` writes the range into the destination sheet. | Это ядро **copy range between workbooks** — API автоматически обрабатывает скрытые объекты. |
| **4️⃣ Refresh pivot** | `pivotTable.refresh()` forces the pivot to recalculate. | Гарантирует, что дублированная сводная таблица показывает те же значения, что и оригинальная, особенно после изменений. |
| **5️⃣ Save workbook** | `destWb.save(destPath)` writes the file to disk. | Создаёт окончательный результат **copy excel range**, который можно открыть в Excel. |

#### Ожидаемый результат

После запуска программы откройте `CopyWithPivot.xlsx`. Вы увидите лист, полностью идентичный исходному, и сводная таблица будет работать точно так же, как оригинальная – вы сможете разворачивать строки, фильтровать поля и обновлять данные без ошибок.

## Общие варианты и граничные случаи

### 1️⃣ Копирование сводной таблицы, охватывающей несколько листов

Если исходные данные сводной таблицы находятся на другом листе, чем сама сводная таблица, включите оба листа в операцию копирования. Самый простой подход – сначала скопировать весь исходный лист, затем скопировать лист со сводной таблицей:

```java
// Copy source data sheet
Workbook temp = new Workbook(); // temporary workbook for the data sheet
temp.getWorksheets().addCopy(srcWb.getWorksheets().get(0));
Workbook dest = new Workbook();
dest.getWorksheets().addCopy(temp.getWorksheets().get(0));

// Then copy the pivot sheet as shown earlier
```

### 2️⃣ Работа с именованными диапазонами

Aspose.Cells сохраняет именованные диапазоны при копировании диапазона. Однако, если целевая рабочая книга уже содержит имя с тем же идентификатором, будет выброшено `CellsException`. Решите проблему, переименовав конфликтующее имя перед копированием:

```java
if (destWb.getWorksheets().get(0).getNames().containsKey("MyRange")) {
    destWb.getWorksheets().get(0).getNames().remove("MyRange");
}
```

### 3️⃣ Большие рабочие книги и производительность

Копирование очень больших диапазонов (сотни тысяч строк) может требовать много памяти. Включите **memory optimization**:

```java
LoadOptions loadOptions = new LoadOptions(LoadFormat.XLSX);
loadOptions.setMemorySetting(MemorySetting.MEMORY_PREFERENCE);
Workbook largeSrc = new Workbook(srcPath, loadOptions);
```

### 4️⃣ Сохранение формул без изменений

Если исходный диапазон содержит формулы, ссылающиеся на ячейки за пределами копируемой области, после копирования такие ссылки будут нарушены. Чтобы избежать этого, расширьте диапазон, включив все зависимые ячейки, или используйте `copyRange` с флагом `CopyOptions` — `CopyOptions.COPY_FORMULA`.

```java
CopyOptions options = new CopyOptions();
options.setCopyFormula(true);
destSheet.getCells().copyRange(srcRange, "A1", options);
```

## Профессиональные советы для надёжного **copy range between workbooks**

* **Always use absolute addresses** (`$A$1:$G$20`) when the source sheet may be renamed.  
* **Refresh after copy** – even though Aspose.Cells rebuilds the cache, calling `refresh()` eliminates occasional stale‑cache warnings in Excel.  
* **Validate the pivot**: after saving, open the file programmatically and call `pivotTable.validate()` to ensure no broken references.  
* **Version compatibility**: the code works with Excel 2007‑2024 files (`.xlsx`, `.xlsm`). For legacy `.xls` files, set `LoadOptions.setLoadFormat(LoadFormat.XLS)`.

## Полный листинг исходного кода (готов к компиляции)

```java
import com.aspose.cells.*;

public class DuplicatePivot {
    public static void main(String[] args) {
        // --------------------------------------------------------------------
        // 1️⃣ Load source workbook
        // --------------------------------------------------------------------
        String srcPath = "YOUR_DIRECTORY/Source.xlsx";
        Workbook srcWb;
        try {
            srcWb = new Workbook(srcPath);
        } catch (Exception e) {
            System.err.println("Failed to load source workbook: " + e.getMessage());
            return;
        }

        // --------------------------------------------------------------------
        // 2️⃣ Define the range that contains the pivot table
        // --------------------------------------------------------------------
        Worksheet srcSheet = srcWb.getWorksheets().get(0);
        String pivotRangeAddress = "A1:G20"; // adjust to your pivot's actual area
        Range srcRange = srcSheet.getCells().createRange(pivotRangeAddress);

        // --------------------------------------------------------------------
        // 3️⃣ Copy the range (including the pivot) to a new workbook
        // --------------------------------------------------------------------
        Workbook destWb = new Workbook(); // blank workbook
        Worksheet destSheet = destWb.getWorksheets().get(0);
        try {
            destSheet.getCells().copyRange(srcRange, "A1");
        } catch (Exception e) {
            System.err.println("Failed to copy range: " + e.getMessage());
            return;
        }

        // --------------------------------------------------------------------
        // 4️⃣ Refresh the duplicated pivot (ensures correct values)
        // --------------------------------------------------------------------
        for (int i = 0; i < destSheet.getPivotTables().getCount(); i++) {
            destSheet


## Что вам стоит изучить дальше?

Следующие учебники охватывают тесно связанные темы, построенные на техниках, продемонстрированных в этом руководстве. Каждый ресурс включает полные рабочие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы к реализации в собственных проектах.

- [Как скопировать сводную таблицу в Java – Полное руководство Aspose.Cells](/cells/english/java/excel-pivot-tables/how-to-copy-pivot-table-in-java-complete-aspose-cells-guide/)
- [Как создавать сводные таблицы в Excel с помощью Aspose.Cells for Java: Полное руководство](/cells/english/java/data-analysis/create-pivot-tables-excel-aspose-cells-java/)
- [Как обновить источник сводной таблицы Excel с помощью Aspose.Cells for Java: Полное руководство](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}