---
category: general
date: 2026-11-22
description: Узнайте, как встраивать шрифты при сохранении Excel в HTML, обеспечивая
  их внедрение для одинакового отображения во всех браузерах.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to embed fonts
- enable font embedding
- save excel html
- html font embedding
- embed fonts html
language: ru
lastmod: 2026-11-22
og_description: Как внедрять шрифты при сохранении Excel в формате HTML. Следуйте
  этому руководству, чтобы включить внедрение шрифтов и обеспечить одинаковый вид
  ваших таблиц в любом браузере.
og_image_alt: Screenshot showing an Excel file exported to HTML with embedded fonts
og_title: Как встроить шрифты при сохранении Excel в HTML – пошагово
schemas:
- author: Aspose
  dateModified: '2026-11-22'
  description: Learn how to embed fonts while saving Excel as HTML, enabling font
    embedding for consistent rendering across browsers.
  headline: How to embed fonts when saving Excel as HTML – complete guide
  type: TechArticle
- description: Learn how to embed fonts while saving Excel as HTML, enabling font
    embedding for consistent rendering across browsers.
  name: How to embed fonts when saving Excel as HTML – complete guide
  steps:
  - name: What if the font is not found?
    text: Aspose.Cells can embed only fonts that the JVM can locate. If you receive
      a warning like *“Font not found, falling back to default”*, make sure the font
      file is installed on the operating system or placed in a directory listed in
      the `java.library.path`.
  - name: Does embedding increase file size?
    text: 'Yes. Embedding a full TrueType font can add 30–200 KB to the HTML file,
      depending on the font. If size is a concern, consider:'
  - name: Can I embed multiple fonts?
    text: Absolutely. The library examines every cell style, extracts all referenced
      fonts, and embeds each one when `setEmbedFonts(true)` is active.
  - name: Is the approach compatible with older browsers?
    text: The `@font-face` rule works in all browsers that support CSS 2.1 and later,
      which includes IE 9 +, Chrome, Firefox, Safari, and Edge. For very old browsers
      (IE 8‑), you may need to provide a fallback font family.
  type: HowTo
tags:
- Excel
- HTML
- Font embedding
title: Как внедрять шрифты при сохранении Excel в HTML — полное руководство
url: /ru/java/excel-import-export/how-to-embed-fonts-when-saving-excel-as-html-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как встраивать шрифты при сохранении Excel в HTML – полное руководство

Если вам нужно **встраивать шрифты** при экспорте рабочей книги Excel в HTML, это руководство покажет точные шаги. Встраивание шрифтов гарантирует, что сгенерированный HTML‑файл отображает ту же типографику, что и оригинальная рабочая книга, даже на системах, где отсутствуют необходимые шрифты. Вы также узнаете, как **включить встраивание шрифтов** с помощью Aspose.Cells for Java, надёжного способа **сохранить Excel в HTML** с полной визуальной точностью.

В этом руководстве вы:

* Настроите Java‑проект с библиотекой Aspose.Cells.  
* Создадите объект `HtmlSaveOptions` и включите **встраивание шрифтов в HTML**.  
* Сохраните рабочую книгу в HTML‑файл, содержащий необходимые файлы шрифтов.  

Требования:

* Java 8 или новее.  
* Aspose.Cells for Java (рекомендуется последняя версия).  
* Базовые знания Java и работы с файлами Excel.

---

## Что вам понадобится

| Item | Reason |
|------|--------|
| **Aspose.Cells for Java** | Предоставляет класс `HtmlSaveOptions` и метод `setEmbedFonts`. |
| **TrueType или OpenType шрифт**, установленный на машине | Библиотека может встраивать только шрифты, доступные JVM. |
| **IDE или система сборки** (например, Maven, Gradle или обычный `javac`) | Для компиляции и запуска примера. |

---

## Шаг 1: Добавьте Aspose.Cells в ваш проект

Если вы используете Maven, добавьте зависимость в `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version> <!-- use the latest version -->
</dependency>
```

Для Gradle поместите следующее в `build.gradle`:

```gradle
implementation 'com.aspose:aspose-cells:23.12'
```

*Совет:* Держите версию библиотеки актуальной; новые релизы включают исправления ошибок обработки **встраивания шрифтов в HTML**.

---

## Шаг 2: Создайте рабочую книгу и заполните её

Ниже приведена минимальная, автономная Java‑программа, которая создаёт рабочую книгу, записывает стилизованный текст и готовит её к экспорту в HTML.

```java
import com.aspose.cells.*;

public class ExcelHtmlFontEmbedding {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Create a new workbook
        Workbook wb = new Workbook();

        // 2️⃣ Access the first worksheet
        Worksheet sheet = wb.getWorksheets().get(0);
        Cells cells = sheet.getCells();

        // 3️⃣ Put some text in A1 and apply a custom font
        Cell a1 = cells.get("A1");
        a1.putValue("Hello, embedded fonts!");
        Style style = a1.getStyle();
        Font font = style.getFont();
        font.setName("Comic Sans MS");   // any installed font works
        font.setSize(14);
        a1.setStyle(style);

        // 4️⃣ Save as HTML with font embedding (see next step)
        saveWithEmbeddedFonts(wb);
    }

    private static void saveWithEmbeddedFonts(Workbook wb) throws Exception {
        // This method contains the core of **html font embedding**
        HtmlSaveOptions saveOptions = new HtmlSaveOptions();
        // Enable font embedding so the HTML contains the required .ttf files
        saveOptions.setEmbedFonts(true);

        // Optional: specify a folder for the generated assets (fonts, images)
        saveOptions.setExportImagesAsBase64(true); // reduces external files
        String outputPath = "output/embedded.html";

        // Perform the save operation
        wb.save(outputPath, saveOptions);
        System.out.println("Workbook saved with embedded fonts to: " + outputPath);
    }
}
```

**Почему это работает:**  
* `HtmlSaveOptions#setEmbedFonts(true)` указывает Aspose.Cells включить файлы шрифтов, используемые в рабочей книге, в сгенерированный HTML.  
* Установка `ExportImagesAsBase64` делает вывод более аккуратным, но это необязательно.

---

## Шаг 3: Проверьте сгенерированный HTML

Откройте `output/embedded.html` в любом современном браузере. Вы должны увидеть текст, отрисованный шрифтом *Comic Sans MS*, даже если шрифт не установлен на клиентской машине. Чтобы убедиться, что шрифт действительно встроен, посмотрите исходный код страницы; вы найдёте блок `<style>`, содержащий правило `@font-face`, ссылающееся на шрифт, закодированный в base64.

```html
<style>
@font-face {
    font-family: 'Comic Sans MS';
    src: url(data:font/ttf;base64,AAEAAAARAQAABAA...);
}
...
</style>
```

**Ожидаемый результат:** Страница отображает «Hello, embedded fonts!» с использованием указанного шрифта, а HTML‑файл содержит встроенные данные шрифта.

---

## Часто задаваемые вопросы и особые случаи

### Что делать, если шрифт не найден?
Aspose.Cells может встраивать только те шрифты, которые JVM может найти. Если вы получаете предупреждение вроде *«Font not found, falling back to default»*, убедитесь, что файл шрифта установлен в операционной системе или помещён в каталог, указанный в `java.library.path`.

### Увеличивает ли встраивание размер файла?
Да. Встраивание полного TrueType шрифта может добавить от 30 до 200 KB к HTML‑файлу, в зависимости от шрифта. Если размер важен, рассмотрите:

* Использование только тех символов, которые присутствуют в рабочей книге (Aspose.Cells обрезает неиспользуемые глифы).  
* Выбор лёгкого веб‑безопасного шрифта, который уже есть в большинстве браузеров.

### Можно ли встраивать несколько шрифтов?
Конечно. Библиотека проверяет каждый стиль ячейки, извлекает все используемые шрифты и встраивает каждый из них, когда активен `setEmbedFonts(true)`.

### Совместим ли подход со старыми браузерами?
Правило `@font-face` работает во всех браузерах, поддерживающих CSS 2.1 и новее, включая IE 9 +, Chrome, Firefox, Safari и Edge. Для очень старых браузеров (IE 8‑) может потребоваться указать запасной семейство шрифтов.

---

## Советы для продакшн‑использования

* **Кешировать сгенерированный HTML** – встраивание шрифтов делает каждый экспорт более тяжёлым; сохраняйте результат, если планируете отдавать его многократно.  
* **Отдельная папка ресурсов** – вместо base64 можно позволить Aspose.Cells записать файлы `.ttf` в папку (`saveOptions.setExportFontFile(true)`). Это уменьшает размер HTML и позволяет браузерам кешировать файлы шрифтов.  
* **Безопасность** – никогда не встраивайте шрифты из ненадёжных источников; они могут содержать вредоносные данные. Используйте только шрифты, которыми вы управляете.

---

## Заключение

Теперь вы знаете, **как встраивать шрифты** при **сохранении Excel в HTML** с помощью Aspose.Cells for Java. Включив **встраивание шрифтов**, сгенерированный HTML содержит необходимые правила `@font-face`, гарантируя, что ваша таблица выглядит одинаково во всех браузерах. Этот приём решает классическую проблему *встраивания шрифтов в HTML* и является рекомендованным способом **включить встраивание шрифтов** для любого рабочего процесса конвертации Excel в HTML.

Готовы к следующему шагу? Изучите связанные темы, такие как **сохранение Excel в PDF с встроенными шрифтами**, или узнайте, как **настроить вывод CSS** для адаптивных веб‑страниц. Приятного кодирования!

## Что вам стоит изучить дальше?

Следующие руководства охватывают тесно связанные темы, построенные на техниках, продемонстрированных в этом руководстве. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, помогающими освоить дополнительные возможности API и исследовать альтернативные подходы к реализации в ваших проектах.

- [Как встраивать шрифты при сохранении Excel в HTML с Aspose.Cells для C#](/cells/english/net/exporting-excel-to-html-with-advanced-options/how-to-embed-fonts-when-saving-excel-to-html-with-c/)
- [Как использовать wrapcols и встраивать шрифты при сохранении Excel в HTML](/cells/english/net/exporting-excel-to-html-with-advanced-options/how-to-use-wrapcols-and-embed-fonts-saving-excel-to-html/)
- [Как встраивать шрифты в HTML при сохранении рабочей книги](/cells/english/net/exporting-excel-to-html-with-advanced-options/how-to-embed-fonts-in-html-when-saving-a-workbook/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}