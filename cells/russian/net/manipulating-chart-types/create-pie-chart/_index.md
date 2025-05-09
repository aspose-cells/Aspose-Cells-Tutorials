---
"description": "Узнайте, как создать круговую диаграмму в Excel с помощью Aspose.Cells для .NET с помощью этого пошагового руководства. Визуализируйте свои данные без усилий."
"linktitle": "Создать круговую диаграмму"
"second_title": "API обработки Excel Aspose.Cells .NET"
"title": "Создать круговую диаграмму"
"url": "/ru/net/manipulating-chart-types/create-pie-chart/"
"weight": 12
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Создать круговую диаграмму

## Введение

Создание диаграмм необходимо для визуального представления данных, а круговые диаграммы являются одним из самых популярных способов проиллюстрировать, как части составляют целое. С Aspose.Cells для .NET вы можете легко автоматизировать создание круговых диаграмм в файлах Excel. В этом руководстве мы рассмотрим, как создать круговую диаграмму с нуля с помощью Aspose.Cells для .NET, с пошаговым руководством, которое сделает этот процесс простым и понятным. Независимо от того, новичок ли вы в этом инструменте или хотите улучшить свои навыки автоматизации Excel, это руководство вам поможет!

## Предпосылки

Прежде чем приступить к работе с кодом, убедитесь, что у вас настроено следующее:

1. Библиотека Aspose.Cells for .NET: Убедитесь, что в вашем проекте установлен Aspose.Cells. Если вы еще не установили его, вы можете загрузить его с [здесь](https://releases.aspose.com/cells/net/).
2. Среда разработки .NET: убедитесь, что ваш проект настроен на использование .NET Framework или .NET Core.
3. Базовые знания C#: вы должны иметь навыки программирования на C#, особенно объектно-ориентированного программирования (ООП).

Для продвинутых пользователей может быть применена временная лицензия, чтобы разблокировать все функции Aspose.Cells. Вы можете запросить ее у [здесь](https://purchase.aspose.com/temporary-license/).

## Импортные пакеты

Для начала импортируйте необходимые пространства имен и пакеты, требуемые для этого руководства. Они включают базовые операции ввода-вывода и пакет Aspose.Cells.

```csharp
using System;
using System.IO;

using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
using Aspose.Cells.Charts;
```

## Шаг 1: Создайте новую рабочую книгу

Для начала нам нужно создать экземпляр `Workbook` класс, который представляет файл Excel. Рабочая книга содержит несколько листов, и в нашем примере мы будем работать с двумя листами — одним для данных и одним для круговой диаграммы.

```csharp
Workbook workbook = new Workbook();
```

Это инициализирует новую книгу Excel. Но куда попадают данные? Давайте займемся этим на следующем шаге.

## Шаг 2: Добавьте данные на рабочий лист

После создания рабочей книги нам нужно получить доступ к первому рабочему листу и дать ему имя. Здесь мы будем вводить данные, необходимые для круговой диаграммы.

```csharp
Worksheet sheet = workbook.Worksheets[0];
sheet.Name = "Data";
Cells cells = sheet.Cells;
```

Теперь мы можем ввести некоторые фиктивные данные о продажах, представляющие разные регионы:

```csharp
cells["A1"].PutValue("Region");
cells["A2"].PutValue("France");
cells["A3"].PutValue("Germany");
cells["A4"].PutValue("England");
cells["A5"].PutValue("Sweden");
cells["A6"].PutValue("Italy");
cells["A7"].PutValue("Spain");
cells["A8"].PutValue("Portugal");

cells["B1"].PutValue("Sales");
cells["B2"].PutValue(70000);
cells["B3"].PutValue(55000);
cells["B4"].PutValue(30000);
cells["B5"].PutValue(40000);
cells["B6"].PutValue(35000);
cells["B7"].PutValue(32000);
cells["B8"].PutValue(10000);
```

Здесь мы добавляем два столбца: один для регионов и другой для показателей продаж. Эти данные будут представлены в круговой диаграмме.

## Шаг 3: Добавьте лист диаграммы

Далее давайте добавим отдельный рабочий лист для хранения круговой диаграммы.

```csharp
int sheetIndex = workbook.Worksheets.Add(SheetType.Chart);
Worksheet chartSheet = workbook.Worksheets[sheetIndex];
chartSheet.Name = "Chart";
```

Этот новый лист будет содержать круговую диаграмму. Присвоение ему имени, например, «Диаграмма», гарантирует, что пользователи будут знать, чего ожидать, когда они откроют файл.

## Шаг 4: Создание круговой диаграммы

Теперь пришло время создать саму диаграмму. Укажем, что хотим круговую диаграмму, и определим ее положение на листе.

```csharp
int chartIndex = chartSheet.Charts.Add(Aspose.Cells.Charts.ChartType.Pie, 5, 0, 25, 10);
Aspose.Cells.Charts.Chart chart = chartSheet.Charts[chartIndex];
```

Метод `Add()` принимает параметры для типа диаграммы (в данном случае, `ChartType.Pie`), и его местоположение на рабочем листе. Числа представляют позиции строк и столбцов.

## Шаг 5: Настройте внешний вид диаграммы

Круговая диаграмма не будет полной без некоторой настройки! Давайте сделаем нашу диаграмму визуально привлекательной, изменив цвета, метки и заголовок.

### Установить заголовок диаграммы
```csharp
chart.Title.Text = "Sales By Region";
chart.Title.Font.Color = Color.Blue;
chart.Title.Font.IsBold = true;
chart.Title.Font.Size = 12;
```

### Настроить площадь участка
```csharp
chart.PlotArea.Area.ForegroundColor = Color.Coral;
chart.PlotArea.Area.FillFormat.SetTwoColorGradient(Color.Yellow, Color.White, GradientStyleType.Vertical, 2);
chart.PlotArea.Border.IsVisible = false;
```

Мы устанавливаем градиентную заливку для области графика и скрываем границу для более чистого вида.

## Шаг 6: Определите данные диаграммы

Пришло время связать диаграмму с нашими данными. `NSeries` Свойство диаграммы привязывает показатели продаж и регионы к круговой диаграмме.

```csharp
chart.NSeries.Add("Data!B2:B8", true);
chart.NSeries.CategoryData = "Data!A2:A8";
chart.NSeries.IsColorVaried = true;
```

Первая строка указывает, что мы используем данные о продажах из ячеек `B2:B8`. Мы также говорим диаграмме использовать названия регионов из `A2:A8` как метки категорий.

## Шаг 7: Добавьте метки данных

Добавление меток непосредственно к сегментам диаграммы может облегчить понимание. Давайте включим названия регионов и значения продаж в сегменты круговой диаграммы.

```csharp
for (int i = 0; i < chart.NSeries.Count; i++)
{
    DataLabels labels = chart.NSeries[i].DataLabels;
    labels.ShowCategoryName = true;
    labels.ShowValue = true;
    labels.Position = LabelPositionType.InsideBase;
}
```

## Шаг 8: Настройте область диаграммы и легенду

Наконец, давайте придадим области диаграммы и легенде последние штрихи. Это улучшит общее представление диаграммы.

### Область диаграммы
```csharp
ChartArea chartArea = chart.ChartArea;
chartArea.Area.Formatting = FormattingType.Custom;
chartArea.Area.FillFormat.Texture = TextureType.BlueTissuePaper;
```

### Легенда
```csharp
Legend legend = chart.Legend;
legend.Position = LegendPositionType.Left;
legend.Font.IsBold = true;
legend.Border.Color = Color.Blue;
legend.Area.FillFormat.Texture = TextureType.Bouquet;
```

## Шаг 9: Сохраните рабочую книгу

Наконец, мы сохраняем книгу в файл Excel. Вы можете указать выходной каталог и имя файла по мере необходимости.

```csharp
workbook.Save(outputDir + "outputHowToCreatePieChart.xlsx");
```

## Заключение

Создание круговой диаграммы с помощью Aspose.Cells для .NET — простой и настраиваемый процесс. Следуя этому руководству, вы сможете создать профессионально выглядящую диаграмму, которая передает ценную информацию всего за несколько шагов. Будь то для бизнес-отчетов или образовательных целей, освоение создания диаграмм повысит ваши навыки автоматизации Excel. Помните, Aspose.Cells обеспечивает гибкость, необходимую для создания потрясающих, управляемых данными файлов Excel без усилий.

## Часто задаваемые вопросы

### Могу ли я создавать другие типы диаграмм с помощью Aspose.Cells для .NET?
Да! Aspose.Cells поддерживает различные типы диаграмм, включая столбчатые диаграммы, линейные диаграммы и диаграммы рассеяния.

### Нужна ли мне платная лицензия для использования Aspose.Cells для .NET?
Вы можете использовать бесплатную версию с некоторыми ограничениями. Для полного функционала вам понадобится лицензия, которую вы можете купить [здесь](https://purchase.aspose.com/buy).

### Могу ли я экспортировать диаграмму в такие форматы, как PDF или изображения?
Конечно! Aspose.Cells позволяет экспортировать диаграммы в различные форматы, включая PDF и PNG.

### Можно ли оформить каждый кусок пирога разными цветами?
Да, вы можете применить разные цвета к каждому срезу, установив `IsColorVaried` собственность `true`, как показано в уроке.

### Можно ли автоматизировать создание нескольких диаграмм в одной рабочей книге?
Да, вы можете создавать и настраивать столько диаграмм, сколько необходимо, в одном файле Excel.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}