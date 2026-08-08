---
category: general
date: 2026-08-08
description: Как скопировать сводную таблицу в Aspose.Cells и скопировать диапазон
  в книгу с помощью Java. Узнайте точные шаги для дублирования сводной таблицы с использованием
  CopyOptions.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy pivot
- copy range to workbook
- aspose.cells copy range
language: ru
lastmod: 2026-08-08
og_description: Как скопировать сводную таблицу в Aspose.Cells и скопировать диапазон
  в книгу с помощью Java. Следуйте этому полному руководству, чтобы дублировать сводную
  таблицу, используя CopyOptions.
og_image_alt: Diagram showing how to copy pivot in Aspose.Cells
og_title: Как скопировать сводную таблицу в Aspose.Cells – копировать диапазон в рабочую
  книгу
schemas:
- author: Aspose
  dateModified: '2026-08-08'
  description: How to copy pivot in Aspose.Cells and copy range to workbook using
    Java. Learn the exact steps to duplicate a pivot table with CopyOptions.
  headline: How to copy pivot in Aspose.Cells – copy range to workbook
  type: TechArticle
- description: How to copy pivot in Aspose.Cells and copy range to workbook using
    Java. Learn the exact steps to duplicate a pivot table with CopyOptions.
  name: How to copy pivot in Aspose.Cells – copy range to workbook
  steps:
  - name: Add Aspose.Cells to your project
    text: 'If you use Maven, add the following dependency to your `pom.xml`:'
  - name: Load the source workbook
    text: '```java import com.aspose.cells.*;'
  - name: Configure copy options to include the pivot table
    text: '```java // Define copy options to include the pivot table in the copied
      range CopyOptions copyOptions = new CopyOptions() .setCopyPivotTable(true);
      ```'
  - name: Copy the desired range with the pivot table
    text: '```java // Copy the range A1:H20, preserving the pivot table workbook.getWorksheets().get(0).getCells()
      .copyRange("A1:H20", copyOptions); ```'
  - name: Save the modified workbook
    text: '```java // Save the workbook with the copied pivot table workbook.save("YOUR_DIRECTORY/output.xlsx");
      } } ```'
  - name: Expected result
    text: '* `output.xlsx` contains the same data as `input.xlsx`. * The pivot table
      that originally occupied the source range appears in the destination cells,
      fully functional (filters, refresh capability, etc.). * All cell formatting,
      formulas, and column widths are preserved because `copyRange` copies the '
  type: HowTo
tags:
- Aspose.Cells
- Java
- PivotTable
- CopyRange
title: Как скопировать сводную таблицу в Aspose.Cells – копировать диапазон в рабочую
  книгу
url: /ru/java/excel-pivot-tables/how-to-copy-pivot-in-aspose-cells-copy-range-to-workbook/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как скопировать сводную таблицу в Aspose.Cells – копировать диапазон в книгу

Если вам нужно **скопировать сводную таблицу** в файле Excel с помощью Aspose.Cells, это руководство покажет точный процесс. К концу урока вы сможете **скопировать диапазон в книгу**, сохранив определение сводной таблицы.

В примере используется Java, но те же концепции применимы к любому .NET‑языку, работающему с Aspose.Cells. Внешние инструменты не требуются — только библиотека Aspose.Cells for Java и базовая среда разработки.

## Требования

Прежде чем начать, убедитесь, что у вас есть:

* Java Development Kit (JDK) 8 или новее.  
* Maven или Gradle для управления зависимостями (в примере используется Maven).  
* Aspose.Cells for Java 23.9 (или последняя версия), добавленная в ваш проект.  
* Входная книга (`input.xlsx`), содержащая как минимум одну сводную таблицу на первом листе.

Наличие этих элементов предотвращает ошибки выполнения при доступе к книге.

## Как скопировать сводную таблицу с помощью Aspose.Cells

В этом разделе пошагово рассматривается процесс **копирования сводной таблицы** из одной части листа в другую с использованием класса `CopyOptions`.

### Шаг 1: Добавьте Aspose.Cells в ваш проект

Если вы используете Maven, добавьте следующую зависимость в ваш `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.9</version>
    <classifier>jdk17</classifier> <!-- adjust JDK version as needed -->
</dependency>
```

*Почему это важно*: Библиотека предоставляет классы `Workbook`, `CopyOptions` и другие, необходимые для операций **aspose.cells copy range**. Без зависимости компилятор не сможет разрешить эти типы.

### Шаг 2: Загрузите исходную книгу

```java
import com.aspose.cells.*;

public class CopyPivotTableRange {
    public static void main(String[] args) throws Exception {
        // Load the workbook that contains the pivot table
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

Загрузка файла создаёт представление таблицы в памяти. Объект `Workbook` даёт доступ к листам, ячейкам и сводным таблицам.

### Шаг 3: Настройте параметры копирования для включения сводной таблицы

```java
        // Define copy options to include the pivot table in the copied range
        CopyOptions copyOptions = new CopyOptions()
                .setCopyPivotTable(true);
```

`CopyOptions.setCopyPivotTable(true)` указывает Aspose.Cells, что операция должна сохранять метаданные сводной таблицы. Если этот флаг опустить, сводная таблица превратится в статические данные, потеряв интерактивность.

### Шаг 4: Скопируйте нужный диапазон вместе со сводной таблицей

```java
        // Copy the range A1:H20, preserving the pivot table
        workbook.getWorksheets().get(0).getCells()
                .copyRange("A1:H20", copyOptions);
```

Метод `copyRange` копирует ячейки, форматирование и — благодаря настройкам из предыдущего шага — любые сводные таблицы, пересекающие диапазон. Это ядро функциональности **copy range to workbook**.

### Шаг 5: Сохраните изменённую книгу

```java
        // Save the workbook with the copied pivot table
        workbook.save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

Сохранение записывает изменения в новый файл (`output.xlsx`). Теперь вы можете открыть его в Excel и увидеть, что сводная таблица была точно дублирована в месте копирования диапазона.

## Полный, исполняемый пример

Объединив все части, получаем полную программу, которую можно скомпилировать и запустить:

```java
import com.aspose.cells.*;

public class CopyPivotTableRange {
    public static void main(String[] args) throws Exception {
        // 1. Load the workbook that contains the pivot table
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // 2. Define copy options to include the pivot table
        CopyOptions copyOptions = new CopyOptions()
                .setCopyPivotTable(true);

        // 3. Copy the range A1:H20 with the specified options
        workbook.getWorksheets().get(0).getCells()
                .copyRange("A1:H20", copyOptions);

        // 4. Save the modified workbook
        workbook.save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

### Ожидаемый результат

* `output.xlsx` содержит те же данные, что и `input.xlsx`.  
* Сводная таблица, изначально находившаяся в исходном диапазоне, появляется в целевых ячейках, полностью функциональная (фильтры, возможность обновления и т.д.).  
* Всё форматирование ячеек, формулы и ширины столбцов сохраняются, поскольку `copyRange` копирует весь блок ячеек.

## Распространённые вопросы и особые случаи

**Что делать, если целевой диапазон пересекается с существующей сводной таблицей?**  
Aspose.Cells перезапишет целевые ячейки. Чтобы избежать потери данных, убедитесь, что область назначения пуста, либо сначала переместите существующую сводную таблицу.

**Можно ли копировать сводную таблицу между листами?**  
Да. Используйте `workbook.getWorksheets().get(targetSheetIndex).getCells().copyRange(sourceRange, copyOptions);`, где `targetSheetIndex` указывает на лист‑назначение.

**Копирует ли `setCopyPivotTable(true)` исходный источник данных?**  
Метод копирует только ссылку на кэш сводной таблицы. Если исходные данные находятся в той же книге, сводная таблица в месте назначения будет ссылаться на тот же кэш. Чтобы дублировать кэш, его нужно создать вручную.

**Как эффективно копировать большой диапазон?**  
При копировании очень больших диапазонов рассмотрите возможность использования только `CopyOptions.setCopyFormula(true)` и `setCopyDataValidation(true)` при необходимости. Сокращение количества опций может улучшить производительность.

## Советы по надёжному использованию **aspose.cells copy range**

* **Pro tip:** Всегда вызывайте `workbook.calculateFormula()` после копирования, если диапазон содержит формулы, зависящие от кэша сводной таблицы.  
* **Обратите внимание:** Скрытые листы. `copyRange` работает только с видимыми листами, если вы явно не укажете скрытый лист по индексу.  
* **Проверка версии:** Флаг `setCopyPivotTable` доступен, начиная с Aspose.Cells 20.9. Убедитесь, что ваша версия библиотеки поддерживает его.

## Заключение

Теперь вы знаете, **как скопировать сводную таблицу** в Aspose.Cells и **как скопировать диапазон в книгу**, сохранив полную функциональность сводной таблицы. Шаги — добавление библиотеки, загрузка книги, настройка `CopyOptions`, выполнение копирования и сохранение — образуют повторяемый шаблон, который можно адаптировать к другим сценариям копирования‑вставки.

Далее изучайте связанные темы, такие как **aspose.cells copy range** для диаграмм, условного форматирования и проверки данных. Поэкспериментируйте с копированием между разными форматами файлов (XLSX → XLS), чтобы расширить возможности автоматизации. Приятного кодинга!

## Что следует изучить дальше?

Следующие руководства охватывают тесно связанные темы, построенные на техниках, продемонстрированных в этом руководстве. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, помогая вам освоить дополнительные возможности API и исследовать альтернативные подходы в собственных проектах.

- [Как создать сводные таблицы в Excel с помощью Aspose.Cells для Java: Полное руководство](/cells/english/java/data-analysis/create-pivot-tables-excel-aspose-cells-java/)
- [Как обновить источник данных сводной таблицы Excel с помощью Aspose.Cells для Java: Полное руководство](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [Как реализовать срезы в сводных таблицах с помощью Aspose.Cells для Java: Полное руководство](/cells/english/java/data-analysis/implement-slicers-pivot-tables-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}