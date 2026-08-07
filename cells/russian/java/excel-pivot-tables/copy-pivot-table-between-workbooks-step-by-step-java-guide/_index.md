---
category: general
date: 2026-07-14
description: Копировать сводную таблицу между рабочими книгами с помощью Java. Узнайте,
  как копировать сводную таблицу, копировать диапазон Excel и экспортировать сводную
  таблицу за несколько минут.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy pivot table
- how to copy pivot
- copy excel range
- copy range between workbooks
- export pivot table
language: ru
lastmod: 2026-07-14
og_description: Быстро копировать сводную таблицу в Java. Это руководство показывает,
  как копировать сводную таблицу, копировать диапазон Excel и экспортировать сводную
  таблицу с помощью Aspose.Cells.
og_image_alt: Diagram illustrating copy pivot table process between two Excel workbooks
og_title: Копирование сводной таблицы между книгами – учебник по автоматизации на
  Java
schemas:
- author: Aspose
  dateModified: '2026-07-14'
  description: Copy pivot table between workbooks using Java. Learn how to copy pivot,
    copy Excel range, and export pivot table in minutes.
  headline: Copy Pivot Table Between Workbooks – Step‑by‑Step Java Guide
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel Automation
title: Копирование сводной таблицы между рабочими книгами — пошаговое руководство
  на Java
url: /ru/java/excel-pivot-tables/copy-pivot-table-between-workbooks-step-by-step-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Копировать сводную таблицу между рабочими книгами – Полный учебник Java

Когда‑нибудь вам нужно было **copy pivot table** из одной рабочей книги в другую и вы задавались вопросом, почему обычные приёмы копирования‑вставки ломают макет? Вы не одиноки. Во многих конвейерах отчётности сводная таблица находится в мастер‑файле, но последующие процессы требуют лёгкую копию.  

В этом руководстве мы пройдём чистый программный способ дублирования сводной таблицы — без ручных манипуляций. К концу вы узнаете **how to copy pivot**, как **copy Excel range** безопасно, и даже как **export pivot table** в новый файл, используя Aspose.Cells for Java.

## Что вы построите

- Загрузить исходную рабочую книгу, которая уже содержит сводную таблицу.  
- Создать (или открыть) целевую рабочую книгу.  
- Определить точный диапазон, в котором находится сводная таблица.  
- Скопировать этот диапазон — включая определение сводной таблицы — в новую рабочую книгу.  
- Сохранить результат, чтобы другие приложения могли открыть его без потери вычислений.

## Предварительные требования

- Java 17 или новее (код работает на Java 8+, но более новые JDK обеспечивают лучшую производительность).  
- Aspose.Cells for Java 23.9 или новее — добавьте зависимость из Maven Central.  
- Два файла Excel: `SourceWithPivot.xlsx` (содержит сводную таблицу) и пустой шаблон для копии.  

Если вы новичок в Aspose.Cells, библиотека абстрагирует детали низкоуровневого OOXML, позволяя работать с листами как с обычными объектами Java.

## Шаг 1: Настройте ваш проект

Сначала добавьте артефакт Aspose.Cells Maven в ваш `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.9</version>
    <classifier>jdk17</classifier> <!-- adjust if you use a different JDK -->
</dependency>
```

Или для Gradle:

```gradle
implementation 'com.aspose:aspose-cells:23.9:jdk17'
```

> **Pro tip:** Если вы используете IDE, например IntelliJ, позвольте ей автоматически импортировать библиотеку; это экономит массу ввода.

## Шаг 2: Загрузите исходную рабочую книгу

Нужен экземпляр `Workbook`, указывающий на файл, содержащий сводную таблицу. Конструктор читает весь файл в память, поэтому вы можете работать с ним офлайн.

```java
import com.aspose.cells.*;

public class PivotCopyDemo {
    public static void main(String[] args) throws Exception {

        // Load the source workbook that contains the pivot table
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/SourceWithPivot.xlsx");
```

Зачем загружать её сначала? Потому что кэш сводной таблицы, список полей и макет хранятся внутри листа. Загрузка рабочей книги в память гарантирует, что мы копируем *определение*, а не только отрисованные значения.

## Шаг 3: Создайте или откройте целевую рабочую книгу

У вас есть два варианта: начать с совершенно новой рабочей книги или открыть существующий шаблон. Здесь мы создадим пустую, что является наиболее распространённым сценарием, когда нужна чистая копия.

```java
        // Create an empty destination workbook (or open an existing one)
        Workbook destinationWorkbook = new Workbook(); // blank workbook with a default sheet
```

Если позже вы решите копировать в конкретный лист, просто замените `getWorksheets().get(0)` на нужный индекс или имя.

## Шаг 4: Определите точный диапазон, содержащий сводную таблицу

Сводная таблица обычно занимает прямоугольный блок. Самый надёжный подход — явно указать ячейки верхнего‑левого и нижнего‑правого угла. В нашем примере сводная таблица находится от **A1** до **H30**.

```java
        // Define the range in the source sheet that includes the pivot table
        Range sourceRange = sourceWorkbook.getWorksheets()
                                          .get(0)                     // first worksheet
                                          .getCells()
                                          .createRange("A1:H30");
```

> **Почему не использовать `copyRows`?**  
> `copyRows` копирует сырые значения ячеек, но отбрасывает базовый кэш сводной таблицы. Копируя весь диапазон, Aspose.Cells сохраняет метаданные сводной таблицы, позволяя получателю сохранять полную интерактивность.

## Шаг 5: Скопируйте диапазон (включая сводную таблицу) в целевую книгу

Теперь происходит магия. Метод `copy` клонирует всё — значения, формулы, форматы и сам объект сводной таблицы — в целевое место.

```java
        // Copy the defined range (with the pivot table) to the destination sheet
        sourceRange.copy(destinationWorkbook.getWorksheets()
                                            .get(0)               // destination sheet
                                            .getCells()
                                            .createRange("A1"));
```

Если вам нужно вставить в другую ячейку, просто измените `"A1"` на `"C5"` или любой другой адрес. Метод автоматически корректирует внутренние ссылки, чтобы сводная таблица продолжала работать.

## Шаг 6: Сохраните целевую рабочую книгу

Наконец, запишите новую рабочую книгу на диск. Полученный файл можно открыть в Excel, LibreOffice или любом другом просмотрщике таблиц, и сводная таблица будет вести себя точно так же, как в исходнике.

```java
        // Save the destination workbook with the copied pivot table
        destinationWorkbook.save("YOUR_DIRECTORY/CopyPivotResult.xlsx");
    }
}
```

### Ожидаемый результат

- `CopyPivotResult.xlsx` открывается с полностью функционирующей сводной таблицей, идентичной оригиналу.  
- Все срезы, фильтры и вычисляемые поля остаются нетронутыми.  
- Нет потери данных — значения вычисляются «на лету», когда вы обновляете сводную таблицу.

## Общие варианты и граничные случаи

| Ситуация | Что изменить |
|-----------|----------------|
| **Copy into an existing workbook** | Загрузите целевую рабочую книгу вместо создания новой: `new Workbook("ExistingFile.xlsx")`. |
| **Pivot spans an unknown size** | Используйте `Worksheet.getPivotTables().get(0).getPivotTableRange()` для программного получения точного адреса. |
| **Preserve data connections** | После копирования вызовите `destinationWorkbook.getWorksheets().get(0).getPivotTables().get(0).setRefreshOnLoad(true);`, чтобы сохранить внешние ссылки на данные. |
| **Export pivot table as CSV** | После копирования вы можете вызвать `destinationWorkbook.save("PivotExport.csv", SaveFormat.CSV);` — это сохраняет только плоские значения сводной таблицы. |

> **Осторожно:** Когда исходная и целевая рабочие книги используют разные региональные настройки, форматы чисел могут измениться. Явно задайте `setLocale` рабочей книги, если нужна согласованность.

## Полный рабочий пример (все импорты включены)

```java
import com.aspose.cells.*;

public class CopyPivotTableExample {
    public static void main(String[] args) throws Exception {

        // 1️⃣ Load source workbook containing the pivot
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/SourceWithPivot.xlsx");

        // 2️⃣ Create (or open) destination workbook
        Workbook destinationWorkbook = new Workbook(); // blank workbook

        // 3️⃣ Identify the range that encloses the pivot table
        //    If you don't know the range, you can retrieve it via:
        //    PivotTable pt = sourceWorkbook.getWorksheets().get(0).getPivotTables().get(0);
        //    String address = pt.getPivotTableRange().getRefersTo();
        Range sourceRange = sourceWorkbook.getWorksheets()
                                          .get(0)
                                          .getCells()
                                          .createRange("A1:H30");

        // 4️⃣ Copy the range (pivot included) to the destination sheet
        sourceRange.copy(destinationWorkbook.getWorksheets()
                                            .get(0)
                                            .getCells()
                                            .createRange("A1"));

        // 5️⃣ Persist the result
        destinationWorkbook.save("YOUR_DIRECTORY/CopyPivotResult.xlsx");

        System.out.println("Pivot table copied successfully!");
    }
}
```

Запустите программу, откройте `CopyPivotResult.xlsx`, и вы увидите точно такую же сводную таблицу, с которой начали — готовую к дальнейшему анализу или распространению.

## Итоги

Мы только что продемонстрировали **how to copy pivot** из одной рабочей книги в другую с помощью Aspose.Cells for Java. Шаги охватывали загрузку источника, определение точного **copy Excel range**, выполнение копирования и, наконец, **export pivot table** в новый файл. Обрабатывая диапазон, а не отдельные ячейки, мы гарантируем, что внутренний кэш сводной таблицы переезжает вместе с ней, сохраняя динамичность отчёта.

## Что изучить дальше

- **Automate refresh**: Запланируйте операцию копирования с помощью Quartz‑задачи, чтобы ваши последующие файлы оставались актуальными.  
- **Copy multiple pivots**: Пройдитесь в цикле по `sourceWorkbook.getWorksheets().get(0).getPivotTables()` и скопируйте каждую в отдельный лист.  
- **Apply styling**: Используйте объекты `Style` для согласования шрифтов и цветов в целевой рабочей книге.  

Если у вас есть вопросы по работе с большими рабочими книгами или сохранению внешних источников данных, оставьте комментарий ниже. Счастливого кодинга и наслаждайтесь свободой программной автоматизации Excel!

## Что вам стоит изучить дальше?

Следующие учебники охватывают тесно связанные темы, построенные на техниках, продемонстрированных в этом руководстве. Каждый ресурс включает полные рабочие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы к реализации в ваших проектах.

- [Манипулирование сводными таблицами Excel с Aspose.Cells Java: Полное руководство](/cells/english/java/data-analysis/excel-pivot-table-manipulation-aspose-cells-java/)
- [Как обновить источник сводной таблицы Excel с Aspose.Cells for Java: Полное руководство](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [Автоматизация стилизации и сохранения сводных таблиц Excel с Aspose.Cells for Java: Полное руководство](/cells/english/java/data-analysis/excel-pivot-table-styling-saving-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}