---
category: general
date: 2026-03-30
description: Создайте презентацию PowerPoint из Excel быстро с помощью Aspose.Cells
  и Aspose.Slides. Узнайте, как экспортировать лист как изображение и сохранить презентацию
  в формате PPTX на C#.
draft: false
keywords:
- create powerpoint from excel
- convert excel to powerpoint
- export worksheet as image
- save presentation as pptx
- export excel chart as picture
language: ru
og_description: Создайте PowerPoint из Excel на C# с помощью Aspose. Экспортируйте
  лист как изображение, оставьте формы редактируемыми и сохраните результат в формате
  PPTX.
og_title: Создайте PowerPoint из Excel — Полный учебник по C#
tags:
- Aspose
- C#
- Office Automation
title: Создание PowerPoint из Excel — пошаговое руководство на C#
url: /ru/net/converting-excel-files-to-other-formats/create-powerpoint-from-excel-step-by-step-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Создание PowerPoint из Excel – Полный C#‑урок

Когда‑то вам нужно **создать PowerPoint из Excel**, но вы не знаете, какая библиотека позволит сохранить диаграммы редактируемыми? Вы не одиноки. Во многих сценариях отчётности требуется превратить таблицу в набор слайдов, не теряя возможности позже поправить текстовые поля. В этом руководстве показано, как **конвертировать Excel в PowerPoint** с помощью Aspose.Cells и Aspose.Slides, а также как **экспортировать лист как изображение** и, наконец, **сохранить презентацию в формате PPTX**.

Мы пройдёмся по каждой строке кода, объясним *почему* каждое настройка важна и обсудим, что делать, если ваша книга содержит сложные диаграммы, которые лучше экспортировать как картинку. К концу вы получите готовое к запуску консольное приложение C#, которое берёт `ShapesDemo.xlsx` и выдаёт `Result.pptx` — все текстовые поля остаются редактируемыми, а изображения чёткими.

## Что понадобится

- .NET 6.0 или новее (API также работает с .NET Framework, но .NET 6 — оптимальный вариант).  
- NuGet‑пакеты **Aspose.Cells** и **Aspose.Slides** (для тестирования подойдёт бесплатная пробная лицензия).  
- Базовое знакомство с синтаксисом C# — если вы умеете писать `Console.WriteLine`, вам достаточно.  

Никакого дополнительного COM‑interop, без установки Office на сервере и без ручного копирования‑вставки изображений. Всё делается программно.

---

## Создание PowerPoint из Excel – Загрузка книги и настройка параметров экспорта

Первое, что мы делаем, — открываем файл Excel и указываем Aspose.Cells, как должен быть отрисован лист. Объект `ImageOrPrintOptions` — это место, где происходит магия: мы включаем `ExportShapes` и `ExportEditableTextBoxes`, чтобы любые фигуры (включая диаграммы) стали частью слайда **и** оставались редактируемыми после конвертации.

```csharp
using Aspose.Cells;
using Aspose.Slides;

// 1️⃣ Load the Excel workbook
string excelPath = "YOUR_DIRECTORY/ShapesDemo.xlsx";
Workbook workbook = new Workbook(excelPath);
Worksheet worksheet = workbook.Worksheets[0];   // Grab the first sheet

// 2️⃣ Configure image export – keep shapes editable
ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
{
    OnePagePerSheet = true,          // Export the whole sheet as one slide
    ExportShapes = true,             // Include shapes (charts, drawings)
    ExportEditableTextBoxes = true   // Make text boxes editable in PPTX
};
```

**Зачем эти флаги?**  
- `OnePagePerSheet` предотвращает разбивку листа на несколько слайдов — вы получаете одну картинку полного размера.  
- `ExportShapes` заставляет Aspose.Cells растеризовать диаграммы *и* векторные фигуры, сохраняя их внешний вид.  
- `ExportEditableTextBoxes` — секретный ингредиент, позволяющий дважды кликнуть по текстовому полю в PowerPoint и отредактировать текст без открытия Excel.

> **Pro tip:** Если вам нужна только статичная картинка диаграммы, установите `ExportShapes = false` и позже используйте метод `ExportExcelChartAsPicture` (см. завершающий раздел).

---

## Конвертация Excel в PowerPoint – Генерация изображения из листа

С готовыми параметрами мы превращаем лист в `System.Drawing.Image`. Класс `WorksheetToImageConverter` делает всю тяжёлую работу, применяя только что заданные настройки.

```csharp
// 3️⃣ Convert the worksheet to an image using the options above
WorksheetToImageConverter converter = new WorksheetToImageConverter(worksheet);
System.Drawing.Image sheetImage = converter.ConvertToImage(0, imageOptions);
```

Аргумент `0` указывает на первую страницу (у нас только одна из‑за `OnePagePerSheet`). Полученный `sheetImage` сохраняет исходное DPI, поэтому ваш слайд не будет выглядеть пиксельным даже на дисплеях с высоким разрешением.

---

## Сохранение презентации в PPTX – Вставка изображения на слайд

Теперь создаём новый файл PowerPoint, добавляем слайд и помещаем битмап на него. Aspose.Slides рассматривает картинку как форму *picture frame*, которую позже можно масштабировать или перемещать так же, как любой нативный объект PowerPoint.

```csharp
// 4️⃣ Create a new PowerPoint presentation
Presentation presentation = new Presentation();
ISlide slide = presentation.Slides[0];   // The default blank slide

// Add the Excel‑derived image as a picture frame
slide.Shapes.AddPictureFrame(
    ShapeType.Rectangle,                 // Simple rectangle container
    0, 0,                                // Top‑left corner (0,0)
    sheetImage.Width,                    // Width of the picture
    sheetImage.Height,                   // Height of the picture
    sheetImage);                         // The bitmap we generated
```

> **Что делать, если изображение больше размеров слайда?**  
> PowerPoint автоматически обрежет всё, что выходит за пределы слайда. Быстрое решение — масштабировать изображение перед вставкой:

```csharp
float scale = Math.Min(presentation.SlideSize.Size.Width / (float)sheetImage.Width,
                       presentation.SlideSize.Size.Height / (float)sheetImage.Height);
int newWidth  = (int)(sheetImage.Width * scale);
int newHeight = (int)(sheetImage.Height * scale);
```

Затем передайте `newWidth` и `newHeight` в `AddPictureFrame`.

---

## Экспорт листа как изображения – Сохранение файла PPTX

Наконец, сохраняем презентацию на диск. Флаг `SaveFormat.Pptx` гарантирует современный формат OpenXML, который работает во всех последних версиях PowerPoint.

```csharp
// 5️⃣ Save the presentation as a PPTX file
string pptxPath = "YOUR_DIRECTORY/Result.pptx";
presentation.Save(pptxPath, SaveFormat.Pptx);
```

Когда откроете `Result.pptx`, вы увидите один слайд, полностью копирующий ваш лист Excel, но при этом сможете кликнуть по любому текстовому полю и отредактировать его прямо в PowerPoint.

---

## Экспорт диаграммы Excel как картинки – Когда предпочтительны растровые изображения

Иногда редактируемые фигуры не нужны; достаточно качественного PNG‑изображения диаграммы. Aspose.Cells может экспортировать конкретную диаграмму в изображение без конвертации всего листа:

```csharp
// Example: Export the first chart on the sheet as a PNG
int chartIndex = 0; // Adjust if you have multiple charts
Chart chart = worksheet.Charts[chartIndex];
ImageOrPrintOptions chartOptions = new ImageOrPrintOptions
{
    ImageFormat = ImageFormat.Png,
    OnePagePerSheet = false
};
chart.ToImage("chart.png", chartOptions);
```

Затем можно вставить `chart.png` в слайд тем же способом, что и `sheetImage`. Такой подход уменьшает размер файла PPTX и полезен, когда окружающие данные не требуются на слайде.

---

## Распространённые подводные камни и как их избежать

| Проблема | Почему происходит | Как исправить |
|----------|-------------------|---------------|
| **Текст выглядит размытым** | Экспорт выполнен с низким DPI (по умолчанию 96). | Установите `imageOptions.Dpi = 300;` перед конвертацией. |
| **Фигуры исчезают** | `ExportShapes` оставлен `false`. | Убедитесь, что `ExportShapes = true`, когда нужны редактируемые графики. |
| **Несоответствие размеров слайда** | Изображение больше размеров слайда. | Масштабируйте изображение (см. фрагмент кода) или измените размер слайда через `presentation.SlideSize`. |
| **Исключение лицензии** | Используется пробная версия без активации. | В начале `Main` вызовите `License license = new License(); license.SetLicense("Aspose.Total.lic");`. |

---

## Полный рабочий пример (готов к копированию)

Ниже представлен весь код программы, готовый к вставке в новый консольный проект. Замените `YOUR_DIRECTORY` на папку, где находится ваш файл Excel.

```csharp
using System;
using Aspose.Cells;
using Aspose.Slides;
using System.Drawing;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -----------------------------------------------------------------
            // 1️⃣ Load the Excel workbook
            // -----------------------------------------------------------------
            string excelPath = "YOUR_DIRECTORY/ShapesDemo.xlsx";
            Workbook workbook = new Workbook(excelPath);
            Worksheet worksheet = workbook.Worksheets[0];

            // -----------------------------------------------------------------
            // 2️⃣ Set up export options – keep shapes editable
            // -----------------------------------------------------------------
            ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
            {
                OnePagePerSheet = true,
                ExportShapes = true,
                ExportEditableTextBoxes = true,
                Dpi = 300                 // High‑resolution output
            };

            // -----------------------------------------------------------------
            // 3️⃣ Convert worksheet to an image
            // -----------------------------------------------------------------
            WorksheetToImageConverter converter = new WorksheetToImageConverter(worksheet);
            Image sheetImage = converter.ConvertToImage(0, imageOptions);

            // -----------------------------------------------------------------
            // 4️⃣ Create PowerPoint and add the image as a slide
            // -----------------------------------------------------------------
            Presentation presentation = new Presentation();
            ISlide slide = presentation.Slides[0];
            slide.Shapes.AddPictureFrame(
                ShapeType.Rectangle,
                0, 0,
                sheetImage.Width,
                sheetImage.Height,
                sheetImage);

            // -----------------------------------------------------------------
            // 5️⃣ Save the PPTX file
            // -----------------------------------------------------------------
            string pptxPath = "YOUR_DIRECTORY/Result.pptx";
            presentation.Save(pptxPath, SaveFormat.Pptx);

            Console.WriteLine("✅ PowerPoint created successfully at: " + pptxPath);
        }
    }
}
```

**Ожидаемый вывод:**  
При запуске программа выводит `✅ PowerPoint created successfully at: YOUR_DIRECTORY/Result.pptx`. Открытие PPTX показывает один слайд, отражающий оригинальный лист Excel, с редактируемыми текстовыми полями.

---

## Итоги и дальнейшие шаги

Теперь вы знаете, как **создавать PowerPoint из Excel** с помощью мощных API Aspose, как **экспортировать лист как изображение** и как **сохранять презентацию в PPTX**, сохраняя возможность редактирования. Та же схема работает и с книгами, содержащими несколько листов — просто пройдитесь в цикле по `workbook.Worksheets` и добавляйте новый слайд для каждого листа.

**Что изучать дальше?**  

- **Пакетная конверсия:** Обход папки с Excel‑файлами и генерация наборов слайдов для каждого.  
- **Динамические макеты:** Используйте `slide.LayoutSlide` для применения заранее подготовленных шаблонов PowerPoint.  
- **Экспорт только диаграмм:** Сочетайте фрагмент «Export Excel chart as picture» с заполнителями слайдов для более лёгкой презентации.  
- **Продвинутая стилизация:** Добавляйте пользовательские фоны слайдов, переходы или анимацию через Aspose.Slides.

Экспериментируйте — изменяйте DPI, заменяйте `ShapeType.Ellipse` на круглую рамку для изображения, или даже вставляйте несколько картинок на один слайд. Возможности безграничны, когда у вас есть программный контроль над

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}