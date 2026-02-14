---
category: general
date: 2026-02-14
description: كيفية تصدير الجدول المحوري من مصنف Excel إلى PNG باستخدام Aspose.Cells.
  تعلّم كيفية تحميل مصنف Excel، تحويل الجدول المحوري إلى صورة وحفظ صورة الجدول المحوري
  بسهولة.
draft: false
keywords:
- how to export pivot
- export excel pivot
- load excel workbook
- pivot table to png
- save pivot image
language: ar
og_description: كيفية تصدير جدول محوري من Excel إلى PNG باستخدام C#. يوضح لك هذا الدليل
  كيفية تحميل ملف Excel، وتحويل الجدول المحوري إلى PNG، وحفظ صورة الجدول المحوري.
og_title: كيفية تصدير Pivot إلى PNG في C# – دليل كامل
tags:
- Aspose.Cells
- C#
- Excel automation
title: كيفية تصدير Pivot إلى PNG في C# – دليل خطوة بخطوة
url: /ar/net/rendering-and-export/how-to-export-pivot-to-png-in-c-step-by-step-guide/
---

and title.

Now produce final content.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تصدير Pivot إلى PNG في C# – دليل كامل

هل تساءلت يومًا **كيفية تصدير Pivot** من ورقة Excel كملف PNG واضح؟ لست وحدك—غالبًا ما يحتاج المطورون إلى صورة سريعة لجدول Pivot للتقارير أو لوحات التحكم أو مرفقات البريد الإلكتروني. الخبر السار؟ باستخدام Aspose.Cells يمكنك تحميل دفتر Excel، الحصول على أول جدول Pivot، تحويله إلى صورة، و**حفظ صورة Pivot** ببضع أسطر من C# فقط.

في هذا الدرس سنستعرض كل ما تحتاجه: من أساسيات **load excel workbook**، إلى تحويل **pivot table to png**، وأخيرًا حفظ الملف على القرص. في النهاية ستحصل على برنامج مستقل قابل للتنفيذ يمكنك إدراجه في أي مشروع .NET.

---

## ما ستحتاجه

- **.NET 6 أو أحدث** (الكود يعمل على .NET Framework 4.7+ أيضًا)
- حزمة NuGet **Aspose.Cells for .NET** (الإصدار 23.12 وقت الكتابة)
- ملف Excel (`input.xlsx`) يحتوي على جدول Pivot واحد على الأقل
- بيئة Visual Studio أو VS Code التي تشعر بالراحة معها

لا تحتاج إلى مكتبات إضافية، ولا إلى COM interop، ولا إلى تثبيت Excel—Aspose.Cells يتعامل مع كل شيء في الذاكرة.

---

## الخطوة 1 – تحميل دفتر عمل Excel

الأول هو جلب دفتر العمل إلى الذاكرة. هنا يبرز دور كلمة المفتاح **load excel workbook**.

```csharp
using System.Drawing;
using Aspose.Cells;

class PivotExport
{
    static void Main()
    {
        // Step 1: Load the workbook from disk
        // Adjust the path to where your input.xlsx lives
        var workbookPath = @"YOUR_DIRECTORY\input.xlsx";
        Workbook workbook = new Workbook(workbookPath);

        // Grab the first worksheet (you can also select by name)
        Worksheet worksheet = workbook.Worksheets[0];
```

> **لماذا هذا مهم:**  
> تحميل دفتر العمل مرة واحدة يحافظ على سرعة العملية ويتجنب قفل الملف الأصلي. Aspose.Cells يقرأ الملف إلى تدفق مُدار، لذا يمكنك حتى التحميل من مصفوفة بايت أو موقع شبكة لاحقًا.

---

## الخطوة 2 – تحويل جدول Pivot إلى صورة

الآن بعد أن أصبح دفتر العمل في الذاكرة يمكننا الوصول إلى جداول Pivot. توفر الـ API طريقة `ToImage()` التي تُعيد كائن `System.Drawing.Image`.

```csharp
        // Step 2: Find the first pivot table on the worksheet
        if (worksheet.PivotTables.Count == 0)
        {
            System.Console.WriteLine("No pivot tables found on the first worksheet.");
            return;
        }

        // Export the first pivot table as an image
        Image pivotImage = worksheet.PivotTables[0].ToImage();

        // Optional: tweak image quality or size here
        // pivotImage.SetResolution(300, 300);
```

> **نصيحة احترافية:** إذا كان دفتر العمل يحتوي على جداول Pivot متعددة، ما عليك سوى التكرار عبر `worksheet.PivotTables` وتصدير كل واحدة. استدعاء `ToImage()` يحترم العرض الحالي (الفلاتر، slicers، إلخ)، لذا ستحصل على ما يراه المستخدم بالضبط.

---

## الخطوة 3 – حفظ ملف PNG المُولد

أخيرًا، نقوم بحفظ الـ bitmap على القرص. اختيار التحميل `Save` يحدد الصيغة تلقائيًا بناءً على امتداد الملف.

```csharp
        // Step 3: Save the image as PNG
        var outputPath = @"YOUR_DIRECTORY\pivot.png";
        pivotImage.Save(outputPath, System.Drawing.Imaging.ImageFormat.Png);

        System.Console.WriteLine($"Pivot table exported successfully to {outputPath}");
    }
}
```

تشغيل البرنامج ينتج ملف `pivot.png` يبدو تمامًا مثل جدول Pivot داخل Excel. افتحه بأي عارض صور وسترى الصفوف والأعمدة والإجماليات مُرَسَّمة بدقة بكسلية.

---

## معالجة الحالات الشائعة

### جداول Pivot أو أوراق عمل متعددة

إذا كان دفتر العمل يخزن الـ Pivot في ورقة مختلفة، غيّر فهرس الورقة أو استخدم اسم الورقة:

```csharp
Worksheet ws = workbook.Worksheets["SalesData"];
```

ثم قم بالتكرار:

```csharp
foreach (PivotTable pt in ws.PivotTables)
{
    Image img = pt.ToImage();
    img.Save($"pivot_{pt.Name}.png", ImageFormat.Png);
}
```

### جداول Pivot الكبيرة

بالنسبة للـ Pivot الكبيرة قد يكون حجم الصورة الافتراضي ضخمًا. يمكنك التحكم في حجم العرض عن طريق تعديل عامل التكبير للورقة قبل استدعاء `ToImage()`:

```csharp
worksheet.PageSetup.Zoom = 75; // renders at 75 % of original size
```

### إدارة الذاكرة

`System.Drawing.Image` يُطبق `IDisposable`. في الكود الإنتاجي ضع الصورة داخل كتلة `using` لتحرير الموارد الأصلية فورًا:

```csharp
using (Image pivotImage = worksheet.PivotTables[0].ToImage())
{
    pivotImage.Save(outputPath, ImageFormat.Png);
}
```

---

## مثال كامل يعمل

فيما يلي البرنامج الكامل الجاهز للتنفيذ. الصقه في مشروع Console جديد، عدل مسارات الملفات، ثم اضغط **F5**.

```csharp
using System;
using System.Drawing;
using System.Drawing.Imaging;
using Aspose.Cells;

namespace PivotExportDemo
{
    class Program
    {
        static void Main()
        {
            // -----------------------------------------------------------------
            // 1️⃣ Load the Excel workbook (load excel workbook)
            // -----------------------------------------------------------------
            string inputFile = @"YOUR_DIRECTORY\input.xlsx";
            Workbook wb = new Workbook(inputFile);
            Worksheet ws = wb.Worksheets[0]; // first worksheet

            // -----------------------------------------------------------------
            // 2️⃣ Ensure a pivot table exists and export it (how to export pivot)
            // -----------------------------------------------------------------
            if (ws.PivotTables.Count == 0)
            {
                Console.WriteLine("No pivot tables found. Exiting.");
                return;
            }

            // Export the first pivot table as a PNG image (pivot table to png)
            using (Image img = ws.PivotTables[0].ToImage())
            {
                // -----------------------------------------------------------------
                // 3️⃣ Save the pivot image to disk (save pivot image)
                // -----------------------------------------------------------------
                string outputFile = @"YOUR_DIRECTORY\pivot.png";
                img.Save(outputFile, ImageFormat.Png);
                Console.WriteLine($"Pivot exported successfully → {outputFile}");
            }
        }
    }
}
```

**الناتج المتوقع:**  
```
Pivot exported successfully → YOUR_DIRECTORY\pivot.png
```

وسيحتوي الملف `pivot.png` على نسخة بصرية من جدول Pivot الأصلي.

---

## الأسئلة المتكررة

- **هل يعمل هذا مع ملفات .xlsx التي تحتوي على مخططات؟**  
  نعم. طريقة `ToImage()` تهتم فقط بتخطيط جدول Pivot؛ المخططات لا تتأثر.

- **هل يمكنني التصدير إلى JPEG أو BMP بدلاً من PNG؟**  
  بالتأكيد—ما عليك سوى تغيير معامل `ImageFormat` في `Save`. PNG غير مضغوط، لذا نوصي به للبيانات الحادة.

- **ماذا لو كان دفتر العمل محميًا بكلمة مرور؟**  
  حمّله باستخدام نسخة التحميل التي تقبل كلمة المرور:  
  `Workbook wb = new Workbook(inputFile, new LoadOptions { Password = "mySecret" });`

---

## الخلاصة

لقد غطينا الآن **كيفية تصدير Pivot** من ملف Excel إلى صورة PNG باستخدام Aspose.Cells. الخطوات—**load excel workbook**، تحديد **pivot table to png**، و**save pivot image**—بسيطة، لكنها قوية بما يكفي لتدفقات التقارير الواقعية.

بعد ذلك، يمكنك استكشاف:

- أتمتة التصدير لجميع جداول Pivot في مجلد (export excel pivot in bulk)  
- دمج PNG في PDF أو بريد إلكتروني HTML (combine with iTextSharp or Razor)  
- إضافة علامات مائية أو تنسيق مخصص إلى الصورة المصدرة  

جرّب ذلك ودع الصور تتحدث في لوحة التحكم التالية لك.

---

![مثال على نتيجة تصدير Pivot](assets/pivot-export-example.png "مثال على نتيجة تصدير Pivot")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}