---
category: general
date: 2026-03-30
description: Узнайте, как сохранять XLSB в C#, добавляя пользовательское свойство,
  считывать его обратно и освоить сохранение книги в формате XLSB с помощью Aspose.Cells.
  Полный код включён.
draft: false
keywords:
- how to save xlsb
- add custom property
- how to add property
- how to read property
- save workbook as xlsb
language: ru
og_description: Как сохранить XLSB в C#? Этот учебник показывает, как добавить пользовательское
  свойство, прочитать его обратно и сохранить книгу в формате XLSB с помощью Aspose.Cells.
og_title: Как сохранить XLSB с пользовательскими свойствами в C# – Полное руководство
tags:
- Aspose.Cells
- C#
- Excel Automation
title: Как сохранить XLSB с пользовательскими свойствами в C# — пошаговое руководство
url: /ru/net/document-properties/how-to-save-xlsb-with-custom-properties-in-c-step-by-step-gu/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как сохранить XLSB с пользовательскими свойствами в C# – Пошаговое руководство

Когда‑нибудь задумывались **как сохранить XLSB**, сохранив при этом дополнительные метаданные, привязанные к листу? Вы не одиноки. Во многих корпоративных сценариях нужен бинарный файл Excel, который всё ещё содержит ваши собственные пары ключ/значение — например, идентификатор контракта, флаг обработки или тег версии.  

Хорошая новость в том, что Aspose.Cells делает это проще простого. В этом руководстве вы увидите, как добавить пользовательское свойство, сохранить его и затем прочитать, при этом **сохраняя книгу в формате XLSB**. Никаких расплывчатых ссылок, только полностью готовый к запуску пример, который вы можете сразу добавить в свой проект.

## Что вы получите в результате

- Свежий файл `.xlsb`, созданный с нуля.  
- Возможность **добавлять пользовательские свойства** к листу.  
- Код, демонстрирующий **как читать свойство** после перезагрузки файла.  
- Советы по подводным камням, которые могут возникнуть при **сохранении книги как XLSB**.  

> **Prerequisites:** .NET 6+ (или .NET Framework 4.6+), Visual Studio (или любой IDE для C#) и библиотека Aspose.Cells for .NET, установленная через NuGet. Больше ничего не требуется.

---

## Шаг 1: Настройте проект и создайте новую книгу  

Сначала получим чистый объект книги.

```csharp
using Aspose.Cells;
using System;

// Initialize a new workbook; this will be an in‑memory Excel file.
Workbook workbook = new Workbook();

// Grab the first worksheet (index 0) – it’s created automatically.
Worksheet worksheet = workbook.Worksheets[0];
```

*Почему это важно:* `Workbook` — точка входа для любой операции в Aspose.Cells. Начав с полностью нового экземпляра, вы избегаете скрытого состояния, которое могло бы испортить ваши пользовательские метаданные позже.

---

## Шаг 2: **Добавить пользовательское свойство** к листу  

Теперь прикрепим пару ключ/значение, которая существует только на этом листе.

```csharp
// Add a user‑defined property called "MyProperty" with the value "CustomValue".
worksheet.CustomProperties.Add("MyProperty", "CustomValue");
```

> **Pro tip:** Имена свойств чувствительны к регистру. Если позже попытаться получить `"myproperty"`, вы получите `KeyNotFoundException`. Придерживайтесь единого стиля именования — camelCase или PascalCase — с самого начала.

---

## Шаг 3: **Сохранить книгу как XLSB** – Сериализация свойства  

Магия происходит, когда вы записываете книгу в бинарный формат XLSB.

```csharp
// Define the output path. Adjust the folder to something writable on your machine.
string outputPath = @"C:\Temp\WithCustomProp.xlsb";

// Save the workbook; the custom property travels with the file.
workbook.Save(outputPath, SaveFormat.Xlsb);
```

*Что вы на самом деле делаете:* Перечисление `SaveFormat.Xlsb` указывает Aspose.Cells вывести бинарный файл Excel (быстрее открывается, меньше по размеру). Все пользовательские свойства уровня листа сериализуются автоматически — дополнительных действий не требуется.

---

## Шаг 4: Перезагрузите файл и **как прочитать свойство**  

Давайте проверим, что свойство выжило после кругового перехода.

```csharp
// Load the just‑saved XLSB file back into memory.
Workbook reloadedWorkbook = new Workbook(outputPath);

// Access the same worksheet (index 0) and fetch the property value.
string customValue = reloadedWorkbook.Worksheets[0]
    .CustomProperties["MyProperty"].Value.ToString();
```

Если всё прошло гладко, `customValue` теперь содержит `"CustomValue"`.

---

## Шаг 5: Проверка результата – Быстрый вывод в консоль  

Небольшая проверка помогает во время разработки.

```csharp
Console.WriteLine($"Custom property value: {customValue}");
```

Запуск программы должен вывести:

```
Custom property value: CustomValue
```

Появление этой строки означает, что вы успешно освоили **как сохранить XLSB**, **добавить пользовательское свойство** и **как прочитать свойство** — всё в одном аккуратном процессе.

---

## Полный рабочий пример (готов к копированию)

Ниже представлен весь код программы. Вставьте его в новый консольный проект, нажмите **F5** и наблюдайте, как консоль подтверждает значение свойства.

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // 1️⃣ Create a new workbook and get its first sheet
        // -------------------------------------------------
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // -------------------------------------------------
        // 2️⃣ Add a custom property (key/value) to the sheet
        // -------------------------------------------------
        worksheet.CustomProperties.Add("MyProperty", "CustomValue");

        // -------------------------------------------------
        // 3️⃣ Save the workbook as XLSB – the property is kept
        // -------------------------------------------------
        string outputPath = @"C:\Temp\WithCustomProp.xlsb";
        workbook.Save(outputPath, SaveFormat.Xlsb);

        // -------------------------------------------------
        // 4️⃣ Reload the saved file to demonstrate persistence
        // -------------------------------------------------
        Workbook reloaded = new Workbook(outputPath);

        // -------------------------------------------------
        // 5️⃣ Retrieve the custom property's value
        // -------------------------------------------------
        string customValue = reloaded.Worksheets[0]
            .CustomProperties["MyProperty"].Value.ToString();

        // -------------------------------------------------
        // 6️⃣ Display the retrieved value (optional)
        // -------------------------------------------------
        Console.WriteLine($"Custom property value: {customValue}");
    }
}
```

> **Remember:** Измените `outputPath` на папку, в которую у вас есть права записи. Если вы работаете в Linux/macOS, используйте путь вроде `"/tmp/WithCustomProp.xlsb"`.

---

## Часто задаваемые вопросы и особые случаи  

### Что делать, если свойство уже существует?  
Вызов `Add` с уже существующим ключом бросает `ArgumentException`. Используйте `ContainsKey` или оберните вызов в `try/catch`, если не уверены.

```csharp
if (!worksheet.CustomProperties.ContainsKey("MyProperty"))
{
    worksheet.CustomProperties.Add("MyProperty", "AnotherValue");
}
```

### Можно ли хранить значения не‑строкового типа?  
Конечно. Свойство `Value` принимает любой `object`. Для чисел, дат или логических значений просто передайте соответствующий тип — Aspose.Cells выполнит преобразование при чтении.

### Выживает ли свойство при конвертации в XLSX?  
Да. Пользовательские свойства являются частью XML‑представления листа, поэтому они сохраняются при переходе между форматами XLSX, XLS и XLSB.

### Как **добавить свойство** к нескольким листам?  
Пройдитесь по коллекции `Worksheets` и выполните тот же вызов `CustomProperties.Add` для каждого нужного листа.

```csharp
foreach (Worksheet ws in workbook.Worksheets)
{
    ws.CustomProperties.Add("ExportedBy", "MyApp");
}
```

### Совет по производительности при **сохранении книг как XLSB** массово  
Если вы генерируете сотни файлов, переиспользуйте один экземпляр `Workbook` и вызывайте `Clear` после каждого сохранения, чтобы освободить память. Кроме того, установите `Workbook.Settings.CalculateFormulaOnOpen = false`, если вам не требуется вычислять формулы при загрузке.

---

## Заключение  

Теперь вы знаете **как сохранить XLSB** в C# с внедрением и последующим извлечением пользовательского свойства с помощью Aspose.Cells. Полное решение — создание книги, добавление свойства, сохранение её через **save workbook as XLSB**, повторная загрузка и чтение значения — укладывается в менее чем 50 строк кода.  

Дальше вы можете исследовать:

- Добавление нескольких пользовательских свойств на лист.  
- Хранение сложных объектов в виде JSON‑строк.  
- Шифрование файла XLSB для дополнительной безопасности.  

Попробуйте эти идеи, и вы быстро станете главным специалистом по автоматизации Excel в своей команде. Есть вопросы или сложный сценарий? Оставляйте комментарий ниже, и удачной разработки!  

![Как сохранить XLSB с пользовательским свойством](/images/how-to-save-xlsb.png)   <!-- Image alt includes primary keyword -->

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}