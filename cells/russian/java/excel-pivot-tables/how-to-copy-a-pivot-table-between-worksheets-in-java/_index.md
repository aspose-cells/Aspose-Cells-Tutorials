---
category: general
date: 2026-10-16
description: Как скопировать сводную таблицу в Java с помощью Aspose.Cells — узнайте,
  как эффективно копировать диапазон на другой лист и между листами.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy pivot table
- copy range to another sheet
- copy range between worksheets
language: ru
lastmod: 2026-10-16
og_description: Как скопировать сводную таблицу в Java с помощью Aspose.Cells. Этот
  учебник покажет, как скопировать диапазон на другой лист и как скопировать диапазон
  между листами с полным кодом.
og_image_alt: Diagram illustrating how to copy pivot table from one worksheet to another
  in Java
og_title: Как скопировать сводную таблицу между листами в Java – пошаговое руководство
schemas:
- author: Aspose
  dateModified: '2026-10-16'
  description: How to copy pivot table in Java with Aspose.Cells – learn to copy range
    to another sheet and copy range between worksheets efficiently.
  headline: How to copy a pivot table between worksheets in Java
  type: TechArticle
- description: How to copy pivot table in Java with Aspose.Cells – learn to copy range
    to another sheet and copy range between worksheets efficiently.
  name: How to copy a pivot table between worksheets in Java
  steps:
  - name: Load the workbook
    text: '```java import com.aspose.cells.*;'
  - name: Locate the source range that contains the pivot table
    text: '```java // The first worksheet (index 0) holds the pivot table. Worksheet
      sourceSheet = workbook.getWorksheets().get(0);'
  - name: Define the destination range on another sheet
    text: '```java // The second worksheet (index 1) will receive the copied pivot
      table. Worksheet destSheet = workbook.getWorksheets().get(1);'
  - name: Copy the source range while preserving the pivot table
    text: '```java // Configure copy options to keep all formatting, formulas, and
      pivot data. CopyOptions copyOptions = new CopyOptions(); copyOptions.setPasteType(PasteType.PASTE_ALL);
      // copies everything copyOptions.setSkipEmptyRows(false); copyOptions.setSkipEmptyColumns(false);'
  - name: Save the workbook and verify the result
    text: '```java // Save the modified workbook to a new file. workbook.save("output.xlsx");
      System.out.println("Pivot table copied successfully."); } } ```'
  type: HowTo
tags:
- Aspose.Cells
- Java
- PivotTable
- Excel automation
title: Как скопировать сводную таблицу между листами в Java
url: /ru/java/excel-pivot-tables/how-to-copy-a-pivot-table-between-worksheets-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как скопировать сводную таблицу между листами в Java

Если вам нужно **скопировать сводную таблицу** с одного листа на другой в той же книге, это руководство предоставляет полное, готовое к запуску решение. Вы увидите, как скопировать исходный диапазон, содержащий сводную таблицу, сохранить её функциональность и проверить результат — всё с помощью Aspose.Cells for Java.

Копирование сводной таблицы — распространённая задача при программной генерации отчетов, и правильное выполнение предотвращает потерю кэша сводной таблицы или поломку формул. К концу этого руководства вы сможете **скопировать диапазон на другой лист** и **скопировать диапазон между листами** без каких-либо ручных действий.

## Что вы узнаете

* Загрузить существующий файл Excel со сводной таблицей.
* Определить исходный диапазон, содержащий сводную таблицу.
* Определить диапазон назначения на другом листе.
* Использовать `CopyOptions`, чтобы сохранить сводную таблицу неизменной.
* Проверить, что скопированная сводная таблица работает как ожидается.

**Требования**

* Java 17 или новее.
* Aspose.Cells for Java (версия 23.12 или новее).  
* Файл Excel (`input.xlsx`), содержащий сводную таблицу на первом листе.

---

## Как скопировать сводную таблицу с помощью Aspose.Cells

Суть операции состоит из четырёх шагов: загрузить книгу, найти исходный диапазон, задать диапазон назначения и выполнить копирование. Ниже каждый шаг подробно объяснён.

### Шаг 1: Загрузка книги

```java
import com.aspose.cells.*;

public class CopyPivotTableExample {
    public static void main(String[] args) throws Exception {
        // Load the workbook that contains the original pivot table
        Workbook workbook = new Workbook("input.xlsx");
```

*Зачем этот шаг?*  
Загрузка книги помещает весь файл в память, предоставляя доступ к листам, ячейкам и кэшу сводных таблиц. Aspose.Cells автоматически читает формат файла, поэтому вам не нужно беспокоиться о различиях между `.xls` и `.xlsx`.

### Шаг 2: Поиск исходного диапазона, содержащего сводную таблицу

```java
        // The first worksheet (index 0) holds the pivot table.
        Worksheet sourceSheet = workbook.getWorksheets().get(0);

        // Define the exact area that includes the pivot table.
        // Adjust the address if your pivot table spans a different range.
        Range sourceRange = sourceSheet.getCells().createRange("A1:G20");
```

*Зачем этот шаг?*  
Сводная таблица хранится в блоке ячеек, который также ссылается на скрытый кэш. Выбирая точный диапазон (`A1:G20` в этом примере), вы гарантируете, что кэш останется связанным при копировании диапазона.

### Шаг 3: Определение диапазона назначения на другом листе

```java
        // The second worksheet (index 1) will receive the copied pivot table.
        Worksheet destSheet = workbook.getWorksheets().get(1);

        // Destination starts at cell A1 of the second sheet.
        Range destRange = destSheet.getCells().createRange("A1");
```

*Зачем этот шаг?*  
Выбор назначения на другом листе позволяет вам **скопировать диапазон на другой лист**. Ячейка в левом верхнем углу (`A1`) является обычной точкой начала, но вы можете разместить её где угодно, изменив адрес.

### Шаг 4: Копирование исходного диапазона с сохранением сводной таблицы

```java
        // Configure copy options to keep all formatting, formulas, and pivot data.
        CopyOptions copyOptions = new CopyOptions();
        copyOptions.setPasteType(PasteType.PASTE_ALL); // copies everything
        copyOptions.setSkipEmptyRows(false);
        copyOptions.setSkipEmptyColumns(false);

        // Perform the copy operation.
        sourceRange.copy(destRange, copyOptions);
```

*Зачем этот шаг?*  
`CopyOptions` управляет тем, что будет перенесено. Использование `PasteType.PASTE_ALL` гарантирует, что сводная таблица, её форматирование и базовые формулы будут дублированы. Без этих параметров могут быть скопированы только сырые значения, что нарушит работу сводной таблицы.

### Шаг 5: Сохранение книги и проверка результата

```java
        // Save the modified workbook to a new file.
        workbook.save("output.xlsx");
        System.out.println("Pivot table copied successfully.");
    }
}
```

Откройте `output.xlsx` в Excel и убедитесь, что:

* На втором листе находится полностью функциональная сводная таблица, идентичная оригиналу.
* Обновление сводной таблицы (Refresh) изменяет данные, подтверждая, что кэш сохранён.

---

## Копирование диапазона на другой лист с помощью Java

Если ваша цель — просто **скопировать диапазон на другой лист** без сводной таблицы, тот же код работает с обычным диапазоном ячеек. Единственное изменение — адрес источника. Конфигурация `CopyOptions` остаётся той же, обеспечивая сохранение формул и форматирования.

```java
// Example: copy a plain data table from Sheet1!B2:D10 to Sheet3!A1
Range plainSource = workbook.getWorksheets().get(0)
                            .getCells().createRange("B2:D10");
Range plainDest = workbook.getWorksheets().get(2)
                          .getCells().createRange("A1");
plainSource.copy(plainDest, copyOptions);
```

Этот фрагмент демонстрирует гибкость API как для сценариев со сводными, так и без них.

---

## Копирование диапазона между листами без потери формул

При **копировании диапазона между листами** формулы, ссылающиеся на другие листы, могут стать некорректными, если изменятся относительные ссылки. Чтобы этого избежать:

1. Используйте `CopyOptions.setPasteType(PasteType.PASTE_FORMULAS)`, если нужны только формулы.
2. Оставьте лист назначения в той же книге, чтобы внутренние ссылки оставались действительными.
3. После копирования вызовите `workbook.calculateFormula();`, чтобы принудительно выполнить перерасчёт.

```java
copyOptions.setPasteType(PasteType.PASTE_FORMULAS);
sourceRange.copy(destRange, copyOptions);
workbook.calculateFormula();
```

Эти дополнительные шаги гарантируют, что скопированный диапазон будет вести себя точно так же, как оригинал, даже если он охватывает несколько листов.

---

## Профессиональные советы и распространённые подводные камни

| Situation | Tip |
|-----------|-----|
| **Pivot cache not updating** | После копирования вызовите `destSheet.getPivotTables().get(0).refresh();`, чтобы обновить кэш. |
| **Copying to a different workbook** | Используйте `Workbook destWorkbook = new Workbook();` и затем `sourceRange.copy(destWorkbook.getWorksheets().get(0).getCells().createRange("A1"), copyOptions);`. Не забудьте при необходимости отдельно скопировать кэш сводной таблицы. |
| **Large pivot tables** | Увеличьте размер кучи Java (`-Xmx2g`), чтобы избежать `OutOfMemoryError` во время копирования. |
| **Preserving styles** | Установите `copyOptions.setPasteType(PasteType.PASTE_ALL)`; иначе будут скопированы только значения. |

---

## Ожидаемый результат

Запуск полной программы создаёт `output.xlsx`. При открытии в Excel:

* **Sheet2!A1:G20** отображает ту же сводную таблицу, что и **Sheet1!A1:G20**.
* Список полей сводной таблицы, метки строк/столбцов и значения данных совпадают с источником.
* Обновление сводной таблицы изменяет числа, подтверждая, что кэш работает.

Консоль выведет:

```
Pivot table copied successfully.
```

---

## Заключение

В этом руководстве вы узнали, как **скопировать сводную таблицу** с одного листа на другой с помощью Aspose.Cells for Java. Загрузив книгу, выбрав правильный исходный диапазон, задав назначение и настроив `CopyOptions`, вы можете надёжно **скопировать диапазон на другой лист** и **скопировать диапазон между листами**, сохраняя всю функциональность сводной таблицы.

Далее вы можете изучить:

* Экспорт скопированной сводной таблицы в PDF или HTML.
* Автоматизацию обновления сводных таблиц в нескольких книгах.
* Использование `CopyOptions` для копирования только определённых элементов (например, значений, форматов).

Не стесняйтесь экспериментировать с различными адресами диапазонов, структурами книг или даже копированием между книгами. Приятного кодинга!

## Что вам стоит изучить дальше?

Следующие руководства охватывают тесно связанные темы, опирающиеся на техники, продемонстрированные в этом руководстве. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы к реализации в ваших проектах.

- [Как скопировать диапазон в Java – копировать сводную таблицу с Aspose.Cells](/cells/english/java/excel-pivot-tables/how-to-copy-range-in-java-copy-pivot-table-with-aspose-cells/)
- [Как скопировать сводную таблицу в Java – полное руководство по Aspose.Cells](/cells/english/java/excel-pivot-tables/how-to-copy-pivot-table-in-java-complete-aspose-cells-guide/)
- [Копирование сводной таблицы Excel – пошаговое руководство с использованием Java](/cells/english/java/excel-pivot-tables/copy-pivot-table-excel-step-by-step-guide-using-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}