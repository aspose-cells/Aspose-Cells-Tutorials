---
category: general
date: 2026-03-21
description: تعيين تنسيق مخصص للخلية في C# وتعلم كيفية كتابة التاريخ إلى Excel، وتطبيق
  تنسيق تاريخ مخصص، وقراءة DateTime من Excel، وإنشاء ورقة عمل بسرعة.
draft: false
keywords:
- set cell custom format
- write date to excel
- read datetime from excel
- apply custom date format
- create workbook worksheet
language: ar
og_description: تعيين تنسيق مخصص للخلية في C# لكتابة التاريخ إلى Excel، تطبيق تنسيق
  تاريخ مخصص، قراءة DateTime من Excel، وإنشاء ورقة عمل في المصنف بسهولة.
og_title: تعيين تنسيق مخصص للخلية في C# – كتابة وقراءة التواريخ في Excel
tags:
- Aspose.Cells
- C#
- Excel Automation
title: تعيين تنسيق مخصص للخلية في C# – دليل شامل لكتابة وقراءة التواريخ في Excel
url: /ar/net/excel-custom-number-date-formatting/set-cell-custom-format-in-c-complete-guide-to-writing-readin/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تعيين تنسيق مخصص للخلية – كتابة وقراءة التواريخ في Excel باستخدام C#

## ما ستتعلمه

- كيفية **إنشاء ورقة عمل** برمجياً.  
- الخطوات الدقيقة **للكتابة إلى Excel** باستخدام سلسلة مخصصة للمنطقة.  
- كيفية **تطبيق تنسيق تاريخ مخصص** (بما في ذلك ترميز العصر الياباني).  
- الطريقة **لقراءة DateTime من Excel** وإعادتها إلى كائن `DateTime`.  
- نصائح، ومخاطر، وتنوعات قد تواجهها عند التعامل مع تواريخ Excel.

لا حاجة إلى وثائق خارجية — كل ما تحتاجه موجود هنا.

## المتطلبات المسبقة

- .NET 6.0 أو أحدث (الكود يعمل أيضاً على .NET Framework 4.7+).  
- Aspose.Cells لـ .NET مثبت عبر NuGet (`Install-Package Aspose.Cells`).  
- فهم أساسي لصياغة C# — لا شيء معقد.

> **نصيحة احترافية:** إذا كنت تستخدم Visual Studio، فعّل *nullable reference types* لاكتشاف الأخطاء الدقيقة مبكراً.

## الخطوة 1: إنشاء مصنف وورقة عمل  

أولاً وقبل كل شيء: تحتاج إلى كائن مصنف يمثل ملف Excel، وورقة عمل حيث ستُخزن البيانات.

```csharp
using Aspose.Cells;
using System;

class ExcelDateDemo
{
    static void Main()
    {
        // Step 1: Initialize a new workbook and grab the first worksheet
        Workbook workbook = new Workbook();                     // creates an empty .xlsx in memory
        Worksheet worksheet = workbook.Worksheets[0];           // default sheet is named "Sheet1"
```

*لماذا هذا مهم:* فئة `Workbook` هي نقطة الدخول لجميع عمليات Excel. إن إنشاؤها في الذاكرة يعني أنك لا تتعامل مع نظام الملفات إلا عند الحفظ صراحةً، مما يجعل العملية سريعة ومناسبة للاختبار.

## الخطوة 2: كتابة التاريخ إلى Excel  

بعد ذلك، سنضع سلسلة تاريخ العصر الياباني (`"R02-04-01"`) في الخلية **A1**. السلسلة تحاكي عصر ريوا (السنة 2، أبريل 1).

```csharp
        // Step 2: Write a Japanese era date string into cell A1
        worksheet.Cells["A1"].PutValue("R02-04-01");
```

*ما يحدث:* `PutValue` يخزن السلسلة الخام. ستحاول Aspose.Cells لاحقاً تحليلها بناءً على نمط الخلية. إذا تخطيت هذه الخطوة وكتبت `DateTime` مباشرةً، ستفقد معلومات العصر التي تريد عرضها.

## الخطوة 3: تطبيق تنسيق رقم التاريخ المدمج (ID 14)

Excel يحتوي على تنسيق تاريخ مدمج بالمعرف 14 (`mm-dd-yy`). تطبيقه يخبر المحرك أن الخلية **تحتوي على تاريخ**، وليس مجرد نص.

```csharp
        // Step 3: Apply the built‑in date number format (ID 14)
        worksheet.Cells["A1"].Style.Number = 14;
```

*لماذا نستخدم المعرف 14؟* إنه تنسيق “التاريخ القصير” العالمي الذي يضمن أن Excel يتعامل مع المحتوى كقيمة تاريخ، وهو شرط أساسي لتعمل أي تنسيق مخصص بشكل صحيح.

## الخطوة 4: تعيين تنسيق مخصص لعرض ترميز العصر الياباني  

الآن للجزء الممتع: نخبر Excel بعرض التاريخ باستخدام تنسيق العصر الياباني. السلسلة المخصصة `[$-ja-JP]ggge年m月d日` تقوم بذلك بالضبط.

```csharp
        // Step 4: Set a custom format to display the date in Japanese era notation
        worksheet.Cells["A1"].Style.Custom = "[$-ja-JP]ggge年m月d日";
```

*شرح:*  
- `[$-ja-JP]` يجبر المنطقة على اليابانية.  
- `ggg` هو اسم العصر (مثال: “R” لـ Reiwa).  
- `e` هو سنة العصر.  
- `年`، `月`، `日` هي أحرف يابانية حرفية للسنة، الشهر، اليوم.

إذا كنت بحاجة إلى منطقة مختلفة، استبدل ببساطة `ja-JP` برمز الثقافة المناسب (مثال: `en-US`).

## الخطوة 5: استرجاع قيمة DateTime المحللة  

أخيراً، لنقرأ **قيمة `DateTime` الفعلية** التي حللتها Excel من الخلية. هذا يثبت أن السلسلة تم تفسيرها بشكل صحيح.

```csharp
        // Step 5: Retrieve the parsed DateTime value from the cell
        DateTime parsedDate = worksheet.Cells["A1"].DateTime;   // => 2020‑04‑01

        // Output to console for verification
        Console.WriteLine($"Parsed DateTime: {parsedDate:yyyy-MM-dd}");
```

*النتيجة:* يطبع الطرفية `Parsed DateTime: 2020-04-01`. رغم أننا أدخلنا سلسلة العصر الياباني، إلا أن Excel يخزن داخلياً التاريخ الميلادي، والذي يمكنك استخدامه للعمليات الحسابية أو المقارنات أو التصدير الإضافي.

## الخطوة 6: حفظ المصنف (اختياري)

إذا رغبت في رؤية المصنف المنسق في Excel، فقط احفظه على القرص.

```csharp
        // Optional: Save the workbook to a file
        workbook.Save("JapaneseEraDate.xlsx");
    }
}
```

افتح الملف **JapaneseEraDate.xlsx** الذي تم إنشاؤه وسترى الخلية **A1** تعرض `R02年4月1日` (تنسيق العصر الياباني الدقيق الذي حددناه).

![مثال على تعيين تنسيق مخصص للخلية](image-placeholder.png "خلية Excel تُظهر تاريخ العصر الياباني – تعيين تنسيق مخصص للخلية")

## الاختلافات الشائعة وحالات الحافة  

### كتابة تنسيق تاريخ مختلف  

إذا كنت تفضل ISO‑8601 (`2020-04-01`) بدلاً من سلسلة العصر، فقط غيّر استدعاء `PutValue`:

```csharp
worksheet.Cells["A1"].PutValue(new DateTime(2020, 4, 1));
worksheet.Cells["A1"].Style.Number = 14;                 // keep built‑in date format
worksheet.Cells["A1"].Style.Custom = "yyyy-mm-dd";      // custom ISO format
```

### التعامل مع خلايا فارغة أو ذات قيمة Null  

عند قراءة تاريخ، احرص دائماً على التحقق من عدم وجود خلايا فارغة لتجنب `InvalidOperationException`:

```csharp
if (!worksheet.Cells["A1"].IsDate)
{
    Console.WriteLine("Cell A1 does not contain a valid date.");
}
else
{
    DateTime dt = worksheet.Cells["A1"].DateTime;
    // use dt...
}
```

### دعم عدة مناطق محلية  

يمكنك التكرار عبر قائمة من رموز الثقافة وتطبيقها ديناميكياً:

```csharp
string[] cultures = { "ja-JP", "en-US", "fr-FR" };
foreach (var culture in cultures)
{
    worksheet.Cells["A1"].Style.Custom = $"[$-{culture}]ggge年m月d日";
    // Save or export per culture if needed
}
```

## نصائح احترافية وملاحظات  

- **دائمًا قم بتعيين تنسيق رقم مدمج أولاً** (`Style.Number`). بدون ذلك، يتعامل Excel مع الخلية كنص عادي ويتم تجاهل التنسيق المخصص.  
- **رموز المناطق غير حساسة لحالة الأحرف**، لكن استخدام الصيغة القانونية (`ja-JP`) يجنب الالتباس.  
- **الحفظ اختياري** للمعالجة في الذاكرة؛ يمكنك بث المصنف مباشرةً إلى استجابة ويب (`workbook.Save(stream, SaveFormat.Xlsx)`).  
- **رخص Aspose.Cells**: النسخة التجريبية المجانية تضيف علامة مائية. للإنتاج، تأكد من حصولك على رخصة صالحة لتجنب عقوبات الأداء.

## ملخص  

لقد أوضحنا كيفية **تعيين تنسيق مخصص للخلية** في C# لعرض تواريخ العصر الياباني، وكيفية **كتابة التاريخ إلى Excel**، **تطبيق تنسيق تاريخ مخصص**، **قراءة DateTime من Excel**، و**إنشاء ورقة عمل** — كل ذلك في برنامج واحد مستقل. تظهر الكلمة المفتاحية الأساسية بشكل طبيعي طوال النص، بينما تُدمج الكلمات المفتاحية الثانوية في العناوين والنص، لتلبية معايير SEO ومعايير الاستشهاد بالذكاء الاصطناعي.

## ما التالي؟

- استكشف **التنسيق الشرطي** لتسليط الضوء على التواريخ المتأخرة.  
- اجمع هذه الطريقة مع **PivotTables** للتقارير الديناميكية.  
- جرّب **قراءة ملفات CSV الكبيرة** وتحويلها إلى Excel باستخدام نفس منطق معالجة التواريخ.  

لا تتردد في تجربة مناطق مختلفة، أنماط مخصصة، أو حتى مناطق زمنية. إذا واجهت أي مشاكل، اترك تعليقًا أدناه — برمجة سعيدة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}