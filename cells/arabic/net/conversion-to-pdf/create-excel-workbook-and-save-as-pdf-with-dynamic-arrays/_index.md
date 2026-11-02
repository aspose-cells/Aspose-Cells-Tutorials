---
category: general
date: 2026-09-15
description: إنشاء مصنف Excel باستخدام C# وتعلم كيفية حفظ المصنف كملف PDF مع تفريغ
  المصفوفات الديناميكية باستخدام دالة EXPAND.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook
- save workbook as pdf
- spill dynamic array
- use expand function
- how to create dynamic array in excel
language: ar
lastmod: 2026-09-15
og_description: إنشاء مصنف Excel باستخدام C# وحفظ المصنف بسرعة كملف PDF مع استخدام
  دالة EXPAND لتفريغ مصفوفة ديناميكية.
og_image_alt: Create Excel workbook screenshot showing dynamic array and PDF output
og_title: إنشاء مصنف إكسل وحفظه كملف PDF مع المصفوفات الديناميكية
schemas:
- author: Aspose
  dateModified: '2026-09-15'
  description: Create Excel workbook in C# and learn how to save workbook as PDF while
    spilling dynamic arrays using the EXPAND function.
  headline: Create Excel workbook and save as PDF with dynamic arrays
  type: TechArticle
tags:
- excel
- csharp
- aspose-cells
- pdf
- dynamic-array
title: إنشاء مصنف إكسل وحفظه كملف PDF مع المصفوفات الديناميكية
url: /ar/net/conversion-to-pdf/create-excel-workbook-and-save-as-pdf-with-dynamic-arrays/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء مصنف Excel وحفظه كملف PDF باستخدام المصفوفات الديناميكية

إذا كنت بحاجة إلى **إنشاء مصنف Excel** برمجياً ثم **حفظ المصنف كملف PDF**، فإن هذا الدليل يوضح لك حلاً كاملاً من البداية إلى النهاية بلغة C#. ستتعرف أيضاً على كيفية **توسيع نتائج المصفوفة الديناميكية** باستخدام **دالة EXPAND**، وهي الطريقة الحديثة لإنشاء المصفوفات دون الحاجة إلى VBA.  

سواءً كنت تبني خدمة تقارير، أو ميزة تصدير لنظام ERP، أو لوحة معلومات تعتمد على البيانات، فإن الخطوات أدناه تسمح لك بإنشاء مصنف، تعبئته ببيانات Smart‑Marker، وإنتاج ملف PDF يحافظ على خصائص الخط المتقدمة.

## المتطلبات المسبقة

قبل أن تبدأ، تأكد من وجود ما يلي:

* .NET 6.0 أو أحدث (الكود يعمل أيضاً مع .NET Framework 4.8)
* نسخة حديثة من **Aspose.Cells for .NET** (الإصدار 25.8 أو أحدث) – توفر `Workbook`، `PdfSaveOptions`، و `SmartMarkerProcessor`.
* بيئة تطوير متكاملة مثل Visual Studio 2022 (أي محرر يستطيع تجميع C# يعمل).

أضف حزمة NuGet إلى مشروعك:

```bash
dotnet add package Aspose.Cells --version 25.8
```

## الخطوة 1: إنشاء مصنف Excel وإعداد الورقة الأولى

المهمة الأولى هي **إنشاء مصنف Excel** والحصول على مرجع للورقة الافتراضية. ستستضيف هذه الورقة المصفوفة الديناميكية وقالب Smart Marker.

```csharp
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;
using System;

class Program
{
    static void Main()
    {
        // Create a new workbook in memory
        Workbook wb = new Workbook();

        // Get the first (default) worksheet
        Worksheet ws = wb.Worksheets[0];
```

*لماذا هذا مهم*: إنشاء كائن `Workbook` يخصص بنية المصنف الداخلية، بينما الوصول إلى `Worksheets[0]` يمنحك ورقة جاهزة للاستخدام دون الحاجة لإضافتها يدوياً.

## الخطوة 2: توسيع المصفوفة الديناميكية باستخدام دالة EXPAND

يمكن لدالة **EXPAND** في Excel تحويل مصفوفة ثابتة إلى نطاق متسلسل بأي حجم. هنا نطلب من Excel توسيع `{1,2,3}` إلى نطاق 5 صفوف × عمود واحد يبدأ من `A1`.

```csharp
        // Write the EXPAND formula into A1
        ws.Cells["A1"].Formula = "=EXPAND({1,2,3},5,1)";

        // Force calculation so the spill occurs immediately
        ws.Calculate();
```

*لماذا هذا مهم*: استخدام `EXPAND` يتجنب الحلقات اليدوية في C#. تقوم الآلية بحساب نطاق التوسيع وتخزين القيم مباشرة في الورقة، لتظهر لاحقاً في ملف PDF.

## الخطوة 3: حفظ المصنف كملف PDF مع الحفاظ على محددات تنوع الخط

عند الحاجة إلى **حفظ المصنف كملف PDF**، يمكنك أيضاً تمكين ميزات الطباعة المتقدمة مثل محددات تنوع الخط (متوفرة منذ Aspose.Cells v25.8). يضمن ذلك أن ملفات PDF تعرض النصوص المعقدة بشكل صحيح.

```csharp
        // Configure PDF options
        PdfSaveOptions pdfOpts = new PdfSaveOptions
        {
            FontVariationSelectors = true   // keeps variation selectors for OpenType fonts
        };

        // Save the current workbook (with the spilled array) as PDF
        wb.Save(@"YOUR_DIRECTORY\VarSelector.pdf", pdfOpts);
```

*لماذا هذا مهم*: ضبط `FontVariationSelectors` إلى `true` ضروري للغات التي تعتمد على تنوع الحروف (مثل الصينية، اليابانية، الإيموجي). الملف PDF الناتج يعكس عرض Excel على الشاشة.

## الخطوة 4: إدراج قالب Smart Marker يشير إلى مصدر بيانات متداخل

تتيح لك Smart Markers تضمين عناصر نائبة مباشرة في الورقة. القالب أدناه سيولد قائمة بالطلبات وعناصرها.

```csharp
        // Define a Smart Marker template in cell A1
        string template = "${Orders.OrderId}\n${Orders.Items:ItemName}\n";
        ws.Cells["A1"].PutValue(template);
```

*لماذا هذا مهم*: بوضع القالب في `A1`، تخبر Aspose.Cells من أين يبدأ توسيع البيانات. الصيغة `:` (`Items:ItemName`) تخبر المعالج بالتكرار عبر مجموعة متداخلة.

## الخطوة 5: تعريف مصدر البيانات المتداخل (طلبات تحتوي على عناصر)

ننشئ مصفوفة مجهولة للطلبات، كل طلب يحتوي على مجموعة خاصة به من كائنات العنصر. هذا يعكس سيناريو ماستر‑ديتيل شائع.

```csharp
        // Sample nested data source
        var orders = new[]
        {
            new
            {
                OrderId = 1,
                Items = new[]
                {
                    new { ItemName = "Apple" },
                    new { ItemName = "Banana" }
                }
            },
            new
            {
                OrderId = 2,
                Items = new[]
                {
                    new { ItemName = "Carrot" }
                }
            }
        };
```

*لماذا هذا مهم*: البنية المتداخلة توضح **كيفية إنشاء مصفوفة ديناميكية في Excel** عبر Smart Markers، دون كتابة أي VBA أو حلقات يدوية في الخلايا.

## الخطوة 6: معالجة Smart Markers وحفظ ملف Excel النهائي

الآن نمرر المصنف ومصدر البيانات إلى `SmartMarkerProcessor`. بعد المعالجة، تُستبدل العناصر النائبة بالصفوف الفعلية، ونحفظ النتيجة كملف `.xlsx` عادي.

```csharp
        // Process the Smart Markers
        SmartMarkerProcessor processor = new SmartMarkerProcessor();
        processor.Process(wb, orders);

        // Save the populated workbook
        wb.Save(@"YOUR_DIRECTORY\NestedSmartMarker.xlsx");
    }
}
```

*لماذا هذا مهم*: `SmartMarkerProcessor` يوسع القالب تلقائياً، ينشئ الصفوف اللازمة، ويملأها بالبيانات. يمكن فتح المصنف النهائي في Excel للتحقق من ظهور كل طلب وعناصره بشكل صحيح.

## النتيجة المتوقعة

* **VarSelector.pdf** – ملف PDF يُظهر الأرقام 1‑3 تتسلسل عبر خمسة صفوف، مع تطبيق أي تنوعات خط OpenType مفعلة.
* **NestedSmartMarker.xlsx** – ملف Excel يحتوي على الصفوف التالية (بدءاً من `A1`):

| OrderId | ItemName |
|---------|----------|
| 1       | Apple    |
| 1       | Banana   |
| 2       | Carrot   |

نسخة PDF تحتفظ بنفس التوسع العددي لأن حالة الورقة تم حفظها قبل معالجة Smart Marker؛ يمكنك تكرار حفظ PDF بعد المعالجة إذا احتجت البيانات النهائية في PDF أيضاً.

## نصائح احترافية ومخاطر شائعة

| النصيحة | الشرح |
|-----|-------------|
| **إعادة استخدام نفس كائن `PdfSaveOptions`** | إنشاء كائن الخيارات مرة واحدة وإعادة استخدامه يجنب الفروقات الدقيقة في العرض (مثل فقدان محددات التنوع). |
| **استدعاء `ws.Calculate()` بعد ضبط الصيغ** | بدون حساب صريح، قد يبقى نطاق التوسيع فارغاً عند فحص المصنف برمجياً. |
| **وضع قوالب Smart Marker على ورقة نظيفة** | خلط القوالب مع بيانات موجودة قد يسبب إدراج صفوف غير متوقع. استخدم ورقة مخصصة إذا أمكن. |
| **الاهتمام بمسارات الملفات** | استخدم `Path.Combine(Environment.CurrentDirectory, "output.pdf")` لتجنب المسارات الصلبة على أجهزة مختلفة. |
| **التحقق من الإصدار** | `FontVariationSelectors` متاح فقط منذ الإصدار 25.8؛ الإصدارات الأقدم ستتجاهل الخاصية دون إلقاء استثناء. |

## الخطوات التالية

الآن بعد أن عرفت كيفية **إنشاء مصنف Excel**، **توسيع مصفوفة ديناميكية**، و**حفظ المصنف كملف PDF**، يمكنك استكشاف:

* إضافة مخططات أو صور قبل تحويل الملف إلى PDF.
* تصدير نفس المصنف إلى صيغ أخرى (مثل HTML، CSV) باستخدام overloads الخاصة بـ `Save`.
* استخدام **تعبيرات Smart Marker** (`${Orders.Total:SUM(Items.Price)}`) لحساب التجميعات مباشرة.
* دمج هذا الكود في API مبني على ASP.NET Core لتمكين المستخدمين من تنزيل PDF المولد مباشرة من نقطة نهاية ويب.

---

**ملخص** – يوضح لك هذا الدرس كيفية **إنشاء مصنف Excel**، واستخدام **دالة EXPAND** لتوسيع **مصفوفة ديناميكية**، وإدراج **Smart Marker** يعمل مع مصدر بيانات متداخل، وأخيراً **حفظ المصنف كملف PDF** مع الحفاظ على ميزات الخط المتقدمة. يمكن نسخ المثال الكامل القابل للتنفيذ إلى أي مشروع C# وتعديله ليتناسب مع هياكل البيانات الخاصة بك. برمجة سعيدة!

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مورد يتضمن أمثلة شفرة كاملة مع شروحات خطوة‑بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [Create and Save Excel Workbook as PDF in ASP.NET Using Aspose.Cells](/cells/english/net/workbook-operations/create-save-excel-workbook-pdf-aspnet-aspose-cells/)
- [How to Create and Save an Excel Workbook as ODS Using Aspose.Cells for .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)
- [How to Create and Save an Excel Workbook as SVG using Aspose.Cells for Java](/cells/english/java/workbook-operations/create-save-workbook-svg-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}