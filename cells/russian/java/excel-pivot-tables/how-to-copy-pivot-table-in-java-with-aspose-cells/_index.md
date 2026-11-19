---
category: general
date: 2026-11-19
description: Узнайте, как скопировать сводную таблицу в Java, сохранив её данные и
  макет. Это пошаговое руководство также показывает, как эффективно копировать сводные
  таблицы Excel.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy pivot table
- how to copy pivot
- how to preserve pivot
- preserve pivot table
- copy excel pivot
language: ru
lastmod: 2026-11-19
og_description: Копировать сводную таблицу в Java с помощью Aspose.Cells. Следуйте
  этому руководству, чтобы узнать, как сохранять сводные таблицы и точно копировать
  данные сводных таблиц Excel.
og_image_alt: Illustration of the copy pivot table workflow in Java
og_title: Копирование сводной таблицы в Java – полное руководство по Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-11-19'
  description: Learn how to copy pivot table in Java while preserving its data and
    layout. This step‑by‑step guide also shows how to copy excel pivot tables efficiently.
  headline: How to copy pivot table in Java with Aspose.Cells
  type: TechArticle
tags:
- Java
- Aspose.Cells
- Excel automation
- Pivot tables
title: Как скопировать сводную таблицу в Java с помощью Aspose.Cells
url: /ru/java/excel-pivot-tables/how-to-copy-pivot-table-in-java-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как скопировать сводную таблицу в Java с помощью Aspose.Cells

Если вам нужно **скопировать сводную таблицу** из одной книги в другую, это руководство покажет, как сделать это в Java. Независимо от того, создаёте ли вы движок отчётов или переносите данные, вы увидите надёжный способ сохранить кэш сводной таблицы, её поля и форматирование.

Копирование сводной таблицы может быть сложным, потому что простое копирование диапазона часто теряет исходный источник данных. В этом уроке мы используем Aspose.Cells, чтобы **скопировать сводную таблицу**, сохранив все расчёты, а также рассмотрим **как сохранить сводные таблицы**, когда целевая книга пуста.

## Требования

Прежде чем начать, убедитесь, что у вас есть:

* Java 17 или новее.
* Aspose.Cells for Java (версия 23.9 или новее), добавленная в classpath вашего проекта.
* Два Excel‑файла: исходная книга, содержащая сводную таблицу, и пустая целевая книга (или книга, в которую вы хотите выполнить слияние).

Для примера кода лицензия не требуется, но действующая лицензия Aspose.Cells убирает водяные знаки оценки.

## Шаг 1: Загрузите исходную книгу, содержащую сводную таблицу

Первый шаг — открыть книгу, в которой находится оригинальная сводная таблица. Загрузка файла даёт доступ к листу, ячейкам и кэшу сводной таблицы.

```java
// Step 1: Load the source workbook that contains the pivot table
Workbook srcWb = new Workbook("YOUR_DIRECTORY/source.xlsx");
```

*Почему это важно*: Aspose.Cells читает всю книгу, включая скрытые данные кэша, которые питают сводную таблицу. Без полной загрузки файл копирования потеряет определение сводной таблицы.

## Шаг 2: Подготовьте целевую книгу

Создайте новую книгу (или откройте существующую) и получите её первый лист. Именно туда будет помещена сводная таблица.

```java
// Step 2: Create a new destination workbook and get its first worksheet
Workbook destWb = new Workbook();                     // empty workbook
Worksheet destWs = destWb.getWorksheets().get(0);    // first sheet
```

*Подсказка*: Если у вас уже есть целевая книга, замените вызов `new Workbook()` на `new Workbook("target.xlsx")`. Это позволит **скопировать excel pivot** в уже заполненную книгу.

## Шаг 3: Определите область ячеек, охватывающую сводную таблицу

Необходимо указать точный диапазон, покрывающий сводную таблицу. Диапазон включает таблицу сводной, список полей и любые окружающие данные, которые вы хотите сохранить.

```java
// Step 3: Define the cell area that covers the pivot table in the source sheet
CellArea area = CellArea.createCellArea("A1", "H30"); // adjust as needed
```

*Почему это важно*: `CellArea` сообщает Aspose.Cells, что копировать. Если область слишком мала, сводная будет обрезана; если слишком велика — скопируются лишние данные. Настройте координаты в соответствии с реальными размерами вашей сводной таблицы.

## Шаг 4: Выполните копирование с помощью CopyOptions

Вызовите метод `copy` у коллекции ячеек исходного листа. Передача нового объекта `CopyOptions()` гарантирует, что будет перенесено всё форматирование, формулы и кэш сводной таблицы.

```java
// Step 4: Copy the defined range (including the pivot table) to the destination worksheet
srcWb.getWorksheets().get(0).getCells().copy(area, destWs.getCells(), new CopyOptions());
```

### Почему `CopyOptions` сохраняет сводную таблицу

`CopyOptions` указывает Aspose.Cells рассматривать диапазон как *целый* объект, а не как набор отдельных значений. Это ключ к **how to preserve pivot**: кэш сводной дублируется, поэтому целевая книга может пересчитать сводную без дополнительного вмешательства.

## Шаг 5: Сохраните целевую книгу

Наконец, запишите целевой файл на диск. Сохранённый файл будет содержать полностью рабочую копию оригинальной сводной таблицы.

```java
// Step 5: Save the destination workbook – the pivot table is preserved
destWb.save("YOUR_DIRECTORY/copied_with_pivot.xlsx");
```

*Ожидаемый результат*: Открытие `copied_with_pivot.xlsx` в Excel показывает идентичную сводную таблицу со слайсерами, фильтрами и вычисляемыми полями. Вы можете обновить её, и источник данных будет указывать на скопированный диапазон внутри той же книги.

---

![Диаграмма, показывающая процесс копирования сводной таблицы](/images/copy-pivot-table-workflow.png){.align-center width=600 alt="Диаграмма, иллюстрирующая процесс копирования сводной таблицы из исходной книги в целевую"}

## Как копировать сводные таблицы между несколькими листами

Если нужно **скопировать excel pivot** таблицы с нескольких листов, повторите Шаги 3‑4 для каждого исходного листа. Можно также пройтись циклом по `srcWb.getWorksheets()` и копировать каждую сводную в соответствующий лист `destWb`. Ниже — лаконичный пример цикла:

```java
for (int i = 0; i < srcWb.getWorksheets().getCount(); i++) {
    Worksheet srcWs = srcWb.getWorksheets().get(i);
    Worksheet newDestWs = destWb.getWorksheets().add();
    // Assume each pivot occupies A1:H30 – adjust per sheet if needed
    CellArea area = CellArea.createCellArea("A1", "H30");
    srcWs.getCells().copy(area, newDestWs.getCells(), new CopyOptions());
}
destWb.save("YOUR_DIRECTORY/multi_sheet_copy.xlsx");
```

*Профессиональный совет*: Используйте `srcWs.getPivotTables().getCount()`, чтобы проверить, содержит ли лист сводную таблицу, прежде чем копировать. Это избавит от копирования нерелевантных данных.

## Распространённые подводные камни и как их избежать

| Проблема | Почему происходит | Решение |
|----------|-------------------|---------|
| **Сводная теряет кэш** | Используется `Worksheet.copy()` без `CopyOptions`, копируются только значения ячеек. | Всегда используйте `srcWs.getCells().copy(..., new CopyOptions())`. |
| **В целевой книге появляются ошибки #REF!** | Скопированная сводная всё ещё ссылается на внешний источник данных исходной книги. | После копирования вызовите `destWs.getPivotTables().get(0).refresh();`, чтобы привязать кэш к новому диапазону. |
| **Слайсеры исчезают** | Слайсеры хранятся вне основной области ячеек. | Расширьте `CellArea`, включив диапазоны слайсеров, или копируйте весь лист (`srcWs.copy(destWs, new CopyOptions())`). |
| **Снижение производительности при больших сводных** | Копирование огромных диапазонов с форматированием может быть медленным. | Используйте `CopyOptions.setOnlyData(true)`, если форматирование не требуется, а затем применяйте стили вручную. |

## Как сохранить форматирование сводной таблицы при обновлении данных

Иногда требуется **how to preserve pivot** макет после изменения исходных данных. После копирования можно зафиксировать стиль сводной:

```java
PivotTable pt = destWs.getPivotTables().get(0);
pt.setPreserveFormatting(true);   // keeps colors, fonts, and layout
pt.refresh();                     // recalculates with new data
```

Установка `PreserveFormatting` гарантирует, что любые пользовательские стили, применённые в источнике, сохранятся при копировании.

## Проверка копии

Быстрый способ убедиться, что копирование прошло успешно, — сравнить определения сводных таблиц:

```java
PivotTable srcPt = srcWb.getWorksheets().get(0).getPivotTables().get(0);
PivotTable destPt = destWs.getPivotTables().get(0);

System.out.println("Source fields: " + srcPt.getFields().size());
System.out.println("Destination fields: " + destPt.getFields().size());
// Both numbers should match
```

Если количества совпадают и целевая книга открывается без ошибок, вы успешно **copy pivot table**.

## Заключение

Теперь вы знаете, как **copy pivot table** из одной Excel‑книги в другую с помощью Aspose.Cells для Java, и видели точные шаги **how to copy pivot**, обеспечивая сохранность кэша, форматирования и слайсеров. Тот же подход работает для сценариев **copy excel pivot** на нескольких листах, а код можно адаптировать под особые случаи, такие как сохранение форматирования сводных или работа с большими наборами данных.

### Что дальше

* Изучите параметры **preserve pivot table**, такие как `setPreserveFormatting` и `refresh`, для динамических источников данных.  
* Попробуйте копировать сводные таблицы между книгами с разным порядком столбцов — скорректируйте `CellArea` соответственно.  
* Совместите эту технику с Aspose.Slides, чтобы вставлять снимки сводных в презентации PowerPoint.

Удачной разработки, экспериментируйте с вариантами, чтобы они соответствовали вашему конвейеру автоматизации!

## Что вам стоит изучить дальше?

Следующие руководства охватывают близкие темы, расширяющие техники, продемонстрированные в этом руководстве. Каждый ресурс содержит полностью работающие примеры кода с пошаговыми объяснениями, помогающими освоить дополнительные возможности API и исследовать альтернативные подходы в ваших проектах.

- [Как скопировать диапазон и сохранить сводную таблицу в Java](/cells/english/java/excel-pivot-tables/how-to-copy-range-and-preserve-a-pivot-table-in-java/)
- [Как скопировать сводную таблицу между листами в Java](/cells/english/java/excel-pivot-tables/how-to-copy-a-pivot-table-between-worksheets-in-java/)
- [Как скопировать сводную таблицу в новую книгу в Java](/cells/english/java/excel-pivot-tables/how-to-copy-pivot-table-to-a-new-workbook-in-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}