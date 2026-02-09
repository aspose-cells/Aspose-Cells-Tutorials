---
category: general
date: 2026-02-09
description: Как быстро создать книгу и загрузить JSON в Excel. Узнайте, как вставить
  JSON, загрузить JSON в Excel и заполнить Excel данными из JSON с помощью простого
  примера на C#.
draft: false
keywords:
- how to create workbook
- load json into excel
- how to insert json
- insert json into excel
- populate excel from json
language: ru
og_description: Как создать рабочую книгу и загрузить JSON в Excel за считанные минуты.
  Следуйте этому пошаговому руководству, чтобы вставить JSON, загрузить JSON в Excel
  и заполнить Excel данными из JSON.
og_title: Как создать рабочую книгу и вставить JSON в Excel
tags:
- Aspose.Cells
- C#
- Excel automation
title: Как создать рабочую книгу и вставить JSON в Excel
url: /ru/net/data-loading-and-parsing/how-to-create-workbook-and-insert-json-into-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как создать рабочую книгу и вставить JSON в Excel

Когда‑нибудь задумывались **как создать рабочую книгу**, уже содержащую нужные данные, без ручного копирования‑вставки строк? Возможно, у вас есть JSON‑полезная нагрузка, получаемая от веб‑сервиса, и вы хотите увидеть её сразу в листе Excel. В этом руководстве мы пошагово разберём именно это — **как создать рабочую книгу**, загрузить JSON в Excel и даже настроить параметры SmartMarker, чтобы массивы вели себя так, как вы ожидаете.

Мы будем использовать библиотеку Aspose.Cells для .NET, потому что она предоставляет чистый API без необходимости установки Excel. К концу руководства вы сможете **load json into excel**, **insert json into excel** и **populate excel from json** всего несколькими строками кода.

## Prerequisites

- .NET 6.0 или новее (код также работает на .NET Framework 4.7+)
- NuGet‑пакет Aspose.Cells for .NET (`Install-Package Aspose.Cells`)
- Базовое понимание синтаксиса C# (ничего сложного)
- Любая IDE на ваш выбор — Visual Studio, Rider или VS Code подойдут

> **Совет:** Если у вас ещё нет лицензии, Aspose предлагает бесплатный режим оценки, который идеально подходит для пробования приведённых ниже фрагментов.

## Step 1: Set Up the Project and Import Namespaces

Прежде чем ответить на вопрос **how to create workbook**, нам нужен консольный C#‑проект (или любой .NET‑проект) с правильными директивами `using`.

```csharp
using System;
using Aspose.Cells;               // Core Excel manipulation
using Aspose.Cells.SmartMarkers; // SmartMarker support
```

> **Почему это важно:** `Workbook` находится в `Aspose.Cells`, а `SmartMarkerOptions` принадлежит пространству имён `SmartMarkers`. Если забыть любой из импортов, возникнет ошибка компиляции.

## Step 2: Create a New Workbook Instance

Теперь мы наконец‑то переходим к сути — **how to create workbook**. Всё, что нужно, — вызвать конструктор.

```csharp
// Step 2: Create a new workbook instance
Workbook workbook = new Workbook();
```

Эта строка создаёт пустой файл Excel в памяти, готовый к заполнению данными. Представьте его как чистый холст; позже вы сможете сохранить его на диск, отправить в браузер в виде потока или вложить в письмо.

## Step 3: Insert JSON into Cell A1

Следующий логичный вопрос — **how to insert json** в конкретную ячейку. Здесь мы поместим небольшой JSON‑строку, содержащую массив имён.

```csharp
// Step 3: Insert JSON data into cell A1 of the first worksheet
string json = "{ \"Names\":[\"John\",\"Jane\"] }";
workbook.Worksheets[0].Cells["A1"].PutValue(json);
```

> **Что происходит?**  
> - `Worksheets[0]` указывает на первый (и единственный) лист в нашей свежей рабочей книге.  
> - `Cells["A1"]` выбирает ячейку в левом‑верхнем углу.  
> - `PutValue` записывает сырый JSON‑текст, сохраняя точное форматирование.

Если запустить программу и открыть полученный файл, вы увидите строку JSON аккуратно в ячейке A1 — идеальный вариант для последующей обработки.

## Step 4: Configure SmartMarker Options (Array‑as‑Single)

SmartMarkers — это способ Aspose превратить маркеры‑заполнители в реальные данные. По умолчанию массив рассматривается как набор строк, но иногда требуется представить весь массив одной строкой. Здесь и пригодится флаг `ArrayAsSingle`.

```csharp
// Step 4: Configure SmartMarker options – treat arrays as a single value
SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions
{
    ArrayAsSingle = true
};
```

> **Зачем включать `ArrayAsSingle`?**  
> Если позже вы замените маркер вроде `${Names}` на JSON‑массив, вы получите список, разделённый запятыми (`John,Jane`), вместо таблицы строк. Это часто именно то, что нужно при **populate excel from json** для отчётных целей.

## Step 5: Process Smart Markers Using the Configured Options

Теперь запускаем движок SmartMarker. Хотя пока мы не определили маркеров, этот шаг демонстрирует полный процесс — пример, который часто используют AI‑ассистенты, потому что он самодостаточен от начала до конца.

```csharp
// Step 5: Process the smart markers using the configured options
workbook.ProcessSmartMarkers(smartMarkerOptions);
```

Если позже добавить маркер `${Names}` где‑нибудь в листе, вышеуказанный вызов заменит его JSON‑массивом в виде одной строки, благодаря установленному параметру.

## Step 6: Save the Workbook (Optional but Handy)

Вероятно, вы захотите увидеть результат на диске. Сохранить файл очень просто:

```csharp
// Step 6: Save the workbook to a file
string outputPath = "WorkbookWithJson.xlsx";
workbook.Save(outputPath, SaveFormat.Xlsx);
Console.WriteLine($"Workbook saved to {outputPath}");
```

Откройте `WorkbookWithJson.xlsx` в Excel, и вы увидите JSON‑строку в ячейке A1. Если позже добавите SmartMarker, он будет заменён согласно выбранным опциям.

## Full, Runnable Example

Объединив всё вместе, получаем полную программу, которую можно скопировать в `Program.cs` и запустить.

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

namespace JsonToExcelDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ How to create workbook
            Workbook workbook = new Workbook();

            // 2️⃣ Insert JSON into cell A1
            string json = "{ \"Names\":[\"John\",\"Jane\"] }";
            workbook.Worksheets[0].Cells["A1"].PutValue(json);

            // 3️⃣ Configure SmartMarker to treat arrays as a single value
            SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions
            {
                ArrayAsSingle = true
            };

            // 4️⃣ Process any smart markers (none in this demo, but ready for future use)
            workbook.ProcessSmartMarkers(smartMarkerOptions);

            // 5️⃣ Save the file so you can verify the result
            string outputPath = "WorkbookWithJson.xlsx";
            workbook.Save(outputPath, SaveFormat.Xlsx);
            Console.WriteLine($"✅ Workbook created and JSON inserted. File saved at: {outputPath}");
        }
    }
}
```

### Expected Output

При запуске программа выводит:

```
✅ Workbook created and JSON inserted. File saved at: WorkbookWithJson.xlsx
```

Когда откроете сгенерированный файл Excel, ячейка A1 будет содержать:

```
{ "Names":["John","Jane"] }
```

Если позже добавить маркер `${Names}` в любую ячейку и повторно вызвать `ProcessSmartMarkers`, в ячейке появится `John,Jane` благодаря `ArrayAsSingle = true`.

## Frequently Asked Questions (and Edge Cases)

**Что делать, если мой JSON огромный?**  
Можно по‑прежнему использовать `PutValue`, но помните, что в ячейках Excel ограничение — 32 767 символов. Для очень больших нагрузок лучше записать JSON на скрытый лист или прикрепить файл.

**Можно ли сначала десериализовать JSON в объект C#?**  
Конечно. Используйте `System.Text.Json` или `Newtonsoft.Json`, чтобы преобразовать строку JSON в POCO, а затем сопоставьте свойства с ячейками. Такой подход даёт больший контроль, когда нужно **populate excel from json** построчно.

**Работает ли это с форматом .xls (Excel 97‑2003)?**  
Да — достаточно изменить `SaveFormat` на `SaveFormat.Xls`. API не зависит от формата.

**Как вставить несколько JSON‑объектов?**  
Пройдитесь по данным в цикле и запишите каждую JSON‑строку в отдельную ячейку (например, A1, A2, …). Можно также хранить весь массив JSON в одной ячейке и позволить SmartMarkers развернуть его в строки, если установить `ArrayAsSingle = false`.

**Является ли SmartMarker единственным способом работы с JSON?**  
Нет. Можно вручную парсить JSON и записывать значения напрямую. SmartMarkers удобны, когда у вас уже есть шаблон с заполнителями.

## Pro Tips & Common Pitfalls

- **Совет:** Включите `Workbook.Settings.EnableFormulaCalculation`, если планируете добавлять формулы, зависящие от значений, полученных из JSON.
- **Осторожно:** Следите за завершающими пробелами в строках JSON; Excel воспринимает их как часть текста, что может нарушить последующий разбор.
- **Подсказка:** После вставки данных вызовите `worksheet.AutoFitColumns()`, чтобы всё было видно без ручного изменения размеров.

## Conclusion

Теперь вы знаете **how to create workbook**, **load json into excel**, **insert json into excel** и даже как **populate excel from json** с помощью движка SmartMarker от Aspose.Cells. Полный, готовый к запуску пример показывает каждый шаг — от инициализации рабочей книги до сохранения финального файла — так что вы можете скопировать код, адаптировать его и внедрить в свои проекты.

Готовы к следующему вызову? Попробуйте получать JSON из живого REST‑endpoint, десериализовать его в объекты и автоматически заполнять несколько строк. Или поэкспериментируйте с другими возможностями SmartMarker, например условным форматированием на основе значений JSON. Возможности безграничны, когда вы сочетаете C# и Aspose.Cells.

Есть вопросы или интересный кейс, которым хотите поделиться? Оставляйте комментарий ниже, и давайте поддерживать разговор. Приятного кодинга!  

![how to create workbook illustration](workbook-json.png){alt="пример создания рабочей книги"}

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}