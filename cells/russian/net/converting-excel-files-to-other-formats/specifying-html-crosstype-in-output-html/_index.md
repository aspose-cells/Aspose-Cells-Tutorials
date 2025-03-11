---
title: Указание HTML CrossType в выходном HTML программным способом в .NET
linktitle: Указание HTML CrossType в выходном HTML программным способом в .NET
second_title: API обработки Excel Aspose.Cells .NET
description: Узнайте, как указать HTML CrossType в Aspose.Cells для .NET. Следуйте нашему пошаговому руководству, чтобы преобразовать файлы Excel в HTML с точностью.
weight: 17
url: /ru/net/converting-excel-files-to-other-formats/specifying-html-crosstype-in-output-html/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Указание HTML CrossType в выходном HTML программным способом в .NET

## Введение
Когда дело доходит до преобразования файлов Excel в HTML в приложениях .NET, вам может потребоваться указать, как обрабатываются перекрестные ссылки в выходных данных. Класс HtmlSaveOptions в Aspose.Cells для .NET предоставляет различные параметры для управления процессом преобразования, и одним из таких параметров является HtmlCrossType. В этом руководстве мы рассмотрим, как программно указать перекрестный тип HTML при экспорте файлов Excel в формат HTML. 
## Предпосылки
Прежде чем приступить к изучению кода, убедитесь, что у вас есть следующее:
-  Aspose.Cells для .NET: Убедитесь, что в вашем проекте установлена библиотека Aspose.Cells. Вы можете загрузить ее с[Сайт Aspose](https://releases.aspose.com/cells/net/).
- Visual Studio: рабочая установка Visual Studio или любой другой среды разработки .NET.
- Базовые знания C#: знакомство с программированием на C# поможет вам лучше понять примеры.
-  Образец файла Excel: Имейте готовый образец файла Excel для работы. Для этого примера мы будем использовать`sampleHtmlCrossStringType.xlsx`.
## Импортные пакеты
Для начала вам нужно импортировать необходимые пространства имен Aspose.Cells. Вот как это можно сделать:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
Давайте разберем это шаг за шагом, чтобы вам было легче следовать инструкциям и реализовывать эту функциональность в своих собственных проектах.
## Шаг 1: Определите исходные и выходные каталоги
Сначала вам необходимо указать каталоги для исходного файла Excel и место, где вы хотите сохранить выходной HTML-файл.
```csharp
// Исходный каталог
string sourceDir = "Your Document Directory";
// Выходной каталог
string outputDir = "Your Document Directory";
```
## Шаг 2: Загрузите образец файла Excel
 Затем загрузите ваш образец файла Excel в`Workbook` объект. Вот тут-то и начинается вся магия.
```csharp
// Загрузите образец файла Excel
Workbook wb = new Workbook(sourceDir + "sampleHtmlCrossStringType.xlsx");
```
 Здесь замените`"Your Document Directory"` с фактическим путем, где находится ваш файл Excel. Эта строка считывает файл Excel в память, чтобы вы могли им манипулировать.
## Шаг 3: Укажите параметры сохранения HTML
 Теперь мы создадим экземпляр`HtmlSaveOptions`, который позволяет настроить способ преобразования файла Excel в HTML.
```csharp
// Укажите перекрестный тип HTML
HtmlSaveOptions opts = new HtmlSaveOptions();
opts.HtmlCrossStringType = HtmlCrossType.Default;
```
 На этом этапе мы установили`HtmlCrossStringType` к`HtmlCrossType.Default`, что является одним из вариантов обработки перекрестных ссылок в выходном HTML.
## Шаг 4: Измените тип креста по мере необходимости.
 Вы можете указать различные типы для`HtmlCrossStringType` на основе ваших требований. Вот различные варианты, которые вы можете использовать:
- `HtmlCrossType.Default`: Тип креста по умолчанию.
- `HtmlCrossType.MSExport`: Экспортирует HTML с поведением, аналогичным MS Excel.
- `HtmlCrossType.Cross`: Создает перекрестные ссылки.
- `HtmlCrossType.FitToCell`: Подгоняет перекрестные ссылки под размеры ячеек.
 Вы можете изменить`HtmlCrossStringType` так:
```csharp
opts.HtmlCrossStringType = HtmlCrossType.MSExport;
// или
opts.HtmlCrossStringType = HtmlCrossType.Cross;
// или
opts.HtmlCrossStringType = HtmlCrossType.FitToCell;
```
## Шаг 5: Сохраните выходной HTML-файл
 После того, как вы настроили параметры, пришло время сохранить преобразованный HTML-файл. Используйте`Save` метод на вашем`Workbook` объект:
```csharp
// Выходной HTML-код
wb.Save(outputDir + "out" + opts.HtmlCrossStringType + ".htm", opts);
```
 Здесь мы даем выходному файлу имя на основе`HtmlCrossStringType` мы установили. Таким образом, вы можете легко определить, какой тип креста использовался при конвертации.
## Шаг 6: Подтвердите успешное выполнение
Наконец, всегда полезно подтвердить, что ваша операция прошла успешно. Вы можете вывести сообщение на консоль:
```csharp
Console.WriteLine("SpecifyHtmlCrossTypeInOutputHTML executed successfully.\r\n");
```
Это даст вам знать, что процесс был завершен без ошибок.
## Заключение
И вот оно! Вы успешно указали перекрестный тип HTML для экспорта Excel в .NET с помощью Aspose.Cells. Эта функция особенно полезна, когда вам нужно сохранить определенное форматирование или ссылки в вашем HTML-выводе, гарантируя, что ваши преобразованные документы соответствуют вашим требованиям.
## Часто задаваемые вопросы
### Что такое HtmlCrossType в Aspose.Cells?  
HtmlCrossType определяет, как обрабатываются перекрестные ссылки в файле Excel во время преобразования HTML. Вы можете выбрать такие параметры, как Default, MSExport, Cross и FitToCell.
### Могу ли я использовать Aspose.Cells бесплатно?  
 Aspose.Cells предлагает бесплатную пробную версию. Вы можете загрузить ее с их сайта[веб-сайт](https://releases.aspose.com/).
### Как установить Aspose.Cells в моем проекте .NET?  
 Установить Aspose.Cells можно через диспетчер пакетов NuGet в Visual Studio, выполнив команду:`Install-Package Aspose.Cells`.
### Где я могу найти документацию по Aspose.Cells?  
 Вы можете найти подробную документацию по Aspose.Cells[здесь](https://reference.aspose.com/cells/net/).
### Что делать, если при сохранении HTML-файла возникла ошибка?  
Убедитесь, что пути к каталогам указаны правильно и у вас есть права на запись в выходной каталог. Если проблема не устранена, обратитесь за помощью на форум поддержки Aspose.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
