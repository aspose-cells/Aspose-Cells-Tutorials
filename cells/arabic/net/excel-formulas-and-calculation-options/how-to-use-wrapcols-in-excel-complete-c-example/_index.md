---
category: general
date: 2026-06-24
description: كيفية استخدام WRAPCOLS مع مثال واضح لصيغة مصفوفة إكسل. تعلم كيفية إجبار
  حساب الورقة وتوليد الصفوف من المصفوفة في دقائق.
draft: false
keywords:
- how to use wrapcols
- excel array formula example
- force worksheet calculation
- generate rows from array
language: ar
og_description: كيفية استخدام WRAPCOLS في Excel مع مثال خطوة‑بخطوة لصيغة مصفوفة Excel.
  اكتشف كيفية إجبار حساب الورقة وتوليد الصفوف من المصفوفة بكفاءة.
og_title: كيفية استخدام WRAPCOLS في Excel – مثال كامل بلغة C#
schemas:
- author: Aspose
  dateModified: '2026-06-24'
  description: How to use WRAPCOLS with a clear excel array formula example. Learn
    to force worksheet calculation and generate rows from array in minutes.
  headline: How to Use WRAPCOLS in Excel – Complete C# Example
  type: TechArticle
- description: How to use WRAPCOLS with a clear excel array formula example. Learn
    to force worksheet calculation and generate rows from array in minutes.
  name: How to Use WRAPCOLS in Excel – Complete C# Example
  steps:
  - name: Set Up the Workbook and Worksheet
    text: First things first—we need a `Workbook` instance and a reference to its
      first worksheet. Think of the workbook as the notebook and the worksheet as
      the first page you’ll write on.
  - name: Write the WRAPCOLS Array Formula
    text: Now we actually answer **how to use WRAPCOLS**. The formula `=WRAPCOLS({1,2,3,4,5,6},3)`
      tells Excel to take the six numbers and wrap them into three columns. Excel
      automatically decides how many rows are needed—in this case two rows.
  - name: Force Worksheet Calculation
    text: Aspose.Cells respects Excel’s calculation settings, meaning the formula
      won’t evaluate until the engine runs. To see the results immediately we need
      to **force worksheet calculation**.
  - name: Verify the Result and Save the Workbook
    text: Finally, let’s confirm that the values are where we expect them, then write
      the file to disk. This also serves as a quick sanity check for anyone reading
      the code.
  type: HowTo
tags:
- Excel
- C#
- Aspose.Cells
- ArrayFormula
title: كيفية استخدام WRAPCOLS في إكسل – مثال كامل بلغة C#
url: /ar/net/excel-formulas-and-calculation-options/how-to-use-wrapcols-in-excel-complete-c-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية استخدام WRAPCOLS في Excel – مثال كامل بلغة C#

هل تساءلت يومًا **كيفية استخدام WRAPCOLS** لنشر مصفوفة أحادية البُعد عبر شبكة من الخلايا؟ لست وحدك. يواجه العديد من المطورين صعوبة عندما يحتاجون إلى **إنشاء صفوف من مصفوفة** دون كتابة حلقة لكل خلية.  

في هذا الدرس سنستعرض مثالًا عمليًا **لصيغة مصفوفة Excel** يكتب `{1,2,3,4,5,6}` في ثلاثة أعمدة، مع إنشاء الصفوف اللازمة تلقائيًا. سنوضح أيضًا الطريقة الصحيحة **لإجبار حساب الورقة** حتى تظهر القيم فورًا. في النهاية ستحصل على مقتطف C# جاهز للتنفيذ يمكنك إدراجه في أي مشروع Aspose.Cells.

## ما ستحصل عليه بعد القراءة

- برنامج C# كامل، قابل للترجمة، ينشئ مصنفًا، يطبق صيغة المصفوفة `WRAPCOLS`، ويجبر الحساب.  
- فهم لماذا تُفضَّل `WRAPCOLS` على الحلقات اليدوية عندما تحتاج إلى تعبئة سريعة على نمط المصفوفة.  
- نصائح لتجاوز المشكلات الشائعة (مثل صياغة الصيغة، وضع الحساب).  

**المتطلبات المسبقة:** .NET 6+ (أو .NET Framework 4.6+)، مكتبة Aspose.Cells for .NET، وفهم أساسي للغة C#. لا توجد تبعيات أخرى.

![كيفية استخدام WRAPCOLS في Excel](/images/wrapcols-output.png){: .center alt="نتيجة استخدام WRAPCOLS في Excel"}

## كيفية استخدام WRAPCOLS – تنفيذ خطوة بخطوة

نقسم العملية إلى أربع خطوات منطقية. كل خطوة مقدمة بعنوان H2 لتتمكن من القفز مباشرة إلى الجزء الذي تحتاجه.

### الخطوة 1: إعداد المصنف والورقة

أولًا—نحتاج إلى كائن `Workbook` وإشارة إلى الورقة الأولى. فكر في المصنف كدفتر ملاحظات والورقة كصفحة أولى ستكتب عليها.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Create a new workbook (in‑memory, no file on disk yet)
        Workbook workbook = new Workbook();

        // Grab the first worksheet – this is where we’ll place the formula
        Worksheet worksheet = workbook.Worksheets[0];
```

> **لماذا هذا مهم:** إنشاء كائن المصنف يمنحنا مساحة عمل نظيفة. استخدام `Worksheets[0]` آمن لأن المصنف الجديد يحتوي دائمًا على ورقة واحدة على الأقل.

### الخطوة 2: كتابة صيغة المصفوفة WRAPCOLS

الآن نجيب على **كيفية استخدام WRAPCOLS**. الصيغة `=WRAPCOLS({1,2,3,4,5,6},3)` تخبر Excel بأخذ الأرقام الستة وتوزيعها على ثلاثة أعمدة. يحدد Excel عدد الصفوف المطلوب تلقائيًا—في هذه الحالة صفّين.

```csharp
        // Apply the WRAPCOLS array formula to cell A1
        // This will fill A1:C2 with the numbers 1‑6
        worksheet.Cells["A1"].Formula = "=WRAPCOLS({1,2,3,4,5,6},3)";
```

> **لماذا هذا مهم:** استخدام **مثال لصيغة مصفوفة Excel** مثل `WRAPCOLS` يلغي الحاجة إلى الحلقات اليدوية. إنها طريقة أحادية السطر، إعلانية، لإعادة تشكيل البيانات، مما يجعل الكتابة أسرع وأسهل في الصيانة.

### الخطوة 3: إجبار حساب الورقة

Aspose.Cells يلتزم بإعدادات حساب Excel، مما يعني أن الصيغة لن تُحسب حتى يُشغل المحرك. لرؤية النتائج فورًا نحتاج إلى **إجبار حساب الورقة**.

```csharp
        // Force calculation so the array formula resolves instantly
        worksheet.CalculateFormula();
```

> **لماذا هذا مهم:** إذا تخطيت هذه الخطوة، ستظل الخلايا تحتوي على نص الصيغة بدلاً من الأرقام المحسوبة. استدعاء `CalculateFormula()` يضمن أن المصنف يعكس أحدث البيانات عند حفظه أو فحصه.

### الخطوة 4: التحقق من النتيجة وحفظ المصنف

أخيرًا، دعنا نتأكد من أن القيم في الموضع المتوقع، ثم نكتب الملف إلى القرص. هذا أيضًا يُعد فحصًا سريعًا لأي شخص يقرأ الكود.

```csharp
        // Optional: Print the populated cells to the console for verification
        Console.WriteLine("A1 = " + worksheet.Cells["A1"].StringValue);
        Console.WriteLine("B1 = " + worksheet.Cells["B1"].StringValue);
        Console.WriteLine("C1 = " + worksheet.Cells["C1"].StringValue);
        Console.WriteLine("A2 = " + worksheet.Cells["A2"].StringValue);
        Console.WriteLine("B2 = " + worksheet.Cells["B2"].StringValue);
        Console.WriteLine("C2 = " + worksheet.Cells["C2"].StringValue);

        // Save the workbook so you can open it in Excel
        workbook.Save("WrapColsDemo.xlsx");
    }
}
```

**الناتج المتوقع في وحدة التحكم**

```
A1 = 1
B1 = 2
C1 = 3
A2 = 4
B2 = 5
C2 = 6
```

عند فتح `WrapColsDemo.xlsx`، سترى الأرقام الستة مرتبة بدقة في كتلة 2 × 3—تمامًا ما وعدت به عملية **إنشاء صفوف من مصفوفة**.

## أسئلة شائعة وحالات خاصة

| السؤال | الجواب |
|----------|--------|
| *ماذا لو احتجت إلى أكثر من ثلاثة أعمدة؟* | غيّر الوسيط الثاني في `WRAPCOLS`. لأربعة أعمدة، استخدم `=WRAPCOLS({1,2,3,4,5,6},4)`. سيُنشئ Excel عدد الصفوف المطلوب (في هذه الحالة صفّين، مع خليةين أخريين فارغتين). |
| *هل يمكن الإشارة إلى نطاق مسمى بدلًا من مصفوفة حرفية؟* | بالتأكيد. استخدم `=WRAPCOLS(MyRange,3)` حيث `MyRange` معرف مسبقًا في الورقة. |
| *هل يجب حفظ المصنف قبل استدعاء `CalculateFormula()`؟* | لا. الحساب يتم بالكامل في الذاكرة، وهذا هو السبب في أننا نستطيع التحقق من القيم قبل حفظ الملف. |
| *ماذا لو كان المصنف مضبوطًا على وضع الحساب اليدوي؟* | `worksheet.CalculateFormula()` يتجاوز الوضع لهذا الورقة فقط، مما يضمن حساب الصيغة بغض النظر عن الإعداد العام. |

> **نصيحة احترافية:** إذا كنت تُنشئ مصفوفات كبيرة، ضع استدعاء `WRAPCOLS` داخل حلقة تُعدِّل عدد الأعمدة ديناميكيًا. هذا يبقي الكود مختصرًا مع الاستفادة من قوة صيغة المصفوفة.

## توسيع المثال – الخطوات التالية

- **الدمج مع وظائف أخرى:** ضع `WRAPCOLS` داخل `SORT` أو `FILTER` لمعالجة البيانات قبل توزيعها.  
- **المصفوفات الديناميكية:** أنشئ سلسلة المصفوفة برمجيًا (`"{"+string.Join(",", numbers)+"}"`) للتعامل مع مجموعات بيانات يُدخلها المستخدم.  
- **التنسيق:** بعد الحساب، أضف حدودًا أو تنسيقات رقمية للنطاق المملوء للحصول على تقرير مصقول.  

جميع هذه الأفكار تدور حول المبدأ الأساسي **كيفية استخدام WRAPCOLS**—اجعل الصيغة إعلانية، ودع Excel يتولى العمل الشاق، وتدخل برمجيًا فقط عندما تحتاج إلى **إجبار حساب الورقة** أو تعديل التخطيط.

## الخلاصة

غطينا **كيفية استخدام WRAPCOLS** من البداية حتى النهاية: إنشاء مصنف، وضع **مثال لصيغة مصفوفة Excel** `WRAPCOLS` في خلية، **إجبار حساب الورقة**، والتحقق من أن القيم **تنشئ صفوفًا من مصفوفة** كما هو متوقع. المقتطف الكامل القابل للتنفيذ أعلاه يعمل مباشرة مع Aspose.Cells for .NET، مما يمنحك أساسًا قويًا لأتمتة جداول البيانات المتقدمة.

هل أنت مستعد للتجربة؟ جرّب تغيير محتويات المصفوفة، تعديل عدد الأعمدة، أو ربط وظائف Excel إضافية. الاحتمالات لا حدود لها، والآن لديك نمط موثوق للبناء عليه.

برمجة سعيدة، ولتُحسب أوراقك دائمًا في الوقت الذي تحتاجه!

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تُكمل التقنيات الموضحة في هذا الدليل. كل مصدر يتضمن أمثلة شاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [إتقان Aspose.Cells Java: كيفية إيقاف حساب الصيغ في مصنفات Excel](/cells/english/java/calculation-engine/master-aspose-cells-java-interrupt-formula-calculation-workbook/)
- [كيفية تصدير الصفوف المرئية في Excel باستخدام Aspose.Cells for .NET: دليل خطوة بخطوة](/cells/english/net/workbook-operations/export-visible-rows-aspose-cells-dotnet/)
- [كيفية إنشاء واستخدام نطاقات الاتحاد في Excel مع Aspose.Cells .NET (دليل C#)](/cells/english/net/range-management/excel-union-range-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}