---
category: general
date: 2026-05-04
description: كيفية تحديث Pivot في C# وتصديره كملف PNG، ثم إدراج الصورة في ورقة العمل.
  اتبع هذا الدليل خطوة بخطوة مع الكود الكامل.
draft: false
keywords:
- how to refresh pivot
- how to export pivot
- insert image into worksheet
- refresh pivot table code
- load excel workbook c#
language: ar
og_description: كيفية تحديث Pivot في C#؟ تعلم تصدير جدول Pivot كصورة وإدراجه في ورقة
  عمل مع أمثلة شاملة للكود.
og_title: كيفية تحديث Pivot في C# – تصدير وإدراج كصورة
tags:
- C#
- Aspose.Cells
- Excel Automation
title: كيفية تحديث Pivot في C# – التصدير والإدراج كصورة
url: /ar/net/pivot-tables/how-to-refresh-pivot-in-c-export-and-insert-as-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تحديث Pivot في C# – التصدير والإدراج كصورة

كيفية تحديث Pivot في C# هي عقبة شائعة عندما تقوم بأتمتة تقارير Excel. في هذا الدليل ستتعرف بالضبط **على كيفية تحديث Pivot**، وتصديره كملف PNG، وإدراج تلك الصورة في عنصر نائب داخل ورقة العمل — كل ذلك ببرنامج واحد قابل للتنفيذ.

إذا كنت تتساءل أيضًا *كيف تصدر Pivot* أو تحتاج إلى **إدراج صورة في ورقة العمل**، فأنت في المكان المناسب. سنستعرض كل سطر من الشيفرة، نشرح سبب أهميته، وحتى نتطرق إلى بعض الحالات الخاصة التي قد تواجهها في مشاريع العالم الحقيقي.

---

## ما الذي ستحتاجه

قبل أن نبدأ، تأكد من توفر ما يلي:

- **Aspose.Cells for .NET** (المكتبة التي توفر `Workbook`، `Worksheet`، `ImageOrPrintOptions`، إلخ). يمكنك الحصول عليها من NuGet: `Install-Package Aspose.Cells`.
- .NET 6 أو أحدث (الكود أدناه يستهدف .NET 6، لكن أي نسخة حديثة تعمل كذلك).
- فهم أساسي للغة C# وتعامل مع الملفات — لا شيء معقد.

هذا كل ما تحتاجه. لا مكتبات DLL إضافية، لا تفاعل COM، مجرد تطبيق كونسول C# نظيف.

---

## الخطوة 1 – تحميل ملف Excel بأسلوب C#

أولاً، نحتاج إلى فتح الملف المصدر. هنا يأتي جزء **load excel workbook c#**.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Load the workbook from disk
        string inputPath = @"YOUR_DIRECTORY\input.xlsx";
        Workbook workbook = new Workbook(inputPath);

        // Grab the first worksheet (index 0)
        Worksheet worksheet = workbook.Worksheets[0];
```

> **لماذا؟**  
> تحميل المصنف يمنحنا الوصول إلى أوراقه، وجداول Pivot، وعناصر الصورة. إذا لم يُعثر على الملف، ستطرح Aspose استثناء `FileNotFoundException` واضح، يمكنك التقاطه لتوفير واجهة مستخدم أكثر ودية.

---

## الخطوة 2 – إعداد خيارات الصورة لتصدير Pivot

الآن نخبر Aspose كيف نريد أن تبدو الصورة المصدرة. هذا هو جوهر **how to export pivot**.

```csharp
        // Step 2: Set up image export options – PNG is lossless and widely supported
        ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
        {
            SaveFormat = SaveFormat.Png,
            // Optional: tweak resolution for sharper images
            HorizontalResolution = 300,
            VerticalResolution = 300
        };
```

> **نصيحة احترافية:**  
> إذا كنت تحتاج إلى JPEG لتقليل حجم الملف، غيّر `SaveFormat.Png` إلى `SaveFormat.Jpeg` واضبط `Quality` وفقًا لذلك.

---

## الخطوة 3 – كود تحديث جدول Pivot

جدول Pivot قديم يعرض بيانات قديمة. تحديثه يضمن أن الصورة تعكس أحدث الأرقام.

```csharp
        // Step 3: Refresh the first pivot table in the worksheet
        if (worksheet.PivotTables.Count > 0)
        {
            worksheet.PivotTables[0].Refresh();
        }
        else
        {
            Console.WriteLine("No pivot tables found on the first worksheet.");
            return;
        }
```

> **لماذا نحدث؟**  
> جداول Pivot تخزن نسخة مؤقتة من البيانات المصدر عند إنشائها. إذا تغيرت ورقة العمل الأساسية (مثلاً أضيفت صفوف جديدة)، يصبح التخزين المؤقت غير محدث. استدعاء `Refresh()` يجبر Aspose على إعادة استعلام النطاق المصدر، مما يضمن أن الصورة المصدرة لا تُظهر أرقامًا قديمة.

---

## الخطوة 4 – تحويل Pivot المحدث إلى صورة

هذه هي السطر السحري الذي فعليًا **export pivot** إلى مصفوفة بايت.

```csharp
        // Step 4: Export the refreshed pivot table as an image
        byte[] pivotImage = worksheet.PivotTables[0].ToImage(imageOptions);
```

> **ما ستحصل عليه:**  
> `pivotImage` الآن يحتوي على صورة مشفرة بصيغة PNG لجدول Pivot، جاهزة للكتابة إلى القرص أو تضمينها في مكان آخر.

---

## الخطوة 5 – إدراج الصورة في ورقة العمل

هنا نطبق **insert image into worksheet**. سنضع الصورة في أول عنصر نائب للصور (إن وجد).

```csharp
        // Step 5: Insert the image into the first picture placeholder
        if (worksheet.Pictures.Count > 0)
        {
            worksheet.Pictures[0].ImageBytes = pivotImage;
        }
        else
        {
            // If no placeholder exists, add a new picture at cell A1
            int pictureIndex = worksheet.Pictures.Add(0, 0, pivotImage).Index;
            Console.WriteLine($"Added new picture at index {pictureIndex}.");
        }
```

> **لماذا نستخدم عنصرًا نائبًا؟**  
> العديد من قوالب Excel تأتي مع شكل صورة مُنسق مسبقًا (حجم، حد، موضع). باستهداف `Pictures[0]` نحافظ على تخطيط القالب. إذا لم يكن القالب يحتوي على عنصر نائب، فإن النسخة الاحتياطية تنشئ صورة جديدة مُثبتة في الخلية A1.

---

## الخطوة 6 – حفظ المصنف (اختياري)

أخيرًا، نجعل التغييرات دائمة. يمكنك الكتابة فوق الملف الأصلي أو حفظه في ملف جديد.

```csharp
        // Step 6: Save the updated workbook
        string outputPath = @"YOUR_DIRECTORY\output.xlsx";
        workbook.Save(outputPath);

        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

> **النتيجة المتوقعة:**  
> افتح `output.xlsx` وسترى جدول Pivot محدثًا، مُصدّرًا كصورة PNG واضحة، ومعروضًا داخل أول فتحة صورة. باقي المصنف يبقى دون تغيير.

---

## مثال كامل جاهز للتنفيذ (انسخه‑الصقه)

فيما يلي كتلة الشيفرة الكاملة التي يمكنك وضعها في مشروع كونسول جديد. لا توجد أجزاء مفقودة.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Load the workbook
        string inputPath = @"YOUR_DIRECTORY\input.xlsx";
        Workbook workbook = new Workbook(inputPath);
        Worksheet worksheet = workbook.Worksheets[0];

        // Configure image export options (PNG, 300 DPI)
        ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
        {
            SaveFormat = SaveFormat.Png,
            HorizontalResolution = 300,
            VerticalResolution = 300
        };

        // Refresh the first pivot table
        if (worksheet.PivotTables.Count == 0)
        {
            Console.WriteLine("No pivot tables found.");
            return;
        }
        worksheet.PivotTables[0].Refresh();

        // Export pivot to PNG byte array
        byte[] pivotImage = worksheet.PivotTables[0].ToImage(imageOptions);

        // Insert the image into a picture placeholder or add a new picture
        if (worksheet.Pictures.Count > 0)
        {
            worksheet.Pictures[0].ImageBytes = pivotImage;
        }
        else
        {
            worksheet.Pictures.Add(0, 0, pivotImage);
        }

        // Save the workbook
        string outputPath = @"YOUR_DIRECTORY\output.xlsx";
        workbook.Save(outputPath);

        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

شغّل البرنامج، افتح الملف الناتج، وتأكد من أن Pivot يعكس أحدث البيانات ويظهر كصورة عالية الدقة.

---

## الأسئلة المتكررة والحالات الخاصة

| السؤال | الجواب |
|----------|--------|
| **ماذا لو كان للمصنف عدة أوراق عمل؟** | عدل `workbook.Worksheets[0]` إلى الفهرس أو الاسم المناسب (`workbook.Worksheets["Sheet2"]`). |
| **هل يمكنني تصدير عدة جداول Pivot؟** | كرّر الحلقة عبر `worksheet.PivotTables` وطبق الخطوتين 3‑4 لكل جدول. احفظ كل صورة في عنصر نائب منفصل أو اجمعها في ورقة واحدة. |
| **ماذا عن جداول Pivot الكبيرة التي تستهلك الذاكرة؟** | استخدم `ImageOrPrintOptions` بدقة DPI أقل أو صدّر إلى JPEG لتقليل حجم مصفوفة البايت. |
| **هل يجب عليّ تحرير أي موارد؟** | كائنات Aspose مُدارة؛ لا يلزم استخدام `using`، لكن يمكنك وضع `Workbook` داخل كتلة `using` إذا رغبت في تنظيف موارد بشكل حتمي. |
| **هل هذا متوافق مع .NET Core؟** | نعم. Aspose.Cells يدعم .NET Core، .NET 5/6، و .NET Framework. فقط أضف الحزمة المناسبة من NuGet. |

---

## نصائح وممارسات أفضل

- **تحقق من المسارات**: استخدم `Path.Combine` و `Environment.GetFolderPath` لتجنب الفواصل الصلبة.
- **معالجة الأخطاء**: غلف كامل جسم `Main` بكتلة `try/catch` وسجل `Exception.Message` للسكربتات الإنتاجية.
- **تصميم القالب**: ضع شكل صورة شفاف في المكان الذي تريد أن تظهر فيه صورة Pivot؛ هذا يحافظ على عرض الأعمدة وارتفاع الصفوف.
- **الأداء**: إذا كنت تحتاج فقط إلى الصورة، يمكنك تخطي حفظ المصنف تمامًا وكتابة `pivotImage` إلى ملف PNG منفصل.

---

## الخلاصة

أنت الآن تعرف **كيفية تحديث Pivot** في C#، وتصدير العرض المحدث كصورة، و**إدراج الصورة في ورقة العمل** بسلاسة. الحل الكامل — تحميل المصنف، ضبط خيارات التصدير، تحديث Pivot، تحويله إلى PNG، وحفظ الملف — يغطي كامل سير العمل الذي طلبته.

مستعد للتحدي التالي؟ جرّب دمج **how to export pivot** مع معالجة دفعات من الملفات المتعددة، أو استكشف **refresh pivot table code** لمصادر بيانات ديناميكية مثل قواعد البيانات أو ملفات CSV. النمط نفسه ينطبق: تحميل، تحديث، تصدير، إدراج، حفظ.

برمجة سعيدة، ولتظل أتمتة Excel لديك دائمًا محدثة ومثالية بصريًا!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}