---
category: general
date: 2026-07-23
description: Создайте новую книгу в Java и узнайте, как копировать сводную таблицу,
  копировать диапазон Excel и экспортировать сводную таблицу с помощью Aspose.Cells
  за несколько минут.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create new workbook
- copy pivot table
- how to copy pivot
- copy excel range
- export pivot table
language: ru
lastmod: 2026-07-23
og_description: Создайте новую рабочую книгу в Java и мгновенно скопируйте сводную
  таблицу, скопируйте диапазон Excel, затем экспортируйте сводную таблицу с помощью
  Aspose.Cells. Следуйте этому полному руководству.
og_image_alt: Screenshot of Java code copying a pivot table from one workbook to another
og_title: Создать новую книгу в Java – копировать сводную таблицу шаг за шагом
schemas:
- author: Aspose
  dateModified: '2026-07-23'
  description: Create new workbook in Java and learn how to copy pivot table, copy
    excel range, and export pivot table with Aspose.Cells in minutes.
  headline: Create New Workbook in Java – Full Guide to Copy Pivot Table
  type: TechArticle
- questions:
  - answer: You’ll need to copy each relevant range separately, then recreate the
      pivot on the destination sheet using `PivotTable` APIs.
    question: What if the source pivot spans more than one worksheet?
  - answer: Set `sourceRange.setCopyDataOnly(false)` before the copy. This tells Aspose
      to keep the cache but not the underlying source data.
    question: Can I copy only the pivot layout without the data?
  - answer: CSV doesn’t support pivots, but you can export the pivot’s *result* by
      calling `pivotTable.calculate()` and then saving the sheet as CSV.
    question: Is there a way to copy the pivot to a CSV file?
  - answer: Formatting lives in the style collection. After copying, you can call
      `destinationSheet.getCells().applyStyle(sourceSheet.getCells().getStyle())`
      to transfer styles.
    question: Why does the copied pivot lose its formatting?
  type: FAQPage
tags:
- Java
- Aspose.Cells
- Excel Automation
title: Создать новую рабочую книгу в Java – Полное руководство по копированию сводной
  таблицы
url: /ru/java/excel-pivot-tables/create-new-workbook-in-java-full-guide-to-copy-pivot-table/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Создание новой книги в Java – Полное руководство по копированию сводной таблицы

Когда‑нибудь задумывались, как **create new workbook** в Java, сохранив сложную сводную таблицу? Вы не одиноки в этом вопросе. Во многих отчетных приложениях необходимо переместить сводную таблицу из исходного файла в новую книгу, возможно, чтобы отправить её клиенту или выполнить дальнейшие расчёты. Хорошая новость: с помощью нескольких строк кода вы можете сделать именно это — без ручного копирования‑вставки.

В этом руководстве мы пройдём весь процесс: загрузка исходного файла, определение диапазона, содержащего сводную таблицу, **copying the Excel range**, создание **new workbook** и, наконец, **exporting the pivot table** в новый файл. К концу вы получите самостоятельную, готовую к запуску программу на Java, отвечающую на вопрос «**how to copy pivot**» без догадок.

## Требования

Перед тем как начать, убедитесь, что у вас есть:

- Java 17 или новее (код работает с любой современной JDK)
- Библиотека Aspose.Cells for Java (бесплатная пробная версия или лицензия)
- Пример `source.xlsx`, содержащий сводную таблицу в диапазоне `A1:G20`
- IDE или система сборки (Maven/Gradle) для управления JAR‑файлом Aspose.Cells

Есть всё? Отлично — приступим.

## Шаг 1: Настройка проекта и импорт Aspose.Cells

Для начала нужно добавить Aspose.Cells в ваш проект. Если вы используете Maven, поместите эту зависимость в ваш `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.8</version> <!-- check for the latest version -->
</dependency>
```

Если предпочитаете Gradle, эквивалент выглядит так:

```groovy
implementation 'com.aspose:aspose-cells:24.8'
```

После того как библиотека окажется в classpath, импортируйте необходимые классы:

```java
import com.aspose.cells.*;
import java.io.IOException;
```

> **Pro tip:** Aspose.Cells — коммерческая библиотека, но она предлагает полностью функциональную 30‑дневную оценочную версию, которая ставит водяной знак на вывод — идеально для пробного использования.

## Шаг 2: Загрузка исходной книги

Теперь мы **create new workbook** объекты, но сначала нам нужен источник, содержащий сводную таблицу. Этот шаг является основой любой операции **copy excel range**, потому что объект диапазона точно знает, какие ячейки (включая кэш сводной) нужно перенести.

```java
// Load the source workbook that contains the pivot table
Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/source.xlsx");

// Grab the first worksheet (index 0) – adjust if your pivot lives elsewhere
Worksheet sourceSheet = sourceWorkbook.getWorksheets().get(0);
```

Почему бы не прочитать диапазон напрямую? Потому что метаданные сводной таблицы находятся в кэше листа, и Aspose.Cells автоматически включает их при копировании диапазона.

## Шаг 3: Определение диапазона, содержащего сводную таблицу

Во многих реальных файлах сводная таблица занимает прямоугольный блок. В этом примере будем считать, что она находится в `A1:G20`. Разумеется, вы можете изменить адрес в соответствии с вашей фактической разметкой.

```java
// Define the exact area that includes the pivot table
Range sourceRange = sourceSheet.getCells().createRange("A1:G20");
```

Если вы не уверены в точном адресе, можете использовать `sourceSheet.getCells().getMaxDataRow()` и `getMaxDataColumn()` для динамического вычисления границ. Это удобный приём, когда размер сводной меняется со временем.

## Шаг 4: **Create New Workbook** и лист назначения

Вот момент, когда мы действительно **create new workbook**, который получит скопированный контент. Считайте это пустым холстом, на который вы вставите сводную таблицу.

```java
// Create an empty workbook – this is our destination
Workbook destinationWorkbook = new Workbook();

// By default a new workbook comes with one worksheet
Worksheet destinationSheet = destinationWorkbook.getWorksheets().get(0);
```

Почему начинать с пустой книги? Это гарантирует, что скрытые стили или предыдущие сводные не вмешаются в копирование, давая чистый результат, готовый к **export pivot table**.

## Шаг 5: Копирование сводной таблицы (и её базового диапазона)

Теперь основная часть руководства: **copy pivot table**. Aspose.Cells рассматривает копирование диапазона как глубокое копирование, то есть кэш сводной переезжает вместе с ячейками. Поэтому эта одна строка делает всю тяжёлую работу.

```java
// Copy the defined range (including the pivot) to the destination sheet at A1
sourceRange.copy(destinationSheet.getCells().createRange("A1"));
```

Если вы когда‑нибудь задавались вопросом **how to copy pivot** без потери функциональности, вот ответ. Лист назначения теперь содержит полностью рабочую сводную, которую можно обновлять, изменять или просто экспортировать.

### Edge Case: Сохранение настроек обновления

Иногда исходная сводная настроена на обновление при открытии. Чтобы сохранить это поведение, можно явно скопировать параметры сводной:

```java
// Optional: retain the original pivot's refresh settings
PivotTable srcPivot = sourceSheet.getPivotTables().get(0);
PivotTable destPivot = destinationSheet.getPivotTables().get(0);
destPivot.setRefreshOnFileOpen(srcPivot.isRefreshOnFileOpen());
```

Этот фрагмент кода гарантирует, что скопированная сводная будет вести себя точно так же, как оригинал.

## Шаг 6: Сохранение книги назначения – **Export Pivot Table**

Наконец, мы **export pivot table**, сохранив новую книгу на диск. Вы можете выбрать любой формат, поддерживаемый Aspose: XLSX, XLS, CSV, PDF и т.д. В этом руководстве мы останемся на XLSX.

```java
// Save the workbook that now contains the copied pivot
destinationWorkbook.save("YOUR_DIRECTORY/copied_with_pivot.xlsx", SaveFormat.XLSX);
```

Если нужно отправить файл через веб‑службу, вы можете записать его в `ByteArrayOutputStream` вместо пути к файлу — Aspose делает это тривиальным.

## Полный рабочий пример

Собрав всё вместе, получаем полностью готовую к запуску программу. Смело копируйте, вставляйте и выполняйте её в своей IDE.

```java
import com.aspose.cells.*;

public class CopyPivotExample {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load the source workbook
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/source.xlsx");
        Worksheet sourceSheet = sourceWorkbook.getWorksheets().get(0);
        Range sourceRange = sourceSheet.getCells().createRange("A1:G20");

        // 2️⃣ Create a new workbook that will receive the copied range
        Workbook destinationWorkbook = new Workbook();
        Worksheet destinationSheet = destinationWorkbook.getWorksheets().get(0);

        // 3️⃣ Copy the range (pivot table included) to the destination sheet
        sourceRange.copy(destinationSheet.getCells().createRange("A1"));

        // Optional: Preserve refresh settings if needed
        if (!sourceSheet.getPivotTables().isEmpty()) {
            PivotTable srcPivot = sourceSheet.getPivotTables().get(0);
            PivotTable destPivot = destinationSheet.getPivotTables().get(0);
            destPivot.setRefreshOnFileOpen(srcPivot.isRefreshOnFileOpen());
        }

        // 4️⃣ Save the result – this effectively **export pivot table**
        destinationWorkbook.save("YOUR_DIRECTORY/copied_with_pivot.xlsx", SaveFormat.XLSX);

        System.out.println("Pivot table copied successfully!");
    }
}
```

### Ожидаемый вывод

При запуске программы в консоль будет выведено:

```
Pivot table copied successfully!
```

И файл `copied_with_pivot.xlsx` появится в `YOUR_DIRECTORY`. Откройте его в Excel, и вы увидите сводную таблицу в целостности, готовую к обновлению или редактированию.

## Часто задаваемые вопросы и устранение неполадок

- **Что если исходная сводная таблица охватывает более одного листа?**  
  Вам придётся копировать каждый соответствующий диапазон отдельно, а затем воссоздать сводную на листе назначения, используя API `PivotTable`.

- **Можно ли скопировать только макет сводной без данных?**  
  Установите `sourceRange.setCopyDataOnly(false)` перед копированием. Это заставит Aspose сохранить кэш, но не исходные данные.

- **Есть ли способ скопировать сводную в CSV‑файл?**  
  CSV не поддерживает сводные, но вы можете экспортировать *результат* сводной, вызвав `pivotTable.calculate()` и затем сохранив лист как CSV.

- **Почему скопированная сводная теряет форматирование?**  
  Форматирование хранится в коллекции стилей. После копирования можно вызвать `destinationSheet.getCells().applyStyle(sourceSheet.getCells().getStyle())`, чтобы перенести стили.

## Заключение

Мы только что показали, как **create new workbook** в Java, **copy pivot table** и **export pivot table** — всё это с чистым, воспроизводимым примером кода. Определив точный **copy excel range**, используя глубокое копирование Aspose.Cells и сохраняя дополнительные настройки, вы сможете автоматизировать практически любую задачу миграции сводных таблиц.

Готовы к следующему шагу? Попробуйте изменить формат вывода на PDF или обработать несколько исходных файлов в цикле, чтобы пакетно обработать десятки сводных. Тот же шаблон применим — просто скорректируйте пути к файлам и адреса диапазонов.

Если возникнут проблемы, оставьте комментарий ниже или обратитесь к документации Aspose.Cells для продвинутой работы со сводными. Счастливого кодинга и наслаждайтесь сэкономленным временем благодаря автоматизации этих утомительных операций копирования‑вставки!

## Что вам стоит изучить дальше?

Следующие руководства охватывают тесно связанные темы, построенные на техниках, продемонстрированных в этом гайде. Каждый ресурс включает полные рабочие примеры кода с пошаговыми объяснениями, помогающими освоить дополнительные возможности API и исследовать альтернативные подходы в ваших проектах.

- [Как создавать сводные таблицы в Excel с помощью Aspose.Cells for Java: Полное руководство](/cells/english/java/data-analysis/create-pivot-tables-excel-aspose-cells-java/)
- [Как обновлять источник сводной таблицы Excel с помощью Aspose.Cells for Java: Полное руководство](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [Как создавать и экспортировать Excel в HTML с помощью Aspose.Cells Java | Руководство по операциям с книгами](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}