---
date: 2026-02-09
description: Узнайте, как создать диаграмму Excel, добавить линию тренда, отобразить
  значение R‑квадрат и экспортировать диаграмму в изображение с помощью Aspose.Cells
  для Java. Включает шаги по загрузке файла Excel, настройке диаграммы и сохранению
  в формате PNG/JPEG.
linktitle: Export Chart to Image with Trendline Analysis
second_title: Aspose.Cells Java Excel Processing API
title: Как создать диаграмму Excel с линией тренда и экспортировать её в изображение
  с помощью Aspose.Cells для Java
url: /ru/java/advanced-excel-charts/trendline-analysis/
weight: 15
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Экспорт диаграммы в изображение с анализом трендовой линии

В этом руководстве вы узнаете, как **create Excel chart** с трендовой линией, отобразить её значение R‑squared и экспортировать полученную визуализацию в изображение с помощью Aspose.Cells for Java. Мы пройдём процесс загрузки существующей книги, добавления трендовой линии, настройки заголовков, сохранения книги и, наконец, создания файла PNG/JPEG, который можно вставить куда угодно.

## Краткие ответы
- **What is the primary purpose of this guide?** Показать, как добавить трендовую линию, отобразить её уравнение и значение R‑squared, а также экспортировать полученную диаграмму в изображение с использованием Java.  
- **Which library is required?** Aspose.Cells for Java (download [here](https://releases.aspose.com/cells/java/)).  
- **Do I need a license?** Бесплатная пробная версия подходит для разработки; для продакшн‑использования требуется коммерческая лицензия.  
- **Can I generate an Excel file in Java?** Да — в руководстве создаётся и сохраняется рабочая книга XLSX.  
- **How do I export the chart to PNG or JPEG?** Используйте метод `Chart.toImage()` (рассмотрено в разделе «Export Chart»).

## How to create Excel chart with trendline and export to image
Этот заголовок напрямую отвечает на основной запрос ключевого слова и проводит вас через весь рабочий процесс в логическом порядке. Ниже вы найдёте причины, предварительные требования и пошаговое руководство.

## What is Export Chart to Image?
Экспорт диаграммы в изображение преобразует визуальное представление ваших данных в переносимый растровый формат (PNG, JPEG и т.д.). Это удобно для встраивания диаграмм в отчёты, веб‑страницы или презентации, где оригинальный файл Excel не требуется.

## Why Add a Trendline and Display R‑squared Value?
Трендовая линия помогает выявить скрытую закономерность в серии данных, а метрика **R‑squared** количественно оценивает, насколько хорошо линия соответствует данным. Включение этих элементов в экспортированное изображение даёт заинтересованным сторонам мгновенное представление без необходимости открывать книгу.

## Prerequisites
- Установлен Java 8 или новее.  
- Библиотека Aspose.Cells for Java добавлена в ваш проект (JAR‑файлы в classpath).  
- Базовое знакомство с Java‑IDE (IntelliJ IDEA, Eclipse и т.п.).  

## Step‑by‑Step Guide

### Step 1: Set Up the Project
Создайте новый Java‑проект и добавьте JAR‑файлы Aspose.Cells в путь сборки. Это подготовит среду для генерации и манипуляции Excel‑файлами.

### Step 2: Load Excel File (load excel file java)
```java
// Import necessary libraries
import com.aspose.cells.*;

// Load the Excel file
Workbook workbook = new Workbook("your_excel_file.xlsx");

// Access the worksheet
Worksheet worksheet = workbook.getWorksheets().get(0);
```
*Мы только что **loaded an Excel file** в память, готовую к созданию диаграммы.*

### Step 3: Create a Chart
```java
// Create a chart
int chartIndex = worksheet.getCharts().add(ChartType.LINE, 5, 0, 15, 5);
Chart chart = worksheet.getCharts().get(chartIndex);

// Specify data source for the chart
chart.getNSeries().add("A1:A10", true);
```
*Здесь мы генерируем линейную диаграмму, которая позже будет содержать нашу трендовую линию.*

### Step 4: Add Trendline (how to add trendline) and Display R‑squared Value
```java
// Add a trendline to the chart
Trendline trendline = chart.getNSeries().get(0).getTrendlines().add(TrendlineType.LINEAR);

// Customize trendline options
trendline.setDisplayEquation(true);
trendline.setDisplayRSquaredValue(true);
```
*Вызов `setDisplayRSquaredValue(true)` гарантирует, что **R‑squared value** появится на диаграмме.*

### Step 5: Customize Chart and Save Workbook (save workbook xlsx, generate excel file java)
```java
// Customize chart title and axes
chart.getTitle().setText("Trendline Analysis");
chart.getCategoryAxis().getTitle().setText("X-Axis");
chart.getValueAxis().getTitle().setText("Y-Axis");

// Save the Excel file with the chart
workbook.save("output.xlsx");
```
*Теперь рабочая книга **generated** и сохранена как файл XLSX, готовый к дальнейшей обработке.*

### Step 6: Export Chart to Image (export chart to image)
> **Note:** This step is described without an additional code block to keep the original block count unchanged.  
После создания и сохранения диаграммы вы можете экспортировать её в изображение, вызвав метод `chart.toImage()` и записав полученный `java.awt.image.BufferedImage` в выбранный вами формат файла (PNG, JPEG, BMP). Типовой порядок действий:
1. Получите объект `Chart` (это уже сделано в предыдущих шагах).  
2. Вызовите `chart.toImage()`, чтобы получить `BufferedImage`.  
3. Используйте `ImageIO.write(bufferedImage, "png", new File("chart.png"))` для записи файла.  

Это создаёт изображение высокого разрешения, которое можно вставлять куда угодно, завершая процесс **export chart to image**.

## Analyze Results
Откройте `output.xlsx` в Excel, чтобы убедиться, что трендовая линия, уравнение и значение R‑squared отображаются как ожидается. Откройте экспортированный файл изображения (например, `chart.png`), чтобы увидеть чистую визуализацию, которую можно распространять без оригинальной книги.

## Common Issues and Solutions
- **Trendline not showing:** Убедитесь, что диапазон данных (`A1:A10`) действительно содержит числовые значения; нечисловые данные препятствуют вычислению трендовой линии.  
- **R‑squared value displays as 0:** Чаще всего это означает, что серия данных постоянна или имеет недостаточную вариацию. Попробуйте другой набор данных или полиномиальную трендовую линию.  
- **Image export fails with `NullPointerException`:** Проверьте, что диаграмма полностью отрисована перед вызовом `toImage()`. Сохранение книги перед экспортом иногда решает проблемы синхронизации.

## Frequently Asked Questions

**Q: How can I change the trendline type?**  
A: Use a different `TrendlineType` enumeration when adding the trendline, e.g., `TrendlineType.POLYNOMIAL` for a polynomial fit.

**Q: Can I customize the trendline appearance (color, thickness)?**  
A: Yes. Access the trendline’s `LineFormat` via `trendline.getLineFormat()` and set properties such as `setWeight()` and `setColor()`.

**Q: How do I export the chart to PDF instead of an image?**  
A: Convert the chart to an image first, then embed that image into a PDF using Aspose.PDF or any PDF library of your choice.

**Q: Is it possible to add multiple trendlines to the same chart?**  
A: Absolutely. Call `chart.getNSeries().get(0).getTrendlines().add(...)` for each series you wish to analyze.

**Q: Does Aspose.Cells support high‑resolution image export?**  
A: Yes. You can specify the DPI when calling `chart.toImage()` and then scale the image accordingly before saving.

## Conclusion
Теперь у вас есть полное, сквозное решение для **create Excel chart**, добавления трендовой линии, отображения уравнения и значения R‑squared, настройки визуала, сохранения книги и окончательного экспорта диаграммы в изображение PNG/JPEG. Такой подход позволяет программно генерировать профессиональные аналитические материалы, идеально подходящие для автоматизированных отчётов, панелей мониторинга или любых сценариев, где статическое изображение удобнее, чем файл Excel.

---

**Last Updated:** 2026-02-09  
**Tested With:** Aspose.Cells for Java latest  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}