---
date: '2026-04-08'
description: Узнайте, как создать линейный график с маркерами с помощью Aspose.Cells
  for Java, добавить график на лист и настроить диаграммы Excel для автоматизированной
  отчетности.
keywords:
- line chart with markers
- add chart to worksheet
- automate excel chart creation
- populate data for chart
- export styled chart excel
title: Создание линейного графика с маркерами с помощью Aspose.Cells для Java
url: /ru/java/charts-graphs/aspose-cells-java-excel-charts-creation/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Создание и стилизация диаграмм Excel с помощью Aspose.Cells Java

## Введение

В современном мире, управляемом данными, **line chart with markers** является одним из самых эффективных способов визуализации тенденций и выбросов. Независимо от того, создаёте ли вы автоматизированные отчёты или панель мониторинга, обновляющуюся ежедневно, возможность программно добавить line chart with markers в лист экономит бесчисленное количество ручных шагов. Этот учебник проведёт вас через использование Aspose.Cells для Java для создания, стилизации и экспорта таких диаграмм, чтобы вы могли сосредоточиться на инсайтах, а не на утомительном «кручении» Excel.

**Что вы узнаете**
- Инициализация рабочей книги и заполнение её данными с помощью Aspose.Cells.  
- **Как добавить line chart with markers в лист** и настроить его внешний вид.  
- Настройка цветов серий, маркеров и других параметров стиля.  
- Сохранение рабочей книги в файл Excel, включающий вашу стилизованную диаграмму.

## Быстрые ответы
- **Какой основной класс для начала?** `Workbook` инициализирует новый файл Excel.  
- **Какой тип диаграммы создаёт line chart with markers?** `ChartType.LINE_WITH_DATA_MARKERS`.  
- **Как задать пользовательские цвета для точек серии?** Используйте `chart.getNSeries().setColorVaried(true)` и задайте цвета области маркеров.  
- **Нужна ли лицензия для полной функциональности?** Да, платная или временная лицензия Aspose.Cells снимает ограничения оценки.  
- **Могу ли я экспортировать результат как XLSX?** Конечно—`workbook.save("StyledChart.xlsx")` создаёт файл XLSX.

## Предварительные требования

Прежде чем создавать и стилизовать диаграммы с помощью Aspose.Cells для Java, убедитесь, что у вас настроена следующая среда:

### Необходимые библиотеки
Включите Aspose.Cells как зависимость в ваш проект. Ниже приведены инструкции для пользователей Maven и Gradle:

**Maven:**
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

**Gradle:**
```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

### Требования к настройке среды
- Установлен Java Development Kit (JDK) на вашей системе.  
- Интегрированная среда разработки (IDE), например IntelliJ IDEA или Eclipse, для написания кода и тестирования.

### Требования к знаниям
Необходимо базовое понимание программирования на Java, а также знакомство с рабочими книгами Excel и концепциями построения диаграмм. 

### Получение лицензии
Aspose.Cells — коммерческий продукт, требующий лицензии для полной функциональности. Вы можете получить бесплатную пробную версию для оценки возможностей, запросить временную лицензию для расширенного тестирования или приобрести продукт для длительного использования.

- **Бесплатная пробная версия:** [Download Free Trial](https://releases.aspose.com/cells/java/)  
- **Временная лицензия:** [Запросить временную лицензию](https://purchase.aspose.com/temporary-license/)  
- **Покупка:** [Купить Aspose.Cells](https://purchase.aspose.com/buy)

## Настройка Aspose.Cells для Java

После установки необходимых зависимостей настройте свою среду разработки для использования Aspose.Cells. Начните с импорта библиотеки и инициализации объекта `Workbook` в вашем Java‑приложении:

```java
import com.aspose.cells.*;

public class SetupAsposeCells {
    public static void main(String[] args) throws Exception {
        // Initialize a new workbook instance
        Workbook workbook = new Workbook();
        
        System.out.println("Workbook initialized successfully!");
    }
}
```

## Руководство по реализации

В этом разделе мы разберём реализацию на отдельные функции: Инициализация рабочей книги и заполнение данными, Создание и настройка диаграммы, Кастомизация серии и Сохранение рабочей книги.

### Функция 1: Инициализация рабочей книги и заполнение данными

**Обзор:** Эта функция сосредоточена на создании новой рабочей книги, доступе к её первому листу и заполнении его данными для построения диаграммы.

#### Шаг 1: Инициализировать рабочую книгу
Начните с создания объекта `Workbook`:

```java
import com.aspose.cells.*;

public class FeatureWorkbookInitialization {
    public static void main(String[] args) throws Exception {
        // Instantiate a workbook
        Workbook workbook = new Workbook();
        
        // Access first worksheet
        Worksheet worksheet = workbook.getWorksheets().get(0);
```

#### Шаг 2: Установить заголовки столбцов и заполнить данные
Определите заголовки столбцов и заполните строки примерными данными:

```java
        // Set columns title 
        worksheet.getCells().get(0, 0).setValue("X");
        worksheet.getCells().get(0, 1).setValue("Y");

        // Create random data for series 1
        for (int i = 1; i < 21; i++) {
            worksheet.getCells().get(i, 0).setValue(i);
            worksheet.getCells().get(i, 1).setValue(0.8);
        }

        // Create random data for series 2
        for (int i = 21; i < 41; i++) {
            worksheet.getCells().get(i, 0).setValue(i - 20);
            worksheet.getCells().get(i, 1).setValue(0.9);
        }
    }
}
```

### Функция 2: Создание и настройка диаграммы

**Обзор:** Эта функция демонстрирует, как добавить диаграмму на лист рабочей книги, задать её стиль и настроить базовые свойства.

#### Шаг 3: Добавить диаграмму в лист
Добавьте line chart with data markers:

```java
import com.aspose.cells.*;

public class FeatureChartCreation {
    public static void main(String[] args) throws Exception {
        // Instantiate a workbook
        Workbook workbook = new Workbook();
        
        // Access first worksheet
        Worksheet worksheet = workbook.getWorksheets().get(0);
        
        // Add chart to the worksheet
        int idx = worksheet.getCharts().add(ChartType.LINE_WITH_DATA_MARKERS, 1, 3, 20, 20);

        // Access and configure the chart
        Chart chart = worksheet.getCharts().get(idx);
        chart.setStyle(3); // Set a predefined style
        chart.setAutoScaling(true);
        chart.getTitle().setText("Sample Chart");
        chart.getCategoryAxis().getTitle().setText("Units");
    }
}
```

### Функция 3: Настройка и кастомизация серии

**Обзор:** Улучшите визуальную привлекательность ваших диаграмм, настроив параметры серии, такие как разнообразные цвета и стили маркеров.

#### Шаг 4: Настроить параметры серии
Настройте данные серии, примените пользовательское форматирование и скорректируйте маркеры:

```java
import com.aspose.cells.*;

public class FeatureSeriesConfiguration {
    public static void main(String[] args) throws Exception {
        // Instantiate a workbook
        Workbook workbook = new Workbook();
        
        // Access first worksheet
        Worksheet worksheet = workbook.getWorksheets().get(0);
        
        // Add series to the chart
        Chart chart = worksheet.getCharts().add(ChartType.LINE_WITH_DATA_MARKERS, 1, 3, 20, 20).get(0);

        int s2_idx = chart.getNSeries().add("A2: A21", true);
        int s3_idx = chart.getNSeries().add("A22: A41", true);

        // Enable varied colors for series points
        chart.getNSeries().setColorVaried(true);

        // Customize first series marker styles and colors
        chart.getNSeries().get(s2_idx).getArea().setFormatting(FormattingType.CUSTOM);
        chart.getNSeries().get(s2_idx).getMarker().getArea().setForegroundColor(Color.getYellow());
        chart.getNSeries().get(s2_idx).getMarker().getBorder().setVisible(false);

        // Set X and Y values for the first series
        chart.getNSeries().get(s2_idx).setXValues("A2: A21");
        chart.getNSeries().get(s2_idx).setValues("B2: B21");

        // Customize second series marker styles and colors
        chart.getNSeries().get(s3_idx).getArea().setFormatting(FormattingType.CUSTOM);
        chart.getNSeries().get(s3_idx).getMarker().getArea().setForegroundColor(Color.getGreen());
        chart.getNSeries().get(s3_idx).getMarker().getBorder().setVisible(false);

        // Set X and Y values for the second series
        chart.getNSeries().get(s3_idx).setXValues("A22: A41");
        chart.getNSeries().get(s3_idx).setValues("B22: B41");
    }
}
```

### Функция 4: Сохранение рабочей книги

**Обзор:** Наконец, сохраните рабочую книгу, чтобы зафиксировать изменения и убедиться, что диаграмма включена в файл Excel.

#### Шаг 5: Сохранить рабочую книгу
Сохраните вашу рабочую книгу с новыми диаграммами:

```java
import com.aspose.cells.*;

public class FeatureWorkbookSaving {
    public static void main(String[] args) throws Exception {
        // Instantiate a workbook
        Workbook workbook = new Workbook();
        
        // Access first worksheet and add data, chart configuration as per previous steps...
        Worksheet worksheet = workbook.getWorksheets().get(0);
        // (Implementation of adding data and configuring the chart would be here)

        // Save the workbook to an Excel file
        workbook.save("StyledChart.xlsx");
    }
}
```

### Распространённые проблемы и их устранение

- **Диаграмма отображается пустой:** Убедитесь, что диапазоны ячеек, используемые в `setXValues` и `setValues`, правильно ссылаются на заполненные ячейки.  
- **Цвета не применяются:** Убедитесь, что `chart.getNSeries().setColorVaried(true)` вызывается до настройки отдельных серий.  
- **Ошибки лицензии:** Пробная лицензия может ограничивать количество диаграмм; установите полную лицензию, чтобы снять ограничения.

## Часто задаваемые вопросы

**В: Могу ли я создавать другие типы диаграмм (например, столбчатые, круговые) с помощью Aspose.Cells?**  
О: Да, Aspose.Cells поддерживает широкий спектр типов диаграмм; просто замените `ChartType.LINE_WITH_DATA_MARKERS` нужным значением перечисления.

**В: Нужно ли закрывать рабочую книгу или освобождать ресурсы?**  
О: Класс `Workbook` управляет ресурсами автоматически, но в длительно работающих приложениях вы можете вызвать `workbook.dispose()`, чтобы освободить память.

**В: Можно ли добавить несколько диаграмм на один лист?**  
О: Конечно—вызовите `worksheet.getCharts().add(...)` для каждой диаграммы, которую хотите вставить.

**В: Как экспортировать файл в более старый формат Excel (XLS)?**  
О: Используйте `workbook.save("StyledChart.xls", SaveFormat.EXCEL_97_TO_2003);`.

**В: Сохранит ли диаграмма свой стиль при открытии в Microsoft Excel?**  
О: Да, Aspose.Cells записывает нативные объекты диаграмм Excel, поэтому все стили, цвета и маркеры отображаются точно так, как заданы.

---

**Последнее обновление:** 2026-04-08  
**Тестировано с:** Aspose.Cells 25.3 for Java  
**Автор:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}