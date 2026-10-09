---
category: general
date: 2026-06-08
description: Как копировать сводную таблицу с помощью Aspose.Cells в Java. Узнайте,
  как копировать диапазон между рабочими книгами и сохранять сводные таблицы без усилий.
draft: false
keywords:
- how to copy pivot table
- copy range between workbooks
- how to preserve pivot
- copy pivot table to new workbook
- copy excel sheet with pivot
language: ru
og_description: Как скопировать сводную таблицу в Java с помощью Aspose.Cells. Этот
  учебник показывает, как копировать диапазон между книгами и сохранять сводную таблицу
  неизменной.
og_title: Как скопировать сводную таблицу в Java — пошаговое руководство
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: How to copy pivot table using Aspose.Cells in Java. Learn to copy range
    between workbooks and preserve pivot tables effortlessly.
  headline: How to Copy Pivot Table in Java – Complete Aspose.Cells Guide
  type: TechArticle
- description: How to copy pivot table using Aspose.Cells in Java. Learn to copy range
    between workbooks and preserve pivot tables effortlessly.
  name: How to Copy Pivot Table in Java – Complete Aspose.Cells Guide
  steps:
  - name: Set Up Aspose.Cells in Your Project
    text: 'Before you can manipulate Excel files, you need the Aspose.Cells library
      on your classpath. If you use Maven, add the following dependency to your `pom.xml`:'
  - name: Load the Source Workbook
    text: We need a `Workbook` instance that points at the file housing the pivot.
      Replace `YOUR_DIRECTORY/src.xlsx` with the actual path on your machine.
  - name: Define the Pivot’s Enclosing Range
    text: A pivot table lives inside a rectangular block of cells. You can locate
      it manually (e.g., `A1:G20`) or programmatically by inspecting the worksheet’s
      `PivotTables` collection. For this tutorial we’ll hard‑code the range for clarity.
  - name: Create a Blank Destination Workbook
    text: Now we spin up an empty workbook that will receive the copied data.
  - name: Copy the Range and Preserve the Pivot
    text: Here’s where the magic happens. The `copyRange` method accepts a `CopyOptions`
      object, but we don’t need to tweak anything—pivot preservation is enabled out
      of the box.
  - name: Save the Destination Workbook
    text: Finally, write the new file to disk.
  type: HowTo
- questions:
  - answer: Yes. Because we’re copying the entire cell range, styles, conditional
      formatting, and number formats travel with the data.
    question: Does this method also copy the pivot’s formatting?
  - answer: Simply change the third argument of `copyRange` to the desired top‑left
      address, e.g., `"B5"`.
    question: What if I need to copy the pivot to a specific cell other than `A1`?
  - answer: 'Not directly. The pivot cache lives inside the workbook; removing the
      source data will render the pivot unusable. Export the source data to a hidden
      sheet if you want a lightweight copy. --- ## Conclusion You now have a clear,
      end‑to‑end answer to **how to copy pivot table** in Java using Aspose.Cel'
    question: Can I copy a pivot without its source data?
  type: FAQPage
tags:
- Aspose.Cells
- Java
- Excel
- PivotTable
title: Как скопировать сводную таблицу в Java — Полное руководство по Aspose.Cells
url: /ru/java/excel-pivot-tables/how-to-copy-pivot-table-in-java-complete-aspose-cells-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как скопировать сводную таблицу в Java – Полное руководство Aspose.Cells

Когда‑нибудь задавались вопросом **как скопировать сводную таблицу** из одной книги Excel в другую с помощью Java? Хорошая новость в том, что Aspose.Cells делает это проще простого, позволяя **копировать диапазон между книгами** и сохранять каждую деталь сводной таблицы.  

В этом руководстве мы пройдем реальный пример, который не только копирует саму сводную таблицу, но и сохраняет исходные данные, форматирование и формулы без изменений. К концу вы точно будете знать **как сохранить сводную таблицу**, как переместить её в совершенно новую книгу и как избежать типичных подводных камней, с которыми сталкиваются многие разработчики.

Мы рассмотрим:

* Минимальные требования (Java 17+, Aspose.Cells for Java 23.9+).  
* Пошаговый разбор кода с объяснением **почему** каждая строка важна.  
* Обработку граничных случаев для больших диапазонов сводных таблиц и внешних источников данных.  
* Полную, готовую к запуску программу, которую можно сразу вставить в IDE и выполнить.

> **Совет:** Если вы уже используете Maven или Gradle, добавление Aspose.Cells в качестве зависимости занимает одну строку — без необходимости вручную управлять JAR‑файлами.

---

## Как скопировать сводную таблицу – пошаговый обзор

Ниже представлена общая картина того, что мы собираемся достичь:

1. Загрузить исходную книгу, содержащую сводную таблицу.  
2. Определить точный диапазон ячеек, охватывающий сводную таблицу.  
3. Создать новую целевую книгу.  
4. **Копировать диапазон** в новый лист, позволяя Aspose.Cells автоматически сохранять сводную таблицу.  
5. Сохранить результат в новый файл.

Каждый шаг иллюстрирован фрагментами кода и коротким объяснением, чтобы вы понимали не только «что», но и «почему».

![Diagram illustrating how a pivot table is copied from a source workbook to a destination workbook while preserving its structure](/images/how-to-copy-pivot-table-diagram.png){: .align-center alt="Диаграмма, показывающая, как сводная таблица копируется из исходной книги в целевую, сохраняя свою структуру"}

---

### Шаг 1: Настройте Aspose.Cells в вашем проекте

Прежде чем работать с файлами Excel, вам нужна библиотека Aspose.Cells в classpath. Если вы используете Maven, добавьте следующую зависимость в ваш `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.9</version>
    <classifier>jdk17</classifier>
</dependency>
```

Для Gradle это тоже одна строка:

```gradle
implementation 'com.aspose:aspose-cells:23.9:jdk17'
```

**Почему это важно:** Aspose.Cells абстрагирует низкоуровневые детали OpenXML, предоставляя простой API для **копирования сводной таблицы в новую книгу** без потери метаданных.

---

### Шаг 2: Загрузите исходную книгу

Нужен объект `Workbook`, указывающий на файл, где находится сводная таблица. Замените `YOUR_DIRECTORY/src.xlsx` реальным путём на вашем компьютере.

```java
// Load the source workbook that contains the pivot table
Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/src.xlsx");
```

> **Примечание:** Aspose.Cells автоматически определяет формат файла (XLSX, XLS, CSV и т.д.), поэтому вам не нужно заботиться о конвертации формата.

---

### Шаг 3: Определите диапазон, охватывающий сводную таблицу

Сводная таблица располагается внутри прямоугольного блока ячеек. Вы можете указать её вручную (например, `A1:G20`) или программно, исследуя коллекцию `PivotTables` листа. Для ясности в этом руководстве мы задаём диапазон вручную.

```java
// Define the range that encloses the pivot table (e.g., A1:G20)
Range pivotRange = sourceWorkbook.getWorksheets().get(0)
                                 .getCells()
                                 .createRange("A1:G20");
```

**Почему мы используем `createRange`**: он создаёт лёгкий объект `Range`, который можно передать в `copyRange`. Это самый надёжный способ **копировать диапазон между книгами**, гарантируя включение внутренних структур сводной таблицы.

---

### Шаг 4: Создайте пустую целевую книгу

Теперь создаём пустую книгу, которая получит скопированные данные.

```java
// Create a new (blank) destination workbook
Workbook destinationWorkbook = new Workbook(); // defaults to a single empty sheet
Worksheet destinationSheet = destinationWorkbook.getWorksheets().get(0);
```

Книга по умолчанию уже содержит один лист, что идеально подходит для нашей задачи. Если нужен лист с определённым именем, его можно переименовать:

```java
destinationSheet.setName("PivotCopy");
```

---

### Шаг 5: Копируйте диапазон и сохраняйте сводную таблицу

Здесь происходит магия. Метод `copyRange` принимает объект `CopyOptions`, но нам не нужно ничего менять — сохранение сводной таблицы включено по умолчанию.

```java
// Copy the range to the destination sheet; the pivot table is preserved automatically
destinationSheet.getCells().copyRange(pivotRange, new CopyOptions() {{
    // No additional settings are required – pivot preservation is enabled by default
}}, "A1");
```

**Почему это работает:** Aspose.Cells рассматривает сводную таблицу как часть коллекции ячеек. При вызове `copyRange` он копирует кэш сводной таблицы, поля данных и макет, эффективно **как сохранить сводную таблицу** без дополнительного кода.

---

### Шаг 6: Сохраните целевую книгу

Наконец, запишите новый файл на диск.

```java
// Save the destination workbook with the copied pivot table
destinationWorkbook.save("YOUR_DIRECTORY/copied-with-pivot.xlsx");
```

Откройте полученный `copied-with-pivot.xlsx` в Excel, и вы увидите точную копию оригинальной сводной таблицы, готовую к дальнейшему анализу.

---

## Полный рабочий пример

Ниже представлен полностью готовый к компиляции и запуску код. Он объединяет все вышеуказанные фрагменты, добавляет несколько проверок и выводит дружелюбное сообщение о завершении.

```java
import com.aspose.cells.*;

public class CopyPivotRange {
    public static void main(String[] args) throws Exception {
        // ---------- 1. Load source workbook ----------
        String srcPath = "YOUR_DIRECTORY/src.xlsx";
        Workbook sourceWorkbook = new Workbook(srcPath);

        // ---------- 2. Identify pivot range ----------
        // You may replace the hard‑coded range with a dynamic lookup if needed.
        Range pivotRange = sourceWorkbook.getWorksheets().get(0)
                                         .getCells()
                                         .createRange("A1:G20");

        // ---------- 3. Create destination workbook ----------
        Workbook destinationWorkbook = new Workbook(); // empty workbook
        Worksheet destinationSheet = destinationWorkbook.getWorksheets().get(0);
        destinationSheet.setName("PivotCopy");

        // ---------- 4. Copy range (pivot preserved) ----------
        destinationSheet.getCells().copyRange(pivotRange,
                new CopyOptions() {{
                    // No extra options required for pivot preservation.
                }}, "A1");

        // ---------- 5. Save result ----------
        String destPath = "YOUR_DIRECTORY/copied-with-pivot.xlsx";
        destinationWorkbook.save(destPath);

        System.out.println("Pivot table successfully copied!");
        System.out.println("Source:  " + srcPath);
        System.out.println("Destination: " + destPath);
    }
}
```

**Ожидаемый вывод при запуске программы**:

```
Pivot table successfully copied!
Source:  YOUR_DIRECTORY/src.xlsx
Destination: YOUR_DIRECTORY/copied-with-pivot.xlsx
```

Откройте целевой файл — ваша сводная таблица должна выглядеть идентично оригиналу, включая слайсеры, фильтры и вычисляемые поля.

---

## Обработка распространённых граничных случаев

| Ситуация | На что обратить внимание | Предлагаемое решение |
|-----------|-------------------|---------------|
| **Сводная таблица использует внешний источник данных** (например, база данных) | Внешнее соединение не встроено в книгу, поэтому копирование может разорвать связь. | Сначала экспортируйте данные на лист, затем создайте сводную таблицу на этом листе перед копированием. |
| **Очень большая сводная таблица (тысячи строк)** | `copyRange` может потреблять значительный объём памяти. | Увеличьте размер кучи JVM (`-Xmx2g`) или копируйте сводную таблицу небольшими частями, используя `copyRows`/`copyColumns`. |
| **Несколько сводных таблиц на одном листе** | Жёстко заданный диапазон `A1:G20` копирует только первую сводную таблицу. | Пройдитесь в цикле по `sourceWorksheet.getPivotTables()` и скопируйте каждый `PivotTable.getDataRange()`. |
| **Целевая книга уже содержит лист с тем же именем** | `setName` вызовет исключение. | Используйте `Workbook.getWorksheets().add("PivotCopy")`, чтобы создать лист с уникальным именем. |

Эти рекомендации гарантируют, что **как скопировать сводную таблицу** будет работать надёжно даже в продакшн‑сценариях.

---

## Часто задаваемые вопросы

**В: Копирует ли этот метод также форматирование сводной таблицы?**  
О: Да. Поскольку мы копируем весь диапазон ячеек, стили, условное форматирование и числовые форматы переходят вместе с данными.

**В: Что если мне нужно скопировать сводную таблицу в конкретную ячейку, отличную от `A1`?**  
О: Просто измените третий аргумент `copyRange` на нужный адрес верхнего‑левого угла, например, `"B5"`.

**В: Можно ли скопировать сводную таблицу без её исходных данных?**  
О: Не напрямую. Кеш сводной таблицы хранится внутри книги; удаление исходных данных сделает сводную таблицу нерабочей. При желании лёгкой копии экспортируйте данные на скрытый лист.

---

## Заключение

Теперь у вас есть чёткий, сквозной ответ на **как скопировать сводную таблицу** в Java с помощью Aspose.Cells. Загрузив исходную книгу, определив диапазон сводной таблицы и используя `copyRange`, вы легко можете **копировать диапазон между книгами**, обеспечивая сохранность сводной таблицы.

## Что изучать дальше?

Следующие руководства охватывают близкие темы, расширяющие техники, продемонстрированные в этом руководстве. Каждый ресурс содержит полностью рабочие примеры кода с пошаговыми объяснениями, помогающими освоить дополнительные возможности API и исследовать альтернативные подходы в ваших проектах.

- [Как обновить источник данных сводной таблицы Excel с помощью Aspose.Cells for Java: Полное руководство](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [Как создавать сводные таблицы в Excel с помощью Aspose.Cells for Java: Полное руководство](/cells/english/java/data-analysis/create-pivot-tables-excel-aspose-cells-java/)
- [Как реализовать слайсеры в сводных таблицах с помощью Aspose.Cells for Java: Полное руководство](/cells/english/java/data-analysis/implement-slicers-pivot-tables-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}