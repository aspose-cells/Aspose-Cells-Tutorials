---
category: general
date: 2026-11-22
description: Создайте файл xlsb на C# и узнайте, как добавить свойства к листу Excel;
  сохраните книгу в формате xlsb с помощью Aspose.Cells для быстрого бинарного хранения.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create xlsb file
- how to add properties
- excel worksheet custom properties
- custom worksheet properties
- save workbook as xlsb
language: ru
lastmod: 2026-11-22
og_description: Создайте файл xlsb в C# с помощью Aspose.Cells. Этот учебник показывает,
  как добавить свойства к листу Excel и сохранить книгу в формате xlsb для быстрого
  бинарного хранения.
og_image_alt: Screenshot of an Excel workbook saved as .xlsb with custom worksheet
  properties displayed in the file explorer
og_title: Создайте файл xlsb с пользовательскими свойствами – руководство по C#
schemas:
- author: Aspose
  dateModified: '2026-11-22'
  description: Create xlsb file in C# and learn how to add properties to an Excel
    worksheet; save workbook as xlsb using Aspose.Cells for fast binary storage.
  headline: How to create xlsb file with custom worksheet properties in C#
  type: TechArticle
- description: Create xlsb file in C# and learn how to add properties to an Excel
    worksheet; save workbook as xlsb using Aspose.Cells for fast binary storage.
  name: How to create xlsb file with custom worksheet properties in C#
  steps:
  - name: Open your preferred IDE (Visual Studio, Rider, or VS Code).
    text: Open your preferred IDE (Visual Studio, Rider, or VS Code).
  - name: 'Create a new console project:'
    text: 'Create a new console project:'
  - name: 'Add the Aspose.Cells NuGet package:'
    text: 'Add the Aspose.Cells NuGet package:'
  - name: Open the file.
    text: Open the file.
  - name: Right‑click the sheet tab and choose **View Code** → **Properties** (or
      use the *File → Info → Properties* dialog).
    text: Right‑click the sheet tab and choose **View Code** → **Properties** (or
      use the *File → Info → Properties* dialog).
  - name: You will see the `Department` and `Reviewed` entries.
    text: You will see the `Department` and `Reviewed` entries.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: Как создать файл xlsb с пользовательскими свойствами листа в C#
url: /ru/net/saving-and-exporting-excel-files-with-options/how-to-create-xlsb-file-with-custom-worksheet-properties-in/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как создать файл xlsb с пользовательскими свойствами листа в C#

Если вам нужно **программно создать файл xlsb**, это руководство предоставляет полное решение. Вы увидите, как **добавить свойства** к листу Excel и затем **сохранить книгу как xlsb** с помощью Aspose.Cells. Шаги работают с .NET 6 и новее и не требуют установки Excel вручную.

В руководстве рассматриваются настройка проекта, создание книги, добавление пользовательских свойств листа, сохранение файла в бинарном формате Excel и проверка результата. К концу вы сможете генерировать компактную книгу *.xlsb*, содержащую метаданные, такие как отдел или статус проверки.

## Создание файла xlsb – обзор

Создание файла *.xlsb* отличается от классического формата *.xlsx* только конечным шагом сохранения. Структура книги, листы и данные ячеек одинаковы; бинарный формат уменьшает размер файла и ускоряет его открытие в Excel. Пример кода ниже демонстрирует полный жизненный цикл, от пустой книги до сохранённого файла *.xlsb*, содержащего **пользовательские свойства листа Excel**.

## Настройка Aspose.Cells в вашем проекте C#

1. Откройте предпочитаемую IDE (Visual Studio, Rider или VS Code).  
2. Создайте новый консольный проект:

   ```bash
   dotnet new console -n XlsbDemo
   cd XlsbDemo
   ```

3. Добавьте пакет Aspose.Cells через NuGet:

   ```bash
   dotnet add package Aspose.Cells
   ```

   Пакет предоставляет классы `Workbook`, `Worksheet` и `CustomPropertyCollection`, необходимые для этого руководства.

## Как добавить свойства к листу Excel

Пользовательские свойства листа позволяют хранить произвольные метаданные рядом с листом. Они полезны для последующей обработки, аудита или подсказок в UI. Следующий код создаёт книгу, получает доступ к первому листу и добавляет два свойства: строку `Department` и логическое `Reviewed`.

```csharp
using Aspose.Cells;

class XlsbCustomPropsDemo
{
    static void Main()
    {
        // Step 1: Create a new workbook and get its first worksheet
        Workbook workbook = new Workbook();                 // workbook is the container for all sheets
        Worksheet worksheet = workbook.Worksheets[0];       // the default sheet is at index 0

        // Step 2: Add custom properties to the worksheet
        // These are *excel worksheet custom properties* that travel with the sheet.
        worksheet.CustomProperties.Add("Department", "Finance");
        worksheet.CustomProperties.Add("Reviewed", true);

        // Step 3: Save the workbook in binary Excel format (.xlsb)
        // The file will contain the custom properties defined above.
        workbook.Save("CustomProps.xlsb");
    }
}
```

**Почему эти строки важны**

- `Workbook()` создаёт представление Excel‑файла в памяти.  
- `worksheet.CustomProperties.Add` сохраняет пары «ключ‑значение», которые Excel может прочитать через диалог *Custom Properties*.  
- `workbook.Save` с расширением `.xlsb` инициирует **сохранение книги как xlsb**, автоматически используя бинарный формат.

Вы можете добавить любое количество свойств; коллекция принимает строки, числа, даты и логические значения. Если понадобится прочитать их позже, используйте `worksheet.CustomProperties["Department"]`.

## Сохранить книгу как xlsb

Метод `Save` определяет формат файла по расширению. Указав `"CustomProps.xlsb"`, вы заставляете Aspose.Cells записать бинарную книгу. Этот шаг — единственное место, где в коде встречается **save workbook as xlsb**, но эффект виден во всём размере файла и скорости открытия.

Если хотите явно управлять форматом, используйте объект `SaveOptions`:

```csharp
// Alternative: specify the save format with SaveOptions
var options = new XlsbSaveOptions(SaveFormat.Xlsb);
workbook.Save("CustomPropsExplicit.xlsb", options);
```

Оба подхода создают корректный файл *.xlsb*, содержащий **пользовательские свойства листа**, которые вы определили.

## Проверка пользовательских свойств листа

После выполнения программы откройте сгенерированный `CustomProps.xlsb` в Excel:

1. Откройте файл.  
2. Щёлкните правой кнопкой мыши по вкладке листа и выберите **View Code** → **Properties** (или используйте диалог *File → Info → Properties*).  
3. Вы увидите записи `Department` и `Reviewed`.

Наличие этих записей подтверждает, что **excel worksheet custom properties** были успешно внедрены.

### Ожидаемый результат

Запуск программы создаёт два файла в папке проекта:

- `CustomProps.xlsb` – бинарная книга с пользовательскими свойствами.  
- `CustomPropsExplicit.xlsb` – идентичное содержимое, сохранённое через `XlsbSaveOptions`.

Оба файла открываются в Excel без предупреждений и показывают пользовательские метаданные при просмотре.

## Распространённые ошибки и рекомендации по лучшим практикам

- **Не смешивайте расширения файлов.** Использование `.xlsx` при передаче `XlsbSaveOptions` приводит к повреждённому файлу. Всегда согласовывайте расширение с выбранным форматом.  
- **Имена свойств чувствительны к регистру** в коллекции. Обращайтесь к ним точно так же, как они были добавлены.  
- **Большие книги выигрывают от бинарного формата**, поскольку размер файла может уменьшиться до 50 % по сравнению с `.xlsx`. Это особенно актуально, когда книга содержит множество формул или стилей.  
- **Потокобезопасность:** экземпляры `Workbook` не являются потокобезопасными. Создавайте отдельный экземпляр для каждого потока, если генерируете несколько файлов одновременно.  

## Следующие шаги

Теперь, когда вы умеете **создавать файл xlsb** с **пользовательскими свойствами листа**, вы можете исследовать:

- Добавление **excel worksheet custom properties** к нескольким листам в одной книге.  
- Использование **how to add properties** для строк или ячеек через коллекцию `Cell.CustomProperties`.  
- Экспорт книги в PDF или HTML с сохранением метаданных.  
- Автоматизацию процесса в веб‑API, которое напрямую возвращает поток *.xlsb* клиенту.

Эти расширения позволяют построить надёжные конвейеры автоматизации Excel, использующие скорость бинарного формата и гибкость пользовательских метаданных.

---

*Вы узнали, как создать книгу *.xlsb* в C#, добавить пользовательские свойства листа и сохранить файл с помощью Aspose.Cells. Применяйте приведённые шаблоны к своим отчётам, панелям мониторинга или сервисам обмена данными.*


## Что изучать дальше?


Следующие руководства охватывают тесно связанные темы, построенные на техниках, продемонстрированных в этом руководстве. Каждый ресурс содержит полностью работающие примеры кода с пошаговыми объяснениями, помогающими освоить дополнительные возможности API и исследовать альтернативные подходы в ваших проектах.

- [Create Excel Workbook C# – Add Custom Property & Save XLSB](/cells/english/net/document-properties/create-excel-workbook-c-add-custom-property-save-xlsb/)
- [How to Save XLSB and Add Custom Document Properties in C#](/cells/english/net/document-properties/how-to-save-xlsb-and-add-custom-document-properties-in-c/)
- [How to Save XLSB with Custom Properties in C# – Step‑by‑Step Guide](/cells/english/net/document-properties/how-to-save-xlsb-with-custom-properties-in-c-step-by-step-gu/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}