---
category: general
date: 2026-06-21
description: Программно копировать диапазон листа в Java с использованием Aspose.Cells.
  Узнайте, как эффективно копировать диапазон Excel в другую книгу.
draft: false
keywords:
- programmatically copy worksheet range
- how to copy excel range to another workbook
- Aspose.Cells copy range Java
- copy pivot table between workbooks
- Java Excel automation
language: ru
og_description: Программно копировать диапазон листа в Java. Это руководство показывает,
  как скопировать диапазон Excel в другую книгу с полным кодом и советами.
og_title: Программное копирование диапазона листа — пошаговое руководство на Java
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Programmatically copy worksheet range in Java using Aspose.Cells. Learn
    how to copy excel range to another workbook efficiently.
  headline: Programmatically Copy Worksheet Range – Complete Java Guide
  type: TechArticle
- description: Programmatically copy worksheet range in Java using Aspose.Cells. Learn
    how to copy excel range to another workbook efficiently.
  name: Programmatically Copy Worksheet Range – Complete Java Guide
  steps:
  - name: 1. Copying Across Different Excel Versions
    text: Aspose.Cells works with `.xls`, `.xlsx`, `.xlsb`, and even `.csv`. If the
      source and destination use different formats, the library automatically converts
      them. Just ensure the file extensions match your desired output.
  - name: 2. Preserving External Data Sources in Pivot Tables
    text: If the pivot table in the source references an external data source (e.g.,
      a database connection), the copied pivot will retain the connection string but
      **won’t automatically refresh**. Call `pivotTable.refreshData()` after copying
      if you need up‑to‑date results.
  - name: 3. Large Ranges and Memory Consumption
    text: Copying massive ranges (hundreds of thousands of rows) can spike memory
      usage. Use `Workbook.setMemorySetting(MemorySetting.MEMORY_PREFERENCE)` before
      loading large files to keep the footprint low.
  - name: 4. Multiple Sheets or Ranges
    text: If you need to copy several non‑contiguous ranges, repeat steps 4‑6 for
      each range, or use `copyRange` with a union range (`Cells.createRange("A1:B10,C1:D10")`).
  type: HowTo
tags:
- Java
- Excel
- Aspose.Cells
- Workbook
- Automation
title: Программное копирование диапазона листа — Полное руководство по Java
url: /ru/java/range-management/programmatically-copy-worksheet-range-complete-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Программное копирование диапазона листа – Полное руководство на Java

Когда‑нибудь задумывались, как **программно копировать диапазон листа** без ручного открытия Excel? Вы не одиноки. Нужно продублировать отчёт, клонировать панель управления на основе сводных таблиц или просто переместить данные между файлами — сделать это в коде экономит время и исключает человеческие ошибки.

В этом руководстве мы пошагово разберём чистое, сквозное решение, показывающее **как скопировать диапазон Excel в другую книгу** с помощью Java и библиотеки Aspose.Cells. К концу вы получите готовую к запуску программу, поймёте причину каждого шага и узнаете о подводных камнях.

---

## Что понадобится

- **Java Development Kit (JDK) 11+** — код компилируется любой современной JDK.
- **Aspose.Cells for Java** (бесплатная пробная версия или лицензия). Добавьте зависимость Maven или скачайте JAR.
- Два файла Excel: `input.xlsx` — с исходным диапазоном (включая сводную таблицу) и пустой `output.xlsx`, куда будет скопирован диапазон.
- Любая IDE — IntelliJ IDEA, Eclipse или простой текстовый редактор.

И всё. Никаких дополнительных сервисов, без COM‑interop, только чистый Java.

---

![Diagram illustrating programmatically copy worksheet range between two workbooks](image.png)

*Текст альтернативного изображения: иллюстрация программного копирования диапазона листа*

---

## Шаг 1: Настройка проекта и импорт Aspose.Cells

Прежде всего, нам нужна библиотека в classpath. Если вы используете Maven, добавьте:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- Use the latest stable version -->
</dependency>
```

Если предпочитаете ручной JAR, поместите его в папку `libs` и добавьте в путь сборки.

Почему это важно: Aspose.Cells предоставляет богатую объектную модель (`Workbook`, `Worksheet`, `Range`), позволяющую копировать данные **включая сводные таблицы, формулы и форматирование** одним вызовом — чего нельзя сделать так же чисто в Apache POI.

---

## Шаг 2: Загрузка исходной книги

Откроем книгу, содержащую данные, которые нужно клонировать. Конструктор `Workbook` принимает путь к файлу, и Aspose загрузит весь файл в память.

```java
import com.aspose.cells.*;

public class CopyWorksheetRange {
    public static void main(String[] args) throws Exception {
        // Load the source workbook containing the data and pivot table
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

*Совет:* оберните загрузку в блок `try‑catch`, если файл может отсутствовать; иначе программа завершится с понятной ошибкой.

---

## Шаг 3: Создание пустой целевой книги

Новая книга — чистый холст. Предзаполнять листы не требуется; Aspose добавит лист автоматически.

```java
        // Create an empty destination workbook
        Workbook destinationWorkbook = new Workbook();
```

Почему не использовать исходную? Разделение предотвращает случайные перезаписи и делает код пригодным для пакетных операций.

---

## Шаг 4: Определение точного диапазона для копирования

Здесь начинается магия **программного копирования диапазона листа**. Мы выбираем ячейки `A1:D20` с первого листа исходного файла. Метод `createRange` возвращает объект `Range`, представляющий именно эти ячейки, включая сводные таблицы.

```java
        // Define the range to copy (A1:D20) from the first worksheet of the source
        Range sourceRange = sourceWorkbook.getWorksheets()
                                          .get(0)               // first sheet (index 0)
                                          .getCells()
                                          .createRange("A1:D20");
```

Если нужен динамический диапазон (например, «последняя используемая строка»), замените жёстко заданный адрес на `Cells.maxDisplayRange` или вычислите его с помощью `Cells.getMaxDataColumn()` и `Cells.getMaxDataRow()`.

---

## Шаг 5: Добавление целевого листа в книгу‑назначение

Aspose создаёт лист по умолчанию с именем «Sheet1» при создании `Workbook`. Добавим новый, чтобы всё было аккуратно, особенно если планируется копировать несколько диапазонов.

```java
        // Add a new worksheet to the destination workbook where the range will be placed
        Worksheet targetWorksheet = destinationWorkbook.getWorksheets().add();
```

Можно задать листу дружелюбное имя:

```java
        targetWorksheet.setName("CopiedData");
```

---

## Шаг 6: Выполнение копирования — включая сводные таблицы

Теперь основная операция: `copyRange`. Этот метод копирует **значения, формулы, форматирование и вложенные объекты** (например, сводные таблицы) из исходного диапазона в целевую ячейку (`A1` на новом листе). Это самый простой способ реализовать **как скопировать диапазон Excel в другую книгу** без низкоуровневых циклов по ячейкам.

```java
        // Copy the defined range (including the pivot table) to cell A1 of the new worksheet
        sourceWorkbook.getWorksheets()
                      .get(0)               // source sheet index
                      .getCells()
                      .copyRange(sourceRange, targetWorksheet, "A1");
```

За кулисами Aspose сериализует исходный диапазон во промежуточный формат, а затем десериализует его в целевой лист — всё остаётся неизменным.

---

## Шаг 7: Сохранение целевой книги и проверка

Наконец, записываем целевую книгу на диск. Откройте `output.xlsx` в Excel, чтобы увидеть скопированный диапазон, сводную таблицу и сохранённое оформление.

```java
        // (Optional) Save the destination workbook to verify the result
        destinationWorkbook.save("YOUR_DIRECTORY/output.xlsx");
        System.out.println("Range copied successfully!");
    }
}
```

При открытии `output.xlsx` вы должны увидеть лист «CopiedData» с тем же макетом, что и `A1:D20` из исходного файла, включая сводную таблицу, теперь ссылающуюся на скопированные данные.

---

## Обработка распространённых граничных случаев

### 1. Копирование между разными версиями Excel
Aspose.Cells работает с `.xls`, `.xlsx`, `.xlsb` и даже `.csv`. Если исходный и целевой форматы различаются, библиотека автоматически их конвертирует. Просто убедитесь, что расширения файлов соответствуют желаемому результату.

### 2. Сохранение внешних источников данных в сводных таблицах
Если сводная таблица в источнике ссылается на внешний источник (например, базу данных), скопированная сводная таблица сохранит строку подключения, но **не обновится автоматически**. Вызовите `pivotTable.refreshData()` после копирования, если нужны актуальные результаты.

```java
        PivotTable pt = targetWorksheet.getPivotTables().get(0);
        pt.refreshData();
        pt.calculateData();
```

### 3. Большие диапазоны и потребление памяти
Копирование огромных диапазонов (сотни тысяч строк) может резко увеличить использование памяти. Перед загрузкой больших файлов используйте `Workbook.setMemorySetting(MemorySetting.MEMORY_PREFERENCE)`, чтобы снизить нагрузку.

### 4. Несколько листов или диапазонов
Если нужно скопировать несколько несмежных диапазонов, повторите шаги 4‑6 для каждого, либо используйте `copyRange` с объединённым диапазоном (`Cells.createRange("A1:B10,C1:D10")`).

---

## Профессиональные советы для надёжной автоматизации

- **Проверяйте исходный диапазон** перед копированием. Используйте `sourceRange.isValid()`, чтобы избежать ошибок во время выполнения.
- **Снимайте блокировку** с целевого файла через `FileInfo.setReadOnly(false)`, если перезаписываете существующую книгу.
- **Ведите журнал действий** лёгким логгером (SLF4J) — особенно полезно при пакетной обработке.
- **Освобождайте книги** (`sourceWorkbook.dispose(); destinationWorkbook.dispose();`) в длительно работающих сервисах, чтобы освободить нативные ресурсы.

---

## Полный рабочий пример

Ниже приведён полностью самодостаточный Java‑класс, который можно вставить в IDE и запустить. Не забудьте заменить `YOUR_DIRECTORY` на реальный путь к папке на вашем компьютере.

```java
import com.aspose.cells.*;

public class CopyWorksheetRange {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load the source workbook containing the data and pivot table
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // 2️⃣ Create an empty destination workbook
        Workbook destinationWorkbook = new Workbook();

        // 3️⃣ Define the range to copy (A1:D20) from the first worksheet of the source
        Range sourceRange = sourceWorkbook.getWorksheets()
                                          .get(0)
                                          .getCells()
                                          .createRange("A1:D20");

        // 4️⃣ Add a new worksheet to the destination workbook where the range will be placed
        Worksheet targetWorksheet = destinationWorkbook.getWorksheets().add();
        targetWorksheet.setName("CopiedData");

        // 5️⃣ Copy the defined range (including the pivot table) to cell A1 of the new worksheet
        sourceWorkbook.getWorksheets()
                      .get(0)
                      .getCells()
                      .copyRange(sourceRange, targetWorksheet, "A1");

        // 6️⃣ (Optional) Save the destination workbook to verify the result
        destinationWorkbook.save("YOUR_DIRECTORY/output.xlsx");

        System.out.println("Programmatically copy worksheet range completed successfully.");
    }
}
```

**Ожидаемый результат:** файл `output.xlsx` с листом «CopiedData». Ячейки `A1:D20` будут точно копировать источник, а любая сводная таблица внутри этого блока будет полностью функционировать, ссылаясь на скопированные данные.

---

## Заключение

Мы продемонстрировали чистое решение **программного копирования диапазона листа** на Java, отвечая на часто задаваемый вопрос **как скопировать диапазон Excel в другую книгу**. Используя высокоуровневый API Aspose.Cells, мы избежали низкоуровневых циклов, сохранили сводные таблицы и оставили код читабельным.

Что дальше? Попробуйте расширить этот шаблон до:

- Копирования целых листов вместо одного диапазона.
- Пакетной обработки десятков книг в папке.
- Экспорта скопированного диапазона в CSV или PDF для конвейеров отчётности.

Экспериментируйте, а при возникновении вопросов оставляйте комментарий. Приятного кодинга!

## Что изучать дальше?

Следующие руководства охватывают тесно связанные темы, расширяющие техники, продемонстрированные в этом руководстве. Каждый ресурс содержит полностью рабочие примеры кода с пошаговыми объяснениями, помогающие освоить дополнительные возможности API и исследовать альтернативные подходы в ваших проектах.

- [Как копировать несколько столбцов в Excel с помощью Aspose.Cells Java: Полное руководство](/cells/english/java/range-management/copy-multiple-columns-excel-aspose-cells-java/)
- [Эффективное копирование столбцов Excel с помощью Aspose.Cells for Java: Полное руководство](/cells/english/java/range-management/copy-excel-columns-aspose-cells-java/)
- [Копирование изображений между листами в Excel с помощью Aspose.Cells for Java: Полное руководство](/cells/english/java/images-shapes/copy-images-between-sheets-excel-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}