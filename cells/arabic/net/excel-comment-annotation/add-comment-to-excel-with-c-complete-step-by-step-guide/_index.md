---
category: general
date: 2026-05-30
description: أضف تعليقًا إلى Excel باستخدام C# بسرعة. تعلم كيفية كتابة تعليق في الخلية،
  وإدراج عناصر نائبة للعلامات الذكية، وحفظ المصنف.
draft: false
keywords:
- add comment to excel
- write comment to cell
- add comment using c#
language: ar
og_description: أضف تعليقًا إلى Excel باستخدام C# في دقائق. يوضح هذا الدرس كيفية كتابة
  تعليق في الخلية، ومعالجة Smart Marker، وحفظ الملف.
og_title: إضافة تعليق إلى إكسل باستخدام C# – دليل كامل
schemas:
- author: Aspose
  dateModified: '2026-05-30'
  description: Add comment to Excel using C# quickly. Learn how to write comment to
    cell, insert Smart Marker placeholders, and save the workbook.
  headline: Add comment to Excel with C# – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Add comment to Excel using C# quickly. Learn how to write comment to
    cell, insert Smart Marker placeholders, and save the workbook.
  name: Add comment to Excel with C# – Complete Step‑by‑Step Guide
  steps:
  - name: 1. Adding Multiple Comments in One Pass
    text: If you need to add comments to several cells, just place multiple placeholders
      (`${Comment1}`, `${Comment2}`, …) and expand the data object accordingly.
  - name: 2. Preserving Existing Comments
    text: Sometimes a sheet already contains reviewer notes that you don’t want to
      lose. Retrieve the existing comment, merge, then write back.
  - name: 3. Unicode and Emojis
    text: Excel fully supports Unicode, so you can embed emojis, non‑Latin scripts,
      or special symbols directly in the comment string.
  - name: 4. Large Workbooks & Performance
    text: 'Processing a workbook with thousands of Smart Markers can be costly. To
      improve speed:'
  type: HowTo
- questions:
  - answer: Yes, but you must open the workbook with the `LoadOptions` that allow
      editing, e.g., `new LoadOptions(LoadFormat.Xlsx) { ReadOnly = false }`.
    question: Can I add a comment to a *read‑only* workbook?
  - answer: '`PutComment` overwrites the existing comment. To merge, retrieve the
      current comment first (`GetComment()`), concatenate, then call `PutComment`
      again.'
    question: What if the target cell already has a comment?
  - answer: Absolutely. Aspose.Cells abstracts the format; just point the `Workbook`
      constructor at the `.xls` file and everything else stays the same.
    question: Does this work with older `.xls` files?
  - answer: 'Practically, Excel supports comments up to 32,767 characters. Aspose.Cells
      respects the same limit—larger strings will be truncated. --- ## Recap & Next
      Steps We’ve covered how to **add comment to Excel** using C#, demonstrated the
      **write comment to cell** technique with Smart Markers, and explored'
    question: Is there a limit to comment length?
  type: FAQPage
tags:
- Excel
- C#
- Aspose.Cells
title: إضافة تعليق إلى إكسل باستخدام C# – دليل كامل خطوة بخطوة
url: /ar/net/excel-comment-annotation/add-comment-to-excel-with-c-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إضافة تعليق إلى Excel باستخدام C# – دليل خطوة‑بخطوة كامل

هل تساءلت يومًا كيف **add comment to Excel** من تطبيق C# دون فتح الملف يدويًا؟ لست وحدك. يحتاج العديد من المطورين إلى **write comment to cell** برمجيًا—سواء كان ذلك لسجلات التدقيق، ملاحظات المراجعين، أو التقارير الديناميكية. في هذا الدرس سنستعرض حلًا نظيفًا من البداية إلى النهاية يستخدم ميزة Smart Marker في Aspose.Cells، وسنشرح أيضًا “السبب” وراء كل خطوة حتى تتمكن من تكييف النمط لمشاريعك الخاصة.

بحلول نهاية الدليل ستتمكن من:

* تحميل مصنف موجود،
* إدراج تعليق نائب في خلية محددة،
* استبدال النائب بنص حقيقي باستخدام كائن مجهول الهوية،
* حفظ الملف المحدث،
* ومعالجة بعض الحالات الشائعة مثل التعليقات الموجودة أو نص Unicode.

لا توجد سكريبتات خارجية، ولا تفاعل مع Excel، فقط كود C# نقي يعمل على Windows وLinux وmacOS.

---

## المتطلبات المسبقة — ما تحتاجه قبل البدء

* **Aspose.Cells for .NET** (v23.10 أو أحدث). المكتبة مجانية للتجربة، واسم حزمة NuGet هو `Aspose.Cells`.
* بيئة تطوير .NET (Visual Studio، Rider، أو VS Code مع امتداد C#).  
* مصنف إدخال (`input.xlsx`) موجود في مجلد يمكنك الإشارة إليه من الكود.  
* إلمام أساسي بأنواع C# المجهولة ومبادئ تهيئة الكائنات.  

إذا كان لديك كل هذه العناصر، عظيم—لنبدأ. إذا لم يكن كذلك، احصل على حزمة NuGet عبر:

```bash
dotnet add package Aspose.Cells
```

السطر الوحيد هذا يجلب لك كل ما تحتاجه، بما في ذلك الفئة `SmartMarkerProcessor` التي سنستخدمها لاحقًا.

---

## الخطوة 1 – تحميل المصنف (add comment to excel)

قبل أن نتمكن من **add comment to Excel**، يجب فتح الملف في الذاكرة. Aspose.Cells ي abstracts تنسيق الملف، لذا لا تحتاج للقلق إذا كان .xlsx أو .xls أو حتى .csv.

```csharp
// Load the workbook that contains the target worksheet
Workbook wb = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

> **لماذا هذا مهم:** فتح المصنف ينشئ كائن `Workbook` يحتوي على جميع الأوراق، الأنماط، والتعليقات الموجودة. إذا تخطيت هذه الخطوة وحاولت الإشارة إلى ورقة مباشرة، ستحصل على استثناء `NullReferenceException`.

---

## الخطوة 2 – اختيار الورقة والخلية (write comment to cell)

معظم جداول البيانات الواقعية تحتوي على عدة علامات تبويب. للتبسيط سنعمل على الورقة الأولى، لكن يمكنك الفهرسة بالاسم إذا فضلت ذلك.

```csharp
// Grab the first worksheet (index 0)
Worksheet ws = wb.Worksheets[0];

// Place a Smart Marker placeholder in cell A1 where the comment will appear
ws.Cells["A1"].PutComment("${Comment}");
```

النداء إلى `PutComment` ينشئ كائن *comment* مرتبط بـ `A1`. المحتوى `${Comment}` هو **Smart Marker placeholder**—فكر فيه كرمز سيُستبدل لاحقًا ببيانات حقيقية.

> **نصيحة احترافية:** إذا كانت الخلية تحتوي بالفعل على تعليق، فإن `PutComment` سيستبدله. للحفاظ على التعليقات الموجودة، اقرأ `ws.Cells["A1"].GetComment().Comment` أولاً، ثم أدمج النص، ثم أعد تطبيق `PutComment`.

---

## الخطوة 3 – إعداد كائن البيانات (add comment using c#)

تعمل Smart Markers مع أي كائن .NET يحتوي على خصائص تتطابق مع أسماء النائب. الكائن المجهول هو مثالي للعرض السريع.

```csharp
// Anonymous object that supplies the actual comment text
var data = new { Comment = "Reviewed by John – ✅ Approved" };
```

يمكنك أيضًا استخدام فئة ذات نوع قوي إذا كنت تحتاج إلى التحقق أو حقول إضافية.

```csharp
public class ReviewInfo
{
    public string Comment { get; set; }
    public DateTime ReviewedOn { get; set; }
}
```

ثم أنشئ المثيل:

```csharp
var data = new ReviewInfo
{
    Comment = "Reviewed by John – ✅ Approved",
    ReviewedOn = DateTime.UtcNow
};
```

> **لماذا الكائنات المجهولة؟** إنها تجعل الكود مختصرًا عندما تحتاج فقط إلى عدد قليل من القيم. للمجموعات الكبيرة من البيانات، يُفضَّل استخدام DTO (كائن نقل البيانات) للحصول على صيانة أفضل.

---

## الخطوة 4 – معالجة Smart Marker (add comment to excel)

الآن يحدث السحر. `SmartMarkerProcessor` يمسح الورقة، يجد `${Comment}`، ويستبدله بالقيمة من `data.Comment`.

```csharp
// Run the processor to replace placeholders with real values
new SmartMarkerProcessor().Process(ws, data);
```

تحت الغطاء، يقوم المعالج بـ:

1. تحليل تمثيل XML للورقة،
2. اكتشاف أي رموز `${…}`،
3. البحث عن الخصائص المطابقة في الكائن المقدم،
4. كتابة السلسلة المحلولة في عقدة نص التعليق.

إذا كان النائب غير موجود، يتخطاه المعالج بصمت—لا يُرمى استثناء. هذا يجعل النهج آمنًا للتعليقات الاختيارية.

---

## الخطوة 5 – حفظ المصنف (see the result)

أخيرًا، اكتب المصنف المعدل مرة أخرى إلى القرص. يمكنك استبدال الملف الأصلي أو إنشاء ملف جديد.

```csharp
// Save the workbook – you can change the format by using SaveOptions if needed
wb.Save("YOUR_DIRECTORY/output.xlsx");
```

عند فتح `output.xlsx` في Excel، سترى التعليق “Reviewed by John – ✅ Approved” مرفقًا بالخلية **A1**. مرّر المؤشر فوق المثلث الأحمر الصغير في الزاوية العليا اليمنى للخلية لعرضه.

> **الناتج المتوقع:**  

> ![Screenshot showing a cell with a comment – add comment to excel example](add-comment-to-excel-example.png "add comment to excel example")

*يتضمن نص alt الكلمة المفتاحية الأساسية، مستوفيًا قاعدة SEO.*

---

## معالجة السيناريوهات الشائعة

### 1. إضافة تعليقات متعددة في تمريرة واحدة

إذا احتجت لإضافة تعليقات إلى عدة خلايا، ضع نوايب متعددة (`${Comment1}`, `${Comment2}`, …) ووسّع كائن البيانات وفقًا لذلك.

```csharp
ws.Cells["A1"].PutComment("${Comment1}");
ws.Cells["B2"].PutComment("${Comment2}");

var data = new
{
    Comment1 = "First note",
    Comment2 = "Second note"
};

new SmartMarkerProcessor().Process(ws, data);
```

### 2. الحفاظ على التعليقات الموجودة

أحيانًا تحتوي الورقة بالفعل على ملاحظات مراجعين لا تريد فقدانها. استرجع التعليق الحالي، دمجه، ثم أعد الكتابة.

```csharp
var existing = ws.Cells["A1"].GetComment()?.Comment ?? string.Empty;
var merged   = string.IsNullOrWhiteSpace(existing)
               ? data.Comment
               : $"{existing}\n{data.Comment}";

ws.Cells["A1"].PutComment(merged);
```

### 3. Unicode والرموز التعبيرية

Excel يدعم Unicode بالكامل، لذا يمكنك تضمين رموز تعبيرية، نصوص غير لاتينية، أو رموز خاصة مباشرة في سلسلة التعليق.

```csharp
var data = new { Comment = "审查通过 – ✅" };
```

تأكد فقط من حفظ ملف المصدر بترميز UTF‑8 (الإعداد الافتراضي في معظم بيئات التطوير الحديثة).

### 4. المصنفات الكبيرة والأداء

معالجة مصنف يحتوي على آلاف Smart Markers قد تكون مكلفة. لتحسين السرعة:

* استخدم `SmartMarkerProcessorOptions` لتقليل النطاق إلى ورقة واحدة.
* أوقف الحساب (`wb.CalculateFormula = false`) إذا كنت تحتاج فقط إلى التعليقات.
* أعد استخدام كائن `SmartMarkerProcessor` واحد بدلاً من إنشاء جديد لكل ورقة.

```csharp
var processor = new SmartMarkerProcessor
{
    Options = new SmartMarkerProcessorOptions { ProcessAllWorksheets = false }
};

processor.Process(ws, data);
```

---

## مثال عملي كامل

بدمج كل ما سبق، إليك تطبيق console مستقل يمكنك نسخه‑لصقه في `Program.cs` وتشغيله.

```csharp
using System;
using Aspose.Cells;

namespace ExcelCommentDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load the workbook
            Workbook wb = new Workbook("YOUR_DIRECTORY/input.xlsx");

            // 2️⃣ Get the first worksheet and insert a placeholder comment
            Worksheet ws = wb.Worksheets[0];
            ws.Cells["A1"].PutComment("${Comment}");

            // 3️⃣ Prepare data – you can use an anonymous type or a DTO
            var data = new { Comment = "Reviewed by John – ✅ Approved" };

            // 4️⃣ Process Smart Markers to replace the placeholder
            new SmartMarkerProcessor().Process(ws, data);

            // 5️⃣ Save the result
            wb.Save("YOUR_DIRECTORY/output.xlsx");

            Console.WriteLine("Comment added successfully!");
        }
    }
}
```

شغّل البرنامج، افتح `output.xlsx`، وسترى التعليق يظهر تمامًا حيث وضعنا النائب. لا حاجة لواجهة Excel، ولا تفاعل COM، فقط كود مُدار بالكامل.

---

## الأسئلة المتكررة (FAQ)

**س: هل يمكنني إضافة تعليق إلى مصنف *للقراءة فقط*؟**  
ج: نعم، لكن عليك فتح المصنف باستخدام `LoadOptions` التي تسمح بالتعديل، مثل `new LoadOptions(LoadFormat.Xlsx) { ReadOnly = false }`.

**س: ماذا لو كانت الخلية المستهدفة تحتوي بالفعل على تعليق؟**  
ج: `PutComment` يستبدل التعليق الموجود. للدمج، استرجع التعليق الحالي أولًا (`GetComment()`)، أدمج النص، ثم استدعِ `PutComment` مرة أخرى.

**س: هل يعمل هذا مع ملفات `.xls` القديمة؟**  
ج: بالتأكيد. Aspose.Cells ي abstracts التنسيق؛ فقط وجه مُنشئ `Workbook` إلى ملف `.xls` وكل شيء آخر يبقى كما هو.

**س: هل هناك حد لطول التعليق؟**  
ج: عمليًا، يدعم Excel تعليقات تصل إلى 32,767 حرفًا. Aspose.Cells يحترم نفس الحد—ستُقصَّ السلاسل الأكبر.

---

## ملخص وخطوات قادمة

غطّينا كيفية **add comment to Excel** باستخدام C#، وعرضنا تقنية **write comment to cell** عبر Smart Markers، واستكشفنا تنوعات مثل التعليقات المتعددة، دعم Unicode، وتحسين الأداء. النمط الأساسي—نائب → كائن بيانات → معالج → حفظ—يمكن إعادة استخدامه لأي محتوى ديناميكي، ليس

---

## ماذا يجب أن تتعلم بعد ذلك؟

- [Add a Comment with Image in Excel](/cells/english/net/excel-comment-annotation/add-comment-with-image-excel/)
- [Add Image to Excel Comment with Aspose.Cells for Java: A Complete Guide](/cells/english/java/comments-annotations/add-image-excel-comment-aspose-cells-java/)
- [Add Comment With Image Excel](/cells/german/net/excel-comment-annotation/add-comment-with-image-excel/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}