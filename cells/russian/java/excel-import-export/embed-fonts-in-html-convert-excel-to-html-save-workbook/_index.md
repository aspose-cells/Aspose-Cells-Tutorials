---
category: general
date: 2026-06-27
description: Встраивание шрифтов в HTML при конвертации Excel в HTML. Узнайте, как
  сохранить книгу в формате HTML со встроенными шрифтами с помощью простого кода на
  Java.
draft: false
keywords:
- embed fonts in html
- convert excel to html
- save workbook as html
- Java Excel to HTML conversion
- Aspose.Cells HTML export
language: ru
og_description: Встраивание шрифтов в HTML при конвертации Excel в HTML. Это руководство
  показывает, как сохранить книгу в формате HTML с встроенными шрифтами с использованием
  Java.
og_title: Встраивание шрифтов в HTML – Конвертировать Excel в HTML и сохранить рабочую
  книгу
schemas:
- author: Aspose
  dateModified: '2026-06-27'
  description: Embed fonts in HTML when you convert Excel to HTML. Learn how to save
    workbook as HTML with embedded fonts using simple Java code.
  headline: Embed Fonts in HTML – Convert Excel to HTML & Save Workbook
  type: TechArticle
- description: Embed fonts in HTML when you convert Excel to HTML. Learn how to save
    workbook as HTML with embedded fonts using simple Java code.
  name: Embed Fonts in HTML – Convert Excel to HTML & Save Workbook
  steps:
  - name: Right‑click the page → “View Page Source”.
    text: Right‑click the page → “View Page Source”.
  - name: 'Search for `@font-face`. You’ll find a CSS rule that contains a `src: url(data:font/ttf;base64,…)`
      line—this is the Base64‑encoded font data.'
    text: 'Search for `@font-face`. You’ll find a CSS rule that contains a `src: url(data:font/ttf;base64,…)`
      line—this is the Base64‑encoded font data.'
  - name: Load or create the workbook.
    text: Load or create the workbook.
  - name: Create `HtmlSaveOptions` and enable `setEmbedFonts(true)`.
    text: Create `HtmlSaveOptions` and enable `setEmbedFonts(true)`.
  - name: Call `Workbook.save` with those options.
    text: Call `Workbook.save` with those options.
  type: HowTo
tags:
- Java
- Aspose.Cells
- HTML
- Excel
title: Встраивание шрифтов в HTML – преобразовать Excel в HTML и сохранить рабочую
  книгу
url: /ru/java/excel-import-export/embed-fonts-in-html-convert-excel-to-html-save-workbook/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Встраивание шрифтов в HTML – Конвертация Excel в HTML и сохранение рабочей книги

Когда‑нибудь нужно было **встроить шрифты в HTML** при *конвертации Excel в HTML*? Возможно, вы создаёте портал отчетов, и стандартные веб‑шрифты просто не подходят. Хорошая новость — вам не придётся довольствоваться скучным, общим видом: Aspose.Cells позволяет упаковать именно те типографские гарнитуры, которые использовались в таблице, прямо в сгенерированный HTML‑файл.

В этом руководстве мы пройдём полный, готовый к запуску пример на Java, который **сохраняет рабочую книгу как HTML** со встроенными шрифтами, объяснит, зачем это нужно, и укажет на несколько подводных камней, с которыми вы можете столкнуться. К концу вы получите автономную HTML‑страницу, выглядящую точно так же, как оригинальная таблица Excel, без недостающих глифов и без внешних CSS‑файлов.

## Что вы узнаете

- Как загрузить существующую рабочую книгу Excel (или создать её с нуля) на Java.  
- Как настроить `HtmlSaveOptions` для встраивания шрифтов рабочей книги непосредственно в HTML‑вывод.  
- Как вызвать `Workbook.save`, чтобы файл был записан как **HTML со встроенными шрифтами**.  
- Советы по работе с большими файлами шрифтов, пользовательскими каталогами шрифтов и устранению распространённых проблем.

> **Предварительные требования:** На вашем classpath должна быть Aspose.Cells for Java (последняя версия) и среда выполнения Java 8+. Другие сторонние библиотеки не требуются.

---

## Шаг 1: Настройка проекта и импорт необходимых классов

Прежде чем перейти к коду, убедимся, что среда разработки готова. Если вы используете Maven, добавьте зависимость Aspose.Cells в ваш `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version> <!-- Use the newest version available -->
</dependency>
```

Если вы предпочитаете Gradle, эквивалент выглядит так:

```gradle
implementation 'com.aspose:aspose-cells:23.12'
```

> **Pro tip:** Держите библиотеку в актуальном состоянии. Новые релизы часто улучшают работу со шрифтами и уменьшают размер встроенных данных.

Теперь импортируем необходимые классы:

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.HtmlSaveOptions;
import com.aspose.cells.SaveFormat;
import java.io.File;
```

Эти импорты дают нам доступ к модели рабочей книги, параметрам экспорта в HTML и нескольким вспомогательным классам.

---

## Шаг 2: Загрузка (или создание) рабочей книги Excel

Вы можете либо загрузить существующий файл `.xlsx`, либо создать книгу «на лету». Для примера предположим, что у нас есть файл `Sample.xlsx` в папке `resources` проекта.

```java
// Load an existing workbook
String inputPath = "resources/Sample.xlsx";
Workbook wb = new Workbook(inputPath);
```

Если у вас нет исходного файла, можно быстро сгенерировать книгу:

```java
// Create a workbook from scratch (optional)
Workbook wb = new Workbook();               // creates a new empty workbook
wb.getWorksheets().get(0).getCells().putValue("A1", "Hello, world!");
```

> **Почему это важно:** При встраивании шрифтов Aspose.Cells извлекает точные определения шрифтов, использованных в книге. Если в книге есть пользовательские шрифты, они будут перенесены в HTML, гарантируя визуальную точность.

---

## Шаг 3: Настройка HtmlSaveOptions для встраивания шрифтов

Это сердце руководства. По умолчанию `HtmlSaveOptions` пишет CSS, ссылающийся на системные шрифты. Чтобы изменить это поведение, включаем флаг `setEmbedFonts(true)`.

```java
// Step 1: Create HTML save options
HtmlSaveOptions htmlOpts = new HtmlSaveOptions(SaveFormat.HTML);

// Step 2: Enable embedding of fonts in the HTML output
htmlOpts.setEmbedFonts(true);

// (Optional) Reduce the size of embedded fonts by subsetting only used glyphs
htmlOpts.setSubsetFonts(true);
```

### Что делают параметры

| Параметр | По умолчанию | Эффект при изменении |
|----------|--------------|----------------------|
| `setEmbedFonts(true)` | `false` | Встраивает полные файлы шрифтов (обычно как Base64‑закодированные data URI) в генерируемый HTML. |
| `setSubsetFonts(true)` | `false` | Ограничивает встроенный шрифт только символами, реально использованными, значительно уменьшая размер файла. |
| `setFontEmbeddingMode(HtmlSaveOptions.FontEmbeddingMode.EMBED_ALL)` | `EMBED_ALL` | Можно выбрать встраивание только определённых шрифтов, если есть ограничения лицензии. |

> **Особый случай:** Если книга использует шрифт, не установленный на сервере, Aspose.Cells переключается на шрифт системы по умолчанию. Чтобы избежать сюрпризов, убедитесь, что все пользовательские шрифты доступны в каталоге шрифтов Java‑runtime или зарегистрируйте их вручную через `FontConfig`.

---

## Шаг 4: Сохранение рабочей книги как HTML со встроенными шрифтами

После настройки параметров просто вызываем `save`. В результате получится один файл `.html`, содержащий данные книги **и** файлы шрифтов, закодированные прямо в разметке.

```java
// Step 3: Save the workbook as an HTML file with embedded fonts
String outputDir = "output";
new File(outputDir).mkdirs(); // Ensure the folder exists

String outputPath = outputDir + File.separator + "page.html";
wb.save(outputPath, htmlOpts);

System.out.println("HTML file with embedded fonts created at: " + outputPath);
```

Открыв `page.html` в любом современном браузере, вы увидите страницу с той же типографикой, что и в Excel — без внешних файлов шрифтов и без пропущенных символов.

---

## Шаг 5: Проверка результата и понимание вывода

Откройте сгенерированный HTML‑файл в браузере (Chrome, Firefox, Edge — любой). Вы должны увидеть лист, отрендеренный точно. Чтобы убедиться, что шрифты действительно встроены:

1. Щёлкните правой кнопкой мыши по странице → “View Page Source”.  
2. Найдите `@font-face`. Вы увидите правило CSS, содержащее строку `src: url(data:font/ttf;base64,…)` — это Base64‑закодированные данные шрифта.  

Если это есть, шаг **встроить шрифты в HTML** выполнен успешно.

### Часто задаваемые вопросы

- **«Почему HTML‑файл больше, чем ожидалось?»**  
  Встраивание полных файлов шрифтов может добавить несколько сотен килобайт. Используйте `setSubsetFonts(true)`, чтобы уменьшить размер, или конвертируйте только необходимые листы.

- **«Можно ли встроить только конкретный шрифт?»**  
  Да. Установите `htmlOpts.setFontEmbeddingMode(HtmlSaveOptions.FontEmbeddingMode.EMBED_SPECIFIED)` и затем добавьте имена шрифтов через `htmlOpts.getSpecifiedFontNames().add("MyCustomFont")`.

- **«Что делать, если шрифт лицензирован и его нельзя встраивать?»**  
  Отключите флаг (`setEmbedFonts(false)`) и предоставьте веб‑безопасный запасной шрифт через CSS, либо разместите шрифт на CDN, где у вас есть разрешение.

---

## Шаг 6: Работа с большими книгами и советы по производительности

Встраивание шрифтов хорошо подходит для небольших таблиц, но рабочая книга с десятками пользовательских шрифтов может сильно увеличить размер HTML. Вот несколько рекомендаций, ориентированных на производительность:

- **Подмножество шрифтов** (уже показано) — оставляет только используемые глифы.  
- **Экспортировать только нужные листы** с помощью `htmlOpts.setExportActiveWorksheetOnly(true)`.  
- **Сжимать HTML** после генерации (например, gzip на сервере), чтобы снизить сетевую задержку.  
- **Кешировать сгенерированный HTML**, если один и тот же Excel‑файл запрашивается часто.

---

## Шаг 7: Следующие шаги — выход за пределы базового экспорта

Теперь, когда вы освоили **встраивание шрифтов в HTML**, можете изучить связанные возможности:

- **Конвертация Excel в HTML с изображениями** (`htmlOpts.setExportImagesAsBase64(true)`).  
- **Генерация PDF вместо HTML** (`wb.save("output.pdf", SaveFormat.PDF)`).  
- **Создание адаптивного HTML** путем настройки `htmlOpts.setExportActiveWorksheetOnly` и `htmlOpts.setExportGridLines`.  

Все эти функции следуют одной схеме: создаёте объект `*SaveOptions`, переключаете нужные флаги и вызываете `Workbook.save`.

---

## Заключение

Вы только что узнали, как **встроить шрифты в HTML** при **конвертации Excel в HTML** и **сохранении рабочей книги как HTML** с помощью Aspose.Cells for Java. Ключевые шаги:

1. Загрузить или создать рабочую книгу.  
2. Создать `HtmlSaveOptions` и включить `setEmbedFonts(true)`.  
3. Вызвать `Workbook.save` с этими параметрами.

В результате вы получаете один переносимый HTML‑файл, который выглядит точно так же, как оригинальная таблица — без недостающих шрифтов, без дополнительных CSS‑файлов и без зависимости от шрифтов, установленных у клиента.

Экспериментируйте с подмножеством шрифтов, выборочным встраиванием или даже комбинируйте это с кешированием на стороне сервера для сценариев с высоким трафиком. Если столкнётесь с неожиданно большими файлами или пропущенными глифами, вернитесь к рассмотренным настройкам и скорректируйте их.

Приятного кодинга и наслаждайтесь пиксельно‑идеальным HTML, который теперь можно обслуживать напрямую из ваших Java‑приложений!

## Что стоит изучить дальше?

Следующие руководства охватывают тесно связанные темы, расширяющие техники, продемонстрированные в этом руководстве. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, помогающими вам освоить дополнительные возможности API и исследовать альтернативные подходы в собственных проектах.

- [Конвертация Excel в HTML на Java с использованием Aspose.Cells: пошаговое руководство](/cells/english/java/workbook-operations/convert-excel-html-aspose-cells-java/)
- [Экспорт Excel в HTML с помощью Aspose.Cells for Java: полный гид](/cells/english/java/workbook-operations/export-excel-to-html-aspose-cells-java/)
- [Экспорт Excel в HTML с использованием IStreamProvider и Aspose.Cells for Java: всестороннее руководство](/cells/english/java/workbook-operations/export-excel-html-streamprovider-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}