---
category: general
date: 2026-02-21
description: Узнайте, как сделать текст в TextBox жирным, изменить размер шрифта TextBox
  и загрузить книгу Excel в C# с помощью Aspose.Cells в полном, исполняемом примере.
draft: false
keywords:
- make textbox text bold
- change textbox font size
- load excel workbook c#
- format excel shape text
language: ru
og_description: Сделайте текст в TextBox жирным в файле Excel с помощью C#. Этот учебник
  также показывает, как изменить размер шрифта TextBox и загрузить книгу Excel в C#
  с использованием Aspose.Cells.
og_title: Сделать текст в TextBox жирным в Excel с помощью C# – Полное руководство
tags:
- C#
- Aspose.Cells
- Excel automation
title: Сделать текст в TextBox жирным в Excel с помощью C# — пошаговое руководство
url: /ru/net/excel-shape-text-modifications/make-textbox-text-bold-in-excel-with-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Сделать текст в TextBox жирным в Excel с помощью C# – Пошаговое руководство

Нужно **сделать текст в TextBox жирным** в файле Excel с помощью C#? В этом руководстве мы покажем, как *загрузить книгу Excel*, **изменить размер шрифта TextBox** и отформатировать текст фигуры с помощью Aspose.Cells.  
Если вы когда‑нибудь смотрели на скучную таблицу и думали «мой TextBox должен выделяться», вы попали по адресу.

Мы пройдемся по каждой строке кода, объясним, почему каждый вызов важен, и даже расскажем, что делать, если на листе нет никаких TextBox‑ов. К концу у вас будет переиспользуемый фрагмент, который можно вставить в любой .NET‑проект — без загадочных ссылок «см. документацию».

## Что понадобится

- **Aspose.Cells for .NET** (бесплатная пробная версия или лицензированная) – API, которое мы используем для работы с фигурами Excel.  
- .NET 6 или новее (код также работает с .NET Framework 4.7+).  
- Простой файл Excel (`input.xlsx`), который уже содержит хотя бы один TextBox на первом листе.  

Вот и всё. Никаких дополнительных пакетов NuGet, без COM‑interop, просто чистый C#.

## Сделать текст в TextBox жирным – загрузить книгу и получить доступ к фигуре

Первый шаг — открыть книгу и получить нужный TextBox для редактирования.  
Мы также делаем быструю проверку безопасности, чтобы код не упал, если лист пуст.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Load the workbook (load excel workbook c#)
        var workbookPath = @"YOUR_DIRECTORY\input.xlsx";
        Workbook workbook = new Workbook(workbookPath);

        // Step 2: Get the first worksheet
        Worksheet worksheet = workbook.Worksheets[0];

        // Verify that at least one TextBox exists
        if (worksheet.TextBoxes.Count == 0)
        {
            Console.WriteLine("No TextBoxes found on the first sheet.");
            return;
        }

        // Step 3: Access the first TextBox shape
        Shape textBox = worksheet.TextBoxes[0];

        // From here on we can format the shape's text
```

**Почему это важно:**  
*Загрузка книги* дает нам объект `Workbook`, представляющий весь файл в памяти. Доступ к `Worksheets[0]` безопасен, потому что у каждого файла Excel как минимум один лист. Защитное условие (`if (worksheet.TextBoxes.Count == 0)`) предотвращает `IndexOutOfRangeException` — распространённую ошибку при автоматизации существующих файлов.

## Изменить размер шрифта TextBox

Прежде чем делать текст жирным, убедимся, что размер именно тот, который вам нужен.  
Изменить размер так же просто, как изменить свойство `Font.Size`.

```csharp
        // Step 4: Set the font name (optional but often useful)
        textBox.Font.Name = "Calibri";

        // Step 5: Change the font size (change textbox font size)
        textBox.Font.Size = 12; // 12 points is a comfortable default
```

**Полезный совет:**  
Если нужен динамический размер, основанный на вводе пользователя, просто замените `12` переменной. Объект `Font` общий для всей фигуры, поэтому изменение размера сразу влияет на каждый символ внутри TextBox.

## Сделать текст в TextBox жирным – основное действие

Теперь к основной функции: сделать текст жирным.  
Флаг `IsBold` меняет толщину шрифта, не изменяя другие стили.

```csharp
        // Step 6: Make the text bold (make textbox text bold)
        textBox.Font.IsBold = true;
```

**Что происходит «под капотом»?**  
Aspose.Cells хранит форматирование текста в объекте `Font`, привязанном к фигуре. Установка `IsBold = true` обновляет базовый XML (`<b>1</b>`), который Excel читает при отрисовке листа. Это **неразрушающая** операция — если позже установить `IsBold = false`, текст вернётся к обычному весу.

## Сохранить изменённую книгу

После завершения форматирования мы записываем изменения обратно на диск.  
Можно перезаписать оригинальный файл или, как показано здесь, создать новый, чтобы оставить исходный нетронутым.

```csharp
        // Step 7: Save the modified workbook
        var outputPath = @"YOUR_DIRECTORY\output.xlsx";
        workbook.Save(outputPath);

        Console.WriteLine($"Workbook saved. TextBox is now bold and 12pt Calibri in '{outputPath}'.");
    }
}
```

**Ожидаемый результат:**  
Откройте `output.xlsx` в Excel. Первый TextBox на первом листе должен отображать текст **Calibri 12 pt, жирный**. Другие фигуры не затронуты.

## Форматировать текст фигуры Excel – дополнительные варианты стилизации (необязательно)

Хотя основной целью является **сделать текст в TextBox жирным**, вы также можете захотеть:

| Опция | Code Snippet | Когда использовать |
|--------|--------------|---------------------|
| Курсив | `textBox.Font.IsItalic = true;` | Для выделения подзаголовка |
| Цвет текста | `textBox.Font.Color = System.Drawing.Color.DarkBlue;` | Цвета бренда |
| Выравнивание | `textBox.AlignmentHorizontal = TextAlignmentType.Center;` | Центрированные заголовки |
| Несколько TextBox‑ов | Loop through `worksheet.TextBoxes` | Пакетное форматирование |

```csharp
// Example: Apply a blue color and center alignment to all textboxes
foreach (Shape tb in worksheet.TextBoxes)
{
    tb.Font.Color = System.Drawing.Color.Blue;
    tb.AlignmentHorizontal = TextAlignmentType.Center;
}
```

Эти дополнительные настройки показывают, как *format excel shape text* можно расширить за пределы простого жирного текста.

## Пограничные случаи и распространённые подводные камни

1. **Нет TextBox‑ов на листе** – Добавленное нами условие (`if (worksheet.TextBoxes.Count == 0)`) корректно завершает работу и информирует пользователя.  
2. **Скрытые листы** – Скрытые листы всё равно доступны через коллекцию `Worksheets`; просто убедитесь, что ссылаетесь на правильный индекс.  
3. **Большие файлы** – Загрузка огромной книги может потреблять много памяти. Рассмотрите возможность использования `Workbook.LoadOptions` для загрузки только необходимых частей.  
4. **Разные версии Excel** – Aspose.Cells работает с `.xls`, `.xlsx` и даже `.xlsb`. Один и тот же код работает во всех версиях, но более старые версии Excel могут игнорировать некоторые новые возможности шрифтов.

## Полный рабочий пример (готовый к копированию и вставке)

```csharp
using System;
using Aspose.Cells;

class MakeTextboxBoldDemo
{
    static void Main()
    {
        // Load the workbook (load excel workbook c#)
        var inputFile = @"YOUR_DIRECTORY\input.xlsx";
        Workbook workbook = new Workbook(inputFile);

        // Get the first worksheet
        Worksheet sheet = workbook.Worksheets[0];

        // Ensure a textbox exists
        if (sheet.TextBoxes.Count == 0)
        {
            Console.WriteLine("No textbox found on the first sheet.");
            return;
        }

        // Access the first textbox
        Shape txtBox = sheet.TextBoxes[0];

        // Set font name and size (change textbox font size)
        txtBox.Font.Name = "Calibri";
        txtBox.Font.Size = 12;

        // Make the text bold (make textbox text bold)
        txtBox.Font.IsBold = true;

        // Optional: extra styling (format excel shape text)
        txtBox.Font.Color = System.Drawing.Color.DarkGreen;
        txtBox.AlignmentHorizontal = TextAlignmentType.Center;

        // Save the result
        var outputFile = @"YOUR_DIRECTORY\output.xlsx";
        workbook.Save(outputFile);

        Console.WriteLine($"Saved: {outputFile}");
    }
}
```

Запустите программу, откройте сгенерированный `output.xlsx`, и вы увидите жирный текст Calibri 12 pt внутри TextBox. Просто, не правда ли?

## Заключение

Теперь вы знаете, **как сделать текст в TextBox жирным** в книге Excel с помощью C#, как **изменить размер шрифта TextBox**, а также основы **загрузки книги Excel C#** с помощью Aspose.Cells. Приведённый выше полный пример готов к использованию в любом проекте, и вы также увидели способы **форматировать текст фигуры Excel** для более богатого оформления.

Что дальше? Попробуйте пройтись по каждому листу, чтобы сделать жирными все TextBox‑ы, или объедините это с генерацией контента на основе данных — возможно, заполняя TextBox значениями из базы данных. Принципы остаются теми же, а код остаётся чистым.

Есть свой вариант, которым хотите поделиться, или столкнулись с неожиданной ошибкой? Оставьте комментарий, и давайте продолжать обсуждение. Счастливого кодинга! 

![make textbox text bold in Excel using C#](/images/make-textbox-text-bold-csharp.png)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}