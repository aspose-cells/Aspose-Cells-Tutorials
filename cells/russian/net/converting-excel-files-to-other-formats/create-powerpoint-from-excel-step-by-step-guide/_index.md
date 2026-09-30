---
category: general
date: 2026-02-09
description: Создайте PowerPoint из Excel за считанные минуты — узнайте, как преобразовать
  Excel в PowerPoint и экспортировать Excel в PPT с простым примером кода на C#.
draft: false
keywords:
- create powerpoint from excel
- convert excel to powerpoint
- export excel to ppt
- generate ppt from excel
- how to convert excel to pptx
language: ru
og_description: Создавайте PowerPoint из Excel быстро. Это руководство показывает,
  как преобразовать Excel в PowerPoint, экспортировать Excel в PPT и генерировать
  PPT из Excel с помощью C#.
og_title: Создание PowerPoint из Excel – Полное руководство по программированию
tags:
- C#
- Aspose.Cells
- PowerPoint automation
- Office interop
title: Создание PowerPoint из Excel – пошаговое руководство
url: /ru/net/converting-excel-files-to-other-formats/create-powerpoint-from-excel-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Создание PowerPoint из Excel – Полное руководство по программированию

Когда‑то вам нужно **создать PowerPoint из Excel**, но вы не знали, какой API вызвать? Вы не одиноки. Многие разработчики сталкиваются с проблемой, когда хотят превратить таблицы в набор слайдов без ручного копирования‑вставки.  

Хорошая новость: с несколькими строками C# вы можете **конвертировать Excel в PowerPoint**, экспортировать фигуры листа и получить готовый к презентации файл PPTX. В этом руководстве мы пройдем весь процесс, объясним, почему каждый шаг важен, и покажем, как справиться с наиболее распространенными подводными камнями.

## Что вы узнаете

- Как загрузить книгу Excel, содержащую диаграммы, изображения или SmartArt.  
- Точный вызов, который **экспортирует Excel в PPT** с помощью библиотеки Aspose.Cells.  
- Как сохранить полученную презентацию и проверить результат.  
- Советы по работе с книгами без фигур, настройке размера слайда и устранению несоответствий версий.

Никаких внешних инструментов, без COM‑interop, только чистый .NET‑код, который работает где угодно, где поддерживается .NET Core или .NET 5+.

---

## Требования

Прежде чем начать, убедитесь, что у вас есть:

1. **Aspose.Cells for .NET** (библиотека, предоставляющая `SaveToPresentation`). Вы можете получить её из NuGet:  

   ```bash
   dotnet add package Aspose.Cells
   ```
2. Последний .NET SDK (рекомендуется 6.0 или новее).  
3. Файл Excel (`shapes.xlsx`), содержащий хотя бы одну фигуру, диаграмму или изображение, которые вы хотите увидеть на слайде.

Вот и всё — никакой установки Office, никаких проблем с лицензией для этой демонстрации (бесплатная оценочная версия работает отлично).

---

## Шаг 1: Загрузка книги Excel (Create PowerPoint from Excel)

Первое, что нам нужно, — объект `Workbook`, указывающий на исходный файл. Этот объект представляет весь документ Excel, включая листы, диаграммы и встроенные объекты.

```csharp
using Aspose.Cells;
using Aspose.Slides;

// Step 1: Load the Excel workbook containing the shapes
Workbook workbook = new Workbook(@"C:\MyProjects\ExcelToPpt\shapes.xlsx");

// Why this matters:
// - `Workbook` abstracts the file format, so you don’t have to worry about .xls vs .xlsx.
// - Loading the file early lets you inspect its contents (e.g., count of worksheets) before conversion.
```

> **Pro tip:** Если вы не уверены, существует ли файл, оберните конструктор в `try/catch` и выведите понятное сообщение об ошибке. Это избавит от загадочного `FileNotFoundException` позже.

---

## Шаг 2: Конвертация книги в презентацию PowerPoint (Export Excel to PPT)

Aspose.Cells поставляется со встроенным экспортером, который превращает всю книгу — или выбранные листы — в презентацию PowerPoint. Метод `SaveToPresentation` делает всю тяжелую работу.

```csharp
// Step 2: Convert the workbook to a PowerPoint presentation (PPTX format)
Presentation presentation = workbook.SaveToPresentation(ExportTo.Pptx);

// How it works:
// - Each worksheet becomes a separate slide.
// - Shapes, charts, and images are rasterized and placed on the slide preserving their layout.
// - You can later tweak the `Presentation` object (e.g., add a title slide) before saving.
```

Если вам нужно **generate ppt from excel** только для части листов, используйте перегрузку, принимающую коллекцию `SheetOptions`. Для большинства сценариев достаточно стандартного преобразования.

---

## Шаг 3: Сохранение полученной презентации (How to Convert Excel to PPTX)

Теперь, когда у нас есть экземпляр `Presentation`, сохранить его на диск просто. На выходе будет обычный файл `.pptx`, который откроет любой современный PowerPoint.

```csharp
// Step 3: Save the generated presentation to a file
presentation.Save(@"C:\MyProjects\ExcelToPpt\shapes.pptx");

// Verification:
// Open the file in PowerPoint or use Aspose.Slides to programmatically inspect slide count.
```

> **Что если в книге нет фигур?**  
> Экспортер всё равно создаст слайды, но они будут пустыми. Вы можете проверить `workbook.Worksheets[i].Shapes.Count` перед конвертацией и решить, пропускать ли такой лист.

---

## Необязательно: Тонкая настройка вывода (Advanced Export Excel to PPT)

Иногда стандартный размер слайда (4:3) не подходит для широкоформатных презентаций. Вы можете изменить размеры слайда перед сохранением:

```csharp
// Set slide size to widescreen (16:9)
presentation.SlideSize.SetSize(SlideSizeType.Widescreen, SlideSizeScaleType.DoNotScale);

// Add a custom title slide (optional)
ISlide titleSlide = presentation.Slides.InsertEmptySlide(0, presentation.LayoutSlides[0]);
titleSlide.Shapes.AddAutoShape(ShapeType.Rectangle, 50, 50, 600, 100)
          .TextFrame.Text = "Quarterly Report – Exported from Excel";
```

Эти настройки демонстрируют **how to convert Excel to PowerPoint** с профессиональным видом, а не просто «сырой» выгрузкой данных.

---

## Полный рабочий пример (All Steps Combined)

Ниже представлен полностью готовый к запуску код. Скопируйте его в консольное приложение, поправьте пути к файлам и нажмите **F5**.

```csharp
using System;
using Aspose.Cells;
using Aspose.Slides;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the workbook
            string excelPath = @"C:\MyProjects\ExcelToPpt\shapes.xlsx";
            Workbook workbook = new Workbook(excelPath);

            // 2️⃣ Convert to PPTX
            Presentation presentation = workbook.SaveToPresentation(ExportTo.Pptx);

            // Optional: set widescreen layout
            presentation.SlideSize.SetSize(SlideSizeType.Widescreen, SlideSizeScaleType.DoNotScale);

            // Optional: add a title slide
            ISlide titleSlide = presentation.Slides.InsertEmptySlide(0, presentation.LayoutSlides[0]);
            titleSlide.Shapes.AddAutoShape(ShapeType.Rectangle, 50, 50, 600, 100)
                      .TextFrame.Text = "Quarterly Report – Exported from Excel";

            // 3️⃣ Save the PPTX file
            string pptxPath = @"C:\MyProjects\ExcelToPpt\shapes.pptx";
            presentation.Save(pptxPath);

            Console.WriteLine($"✅ Successfully created PowerPoint from Excel! File saved at: {pptxPath}");
        }
    }
}
```

**Ожидаемый результат:** Откройте `shapes.pptx` в PowerPoint. Вы увидите один слайд на каждый лист, каждый из которых сохраняет оригинальные диаграммы, изображения и другие фигуры. При желании в начале будет добавлен титульный слайд, придающий колоде презентацию.

---

## Часто задаваемые вопросы и особые случаи

| Вопрос | Ответ |
|----------|--------|
| *Что если нужен только один лист?* | Используйте `Workbook.Worksheets[0]` и вызовите `SaveToPresentation` для этого листа через `SheetOptions`. |
| *Можно ли сохранить формулы Excel?* | Нет — формулы отображаются как статические значения на слайде. Если нужны живые данные, рассмотрите возможность привязки PPTX к файлу Excel позже. |
| *Работает ли это на Linux/macOS?* | Да. Aspose.Cells платформенно‑независим; достаточно установить .NET‑runtime. |
| *А как с защищёнными паролем книгами?* | Загрузите их с помощью `LoadOptions`, где указывается пароль, перед вызовом `SaveToPresentation`. |
| *Почему получаю пустые слайды?* | Проверьте, что в книге действительно есть фигуры (`Shapes.Count > 0`). Пустые слайды создаются для пустых листов. |

---

## Заключение

Теперь у вас есть чёткое, сквозное решение для **create PowerPoint from Excel** с помощью C#. Загрузив книгу, вызвав `SaveToPresentation` и сохранив результат, вы можете **convert Excel to PowerPoint**, **export Excel to PPT** и **generate PPT from Excel** всего в несколько строк кода.  

Дальше вы можете:

- Добавлять анимацию к сгенерированным слайдам с помощью Aspose.Slides.  
- Автоматизировать весь конвейер (например, читать файлы из папки и пакетно их конвертировать).  
- Интегрировать код в API ASP.NET Core, чтобы пользователи могли загрузить Excel‑файл и мгновенно получить PPTX.

Попробуйте, поиграйте с размером слайда, добавьте собственный титульный слайд — много возможностей, чтобы сделать результат по‑настоящему вашим. Есть вопросы или возникли сложности? Оставляйте комментарий ниже, и happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}