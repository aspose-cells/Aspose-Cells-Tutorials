---
category: general
date: 2026-09-21
description: Узнайте, как копировать диапазон в Java, сохраняя сводную таблицу. Это
  пошаговое руководство покажет, как безопасно экспортировать сводную таблицу.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy range
- copy pivot table
- preserve pivot table
- export pivot table
- how to preserve pivot
language: ru
lastmod: 2026-09-21
og_description: Как скопировать диапазон в Java, сохранив сводную таблицу. Следуйте
  этому полному руководству, чтобы безопасно экспортировать сводные таблицы.
og_image_alt: Screenshot of Java code copying a range and preserving a pivot table
og_title: Как скопировать диапазон и сохранить сводную таблицу в Java
schemas:
- author: Aspose
  dateModified: '2026-09-21'
  description: Learn how to copy range in Java while preserving the pivot table. This
    step‑by‑step guide shows you how to export a pivot table safely.
  headline: How to copy range and preserve a pivot table in Java
  type: TechArticle
- description: Learn how to copy range in Java while preserving the pivot table. This
    step‑by‑step guide shows you how to export a pivot table safely.
  name: How to copy range and preserve a pivot table in Java
  steps:
  - name: Load the source workbook
    text: '```java // Load the source workbook that contains the pivot table Workbook
      srcWb = new Workbook("YOUR_DIRECTORY/Source.xlsx"); Worksheet srcWs = srcWb.getWorksheets().get(0);
      ```'
  - name: Define the range that covers the pivot table
    text: '```java // Define the range covering the pivot table (including its data
      source) Range srcRange = srcWs.getCells().createRange("A1:G20"); ```'
  - name: Create an empty destination workbook
    text: '```java // Create a new, empty destination workbook Workbook destWb = new
      Workbook(); Worksheet destWs = destWb.getWorksheets().get(0); ```'
  - name: Copy the range – the pivot table is preserved
    text: '```java // Copy the defined range to the destination sheet – the pivot
      table is preserved destWs.getCells().copyRange(srcRange, new CellArea("A1",
      "G20")); ```'
  - name: Save the destination workbook
    text: '```java // Save the destination workbook with the copied pivot table destWb.save("YOUR_DIRECTORY/DestWithPivot.xlsx");
      ```'
  - name: Copy pivot table across different workbook versions
    text: Aspose.Cells supports older `.xls` files as well as the newer `.xlsx` format.
      The same code works regardless of the file extension, making it a universal
      solution for **how to preserve pivot** across versions.
  - name: Preserving pivot table when using a filtered source
    text: 'If the source pivot is filtered, the filter state is also copied. Should
      you need to reset filters in the destination, call `PivotTable.refreshData()`
      after copying:'
  - name: Export pivot table as a static snapshot
    text: Sometimes you may want a static copy (values only) rather than a live pivot.
      Replace `copyRange` with `copyRange` followed by `pt.setEnableRefresh(false)`
      to disable further calculations.
  - name: Handling large workbooks
    text: For workbooks with many worksheets, limit the copy operation to the specific
      sheet to reduce memory usage. Use `Workbook.getSettings().setMemorySetting(MemorySetting.MEMORY_PREFERENCE)`
      to fine‑tune performance.
  type: HowTo
tags:
- Java
- Aspose.Cells
- pivot table
- Excel automation
- range copy
title: Как скопировать диапазон и сохранить сводную таблицу в Java
url: /ru/java/excel-pivot-tables/how-to-copy-range-and-preserve-a-pivot-table-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как скопировать диапазон и сохранить сводную таблицу в Java

Если вам нужно **how to copy range**, содержащий сводную таблицу, это руководство покажет надежный способ сохранить сводную таблицу в целостности. Многие разработчики сталкиваются с потерей сводной таблицы при экспорте данных, но предложенный подход позволяет **copy pivot table** данные без нарушения их функциональности. К концу этого руководства вы сможете **preserve pivot table** структуру, **export pivot table** файлы и понять **how to preserve pivot** в различных сценариях.

В примере используется Aspose.Cells for Java, популярная библиотека для автоматизации Excel. Дополнительные инструменты не требуются, достаточно стандартной среды разработки Java.

## Требования

* Java 17 (или новее), установленный.
* Maven или Gradle для управления зависимостями.
* Aspose.Cells for Java (версия 23.9 или новее). Добавьте следующую зависимость Maven:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.9</version>
    <classifier>jdk17</classifier>
</dependency>
```

* Исходная рабочая книга (`Source.xlsx`), содержащая сводную таблицу, которую вы хотите скопировать.

## Как скопировать диапазон и сохранить сводную таблицу неизменной

Основная идея состоит в копировании **range**, охватывающего всю сводную таблицу, включая её источник данных, с помощью `copyRange`. Этот метод копирует как исходные данные, так и определение сводной таблицы, гарантируя, что целевая рабочая книга получит полностью функционирующую сводную таблицу.

### Шаг 1: Загрузить исходную рабочую книгу

```java
// Load the source workbook that contains the pivot table
Workbook srcWb = new Workbook("YOUR_DIRECTORY/Source.xlsx");
Worksheet srcWs = srcWb.getWorksheets().get(0);
```

*Почему этот шаг?*  
Загрузка рабочей книги дает доступ к листу, содержащему сводную таблицу. Класс `Workbook` представляет весь файл Excel, а `Worksheet` предоставляет операции на уровне ячеек.

### Шаг 2: Определить диапазон, охватывающий сводную таблицу

```java
// Define the range covering the pivot table (including its data source)
Range srcRange = srcWs.getCells().createRange("A1:G20");
```

*Почему этот шаг?*  
Сводная таблица не является одной ячейкой; она охватывает блок, включающий заголовки, строки данных и кэш сводной таблицы. Указав диапазон, полностью содержащий сводную таблицу, вы гарантируете, что `copyRange` также скопирует базовый кэш, что необходимо для поведения **preserve pivot table**.

### Шаг 3: Создать пустую целевую рабочую книгу

```java
// Create a new, empty destination workbook
Workbook destWb = new Workbook();
Worksheet destWs = destWb.getWorksheets().get(0);
```

*Почему этот шаг?*  
Начало с чистой рабочей книги предотвращает случайные конфликты с существующими листами или именованными диапазонами. Целевая рабочая книга получит скопированный диапазон, эффективно содержащий **export pivot table**.

### Шаг 4: Скопировать диапазон — сводная таблица сохраняется

```java
// Copy the defined range to the destination sheet – the pivot table is preserved
destWs.getCells().copyRange(srcRange, new CellArea("A1", "G20"));
```

*Почему этот шаг?*  
`copyRange` выполняет глубокое копирование: значения ячеек, форматирование и метаданные сводной таблицы передаются. Это критическая операция, позволяющая **copy pivot table** без потери её функциональности. Объект `CellArea` определяет, куда диапазон будет помещён на листе назначения.

### Шаг 5: Сохранить целевую рабочую книгу

```java
// Save the destination workbook with the copied pivot table
destWb.save("YOUR_DIRECTORY/DestWithPivot.xlsx");
```

*Почему этот шаг?*  
Сохранение завершает процесс **export pivot table**. Полученный файл (`DestWithPivot.xlsx`) содержит полностью рабочую сводную таблицу, которую можно открыть в Excel, Google Sheets или любом другом просмотрщике таблиц.

## Проверка сохранения сводной таблицы

Откройте `DestWithPivot.xlsx` в Excel и проверьте следующее:

1. Сводная таблица отображается в том же месте (A1:G20), что и в исходном файле.
2. Обновление сводной таблицы корректно обновляет данные, подтверждая, что кэш был скопирован.
3. Все форматирование (ширина столбцов, числовые форматы) соответствует оригиналу.

Если любой из этих пунктов не выполнен, проверьте, что исходный диапазон полностью охватывает сводную таблицу и её источник данных. Частая ошибка — выбрать диапазон, не включающий кэш данных, что приводит к неработающей сводной таблице.

## Дополнительные соображения

### Копирование сводной таблицы между разными версиями рабочих книг

Aspose.Cells поддерживает как старые файлы `.xls`, так и новый формат `.xlsx`. Один и тот же код работает независимо от расширения файла, что делает его универсальным решением для **how to preserve pivot** между версиями.

### Сохранение сводной таблицы при использовании отфильтрованного источника

Если исходная сводная таблица отфильтрована, состояние фильтра также копируется. Если необходимо сбросить фильтры в целевом файле, вызовите `PivotTable.refreshData()` после копирования:

```java
PivotTable pt = destWs.getPivotTables().get(0);
pt.refreshData();   // Clears filters but keeps the pivot definition
```

### Экспорт сводной таблицы как статического снимка

Иногда может потребоваться статическая копия (только значения) вместо живой сводной таблицы. Замените `copyRange` на `copyRange`, а затем вызовите `pt.setEnableRefresh(false)`, чтобы отключить дальнейшие вычисления.

```java
destWs.getCells().copyRange(srcRange, new CellArea("A1", "G20"));
PivotTable pt = destWs.getPivotTables().get(0);
pt.setEnableRefresh(false); // Makes the pivot static
```

### Обработка больших рабочих книг

Для книг с множеством листов ограничьте операцию копирования конкретным листом, чтобы снизить использование памяти. Используйте `Workbook.getSettings().setMemorySetting(MemorySetting.MEMORY_PREFERENCE)` для тонкой настройки производительности.

## Полный исполняемый пример

Ниже представлен полный пример программы, который вы можете скопировать, вставить и запустить. Скорректируйте пути к файлам под вашу среду.

```java
import com.aspose.cells.*;

public class CopyPivotRange {
    public static void main(String[] args) throws Exception {
        // Step 1: Load the source workbook that contains the pivot table
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/Source.xlsx");
        Worksheet srcWs = srcWb.getWorksheets().get(0);

        // Step 2: Define the range covering the pivot table (including its data source)
        // Adjust the range as needed to fully contain your pivot
        Range srcRange = srcWs.getCells().createRange("A1:G20");

        // Step 3: Create a new, empty destination workbook
        Workbook destWb = new Workbook();
        Worksheet destWs = destWb.getWorksheets().get(0);

        // Step 4: Copy the defined range – the pivot table is preserved
        destWs.getCells().copyRange(srcRange, new CellArea("A1", "G20"));

        // Optional: If you need a static snapshot, disable refresh
        // PivotTable pt = destWs.getPivotTables().get(0);
        // pt.setEnableRefresh(false);

        // Step 5: Save the destination workbook with the copied pivot table
        destWb.save("YOUR_DIRECTORY/DestWithPivot.xlsx");

        System.out.println("Pivot table copied successfully. File saved as DestWithPivot.xlsx");
    }
}
```

**Ожидаемый вывод**

```
Pivot table copied successfully. File saved as DestWithPivot.xlsx
```

Когда вы откроете `DestWithPivot.xlsx`, вы должны увидеть оригинальную сводную таблицу полностью функциональной, подтверждая, что вы успешно **how to copy range** при **preserve pivot table**.

## Распространённые подводные камни и профессиональные советы

| Проблема | Почему это происходит | Решение |
|----------|-----------------------|---------|
| Сводная таблица отображается, но показывает ошибки `#REF!` | Скопированный диапазон не включал скрытый лист кэша | Расширьте исходный диапазон, чтобы включить весь кэш (обычно строки под сводной таблицей) |
| Целевая рабочая книга больше, чем ожидалось | `copyRange` также копирует форматирование | Используйте `CopyOptions`, чтобы исключить форматирование, если размер имеет значение |
| Обновление не удалось с ошибкой «Data source not found» | Исходная рабочая книга использовала внешние соединения данных | Воссоздайте соединение в целевой книге или сначала скопируйте лист с источником данных |

**Pro tip:** Всегда выполняйте быструю проверку `destWs.getPivotTables().size()` после копирования. Если количество равно нулю, диапазон не включал определение сводной таблицы, и его нужно расширить.

## Заключение

В этом руководстве мы продемонстрировали **how to copy range**, содержащий сводную таблицу, и гарантировали, что поведение **preserve pivot table** остаётся неизменным. Загрузив исходную рабочую книгу, определив всесторонний диапазон, используя `copyRange` и сохранив целевой файл, вы можете надёжно **export pivot table** данные и ответить на вопрос **how to preserve pivot** в проектах Java.

Следующие шаги, которые вы можете изучить, включают:

* Автоматизацию копирования для нескольких листов (используйте вторичное ключевое слово **copy pivot table** в цикле).
* Преобразование экспортированной рабочей книги в CSV, сохраняя исходные данные (по‑прежнему логика **preserve pivot table** для источника).

## Что изучать дальше?

Следующие руководства охватывают близко связанные темы, которые развивают техники, продемонстрированные в этом руководстве. Каждый ресурс включает полные рабочие примеры кода с пошаговыми объяснениями, помогающими вам освоить дополнительные возможности API и исследовать альтернативные подходы к реализации в собственных проектах.

- [Copy Pivot Table in Java – Preserve It, Export to PPTX](/cells/english/java/excel-pivot-tables/copy-pivot-table-in-java-preserve-it-export-to-pptx/)
- [How to Update Excel Pivot Table Source with Aspose.Cells for Java: A Comprehensive Guide](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [How to Export Pivot Table as an Image in C# – Step‑by‑Step Guide](/cells/english/net/pivot-tables/how-to-export-pivot-table-as-an-image-in-c-step-by-step-guid/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}