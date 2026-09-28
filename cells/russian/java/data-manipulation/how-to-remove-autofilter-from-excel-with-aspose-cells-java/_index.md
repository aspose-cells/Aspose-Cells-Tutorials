---
category: general
date: 2026-09-27
description: Узнайте, как удалить автофильтр из Excel с помощью Aspose.Cells для Java.
  Пошаговое руководство по очистке автофильтра в рабочей книге, удалению фильтра таблицы
  Excel и сохранению файла.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- remove autofilter from excel
- remove excel table filter
- remove filter from excel table
- clear autofilter in workbook
language: ru
lastmod: 2026-09-27
og_description: Удалите автофильтр из Excel с помощью Aspose.Cells для Java. Этот
  учебник показывает, как очистить автофильтр в рабочей книге, удалить фильтр таблицы
  Excel и сохранить обновлённый файл.
og_image_alt: Screenshot of an Excel worksheet after remove autofilter from excel
  using Java
og_title: Удаление автофильтра из Excel с помощью Aspose.Cells Java – полное руководство
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Learn how to remove autofilter from Excel using Aspose.Cells for Java.
    Step‑by‑step guide to clear autofilter in workbook, remove excel table filter
    and save the file.
  headline: How to remove autofilter from Excel with Aspose.Cells Java
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel
- AutoFilter
title: Как удалить автофильтр из Excel с помощью Aspose.Cells Java
url: /ru/java/data-manipulation/how-to-remove-autofilter-from-excel-with-aspose-cells-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как удалить автофильтр из Excel с помощью Aspose.Cells Java

Если вам нужно удалить автофильтр из Excel, это руководство покажет точные шаги, которые можно выполнить с Aspose.Cells для Java. Вы увидите, как очистить автофильтр в рабочей книге, удалить фильтр, прикреплённый к таблице Excel, и сохранить результат без потери данных.

Работа с Excel программно часто подразумевает обработку таблиц, которые уже содержат фильтры. Удаление этих фильтров предотвращает случайное скрытие данных при последующей обработке рабочей книги. В этом учебнике рассматривается всё необходимое: требуемые библиотеки, объяснение кода, обработка граничных случаев и проверка конечного файла.

## Предварительные требования

Прежде чем начать, убедитесь, что у вас есть:

* Java Development Kit 8 или новее.
* Maven или Gradle для управления зависимостями (в примере используется Maven).
* Aspose.Cells for Java 23.8 или новее – вы можете получить бесплатную временную лицензию на сайте Aspose.
* Пример рабочей книги (`TableWithFilter.xlsx`), содержащей таблицу с применённым автофильтром.

## Шаг 1: Настройка проекта Maven

Создайте файл `pom.xml` (или добавьте в существующий проект) и включите зависимость Aspose.Cells:

```xml
<project>
    <modelVersion>4.0.0</modelVersion>
    <groupId>com.example</groupId>
    <artifactId>ExcelFilterRemoval</artifactId>
    <version>1.0.0</version>
    <dependencies>
        <dependency>
            <groupId>com.aspose</groupId>
            <artifactId>aspose-cells</artifactId>
            <version>23.8</version>
        </dependency>
    </dependencies>
</project>
```

Добавление зависимости гарантирует, что классы `com.aspose.cells.*` будут доступны во время компиляции. После сохранения файла выполните `mvn clean install`, чтобы загрузить библиотеку.

## Шаг 2: Загрузка рабочей книги, содержащей отфильтрованную таблицу

Первая строка кода создаёт экземпляр `Workbook`, указывающий на исходный файл. Загрузка рабочей книги в память требуется перед тем, как вы сможете взаимодействовать с объектами листов.

```java
import com.aspose.cells.*;

public class RemoveAutoFilter {
    public static void main(String[] args) throws Exception {
        // Load the workbook that contains a table with an AutoFilter
        Workbook workbook = new Workbook("YOUR_DIRECTORY/TableWithFilter.xlsx");
```

Если файл не существует, Aspose.Cells бросит `FileNotFoundException`. Проверьте путь и имя файла перед запуском программы.

## Шаг 3: Доступ к листу, содержащему таблицу

Большинство рабочих книг имеют лист по умолчанию с индексом 0. Вы также можете получить лист по имени, если в книге несколько листов.

```java
        // Access the first worksheet (where the table resides)
        Worksheet worksheet = workbook.getWorksheets().get(0);
```

Получение правильного листа важно, потому что `removeAutoFilter` работает с `ListObject` (таблицей), находящейся внутри конкретного листа.

## Шаг 4: Поиск ListObject (таблицы Excel) и удаление её фильтра

`ListObject` представляет таблицу Excel. Метод `removeAutoFilter` удаляет UI‑элемент автофильтра, прикреплённый к этой таблице. Если у таблицы нет фильтра, метод ничего не делает, что делает его безопасным при повторных запусках.

```java
        // Retrieve the first ListObject (table) from the worksheet
        ListObject table = worksheet.getListObjects().get(0);

        // Remove the AutoFilter element from the table
        table.removeAutoFilter();
```

**Почему этот шаг важен:**  
* `removeAutoFilter` очищает стрелки фильтра и любые скрытые строки, вызванные фильтром.  
* Исходные данные остаются неизменными, поэтому вы всё ещё можете читать или изменять строки программно.  
* Если позже понадобится снова применить фильтр, можно вызвать `table.setAutoFilter()`.

### Обработка нескольких таблиц

Если на листе более одной таблицы, пройдитесь по коллекции:

```java
        for (int i = 0; i < worksheet.getListObjects().getCount(); i++) {
            worksheet.getListObjects().get(i).removeAutoFilter();
        }
```

Этот цикл гарантирует, что **remove excel table filter** будет применён к каждой таблице, предотвращая скрытые строки в больших рабочих книгах.

## Шаг 5: Сохранение рабочей книги без автофильтра

После очистки фильтра запишите рабочую книгу в новый файл. Метод `save` поддерживает множество форматов; в примере сохраняется файл с расширением `.xlsx`.

```java
        // Save the modified workbook without the AutoFilter
        workbook.save("YOUR_DIRECTORY/TableNoFilter.xlsx");
    }
}
```

Сохранение создаёт чистую копию (`TableNoFilter.xlsx`), в которой больше нет стрелок фильтра. Откройте файл в Excel, чтобы убедиться, что **remove filter from excel table** выполнен успешно.

## Полный, готовый к запуску пример

Объединив все шаги, получаем самостоятельную программу, которую можно скомпилировать и запустить:

```java
import com.aspose.cells.*;

public class RemoveAutoFilter {
    public static void main(String[] args) throws Exception {
        // 1. Load the workbook containing a filtered table
        Workbook workbook = new Workbook("YOUR_DIRECTORY/TableWithFilter.xlsx");

        // 2. Get the first worksheet (adjust index if needed)
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // 3. Remove AutoFilter from each table on the sheet
        for (int i = 0; i < worksheet.getListObjects().getCount(); i++) {
            worksheet.getListObjects().get(i).removeAutoFilter();
        }

        // 4. Save the workbook – the AutoFilter is now cleared
        workbook.save("YOUR_DIRECTORY/TableNoFilter.xlsx");
    }
}
```

**Ожидаемый результат:**  
При открытии `TableNoFilter.xlsx` в Microsoft Excel стрелки выпадающих списков фильтра исчезнут, и все строки будут видимы. Данные не потеряны, и рабочая книга ведёт себя так, как будто автофильтра никогда не было.

## Часто задаваемые вопросы и обработка граничных случаев

| Question | Answer |
|----------|--------|
| *What if the workbook has no tables?* | The `getListObjects().getCount()` call returns 0, so the loop exits without error. |
| *Can I remove the filter from a specific column only?* | Aspose.Cells does not expose column‑level removal; you must clear the entire table’s AutoFilter. |
| *Does `removeAutoFilter` affect conditional formatting?* | No. Conditional formatting remains intact because the method only touches the filter UI. |
| *Is the operation fast for large workbooks?* | Yes. Removing the filter is an O(1) operation per table; the dominant cost is loading and saving the workbook. |
| *Do I need a license for production use?* | A valid Aspose.Cells license removes evaluation watermarks and enables full performance. |

## Pro tips

* **License early** – call `License license = new License(); license.setLicense("Aspose.Total.Java.lic");` before loading the workbook to avoid the evaluation banner.
* **Batch processing** – when processing dozens of files, reuse a single `Workbook` instance by loading, clearing, saving, and then calling `workbook.dispose();` to free memory.
* **Verification script** – after saving, you can programmatically confirm that the filter is gone:

```java
Workbook check = new Workbook("YOUR_DIRECTORY/TableNoFilter.xlsx");
boolean hasFilter = check.getWorksheets().get(0).getListObjects().get(0).isAutoFilterEnabled();
System.out.println("Filter present? " + hasFilter); // should print false
```

## Заключение

Теперь вы знаете, как **remove autofilter from Excel** с помощью Aspose.Cells for Java, как **remove excel table filter** для каждой таблицы на листе и как **clear autofilter in workbook** перед сохранением файла. Полный пример кода демонстрирует надёжный шаблон, который можно встроить в более крупные конвейеры автоматизации, инструменты миграции данных или сервисы отчётности.

Дальнейшие шаги, которые вы можете изучить:

* Добавление проверки данных после очистки фильтра.
* Экспорт очищенной рабочей книги в CSV или PDF.
* Использование Aspose.Cells для программного применения нового фильтра на основе бизнес‑правил.

Не стесняйтесь экспериментировать с различными структурами рабочих книг и делиться своими находками в комментариях. Приятного кодинга!

## Что вам стоит изучить дальше?

Следующие учебники охватывают тесно связанные темы, которые развивают техники, продемонстрированные в этом руководстве. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы в ваших проектах.

- [Clear filter UI in Excel with C# – Remove AutoFilter Button](/cells/english/net/excel-autofilter-validation/clear-filter-ui-in-excel-with-c-remove-autofilter-button/)
- [Implement 'Ends With' Autofilter in Excel Using Aspose.Cells for Java: A Comprehensive Guide](/cells/english/java/data-analysis/aspose-cells-java-autofilter-ends-with/)
- [Implement AutoFilter 'Begins With' in Excel using Aspose.Cells Java](/cells/english/java/data-analysis/implement-autofilter-begins-with-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}