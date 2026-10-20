---
category: general
date: 2026-08-11
description: كيفية تقريب أرقام Excel باستخدام C#. تعلّم كيفية تحميل مصنف Excel باستخدام
  C#، ضبط الأرقام ذات الدقة في Excel، وتصدير Excel بدقة في دليل واحد.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to round excel numbers
- load excel workbook c#
- set significant digits excel
- export excel with precision
language: ar
lastmod: 2026-08-11
og_description: كيفية تقريب أرقام Excel في C# باستخدام Aspose.Cells. تحميل مصنف Excel
  في C#، تعيين الأرقام ذات الدقة المهمة في Excel، وتصدير Excel بدقة لتقارير موثوقة.
og_image_alt: Screenshot showing how to round Excel numbers in a C# code editor
og_title: كيفية تقريب أرقام Excel في C# – دليل خطوة بخطوة
schemas:
- author: Aspose
  dateModified: '2026-08-11'
  description: How to round Excel numbers using C#. Learn to load Excel workbook C#,
    set significant digits Excel, and export Excel with precision in a single tutorial.
  headline: How to round Excel numbers in C# – complete programming guide
  type: TechArticle
- description: How to round Excel numbers using C#. Learn to load Excel workbook C#,
    set significant digits Excel, and export Excel with precision in a single tutorial.
  name: How to round Excel numbers in C# – complete programming guide
  steps:
  - name: '**Determine the order of magnitude** of the original value (e.g., 1.23 × 10⁴
      for 12300).'
    text: '**Determine the order of magnitude** of the original value (e.g., 1.23 × 10⁴
      for 12300).'
  - name: '**Shift the decimal point** so that the first significant digit aligns
      with the integer part.'
    text: '**Shift the decimal point** so that the first significant digit aligns
      with the integer part.'
  - name: '**Round** to the requested number of digits using “round‑half‑up” (the
      default).'
    text: '**Round** to the requested number of digits using “round‑half‑up” (the
      default).'
  - name: '**Shift the decimal point back** to its original position.'
    text: '**Shift the decimal point back** to its original position.'
  type: HowTo
- questions:
  - answer: No. `ExportTableOptions` only influences the **values** written to the
      file. Formulas remain unchanged, and their results are re‑calculated when the
      workbook is opened in Excel.
    question: Does this method affect formulas?
  - answer: Yes. Instead of assigning `ExportTableOptions` to the whole worksheet,
      iterate over the desired columns and use `Cell.PutValue(Math.Round(...))` for
      custom logic.
    question: Can I round only specific columns?
  - answer: 'Adjust `SignificantDigits` to the required count. The same algorithm
      scales automatically. ## Next steps Now that you know **how to round Excel numbers**
      in C#, consider exploring these related topics: * **Load Excel workbook C#**
      – Learn how to read cell styles, formulas, and embedded images. * **S'
    question: What if I need more than four digits?
  type: FAQPage
tags:
- Excel
- C#
- Number rounding
- Aspose.Cells
title: كيفية تقريب أرقام Excel في C# – دليل برمجي كامل
url: /ar/net/number-and-display-formats-in-excel/how-to-round-excel-numbers-in-c-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تقريب أرقام Excel في C# – دليل برمجي كامل

إذا كنت بحاجة إلى **how to round Excel numbers** في سير عمل آلي، يوضح لك هذا الدليل الخطوات الدقيقة. باستخدام Aspose.Cells for .NET يمكنك **load Excel workbook C#**، تحديد عدد **significant digits Excel** التي يجب الاحتفاظ بها، ثم **export Excel with precision** إلى ملف جديد.  

سنستعرض العملية بالكامل، من تثبيت المكتبة إلى التحقق من النتيجة المقربة، حتى تتمكن من دمج منطق التقريب الدقيق في أي تطبيق C#.

## ما ستتعلمه

* تحميل ملف `.xlsx` موجود من القرص.  
* تكوين خيارات التصدير لتقريب القيم إلى عدد محدد من الأرقام ذات الدلالة.  
* تطبيق هذه الخيارات على ورقة العمل الأولى.  
* حفظ المصنف مع الحفاظ على القيم المقربة.  
* فهم كيفية عمل خوارزمية التقريب وكيفية التعامل مع الحالات الحدية مثل الأعداد السالبة أو الصيغة العلمية.

## المتطلبات المسبقة

* .NET 6.0 SDK أو أحدث مثبت.  
* Visual Studio 2022 (أو أي بيئة تطوير C# تفضلها).  
* رخصة Aspose.Cells for .NET أو مفتاح تقييم مجاني.  
* ملف Excel تجريبي (`input.xlsx`) يحتوي على الأرقام التي تريد تقريبها.

يمكنك تثبيت Aspose.Cells عبر NuGet:

```bash
dotnet add package Aspose.Cells
```

> **Pro tip:** إذا كنت تستخدم خط أنابيب CI/CD، أضف إشارة الحزمة إلى ملف المشروع بدلاً من تشغيل الأمر يدويًا.

## الخطوة 1: تحميل مصنف Excel C# الكود

العملية الأولى هي فتح المصنف المصدر. تقوم Aspose.Cells بقراءة الملف إلى كائن `Workbook`، مما يمنحك تحكمًا برمجيًا كاملاً في أوراق العمل والخلايا وإعدادات التصدير.

```csharp
using Aspose.Cells;
using System;

class ExcelRoundingDemo
{
    static void Main()
    {
        // Step 1: Load the source workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

*لماذا هذا مهم:* تحميل المصنف هو الأساس لأي تعديل لاحق. تقوم فئة `Workbook` بتحليل جميع أوراق العمل والأنماط والصيغ، مما يضمن أن يتم تطبيق التقريب على البيانات الفعلية وليس على نسخة مرئية.

## الخطوة 2: تعيين الأرقام ذات الدلالة في Excel باستخدام ExportTableOptions

توفر Aspose.Cells الخاصية `ExportTableOptions` للتحكم في كيفية كتابة القيم الرقمية أثناء التصدير. الخاصية `SignificantDigits` تقرب كل رقم إلى الدقة المطلوبة.

```csharp
        // Step 2: Define export options with the desired number of significant digits
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            SignificantDigits = 4   // Example: 12345.6789 → 12350
        };
```

*لماذا هذا مهم:* ضبط `SignificantDigits` يجيب مباشرة على **how to round Excel numbers** دون الحاجة إلى التكرار اليدوي على كل خلية. تستخدم المكتبة خوارزمية تقريب رياضية صحيحة تحترم حجم كل قيمة.

## الخطوة 3: تطبيق خيارات التصدير على ورقة العمل الأولى

الآن قم بإرفاق الخيارات بالورقة التي تنوي تصديرها. توضح هذه الخطوة قدرة **set significant digits Excel** على أساس كل ورقة.

```csharp
        // Step 3: Apply the export options to the first worksheet
        Worksheet worksheet = workbook.Worksheets[0];
        worksheet.ExportTableOptions = exportOptions;
```

*لماذا هذا مهم:* من خلال تعيين الخيارات إلى `worksheet.ExportTableOptions`، تضمن أن الورقة المستهدفة فقط هي المتأثرة، مع ترك الأوراق الأخرى دون تعديل—مفيد لتقارير ذات دقة مختلطة.

## الخطوة 4: حفظ المصنف بالإعدادات المطبقة

أخيرًا، اكتب المصنف المعدل مرة أخرى إلى القرص. طريقة `Save` تحترم `ExportTableOptions` التي قمت بتكوينها، وتنتج لك ملف **export Excel with precision**.

```csharp
        // Step 4: Save the workbook with the applied settings
        workbook.Save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

عند فتح `output.xlsx` في Excel، ستلاحظ أن جميع الأرقام قد تم تقريبها إلى أربعة أرقام ذات دلالة، مطابقةً للسلوك الموضح في تعليقات الكود.

## فهم خوارزمية التقريب

تقوم Aspose.Cells بتقريب الأرقام باستخدام المنطق التالي:

1. **تحديد رتبة الحجم** للقيمة الأصلية (مثال: 1.23 × 10⁴ لـ 12300).  
2. **تحريك الفاصلة العشرية** بحيث يتطابق الرقم ذو الدلالة الأولى مع الجزء الصحيح.  
3. **تقريب** إلى عدد الأرقام المطلوب باستخدام “تقريب‑نصف‑للأعلى” (الإعداد الافتراضي).  
4. **إعادة الفاصلة العشرية** إلى موقعها الأصلي.  

تضمن هذه الطريقة أن الأرقام مثل `0.0012345` تصبح `0.001235` عند تقريبها إلى أربعة أرقام ذات دلالة، بينما `12345.6789` تصبح `12350`.

### الحالات الحدية التي قد تواجهها

| السيناريو                              | النتيجة المتوقعة (`SignificantDigits = 4`) |
|--------------------------------------|-------------------------------------------|
| الأعداد السالبة (`-9876.543`)       | `-9880`                                   |
| الأعداد الصغيرة جدًا (`0.00012345`) | `0.0001235`                               |
| الصيغة العلمية (`1.23E+5`)           | `1.23E+5` (لم يتغير لأنه يحتوي بالفعل على 3 أرقام ذات دلالة) |
| الصفر (`0`)                           | `0` (لا حاجة للتقريب)                    |

إذا كنت بحاجة إلى وضع تقريب مختلف (مثال: تقريب‑نصف‑للزوج)، يمكنك استخدام الخاصية `ExportTableOptions.RoundingMode`.

## نصائح عملية للاستخدام في بيئات الإنتاج

* **تحقق من صحة ملفات الإدخال** – تأكد من أن المصنف يحتوي فعليًا على خلايا رقمية قبل تطبيق التقريب.  
* **تخزين المصنف مؤقتًا** – إذا كنت تعالج العديد من الملفات، أعد استخدام نسخة واحدة من `Workbook` لتقليل تخصيص الذاكرة.  
* **سجل إعدادات التقريب** – احفظ `SignificantDigits` في ملف إعدادات لتتمكن من تغيير الدقة دون إعادة التجميع.  
* **اختبر بالقيم الحدية** – أعداد مثل `9999.5` قد تكشف عن أخطاء إزاحة واحدة إذا كانت خوارزمية التقريب غير مضبوطة.  

## مثال كامل قابل للتنفيذ

فيما يلي البرنامج الكامل الذي يمكنك نسخه ولصقه في مشروع وحدة تحكم جديد. يتضمن توجيهات `using`، طريقة `Main`، وتعليقات توضح كل سطر.

```csharp
using Aspose.Cells;
using System;

namespace ExcelRoundingDemo
{
    class Program
    {
        static void Main()
        {
            // Load the source workbook (replace YOUR_DIRECTORY with your actual path)
            Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

            // Define export options: round to 4 significant digits
            ExportTableOptions exportOptions = new ExportTableOptions
            {
                SignificantDigits = 4   // e.g., 12345.6789 → 12350
            };

            // Apply the options to the first worksheet
            Worksheet worksheet = workbook.Worksheets[0];
            worksheet.ExportTableOptions = exportOptions;

            // Save the workbook; the numbers are now rounded
            workbook.Save("YOUR_DIRECTORY/output.xlsx");

            Console.WriteLine("Excel file has been saved with rounded numbers.");
        }
    }
}
```

شغّل البرنامج، ثم افتح `output.xlsx` للتحقق من أن كل خلية رقمية تعكس القيم المقربة.

## الأسئلة المتكررة

**س: هل تؤثر هذه الطريقة على الصيغ؟**  
ج: لا. `ExportTableOptions` يؤثر فقط على **القيم** المكتوبة في الملف. تبقى الصيغ دون تعديل، وتُعاد حساب نتائجها عند فتح المصنف في Excel.

**س: هل يمكن تقريب أعمدة محددة فقط؟**  
ج: نعم. بدلاً من تعيين `ExportTableOptions` للورقة بأكملها، يمكنك التكرار على الأعمدة المطلوبة واستخدام `Cell.PutValue(Math.Round(...))` لمنطق مخصص.

**س: ماذا لو احتجت إلى أكثر من أربعة أرقام؟**  
ج: عدل `SignificantDigits` إلى العدد المطلوب. الخوارزمية نفسها تتوسع تلقائيًا.

## الخطوات التالية

الآن بعد أن عرفت **how to round Excel numbers** في C#، فكر في استكشاف المواضيع ذات الصلة التالية:

* **Load Excel workbook C#** – تعلّم كيفية قراءة أنماط الخلايا، الصيغ، والصور المدمجة.  
* **Set significant digits Excel** – دمج التقريب مع التنسيق الشرطي لتقارير أوضح.  
* **Export Excel with precision** – استخدم `PdfSaveOptions` أو `CsvSaveOptions` للتصدير إلى صيغ أخرى مع الحفاظ على التقريب.  

جرّب قيم `SignificantDigits` مختلفة، دمج الكود في واجهة برمجة تطبيقات ويب، أو أتمتة معالجة دفعات من عشرات الجداول.

---

*لقد أتقنت الآن تقريب أرقام Excel برمجيًا. نفّذ النمط، عدّل الدقة حسب الحاجة، وتمتع بمخرجات رقمية موثوقة عبر جميع مشاريع .NET الخاصة بك.*

## ما الذي ينبغي أن تتعلمه لاحقًا؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مورد يتضمن أمثلة كود كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [How to Load HTML into Excel with Aspose.Cells for .NET: A Precision Guide](/cells/english/net/workbook-operations/implement-net-load-html-aspose-cells-precision-guide/)
- [How to Load an Excel Workbook & Set Printer Sizes Using Aspose.Cells for .NET](/cells/english/net/workbook-operations/load-workbook-set-printer-sizes-aspose-cells-dotnet/)
- [How to Load an Excel Workbook Without Defined Names Using Aspose.Cells for .NET](/cells/english/net/workbook-operations/load-excel-workbook-without-defined-names-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}