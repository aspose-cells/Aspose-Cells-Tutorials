---
category: general
date: 2026-08-14
description: Копировать диапазон между книгами Excel с помощью Java и Aspose.Cells.
  Узнайте, как копировать книгу со сводной таблицей, экспортировать изображение в
  PowerPoint и удалять автофильтр из таблицы Excel.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy range between workbooks
- copy pivot table workbook
- export picture to powerpoint
- copy excel range to new workbook
- remove autofilter from excel table
language: ru
lastmod: 2026-08-14
og_description: Копирование диапазона между книгами в Java. В этом руководстве показано,
  как скопировать книгу со сводной таблицей, экспортировать изображение в PowerPoint
  и удалить автофильтр из таблицы Excel.
og_image_alt: Screenshot of Java code copying range between workbooks with Aspose.Cells
og_title: Копирование диапазона между рабочими книгами в Java – полный учебник по
  Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-08-14'
  description: Copy range between workbooks with Java using Aspose.Cells. Learn to
    copy pivot table workbook, export picture to PowerPoint and remove AutoFilter
    from Excel table.
  headline: Copy range between workbooks in Java – step‑by‑step guide
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel automation
- PowerPoint export
title: Копирование диапазона между рабочими книгами в Java — пошаговое руководство
url: /ru/java/range-management/copy-range-between-workbooks-in-java-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Копирование диапазона между книгами в Java – пошаговое руководство

Если вам нужно **скопировать диапазон между книгами** в Java, Aspose.Cells предоставляет чистый API, который работает с сложными объектами, такими как сводные таблицы и изображения. В этом руководстве показано, как **скопировать книгу со сводной таблицей**, **экспортировать изображение в PowerPoint** и **удалить AutoFilter из таблицы Excel**, при этом код остаётся простым для чтения и поддержки.

Вы узнаете, как:

* Загрузить исходную книгу и определить исходный диапазон.  
* Создать целевую книгу и скопировать диапазон так, чтобы сводная таблица осталась неизменной.  
* Экспортировать первое изображение на листе как редактируемый объект PowerPoint.  
* Удалить AutoFilter из первой таблицы Excel.  
* Загрузить книгу с `SmartMarkerOptions`, чтобы обрабатывать массивы JSON как значение одной ячейки.

Пример использует Aspose.Cells 23.10 для Java, но концепции применимы и к более ранним версиям.

---

## Требования

| Требование | Зачем это нужно |
|-------------|----------------|
| Java 17 или новее | Требуется последняя среда выполнения Aspose.Cells. |
| Aspose.Cells for Java (Maven artifact `com.aspose:aspose-cells`) | Предоставляет классы `Workbook`, `Worksheet`, `Range` и связанные классы, используемые в коде. |
| Исходный файл Excel (`src.xlsx`), содержащий сводную таблицу, изображение и таблицу с AutoFilter. | В руководстве эти объекты используются для демонстрации каждой функции. |

Добавьте зависимость Maven в ваш `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.10</version>
    <classifier>jdk17</classifier>
</dependency>
```

---

## Копирование диапазона между книгами – загрузка источника и назначения

Первый шаг – открыть исходную книгу, выбрать диапазон, содержащий данные, которые нужно скопировать, и создать пустую целевую книгу.

```java
import com.aspose.cells.*;

public class CopyRangeDemo {
    public static void main(String[] args) throws Exception {
        // Load the source workbook that holds the pivot table, picture, and table.
        Workbook sourceWb = new Workbook("YOUR_DIRECTORY/src.xlsx");
        Worksheet sourceWs = sourceWb.getWorksheets().get(0);

        // Define the range that includes the pivot table (A1:G20 in this example).
        Range sourceRange = sourceWs.getCells().createRange("A1:G20");

        // Create a new workbook that will receive the copied range.
        Workbook destWb = new Workbook();
        Worksheet destWs = destWb.getWorksheets().get(0);
        Range destRange = destWs.getCells().createRange("A1");
```

> **Почему это важно:** При использовании `Range.copy` Aspose.Cells копирует не только сырые значения ячеек, но и подлежащий кэш сводных таблиц, сохраняя их работоспособность в целевой книге.

---

## Копирование книги со сводной таблицей при копировании диапазона

Теперь скопируйте определённый диапазон из исходной книги в целевую. Сводная таблица сохраняется автоматически, потому что диапазон включает кэш сводных данных.

```java
        // Copy the source range to the destination range.
        destRange.copy(sourceRange);

        // Save the intermediate workbook to verify that the pivot table was copied.
        destWb.save("YOUR_DIRECTORY/destination.xlsx");
```

> **Результат:** При открытии `destination.xlsx` отображается тот же макет сводной таблицы, что и в `src.xlsx`. Дополнительный код для восстановления кэша не требуется.

---

## Экспорт изображения в PowerPoint

Aspose.Cells может пометить изображение для экспорта в редактируемый объект PowerPoint. Следующий код выбирает первое изображение на целевом листе и устанавливает флаг экспорта.

```java
        // Retrieve the first picture on the destination sheet.
        Shape picture = destWs.getPictures().get(0);

        // Instruct Aspose.Cells to export this picture as a PowerPoint object.
        picture.getPictureFormat().setExportToPptx(true);

        // Optionally, save the workbook as PPTX to see the result.
        destWb.save("YOUR_DIRECTORY/destination.pptx");
```

> **Что вы видите:** При открытии `destination.pptx` в PowerPoint изображение отображается как нативный объект, который можно редактировать, изменять размер или анимировать.

---

## Удаление AutoFilter из таблицы Excel

Если на исходном листе есть таблица с AutoFilter, её можно очистить после копирования. Ниже код получает первую таблицу и удаляет её фильтр.

```java
        // Access the first table on the destination sheet.
        Table table = destWs.getTables().get(0);

        // Remove the AutoFilter by assigning null.
        table.setAutoFilter(null);

        // Save the final workbook.
        destWb.save("YOUR_DIRECTORY/final_output.xlsx");
```

> **Эффект:** Таблица остаётся в книге, но стрелки выпадающих фильтров исчезают, предоставляя чистый вид данных.

---

## Загрузка книги с параметрами SmartMarker – обработка массивов JSON как единой ячейки

При генерации отчёта из JSON Aspose.Cells может рассматривать весь массив как значение одной ячейки. Это удобно для вставки строк JSON в шаблон без их разбивки по нескольким ячейкам.

```java
        // Configure LoadOptions to enable SmartMarker array handling.
        LoadOptions loadOptions = new LoadOptions();
        SmartMarkerOptions smOptions = new SmartMarkerOptions();
        smOptions.setArrayAsSingle(true);
        loadOptions.setSmartMarkerOptions(smOptions);

        // Load a template workbook using the configured options.
        Workbook smartMarkerWb = new Workbook("YOUR_DIRECTORY/template.xlsx", loadOptions);

        // Continue processing (e.g., populate markers) as needed.
        // ...

        // Save the processed workbook.
        smartMarkerWb.save("YOUR_DIRECTORY/template_filled.xlsx");
    }
}
```

> **Почему это может понадобиться:** Если ваш JSON‑payload содержит массив, который должен отображаться как строка JSON в одной ячейке, `setArrayAsSingle(true)` предотвращает разбиение массива Aspose.Cells на отдельные строки или столбцы.

![Копирование диапазона между книгами в Java – пример кода Aspose.Cells](copy-range-workbooks.png)

*Текст альтернативного изображения:* **Копирование диапазона между книгами в Java – пример кода Aspose.Cells** (соответствует основному ключевому слову).

---

## Ожидаемый результат

| Имя файла                | Содержимое |
|--------------------------|------------|
| `destination.xlsx`       | Скопированный диапазон с работающей сводной таблицей. |
| `destination.pptx`       | Экспортированное изображение как редактируемый объект PowerPoint. |
| `final_output.xlsx`      | Таблица без стрелок AutoFilter. |
| `template_filled.xlsx`   | Массив JSON, сохранённый как значение единой ячейки. |

Откройте каждый файл в соответствующем приложении (Excel или PowerPoint), чтобы убедиться, что операции выполнены успешно.

---

## Заключение

Теперь вы знаете, как **скопировать диапазон между книгами** в Java с помощью Aspose.Cells, сохраняя сводную таблицу, экспортируя изображение в PowerPoint и удаляя AutoFilter из таблицы Excel. Та же схема может быть расширена для копирования любого диапазона Excel в новую книгу, обработки массивов JSON через SmartMarker или цепочки дополнительных преобразований.

Следующие шаги, которые стоит изучить:

* **Копировать диапазон Excel в новую книгу** с несколькими листами.  
* Использовать **экспорт изображения в PowerPoint** для пакетного извлечения изображений.  
* Применять **удаление AutoFilter из таблицы Excel** в более крупных конвейерах отчётности.  
* Скомбинировать эти техники с Aspose.Slides для полной автоматизации перехода от Excel к PowerPoint.

Не стесняйтесь экспериментировать с различными адресами диапазонов, несколькими сводными таблицами или пользовательскими форматами изображений. API Aspose.Cells разработан для программной гибкости, поэтому вы можете адаптировать показанные здесь шаблоны под любые корпоративные сценарии автоматизации Excel.

## Что вам стоит изучить дальше?

Следующие руководства охватывают тесно связанные темы, расширяющие техники, продемонстрированные в этом руководстве. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, помогающими освоить дополнительные возможности API и исследовать альтернативные подходы в ваших проектах.

- [Копирование изображений между листами в Excel с помощью Aspose.Cells для Java: Полное руководство](/cells/english/java/images-shapes/copy-images-between-sheets-excel-aspose-cells-java/)
- [Копирование настроек разметки страницы между листами в Excel с помощью Aspose.Cells Java](/cells/english/java/headers-footers/copy-page-setup-excel-aspose-cells-java/)
- [Копирование листов Excel между книгами](/cells/english/net/excel-copy-worksheet/excel-copy-worksheets-between-workbooks/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}