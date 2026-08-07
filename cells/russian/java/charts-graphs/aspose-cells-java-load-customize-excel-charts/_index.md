---
date: '2026-06-12'
description: Узнайте, как экспортировать диаграмму в PNG с Aspose.Cells Java, генерировать
  изображения диаграмм, рендерить диаграммы Excel в PNG и эффективно настраивать визуализации.
keywords:
- export chart to png
- java generate chart image
- render excel chart image
- java chart visualization library
- Aspose.Cells Java
schemas:
- author: Aspose
  dateModified: '2026-06-12'
  description: Learn how to export chart to PNG with Aspose.Cells Java, generate chart
    images, render Excel charts as PNG, and customize visualizations efficiently.
  headline: Export chart to PNG using Aspose.Cells Java
  type: TechArticle
- description: Learn how to export chart to PNG with Aspose.Cells Java, generate chart
    images, render Excel charts as PNG, and customize visualizations efficiently.
  name: Export chart to PNG using Aspose.Cells Java
  steps:
  - name: Verify that **JDK 8** or newer is on your `PATH`.
    text: Verify that **JDK 8** or newer is on your `PATH`.
  - name: Open your preferred IDE and create a new Maven/Gradle Java project.
    text: Open your preferred IDE and create a new Maven/Gradle Java project.
  - name: Add the Aspose.Cells dependency using the snippets above.
    text: Add the Aspose.Cells dependency using the snippets above.
  - name: Add the Maven or Gradle dependency as shown earlier.
    text: Add the Maven or Gradle dependency as shown earlier.
  - name: Place your license file (`Aspose.Cells.lic`) in the project’s resources
      folder.
    text: Place your license file (`Aspose.Cells.lic`) in the project’s resources
      folder.
  - name: 'Load the license at runtime:'
    text: 'Load the license at runtime:'
  type: HowTo
- questions:
  - answer: Place the `Aspose.Cells.lic` file in the resources folder and load it
      with `License license = new License(); license.setLicense("Aspose.Cells.lic");`.
    question: How do I resolve license activation issues?
  - answer: Yes, it integrates seamlessly with Spring Boot, Jakarta EE, or any servlet
      container.
    question: Can I use Aspose.Cells for Java in a web application?
  - answer: Forgetting to update the source data before calling `calculate()` leads
      to stale visuals.
    question: What are common pitfalls when refreshing charts?
  - answer: Use `Workbook.setMemorySetting(MemorySetting.MEMORY_PREFERENCE)` and process
      worksheets in streams.
    question: How do I handle large Excel files efficiently?
  - answer: PNG, JPEG, BMP, and TIFF are fully supported; choose PNG for loss‑less
      quality.
    question: What image formats are supported for rendering charts?
  type: FAQPage
title: Экспортировать диаграмму в PNG с помощью Aspose.Cells Java
url: /ru/java/charts-graphs/aspose-cells-java-load-customize-excel-charts/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Экспорт диаграммы в PNG с помощью Aspose.Cells Java

## Введение

Экспорт диаграммы в PNG является распространенной задачей, когда необходимо встроить визуальные данные в отчеты, презентации или веб‑страницы. С помощью **Aspose.Cells for Java** вы можете загрузить существующую книгу Excel, обновить данные диаграммы, применить настройки глобализации и отобразить диаграмму непосредственно как изображение PNG высокого качества — без необходимости установки Microsoft Excel. В этом руководстве вы узнаете, как **export chart to PNG**, генерировать изображения диаграмм программно и настраивать вывод для глобальной аудитории.

## Быстрые ответы
- **Как экспортировать диаграмму в PNG?** Загрузите книгу, получите доступ к диаграмме и вызовите `chart.toImage()` с параметром `ImageOrPrintOptions`, установленным в PNG.  
- **Какая библиотека поддерживает генерацию изображений диаграмм в Java?** Aspose.Cells for Java предоставляет полный API для рендеринга диаграмм Excel в виде изображений.  
- **Нужна ли лицензия для экспорта в PNG?** Бесплатная пробная версия работает, но коммерческая лицензия снимает ограничения оценки.  
- **Можно ли глобально настроить форматы чисел?** Да, используйте `Workbook.getSettings().setGlobalizationSettings()` перед рендерингом.  
- **Является ли PNG единственным форматом?** Нет, вы также можете рендерить в JPEG, BMP или TIFF, изменив параметр формата изображения.

## Что такое Aspose.Cells for Java?
`Aspose.Cells for Java` — это **библиотека обработки электронных таблиц на Java**, позволяющая разработчикам создавать, изменять, конвертировать и рендерить файлы Excel без Microsoft Office. Она поддерживает более 50 форматов файлов, работает с книгами, содержащими тысячи строк, и может отрисовывать диаграммы в изображения менее чем за секунду на типичном серверном оборудовании.

## Почему экспортировать диаграмму в PNG с помощью Aspose.Cells?
Экспорт диаграмм в PNG с помощью Aspose.Cells обеспечивает высокую производительность, низкое потребление памяти и гибкость форматов, одновременно устраняя необходимость в Microsoft Excel. Библиотека рендерит диаграммы менее чем за секунду, поддерживает умеренное использование кучи и поддерживает PNG, JPEG, BMP и TIFF, что делает её идеальной для веб‑, печатных и кросс‑платформенных развертываний.

## Предварительные требования

- **Aspose.Cells for Java** v25.3 (или новее).  
- **JDK 8+** установлен на вашей машине разработки.  
- **IDE**, например IntelliJ IDEA или Eclipse.  
- **Maven или Gradle** для управления зависимостями.  

### Требуемые библиотеки и зависимости

**Maven**  
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```  

**Gradle**  
```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```  

### Настройка окружения

1. Убедитесь, что **JDK 8** или новее находится в вашем `PATH`.  
2. Откройте предпочитаемую IDE и создайте новый Maven/Gradle Java проект.  
3. Добавьте зависимость Aspose.Cells, используя приведенные выше фрагменты.  

### Получение лицензии

Aspose.Cells предлагает бесплатную пробную версию для оценки функций:

- [Скачать бесплатную пробную версию](https://releases.aspose.com/cells/java/)  
- Для использования в продакшене приобретите лицензию по ссылке [Приобрести Aspose.Cells](https://purchase.aspose.com/buy).  
- Временную лицензию можно запросить для расширенного тестирования.

## Настройка Aspose.Cells для Java

После подготовки окружения инициализируйте Aspose.Cells в вашем проекте:

1. Добавьте зависимость Maven или Gradle, как показано выше.  
2. Поместите файл лицензии (`Aspose.Cells.lic`) в папку ресурсов проекта.  
3. Загрузите лицензию во время выполнения:

```java
   License license = new License();
   license.setLicense("path/to/Aspose.Total.Java.lic");
   ```  

## Руководство по реализации

Мы пройдем три основных сценария: загрузка и обновление диаграммы, настройка параметров глобализации и рендеринг диаграммы в PNG.

### Как экспортировать диаграмму в PNG с помощью Aspose.Cells Java?

Чтобы экспортировать диаграмму в PNG с помощью Aspose.Cells for Java, сначала загрузите книгу, используя класс `Workbook`, затем получите нужный объект `Chart` из соответствующего листа. Настройте `ImageOrPrintOptions`, установив формат изображения в PNG, и в конце вызовите `chart.toImage(outputStream, options)`. Полученный поток содержит PNG высокого качества, который можно сохранить или отправить напрямую клиенту.

### Загрузка и обновление диаграммы из файла Excel

**Обзор**: Загрузите существующую книгу, убедитесь, что диаграмма отражает актуальные данные, и подготовьте её к рендерингу.

#### 1. Загрузка книги  
```java
String dataDir = "YOUR_DATA_DIRECTORY";
Workbook book = new Workbook(dataDir + "sample.xlsx");
```  
*Определение*: Класс `Workbook` представляет весь файл Excel в памяти, предоставляя доступ к листам, диаграммам и ячейкам.

#### 2. Доступ к листу и диаграмме  
```java
Worksheet sheet = book.getWorksheets().get(0);
Chart chart = sheet.getCharts().get(0);
```  
*Определение*: Объект `Worksheet` предоставляет доступ к строкам/столбцам, а объект `Chart` инкапсулирует все свойства, специфичные для диаграмм.

#### 3. Обновление диаграммы  
```java
chart.calculate();
```  
Вызов `calculate()` заставляет диаграмму пересчитать свои серии на основе измененных исходных данных, гарантируя визуальную точность.

### Настройка параметров глобализации для диаграмм

**Обзор**: Настройте форматы даты, времени и чисел в соответствии с региональными стандартами перед рендерингом.

#### 1. Загрузка книги  
```java
Workbook book = new Workbook(dataDir + "sample.xlsx");
```  

#### 2. Установка пользовательских параметров глобализации  
```java
CustomSettings customGlobalizationSettings = new CustomSettings();
customGlobalizationSettings.setChartSettings(new CustomChartGlobalizationSettings());
book.getSettings().setGlobalizationSettings(customGlobalizationSettings);
```  
Вы можете задать специфичные для локали шаблоны, такие как `"dd-MMM-yyyy"` для дат или `"#,##0.00"` для чисел, обеспечивая, что экспортированный PNG соответствует местным стандартам.

### Рендеринг диаграммы в изображение

**Обзор**: Преобразуйте обновленную диаграмму в файл PNG, который можно использовать в презентациях, PDF или веб‑страницах.

#### 1. Загрузка книги и доступ к диаграмме  
```java
String outDir = "YOUR_OUTPUT_DIRECTORY";
Workbook book = new Workbook(dataDir + "sample.xlsx");
Worksheet sheet = book.getWorksheets().get(0);
Chart chart = sheet.getCharts().get(0);
chart.calculate();
```  

#### 2. Рендеринг в изображение  
```java
ImageOrPrintOptions options = new ImageOrPrintOptions();
chart.toImage(outDir + "CustomTextforOtherLabelofPieChart_out.png", options);
```  
Метод `toImage()` записывает диаграмму в `java.io.OutputStream`. Установив `ImageOrPrintOptions.setImageFormat(ImageFormat.png)`, вы получаете четкий PNG‑файл.

## Практические применения

- **Бизнес‑отчеты** – Встраивание PNG‑диаграмм в документы PDF или Word для распределения среди заинтересованных сторон.  
- **Дашборды данных** – Обновляйте диаграммы в реальном времени по мере поступления новых данных, затем рендерьте в PNG для быстрой веб‑доставки.  
- **Глобальное соответствие** – Применяйте локальные форматы чисел и дат для соответствия региональным нормативным требованиям.

## Соображения по производительности

- **Управление памятью**: Используйте `Workbook.setMemorySetting(MemorySetting.MEMORY_PREFERENCE)` для больших файлов.  
- **Избирательное обновление**: Вызывайте `chart.calculate()` только для диаграмм, у которых изменились исходные данные.  
- **Безопасность потоков**: Создавайте отдельный `Workbook` для каждого потока, чтобы избежать проблем конкурентного доступа.

## Распространённые проблемы и решения

| Проблема | Решение |
|----------|----------|
| License not found | Verify the `Aspose.Cells.lic` path and ensure it’s on the classpath. |
| PNG output is blank | Confirm the chart is not hidden and that `calculate()` has been called before rendering. |
| Slow rendering on large files | Enable `MemorySetting.MEMORY_PREFERENCE` and render only the required worksheet. |

## Часто задаваемые вопросы

**Q: Как решить проблемы с активацией лицензии?**  
A: Разместите файл `Aspose.Cells.lic` в папке ресурсов и загрузите его с помощью `License license = new License(); license.setLicense("Aspose.Cells.lic");`.

**Q: Можно ли использовать Aspose.Cells for Java в веб‑приложении?**  
A: Да, он без проблем интегрируется со Spring Boot, Jakarta EE или любым контейнером сервлетов.

**Q: Какие распространённые подводные камни при обновлении диаграмм?**  
A: Необновление исходных данных перед вызовом `calculate()` приводит к устаревшим визуализациям.

**Q: Как эффективно работать с большими файлами Excel?**  
A: Используйте `Workbook.setMemorySetting(MemorySetting.MEMORY_PREFERENCE)` и обрабатывайте листы потоками.

**Q: Какие форматы изображений поддерживаются для рендеринга диаграмм?**  
A: PNG, JPEG, BMP и TIFF полностью поддерживаются; выбирайте PNG для без потерь качества.

## Ресурсы

- **Документация**: [Aspose.Cells Java API](https://reference.aspose.com/cells/java/)  
- **Загрузки**: [Aspose.Cells Releases](https://releases.aspose.com/cells/java/)  
- **Покупка и лицензирование**: [Купить Aspose.Cells](https://purchase.aspose.com/buy)  
- **Бесплатная пробная версия**: [Получить бесплатную пробную версию Aspose.Cells](https://releases.aspose.com/cells/java/)  
- **Временная лицензия**: [Запросить временную лицензию](https://purchase.aspose.com/temporary-license/)  
- **Поддержка и форумы**: [Форум поддержки Aspose](https://forum.aspose.com/c/cells/9)

Освоив эти шаги, вы сможете надёжно **export chart to PNG** и интегрировать визуализации высокого качества в любое решение на Java.

---

**Последнее обновление:** 2026-06-12  
**Тестировано с:** Aspose.Cells 25.3 for Java  
**Автор:** Aspose  

{{< blocks/products/products-backtop-button >}}

## Связанные руководства

- [Как экспортировать диаграммы Excel в SVG с помощью Aspose.Cells Java для масштабируемой векторной графики](/cells/java/charts-graphs/export-excel-charts-svg-aspose-cells-java/)
- [Экспорт диаграмм Excel в PDF с помощью Aspose.Cells for Java: Руководство по пользовательским размерам страниц](/cells/java/charts-graphs/export-excel-charts-pdf-aspose-cells-java/)
- [Как настроить диаграммы Excel с помощью цветовых тем, используя Aspose.Cells Java](/cells/java/charts-graphs/customize-excel-charts-aspose-cells-java/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

```text
// Direct answer (no code block needed here as per preservation rules)
```