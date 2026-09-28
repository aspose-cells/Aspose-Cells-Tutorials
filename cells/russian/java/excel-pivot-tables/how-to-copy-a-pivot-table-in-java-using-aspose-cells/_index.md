---
category: general
date: 2026-09-27
description: Копирование сводной таблицы в Java с Aspose.Cells — пошаговое руководство,
  показывающее, как скопировать диапазон и сохранить определения сводной таблицы.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy pivot table
- how to copy pivot table
- copy range aspose cells
language: ru
lastmod: 2026-09-27
og_description: Копировать сводную таблицу в Java с помощью Aspose.Cells. Следуйте
  этому полному руководству, чтобы скопировать диапазон в Aspose.Cells и сохранить
  определения сводных таблиц без изменений.
og_image_alt: Screenshot of copy pivot table operation in Aspose.Cells Java
og_title: Копирование сводной таблицы в Java – краткое руководство Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Copy pivot table in Java with Aspose.Cells – a step‑by‑step guide that
    shows how to copy range and preserve pivot definitions.
  headline: How to copy a pivot table in Java using Aspose.Cells
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel automation
title: Как скопировать сводную таблицу в Java с помощью Aspose.Cells
url: /ru/java/excel-pivot-tables/how-to-copy-a-pivot-table-in-java-using-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как скопировать сводную таблицу в Java с помощью Aspose.Cells

Если вам нужно **скопировать сводную таблицу** из одной книги в другую, это руководство покажет, как сделать это с помощью Aspose.Cells для Java. Решение работает для любой созданной вами сводной таблицы и сохраняет её определение без ручного воссоздания.

Вы узнаете, как загрузить исходный файл, определить диапазон, содержащий сводную таблицу, скопировать этот диапазон в новую книгу и, наконец, сохранить результат. В руководстве также рассматриваются распространённые подводные камни, такие как сохранение источников данных и работа с большими книгами.

## Что понадобится

* Java 17 или новее (код также компилируется с JDK 8+)
* Aspose.Cells for Java 23.9 или новее — последняя версия предоставляет наиболее надёжную поддержку **copy range aspose cells**
* Исходный файл Excel, содержащий сводную таблицу (например, `SourceWithPivot.xlsx`)
* IDE или система сборки (Maven/Gradle), способная подключить JAR‑файл Aspose.Cells

## Шаг 1: Загрузить исходную книгу, содержащую сводную таблицу

Первое действие — открыть книгу, в которой находится сводная таблица, которую вы хотите дублировать. Загрузка файла создаёт представление в памяти всех листов, ячеек и кэшей сводных таблиц.

```java
import com.aspose.cells.*;

public class CopyPivotTable {
    public static void main(String[] args) throws Exception {
        // Load the source workbook
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/SourceWithPivot.xlsx");
        // Access the first worksheet (adjust the index if needed)
        Worksheet srcWs = srcWb.getWorksheets().get(0);
```

**Почему это важно:**  
Aspose.Cells читает всю книгу, включая скрытые листы кэша сводных таблиц. Если пропустить этот шаг, последующая операция **copy pivot table** потеряет исходный источник данных.

## Шаг 2: Создать пустую целевую книгу

Затем создайте новую книгу, в которую будет помещена скопированная сводная таблица. Начало с чистой книги избавляет от случайных перезаписей.

```java
        // Create an empty destination workbook
        Workbook destWb = new Workbook();
        Worksheet destWs = destWb.getWorksheets().get(0);
```

**Подсказка:** По умолчанию книга содержит один пустой лист, что идеально подходит для простого копирования. Если нужно скопировать в лист с определённым именем, переименуйте `destWs` с помощью `destWs.setName("TargetSheet")`.

## Шаг 3: Определить исходный диапазон, включающий сводную таблицу

Сводная таблица занимает прямоугольный блок ячеек. Необходимо указать точный диапазон; иначе будет скопированы только сырые данные. В этом примере мы считаем, что сводная таблица находится в **A1:G20**, но вы можете изменить адрес в соответствии с вашим файлом.

```java
        // Define the range that includes the pivot table
        Range srcRange = srcWs.getCells().createRange("A1:G20");
```

**Почему это работает:**  
При вызове `createRange` у коллекции `Cells` листа Aspose.Cells включает определение сводной таблицы, её кэш и любое форматирование. Это и есть ядро корректного **how to copy pivot table**.

## Шаг 4: Скопировать определённый диапазон на целевой лист

Теперь используйте метод `copy` для дублирования диапазона. Метод копирует всё, что находится внутри диапазона, включая определение сводной таблицы, формулы и стили.

```java
        // Copy the range (pivot table definition is included) to the destination sheet
        srcRange.copy(destWs.getCells().createRange("A1"));
```

**Важно:**  
Если вам нужны только данные без сводной таблицы, можно воспользоваться `srcRange.copyData`. Однако для настоящего **copy pivot table** необходимо копировать весь диапазон, как показано выше.

## Шаг 5: Сохранить целевую книгу

Наконец, запишите новую книгу на диск. Полученный файл будет содержать полностью функционирующую сводную таблицу, идентичную исходной.

```java
        // Save the destination workbook
        destWb.save("YOUR_DIRECTORY/CopyPivotResult.xlsx");
    }
}
```

Запуск программы создаёт `CopyPivotResult.xlsx` с тем же макетом сводной таблицы, фильтрами и вычислениями, что и в оригинальном файле.

## Ожидаемый результат

При открытии `CopyPivotResult.xlsx` в Excel:

* Сводная таблица появляется в **A1:G20** на первом листе.
* Все поля строк/столбцов, фильтры и поля значений сохранены.
* Обновление сводной таблицы переходит к тому же источнику данных, что и в исходной книге (если данные встроены).

## Пограничные случаи и практические советы

| Ситуация | Как решить |
|-----------|------------------|
| **Сводная таблица охватывает больше столбцов, чем ожидалось** | Используйте `srcWs.getPivotTables().get(0).getPivotTableArea()` для получения точного адреса программно. |
| **Исходная книга содержит несколько сводных таблиц** | Пройдитесь по `srcWs.getPivotTables()` и копируйте каждый диапазон отдельно, корректируя адреса назначения. |
| **Большие книги вызывают нагрузку на память** | Включите `WorkbookSettings.setMemorySetting(MemorySetting.MEMORY_PREFERENCE)` перед загрузкой исходной книги. |
| **Нужно скопировать только определение сводной таблицы, без данных** | После копирования удалите строки с исходными данными в целевой книге с помощью `destWs.getCells().deleteRows(startRow, count)`. |
| **Файл назначения должен сохранять оригинальное форматирование** | Установите `CopyOptions` с `options.setPasteType(PasteType.ALL)` для копирования с полной точностью. |

**Pro tip:** Всегда проверяйте скопированную сводную таблицу, вызывая `destWs.getPivotTables().get(0).refresh()` программно. Это гарантирует актуальность кэша, особенно когда исходные данные находятся во внешнем соединении.

## Полный исполняемый пример

Ниже представлен весь код, который можно скопировать и вставить в свою IDE. Замените `YOUR_DIRECTORY` реальным путём на вашем компьютере.

```java
import com.aspose.cells.*;

public class CopyPivotTable {
    public static void main(String[] args) throws Exception {
        // Step 1: Load the source workbook that contains the pivot table
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/SourceWithPivot.xlsx");
        Worksheet srcWs = srcWb.getWorksheets().get(0);

        // Step 2: Create an empty destination workbook
        Workbook destWb = new Workbook();
        Worksheet destWs = destWb.getWorksheets().get(0);

        // Step 3: Define the range that includes the pivot table in the source sheet
        // Adjust the address if your pivot occupies a different area
        Range srcRange = srcWs.getCells().createRange("A1:G20");

        // Step 4: Copy the defined range (pivot table definition is included) to the destination sheet
        srcRange.copy(destWs.getCells().createRange("A1"));

        // Step 5: Save the destination workbook with the copied pivot table
        destWb.save("YOUR_DIRECTORY/CopyPivotResult.xlsx");
    }
}
```

Запуск этого кода **скопирует сводную таблицу** точно так, как описано, и демонстрирует самый простой способ **copy range aspose cells** с сохранением функциональности сводной таблицы.

## Заключение

Теперь вы знаете, как **copy pivot table** в Java с помощью Aspose.Cells, от загрузки исходной книги до сохранения целевого файла. Руководство охватило основные шаги, объяснило, почему каждый из них важен, и рассмотрело типичные пограничные случаи.  

Далее вы можете изучить:

* **how to copy pivot table** между разными листами в одной книге
* Использование **copy range aspose cells** для дублирования диаграмм или условного форматирования
* Автоматизацию обновления сводных таблиц после копирования для поддержания актуальности данных

Не стесняйтесь экспериментировать с большими диапазонами, несколькими сводными таблицами или интегрировать эту логику в более крупный конвейер обработки Excel. Приятного кодинга!

## Что стоит изучить дальше?

Следующие руководства охватывают тесно связанные темы, построенные на техниках, продемонстрированных в этом руководстве. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, помогающими освоить дополнительные возможности API и исследовать альтернативные подходы к реализации в ваших проектах.

- [Копировать сводную таблицу в Java – Сохранить, экспортировать в PPTX](/cells/english/java/excel-pivot-tables/copy-pivot-table-in-java-preserve-it-export-to-pptx/)
- [Как обновить источник сводной таблицы Excel с помощью Aspose.Cells для Java&#58; Полное руководство](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [Манипуляция сводными таблицами Excel с Aspose.Cells Java&#58; Полное руководство](/cells/english/java/data-analysis/excel-pivot-table-manipulation-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}