---
category: general
date: 2026-10-10
description: تعلم كيفية حفظ ملف Excel كنص في C# باستخدام Aspose.Cells. يغطي هذا الدليل
  تحويل Excel إلى txt، وتصدير XLSX إلى txt، وإنشاء ملف txt من Excel مع الشيفرة الكاملة.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- save excel as text
- convert excel to txt
- export xlsx to txt
- create txt from excel
language: ar
lastmod: 2026-10-10
og_description: احفظ ملف Excel كنص باستخدام Aspose.Cells لـ .NET. اتبع هذا الدليل
  لتحويل Excel إلى txt، وتصدير XLSX إلى txt، وإنشاء txt من Excel مع كود عينة.
og_image_alt: Screenshot of C# code that saves an Excel workbook as a plain‑text file
og_title: حفظ Excel كنص في C# – دليل Aspose.Cells الكامل
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: Learn how to save Excel as text in C# using Aspose.Cells. This guide
    covers convert Excel to txt, export XLSX to txt, and create txt from Excel with
    full code.
  headline: How to save Excel as text with Aspose.Cells – step‑by‑step guide
  type: TechArticle
- description: Learn how to save Excel as text in C# using Aspose.Cells. This guide
    covers convert Excel to txt, export XLSX to txt, and create txt from Excel with
    full code.
  name: How to save Excel as text with Aspose.Cells – step‑by‑step guide
  steps:
  - name: Prerequisites
    text: '* .NET 6.0 or later (the code also works with .NET Framework 4.7.2+). *
      Basic familiarity with C# and Visual Studio (or any .NET IDE). * An active Aspose.Cells
      for .NET license or a free evaluation key. * The Excel file you want to convert
      (`input.xlsx` in the examples).'
  - name: Full runnable program
    text: 'Putting the pieces together, here is a complete, self‑contained console
      application:'
  - name: Verify programmatically
    text: 'You can read the generated file back into memory to confirm that the export
      succeeded:'
  - name: Common edge cases
    text: '| Situation | What to watch for | Recommended fix | |----------------------------------------|---------------------------------------------------|-----------------|
      | Cells contain formulas | The exported value is the **calculated result**,
      not the formula text. | Ensure the workbook is fully calcul'
  - name: What’s next?
    text: '* Try exporting to CSV (`CsvSaveOptions`) for Excel‑compatible comma‑separated
      files. * Explore the `PdfSaveOptions` class to **export Excel to PDF** in a
      single line. * Combine multiple worksheets into one text file by iterating over
      `workbook.Worksheets`.'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
- Text export
title: كيفية حفظ ملف Excel كنص باستخدام Aspose.Cells – دليل خطوة بخطوة
url: /ar/net/converting-excel-files-to-other-formats/how-to-save-excel-as-text-with-aspose-cells-step-by-step-gui/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية حفظ Excel كنص باستخدام Aspose.Cells – دليل خطوة بخطوة

إذا كنت بحاجة إلى **حفظ Excel كنص** بسرعة، فإن هذا الدليل يوضح لك بالضبط كيفية القيام بذلك في C# باستخدام Aspose.Cells. سترى كيف **تحول Excel إلى txt**، وتتحكم في دقة الأرقام، وتتعامل مع الحالات الشائعة—all in a single, runnable example. كل ذلك في مثال واحد قابل للتنفيذ.

في الأقسام التالية ستتعلم سير العمل الكامل، من تثبيت المكتبة إلى التحقق من ملف الإخراج. لا حاجة إلى أي وثائق خارجية؛ كل ما تحتاجه مضمّن هنا.

## ما ستحققه

* تحميل أي مصنف `.xlsx` من القرص.  
* تهيئة `TxtSaveOptions` لتحديد عدد الأرقام المهمة.  
* **تصدير XLSX إلى txt** باستخدام استدعاء `Save` واحد.  
* فهم كيفية استكشاف مشكلات التنسيق عندما **تنشئ txt من Excel**.

### المتطلبات المسبقة

* .NET 6.0 أو أحدث (الكود يعمل أيضًا مع .NET Framework 4.7.2+).  
* إلمام أساسي بـ C# و Visual Studio (أو أي بيئة تطوير .NET).  
* رخصة سارية لـ Aspose.Cells for .NET أو مفتاح تقييم مجاني.  
* ملف Excel الذي تريد تحويله (`input.xlsx` في الأمثلة).

> **نصيحة احترافية:** إذا كنت تخطط لتشغيل هذا على خادم، احفظ ملف الترخيص في موقع آمن وقم بتحميله مرة واحدة عند بدء تشغيل التطبيق.

## الخطوة 1: إعداد بيئة التطوير

1. إنشاء مشروع وحدة تحكم جديد:

   ```bash
   dotnet new console -n ExcelToTxtDemo
   cd ExcelToTxtDemo
   ```

2. إضافة حزمة Aspose.Cells عبر NuGet:

   ```bash
   dotnet add package Aspose.Cells
   ```

   هذا يجلب أحدث نسخة مستقرة (اعتبارًا من 2026‑10‑10 الإصدار هو 23.9).

3. (اختياري) إذا كان لديك ملف ترخيص، ضع `Aspose.Cells.lic` في جذر المشروع وأضف الكود التالي في بداية `Program.cs`:

   ```csharp
   // Load Aspose.Cells license (required for production use)
   var license = new Aspose.Cells.License();
   license.SetLicense("Aspose.Cells.lic");
   ```

   تحميل الترخيص يزيل علامات التقييم المائية ويعطل حدود الحجم.

## الخطوة 2: تحميل مصنف Excel

السطر الوظيفي الأول ينشئ كائن `Workbook` يمثل ملف Excel بالكامل.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 2: Load the workbook you want to convert
        var workbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");
        // Continue with export logic...
    }
}
```

**لماذا هذا مهم:**  
`Workbook` ي抽象 الأوراق، الخلايا، الصيغ، والتنسيق. بتحميل الملف مرة واحدة، تحافظ على سرعة التحويل وكفاءة الذاكرة.

## الخطوة 3: تهيئة TxtSaveOptions للتحكم الدقيق في الأرقام

عند **تحويل Excel إلى txt**، قد تحتوي القيم الرقمية على العديد من الأرقام العشرية. يتيح لك `TxtSaveOptions` تحديد عدد الأرقام المهمة في الناتج، وهو ما يُطلب غالبًا من الأنظمة اللاحقة التي تتوقع نصًا بعرض ثابت.

```csharp
// Step 3: Create and configure TxtSaveOptions
var txtOptions = new TxtSaveOptions
{
    // Keep only 5 significant digits (e.g., 123.45678 → 123.46)
    SignificantDigits = 5,

    // Optional: Use tab as the delimiter for column separation
    Separator = "\t",

    // Optional: Export only the first worksheet
    ExportActiveWorksheetOnly = true
};
```

**شرح:**  
* `SignificantDigits` يزيل الضوضاء العائمة مع الحفاظ على دقة كافية لمعظم الحسابات التجارية.  
* `Separator` الافتراضي هو مساحة؛ ضبطه إلى `\t` (علامة تبويب) يجعل الملف الناتج أسهل للاستيراد إلى قواعد البيانات أو جداول البيانات.  
* `ExportActiveWorksheetOnly` يمنع تصدير الأوراق المخفية عن طريق الخطأ، مما قد يضيف حجمًا غير مرغوب فيه إلى ملف النص.

## الخطوة 4: تصدير XLSX إلى txt باستخدام الخيارات المهيأة

الآن لديك كل ما تحتاجه **لحفظ Excel كنص**. طريقة `Save` تكتب تمثيل النص العادي إلى المسار المستهدف.

```csharp
// Step 4: Save the workbook as a plain‑text file
workbook.Save(@"YOUR_DIRECTORY\output.txt", txtOptions);
Console.WriteLine("Export completed: output.txt");
```

الملف `output.txt` المُنشأ سيحتوي على صفوف من القيم المفصولة بعلامات تبويب، كل خلية تُعرض كنص عادي وفقًا للخيارات التي حددتها.

### برنامج كامل قابل للتنفيذ

بجمع الأجزاء معًا، إليك تطبيق وحدة تحكم كامل ومستقل:

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Load license if you have one (remove comments if not needed)
        // var license = new License();
        // license.SetLicense("Aspose.Cells.lic");

        // 1️⃣ Load the Excel workbook
        var workbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");

        // 2️⃣ Configure TxtSaveOptions
        var txtOptions = new TxtSaveOptions
        {
            SignificantDigits = 5,
            Separator = "\t",
            ExportActiveWorksheetOnly = true
        };

        // 3️⃣ Export XLSX to TXT
        workbook.Save(@"YOUR_DIRECTORY\output.txt", txtOptions);

        Console.WriteLine("✅ Excel workbook successfully saved as text at: output.txt");
    }
}
```

**الناتج المتوقع** (وحدة التحكم):

```
✅ Excel workbook successfully saved as text at: output.txt
```

**عينة `output.txt` الناتجة** (أول ثلاث صفوف):

```
Name    Age     Salary
Alice   30      55000
Bob     27      47000
```

الأرقام مُقربة إلى خمسة أرقام مهمة، والأعمدة مفصولة بعلامات تبويب.

## الخطوة 5: التحقق من الناتج ومعالجة الحالات الخاصة

### التحقق برمجياً

يمكنك قراءة الملف المُنشأ مرة أخرى إلى الذاكرة لتأكيد نجاح التصدير:

```csharp
string[] lines = File.ReadAllLines(@"YOUR_DIRECTORY\output.txt");
if (lines.Length > 0)
{
    Console.WriteLine("First line of the txt file:");
    Console.WriteLine(lines[0]);
}
```

### الحالات الخاصة الشائعة

| الحالة                                 | ما الذي يجب مراقبته                                 | الإصلاح المقترح |
|----------------------------------------|---------------------------------------------------|-----------------|
| الخلايا التي تحتوي على صيغ            | القيمة المصدرة هي **النتيجة المحسوبة**، وليس نص الصيغة. | تأكد من حساب المصنف بالكامل (`workbook.CalculateFormula();`) قبل الحفظ. |
| التواريخ تظهر كأرقام متسلسلة          | Excel يخزن التواريخ كأرقام؛ قد تظهر كـ `44745`.   | اضبط `txtOptions.ConvertDateTime = true;` لفرض تنسيق تاريخ قابل للقراءة. |
| الأوراق الكبيرة (>10 000 صف)          | استهلاك الذاكرة قد يرتفع.                         | استخدم `txtOptions.ExportAllSheets = false;` وعالج الأوراق بشكل فردي. |
| حروف Unicode (مثل الرموز التعبيرية)   | الترميز الافتراضي هو UTF‑8؛ الأنظمة القديمة قد تتوقع ANSI. | اضبط `txtOptions.Encoding = Encoding.GetEncoding("windows-1252");` إذا لزم الأمر. |

من خلال توقع هذه السيناريوهات يمكنك **إنشاء txt من Excel** بشكل موثوق عبر مجموعات بيانات مختلفة.

## الخلاصة

أنت الآن تعرف كيف **تحفظ Excel كنص** باستخدام Aspose.Cells لـ .NET، بدءًا من تحميل المصنف إلى تهيئة `TxtSaveOptions` وأخيرًا **تصدير XLSX إلى txt**. المثال يوضح مسار الكود الكامل، يشرح السبب وراء كل إعداد، ويغطي المشكلات الشائعة عند **تحويل Excel إلى txt**.

### ما التالي؟

* جرب التصدير إلى CSV (`CsvSaveOptions`) للحصول على ملفات متوافقة مع Excel مفصولة بفواصل.  
* استكشف فئة `PdfSaveOptions` لـ **تصدير Excel إلى PDF** بسطر واحد.  
* اجمع عدة أوراق عمل في ملف نصي واحد عبر التكرار على `workbook.Worksheets`.  

لا تتردد في تجربة الخيارات—تغيير الفاصل، الدقة، أو اختيار ورقة العمل—لتتناسب مع سير عملك الخاص.

برمجة سعيدة!

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مصدر يتضمن أمثلة كود كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [حفظ Excel كملف نصي بفاصل مخصص باستخدام Aspose.Cells](/cells/english/net/workbook-operations/save-excel-text-custom-separator-aspose-cells-net/)
- [حفظ Excel كملف txt – دليل C# كامل لتصدير الأرقام بالأرقام المهمة](/cells/english/net/converting-excel-files-to-other-formats/save-excel-as-txt-complete-c-guide-to-export-numbers-with-si/)
- [كيفية حفظ ملفات Excel بصيغ متعددة باستخدام Aspose.Cells .NET (دليل 2023)](/cells/english/net/workbook-operations/aspose-cells-net-save-excel-formats/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}