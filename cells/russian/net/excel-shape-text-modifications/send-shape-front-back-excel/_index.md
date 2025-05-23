---
"description": "Узнайте, как отправлять фигуры на передний или задний план в Excel с помощью Aspose.Cells для .NET. Это руководство содержит пошаговое руководство с советами."
"linktitle": "Отправить форму спереди или сзади в Excel"
"second_title": "API обработки Excel Aspose.Cells .NET"
"title": "Отправить форму спереди или сзади в Excel"
"url": "/ru/net/excel-shape-text-modifications/send-shape-front-back-excel/"
"weight": 16
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Отправить форму спереди или сзади в Excel

## Введение
При работе с файлами Excel вам может потребоваться больше контроля над визуальными элементами в вашей таблице. Формы, такие как изображения и графика, могут улучшить представление ваших данных. Но что происходит, когда эти формы накладываются друг на друга или их нужно переупорядочить? Вот где Aspose.Cells for .NET блистает. В этом уроке мы проведем вас через шаги по управлению формами на листе Excel, в частности, отправке форм на передний или задний план других форм. Если вы готовы улучшить свою игру в Excel, давайте сразу же приступим!
## Предпосылки
Прежде чем начать, вам необходимо подготовить несколько вещей:
1. Установка библиотеки Aspose.Cells: Убедитесь, что у вас установлена библиотека Aspose.Cells для .NET. Вы можете найти ее [здесь](https://releases.aspose.com/cells/net/).
2. Среда разработки: убедитесь, что у вас настроена среда разработки с поддержкой .NET, например Visual Studio.
3. Базовые знания C#: знакомство с программированием на C# поможет вам лучше понимать фрагменты кода.
Хорошо, вы отметили все пункты в списке предварительных условий? Отлично! Давайте перейдем к самой интересной части — написанию кода!
## Импортные пакеты
Прежде чем погрузиться в фактическое кодирование, давайте импортируем необходимые пакеты. Просто добавьте следующую директиву using в начало вашего файла C#:
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System;
```
Эти пространства имен имеют решающее значение, поскольку они содержат классы и методы, которые мы будем использовать для управления файлами и фигурами Excel.
## Шаг 1: Определите пути к файлам
На этом первом шаге нам нужно установить исходный и выходной каталоги. Это то, где находится ваш файл Excel и где вы хотите сохранить измененный файл.
```csharp
//Исходный каталог
string sourceDir = "Your Document Directory";
//Выходной каталог
string outputDir = "Your Document Directory";
```
Заменять `"Your Document Directory"` с фактическим путем хранения ваших файлов Excel.
## Шаг 2: Загрузите рабочую книгу
Теперь, когда у нас настроены каталоги, давайте загрузим рабочую книгу (файл Excel), содержащую фигуры, которыми мы хотим управлять.
```csharp
//Загрузить исходный файл Excel
Workbook wb = new Workbook(sourceDir + "sampleToFrontOrBack.xlsx");
```
Эта строка кода инициализирует новый `Workbook` объект, загружающий указанный файл Excel в память, чтобы мы могли с ним работать.
## Шаг 3: Доступ к рабочему листу 
Далее нам нужно получить доступ к конкретному рабочему листу, где находятся наши фигуры. Для этого примера мы будем использовать первый рабочий лист.
```csharp
//Доступ к первому рабочему листу
Worksheet ws = wb.Worksheets[0];
```
Ссылаясь `Worksheets[0]`, мы ориентируемся на первый лист нашей рабочей книги. Если ваши фигуры находятся на другом листе, измените индекс соответствующим образом.
## Шаг 4: Доступ к фигурам
Имея доступ к рабочему листу, давайте выберем интересующие нас фигуры. В этом примере мы получим доступ к первой и четвертой фигурам.
```csharp
//Доступ к первой и четвертой форме
Shape sh1 = ws.Shapes[0];
Shape sh4 = ws.Shapes[3];
```
Эти линии получают определенные фигуры из рабочего листа на основе их индекса.
## Шаг 5: Распечатайте Z-положение фигур
Прежде чем перемещать какие-либо фигуры, давайте распечатаем их текущую позицию Z-Order. Это поможет нам отслеживать их позиционирование, прежде чем вносить изменения.
```csharp
//Распечатать Z-положение фигуры
Console.WriteLine("Z-Order Shape 1: " + sh1.ZOrderPosition);
```
Позвонив по телефону `ZOrderPosition`, мы можем увидеть, где каждая фигура находится в порядке рисования.
## Шаг 6: Отправьте первую фигуру на передний план
Теперь пришло время действовать! Давайте отправим первую фигуру в начало Z-порядка.
```csharp
//Отправить эту форму на передний план
sh1.ToFrontOrBack(2);
```
Проходя мимо `2` к `ToFrontOrBack`, мы даем указание Aspose.Cells вывести эту фигуру на передний план. 
## Шаг 7: Распечатайте Z-положение второй фигуры
Прежде чем отправить вторую фигуру на задний план, давайте проверим, где она расположена.
```csharp
//Распечатать Z-положение фигуры
Console.WriteLine("Z-Order Shape 4: " + sh4.ZOrderPosition);
```
Это дает нам представление о положении четвертой фигуры, прежде чем мы внесем какие-либо изменения.
## Шаг 8: Отправьте четвертую фигуру на задний план.
Наконец, мы отправим четвертую фигуру в конец стека Z-порядка.
```csharp
//Отправить эту форму на задний план
sh4.ToFrontOrBack(-2);
```
С использованием `-2` поскольку параметр переносит фигуру в конец стека, гарантируя, что она не будет мешать другим фигурам или тексту.
## Шаг 9: Сохраните рабочую книгу 
Последний шаг — сохранить рабочую книгу с вновь размещенными фигурами.
```csharp
//Сохраните выходной файл Excel.
wb.Save(outputDir + "outputToFrontOrBack.xlsx");
```
Эта команда сохраняет измененную книгу в указанном выходном каталоге.
## Шаг 10: Подтверждающее сообщение
Наконец, давайте предоставим простое подтверждение, которое даст нам знать, что наша задача выполнена успешно.
```csharp
Console.WriteLine("SendShapeFrontOrBackInWorksheet executed successfully.\r\n");
```
И на этом код нашего урока завершен!
## Заключение
Манипулирование фигурами в Excel с помощью Aspose.Cells for .NET не только простое, но и мощное. Следуя этому руководству, вы теперь сможете легко отправлять фигуры на передний или задний план, что позволит лучше контролировать ваши презентации Excel. Имея в своем распоряжении эти инструменты, вы готовы улучшить визуальную привлекательность ваших электронных таблиц.
## Часто задаваемые вопросы
### Какой язык программирования мне нужен для Aspose.Cells?  
Для работы с Aspose.Cells вам необходимо использовать C# или любой язык, поддерживаемый .NET.
### Могу ли я попробовать Aspose.Cells бесплатно?  
Да, вы можете начать с бесплатной пробной версии Aspose.Cells. [здесь](https://releases.aspose.com/).
### Какими фигурами можно манипулировать в Excel?  
Вы можете манипулировать различными фигурами, такими как прямоугольники, круги, линии и изображения.
### Как я могу получить поддержку по Aspose.Cells?  
Вы можете посетить форум сообщества для получения поддержки или вопросов. [здесь](https://forum.aspose.com/c/cells/9).
### Существует ли временная лицензия для Aspose.Cells?  
Да, вы можете запросить временную лицензию. [здесь](https://purchase.aspose.com/temporary-license/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}