---
category: general
date: 2026-06-21
description: Руководство по форматам даты в Aspose Cells — узнайте, как задать пользовательский
  формат даты, изменить локаль рабочей книги и применить глобальный формат даты в
  Java.
draft: false
keywords:
- aspose cells date format
- set custom date format
- how to set date format
- change workbook locale
- set global date format
language: ru
og_description: 'Учебник по формату даты Aspose Cells: узнайте, как установить пользовательский
  формат даты, изменить локаль книги и задать глобальный формат даты для проектов
  Java.'
og_title: Формат даты Aspose Cells – установить пользовательский формат даты в Java
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Aspose Cells date format guide – learn how to set custom date format,
    change workbook locale, and apply a global date format in Java.
  headline: 'Aspose Cells Date Format: How to Set Custom Date Format in Java'
  type: TechArticle
- description: Aspose Cells date format guide – learn how to set custom date format,
    change workbook locale, and apply a global date format in Java.
  name: 'Aspose Cells Date Format: How to Set Custom Date Format in Java'
  steps:
  - name: 1. Overriding the Global Format at the Cell Level
    text: 'If a cell already has a style with a specific number format, the global
      setting is ignored for that cell. To force the global format, clear the cell’s
      style:'
  - name: 2. Changing Workbook Locale Without a Custom Pattern
    text: 'Sometimes you just want to **change workbook locale** so that built‑in
      date formats (like `14‑03‑2024`) follow regional conventions. You can do this
      without a `DateTimeFormatter`:'
  - name: 3. Using Multiple Custom Formats in One Workbook
    text: 'Aspose Cells allows you to define several custom formats and apply them
      selectively:'
  - name: 4. Resetting to the Default Format
    text: 'If you need to revert to Aspose’s default date handling, simply pass `null`:'
  type: HowTo
- questions:
  - answer: Yes—any worksheet loaded into the `Workbook` after you set the global
      format will inherit it, unless a cell already has an explicit style.
    question: Does this affect existing worksheets?
  - answer: Absolutely. The global format is applied at render time, so you can populate
      cells first and set the format later.
    question: Can I set the format after writing data?
  - answer: Use the appropriate `CultureInfo` code (`"th-TH"`), and the formatter
      will respect that calendar automatically.
    question: What if I need a locale‑specific calendar (e.g., Thai Buddhist)?
  - answer: Negligible. The formatter is cached inside `WorkbookSettings`, so the
      overhead is only incurred once per workbook.
    question: Is there a performance penalty?
  type: FAQPage
tags:
- aspose-cells
- java
- date-formatting
title: 'Формат даты в Aspose Cells: как задать пользовательский формат даты в Java'
url: /ru/java/formatting/aspose-cells-date-format-how-to-set-custom-date-format-in-ja/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose Cells Date Format – Полное руководство по Java

Когда‑нибудь задумывались, как задать пользовательский формат даты в Aspose Cells для Java? Вы не одиноки. Независимо от того, создаёте ли вы отчёты для японского клиента или просто хотите единый стиль даты во всей книге, освоение **aspose cells date format** является обязательным.

В этом руководстве мы пройдём практический, сквозной пример, который покажет, **как задать формат даты** глобально, изменить локаль книги и применить пользовательский шаблон, например, год японской эры. К концу вы получите переиспользуемый фрагмент кода, который можно вставить в любой проект — без догадок.

## Что покрывает это руководство

- Создание нового экземпляра `Workbook`.
- Изменение локали книги, чтобы встроенные форматы учитывали региональные правила.
- Определение **пользовательского формата даты** с помощью `DateTimeFormatter`.
- Применение этого формата глобально через `WorkbookSettings`.
- Распространённые подводные камни (например, переопределение форматов на уровне ячеек) и способы их избежать.
- Быстрые варианты для других локалей или строк формата.

Вам понадобится лишь среда разработки Java, Maven или Gradle для подключения Aspose Cells и базовое понимание синтаксиса Java. Готовы? Поехали.

## Шаг 1: Настройте проект и импортируйте Aspose Cells

Прежде всего, убедитесь, что Aspose Cells for Java находится в вашем classpath. Если вы используете Maven, добавьте следующую зависимость в ваш `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- Use the latest stable version -->
</dependency>
```

Пользователи Gradle могут добавить:

```gradle
implementation 'com.aspose:aspose-cells:24.9'
```

> **Совет:** Aspose предлагает бесплатную 30‑дневную пробную лицензию. Поместите файл `Aspose.Cells.lic` в корень проекта и вызовите  
> `License license = new License(); license.setLicense("Aspose.Cells.lic");` перед созданием любой книги.

Теперь импортируем необходимые классы:

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.WorkbookSettings;
import com.aspose.cells.DateTimeFormatter;
import com.aspose.cells.CultureInfo;
```

Эти импорты дают нам доступ к контейнеру книги, её настройкам и локализованному форматтеру.

## Шаг 2: Создайте новую книгу и получите её настройки

Новая `Workbook` создаётся с локалью по умолчанию (обычно США). Чтобы управлять датами глобально, нам нужно получить объект `WorkbookSettings`:

```java
// Step 2: Initialize a new workbook
Workbook workbook = new Workbook();

// Grab the settings object – this is where we’ll apply the date format
WorkbookSettings settings = workbook.getSettings();
```

Объект `settings` — центральный узел. Всё, что вы здесь изменяете, например формат даты, влияет на каждую ячейку, **не имеющую** собственного стиля, переопределяющего его.

## Шаг 3: Определите пользовательский формат даты/времени (пример с японской эрой)

Предположим, вам нужны даты в формате японской эры, например «令和04.10.01». Шаблон `"ggyy.MM.dd"` делает это, если использовать японскую культуру:

```java
// Step 3: Build a formatter for the Japanese era year
DateTimeFormatter formatter = new DateTimeFormatter(
        "ggyy.MM.dd",                // Pattern: era (gg), year (yy), month, day
        new CultureInfo("ja-JP")    // Locale: Japanese (Japan)
);
```

Если предпочтительнее более простой ISO‑стиль (`"yyyy-MM-dd"`), просто замените строку шаблона — никаких других изменений не требуется.

## Шаг 4: Примените пользовательский формат как глобальный формат даты

Теперь привяжем форматтер к глобальным настройкам книги. Это шаг **set global date format**, который гарантирует, что любая ячейка, отображающая дату, автоматически использует наш шаблон:

```java
// Step 4: Apply the custom formatter globally
settings.setDateTimeFormat(formatter);
```

На этом этапе любая дата, записанная в лист — будь то `Cell.putValue(new Date())` или чтение из источника данных — будет отображаться по шаблону японской эры.

## Шаг 5: Заполните книгу примерными датами (по желанию)

Добавим несколько строк, чтобы увидеть формат в действии. Эта часть не обязательна для логики форматирования, но помогает убедиться, что всё работает:

```java
// Step 5: Insert sample dates into the first sheet
var sheet = workbook.getWorksheets().get(0);
var cells = sheet.getCells();

cells.get("A1").putValue(new java.util.Date()); // Today’s date
cells.get("A2").putValue(java.sql.Date.valueOf("2024-12-31")); // Specific date
cells.get("A3").putValue(java.time.LocalDateTime.now()); // Date‑time now
```

При сохранении книги эти ячейки покажут, например:

```
A1: 令和05.04.21
A2: 令和06.12.31
A3: 令和05.04.21 14:37:12
```

(Точный год эры зависит от текущего японского календаря.)

## Шаг 6: Сохраните книгу и проверьте результат

Наконец, запишите книгу в файл, чтобы открыть её в Excel, LibreOffice или любом просмотрщике, поддерживающем формат:

```java
// Step 6: Save the workbook
workbook.save("CustomDateFormatDemo.xlsx");
System.out.println("Workbook saved with custom date format.");
```

Откройте `CustomDateFormatDemo.xlsx`, и вы должны увидеть даты, отформатированные согласно заданному шаблону. Если заметите несоответствие, проверьте, не переопределён ли глобальный стиль на уровне ячейки (см. раздел «Edge Cases» ниже).

## Edge Cases & Variations

### 1. Переопределение глобального формата на уровне ячейки

Если у ячейки уже есть стиль с конкретным числовым форматом, глобальная настройка игнорируется для этой ячейки. Чтобы принудительно применить глобальный формат, очистите стиль ячейки:

```java
cells.get("A1").getStyle().setNumber(0); // Reset number format to default
```

### 2. Изменение локали книги без пользовательского шаблона

Иногда достаточно **change workbook locale**, чтобы встроенные форматы дат (например `14‑03‑2024`) соответствовали региональным конвенциям. Это можно сделать без `DateTimeFormatter`:

```java
WorkbookSettings localeSettings = workbook.getSettings();
localeSettings.setCultureInfo(new CultureInfo("fr-FR")); // French (France)
```

Теперь любой стандартный стиль даты будет выглядеть как `21/04/2025` вместо `04/21/2025`.

### 3. Использование нескольких пользовательских форматов в одной книге

Aspose Cells позволяет определить несколько пользовательских форматов и применять их выборочно:

```java
// Define two formatters
DateTimeFormatter usFormatter = new DateTimeFormatter("MM/dd/yyyy", new CultureInfo("en-US"));
DateTimeFormatter jpFormatter = new DateTimeFormatter("ggyy.MM.dd", new CultureInfo("ja-JP"));

// Apply US format globally
settings.setDateTimeFormat(usFormatter);

// Later, apply Japanese format to a specific range
var style = workbook.createStyle();
style.setCustom(usFormatter.getFormatString()); // Or jpFormatter.getFormatString()
cells.get("B1").setStyle(style);
```

### 4. Возврат к формату по умолчанию

Если нужно вернуть обработку дат к настройкам Aspose, просто передайте `null`:

```java
settings.setDateTimeFormat(null); // Clears the custom global format
```

## Часто задаваемые вопросы

- **Влияет ли это на уже существующие листы?**  
  Да — любой лист, загруженный в `Workbook` после установки глобального формата, унаследует его, если только ячейка не имеет собственного стиля.

- **Можно ли задать формат после записи данных?**  
  Конечно. Глобальный формат применяется во время рендеринга, поэтому вы можете сначала заполнить ячейки, а затем установить формат.

- **Что если нужен календарь, специфичный для локали (например, тайский буддийский)?**  
  Используйте соответствующий код `CultureInfo` (`"th-TH"`), и форматтер автоматически учтёт этот календарь.

- **Есть ли штраф в производительности?**  
  Незначительный. Форматтер кэшируется внутри `WorkbookSettings`, поэтому накладные расходы возникают лишь один раз на книгу.

## Полный рабочий пример

Ниже представлена полностью готовая к запуску программа, включающая все обсуждённые шаги:

```java
import com.aspose.cells.*;

public class AsposeCellsDateFormatDemo {
    public static void main(String[] args) throws Exception {
        // Apply license if you have one
        // License lic = new License();
        // lic.setLicense("Aspose.Cells.lic");

        // 1️⃣ Create workbook
        Workbook workbook = new Workbook();

        // 2️⃣ Access settings
        WorkbookSettings settings = workbook.getSettings();

        // 3️⃣ Define custom Japanese era format
        DateTimeFormatter jpFormatter = new DateTimeFormatter(
                "ggyy.MM.dd",
                new CultureInfo("ja-JP")
        );

        // 4️⃣ Set as global date format
        settings.setDateTimeFormat(jpFormatter);

        // 5️⃣ Add sample dates
        var sheet = workbook.getWorksheets().get(0);
        var cells = sheet.getCells();

        cells.get("A1").putValue(new java.util.Date());                     // Today
        cells.get("A2").putValue(java.sql.Date.valueOf("2024-12-31"));      // Fixed date
        cells.get("A3").putValue(java.time.LocalDateTime.now());           // Date‑time now

        // 6️⃣ Save to file
        workbook.save("AsposeCellsCustomDateFormat.xlsx");
        System.out.println("Workbook saved with custom Japanese era date format.");
    }
}
```

**Ожидаемый вывод в Excel:**

| Ячейка | Отображаемое значение |
|--------|------------------------|
| A1     | 令和05.04.21           |
| A2     | 令和06.12.31           |
| A3     | 令和05.04.21 14:45:03 (время может отличаться) |

Откройте файл, и вы увидите даты, отформатированные точно так, как задано.

## Заключение

Вы только что узнали, как **aspose cells date format** книгу в Java, от изменения локали до применения **set custom date format**, работающего глобально. Используя `WorkbookSettings` и `DateTimeFormatter`, вы получаете точный контроль над отображением каждой даты — без необходимости ручного стилизования.

Далее вы можете изучить **how to set date format** для отдельных столбцов или комбинировать пользовательские числовые форматы с условным форматированием для создания профессионального отчёта. Принципы те же: определить форматтер, привязать его через стиль и позволить Aspose выполнить остальное.

Счастливого кодинга, экспериментируйте с другими локалями — ваши пользователи оценят аккуратные, культурно‑адаптированные таблицы!

## Что изучать дальше?

Следующие руководства охватывают тесно связанные темы, расширяющие техники, продемонстрированные в этом руководстве. Каждый ресурс включает полностью работающий код с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы в собственных проектах.

- [Efficiently Convert Excel to PDF with Custom Date Formats Using Aspose.Cells for Java](/cells/english/java/workbook-operations/render-excel-custom-date-formats-pdf-aspose-cells-java/)
- [Mastering Data Presentation in Excel: Number and Custom Date Formatting with Aspose.Cells for Java](/cells/english/java/formatting/aspose-cells-java-data-formatting-excel/)
- [How to Create & Format Excel Cells Using Aspose.Cells for Java: A Step‑By‑Step Guide](/cells/english/java/formatting/aspose-cells-java-excel-automation-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}