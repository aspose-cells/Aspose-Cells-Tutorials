---
category: general
date: 2026-09-27
description: تحديد منطقة الطباعة في Excel وتعلم كيفية تصدير صور PNG للخلايا المحددة.
  يغطي هذا الدليل أيضًا حفظ النطاق كصورة وإضافة صورة إلى ورقة العمل.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- set print area excel
- how to export png
- save range as image
- add picture to worksheet
- export selected cells image
language: ar
lastmod: 2026-09-27
og_description: تحديد منطقة الطباعة في Excel وتصدير PNG باستخدام Aspose.Cells. اتبع
  هذا الدليل خطوة بخطوة لحفظ النطاق كصورة وإضافة صورة إلى ورقة العمل.
og_image_alt: Screenshot showing set print area excel and exported PNG file
og_title: تحديد منطقة الطباعة في إكسل – تصدير PNG باستخدام C#
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Set print area in Excel and learn how to export PNG images of selected
    cells. This guide also covers saving range as image and adding picture to worksheet.
  headline: How to set print area in Excel and export PNG
  type: TechArticle
tags:
- Excel automation
- C#
- Aspose.Cells
title: كيفية تحديد منطقة الطباعة في إكسل وتصدير PNG
url: /ar/net/rendering-and-export/how-to-set-print-area-in-excel-and-export-png/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تعيين منطقة الطباعة في Excel وتصدير PNG

إذا كنت بحاجة إلى **set print area excel** قبل إنشاء صورة، يوضح لك هذا الدليل بالضبط كيفية القيام بذلك. ستتعلم أيضًا **how to export png** من نطاق محدد، **save range as image**، و**add picture to worksheet** في سير عمل واحد قابل للتكرار.

العمل مع Excel برمجيًا يعني غالبًا أنك تريد جزءًا من الخلايا فقط—مثل جدول محوري أو مخطط—أن يتحول إلى صورة. من خلال تعريف منطقة الطباعة أولاً، تضمن أن ملف PNG المُصدَّر يحتوي بالضبط على الخلايا التي تريدها، لا أكثر ولا أقل. يمرّك هذا البرنامج التعليمي عبر كل خطوة، من تحميل المصنف إلى حفظ ملف PNG النهائي، ويشرح لماذا كل إعداد مهم.

## المتطلبات المسبقة

قبل أن تبدأ، تأكد من وجود ما يلي:

* .NET 6.0 أو أحدث مثبت  
* Visual Studio 2022 (أو أي بيئة تطوير C#)  
* حزمة **Aspose.Cells for .NET** عبر NuGet (`Install-Package Aspose.Cells`)  
* ملف Excel (`input.xlsx`) موجود في مسار معروف  

هذه المتطلبات تضمن تشغيل الكود دون الحاجة إلى إعدادات إضافية.

## الخطوة 1: تحميل المصنف الذي تريد العمل معه

```csharp
using Aspose.Cells;
using System.Drawing.Imaging;

// Load the workbook from disk
Workbook workbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");
```

فئة `Workbook` تمثل ملف Excel بالكامل. تحميلها أولاً يمنحك الوصول إلى أوراق العمل، الخلايا، وإعدادات إعداد الصفحة.

## الخطوة 2: **set print area excel** للنطاق المستهدف

```csharp
// Define the range you want to capture
string printArea = "A1:G20";

// Apply the range as the print area on the first worksheet
workbook.Worksheets[0].PageSetup.PrintArea = printArea;
```

تحديد **منطقة الطباعة** يخبر Excel (وAspose.Cells) أي الخلايا تنتمي إلى الصفحة القابلة للطباعة. عندما تقوم لاحقًا بتصدير الورقة كصورة، يتم رسم هذا النطاق فقط، وهو أمر أساسي للحصول على **export selected cells image** نظيفة.

## الخطوة 3: تكوين خيارات تصدير الصورة – **how to export png**

```csharp
ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
{
    ImageFormat = ImageFormat.Png,   // PNG ensures lossless quality
    OnePagePerSheet = true           // Export the defined print area as a single page
};
```

`ImageOrPrintOptions` يتحكم في تنسيق الإخراج. باختيار `ImageFormat.Png`، تضمن صورة ذات دقة عالية وخلفية شفافة تعمل جيدًا في الويب وسطح المكتب.

## الخطوة 4: إنشاء صورة من النطاق المحدد و**add picture to worksheet**

```csharp
// Create a picture object from the selected range
Picture picture = workbook.Worksheets[0].Pictures.Add(
    0,                                     // top‑left row index where the picture will be placed
    0,                                     // top‑left column index where the picture will be placed
    workbook.Worksheets[0].Cells.CreateRange(printArea));
```

طريقة `Pictures.Add` تُدرج صورة جديدة في ورقة العمل. بتمرير النطاق الذي تم إنشاؤه في الخطوة 2، تقوم بـ **save range as image** مباشرةً على الورقة، وهو مفيد إذا احتجت لاحقًا الإشارة إلى الصورة في أجزاء أخرى من المصنف.

## الخطوة 5: **Save the picture as an image file** – إكمال سير عمل **export selected cells image**

```csharp
// Save the picture to disk as a PNG file
picture.Save(@"YOUR_DIRECTORY\selected_range.png", imageOptions);
```

استدعاء `Save` يكتب الصورة إلى نظام الملفات باستخدام الخيارات المحددة في الخطوة 3. الملف الناتج `selected_range.png` يحتوي بالضبط على الخلايا التي حُدِّدَت بأمر **set print area excel**.

## مثال كامل قابل للتنفيذ

جمع كل الأجزاء معًا يمنحك برنامجًا مختصرًا يمكنك وضعه في أي تطبيق Console:

```csharp
using System;
using Aspose.Cells;
using System.Drawing.Imaging;

class ExportExcelRangeAsPng
{
    static void Main()
    {
        // 1️⃣ Load the workbook
        Workbook workbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");

        // 2️⃣ Set print area excel
        string printArea = "A1:G20";
        workbook.Worksheets[0].PageSetup.PrintArea = printArea;

        // 3️⃣ Configure how to export png
        ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
        {
            ImageFormat = ImageFormat.Png,
            OnePagePerSheet = true
        };

        // 4️⃣ Add picture to worksheet (save range as image)
        Picture picture = workbook.Worksheets[0].Pictures.Add(
            0,
            0,
            workbook.Worksheets[0].Cells.CreateRange(printArea));

        // 5️⃣ Export selected cells image
        picture.Save(@"YOUR_DIRECTORY\selected_range.png", imageOptions);

        Console.WriteLine("PNG exported successfully to YOUR_DIRECTORY\\selected_range.png");
    }
}
```

### النتيجة المتوقعة

تشغيل البرنامج يطبع:

```
PNG exported successfully to YOUR_DIRECTORY\selected_range.png
```

وستجد ملف `selected_range.png` الذي يظهر فقط الخلايا من A1 إلى G20 من `input.xlsx`.

## الأخطاء الشائعة وكيفية تجنّبها

| المشكلة | السبب | الحل |
|-------|----------------|-----|
| الصورة المُصدَّرة تحتوي على الورقة بالكامل | لم يتم تعريف منطقة طباعة | تأكد من **set print area excel** قبل إنشاء الصورة |
| PNG غير واضح | DPI الافتراضي منخفض | عيّن `imageOptions.DpiX` و `imageOptions.DpiY` إلى قيمة أعلى (مثال: 300) |
| خطأ ملف غير موجود | مسار الدليل غير صحيح | استخدم `Path.Combine` أو تحقق من وجود المجلد |
| الصورة تظهر مُزاحة | مؤشرات الصف/العمود غير صحيحة | المعاملان الأولان لـ `Pictures.Add` هما الخلية العلوية اليسرى التي تُوضع فيها الصورة؛ احتفظ بهما على `0,0` لتصدير نظيف |

## نصيحة احترافية: تصدير نطاقات متعددة في تشغيل واحد

إذا كنت بحاجة إلى **export selected cells image** لعدة مناطق، كرّر الخطوات 2‑5 داخل حلقة، مع تغيير `printArea` في كل تكرار. تذكّر إعطاء كل صورة اسم ملف فريد، وإلا سيُستبدل الملف السابق بالحفظ اللاحق.

## الخاتمة

أنت الآن تعرف كيف **set print area excel**، وتُكوّن **how to export png**، و**save range as image**، و**add picture to worksheet** باستخدام Aspose.Cells. هذا الحل المتكامل يتيح لك تحويل أي مجموعة خلايا إلى PNG عالي الجودة ببضع أسطر من كود C#.

الخطوات التالية التي قد تستكشفها:

* إضافة حدود أو علامات مائية إلى PNG المُصدَّر (ابحث عن *add picture to worksheet* مع تنسيق)
* تصدير مباشرة إلى PDF لتقارير قابلة للطباعة (*export selected cells image* → سير عمل PDF)
* أتمتة العملية لعدة مصنفات في مهمة دفعة

لا تتردد في تجربة نطاقات مختلفة، إعدادات DPI، أو صيغ صور لتناسب احتياجات مشروعك. برمجة سعيدة!

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة شاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [Set Print Area in Excel and Export to PowerPoint – Step‑by‑Step Guide](/cells/english/net/converting-excel-files-to-other-formats/set-print-area-in-excel-and-export-to-powerpoint-step-by-ste/)
- [Export Excel Print Area to HTML with Aspose.Cells Java](/cells/english/java/workbook-operations/export-excel-print-area-html-aspose-cells-java/)
- [How to Set a Print Area in Excel Using Aspose.Cells for .NET](/cells/english/net/headers-footers/set-print-area-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}