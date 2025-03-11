---
title: Обновить элемент формулы Power Query
linktitle: Обновить элемент формулы Power Query
second_title: Справочник API Aspose.Cells для .NET
description: Легко обновляйте элементы формулы Power Query в Excel с помощью Aspose.Cells для .NET. Пошаговое руководство по оптимизации процессов обработки данных.
weight: 160
url: /ru/net/excel-workbook/update-power-query-formula-item/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Обновить элемент формулы Power Query

## Введение

Если вы когда-либо работали с Excel, вы знаете, насколько мощным он может быть, особенно когда вы начинаете погружаться в Power Query. Это секретный соус, который позволяет вам преобразовывать, очищать и анализировать ваши данные без усилий. Один изящный способ манипулировать вашими формулами Power Query в Excel — через Aspose.Cells для .NET. Сегодня мы проведем вас через обновление элементов формулы Power Query шаг за шагом. Итак, хватайте свою шляпу кодера, и давайте начнем!

## Предпосылки

Прежде чем погрузиться в код, вам нужно настроить несколько вещей:

1. Visual Studio: Вам понадобится интегрированная среда разработки (IDE) для написания и запуска вашего кода .NET. Visual Studio — это лучший выбор.
2.  Библиотека Aspose.Cells: Убедитесь, что в вашем проекте доступна библиотека Aspose.Cells. Вы можете загрузить ее с[сайт](https://releases.aspose.com/cells/net/).
3. Базовые знания C#: Хотя мы и рассмотрим это вместе, наличие некоторых базовых знаний C#, безусловно, будет полезно, особенно при навигации по различным классам и методам.
4. Образцы файлов Excel: Вам понадобятся файлы Excel, упомянутые в фрагменте кода. Убедитесь, что у вас есть:
   - `SamplePowerQueryFormula.xlsx`
   - `SamplePowerQueryFormulaSource.xlsx`

5. .NET Framework: убедитесь, что ваш проект ориентирован на совместимую версию .NET Framework.

Теперь, когда наш комплект готов, мы можем приступить к самой интересной части: написанию кода!

## Импортные пакеты

Первым делом вам нужно импортировать необходимые пространства имен. Вот как это сделать:

```csharp
using Aspose.Cells.DigitalSignatures;
using Aspose.Cells.QueryTables;
using System;
using System.IO;
```

Добавляя эти пространства имен, вы даете понять компилятору, что вы собираетесь использовать классы и методы из библиотеки Aspose.Cells. Этот шаг имеет решающее значение, поскольку он закладывает основу для последующего кода.

Давайте разберем предоставленный вами фрагмент кода. Этот урок проведет вас через каждую часть, гарантируя, что вы поймете, что происходит.

## Шаг 1: Настройте рабочие каталоги

На этом этапе мы определим, где находятся наши исходные и выходные файлы. Это гарантирует, что Aspose будет знать, где искать ваши файлы Excel.

```csharp
// Рабочие каталоги
string SourceDir = "Your Document Directory";
string outputDir = "Your Output Directory";
```

## Шаг 2: Загрузите рабочую книгу

Теперь давайте загрузим файл Excel, в котором находится Power Query.

```csharp
Workbook workbook = new Workbook(SourceDir + "SamplePowerQueryFormula.xlsx");
```
 The`Workbook` class — это ваша точка входа в файл Excel. Передавая путь к нашему исходному файлу, мы создаем экземпляр, который позволяет нам манипулировать им. Вы можете представить это как открытие книги — вы готовитесь прочитать (или отредактировать) ее содержимое.

## Шаг 3: Получите доступ к Data Mashup

Далее мы получим доступ к формулам Power Query, хранящимся в Data Mashup рабочей книги.

```csharp
DataMashup mashupData = workbook.DataMashup;
```
 The`DataMashup` class содержит все формулы Power Query, связанные с вашей рабочей книгой. Здесь мы будем выполнять тяжелую работу, как когда вы открываете ящик с инструментами для ремонта.

## Шаг 4: Цикл по формулам Power Query

Теперь наступает момент, когда мы перебираем формулы Power Query, чтобы найти ту, которую хотим обновить.

```csharp
foreach (PowerQueryFormula formula in mashupData.PowerQueryFormulas)
{
    foreach (PowerQueryFormulaItem item in formula.PowerQueryFormulaItems)
    {
        if (item.Name == "Source")
        {
            item.Value = "Excel.Workbook(File.Contents(\"" + SourceDir + "SamplePowerQueryFormulaSource.xlsx\"), null, true)";
        }
    }
}
```

-  Мы просматриваем каждый`PowerQueryFormula` в`mashupData`.
- В этом цикле мы погружаемся в каждый`PowerQueryFormulaItem`.
- Мы проверяем, соответствует ли имя элемента «Источник». Если это так, мы обновляем его значение, чтобы оно ссылалось на наш новый исходный файл.

Это похоже на поиск нужной страницы в руководстве и последующее внесение необходимых изменений — это простой и кропотливый процесс.

## Шаг 5: Сохраните обновленную рабочую книгу.

После внесения обновлений пришло время сохранить изменения.

```csharp
// Сохраните выходную книгу.
workbook.Save(outputDir + "SamplePowerQueryFormula_out.xlsx");
Console.WriteLine("UpdatePowerQueryFormulaItem executed successfully.");
```
 The`Save` метод записывает обновленную рабочую книгу в указанный выходной каталог. Это как запечатывание ваших правок в новой версии руководства, готовой для использования другими!

## Заключение

Поздравляем! Вы успешно обновили элемент формулы Power Query с помощью Aspose.Cells for .NET. С помощью этого метода вы можете автоматизировать изменение формул Power Query в файлах Excel, экономя драгоценное время и усилия.

## Часто задаваемые вопросы

### Что такое Aspose.Cells?
Aspose.Cells — мощная библиотека для работы с файлами Excel в приложениях .NET без необходимости установки Microsoft Excel.

### Нужен ли мне Microsoft Excel для запуска Aspose.Cells?
Нет, Aspose.Cells позволяет вам создавать и редактировать файлы Excel программным способом, не требуя наличия Excel на вашем сервере или компьютере для разработки.

### С какими типами файлов Excel я могу работать с помощью Aspose.Cells?
С помощью Aspose.Cells вы можете работать с .xlsx, .xls, .xlsm и несколькими другими форматами Excel.

### Существует ли пробная версия Aspose.Cells?
 Да, вы можете загрузить бесплатную пробную версию с сайта[Страница релиза Aspose Cells](https://releases.aspose.com/).

### Как я могу получить поддержку по Aspose.Cells?
 Вы можете получить поддержку через[Форум Aspose](https://forum.aspose.com/c/cells/9), где вы можете задать вопросы и найти ответы от сообщества и команды Aspose.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
