---
date: '2026-04-11'
description: Изучите автоматизацию Excel на Java с Aspose.Cells. Этот учебник показывает,
  как создать книгу Excel на Java, заполнить данные Excel на Java и сохранить файл
  Excel на Java с диаграммами.
keywords:
- excel automation java
- create excel workbook java
- save excel file java
- populate excel data java
- aspose cells java
title: 'Автоматизация Excel на Java: создание рабочих книг и диаграмм с помощью Aspose'
url: /ru/java/charts-graphs/aspose-cells-java-excel-workbook-charts/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Автоматизация Excel на Java: создание книг и диаграмм с помощью Aspose

## Введение

Автоматизация задач Excel с помощью Java может сэкономить часы ручной работы, особенно когда необходимо быстро генерировать отчёты, панели мониторинга или диаграммы, основанные на данных. **Excel automation java** с Aspose.Cells предоставляет чистый, высокопроизводительный API, который справляется со всем — от создания книги до сложного стилизования диаграмм. В этом руководстве вы узнаете, как настроить Aspose.Cells, **create an Excel workbook java**, заполнить её данными, добавить диаграмму, применить 3‑D‑форматирование и, наконец, **save the Excel file java**.

### Быстрые ответы
- **Which library simplifies Excel automation in Java?** Какая библиотека упрощает автоматизацию Excel в Java? Aspose.Cells for Java.  
- **Can I add 3‑D charts programmatically?** Могу ли я программно добавить 3‑D‑диаграммы? Да — API поддерживает 3‑D‑форматирование и эффекты освещения.  
- **Do I need a license for development?** Нужна ли лицензия для разработки? Доступна бесплатная пробная лицензия; для продакшн‑использования требуется коммерческая лицензия.  
- **What Java build tools are supported?** Какие инструменты сборки Java поддерживаются? Maven и Gradle полностью поддерживаются.  
- **What file formats can I export?** Какие форматы файлов можно экспортировать? XLS, XLSX, CSV, PDF и многие другие.

## Что такое автоматизация Excel на Java?

Автоматизация Excel на Java относится к процессу программного создания, изменения и сохранения книг Excel с использованием кода Java. Это устраняет ручное редактирование таблиц, обеспечивает согласованность и позволяет интегрировать Excel с другими системами, такими как базы данных или веб‑сервисы.

## Почему использовать Aspose.Cells для Java?

- **Rich feature set** – от простых значений ячеек до сложных диаграмм, сводных таблиц и условного форматирования.  
- **No Microsoft Office dependency** – работает в любой серверной среде.  
- **High performance** – оптимизировано для больших наборов данных и многопоточных сценариев.  
- **Broad format support** – чтение/запись XLS, XLSX, ODS, CSV, PDF, HTML и др.

## Требования

- **Java Development Kit (JDK) 8+**  
- **Maven или Gradle** для управления зависимостями  
- **Aspose.Cells for Java 25.3 или новее** (пробная или лицензированная версия)  

## Настройка Aspose.Cells для Java

Добавьте библиотеку в проект, используя одну из следующих конфигураций.

### Maven
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

### Gradle
```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

#### Получение лицензии

Запросите бесплатную пробную лицензию на сайте Aspose или приобретите полную лицензию для продакшн‑использования. Поместите файл лицензии в проект и загрузите его во время выполнения.

## Базовая инициализация и настройка

После того как зависимость будет подключена, можно приступать к написанию кода.

```java
import com.aspose.cells.Workbook;

public class ExcelDemo {
    public static void main(String[] args) throws Exception {
        String dataDir = "YOUR_DATA_DIRECTORY";
        String outDir = "YOUR_OUTPUT_DIRECTORY";

        // Initialize a new Workbook object
        Workbook book = new Workbook();
        System.out.println("Workbook initialized successfully.");
    }
}
```

## Пошаговое руководство

### Шаг 1: Как создать книгу Excel на Java

Создайте новый экземпляр книги, который будет содержать все ваши листы.

```java
import com.aspose.cells.Workbook;
// Initialize a new Workbook object
Workbook book = new Workbook();
```

### Шаг 2: Добавить листы (включая лист с диаграммой)

```java
import com.aspose.cells.Worksheet;
Worksheet dataSheet = book.getWorksheets().add("DataSheet");
Worksheet chartSheet = book.getWorksheets().add("MyChart");
System.out.println("Worksheets added successfully.");
```

### Шаг 3: Как заполнить данные Excel на Java

Вставьте примерные данные, которые будет использовать диаграмма.

```java
import com.aspose.cells.Cells;
Cells cells = dataSheet.getCells();
cells.get("B1").putValue(1);
cells.get("B2").putValue(2);
cells.get("B3").putValue(3);
cells.get("A1").putValue("A");
cells.get("A2").putValue("B");
cells.get("A3").putValue("C");
System.out.println("Data populated successfully.");
```

### Шаг 4: Добавить столбчатую диаграмму в книгу

```java
import com.aspose.cells.Chart;
import com.aspose.cells.ChartCollection;
import com.aspose.cells.ChartType;
ChartCollection charts = chartSheet.getCharts();
charts.add(ChartType.COLUMN, 5, 0, 25, 15);
Chart chart = book.getWorksheets().get(2).getCharts().get(0);
System.out.println("Chart added successfully.");
```

### Шаг 5: Применить цветовое форматирование к области диаграммы

```java
import com.aspose.cells.Color;
chart.getPlotArea().getArea().setBackgroundColor(Color.getWhite());
chart.getChartArea().getArea().setBackgroundColor(Color.getWhite());
chart.getPlotArea().getArea().setForegroundColor(Color.getWhite());
chart.getChartArea().getArea().setForegroundColor(Color.getWhite());
System.out.println("Color formatting applied successfully.");
```

### Шаг 6: Настроить легенду и серии данных

```java
import com.aspose.cells.Series;
chart.setShowLegend(false);
chart.getNSeries().add("DataSheet!B1:B3", true);
chart.getNSeries().setCategoryData("DataSheet!A1:A3");
Series ser = chart.getNSeries().get(0);
System.out.println("Chart series configured successfully.");
```

### Шаг 7: Применить 3D-форматирование к сериям

```java
import com.aspose.cells.Bevel;
import com.aspose.cells.BevelPresetType;
import com.aspose.cells.Format3D;
import com.aspose.cells.LightRigType;
import com.aspose.cells.PresetMaterialType;
import com.aspose.cells.ShapePropertyCollection;
ShapePropertyCollection spPr = ser.getShapeProperties();
Format3D fmt3d = spPr.getFormat3D();

Bevel bevel = fmt3d.getTopBevel();
bevel.setType(BevelPresetType.CIRCLE);
bevel.setHeight(5);
bevel.setWidth(9);
fmt3d.setSurfaceMaterialType(PresetMaterialType.WARM_MATTE);
fmt3d.setSurfaceLightingType(LightRigType.THREE_POINT);
fmt3d.setLightingAngle(20);
System.out.println("3D formatting applied successfully.");
```

### Шаг 8: Установить цвета серий для лучшего визуального различия

```java
ser.getArea().setBackgroundColor(Color.getMaroon());
ser.getArea().setForegroundColor(Color.getMaroon());
ser.getBorder().setColor(Color.getMaroon());
System.out.println("Series color formatting applied successfully.");
```

### Шаг 9: Как сохранить файл Excel на Java

```java
book.save(outDir + "A3DFormat_out.xls");
System.out.println("Workbook saved successfully.");
```

## Практические применения

- **Financial Reporting** – Генерация квартальных отчётов с динамическими диаграммами.  
- **Data‑Analysis Dashboards** – Создание интерактивных панелей, автоматически обновляющихся.  
- **Inventory Management** – Экспорт уровней запасов и трендов в Excel для обзора заинтересованными сторонами.  
- **Project Planning** – Создание диаграмм в стиле Ганта напрямую из Java‑основных систем планирования.

## Советы по производительности для автоматизации Excel на Java

- **Reuse Workbook Objects** повторно используйте объекты книги при обработке нескольких листов, чтобы снизить нагрузку на память.  
- **Batch Cell Updates** используйте `Cells.importArray` для больших наборов данных вместо отдельных вызовов `putValue`.  
- **Dispose Resources** вызывайте `book.dispose()` после сохранения крупных файлов.

## Часто задаваемые вопросы

**Q: Can I generate XLSX instead of XLS?**  
A: Да — просто измените расширение файла в `book.save("output.xlsx")`; Aspose автоматически выберет правильный формат.

**Q: Is a license required for development?**  
A: Бесплатная пробная лицензия подходит для разработки и тестирования. Для продакшн‑развёртываний требуется приобретённая лицензия.

**Q: How do I add more chart types?**  
A: Используйте перечисление `ChartType` (например, `ChartType.PIE`, `ChartType.LINE`) при вызове `charts.add(...)`.

**Q: What if I need to protect the workbook?**  
A: Вызовите `book.getSettings().setPassword("yourPassword")` перед сохранением.

**Q: Does Aspose.Cells support macro‑enabled files?**  
A: Да — вы можете создавать или сохранять VBA‑макросы в рабочих книгах XLSM.

---

**Последнее обновление:** 2026-04-11  
**Тестировано с:** Aspose.Cells 25.3 (Java)  
**Автор:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}