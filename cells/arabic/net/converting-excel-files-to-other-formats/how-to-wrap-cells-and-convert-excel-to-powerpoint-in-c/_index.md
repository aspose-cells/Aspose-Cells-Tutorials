---
category: general
date: 2026-09-18
description: كيفية تغليف الخلايا في مصنف Excel وحفظه كملف PowerPoint. تعلم استخدام
  WRAPCOLS، إنشاء ورقة عمل المصنف، وتصدير إلى PPTX.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to wrap cells
- convert excel to powerpoint
- save excel as powerpoint
- how to use wrapcols
- create workbook worksheet
language: ar
lastmod: 2026-09-18
og_description: كيفية لف الخلايا في Excel وتصدير المصنف كملف PowerPoint قابل للتحرير
  باستخدام C#. اتبع الدليل خطوة بخطوة لإتقان WRAPCOLS وإنشاء أوراق عمل المصنف.
og_image_alt: Diagram showing how to wrap cells in Excel before exporting to PowerPoint
og_title: كيفية تغليف الخلايا وتحويل Excel إلى PowerPoint باستخدام C#
schemas:
- author: Aspose
  dateModified: '2026-09-18'
  description: How to wrap cells in an Excel workbook and save it as a PowerPoint
    file. Learn to use WRAPCOLS, create workbook worksheet, and export to PPTX.
  headline: How to wrap cells and convert Excel to PowerPoint in C#
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
- PowerPoint export
title: كيفية تغليف الخلايا وتحويل Excel إلى PowerPoint في C#
url: /ar/net/converting-excel-files-to-other-formats/how-to-wrap-cells-and-convert-excel-to-powerpoint-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية التفاف الخلايا وتحويل Excel إلى PowerPoint باستخدام C#

إذا كنت بحاجة إلى **how to wrap cells** في ورقة Excel ثم تحويل تلك الورقة إلى عرض تقديمي PowerPoint، يوضح لك هذا الدليل حلاً كاملاً وجاهزًا للتنفيذ. بحلول نهاية الجملتين الأوليين ستعرف بالضبط أي استدعاءات API تقوم باللف وأي طريقة تحفظ الملف كملف PPTX.

سنستخدم Aspose.Cells for .NET، مكتبة تتيح لك التعامل مع دفاتر Excel دون الحاجة إلى تثبيت Microsoft Office. يغطي الدليل **convert Excel to PowerPoint**، ويظهر **how to use WRAPCOLS**، ويشرح أفضل الممارسات لـ **create workbook worksheet**. لا توجد أدوات خارجية مطلوبة—فقط بيئة تطوير .NET.

## المتطلبات المسبقة

- .NET 6.0 أو أحدث (الكود يعمل أيضًا مع .NET Framework 4.6+)
- حزمة NuGet الخاصة بـ Aspose.Cells for .NET (`Install-Package Aspose.Cells`)
- إلمام أساسي بـ C# ومفهوم أوراق العمل
- بيئة تطوير متكاملة مثل Visual Studio أو VS Code

> **نصيحة احترافية:** استخدم ترخيص التقييم المجاني لـ Aspose.Cells أثناء التجربة؛ استبدله بترخيص كامل قبل الإنتاج.

## الخطوة 1: إنشاء دفتر عمل وإضافة ورقة عمل

أول شيء يجب عليك **create workbook worksheet** هو إنشاء كائن `Workbook`. بشكل افتراضي، تقوم Aspose.Cells بإنشاء ورقة عمل واحدة (الفهرس 0)، والتي سنستخدمها في العرض.

```csharp
using System;
using Aspose.Cells;

class WrapAndExport
{
    static void Main()
    {
        // Step 1: Initialize a new workbook (creates one worksheet automatically)
        Workbook workbook = new Workbook();

        // Reference the first worksheet for later operations
        Worksheet ws = workbook.Worksheets[0];
```

**لماذا هذا مهم:** تهيئة دفتر العمل يمنحك لوحة نظيفة. ورقة العمل الافتراضية هي بالفعل جزء من مجموعة `Worksheets`، لذا لا تحتاج إلى استدعاء `Add()` إلا إذا كنت تريد أوراقًا إضافية.

## الخطوة 2: تعبئة النطاق المصدر (A2:A10)

قبل أن نتمكن من **how to wrap cells**، نحتاج إلى بعض البيانات لللف. هذه الخطوة تملأ الخلايا من A2 إلى A10 بنص تجريبي.

```csharp
        // Fill cells A2:A10 with a long string to demonstrate wrapping
        for (int i = 2; i <= 10; i++)
        {
            ws.Cells[$"A{i}"].PutValue(
                "Lorem ipsum dolor sit amet, consectetur adipiscing elit. " +
                "Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.");
        }
```

**حالة حافة:** إذا كان النطاق المصدر فارغًا، فإن `WRAPCOLS` تُرجع `#VALUE!`. تأكد دائمًا من أن النطاق يحتوي على خلية واحدة على الأقل غير فارغة.

## الخطوة 3: تطبيق صيغة WRAPCOLS

الآن نجيب على السؤال الأساسي **how to use WRAPCOLS**. الصيغة تأخذ نطاقًا عموديًا وتوزعه عبر عدد محدد من الأعمدة. نكتب الصيغة في الخلية `A1`؛ المصفوفة الناتجة ستنتشر تلقائيًا إلى الخلايا المجاورة.

```csharp
        // Step 3: Apply WRAPCOLS to wrap A2:A10 into 3 columns, result starts at A1
        ws.Cells["A1"].Formula = "=WRAPCOLS(A2:A10,3)";
```

**ما يحدث في الخلفية:** `WRAPCOLS` تقيم النطاق المصدر، تقسم العناصر بالتساوي (أو بأقرب ما يمكن) بين الأعمدة المستهدفة، وتكتب القيم في كتلة مستطيلة. حجم الكتلة ديناميكي، لذا لا تحتاج إلى تعريف النطاق الوجهة مسبقًا.

## الخطوة 4: حفظ دفتر العمل كملف PowerPoint قابل للتحرير

أخيرًا، نتعامل مع **convert Excel to PowerPoint** و**save Excel as PowerPoint**. يمكن لـ Aspose.Cells تصدير ورقة العمل مباشرةً إلى PPTX، مع الحفاظ على التخطيط كشكل قابل للتحرير.

```csharp
        // Step 4: Export the worksheet to an editable PPTX presentation
        string outputPath = @"YOUR_DIRECTORY\ChartEditable.pptx";
        workbook.Save(outputPath, SaveFormat.Pptx);

        Console.WriteLine($"Workbook exported successfully to {outputPath}");
    }
}
```

**لماذا PPTX؟** يحتوي PowerPoint المُولد على شريحة واحدة مع الخلايا الملتفة معروضة كجدول. يمكنك فتح الملف في Microsoft PowerPoint، تعديل النص، تغيير الأنماط، أو إضافة شرائح إضافية—كل شيء يظل قابلًا للتحرير بالكامل.

### النتيجة المتوقعة

- **جانب Excel:** الخلية `A1` تُظهر مصفوفة من 3 أعمدة للسلاسل الطويلة الأصلية، كل عمود يحتوي تقريبًا على نفس عدد الصفوف.
- **جانب PowerPoint:** عند فتح `ChartEditable.pptx` يتم عرض شريحة تحتوي على جدول يعكس التخطيط الملتف. يمكن تحديد الجدول، تغيير حجمه، أو تحريره مثل أي كائن PowerPoint أصلي.

## الاختلافات الشائعة وما يجب الانتباه إليه

| السيناريو | التعديل |
|----------|------------|
| **اللف إلى أعمدة أكثر** | غيّر الوسيط الثاني لـ `WRAPCOLS`، مثال: `=WRAPCOLS(A2:A10,5)`. |
| **اللف لنطاق مختلف** | حدّث مرجع الصيغة، مثال: `=WRAPCOLS(B2:B15,2)`. |
| **تصدير جزء فقط من الورقة** | استخدم `Worksheet.ExportDataTable` لاستخراج `DataTable` ثم واجهات برمجة `Presentation` لإنشاء PPTX مخصص. |
| **أوراق عمل كبيرة ( > 10 000 صف )** | فكّر في تقسيم التصدير إلى عدة شرائح لتجنب اختناقات الأداء. |

> **احذر من:** تصدير PPTX الافتراضي يعرض ورقة العمل كصورة واحدة عندما يحتوي دفتر العمل على مخططات. استخدام `WRAPCOLS` يضمن بقاء البيانات كجدول، مما يبقى قابلًا للتحرير.

## الكود الكامل للنسخ السريع

```csharp
using System;
using Aspose.Cells;

class WrapAndExport
{
    static void Main()
    {
        // Create a new workbook (contains one default worksheet)
        Workbook workbook = new Workbook();
        Worksheet ws = workbook.Worksheets[0];

        // Populate A2:A10 with sample long text
        for (int i = 2; i <= 10; i++)
        {
            ws.Cells[$"A{i}"].PutValue(
                "Lorem ipsum dolor sit amet, consectetur adipiscing elit. " +
                "Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.");
        }

        // Apply WRAPCOLS to wrap the range into 3 columns, result starts at A1
        ws.Cells["A1"].Formula = "=WRAPCOLS(A2:A10,3)";

        // Save as an editable PowerPoint presentation
        string outputPath = @"YOUR_DIRECTORY\ChartEditable.pptx";
        workbook.Save(outputPath, SaveFormat.Pptx);

        Console.WriteLine($"Workbook exported successfully to {outputPath}");
    }
}
```

احفظ الملف باسم `Program.cs`، استعد حزمة NuGet، ثم شغّله:

```bash
dotnet run
```

يجب أن ترى رسالة وحدة التحكم التي تؤكد التصدير، وسيظهر ملف PPTX في المجلد المحدد.

## الخلاصة

أنت الآن تعرف **how to wrap cells** في ورقة عمل Excel، **how to use WRAPCOLS**، والخطوات الدقيقة لـ **convert Excel to PowerPoint** عبر **save excel as powerpoint** باستخدام Aspose.Cells. الحل الكامل يوضح **create workbook worksheet**، يطبق صيغة اللف، وينتج ملف PPTX قابل للتحرير جاهز لتعديلات العرض.

### الخطوات التالية

- استكشف وظائف Excel الأخرى (مثل `TRANSPOSE`، `FILTER`) قبل التصدير.
- دمج أوراق عمل متعددة في مجموعة شرائح PowerPoint متعددة باستخدام حلقة.
- أضف عناوين شرائح مخصصة أو علامة تجارية بدمج Aspose.Slides بعد التصدير.

لا تتردد في تجربة عدد أعمدة مختلف، نطاقات مصدر مختلفة، أو حتى دمج المخططات والجداول في نفس ملف PPTX. برمجة سعيدة!

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مصدر يتضمن أمثلة كود كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [كيفية تحويل Excel إلى PowerPoint باستخدام Aspose.Cells for .NET: دليل كامل](/cells/english/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)
- [كيفية التفاف النص في Excel باستخدام Aspose.Cells for .NET | درس تنسيق](/cells/english/net/formatting/wrap-text-excel-aspose-cells-net/)
- [تصدير خصائص دفتر عمل Excel وورقة العمل إلى HTML باستخدام Aspose.Cells for .NET](/cells/english/net/workbook-operations/export-excel-properties-to-html-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}