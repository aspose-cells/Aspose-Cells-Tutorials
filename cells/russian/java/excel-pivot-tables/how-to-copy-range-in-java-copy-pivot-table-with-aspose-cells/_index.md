---
category: general
date: 2026-06-30
description: Как скопировать диапазон в Java с помощью Aspose.Cells – дублировать
  диапазон Excel, копировать сводную таблицу и эффективно загружать книгу Excel.
draft: false
keywords:
- how to copy range
- copy pivot table
- pivot table to sheet
- duplicate excel range
- load excel workbook
language: ru
og_description: Как копировать диапазон в Java с помощью Aspose.Cells. Узнайте, как
  дублировать диапазон Excel, копировать сводную таблицу и загружать книгу Excel за
  считанные минуты.
og_title: Как скопировать диапазон в Java – пошаговое руководство
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: How to copy range in Java using Aspose.Cells – duplicate Excel range,
    copy pivot table, and load Excel workbook efficiently.
  headline: How to copy range in Java – Copy Pivot Table with Aspose.Cells
  type: TechArticle
- description: How to copy range in Java using Aspose.Cells – duplicate Excel range,
    copy pivot table, and load Excel workbook efficiently.
  name: How to copy range in Java – Copy Pivot Table with Aspose.Cells
  steps:
  - name: Expected Output
    text: 'When you execute `CopyPivotDemo`, the console prints:'
  - name: What if the source workbook has multiple worksheets?
    text: You can loop through `sourceWorkbook.getWorksheets()` and copy each relevant
      range. Just be careful to maintain the same sheet names in the destination if
      you need to preserve references.
  - name: Does the copied pivot retain its data source?
    text: Yes. Aspose.Cells copies the pivot cache along with the range, so the destination
      workbook still points to the original data source within the same file. If you
      later move the data to a different sheet, you may need to refresh the pivot
      manually.
  - name: How to copy a pivot that uses an external data source?
    text: When the pivot’s data source is an external file, you’ll have to embed that
      data into the destination workbook first (e.g., copy the source data range)
      before copying the pivot. Otherwise the pivot will show “#REF!” errors.
  - name: Can I copy the pivot without the surrounding data?
    text: Absolutely. Just adjust `pivotRange` to cover only the pivot’s cells (usually
      the top‑left corner plus the data area). You can also use `sourceSheet.getPivotTables().get(0).getPivotTableArea()`
      to retrieve the exact range programmatically.
  type: HowTo
tags:
- Java
- Aspose.Cells
- Excel Automation
title: Как скопировать диапазон в Java – Копирование сводной таблицы с помощью Aspose.Cells
url: /ru/java/excel-pivot-tables/how-to-copy-range-in-java-copy-pivot-table-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как скопировать диапазон в Java – копирование сводной таблицы с помощью Aspose.Cells

Когда‑то задавались вопросом **как скопировать диапазон** из одной книги Excel в другую, не потеряв целостность сводной таблицы? Вы не одиноки. Во многих конвейерах отчетности необходимость *дублировать диапазон Excel* при сохранении логики сводной таблицы становится ежедневной головной болью. К счастью, Aspose.Cells для Java делает это проще простого, и в этом руководстве мы пройдем полный, готовый к запуску пример, который также покажет, как **загрузить книгу Excel**, скопировать сводную таблицу и сохранить результат.

К концу этого руководства у вас будет автономная Java‑программа, которая:

* Загружает существующую книгу (`load excel workbook`);
* Определяет точные ячейки, содержащие сводную таблицу;
* Копирует эту **сводную таблицу на лист** в совершенно новой книге;
* Сохраняет новый файл, готовый к дальнейшей обработке.

Никаких внешних скриптов, никаких ручных шагов — только чистый код.

## Что вам понадобится

Прежде чем погрузиться в детали, убедитесь, что у вас есть:

* Java 8 или новее (код также работает с Java 11+);
* Библиотека Aspose.Cells for Java (можно взять из Maven Central);
* Два примера файлов Excel — один‑источник со сводной таблицей (`source.xlsx`) и папка‑назначение, куда будет записан `copy-pivot.xlsx`.

И всё. Никаких сложных трюков в IDE; любой текстовый редактор и `javac` подойдут.

## Шаг 1: Настройка проекта и импорт Aspose.Cells

Сначала подключим библиотеку. Если вы используете Maven, добавьте эту зависимость в ваш `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version> <!-- check for the latest version -->
</dependency>
```

Если Maven не используется, скачайте JAR с сайта Aspose и разместите его в classpath. После этого создайте новый Java‑класс под названием `CopyPivotDemo`.

```java
package com.example.excel;

import com.aspose.cells.*;

public class CopyPivotDemo {
    public static void main(String[] args) throws Exception {
        // The implementation will go here.
    }
}
```

> **Pro tip:** Держите папку `src/main/java` в порядке и дайте классу осмысленное имя; это упростит дальнейшее обслуживание.

## Шаг 2: Загрузка исходной книги (`load excel workbook`)

Теперь действительно **load excel workbook**, содержащую сводную таблицу, которую нужно скопировать. Конструктор `Workbook` принимает путь к файлу, поэтому убедитесь, что путь указан правильно.

```java
// Step 2: Load the source workbook
Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/source.xlsx");

// Grab the first worksheet (index 0)
Worksheet sourceSheet = sourceWorkbook.getWorksheets().get(0);
```

Почему мы выбираем первый лист? В большинстве простых случаев сводная таблица находится на первом листе, но при необходимости можно изменить индекс или использовать имя листа. Такая гибкость — одна из причин, почему Aspose.Cells так хорош.

## Шаг 3: Определение диапазона, содержащего сводную таблицу

Сводная таблица обычно охватывает блок ячеек. Предположим, что она занимает `A1:G20`. При необходимости скорректируйте адрес под свои данные.

```java
// Step 3: Define the range that includes the pivot table
Range pivotRange = sourceSheet.getCells().createRange("A1:G20");
```

Если вы не уверены в точном адресе, откройте книгу в Excel, выделите всю сводную таблицу и посмотрите в поле имени. Помните, **duplicate excel range** работает лучше всего, когда вы указываете точную область — без лишних строк и без недостающих столбцов.

## Шаг 4: Создание новой книги‑назначения

Нужна свежая книга, которая получит скопированный диапазон. Здесь мы **copy pivot table** на новый лист.

```java
// Step 4: Create a new workbook to receive the copied range
Workbook destinationWorkbook = new Workbook(); // starts with a default empty sheet
Worksheet destinationSheet = destinationWorkbook.getWorksheets().get(0);
```

На данный момент книга‑назначение пуста, но Aspose.Cells автоматически добавляет лист по умолчанию, которым мы и будем пользоваться в качестве цели.

## Шаг 5: Копирование диапазона — сводная таблица остаётся целой

Вот магическая строка, которая **copy pivot table**, сохраняя все внутренние связи.

```java
// Step 5: Copy the range (pivot table stays intact) to the destination sheet
destinationSheet.getCells().copy(pivotRange,
        destinationSheet.getCells().createRange("A1"));
```

Метод `copy` принимает два аргумента: исходный `Range` и целевой `Range`. Начав целевой диапазон с `A1`, мы размещаем сводную таблицу точно там, где она была в источнике. Aspose.Cells копирует подлежащий кэш сводной таблицы, поэтому новая книга всё ещё умеет обновлять сводную таблицу.

## Шаг 6: Сохранение полученной книги

Наконец, запишем новый файл на диск. Вы можете выбрать любой поддерживаемый Aspose формат (`.xlsx`, `.xls`, `.csv` и т.д.). Остановимся на `.xlsx`.

```java
// Step 6: Save the resulting workbook
destinationWorkbook.save("YOUR_DIRECTORY/copy-pivot.xlsx");
System.out.println("Pivot table successfully copied to copy-pivot.xlsx");
```

Запустите программу, и вы увидите новую книгу с тем же макетом сводной таблицы. Откройте её в Excel — если всё прошло успешно, вы сможете обновить сводную таблицу без ошибок.

### Ожидаемый вывод

При выполнении `CopyPivotDemo` в консоль будет выведено:

```
Pivot table successfully copied to copy-pivot.xlsx
```

Открытие `copy-pivot.xlsx` покажет лист, идентичный области сводной таблицы в исходнике, и **pivot table to sheet** будет работать так же, как оригинал.

## Полный рабочий пример

Ниже представлен полностью готовый к запуску Java‑класс, объединяющий все шаги. Скопируйте‑вставьте его в свою IDE, поправьте пути к файлам и запустите.

```java
package com.example.excel;

import com.aspose.cells.*;

public class CopyPivotDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load the source workbook (load excel workbook)
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/source.xlsx");
        Worksheet sourceSheet = sourceWorkbook.getWorksheets().get(0);

        // 2️⃣ Define the range that contains the pivot table
        // Adjust the address if your pivot occupies a different area
        Range pivotRange = sourceSheet.getCells().createRange("A1:G20");

        // 3️⃣ Create a fresh workbook for the destination
        Workbook destinationWorkbook = new Workbook(); // empty workbook
        Worksheet destinationSheet = destinationWorkbook.getWorksheets().get(0);

        // 4️⃣ Copy the range – the pivot table stays intact
        destinationSheet.getCells().copy(pivotRange,
                destinationSheet.getCells().createRange("A1"));

        // 5️⃣ Save the new workbook
        destinationWorkbook.save("YOUR_DIRECTORY/copy-pivot.xlsx");

        System.out.println("Pivot table successfully copied to copy-pivot.xlsx");
    }
}
```

> **Note:** Если ваша сводная таблица охватывает более одного листа, повторите шаг копирования для каждого нужного листа или используйте `Workbook.copy` для клонирования целых листов.

## Часто задаваемые вопросы и особые случаи

### Что делать, если в исходной книге несколько листов?

Можно пройтись в цикле по `sourceWorkbook.getWorksheets()` и копировать каждый нужный диапазон. Только будьте внимательны, чтобы сохранять одинаковые имена листов в книге‑назначении, если требуется сохранить ссылки.

### Сохраняет ли скопированная сводная таблица свой источник данных?

Да. Aspose.Cells копирует кэш сводной таблицы вместе с диапазоном, поэтому книга‑назначение по‑прежнему указывает на оригинальный источник данных внутри того же файла. Если позже переместить данные на другой лист, возможно, понадобится вручную обновить сводную таблицу.

### Как скопировать сводную таблицу, использующую внешний источник данных?

Когда источник данных сводной таблицы находится во внешнем файле, сначала нужно встроить эти данные в книгу‑назначение (например, скопировать диапазон исходных данных), а затем копировать сводную таблицу. Иначе появятся ошибки «#REF!».

### Можно ли скопировать сводную таблицу без окружающих данных?

Конечно. Просто задайте `pivotRange` так, чтобы он охватывал только ячейки сводной таблицы (обычно верхний‑левый угол плюс область данных). Также можно программно получить точный диапазон через `sourceSheet.getPivotTables().get(0).getPivotTableArea()`.

## Советы для реальных проектов

* **Пакетная обработка:** Если нужно дублировать десятки книг, вынесите код выше в отдельный метод и вызывайте его в цикле, проходящем по каталогу.
* **Производительность:** Для больших файлов переиспользуйте один экземпляр `Workbook` и вызывайте `Workbook.calculateFormula()` только после завершения всех копирований.
* **Обработка ошибок:** Оберните логику копирования в блоки `try‑catch` и логируйте `Exception.getMessage()`; Aspose бросает `CellsException` при неверных диапазонах.

## Заключение

Мы только что рассмотрели **how to copy range** в Java с помощью Aspose.Cells, показав, как **duplicate excel range**, **copy pivot table** и **load excel workbook** в одной аккуратной программе. Шаги просты, код полностью исполняем, а подход масштабируется от однолистового демо до корпоративных пакетных задач.

Готовы к следующему вызову? Попробуйте экспортировать скопированную сводную таблицу в PDF или программно обновить её после добавления новых данных. Оба задания опираются на ту же основу, которую мы здесь заложили, так что вы будете полностью подготовлены.

Есть вопросы или хотите поделиться своими доработками? Оставляйте комментарий ниже — приятного кодинга! 

![Diagram illustrating how a range with a pivot table is copied from one workbook to another](https://example.com/images/how-to-copy-range-diagram.png "how to copy range diagram")


## Что изучать дальше?


Следующие руководства охватывают тесно связанные темы, построенные на техниках, продемонстрированных в этом гайде. Каждый ресурс содержит полностью рабочие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы в собственных проектах.

- [How to Implement a Named Range with Workbook Scope in Aspose.Cells Java for Enhanced Excel Data Management](/cells/english/java/tables-structured-references/implement-named-range-workbook-scope-aspose-cells-java/)
- [How to Copy Multiple Columns in Excel Using Aspose.Cells Java: A Complete Guide](/cells/english/java/range-management/copy-multiple-columns-excel-aspose-cells-java/)
- [Excel Aspose Cells Dotnet Copy Range Data](/cells/hindi/net/range-management/excel-aspose-cells-dotnet-copy-range-data/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}