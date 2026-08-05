---
category: general
date: 2026-08-04
description: Копировать сводную таблицу с помощью Aspose.Cells для Java. Узнайте,
  как копировать диапазон Excel, дублировать сводную таблицу и копировать лист с сводной
  таблицей всего за несколько строк.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy pivot table
- copy excel range
- copy range java
- duplicate pivot table
- copy worksheet with pivot
language: ru
lastmod: 2026-08-04
og_description: Скопировать сводную таблицу с помощью Aspose.Cells для Java. Этот
  учебник пошагово покажет, как скопировать диапазон Excel, дублировать сводную таблицу
  и сохранить все данные на новом листе.
og_image_alt: Screenshot of a Java program that copies a pivot table to a new worksheet
og_title: Копировать сводную таблицу в Java – полный учебник Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-08-04'
  description: Copy pivot table with Aspose.Cells for Java. Learn how to copy excel
    range, duplicate pivot table, and copy worksheet with pivot in just a few lines.
  headline: Copy pivot table in Java – step‑by‑step guide using Aspose.Cells
  type: TechArticle
- description: Copy pivot table with Aspose.Cells for Java. Learn how to copy excel
    range, duplicate pivot table, and copy worksheet with pivot in just a few lines.
  name: Copy pivot table in Java – step‑by‑step guide using Aspose.Cells
  steps:
  - name: '`CopyWithPivot.xlsx` appears in `YOUR_DIRECTORY`.'
    text: '`CopyWithPivot.xlsx` appears in `YOUR_DIRECTORY`.'
  - name: Opening the file in Excel shows a new sheet named **CopySheet**.
    text: Opening the file in Excel shows a new sheet named **CopySheet**.
  - name: '**CopySheet** contains a fully functional pivot table identical to the
      original, ready to refresh.'
    text: '**CopySheet** contains a fully functional pivot table identical to the
      original, ready to refresh.'
  - name: All formatting, filters, and calculated fields are preserved.
    text: All formatting, filters, and calculated fields are preserved.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
- PivotTable
- Data copying
title: Копирование сводной таблицы в Java – пошаговое руководство с использованием
  Aspose.Cells
url: /ru/java/excel-pivot-tables/copy-pivot-table-in-java-step-by-step-guide-using-aspose-cel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Копирование сводной таблицы в Java – пошаговое руководство с использованием Aspose.Cells

Если вам нужно **скопировать сводную таблицу** из одного листа в другой в Java, это руководство покажет, как сделать это с помощью Aspose.Cells. Независимо от того, генерируете ли вы отчёты программно или создаёте инструмент миграции данных, вы увидите полный, исполняемый пример, сохраняющий определение и данные сводной таблицы.

Копирование сводной таблицы — это больше, чем просто копирование диапазона ячеек; скрытый кэш и источник данных должны оставаться неизменными. В этом уроке мы также рассмотрим, как **скопировать диапазон Excel**, как **дублировать сводную таблицу** между листами и как **скопировать лист со сводной таблицей** с использованием того же API.

## Требования

* Java Development Kit (JDK) 8 или новее.
* Maven или Gradle для управления зависимостями.
* Aspose.Cells for Java (последняя версия, например, 23.12). Добавьте следующую координату Maven в ваш `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version>
</dependency>
```

* Исходный рабочий файл (`Source.xlsx`), содержащий сводную таблицу на первом листе.

## Как скопировать сводную таблицу в Java с помощью Aspose.Cells

Основная идея состоит в том, чтобы скопировать *исходный диапазон*, охватывающий сводную таблицу, а затем вставить его в новый лист. Aspose.Cells автоматически копирует кэш сводной таблицы, поэтому полученный лист содержит полностью функциональную **дублированную сводную таблицу**.

```java
import com.aspose.cells.*;

public class CopyPivotTableDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Load the workbook that contains the PivotTable
        Workbook workbook = new Workbook("YOUR_DIRECTORY/Source.xlsx");

        // Step 2: Define the source range (including the PivotTable) to be copied
        // The range must cover the entire pivot table area, e.g., A1:G20
        Range sourceRange = workbook.getWorksheets()
                                    .get(0)                 // first worksheet
                                    .getCells()
                                    .createRange("A1:G20");

        // Step 3: Add a new worksheet that will receive the copied range
        Worksheet destinationSheet = workbook.getWorksheets().add("CopySheet");

        // Step 4: Copy the source range to cell A1 of the new worksheet
        sourceRange.copy(destinationSheet.getCells().createRange("A1"));

        // Step 5: Save the workbook with the copied PivotTable intact
        workbook.save("YOUR_DIRECTORY/CopyWithPivot.xlsx");
    }
}
```

### Почему это работает

* **Копирование диапазона включает кэш сводной таблицы** – Aspose.Cells рассматривает сводную таблицу как специальный объект, встроенный в диапазон ячеек. При вызове `Range.copy` библиотека копирует как видимые ячейки, так и скрытый кэш, который питает сводную таблицу.
* **Не требуется ручное воссоздание** – Вам не нужно восстанавливать поля сводной таблицы или источник данных; дубликат готов к мгновенному обновлению.
* **Работает с любой версией Excel** – Сгенерированный файл соответствует стандарту Office Open XML (XLSX), поэтому Excel 2007+ открывает его без предупреждений.

## Копировать диапазон Excel – повторное использование того же кода для данных без сводных таблиц

Если вам нужно только **скопировать диапазон Excel** без сводной таблицы, применяется тот же шаблон. Просто измените адрес диапазона на область, которую хотите дублировать.

```java
// Example: copy A1:D10 from Sheet1 to Sheet2
Range dataRange = workbook.getWorksheets()
                          .get(0)
                          .getCells()
                          .createRange("A1:D10");
Worksheet sheet2 = workbook.getWorksheets().add("DataCopy");
dataRange.copy(sheet2.getCells().createRange("A1"));
```

Метод `copy` сохраняет формулы, форматирование и комментарии, делая его универсальным решением для любого блока данных Excel.

## Дублировать сводную таблицу на нескольких листах

Иногда необходимо **дублировать сводную таблицу** несколько раз — например, по одному на каждый отдел. Пройдитесь по листам назначения и повторно используйте тот же вызов `sourceRange.copy`:

```java
String[] departments = {"Sales", "Marketing", "Finance"};
for (String dept : departments) {
    Worksheet ws = workbook.getWorksheets().add(dept + "Pivot");
    sourceRange.copy(ws.getCells().createRange("A1"));
}
```

Каждый новый лист содержит независимую сводную таблицу, которую можно обновлять отдельно. Кэш дублируется, поэтому изменения в одном листе не влияют на другие.

## Копировать лист со сводной таблицей — сохранение настроек уровня листа

Если вы хотите **скопировать лист со сводной таблицей**, одновременно сохранив параметры страницы, ширину столбцов и именованные диапазоны, используйте `Worksheet.copy` вместо ручного копирования диапазона. Этот метод клонирует весь лист, включая сводную таблицу.

```java
Worksheet original = workbook.getWorksheets().get(0);
Worksheet clone = workbook.getWorksheets().addCopy(original);
clone.setName("FullCopy");
workbook.save("YOUR_DIRECTORY/FullCopy.xlsx");
```

`addCopy` удобен, когда лист содержит диаграммы, изображения или пользовательские стили, которые должны перемещаться вместе со сводной таблицей.

## Распространённые подводные камни и как их избежать

| Проблема | Почему происходит | Решение |
|----------|-------------------|---------|
| **Потеря кэша сводной таблицы после копирования** | Использование `Cell.copy` для отдельных ячеек (вместо диапазона) отбрасывает скрытый кэш. | Всегда копируйте *весь* диапазон, охватывающий сводную таблицу, как показано в Шаге 2. |
| **Исходный диапазон слишком мал** | Диапазон не включает область данных сводной таблицы, поэтому на новом листе отображаются только статические значения. | Увеличьте адрес (например, `A1:G20`), чтобы охватить всю сводную таблицу и любые срезы или фильтры. |
| **Несоответствие версии целевого рабочего файла** | Сохранение в формате XLS (устаревший) удаляет современные функции сводных таблиц. | Сохраните как XLSX (по умолчанию) или явно укажите `SaveFormat.XLSX`. |
| **Внешний источник данных повреждён** | Сводная таблица ссылается на источник данных вне рабочей книги; копирование не встраивает его. | Используйте `PivotTable.refreshData()` после копирования или встраивайте исходные данные в ту же рабочую книгу. |

## Ожидаемый результат

После запуска программы:

1. `CopyWithPivot.xlsx` появляется в `YOUR_DIRECTORY`.
2. Открывая файл в Excel, вы видите новый лист с именем **CopySheet**.
3. **CopySheet** содержит полностью функциональную сводную таблицу, идентичную оригиналу, готовую к обновлению.
4. Все форматирование, фильтры и вычисляемые поля сохраняются.

Если открыть `FullCopy.xlsx`, вы увидите полную копию оригинального листа, включая любые диаграммы или изображения, которые были на исходном листе.

## Итоги

* Вы узнали, как **скопировать сводную таблицу** в Java с помощью Aspose.Cells.
* Тот же подход работает для простого **копирования диапазона Excel** или сценариев **copy range java**.
* Для массовых операций вы можете **дублировать сводную таблицу** на многих листах.
* Когда нужен весь лист, **copy worksheet with pivot** с использованием `addCopy`.

## Следующие шаги

* Изучите **PivotTable.refreshData()**, чтобы программно обновлять кэш после копирования.
* Скомбинируйте логику копирования с **Excel file streaming**, чтобы работать с большими рабочими книгами без загрузки всего в память.
* Ознакомьтесь с поддержкой **pivot slicers** в Aspose.Cells, если ваши отчёты используют интерактивные фильтры.

Не стесняйтесь адаптировать код под структуру вашего проекта, экспериментировать с различными размерами диапазонов или интегрировать его в более крупный конвейер обработки данных. Приятного кодинга!

## Что стоит изучить дальше?

Следующие учебники охватывают тесно связанные темы, основанные на техниках, продемонстрированных в этом руководстве. Каждый ресурс включает полные работающие примеры кода с пошаговыми объяснениями, помогающими освоить дополнительные возможности API и исследовать альтернативные подходы к реализации в ваших проектах.

- [Как обновить источник сводной таблицы Excel с помощью Aspose.Cells для Java: Полное руководство](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [Манипуляция сводными таблицами Excel Aspose Cells Java](/cells/hongkong/java/data-analysis/excel-pivot-table-manipulation-aspose-cells-java/)
- [Создание новой рабочей книги Excel – копирование и дублирование сводной таблицы](/cells/english/net/pivot-tables/create-new-excel-workbook-copy-duplicate-pivot-table/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}