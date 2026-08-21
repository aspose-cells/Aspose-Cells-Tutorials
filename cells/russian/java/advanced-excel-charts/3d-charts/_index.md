---
date: 2026-08-21
description: Узнайте, как экспортировать диаграмму как изображение и создавать 3D
  pie charts в Java с Aspose.Cells. Генерируйте 3D bar charts, добавляйте 3D charts
  в Excel и сохраняйте рабочие книги как XLSX.
keywords:
- export chart as image
- 3d pie chart java
- 3d bar chart java
- save workbook as xlsx
- add 3d chart excel
lastmod: 2026-08-21
linktitle: Создать 3D Pie Chart Java
og_description: Экспортируйте диаграмму как изображение и создавайте 3D pie charts
  в Java с помощью Aspose.Cells. Пошаговое руководство по генерации 3D bar и pie charts,
  их настройке и сохранению рабочих книг как XLSX.
og_image_alt: Developer guide showing how to export a 3D chart as an image with Aspose.Cells
  for Java
og_title: Экспортировать диаграмму как изображение и создать 3D pie chart в Java
schemas:
- author: Aspose
  dateModified: '2026-08-21'
  description: Learn how to export chart as image and create 3D pie charts in Java
    with Aspose.Cells. Generate 3D bar charts, add 3D charts to Excel, and save workbooks
    as XLSX.
  headline: How to export chart as image and create 3D pie chart in Java
  type: TechArticle
- questions:
  - answer: Use `chart.getNSeries().add()` for each series range and ensure the chart
      type remains 3‑D (e.g., `ChartType.BAR_3_D` or `ChartType.PIE_3_D`).
    question: How can I add multiple data series to a 3D chart?
  - answer: Yes, you can save the chart as PNG, JPEG, or PDF by calling the appropriate
      `chart.toImage()` overload or `workbook.save()` with an image or PDF format,
      satisfying the **convert chart png** requirement.
    question: Can I export 3D charts created with Aspose.Cells for Java to other formats?
  - answer: Aspose.Cells focuses on static Excel charts. For interactive web‑based
      3‑D visualizations, consider coupling Excel data with JavaScript libraries such
      as Three.js.
    question: Is it possible to create interactive 3D charts with Aspose.Cells for
      Java?
  - answer: Absolutely. Load new data into the worksheet programmatically and refresh
      the chart range; the next time the workbook is opened, the chart reflects the
      updated values.
    question: Can I automate the process of updating data in my 3D charts?
  - answer: 'You can find comprehensive documentation and resources for Aspose.Cells
      for Java at the website: [Aspose.Cells for Java Documentation](https://reference.aspose.com/cells/java/).'
    question: Where can I find more resources and documentation for Aspose.Cells for
      Java?
  type: FAQPage
second_title: Aspose.Cells Java Excel Processing API
tags:
- export chart as image
- 3d pie chart
- Aspose.Cells Java
- Excel chart automation
title: Как экспортировать диаграмму как изображение и создать 3D pie chart в Java
url: /ru/java/advanced-excel-charts/3d-charts/
weight: 13
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Создать 3D круговую диаграмму Java

## Введение в 3D диаграммы

Aspose.Cells for Java — мощный Java API для работы с файлами Excel, который упрощает создание проектов **создавать 3D круговую диаграмму** и классических 3‑D столбчатых визуализаций. В этом руководстве вы точно увидите, как **экспортировать диаграмму как изображение**, сгенерировать 3‑D столбчатую диаграмму, адаптировать тот же подход для 3‑D круговой диаграммы, настроить внешний вид и наконец **добавлять 3D диаграммы в Excel** файлы в ваши отчёты. Независимо от того, создаёте ли вы финансовую панель, лист продаж или визуализируете научные данные, нижеописанные шаги дадут вам прочную основу.

## Быстрые ответы
- **Какую библиотеку мне нужно?** Aspose.Cells for Java (последняя версия)  
- **Могу ли я создать 3D столбчатую диаграмму?** Да — используйте `ChartType.BAR_3_D`  
- **Нужна ли лицензия?** Действительная лицензия снимает ограничения оценки  
- **Какие версии Excel поддерживаются?** Все основные версии с 2003 по 2023  
- **Можно ли экспортировать диаграмму как изображение?** Да — вызовите `chart.toImage()` после создания диаграммы  

## Что такое 3D диаграммы?
3D диаграммы добавляют глубину к традиционным 2D визуализациям, помогая зрителям более интуитивно воспринимать многомерные взаимосвязи. Они особенно полезны, когда нужно сравнить несколько категорий рядом, сохраняя при этом чёткую визуальную иерархию. Добавив третье измерение, такие диаграммы могут выделять различия в величине, которые могут быть менее очевидны в плоских представлениях, делая сложные данные легче интерпретировать бизнес‑заинтересованным сторонам.

## Почему использовать Aspose.Cells for Java для создания 3D столбчатой диаграммы?
Aspose.Cells for Java предоставляет более 150 встроенных типов диаграмм и поддерживает более 100 функций Excel, предлагая полностью укомплектованный движок, работающий со всеми версиями Excel от 2003 до 2023 без необходимости Microsoft Office. Это означает, что вы можете **генерировать 3D столбчатую диаграмму** программно с предсказуемыми результатами и минимальными затратами.

## Настройка Aspose.Cells for Java

### Загрузка и установка
Вы можете скачать библиотеку Aspose.Cells for Java с официального сайта. Следуйте инструкциям Maven/Gradle или добавьте JAR‑файл напрямую в classpath вашего проекта.

### Инициализация лицензии
Класс `License` используется для применения вашей лицензии Aspose.Cells и разблокировки полной функциональности.  
```java
// Initialize Aspose.Cells license
License license = new License();
license.setLicense("path_to_license_file.xml");
```

## Создание базовой 3D диаграммы

### Импорт необходимых библиотек
Сначала импортируйте требуемые классы:  
```java
import com.aspose.cells.*;
```

### Инициализация рабочей книги
Создайте новую рабочую книгу, в которой будет размещена диаграмма:  
```java
Workbook workbook = new Workbook();
```

### Добавление данных в диаграмму
Заполните лист образцовыми данными, которые будет использовать диаграмма:  
```java
Worksheet worksheet = workbook.getWorksheets().get(0);

// Adding data to cells
worksheet.getCells().get("A1").putValue("Category");
worksheet.getCells().get("A2").putValue("A");
worksheet.getCells().get("A3").putValue("B");
worksheet.getCells().get("A4").putValue("C");

worksheet.getCells().get("B1").putValue("Value");
worksheet.getCells().get("B2").putValue(10);
worksheet.getCells().get("B3").putValue(20);
worksheet.getCells().get("B4").putValue(30);
```

## Как создать 3D столбчатую диаграмму в Java
Чтобы создать 3D столбчатую диаграмму, добавьте объект диаграммы на лист, задайте его тип `ChartType.BAR_3_D`, а затем привяжите серии данных к ячейкам, содержащим ваши значения. После настройки внешнего вида диаграммы вы можете отобразить её или экспортировать по необходимости.  
```java
int chartIndex = worksheet.getCharts().add(ChartType.BAR_3_D, 5, 0, 15, 5);
Chart chart = worksheet.getCharts().get(chartIndex);

// Setting the data range for the chart
chart.getNSeries().add("A2:B4", true);

// Customizing chart attributes
chart.getChartArea().getBorder().setVisible(false);
chart.getChartTitle().setText("3D Bar Chart");
```

## Сохранение диаграммы в файл
Наконец, запишите рабочую книгу (которая теперь содержит 3‑D диаграмму) на диск. Это также **сохраняет рабочую книгу xlsx** в стандартном формате Excel:  
```java
workbook.save("3D_Chart.xlsx");
```

## Как создать 3D круговую диаграмму с помощью Aspose.Cells for Java
Если вам нужна визуализация в виде круга, процесс почти идентичен — меняется только значение перечисления `ChartType`. Замените `ChartType.BAR_3_D` на `ChartType.PIE_3_D` при добавлении диаграммы и укажите тот же диапазон данных. После создания диаграммы вы можете задать описательный заголовок, настроить цвета секторов и экспортировать результат как изображение. Этот подход позволяет переиспользовать тот же код подготовки данных, получая иной визуальный взгляд.

## Как экспортировать диаграмму как изображение в Java
Метод `toImage` объекта `Chart` сохраняет диаграмму в виде файла изображения. Вы можете экспортировать любую 3D диаграмму в растровое изображение одним вызовом: `chart.toImage("myChart.png", ImageFormat.getPng())`. Этот метод рендерит диаграмму точно так, как она выглядит в Excel, сохраняет 3‑D глубину, цвета и легенды, и записывает результат в указанный путь. Используйте PNG для без потерь качества или JPEG для меньшего размера файла при встраивании изображения в веб‑отчёты.

## Разные типы 3D диаграмм
Aspose.Cells for Java поддерживает несколько вариантов 3D диаграмм, которые вы можете **добавлять 3D диаграммы в Excel** файлы:

- **Столбчатые диаграммы** — идеальны для сравнения категорий.  
- **Круговые диаграммы** — показывают пропорциональные вклады (включая 3D круговую).  
- **Линейные диаграммы** — иллюстрируют тенденции во времени.  
- **Областные диаграммы** — подчеркивают величину изменения.

Вы можете переключить перечисление `ChartType` на любой из перечисленных, сохраняя тот же шаблон создания.

## Расширенная настройка диаграмм

### Добавление заголовков и подписей
Придайте диаграмме контекст, задав описательный заголовок и подписи осей.

### Настройка цветов и стилей
Используйте метод `chart.getSeries().get(i).getArea().setForegroundColor(Color.getRGB(...))`, чтобы соответствовать фирменному стилю.

### Работа с осями диаграммы
Точно настройте шкалы осей, интервалы и деления, чтобы улучшить читаемость.

### Добавление легенд
Включите легенды с помощью `chart.getLegend().setVisible(true)`, чтобы зрители могли идентифицировать каждую серию данных.

### Экспорт диаграмм как изображений
Когда нужен статический образ для веб‑отчёта, вызовите `chart.toImage("chart.png", ImageFormat.getPng())`. Это решает задачу **конвертировать диаграмму png** без выхода из рабочей книги.

## Интеграция данных
Aspose.Cells for Java может извлекать данные из баз данных, CSV‑файлов или живых API. Просто заполните ячейки листа полученными данными перед привязкой диапазона к диаграмме. Это сохраняет ваш **добавлять 3D диаграммы в Excel** процесс динамичным и актуальным.

## Заключение
В этом руководстве мы прошли путь от **создания 3D круговой диаграммы** и **создания 3D столбчатой диаграммы** до завершения проекта — настройка библиотеки, добавление данных, генерация 3‑D столбчатой диаграммы, адаптация тех же шагов для 3‑D круговой диаграммы и применение продвинутого стилирования. С Aspose.Cells for Java у вас есть надёжный, независимый от версии способ встраивать богатые 3‑D визуализации непосредственно в Excel‑книги и даже **экспортировать диаграмму как изображение** для использования в панелях мониторинга или отчётах.

## Часто задаваемые вопросы

**В: Как добавить несколько рядов данных в 3D диаграмму?**  
О: Используйте `chart.getNSeries().add()` для каждого диапазона серии и убедитесь, что тип диаграммы остаётся 3‑D (например, `ChartType.BAR_3_D` или `ChartType.PIE_3_D`).

**В: Можно ли экспортировать 3D диаграммы, созданные с помощью Aspose.Cells for Java, в другие форматы?**  
О: Да, вы можете сохранить диаграмму как PNG, JPEG или PDF, вызвав соответствующий перегруженный вариант `chart.toImage()` или `workbook.save()` с форматом изображения или PDF, удовлетворяя требование **конвертировать диаграмму png**.

**В: Возможно ли создавать интерактивные 3D диаграммы с помощью Aspose.Cells for Java?**  
О: Aspose.Cells ориентирован на статические диаграммы Excel. Для интерактивных веб‑ориентированных 3‑D визуализаций рассмотрите сочетание данных Excel с JavaScript‑библиотеками, такими как Three.js.

**В: Можно ли автоматизировать процесс обновления данных в моих 3D диаграммах?**  
О: Абсолютно. Программно загружайте новые данные в лист и обновляйте диапазон диаграммы; при следующем открытии рабочей книги диаграмма отразит обновлённые значения.

**В: Где можно найти дополнительные ресурсы и документацию по Aspose.Cells for Java?**  
О: Вы можете найти полную документацию и ресурсы по Aspose.Cells for Java на сайте: [Документация Aspose.Cells for Java](https://reference.aspose.com/cells/java/).

---

**Последнее обновление:** 2026-08-21  
**Тестировано с:** Aspose.Cells for Java 24.12 (latest)  
**Автор:** Aspose

## Связанные руководства

- [Создание круговых диаграмм в Excel с помощью Aspose.Cells for Java: Полное руководство](/cells/java/charts-graphs/master-pie-chart-creation-excel-aspose-cells-java/)
- [aspose cells java – Создание диаграммы Excel с аннотациями](/cells/java/advanced-excel-charts/chart-annotations/)
- [Добавление подписей данных к диаграмме Excel с Aspose.Cells Java](/cells/java/advanced-excel-charts/chart-interactivity/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}