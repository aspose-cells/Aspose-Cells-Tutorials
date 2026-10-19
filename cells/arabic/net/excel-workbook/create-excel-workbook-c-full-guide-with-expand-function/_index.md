---
category: general
date: 2026-06-08
description: إنشاء مصنف Excel باستخدام C# خطوة بخطوة وتعلم كيفية استخدام دالة EXPAND
  في Excel للنطاقات الديناميكية. مثالي لمطوري .NET.
draft: false
keywords:
- create excel workbook c#
- use expand function in excel
language: ar
og_description: إنشاء مصنف Excel باستخدام C# مع مثال واضح واكتشف كيفية استخدام دالة EXPAND في
  Excel لإنشاء مصفوفات ديناميكية.
og_title: إنشاء مصنف إكسل C# – دليل برمجة شامل
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: Create Excel workbook C# step‑by‑step and learn how to use expand function
    in Excel for dynamic ranges. Perfect for .NET developers.
  headline: Create Excel Workbook C# – Full Guide with Expand Function
  type: TechArticle
- description: Create Excel workbook C# step‑by‑step and learn how to use expand function
    in Excel for dynamic ranges. Perfect for .NET developers.
  name: Create Excel Workbook C# – Full Guide with Expand Function
  steps:
  - name: '`SEQUENCE(3)` produces a vertical array `{1;2;3}`.'
    text: '`SEQUENCE(3)` produces a vertical array `{1;2;3}`.'
  - name: '`EXPAND(...,5,5)` tells Excel to grow that array to 5 rows and 5 columns.'
    text: '`EXPAND(...,5,5)` tells Excel to grow that array to 5 rows and 5 columns.'
  - name: The result is a 5 × 5 grid where the first three rows contain the numbers
      1‑3 repeated across columns, and the remaining two rows are blank.
    text: The result is a 5 × 5 grid where the first three rows contain the numbers
      1‑3 repeated across columns, and the remaining two rows are blank.
  - name: '**Creates an Excel workbook C#** using Aspose.Cells.'
    text: '**Creates an Excel workbook C#** using Aspose.Cells.'
  - name: '**Uses the EXPAND function in Excel** to turn a 3‑row array into a 5 × 5
      block.'
    text: '**Uses the EXPAND function in Excel** to turn a 3‑row array into a 5 × 5
      block.'
  - name: Adds a cotangent formula (`COT(PI()/4)`).
    text: Adds a cotangent formula (`COT(PI()/4)`).
  - name: Saves the file and optionally auto‑fits columns.
    text: Saves the file and optionally auto‑fits columns.
  type: HowTo
- questions:
  - answer: Absolutely. Aspose.Cells targets .NET Standard 2.0, which is compatible
      with both .NET Core and the classic Framework.
    question: Does this work with .NET Framework 4.8?
  - answer: Use `ws.Protect(ProtectionType.All, "yourPassword");` before saving.
    question: What if I need to protect the sheet?
  - answer: 'Yes—`workbook.Save(stream, SaveFormat.Xlsx);` is handy for web APIs that
      return the file as a download. --- ## TL;DR We built a **complete C# console
      app** that: 1. **Creates an Excel workbook C#** using Aspose.Cells. 2. **Uses
      the EXPAND function in Excel** to turn a 3‑row array into a 5 × 5 block.'
    question: Can I write the workbook directly to a `MemoryStream`?
  type: FAQPage
tags:
- csharp
- excel
- aspose-cells
- .net
title: إنشاء مصنف إكسل C# – دليل كامل مع وظيفة التوسيع
url: /ar/net/excel-workbook/create-excel-workbook-c-full-guide-with-expand-function/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء دفتر عمل Excel C# – دليل كامل مع دالة EXPAND

هل تساءلت يومًا كيف **إنشاء دفتر عمل Excel C#** دون التعامل مع COM interop أو العبث بـ XML؟ لست الوحيد. في العديد من مشاريع .NET نحتاج إلى إنشاء جدول بيانات، ملئه بالمعادلات، وتسليمه للمستخدمين غير التقنيين. الخبر السار؟ باستخدام مكتبة حديثة مثل **Aspose.Cells** العملية كلها سهلة كقطعة من الكعك.

في هذا الدرس سنستعرض مثالًا كاملًا وقابلًا للتنفيذ ي **إنشاء دفتر عمل Excel C#**، يضيف بضع صيغ—بما في ذلك **استخدام دالة EXPAND في Excel**—ويحفظ الملف حتى تتمكن من فتحه في Excel فورًا. في النهاية ستعرف ليس فقط *ما* يجب كتابته، بل *لماذا* كل سطر مهم، وستحصل على قالب يمكنك نسخه إلى أي مشروع.

## المتطلبات المسبقة

- .NET 6 SDK (أو أي نسخة حديثة من .NET) مثبت.
- بيئة تطوير متوافقة مع NuGet (Visual Studio، VS Code، Rider، إلخ).
- حزمة NuGet **Aspose.Cells** – توفر الفئات `Workbook` و `Worksheet` المستخدمة في الشيفرة.
- إلمام أساسي بـ C#؛ لا حاجة لخبرة سابقة في Excel.

هل لديك كل ذلك؟ رائع—هيا نبدأ.

## الخطوة 1: إعداد المشروع وإضافة Aspose.Cells

أولاً، أنشئ تطبيقًا من نوع console وأضف المكتبة.

```bash
dotnet new console -n ExcelDemo
cd ExcelDemo
dotnet add package Aspose.Cells
```

> **نصيحة احترافية:** إذا كنت على شبكة شركة، قد تحتاج إلى تكوين بروكسي لـ NuGet. حزمة Aspose.Cells خفيفة الوزن، لذا يكتمل التثبيت خلال ثوانٍ.

الآن افتح `Program.cs`. سترى طريقة `Main` الافتراضية—استبدلها بالهيكل أدناه.

```csharp
using System;
using Aspose.Cells;

namespace ExcelDemo
{
    class Program
    {
        static void Main()
        {
            // All of our Excel logic will go here.
        }
    }
}
```

سطر `using Aspose.Cells;` يجلب فئات جداول البيانات إلى النطاق. إذا نسيت إضافته، سيشتكي المترجم بأن `Workbook` غير معرف—وهو ما سنتجنبه لاحقًا.

## الخطوة 2: إنشاء دفتر عمل Excel C# والوصول إلى الورقة الأولى

مع جاهزية المشروع، يمكننا أخيرًا **إنشاء دفتر عمل Excel C#**. مُنشئ `Workbook` يمنحنا دفتر عمل جديد فارغ، ومؤشر `Worksheets[0]` يُعيد الورقة الافتراضية (المسمَّاة “Sheet1”).

```csharp
// Step 2: Create a new workbook and get the first worksheet
Workbook workbook = new Workbook();               // creates an empty .xlsx file in memory
Worksheet ws = workbook.Worksheets[0];            // reference to the first (default) sheet
```

لماذا نأخذ الورقة الأولى صراحةً؟ لأن العديد من واجهات برمجة التطبيقات اللاحقة (مثل تعيين الصيغ) تتطلب كائن `Worksheet`، وليس مجرد `Workbook`. هذا يجعل الشيفرة أوضح لأي شخص يقرأها لاحقًا.

## الخطوة 3: استخدام دالة EXPAND في Excel لملء نطاق ديناميكي

الآن يأتي العنصر الرئيسي: **استخدام دالة EXPAND في Excel**. دالة `EXPAND` (متوفرة بدءًا من Excel 365) تأخذ مصفوفة مصدر وتملأها إلى الحجم المطلوب. في مثالنا سنبدأ بمصفوفة عمودية من 3 صفوف تم إنشاؤها بواسطة `SEQUENCE(3)` ونوسعها إلى كتلة 5 × 5.

```csharp
// Step 3: Insert the EXPAND formula into cell A1
ws.Cells["A1"].Formula = "EXPAND(SEQUENCE(3),5,5)";
```

ماذا يحدث فعليًا؟

1. `SEQUENCE(3)` ينتج مصفوفة عمودية `{1;2;3}`.
2. `EXPAND(...,5,5)` يطلب من Excel توسيع تلك المصفوفة إلى 5 صفوف و5 أعمدة.
3. النتيجة هي شبكة 5 × 5 حيث تحتوي الصفوف الثلاثة الأولى على الأرقام 1‑3 مكررة عبر الأعمدة، والصفوف المتبقية (صفين) فارغة.

نظرًا لأننا نكتب الصيغة كسلسلة نصية، يقوم Excel بتقييمها *عند فتح الملف*، وليس أثناء التشغيل. هذا يعني أن دفتر العمل يبقى خفيفًا، وأي تغييرات في مصفوفة المصدر ستنتقل تلقائيًا.

> **حالة خاصة:** إذا فتح المستخدم دفتر العمل في نسخة قديمة من Excel لا تدعم `EXPAND`، ستظهر الخلية `#NAME?`. لتجنب ذلك يمكنك تغليف الصيغة بـ `IFERROR`، لكن في البيئات الحديثة من الآمن الاعتماد على الدالة.

## الخطوة 4: إضافة صيغة Cotangent لتكملة المثال

لنضيف صيغة أخرى لتوضيح مدى سهولة إضافة تعبيرات رياضية. سنحسب cotangent للزاوية π/4، والتي تساوي بالضبط `1`.

```csharp
// Step 4: Insert a cotangent calculation in cell B1
ws.Cells["B1"].Formula = "COT(PI()/4)";
```

دالة `COT` في Excel ليست شائعة كما `SIN` أو `COS`، لكنها مثالية لتدفقات العمل المثلثية. عند فتح دفتر العمل، ستظهر الخلية **B1** القيمة `1`.

## الخطوة 5: حفظ دفتر العمل والتحقق من النتيجة

كل هذا العمل سيكون بلا فائدة إذا لم نحفظ الملف. طريقة `Save` تكتب دفتر العمل الموجود في الذاكرة إلى القرص. اختر مجلدًا لديك صلاحية كتابة فيه، ومنح الملف اسمًا مناسبًا.

```csharp
// Step 5: Save the workbook to the output folder
string outputPath = @"./output.xlsx";
workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to {outputPath}");
```

شغّل البرنامج:

```bash
dotnet run
```

يجب أن ترى رسالة في وحدة التحكم تؤكد الحفظ. افتح `output.xlsx` في Excel، وستلاحظ ما يلي:

- الخلايا **A1:E5** مملوءة بالتسلسل الموسع (1,2,3 في الصفوف الثلاثة الأولى، وفراغات في الصفوف 4‑5).
- الخلية **B1** تعرض القيمة `1` من صيغة cotangent.

هذه هي الدورة الكاملة: **إنشاء دفتر عمل Excel C#**، تضمين الصيغ، وإنتاج جدول بيانات قابل للاستخدام.

![لقطة شاشة لدفتر Excel المُنشأ تُظهر المصفوفة الموسعة ونتيجة cotangent](/images/create-excel-workbook-csharp.png "مثال إنشاء دفتر عمل excel c#")

*نص بديل للصورة: إنشاء دفتر عمل excel c# – عرض للجدول المملوء.*

## الخطوة 6: اختياري – ضبط الأعمدة تلقائيًا لمظهر مصقول

إذا كنت تخطط لتوزيع الملف على المستخدمين النهائيين، فإن الضبط التلقائي السريع للأعمدة يمنحه مظهرًا احترافيًا.

```csharp
// Optional: Auto‑fit all columns in the used range
ws.AutoFitColumns(0, ws.Cells.MaxColumn);
```

هذا السطر يمر عبر كل عمود يحتوي على بيانات ويضبط عرضه وفقًا لأطول قيمة. إنها لمسة بسيطة، لكنها تمنع حدوث الفائض “…###” عندما تكون الأرقام أوسع من عرض العمود الافتراضي.

## الخطوة 7: الخاتمة والخطوات التالية

تهانينا—لقد أتقنت الآن كيفية **إنشاء دفتر عمل excel c#** من الصفر وتعلمت كيفية **استخدام دالة EXPAND في excel** لتوليد مصفوفات ديناميكية. الشيفرة بسيطة عمدًا لتتمكن من نسخها ولصقها في أي مشروع، لكن المفاهيم قابلة للتوسع:

- **مصادر بيانات ديناميكية:** استبدل `SEQUENCE(3)` بإشارة إلى نطاق آخر أو جدول مسمى.
- **تنسيق شرطي:** استخدم `ws.Cells["A1:E5"].Style` لإضافة ألوان بناءً على القيم.
- **الرسوم البيانية والرسومات:** يمكن لـ Aspose.Cells تضمين مخططات، صور، وحتى جداول محورية.

لا تتردد في التجربة—غيّر أبعاد `EXPAND`، جرّب `FILTER` أو `SORT`، أو ربط صيغ متعددة معًا. المكتبة تتعامل مع كل ذلك دون الحاجة إلى التعامل مع تنسيق OpenXML منخفض المستوى.

---

### الأسئلة المتكررة

**س: هل يعمل هذا مع .NET Framework 4.8؟**  
ج: بالتأكيد. Aspose.Cells تستهدف .NET Standard 2.0، وهي متوافقة مع كل من .NET Core والإطار الكلاسيكي.

**س: ماذا لو احتجت لحماية الورقة؟**  
ج: استخدم `ws.Protect(ProtectionType.All, "yourPassword");` قبل الحفظ.

**س: هل يمكن كتابة دفتر العمل مباشرة إلى `MemoryStream`؟**  
ج: نعم—`workbook.Save(stream, SaveFormat.Xlsx);` مفيد لواجهات برمجة التطبيقات الويب التي تُعيد الملف كتحميل.

## TL;DR

لقد بنينا **تطبيق console كامل بـ C#** الذي:

1. **ينشئ دفتر عمل Excel C#** باستخدام Aspose.Cells.  
2. **يستخدم دالة EXPAND في Excel** لتحويل مصفوفة من 3 صفوف إلى كتلة 5 × 5.  
3. يضيف صيغة cotangent (`COT(PI()/4)`).  
4. يحفظ الملف ويضبط الأعمدة تلقائيًا اختياريًا.

الآن لديك أساس قوي لأي مهمة أتمتة تتضمن إنشاء ملفات Excel من .NET. برمجة سعيدة، ولتظل جداولك خالية دائمًا من الأخطاء!

## ما الذي ينبغي أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مورد يتضمن أمثلة شيفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [كيفية إنشاء نطاقات مسماة محلية للدفتر في Excel باستخدام Aspose.Cells .NET](/cells/english/net/range-management/excel-workbook-scoped-named-ranges-aspose-cells-net/)
- [كيفية إنشاء واستخدام نطاقات الاتحاد في Excel مع Aspose.Cells .NET (دليل C#)](/cells/english/net/range-management/excel-union-range-aspose-cells-net/)
- [إنشاء دفتر عمل Excel مع مخططات باستخدام Aspose.Cells .NET | دليل خطوة بخطوة](/cells/english/net/charts-graphs/create-excel-workbook-charts-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}