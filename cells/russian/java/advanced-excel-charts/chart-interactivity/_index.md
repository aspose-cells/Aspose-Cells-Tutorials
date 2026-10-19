---
date: 2026-08-21
description: Узнайте, как добавить tooltips, data labels и изменить тип диаграммы
  в Excel charts с помощью Aspose.Cells for Java — пошаговое руководство с интерактивными
  примерами.
keywords:
- how to add tooltips
- how to change chart type
- how to add data labels
lastmod: 2026-08-21
linktitle: Изменить тип диаграммы Excel
og_description: Узнайте, как добавить tooltips, data labels и изменить тип диаграммы
  в Excel charts с помощью Aspose.Cells for Java — пошаговое руководство с интерактивными
  примерами.
og_image_alt: 'Developer guide: Adding tooltips and data labels to Excel charts with
  Aspose.Cells for Java'
og_title: Как добавить tooltips и data labels в диаграммы Excel на Java
schemas:
- author: Aspose
  dateModified: '2026-08-21'
  description: Learn how to add tooltips, data labels, and change chart type in Excel
    charts using Aspose.Cells for Java – step‑by‑step guide with interactive examples.
  headline: How to add tooltips and data labels to Excel charts in Java
  type: TechArticle
- questions:
  - answer: You need to create a new chart with the desired `ChartType`. Aspose.Cells
      does not provide an in‑place type conversion, so remove the old chart and add
      a new one.
    question: How can I change the chart type after it’s created?
  - answer: Yes. Use the `DataLabel` properties such as `setFontSize`, `setFontColor`,
      and `setBackgroundColor` to style the tooltip text.
    question: Can I customize the appearance of tooltips?
  - answer: Export the workbook to an HTML or XLSX file and use JavaScript on the
      client side to capture click events on chart elements.
    question: How do I handle user interactions in a web application?
  - answer: Visit the [Aspose.Cells Java API Reference](https://reference.aspose.com/cells/java/)
      for a full list of chart‑related classes and methods.
    question: Where can I find more examples and documentation?
  type: FAQPage
second_title: Aspose.Cells Java Excel Processing API
tags:
- Aspose.Cells
- Java chart
- Excel interactivity
- tooltips
- data labels
title: Как добавить tooltips и data labels в диаграммы Excel на Java
url: /ru/java/advanced-excel-charts/chart-interactivity/
weight: 19
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Добавить подписи данных к диаграмме Excel и изменить тип диаграммы – Aspose.Cells Java

Интерактивные диаграммы придают вашим отчетам Excel новый уровень аналитики, а **как добавить всплывающие подсказки** делает информацию мгновенно читаемой. В этом руководстве вы узнаете, как **добавить подписи данных к диаграмме Excel**, **изменить тип диаграммы** и создать интерактивные решения на Java с Aspose.Cells. Мы также покажем, как добавить всплывающие подсказки и простой гиперссылка‑drill‑down, чтобы ваша аудитория могла глубже исследовать данные.

## Быстрые ответы
- **Какая библиотека используется?** Aspose.Cells for Java  
- **Можно ли изменить тип диаграммы?** Да – просто измените перечисление `ChartType` при создании диаграммы.  
- **Как добавить всплывающие подсказки к диаграмме?** Используйте API подписи данных (`setHasDataLabels(true)`) и включите отображение значений.  
- **Поддерживается ли drill‑down?** Вы можете прикрепить гиперссылки к точкам данных для базового поведения drill‑down.  
- **Требования?** Java IDE, Aspose.Cells JAR и файл Excel с примерными данными.

## Что такое как добавить всплывающие подсказки?
**Как добавить всплывающие подсказки** относится к процессу включения текста, отображаемого при наведении, который показывает значение точки данных или пользовательскую информацию на диаграмме Excel. В Aspose.Cells это достигается через настройки подписи данных диаграммы. Всплывающие подсказки помогают пользователям быстро понять данные без захламления диаграммы и могут быть настроены по шрифту, цвету и формату.

## Почему использовать интерактивные диаграммы с Aspose.Cells?
Aspose.Cells поддерживает **более 50 форматов ввода и вывода** — включая XLSX, CSV, PDF и HTML — и может обрабатывать книги с **более 1 000 листов** без загрузки всего файла в память, обеспечивая быструю серверную генерацию диаграмм для корпоративной отчетности. Интерактивные диаграммы также позволяют встраивать гиперссылки, динамически обновлять данные и экспортировать в веб‑дружественные форматы, что делает их идеальными для панелей мониторинга и порталов отчетности.

## Требования

Прежде чем начать, убедитесь, что у вас есть следующее:

- Среда разработки Java (рекомендовано JDK 8+)  
- Библиотека Aspose.Cells for Java (скачать со [страницы загрузки Aspose.Cells for Java](https://releases.aspose.com/cells/java/))  
- Пример рабочей книги (`data.xlsx`) с данными, которые вы хотите визуализировать  

## Шаг 1: настройка проекта Java

1. Создайте новый проект Java в вашей любимой IDE (IntelliJ IDEA, Eclipse и т.д.).  
2. Добавьте Aspose.Cells JAR в путь сборки проекта или в зависимости Maven/Gradle.

## Шаг 2: загрузка данных

Чтобы работать с диаграммами, сначала необходимо загрузить книгу в память.

Класс `Workbook` представляет файл Excel, а `Worksheet` представляет отдельный лист внутри этого файла.

```java
// Load the Excel file
Workbook workbook = new Workbook("data.xlsx");
Worksheet worksheet = workbook.getWorksheets().get(0);
```

## Как изменить тип диаграммы в Aspose.Cells?

Создайте новую диаграмму с нужным перечислением `ChartType`; Aspose.Cells не изменяет тип существующей диаграммы «на месте», поэтому вам нужно добавить новую диаграмму нужного типа и при желании удалить старую. Такой подход гарантирует, что все серии и оси будут правильно перестроены для нового визуального представления.

## Шаг 3: создание диаграммы (и изменение её типа)

Вы можете выбрать любой тип диаграммы, подходящий для вашего анализа. Ниже мы создаём **столбчатую диаграмму**, но вы легко можете переключиться на линейную, круговую или гистограмму, изменив перечисление `ChartType`.

Объект `Chart` предоставляет методы для настройки визуального представления данных в листе.

```java
// Create a column chart
int chartIndex = worksheet.getCharts().add(ChartType.COLUMN, 5, 0, 15, 5);
Chart chart = worksheet.getCharts().get(chartIndex);
```

> **Pro tip:** Чтобы **изменить тип диаграммы Excel**, замените `ChartType.COLUMN` на `ChartType.LINE`, `ChartType.PIE` и т.д.

## Как добавить всплывающие подсказки к диаграмме Excel?

Загрузите вашу диаграмму, включите подписи данных и установите флаг `showValue`. Всплывающая подсказка будет отображать значение ячейки, когда пользователь наведёт курсор на точку данных в сгенерированном файле Excel или в представлении HTML. Вы также можете настроить шрифт, цвет и фон подсказки, чтобы они соответствовали стилю вашего отчёта.

Класс `DataLabel` управляет внешним видом и содержимым подписей данных, которые также служат всплывающими подсказками.

```java
// Enable tooltips for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowValue(true);
```

## Шаг 4: добавление интерактивности

### 4.1. Добавление всплывающих подсказок (add tooltips to chart)

Всплывающие подсказки появляются, когда пользователь наводит курсор на точку данных. Следующий код включает подписи данных и отображает значение как подсказку.

```java
// Enable data labels for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowLabelAsDataCallout(true);
```

### 4.2. Добавление подписей данных – **add data labels to excel chart**

Подписи данных предоставляют постоянный визуальный индикатор непосредственно на диаграмме. Вы можете отображать их в виде выноски для лучшей читаемости.

Класс `DataLabel` управляет внешним видом подписей на каждой серии. Вызвав `setHasDataLabels(true)` и настроив свойства, такие как `setShowValue(true)`, вы встраиваете числовое значение прямо в диаграмму, делая его мгновенно видимым без какого‑либо взаимодействия. Дополнительные параметры позволяют показывать имена серий, проценты или пользовательский текст для более богатого контекста.

> **Зачем добавлять подписи данных?** Размещение подписей непосредственно на диаграмме устраняет необходимость наведения курсора или угадывания значений, повышая ясность отчёта.

### 4.3. Реализация drill‑down (гиперссылка на точку данных)

Простой способ добавить возможность drill‑down – прикрепить гиперссылку к конкретной точке. При щелчке по точке откроется веб‑страница с подробной информацией.

Класс `Hyperlink` прикрепляет кликабельную ссылку к элементу диаграммы, обеспечивая навигацию drill‑down.

```java
// Add a hyperlink to a data point
String url = "https://example.com/data-details";
chart.getNSeries().get(0).getPoints().get(0).getHyperlinks().add(url);
```

## Как добавить подписи данных к диаграмме Excel?

Класс `DataLabel` управляет внешним видом подписей на каждой серии. Вызвав `setHasDataLabels(true)` и настроив свойства, такие как `setShowValue(true)`, вы встраиваете числовое значение прямо в диаграмму, делая его мгновенно видимым без какого‑либо взаимодействия. Дополнительные параметры позволяют показывать имена серий, проценты или пользовательский текст для более богатого контекста.

## Шаг 5: сохранение книги

После настройки диаграммы сохраните книгу, чтобы интерактивные функции были сохранены в выходном файле.

Вызов `workbook.save` записывает изменённую книгу в файл в выбранном формате.

```java
// Save the workbook
workbook.save("interactive_chart_output.xlsx");
```

## Распространённые проблемы и решения

| Проблема | Решение |
|----------|---------|
| **Всплывающие подсказки не отображаются** | Убедитесь, что `setHasDataLabels(true)` вызывается до настройки `setShowValue(true)`. |
| **Гиперссылка не кликабельна** | Проверьте, поддерживает ли выходной формат гиперссылки (например, XLSX, а не CSV). |
| **Тип диаграммы не меняется** | Дважды проверьте, что вы изменили правильное перечисление `ChartType` при добавлении диаграммы. |

## Часто задаваемые вопросы

**В: Как изменить тип диаграммы после её создания?**  
О: Нужно создать новую диаграмму с нужным `ChartType`. Aspose.Cells не предоставляет преобразование типа «на месте», поэтому удалите старую диаграмму и добавьте новую.

**В: Можно ли настроить внешний вид всплывающих подсказок?**  
О: Да. Используйте свойства `DataLabel`, такие как `setFontSize`, `setFontColor` и `setBackgroundColor`, чтобы стилизовать текст подсказки.

**В: Как обрабатывать взаимодействия пользователя в веб‑приложении?**  
О: Экспортируйте книгу в HTML или XLSX и используйте JavaScript на клиенте для захвата событий щелчка по элементам диаграммы.

**В: Где найти больше примеров и документацию?**  
О: Посетите [Aspose.Cells Java API Reference](https://reference.aspose.com/cells/java/) для полного списка классов и методов, связанных с диаграммами.

## Заключение

Теперь вы знаете, как **добавить подписи данных к диаграмме Excel**, **изменить тип диаграммы Excel**, **создать интерактивные решения на Java** и обогатить их всплывающими подсказками, подписями данных и гиперссылками drill‑down с помощью Aspose.Cells for Java. Эти улучшения делают ваши отчёты Excel гораздо более привлекательными и информативными для конечных пользователей.

---

**Последнее обновление:** 2026-08-21  
**Тестировано с:** Aspose.Cells for Java 24.12  
**Автор:** Aspose

## Похожие руководства

- [How to Modify Excel Charts and Data Labels Using Aspose.Cells for Java](/cells/java/charts-graphs/aspose-cells-java-modify-excel-charts-data-labels/)
- [Extract Excel Chart Axis Labels Using Aspose.Cells Java: A Comprehensive Guide](/cells/java/charts-graphs/aspose-cells-java-excel-chart-axis-labels/)
- [Create Bubble Charts in Excel Using Aspose.Cells for Java: A Step‑By‑Step Guide](/cells/java/charts-graphs/aspose-cells-java-create-bubble-charts/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}