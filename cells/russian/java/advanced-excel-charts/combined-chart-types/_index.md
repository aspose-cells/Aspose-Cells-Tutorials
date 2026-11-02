---
date: 2026-09-02
description: Узнайте, как экспортировать диаграмму в PNG, добавить серию данных, объединить
  line column chart, сохранить рабочую книгу как XLSX и добавить legend chart с помощью
  Aspose.Cells for Java.
keywords:
- export chart to png
- combine line and column chart
- save workbook as xlsx
- generate chart image java
lastmod: 2026-09-02
linktitle: Экспорт диаграммы в PNG и добавление серии данных для combined chart
og_description: Экспорт диаграммы в PNG с Aspose.Cells for Java, объединение line
  and column chart, добавление серии данных и сохранение рабочей книги как XLSX в
  одном руководстве.
og_image_alt: Developer guide showing combined line‑column chart export to PNG using
  Aspose.Cells for Java
og_title: Экспорт диаграммы в PNG и добавление серии данных для combined chart
schemas:
- author: Aspose
  dateModified: '2026-09-02'
  description: Learn how to export chart to PNG, add data series, combine line column
    chart, save workbook as XLSX and add legend chart using Aspose.Cells for Java.
  headline: Export chart to PNG and add data series for combined chart
  type: TechArticle
- description: Learn how to export chart to PNG, add data series, combine line column
    chart, save workbook as XLSX and add legend chart using Aspose.Cells for Java.
  name: Export chart to PNG and add data series for combined chart
  steps:
  - name: import aspose.cells classes
    text: '`Workbook` is Aspose.Cells’ core object that represents an entire Excel
      file in memory.'
  - name: create a new workbook
    text: '`Worksheet` represents a single sheet inside a `Workbook` and provides
      access to cells, rows, and charts.'
  - name: access the first worksheet
    text: '`Chart` is the object that holds all chart‑related settings, series, and
      rendering options.'
  - name: add a combined chart object to the worksheet
    text: We’ll start with a line chart and later add a column series to achieve a
      **combined line column chart** effect.
  - name: define the data ranges and add data series
    text: '`NSeries` is the collection that stores each data series for a chart. Adding
      a series links a range of cells to the chart. > **Pro tip:** The first parameter
      (`"A1:A5"`) is the range for the first series, and the second (`"B1:B5"`) creates
      a second series that will be combined with the first.'
  - name: set the category (X‑axis) data
    text: '`CategoryAxis` represents the horizontal axis of the chart, controlling
      the labels displayed along the X‑axis.'
  - name: set chart axis labels and title
    text: '`Title` sets the main title of the chart, and `Axis` objects represent
      the X and Y axes.'
  - name: add legend chart and adjust its position
    text: '`Legend` controls the placement and appearance of the series legend in
      the chart.'
  - name: save the workbook as an Excel file (XLSX)
    text: '`Workbook.save` writes the in‑memory workbook to a file in the specified
      format.'
  - name: export chart to PNG
    text: '`Chart.toImage` renders the chart as an image file in the chosen format.
      > The `chart.toImage` method **generates Excel chart** images that can be used
      in web pages, reports, or emails.'
  type: HowTo
- questions:
  - answer: 'Download the JAR from the official site and add it to your project’s
      classpath. The download link is: [Download Aspose.Cells for Java](https://releases.aspose.com/cells/java/).'
    question: How do I install Aspose.Cells for Java?
  - answer: Yes, Aspose.Cells supports bar, pie, scatter, area, and many more chart
      types. Refer to the API documentation for the full list.
    question: Can I create other chart types besides line and column?
  - answer: A valid Aspose.Cells license is required for production deployments. A
      free trial is available for evaluation.
    question: Is a license required for production use?
  - answer: Use `chart.getNSeries().get(i).setAreaColor(Color.getRed())` (or similar)
      after adding the series.
    question: How can I change the colors of each series?
  - answer: 'Comprehensive documentation and additional samples are available at the
      Aspose reference site: [Aspose Cells Java reference documentation](https://reference.aspose.com/cells/java/).'
    question: Where can I find more code examples?
  type: FAQPage
second_title: Aspose.Cells Java Excel Processing API
tags:
- export chart to png
- Aspose.Cells
- Java Excel charts
title: Экспорт диаграммы в PNG и добавление серии данных для combined chart
url: /ru/java/advanced-excel-charts/combined-chart-types/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Экспорт диаграммы в PNG и добавление серии данных для комбинированной диаграммы

В этом руководстве вы **добавите серию данных** в книгу Excel, **объедините элементы линейной и столбчатой диаграмм** и узнаете, как **экспортировать диаграмму в PNG** с помощью Aspose.Cells for Java. Мы пройдем каждый шаг — от настройки книги, добавления диаграммы на лист, настройки легенды, до **сохранения книги как XLSX** и создания PNG‑изображения диаграммы. К концу вы получите готовую комбинированную диаграмму, которую можно встроить в отчеты или панели мониторинга.

## Быстрые ответы
- **Какой библиотека создает комбинированные диаграммы?** Aspose.Cells for Java.  
- **Как добавить серию данных?** Вызовите `chart.getNSeries().add(...)` с соответствующим диапазоном.  
- **Как экспортировать диаграмму в PNG?** Используйте `chart.toImage("chart.png", ImageFormat.getPng())`.  
- **В каком файловом формате можно сохранить книгу?** Стандартный `.xlsx` (сохранить книгу как XLSX).  
- **Нужна ли лицензия для продакшна?** Да — для продакшн‑развертываний требуется действующая лицензия Aspose.Cells.

## Что такое экспорт диаграммы в PNG в Aspose.Cells?
Экспорт диаграммы в PNG создает растровое изображение диаграммы Excel, которое можно отображать на веб‑страницах, в отчетах или электронных письмах без необходимости использовать приложение Excel. Этот метод фиксирует точный визуальный макет, цвета и маркеры данных, создавая переносимый файл изображения.

## Зачем создавать комбинированную линейно‑столбчатую диаграмму?
Комбинированная линейно‑столбчатая диаграмма позволяет отображать разные наборы данных с различными визуальными представлениями (например, линейную серию поверх столбчатой) в одном представлении. Такой подход идеален для сравнения тенденций с общими суммами, выделения корреляций или предоставления более глубоких инсайтов при небольшом визуальном объёме.

## Требования
- Java Development Kit (JDK) 8 или выше  
- Библиотека Aspose.Cells for Java (скачать по ссылке ниже)  
- Базовое знакомство с синтаксисом Java и концепциями Excel  

## Начало работы

Сначала скачайте библиотеку Aspose.Cells for Java с официального сайта:

[Download Aspose.Cells for Java](https://releases.aspose.com/cells/java/)

После добавления JAR в classpath вашего проекта вы можете приступить к построению диаграммы.

### Шаг 1: импортировать классы aspose.cells
`Workbook` — основной объект Aspose.Cells, представляющий в памяти целый файл Excel.  
```java
import com.aspose.cells.*;
```

### Шаг 2: создать новую книгу
`Worksheet` представляет отдельный лист внутри `Workbook` и предоставляет доступ к ячейкам, строкам и диаграммам.  
```java
Workbook workbook = new Workbook();
```

### Шаг 3: получить доступ к первому листу
`Chart` — объект, содержащий все настройки, связанные с диаграммой, серии и параметры рендеринга.  
```java
Worksheet worksheet = workbook.getWorksheets().get(0);
```

### Шаг 4: добавить объект комбинированной диаграммы на лист
Мы начнём с линейной диаграммы, а затем добавим столбцовую серию, чтобы получить эффект **комбинированной линейно‑столбчатой диаграммы**.  
```java
int chartIndex = worksheet.getCharts().add(ChartType.LINE, 0, 0, 20, 10);
Chart chart = worksheet.getCharts().get(chartIndex);
```

## Добавление данных в диаграмму

Теперь, когда контейнер диаграммы существует, нам нужно заполнить его данными.

### Шаг 5: определить диапазоны данных и добавить серии
`NSeries` — коллекция, хранящая каждую серию данных для диаграммы. Добавление серии связывает диапазон ячеек с диаграммой.  
```java
Cells cells = worksheet.getCells();
chart.getNSeries().add("A1:A5", true);
chart.getNSeries().add("B1:B5", true);
```
> **Совет:** Первый параметр (`"A1:A5"`) — диапазон для первой серии, а второй (`"B1:B5"`) создаёт вторую серию, которая будет объединена с первой.

### Шаг 6: задать данные категорий (ось X)
`CategoryAxis` представляет горизонтальную ось диаграммы, управляя метками, отображаемыми вдоль оси X.  
```java
chart.getNSeries().setCategoryData("C1:C5");
```

## Настройка диаграммы

Хорошая диаграмма рассказывает историю. Давайте добавим ей заголовки, подписи осей и понятную легенду.

### Шаг 7: задать подписи осей и заголовок диаграммы
`Title` задаёт основной заголовок диаграммы, а объекты `Axis` представляют оси X и Y.  
```java
chart.getTitle().setText("Combined Chart Example");
chart.getCategoryAxis().getTitle().setText("Categories");
chart.getValueAxis().getTitle().setText("Values");
```

### Шаг 8: добавить легенду к диаграмме и скорректировать её позицию
`Legend` управляет размещением и внешним видом легенды серий в диаграмме.  
```java
chart.getLegend().setPosition(LegendPositionType.BOTTOM);
chart.getLegend().setOverlay(true);
```

## Сохранение и экспорт диаграммы

После настройки вы захотите **сохранить книгу как XLSX** и также создать изображение.

### Шаг 9: сохранить книгу как файл Excel (XLSX)
`Workbook.save` записывает книгу из памяти в файл в указанном формате.  
```java
workbook.save("CombinedChart.xlsx");
```

### Шаг 10: экспортировать диаграмму в PNG
`Chart.toImage` рендерит диаграмму в файл изображения в выбранном формате.  
```java
chart.toImage("CombinedChart.png", ImageFormat.getPng());
```
> Метод `chart.toImage` **создаёт изображения диаграмм Excel**, которые можно использовать на веб‑страницах, в отчетах или электронных письмах.

## Распространённые проблемы и их устранение

| Проблема | Решение |
|----------|---------|
| **Нет данных** | Убедитесь, что диапазоны ячеек (`A1:A5`, `B1:B5`, `C1:C5`) действительно содержат данные перед созданием диаграммы. |
| **Легенда перекрывает диаграмму** | Установите `chart.getLegend().setOverlay(false)` или переместите легенду в другое положение (например, `RIGHT`). |
| **Файл изображения пустой** | Убедитесь, что у диаграммы есть хотя бы одна серия и что `chart.toImage` вызывается после всех настроек. |
| **Ошибка при сохранении** | Проверьте, есть ли у вас права записи в целевой каталог и что файл не открыт в Excel. |

## Часто задаваемые вопросы

**В: Как установить Aspose.Cells for Java?**  
A: Скачайте JAR с официального сайта и добавьте его в classpath вашего проекта. Ссылка для скачивания: [Download Aspose.Cells for Java](https://releases.aspose.com/cells/java/).

**В: Можно ли создавать другие типы диаграмм, кроме линейных и столбчатых?**  
A: Да, Aspose.Cells поддерживает гистограммы, круговые, точечные, областные и многие другие типы диаграмм. Смотрите документацию API для полного списка.

**В: Требуется ли лицензия для использования в продакшн?**  
A: Для продакшн‑развертываний требуется действующая лицензия Aspose.Cells. Доступна бесплатная пробная версия для оценки.

**В: Как изменить цвета каждой серии?**  
A: Используйте `chart.getNSeries().get(i).setAreaColor(Color.getRed())` (или аналогично) после добавления серии.

**В: Где найти больше примеров кода?**  
A: Подробная документация и дополнительные примеры доступны на сайте справки Aspose: [Aspose Cells Java reference documentation](https://reference.aspose.com/cells/java/).

---

**Последнее обновление:** 2026-09-02  
**Тестировано с:** Aspose.Cells for Java последняя версия  
**Автор:** Aspose

## Связанные руководства

- [Как добавить подписи к диаграммам Excel с помощью Aspose.Cells for Java](/cells/java/charts-graphs/adding-labels-to-charts-aspose-cells-java-tutorial/)
- [Как создать диаграмму Excel с линией тренда и экспортировать в изображение с помощью Aspose.Cells for Java](/cells/java/advanced-excel-charts/trendline-analysis/)
- [Экспорт диаграмм Excel в PDF с помощью Aspose.Cells for Java: Руководство по пользовательским размерам страниц](/cells/java/charts-graphs/export-excel-charts-pdf-aspose-cells-java/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}