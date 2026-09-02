---
date: 2026-09-02
description: Узнайте, как создать водопадную диаграмму Excel в Java с помощью Aspose.Cells,
  задать диапазон данных диаграммы, настроить подписи и экспортировать в XLSX.
keywords:
- create excel waterfall chart
- waterfall chart data labels
- Aspose.Cells Java chart
lastmod: 2026-09-02
linktitle: Водопадные диаграммы
og_description: Создайте водопадную диаграмму Excel с использованием Aspose.Cells
  для Java — задайте диапазон данных диаграммы, добавьте подписи данных и экспортируйте
  в XLSX за несколько шагов.
og_image_alt: 'Tutorial: create excel waterfall chart with Aspose.Cells Java'
og_title: Создать водопадную диаграмму Excel с помощью Aspose.Cells для Java
schemas:
- author: Aspose
  dateModified: '2026-09-02'
  description: Learn how to create excel waterfall chart in Java with Aspose.Cells,
    set the chart data range, customize labels and export to XLSX.
  headline: Create excel waterfall chart with Aspose.Cells for Java
  type: TechArticle
- description: Learn how to create excel waterfall chart in Java with Aspose.Cells,
    set the chart data range, customize labels and export to XLSX.
  name: Create excel waterfall chart with Aspose.Cells for Java
  steps:
  - name: import Aspose.Cells
    text: The `com.aspose.cells` package contains all classes required for Excel manipulation,
      including workbook creation, worksheet handling, and chart generation.
  - name: initialize workbook and worksheet
    text: A **Workbook** represents an Excel file, and a **Worksheet** is a single
      sheet within that file. Creating these objects provides the canvas for both
      raw data and the chart.
  - name: enter data
    text: Column A holds category labels, while column B contains the numeric values
      for the waterfall. This layout matches the typical profit‑and‑loss flow used
      in financial analysis.
  - name: create the waterfall chart
    text: The **Chart** object creates a visual representation; setting its type to
      `ChartType.WATERFALL` configures it as a waterfall chart. Use the `add` method
      to set the chart data range for the series (`"B2:B6"`), and link the category
      axis to `"A2:A6"`.
  - name: save the workbook
    text: Saving the workbook writes the chart and data to the specified file format.
      Call `workbook.save("WaterfallChart.xlsx")` to generate an XLSX file, or change
      the format parameter to export to PDF, CSV, or HTML.
  type: HowTo
- questions:
  - answer: Use the `add` method on the chart’s series, passing the cell range that
      contains your values, e.g., `"B2:B6"`.
    question: How do I set the chart data range for a financial waterfall chart?
  - answer: Yes, call `workbook.save("WaterfallChart.pdf", SaveFormat.PDF);` to generate
      a PDF version.
    question: Can I export the workbook to PDF instead of XLSX?
  - answer: Extend the data range in both the values column and the category column,
      then update the `add` and `setCategoryData` calls accordingly.
    question: What if I need to create a waterfall chart with more categories?
  - answer: Iterate through the `Series` collection and set the `FillFormat` color
      based on each value’s sign; Aspose.Cells lets you apply conditional formatting
      programmatically.
    question: Is there a way to automatically format positive and negative bars?
  - answer: Yes. After modifying cell values, simply re‑save the workbook—the chart
      will reflect the new data automatically.
    question: Does Aspose.Cells support dynamic data updates for charts?
  type: FAQPage
second_title: Aspose.Cells Java Excel Processing API
tags:
- waterfall chart
- Aspose.Cells
- java excel charts
- excel automation
title: Создать водопадную диаграмму Excel с помощью Aspose.Cells для Java
url: /ru/java/advanced-excel-charts/waterfall-charts/
weight: 18
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Водопадные диаграммы

## Введение в водопадные диаграммы с использованием Aspose.Cells for Java

В этом руководстве вы узнаете, как **create excel waterfall chart** и **set chart data range** с помощью Aspose.Cells for Java. Водопадные диаграммы превращают серию положительных и отрицательных чисел в наглядную визуальную историю, делая их идеальными для финансовой отчётности, обзоров продаж и любых сценариев, где необходимо увидеть, как отдельные элементы вносят вклад в общий итог.

## Быстрые ответы
- **What is a waterfall chart?** Визуализация, показывающая, как начальное значение увеличивается и уменьшается серией промежуточных значений, завершаясь конечным итогом.  
- **Which library is used?** Aspose.Cells for Java.  
- **Do I need a license?** Бесплатная пробная версия подходит для разработки; для продакшн‑использования требуется коммерческая лицензия.  
- **Can I save the file as XLSX?** Да – используйте `workbook.save("FileName.xlsx")`.  
- **Is it suitable for Java data visualization?** Абсолютно; Aspose.Cells предоставляет богатые возможности построения диаграмм без установки Office.

## Что такое водопадная диаграмма?
Водопадная диаграмма отображает последовательные положительные и отрицательные вклады в начальное значение, помогая понять, как каждый компонент влияет на общий результат. Визуализируя приросты и убытки рядом, она делает сложные финансовые потоки мгновенно читаемыми.

## Почему использовать Aspose.Cells for Java для добавления водопадной диаграммы?
Aspose.Cells позволяет генерировать Excel‑диаграммы на любом сервере, в CI‑конвейере или на рабочем столе без необходимости установки Microsoft Excel. Он поддерживает **15+ форматов вывода** (XLSX, PDF, HTML, CSV и др.), обрабатывает книги с **500+ строками** менее чем за секунду и предоставляет программный контроль над каждым элементом диаграммы — от цветов до подписей данных.

## Предварительные требования

Прежде чем погрузиться в код, убедитесь, что у вас есть следующие требования:

- Aspose.Cells for Java: Вам потребуется установить Aspose.Cells for Java. Скачать его можно со страницы релизов Aspose.Cells for Java: [Aspose.Cells for Java releases](https://releases.aspose.com/cells/java/).
- Среда разработки Java: Убедитесь, что Java установлена в вашей системе и готов инструмент сборки (Maven/Gradle).

Теперь давайте начнём создание водопадной диаграммы шаг за шагом.

## Как установить диапазон данных диаграммы для водопадной диаграммы в Java
Загрузите новую книгу, заполните её данными, добавьте объект `Chart`, определите диапазон серии и, наконец, сохраните файл. Этот процесс прост: вы создаёте книгу, заполняете ячейки категориями и значениями, создаёте диаграмму, привязываете диапазоны данных и экспортируете книгу. В результате получаем полностью функционирующую водопадную диаграмму, готовую к использованию в отчётах или дашбордах.

### Шаг 1: импорт Aspose.Cells
Пакет `com.aspose.cells` содержит все классы, необходимые для работы с Excel, включая создание книг, работу с листами и генерацию диаграмм.

### Шаг 2: инициализация Workbook и Worksheet
**Workbook** представляет файл Excel, а **Worksheet** — отдельный лист внутри этого файла. Создание этих объектов обеспечивает холст как для исходных данных, так и для диаграммы.

### Шаг 3: ввод данных
Столбец A содержит метки категорий, а столбец B — числовые значения для водопадной диаграммы. Такая раскладка соответствует типичному потоку прибыли‑убытка, используемому в финансовом анализе.

### Шаг 4: создание водопадной диаграммы
Объект **Chart** создаёт визуальное представление; установка его типа в `ChartType.WATERFALL` конфигурирует его как водопадную диаграмму. Используйте метод `add` для задания диапазона данных серии (`"B2:B6"`), а также привяжите ось категорий к `"A2:A6"`.

### Шаг 5: сохранение Workbook
Сохранение книги записывает диаграмму и данные в указанный формат файла. Вызов `workbook.save("WaterfallChart.xlsx")` генерирует файл XLSX, либо измените параметр формата для экспорта в PDF, CSV или HTML.

## Распространённые проблемы и решения

- **Chart appears blank** – Убедитесь, что ссылки на диапазоны данных (`B2:B6` и `A2:A6`) соответствуют фактическим ячейкам, содержащим ваши значения и категории.  
- **Negative values not displayed correctly** – Проверьте, что тип серии установлен в `ChartType.WATERFALL`; другие типы диаграмм обрабатывают отрицательные значения иначе.  
- **File not opening in Excel** – Используйте последнюю версию Aspose.Cells и убедитесь, что расширение файла соответствует формату (`.xlsx` для Excel).

## Часто задаваемые вопросы

### Как я могу настроить внешний вид моей водопадной диаграммы?
Вы можете изменить свойства, например `Chart.getSeries().get(0).getFillFormat().setColor(Color.getRed())`, чтобы изменить цвет столбцов, включить подписи данных с `setShowDataLabels(true)` и настроить названия осей через `getCategoryAxis().setTitle("Stage")`. Справочник API Aspose.Cells содержит полный список настраиваемых опций.

### Могу ли я создать несколько водопадных диаграмм на одном листе?
Да. После добавления первой диаграммы повторите шаги создания диаграммы с другим диапазоном данных и новым объектом `Chart`. Каждая диаграмма независима и может быть размещена в любой части листа.

### Совместима ли Aspose.Cells с различными средами разработки Java?
Абсолютно. Библиотека работает в Eclipse, IntelliJ IDEA, NetBeans и любой системе сборки, поддерживающей Maven или Gradle. Дополнительные плагины не требуются.

### Могу ли я добавить дополнительные серии данных в мою водопадную диаграмму?
Вы можете добавить новые серии, вызвав `chart.getNSeries().add("C2:C6", true)` и настроив каждую серию отдельно. Это позволяет сравнивать несколько сценариев рядом.

### Где я могу найти больше ресурсов и примеров для Aspose.Cells for Java?
Изучите полную документацию в справочнике API Aspose.Cells Java: [Aspose.Cells Java API reference](https://reference.aspose.com/cells/java/).

## Часто задаваемые вопросы

**Q: Как установить диапазон данных диаграммы для финансовой водопадной диаграммы?**  
A: Используйте метод `add` у серии диаграммы, передавая диапазон ячеек, содержащий ваши значения, например `"B2:B6"`.

**Q: Можно ли экспортировать книгу в PDF вместо XLSX?**  
A: Да, вызовите `workbook.save("WaterfallChart.pdf", SaveFormat.PDF);` для создания PDF‑версии.

**Q: Что делать, если нужно создать водопадную диаграмму с большим числом категорий?**  
A: Расширьте диапазон данных в обоих столбцах (значения и категории), затем обновите вызовы `add` и `setCategoryData` соответственно.

**Q: Есть ли способ автоматически форматировать положительные и отрицательные столбцы?**  
A: Пройдитесь по коллекции `Series` и задайте цвет `FillFormat` в зависимости от знака значения; Aspose.Cells позволяет программно применять условное форматирование.

**Q: Поддерживает ли Aspose.Cells динамические обновления данных для диаграмм?**  
A: Да. После изменения значений ячеек просто сохраните книгу — диаграмма автоматически отобразит новые данные.

---

**Last Updated:** 2026-09-02  
**Tested with:** Aspose.Cells for Java (latest)  
**Author:** Aspose  









```java
import com.aspose.cells.*;
```

```java
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.getWorksheets().get(0);
```

```java
Cells cells = worksheet.getCells();

// Insert data
cells.get("A1").putValue("Categories");
cells.get("A2").putValue("Start");
cells.get("A3").putValue("Positive Value 1");
cells.get("A4").putValue("Negative Value 1");
cells.get("A5").putValue("Positive Value 2");
cells.get("A6").putValue("End");

cells.get("B1").putValue("Values");
cells.get("B2").putValue(0);
cells.get("B3").putValue(20);
cells.get("B4").putValue(-10);
cells.get("B5").putValue(15);
cells.get("B6").putValue(25);
```

```java
int chartIndex = worksheet.getCharts().add(ChartType.WATERFALL, 5, 0, 15, 5);
Chart waterfallChart = worksheet.getCharts().get(chartIndex);
waterfallChart.getNSeries().add("B2:B6", true);
waterfallChart.getNSeries().setCategoryData("A2:A6");
```

```java
workbook.save("WaterfallChart.xlsx");
```

## Связанные руководства

- [Настройка подписей данных в диаграммах Excel с помощью Aspose.Cells for Java: пошаговое руководство](/cells/java/charts-graphs/customize-chart-data-labels-aspose-cells-java/)
- [Добавление подписей данных к диаграмме Excel с Aspose.Cells Java](/cells/java/advanced-excel-charts/chart-interactivity/)
- [Как создавать и экспортировать диаграммы в Java с помощью Aspose.Cells: полное руководство](/cells/java/charts-graphs/aspose-cells-java-create-export-charts/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}