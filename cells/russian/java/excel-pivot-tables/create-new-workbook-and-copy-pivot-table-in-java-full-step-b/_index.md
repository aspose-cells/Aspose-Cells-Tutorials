---
category: general
date: 2026-07-16
description: Создайте новую книгу и скопируйте сводную таблицу с помощью Aspose.Cells
  для Java. Узнайте, как за считанные минуты дублировать сводную таблицу и копировать
  диапазон Excel.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create new workbook
- copy pivot table
- duplicate pivot table
- how to copy pivot
- copy excel range
language: ru
lastmod: 2026-07-16
og_description: Создайте новую книгу и скопируйте сводную таблицу с помощью Aspose.Cells
  для Java. Это руководство показывает, как эффективно дублировать сводную таблицу
  и копировать диапазон Excel.
og_image_alt: Screenshot of Java code that creates a new workbook and copies a pivot
  table using Aspose.Cells
og_title: Создать новую книгу и скопировать сводную таблицу в Java – Полный учебник
schemas:
- author: Aspose
  dateModified: '2026-07-16'
  description: Create new workbook and copy pivot table using Aspose.Cells for Java.
    Learn how to duplicate pivot table and copy Excel range in minutes.
  headline: Create New Workbook and Copy Pivot Table in Java – Full Step‑by‑Step Guide
  type: TechArticle
- description: Create new workbook and copy pivot table using Aspose.Cells for Java.
    Learn how to duplicate pivot table and copy Excel range in minutes.
  name: Create New Workbook and Copy Pivot Table in Java – Full Step‑by‑Step Guide
  steps:
  - name: What if the source pivot spans more than one sheet?
    text: Aspose.Cells can only copy ranges within a single worksheet at a time. If
      your pivot stretches across sheets, you’ll need to copy each relevant range
      separately and then re‑link them manually.
  - name: Does this method preserve custom number formats?
    text: Yes. The `copy` method copies cell styles, including number formats, fonts,
      and colors. However, if you have conditional formatting that references external
      ranges, double‑check those references after the copy.
  - name: How to copy a pivot that uses an external data source?
    text: When the pivot pulls data from an external connection (e.g., a SQL query),
      the connection information is **not** transferred by `copy`. You’ll need to
      recreate the data source in the destination workbook or embed the source data
      beforehand.
  - name: Can I copy only the pivot layout without the underlying data?
    text: You can achieve that by first clearing the data cells in the source range,
      then copying only the pivot’s layout. This is a more advanced scenario and usually
      not required for a simple **duplicate pivot table** task.
  type: HowTo
tags:
- Java
- Aspose.Cells
- Excel Automation
title: Создание новой книги и копирование сводной таблицы в Java – полное пошаговое
  руководство
url: /ru/java/excel-pivot-tables/create-new-workbook-and-copy-pivot-table-in-java-full-step-b/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Создание новой книги и копирование сводной таблицы в Java – Полное пошаговое руководство

Вы когда‑нибудь задумывались, как **create new workbook**, сохраняя сложную сводную таблицу из существующего файла? Если вы когда‑то уставились на лист Excel, подумали «Мне нужна эта сводка в другой книге», и потом почесали голову, вы не одиноки. Хорошая новость в том, что с Aspose.Cells for Java вы можете дублировать сводную таблицу всего в нескольких строках кода.

В этом руководстве мы пройдем все шаги по **copy pivot table** данным, **duplicate pivot table** структурам и содержимому **copy Excel range** — всё это при создании новой книги с нуля. К концу вы получите готовую к запуску программу на Java, которая делает именно то, что вы просили.

## Что вы узнаете

- Как программно **create new workbook** с помощью Aspose.Cells.
- Точный способ определить диапазон, содержащий сводную таблицу.
- Приёмы для **copy pivot table** и **duplicate pivot table** без потери форматирования или соединений данных.
- Как эффективно **copy Excel range** и сохранить результат.
- Распространённые подводные камни и советы по работе с большими сводными таблицами.

No external references needed—everything is self‑contained, runnable, and explained.

---

## Требования

1. **Java Development Kit (JDK) 11+** – любая современная версия подойдет.  
2. **Aspose.Cells for Java** library (последняя версия на 2026‑07‑16). Вы можете получить её из Maven Central:

   ```xml
   <dependency>
       <groupId>com.aspose</groupId>
       <artifactId>aspose-cells</artifactId>
       <version>23.12</version>
   </dependency>
   ```

3. Исходный файл Excel (`SourceWithPivot.xlsx`), уже содержащий сводную таблицу, которую нужно скопировать.  
4. IDE или простой текстовый редактор — подойдут IntelliJ IDEA, Eclipse или VS Code.

Все готово? Отлично — поехали.

---

## Шаг 1: **Create New Workbook** и загрузка исходного файла

Первое, что нам нужно, — это новый объект книги, который в дальнейшем будет содержать дублированную сводную таблицу. Одновременно необходимо загрузить оригинальную книгу, чтобы иметь доступ к диапазону её сводной таблицы.

```java
import com.aspose.cells.*;

public class CopyPivotTableDemo {
    public static void main(String[] args) throws Exception {
        // Load the source workbook that already contains the pivot table
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/SourceWithPivot.xlsx");
        // Grab the first worksheet where the pivot lives
        Worksheet srcWs = srcWb.getWorksheets().get(0);
```

> **Почему это важно:**  
> Загрузка исходной книги дает доступ к базовому объекту `Range`, который охватывает сводную таблицу. Если пропустить этот шаг, нечего будет копировать, и операция **duplicate pivot table** завершится без ошибок, но без результата.

---

## Шаг 2: Определите **Copy Excel Range**, содержащий сводную таблицу

Сводная таблица — это не одна ячейка, а прямоугольный блок. Нам нужно точно указать Aspose.Cells, какие ячейки копировать.

```java
        // Define the cell range that includes the pivot table (adjust as needed)
        Range srcRange = srcWs.getCells().createRange("A1:G20");
```

> **Подсказка:**  
> Если вы не уверены в точном диапазоне, откройте исходную книгу в Excel, выделите сводную таблицу и посмотрите в поле имени. Там будет что‑то вроде `A1:G20`. Использование точного диапазона гарантирует, что все настройки полей, фильтры и вычисления сохранятся при последующем **copy pivot table**.

---

## Шаг 3: **Create New Workbook**, получающая скопированную сводную таблицу

Теперь мы создаём совершенно новую книгу — здесь будет размещена наша **duplicate pivot table**.

```java
        // Create a completely empty workbook for the destination
        Workbook dstWb = new Workbook(); // this automatically creates one empty worksheet
        Worksheet dstWs = dstWb.getWorksheets().get(0);
```

> **Что происходит под капотом?**  
> Конструктор по умолчанию создаёт книгу с одним пустым листом. Это чистый холст, необходимый для сценария **create new workbook**. Нет оставшихся стилей или скрытых листов, о которых нужно беспокоиться.

---

## Шаг 4: **Copy Pivot Table** — фактическое копирование определённого диапазона Excel

Когда исходный и целевой файлы готовы, мы выполняем операцию копирования. Этот шаг решает часть задачи **how to copy pivot**.

```java
        // Copy the defined range (which includes the pivot) to the destination worksheet
        srcRange.copy(dstWs.getCells().createRange("A1"));
```

> **Почему `copy` работает со сводными:**  
> Aspose.Cells рассматривает сводную таблицу как часть коллекции ячеек. При копировании диапазона переносится кэш сводной, список полей и макет. В результате в новой книге появляется полностью функционирующая **duplicate pivot table**.

---

## Шаг 5: Сохраните результат и проверьте операцию **Copy Pivot Table**

Наконец, сохраняем целевую книгу на диск. Откройте файл в Excel, чтобы убедиться, что сводная таблица выглядит точно так же, как в исходном файле.

```java
        // Save the destination workbook with the duplicated pivot table
        dstWb.save("YOUR_DIRECTORY/CopyPivotResult.xlsx");
    }
}
```

**Ожидаемый результат:**  
- `CopyPivotResult.xlsx` открывается с листом, содержащим ту же сводную таблицу, что и в `SourceWithPivot.xlsx`.  
- Все подписи строк/столбцов, фильтры и вычисляемые поля сохранены.  
- Теперь вы можете изменять исходные данные независимо, а новая книга будет иметь собственный кэш сводной таблицы.

---

## Особые случаи и часто задаваемые вопросы

### Что делать, если исходная сводная таблица охватывает более одного листа?
Aspose.Cells может копировать диапазоны только внутри одного листа за раз. Если ваша сводная таблица растягивается на несколько листов, вам придётся копировать каждый соответствующий диапазон отдельно, а затем вручную связать их.

### Сохраняет ли этот метод пользовательские числовые форматы?
Да. Метод `copy` копирует стили ячеек, включая числовые форматы, шрифты и цвета. Однако если у вас есть условное форматирование, ссылающееся на внешние диапазоны, проверьте эти ссылки после копирования.

### Как скопировать сводную, использующую внешний источник данных?
Когда сводная таблица получает данные из внешнего соединения (например, SQL‑запроса), информация о соединении **не** переносится методом `copy`. Вам потребуется заново создать источник данных в целевой книге или предварительно встроить исходные данные.

### Можно ли скопировать только макет сводной без исходных данных?
Это можно сделать, предварительно очистив ячейки данных в исходном диапазоне, а затем скопировав только макет сводной. Это более продвинутый сценарий и обычно не требуется для простой задачи **duplicate pivot table**.

---

## Полный рабочий пример (все шаги вместе)

Ниже приведён полностью готовый к запуску Java‑класс. Просто замените `YOUR_DIRECTORY` на реальный путь к папке на вашем компьютере.

```java
import com.aspose.cells.*;

public class CopyPivotTableDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Load the source workbook containing the pivot table
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/SourceWithPivot.xlsx");
        Worksheet srcWs = srcWb.getWorksheets().get(0);

        // Step 2: Define the exact range that holds the pivot table
        // Adjust "A1:G20" to match your pivot's size
        Range srcRange = srcWs.getCells().createRange("A1:G20");

        // Step 3: Create a brand‑new workbook that will receive the copy
        Workbook dstWb = new Workbook(); // creates an empty workbook with one sheet
        Worksheet dstWs = dstWb.getWorksheets().get(0);

        // Step 4: Copy the pivot (and any surrounding data) to the new workbook
        srcRange.copy(dstWs.getCells().createRange("A1"));

        // Step 5: Save the destination file – now it contains the duplicated pivot table
        dstWb.save("YOUR_DIRECTORY/CopyPivotResult.xlsx");

        System.out.println("Pivot table copied successfully! Check CopyPivotResult.xlsx.");
    }
}
```

Запустите программу (`java CopyPivotTableDemo`), и вы увидите сообщение в консоли, подтверждающее успех.

---

## Профессиональные советы и лучшие практики

- **Validate the range** перед копированием. Используйте `srcWs.getCells().maxDisplayRange`, чтобы программно определить используемую область, если не хотите жёстко задавать `"A1:G20"`.
- **Turn off calculation** временно для огромных книг, чтобы ускорить копирование:

  ```java
  srcWb.getSettings().setCalculateFormulaOnOpen(false);
  ```

- **Dispose of resources** (`srcWb.dispose(); dstWb.dispose();`) в длительно работающих сервисах, чтобы избежать утечек памяти.
- **Version compatibility:** Код работает с Aspose.Cells 23.12 и новее. В более старых версиях может потребоваться `srcRange.copyTo` вместо `copy`.

---

## Следующие шаги

Теперь, когда вы освоили **create new workbook** и **copy pivot table**, вы можете изучить:

- **How to copy pivot** across multiple worksheets in a batch job.
- Adding **copy excel range** for regular data tables alongside the pivot.
- Automating **duplicate pivot table** creation for each month’s report using a loop.
- Exporting the duplicated pivot to PDF or HTML with Aspose.Cells’ built‑in renderers.

---

## Заключение

Мы прошли весь процесс **create new workbook**, определили исходный **copy excel range** и **copy pivot table**, чтобы получить **duplicate pivot table** в Java с использованием Aspose.Cells. Решение краткое, полностью работоспособное и готово к использованию в продакшене. Не стесняйтесь менять диапазон, экспериментировать с разными исходными файлами или внедрять эту логику в более крупный конвейер отчётности.

Если вы столкнётесь с проблемами или у вас есть идеи по расширению этого руководства, оставьте комментарий ниже. Happy coding!

## Что вам стоит изучить дальше?

Следующие руководства охватывают тесно связанные темы, построенные на техниках, продемонстрированных в этом пособии. Каждый ресурс включает полные рабочие примеры кода с пошаговыми объяснениями, помогающими освоить дополнительные возможности API и исследовать альтернативные подходы к реализации в ваших проектах.

- [How to Create Pivot Tables in Excel Using Aspose.Cells for Java&#58; A Comprehensive Guide](/cells/english/java/data-analysis/create-pivot-tables-excel-aspose-cells-java/)
- [How to Update Excel Pivot Table Source with Aspose.Cells for Java&#58; A Comprehensive Guide](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [Excel Pivot Table Manipulation with Aspose.Cells Java&#58; A Comprehensive Guide](/cells/english/java/data-analysis/excel-pivot-table-manipulation-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}