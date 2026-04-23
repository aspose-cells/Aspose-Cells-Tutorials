---
category: general
date: 2026-03-27
description: Как привязывать данные в C# с помощью Aspose.Cells — научитесь сохранять
  книгу в формате XLSX, добавлять диаграмму и экспортировать Excel с диаграммой за
  считанные минуты.
draft: false
keywords:
- how to bind data
- save workbook as xlsx
- create excel workbook c#
- how to add chart
- export excel with chart
language: ru
og_description: Как привязать данные в C# с помощью Aspose.Cells. Это руководство
  покажет, как сохранить книгу в формате XLSX, добавить диаграмму и экспортировать
  Excel с диаграммой.
og_title: Как привязать данные в C# – создать книгу Excel
tags:
- Aspose.Cells
- C#
- Excel Automation
title: Как привязать данные в C# — создать книгу Excel
url: /ru/net/excel-data-import-export/how-to-bind-data-in-c-create-excel-workbook/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как привязать данные в C# – Создать книгу Excel

Когда‑то задавались вопросом **как привязать данные** к диаграмме в C# без потери волос? Вы не одиноки. Многие разработчики сталкиваются с проблемой, когда нужно программно генерировать файлы Excel, которые действительно *выглядят* так же, как те, что они создавали вручную.  

В этом руководстве мы пройдем через полностью готовый к запуску пример, который создает книгу Excel, заполняет её данными, привязывает эти данные к водопадной диаграмме и, наконец, сохраняет файл в формате `.xlsx`. К концу вы точно будете знать, как **сохранить книгу как XLSX**, **как добавить диаграмму** на лист и как **экспортировать Excel с диаграммой** для дальнейшей отчетности.

> **Prerequisites** – Вам понадобится Aspose.Cells for .NET (подойдет бесплатная trial‑версия) и среда разработки .NET, например Visual Studio 2022. Другие пакеты NuGet не требуются.

---

## Что покрывает этот гид

- **Create Excel workbook C#** – создание нового `Workbook` и листа.  
- **How to bind data** – сопоставление числовых рядов и меток категорий источнику данных диаграммы.  
- **How to add chart** – вставка водопадной диаграммы и настройка её заголовка.  
- **Save workbook as XLSX** – сохранение файла на диск, чтобы любой мог открыть его в Excel.  
- **Export Excel with chart** – конечный продукт – полностью функционирующая книга, которую можно делиться.

Если вы знакомы с базовым синтаксисом C#, это будет проще простого. Приступим.

---

## Шаг 1: Создать книгу Excel в C#  

Первое, что нужно – объект книги, с которым будем работать. Класс `Workbook` можно представить как пустой блокнот, который позже заполните листами (worksheets) и содержимым.

```csharp
using Aspose.Cells;
using Aspose.Cells.Charts;

class WaterfallDemo
{
    static void Main()
    {
        // Initialize a new workbook – this is your blank Excel file.
        Workbook workbook = new Workbook();

        // Grab the first worksheet (index 0). It’s already created for us.
        Worksheet worksheet = workbook.Worksheets[0];
```

> **Pro tip:** Если понадобится несколько листов, просто вызовите `workbook.Worksheets.Add()` и сохраните ссылку на каждый новый `Worksheet`.

---

## Шаг 2: Заполнить лист категориями и значениями  

Теперь мы **создадим данные в стиле excel workbook c#**. В примере используется классический сценарий водопада: старт, доход, расходы, прибыль и конец.  

```csharp
        // Add header labels.
        worksheet.Cells["A1"].PutValue("Category");
        worksheet.Cells["B1"].PutValue("Amount");

        // Sample data – you can replace these with your own source (database, API, etc.).
        string[] categoryLabels = { "Start", "Revenue", "Cost", "Profit", "End" };
        double[] values = { 0, 150, -70, 0, 80 };

        // Fill rows 2‑6 with the data.
        for (int i = 0; i < categoryLabels.Length; i++)
        {
            worksheet.Cells[i + 1, 0].PutValue(categoryLabels[i]); // Column A
            worksheet.Cells[i + 1, 1].PutValue(values[i]);       // Column B
        }
```

Почему мы ставим `0` для «Start» и «Profit»? В водопадной диаграмме эти нули выступают как *соединители*, обеспечивая правильный визуальный поток. Если их убрать, диаграмма будет выглядеть сломанной.

---

## Шаг 3: Как добавить диаграмму – вставить водопадную диаграмму  

С данными на месте пришло время **how to add chart**. Aspose.Cells делает это так же просто, как вызов `Charts.Add`.

```csharp
        // Insert a Waterfall chart starting at row 7, column 0 and spanning to row 25, column 10.
        int chartIndex = worksheet.Charts.Add(ChartType.Waterfall, 7, 0, 25, 10);
        Chart waterfallChart = worksheet.Charts[chartIndex];

        // Give the chart a meaningful title.
        waterfallChart.Title.Text = "Quarterly Waterfall";
```

Координаты `(7,0,25,10)` определяют левую‑верхнюю и правую‑нижнюю ячейки ограничивающего прямоугольника диаграммы. Подгоняйте их под свой макет.

---

## Шаг 4: Как привязать данные – соединить серии и категории  

Вот сердце руководства: **how to bind data** к диаграмме. Метод `NSeries.Add` принимает диапазон Y‑значений, а `CategoryData` указывает метки оси X.

```csharp
        // Bind the numeric series (values) – the second parameter “true” tells Aspose to treat it as a series.
        waterfallChart.NSeries.Add("B2:B6", true);

        // Bind the category (X‑axis) labels.
        waterfallChart.NSeries.CategoryData = "A2:A6";
```

Обратите внимание, что мы ссылаемся на те же ячейки, которые заполнили ранее (`A2:A6` для категорий, `B2:B6` для сумм). Если измените расположение данных, просто обновите эти диапазоны.

---

## Шаг 5: Сохранить книгу как XLSX – записать файл  

Наконец, мы **save workbook as XLSX**. Метод `Save` автоматически выбирает правильный формат по расширению файла.

```csharp
        // Save the workbook to disk. Replace YOUR_DIRECTORY with an actual path.
        workbook.Save("YOUR_DIRECTORY/WaterfallChart.xlsx");
    }
}
```

Когда откроете `WaterfallChart.xlsx` в Excel, увидите красиво отрисованную водопадную диаграмму, отражающую введённые данные. Это завершает часть **export excel with chart**.

---

## Ожидаемый результат  

- **Excel‑файл:** `WaterfallChart.xlsx` в указанной вами папке.  
- **Размещение на листе:** Столбец A содержит категории, столбец B – суммы, а диаграмма располагается под таблицей.  
- **Внешний вид диаграммы:** Водопадная диаграмма с заголовком «Quarterly Waterfall» и пятью столбцами, представляющими Start, Revenue, Cost, Profit и End.  

![пример привязки данных к водопадной диаграмме](waterfall_chart.png "Водопадная диаграмма, сгенерированная Aspose.Cells")

*Текст alt‑изображения включает основной ключевой запрос, помогая как SEO, так и AI‑цитированию.*

---

## Часто задаваемые вопросы и особые случаи  

### Что делать, если источник данных динамический?  
Замените статические массивы циклом, который читает из базы данных или API. Пока вы записываете значения в тот же диапазон ячеек, код привязки остаётся без изменений.

### Можно ли изменить тип диаграммы?  
Конечно. Замените `ChartType.Waterfall` на `ChartType.Column`, `ChartType.Line` и т.д. Не забудьте скорректировать данные серии, если новый тип ожидает другую структуру.

### Как задать цвета диаграммы?  
Используйте `waterfallChart.NSeries[0].Format.Fill.ForeColor = Color.Yellow;` (или любой `System.Drawing.Color`). Это удобно, когда нужно выделить столбец «Profit».

### Что если нужно экспортировать в PDF вместо XLSX?  
Вызовите `workbook.Save("Report.pdf", SaveFormat.Pdf);`. Диаграмма будет автоматически отрисована в PDF.

---

## Советы для production‑готового кода  

- **Dispose objects** – Оберните `Workbook` в `using`, если работаете на .NET Core, чтобы своевременно освобождать ресурсы.  
- **Path handling** – Используйте `Path.Combine(Environment.CurrentDirectory, "WaterfallChart.xlsx")`, чтобы избежать жёстко прописанных разделителей.  
- **Error handling** – Оберните `Save` в `try‑catch` для раннего обнаружения проблем с правами доступа или нехваткой места.  
- **Version check** – Aspose.Cells 23.10+ добавил улучшенную поддержку водопадных диаграмм; убедитесь, что используете актуальную версию.

---

## Заключение  

Теперь у вас есть полный, сквозной пример, демонстрирующий **how to bind data** в C#, **create excel workbook c#**, **how to add chart**, **save workbook as xlsx** и **export excel with chart**. Код готов к вставке в любой .NET‑проект, а концепции масштабируются на большие наборы данных и другие типы диаграмм.

Готовы к следующему шагу? Попробуйте добавить несколько серий, поэкспериментировать со stacked‑диаграммами или автоматизировать генерацию ежемесячных отчётов, которые будут отправляться по электронной почте заинтересованным сторонам. Возможности безграничны, как только вы освоите основы автоматизации Excel с Aspose.Cells.

Счастливого кодинга, и пусть ваши таблицы всегда отображаются безупречно!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}