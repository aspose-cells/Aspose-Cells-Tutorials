---
category: general
date: 2026-10-01
description: Узнайте, как копировать сводные таблицы между рабочими книгами Excel
  с помощью Java. Это пошаговое руководство также показывает, как копировать диапазоны
  между книгами и безопасно дублировать диапазоны Excel.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy pivot
- copy range between workbooks
- how to copy excel
- duplicate excel range
- copy range to workbook
language: ru
lastmod: 2026-10-01
og_description: Как копировать сводные таблицы между рабочими книгами Excel с помощью
  Java. Следуйте этому руководству, чтобы копировать диапазон в книгу, дублировать
  диапазоны Excel и сохранять данные сводных таблиц.
og_image_alt: Screenshot of Java code that copies a pivot table from one Excel workbook
  to another
og_title: Как копировать сводные таблицы между рабочими книгами Excel в Java — полное
  руководство
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Learn how to copy pivot tables between Excel workbooks using Java.
    This step‑by‑step guide also shows how to copy range between workbooks and duplicate
    Excel ranges safely.
  headline: How to copy pivot tables between Excel workbooks in Java
  type: TechArticle
- description: Learn how to copy pivot tables between Excel workbooks using Java.
    This step‑by‑step guide also shows how to copy range between workbooks and duplicate
    Excel ranges safely.
  name: How to copy pivot tables between Excel workbooks in Java
  steps:
  - name: Expected output
    text: '* Console: `Pivot table copied successfully.` * `destination.xlsx` opens
      in Excel with a pivot table identical to the one in `source.xlsx`. Refreshing
      the pivot shows the same data source, proving that **how to copy pivot** works
      as intended.'
  - name: Copying multiple worksheets
    text: If your project requires copying several sheets, loop through the workbook’s
      worksheets and repeat steps 2‑4 for each sheet. The pivot in each sheet will
      be preserved independently.
  - name: Preserving external data connections
    text: Pivot tables that rely on external data sources keep the connection string
      after copying. However, the destination file must have access to the same data
      source. Verify the connection by opening the pivot and checking the **Data**
      tab.
  - name: Dealing with merged cells
    text: If the source range contains merged cells, Aspose.Cells copies the merge
      layout automatically. Still, validate the result if the destination workbook
      uses a different default column width.
  type: HowTo
tags:
- Excel
- Java
- Aspose.Cells
- Pivot table
- Data manipulation
title: Как копировать сводные таблицы между рабочими книгами Excel в Java
url: /ru/java/excel-pivot-tables/how-to-copy-pivot-tables-between-excel-workbooks-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как копировать сводные таблицы между книгами Excel в Java

Если вам нужно **how to copy pivot** таблицы из одного файла Excel в другой, это руководство предоставляет готовое решение. К концу первых двух предложений вы точно узнаете, какие вызовы API сохраняют определение сводной таблицы при копировании диапазона данных.

Вы также узнаете, как **copy range between workbooks**, **duplicate Excel range** объекты, и безопасно **copy range to workbook** без потери формул или форматирования. Внешние скрипты не требуются — достаточно одного проекта Java, использующего Aspose.Cells for Java.

## Предварительные требования

Перед началом убедитесь, что у вас есть:

* Java Development Kit 17 или новее.
* Maven или Gradle для управления зависимостями.
* Действительная лицензия Aspose.Cells for Java (бесплатная оценочная версия подходит для тестирования).
* Два файла Excel: `source.xlsx` (содержит сводную таблицу) и пустой `destination.xlsx` (или позволить коду создать его).

## Шаг 1: Настройка проекта Maven

Создайте `pom.xml`, включающий Aspose.Cells. Эта зависимость предоставляет классы `Workbook`, `Worksheet` и `Range`, используемые в примере.

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0" 
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 
         http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>com.example</groupId>
    <artifactId>excel-pivot-copy</artifactId>
    <version>1.0.0</version>
    <properties>
        <java.version>17</java.version>
    </properties>

    <dependencies>
        <dependency>
            <groupId>com.aspose</groupId>
            <artifactId>aspose-cells</artifactId>
            <version>24.10</version> <!-- latest at time of writing -->
        </dependency>
    </dependencies>
</project>
```

> **Pro tip:** Держите версию Aspose.Cells актуальной; новые релизы добавляют лучшую поддержку сложных структур кэша сводных таблиц.

## Шаг 2: Загрузка исходной книги, содержащей сводную таблицу

Первый блок кода демонстрирует **how to copy excel** данные путем загрузки исходного файла. Конструктор `Workbook` читает весь файл в память, сохраняя все объекты листов, включая сводные таблицы.

```java
import com.aspose.cells.*;

public class PivotCopyDemo {
    public static void main(String[] args) throws Exception {
        // Load the source workbook containing the pivot table
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/source.xlsx");

        // Access the first worksheet (index 0) where the pivot resides
        Worksheet srcWs = srcWb.getWorksheets().get(0);
```

*Почему это важно:* Aspose.Cells хранит сводные таблицы как часть внутренней модели листа. Загрузка книги гарантирует, что кэш сводных таблиц будет доступен для последующего копирования.

## Шаг 3: Определение диапазона, включающего сводную таблицу

Сводная таблица может охватывать несколько строк и столбцов. В большинстве случаев можно скопировать весь используемый диапазон листа. Метод `createRange` создает объект `Range`, который будет обрабатываться операцией копирования.

```java
        // Define the range to copy – includes the pivot table and its source data
        // Adjust the address if your pivot occupies a different block
        Range srcRange = srcWs.getCells().createRange("A1:H20");
```

Если сводная таблица выходит за пределы `H20`, просто измените строку адреса. Этот шаг является ядром обработки **duplicate excel range**; объект диапазона знает о формулах, стилях и скрытых строках.

## Шаг 4: Создание новой книги, получающей скопированный диапазон

Вы можете начать с пустой книги или загрузить существующий файл назначения. Здесь мы создаём новую книгу, что является самым чистым способом **copy range to workbook**.

```java
        // Create a new workbook for the destination
        Workbook destWb = new Workbook(); // starts with one default sheet
        Worksheet destWs = destWb.getWorksheets().get(0);
```

> **Note:** Если необходимо скопировать сводную таблицу в лист с определённым именем, переименуйте `destWs` с помощью `destWs.setName("Report")` перед вставкой.

## Шаг 5: Копирование диапазона — Aspose.Cells автоматически сохраняет сводную таблицу

Метод `copy` переносит всё внутри исходного диапазона, включая определение сводной таблицы, кэш и форматирование. Дополнительный код не требуется для сохранения функциональности сводной таблицы.

```java
        // Copy the range to the destination worksheet; pivot tables are preserved automatically
        srcRange.copy(destWs.getCells().createRange("A1"));
```

*Почему это работает:* Aspose.Cells рассматривает сводную таблицу как набор скрытых ячеек и метаданных, привязанных к диапазону. При вызове `copy` библиотека копирует эти метаданные в целевую книгу.

## Шаг 6: Сохранение книги назначения

Наконец, запишите результат на диск. Сохранённый файл содержит идентичную сводную таблицу, которую можно обновлять или изменять так же, как оригинал.

```java
        // Save the destination workbook
        destWb.save("YOUR_DIRECTORY/destination.xlsx");

        System.out.println("Pivot table copied successfully.");
    }
}
```

Запуск программы выводит подтверждение и создаёт `destination.xlsx` с полностью функционирующей сводной таблицей.

## Полный, исполняемый пример

Объединив все шаги, получаем полный Java‑класс, выглядящий так:

```java
import com.aspose.cells.*;

public class PivotCopyDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load source workbook with pivot table
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/source.xlsx");
        Worksheet srcWs = srcWb.getWorksheets().get(0);

        // 2️⃣ Define the range that contains the pivot and its source data
        Range srcRange = srcWs.getCells().createRange("A1:H20");

        // 3️⃣ Prepare destination workbook (blank by default)
        Workbook destWb = new Workbook();
        Worksheet destWs = destWb.getWorksheets().get(0);

        // 4️⃣ Copy range – pivot table is kept intact
        srcRange.copy(destWs.getCells().createRange("A1"));

        // 5️⃣ Save the new file
        destWb.save("YOUR_DIRECTORY/destination.xlsx");
        System.out.println("Pivot table copied successfully.");
    }
}
```

### Ожидаемый вывод

* Консоль: `Pivot table copied successfully.`
* `destination.xlsx` открывается в Excel со сводной таблицей, идентичной той, что в `source.xlsx`. Обновление сводной таблицы показывает тот же источник данных, подтверждая, что **how to copy pivot** работает как задумано.

## Обработка распространённых вариантов

### Копирование нескольких листов

Если ваш проект требует копирования нескольких листов, пройдитесь циклом по листам книги и повторите шаги 2‑4 для каждого листа. Сводная таблица на каждом листе будет сохранена независимо.

```java
for (int i = 0; i < srcWb.getWorksheets().getCount(); i++) {
    Worksheet src = srcWb.getWorksheets().get(i);
    Worksheet dest = destWb.getWorksheets().add();
    src.getCells().copy(dest.getCells());
}
```

### Сохранение внешних соединений данных

Сводные таблицы, использующие внешние источники данных, сохраняют строку подключения после копирования. Однако файл назначения должен иметь доступ к тому же источнику данных. Проверьте соединение, открыв сводную таблицу и проверив вкладку **Data**.

### Работа со слитными ячейками

Если исходный диапазон содержит слитные ячейки, Aspose.Cells автоматически копирует их расположение. Тем не менее, проверьте результат, если в книге назначения используется другая ширина столбцов по умолчанию.

## Лучшие практики надёжного копирования

| Practice | Reason |
|----------|--------|
| Используйте точный используемый диапазон (`srcWs.getCells().getMaxDisplayRange()`) вместо жёстко заданного адреса | Гарантирует, что включены вся сводная таблица и её исходные данные. |
| Применяйте лицензию перед тяжёлыми операциями | Избавляет от водяного знака оценки и повышает производительность. |
| Обновляйте сводную таблицу после копирования (`pivotTable.refresh()`), если исходные данные изменились | Обеспечивает, что назначение отражает последние значения. |
| Пишите модульные тесты, которые открывают книгу назначения и проверяют, что `pivotTable.getPivotFields().size()` совпадает с исходной | Обнаруживает случайную потерю полей при будущих изменениях кода. |

## Заключение

Теперь вы знаете, как **how to copy pivot** таблицы между книгами Excel в Java, а также как **copy range between workbooks**, **duplicate excel range** и **copy range to workbook**, сохраняя всё форматирование и формулы. Пример использует Aspose.Cells, который абстрагирует низкоуровневую работу с XML, требуемую OpenXML SDK.

Далее изучайте связанные темы, такие как **updating pivot cache programmatically**, **exporting pivot data to CSV** или **creating pivot tables from scratch**. Каждая из них опирается на те же концепции, продемонстрированные здесь.

Удачной разработки, и не стесняйтесь экспериментировать с более крупными диапазонами, несколькими сводными таблицами или пользовательским стилем — тот же шаблон применим во всех сценариях.

## Что стоит изучить дальше?

Следующие руководства охватывают тесно связанные темы, построенные на техниках, продемонстрированных в этом руководстве. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, помогающими освоить дополнительные возможности API и исследовать альтернативные подходы к реализации в ваших проектах.

- [How to Create Pivot Tables in Excel Using Aspose.Cells for Java: A Comprehensive Guide](/cells/english/java/data-analysis/create-pivot-tables-excel-aspose-cells-java/)
- [How to Copy Multiple Columns in Excel Using Aspose.Cells Java: A Complete Guide](/cells/english/java/range-management/copy-multiple-columns-excel-aspose-cells-java/)
- [Copy Images Between Sheets in Excel Using Aspose.Cells for Java: A Comprehensive Guide](/cells/english/java/images-shapes/copy-images-between-sheets-excel-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}