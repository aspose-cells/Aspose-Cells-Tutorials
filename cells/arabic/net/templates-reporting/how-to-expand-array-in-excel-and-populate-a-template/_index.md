---
category: general
date: 2026-09-18
description: تعلم كيفية توسيع المصفوفة في Excel باستخدام دالة EXPAND، وتعبئة قالب
  Excel، وإنشاء ورقة عمل Excel بنطاق ديناميكي باستخدام C#.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to expand array
- populate excel template
- dynamic range excel
- use expand function
- expand array formula
language: ar
lastmod: 2026-09-18
og_description: كيفية توسيع المصفوفة في Excel باستخدام دالة EXPAND، تعبئة قالب Excel،
  وبناء حل نطاق ديناميكي في Excel باستخدام كود C#.
og_image_alt: Excel worksheet showing expanded 5x5 array and Smart Markers result
og_title: كيفية توسيع المصفوفة في إكسل وتعبئة قالب
schemas:
- author: Aspose
  dateModified: '2026-09-18'
  description: Learn how to expand array in Excel using the EXPAND function, populate
    an Excel template, and create a dynamic range Excel worksheet with C#.
  headline: How to expand array in Excel and populate a template
  type: TechArticle
tags:
- Excel
- C#
- Aspose.Cells
title: كيفية توسيع المصفوفة في إكسل وتعبئة قالب
url: /ar/net/templates-reporting/how-to-expand-array-in-excel-and-populate-a-template/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية توسيع المصفوفة في Excel وتعبئة قالب

إذا كنت بحاجة إلى **how to expand array** في Excel أثناء تعبئة قالب مُصمم مسبقًا، يوضح لك هذا الدليل حلاً كاملاً من البداية إلى النهاية. باستخدام دالة `EXPAND` مع Smart Markers من Aspose.Cells، يمكنك تحويل مرجع خلية واحدة إلى نطاق 5 × 5 وتبديل العلامات مثل `{IsActive}` بالبيانات الحية تلقائيًا.

سترى كيف **populate excel template**، وإنشاء **dynamic range excel**، واستخدام **use expand function** بشكل صحيح في مشروع C#. في نهاية الدليل ستحصل على برنامج قابل للتنفيذ يقوم بتحميل ملف `.xlsx`، ويوسّع صيغة المصفوفة، ويطبق Smart Markers، ويحفظ النتيجة.

## المتطلبات المسبقة

* .NET 6.0 أو أحدث (الكود يعمل أيضًا مع .NET Core 3.1+)
* Aspose.Cells for .NET (حزمة NuGet `Aspose.Cells`)
* مصنف Excel يحتوي على خلية صيغة placeholder (مثال: `B2`) وعلامة Smart Marker مثل `{IsActive}`
* إلمام أساسي بـ C# وصيغ Excel

> **نصيحة احترافية:** دالة `EXPAND` متاحة فقط في Excel لـ Microsoft 365 وExcel 2021+. الإصدارات الأقدم ستعيد خطأ `#NAME?`.

## الخطوة 1: كيفية توسيع المصفوفة باستخدام دالة EXPAND

الخطوة الأولى هي تحميل المصنف وكتابة صيغة `EXPAND` التي تحول خلية مصدر واحدة إلى مصفوفة أكبر.  

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Load the workbook that contains the template layout
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // Access the first worksheet (index 0)
        Worksheet ws = workbook.Worksheets[0];

        // Apply the EXPAND function to cell B2.
        // =EXPAND(A2,5,5) expands the array that starts at A2 into a 5‑row by 5‑column range.
        ws.Cells["B2"].Formula = "=EXPAND(A2,5,5)";
```

لماذا هذا مهم: `EXPAND` يلغي الحاجة إلى نسخ الصيغ يدويًا عبر الصفوف والأعمدة. عندما تتغير خلية المصدر (`A2`)، يتم تحديث الكتلة 5 × 5 بالكامل تلقائيًا، مما يمنحك **dynamic range excel** يتفاعل مع تغيّر البيانات.

## الخطوة 2: تعبئة قالب Excel باستخدام Smart Markers

تتيح لك Smart Markers تضمين عناصر placeholder داخل القالب التي يتم استبدالها بقيم من كائن C#. هذه هي الطريقة الأكثر ملاءمة لـ **populate excel template** دون كتابة كود خلية بخلية.

```csharp
        // Prepare an anonymous object that matches the marker names in the template.
        var data = new { IsActive = true };

        // Apply Smart Markers. The marker {IsActive} inside a formula like
        // =IF({IsActive}, "Active", "Inactive") will be replaced with the value from the object.
        workbook.Worksheets[0].SmartMarkersProcessor().Apply(data);
```

نداء `SmartMarkersProcessor().Apply` يفحص الورقة بأكملها، يجد `{IsActive}`، ويُدخل القيمة المنطقية. ثم تُقيم الصيغة إلى `"Active"` أو `"Inactive"` تلقائيًا.

## الخطوة 3: التحقق من النطاق الموسع والنتيجة المعبأة

بعد تطبيق كل من صيغة `EXPAND` وSmart Markers، يمكنك قراءة بعض الخلايا برمجيًا للتأكد من أن كل شيء عمل كما هو متوقع.

```csharp
        // Optional: read a cell from the expanded block to confirm the value.
        var sampleValue = ws.Cells["B2"].Value; // top‑left cell of the expanded range
        Console.WriteLine($"Top‑left of expanded range: {sampleValue}");

        // Read the marker result cell (assume it is C2)
        var status = ws.Cells["C2"].StringValue;
        Console.WriteLine($"Status from Smart Marker: {status}");
```

تشغيل البرنامج يجب أن يطبع القيمة الأصلية من `A2` (أو نتيجة المصفوفة) وإما **Active** أو **Inactive** اعتمادًا على علم `IsActive`.

## الخطوة 4: حفظ المصنف – النتيجة النهائية

أخيرًا، احفظ المصنف المعدل إلى القرص. تُظهر هذه الخطوة التدفق الكامل من التحميل، التوسيع، التعبئة، إلى حفظ الملف.

```csharp
        // Save the workbook with the expanded array and populated markers.
        workbook.Save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

الملف `output.xlsx` المحفوظ الآن يحتوي على مصفوفة 5 × 5 تم إنشاؤها بواسطة صيغة `EXPAND` وخلية تعكس قيمة `{IsActive}`. افتح الملف في Excel لرؤية النطاق الديناميكي قيد التنفيذ.

## الحالات الخاصة وأفضل الممارسات

| Situation                              | Recommendation                                                                 |
|----------------------------------------|--------------------------------------------------------------------------------|
| Excel version does not support `EXPAND`| العودة إلى صيغ `=OFFSET` أو `=INDEX` التقليدية، أو الترقية إلى Office 365. |
| Need to expand to a variable size      | استخدام `ROWS(source)` و `COLUMNS(source)` داخل `EXPAND` للحصول على ديناميكية حقيقية.   |
| Multiple Smart Markers in the same sheet| استدعاء `SmartMarkersProcessor().Apply` مرة واحدة مع كائن بيانات مركب.      |
| Large workbooks ( > 10 000 rows)       | تعطيل الحساب أثناء كتابة الصيغ (`workbook.Settings.CheckFormula = false`). |

## مثال عملي كامل

فيما يلي البرنامج الكامل المستقل الذي يمكنك نسخه ولصقه في مشروع وحدة تحكم جديد.

```csharp
using System;
using Aspose.Cells;

class ExpandArrayDemo
{
    static void Main()
    {
        // 1️⃣ Load the workbook that serves as the template.
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
        Worksheet ws = workbook.Worksheets[0];

        // 2️⃣ Write the EXPAND formula to create a 5x5 dynamic range.
        ws.Cells["B2"].Formula = "=EXPAND(A2,5,5)";

        // 3️⃣ Prepare data for Smart Markers.
        var data = new { IsActive = true };

        // 4️⃣ Apply Smart Markers – replaces {IsActive} in any formula or text.
        workbook.Worksheets[0].SmartMarkersProcessor().Apply(data);

        // 5️⃣ (Optional) Verify a couple of cells.
        Console.WriteLine($"Expanded top‑left: {ws.Cells["B2"].Value}");
        Console.WriteLine($"Marker result: {ws.Cells["C2"].StringValue}");

        // 6️⃣ Save the final workbook.
        workbook.Save("YOUR_DIRECTORY/output.xlsx");
        Console.WriteLine("Workbook saved successfully.");
    }
}
```

**الناتج المتوقع عند تشغيل البرنامج** (مع افتراض أن `A2` يحتوي على الرقم `42`):

```
Expanded top‑left: 42
Marker result: Active
Workbook saved successfully.
```

فتح `output.xlsx` يُظهر كتلة 5 × 5 مملوءة بالقيم المستمدة من `A2` وخلية تُظهر **Active**.

## الخلاصة

أنت الآن تعرف **how to expand array** في Excel باستخدام دالة `EXPAND`، وكيفية **populate excel template** باستخدام Smart Markers، وكيفية بناء **dynamic range excel** يتكيف تلقائيًا مع بيانات المصدر. يوضح المثال أيضًا الطريقة الصحيحة لـ **use expand function** و**expand array formula** في سيناريو أتمتة C# واقعي.

بعد ذلك، فكر في توسيع الحل:

* استبدال أبعاد `5,5` الثابتة بـ `ROWS(A2:A10), COLUMNS(A2:E2)` للحصول على نطاقات متغيرة حقًا.
* دمج عدة Smart Markers لتوليد تقارير كاملة (مثل قوائم الموظفين، جداول المبيعات).
* استكشاف API تنسيق Aspose.Cells لتنسيق الكتلة الموسعة تلقائيًا.

لا تتردد في تجربة مصفوفات مصدر مختلفة، أسماء العلامات، وتنسيقات المصنف. برمجة سعيدة!

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مصدر يتضمن أمثلة كود كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [Export Data to Excel: Populate a Template from an Array in C#](/cells/english/net/smart-markers-dynamic-data/export-data-to-excel-populate-a-template-from-an-array-in-c/)
- [How to create array in Excel with C# – Step-by-Step Guide](/cells/english/net/data-manipulation/how-to-create-array-in-excel-with-c-step-by-step-guide/)
- [Processing Data Using Array Function in Excel](/cells/english/net/excel-formulas-and-calculation-options/processing-data-using-array-function/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}