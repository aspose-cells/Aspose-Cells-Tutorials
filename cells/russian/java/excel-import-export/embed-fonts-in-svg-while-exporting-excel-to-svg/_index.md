---
category: general
date: 2026-08-14
description: Встраивание шрифтов в SVG при экспорте Excel в SVG с помощью Aspose.Cells.
  Узнайте, как задать область печати, установить параметры печати и использовать функцию
  WRAPCOLS.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- embed fonts in svg
- export excel to svg
- set print area
- set print options
- use wrapcols function
language: ru
lastmod: 2026-08-14
og_description: Встраивание шрифтов в SVG при экспорте Excel в SVG с помощью Aspose.Cells.
  В этом руководстве показано, как установить область печати, настроить параметры
  печати и применить функцию WRAPCOLS.
og_image_alt: Screenshot of Java code exporting an Excel sheet to SVG with embedded
  fonts
og_title: Встраивание шрифтов в SVG при экспорте Excel в SVG – пошагово
schemas:
- author: Aspose
  dateModified: '2026-08-14'
  description: Embed fonts in SVG while exporting Excel to SVG using Aspose.Cells.
    Learn how to set print area, set print options, and use WRAPCOLS function.
  headline: Embed fonts in SVG while exporting Excel to SVG
  type: TechArticle
- description: Embed fonts in SVG while exporting Excel to SVG using Aspose.Cells.
    Learn how to set print area, set print options, and use WRAPCOLS function.
  name: Embed fonts in SVG while exporting Excel to SVG
  steps:
  - name: Run the program.
    text: Run the program.
  - name: Open `output.svg` in a web browser.
    text: Open `output.svg` in a web browser.
  - name: Confirm that the text uses the same typeface as the original Excel file
      (fonts are embedded).
    text: Confirm that the text uses the same typeface as the original Excel file
      (fonts are embedded).
  - name: Verify that only the cells within `A1:H30` appear and that the data from
      `A2:A10` is displayed in three columns.
    text: Verify that only the cells within `A1:H30` appear and that the data from
      `A2:A10` is displayed in three columns.
  type: HowTo
tags:
- Aspose.Cells
- Java
- SVG
title: Встраивание шрифтов в SVG при экспорте Excel в SVG
url: /ru/java/excel-import-export/embed-fonts-in-svg-while-exporting-excel-to-svg/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Встраивание шрифтов в SVG при экспорте Excel в SVG

Если вам нужно **встраивать шрифты в SVG при экспорте Excel в SVG**, этот учебник покажет, как сделать это с помощью Aspose.Cells for Java. Мы также рассмотрим, как **установить область печати**, **задать параметры печати** и **использовать функцию WRAPCOLS** для форматирования данных без потери макета.

Вы пройдёте полный, исполняемый пример, который загружает существующую книгу, применяет формулу `WRAPCOLS`, настраивает специфические для SVG параметры изображения, определяет область печати и, наконец, сохраняет файл как SVG с встроенными шрифтами. Внешняя документация не требуется — просто скопируйте код, запустите его и проверьте полученный SVG.

## Встраивание шрифтов в SVG — настройка ImageOrPrintOptions

Встраивание шрифтов гарантирует, что SVG отображается точно так же, как в Excel, даже на компьютерах, где оригинальные шрифты не установлены.

```java
// Create ImageOrPrintOptions for SVG output
ImageOrPrintOptions imgOptions = new ImageOrPrintOptions();
imgOptions.setImageFormat(ImageFormat.SVG);          // Target format
imgOptions.setEmbedFonts(true);                     // <-- embed fonts in SVG
imgOptions.setFontVariationSelectors(true);        // Preserve variation selectors
```

*Почему это важно*: Когда включено `setEmbedFonts(true)`, Aspose.Cells записывает данные шрифта непосредственно в раздел `<defs>` SVG. В результате получается автономный файл, который выглядит одинаково во всех браузерах и платформах.

## Экспорт Excel в SVG — полный рабочий процесс

Следующие шаги иллюстрируют процесс от начала до конца: от загрузки книги до сохранения SVG‑файла.

```java
// Step 1: Load a workbook and access the first worksheet
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
Worksheet ws = workbook.getWorksheets().get(0);

// Step 2: Apply the WRAPCOLS formula to cell A1
Cell cell = ws.getCells().get("A1");
cell.setFormula("=WRAPCOLS(A2:A10,3)");

// Step 3: Configure image options (see previous section)
ImageOrPrintOptions imgOptions = new ImageOrPrintOptions();
imgOptions.setImageFormat(ImageFormat.SVG);
imgOptions.setEmbedFonts(true);
imgOptions.setFontVariationSelectors(true);

// Step 4: Define the print area and assign the image options
ws.getPageSetup().setPrintArea("A1:H30");           // <-- set print area
ws.getPageSetup().setPrintOptions(imgOptions);     // <-- set print options

// Step 5: Save the worksheet as an SVG file
ws.getPageSetup().save("YOUR_DIRECTORY/output.svg", SaveFormat.SVG);
```

**Ожидаемый результат**: `output.svg` появляется в `YOUR_DIRECTORY`. При открытии в браузере отображается лист с встроенными шрифтами, данные разбиты на три столбца (благодаря `WRAPCOLS`), и отрисованы только ячейки в диапазоне `A1:H30`.

## Установка области печати для листа

Определение области печати ограничивает экспортируемый SVG определённым диапазоном, что уменьшает размер файла и фокусирует просмотр на нужных данных.

```java
// Define a rectangular region that will be exported
ws.getPageSetup().setPrintArea("A1:H30");   // you can change the range as needed
```

*Совет*: Диапазон задаётся в нотации A1 Excel. Если нужна динамическая область, её можно вычислить программно с помощью `ws.getCells().getMaxDisplayRange()`.

## Установка параметров печати для вывода SVG

Параметры печати управляют тем, как Aspose.Cells преобразует лист в изображение. Помимо встраивания шрифтов, можно настроить разрешение, масштабирование и макет страницы.

```java
// Assign the previously configured ImageOrPrintOptions
ws.getPageSetup().setPrintOptions(imgOptions);
```

*Почему следует задавать параметры печати*: Без явных параметров Aspose.Cells использует значения по умолчанию, которые могут не включать встраивание шрифтов или применять нежелательный коэффициент масштабирования, что приводит к размытым или некорректно стилизованным SVG.

## Использование функции WRAPCOLS для переноса данных по столбцам

`WRAPCOLS` — формула Excel, которая распределяет вертикальный диапазон по заданному количеству столбцов. Это удобно, когда нужно отобразить длинный список в компактной сетке.

```java
// Insert the WRAPCOLS formula into cell A1
cell.setFormula("=WRAPCOLS(A2:A10,3)");
```

При сохранении книги Aspose.Cells вычисляет формулу, создавая трёхколоночный макет внутри определённой области печати. Эта техника работает для любого размера диапазона — просто измените второй аргумент на нужное количество столбцов.

## Полный исполняемый пример

Ниже приведена полная Java‑программа, которую можно вставить в любую IDE. Убедитесь, что библиотека Aspose.Cells for Java находится в вашем classpath.

```java
import com.aspose.cells.*;

public class ExportExcelToSvg {
    public static void main(String[] args) throws Exception {
        // Load the source workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
        Worksheet ws = workbook.getWorksheets().get(0);

        // Apply WRAPCOLS to reorganize data
        Cell wrapCell = ws.getCells().get("A1");
        wrapCell.setFormula("=WRAPCOLS(A2:A10,3)");

        // Configure SVG options with embedded fonts
        ImageOrPrintOptions imgOptions = new ImageOrPrintOptions();
        imgOptions.setImageFormat(ImageFormat.SVG);
        imgOptions.setEmbedFonts(true);
        imgOptions.setFontVariationSelectors(true);

        // Set the region that will appear in the SVG
        ws.getPageSetup().setPrintArea("A1:H30");

        // Attach the image options to the worksheet
        ws.getPageSetup().setPrintOptions(imgOptions);

        // Export the worksheet as an SVG file
        ws.getPageSetup().save("YOUR_DIRECTORY/output.svg", SaveFormat.SVG);

        System.out.println("SVG exported successfully with embedded fonts.");
    }
}
```

**Шаги проверки**

1. Запустите программу.  
2. Откройте `output.svg` в веб‑браузере.  
3. Убедитесь, что текст использует тот же шрифт, что и оригинальный файл Excel (шрифты встроены).  
4. Проверьте, что отображаются только ячейки в диапазоне `A1:H30`, а данные из `A2:A10` показаны в трёх столбцах.

## Распространённые проблемы и как их избежать

| Проблема | Почему происходит | Как исправить |
|----------|-------------------|---------------|
| Шрифты отсутствуют в SVG | `setEmbedFonts(false)` или файл шрифта недоступен | Убедитесь, что `setEmbedFonts(true)` и шрифт установлен на машине, где выполняется код |
| WRAPCOLS не вычисляется | Движок вычислений отключён | Вызовите `workbook.calculateFormula()` перед экспортом или позвольте Aspose.Cells вычислить при сохранении |
| Экспортированный SVG пустой | Область печати не содержит данных | Дважды проверьте диапазон, передаваемый в `setPrintArea` |
| SVG‑файл огромный | Не применено масштабирование, высокое разрешение изображения | Отрегулируйте `imgOptions.setResolution(96)` или аналогичное значение для контроля DPI |

## Совет профессионала: повторное использование ImageOrPrintOptions для нескольких листов

Если ваша книга содержит несколько листов, которым нужны одинаковые настройки SVG, создайте один экземпляр `ImageOrPrintOptions` и назначьте его каждому `PageSetup` листа. Это уменьшает потребление памяти и гарантирует единообразное встраивание шрифтов во всех экспортированных файлах.

```java
ImageOrPrintOptions sharedOptions = new ImageOrPrintOptions();
sharedOptions.setImageFormat(ImageFormat.SVG);
sharedOptions.setEmbedFonts(true);
sharedOptions.setFontVariationSelectors(true);

for (int i = 0; i < workbook.getWorksheets().getCount(); i++) {
    Worksheet sheet = workbook.getWorksheets().get(i);
    sheet.getPageSetup().setPrintOptions(sharedOptions);
    sheet.getPageSetup().setPrintArea("A1:H30");
    sheet.getPageSetup().save("YOUR_DIRECTORY/sheet" + i + ".svg", SaveFormat.SVG);
}
```

## Следующие шаги

* **Экспорт в другие векторные форматы** — замените `ImageFormat.SVG` на `ImageFormat.PDF` для PDF высокого качества.  
* **Пакетная обработка** — пройдитесь по папке с файлами `.xlsx` и автоматически генерируйте SVG.  
* **Работа с пользовательскими шрифтами** — используйте `FontSettings` для загрузки шрифтов из конкретного каталога, если системных шрифтов недостаточно.  

Освоив **embed fonts in SVG**, **export excel to svg**, **set print area**, **set print options** и **use WRAPCOLS function**, вы сможете автоматизировать создание SVG‑файлов высокого качества для отчётов, панелей мониторинга и веб‑визуализаций напрямую из данных Excel. Приятного кодинга!

## Что изучать дальше?

В следующих учебниках рассматриваются тесно связанные темы, которые расширяют техники, продемонстрированные в этом руководстве. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы к реализации в ваших проектах.

- [How to Set a Print Area in Excel Using Aspose.Cells for .NET](/cells/english/net/headers-footers/set-print-area-excel-aspose-cells-net/)
- [Set Print Area Excel Aspose Cells Net](/cells/german/net/headers-footers/set-print-area-excel-aspose-cells-net/)
- [Set Print Area Excel Aspose Cells Net](/cells/french/net/headers-footers/set-print-area-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}