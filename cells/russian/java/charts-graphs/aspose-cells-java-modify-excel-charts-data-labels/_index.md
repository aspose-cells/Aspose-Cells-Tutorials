---
date: '2026-06-22'
description: Узнайте, как изменить chart data labels и настроить data labels в Excel
  с помощью Aspose.Cells for Java. Это руководство охватывает chart modification,
  font formatting и практические примеры.
keywords:
- change chart data labels
- customize data labels excel
- format data label fonts
- Aspose.Cells Java chart modification
- Excel automation Java
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Learn how to change chart data labels and customize data labels in
    Excel with Aspose.Cells for Java. This guide covers chart modification, font formatting,
    and practical examples.
  headline: How to Change Chart Data Labels and Modify Excel Charts Using Aspose.Cells
    for Java
  type: TechArticle
- description: Learn how to change chart data labels and customize data labels in
    Excel with Aspose.Cells for Java. This guide covers chart modification, font formatting,
    and practical examples.
  name: How to Change Chart Data Labels and Modify Excel Charts Using Aspose.Cells
    for Java
  steps:
  - name: Create a Workbook
    text: This line creates the `Workbook` instance, giving you full access to worksheets,
      charts, and cells.
  - name: Save the Modified Workbook
    text: After you finish editing, call `save` to write the changes to disk.
  - name: Access First Worksheet
    text: The `Worksheet` class represents a single sheet; accessing it via `getWorksheets().get(0)`
      gives you the first sheet.
  - name: Access First Chart
    text: The `Chart` class encapsulates all chart‑related properties. Once you have
      a reference, you can modify series, axes, and data labels.
  - name: Modify Data Label Text
    text: Use `setText("Your custom label")` on the `DataLabel` object to replace
      the default value.
  - name: Customize Font
    text: The `Font` class lets you set `setBold(true)`, `setColor(Color.getRed())`,
      and other attributes for precise visual control.
  type: HowTo
- questions:
  - answer: Yes, the free trial provides full functionality for development and testing;
      a commercial license is required for production deployments.
    question: Can I use Aspose.Cells for Java without a paid license?
  - answer: It can process files with over 500 MB and 100 + worksheets using less
      than 300 MB of RAM when memory‑optimized settings are enabled.
    question: How does Aspose.Cells handle large Excel files?
  - answer: Absolutely – iterate over `worksheet.getCharts()` and apply the same label‑changing
      logic to each chart object.
    question: Is it possible to modify multiple charts in one workbook?
  - answer: Forgetting to call `setShowValue(true)` on the series, or not disposing
      of the workbook, can lead to missing labels or memory leaks.
    question: What are the most common pitfalls when customizing data labels?
  - answer: Yes, simply add the Maven/Gradle dependency and inject the workbook handling
      code into a Spring service component.
    question: Can Aspose.Cells be integrated with Spring Boot?
  type: FAQPage
title: Как изменить chart data labels и модифицировать Excel charts с помощью Aspose.Cells
  for Java
url: /ru/java/charts-graphs/aspose-cells-java-modify-excel-charts-data-labels/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Как изменить подписи данных диаграммы и модифицировать диаграммы Excel с помощью Aspose.Cells для Java

## Введение

Программное изменение подписей данных диаграммы может сэкономить часы ручной доработки, особенно когда необходимо автоматически генерировать десятки финансовых отчетов. В этом руководстве вы узнаете, как **изменять подписи данных диаграммы** в рабочей книге Excel с помощью Aspose.Cells для Java, а также как настроить шрифты подписей для более профессионального вида. К концу руководства вы сможете загрузить рабочую книгу, найти диаграмму и применить форматирование rich‑text к любой подписи данных — без открытия Excel.

**Что вы узнаете**
- Доступ к рабочим книгам Excel и их изменение
- Навигация по листам и диаграммам
- Изменение подписей данных диаграммы и настройка их внешнего вида
- Форматирование шрифтов подписей данных для визуального воздействия

Убедимся, что у вас есть всё необходимое, прежде чем мы перейдём к коду.

## Быстрые ответы
- **Могу ли я изменить подписи данных диаграммы без открытия Excel?** Да, Aspose.Cells позволяет изменять подписи непосредственно в файле.
- **Какая версия библиотеки поддерживает эту функцию?** Все выпуски Aspose.Cells for Java, начиная с 20.10.
- **Нужна ли платная лицензия для запуска примера?** Бесплатная пробная версия подходит для разработки; для продакшн‑использования требуется лицензия.
- **Достаточно ли Java 8?** Да, Java 8 или новее полностью поддерживается.
- **Могу ли я форматировать шрифты подписей (цвет, жирный, размер)?** Абсолютно — API предоставляет полный контроль над стилем шрифта.

## Что такое Aspose.Cells для Java?
Aspose.Cells для Java — мощный API, позволяющий создавать, изменять и конвертировать электронные таблицы Excel без Microsoft Excel. Он поддерживает **50+** форматов файлов, включая XLSX, CSV, PDF и HTML, и может обрабатывать многосотстраничные рабочие книги, используя менее 200 МБ памяти.

## Почему менять подписи данных диаграммы?
Программное изменение подписей данных диаграммы уменьшает ручные ошибки, обеспечивает согласованность отчетов и позволяет динамически обновлять их на основе данных в реальном времени. С помощью Aspose.Cells вы можете обновить тысячи диаграмм за секунды, что в противном случае заняло бы дни при ручном выполнении.

## Предварительные требования

- **Aspose.Cells Library** – добавить JAR через Maven или Gradle (см. ниже).  
- **Java Development Kit (JDK)** – версия 8 или новее.  
- **IDE** – IntelliJ IDEA, Eclipse или любой совместимый с Java редактор.

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

### Получение лицензии

Aspose.Cells предлагает бесплатную пробную версию, временные лицензии для оценки и полные коммерческие лицензии. Чтобы начать с бесплатной пробной версии:

1. Перейдите на страницу [Aspose's Free Trial](https://releases.aspose.com/cells/java/).  
2. Скачайте библиотеку и примените пробную лицензию в вашем проекте.

Для использования в продакшн‑среде получите временную или постоянную лицензию на странице [Purchase Page](https://purchase.aspose.com/buy).

### Базовая инициализация

Класс `Workbook` является основным объектом Aspose.Cells, представляющим целый файл Excel в памяти. Инициализируйте его, указав путь к исходной рабочей книге:

```java
String dataDir = "YOUR_DATA_DIRECTORY";
Workbook workbook = new Workbook(dataDir + "/source.xlsx");
```

## Настройка Aspose.Cells для Java

После добавления библиотеки в проект настройте окружение, чтобы без проблем работать с файлами Excel.

### Требования к настройке окружения

- JDK 8+  
- Предпочтительная IDE (IntelliJ IDEA, Eclipse)  
- Maven или Gradle для управления зависимостями  

## Руководство по реализации

Мы пройдём каждый шаг, необходимый для **изменения подписей данных диаграммы** и применения пользовательского форматирования шрифтов.

### Доступ и изменение рабочей книги Excel

**Обзор**: Загрузите существующую рабочую книгу, внесите изменения и сохраните новую копию.

#### Как загрузить и сохранить рабочую книгу

Загрузите рабочую книгу с помощью `new Workbook("input.xlsx")` и сохраните её, используя `workbook.save("output.xlsx")`. Этот двухстрочный шаблон является основой для всех последующих операций.

#### Шаг 1: Создать рабочую книгу  
```java
String dataDir = "YOUR_DATA_DIRECTORY";
Workbook workbook = new Workbook(dataDir + "/source.xlsx");
```  
Эта строка создаёт экземпляр `Workbook`, предоставляя полный доступ к листам, диаграммам и ячейкам.

#### Шаг 2: Сохранить изменённую рабочую книгу  
```java
String outDir = "YOUR_OUTPUT_DIRECTORY";
workbook.save(outDir + "/ModifiedData_out.xlsx");
```  
После завершения редактирования вызовите `save`, чтобы записать изменения на диск.

### Доступ к листу в рабочей книге Excel

**Обзор**: Получите конкретный лист, содержащий диаграмму, которую вы хотите отредактировать.

#### Шаг 1: Доступ к первому листу  
```java
Worksheet worksheet = workbook.getWorksheets().get(0);
```  
Класс `Worksheet` представляет отдельный лист; доступ к нему через `getWorksheets().get(0)` возвращает первый лист.

### Доступ и изменение диаграммы в листе

**Обзор**: Найдите объект диаграммы внутри листа и подготовьте его к изменению подписей.

#### Шаг 1: Доступ к первой диаграмме  
```java
Chart chart = worksheet.getCharts().get(0);
```  
Класс `Chart` инкапсулирует все свойства, связанные с диаграммой. Получив ссылку, вы можете изменять серии, оси и подписи данных.

### Изменение подписей данных в точке серии диаграммы

**Обзор**: Измените отображаемый текст подписи данных, чтобы показать пользовательскую информацию.

`DataLabel` представляет текстовую подпись, прикреплённую к точке данных в диаграмме.

#### Шаг 1: Изменить текст подписи данных  
```java
DataLabels dlbls = chart.getNSeries().get(0).getPoints().get(0).getDataLabels();
dlbls.setText("Rich Text Label");
```  
Вызовите `setText("Your custom label")` у объекта `DataLabel`, чтобы заменить значение по умолчанию.

### Настройка параметров шрифта подписей данных

**Обзор**: Примените полужирное начертание, изменение цвета и настройку размера шрифта, чтобы подписи выделялись.

#### Шаг 1: Настроить шрифт  
```java
FontSetting fntSetting = dlbls.characters(0, 10);
fntSetting.getFont().setColor(Color.getRed());
fntSetting.getFont().setBold(true);
```  
Класс `Font` позволяет задавать `setBold(true)`, `setColor(Color.getRed())` и другие атрибуты для точного визуального контроля.

## Как изменить подписи данных диаграммы в Excel с помощью Aspose.Cells?

Загрузите рабочую книгу, получите целевую диаграмму, затем пройдитесь по точкам её серий и вызовите `setText` для каждой `DataLabel`. В конце настройте свойства `Font` подписи, чтобы достичь желаемого вида. Такой подход работает для любого типа диаграмм — столбчатых, линейных, круговых или радиальных — и обновляет все подписи за один проход.

## Распространённые сценарии использования

- **Financial Dashboards** – Автоматически обновлять квартальные показатели по мере поступления новых данных.  
- **Sales Reports** – Выделять лучшие продукты, делая их подписи полужирными.  
- **Project Management** – Отображать процент завершения задач непосредственно на диаграммах в стиле Ганта.  

## Соображения по производительности

При обработке больших рабочих книг (200 + страниц) учитывайте следующие рекомендации:

- Используйте `WorkbookSettings.setMemorySetting(MemorySetting.MEMORY_PREFERENCE)`, чтобы ограничить использование ОЗУ.  
- Сразу после сохранения закрывайте объект `Workbook` с помощью `workbook.dispose()`.  
- Для пакетных операций по возможности переиспользуйте один экземпляр `Workbook`, чтобы снизить нагрузку на сборщик мусора.

## Часто задаваемые вопросы

**Q: Могу ли я использовать Aspose.Cells для Java без платной лицензии?**  
A: Да, бесплатная пробная версия предоставляет полный набор функций для разработки и тестирования; для продакшн‑развертываний требуется коммерческая лицензия.

**Q: Как Aspose.Cells обрабатывает большие файлы Excel?**  
A: Он может обрабатывать файлы более 500 МБ и более 100 листов, используя менее 300 МБ ОЗУ при включённых настройках оптимизации памяти.

**Q: Можно ли изменить несколько диаграмм в одной рабочей книге?**  
A: Конечно — пройдитесь по `worksheet.getCharts()` и примените ту же логику изменения подписей к каждому объекту диаграммы.

**Q: Какие самые распространённые подводные камни при настройке подписей данных?**  
A: Забвение вызова `setShowValue(true)` у серии или отсутствие освобождения рабочей книги могут привести к отсутствию подписей или утечкам памяти.

**Q: Можно ли интегрировать Aspose.Cells со Spring Boot?**  
A: Да, просто добавьте зависимость Maven/Gradle и внедрите код работы с рабочей книгой в компонент сервиса Spring.

## Ресурсы

- [Документация Aspose](https://reference.aspose.com/cells/java/)
- [Документация Aspose.Cells](https://reference.aspose.com/cells/java/)
- [Скачать Aspose.Cells для Java](https://releases.aspose.com/cells/java/)
- [Купить Aspose.Cells](https://purchase.aspose.com/buy)
- [Бесплатная пробная лицензия](https://releases.aspose.com/cells/java/)
- [Получение временной лицензии](https://purchase.aspose.com/temporary-license/)
- [Форум поддержки Aspose](https://forum.aspose.com/c/cells/9)

Изучите эти ссылки, чтобы углубить свои знания и открыть дополнительные API, связанные с диаграммами.

---

**Последнее обновление:** 2026-06-22  
**Тестировано с:** Aspose.Cells 24.12 for Java  
**Автор:** Aspose  

{{< blocks/products/products-backtop-button >}}

## Связанные руководства

- [Как автоматически изменять размер подписей данных диаграммы в Excel с помощью Aspose.Cells для Java](/cells/java/charts-graphs/aspose-cells-java-auto-resize-chart-data-labels/)
- [Как добавить подписи к диаграммам Excel с помощью Aspose.Cells для Java](/cells/java/charts-graphs/adding-labels-to-charts-aspose-cells-java-tutorial/)
- [Мастер Aspose.Cells Java для настройки диаграмм Excel: Полное руководство](/cells/java/charts-graphs/aspose-cells-java-excel-charts-customization/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}