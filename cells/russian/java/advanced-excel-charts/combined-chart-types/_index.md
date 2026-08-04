---
date: 2026-02-14
description: Узнайте, как экспортировать диаграмму в PNG, добавить серию данных, объединить
  линейную и столбчатую диаграммы, сохранить рабочую книгу в формате XLSX и добавить
  легенду к диаграмме с помощью Aspose.Cells для Java.
linktitle: Export chart to PNG and add data series for combined chart
second_title: Aspose.Cells Java Excel Processing API
title: Экспортировать диаграмму в PNG и добавить серии данных для комбинированной
  диаграммы
url: /ru/java/advanced-excel-charts/combined-chart-types/
weight: 12
---

.{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Export chart to PNG and add data series for combined chart

В этом руководстве вы **добавите серию данных** в книгу Excel, **объедините элементы линейной и столбчатой диаграмм** и узнаете, как **экспортировать диаграмму в PNG** с помощью Aspose.Cells for Java. Мы пройдем каждый шаг — от настройки книги, добавления диаграммы на лист, настройки легенды, до **save workbook as xlsx** и создания PNG‑изображения диаграммы. В конце у вас будет готовая комбинированная диаграмма, которую можно встроить в отчёты или панели мониторинга.

## Быстрые ответы
- **Какая библиотека создаёт комбинированные диаграммы?** Aspose.Cells for Java  
- **Как добавить серию данных?** Use `chart.getNSeries().add(...)`  
- **Как экспортировать диаграмму в png?** Call `chart.toImage("file.png", ImageFormat.getPng())`  
- **В каком формате можно сохранить книгу?** Standard `.xlsx` (save workbook as xlsx)  
- **Нужна ли лицензия для продакшн?** A valid Aspose.Cells license is required  

## Что такое **export chart to PNG** в Aspose.Cells?
Экспорт диаграммы в PNG создаёт растровое изображение диаграммы Excel, которое можно отображать на веб‑страницах, в отчётах или электронных письмах без необходимости использовать приложение Excel.

## Почему создавать **combined line column chart**?
Комбинированная диаграмма позволяет отображать разные наборы данных с различными визуальными представлениями (например, линейную серию поверх столбчатой) в одном окне. Это идеально для сравнения тенденций с общими итогами, выделения корреляций или предоставления более глубоких инсайтов в компактном формате.

## Требования
- Java Development Kit (JDK) 8 или выше  
- Aspose.Cells for Java library (скачайте по ссылке ниже)  
- Базовые знания синтаксиса Java и концепций Excel  

## Начало работы

Сначала скачайте библиотеку Aspose.Cells for Java с официального сайта:

[Download Aspose.Cells for Java](https://releases.aspose.com/cells/java/)

После того как JAR‑файл будет добавлен в classpath вашего проекта, вы можете приступить к построению диаграммы.

### Шаг 1: Импортировать классы Aspose.Cells
```java
import com.aspose.cells.*;
```

### Шаг 2: Создать новую книгу
```java
Workbook workbook = new Workbook();
```

### Шаг 3: Получить доступ к первому листу
```java
Worksheet worksheet = workbook.getWorksheets().get(0);
```

### Шаг 4: Добавить объект комбинированной диаграммы на лист  
Мы начнём с линейной диаграммы, а позже добавим столбцовую серию, чтобы получить эффект **combined line column chart**.
```java
int chartIndex = worksheet.getCharts().add(ChartType.LINE, 0, 0, 20, 10);
Chart chart = worksheet.getCharts().get(chartIndex);
```

## Добавление данных в диаграмму

Теперь, когда контейнер диаграммы существует, нам нужно заполнить его данными.

### Шаг 5: Определить диапазоны данных и **add data series**
```java
Cells cells = worksheet.getCells();
chart.getNSeries().add("A1:A5", true);
chart.getNSeries().add("B1:B5", true);
```
> **Pro tip:** Первый параметр (`"A1:A5"`) — диапазон первой серии, а второй (`"B1:B5"`) создаёт вторую серию, которая будет объединена с первой.

### Шаг 6: Установить данные категорий (ось X)
```java
chart.getNSeries().setCategoryData("C1:C5");
```

## Настройка диаграммы

Хорошая диаграмма рассказывает историю. Давайте добавим ей заголовки, подписи осей и понятную легенду.

### Шаг 7: **Set chart axis labels** и заголовок
```java
chart.getTitle().setText("Combined Chart Example");
chart.getCategoryAxis().getTitle().setText("Categories");
chart.getValueAxis().getTitle().setText("Values");
```

### Шаг 8: **Add legend chart** и изменить её позицию
```java
chart.getLegend().setPosition(LegendPositionType.BOTTOM);
chart.getLegend().setOverlay(true);
```

## Сохранение и экспорт диаграммы

После настройки вы захотите **save workbook as xlsx** и также создать изображение.

### Шаг 9: Сохранить книгу как файл Excel (xlsx)
```java
workbook.save("CombinedChart.xlsx");
```

### Шаг 10: **Export chart to PNG**
```java
chart.toImage("CombinedChart.png", ImageFormat.getPng());
```
> Метод `chart.toImage` **generates excel chart** изображения, которые можно использовать на веб‑страницах, в отчётах или электронных письмах.

## Распространённые проблемы и их решение

| Issue | Solution |
|-------|----------|
| **Нет данных** | Проверьте, что диапазоны ячеек (`A1:A5`, `B1:B5`, `C1:C5`) действительно содержат данные перед созданием диаграммы. |
| **Легенда перекрывает диаграмму** | Установите `chart.getLegend().setOverlay(false)` или переместите легенду в другое положение (например, `RIGHT`). |
| **Файл изображения пустой** | Убедитесь, что диаграмма имеет хотя бы одну серию и что `chart.toImage` вызывается после всех настроек. |
| **Ошибка при сохранении** | Проверьте, есть ли права записи в целевой каталог и что файл не открыт в Excel. |

## Часто задаваемые вопросы

**Q: Как установить Aspose.Cells for Java?**  
A: Скачайте JAR с официального сайта и добавьте его в classpath вашего проекта. Ссылка для загрузки: [Download Aspose.Cells for Java](https://releases.aspose.com/cells/java/).

**Q: Можно ли создавать другие типы диаграмм, кроме линейных и столбчатых?**  
A: Да, Aspose.Cells поддерживает гистограммы, круговые, точечные, областные и многие другие типы диаграмм. Обратитесь к документации API для полного списка.

**Q: Требуется ли лицензия для использования в продакшн?**  
A: Для продакшн‑развертываний требуется действующая лицензия Aspose.Cells. Доступна бесплатная пробная версия для оценки.

**Q: Как изменить цвета каждой серии?**  
A: Используйте `chart.getNSeries().get(i).setAreaColor(Color.getRed())` (или аналогичный метод) после добавления серии.

**Q: Где можно найти больше примеров кода?**  
A: Полная документация и дополнительные примеры доступны на справочном сайте Aspose: [here](https://reference.aspose.com/cells/java/).

---

**Последнее обновление:** 2026-02-14  
**Тестировано с:** Aspose.Cells for Java последняя версия  
**Автор:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}