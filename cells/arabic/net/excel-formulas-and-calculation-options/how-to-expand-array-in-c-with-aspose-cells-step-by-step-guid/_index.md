---
category: general
date: 2026-04-07
description: تعلم كيفية توسيع المصفوفة في C# باستخدام Aspose.Cells. يوضح هذا الدرس
  كيفية إنشاء دفتر عمل C#، كتابة صيغة Excel في C#، وتعيين صيغة الخلية في C# بسهولة.
draft: false
keywords:
- how to expand array
- create workbook c#
- use aspose cells
- write excel formula c#
- set cell formula c#
language: ar
og_description: اكتشف كيفية توسيع المصفوفة في C# باستخدام Aspose.Cells. اتبع خطواتنا
  الواضحة لإنشاء دفتر عمل C#، وكتابة صيغة Excel في C#، وتعيين صيغة الخلية في C#.
og_title: كيفية توسيع المصفوفة في C# باستخدام Aspose.Cells – دليل كامل
tags:
- Aspose.Cells
- C#
- Excel Automation
title: كيفية توسيع المصفوفة في C# باستخدام Aspose.Cells – دليل خطوة بخطوة
url: /ar/net/excel-formulas-and-calculation-options/how-to-expand-array-in-c-with-aspose-cells-step-by-step-guid/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية توسيع المصفوفة في C# باستخدام Aspose.Cells – دليل خطوة بخطوة

هل تساءلت يومًا **كيف يتم توسيع المصفوفة** داخل ورقة Excel من C# دون الحاجة إلى حلقات معقدة؟ لست وحدك. يواجه العديد من المطورين صعوبة عندما يحتاجون إلى تحويل مصفوفة ثابتة صغيرة إلى عمود أو صف أكبر لحسابات لاحقة. الخبر السار؟ Aspose.Cells يجعل الأمر سهلًا، ويمكنك القيام بذلك باستخدام صيغة Excel واحدة.

في هذا الدرس سنستعرض العملية بالكامل: إنشاء مصنف C#، استخدام Aspose.Cells، كتابة صيغة Excel C#، وأخيرًا ضبط صيغة الخلية C# بحيث يتم توسيع المصفوفة بالضبط كما تتوقع. في النهاية ستحصل على مقطع شفرة قابل للتنفيذ يطبع القيم الموسعة في وحدة التحكم، وستفهم لماذا هذه الطريقة نظيفة وعالية الأداء.

## المتطلبات المسبقة

- .NET 6.0 أو أحدث (الكود يعمل على .NET Core و .NET Framework على حد سواء)  
- Aspose.Cells for .NET ≥ 23.12 (أحدث نسخة وقت كتابة المقال)  
- معرفة أساسية بصياغة C#—لا تحتاج إلى خبرة عميقة في أتمتة Excel  

إذا كان لديك كل ذلك، رائع—لنبدأ.

## الخطوة 1: إنشاء مصنف C# باستخدام Aspose.Cells

أولاً، نحتاج إلى كائن مصنف جديد. فكر فيه كملف Excel فارغ يعيش في الذاكرة حتى تقرر حفظه.

```csharp
using Aspose.Cells;
using System;

namespace ExpandArrayDemo
{
    class Program
    {
        static void Main()
        {
            // Initialize a new workbook – this is the canvas for our work.
            Workbook workbook = new Workbook();

            // Grab the first worksheet (index 0). Most demos start here.
            Worksheet ws = workbook.Worksheets[0];
```

> **نصيحة احترافية:** إذا كنت تخطط للعمل مع عدة أوراق، يمكنك إضافتها عبر `workbook.Worksheets.Add()` والإشارة إليها بالاسم أو الفهرس.

## الخطوة 2: كتابة صيغة Excel C# لتوسيع المصفوفة

الآن يأتي جوهر الموضوع—كيف يتم توسيع المصفوفة. دالة `EXPAND` (المتوفرة في إصدارات Excel الحديثة) تأخذ مصفوفة مصدر وتمدها إلى حجم محدد. في C# نُعيّن تلك الصيغة إلى خلية.

```csharp
            // Set a formula that expands a 3‑element array into a 5‑row column.
            // The syntax mirrors what you'd type in Excel: =EXPAND({1,2,3},5,1)
            ws.Cells["A1"].Formula = "=EXPAND({1,2,3},5,1)";
```

لماذا نستخدم `EXPAND`؟ لأنها تتجنب الحلقات اليدوية، تحافظ على خفة وزن المصنف، وتسمح لـ Excel بإعادة الحساب تلقائيًا إذا غيرت مصفوفة المصدر لاحقًا. هذه هي الطريقة الأنظف للإجابة على سؤال **كيف يتم توسيع المصفوفة** دون كتابة كود C# إضافي.

## الخطوة 3: حساب المصنف لتفعيل تنفيذ الصيغة

Aspose.Cells لا يقوم بتقييم الصيغ تلقائيًا حتى تطلب ذلك. استدعاء `Calculate` يجبر المحرك على تشغيل دالة `EXPAND` وتعبئة النطاق المستهدف.

```csharp
            // Force calculation so the formula result becomes available.
            workbook.Calculate();
```

إذا تخطيت هذه الخطوة، فإن قراءة قيم الخلايا ستعيد نص الصيغة بدلاً من الأرقام المحسوبة.

## الخطوة 4: قراءة القيم الموسعة – ضبط صيغة الخلية C# واسترجاع النتائج

بعد حساب الورقة، يمكننا الآن قراءة الخلايا الخمس التي ملأتها `EXPAND`. هذا يُظهر **set cell formula c#** عمليًا ويظهر أيضًا كيفية سحب البيانات مرة أخرى إلى تطبيقك.

```csharp
            // Loop through the first 5 rows of column A and print each value.
            for (int row = 0; row < 5; row++)
            {
                // Cells[row, 0] corresponds to column A (zero‑based index).
                Console.WriteLine(ws.Cells[row, 0].Value);
            }

            // Optional: keep the console window open when debugging.
            Console.WriteLine("Press any key to exit...");
            Console.ReadKey();
        }
    }
}
```

### النتيجة المتوقعة

تشغيل البرنامج يطبع ما يلي في وحدة التحكم:

```
1
2
3
0
0
```

الأرقام الثلاثة الأولى تأتي من المصفوفة الأصلية `{1,2,3}`. الصفان الأخيران مملوءان بالأصفار لأن `EXPAND` يملأ الحجم المستهدف بالقيمة الافتراضية (صفر للمصفوفات الرقمية). إذا رغبت في قيمة تعبئة مختلفة، يمكنك تغليف استدعاء `EXPAND` داخل `IFERROR` أو دمجه مع `CHOOSE`.

## الخطوة 5: حفظ المصنف (اختياري)

إذا أردت فحص ملف Excel المُنشأ، فقط أضف استدعاء `Save` قبل انتهاء البرنامج:

```csharp
            // Save the workbook to disk for verification.
            workbook.Save("ExpandedArray.xlsx");
```

فتح `ExpandedArray.xlsx` سيظهر نفس العمود المكوّن من خمس صفوف في الخلايا A1:A5، مؤكدًا أن الصيغة تم تقييمها بشكل صحيح.

## أسئلة شائعة وحالات خاصة

### ماذا لو احتجت إلى توسيع أفقي بدلاً من عمودي؟

غيّر الوسيط الثالث في `EXPAND` من `1` (صفوف) إلى `0` (أعمدة) واضبط الحلقة وفقًا لذلك:

```csharp
ws.Cells["A1"].Formula = "=EXPAND({1,2,3},1,5)"; // expands to a 1‑row, 5‑column range
```

### هل يمكن توسيع نطاق ديناميكي بدلاً من مصفوفة ثابتة؟

بالطبع. استبدل الثابت `{1,2,3}` بإشارة إلى نطاق خلايا آخر، مثل `A10:C10`. تصبح الصيغة:

```csharp
ws.Cells["A1"].Formula = "=EXPAND(A10:C10,5,1)";
```

تأكد فقط من وجود نطاق المصدر قبل تشغيل الحساب.

### كيف تقارن هذه الطريقة مع الحلقة في C#؟

الحلقة تتطلب كتابة كل قيمة يدويًا:

```csharp
for (int i = 0; i < 5; i++) ws.Cells[i, 0].PutValue(i < 3 ? i + 1 : 0);
```

بينما ذلك يعمل، فإن استخدام `EXPAND` يبقي المنطق داخل Excel، وهو مفيد عندما يتم تعديل المصنف لاحقًا من قبل غير المطورين أو عندما تريد أن يتولى محرك إعادة الحساب الأصلي في Excel التعامل مع التغييرات تلقائيًا.

## ملخص المثال الكامل القابل للتنفيذ

فيما يلي البرنامج الكامل الجاهز للنسخ واللصق الذي يوضح **كيف يتم توسيع المصفوفة** باستخدام Aspose.Cells. لا توجد تبعيات مخفية، فقط بيانات `using` التي تحتاجها.

```csharp
using Aspose.Cells;
using System;

namespace ExpandArrayDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create a new workbook.
            Workbook workbook = new Workbook();

            // 2️⃣ Access the first worksheet.
            Worksheet ws = workbook.Worksheets[0];

            // 3️⃣ Write the EXPAND formula – this is the core of how to expand array.
            ws.Cells["A1"].Formula = "=EXPAND({1,2,3},5,1)";

            // 4️⃣ Calculate so the formula resolves.
            workbook.Calculate();

            // 5️⃣ Read and display the expanded values.
            for (int row = 0; row < 5; row++)
            {
                Console.WriteLine(ws.Cells[row, 0].Value);
            }

            // Optional: Save the workbook for visual verification.
            workbook.Save("ExpandedArray.xlsx");

            Console.WriteLine("Done – press any key to close.");
            Console.ReadKey();
        }
    }
}
```

شغّله في Visual Studio أو Rider أو عبر سطر الأوامر `dotnet run` وسترى المصفوفة مُوسعة كما هو موضح.

## الخلاصة

غطّينا **كيفية توسيع المصفوفة** داخل ورقة Excel باستخدام C# وAspose.Cells، من إنشاء المصنف C# إلى كتابة صيغة Excel C# وأخيرًا ضبط صيغة الخلية C# لاسترجاع النتائج. تعتمد التقنية على الدالة الأصلية `EXPAND`، مما يبقي الكود منظمًا وجداولك الديناميكية.

ما الخطوة التالية؟ جرّب استبدال مصفوفة المصدر بنطاق مسمى، واختبر قيم تعبئة مختلفة، أو ربط عدة استدعاءات `EXPAND` لبناء جداول بيانات أكبر. يمكنك أيضًا استكشاف دوال قوية أخرى مثل `SEQUENCE` أو `LET` لمزيد من الأتمتة المدفوعة بالصيغ.

هل لديك أسئلة حول استخدام Aspose.Cells في سيناريوهات أكثر تعقيدًا؟ اترك تعليقًا أدناه أو اطلع على الوثائق الرسمية لـ Aspose.Cells لمزيد من التفاصيل حول معالجة الصيغ، تحسين الأداء، ودعم الأنظمة المتعددة.

برمجة سعيدة، واستمتع بتحويل المصفوفات الصغيرة إلى أعمدة قوية!

![مخطط يوضح برنامج C# ينشئ مصنفًا، يطبق صيغة EXPAND، ويطبع النتائج – يوضح كيفية توسيع المصفوفة باستخدام Aspose.Cells](https://example.com/expand-array-diagram.png "مخطط يوضح كيفية توسيع المصفوفة باستخدام Aspose.Cells في C#")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}