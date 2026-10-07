---
category: general
date: 2026-10-07
description: Узнайте, как создать PNG из диапазона и экспортировать данные в PNG в
  Java. Это руководство показывает, как сохранить изображение диапазона Excel с помощью
  Aspose.Cells.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create png from range
- export data as png
- save excel range image
- convert worksheet to png
- save cells as png
language: ru
lastmod: 2026-10-07
og_description: Создайте PNG из диапазона в Java и экспортируйте данные в PNG с помощью
  Aspose.Cells. Следуйте этому полному руководству, чтобы мгновенно сохранить изображение
  диапазона Excel.
og_image_alt: Screenshot of Java code that creates a PNG from an Excel range
og_title: Создание PNG из диапазона в Java – пошаговое руководство Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: Learn how to create PNG from range and export data as PNG in Java.
    This guide shows you how to save Excel range image using Aspose.Cells.
  headline: How to create PNG from range in Java with Aspose.Cells
  type: TechArticle
- description: Learn how to create PNG from range and export data as PNG in Java.
    This guide shows you how to save Excel range image using Aspose.Cells.
  name: How to create PNG from range in Java with Aspose.Cells
  steps:
  - name: Maven dependency
    text: '```xml <dependency> <groupId>com.aspose</groupId> <artifactId>aspose-cells</artifactId>
      <version>23.12</version> </dependency> ```'
  - name: Expected output
    text: '* A file named `PivotImage.png` located in `YOUR_DIRECTORY`. * The image
      shows the exact layout, fonts, colors, and borders from the selected range.
      * If the source range contains a pivot table, the rendered image includes the
      same styling and calculated values as displayed in Excel.'
  - name: Exporting a non‑contiguous range
    text: Aspose.Cells does not render disjoint ranges in a single image. To export
      multiple areas, create separate images for each range and combine them later
      with an image‑processing library (e.g., ImageIO).
  - name: Saving a large worksheet as PNG
    text: 'Rendering an entire sheet that spans thousands of rows can consume significant
      memory. Mitigate this by:'
  - name: Preserving cell formulas
    text: A PNG image is a raster format; formulas are not retained. If downstream
      consumers need the raw data, also export the range as CSV or JSON using `Range.exportDataTable()`.
  - name: Next steps
    text: '* Experiment with different `Resolution` values to balance quality and
      file size. * Use `ImageOrPrintOptions.setTransparent(true)` if you need a PNG
      with a transparent background. * Combine multiple range images into a single
      PDF using `PdfSaveOptions` for multi‑page reports. * Explore exporting to '
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: Как создать PNG из диапазона в Java с помощью Aspose.Cells
url: /ru/java/images-shapes/how-to-create-png-from-range-in-java-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как создать PNG из диапазона в Java с Aspose.Cells

Если вам нужно **создать PNG из диапазона** в рабочей книге Excel, этот учебник покажет, как это сделать. К концу руководства вы сможете **экспортировать данные как PNG**, сохранить изображение диапазона Excel и использовать файл в отчетах или веб‑страницах.

Вы увидите полностью готовую, исполняемую программу на Java, которая загружает рабочую книгу, выбирает нужные ячейки, рендерит их в PNG и сохраняет результат на диск. Внешние инструменты не требуются — всё обрабатывается внутри Aspose.Cells.

## Что покрывает этот учебник

* Предварительные требования и настройка Maven для Aspose.Cells
* Загрузка рабочей книги, содержащей сводную таблицу или любой диапазон данных
* Определение точного диапазона ячеек, который нужно конвертировать
* Настройка параметров изображения для вывода в PNG
* Рендеринг диапазона и сохранение PNG‑файла
* Распространённые подводные камни и советы для получения изображений высокого качества

После выполнения этих шагов вы сможете **конвертировать лист в PNG** для любого диапазона, будь то простая таблица или сложный сводный график.

## Предварительные требования

* Java 17 или новее (код компилируется с JDK 11+)
* Maven 3.6+ (или Gradle, если предпочитаете)
* Aspose.Cells for Java 23.12 или новее — добавьте зависимость, показанную ниже
* Существующий файл Excel (`PivotWithStyle.xlsx`), содержащий диапазон, который нужно захватить

> **Pro tip:** Если у вас нет лицензии, вы можете запросить временный оценочный ключ у Aspose. Библиотека работает в режиме оценки без дополнительной конфигурации.

### Maven‑зависимость

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version>
</dependency>
```

## Шаг 1: Загрузить рабочую книгу, содержащую целевой диапазон

Первой операцией является открытие файла Excel. Aspose.Cells читает файл в память без необходимости установки Microsoft Office.

```java
import com.aspose.cells.*;

public class PivotRangeToPng {
    public static void main(String[] args) throws Exception {
        // Load the workbook containing the data you want to export
        Workbook workbook = new Workbook("YOUR_DIRECTORY/PivotWithStyle.xlsx");
```

*Почему это важно*: Загрузка рабочей книги даёт доступ к листам, ячейкам и свойствам настройки страницы, необходимым для рендеринга.

## Шаг 2: Получить лист, содержащий диапазон

В большинстве книг лист по умолчанию находится на индексе 0, но можно также использовать имя листа.

```java
        // Retrieve the first worksheet (index 0)
        Worksheet worksheet = workbook.getWorksheets().get(0);
```

Если ваши данные находятся на другом листе, замените `0` на соответствующий индекс или используйте `workbook.getWorksheets().get("SheetName")`.

## Шаг 3: Определить диапазон ячеек, который нужно конвертировать

Можно указать любой прямоугольный участок, используя нотацию A1. В этом примере мы захватываем `A1:D15`, что может быть сводной таблицей или обычным блоком данных.

```java
        // Create a range object for cells A1:D15
        Range pivotRange = worksheet.getCells().createRange("A1:D15");
```

*Особый случай*: Когда диапазон включает объединённые ячейки, Aspose.Cells автоматически расширяет изображение, чтобы включить объединённую область.

## Шаг 4: Подготовить параметры PNG‑изображения

`ImageOrPrintOptions` позволяет управлять форматом, разрешением и другими деталями рендеринга. Установка формата сохранения в PNG гарантирует безпотерянное качество.

```java
        // Configure image options – we want a PNG file
        ImageOrPrintOptions imageOptions = new ImageOrPrintOptions();
        imageOptions.setSaveFormat(SaveFormat.PNG);
        // Optional: increase DPI for sharper output (default is 96)
        imageOptions.setImageFormat(ImageFormat.getPng());
        imageOptions.setResolution(150); // 150 DPI for clearer text
```

Увеличение DPI полезно, когда исходные ячейки содержат мелкий шрифт или детализированные графики.

## Шаг 5: Ограничить область рендеринга выбранным диапазоном

Назначив диапазон как область печати, Aspose.Cells рендерит только эти ячейки и игнорирует остальную часть листа.

```java
        // Set the print area so only the defined range is rendered
        worksheet.getPageSetup().setPrintArea(pivotRange.getRefersTo());
```

Если пропустить этот шаг, будет растеризован весь лист, что может расходовать память и создавать более крупный файл изображения.

## Шаг 6: Рендерить диапазон и добавить изображение на лист (по желанию)

Если нужно встроить сгенерированный PNG обратно в рабочую книгу (для предварительного просмотра), его можно добавить как картинку. Этот шаг необязателен для чистого экспорта.

```java
        // Add the rendered image back to the worksheet at cell (0,0) – optional
        worksheet.getPictures().add(0, 0, imageOptions);
```

*Зачем это может понадобиться*: Некоторые рабочие процессы требуют, чтобы изображение было частью книги перед распространением, например при создании печатного отчёта, сочетающего нативные ячейки и изображения.

## Шаг 7: Сохранить PNG‑файл на диск

Наконец, записываем изображение в файл. Метод `save` учитывает формат, указанный в `imageOptions`.

```java
        // Save the rendered PNG image to the specified path
        workbook.save("YOUR_DIRECTORY/PivotImage.png", SaveFormat.PNG);
    }
}
```

Когда программа завершится, `PivotImage.png` будет содержать пиксель‑точный снимок ячеек `A1:D15`.

### Ожидаемый результат

* Файл с именем `PivotImage.png`, расположенный в `YOUR_DIRECTORY`.
* На изображении точно воспроизведены макет, шрифты, цвета и границы выбранного диапазона.
* Если исходный диапазон содержит сводную таблицу, отрисованное изображение будет включать тот же стиль и вычисленные значения, что отображаются в Excel.

## Обработка типовых сценариев

### Экспорт несмежного диапазона

Aspose.Cells не рендерит разрозненные диапазоны в одном изображении. Чтобы экспортировать несколько областей, создайте отдельные изображения для каждого диапазона и объедините их позже с помощью библиотеки обработки изображений (например, ImageIO).

```java
Range first = worksheet.getCells().createRange("A1:B10");
Range second = worksheet.getCells().createRange("D1:E10");
// Render each range individually using the same ImageOrPrintOptions
```

### Сохранение большого листа в PNG

Рендеринг всего листа, охватывающего тысячи строк, может потреблять значительное количество памяти. Снизить нагрузку можно, выполнив следующее:

* Уменьшить DPI (`imageOptions.setResolution(72)`) для получения меньшего файла.
* Использовать `setPageCount`, чтобы ограничить количество рендеримых страниц.
* Экспортировать одну печатную страницу за раз через `worksheet.getPageSetup().setPrintArea(...)`.

### Сохранение формул ячеек

PNG — растровый формат; формулы не сохраняются. Если потребителям нужны исходные данные, экспортируйте диапазон также в CSV или JSON с помощью `Range.exportDataTable()`.

## Полный, исполняемый пример

Ниже приведён полный класс Java, который можно скопировать и вставить в свою IDE. Замените `YOUR_DIRECTORY` на абсолютный или относительный путь на вашем компьютере.

```java
import com.aspose.cells.*;

public class PivotRangeToPng {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load the workbook containing the data
        Workbook workbook = new Workbook("YOUR_DIRECTORY/PivotWithStyle.xlsx");

        // 2️⃣ Access the first worksheet (adjust index or name as needed)
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // 3️⃣ Define the exact cell range you want to convert (A1:D15 in this case)
        Range pivotRange = worksheet.getCells().createRange("A1:D15");

        // 4️⃣ Prepare PNG image options – set format and optional resolution
        ImageOrPrintOptions imageOptions = new ImageOrPrintOptions();
        imageOptions.setSaveFormat(SaveFormat.PNG);
        imageOptions.setResolution(150); // sharper output

        // 5️⃣ Restrict rendering to the selected range
        worksheet.getPageSetup().setPrintArea(pivotRange.getRefersTo());

        // 6️⃣ (Optional) Add the rendered image back to the worksheet for preview
        worksheet.getPictures().add(0, 0, imageOptions);

        // 7️⃣ Save the PNG file – this creates the final image on disk
        workbook.save("YOUR_DIRECTORY/PivotImage.png", SaveFormat.PNG);
    }
}
```

Запустите программу командой `mvn compile exec:java` (или используйте предпочитаемый инструмент сборки). После выполнения откройте `PivotImage.png`, чтобы убедиться в результате.

## Заключение

Теперь вы знаете, как **создать PNG из диапазона** в Java с помощью Aspose.Cells, эффективно **экспортировать данные как PNG** и **сохранить изображение диапазона Excel** для любых отчётов или сценариев обмена. Шаги — загрузка книги, определение диапазона, настройка параметров изображения, установка области печати и сохранение файла — покрывают весь процесс **конвертации листа в PNG** и **сохранения ячеек как PNG**.

### Что делать дальше

* Поэкспериментируйте с различными значениями `Resolution`, чтобы найти баланс между качеством и размером файла.
* Используйте `ImageOrPrintOptions.setTransparent(true)`, если нужен PNG с прозрачным фоном.
* Объедините несколько изображений диапазонов в один PDF с помощью `PdfSaveOptions` для многостраничных отчётов.
* Исследуйте экспорт в другие растровые форматы (JPEG, BMP), изменив `setSaveFormat`.

Не стесняйтесь адаптировать этот шаблон для графиков, таблиц или даже целых листов. Приятного кодинга!

## Что следует изучить дальше?

Следующие учебники охватывают тесно связанные темы, расширяющие техники, продемонстрированные в этом руководстве. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы в собственных проектах.

- [How to Export an Excel Worksheet to PNG Using Aspose.Cells Java](/cells/english/java/workbook-operations/export-excel-to-png-aspose-cells-java/)
- [Convert Excel to PNG Using Aspose.Cells for Java: A Step‑By‑Step Guide](/cells/english/java/workbook-operations/convert-excel-to-png-aspose-cells-java/)
- [Create Union Range in Excel using Aspose.Cells Java: A Comprehensive Guide](/cells/english/java/range-management/create-union-range-excel-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}