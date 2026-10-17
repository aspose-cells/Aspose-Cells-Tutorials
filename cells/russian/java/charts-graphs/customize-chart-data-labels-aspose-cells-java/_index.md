---
date: '2026-10-17'
description: Узнайте, как задать форму подписей данных диаграммы Excel в Java с помощью
  Aspose.Cells. Это руководство покажет, как быстро и эффективно изменять подписи
  диаграмм Excel.
keywords:
- how to set shape
- modify excel chart labels
- customize chart data labels
- add data label shape
lastmod: '2026-10-17'
og_description: Узнайте, как задать форму подписей данных диаграммы Excel в Java с
  помощью Aspose.Cells. Это пошаговое руководство поможет быстро изменять подписи
  диаграмм Excel.
og_image_alt: Guide showing how to set shape of Excel chart data labels using Aspose.Cells
  for Java
og_title: Как задать форму подписей данных диаграммы Excel в Java
schemas:
- author: Aspose
  dateModified: '2026-10-17'
  description: Learn how to set shape of Excel chart data labels in Java using Aspose.Cells.
    This guide shows you how to modify Excel chart labels quickly and efficiently.
  headline: How to set shape of Excel chart data labels in Java
  type: TechArticle
- description: Learn how to set shape of Excel chart data labels in Java using Aspose.Cells.
    This guide shows you how to modify Excel chart labels quickly and efficiently.
  name: How to set shape of Excel chart data labels in Java
  steps:
  - name: load your workbook
    text: The `Workbook` class is Aspose.Cells' top‑level object that represents a
      single Excel file in memory. Use `new Workbook("input.xlsx")` to load the file
      you want to modify.
  - name: access the chart
    text: '`Worksheet` represents a single sheet within a workbook. `Worksheet ws
      = workbook.getWorksheets().get(0);` retrieves the first worksheet. `Chart` is
      an object that represents a chart embedded in a worksheet. `Chart chart = ws.getCharts().get(0);`
      obtains the first chart on that sheet.'
  - name: retrieve series and modify data labels
    text: '`Series` represents a data series plotted on a chart. Each `Series` object
      contains a `DataLabel` collection. `DataLabel` controls the appearance of a
      data label for a series. `DataLabelShapeType` is an enumeration of possible
      shapes for data labels. Call `series.getDataLabels().setShapeType(DataLab'
  - name: save your workbook
    text: After applying the shape, invoke `workbook.save("output.xlsx");` to write
      the changes back to disk.
  type: HowTo
- questions:
  - answer: Loop through each series in the chart and call `setShapeType` on the series’
      `DataLabel` object.
    question: How do I change the shape of multiple data labels at once?
  - answer: Yes. With proper memory management, it processes workbooks containing
      hundreds of thousands of rows without loading the entire file into memory.
    question: Can Aspose.Cells for Java handle large Excel files efficiently?
  - answer: Missing Maven dependencies, using an outdated library version, or providing
      an invalid license file are typical pitfalls.
    question: What are common issues when setting up Aspose.Cells?
  - answer: Set the shape type to `DataLabelShapeType.DEFAULT` to restore the original
      appearance.
    question: Is there a way to revert data label shapes to default?
  - answer: Iterate over `ws.getCharts()` and apply the same `setShapeType` logic
      to each chart’s series collection.
    question: How can I apply this customization to multiple charts in a workbook?
  type: FAQPage
tags:
- excel chart
- aspose.cells
- java chart customization
- data label shape
title: Как задать форму подписей данных диаграммы Excel в Java
url: /ru/java/charts-graphs/customize-chart-data-labels-aspose-cells-java/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Освоение настройки диаграмм в Java с Aspose.Cells: изменение формы меток данных

## Введение

Повышение визуальной привлекательности диаграмм Excel имеет решающее значение при подготовке отчетов или панелей мониторинга, особенно если вы используете Java. С Aspose.Cells — мощной библиотекой для управления и манипуляции электронными таблицами — вы можете **how to set shape** меток данных диаграммы всего в несколько строк кода. Этот учебник проведет вас через процесс изменения формы меток данных в диаграмме Excel с использованием Aspose.Cells для Java. К концу вы узнаете, как:

- Получать доступ к меткам данных диаграммы и изменять их
- Устанавливать пользовательские формы для меток данных
- Сохранять изменения в вашей книге

## Быстрые ответы
- **Что является основным классом для работы с файлами Excel?** `Workbook` представляет собой весь файл Excel в памяти.  
- **Какой метод устанавливает форму метки?** `setShapeType(DataLabelShapeType shape)` у объекта `DataLabel`.  
- **Нужна ли лицензия для разработки?** Бесплатная временная лицензия работает для оценки; полная лицензия требуется для продакшна.  
- **Можно ли применить форму к нескольким сериям?** Да — итеративно пройдитесь по каждой серии и вызовите `setShapeType`.  
- **Совместим ли этот подход с большими книгами?** Aspose.Cells обрабатывает многосотстраничные книги без загрузки всего файла в память.

## Что такое установка формы?
Фраза **how to set shape** относится к настройке визуального контура метки данных диаграммы, например, превращения простого прямоугольника в выноску или эллипс. Изменение формы улучшает читаемость и выделяет ключевые точки данных. Выбирая подходящую форму, вы можете сделать метку более заметной, сгруппировать связанные точки или соответствовать корпоративным рекомендациям по брендингу, тем самым повышая общую читаемость диаграммы.

## Почему использовать Aspose.Cells для настройки меток диаграмм?
Aspose.Cells поддерживает **50+ входных и выходных форматов** — включая XLSX, CSV, ODS и PDF, — и может манипулировать книгами, содержащими **до 1 млн строк** без исчерпания памяти. Его API позволяет программно изменять диаграммы, устраняя необходимость ручных правок в Excel и обеспечивая единообразный стиль в автоматизированных отчетах.

## Необходимые условия

- **Aspose.Cells for Java Library**: Требуется версия 25.3 или новее.  
- **Java Development Environment**: Установленный JDK на вашем компьютере.  
- **IDE Setup**: Используйте IDE, например IntelliJ IDEA или Eclipse, для написания и запуска кода.

### Требуемые библиотеки и зависимости

Для пользователей Maven включите следующую зависимость в ваш `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

Пользователи Gradle должны добавить это в файл `build.gradle`:

```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

### Приобретение лицензии

Aspose.Cells предлагает бесплатную пробную лицензию, которую можно получить со страницы [страница временной лицензии Aspose](https://purchase.aspose.com/temporary-license/). Это дает полный доступ ко всем функциям без ограничений на ограниченный период.

## Настройка Aspose.Cells для Java

Как только ваша среда готова, давайте настроим Aspose.Cells. Вот как начать:

### Шаги установки

1. **Скачать библиотеку**: Используйте Maven или Gradle, как показано выше.  
2. **Конфигурация лицензии**:  
   - `License` — класс, который применяет ваш файл лицензии Aspose.Cells для включения полной функциональности.  
   - Скачайте и примените временную лицензию, используя этот фрагмент кода после инициализации объекта `Workbook`:

    ```java
    License license = new License();
    license.setLicense("path/to/your/license/file");
    ```
3. **Базовая инициализация**: Создайте экземпляр `Workbook`, чтобы начать работу с файлами Excel.

## Как установить форму меток данных в диаграмме?

Загрузите книгу, найдите нужную диаграмму и примените желаемую форму к её меткам данных. Ниже приведены прямые шаги, которые займут менее минуты.

### Пошаговое руководство

#### Шаг 1: загрузить вашу книгу

Класс `Workbook` — объект верхнего уровня Aspose.Cells, представляющий один файл Excel в памяти. Используйте `new Workbook("input.xlsx")`, чтобы загрузить файл, который хотите изменить.

#### Шаг 2: получить доступ к диаграмме

`Worksheet` представляет отдельный лист в книге.  
`Worksheet ws = workbook.getWorksheets().get(0);` получает первый лист.  
`Chart` — объект, представляющий диаграмму, встроенную в лист.  
`Chart chart = ws.getCharts().get(0);` получает первую диаграмму на этом листе.

#### Шаг 3: получить серии и изменить метки данных

`Series` представляет серию данных, построенную на диаграмме.  
Каждый объект `Series` содержит коллекцию `DataLabel`.  
`DataLabel` управляет внешним видом метки данных для серии.  
`DataLabelShapeType` — перечисление возможных форм меток данных.  
Вызовите `series.getDataLabels().setShapeType(DataLabelShapeType.WEDGE_ELLIPSE_CALLOUT);`, чтобы задать форму. Перечисление предоставляет десятки вариантов, таких как `RECTANGLE`, `CLOUD` и `WEDGE_ELLIPSE_CALLOUT`.

#### Шаг 4: сохранить вашу книгу

После применения формы вызовите `workbook.save("output.xlsx");`, чтобы записать изменения на диск.

## Советы по устранению неполадок

- **Проблемы с путями к файлам**: Убедитесь, что путь к файлу абсолютный или правильно относительный к рабочей директории проекта.  
- **Несоответствие версии библиотеки**: Убедитесь, что используете Aspose.Cells версии 25.3 или новее; в более старых версиях метода `setShapeType` нет.  
- **Неподдерживаемые типы диаграмм**: Некоторые устаревшие типы диаграмм (например, радиальная) могут не раскрывать свойства формы меток; переключитесь на поддерживаемый тип, такой как столбчатая или линейная диаграмма.

## Практические применения

1. **Финансовая отчетность** — выделяйте ключевые маржи прибыли метками‑выносками.  
2. **Образовательный контент** — используйте метки в виде облака, чтобы привлечь внимание к важным точкам данных в учебных материалах.  
3. **Маркетинговая аналитика** — применяйте пользовательские формы для различения метрик эффективности кампаний в панелях мониторинга.

Интеграция Aspose.Cells с конвейерами данных или CRM‑системами позволяет автоматически генерировать полностью стилизованные отчеты, снижая ручные трудозатраты и обеспечивая визуалы, соответствующие бренду.

## Соображения по производительности

При работе с большими файлами Excel:

- **Оптимизировать использование памяти**: Вызовите `workbook.dispose();` после сохранения, чтобы быстро освободить нативные ресурсы.  
- **Пакетная обработка**: Обрабатывайте диаграммы группами, а не по одной, чтобы минимизировать накладные расходы на создание объектов.  
- **Эффективная работа с данными**: Избегайте тяжёлых вычислений внутри циклов, проходящих по тысячам строк; вычисляйте значения заранее.

## Заключение

Теперь вы знаете **how to set shape** меток данных диаграммы Excel в Java с помощью Aspose.Cells. Эта возможность не только улучшает эстетический вид диаграмм, но и повышает понимание данных конечными пользователями. Исследуйте дополнительные параметры настройки — например, цвета меток, шрифты и линии‑соединители, — чтобы ещё более усовершенствовать визуализацию.

Для любых вопросов или помощи обратитесь к [форуму поддержки Aspose](https://forum.aspose.com/c/cells/9).

## Часто задаваемые вопросы

**Q: Как изменить форму нескольких меток данных одновременно?**  
A: Пройдитесь по каждой серии в диаграмме и вызовите `setShapeType` у объекта `DataLabel` серии.

**Q: Может ли Aspose.Cells для Java эффективно обрабатывать большие файлы Excel?**  
A: Да. При правильном управлении памятью он обрабатывает книги, содержащие сотни тысяч строк, без загрузки всего файла в память.

**Q: Какие типичные проблемы возникают при настройке Aspose.Cells?**  
A: Отсутствие Maven‑зависимостей, использование устаревшей версии библиотеки или предоставление недействительного файла лицензии — это типичные подводные камни.

**Q: Есть ли способ вернуть формы меток данных к значениям по умолчанию?**  
A: Установите тип формы в `DataLabelShapeType.DEFAULT`, чтобы восстановить исходный вид.

**Q: Как применить эту настройку к нескольким диаграммам в книге?**  
A: Итеративно пройдитесь по `ws.getCharts()` и примените ту же логику `setShapeType` к коллекции серий каждой диаграммы.

## Ресурсы

- [Документация Aspose.Cells](https://reference.aspose.com/cells/java/)
- [Скачать Aspose.Cells для Java](https://releases.aspose.com/cells/java/)
- [Купить лицензию](https://purchase.aspose.com/buy)
- [Бесплатная пробная лицензия](https://releases.aspose.com/cells/java/)
- [Временная лицензия](https://purchase.aspose.com/temporary-license/)

---  

**Last Updated:** 2026-10-17  
**Tested With:** Aspose.Cells 25.3 for Java  
**Author:** Aspose  



```java
Workbook wb = new Workbook("YOUR_DATA_DIRECTORY/sampleSetShapeTypeOfDataLabelsOfChart.xlsx");
```
```java
Worksheet ws = wb.getWorksheets().get(0);
Chart ch = ws.getCharts().get(0);
```
```java
Series srs = ch.getNSeries().get(0);
srs.getDataLabels().setShapeType(DataLabelShapeType.WEDGE_ELLIPSE_CALLOUT);
```
```java
wb.save("YOUR_OUTPUT_DIRECTORY/outputSetShapeTypeOfDataLabelsOfChart.xlsx");
```

## Похожие руководства

- [Изменить метки данных диаграммы Excel с помощью Aspose.Cells Java](/cells/java/charts-graphs/modify-excel-chart-data-labels-aspose-cells-java/)
- [Как изменить размер меток в диаграммах Excel с Aspose.Cells для Java](/cells/java/charts-graphs/aspose-cells-java-auto-resize-chart-data-labels/)
- [Добавить метки к диаграммам Excel с Aspose Cells для Java](/cells/java/charts-graphs/adding-labels-to-charts-aspose-cells-java-tutorial/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}