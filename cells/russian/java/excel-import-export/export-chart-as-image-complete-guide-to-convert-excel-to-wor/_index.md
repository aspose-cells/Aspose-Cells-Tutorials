---
category: general
date: 2026-06-30
description: Экспортируйте диаграмму как изображение и узнайте, как экспортировать
  диаграмму, сохранить Excel в Word, конвертировать Excel в Word и преобразовать XLSX
  в DOCX за несколько простых шагов.
draft: false
keywords:
- export chart as image
- how to export chart
- save excel as word
- convert excel to word
- convert xlsx to docx
language: ru
og_description: Экспортируйте диаграмму как изображение и быстро преобразуйте Excel
  в Word. Следуйте этому руководству, чтобы сохранить Excel в Word, экспортировать
  диаграммы и конвертировать XLSX в DOCX.
og_title: Экспорт диаграммы как изображения – пошаговое преобразование Excel в Word
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Export chart as image and learn how to export chart, save Excel as
    Word, convert Excel to Word, and convert XLSX to DOCX in a few easy steps.
  headline: Export Chart as Image – Complete Guide to Convert Excel to Word
  type: TechArticle
- description: Export chart as image and learn how to export chart, save Excel as
    Word, convert Excel to Word, and convert XLSX to DOCX in a few easy steps.
  name: Export Chart as Image – Complete Guide to Convert Excel to Word
  steps:
  - name: What if my workbook has multiple charts?
    text: You don’t need to change anything—setting `setExportChartAsImage(true)`
      applies to **all** charts in the workbook. If you only want specific charts
      as images, you’ll have to export them manually using `chart.toImage()` and then
      insert them into the Word file yourself.
  - name: Can I control the image format (PNG vs JPEG)?
    text: 'Aspose.Cells uses PNG by default for chart‑as‑image exports. To switch
      to JPEG, you can adjust the `ImageOrPrintOptions` before saving:'
  - name: Does this work with older Excel files (.xls)?
    text: Absolutely. The same code works for both `.xls` and `.xlsx`. Aspose.Cells
      auto‑detects the format, so you can **save Excel as Word** regardless of the
      source version.
  - name: How does this differ from “convert Excel to Word” with native Office interop?
    text: Native interop often requires a Windows machine with Office installed, and
      charts may lose fidelity. Using Aspose.Cells is platform‑agnostic, works on
      Linux/macOS, and preserves chart quality by rasterizing them.
  type: HowTo
tags:
- Excel
- Word
- Chart
- Java
- Aspose.Cells
title: Экспорт диаграммы как изображения – Полное руководство по конвертации Excel
  в Word
url: /ru/java/excel-import-export/export-chart-as-image-complete-guide-to-convert-excel-to-wor/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Экспорт диаграммы как изображения – Полное руководство по конвертации Excel в Word

Когда‑нибудь задавались вопросом, как экспортировать диаграмму как изображение из книги Excel и сразу вставить её в документ Word? Вы не одиноки — разработчики постоянно спрашивают: «Как экспортировать диаграмму из XLSX и встроить её в DOCX без потери качества?»

Хорошая новость в том, что с помощью нескольких строк Java‑кода вы можете **экспортировать диаграмму как изображение**, а затем **сохранить Excel как Word** в одном бесшовном процессе. В этом руководстве мы пройдем весь процесс, от загрузки книги до настройки параметров сохранения, которые превращают ваши диаграммы в чёткие PNG‑изображения внутри DOCX‑файла.

Мы также коснёмся связанных задач, таких как **convert Excel to Word**, **save Excel as Word** и **convert XLSX to DOCX** — всё это при сохранении кода чистым и исполняемым. Без лишних слов, только практическое решение, которое вы можете скопировать‑вставить уже сегодня.

---

## Что вам понадобится

Прежде чем погрузиться в детали, убедитесь, что у вас есть следующее:

- **Java Development Kit (JDK) 8+** — код работает на любой современной JDK.
- Библиотека **Aspose.Cells for Java** (версия 23.10 или новее). Её можно получить из Maven Central или скачать JAR‑файл напрямую.
- **Файл Excel** (`charts.xlsx`), содержащий хотя бы одну диаграмму, которую вы хотите экспортировать.
- **IDE для Java** (IntelliJ IDEA, Eclipse или VS Code) — подойдёт любой.
- Базовое знакомство с Java и Maven/Gradle (необязательно, но полезно).

Вот и всё. Никаких дополнительных плагинов, никакого COM‑interop, только чистый Java.

---

## Шаг 1: Загрузка книги Excel и поиск диаграммы

Первое, что нам нужно сделать, — открыть книгу, в которой находится диаграмма. Aspose.Cells делает это проще простого — достаточно указать путь к файлу.

```java
// Step 1: Load the Excel workbook that contains the chart
Workbook workbook = new Workbook("YOUR_DIRECTORY/charts.xlsx");

// Grab the first worksheet (index 0) and its first chart (index 0)
Chart chart = workbook.getWorksheets().get(0).getCharts().get(0);
```

> **Почему это важно:** Загрузка книги даёт нам доступ к объекту диаграммы, который позже мы попросим Aspose отрисовать как изображение. Если в книге несколько листов или диаграмм, вы можете изменить индексы или пройтись по ним в цикле.

---

## Шаг 2: Настройка параметров сохранения DOCX для экспорта диаграмм как изображений

Aspose.Cells предоставляет класс `DocxSaveOptions`, позволяющий управлять процессом конвертации. Установка `setExportChartAsImage(true)` сообщает библиотеке растеризовать каждую диаграмму в изображение перед вставкой в Word‑файл.

```java
// Step 2: Create DOCX save options and enable chart‑as‑image export
DocxSaveOptions saveOptions = new DocxSaveOptions();
saveOptions.setExportChartAsImage(true); // This is the key line
```

> **Совет:** Если вам нужны векторные графики (EMF/WMF), можно оставить этот флаг выключенным, но растровые изображения обычно отображаются более последовательно во всех версиях Word.

---

## Шаг 3: Сохранение книги как DOCX‑файл

Теперь, когда параметры заданы, просто сохраняем книгу. Библиотека сама преобразует все листы, таблицы и — благодаря установленному флагу — диаграммы в изображения.

```java
// Step 3: Save the workbook as a DOCX file, applying the chart‑export option
workbook.save("YOUR_DIRECTORY/charts.docx", saveOptions);
```

> **Что вы получаете:** Файл `charts.docx`, где оригинальная диаграмма Excel представлена в виде высококачественного PNG (или JPEG, в зависимости от настроек) внутри документа Word. Откройте его в Microsoft Word, чтобы увидеть результат.

---

## Шаг 4: Проверка результата (необязательно, но рекомендуется)

Всегда полезно программно убедиться, что конвертация прошла успешно, особенно при автоматизации пакетных процессов.

```java
// Optional: Verify that the DOCX file exists and is not empty
File docxFile = new File("YOUR_DIRECTORY/charts.docx");
if (docxFile.exists() && docxFile.length() > 0) {
    System.out.println("Success! DOCX created with chart as image.");
} else {
    System.err.println("Conversion failed – check the source file and options.");
}
```

Если вы запустите фрагмент и увидите сообщение об успехе, вы успешно **convert XLSX to DOCX**, сохранив визуальные элементы диаграмм в виде изображений.

---

## Полный рабочий пример

Ниже представлен полностью готовый к запуску Java‑программный код, объединяющий все шаги. Просто замените `YOUR_DIRECTORY` на реальный путь к вашей папке.

```java
import com.aspose.cells.*;

import java.io.File;

public class ExportChartAsImageDemo {
    public static void main(String[] args) throws Exception {
        // Load the Excel workbook containing the chart
        Workbook workbook = new Workbook("YOUR_DIRECTORY/charts.xlsx");

        // Access the first worksheet and its first chart
        Chart chart = workbook.getWorksheets().get(0).getCharts().get(0);
        if (chart == null) {
            System.err.println("No chart found in the first worksheet.");
            return;
        }

        // Configure DOCX save options to export charts as images
        DocxSaveOptions saveOptions = new DocxSaveOptions();
        saveOptions.setExportChartAsImage(true);   // Export chart as image

        // Save as DOCX
        String outputPath = "YOUR_DIRECTORY/charts.docx";
        workbook.save(outputPath, saveOptions);

        // Verify the output file
        File outFile = new File(outputPath);
        if (outFile.exists() && outFile.length() > 0) {
            System.out.println("File saved successfully: " + outputPath);
        } else {
            System.err.println("Failed to create the DOCX file.");
        }
    }
}
```

**Ожидаемый вывод при запуске программы:**

```
File saved successfully: YOUR_DIRECTORY/charts.docx
```

Откройте `charts.docx` в Microsoft Word, и вы увидите диаграмму, отрисованную как чистое изображение, точно на том месте, где она находилась в оригинальном Excel‑файле.

---

## Часто задаваемые вопросы и особые случаи

### Что делать, если в книге несколько диаграмм?

Менять ничего не нужно — установка `setExportChartAsImage(true)` применяется ко **всем** диаграммам в книге. Если нужны изображения только для отдельных диаграмм, придётся экспортировать их вручную через `chart.toImage()` и вставлять в Word самостоятельно.

### Можно ли управлять форматом изображения (PNG vs JPEG)?

Aspose.Cells по умолчанию использует PNG для экспорта диаграмм как изображений. Чтобы переключиться на JPEG, измените `ImageOrPrintOptions` перед сохранением:

```java
ImageOrPrintOptions imgOptions = new ImageOrPrintOptions();
imgOptions.setImageFormat(ImageFormat.getJpeg());
saveOptions.setImageOrPrintOptions(imgOptions);
```

### Работает ли это с более старыми файлами Excel (.xls)?

Абсолютно. Тот же код подходит как для `.xls`, так и для `.xlsx`. Aspose.Cells автоматически определяет формат, так что вы можете **save Excel as Word** независимо от версии исходного файла.

### Чем это отличается от «convert Excel to Word» с помощью нативного Office‑interop?

Нативный interop часто требует Windows‑машины с установленным Office, а диаграммы могут терять точность. Aspose.Cells кросс‑платформенный, работает на Linux/macOS и сохраняет качество диаграмм за счёт их растеризации.

---

## Советы для production‑готовых реализаций

- **Пакетная обработка:** Пройдитесь по каталогу с XLSX‑файлами, применяя одинаковый `DocxSaveOptions`. Оберните конвертацию в `try‑catch`, чтобы корректно обрабатывать повреждённые файлы.
- **Управление памятью:** Для очень больших книг вызывайте `workbook.dispose()` после сохранения, чтобы освободить нативные ресурсы.
- **Настройка:** Можно также установить `saveOptions.setPreserveCellFormatting(true)`, если требуется сохранить стили ячеек при конвертации.
- **Логирование:** Интегрируйте фреймворк логирования (SLF4J, Log4j) для сбора статистики конвертации — полезно для аудита.

---

## Заключение

Теперь у вас есть надёжное сквозное решение, которое **export chart as image**, **save Excel as Word** и **convert XLSX to DOCX** всего несколькими строками Java‑кода. Главное, что `DocxSaveOptions` в Aspose.Cells делает работу с диаграммами простой — без ручного извлечения изображений, без COM‑interop и с полной кросс‑платформенной поддержкой.

Экспериментируйте: пробуйте экспортировать несколько листов, меняйте разрешение изображений или комбинируйте этот подход с другими библиотеками Aspose (например, Aspose.Words) для создания ещё более богатых Word‑документов. Возможности безграничны, когда вы знаете, как правильно экспортировать диаграмму.

Есть вопросы о конвертации Excel‑файлов, встраивании изображений или оптимизации производительности? Оставляйте комментарий ниже, и happy coding!

## Что изучать дальше?

Следующие руководства охватывают тесно связанные темы, расширяющие техники, продемонстрированные в этом руководстве. Каждый ресурс включает полностью рабочие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы в собственных проектах.

- [Convert Excel Chart to Image with Aspose.Cells .NET](/cells/english/net/charts-graphs/convert-excel-chart-image-aspose-cells-dotnet/)
- [How to Create Excel Chart with Trendline and Export to Image using Aspose.Cells for Java](/cells/english/java/advanced-excel-charts/trendline-analysis/)
- [Convert Excel Pie Chart to Image Using Aspose.Cells .NET: A Step‑by‑Step Guide](/cells/english/net/charts-graphs/convert-excel-pie-chart-image-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}