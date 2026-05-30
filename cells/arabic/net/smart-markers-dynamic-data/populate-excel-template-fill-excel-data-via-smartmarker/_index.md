---
category: general
date: 2026-05-30
description: املأ قالب Excel بسرعة وتعلم كيفية تعبئة Excel بالبيانات باستخدام Aspose.Cells
  SmartMarker. دليل كامل بلغة C# مع كود قابل للتنفيذ.
draft: false
keywords:
- populate excel template
- fill excel with data
- Aspose.Cells SmartMarker
- automate Excel reporting
- C# Excel automation
language: ar
og_description: املأ قالب Excel واملأ ملف Excel بالبيانات باستخدام Aspose.Cells SmartMarker.
  اتبع هذا الدليل خطوة بخطوة بلغة C# للحصول على نتائج فورية.
og_title: ملء قالب Excel – تعبئة بيانات Excel عبر SmartMarker
schemas:
- author: Aspose
  dateModified: '2026-05-30'
  description: Populate Excel template quickly and learn how to fill Excel with data
    using Aspose.Cells SmartMarker. Complete C# guide with runnable code.
  headline: Populate Excel Template – Fill Excel Data via SmartMarker
  type: TechArticle
- description: Populate Excel template quickly and learn how to fill Excel with data
    using Aspose.Cells SmartMarker. Complete C# guide with runnable code.
  name: Populate Excel Template – Fill Excel Data via SmartMarker
  steps:
  - name: Empty Collections
    text: 'If `Items` is empty, SmartMarker will leave the table header intact but
      won’t insert any rows. To avoid a blank space, you can add a conditional block:'
  - name: Custom Number Formats
    text: 'Sometimes you need currency symbols or thousands separators. After processing,
      you can apply a style programmatically:'
  - name: Large Data Sets
    text: 'For thousands of rows, enable the `UseFastMode` option to improve performance:'
  type: HowTo
tags:
- Excel
- C#
- Aspose.Cells
title: ملء قالب إكسل – تعبئة بيانات إكسل عبر SmartMarker
url: /ar/net/smart-markers-dynamic-data/populate-excel-template-fill-excel-data-via-smartmarker/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تعبئة قالب Excel – ملء بيانات Excel عبر SmartMarker

هل احتجت يوماً إلى **تعبئة قالب Excel** لكن لم تكن متأكدًا من كيفية أتمتة العملية؟ في هذا الدرس سنوضح لك كيفية **ملء Excel بالبيانات** باستخدام Aspose.Cells SmartMarker — أداة تحول دفتر عمل ثابت إلى مولد تقارير ديناميكي.

تخيل أن لديك ورقة فاتورة مصممة مسبقًا، لوحة تحكم مبيعات، أو أي نموذج قابل للتكرار. بدلاً من كتابة القيم يدويًا، يمكنك تمرير كائن C# ودع SmartMarker يتولى العمل الشاق. بحلول نهاية هذا الدليل ستحصل على مشروع جاهز يعمل بالكامل يأخذ قالبًا، يضيف صفوفًا، إجماليات، وحتى تنسيقًا شرطيًا — كل ذلك دون لمس واجهة المستخدم.

## ما ستتعلمه

- كيفية إعداد مصدر بيانات يتطابق مع العلامات في قالب Excel الخاص بك.  
- كيفية إنشاء **SmartMarkerProcessor** وتمكين دعم النطاقات.  
- كيفية **تعبئة قالب Excel** بمجموعات متداخلة، مثل عناصر الطلب.  
- نصائح للتعامل مع الحالات الخاصة مثل المجموعات الفارغة أو تنسيقات الأرقام المخصصة.  

لا خدمات خارجية، لا ماكرو VBA — فقط C# صافية و Aspose.Cells. كل ما تحتاجه هو .NET 6 (أو أحدث) وحزمة Aspose.Cells من NuGet.

## المتطلبات المسبقة

- Visual Studio 2022 (أو أي بيئة تطوير تفضلها).  
- .NET 6 SDK مثبت.  
- Aspose.Cells for .NET (يمكنك الحصول على نسخة تجريبية مجانية من موقع Aspose).  
- قالب Excel أساسي يحتوي على علامات SmartMarker (سننشئه خلال لحظات).

إذا كان أي من هذه غير مألوف لك، لا تقلق؛ الخطوات أدناه ستقودك عبر كل متطلب.

## الخطوة 1: تصميم قالب Excel مع علامات SmartMarker

أولاً، افتح دفتر عمل جديد ورتب الأجزاء الثابتة — شعار الشركة، العناوين، إلخ. ثم أدخل عناصر نائب SmartMarker حيث يجب أن تظهر البيانات الديناميكية.

| الخلية | المحتوى |
|------|---------|
| A1   | **فاتورة** |
| A3   | `{{CompanyName}}` |
| A5   | **تفاصيل الطلب** |
| A7   | `{{Orders.Items.Name}}` |
| B7   | `{{Orders.Items.Qty}}` |
| C7   | `{{Orders.Items.Price}}` |
| D7   | `{{Orders.Items.Price * Orders.Items.Qty}}` |

**لماذا هذا مهم:** يقرأ SmartMarker الأقواس المزدوجة ويطابقها مع الخصائص في الكائن الذي تمرره لاحقًا. مجموعة `Orders.Items` تخبر المحرك بتكرار الصف لكل عنصر في القائمة.

> **نصيحة احترافية:** استخدم خيار `RangeSmartMarker` (سنفعله لاحقًا) عندما تحتاج إلى أن يقوم المحرك بتوسيع النطاق تلقائيًا — مثالي للجداول التي تنمو أو تتقلص.

احفظ الملف باسم `InvoiceTemplate.xlsx` في مجلد المشروع `Resources`.

## الخطوة 2: إعداد مصدر البيانات المتطابق مع علامات القالب

الآن ننشئ كائنًا مجهولًا في C# (أو فئة ذات نوع قوي) تكون أسماء خصائصه مطابقة للعلامات. المفتاح هو عكس الهيكلية بدقة.

```csharp
// Step 2: Prepare the data source that matches the template markers
var data = new
{
    CompanyName = "Acme Corp.",
    Orders = new[]
    {
        new
        {
            Items = new[]
            {
                new { Name = "Pen",   Qty = 2, Price = 1.5m },
                new { Name = "Notebook", Qty = 1, Price = 3.75m },
                new { Name = "Stapler",  Qty = 1, Price = 5.0m }
            }
        }
    }
};
```

**لماذا هذا مهم:** يحتوي مصفوفة `Orders` على طلب واحد، ولكل طلب مصفوفة `Items`. سيقوم SmartMarker بتكرار `Items`، مستنسخًا الصف لكل عنصر. إذا احتجت لاحقًا إلى طلبات متعددة، ما عليك سوى إضافة المزيد من الكائنات إلى مصفوفة `Orders` — دون الحاجة لتغيير الكود.

## الخطوة 3: تحميل القالب وإنشاء مثيل SmartMarkerProcessor

مع جاهزية البيانات، نقوم بتحميل دفتر العمل، إنشاء المعالج، وإبلاغه باحترام علامات النطاق.

```csharp
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

// Load the template workbook
Workbook workbook = new Workbook("Resources/InvoiceTemplate.xlsx");

// Get the first worksheet (where our markers live)
Worksheet ws = workbook.Worksheets[0];

// Step 3: Create a SmartMarkerProcessor instance
SmartMarkerProcessor processor = new SmartMarkerProcessor();
```

**لماذا هذا مهم:** `SmartMarkerProcessor` هو المحرك الذي يحلل العلامات، يوسع النطاقات، ويكتب القيم. بفصل المعالج عن دفتر العمل، يبقى الكود نظيفًا وقابلًا لإعادة الاستخدام.

## الخطوة 4: معالجة الورقة مع تمكين RangeSmartMarker

السحر يحدث عندما نستدعي `Process`. ضبط `RangeSmartMarker = true` يخبر SmartMarker بمعاملة النطاق الصف بالكامل ككتلة قابلة للتكرار، مدخلًا أو محيًا الصفوف حسب الحاجة.

```csharp
// Step 4: Process the worksheet using SmartMarker with range support enabled
processor.Process(ws, data, new SmartMarkerOptions { RangeSmartMarker = true });
```

في هذه المرحلة يمتلك المحرك ما يلي:

1. مسح الورقة للعثور على العلامات `{{...}}`.  
2. ربط كل علامة بخصيصة في `data`.  
3. اكتشاف نطاق الجدول (A7:D7) وتكراره ثلاث مرات — مرة لكل عنصر.  
4. حساب التعبير `Price * Qty` للعمود الإجمالي.

## الخطوة 5: حفظ دفتر العمل الناتج

أخيرًا، اكتب دفتر العمل المعبأ إلى القرص (أو أرسله عبر تدفق إلى عميل ويب).

```csharp
// Step 5: Save the populated workbook
workbook.Save("Output/InvoicePopulated.xlsx");
```

افتح `InvoicePopulated.xlsx` وسترى جدولًا مملوءًا بشكل منظم:

| الاسم | الكمية | السعر | الإجمالي |
|-----------|-----|-------|-------|
| Pen       | 2   | 1.5   | 3.00 |
| Notebook  | 1   | 3.75  | 3.75 |
| Stapler   | 1   | 5.00  | 5.00 |

اكتملت الآن خطوة **تعبئة قالب Excel**، وقد نجحت في **ملء Excel بالبيانات** لأي عدد من الصفوف.

## التعامل مع الحالات الشائعة

### المجموعات الفارغة

إذا كانت `Items` فارغة، سيترك SmartMarker عنوان الجدول دون إدراج أي صفوف. لتجنب مساحة فارغة، يمكنك إضافة كتلة شرطية:

```csharp
{{#if Orders.Items.Length > 0}}
    ... table rows ...
{{else}}
    No items were ordered.
{{/if}}
```

### تنسيقات الأرقام المخصصة

أحيانًا تحتاج إلى رموز عملة أو فواصل آلاف. بعد المعالجة، يمكنك تطبيق نمط برمجيًا:

```csharp
Style style = workbook.CreateStyle();
style.Number = 164; // Built‑in currency format
StyleFlag flag = new StyleFlag { NumberFormat = true };

foreach (Cell cell in ws.Cells["C8:D12"])
{
    cell.SetStyle(style, flag);
}
```

### مجموعات البيانات الكبيرة

لآلاف الصفوف، فعّل خيار `UseFastMode` لتحسين الأداء:

```csharp
processor.Process(ws, data, new SmartMarkerOptions { 
    RangeSmartMarker = true,
    UseFastMode = true
});
```

## مثال كامل يعمل

فيما يلي البرنامج الكامل المستقل الذي يمكنك نسخه ولصقه في تطبيق Console. يتضمن جميع توجيهات `using`، إعداد البيانات، المعالجة، والحفظ.



## ما الذي ينبغي أن تتعلمه لاحقًا؟

- [Populate Excel with Data Using Aspose.Cells and Smart Markers](/cells/english/java/cell-operations/populate-excel-aspose-cells-smart-markers/)
- [How to Populate Excel Cells with Aspose.Cells for .NET: A Step-by-Step Guide](/cells/english/net/cell-operations/aspose-cells-dotnet-populate-excel-data/)
- [Automate Excel Data Export Using Aspose.Cells for .NET: A Step-by-Step Guide](/cells/english/net/automation-batch-processing/automate-excel-data-export-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}