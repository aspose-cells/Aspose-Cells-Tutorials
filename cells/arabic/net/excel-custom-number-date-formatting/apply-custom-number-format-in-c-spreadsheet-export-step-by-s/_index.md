---
category: general
date: 2026-04-07
description: تطبيق تنسيق رقمي مخصص على خلية في جدول البيانات وتعلم كيفية تنسيق الأرقام
  في جدول البيانات أثناء تصدير قيمة الخلية باستخدام C#. دليل سريع وشامل.
draft: false
keywords:
- apply custom number format
- format number in spreadsheet
- how to format numeric cell
- how to export cell value
language: ar
og_description: تطبيق تنسيق رقم مخصص على خلية في جدول البيانات وتصديرها كسلسلة منسقة.
  تعلّم كيفية تنسيق الأرقام في جدول البيانات وتصدير قيمة الخلية.
og_title: تطبيق تنسيق الأرقام المخصص – دليل كامل لتصدير C#
tags:
- C#
- Spreadsheet
- Number Formatting
title: تطبيق تنسيق رقم مخصص في تصدير جداول البيانات بلغة C# – دليل خطوة بخطوة
url: /ar/net/excel-custom-number-date-formatting/apply-custom-number-format-in-c-spreadsheet-export-step-by-s/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تطبيق تنسيق رقم مخصص في تصدير جداول البيانات C# – دليل كامل

هل احتجت يومًا إلى **تطبيق تنسيق رقم مخصص** على خلية ثم استخراج تلك السلسلة المنسقة من جدول بيانات؟ لست وحدك. يواجه العديد من المطورين صعوبة عندما يكتشفون أن القيمة الخام تُستخرج بدلاً من السلسلة الجميلة المتوافقة مع الإعدادات الإقليمية التي يتوقعونها. في هذا الدليل سنوضح لك بالضبط كيفية تنسيق الأرقام في خلايا جدول البيانات وكيفية تصدير قيمة الخلية كسلسلة منسقة باستخدام مكتبة جداول بيانات شائعة في C#.

بنهاية الشرح ستكون قادرًا على **تطبيق تنسيق رقم مخصص** على أي خلية رقمية، وتصدير النتيجة باستخدام `ExportTable`، ورؤية المخرجات الدقيقة التي تتوقع عرضها في واجهة المستخدم أو تقرير. لا حاجة إلى وثائق خارجية—كل شيء هنا.

## Prerequisites

- .NET 6.0 أو أحدث (الكود يعمل أيضًا على .NET Framework 4.7+)
- إشارة إلى مكتبة جداول البيانات التي توفر `Workbook`، `Worksheet`، و `ExportTableOptions` (مثل **Aspose.Cells** أو **GemBox.Spreadsheet**؛ الـ API المعروض يتطابق مع Aspose.Cells)
- معرفة أساسية بـ C#—إذا كنت تستطيع كتابة `Console.WriteLine` فأنت جاهز للبدء

> **Pro tip:** إذا كنت تستخدم مكتبة مختلفة، فإن أسماء الخصائص عادةً ما تكون مشابهة (`NumberFormat`، `ExportAsString`). ما عليك سوى ربطها وفقًا لذلك.

## What the tutorial covers

1. إنشاء ملف عمل واختيار ورقة العمل الأولى.  
2. إدخال قيمة رقمية في خلية.  
3. إعداد `ExportTableOptions` **لتطبيق تنسيق رقم مخصص** وإرجاع سلسلة.  
4. تصدير الخلية وطباعة النتيجة المنسقة.  
5. معالجة الحالات الخاصة – ماذا لو احتوت الخلية على صيغة أو قيمة فارغة؟

لننطلق.

![apply custom number format example](https://example.com/image.png "تطبيق تنسيق رقم مخصص")

## Step 1 – Create a workbook and get the first worksheet

الخطوة الأولى هي الحصول على كائن workbook. فكر فيه كملف Excel ستفتحه في تطبيق Office. بمجرد حصولك عليه، احصل على الورقة الأولى—معظم الدروس تبدأ من هنا لأنها تجعل المثال مختصرًا.

```csharp
// Step 1: Initialize the workbook and fetch the first worksheet
Workbook workbook = new Workbook();                 // creates an in‑memory workbook
Worksheet worksheet = workbook.Worksheets[0];      // first sheet (index 0)
```

**Why this matters:** يضمن لك ملف العمل الجديد بداية نظيفة، مما يمنع أي تنسيق مخفي من التدخل في تنسيقنا المخصص لاحقًا.

## Step 2 – Put a numeric value into cell B2 (the cell we will export)

الآن نحتاج إلى شيء لنقوم بتنسيقه. الخلية **B2** موقع مناسب—سهل الإشارة إليه وبعيد بما يكفي عن الزاوية الافتراضية A1 لتجنب الكتابة فوق البيانات عن طريق الخطأ.

```csharp
// Step 2: Insert a raw numeric value
worksheet.Cells["B2"].Value = 1234.56;   // raw double, no formatting yet
```

**What if the value is a formula?**  
إذا قمت لاحقًا باستبدال القيمة الخام بصيغة (مثال: `=SUM(A1:A10)`)، فإن روتين التصدير سيظل يحترم تنسيق الرقم الذي نطبقه في الخطوة التالية، لأن التنسيق مرتبط بالخلية وليس بنوع القيمة.

## Step 3 – Configure export options to receive the value as a formatted string

هنا يكمن جوهر الشرح: نخبر المكتبة **بتطبيق تنسيق رقم مخصص** أثناء التصدير. سلسلة `NumberFormat` تتبع نفس النمط الذي تستخدمه في فئة “Custom” في Excel.

```csharp
// Step 3: Set up options for exporting as a formatted string
ExportTableOptions exportOptions = new ExportTableOptions
{
    ExportAsString = true,                         // forces string output
    NumberFormat = "#,##0.00;(#,##0.00)"           // custom format: 1,234.56 or (1,234.56) for negatives
};
```

- `ExportAsString = true` يضمن أن الطريقة تُعيد `string` بدلاً من قيمة double خام.  
- `NumberFormat = "#,##0.00;(#,##0.00)"` يعكس نمط Excel: الفواصل للآلاف، منزلتين عشريتين، وأقواس للأرقام السالبة.

> **Why use a custom format?** يضمن التناسق عبر الثقافات (مثال: الفواصل الأمريكية مقابل الأوروبية) ويسمح لك بإدراج تنسيقات خاصة بالأعمال مثل الأقواس المحاسبية.

## Step 4 – Export the cell using the configured options

الآن نستخرج القيمة من ورقة العمل، مع ترك المكتبة تتولى تطبيق التنسيق الذي عرّفناه.

```csharp
// Step 4: Export the formatted value from B2
string formattedResult = worksheet.Cells.ExportTable(
    worksheet.Cells["B2"],   // the source cell
    exportOptions);         // our custom options
```

**Edge case – empty cell:** إذا كانت الخلية `B2` فارغة، فإن `formattedResult` سيكون `null`. يمكنك الحماية من ذلك بفحص بسيط للـ null قبل الطباعة.

## Step 5 – Display the formatted string

أخيرًا، نكتب النتيجة إلى وحدة التحكم. في تطبيق حقيقي قد تُرسل هذه السلسلة إلى PDF أو بريد إلكتروني أو تسمية واجهة مستخدم.

```csharp
// Step 5: Show the result
Console.WriteLine(formattedResult);   // Expected output: 1,234.56
```

**Expected output**

```
1,234.56
```

إذا غيرت القيمة الخام إلى `-9876.54`، سيعطيك نفس التنسيق `(9,876.54)`—تمامًا ما تتطلبه العديد من التقارير المحاسبية.

## Full, runnable example

فيما يلي البرنامج الكامل الذي يمكنك نسخه ولصقه في مشروع Console جديد. يَـُـترجم ويعمل كما هو، بشرط إضافة حزمة NuGet المناسبة لمكتبة جداول البيانات.

```csharp
using System;
using Aspose.Cells;   // Replace with your library’s namespace if different

class Program
{
    static void Main()
    {
        // 1️⃣ Create workbook and get first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // 2️⃣ Insert numeric value into B2
        worksheet.Cells["B2"].Value = 1234.56;

        // 3️⃣ Set export options – apply custom number format
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,
            NumberFormat = "#,##0.00;(#,##0.00)"   // custom format
        };

        // 4️⃣ Export the cell as a formatted string
        string formattedResult = worksheet.Cells.ExportTable(
            worksheet.Cells["B2"], exportOptions);

        // 5️⃣ Output the result
        Console.WriteLine(formattedResult);   // → 1,234.56
    }
}
```

### Quick sanity check

- **Does it compile?** نعم—فقط تأكد من أن مكتبة `Aspose.Cells` (أو ما يعادلها) مُشار إليها.
- **Will it work with other cultures?** سلسلة التنسيق لا تعتمد على الثقافة؛ المكتبة تحترم النمط الذي تزوده إياه. إذا احتجت إلى فواصل خاصة بإعدادات إقليمية، يمكنك إضافة معالجة `CultureInfo` قبل التصدير.

## Common questions & variations

### How to **format number in spreadsheet** using a different pattern?

استبدل سلسلة `NumberFormat`. على سبيل المثال، لإظهار نسبة مئوية بمنزل عشري واحد:

```csharp
NumberFormat = "0.0%";
```

### What if I need to **how to export cell value** as HTML instead of plain text?

معظم المكتبات توفر overload يقبل نوع التصدير. ستضبط `ExportAsString = true` وتضيف `ExportHtml = true` (أو ما شابه). المبدأ يبقى نفسه: عرّف التنسيق، ثم اختر تمثيل الإخراج.

### Can I apply the format to a whole range, not just one cell?

بالتأكيد. يمكنك إسناد `NumberFormat` إلى كائن `Style` ثم تطبيق هذا النمط على `Range`. استدعاء التصدير يظل كما هو؛ سيُلتقط النمط تلقائيًا.

```csharp
Style style = workbook.CreateStyle();
style.Custom = "#,##0.00;(#,##0.00)";
Range range = worksheet.Cells.CreateRange("A1:C10");
range.ApplyStyle(style, new StyleFlag { NumberFormat = true });
```

### What happens when the cell contains a formula?

روتين التصدير يُقيم الصيغة أولًا، ثم يُنسق القيمة الرقمية الناتجة. لا حاجة إلى كود إضافي—فقط تأكد من استدعاء `Calculate` إذا عطلت الحساب التلقائي.

```csharp
worksheet.Cells["B2"].Formula = "=SUM(A1:A5)";
worksheet.Calculate();   // forces evaluation
```

## Conclusion

الآن تعرف كيف **تطبق تنسيق رقم مخصص** على خلية جدول بيانات، **تنسيق رقم في جدول البيانات** في السياقات المختلفة، و**تصدير قيمة الخلية** كسلسلة جاهزة للعرض. يغطي المثال المختصر أعلاه كل خطوة—from إنشاء ملف العمل إلى الإخراج النهائي—حتى يمكنك إدراجه مباشرة في مشروع إنتاجي.

هل أنت مستعد للتحدي التالي؟ جرّب دمج هذه التقنية مع **كيفية تنسيق خلية رقمية** للتواريخ، رموز العملات، أو التنسيق الشرطي. أو استكشف تصدير خلايا متعددة كملف CSV مع الحفاظ على تنسيق كل خلية. السماء هي الحد، ومع هذه الأساسيات لديك بنية قوية.

برمجة سعيدة، ولا تنس التجربة—فأحيانًا تظهر أفضل الإجابات عندما تُعدّل سلسلة التنسيق قليلًا!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}