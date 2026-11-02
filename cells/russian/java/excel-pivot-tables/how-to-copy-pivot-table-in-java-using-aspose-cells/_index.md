---
category: general
date: 2026-07-06
description: Как скопировать сводную таблицу в Java с помощью Aspose.Cells — пошаговое
  руководство по программному дублированию сводных таблиц Excel.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy pivot
- duplicate excel pivot
language: ru
lastmod: 2026-07-06
og_description: Как скопировать сводную таблицу в Java с помощью Aspose.Cells позволяет
  быстро и надёжно дублировать сводные таблицы Excel.
og_image_alt: Screenshot of Java code copying an Excel pivot table with Aspose.Cells
og_title: Как скопировать сводную таблицу в Java – Полное руководство по Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-07-06'
  description: How to copy pivot table in Java with Aspose.Cells – step‑by‑step guide
    to duplicate Excel pivot tables programmatically.
  headline: How to copy pivot table in Java using Aspose.Cells
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel
- Pivot Table
title: Как скопировать сводную таблицу в Java с помощью Aspose.Cells
url: /ru/java/excel-pivot-tables/how-to-copy-pivot-table-in-java-using-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как скопировать сводную таблицу в Java с помощью Aspose.Cells

Когда‑нибудь задавались вопросом, **как скопировать сводные** таблицы в файле Excel без ручного открытия книги? Вы не одиноки. Во многих конвейерах отчетности вам нужно **дублировать сводные таблицы Excel** «на лету» — возможно, чтобы создать снимок, переместить её на новый лист или создать шаблон для downstream‑пользователей.

В этом руководстве мы пройдем через полностью готовый, исполняемый пример, который именно это демонстрирует. С помощью библиотеки Aspose.Cells for Java мы загрузим книгу, найдем диапазон исходной сводной таблицы, скопируем её в новое место и сохраним результат. Никаких расплывчатых ссылок, только конкретное решение, которое вы можете сразу внедрить в свой проект.

---

## Требования

Прежде чем начать, убедитесь, что у вас есть:

* **Java Development Kit (JDK) 8+** – код компилируется любой современной JDK.
* **Aspose.Cells for Java** версии 25.11 или новее – метод `Range.copy`, поддерживающий сводные таблицы, был добавлен в этом релизе.
* Файл **input.xlsx**, уже содержащий сводную таблицу (можете создать её в Excel для тестов).
* Инструмент сборки по вашему выбору (Maven, Gradle или обычный `javac`). Мы покажем зависимость Maven для быстрого старта.

```xml
<!-- Add this to your pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.12</version> <!-- Use the latest stable -->
</dependency>
```

---

## Шаг 1: Загрузить исходную книгу

Первое, что мы делаем, — открываем файл Excel, в котором находится оригинальная сводная таблица. Aspose.Cells рассматривает книгу как объект в памяти, поэтому вы можете манипулировать ею без запуска Excel.

```java
// Load the workbook from disk
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

> **Почему это важно:** Загрузка книги дает доступ к листам, ячейкам и, что особенно важно, к кэшу сводной таблицы, который её поддерживает. Без этого шага библиотека не имеет чего копировать.

---

## Шаг 2: Получить лист, содержащий сводную таблицу

Если в книге несколько листов, нужно указать правильный. Здесь мы просто берём первый лист, но можно также использовать `get("SheetName")` для поиска по имени.

```java
// Obtain the first worksheet (index 0)
Worksheet worksheet = workbook.getWorksheets().get(0);
```

> **Pro tip:** При работе с большим количеством листов кэшируйте индекс или имя в конфигурационном файле, чтобы избежать «жёсткого» кодирования чисел.

---

## Шаг 3: Определить исходный диапазон, включающий сводную таблицу

Начиная с версии 25.11 Aspose.Cells позволяет рассматривать сводную таблицу как обычный диапазон ячеек. Укажите ячейки верхнего‑левого и нижнего‑правого угла, охватывающие всю сводную таблицу.

```java
// The range A1:D20 covers the whole pivot table in this example
Range sourceRange = worksheet.getCells().createRange("A1:D20");
```

> **Edge case:** Если ваша сводная таблица динамически расширяется (например, позже добавляются строки), рассмотрите использование `worksheet.getPivotTables().get(0).getDataRange()` для программного получения точного диапазона.

---

## Шаг 4: Определить диапазон назначения, куда будет скопирована сводная таблица

Выберите любую пустую ячейку, где вы хотите разместить дубликат. В этом демонстрационном примере мы начинаем с **F1**, оставляя промежуток между оригиналом и копией.

```java
// Destination starts at cell F1 – adjust as needed
Range destinationRange = worksheet.getCells().createRange("F1");
```

> **Почему не новый лист?** Вы также можете создать новый лист (`workbook.getWorksheets().add("Copy")`) и использовать его ячейки в качестве места назначения. Тот же метод `copy` работает между листами.

---

## Шаг 5: Скопировать сводную таблицу в новое место

Теперь происходит магия. Метод `copy` клонирует сводную таблицу, её кэш, форматирование и даже связанные срезы (начиная с последней версии).

```java
// Perform the copy – the pivot is now duplicated at the destination
sourceRange.copy(destinationRange);
```

> **Important:** Операция копирования *глубокая*; она **не** создаёт ссылку обратно на оригинальную сводную таблицу. Вы можете изменять новую таблицу независимо, не влияя на исходную.

---

## Шаг 6: Сохранить книгу с дублированной сводной таблицей

Наконец, запишите изменённую книгу обратно на диск. Можно перезаписать оригинал или создать новый файл; в примере мы выбираем второй вариант, чтобы оставить исходный файл нетронутым.

```java
// Save the workbook – the duplicated pivot lives in output.xlsx
workbook.save("YOUR_DIRECTORY/output.xlsx");
```

Когда вы откроете **output.xlsx** в Excel, вы увидите оригинальную сводную таблицу в столбцах A‑D и идеальную копию, начинающуюся с столбца F. Обе сводные таблицы можно обновлять отдельно.

---

## Полный рабочий пример

Объединив всё вместе, получаем полностью готовый Java‑класс, который можно сразу скомпилировать и запустить:

```java
import com.aspose.cells.*;

public class ExportPivotTableExample {
    public static void main(String[] args) throws Exception {
        // Step 1: Load the source workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // Step 2: Get the worksheet that contains the pivot table
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // Step 3: Define the source range that includes the pivot table (supported from version 25.11)
        // Adjust the range to match your actual pivot dimensions
        Range sourceRange = worksheet.getCells().createRange("A1:D20");

        // Step 4: Define the destination range where the pivot table will be copied
        // Change "F1" to any starting cell you prefer
        Range destinationRange = worksheet.getCells().createRange("F1");

        // Step 5: Copy the pivot table to the new location
        sourceRange.copy(destinationRange);

        // Step 6: Save the workbook with the copied pivot table
        workbook.save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

**Expected result:** Открывая `output.xlsx`, вы видите оригинальную сводную таблицу (A1:D20) и идентичную таблицу, начинающуюся с F1. Обе таблицы сохраняют свои фильтры, стили и вычисляемые поля.

---

## Обработка типовых вариантов

| Ситуация | Что нужно изменить |
|-----------|--------------------|
| **Multiple pivots** on the same sheet | Loop through `worksheet.getPivotTables()` and copy each with its own destination range. |
| **Dynamic data range** | Use `worksheet.getPivotTables().get(0).getDataRange()` to auto‑detect the source area. |
| **Copy to another workbook** | Load a second `Workbook` instance, create a destination worksheet, then call `sourceRange.copy(destWorksheet.getCells().createRange("A1"))`. |
| **Preserve slicers** | As of 25.12, slicers are copied automatically when the range includes them. Verify in Excel after saving. |

---

## Полезные советы и подводные камни

* **Version check:** Метод `copy`, поддерживающий сводные таблицы, был добавлен в **Aspose.Cells 25.11**. Если вы используете более старую версию, получите исключение. Всегда проверяйте версию `aspose-cells` в вашем `pom.xml`.
* **Performance:** Копирование больших сводных таблиц может быть ресурсоёмким. Если нужны только данные, рассмотрите экспорт сводной таблицы в плоскую таблицу вместо клонирования всего объекта.
* **Refresh behavior:** Дублированная сводная таблица сохраняет собственный кэш. При изменении исходных данных вызовите `pivotTable.refresh()` у новой таблицы для пересчёта.
* **Formatting quirks:** Некоторые пользовательские числовые форматы могут не сохраниться при копировании в очень старые версии Excel (<2007). Тестируйте на версии Excel вашей целевой аудитории.

---

## Заключение

Теперь у вас есть полное, сквозное решение, **как скопировать сводные** таблицы с помощью Aspose.Cells for Java, и вы увидели, как **дублировать сводные таблицы Excel** в несколько строк кода. Подход работает как с одной, так и с несколькими сводными таблицами, между листами и даже между книгами.

Следующие шаги могут включать:

* Автоматизацию копирования для каждой сводной таблицы в пакетной задаче.
* Добавление кода для переименования дублированной таблицы (например, `pivotTable.setName("Copy_of_Sales")`).
* Интеграцию процедуры в более крупный сервис отчётности, генерирующий PDF или CSV‑экспорты.

Попробуйте, подкорректируйте диапазоны под свои реальные данные, и позвольте библиотеке выполнить тяжёлую работу. Happy coding!

## Что изучать дальше?

Следующие руководства охватывают тесно связанные темы, расширяющие техники, продемонстрированные в этом руководстве. Каждый ресурс включает полностью рабочие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы в собственных проектах.

- [How to Create Pivot Tables in Excel Using Aspose.Cells for Java&#58; A Comprehensive Guide](/cells/english/java/data-analysis/create-pivot-tables-excel-aspose-cells-java/)
- [Excel Pivot Table Manipulation with Aspose.Cells Java&#58; A Comprehensive Guide](/cells/english/java/data-analysis/excel-pivot-table-manipulation-aspose-cells-java/)
- [How to Update Excel Pivot Table Source with Aspose.Cells for Java&#58; A Comprehensive Guide](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}