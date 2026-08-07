---
date: '2026-04-02'
description: Узнайте, как создавать диаграммы и генерировать пузырьковую диаграмму
  Excel с помощью Aspose.Cells для Java. Это руководство проведёт вас через настройку,
  данные и сохранение диаграммы.
keywords:
- how to create chart
- generate excel bubble chart
- set bubble chart data
title: 'Как создать диаграмму: пузырьковая диаграмма Excel с Aspose.Cells Java'
url: /ru/java/charts-graphs/aspose-cells-java-create-bubble-charts/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Как создать диаграмму: Excel Bubble Chart с Aspose.Cells Java

Улучшите свои Excel‑отчёты с помощью динамических пузырьковых диаграмм, используя Aspose.Cells for Java. В этом руководстве вы узнаете **how to create chart** объекты, визуализирующие данные в виде пузырьковых диаграмм, делая ваши презентации более информативными и интерактивными. Мы пройдём каждый шаг — от настройки среды разработки до конфигурирования данных диаграммы и, наконец, сохранения рабочей книги.

## Быстрые ответы
- **Какая библиотека лучше всего подходит для диаграмм Excel в Java?** Aspose.Cells for Java.
- **Могу ли я программно генерировать Excel bubble chart?** Да, используя API диаграмм, показанный ниже.
- **Нужна ли лицензия для выполнения кода?** Бесплатная пробная версия работает, но полная лицензия открывает все функции.
- **Какие инструменты сборки Java поддерживаются?** Maven и Gradle поддерживаются.
- **Какой основной метод для установки данных пузырьковой диаграммы?** Используйте `setBubbleSizes`, `setXValues` и `setValues` у серии.

## Что такое пузырьковая диаграмма?
Пузырьковая диаграмма — это вариант точечной диаграммы, где каждая точка представлена пузырём. Ось X и ось Y определяют позицию, а размер пузыря передаёт третье измерение информации — идеально подходит для визуализации финансовых, продажных или научных данных.

## Почему использовать Aspose.Cells for Java?
- **Zero‑install Excel engine** – не требуется Microsoft Office на сервере.
- **Rich charting API** – поддерживает все современные типы диаграмм, включая пузырьковые диаграммы.
- **Cross‑platform** – работает на Windows, Linux и macOS.
- **High performance** – оптимизировано для больших наборов данных и генерации отчётов в больших объёмах.

## Предварительные требования
Чтобы создавать пузырьковые диаграммы с помощью Aspose.Cells for Java, убедитесь, что выполнены следующие предварительные требования:

### Требуемые библиотеки и зависимости
- **Aspose.Cells for Java**: Установите последнюю версию (например, 25.3).

### Требования к настройке среды
- Установлен совместимый Java Development Kit (JDK).
- Настройте проект для использования Maven или Gradle.

### Требования к знаниям
- Базовое понимание программирования на Java.
- Знакомство со структурой файлов Excel и типами диаграмм.

## Настройка Aspose.Cells for Java
Настройка вашей среды имеет решающее значение. Вот как можно начать:

### Установка через Maven
Добавьте следующую зависимость в ваш `pom.xml`:
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

### Установка через Gradle
Для пользователей Gradle добавьте следующее в ваш `build.gradle`:
```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

### Приобретение лицензии
Aspose.Cells предлагает бесплатную пробную версию с ограниченной функциональностью. Для полного доступа:
- **Purchase**: Перейдите на страницу [purchase page](https://purchase.aspose.com/buy) для вариантов лицензирования.
- **Temporary License**: Получите временную лицензию по ссылке [here](https://purchase.aspose.com/temporary-license/) для полного тестирования.

### Базовая инициализация
Перед использованием Aspose.Cells инициализируйте его в вашем Java‑проекте:
```java
import com.aspose.cells.Workbook;

// Initialize a new Workbook object
Workbook workbook = new Workbook();
```

## Руководство по реализации
Разберём процесс создания и настройки пузырьковых диаграмм с Aspose.Cells.

### Как создать диаграмму: инициализация объекта Workbook
`Workbook` представляет собой весь файл Excel, позволяя управлять листами, ячейками и т.д. Инициализируйте его следующим образом:
```java
import com.aspose.cells.Workbook;

// Create a new Workbook instance
Workbook workbook = new Workbook();
```

### Как установить данные пузырьковой диаграммы: доступ к листам и их манипуляция
Подготовьте данные, которые будут использоваться в пузырьковой диаграмме:
```java
import com.aspose.cells.WorksheetCollection;
import com.aspose.cells.Cells;
import com.aspose.cells.Cell;

// Get the collection of worksheets
WorksheetCollection worksheets = workbook.getWorksheets();
Worksheet sheet = worksheets.get(0);
Cells cells = sheet.getCells();

// Set values in specific cells to prepare data for charting
cells.get("A1").setValue(50);
cells.get("A2").setValue(100);
cells.get("A3").setValue(150);
cells.get("B1").setValue(4);
cells.get("B2").setValue(20);
cells.get("B3").setValue(180);
cells.get("C1").setValue(320);
cells.get("C2").setValue(110);
cells.get("C3").setValue(180);
cells.get("D1").setValue(40);
cells.get("D2").setValue(120);
cells.get("D3").setValue(250);
```

### Как сгенерировать Excel Bubble Chart: создание и настройка диаграммы
Создайте пузырьковую диаграмму, добавив её на лист и задав источники данных:
```java
import com.aspose.cells.ChartCollection;
import com.aspose.cells.Chart;
import com.aspose.cells.SeriesCollection;
import com.aspose.cells.ChartType;

// Access the collection of charts in the sheet
ChartCollection charts = sheet.getCharts();
int chartIndex = charts.add(ChartType.BUBBLE, 5, 0, 15, 5);
Chart chart = charts.get(chartIndex);

// Add series to the chart and set data sources
SeriesCollection serieses = chart.getNSeries();
serieses.add("A1:B3", true);

// Set bubble sizes, X values, and Y values for the chart
chart.getNSeries().get(0).setBubbleSizes("B2:D2");
chart.getNSeries().get(0).setXValues("B3:D3");
chart.getNSeries().get(0).setValues("B1:D1");
```

### Как сохранить диаграмму: сохранение Workbook
Сохраните рабочую книгу (и встроенную диаграмму) на диск:
```java
import com.aspose.cells.SaveFormat;

// Define the directory to save the file
String dataDir = "YOUR_DATA_DIRECTORY";
workbook.save(dataDir + "/HToCrBChart_out.xls", SaveFormat.EXCEL_97_TO_2003);
```

## Практические применения
- **Financial Reporting** – Визуализировать доход, прибыль и долю рынка в одном представлении.
- **Sales Data Analysis** – Выделить региональные показатели продаж, где размер пузыря показывает объём.
- **Scientific Research** – Показать экспериментальные результаты с тремя переменными одновременно.

## Соображения по производительности
- Своевременно освобождайте неиспользуемые объекты, чтобы освободить память.
- Делайте диапазоны данных как можно более узкими; большие ненужные диапазоны могут замедлять отрисовку.
- Применяйте лучшие практики управления памятью в Java при обработке огромных наборов данных.

## Распространённые проблемы и решения
| Проблема | Причина | Решение |
|----------|---------|----------|
| **Empty chart** | Диапазоны данных не соответствуют сериям | Убедитесь, что `setBubbleSizes`, `setXValues` и `setValues` ссылаются на правильные ячейки. |
| **Incorrect bubble sizes** | Несоответствие длины диапазонов | Убедитесь, что все три диапазона содержат одинаковое количество точек. |
| **License exception** | Запуск без действующей лицензии | Примените временную или приобретённую лицензию перед созданием рабочей книги. |

## Часто задаваемые вопросы

**Q: Какова минимальная версия Aspose.Cells, требуемая?**  
A: Рекомендуется версия 25.3 для этого руководства, чтобы обеспечить совместимость со всеми демонстрируемыми функциями.

**Q: Как я могу настроить цвета пузырьковой диаграммы?**  
A: Используйте методы форматирования серии, например `chart.getNSeries().get(0).getArea().getFillFormat().setForeColor(Color.getRed())`.

**Q: Можно ли запускать этот код на серверах Linux?**  
A: Да, Aspose.Cells for Java полностью кросс‑платформенный и работает на любой ОС с совместимым JDK.

**Q: Что делать, если возникает ошибка «Data source size mismatch»?**  
A: Проверьте, что диапазоны для размеров пузырей, X‑значений и Y‑значений содержат одинаковое количество ячеек.

**Q: Где можно получить временную лицензию для тестирования?**  
A: Перейдите на страницу [Aspose's temporary license page](https://purchase.aspose.com/temporary-license/) чтобы запросить пробную лицензию.

## Ресурсы
- **Documentation**: Для получения дополнительной информации обратитесь к [official documentation](https://reference.aspose.com/cells/java/).
- **Download**: Скачайте последнюю версию со [the release page](https://releases.aspose.com/cells/java/).
- **Purchase**: Ознакомьтесь с вариантами лицензирования на [this page](https://purchase.aspose.com/buy).
- **Free Trial**: Начните с бесплатной пробной версии, чтобы протестировать возможности, в разделе [Aspose's releases section](https://releases.aspose.com/cells/java/).
- **Support Forum**: По любым вопросам доступен [support forum](https://forum.aspose.com/c/cells/9).

---

**Последнее обновление:** 2026-04-02  
**Тестировано с:** Aspose.Cells 25.3 for Java  
**Автор:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}