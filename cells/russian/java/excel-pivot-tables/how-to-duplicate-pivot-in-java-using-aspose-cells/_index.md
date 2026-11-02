---
category: general
date: 2026-09-18
description: как дублировать сводную таблицу в Java с помощью Aspose.Cells — быстро
  и надёжно копировать сводную таблицу между рабочими книгами.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to duplicate pivot
- copy range between workbooks
- how to copy pivot
- copy pivot to workbook
- load excel workbook java
language: ru
lastmod: 2026-09-18
og_description: как дублировать сводную таблицу в Java с помощью Aspose.Cells. Следуйте
  этому полному руководству, чтобы скопировать сводную таблицу между рабочими книгами
  с чистым Java‑кодом.
og_image_alt: Screenshot showing a Java IDE copying a pivot table between two Excel
  workbooks
og_title: Дублирование сводной таблицы в Java — пошаговое руководство
schemas:
- author: Aspose
  dateModified: '2026-09-18'
  description: how to duplicate pivot in Java with Aspose.Cells – copy a pivot table
    between workbooks quickly and reliably.
  headline: How to duplicate pivot in Java using Aspose.Cells
  type: TechArticle
- description: how to duplicate pivot in Java with Aspose.Cells – copy a pivot table
    between workbooks quickly and reliably.
  name: How to duplicate pivot in Java using Aspose.Cells
  steps:
  - name: '**Load the source workbook** – this gives you access to the worksheet that
      holds the pivot.'
    text: '**Load the source workbook** – this gives you access to the worksheet that
      holds the pivot.'
  - name: '**Define the cell area** that encloses the pivot.'
    text: '**Define the cell area** that encloses the pivot.'
  - name: '**Create a destination workbook** – an empty file that will receive the
      copied range.'
    text: '**Create a destination workbook** – an empty file that will receive the
      copied range.'
  - name: '**Copy the range** – Aspose.Cells automatically duplicates the pivot definition.'
    text: '**Copy the range** – Aspose.Cells automatically duplicates the pivot definition.'
  - name: '**Save the destination workbook** – you now have a separate file with the
      same pivot.'
    text: '**Save the destination workbook** – you now have a separate file with the
      same pivot.'
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: Как дублировать сводную таблицу в Java с помощью Aspose.Cells
url: /ru/java/excel-pivot-tables/how-to-duplicate-pivot-in-java-using-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как дублировать сводную таблицу в Java с помощью Aspose.Cells

Если вам нужно **как дублировать сводную таблицу** в Java‑приложении, это руководство покажет точные шаги. Загрузив Excel‑книгу, определив область ячеек сводной таблицы и скопировав этот диапазон в новую книгу, вы сможете переместить сводную таблицу, не потеряв её определение и данные.

Копирование сводной таблицы — распространённая задача при генерации отчётов, архивировании анализов или разбиении большой книги на модульные части. В этом учебнике вы узнаете, как **копировать диапазон между книгами**, как **загружать Excel‑книгу Java** и нюансы **как безопасно копировать сводную таблицу**.

В конце вы получите готовую к запуску Java‑программу, которая дублирует сводную таблицу из `Source.xlsx` в `PivotCopied.xlsx` с помощью Aspose.Cells for Java.

## Требования

Прежде чем начать, убедитесь, что у вас есть:

* JDK 8 или новее.
* Maven (или другой инструмент сборки) для управления зависимостями.
* Aspose.Cells for Java версии 23.10 или новее. Добавьте следующую зависимость Maven в ваш `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.10</version>
    <classifier>jdk17</classifier> <!-- adjust classifier to your JDK version -->
</dependency>
```

* Исходная книга (`Source.xlsx`), содержащая сводную таблицу в диапазоне **A1:H30**.

## Как дублировать сводную таблицу в Java

Суть проста:

1. **Загрузить исходную книгу** — это даст доступ к листу, где находится сводная таблица.
2. **Определить область ячеек**, охватывающую сводную таблицу.
3. **Создать целевую книгу** — пустой файл, который получит скопированный диапазон.
4. **Скопировать диапазон** — Aspose.Cells автоматически дублирует определение сводной таблицы.
5. **Сохранить целевую книгу** — теперь у вас есть отдельный файл с той же сводной таблицей.

Ниже приведена полная, готовая к запуску Java‑программа, реализующая эти шаги.

```java
package com.example.excelpivot;

import com.aspose.cells.*;

public class DuplicatePivotExample {

    public static void main(String[] args) throws Exception {
        // ---------- Step 1: Load the source workbook ----------
        // Replace the path with the actual location of your source file.
        String srcPath = "YOUR_DIRECTORY/Source.xlsx";
        Workbook srcWorkbook = new Workbook(srcPath);
        // The first worksheet (index 0) contains the pivot table.
        Worksheet srcWorksheet = srcWorkbook.getWorksheets().get(0);

        // ---------- Step 2: Define the cell area that contains the pivot ----------
        // The pivot occupies A1:H30 in the source sheet.
        CellArea srcRange = CellArea.create("A1", "H30");

        // ---------- Step 3: Create a new workbook for the copy ----------
        Workbook destWorkbook = new Workbook();               // creates a blank workbook
        Worksheet destWorksheet = destWorkbook.getWorksheets().get(0);

        // ---------- Step 4: Copy the range (pivot table is duplicated automatically) ----------
        // CopyOptions can be left default; it ensures that all formatting and pivot objects are preserved.
        srcWorksheet.copyRange(srcRange, destWorksheet, "A1", new CopyOptions());

        // ---------- Step 5: Save the destination workbook ----------
        String destPath = "YOUR_DIRECTORY/PivotCopied.xlsx";
        destWorkbook.save(destPath);

        System.out.println("Pivot table duplicated successfully to " + destPath);
    }
}
```

### Почему это работает

* **Aspose.Cells** рассматривает сводную таблицу как часть коллекции ячеек листа. При вызове `copyRange` библиотека копирует не только значения ячеек, но и подлежащий кэш и определение сводной таблицы, поэтому новая книга содержит полностью рабочую копию.
* Объект `CopyOptions` по умолчанию сохраняет формулы, форматы и встроенные объекты. При необходимости вы можете настроить его (например, `setCopyColumnWidths(true)`), если требуется дополнительный контроль.

## Копирование диапазона между книгами — более подробный взгляд

В примере выше копируется один непрерывный блок, но `copyRange` может работать с любым прямоугольным участком. Если ваша сводная таблица охватывает несмежные диапазоны, вы можете вызвать `copyRange` несколько раз или использовать `Worksheet.copy` для дублирования всего листа.

```java
// Example: copy the whole sheet, preserving all pivots and charts
srcWorksheet.copy(destWorksheet, new CopyOptions());
```

**Совет:** При копировании больших книг включайте `CopyOptions.setPreserveCellStyle(true)`, чтобы избежать избыточного дублирования стилей, что повышает производительность.

## Как копировать сводную таблицу в книгу — работа с несколькими сводными

Если на исходном листе более одной сводной таблицы, можно пройтись по всем сводным таблицам листа и скопировать каждую отдельно:

```java
for (int i = 0; i < srcWorksheet.getPivotTables().getCount(); i++) {
    PivotTable pt = srcWorksheet.getPivotTables().get(i);
    // Determine the range that the pivot occupies
    CellArea pivotArea = pt.getPivotTableArea();
    srcWorksheet.copyRange(pivotArea, destWorksheet, pt.getName() + "!A1", new CopyOptions());
}
```

Такой подход гарантирует, что каждая сводная таблица сохраняет своё оригинальное имя и источник данных.

## Загрузка Excel‑книги Java — типичные подводные камни

* **Разделители путей:** используйте прямые слеши (`/`) или `File.separator`, чтобы код был независим от платформы.
* **Отсутствие лицензии:** Aspose.Cells работает в режиме оценки, но в выводе будет водяной знак. Зарегистрируйте лицензию с помощью `License license = new License(); license.setLicense("Aspose.Total.Java.lic");` перед загрузкой книги, чтобы убрать водяной знак.
* **Большие файлы:** Для книг более 100 МБ рассмотрите использование `WorkbookFactory.create(InputStream, new LoadOptions(LoadFormat.XLSX))` с потоковыми опциями, чтобы снизить потребление памяти.

## Полный пример от начала до конца

Объединив всё, получаем окончательную программу, которую можно скопировать и вставить в IDE:

```java
package com.example.excelpivot;

import com.aspose.cells.*;

public class DuplicatePivotExample {
    public static void main(String[] args) throws Exception {
        // Load license (optional, removes evaluation watermark)
        // License lic = new License();
        // lic.setLicense("Aspose.Total.Java.lic");

        // 1️⃣ Load source workbook
        Workbook srcWorkbook = new Workbook("YOUR_DIRECTORY/Source.xlsx");
        Worksheet srcWorksheet = srcWorkbook.getWorksheets().get(0);

        // 2️⃣ Define pivot range (A1:H30)
        CellArea srcRange = CellArea.create("A1", "H30");

        // 3️⃣ Prepare destination workbook
        Workbook destWorkbook = new Workbook();
        Worksheet destWorksheet = destWorkbook.getWorksheets().get(0);

        // 4️⃣ Copy the pivot (Aspose.Cells handles the pivot cache automatically)
        srcWorksheet.copyRange(srcRange, destWorksheet, "A1", new CopyOptions());

        // 5️⃣ Save the result
        destWorkbook.save("YOUR_DIRECTORY/PivotCopied.xlsx");

        System.out.println("Pivot table duplicated successfully.");
    }
}
```

**Ожидаемый результат:** После выполнения в указанной директории появится `PivotCopied.xlsx`. Открыв её в Excel, вы увидите тот же макет сводной таблицы, фильтры и данные, что и в `Source.xlsx`. Все вычисляемые поля и форматирование сохраняются.

## Часто задаваемые вопросы

* **Работает ли это со старыми форматами Excel (.xls)?**  
  Да. Aspose.Cells автоматически определяет формат. Используйте `new Workbook("file.xls")`, и та же логика копирования применима.

* **Что если сводная таблица ссылается на внешние источники данных?**  
  Копия сохраняет оригинальную ссылку на источник данных. Если в целевой среде источник недоступен, сводная таблица покажет ошибки `#REF!`. Чтобы избежать этого, обновите сводную таблицу после копирования или измените её источник через `PivotTable.setDataSource(...)`.

* **Можно ли копировать сводную таблицу в лист с конкретным именем?**  
  Конечно. После создания листа назначения переименуйте его:

  ```java
  destWorksheet.setName("ReportPivot");
  srcWorksheet.copyRange(srcRange, destWorksheet, "A1", new CopyOptions());
  ```

## Заключение

Теперь вы знаете, **как дублировать сводные таблицы** в Java с помощью Aspose.Cells, **как копировать диапазон между книгами** и лучшие практики **загрузки Excel‑книги Java**. Следуя пятишаговому процессу — загрузка, определение, создание назначения, копирование и сохранение — вы сможете автоматизировать генерацию отчётов, архивировать анализы или разбивать сложные книги без потери функциональности сводных таблиц.

Далее изучайте связанные темы, такие как **копирование сводной таблицы в книгу** с несколькими листами, или интегрируйте дублированную сводную таблицу в более крупный конвейер обработки данных, используя Apache POI для сценариев без Aspose. Экспериментируйте с различными настройками `CopyOptions`, чтобы оптимизировать производительность при работе с массивными книгами.

Счастливого кодинга!

## Что следует изучить дальше?

Следующие учебники охватывают тесно связанные темы, расширяющие техники, продемонстрированные в этом руководстве. Каждый ресурс содержит полностью работающие примеры кода с пошаговыми объяснениями, помогающими освоить дополнительные возможности API и исследовать альтернативные подходы в ваших проектах.

- [Как создавать сводные таблицы в Excel с помощью Aspose.Cells for Java: Полное руководство](/cells/english/java/data-analysis/create-pivot-tables-excel-aspose-cells-java/)
- [Как обновлять источник сводной таблицы Excel с помощью Aspose.Cells for Java: Полное руководство](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [Группировка полей сводной таблицы в Excel‑книгах с помощью Aspose.Cells for Java — Полное руководство](/cells/english/java/data-analysis/aspose-cells-java-group-pivot-fields-excel-workbook/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}