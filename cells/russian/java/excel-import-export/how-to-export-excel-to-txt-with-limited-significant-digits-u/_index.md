---
category: general
date: 2026-08-17
description: Экспорт Excel в TXT с ограничением значимых цифр — узнайте, как задать
  количество цифр и преобразовать Excel в текст на Java с полным примером Aspose.Cells.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel to txt
- how to set digits
- convert excel to text
- how to limit decimals
- limit significant digits
language: ru
lastmod: 2026-08-17
og_description: Экспорт Excel в TXT с ограничением значимых цифр. Этот учебник показывает,
  как задать количество цифр и преобразовать Excel в текст с помощью Aspose.Cells
  для Java.
og_image_alt: Java code exporting Excel to TXT with 4 significant digits
og_title: Экспорт Excel в TXT с ограничением количества значимых цифр – руководство
  по Java
schemas:
- author: Aspose
  dateModified: '2026-08-17'
  description: Export Excel to TXT while limiting significant digits – learn how to
    set digits and convert Excel to text in Java with a complete Aspose.Cells example.
  headline: How to export Excel to TXT with limited significant digits using Java
  type: TechArticle
- description: Export Excel to TXT while limiting significant digits – learn how to
    set digits and convert Excel to text in Java with a complete Aspose.Cells example.
  name: How to export Excel to TXT with limited significant digits using Java
  steps:
  - name: Prerequisites
    text: '- Java 17 or later (the code compiles with Java 8 as well). - Aspose.Cells
      for Java 25.10 or newer. Download the JAR from the [Aspose website](https://products.aspose.com/cells/java)
      and add it to your project’s classpath. - An IDE or a simple text editor and
      command‑line build tool (Maven/Gradle).'
  - name: How the setting differs from “limit decimals”
    text: '- **limit decimals** (`setDecimalPlaces`) trims digits *after* the decimal
      point, regardless of the integer part. - **significant digits** (`setSignificantDigits`)
      counts digits from the first non‑zero digit, which is useful when numbers vary
      in magnitude.'
  - name: Expected output
    text: '| Cell | Original value | Exported (4 significant digits) | |------|----------------|---------------------------------|
      | A1 | 123.456789 | 123.5 |'
  - name: Exporting a whole range
    text: 'If you want to export more than one cell, simply fill the range before
      saving:'
  - name: Handling locale‑specific decimal separators
    text: 'Aspose.Cells respects the system locale when writing text. To force a dot
      (`.`) as the decimal separator, set the `TxtSaveOptions` culture:'
  - name: Overwriting existing files
    text: 'The `save` method overwrites the target file by default. If you need to
      avoid accidental data loss, check for file existence first:'
  - name: Large workbooks and memory usage
    text: 'When exporting very large worksheets, consider streaming the output:'
  - name: Next steps
    text: "- Explore other `TxtSaveOptions` properties such as `setDelimiter('\t')`
      to customize column separators. - Combine the exporter with `CsvSaveOptions`
      if you need comma‑separated values instead of plain text. - Integrate the routine
      into a web service that accepts uploaded Excel files and returns tri"
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel export
- TXT conversion
title: Как экспортировать Excel в TXT с ограниченным числом значимых цифр с помощью
  Java
url: /ru/java/excel-import-export/how-to-export-excel-to-txt-with-limited-significant-digits-u/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Экспорт Excel в TXT с ограничением значимых цифр с помощью Java

Если вам нужно **экспортировать Excel в TXT**, контролируя количество значимых цифр, это руководство предоставляет готовое решение. Вы увидите, как задать количество цифр, конвертировать Excel в текст и поддерживать чистый вывод одним изменением конфигурации.

В примере используется Aspose.Cells for Java 25.10, который вводит опцию `setSignificantDigits`. К концу урока вы сможете создать TXT‑файл, содержащий только нужные цифры, без дополнительного кода округления.

## Что вы получите

- Программное создание рабочей книги.
- Вставка числового значения в ячейку.
- Настройка параметров сохранения TXT для ограничения значимых цифр.
- Сохранение рабочей книги как обычного текстового файла.
- Понимание того, как работает настройка `significantDigits` и как адаптировать её под другие сценарии.

### Предварительные требования

- Java 17 или новее (код также компилируется на Java 8).
- Aspose.Cells for Java 25.10 или новее. Скачайте JAR с [веб‑сайта Aspose](https://products.aspose.com/cells/java) и добавьте его в classpath проекта.
- IDE или простой текстовый редактор и инструмент сборки командной строки (Maven/Gradle).

## Шаг 1: Настройка проекта и импорт Aspose.Cells

Создайте новый Java‑проект и добавьте JAR‑файл Aspose.Cells в путь сборки. Если используете Maven, добавьте следующую зависимость в `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.10</version>
    <classifier>jdk17</classifier>
</dependency>
```

> **Совет:** Используйте классификатор `jdk17` для последней версии Java runtime; это снижает риск предупреждений о совместимости.

## Шаг 2: Создание рабочей книги и запись значения

Рабочая книга представляет собой файл Excel в памяти. Вы можете добавить данные в любую ячейку с помощью метода `putValue`.

```java
import com.aspose.cells.*;

public class SignificantDigitsDemo {
    public static void main(String[] args) throws Exception {
        // Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // Put a numeric value into cell A1
        Cell cell = worksheet.getCells().get("A1");
        cell.putValue(123.456789);
```

Число `123.456789` будет исходным для нашего экспорта в TXT. По умолчанию Aspose.Cells записывает все десятичные знаки, что часто приводит к «шумным» текстовым файлам.

## Шаг 3: Настройка параметров сохранения TXT для ограничения значимых цифр

Aspose.Cells предоставляет `TxtSaveOptions` для тонкой настройки вывода в обычный текст. Метод `setSignificantDigits` указывает экспортеру, сколько цифр сохранять **в целом**, а не только после запятой.

```java
        // Configure TXT save options to keep only 4 significant digits
        TxtSaveOptions saveOptions = new TxtSaveOptions();
        saveOptions.setSignificantDigits(4); // new option in 25.10
```

Когда `significantDigits` установлен в `4`, экспортер округляет значение `123.456789` до `123.5`. Такое поведение соответствует математическому определению значимых цифр: сохраняются первые четыре значащих цифры, отличных от нуля.

### Чем настройка отличается от «ограничения десятичных знаков»

- **limit decimals** (`setDecimalPlaces`) удаляет цифры *после* запятой, независимо от целой части.
- **significant digits** (`setSignificantDigits`) считает цифры, начиная с первой значащей, что удобно, когда числа различаются по порядку величины.

Если вам нужен фиксированный набор десятичных знаков, замените строку выше на:

```java
saveOptions.setDecimalPlaces(2); // keeps two digits after the decimal point
```

## Шаг 4: Сохранение рабочей книги как TXT‑файла

Теперь запишите рабочую книгу на диск, используя сконфигурированные параметры.

```java
        // Save the workbook as a TXT file using the configured options
        workbook.save("significant_digits.txt", saveOptions);
    }
}
```

Запуск программы создаст `significant_digits.txt` в рабочем каталоге. Файл будет содержать одну строку:

```
123.5
```

### Ожидаемый вывод

| Cell | Original value | Exported (4 significant digits) |
|------|----------------|---------------------------------|
| A1   | 123.456789     | 123.5                           |

Если изменить `setSignificantDigits(4)` на `6`, вывод станет `123.457`. Поэкспериментируйте с разными значениями, чтобы увидеть, как меняется округление.

## Шаг 5: Общие варианты и граничные случаи

### Экспорт диапазона целиком

Если нужно экспортировать более одной ячейки, просто заполните диапазон перед сохранением:

```java
worksheet.getCells().get("B1").putValue(0.0012345);
worksheet.getCells().get("C1").putValue(98765.4321);
```

Тот же параметр `significantDigits` применяется к каждой числовой ячейке, обеспечивая одинаковую точность во всём файле.

### Обработка локаль‑специфичных десятичных разделителей

Aspose.Cells учитывает системную локаль при записи текста. Чтобы принудительно использовать точку (`.`) как разделитель, задайте культуру в `TxtSaveOptions`:

```java
saveOptions.setCultureInfo(java.util.Locale.US);
```

Это полезно, когда целевое приложение ожидает определённый формат, например CSV‑парсеры, принимающие только `.`.

### Перезапись существующих файлов

Метод `save` по умолчанию перезаписывает целевой файл. Если нужно избежать случайной потери данных, сначала проверьте наличие файла:

```java
java.io.File outFile = new java.io.File("significant_digits.txt");
if (outFile.exists()) {
    throw new IllegalStateException("File already exists. Choose a different name or delete the existing file.");
}
workbook.save(outFile.getPath(), saveOptions);
```

### Большие рабочие книги и использование памяти

При экспорте очень больших листов рассмотрите возможность потоковой записи вывода:

```java
saveOptions.setEnableMemorySaving(true);
```

Эта опция уменьшает потребление кучи, записывая строки по частям.

## Полный рабочий пример

Ниже приведена полная программа, которую можно скопировать, вставить и сразу запустить:

```java
import com.aspose.cells.*;

public class SignificantDigitsDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook and access the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // Step 2: Put numeric values into cells
        worksheet.getCells().get("A1").putValue(123.456789);
        worksheet.getCells().get("B1").putValue(0.0012345);
        worksheet.getCells().get("C1").putValue(98765.4321);

        // Step 3: Configure TXT save options
        TxtSaveOptions saveOptions = new TxtSaveOptions();
        saveOptions.setSignificantDigits(4);          // limit to 4 significant digits
        saveOptions.setCultureInfo(java.util.Locale.US); // enforce dot as decimal separator
        saveOptions.setEnableMemorySaving(true);      // optional for large files

        // Step 4: Save the workbook as a TXT file
        workbook.save("significant_digits.txt", saveOptions);
    }
}
```

Запуск этого кода создаст `significant_digits.txt` со следующим содержимым (колонки разделены табуляцией):

```
123.5	0.001235	98770
```

Каждое число соблюдает правило **4 значимых цифр**, демонстрируя, что настройка работает для разных порядков величины.

## Заключение

Теперь вы знаете, как **экспортировать Excel в TXT**, контролируя количество значимых цифр. Используя `TxtSaveOptions.setSignificantDigits`, вы можете **задать цифры**, **ограничить десятичные знаки** и **ограничить значимые цифры** одной поддерживаемой строкой кода. Подход работает как для отдельных ячеек, так и для диапазонов и больших книг.

### Следующие шаги

- Исследуйте другие свойства `TxtSaveOptions`, такие как `setDelimiter('\t')`, для настройки разделителей колонок.
- Сочетайте экспортёр с `CsvSaveOptions`, если нужны значения, разделённые запятыми, вместо простого текста.
- Интегрируйте процедуру в веб‑службу, принимающую загруженные Excel‑файлы и мгновенно возвращающую обрезанный TXT‑вывод.

Экспериментируйте с разными ограничениями цифр и локалями. Если столкнётесь со сценарием, где встроенные опции не покрывают особую потребность, всегда можно выполнить пост‑обработку сгенерированного TXT‑файла стандартными средствами Java I/O.

Счастливого кодинга!


## Что вам стоит изучить дальше?


Следующие уроки охватывают тесно связанные темы, расширяющие техники, продемонстрированные в этом руководстве. Каждый ресурс включает полностью рабочие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы в собственных проектах.

- [How to Convert Text to Numbers in Excel Using Aspose.Cells for Java](/cells/english/java/cell-operations/convert-text-to-numbers-excel-aspose-cells-java/)
- [How to Create and Export Excel to HTML Using Aspose.Cells Java | Workbook Operations Guide](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)
- [How to Export Custom Excel Properties to PDF Using Aspose.Cells for Java](/cells/english/java/workbook-operations/export-excel-custom-properties-pdf-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}