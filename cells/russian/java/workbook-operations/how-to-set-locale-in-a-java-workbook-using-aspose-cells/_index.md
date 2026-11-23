---
category: general
date: 2026-11-22
description: Узнайте, как установить локаль в Java‑рабочей книге, изменить язык рабочей
  книги и задать календарь на японский, с понятными примерами кода.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to set locale
- change workbook language
- set locale to japanese
- how to set calendar
language: ru
lastmod: 2026-11-22
og_description: Как быстро установить локаль в Java‑рабочей книге. Следуйте этому
  руководству, чтобы изменить язык книги, установить локаль на японский и настроить
  японский календарь.
og_image_alt: Screenshot showing how to set locale in a Java workbook
og_title: Как установить локаль в Java‑рабочей книге – пошаговое руководство
schemas:
- author: Aspose
  dateModified: '2026-11-22'
  description: Learn how to set locale in a Java workbook, change workbook language,
    and set the calendar to Japanese with clear code examples.
  headline: How to set locale in a Java workbook using Aspose.Cells
  type: TechArticle
- description: Learn how to set locale in a Java workbook, change workbook language,
    and set the calendar to Japanese with clear code examples.
  name: How to set locale in a Java workbook using Aspose.Cells
  steps:
  - name: Run the **FullLocaleExample** class.
    text: Run the **FullLocaleExample** class.
  - name: Open the generated `FullJapaneseLocale.xlsx` in Excel.
    text: Open the generated `FullJapaneseLocale.xlsx` in Excel.
  - name: 'Verify that:'
    text: 'Verify that:'
  type: HowTo
tags:
- Java
- Aspose.Cells
- Internationalization
- Workbook
title: Как задать локаль в Java‑рабочей книге с использованием Aspose.Cells
url: /ru/java/workbook-operations/how-to-set-locale-in-a-java-workbook-using-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как установить локаль в Java‑книге Excel с помощью Aspose.Cells

Установка локали в Java‑книге Excel — распространённая задача, когда необходимо адаптировать таблицу к различным регионам. В этом руководстве вы узнаете, как задать локаль, изменить язык книги и установить календарь на японский с помощью API Aspose.Cells.

Интернационализация книги выходит за рамки простого перевода текста; она также влияет на форматы чисел, разбор дат и используемую календарную систему. По окончании этого урока вы сможете:

* Настроить локаль книги на японскую (Japan) – **set locale to japanese**.  
* Изменить язык книги, чтобы формулы и строки UI учитывали целевую культуру – **change workbook language**.  
* Переключить календарь на японский императорский календарь – **how to set calendar**.  

Эти шаги работают с любой современной версией Aspose.Cells for Java (v23.9 и новее) и требуют лишь стандартной среды разработки Java.

## Требования

| Требование | Причина |
|-------------|--------|
| Java 8 или выше | Библиотека ориентирована на Java 8+. |
| Aspose.Cells for Java (v23.9+) | Предоставляет `Workbook`, `WorkbookSettings` и утилиты локали. |
| IDE (IntelliJ IDEA, Eclipse или VS Code) | Для компиляции и запуска примера. |
| Базовые знания Java | Необходимы для понимания фрагментов кода. |

Добавьте зависимость Aspose.Cells в ваш `pom.xml` (или загрузите JAR вручную):

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.9</version>
    <classifier>jdk17</classifier> <!-- adjust for your JDK version -->
</dependency>
```

## Как установить локаль и календарь в книге

Первый шаг — создать экземпляр книги и получить объект её настроек. Объект настроек раскрывает API локали и календаря.

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.WorkbookSettings;
import java.util.Locale;
import java.util.Calendar;

public class WorkbookLocaleDemo {
    public static void main(String[] args) {
        // Step 1: Create a new workbook (empty by default)
        Workbook workbook = new Workbook();

        // Step 2: Access the workbook's settings
        WorkbookSettings settings = workbook.getSettings();

        // Step 3: Set the calendar to the Japanese calendar
        // Aspose.Cells uses java.util.Calendar; the Japanese calendar is available via Calendar.JAPANESE
        settings.setCalendar(Calendar.getInstance(Locale.JAPAN));

        // Step 4: Set the locale to Japanese (Japan)
        // This influences number formats, date formats, and built‑in function behaviour.
        settings.setLocale(new Locale("ja", "JP"));

        // Optional: Save the workbook to verify the settings
        workbook.save("LocaleDemo.xlsx");
    }
}
```

### Почему важна каждая строка

* **`new Workbook()`** – Создаёт пустую книгу, которую можно изменять перед сохранением.  
* **`getSettings()`** – Возвращает объект `WorkbookSettings`; все региональные параметры находятся здесь.  
* **`setCalendar(...)`** – Заменяет календарь по умолчанию (Григорианский) на японский императорский, влияя на отображение и разбор дат.  
* **`setLocale(new Locale("ja","JP"))`** – Меняет язык и региональные соглашения (например, названия месяцев, десятичные разделители). Это ядро **how to set locale** для книги.  

Запуск программы создаёт `LocaleDemo.xlsx`. Откройте его в Excel или LibreOffice, и вы увидите названия месяцев на японском, символы валюты йен и даты, отформатированные согласно японскому календарю.

## Изменить язык книги (установить локаль на японский)

Если ваша главная цель — **change workbook language**, можно сосредоточиться только на вызове `setLocale`. Ниже приведён фрагмент, изолирующий этот шаг:

```java
Workbook workbook = new Workbook();
WorkbookSettings settings = workbook.getSettings();

// Change only the language to Japanese (Japan)
settings.setLocale(new Locale("ja", "JP"));
workbook.save("JapaneseLanguage.xlsx");
```

**Что меняется?**  
* Строки форматирования ячеек переключаются на японские (например, `#,##0.00` становится `#,##0.00` с символом йены).  
* Встроенные имена функций (например, `SUM`) остаются на английском, потому что локаль функций в Excel независима, но строки дат и сообщения об ошибках следуют японским соглашениям.  

**Когда использовать?**  
* Когда нужен лист, отображающий числа и даты для японской аудитории, но календарь может оставаться Григорианским.  
* Для отчётов, экспортируемых в PDF или печатаемых, чтобы визуальный язык соответствовал целевому рынку.

## Как установить календарь на японский календарь

Иногда требование **how to set calendar** отделено от локали. Для наследуемых систем, хранящих даты в японской императорской эре, необходимо явно задать календарь, при желании оставив локаль по умолчанию.

```java
Workbook workbook = new Workbook();
WorkbookSettings settings = workbook.getSettings();

// Set only the calendar; keep the default (US) locale
settings.setCalendar(Calendar.getInstance(Locale.JAPAN));

// Verify the calendar by creating a date cell
int row = 0, column = 0;
workbook.getWorksheets().get(0).getCells().putValue(row, column, new java.util.Date());

// Save to see the Japanese era (e.g., "R3/04/01" for Reiwa 3)
workbook.save("JapaneseCalendar.xlsx");
```

**Ключевые моменты:**

* `Calendar.getInstance(Locale.JAPAN)` возвращает `java.util.Calendar`, настроенный под японскую эру.  
* Книга теперь будет отображать даты с символами эпох (R для Reiwa, H для Heisei и т.д.).  
* Эта настройка **не** влияет на форматирование чисел или язык UI; комбинируйте её с `setLocale`, если нужны обе функции.

## Полный сквозной пример

Ниже представлен полностью готовый к запуску пример, демонстрирующий **how to set locale**, **change workbook language** и **set the calendar** в едином потоке. Пример также добавляет образцовую ячейку для иллюстрации эффекта.

```java
import com.aspose.cells.*;
import java.util.*;

public class FullLocaleExample {
    public static void main(String[] args) throws Exception {
        // Create a new workbook
        Workbook workbook = new Workbook();

        // Access settings
        WorkbookSettings settings = workbook.getSettings();

        // 1️⃣ Set the locale to Japanese (Japan) – changes language & number formats
        settings.setLocale(new Locale("ja", "JP"));

        // 2️⃣ Set the calendar to the Japanese imperial calendar
        settings.setCalendar(Calendar.getInstance(Locale.JAPAN));

        // 3️⃣ Add a sample date and number to visualize the changes
        Worksheet sheet = workbook.getWorksheets().get(0);
        Cells cells = sheet.getCells();

        // Date cell – will show Japanese era after applying the calendar
        cells.putValue(0, 0, new Date());

        // Number cell – will use Japanese Yen symbol and comma separator
        cells.putValue(1, 0, 1234567.89);

        // Apply a style to the number cell for currency formatting
        Style style = cells.getRows().get(1).getStyle();
        style.setNumber(3); // Built‑in currency format
        cells.getRows().get(1).setStyle(style);

        // Save the workbook
        workbook.save("FullJapaneseLocale.xlsx");
        System.out.println("Workbook created with Japanese locale and calendar.");
    }
}
```

**Ожидаемый результат:**  
Открывая `FullJapaneseLocale.xlsx`, первая ячейка содержит дату вида `R3/04/01` (Reiwa 3), а вторая — формат `¥1,234,567.89`. Это подтверждает, что **how to set locale**, **change workbook language** и **how to set calendar** работают совместно.

## Распространённые подводные камни и как их избежать

| Подводный камень | Почему происходит | Как исправить |
|------------------|-------------------|---------------|
| Использование `Locale.CHINA` вместо `new Locale("ja","JP")` | `Locale.CHINA` задаёт китайский язык, а не японский. | Всегда создавайте `Locale` с `"ja", "JP"` для японского. |
| Заб忘 вызова `settings.setCalendar(...)` после `setLocale` | По умолчанию используется Григорианский календарь, даты отображаются в неверной эре. | Вызывайте `setCalendar` **после** установки локали, либо задавайте оба сразу, как показано. |
| Сохранение книги до применения настроек | Настройки применяются к объекту в памяти; раннее сохранение записывает локаль по умолчанию. | Применяйте все изменения локали/календаря **до** вызова `workbook.save()`. |
| Использование устаревшей версии Aspose.Cells | Старые версии не поддерживают перегрузки `setCalendar`. | Обновитесь до v23.9+ или проверьте примечания к выпуску для поддержки локали. |

## Тестирование вашей конфигурации

1. Запустите класс **FullLocaleExample**.  
2. Откройте сгенерированный `FullJapaneseLocale.xlsx` в Excel.  
3. Проверьте, что:  
   * Столбец дат показывает символы японских эпох (`R`, `H` и т.д.).  
   * Столбец чисел использует символ йены и запятые как разделители.  
   * Любые встроенные сообщения об ошибках (например, `#DIV/0!`) отображаются на японском, если в книге есть ошибки.  

Если какой‑либо из пунктов не выполнен, убедитесь, что изменённый объект `WorkbookSettings` тот же, который используется при сохранении.

## Следующие шаги

* **Локализация формул** – Хотя локаль управляет форматированием, вы также можете переводить пользовательские имена функций с помощью `FormulaParser`.  
* **Применить локаль к существующим книгам** – Загрузите книгу через `new Workbook`  

## Что следует изучить дальше?

Следующие руководства охватывают близкие темы, расширяющие техники, продемонстрированные в этом руководстве. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, помогая вам освоить дополнительные возможности API и исследовать альтернативные подходы в собственных проектах.

- [Aspose Cells Date Format: How to Set Custom Date Format in Java](/cells/english/java/formatting/aspose-cells-date-format-how-to-set-custom-date-format-in-ja/)
- [How to Set Language in Excel Files Using Aspose.Cells .NET for Multilingual Support](/cells/english/net/formulas-functions/specify-language-excel-aspose-cells-net/)
- [How to set cell number format and convert Japanese dates in C# using Aspose.Cells](/cells/english/net/excel-custom-number-date-formatting/set-cell-number-format-and-convert-japanese-dates-in-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}