---
"date": "2025-04-07"
"description": "Узнайте, как создавать и настраивать диаграммы в Excel с помощью Aspose.Cells для Java. Автоматизируйте создание диаграмм, улучшайте визуализацию данных и экономьте время с этим подробным руководством."
"title": "Создание и стилизация диаграмм Excel с помощью Aspose.Cells Java&#58; Полное руководство"
"url": "/ru/java/charts-graphs/aspose-cells-java-excel-charts-creation/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}


# Создание и стилизация диаграмм Excel с помощью Aspose.Cells Java

## Введение

В современном мире, управляемом данными, эффективная визуализация информации имеет решающее значение для анализа и принятия решений. Часто возникает необходимость в программном создании динамических диаграмм в книгах Excel, особенно при работе с большими наборами данных или автоматизированными системами отчетности. В этом руководстве показано, как использовать Aspose.Cells для Java для беспрепятственного создания и настройки диаграмм в Excel. Интегрируя Aspose.Cells в свои приложения Java, вы можете автоматизировать создание диаграмм, улучшить представление данных и сэкономить время.

**Что вы узнаете:**
- Инициализация рабочей книги и заполнение ее данными с помощью Aspose.Cells.
- Создание и настройка линейных диаграмм с маркерами данных.
- Настройка внешнего вида и цветов серии для лучшей визуализации.
- Сохранение книги с вновь созданной диаграммой в формате Excel.

Давайте начнем с обсуждения предварительных условий, необходимых для начала работы.

## Предпосылки

Перед созданием и оформлением диаграмм с помощью Aspose.Cells для Java убедитесь, что у вас выполнены следующие настройки:

### Необходимые библиотеки
Включите Aspose.Cells как зависимость в ваш проект. Вот инструкции для пользователей Maven и Gradle:

**Мейвен:**
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

**Градл:**
```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

### Требования к настройке среды
- В вашей системе установлен Java Development Kit (JDK).
- Интегрированная среда разработки (IDE), такая как IntelliJ IDEA или Eclipse для кодирования и тестирования.

### Необходимые знания
Требуется базовое понимание программирования на Java, а также знакомство с рабочими книгами Excel и концепциями построения диаграмм. 

### Приобретение лицензии
Aspose.Cells — это коммерческий продукт, для полной функциональности которого требуется лицензия. Вы можете получить бесплатную пробную версию, чтобы оценить его возможности, запросить временную лицензию для расширенного тестирования или приобрести продукт для долгосрочного использования.

- **Бесплатная пробная версия:** [Загрузить бесплатную пробную версию](https://releases.aspose.com/cells/java/)
- **Временная лицензия:** [Запросить временную лицензию](https://purchase.aspose.com/temporary-license/)
- **Покупка:** [Купить Aspose.Cells](https://purchase.aspose.com/buy)

## Настройка Aspose.Cells для Java

После установки необходимых зависимостей настройте среду разработки для использования Aspose.Cells. Начните с импорта библиотеки и инициализации объекта Workbook в вашем приложении Java:

```java
import com.aspose.cells.*;

public class SetupAsposeCells {
    public static void main(String[] args) throws Exception {
        // Инициализировать новый экземпляр рабочей книги
        Workbook workbook = new Workbook();
        
        System.out.println("Workbook initialized successfully!");
    }
}
```

## Руководство по внедрению

В этом разделе мы разберем реализацию на отдельные функции: инициализация рабочей книги и заполнение данных, создание и настройка диаграмм, настройка серий и сохранение рабочей книги.

### Функция 1: Инициализация рабочей книги и заполнение данными

**Обзор:** Эта функция позволяет создать новую рабочую книгу, открыть ее первый рабочий лист и заполнить его данными для создания диаграммы.

#### Шаг 1: Инициализация рабочей книги
Начните с создания экземпляра `Workbook` объект:

```java
import com.aspose.cells.*;

public class FeatureWorkbookInitialization {
    public static void main(String[] args) throws Exception {
        // Создать экземпляр рабочей книги
        Workbook workbook = new Workbook();
        
        // Доступ к первому рабочему листу
        Worksheet worksheet = workbook.getWorksheets().get(0);
```

#### Шаг 2: Задайте заголовки столбцов и заполните данные
Определите заголовки столбцов и заполните строки образцами данных:

```java
        // Установить заголовок столбца 
        worksheet.getCells().get(0, 0).setValue("X");
        worksheet.getCells().get(0, 1).setValue("Y");

        // Создать случайные данные для серии 1
        for (int i = 1; i < 21; i++) {
            worksheet.getCells().get(i, 0).setValue(i);
            worksheet.getCells().get(i, 1).setValue(0.8);
        }

        // Создать случайные данные для серии 2
        for (int i = 21; i < 41; i++) {
            worksheet.getCells().get(i, 0).setValue(i - 20);
            worksheet.getCells().get(i, 1).setValue(0.9);
        }
    }
}
```

### Функция 2: Создание и настройка диаграмм

**Обзор:** Эта функция демонстрирует, как добавить диаграмму на лист рабочей книги, задать ее стиль и настроить основные свойства.

#### Шаг 3: Добавьте диаграмму на рабочий лист
Добавьте линейную диаграмму с маркерами данных:

```java
import com.aspose.cells.*;

public class FeatureChartCreation {
    public static void main(String[] args) throws Exception {
        // Создать экземпляр рабочей книги
        Workbook workbook = new Workbook();
        
        // Доступ к первому рабочему листу
        Worksheet worksheet = workbook.getWorksheets().get(0);
        
        // Добавить диаграмму на рабочий лист
        int idx = worksheet.getCharts().add(ChartType.LINE_WITH_DATA_MARKERS, 1, 3, 20, 20);

        // Доступ к диаграмме и ее настройка
        Chart chart = worksheet.getCharts().get(idx);
        chart.setStyle(3); // Установить предопределенный стиль
        chart.setAutoScaling(true);
        chart.getTitle().setText("Sample Chart");
        chart.getCategoryAxis().getTitle().setText("Units");
    }
}
```

### Функция 3: Конфигурация серии и настройка

**Обзор:** Повысьте визуальную привлекательность своих диаграмм, настроив параметры серий, такие как различные цвета и стили маркеров.

#### Шаг 4: Настройте параметры серии
Настройте данные серии, примените пользовательское форматирование и настройте маркеры:

```java
import com.aspose.cells.*;

public class FeatureSeriesConfiguration {
    public static void main(String[] args) throws Exception {
        // Создать экземпляр рабочей книги
        Workbook workbook = new Workbook();
        
        // Доступ к первому рабочему листу
        Worksheet worksheet = workbook.getWorksheets().get(0);
        
        // Добавить ряд в диаграмму
        Chart chart = worksheet.getCharts().add(ChartType.LINE_WITH_DATA_MARKERS, 1, 3, 20, 20).get(0);

        int s2_idx = chart.getNSeries().add("A2: A21", true);
        int s3_idx = chart.getNSeries().add("A22: A41", true);

        // Включить различные цвета для точек серии
        chart.getNSeries().setColorVaried(true);

        // Настройте стили и цвета маркеров первой серии
        chart.getNSeries().get(s2_idx).getArea().setFormatting(FormattingType.CUSTOM);
        chart.getNSeries().get(s2_idx).getMarker().getArea().setForegroundColor(Color.getYellow());
        chart.getNSeries().get(s2_idx).getMarker().getBorder().setVisible(false);

        // Установите значения X и Y для первой серии
        chart.getNSeries().get(s2_idx).setXValues("A2: A21");
        chart.getNSeries().get(s2_idx).setValues("B2: B21");

        // Настройте стили и цвета маркеров второй серии
        chart.getNSeries().get(s3_idx).getArea().setFormatting(FormattingType.CUSTOM);
        chart.getNSeries().get(s3_idx).getMarker().getArea().setForegroundColor(Color.getGreen());
        chart.getNSeries().get(s3_idx).getMarker().getBorder().setVisible(false);

        // Установите значения X и Y для второй серии
        chart.getNSeries().get(s3_idx).setXValues("A22: A41");
        chart.getNSeries().get(s3_idx).setValues("B22: B41");
    }
}
```

### Функция 4: Сохранение рабочей книги

**Обзор:** Наконец, сохраните книгу, чтобы сохранить изменения и убедиться, что диаграмма включена в файл Excel.

#### Шаг 5: Сохраните рабочую книгу
Сохраните свою рабочую книгу с вновь созданными диаграммами:

```java
import com.aspose.cells.*;

public class FeatureWorkbookSaving {
    public static void main(String[] args) throws Exception {
        // Создать экземпляр рабочей книги
        Workbook workbook = new Workbook();
        
        // Откройте первый рабочий лист и добавьте данные, настройте диаграмму, как описано в предыдущих шагах...
        Worksheet worksheet = workbook.getWorksheets().get(0);
        // (Реализация добавления данных и настройки диаграммы будет здесь)

        // Сохраните книгу в файл Excel.
        workbook.save("StyledChart.xlsx");
    }
}
```

**Рекомендации по ключевым словам:**
- «Aspose.Cells для Java»
- «Создание диаграмм Excel с помощью Java»
- «Программирование Java для автоматизации Excel»

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}