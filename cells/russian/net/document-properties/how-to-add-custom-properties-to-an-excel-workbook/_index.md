---
category: general
date: 2026-10-01
description: Узнайте, как добавить пользовательские свойства в книгу Excel с помощью
  Aspose.Cells. Это руководство также показывает, как добавить идентификатор проекта
  и прочитать пользовательские свойства.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add custom properties
- how to add custom
- excel custom properties
- add project id
- read custom properties
language: ru
lastmod: 2026-10-01
og_description: Добавьте пользовательские свойства в книгу Excel с помощью Aspose.Cells.
  Следуйте этому полному руководству, чтобы добавить идентификатор проекта, задать
  информацию о рецензенте и программно считывать пользовательские свойства.
og_image_alt: Screenshot of an Excel worksheet displaying custom properties added
  via Aspose.Cells
og_title: Добавьте пользовательские свойства в книгу Excel – пошаговое руководство
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Learn how to add custom properties to an Excel workbook using Aspose.Cells.
    This guide also shows how to add project ID and read custom properties.
  headline: How to add custom properties to an Excel workbook
  type: TechArticle
- description: Learn how to add custom properties to an Excel workbook using Aspose.Cells.
    This guide also shows how to add project ID and read custom properties.
  name: How to add custom properties to an Excel workbook
  steps:
  - name: Open the saved `DataWithProps.xlsb` file in Microsoft Excel.
    text: Open the saved `DataWithProps.xlsb` file in Microsoft Excel.
  - name: Go to **File → Info → Properties → Advanced Properties**.
    text: Go to **File → Info → Properties → Advanced Properties**.
  - name: Select the **Custom** tab.
    text: Select the **Custom** tab.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: Как добавить пользовательские свойства в книгу Excel
url: /ru/net/document-properties/how-to-add-custom-properties-to-an-excel-workbook/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как добавить пользовательские свойства в книгу Excel

Если вам нужно **добавить пользовательские свойства** в книгу Excel, это руководство покажет, как сделать это с помощью Aspose.Cells for .NET. Вы также узнаете, как добавить идентификатор проекта, установить имя проверяющего и позже **прочитать пользовательские свойства** из файла.

Работа с пользовательскими метаданными позволяет внедрять бизнес‑специфическую информацию непосредственно в таблицу, упрощая отслеживание владельца, версии или любого другого контекста без необходимости поддерживать отдельную базу данных. Ниже представлены все шаги полного сквозного процесса — от создания книги до сохранения новых свойств.

## Требования

Прежде чем начать, убедитесь, что у вас есть:

* .NET 6.0 или более поздняя версия  
* Действительная лицензия Aspose.Cells for .NET (или бесплатная пробная версия)  
* Visual Studio 2022 (или любой IDE для C#)  

Дополнительные пакеты NuGet не требуются, кроме `Aspose.Cells`.

## Шаг 1: Настройка проекта и импорт пространств имён

Создайте новое консольное приложение и добавьте ссылку на Aspose.Cells:

```csharp
using System;
using Aspose.Cells;

namespace ExcelCustomPropertiesDemo
{
    class Program
    {
        static void Main()
        {
            // The rest of the code lives here
        }
    }
}
```

Пространство имён `Aspose.Cells` содержит классы `Workbook`, `Worksheet` и `CustomPropertyCollection`, которые мы будем использовать.

## Шаг 2: Загрузка существующей книги (или создание новой)

Можно начать с уже существующего файла `.xlsb` или создать новую книгу. В примере ниже загружается файл **Data.xlsb**, расположенный в папке `YOUR_DIRECTORY`.

```csharp
// Load the existing workbook
var workbookPath = @"YOUR_DIRECTORY\Data.xlsb";
var workbook = new Workbook(workbookPath);
```

Если файл не существует, замените код на `new Workbook();`, чтобы создать пустую книгу.

## Шаг 3: Добавление пользовательских свойств на первый лист

Основная операция — **добавить пользовательские свойства** на лист. Aspose.Cells хранит пользовательские свойства в коллекции, которая ведёт себя как словарь.

```csharp
// Get the first worksheet (index 0)
var worksheet = workbook.Worksheets[0];

// Add a numeric ProjectId property
worksheet.CustomProperties.Add("ProjectId", 12345);

// Add a string Reviewer property
worksheet.CustomProperties.Add("Reviewer", "John Doe");

// Optional: add a DateTime property for the creation timestamp
worksheet.CustomProperties.Add("CreatedOn", DateTime.UtcNow);
```

Мы используем `CustomProperties.Add` вместо `CustomProperties["Name"] = value`, потому что метод `Add` создаёт запись, если её нет, и гарантирует правильный тип данных. Такой подход предотвращает случайные несоответствия типов, которые могут вызвать ошибки во время чтения значений позже.

## Шаг 4: Сохранение книги с новыми свойствами

После внедрения метаданных сохраните изменения в новый файл, чтобы оригинал остался нетронутым.

```csharp
// Save the workbook with the custom properties
var outputPath = @"YOUR_DIRECTORY\DataWithProps.xlsb";
workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to {outputPath}");
```

На данном этапе файл Excel содержит пользовательские метаданные, которые вы определили. Вы можете проверить свойства, следуя инструкциям в следующем разделе.

## Шаг 5: Чтение пользовательских свойств из книги

Чтение **excel custom properties** происходит по той же схеме коллекции. Этот фрагмент кода демонстрирует, как получить значения, которые мы только что сохранили.

```csharp
// Load the workbook that contains custom properties
var loadedWorkbook = new Workbook(outputPath);
var loadedWorksheet = loadedWorkbook.Worksheets[0];
var props = loadedWorksheet.CustomProperties;

// Retrieve each property safely
int projectId = props["ProjectId"] != null ? (int)props["ProjectId"].Value : -1;
string reviewer = props["Reviewer"] != null ? props["Reviewer"].Value.ToString() : "Unknown";
DateTime createdOn = props["CreatedOn"] != null ? (DateTime)props["CreatedOn"].Value : DateTime.MinValue;

Console.WriteLine($"ProjectId: {projectId}");
Console.WriteLine($"Reviewer: {reviewer}");
Console.WriteLine($"CreatedOn (UTC): {createdOn:u}");
```

Индексатор `CustomPropertyCollection` возвращает объект `CustomProperty`; доступ к его свойству `Value` даёт вам сохранённые данные в их исходном типе. Проверка на `null` перед приведением типов предотвращает `NullReferenceException`, если свойство отсутствует.

### Ожидаемый вывод в консоль

```
ProjectId: 12345
Reviewer: John Doe
CreatedOn (UTC): 2026-10-01 12:34:56Z
```

Отметка времени будет соответствовать точному моменту вызова `Add` в шаге 3.

## Совет профессионала: Обновление существующего пользовательского свойства

Если позже понадобится **how to add custom** информацию (например, изменить проверяющего), используйте сеттер `CustomPropertyCollection`:

```csharp
// Change the reviewer name
if (props["Reviewer"] != null)
{
    props["Reviewer"].Value = "Jane Smith";
}
else
{
    // Property does not exist; add it
    props.Add("Reviewer", "Jane Smith");
}
```

Такой шаблон гарантирует, что свойство будет либо обновлено, либо создано, что полезно в итеративных рабочих процессах, например при автоматической генерации отчётов.

## Шаг 6: Проверка свойств в Excel (необязательно)

Вы также можете просмотреть пользовательские свойства непосредственно в Excel:

1. Откройте сохранённый файл `DataWithProps.xlsb` в Microsoft Excel.  
2. Перейдите в **File → Info → Properties → Advanced Properties**.  
3. Выберите вкладку **Custom**.  

Вы увидите записи `ProjectId`, `Reviewer` и `CreatedOn` со своими значениями.

## Полный рабочий пример

Ниже приведена полная, автономная программа, объединяющая все предыдущие фрагменты. Скопируйте её в `Program.cs` и запустите; консоль отобразит полученные значения.

```csharp
using System;
using Aspose.Cells;

namespace ExcelCustomPropertiesDemo
{
    class Program
    {
        static void Main()
        {
            // Paths (adjust to your environment)
            var sourcePath = @"YOUR_DIRECTORY\Data.xlsb";
            var resultPath = @"YOUR_DIRECTORY\DataWithProps.xlsb";

            // Load or create workbook
            var workbook = new Workbook(sourcePath);
            var worksheet = workbook.Worksheets[0];

            // Add custom properties
            worksheet.CustomProperties.Add("ProjectId", 12345);
            worksheet.CustomProperties.Add("Reviewer", "John Doe");
            worksheet.CustomProperties.Add("CreatedOn", DateTime.UtcNow);

            // Save the workbook
            workbook.Save(resultPath);
            Console.WriteLine($"Saved workbook with custom properties to {resultPath}");

            // Load the saved workbook to read properties
            var loadedWorkbook = new Workbook(resultPath);
            var loadedWorksheet = loadedWorkbook.Worksheets[0];
            var props = loadedWorksheet.CustomProperties;

            // Read properties
            int projectId = props["ProjectId"] != null ? (int)props["ProjectId"].Value : -1;
            string reviewer = props["Reviewer"] != null ? props["Reviewer"].Value.ToString() : "Unknown";
            DateTime createdOn = props["CreatedOn"] != null ? (DateTime)props["CreatedOn"].Value : DateTime.MinValue;

            Console.WriteLine($"ProjectId: {projectId}");
            Console.WriteLine($"Reviewer: {reviewer}");
            Console.WriteLine($"CreatedOn (UTC): {createdOn:u}");
        }
    }
}
```

Запуск этой программы выдаст консольный вывод, показанный ранее, и создаст файл `DataWithProps.xlsb` с внедрёнными метаданными.

## Часто задаваемые вопросы и особые случаи

| Question | Answer |
|---|---|
| **Can I store non‑primitive types?** | Aspose.Cells поддерживает `string`, `int`, `double`, `DateTime` и `bool`. Для сложных объектов сначала сериализуйте их в JSON или XML и сохраняйте как строку. |
| **What if the workbook is password‑protected?** | Откройте книгу с паролем (`new Workbook(path, password)`) перед доступом к `CustomProperties`. Свойства остаются доступными после расшифровки. |
| **Do custom properties survive format conversion?** | При сохранении в другой формат (например, `.xlsx`) Aspose.Cells сохраняет пользовательские свойства, если целевой формат их поддерживает. |
| **How to delete a custom property?** | Используйте `worksheet.CustomProperties.Remove("PropertyName");`. Это удалит запись из коллекции. |

## Следующие шаги

Теперь, когда вы знаете, как **add custom properties**, вы можете изучить связанные темы, такие как:

* **excel custom properties** для версионирования документов  
* **read custom properties** из нескольких листов в одной книге  
* Использование **Aspose.Cells** для создания сводных таблиц, ссылающихся на пользовательские метаданные  
* Экспорт книги в PDF с сохранением пользовательских свойств  

Экспериментируйте с различными типами данных, комбинируйте пользовательские свойства с комментариями ячеек или интегрируйте метаданные в более крупную систему управления документами.

---

**Ready to automate your Excel reporting?** Добавьте приведённый выше код в свой проект, скорректируйте имена свойств под ваши бизнес‑требования, и у вас будет самодокументирующаяся таблица, готовая к дальнейшей обработке.

## Что изучать дальше?

Следующие учебники охватывают тесно связанные темы, расширяющие техники, продемонстрированные в этом руководстве. Каждый ресурс содержит полностью рабочие примеры кода с пошаговыми объяснениями, помогающими освоить дополнительные возможности API и исследовать альтернативные подходы в ваших проектах.

- [Create Excel Workbook – Add Custom Properties and Save as XLSB](/cells/english/net/document-properties/create-excel-workbook-add-custom-properties-and-save-as-xlsb/)
- [How to Access Custom Document Properties in Excel Using Aspose.Cells for .NET](/cells/english/net/workbook-operations/access-custom-excel-properties-aspose-cells-net/)
- [Master Excel Custom Properties Using Aspose.Cells .NET for Enhanced Data Management](/cells/english/net/data-manipulation/excel-custom-properties-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}