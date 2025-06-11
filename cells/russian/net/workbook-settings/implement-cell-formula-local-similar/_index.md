---
"description": "Узнайте, как реализовать формулу ячейки, которая похожа на локальную функциональность формулы диапазона в Aspose.Cells для .NET. Узнайте, как настраивать имена встроенных функций Excel и многое другое."
"linktitle": "Реализовать локальную формулу ячейки, аналогичную локальной формуле диапазона"
"second_title": "API обработки Excel Aspose.Cells .NET"
"title": "Реализовать локальную формулу ячейки, аналогичную локальной формуле диапазона"
"url": "/ru/net/workbook-settings/implement-cell-formula-local-similar/"
"weight": 13
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Реализовать локальную формулу ячейки, аналогичную локальной формуле диапазона

## Введение
Aspose.Cells для .NET — это мощный и гибкий API для работы с электронными таблицами, который позволяет программно создавать, изменять и преобразовывать файлы Excel. Одной из многих функций, предлагаемых Aspose.Cells, является возможность настраивать поведение встроенных функций Excel, включая возможность создания собственных локальных имен функций. В этом руководстве мы проведем вас через шаги по реализации формулы ячейки, которая похожа на локальную функциональность формулы диапазона в Aspose.Cells для .NET.
## Предпосылки
Прежде чем начать, убедитесь, что у вас есть следующее:
1. В вашей системе должна быть установлена Microsoft Visual Studio 2010 или более поздняя версия.
2. Последняя версия библиотеки Aspose.Cells for .NET, установленная в вашем проекте. Вы можете загрузить библиотеку с сайта [Страница загрузки Aspose.Cells для .NET](https://releases.aspose.com/cells/net/).
## Импортные пакеты
Для начала вам нужно импортировать необходимые пакеты в ваш проект C#. Добавьте следующие операторы using в начало вашего файла кода:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
## Шаг 1: Создание пользовательского класса настроек глобализации
Первый шаг — создать пользовательский `GlobalizationSettings` класс, который позволит вам переопределить поведение функций Excel по умолчанию. В этом примере мы изменим имена `SUM` и `AVERAGE` функции для `UserFormulaLocal_SUM` и `UserFormulaLocal_AVERAGE`, соответственно.
```csharp
class GS : GlobalizationSettings
{
    public override string GetLocalFunctionName(string standardName)
    {
        //Измените имя функции СУММ в соответствии с вашими потребностями.
        if (standardName == "SUM")
        {
            return "UserFormulaLocal_SUM";
        }
        //Измените имя функции СРЗНАЧ в соответствии с вашими потребностями.
        if (standardName == "AVERAGE")
        {
            return "UserFormulaLocal_AVERAGE";
        }
        return "";
    }
}
```
## Шаг 2: Создайте новую рабочую книгу и назначьте пользовательские параметры глобализации
Далее создайте новый экземпляр Workbook и назначьте ему пользовательское `GlobalizationSettings` класс реализации для рабочей книги `Settings.GlobalizationSettings` свойство.
```csharp
//Создать рабочую книгу
Workbook wb = new Workbook();
//Назначить класс реализации GlobalizationSettings
wb.Settings.GlobalizationSettings = new GS();
```
## Шаг 3: Получите доступ к первому рабочему листу и ячейке
Теперь давайте перейдем к первому листу в книге и к определенной ячейке на этом листе.
```csharp
//Доступ к первому рабочему листу
Worksheet ws = wb.Worksheets[0];
//Доступ к некоторым ячейкам
Cell cell = ws.Cells["C4"];
```
## Шаг 4: Назначьте формулы и распечатайте FormulaLocal
Наконец, давайте назначим `SUM` и `AVERAGE` формулы в ячейку и распечатать полученный результат `FormulaLocal` ценности.
```csharp
//Назначьте формулу SUM и распечатайте ее FormulaLocal
cell.Formula = "SUM(A1:A2)";
Console.WriteLine("Formula Local: " + cell.FormulaLocal);
//Назначьте формулу СРЗНАЧ и распечатайте ее FormulaLocal
cell.Formula = "=AVERAGE(B1:B2, B5)";
Console.WriteLine("Formula Local: " + cell.FormulaLocal);
```
## Заключение
В этом уроке вы узнали, как реализовать формулу ячейки, которая похожа на локальную функциональность формулы диапазона в Aspose.Cells для .NET. Создавая пользовательскую `GlobalizationSettings` class, вы можете переопределить поведение функций Excel по умолчанию и настроить локальные имена функций в соответствии с вашими потребностями. Это может быть особенно полезно при работе с локализованными или интернационализированными документами Excel.
## Часто задаваемые вопросы
### Какова цель `GlobalizationSettings` класс в Aspose.Cells?
The `GlobalizationSettings` Класс в Aspose.Cells позволяет настраивать поведение встроенных функций Excel, включая возможность изменять имена локальных функций.
### Могу ли я переопределить поведение функций, отличных от `SUM` и `AVERAGE`?
Да, вы можете переопределить поведение любой встроенной функции Excel, изменив ее `GetLocalFunctionName` метод в вашем собственном `GlobalizationSettings` сорт.
### Есть ли способ сбросить имена функций до значений по умолчанию?
Да, вы можете сбросить имена функций, удалив пользовательские `GlobalizationSettings` класс или путем возврата пустой строки из `GetLocalFunctionName` метод.
### Могу ли я использовать эту функцию для создания пользовательских функций в Aspose.Cells?
Нет, `GlobalizationSettings` класс предназначен для переопределения поведения встроенных функций Excel, а не для создания пользовательских функций. Если вам нужно создать пользовательские функции, вы можете использовать `UserDefinedFunction` класс в Aspose.Cells.
### Доступна ли эта функция во всех версиях Aspose.Cells для .NET?
Да, `GlobalizationSettings` класс и возможность настраивать имена функций доступны во всех версиях Aspose.Cells для .NET.


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}