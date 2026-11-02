---
date: '2026-04-08'
description: Узнайте, как создать столбчатую диаграмму в Java с помощью Aspose.Cells,
  охватывая создание диаграммы в Java, добавление листа с диаграммой и экспорт книги
  Excel.
keywords:
- generate column chart
- create chart java
- add chart sheet
- populate excel cells
- set chart title
- export workbook excel
title: Создание столбчатой диаграммы с помощью руководства Aspose.Cells Java
url: /ru/java/charts-graphs/aspose-cells-java-create-customize-charts/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Создание столбчатой диаграммы с Aspose.Cells Java

В современных приложениях, ориентированных на данные, **создание столбчатой диаграммы** быстро и программно может превратить сырые цифры в понятные визуальные инсайты. Независимо от того, создаёте ли вы панель отчётов, аналитический инструмент или простую функцию экспорта, Aspose.Cells for Java предоставляет вам удобный API для **создание chart java** проектов без работы с пользовательским интерфейсом Excel. В этом руководстве вы узнаете, как настроить библиотеку, **заполнить Excel ячейки**, добавить **chart sheet**, настроить **заголовок диаграммы** и, наконец, **экспортировать workbook excel** в файл.

## Быстрые ответы
- **Что означает “generate column chart”?** Она создаёт вертикальную столбчатую визуализацию из табличных данных.  
- **Какая библиотека требуется?** Aspose.Cells for Java (доступна бесплатная пробная версия).  
- **Нужна ли установка Excel?** Нет, библиотека работает независимо от Microsoft Excel.  
- **Можно ли экспортировать в форматы, отличные от XLS?** Да – PDF, PNG, SVG и т.д., через `workbook.save()`.  
- **Обязательна ли лицензия для продакшн?** Да, требуется приобретённая или временная лицензия.

## Что такое generate column chart?
Столбчатая диаграмма отображает серии данных в виде вертикальных столбцов, что упрощает сравнение значений по категориям, таким как регионы, месяцы или продуктовые линии. Aspose.Cells позволяет построить эту диаграмму полностью в коде, предоставляя полный контроль над данными, стилем и форматом вывода.

## Почему использовать Aspose.Cells для создания chart java?
- **Нет COM‑интеропа** – работает на любой ОС с JVM.  
- **Богатые параметры стилизации** – изображения, градиенты, легенды и пользовательские шрифты.  
- **Высокая производительность** – подходит для больших наборов данных.  
- **Множественные форматы экспорта** – XLS, XLSX, PDF, PNG и др.

## Требования
- **Java Development Kit (JDK) 8+** установлен.  
- Базовые знания Java и знакомство с концепциями Excel.  

### Требуемые библиотеки
Добавьте Aspose.Cells в ваш проект, используя один из приведённых ниже фрагментов.

#### Maven
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

#### Gradle
```gradle
implementation group: 'com.aspose', name: 'aspose-cells', version: '25.3'
```

### Получение лицензии
Aspose предлагает бесплатную пробную версию и временную лицензию для обширного тестирования.

- **Бесплатная пробная версия**: [Скачать бесплатно](https://releases.aspose.com/cells/java/)  
- **Временная лицензия**: [Запросить здесь](https://purchase.aspose.com/temporary-license/)

## Настройка Aspose.Cells для Java

Сначала создайте экземпляр `Workbook` – он будет холстом для наших данных и диаграммы.

```java
import com.aspose.cells.Workbook;

// Initialize a new Workbook
Workbook workbook = new Workbook();
```

## Пошаговое руководство

### 1. Создание и именование листа
Мы будем хранить исходные данные на листе под названием **Data**.

```java
import com.aspose.cells.Worksheet;

// Create a new Workbook instance
Workbook workbook = new Workbook();
```

```java
// Access the first worksheet and set its name to "Data"
Worksheet sheet = workbook.getWorksheets().get(0);
sheet.setName("Data");
```

### 2. Заполнение ячеек Excel
Вставьте названия регионов и показатели продаж, которые будет визуализировать столбчатая диаграмма.

```java
import com.aspose.cells.Cells;

// Get the cells collection from the "Data" sheet
Cells cells = sheet.getCells();
```

```java
// Insert region names and sales figures
cells.get("A1").putValue("Region");
cells.get("B1").putValue("Sale");

String[] regions = {"France", "Germany", "England", "Sweden", "Italy", "Spain", "Portugal"};
int[] sales = {70000, 55000, 30000, 40000, 35000, 32000, 10000};

for (int i = 0; i < regions.length; i++) {
    cells.get("A" + (i+2)).putValue(regions[i]);
    cells.get("B" + (i+2)).putValue(sales[i]);
}
```

### 3. Добавление листа диаграммы
Разделение диаграммы и исходных данных делает книгу более упорядоченной.

```java
import com.aspose.cells.SheetType;

// Add a new chart sheet
int sheetIndex = workbook.getWorksheets().add(SheetType.CHART);
Worksheet chartSheet = workbook.getWorksheets().get(sheetIndex);

// Name the worksheet "Chart"
chartSheet.setName("Chart");
```

### 4. Создание столбчатой диаграммы
Теперь мы действительно **generate column chart** объекты.

```java
import com.aspose.cells.Chart;
import com.aspose.cells.ChartType;

// Add a new column chart to the "Chart" sheet
int chartIndex = chartSheet.getCharts().add(ChartType.COLUMN, 1, 1, 25, 10);
Chart chart = chartSheet.getCharts().get(chartIndex);
```

### 5. Установка изображения в качестве фоновой заливки области построения
Фоновое изображение может выделить диаграмму.

```java
import java.io.FileInputStream;
import com.aspose.cells.Color;

String dataDir = "YOUR_DATA_DIRECTORY";
File file = new FileInputStream(dataDir + "aspose-logo.png");
byte[] data = new byte[(int)file.length()];
file.read(data);

chart.getPlotArea().getArea().getFillFormat().setImageData(data);
chart.getPlotArea().getBorder().setVisible(false);
```

### 6. Установка заголовка диаграммы
Настройка **set chart title** улучшает читаемость.

```java
// Configure the chart's title properties
chart.getTitle().setText("Sales By Region");
chart.getTitle().getFont().setColor(Color.getBlue());
chart.getTitle().getFont().setBold(true);
chart.getTitle().getFont().setSize(12);
```

### 7. Настройка данных серии и легенды
Свяжите диапазон данных с диаграммой и разместите легенду.

```java
// Set series and category data for the chart
chart.getNSeries().add("Data!B2:B8", true);
chart.getNSeries().setCategoryData("Data!A2:A8");
chart.getNSeries().setColorVaried(true);

// Position the legend at the top of the chart
import com.aspose.cells.Legend;
import com.aspose.cells.LegendPositionType;

Legend legend = chart.getLegend();
legend.setPosition(LegendPositionType.TOP);
```

### 8. Экспорт workbook Excel
Наконец, **export workbook excel** в файл XLS (или любой поддерживаемый формат).

```java
String outDir = "YOUR_OUTPUT_DIRECTORY";
workbook.save(outDir + "SPAsBFillInChart_out.xls");
```

## Практические применения
- **Business Reports** – Автоматически генерировать диаграммы продаж для ежемесячных PDF.  
- **Data Analysis Tools** – Встраивать динамические диаграммы в пользовательские аналитические панели.  
- **Enterprise Dashboards** – Обновлять изображения диаграмм «на лету» для мониторинга в реальном времени.

## Соображения по производительности
- Пакетные обновления ячеек при работе с большими наборами данных для снижения нагрузки.  
- Освобождайте ресурсы (`workbook.dispose()`), если обрабатываете множество книг в цикле.  

## Распространённые проблемы и решения
- **Image not showing** – Проверьте путь к файлу и поддерживаемый формат изображения (PNG, JPEG).  
- **Chart appears blank** – Убедитесь, что ссылки на диапазон данных (`Data!B2:B8`) соответствуют заполненным ячейкам.  
- **Out‑of‑memory errors** – Обрабатывайте данные порциями и вызывайте `System.gc()` после больших сохранений.  

## Часто задаваемые вопросы

**Q: Как добавить несколько серий в столбчатую диаграмму?**  
A: Call `chart.getNSeries().add()` repeatedly with different data ranges, e.g., `"Data!C2:C8"` for a second series.

**Q: Можно ли изменить подписи осей?**  
A: Да. Use `chart.getCategoryAxis().setTitle("Regions")` and `chart.getValueAxis().setTitle("Sales")`.

**Q: В какие форматы можно экспортировать, кроме XLS?**  
A: Используйте `workbook.save("chart.pdf")`, `workbook.save("chart.png")`, или `workbook.save("chart.xlsx")` для PDF, PNG и XLSX соответственно.

**Q: Требуется ли лицензия для сборок разработки?**  
A: Бесплатная пробная версия подходит для оценки, но для продакшн‑развертываний нужна постоянная или временная лицензия.

**Q: Как улучшить скорость рендеринга при тысячах строк?**  
A: Заполняйте ячейки с помощью `cells.importArray()` и минимизируйте перерисовку диаграмм, создавая её после загрузки всех данных.

---

**Последнее обновление:** 2026-04-08  
**Тестировано с:** Aspose.Cells 25.3 for Java  
**Автор:** Aspose  

## Ресурсы

- [Документация Aspose.Cells](https://reference.aspose.com/cells/java/)
- [Скачать Aspose.Cells](https://releases.aspose.com/cells/java/)
- [Купить лицензию](https://purchase.aspose.com/buy)
- [Бесплатная пробная версия](https://releases.aspose.com/cells/java/)
- [Запрос временной лицензии](https://purchase.aspose.com/temporary-license/)
- [Форум поддержки](https://forum.aspose.com/c/cells/9)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}