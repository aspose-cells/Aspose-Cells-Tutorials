---
category: general
date: 2026-07-16
description: Установите пользовательский разделитель ячеек при экспорте таблицы Excel
  в TXT с помощью Aspose.Cells. Узнайте, как экспортировать формулы Excel в текст
  и сохранить лист как файл txt.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- set custom cell separator
- export excel table to txt
- export excel formulas to text
- save worksheet as txt file
- export excel data as plain text
language: ru
lastmod: 2026-07-16
og_description: Установка пользовательского разделителя ячеек в Aspose.Cells позволяет
  экспортировать таблицу Excel в TXT с точным форматированием. Экспортируйте формулы
  Excel в текст и легко сохраняйте лист как файл txt.
og_image_alt: Screenshot showing set custom cell separator option in Aspose.Cells
  export settings
og_title: Задать пользовательский разделитель ячеек – Экспорт таблицы Excel в TXT
schemas:
- author: Aspose
  dateModified: '2026-07-16'
  description: Set custom cell separator when exporting Excel table to TXT using Aspose.Cells.
    Learn how to export Excel formulas to text and save worksheet as txt file.
  headline: Set Custom Cell Separator – Export Excel Table to TXT
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel Export
title: Задать пользовательский разделитель ячеек – Экспорт таблицы Excel в TXT
url: /ru/java/excel-import-export/set-custom-cell-separator-export-excel-table-to-txt/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Установить пользовательский разделитель ячеек – Экспорт таблицы Excel в TXT

Установка пользовательского разделителя ячеек — это секретный ингредиент, который вам нужен, когда требуется аккуратный текстовый дамп из листа Excel. Когда‑нибудь задумывались, как **export excel table to txt** без получения путаницы из запятых и переводов строк? В этом руководстве мы пройдем весь процесс с использованием Aspose.Cells for Java, от загрузки рабочей книги до **save worksheet as txt file** с выбранным вами разделителем.

## Что вы узнаете

- Как **set custom cell separator** для экспорта текста.
- Точные шаги для **export excel formulas to text**, чтобы экспортировались вычисленные значения.
- Способы **export excel data as plain text**, сохраняя макет.
- Полный готовый к запуску пример кода, который вы можете скопировать и вставить в свой проект.

К концу этого руководства вы сможете взять любую рабочую книгу Excel, выбрать вертикальную черту (`|`), табуляцию (`\t`) или любой другой символ, и создать чистый файл с разделителями, который будет удобен для последующих систем.

### Предварительные требования

- Установлен Java 8 или новее.
- Maven (или любой другой инструмент сборки) для получения библиотеки Aspose.Cells for Java.
- Пример рабочей книги (`TableDemo.xlsx`), содержащей таблицу с формулами.

Если всё готово, приступаем — без лишних деталей, только практические шаги.

## Шаг 1: Добавьте Aspose.Cells в ваш проект

Прежде чем вы сможете **set custom cell separator**, вам нужен JAR Aspose.Cells в classpath. Самый простой способ — через Maven:

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version> <!-- Check Maven Central for the latest version -->
</dependency>
```

Если вы предпочитаете Gradle, замените XML на эквивалент `implementation 'com.aspose:aspose-cells:24.10'`. После разрешения зависимости вы готовы писать Java‑код, работающий с файлами Excel.

## Шаг 2: Загрузите рабочую книгу – Подготовка к экспорту таблицы Excel в TXT

Первая реальная строка кода всегда одинаковая: открыть рабочую книгу, содержащую таблицу, которую нужно экспортировать.

```java
import com.aspose.cells.*;

public class ExportTableWithOptions {
    public static void main(String[] args) throws Exception {
        // Load the workbook containing the table
        Workbook workbook = new Workbook("YOUR_DIRECTORY/TableDemo.xlsx");
        Worksheet worksheet = workbook.getWorksheets().get(0);
```

Здесь мы получаем первый лист (`get(0)`). Если ваши данные находятся на другом листе, просто измените индекс или используйте `get("SheetName")`. Эта часть важна для **export excel table to txt**, так как экспортёр работает на уровне листа.

## Шаг 3: Установить пользовательский разделитель ячеек – Ядро экспорта

Теперь наступает звезда шоу: настройка `ExportTableOptions`. Этот объект позволяет точно определить, как каждая ячейка будет выглядеть в итоговом текстовом файле.

```java
        // Define how the table should be exported
        ExportTableOptions exportTableOptions = new ExportTableOptions();

        // 1️⃣ Export cell contents as plain strings (no rich formatting)
        exportTableOptions.setExportAsString(true);

        // 2️⃣ Include the evaluated formula result, not the formula itself
        exportTableOptions.setFormulaValueInCell(true);

        // 3️⃣ Set the custom separator – this is where we set custom cell separator
        exportTableOptions.setCellValueSeparator("|"); // you can use any char you like
```

Зачем мы **set custom cell separator**? Потому что разделителем по умолчанию является табуляция, которая может конфликтовать с данными, уже содержащими табы. Выбрав вертикальную черту (`|`) или точку с запятой, вы гарантируете, что каждый столбец останется отдельным при чтении файла последующим парсером.

### Export Excel Formulas to Text

Строка `setFormulaValueInCell(true)` указывает Aspose.Cells записывать **export excel formulas to text** как *результат* формулы, а не саму строку формулы. Если бы вы её опустили, ячейка с `=SUM(A1:A5)` отобразилась бы как `=SUM(A1:A5)` в TXT, что редко бывает желаемым.

## Шаг 4: Привязать параметры экспорта к параметрам сохранения TXT

Теперь мы привязываем эти параметры таблицы к общей конфигурации экспорта в TXT.

```java
        // Attach the table export options to TXT save options
        TxtSaveOptions txtSaveOptions = new TxtSaveOptions();
        txtSaveOptions.setExportTableOptions(exportTableOptions);
```

`TxtSaveOptions` — это общий объект, который управляет тем, как записывается весь лист. Подключив `exportTableOptions`, вы гарантируете, что каждая таблица на листе соблюдает правило **set custom cell separator**.

## Шаг 5: Сохранить лист как TXT файл – Завершение экспорта

Наконец, сохраняем файл на диск.

```java
        // Save the worksheet as a TXT file using the configured options
        workbook.save("YOUR_DIRECTORY/TableExported.txt", txtSaveOptions);
    }
}
```

Запуск этой программы создаст `TableExported.txt`. Каждая строка исходной таблицы Excel теперь будет представлена как строка значений, разделённых вертикальной чертой, например:

```
Name|Quantity|Price|Total
Apple|10|0.50|5.00
Banana|5|0.30|1.50
```

Обратите внимание, что формула в столбце **Total** была вычислена перед записью — благодаря `setFormulaValueInCell(true)`. Это суть **export excel data as plain text**, сохраняющая вычисленные результаты.

## Шаг 6: Проверка результата – Всё ли выглядит правильно?

Откройте сгенерированный `TableExported.txt` в любом текстовом редакторе. Вы должны увидеть:

- Одна строка на каждую строку Excel.
- Столбцы разделены символом вертикальной черты, установленным через `setCellValueSeparator`.
- Нет лишних запятых или табов, если только они не были частью исходных значений ячеек.
- Результаты формул, а не сами формулы.

Если вы обнаружите неожиданные символы, перепроверьте выбранный разделитель. Некоторые символы (например, вертикальная черта) безопасны для большинства парсеров в стиле CSV, но если ваши данные уже содержат такие символы, рассмотрите другой разделитель, например `~` или табуляцию (`\t`).

## Советы, граничные случаи и лучшие практики – Export Excel Data as Plain Text

| Ситуация | Что делать |
|-----------|------------|
| **Данные уже содержат выбранный разделитель** | Switch to a less common character (`^`, `~`, or Unicode non‑printing chars). |
| **Необходима кодировка UTF‑8** |  |

## Что вам стоит изучить дальше?

Следующие руководства охватывают тесно связанные темы, построенные на техниках, продемонстрированных в этом руководстве. Каждый ресурс включает полные работающие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы к реализации в ваших проектах.

- [Сохранить Excel как текстовый файл с пользовательским разделителем с помощью Aspose.Cells](/cells/english/net/workbook-operations/save-excel-text-custom-separator-aspose-cells-net/)
- [Сохранить Excel текст с пользовательским разделителем Aspose Cells Net](/cells/german/net/workbook-operations/save-excel-text-custom-separator-aspose-cells-net/)
- [Сохранить Excel текст с пользовательским разделителем Aspose Cells Net](/cells/french/net/workbook-operations/save-excel-text-custom-separator-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}