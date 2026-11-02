---
category: general
date: 2026-08-17
description: حفظ Excel كـ PowerPoint باستخدام C# – دليل خطوة بخطوة لتحويل ملفات XLSX،
  وجعل مربعات النص قابلة للتحرير، وإنشاء مخرجات PPTX.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- save excel as powerpoint
- convert excel to powerpoint
- how to convert xlsx
- make textbox editable
- how to edit textboxes
language: ar
lastmod: 2026-08-17
og_description: احفظ ملف Excel كـ PowerPoint في C# مع مثال كامل للكود. تعلم كيفية
  تحويل XLSX، وجعل صناديق النص قابلة للتحرير، وتصدير إلى PPTX.
og_image_alt: Screenshot showing Excel data saved as a PowerPoint slide
og_title: حفظ Excel كـ PowerPoint في C# – دليل التحويل الكامل
schemas:
- author: Aspose
  dateModified: '2026-08-17'
  description: Save Excel as PowerPoint with C# – step‑by‑step guide to convert XLSX
    files, make textboxes editable, and generate PPTX output.
  headline: How to save Excel as PowerPoint using C# and Aspose.Cells
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel-to-PowerPoint
title: كيفية حفظ ملف Excel كـ PowerPoint باستخدام C# و Aspose.Cells
url: /ar/net/converting-excel-files-to-other-formats/how-to-save-excel-as-powerpoint-using-c-and-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية حفظ Excel كـ PowerPoint باستخدام C# و Aspose.Cells

إذا كنت بحاجة إلى **حفظ Excel كـ PowerPoint** في مشروع .NET، يوضح لك هذا الدليل حلاً كاملاً جاهزًا للتنفيذ. ستتعرف على كيفية تحميل دفتر عمل XLSX، وجعل كل مربع نص في الورقة قابلاً للتحرير، وتصدير النتيجة إلى ملف PPTX—كل ذلك ببضع أسطر من C#.

تحويل Excel إلى PowerPoint هو طلب شائع لتقارير اللوحات، عروض الشرائح، أو إنشاء عروض تقديمية تلقائيًا. يغطي هذا البرنامج التعليمي أيضًا **كيفية تحرير مربعات النص** برمجيًا، حتى تتمكن من تخصيص محتوى الشريحة قبل الحفظ.

## المتطلبات المسبقة

قبل أن تبدأ، تأكد من وجود ما يلي:

* .NET 6.0 (أو أحدث) SDK مثبت  
* بيئة تطوير مثل Visual Studio 2022 أو VS Code  
* ترخيص Aspose.Cells for .NET (أو مفتاح تقييم مجاني) – حمّل من [موقع Aspose](https://products.aspose.com/cells/net/)  
* ملف `input.xlsx` الذي تريد تحويله  

> **نصيحة احترافية:** إذا استخدمت نسخة التقييم المجانية، سيحتوي ملف PPTX الناتج على علامة مائية. النسخة المرخصة تزيلها.

## الخطوة 1: تثبيت حزمة NuGet الخاصة بـ Aspose.Cells

افتح الطرفية في مجلد المشروع وشغّل الأمر التالي:

```bash
dotnet add package Aspose.Cells
```

يضيف هذا التجميع `Aspose.Cells`، الذي يوفر الفئات `Workbook` و `Worksheet` و `Shape` اللازمة للتحويل.

## الخطوة 2: إنشاء هيكل تطبيق وحدة تحكم

أنشئ مشروع وحدة تحكم جديد (إذا لم يكن لديك واحد بالفعل):

```bash
dotnet new console -n ExcelToPptxDemo
cd ExcelToPptxDemo
```

استبدل ملف `Program.cs` المُولد بالكود الموضح في الخطوات التالية.

## الخطوة 3: تحميل دفتر العمل وتحديد الورقة الأولى

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Drawing;

class Program
{
    static void Main()
    {
        // Load the workbook from a file – adjust the path to your environment
        string inputPath = @"YOUR_DIRECTORY\input.xlsx";
        Workbook workbook = new Workbook(inputPath);

        // Get the first worksheet in the workbook
        Worksheet worksheet = workbook.Worksheets[0];
```

**لماذا هذا مهم:**  
`Workbook` يقرأ ملف Excel إلى الذاكرة، بينما `Worksheet` يمنحك الوصول إلى خلايا الورقة، المخططات، والأشكال. عادةً ما تكون الورقة الأولى هي التقرير الافتراضي الذي تريد عرضه.

## الخطوة 4: جعل كل مربع نص في الورقة قابلاً للتحرير

```csharp
        // Iterate through all shapes on the worksheet
        foreach (Shape shapeItem in worksheet.Shapes)
        {
            // Check if the shape is a textbox (ShapeType.TextBox)
            if (shapeItem.Type == ShapeType.TextBox)
            {
                // The IsEditable property was added in Aspose.Cells 25.11
                shapeItem.TextBox.IsEditable = true;
            }
        }
```

**لماذا تحتاج هذا:**  
بشكل افتراضي، تكون مربعات النص المستوردة من Excel للقراءة فقط عند عرضها في PowerPoint. ضبط `IsEditable = true` يتيح لك (أو لمستخدمي PowerPoint لاحقًا) تعديل النص مباشرةً على الشريحة.

## الخطوة 5: حفظ دفتر العمل كعرض تقديمي PowerPoint

```csharp
        // Define the output path for the PPTX file
        string outputPath = @"YOUR_DIRECTORY\output.pptx";

        // Save the workbook as a PowerPoint presentation
        workbook.Save(outputPath, SaveFormat.Pptx);

        Console.WriteLine($"Conversion complete. PPTX saved to: {outputPath}");
    }
}
```

**ما يحدث في الخلفية:**  
`Workbook.Save` يكتشف قيمة التعداد `SaveFormat.Pptx` ويحوّل تخطيط ورقة Excel—بما في ذلك الصفوف، الأعمدة، المخططات، ومربعات النص القابلة للتحرير الآن—إلى كائنات شريحة PowerPoint.

## الشيفرة الكاملة (قابلة للتنفيذ)

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Drawing;

class Program
{
    static void Main()
    {
        // Step 1: Load the workbook from a file
        string inputPath = @"YOUR_DIRECTORY\input.xlsx";
        Workbook workbook = new Workbook(inputPath);

        // Step 2: Get the first worksheet in the workbook
        Worksheet worksheet = workbook.Worksheets[0];

        // Step 3: Make every textbox on the sheet editable (property added in version 25.11)
        foreach (Shape shapeItem in worksheet.Shapes)
        {
            if (shapeItem.Type == ShapeType.TextBox)
            {
                shapeItem.TextBox.IsEditable = true;
            }
        }

        // Step 4: Save the workbook as a PowerPoint presentation
        string outputPath = @"YOUR_DIRECTORY\output.pptx";
        workbook.Save(outputPath, SaveFormat.Pptx);

        Console.WriteLine($"Conversion complete. PPTX saved to: {outputPath}");
    }
}
```

### النتيجة المتوقعة

عند تشغيل البرنامج (`dotnet run`)، يجب أن ترى:

```
Conversion complete. PPTX saved to: YOUR_DIRECTORY\output.pptx
```

فتح `output.pptx` في Microsoft PowerPoint سيعرض شريحة تعكس ورقة Excel الأصلية. يمكن تحرير جميع مربعات النص مباشرةً بالنقر المزدوج عليها.

## أسئلة شائعة وحالات خاصة

| السؤال | الجواب |
|----------|--------|
| **هل يمكنني تحويل ورقة عمل محددة بدلاً من الأولى؟** | نعم. استبدل `workbook.Worksheets[0]` بـ `workbook.Worksheets["SheetName"]` أو أي فهرس تحتاجه. |
| **ماذا لو كان دفتر العمل يحتوي على عدة أوراق؟** | استدعِ `workbook.Save` مرة لكل ورقة عمل، مع توفير اسم ملف PPTX مميز لكل منها، أو اجمعها في عرض تقديمي واحد باستخدام كائنات `Presentation` من Aspose.Slides. |
| **هل سيتم الحفاظ على المخططات؟** | Aspose.Cells يحول مخططات Excel إلى كائنات مخطط PowerPoint تلقائيًا. لا يلزم أي كود إضافي. |
| **كيف أغيّر حجم الشريحة؟** | بعد `workbook.Save`، يمكنك تحميل ملف PPTX الناتج باستخدام Aspose.Slides وتعديل `Presentation.SlideSize`. |
| **ماذا لو احتجت لتعديل نص مربع النص قبل الحفظ؟** | ادخل إلى `shapeItem.TextBox.Text` داخل الحلقة، عدّل النص، ثم اضبط `IsEditable = true`. مثال: `shapeItem.TextBox.Text = "New title";` |

## نصائح استكشاف الأخطاء وإصلاحها

* **“ShapeType.TextBox” غير موجود** – تأكد من أنك تستخدم Aspose.Cells الإصدار 25.11 أو أحدث؛ الإصدارات الأقدم لا تدعم خاصية `IsEditable`.  
* **أخطاء “الملف غير موجود”** – تحقق من أن `YOUR_DIRECTORY` هو مسار مطلق أو أن المسار النسبي يشير إلى الموقع الصحيح.  
* **الترخيص غير مفعل** – استدعِ `License license = new License(); license.SetLicense("Aspose.Total.NET.lic");` قبل تحميل دفتر العمل لإزالة علامات التقييم المائية.

## الخلاصة

أنت الآن تعرف كيفية **حفظ Excel كـ PowerPoint** باستخدام C# عبر تحميل دفتر عمل XLSX، جعل كل مربع نص قابلًا للتحرير، وتصديره إلى PPTX. يتعامل هذا الأسلوب مع المخططات، الصور، وتنسيق الخلايا تلقائيًا، مما يمنحك مجموعة شرائح جاهزة للعرض.

بعد ذلك، استكشف المواضيع ذات الصلة مثل **تحويل Excel إلى PowerPoint باستخدام Aspose.Slides**، **كيفية تحرير مربعات النص برمجيًا بعد التحويل**، أو **معالجة دفاتر عمل متعددة دفعة واحدة**. كل منها يبني على الخطوات الأساسية المذكورة هنا ويمكنه أتمتة سير عمل التقارير لديك بشكل أكبر.

## ما الذي ينبغي أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مورد يتضمن أمثلة شيفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف طرق تنفيذ بديلة في مشاريعك.

- [How to Convert Excel to PowerPoint Using Aspose.Cells for .NET: A Complete Guide](/cells/english/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)
- [How to Copy Pivot Table in C# – Convert Excel to PPTX, Copy Range & Make Textbox](/cells/english/net/pivot-tables/how-to-copy-pivot-table-in-c-convert-excel-to-pptx-copy-rang/)
- [How to Save Excel Files in Multiple Formats Using Aspose.Cells .NET (2023 Guide)](/cells/english/net/workbook-operations/aspose-cells-net-save-excel-formats/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}