---
category: general
date: 2026-03-25
description: تعلم كيفية تكرار العناصر في Excel باستخدام C#. يوضح هذا الدليل كيفية
  إنشاء صفوف Excel بشكل ديناميكي وتعبئة قالب Excel باستخدام C# لأي مجموعة.
draft: false
keywords:
- how to repeat items in excel
- generate excel rows dynamically
- populate excel template c#
language: ar
og_description: كيف تُكرّر العناصر في Excel باستخدام C#؟ اتبع هذا الدرس الكامل لإنشاء
  صفوف Excel بشكل ديناميكي وتعبئة قالب Excel باستخدام C# بسهولة.
og_title: كيفية تكرار العناصر في إكسل – دليل C# خطوة بخطوة
tags:
- C#
- Excel automation
- Aspose.Cells
title: كيفية تكرار العناصر في إكسل – إنشاء صفوف ديناميكي باستخدام C#
url: /ar/net/row-and-column-management/how-to-repeat-items-in-excel-dynamic-row-generation-with-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تكرار العناصر في Excel – إنشاء صفوف ديناميكية باستخدام C#

هل تساءلت يومًا **كيف تُكرر العناصر في Excel** دون الحاجة إلى نسخ الصفوف يدويًا؟ ربما لديك قائمة طلبات، كل طلب يحتوي على عدة بنود، وتحتاج إلى ورقة عمل مرتبة تتوسع تلقائيًا. في هذا الدرس ستشاهد ذلك بالضبط: سنُولِّد صفوف Excel ديناميكيًا ونُـ“populate an Excel template C#” باستخدام ميزة Smart Marker القوية في Aspose.Cells.

سنتبع سيناريو واقعي، نبني نموذج بيانات صغير، ونراقب المكتبة تُحوِّل القالب إلى ورقة مكتملة. في النهاية ستتمكن من تكرار العناصر في Excel لأي مجموعة، سواء كان طلبًا واحدًا أو كتالوجًا ضخمًا. لا إطالة—حل عملي يمكنك نسخه ولصقه في مشروعك.

## المتطلبات المسبقة

- .NET 6.0 أو أحدث (الكود يعمل أيضًا على .NET Framework 4.7+)
- Visual Studio 2022 (أو أي بيئة تطوير تفضّلها)
- حزمة **Aspose.Cells for .NET** عبر NuGet (`Install-Package Aspose.Cells`)
- فهم أساسي لأنواع C# المجهولة (anonymous types)

إذا كان أي من هذه مفقودًا، فقط أضف حزمة NuGet وستكون جاهزًا. المكتبة مُدارة بالكامل، لذا لا تحتاج إلى COM interop أو تثبيت Office.

---

## الخطوة 1: تعريف قالب Smart Marker – جوهر “repeat items in Excel”

أول شيء نحتاجه هو خلية قالب تُخبر Aspose.Cells كيف يتكرر عبر مجموعتنا. يستخدم Smart Markers بناءً بسيطًا للعنصر النائب يُوضع مباشرة داخل ورقة العمل.

```csharp
// Put the template into cell A1
worksheet.Cells["A1"].PutValue(
    "${Orders:Repeat}\n" +          // Start repeating the Orders collection
    "   ${Item:Repeat}\n" +        // For each Order, repeat the Item collection
    "      ${Item.Name}\n" +       // Insert the Name of each Item
    "   ${/Item}\n" +              // End Item repeat block
    "${/Orders}");                 // End Orders repeat block
```

**لماذا هذا مهم:** العلامة `${Orders:Repeat}` تخبر المعالج بالتكرار عبر مصفوفة `Orders`. داخل هذا التكرار نبدأ كتلة تكرار أخرى لـ `Item`. في كل مرة تُنفّذ فيها الحلقة الداخلية، يُستبدل `${Item.Name}` بالاسم الفعلي، مثل “Apple” أو “Banana”. عندما ينتهي المعالج، يتوسع القالب إلى عدد الصفوف المطلوب—وهو بالضبط ما تحتاجه **لإنشاء صفوف Excel ديناميكيًا**.

> **نصيحة احترافية:** حافظ على المسافات داخل السلسلة؛ فهي تُترجم إلى محاذاة صفوف صحيحة في الورقة النهائية.

## الخطوة 2: بناء نموذج بيانات مطابق – “populate excel template c#” ببساطة

قالبنا يتوقع كائنًا يحتوي على خاصية `Orders`، كل طلب يحتوي على مصفوفة `Item`. سنُنشئ كائنًا مجهولًا يعكس هذا الشكل:

```csharp
// Create a simple data model that matches the template
var dataModel = new
{
    Orders = new[]
    {
        new
        {
            Item = new[]
            {
                new { Name = "Apple" },
                new { Name = "Banana" }
            }
        },
        // You can add more orders here – the template will repeat automatically
        new
        {
            Item = new[]
            {
                new { Name = "Orange" },
                new { Name = "Grape" },
                new { Name = "Mango" }
            }
        }
    }
};
```

**لماذا هذا مهم:** يجب أن يتطابق هيكل الكائن المجهول تمامًا مع العلامات. إذا فاتك خاصية أو سميت بطريقة مختلفة، سيتجاهل محرك Smart Marker ذلك بصمت، مما يترك صفوفًا فارغة. هذه فخ شائع عند محاولة **populate excel template c#** للمرة الأولى.

## الخطوة 3: تشغيل معالج Smart Marker – المحرك الذي يكرر العناصر

الآن بعد أن أصبح لدينا قالب ونموذج بيانات، نمررهما إلى Aspose.Cells. يمر المعالج عبر ورقة العمل، يوسّع كتل التكرار، ويكتب القيم.

```csharp
// Process the template with the data model
worksheet.SmartMarkerProcessor.Process(dataModel);
```

هذا هو كل الكود الذي تحتاجه **لتكرار العناصر في Excel**. بعد انتهاء الاستدعاء، ستحتوي ورقة العمل على:

| A (generated) |
|---------------|
| Apple         |
| Banana        |
| Orange        |
| Grape         |
| Mango         |

كل عنصر يظهر في صف خاص به، بغض النظر عن عدد الطلبات أو العناصر التي أضفتها إلى النموذج.

## مثال عملي كامل – من البداية حتى النهاية

فيما يلي تطبيق console كامل جاهز للتنفيذ يوضح التدفق بالكامل. انسخه إلى مشروع C# جديد، أضف حزمة Aspose.Cells عبر NuGet، وشغّله. سيظهر ملف `Output.xlsx` في مجلد `bin`.

```csharp
using System;
using Aspose.Cells;

namespace ExcelSmartMarkerDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create a new workbook and get the first worksheet
            var workbook = new Workbook();
            var worksheet = workbook.Worksheets[0];

            // 2️⃣ Define the Smart Marker template (Step 1)
            worksheet.Cells["A1"].PutValue(
                "${Orders:Repeat}\n" +
                "   ${Item:Repeat}\n" +
                "      ${Item.Name}\n" +
                "   ${/Item}\n" +
                "${/Orders}");

            // 3️⃣ Build the data model (Step 2)
            var dataModel = new
            {
                Orders = new[]
                {
                    new
                    {
                        Item = new[]
                        {
                            new { Name = "Apple" },
                            new { Name = "Banana" }
                        }
                    },
                    new
                    {
                        Item = new[]
                        {
                            new { Name = "Orange" },
                            new { Name = "Grape" },
                            new { Name = "Mango" }
                        }
                    }
                }
            };

            // 4️⃣ Process the template (Step 3)
            worksheet.SmartMarkerProcessor.Process(dataModel);

            // 5️⃣ Save the result
            workbook.Save("Output.xlsx");
            Console.WriteLine("Excel file generated! Open Output.xlsx to see the repeated items.");
        }
    }
}
```

**الناتج المتوقع:** افتح `Output.xlsx` وسترى عمودًا يحتوي على أسماء الفواكه الخمسة، كل واحدة في صف منفصل. لا حاجة للنسخ اليدوي.

### ماذا لو كانت المجموعة فارغة؟

إذا كانت `Orders` أو أي مصفوفة `Item` فارغة، يتخطى محرك Smart Marker الكتلة ولا يُنشئ صفوفًا. هذا مفيد عندما تحتاج إلى **إنشاء صفوف Excel ديناميكيًا** بناءً على بيانات اختيارية—لن يظهر شيء إضافي.

### التعامل مع مجموعات بيانات ضخمة

لآلاف الصفوف، يظل المعالج سريعًا لأنه يعمل في الذاكرة ويكتب مباشرةً إلى المصنف. مع ذلك، قد ترغب في:

- تعطيل الحساب (`workbook.CalculateFormula = false`) قبل المعالجة.
- استخدام `MemoryStream` إذا كنت تحتاج لإرجاع الملف عبر API ويب دون كتابة على نظام الملفات.

## المشكلات الشائعة وكيفية تجنّبها

| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| العلامات لا تتوسع | اسم الخاصية مكتوب بشكل خاطئ أو بحروف غير صحيحة | تأكد من أن أسماء خصائص الكائن المجهول تطابق العلامات تمامًا (`Orders`, `Item`, `Name`). |
| ظهور صفوف فارغة | وجود أحرف سطر جديدة زائدة داخل سلسلة القالب | احذف `\n` الزائدة أو حافظ على القالب مختصرًا. |
| المعالج يرمي `NullReferenceException` | النموذج يحتوي على `null` لمجموعة | احمِ من `null` بتهيئة مصفوفات فارغة (`new object[0]`). |
| ملف الإخراج فاسد | عدم حفظ المصنف بشكل صحيح (مثلاً باستخدام صيغة خاطئة) | استخدم `workbook.Save("file.xlsx")` مع امتداد `.xlsx`. |

## توسيع القالب – أكثر من مجرد أسماء

يدعم Smart Markers أي خاصية، صيغ، وحتى كتل شرطية. على سبيل المثال، لإضافة عمود السعر:

```csharp
worksheet.Cells["A1"].PutValue(
    "${Orders:Repeat}\n" +
    "   ${Item:Repeat}\n" +
    "      ${Item.Name}\t${Item.Price}\n" +
    "   ${/Item}\n" +
    "${/Orders}");
```

وتحديث نموذج البيانات:

```csharp
new { Name = "Apple", Price = 0.99M },
new { Name = "Banana", Price = 0.59M }
```

ستكون النتيجة عمودان—واحد للاسم، وآخر للسعر—مُولَّدان **ديناميكيًا** مرة أخرى.

## الخلاصة

الآن لديك حل كامل ومستقل لـ **كيفية تكرار العناصر في Excel** باستخدام C#. عبر تعريف قالب Smart Marker، ومطابقته بنموذج بيانات مناسب، واستدعاء `SmartMarkerProcessor.Process`، يمكنك **إنشاء صفوف Excel ديناميكيًا** لأي مجموعة وتطبيق **populate excel template c#** بسهولة.

ما الخطوة التالية؟ جرّب إضافة إجماليات، تنسيق شرطي، أو تصدير نفس البيانات إلى CSV. نفس النمط يعمل مع المجموعات المتداخلة، التجميع، وحتى الكائنات المخصصة—فلا تتردد في التجربة.

إذا وجدت هذا الدليل مفيدًا، أعطه نجمة على GitHub، شاركه مع زملائك، أو اترك تعليقًا أدناه. برمجة سعيدة، واستمتع بقوة توليد Excel الآلي! 

![Screenshot of generated Excel rows showing how to repeat items in Excel](/images/repeat-items-excel.png "how to repeat items in Excel")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}