---
category: general
date: 2026-06-30
description: Установите пользовательский числовой формат в Excel с помощью Java. Узнайте,
  как создать рабочую книгу Excel на Java, получить дату и время из ячейки, вычислить
  формулы книги и вывести значение даты и времени.
draft: false
keywords:
- set custom number format
- get datetime from cell
- create excel workbook java
- calculate workbook formulas
- output datetime value
language: ru
og_description: Установите пользовательский числовой формат в Excel с помощью Java.
  Это руководство показывает, как создать рабочую книгу Excel на Java, получить дату
  и время из ячейки, вычислить формулы книги и вывести значение даты и времени.
og_title: Установите пользовательский числовой формат в Excel с помощью Java – полный
  учебник
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Set custom number format in Excel using Java. Learn how to create Excel
    workbook Java, get datetime from cell, calculate workbook formulas and output
    datetime value.
  headline: Set Custom Number Format in Excel with Java – Complete Guide
  type: TechArticle
- description: Set custom number format in Excel using Java. Learn how to create Excel
    workbook Java, get datetime from cell, calculate workbook formulas and output
    datetime value.
  name: Set Custom Number Format in Excel with Java – Complete Guide
  steps:
  - name: The **set custom number format** was applied (you can open the generated
      `.xlsx` in Excel to see “令和2年4月1日”).
    text: The **set custom number format** was applied (you can open the generated
      `.xlsx` in Excel to see “令和2年4月1日”).
  - name: The **calculate workbook formulas** step succeeded, turning the era string
      into a real date.
    text: The **calculate workbook formulas** step succeeded, turning the era string
      into a real date.
  - name: The **get datetime from cell** call returned a proper `Calendar`, which
      we then **output datetime value** to the console.
    text: The **get datetime from cell** call returned a proper `Calendar`, which
      we then **output datetime value** to the console.
  type: HowTo
tags:
- Java
- Excel
- Aspose.Cells
- DateTime
title: Установка пользовательского числового формата в Excel с помощью Java – полное
  руководство
url: /ru/java/formatting/set-custom-number-format-in-excel-with-java-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Установить пользовательский числовой формат в Excel с помощью Java – Полное руководство

Когда‑то вам нужно **установить пользовательский числовой формат** в листе Excel, работая на Java? Вы не одиноки. Будь то построение движка отчётности или просто корректное отображение дат в японской эре, освоение этого приёма экономит часы пост‑обработки. В этом руководстве мы пройдём реальный пример, который **создаёт Excel‑книгу Java**, применяет локализованный формат, пересчитывает формулы и, наконец, **получает DateTime из ячейки** для **вывода значения даты‑времени**.

Мы будем использовать популярную библиотеку Aspose.Cells for Java, потому что она сразу поддерживает числовые форматы и даты, учитывающие культуру. К концу руководства у вас будет автономная, исполняемая программа, которую можно добавить в любой проект Maven или Gradle. Никаких размытых «см. документацию»‑шорткатов — только надёжный код и чёткие объяснения.

---

## Что вы узнаете

- Как **создать Excel‑книгу Java** программно.  
- Точные шаги для **установки пользовательского числового формата** для дат в японской эре.  
- Почему вызов **calculate workbook formulas** необходим перед извлечением значения.  
- Правильный способ **получить datetime из ячейки** и **вывести значение datetime**.  
- Распространённые подводные камни (отсутствующая локаль, устаревшие формулы) и быстрые решения.

---

## Предварительные требования

- Java 8 или новее, установленная на вашем компьютере.  
- Aspose.Cells for Java 23.11 (или любая более свежая версия).  
- Любая базовая IDE или текстовый редактор — IntelliJ IDEA, Eclipse, VS Code, что вам удобно.  

Если вы ещё не добавили Aspose.Cells в проект, вставьте следующий фрагмент Maven в ваш `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.11</version>
</dependency>
```

Пользователи Gradle могут добавить:

```gradle
implementation 'com.aspose:aspose-cells:23.11'
```

Теперь, когда окружение готово, приступим к коду.

---

## Шаг 1: Установить пользовательский числовой формат – Обзор

Прежде чем писать Java‑код, полезно визуализировать, чего мы хотим достичь. Представьте ячейку Excel, которая должна отображать **«令和2年4月1日»** вместо ISO‑8601 строки «2020‑04‑01». Подлежащая величина остаётся истинной датой (поэтому формулы работают), но *отображение* следует формату японской эры. Именно это делает операция **set custom number format**.

Ниже полный исходный файл. Скопируйте‑вставьте его в `src/main/java/SetCustomNumberFormatDemo.java`.

```java
// File: SetCustomNumberFormatDemo.java
import com.aspose.cells.*;

public class SetCustomNumberFormatDemo {
    public static void main(String[] args) throws Exception {
        // -------------------------------------------------
        // 1️⃣ Create Excel workbook Java – a fresh workbook
        // -------------------------------------------------
        Workbook workbook = new Workbook();               // in‑memory workbook, no file yet

        // -------------------------------------------------
        // 2️⃣ Access the first worksheet
        // -------------------------------------------------
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // -------------------------------------------------
        // 3️⃣ Retrieve cell A1 where we’ll store the date string
        // -------------------------------------------------
        Cell cellA1 = worksheet.getCells().get("A1");

        // -------------------------------------------------
        // 4️⃣ Insert a Japanese era date string (Reiwa 2‑04‑01)
        // -------------------------------------------------
        // Note: Aspose.Cells will treat this as a text value until we recalc.
        cellA1.putValue("R02-04-01");

        // -------------------------------------------------
        // 5️⃣ Apply the custom number format (our primary goal)
        // -------------------------------------------------
        // [$-ja-JP] tells Excel to use the Japanese locale.
        // ggge年m月d日 renders as "令和2年4月1日".
        cellA1.setNumberFormat("[$-ja-JP]ggge年m月d日");

        // -------------------------------------------------
        // 6️⃣ Calculate workbook formulas – crucial step!
        // -------------------------------------------------
        // Without this, the cell remains a plain string and the
        // DateTime conversion below will fail.
        workbook.calculateFormula();

        // -------------------------------------------------
        // 7️⃣ Get DateTime from cell – now the value is a true date
        // -------------------------------------------------
        // The getDateTime() method returns a java.util.Calendar instance.
        java.util.Calendar dt = cellA1.getDateTime();

        // -------------------------------------------------
        // 8️⃣ Output datetime value – see the result in console
        // -------------------------------------------------
        System.out.println("Converted DateTime: " + dt.getTime()); // → Tue Apr 01 00:00:00 UTC 2020
    }
}
```

### Почему это работает

- **`setNumberFormat`** сообщает Excel, как *отображать* внутреннее числовое значение. Строка формата `[$-ja-JP]ggge年m月d日` — ключ; `ggg` выбирает название эры, `e` — год внутри эры, далее идут литералы месяца и дня.  
- **`calculateFormula`** заставляет Aspose.Cells интерпретировать текст «R02-04-01» как дату на основе японского календаря. Пропуск этого шага оставит ячейку как обычный текст, и `getDateTime()` выбросит исключение.  
- **`getDateTime`** в конце извлекает *реальный* объект `java.util.Calendar`, с которым можно работать, форматировать или сохранять где‑угодно.

---

## Шаг 2: Создать Excel‑книгу Java – Подробный взгляд

Когда вы **create Excel workbook Java**, вы не просто выделяете память; вы также создаёте стили по умолчанию, лист по умолчанию и культуру (обычно системную локаль). Если нужна другая локаль по умолчанию, можно передать объект `LoadOptions`:

```java
LoadOptions opts = new LoadOptions(LoadFormat.XLSX);
opts.setLocale(new java.util.Locale("ja", "JP"));
Workbook workbook = new Workbook(opts);
```

Для большинства сценариев достаточно простого конструктора, но полезно знать альтернативу — особенно когда в одном приложении работают с несколькими локалями.

*Совет:* Держите книгу в памяти, пока не закончите форматировать. Запись на диск после каждого изменения приводит к лишним операциям ввода‑вывода.

---

## Шаг 3: Получить DateTime из ячейки – Обработка результата

Строка `java.util.Calendar dt = cellA1.getDateTime();` делает всю тяжёлую работу. За кулисами Aspose.Cells преобразует внутренний серийный номер (количество дней с 31‑12‑1899) в `Calendar`. Это преобразование учитывает локаль книги, поэтому вы получаете правильную григорианскую дату, хотя отображение использует японскую эру.

Если нужен `java.time.LocalDate` (современный API), преобразуйте так:

```java
java.time.LocalDate localDate = dt.toInstant()
        .atZone(java.time.ZoneId.systemDefault())
        .toLocalDate();
System.out.println("LocalDate: " + localDate); // 2020-04-01
```

Это покрывает требование **output datetime value**, оставаясь современным.

---

## Шаг 4: Пересчитать формулы книги – Когда это важно

Вы можете задаться вопросом: *«Нужен ли действительно вызов `calculateFormula()`?»* Ответ — решительно «да», если только вы не передаёте в ячейку нативный объект Java `Date` сразу. Когда вы **set custom number format** на строку, Excel (и Aspose.Cells) рассматривают её как формульное выражение, требующее вычисления. Без пересчёта `getDateTime()` вернёт значение по умолчанию `1900‑01‑00` или бросит `CellValueException`.

Если ваша книга уже содержит сложные формулы, ссылающиеся на только что отформатированную ячейку, вызовите `calculateFormula()` *один раз* после всех изменений. Повторные вызовы дорогие.

---

## Шаг 5: Вывести значение DateTime – Проверка результата

Запуск демо выводит примерно следующее:

```
Converted DateTime: Tue Apr 01 00:00:00 UTC 2020
```

Эта строка подтверждает три вещи:

1. **set custom number format** был применён (откройте сгенерированный `.xlsx` в Excel и увидите «令和2年4月1日»).  
2. Шаг **calculate workbook formulas** прошёл успешно, превратив строку эры в реальную дату.  
3. Вызов **get datetime from cell** вернул корректный `Calendar`, который мы затем **output datetime value** в консоль.

Если открыть книгу в табличной программе, вы увидите отформатированный текст, но под‑ячейка остаётся серийным номером `43831` (представление Excel даты 2020‑04‑01). Эта двойственность и делает Excel мощным.

---

## Распространённые подводные камни и граничные случаи

| Проблема | Почему происходит | Решение |
|----------|-------------------|---------|
| `cellA1.getDateTime()` бросает `CellValueException` | Ячейка всё ещё строка, потому что пропущен `calculateFormula()`. | Всегда вызывайте `workbook.calculateFormula()` после установки текстовой даты, требующей преобразования. |
| Японская эра отображается неверно | Отсутствует или неверен код локали. | Используйте `[$-ja-JP]` в строке формата или задайте локаль книги через `LoadOptions`. |
| Формат показывает «#VALUE!» в Excel | Строка формата некорректна. | Проверьте скобки и символы; необходим шаблон `ggge年m月d日` для года эры. |
| Появляется компонент времени (например, «00:00:00») | Исходная строка содержит время или стиль ячейки добавляет его. | Обрежьте исходную строку или скорректируйте формат до `ggge年m月d日;@`. |

---

## Полный рабочий пример – Один клик для запуска

Если нужен один файл без лишних комментариев, вот минимальная версия:



## Что следует изучить дальше?

Следующие руководства охватывают тесно связанные темы, расширяющие техники, продемонстрированные в этом пособии. Каждый ресурс содержит полностью рабочие примеры кода с пошаговыми объяснениями, чтобы вы могли освоить дополнительные возможности API и исследовать альтернативные подходы в своих проектах.

- [Create an Excel Workbook using Aspose.Cells in Java: A Step-by-Step Guide](/cells/english/java/getting-started/create-excel-workbook-aspose-cells-java/)
- [Mastering Data Presentation in Excel: Number and Custom Date Formatting with Aspose.Cells for Java](/cells/english/java/formatting/aspose-cells-java-data-formatting-excel/)
- [How to Create & Format Excel Cells Using Aspose.Cells for Java: A Step-by-Step Guide](/cells/english/java/formatting/aspose-cells-java-excel-automation-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}