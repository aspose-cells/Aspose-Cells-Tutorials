---
category: general
date: 2026-06-27
description: Сохраните книгу Excel в C#, добавив именованный диапазон. Узнайте, как
  создать определённое имя и использовать формулы с определёнными именами в Aspose.Cells.
draft: false
keywords:
- save excel workbook
- add named range
- create defined name
- named range excel
- use defined name formulas
language: ru
og_description: Сохраните книгу Excel в C# и узнайте, как добавить именованный диапазон,
  создать определённое имя и использовать формулы с определёнными именами в Aspose.Cells.
og_title: Сохранение книги Excel и добавление именованного диапазона – учебник C#
schemas:
- author: Aspose
  dateModified: '2026-06-27'
  description: Save Excel Workbook in C# while adding a named range. Learn to create
    defined name and use defined name formulas with Aspose.Cells.
  headline: Save Excel Workbook and Add Named Range – Full C# Guide
  type: TechArticle
tags:
- C#
- Aspose.Cells
- Excel Automation
title: Сохранение книги Excel и добавление именованного диапазона — Полное руководство
  по C#
url: /ru/net/excel-advanced-named-ranges/save-excel-workbook-and-add-named-range-full-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Сохранить книгу Excel и добавить именованный диапазон – Полное руководство на C#

Когда‑то вам нужно **сохранить книгу Excel** после того, как вы добавили несколько пользовательских имён на лист? Вы не одиноки. Во многих инструментах отчётности или приложениях, работающих с данными, мы создаём именованный диапазон, затем ссылаемся на него в формулах и, наконец, сохраняем изменения на диск.  

В этом руководстве мы пройдём именно через это: загрузим файл *.xlsx*, **добавим именованный диапазон**, **создадим определённое имя**, используем это имя в формуле и, наконец, **сохраним книгу Excel** с обновлениями. Без лишних слов — полностью готовый пример, который можно вставить в любой .NET‑проект.

> **Совет:** Aspose.Cells работает без необходимости установки Microsoft Office, что делает его идеальным для серверной автоматизации.

## Что вам понадобится

- .NET 6 (или любой современный .NET‑runtime)  
- NuGet‑пакет Aspose.Cells for .NET (`Install-Package Aspose.Cells`)  
- Пример `input.xlsx` (подойдёт любой файл, но убедитесь, что на листе Sheet1 есть данные в **A1**)  
- Любая удобная IDE (Visual Studio, Rider, VS Code…)

И всё. Если у вас есть всё перечисленное, можно сразу переходить к коду.

## Шаг 1: Настройка проекта

Создайте консольное приложение и подключите Aspose.Cells:

```bash
dotnet new console -n ExcelNamedRangeDemo
cd ExcelNamedRangeDemo
dotnet add package Aspose.Cells
```

Откройте `Program.cs`; вы увидите метод `Main` по умолчанию. Мы заменим его содержимое полным рабочим процессом в следующих шагах.

## Шаг 2: Загрузка книги

Загрузка книги — первое, что нужно сделать, прежде чем **добавлять именованный диапазон**. Это как открыть книгу, прежде чем начинать делать пометки на полях.

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // Step 2: Load the workbook
        string inputPath = @"YOUR_DIRECTORY\input.xlsx";
        Workbook wb = new Workbook(inputPath);
        Console.WriteLine("Workbook loaded successfully.");
```

> **Почему это важно:** Объект `Workbook` представляет всю Excel‑файл в памяти. Без него нельзя манипулировать ячейками, именами или формулами.

## Шаг 3: Создание определённого имени (добавление именованного диапазона)

Теперь мы действительно **создаём определённое имя**, которое указывает на конкретную ячейку или диапазон. В интерфейсе Excel вы бы перешли в *Formulas → Name Manager*; здесь мы делаем это программно.

```csharp
        // Step 3: Add a defined name that points to cell A1 on Sheet1
        // This name can be used in formulas throughout the workbook
        wb.Names.Add("Sales", "=Sheet1!$A$1");
        Console.WriteLine("Defined name 'Sales' added (named range Excel).");
```

> **Объяснение:** `wb.Names.Add` регистрирует *именованный диапазон* с именем **Sales**. Строка `=Sheet1!$A$1` — это формула ссылки, точно такая же, как вы бы ввели в диалоговом окне менеджера имён.

## Шаг 4: Использование определённого имени в формуле

Иметь имя удобно, но обычно хочется **использовать определённые имена в формулах** где‑то. Давайте запишем простую формулу, которая прибавит 10 к значению **Sales** и поместит результат в **B1**.

```csharp
        // Step 4: Write a formula that uses the defined name
        Worksheet sheet = wb.Worksheets["Sheet1"];
        Cell targetCell = sheet.Cells["B1"];
        targetCell.Formula = "=Sales + 10";
        Console.WriteLine("Formula '=Sales + 10' written to B1.");
```

Когда книга пересчитается, в `B1` отобразится значение из `A1` плюс десять. Это демонстрирует силу *именованного диапазона в Excel* — вы меняете базовую ссылку один раз, и все формулы обновляются автоматически.

## Шаг 5: Сохранение изменённой книги

Наконец, мы **сохраняем книгу Excel** в новый файл, чтобы изменения сохранились. Можно перезаписать оригинал или записать в новое место; здесь мы делаем оба варианта.

```csharp
        // Step 5: Save the modified workbook
        string outputPath = @"YOUR_DIRECTORY\output.xlsx";
        wb.Save(outputPath);
        Console.WriteLine($"Workbook saved as '{outputPath}'.");
    }
}
```

Запуск программы выдаст вывод в консоль, похожий на:

```
Workbook loaded successfully.
Defined name 'Sales' added (named range Excel).
Formula '=Sales + 10' written to B1.
Workbook saved as 'YOUR_DIRECTORY\output.xlsx'.
```

Откройте `output.xlsx`, и вы увидите, что **B1** теперь содержит `=Sales + 10`, а **A1** остаётся без изменений. Имя **Sales** появится в *Formulas → Name Manager*.

## Пограничные случаи и часто задаваемые вопросы

| Вопрос | Ответ |
|----------|--------|
| **Что делать, если имя листа содержит пробелы?** | Заключите его в одинарные кавычки: `= 'My Sheet'!$A$1`. |
| **Можно ли привязать имя к диапазону из нескольких ячеек?** | Конечно — используйте `=Sheet1!$A$1:$A$5` при вызове `wb.Names.Add`. |
| **Нужно ли пересчитывать вручную?** | Aspose.Cells пересчитывает автоматически при чтении значения ячейки. Если нужен полный пересчёт, вызовите `wb.CalculateFormula()`. |
| **Что происходит с уже существующими именами?** | `wb.Names.Add` бросит исключение, если имя уже существует. Используйте `wb.Names["Sales"]?.RefersTo = "...";` для обновления. |

## Полный рабочий пример (все шаги вместе)

Ниже полностью готовая к копированию программа. Замените `YOUR_DIRECTORY` на реальный путь к папке на вашем компьютере.

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // Load the workbook
        string inputPath = @"YOUR_DIRECTORY\input.xlsx";
        Workbook wb = new Workbook(inputPath);
        Console.WriteLine("Workbook loaded successfully.");

        // Add a defined name (named range) that points to cell A1 on Sheet1
        wb.Names.Add("Sales", "=Sheet1!$A$1");
        Console.WriteLine("Defined name 'Sales' added (named range Excel).");

        // Write a formula that uses the defined name
        Worksheet sheet = wb.Worksheets["Sheet1"];
        Cell targetCell = sheet.Cells["B1"];
        targetCell.Formula = "=Sales + 10";
        Console.WriteLine("Formula '=Sales + 10' written to B1.");

        // Save the modified workbook
        string outputPath = @"YOUR_DIRECTORY\output.xlsx";
        wb.Save(outputPath);
        Console.WriteLine($"Workbook saved as '{outputPath}'.");
    }
}
```

**Ожидаемый результат:**  

- `output.xlsx` содержит новое имя **Sales**, указывающее на `Sheet1!A1`.  
- Ячейка **B1** отображает значение **A1** плюс `10`.  
- Файл полностью совместим с Excel, Google Sheets и любой библиотекой, понимающей именованные диапазоны.

## Заключение

Теперь вы знаете, как **сохранить книгу Excel**, **добавить именованный диапазон**, **создать определённое имя** и **использовать формулы с определёнными именами** с помощью Aspose.Cells в C#. Шаги просты: загрузить, назвать, сослаться и сохранить.  

Далее вы можете расширить процесс:  

- Создавать динамические диапазоны с функциями `OFFSET`.  
- Применять одно и то же имя на нескольких листах (`Scope = Worksheet`).  
- Генерировать тысячи именованных диапазонов для сложных финансовых моделей.

Попробуйте, измените ссылку или используйте имя в сводной таблице — возможности автоматизации практически безграничны.

---

![Save Excel Workbook flowchart](excel-workflow.png){: .align-center alt="Схема сохранения книги Excel"}

*Готовы автоматизировать свои Excel‑отчёты? Оставьте комментарий, поделитесь своими доработками или форкните репозиторий на GitHub. Приятного кодинга!*


## Что изучать дальше?


Следующие руководства охватывают тесно связанные темы, которые развивают техники, продемонстрированные в этом руководстве. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы в ваших проектах.

- [Create Save Excel Workbook Aspose Cells Dotnet](/cells/english/net/workbook-operations/create-save-excel-workbook-aspose-cells-dotnet/)
- [How to Create and Save an Excel Workbook as ODS Using Aspose.Cells for .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)
- [Create Save Excel Workbook Pdf Aspnet Aspose Cells](/cells/english/net/workbook-operations/create-save-excel-workbook-pdf-aspnet-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}