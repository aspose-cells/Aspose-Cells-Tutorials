---
date: '2026-09-27'
description: Узнайте, как создать круговую диаграмму Java с помощью Aspose.Cells.
  Пошаговое руководство по настройке диаграммы Excel, добавлению Maven‑зависимости
  и созданию профессиональных диаграмм.
keywords:
- create pie chart java
- customize excel pie chart
- maven dependency aspose cells
lastmod: '2026-09-27'
og_description: Создайте круговую диаграмму Java с использованием Aspose.Cells для
  Java. Узнайте, как настроить диаграмму Excel, добавить Maven‑зависимость и за несколько
  минут создать профессиональные диаграммы.
og_image_alt: Java code generating a customized pie chart in Excel with Aspose.Cells
og_title: Создание круговой диаграммы Java с Aspose.Cells – Полное руководство по
  Java
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Learn how to create pie chart java using Aspose.Cells. Step‑by‑step
    guide to customize Excel pie chart, set up Maven dependency, and generate professional
    charts.
  headline: How to create pie chart java with Aspose.Cells
  type: TechArticle
- questions:
  - answer: Yes, repeat the chart‑creation steps for each data range; each chart is
      independent.
    question: Can I generate multiple pie charts in the same workbook?
  - answer: It does; set the chart type to `ChartType.PIE_3D` when adding the chart.
    question: Does Aspose.Cells support 3‑D pie charts?
  - answer: Use the `Workbook.setDefaultTheme` method before creating any charts.
    question: How do I apply a custom theme to all charts?
  - answer: Over 30 formats, including XLSX, CSV, PDF, and HTML.
    question: What file formats can I export the workbook to?
  - answer: Yes, a valid license removes evaluation watermarks and unlocks full functionality.
    question: Is a license required for commercial deployment?
  type: FAQPage
tags:
- Aspose.Cells
- Java charting
- Excel automation
- data visualization
title: Как создать круговую диаграмму Java с Aspose.Cells
url: /ru/java/charts-graphs/create-customize-aspose-cells-pie-chart-java/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как создать круговую диаграмму java с Aspose.Cells

## Введение
Создание **pie chart** программно часто ощущается как головоломка, особенно когда требуется тонкий контроль над цветами, легендами и заголовками. В этом руководстве вы узнаете, как создать круговую диаграмму java с помощью Aspose.Cells, а затем настроить Excel **pie chart**, чтобы он соответствовал вашему бренду или стилю отчётности. Мы пройдём настройку окружения, заполнение данными, генерацию диаграммы и визуальные доработки — всё без выхода из вашей Java IDE.

**Что вы узнаете**
- Добавьте **Maven dependency Aspose.Cells** в ваш проект.
- Создайте рабочую книгу, заполните ячейки данными и сгенерируйте **pie chart**.
- Примените пользовательские цвета, заголовки и легенды к диаграмме.
- Экспортируйте рабочую книгу в файл XLSX, готовый к распространению.

Прежде чем начать, вы должны быть уверены в базовом синтаксисе Java и иметь установленный Maven или Gradle.

## Быстрые ответы
- **Какая библиотека создает pie chart в Java?** Aspose.Cells for Java.
- **Нужна ли лицензия?** Бесплатная пробная версия подходит для разработки; платная лицензия требуется для продакшн.
- **Какие координаты Maven требуются?** `com.aspose:aspose-cells:24.10`.
- **Можно ли изменить цвета секторов?** Да, через метод `setAreaColor` у каждой серии.
- **Можно ли экспортировать диаграмму в XLSX?** Конечно — просто вызовите `workbook.save("output.xlsx")`.

## Что такое pie chart в Excel?
pie chart визуализирует одну серию данных в виде пропорциональных секторов круга, что упрощает сравнение частей целого. Угол каждого сектора соответствует его значению относительно общего количества, позволяя быстро понять распределение по категориям, таким как доля рынка, распределение бюджета или демографические проценты.

## Почему использовать Aspose.Cells для создания pie chart java?
Aspose.Cells поддерживает более 50 типов диаграмм и может работать с листами, содержащими до одного миллиона строк, без загрузки всего файла в память. Это преимущество в производительности позволяет генерировать большие отчёты на скромном оборудовании, одновременно предоставляя тонкий контроль над внешним видом диаграммы, привязкой данных и форматами экспорта, делая его превосходным выбором по сравнению со многими open‑source библиотеками.

## Предварительные требования
- **Java Development Kit (JDK)** 8 или новее.
- **IDE** такая как IntelliJ IDEA или Eclipse.
- **Maven** или **Gradle** для управления зависимостями.
- **пробная или приобретённая лицензия Aspose.Cells**.

### Требуемые библиотеки и зависимости
Add the Aspose.Cells Maven artifact to your `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

Или эквивалент для Gradle:

```gradle
implementation 'com.aspose:aspose-cells:25.3'
```

### Шаги получения лицензии
Aspose.Cells for Java является коммерческим продуктом, но вы можете начать с бесплатной пробной версии. Посетите [purchase page](https://purchase.aspose.com/buy), чтобы получить временный лицензионный ключ.

## Настройка Aspose.Cells для Java
Сначала убедитесь, что библиотека находится в вашем classpath. После добавления зависимости вы можете инициализировать API, как показано ниже.

```java
import com.aspose.cells.Workbook;

// Initialize a new workbook instance
Workbook workbook = new Workbook();
```

## Руководство по реализации

### Создание и настройка рабочей книги
Класс `Workbook` представляет весь файл Excel в памяти.

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;
import com.aspose.cells.Cells;
import com.aspose.cells.ChartType;
import com.aspose.cells.Chart;
import com.aspose.cells.Series;
import com.aspose.cells.Color;
import com.aspose.cells.LegendPositionType;
import com.aspose.cells.SaveFormat;
```

#### Шаг 1: создать экземпляр рабочей книги
```java
// Creates an empty workbook instance to work with.
Workbook workbook = new Workbook();
```  
Это создаёт новую пустую рабочую книгу, в которую вы можете сразу начать добавлять данные.

### Доступ к ячейкам листа или их изменение
`Worksheet` представляет отдельный лист внутри рабочей книги, содержащий ячейки, строки и столбцы.  
Вы запишете данные, которые будут использоваться для построения pie chart, в лист.

#### Шаг 2: получить первый лист и его ячейки
```java
// Access the first worksheet in the workbook.
Worksheet worksheet = workbook.getWorksheets().get(0);
Cells cells = worksheet.getCells();

// Put sample values used for a pie chart into specific cells.
cells.get("C3").putValue("India");
cells.get("C4").putValue("China");
cells.get("C5").parseNumber("United States", true, null);
cells.get("C6").setValue("Russia");
cells.get("C7").setValue("United Kingdom");
cells.get("C8").setValue("Others");

// Put percentage values for a pie chart into specific cells.
cells.get("D2").putValue("% of world population");
cells.get("D3").putValue(25);
cells.get("D4").putValue(30);
cells.get("D5").putValue(10);
cells.get("D6").putValue(13);
cells.get("D7").putValue(9);
cells.get("D8").putValue(13);
```  
Заполните ячейки названиями категорий и значениями, которые будет использовать диаграмма.

### Создание pie chart
Объекты `Chart` визуализируют данные в листе и поддерживают различные типы, такие как pie, column и line.

#### Шаг 3: добавить pie chart на лист
```java
// Create a pie chart in the worksheet.
int pieIdx = worksheet.getCharts().add(ChartType.PIE, 1, 6, 15, 14);
Chart pie = worksheet.getCharts().get(pieIdx);
```  

### Настройка серии и данных pie chart
`Series` определяет диапазон данных и форматирование для диаграммы, связывая ячейки листа с визуальными элементами.

#### Шаг 4: задать серию для диаграммы
```java
// Configure the series data range for the chart.
pie.getNSeries().add("D3:D8", true);
pie.getNSeries().setCategoryData("=Sheet1!$C$3:$C$8");

// Link the pie chart title to a cell containing the title text.
pie.getTitle().setLinkedSource("D2");
```  

### Настройка внешнего вида легенды и заголовка диаграммы
`Legend` диаграммы отображает имена серий и их цвета, помогая читателям идентифицировать каждый сектор.

#### Шаг 5: настроить легенду и заголовок диаграммы
```java
// Set legend position at bottom of the chart.
pie.getLegend().setPosition(LegendPositionType.BOTTOM);

// Set font properties for the chart title.
pie.getTitle().getFont().setName("Calibri");
pie.getTitle().getFont().setSize(18);
```  

### Настройка цветов серии диаграммы
`setAreaColor` задаёт цвет заливки сектора серии диаграммы с использованием RGB‑значения.

#### Шаг 6: изменить цвета сегментов pie
```java
import com.aspose.cells.Color;

// Access and customize colors of individual pie chart segments.
Series srs = pie.getNSeries().get(0);
srs.getPoints().get(0).getArea().setForegroundColor(Color.fromArgb(0, 246, 22, 219));
srs.getPoints().get(1).getArea().setForegroundColor(Color.fromArgb(0, 51, 34, 84));
srs.getPoints().get(2).getArea().setForegroundColor(Color.fromArgb(0, 46, 74, 44));
srs.getPoints().get(3).getArea().setForegroundColor(Color.fromArgb(0, 19, 99, 44));
srs.getPoints().get(4).getArea().setForegroundColor(Color.fromArgb(0, 208, 223, 7));
srs.getPoints().get(5).getArea().setForegroundColor(Color.fromArgb(0, 222, 69, 8));
```  

### Автоподгонка столбцов и сохранение рабочей книги
`autoFitColumns` автоматически подгоняет ширину столбцов под содержимое ячеек.

#### Шаг 7: отрегулировать ширину столбцов и сохранить файл
```java
// Autofit all columns.
worksheet.autoFitColumns();

// Define output directory placeholder path for saving the workbook.
String outDir = "YOUR_OUTPUT_DIRECTORY";

// Save the modified workbook to an Excel file in the specified directory.
workbook.save(outDir + "/CSOrSColorsPieChart_out.xlsx", SaveFormat.XLSX);
```  

## Распространённые сценарии использования
- **Demographic analysis:** Показать распределение населения по регионам.
- **Market‑share reporting:** Визуализировать долю каждого конкурента одним взглядом.
- **Budget allocation:** Выделить, как средства распределены между отделами.

## Соображения по производительности
- Освобождайте объекты (`workbook.dispose()`), когда они больше не нужны, чтобы освободить нативную память.
- Для огромных наборов данных используйте `WorkbookDesigner` для потоковой передачи данных вместо полной загрузки.
- Профилируйте с помощью Java Flight Recorder, чтобы выявить узкие места в генерации диаграмм.

## Часто задаваемые вопросы

**Q: Могу ли я создать несколько pie chart в одной рабочей книге?**  
A: Да, повторите шаги создания диаграммы для каждого диапазона данных; каждая диаграмма независима.

**Q: Поддерживает ли Aspose.Cells 3‑D pie chart?**  
A: Да; установите тип диаграммы `ChartType.PIE_3D` при её добавлении.

**Q: Как применить пользовательскую тему ко всем диаграммам?**  
A: Используйте метод `Workbook.setDefaultTheme` перед созданием любых диаграмм.

**Q: В какие форматы файлов можно экспортировать рабочую книгу?**  
A: Более 30 форматов, включая XLSX, CSV, PDF и HTML.

**Q: Требуется ли лицензия для коммерческого развертывания?**  
A: Да, действительная лицензия удаляет водяные знаки оценки и открывает полный функционал.

## Заключение
Теперь у вас есть полный пошаговый рецепт для **create pie chart java** с Aspose.Cells. Следуя указанным шагам, вы сможете генерировать отшлифованные Excel pie chart, настраивать цвета и заголовки, а также внедрять их в любой конвейер отчётности. Исследуйте другие типы диаграмм — column, line, radar — чтобы расширить ваш набор средств визуализации данных.

---

**Последнее обновление:** 2026-09-27  
**Тестировано с:** Aspose.Cells 24.10 for Java  
**Автор:** Aspose

## Связанные руководства

- [Настройка подписей данных диаграмм Excel с помощью Aspose.Cells for Java: пошаговое руководство](/cells/java/charts-graphs/customize-chart-data-labels-aspose-cells-java/)
- [Создание динамических диаграмм Excel с Aspose.Cells Java: полное руководство для разработчиков](/cells/java/charts-graphs/aspose-cells-java-dynamic-excel-charts/)
- [Создание и настройка Excel рабочих книг с помощью Aspose.Cells Java: пошаговое руководство](/cells/java/workbook-operations/create-customize-excel-workbooks-aspose-cells-java/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}