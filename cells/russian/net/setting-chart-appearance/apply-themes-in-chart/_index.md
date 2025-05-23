---
"description": "Узнайте, как применять темы к диаграммам в Excel с помощью Aspose.Cells для .NET с помощью нашего простого пошагового руководства. Улучшите представление данных."
"linktitle": "Применить темы в диаграмме"
"second_title": "API обработки Excel Aspose.Cells .NET"
"title": "Применить темы в диаграмме"
"url": "/ru/net/setting-chart-appearance/apply-themes-in-chart/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Применить темы в диаграмме

## Введение

Создание визуально привлекательных диаграмм в Excel имеет решающее значение для эффективной передачи ваших данных. Применяя темы, вы можете улучшить эстетику ваших диаграмм, сделав информацию не только доступной, но и увлекательной. В этом руководстве мы рассмотрим, как применять темы с помощью Aspose.Cells для .NET. Итак, хватайте любимую закуску и давайте окунемся в творческий мир диаграмм!

## Предпосылки

Прежде чем перейти к разделу кодирования, необходимо выполнить несколько предварительных условий.

### Необходимое программное обеспечение

1. Visual Studio: Убедитесь, что на вашем компьютере установлена Visual Studio. Она обеспечивает дружественную среду для разработки приложений .NET.
2. .NET Framework или .NET Core: в зависимости от ваших предпочтений у вас должна быть установлена либо .NET Framework, либо .NET Core, чтобы следовать нашему коду.
3. Aspose.Cells for .NET: Вы не можете пропустить это! Загрузите Aspose.Cells for .NET, чтобы начать. Вы можете найти DLL [здесь](https://releases.aspose.com/cells/net/).
4. Базовые знания C#: Хотя мы собираемся провести вас по коду шаг за шагом, некоторые базовые знания C# определенно пригодятся.

## Импортные пакеты

Для работы с Aspose.Cells for .NET первым шагом является импорт необходимых пакетов. В вашем проекте C# включите следующее пространство имен:

```csharp
using System;
using System.IO;

using Aspose.Cells;
using Aspose.Cells.Charts;
```

Теперь, когда мы изучили все необходимые условия, давайте шаг за шагом разберем процесс применения тем к диаграмме в Excel.

## Шаг 1: Настройте выходные и исходные каталоги

Первое, что нам нужно сделать, это установить наш выходной каталог и исходный каталог. Это то, откуда вы будете загружать файлы Excel и где будут сохраняться измененные файлы.

```csharp
// Выходной каталог
string outputDir = "Your Output Directory";

// Исходный каталог
string sourceDir = "Your Document Directory";
```

Здесь замените `Your Output Directory` и `Your Document Directory` с вашими конкретными путями. Четкое определение этих каталогов упростит ваш рабочий процесс и позволит избежать путаницы в дальнейшем.

## Шаг 2: Создание экземпляра рабочей книги

Далее, пора открыть файл Excel, содержащий диаграмму, которую вы хотите изменить. Мы делаем это, создавая экземпляр `Workbook` класс и загрузка нашего исходного файла.

```csharp
// Создайте экземпляр рабочей книги, чтобы открыть файл, содержащий диаграмму.
Workbook workbook = new Workbook(sourceDir + "sampleApplyingThemesInChart.xlsx");
```

Убедитесь, что `sampleApplyingThemesInChart.xlsx` существует в вашем исходном каталоге.

## Шаг 3: Доступ к рабочему листу

Теперь, когда у нас есть настроенная рабочая книга, следующим шагом будет доступ к конкретному рабочему листу, на котором находится наша диаграмма. 

```csharp
// Получить первый рабочий лист
Worksheet worksheet = workbook.Worksheets[0];
```

В этом случае мы просто берем первый рабочий лист, что достаточно для этого примера. Если у вас несколько листов, вы можете указать индекс листа или имя в соответствии с вашими требованиями.

## Шаг 4: Получите диаграмму

Имея рабочий лист на руках, мы теперь можем получить доступ к диаграмме, которую мы собираемся стилизовать.

```csharp
// Получить первую диаграмму на листе
Chart chart = worksheet.Charts[0];
```

Здесь мы извлекаем первую диаграмму. Если ваш рабочий лист содержит несколько диаграмм и вам нужна определенная, просто измените индекс соответствующим образом.

## Шаг 5: Примените сплошную заливку к серии

Прежде чем применять тему, давайте убедимся, что наша серия диаграмм имеет сплошную заливку. Вот как это можно настроить:

```csharp
// Укажите тип FillFormat для Solid Fill первой серии.
chart.NSeries[0].Area.FillFormat.FillType = Aspose.Cells.Drawing.FillType.Solid;
```

Эта строка кода гарантирует, что для первой серии диаграммы будет использоваться сплошная заливка.

## Шаг 6: Настройте цвет

Теперь, когда наша серия готова, нам нужно изменить ее цвет. Это включает в себя создание `CellsColor` объект и указание цвета темы. Для этого примера мы выберем акцентный стиль.

```csharp
// Получить цвет ячеек SolidFill
CellsColor cc = chart.NSeries[0].Area.FillFormat.SolidFill.CellsColor;

// Создать тему в стиле Accent
cc.ThemeColor = new ThemeColor(ThemeColorType.Accent6, 0.6);
```

Вот что происходит:
1. Получаем цвет сплошной заливки.
2. С использованием `ThemeColor`мы задаем цвет для нашей сплошной заливки. Вы можете изменить `Accent6` на любой другой цвет темы в зависимости от того, что вам нравится.

## Шаг 7: Применение темы к серии

После настройки цвета пришло время применить новую тему к нашей серии. 

```csharp
// Применить тему к серии
chart.NSeries[0].Area.FillFormat.SolidFill.CellsColor = cc;
```

Эта линия фактически обновляет цвета на диаграмме. 

## Шаг 8: Сохраните рабочую книгу

После всей этой тяжелой работы нам нужно сохранить изменения в новом файле Excel.

```csharp
// Сохраните файл Excel.
workbook.Save(outputDir + "outputApplyingThemesInChart.xlsx");
```

Здесь мы сохраняем измененную книгу в указанном вами ранее выходном каталоге. 

## Шаг 9: Подтверждение вывода

Чтобы уведомить себя об успешном выполнении процесса, мы можем распечатать подтверждающее сообщение:

```csharp
Console.WriteLine("ApplyingThemesInChart executed successfully.");
```

Эта строка выведет в консоль сообщение о том, что задача выполнена.

## Заключение

Применение тем к вашим диаграммам в Excel с помощью Aspose.Cells for .NET может полностью преобразить способ просмотра ваших данных. Это не только сделает ваши диаграммы эстетически приятными, но и поможет более эффективно донести ваше сообщение. Выполнив шаги, описанные в этом руководстве, вы сможете легко настроить свои диаграммы и представить свои данные таким образом, чтобы привлечь внимание вашей аудитории.

## Часто задаваемые вопросы

### Что такое Aspose.Cells?
Aspose.Cells — мощная библиотека для .NET, которая позволяет разработчикам программно манипулировать файлами Excel.

### Могу ли я попробовать Aspose.Cells перед покупкой?
Да, вы можете загрузить бесплатную пробную версию [здесь](https://releases.aspose.com/).

### Какие типы тем диаграмм я могу применять?
Aspose.Cells поддерживает различные цвета тем, включая стили Accent и другие.

### Можно ли применять темы к нескольким диаграммам?
Конечно! Вы можете пройти по циклу `worksheet.Charts` и применяйте темы по мере необходимости.

### Где я могу получить поддержку по Aspose.Cells?
Вы можете получить поддержку и взаимодействовать с сообществом пользователей. [здесь](https://forum.aspose.com/c/cells/9).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}