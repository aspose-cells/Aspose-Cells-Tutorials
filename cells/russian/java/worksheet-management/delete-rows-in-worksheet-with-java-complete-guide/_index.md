---
category: general
date: 2026-06-18
description: Удаление строк в листе с помощью Aspose.Cells для Java. Узнайте, как
  безопасно удалить строку заголовка таблицы и строки из таблицы Excel.
draft: false
keywords:
- delete rows in worksheet
- remove table header row
- remove rows from excel table
language: ru
og_description: Удалить строки в листе с помощью Aspose.Cells для Java. Это руководство
  показывает, как удалить строку заголовка таблицы и эффективно удалять строки из
  таблицы Excel.
og_title: Удаление строк в листе с помощью Java — пошагово
schemas:
- author: Aspose
  dateModified: '2026-06-18'
  description: Delete rows in worksheet using Aspose.Cells for Java. Learn how to
    remove table header row and delete rows from Excel table safely.
  headline: Delete rows in worksheet with Java – Complete Guide
  type: TechArticle
- description: Delete rows in worksheet using Aspose.Cells for Java. Learn how to
    remove table header row and delete rows from Excel table safely.
  name: Delete rows in worksheet with Java – Complete Guide
  steps:
  - name: '`table.unlist()` strips the table metadata, turning the block into ordinary
      cells.'
    text: '`table.unlist()` strips the table metadata, turning the block into ordinary
      cells.'
  - name: With the header now a regular row, `deleteRows(0, …)` works without complaints.
    text: With the header now a regular row, `deleteRows(0, …)` works without complaints.
  - name: If you still need a table after the cleanup, you can recreate it using `ws.getTables().add(...)`.
    text: If you still need a table after the cleanup, you can recreate it using `ws.getTables().add(...)`.
  - name: Loads a workbook.
    text: Loads a workbook.
  - name: Checks if the first table exists.
    text: Checks if the first table exists.
  - name: Deletes **all** rows *including* the header safely.
    text: Deletes **all** rows *including* the header safely.
  - name: Re‑creates the table from the remaining rows (if any).
    text: Re‑creates the table from the remaining rows (if any).
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel
- Worksheet
title: Удаление строк в листе Excel с помощью Java – Полное руководство
url: /ru/java/worksheet-management/delete-rows-in-worksheet-with-java-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Удаление строк в листе – Полный Java‑урок

Когда‑нибудь вам нужно было **delete rows in worksheet**, но вы столкнулись с проблемой, потому что заголовок таблицы отказывается двигаться? Вы не одиноки. Во многих сценариях автоматизации Excel первая строка принадлежит структурированной таблице, и наивный вызов `deleteRows` бросает исключение или просто оставляет заголовок нетронутым.  

В этом руководстве мы подробно покажем, как *remove table header row* и *remove rows from Excel table* без повреждения листа. К концу вы получите чистый, исполняемый фрагмент кода, работающий с последней версией Aspose.Cells for Java (v23.10 на момент написания).  

Мы рассмотрим предварительные требования, три практических подхода и несколько советов, которые стоит сохранить в закладки. Без лишних слов — именно тот ответ, который вы ожидали бы от опытного разработчика за чашкой кофе.

## Предварительные требования

Перед тем как начать, убедитесь, что у вас есть:

- Java 17 или новее (код компилируется и со старыми версиями, но рекомендуется 17).
- Aspose.Cells for Java 23.10 или новее, добавленный в ваш `pom.xml` Maven:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.10</version>
</dependency>
```

- Пример файла Excel (`Sample.xlsx`), содержащий таблицу на первом листе. Заголовок таблицы находится в строке 0 (строка Excel 1).

Это всё. Готовы? Поехали.

## Delete rows in worksheet – почему важна строка заголовка

Когда вы вызываете:

```java
ws.getCells().deleteRows(0, 2, true);
```

Aspose.Cells отказывается удалять строку 0, потому что она является частью **table**. API защищает целостность таблицы; удаление заголовка сделало бы строки данных «сиротами». Вы увидите исключение вроде *“The specified row belongs to a table and cannot be deleted.”*  

Понимание этого ограничения — первый шаг к успешному решению.

## Подход 1 – Удаление строк **ниже** заголовка (самый распространённый)

Если вам просто нужно очистить данные, сохранив структуру таблицы, начинайте удалять со строки **после** заголовка.

```java
import com.aspose.cells.*;

public class DeleteRowsBelowHeader {
    public static void main(String[] args) throws Exception {
        // Load workbook
        Workbook wb = new Workbook("Sample.xlsx");
        Worksheet ws = wb.getWorksheets().get(0);

        // Determine how many data rows the table currently has
        Table table = ws.getTables().get(0);
        int dataRowCount = table.getDataRange().getRowCount();

        // Delete all data rows (keep header)
        // startRow = 1 because row index 0 is the header
        ws.getCells().deleteRows(1, dataRowCount, true);

        // Save the result
        wb.save("Result_DeleteRowsBelowHeader.xlsx");
    }
}
```

**Почему это работает:** `deleteRows` получает начальный индекс 1, поэтому заголовок остаётся нетронутым. Флаг `true` сдвигает оставшиеся строки вверх, сохраняя любые формулы, которые на них ссылаются. После выполнения кода вы увидите чистую таблицу, в которой осталась только строка заголовка.

### Быстрый совет

Если нужно удалить *конкретный* диапазон строк (например, строки 5‑10), просто скорректируйте начальный индекс и количество. Таблица автоматически изменит размер, чтобы соответствовать новому диапазону данных.

## Подход 2 – Преобразовать таблицу в обычный диапазон, затем удалить

Иногда действительно необходимо **remove table header row** и работать с данными как с обычным диапазоном. Трюк в том, чтобы сначала *unlist* таблицу.

```java
import com.aspose.cells.*;

public class RemoveHeaderAndDeleteRows {
    public static void main(String[] args) throws Exception {
        Workbook wb = new Workbook("Sample.xlsx");
        Worksheet ws = wb.getWorksheets().get(0);
        Table table = ws.getTables().get(0);

        // 1️⃣ Unlist the table – it becomes a normal range
        table.unlist();

        // 2️⃣ Now you can delete the header row (row 0) and any other rows
        // Delete header + first two data rows (total 3 rows)
        ws.getCells().deleteRows(0, 3, true);

        // 3️⃣ (Optional) Re‑create a table from the remaining data
        // Assuming you still have data starting at row 0
        int firstDataRow = 0;
        int lastDataRow = ws.getCells().getMaxDataRow();
        int firstCol = ws.getCells().getMaxDataColumn();
        int lastCol = ws.getCells().getMaxDataColumn();

        String range = new CellArea(firstDataRow, 0, lastDataRow, firstCol).format();
        ws.getTables().add(range, true);
        ws.getTables().get(0).setName("NewTable");

        wb.save("Result_RemoveHeaderAndDeleteRows.xlsx");
    }
}
```

**Explanation:**  

1. `table.unlist()` удаляет метаданные таблицы, превращая блок в обычные ячейки.  
2. Теперь, когда заголовок стал обычной строкой, `deleteRows(0, …)` работает без возражений.  
3. Если после очистки вам всё ещё нужна таблица, её можно создать заново с помощью `ws.getTables().add(...)`.

Этот подход удобен, когда сам заголовок неверен или когда нужно полностью заменить определение таблицы.

## Подход 3 – Использовать Table API для удаления конкретных строк

Aspose.Cells также предоставляет **table‑level** метод для удаления строк, который автоматически учитывает защиту заголовка.

```java
import com.aspose.cells.*;

public class DeleteRowsViaTableAPI {
    public static void main(String[] args) throws Exception {
        Workbook wb = new Workbook("Sample.xlsx");
        Worksheet ws = wb.getWorksheets().get(0);
        Table table = ws.getTables().get(0);

        // Delete the first two data rows (index 0 = first data row, not the header)
        // The Table API counts only data rows, so we don't touch the header.
        table.deleteRows(0, 2);

        wb.save("Result_DeleteRowsViaTableAPI.xlsx");
    }
}
```

**Why you might pick this:** Это самый *semantic* способ — вы говорите таблице «удали мои строки данных». API автоматически обновляет диапазон таблицы, и вам не придётся возиться с сырыми индексами строк.

## Пограничные случаи и распространённые подводные камни

| Ситуация | На что обратить внимание | Рекомендуемое решение |
|-----------|--------------------------|-----------------------|
| **Multiple tables on the same sheet** | `ws.getTables().get(0)` may target the wrong table. | Use `ws.getTables().stream().filter(t -> t.getName().equals("MyTable")).findFirst().orElse(null)` |
| **Merged cells in the header** | Deleting rows can split merged areas, causing layout glitches. | Unmerge before deletion: `ws.getCells().get("A1").getMergedRange().unmerge();` |
| **Formulas referencing the header** | Removing the header breaks external references. | Update formulas after deletion or keep a placeholder row. |
| **Large worksheets (>10 000 rows)** | `deleteRows` may be slower due to internal shifting. | Use `ws.getCells().clearRows(start, count)` if you don’t need to shift. |

## Полный рабочий пример – объединяем лучшее из всех подходов

Ниже приведена автономная программа, которая:

1. Загружает рабочую книгу.
2. Проверяет, существует ли первая таблица.
3. Безопасно удаляет **all** строки *including* заголовок.
4. Воссоздаёт таблицу из оставшихся строк (если они есть).

```java
import com.aspose.cells.*;

public class DeleteRowsInWorksheetFullDemo {
    public static void main(String[] args) throws Exception {
        // ① Load the workbook
        Workbook wb = new Workbook("Sample.xlsx");
        Worksheet ws = wb.getWorksheets().get(0);

        // ② Guard: make sure a table is present
        if (ws.getTables().getCount() == 0) {
            System.out.println("No tables found – nothing to delete.");
            return;
        }

        // ③ Grab the first table (adjust if you have a named table)
        Table table = ws.getTables().get(0);

        // ④ Unlist so we can delete the header row
        table.unlist();

        // ⑤ Determine total rows to delete (header + data)
        int totalRows = table.getRange().getRowCount(); // includes header
        ws.getCells().deleteRows(0, totalRows, true);

        // ⑥ If there are still rows left, rebuild the table
        int maxRow = ws.getCells().getMaxDataRow();
        int maxCol = ws.getCells().getMaxDataColumn();

        if (maxRow >= 0) { // there is at least one row left
            String newRange = new CellArea(0, 0, maxRow, maxCol).format();
            Table newTable = ws.getTables().add(newRange, true);
            newTable.setName("RebuiltTable");
        }

        // ⑦ Save the result
        wb.save("Result_DeleteRowsInWorksheetFullDemo.xlsx");
        System.out.println("Rows deleted and table rebuilt successfully.");
    }
}
```

**Expected output:** После выполнения вы найдете `Result_DeleteRowsInWorksheetFullDemo.xlsx` с удалённой исходной таблицей и — если какие‑то данные выжили — новой таблицей под названием `RebuiltTable`. Консоль выведет краткое сообщение об успехе.

## Визуальное резюме

![Лист Excel до и после удаления строк](https://example.com/images/delete-rows-workbook.png "До и после удаления строк в листе")

*Alt text:* “До и после удаления строк в листе – заголовок удалён, строки данных очищены.”

## Заключение

Мы рассмотрели три надёжных способа **delete rows in worksheet**, учитывающих сложный сценарий *remove table header row* и безопасно **remove rows from Excel table**. Независимо от того, предпочитаете ли вы прямые операции с ячейками, Table API или полный цикл unlist‑relist, приведённые выше фрагменты кода готовы к использованию в вашем проекте.  

Следующий шаг? Попробуйте комбинировать эти техники с условной логикой — удалять строки только тогда, когда определённый столбец содержит «Inactive», или пакетно обрабатывать несколько…

## Что изучать дальше?

Следующие руководства охватывают близко связанные темы, расширяющие техники, продемонстрированные в этом руководстве. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы в собственных проектах.

- [Эффективное управление строками в Excel с помощью Aspose.Cells for Java: вставка и удаление строк](/cells/english/java/worksheet-management/aspose-cells-java-row-operations-excel/)
- [Как удалить пустые строки из файлов Excel с помощью Aspose.Cells for Java](/cells/english/java/data-manipulation/delete-blank-rows-aspose-cells-java/)
- [Как удалить строки в Excel с помощью Aspose.Cells for Java | Руководство и учебник](/cells/english/java/worksheet-management/delete-row-excel-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}