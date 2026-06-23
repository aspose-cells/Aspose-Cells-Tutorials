---
category: general
date: 2026-03-01
description: Узнайте, как встраивать шрифты в HTML и другие форматы. Пошаговое руководство,
  охватывающее встраивание шрифтов в HTML, конвертацию Excel в HTML, экспорт OLE и
  преобразование Excel в XPS.
draft: false
keywords:
- how to embed fonts
- embed fonts in html
- convert excel to html
- how to export ole
- convert excel to xps
language: ru
og_description: Как встраивать шрифты в HTML, XPS и OLE‑экспорты. Узнайте полный рабочий
  процесс, посмотрите работающий код Java и освоите встраивание шрифтов в HTML для
  конвертации в Excel.
og_title: Как встраивать шрифты – Полный учебник по Java
tags:
- Aspose.Cells
- Java
- Document Export
title: Как встраивать шрифты — Полное руководство по экспорту в HTML, XPS и OLE
url: /ru/java/ole-objects-embedded-content/how-to-embed-fonts-complete-guide-for-html-xps-and-ole-expor/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как встраивать шрифты – Полное руководство для HTML, XPS и OLE‑экспорта

Когда‑нибудь задумывались **как встраивать шрифты**, преобразуя книгу Excel в веб‑страницу или печатный документ? Вы не одиноки. Многие разработчики сталкиваются с тем, что вывод выглядит правильно на их машине, но ломается на другой, потому что требуемые шрифты отсутствуют.  

В этом руководстве мы пройдём реальный сценарий с использованием Aspose.Cells for Java: встраивание шрифтов в HTML, сохранение вариантов эмодзи при конвертации в XPS и даже сохранение редактируемого OLE‑объекта при экспорте в PPTX. К концу вы получите готовое решение «копировать‑вставить», отвечающее на вопрос «как встраивать шрифты», а также охватывающее **embed fonts in html**, **convert excel to html**, **how to export ole** и **convert excel to xps**.

## Требования

- Java 17 (или любой современный JDK)  
- Aspose.Cells for Java 25.x или новее  
- Среда разработки (IntelliJ IDEA, Eclipse или VS Code)  
- Базовое знакомство со структурами данных Excel  

Внешние сервисы не требуются — всё работает локально.

## Обзор решения

1. **Создать книгу** и использовать функцию `WRAPCOLS` для преобразования вертикального диапазона в трёхколоночный макет.  
2. **Сохранить книгу как XPS**, включив селекторы вариаций шрифтов, чтобы эмодзи оставались неизменными.  
3. **Экспортировать в HTML** с встраиванием шрифтов, гарантируя одинаковый вид страницы везде.  
4. **Экспортировать книгу, содержащую OLE‑объект, в PPTX**, сохраняя возможность редактирования.  
5. **Применить шаблон Smart Marker**, демонстрирующий привязку данных master‑detail.  

Каждый шаг выделен в отдельный раздел H2, что облегчает быстрый просмотр как для поисковых систем, так и для AI‑ассистентов.

![Иллюстрация по встраиванию шрифтов](image.png "как встраивать шрифты")

*Image alt text: диаграмма, показывающая рабочий процесс от Excel к HTML, XPS и PPTX.*

---

## Шаг 1 – Создать книгу и использовать WRAPCOLS (Почему это важно для embed fonts in html)

Прежде чем говорить о встраивании шрифтов, нам нужна книга, содержащая данные. Функция `WRAPCOLS` удобно разбивает один столбец на несколько, что часто делает итоговый HTML более читаемым.

```java
import com.aspose.cells.*;

public class EmbedFontsDemo {
    public static void main(String[] args) throws Exception {
        // Initialize a new workbook
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.getWorksheets().get(0);

        // Populate A2:A10 with sample data
        for (int i = 2; i <= 10; i++) {
            sheet.getCells().get("A" + i).putValue("Item " + (i - 1));
        }

        // Use WRAPCOLS to create a 3‑column block starting at A1
        Cell resultCell = sheet.getCells().get("A1");
        resultCell.setFormula("=WRAPCOLS(A2:A10,3)");
        workbook.calculateFormula();

        System.out.println("WRAPCOLS result: " + resultCell.getStringValue());
        // -----------------------------------------------------------------
        // The rest of the steps are demonstrated after this point.
        // -----------------------------------------------------------------
```

**Зачем этот шаг?**  
Вызов `WRAPCOLS` генерирует многоколоночный диапазон, который позже появляется в HTML в виде таблицы. Когда мы **embed fonts in html**, стили таблицы будут опираться на встраиваемые шрифты, обеспечивая единообразный рендеринг во всех браузерах.

---

## Шаг 2 – Сохранить книгу как XPS, сохранив эмодзи (convert excel to xps)

Если нужен готовый к печати формат, XPS — надёжный выбор. Однако современные документы часто содержат эмодзи или символы с селекторами вариаций. Включение `EnableFontVariationSelectors` гарантирует, что эти символы сохранятся при конвертации.

```java
        // --------------------------------------------------------------
        // Step 2: Save as XPS with font variation selectors enabled
        // --------------------------------------------------------------
        WorkbookSettings settings = workbook.getSettings();
        settings.setEnableFontVariationSelectors(true); // crucial for emoji

        String xpsPath = "output/withVariations.xps";
        workbook.save(xpsPath, SaveFormat.XPS);
        System.out.println("Workbook saved as XPS at: " + xpsPath);
```

**Что вы получаете:**  
Файл XPS, отображающий любые встроенные эмодзи точно так же, как в исходной книге. Это удовлетворяет требование **convert excel to xps** и демонстрирует, что работа со шрифтами не ограничивается только HTML.

---

## Шаг 3 – Экспортировать в HTML с встраиванием шрифтов (how to embed fonts & embed fonts in html)

Теперь переходим к основной части руководства: **how to embed fonts** при преобразовании Excel в HTML. Aspose.Cells позволяет встраивать шрифты непосредственно в генерируемый HTML‑файл, устраняя необходимость внешних файлов шрифтов.

```java
        // --------------------------------------------------------------
        // Step 3: Export to HTML with embedded fonts
        // --------------------------------------------------------------
        HtmlSaveOptions htmlOptions = new HtmlSaveOptions();
        htmlOptions.setEmbedFonts(true); // this is the key line for embed fonts in html
        htmlOptions.setExportImagesAsBase64(true); // optional, keeps all assets in one file

        String htmlPath = "output/embeddedFonts.html";
        workbook.save(htmlPath, htmlOptions);
        System.out.println("HTML with embedded fonts saved at: " + htmlPath);
```

**Как это работает:**  
`setEmbedFonts(true)` заставляет рендерер читать файлы шрифтов, используемые в книге, и встраивать их как Base64‑закодированные правила `@font-face` внутри тега `<style>`. Полученный HTML является автономным, поэтому его можно разместить на любом сервере, и шрифты отобразятся корректно — именно то, что ищут разработчики, вводя запрос **how to embed fonts**.

**Ожидаемый фрагмент вывода (внутри `embeddedFonts.html`):**

```html
<style>
@font-face{font-family:"Arial";src:url(data:font/ttf;base64,AAEAAA... ) format('truetype');}
</style>
<table>
  <tr><td>Item 1</td><td>Item 4</td><td>Item 7</td></tr>
  <tr><td>Item 2</td><td>Item 5</td><td>Item 8</td></tr>
  <tr><td>Item 3</td><td>Item 6</td><td>Item 9</td></tr>
</table>
```

Обратите внимание на правило `@font-face — это конкретный ответ на **embed fonts in html**.

---

## Шаг 4 – Экспортировать книгу с OLE‑объектом в PPTX (how to export ole)

Во многих бизнес‑отчётах встраиваются документы Word, PDF или другие листы Excel в виде OLE‑объектов. При экспорте такой книги в PowerPoint часто теряется возможность редактировать объект. Aspose.Cells сохраняет редактируемость «из коробки».

```java
        // --------------------------------------------------------------
        // Step 4: Export a workbook with an OLE object to PPTX
        // --------------------------------------------------------------
        // Load a workbook that already contains an OLE object.
        Workbook oleWorkbook = new Workbook("input/oleObject.xlsx");

        String pptxPath = "output/oleEditable.pptx";
        oleWorkbook.save(pptxPath, SaveFormat.PPTX);
        System.out.println("PPTX with editable OLE object saved at: " + pptxPath);
```

**Почему это важно:**  
Если вы ищете **how to export ole**, этот фрагмент показывает точный вызов API. Полученный слайд PowerPoint содержит OLE‑объект как живой элемент, двойной клик — редактирование, без дополнительной пост‑обработки.

---

## Шаг 5 – Применить шаблон Smart Marker (master‑detail) и завершить демонстрацию

Smart Markers позволяют привязывать источник данных (Map, JSON, DataTable) напрямую к шаблону Excel. Ниже минимальный пример, выводящий строки master‑detail.

```java
        // --------------------------------------------------------------
        // Step 5: Apply Smart Marker template (master‑detail)
        // --------------------------------------------------------------
        String smartMarkerTemplate = "${Orders.Master:OrderID,Customer}\n${Orders.Detail:Product,Qty,Price}";
        // Simulated data source
        java.util.Map<String, Object> dataSource = new java.util.HashMap<>();
        java.util.List<java.util.Map<String, Object>> master = new java.util.ArrayList<>();
        java.util.Map<String, Object> masterRow = new java.util.HashMap<>();
        masterRow.put("OrderID", 1001);
        masterRow.put("Customer", "Acme Corp");
        master.add(masterRow);
        dataSource.put("Orders.Master", master);

        java.util.List<java.util.Map<String, Object>> detail = new java.util.ArrayList<>();
        java.util.Map<String, Object> detailRow = new java.util.HashMap<>();
        detailRow.put("Product", "Widget");
        detailRow.put("Qty", 5);
        detailRow.put("Price", 9.99);
        detail.add(detailRow);
        dataSource.put("Orders.Detail", detail);

        SmartMarkerProcessor processor = new SmartMarkerProcessor(new Workbook());
        processor.apply(smartMarkerTemplate, dataSource);
        processor.getWorkbook().save("output/smartMarkerResult.xlsx");
        System.out.println("Smart Marker workbook saved.");
    }
}
```

**Что вы видите:**  
Новая книга (`smartMarkerResult.xlsx`), где заполнители шаблона заменены данными. Этот шаг напрямую не связан со шрифтами, но завершает руководство, показывая типичный рабочий процесс отчётности, который часто предшествует экспорту **embed fonts in html**.

---

## Распространённые ошибки и профессиональные советы (Обеспечение успешного встраивания шрифтов)

| Проблема | Почему происходит | Решение |
|----------|-------------------|---------|
| Шрифты отсутствуют в HTML‑файле | Книга использует системный шрифт, который не установлен на сервере. | Используйте `Workbook.getSettings().setDefaultFont("Arial")` перед загрузкой данных или вручную встраивайте необходимые шрифты. |
| Выходной HTML слишком велик | Встраивание множества больших шрифтов увеличивает размер файла. | Ограничьте встраивание только используемыми шрифтами: `htmlOptions.setFontEmbeddingMode(HtmlFontEmbeddingMode.EmbedSubset)`. |
| Эмодзи исчезают после конвертации в XPS | Селекторы вариаций по умолчанию отбрасываются. | Включите `settings.setEnableFontVariationSelectors(true)`, как показано в Шаге 2. |
| OLE‑объект превращается в статическое изображение в PPTX | Книга была сохранена с `setSuppressOLEObjects(true)`. | Убедитесь, что **не** подавляете OLE‑объекты при сохранении в PPTX. |

---

## Проверка результатов

1. Откройте `embeddedFonts.html` в Chrome/Firefox. Таблица должна отображаться с встраиваемым шрифтом (например, Arial), даже если этот шрифт не установлен на компьютере.  
2. Откройте `withVariations.xps` в Windows XPS Viewer. Эмодзи, такие как 👍, должны отображаться корректно.  
3. Откройте `oleEditable.pptx` в PowerPoint. Дважды щёлкните по OLE‑форме;

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}