---
category: general
date: 2026-07-16
description: Экспорт Excel в TXT с помощью Aspose.Cells на Java. Узнайте, как установить
  значимые цифры, сохранить Excel в виде текстового файла и управлять форматом вывода.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel to txt
- how to set significant digits
- save excel as text file
- save workbook as txt
language: ru
lastmod: 2026-07-16
og_description: Экспорт Excel в TXT на Java с Aspose.Cells. Этот учебник показывает,
  как установить значимые цифры, сохранить Excel как текстовый файл и получить надёжные
  результаты.
og_image_alt: Screenshot of Java code exporting an Excel workbook to a TXT file with
  4 significant digits
og_title: Экспорт Excel в TXT на Java – пошаговое руководство
schemas:
- author: Aspose
  dateModified: '2026-07-16'
  description: Export Excel to TXT using Aspose.Cells in Java. Learn how to set significant
    digits, save Excel as text file, and control the output format.
  headline: Export Excel to TXT with Java – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Export Excel to TXT using Aspose.Cells in Java. Learn how to set significant
    digits, save Excel as text file, and control the output format.
  name: Export Excel to TXT with Java – Complete Step‑by‑Step Guide
  steps:
  - name: Prerequisites
    text: '- Java Development Kit (JDK) 8 or newer. - Maven or Gradle to manage the
      Aspose.Cells dependency (we’ll show the Maven snippet). - A basic understanding
      of Java syntax (if you’ve written a “Hello World”, you’re good).'
  - name: Understanding `setSignificantDigits`
    text: '- **Definition:** The number of digits that remain after the decimal point,
      *including* leading digits. For `123.456789` with `4` significant digits, the
      output becomes `123.5`. - **When to use:** If the downstream system expects
      a fixed precision (e.g., scientific data files), or you need to trunca'
  - name: Folder Considerations
    text: '- The `output` folder must exist, or you’ll get an `IOException`. You can
      create it programmatically:'
  - name: 1️⃣ What if I need a different delimiter?
    text: "`TxtSaveOptions` also offers `setSeparator('\t')` for tabs or `setSeparator(',')`
      for CSV‑style output. Example:"
  - name: 2️⃣ How does locale affect decimal separators?
    text: 'By default Aspose uses the system locale. If you need a period (`.`) regardless
      of locale, set:'
  - name: 3️⃣ Large worksheets – memory concerns?
    text: Aspose.Cells streams data to disk when working with worksheets larger than
      1 GB, so you usually won’t hit an `OutOfMemoryError`. Still, avoid loading massive
      sheets into memory if you only need a subset; use `Workbook.getWorksheets().get(index)`
      to target a specific sheet.
  - name: 4️⃣ Can I export only a range?
    text: Yes. Use `txtOptions.setExportRange("A1:B10")` to restrict the output to
      a specific area. This reduces file size and speeds up the export.
  - name: 5️⃣ What if I don’t have a license?
    text: The evaluation mode adds a watermark line (`"Aspose.Cells for Java Evaluation
      Version"`). For production you’ll need a license; otherwise the watermark may
      break downstream parsers.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: Экспорт Excel в TXT с помощью Java – полное пошаговое руководство
url: /ru/java/excel-import-export/export-excel-to-txt-with-java-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Экспорт Excel в TXT с помощью Java – Полное пошаговое руководство

Когда‑нибудь задавались вопросом **как экспортировать Excel в TXT** без потери числовой точности? Возможно, вам нужен простой текстовый дамп для устаревшей системы, или вы передаёте данные в научный конвейер, который ожидает определённое количество значимых цифр. В этом руководстве мы пройдём через **полный, исполняемый пример на Java**, который покажет именно это — а также **как задать значимые цифры**, **сохранить Excel как текстовый файл** и **сохранить книгу как txt** с помощью Aspose.Cells.

Мы охватим всё от настройки проекта до финального шага проверки, чтобы вы могли скопировать‑вставить код, запустить его и сразу увидеть результат. Никаких загадочных зависимостей, никаких «см. документацию»‑шорткатов — только ясное, сквозное решение.

---

## Что вы узнаете

- Как программно создать книгу (workbook) с помощью Aspose.Cells.
- Точный вызов API для **задания значимых цифр** при экспорте в TXT.
- Разницу между `TxtSaveOptions` и другими параметрами сохранения.
- Как **сохранить Excel как текстовый файл** на любой ОС (Windows, macOS, Linux).
- Распространённые подводные камни (десятичные разделители, зависящие от локали; большие листы) и как их избежать.
- Полный, готовый к запуску класс Java, который вы можете адаптировать под свои проекты.

### Предварительные требования

- Java Development Kit (JDK) 8 или новее.
- Maven или Gradle для управления зависимостью Aspose.Cells (мы покажем фрагмент Maven).
- Базовое понимание синтаксиса Java (если вы писали «Hello World», вам достаточно).

---

## Шаг 1: Настройка проекта и добавление Aspose.Cells

Сначала добавим библиотеку в сборку. Если вы используете Maven, добавьте следующее в ваш `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- Use the latest stable version -->
</dependency>
```

> **Pro tip:** Aspose предлагает бесплатную 30‑дневную оценочную лицензию. Поместите файл `Aspose.Total.lic` в корень проекта или вызовите `License.setLicense("path/to/license")` перед использованием любого API.

После того как зависимость будет разрешена, вы можете начинать кодировать. Если вы предпочитаете Gradle, эквивалент выглядит так:

```gradle
implementation 'com.aspose:aspose-cells:24.9'
```

---

## Шаг 2: Экспорт Excel в TXT – Создание книги

Теперь мы создадим новую книгу, добавим числовое значение и подготовим её к экспорту. Это суть **экспорта Excel в txt**.

```java
import com.aspose.cells.*;

public class ExportExcelToTxtDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Create a fresh workbook (in‑memory Excel file)
        Workbook workbook = new Workbook();

        // 2️⃣ Grab the first worksheet – it's created by default
        Worksheet sheet = workbook.getWorksheets().get(0);

        // 3️⃣ Put a numeric value into cell A1
        Cell cell = sheet.getCells().get("A1");
        cell.putValue(123.456789); // Example number with many decimals
```

**Почему это важно:** Создавая книгу в коде, мы избегаем скрытого форматирования, которое могло бы появиться из шаблонного файла. Метод `putValue` автоматически определяет тип данных, поэтому ячейка становится **числовой**, а не строковой.

---

## Шаг 3: Как задать значимые цифры для вывода в TXT

При экспорте в простой текст Aspose.Cells по умолчанию записывает необработанное числовое значение. Чтобы ограничить вывод, например, **4 значимыми цифрами**, необходимо настроить `TxtSaveOptions`.

```java
        // 4️⃣ Configure TXT save options – this is where we set the precision
        TxtSaveOptions txtOptions = new TxtSaveOptions();
        txtOptions.setSignificantDigits(4); // <-- controls significant digits
```

### Понимание `setSignificantDigits`

- **Определение:** Количество цифр, оставшихся после десятичной точки, *включая* ведущие цифры. Для `123.456789` с `4` значимыми цифрами вывод будет `123.5`.
- **Когда использовать:** Если система получатель ожидает фиксированную точность (например, научные файлы данных) или вам нужно усечь шум плавающей запятой.
- **Особый случай:** Если число содержит меньше цифр, чем указано, Aspose сохранит оригинальное значение (без дополнения нулями).

> **Почему не `setDecimalPlaces`?** Это свойство управляет *только* цифрами после десятичной точки, игнорируя ведущие цифры. Для научных данных `significantDigits` обычно является правильным выбором.

---

## Шаг 4: Сохранить Excel как текстовый файл (TXT)

С готовыми параметрами мы, наконец, записываем книгу в файл `.txt`. Это шаг **сохранения книги как txt**.

```java
        // 5️⃣ Persist the workbook as a TXT file
        String outputPath = "output/SignificantDigits.txt";
        workbook.save(outputPath, txtOptions);

        System.out.println("Excel exported to TXT at: " + outputPath);
    }
}
```

### Учёт папок

- Папка `output` должна существовать, иначе возникнет `IOException`. Вы можете создать её программно:

```java
new java.io.File("output").mkdirs();
```

- В Linux/macOS пути чувствительны к регистру; в Windows — нет. Используйте имена папок в нижнем регистре для кроссплатформенной надёжности.

---

## Шаг 5: Проверка результата

Запустите программу (`mvn compile exec:java -Dexec.mainClass=ExportExcelToTxtDemo`) и откройте `output/SignificantDigits.txt`. Вы должны увидеть:

```
123.5
```

Эта единственная строка подтверждает:

- Книга была успешно **сохранена как текстовый файл**.
- Числовое значение соблюдает **4 значимые цифры**, которые мы задали.
- В файл не попали лишние запятые, табуляции или специфичные для Excel метаданные.

Если вам нужен табуляторный разделитель для нескольких столбцов, просто заполните больше ячеек, и Aspose автоматически вставит табуляции.

---

## Часто задаваемые вопросы и особые случаи

### 1️⃣ Что если нужен другой разделитель?

`TxtSaveOptions` также предоставляет `setSeparator('\t')` для табуляций или `setSeparator(',')` для CSV‑подобного вывода. Пример:

```java
txtOptions.setSeparator('\t'); // Tab delimiter
```

### 2️⃣ Как локаль влияет на десятичные разделители?

По умолчанию Aspose использует системную локаль. Если вам нужен точка (`.`) независимо от локали, установите:

```java
txtOptions.setCultureInfo(java.util.Locale.US);
```

### 3️⃣ Большие листы — проблемы с памятью?

Aspose.Cells передаёт данные на диск при работе с листами более 1 ГБ, поэтому обычно не возникает `OutOfMemoryError`. Тем не менее, избегайте загрузки огромных листов в память, если нужен только их подмножество; используйте `Workbook.getWorksheets().get(index)`, чтобы обратиться к конкретному листу.

### 4️⃣ Можно ли экспортировать только диапазон?

Да. Используйте `txtOptions.setExportRange("A1:B10")`, чтобы ограничить вывод конкретной областью. Это уменьшает размер файла и ускоряет экспорт.

### 5️⃣ Что если у меня нет лицензии?

В режиме оценки добавляется строка‑водяной знак (`"Aspose.Cells for Java Evaluation Version"`). Для продакшна потребуется лицензия; иначе водяной знак может нарушить работу downstream‑парсеров.

---

## Полный рабочий пример (готов к копированию и вставке)

```java
import com.aspose.cells.*;

import java.io.File;

public class ExportExcelToTxtDemo {
    public static void main(String[] args) throws Exception {
        // Ensure output directory exists
        new File("output").mkdirs();

        // 1️⃣ Create workbook and get first worksheet
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.getWorksheets().get(0);

        // 2️⃣ Put several numbers to illustrate formatting
        sheet.getCells().get("A1").putValue(123.456789);
        sheet.getCells().get("A2").putValue(0.0012345);
        sheet.getCells().get("A3").putValue(98765.4321);

        // 3️⃣ Configure TXT options – 4 significant digits, tab delimiter
        TxtSaveOptions txtOptions = new TxtSaveOptions();
        txtOptions.setSignificantDigits(4);
        txtOptions.setSeparator('\t'); // optional, defaults to tab
        txtOptions.setCultureInfo(java.util.Locale.US); // enforce dot as decimal separator

        // 4️⃣ Save as TXT
        String outPath = "output/SignificantDigits.txt";
        workbook.save(outPath, txtOptions);

        System.out.println("Export completed: " + outPath);
    }
}
```

Запуск вышеуказанного создаёт `output/SignificantDigits.txt` со следующим содержимым:

```
123.5
0.001235
98770
```

Обратите внимание, как каждое число соблюдает правило **4 значимых цифр**, даже очень маленькие и очень большие значения.

---

## Заключение

Мы только что продемонстрировали **полный, автономный способ экспорта Excel в TXT** с помощью Java и Aspose.Cells, охватив **как задать значимые цифры**, **сохранить Excel как текстовый файл** и **сохранить книгу как txt**. Ключевые выводы:

- Используйте `TxtSaveOptions.setSignificantDigits` для управления числовой точностью.
- При необходимости корректируйте разделители, культуру и диапазоны экспорта.
- Код работает на любой платформе, требует лишь одну библиотеку и генерирует чистый текст с разделителями‑пробелами, готовый к дальнейшей обработке.

Готовы к следующему шагу? Попробуйте добавить несколько столбцов, поэкспериментировать с различными разделителями или интегрировать экспорт в более крупный ETL‑конвейер. Если столкнётесь с какими‑либо особенностями — возможно, проблемой локали или огромным листом — обратитесь к разделу «Часто задаваемые вопросы и особые случаи» выше.

Есть пример использования, которым хотите поделиться? Оставьте комментарий, сделайте форк репозитория и откройте pull request. Приятного кодинга и наслаждайтесь простотой преобразования таблиц в обычный текст!

## Что изучать дальше?

Следующие руководства охватывают тесно связанные темы, построенные на техниках, продемонстрированных в этом руководстве. Каждый ресурс включает полные рабочие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и изучить альтернативные подходы к реализации в ваших проектах.

- [Как сохранять файлы Excel в различных форматах с помощью Aspose.Cells Java](/cells/english/java/workbook-operations/save-excel-files-aspose-cells-java/)
- [Как загрузить и сохранить Excel как CSV с помощью Aspose.Cells for Java&#58; Полное руководство](/cells/english/java/workbook-operations/aspose-cells-java-load-save-excel-csv/)
- [Как создать и экспортировать Excel в HTML с помощью Aspose.Cells Java | Руководство по операциям с книгой](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}