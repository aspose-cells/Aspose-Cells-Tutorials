---
category: general
date: 2026-10-13
description: تعلم كيفية حفظ ملف Excel كملف TXT باستخدام Aspose.Cells. يغطي هذا الدليل
  تصدير Excel إلى TXT، كتابة قيمة في الخلية، وتحديد الأرقام ذات الدقة في بضع خطوات
  فقط.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- save excel as txt
- export excel to txt
- write value to cell
- set significant digits
- export spreadsheet as txt
language: ar
lastmod: 2026-10-13
og_description: احفظ ملف Excel كملف TXT باستخدام Aspose.Cells. تعلّم كيفية تصدير Excel
  إلى TXT، كتابة قيمة في خلية، وتحديد الأرقام الهامة في بضع أسطر فقط من كود C#.
og_image_alt: Screenshot showing a workbook saved as a TXT file using save excel as
  txt
og_title: حفظ إكسل كملف TXT – دليل خطوة بخطوة لمطوري .NET
schemas:
- author: Aspose
  dateModified: '2026-10-13'
  description: Learn how to save Excel as TXT with Aspose.Cells. This guide covers
    export Excel to TXT, write value to cell, and set significant digits in just a
    few steps.
  headline: How to save Excel as TXT using Aspose.Cells in C#
  type: TechArticle
- questions:
  - answer: It rounds to the nearest value based on the specified number of significant
      digits, ensuring the output is mathematically accurate to that precision.
    question: Does `SignificantDigits` round or truncate?
  - answer: 'Yes. Replace the file path with a `MemoryStream` instance: `workbook.Save(stream,
      txtOptions);`. This is handy for web APIs that need to return the TXT content
      without touching the file system.'
    question: Can I export directly to a memory stream?
  - answer: 'Use `txtOptions.ExportFormattedValues = true`. This forces Aspose.Cells
      to write the cell’s displayed text rather than the raw value. ## Conclusion
      You now know how to **save Excel as TXT** with full control over precision,
      formatting, and output location. By following the four steps—create a workbo'
    question: What if I need to keep the original formatting (e.g., dates)?
  type: FAQPage
tags:
- Excel
- TXT
- Aspose.Cells
- .NET
title: كيفية حفظ Excel كملف TXT باستخدام Aspose.Cells في C#
url: /ar/net/converting-excel-files-to-other-formats/how-to-save-excel-as-txt-using-aspose-cells-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية حفظ Excel كملف TXT باستخدام Aspose.Cells في C#

إذا كنت بحاجة إلى **حفظ Excel كملف TXT** بسرعة، فإن هذا الدليل يوضح العملية الكاملة في أقل من خمس دقائق. ستتعرف على كيفية تصدير Excel إلى TXT، كتابة قيمة إلى خلية، وتحديد الأرقام ذات الدقة المهمة بحيث يحتوي ملف النص على البيانات التي تتوقعها بالضبط.

تصدير جدول بيانات كملف TXT مفيد عندما تقبل الأنظمة اللاحقة مدخلات نصية فقط، أو عندما تحتاج إلى إنشاء سجلات، أو عندما تريد تفريغًا قابلاً للقراءة البشرية للعمليات الحسابية. المثال أدناه يعمل مع Aspose.Cells v25.10 أو أحدث ويعمل على أي بيئة تشغيل .NET 6+.

## المتطلبات المسبقة

قبل أن تبدأ، تأكد من وجود ما يلي:

* نسخة مرخصة من **Aspose.Cells for .NET** (الإصدار التجريبي المجاني يكفي للاختبار).
* .NET 6 SDK أو أحدث مثبت.
* بيئة تطوير متكاملة مثل Visual Studio 2022 أو VS Code أو Rider.
* معرفة أساسية بلغة C#—لا تحتاج إلى خبرة متقدمة في أتمتة Excel.

يمكنك تثبيت حزمة Aspose.Cells عبر NuGet باستخدام:

```bash
dotnet add package Aspose.Cells
```

## الخطوة 1: إنشاء مصنف والوصول إلى ورقة العمل الأولى (save excel as txt)

أول شيء تقوم به عندما تريد **حفظ Excel كملف TXT** هو إنشاء كائن `Workbook`. هذا الكائن يمثل ملف Excel بالكامل في الذاكرة.

```csharp
using Aspose.Cells;

// Create a new workbook (an empty Excel file)
Workbook workbook = new Workbook();

// Access the first worksheet (index 0)
Worksheet worksheet = workbook.Worksheets[0];
```

> **لماذا هذا مهم:** فئة `Workbook` هي نقطة الدخول لجميع عمليات جدول البيانات. ببدء عملك بمصنف جديد تتجنب أي تنسيقات مخفية قد تؤثر على ناتج النص العادي.

## الخطوة 2: كتابة رقم عالي الدقة في خلية (write value to cell)

الآن تحتاج إلى **write value to cell** A1. طريقة `PutValue` تكتشف نوع البيانات تلقائيًا وتخزّنها كقيمة رقمية.

```csharp
// Write a high‑precision number into cell A1
worksheet.Cells["A1"].PutValue(12345.6789012345);
```

> **نصيحة:** إذا احتجت لاحقًا إلى كتابة سلاسل نصية أو تواريخ أو صيغ، فإن طريقة `PutValue` نفسها تعمل—فقط مرّر النوع المناسب من .NET.

## الخطوة 3: ضبط خيارات التصدير للحفاظ على الدقة المطلوبة فقط (set significant digits)

عند التصدير إلى ملف TXT، غالبًا ما ترغب في تحديد عدد الأرقام لتقليل حجم الملف أو لمطابقة مواصفات النظام اللاحق. توفر فئة `TxtSaveOptions` خاصية `SignificantDigits` لهذا الغرض.

```csharp
// Configure TXT save options to retain only 6 significant digits
TxtSaveOptions txtSaveOptions = new TxtSaveOptions(SaveFormat.Txt)
{
    SignificantDigits = 6   // New option in v25.10
};
```

> **لماذا يجب ضبط الأرقام ذات الدقة المهمة:** بدون هذا الإعداد، تقوم Aspose.Cells بكتابة القيمة ذات الدقة المزدوجة بالكامل، مما قد ينتج سلاسل طويلة مثل `12345.6789012345`. ضبط `SignificantDigits = 6` يقتصر الناتج على `12345.7`، وهو ما يلبي معظم متطلبات التقارير.

## الخطوة 4: تصدير المصنف كملف TXT (export excel to txt)

أخيرًا، تقوم **export Excel to TXT** عن طريق استدعاء `Workbook.Save` مع الخيارات التي تم تكوينها مسبقًا.

```csharp
// Save the workbook as a TXT file using the configured options
string outputPath = @"C:\Temp\LimitedDigits.txt";
workbook.Save(outputPath, txtSaveOptions);
```

عند انتهاء التنفيذ، يحتوي الملف `LimitedDigits.txt` على:

```
12345.7
```

> **التحقق من النتيجة:** افتح الملف في أي محرر نصوص (Notepad، VS Code) لتتأكد من وجود ستة أرقام ذات دقة فقط وأنه لا توجد فواصل أو فواصل تبويب إضافية.

## مثال كامل قابل للتنفيذ

فيما يلي تطبيق console مكتمل يمكنك نسخه، لصقه، وتشغيله فورًا.

```csharp
using System;
using Aspose.Cells;

namespace ExcelToTxtDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create workbook and get the first worksheet
            Workbook workbook = new Workbook();
            Worksheet worksheet = workbook.Worksheets[0];

            // 2️⃣ Write a high‑precision number to cell A1
            worksheet.Cells["A1"].PutValue(12345.6789012345);

            // 3️⃣ Set up TXT save options with 6 significant digits
            TxtSaveOptions txtOptions = new TxtSaveOptions(SaveFormat.Txt)
            {
                SignificantDigits = 6
            };

            // 4️⃣ Save as TXT
            string path = @"C:\Temp\LimitedDigits.txt";
            workbook.Save(path, txtOptions);

            Console.WriteLine($"Workbook exported to TXT at: {path}");
        }
    }
}
```

**شرح كل جزء**

| الكتلة | الغرض |
|-------|---------|
| `using Aspose.Cells;` | يستورد مساحة الأسماء Aspose.Cells المطلوبة لـ `Workbook` و `Worksheet` و `TxtSaveOptions`. |
| `Workbook workbook = new Workbook();` | ينشئ مصنف Excel فارغ في الذاكرة. |
| `worksheet.Cells["A1"].PutValue(...);` | **write value to cell** A1 باستخدام رقم بدقة مزدوجة. |
| `TxtSaveOptions` | يضبط سلوك **set significant digits** لتصدير TXT. |
| `workbook.Save(..., txtOptions);` | ينفذ عملية **export excel to txt**، وينشئ ملف النص العادي. |

## الحالات الخاصة ونصائح إضافية

| السيناريو | طريقة التعامل |
|----------|---------------|
| **أوراق عمل كبيرة** (عدد كبير من الصفوف/الأعمدة) | استخدم `txtOptions.Encoding = Encoding.UTF8` إذا كنت تحتاج إلى دعم Unicode، وفكّر في بث الملف باستخدام `Workbook.Save(Stream, txtOptions)` لتقليل استهلاك الذاكرة. |
| **فواصل مخصصة** (قيم مفصولة بفواصل) | `TxtSaveOptions` توفر أيضًا الخاصية `Separator`—قم بتعيينها إلى `','` لإنتاج مخرجات بنمط CSV مع الحفاظ على تنسيق TXT. |
| **الحفاظ على الصيغ** | اضبط `txtOptions.ExportFormulas = true` لكتابة نص الصيغة بدلاً من القيمة المحسوبة. |
| **فواصل عشرية حسب اللغة** | عدّل `txtOptions.DecimalSeparator` إلى `','` للغات الأوروبية. |
| **عدة أوراق عمل** | كرّر عبر `workbook.Worksheets` واستدعِ `Save` لكل ورقة، مع إلحاق اسم الورقة إلى اسم الملف. |

## الأسئلة المتكررة

**س: هل `SignificantDigits` تقوم بالتقريب أم القطع؟**  
ج: تقوم بالتقريب إلى أقرب قيمة بناءً على عدد الأرقام ذات الدقة المحدد، مما يضمن أن يكون الناتج رياضيًا دقيقًا وفقًا لتلك الدقة.

**س: هل يمكنني التصدير مباشرة إلى تدفق الذاكرة؟**  
ج: نعم. استبدل مسار الملف بكائن `MemoryStream`: `workbook.Save(stream, txtOptions);`. هذا مفيد لواجهات API الويب التي تحتاج لإرجاع محتوى TXT دون كتابة ملف على النظام.

**س: ماذا لو أردت الحفاظ على التنسيق الأصلي (مثل التواريخ)؟**  
ج: استخدم `txtOptions.ExportFormattedValues = true`. هذا يجبر Aspose.Cells على كتابة النص المعروض للخلية بدلاً من القيمة الخام.

## الخلاصة

الآن تعرف كيف **تحفظ Excel كملف TXT** مع تحكم كامل في الدقة، التنسيق، وموقع الإخراج. باتباع الخطوات الأربع—إنشاء مصنف، **write value to cell**، **set significant digits**، و**export Excel to TXT**—يمكنك دمج تصدير النص العادي في أي تطبيق .NET.

بعد ذلك، استكشف المواضيع ذات الصلة مثل **export spreadsheet as TXT with custom delimiters**، **convert Excel to CSV**، أو **use Aspose.Cells to generate JSON reports**. كل منها يبني على المفاهيم الأساسية التي تم توضيحها هنا، مما يمنحك مجموعة أدوات متعددة الاستخدامات لتبادل البيانات عبر المنصات.

برمجة سعيدة!

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مورد يتضمن أمثلة شيفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [Save Excel as Text – Complete C# Guide to Export Excel to TXT](/cells/english/net/converting-excel-files-to-other-formats/save-excel-as-text-complete-c-guide-to-export-excel-to-txt/)
- [Create New Workbook and Export Excel to TXT with Precision](/cells/english/net/excel-data-export-retrieval/create-new-workbook-and-export-excel-to-txt-with-precision/)
- [Create new workbook – Export Excel to TXT with Full Precision](/cells/english/net/converting-excel-files-to-other-formats/create-new-workbook-export-excel-to-txt-with-full-precision/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}