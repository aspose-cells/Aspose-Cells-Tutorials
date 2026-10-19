---
category: general
date: 2026-07-13
description: كيفية استخدام WRAPCOLS في C# لتحويل المصفوفة إلى أعمدة، وتطبيق صيغة المصفوفة
  في Excel، وإنشاء مصنف Excel برمجياً—كل ذلك بخطوات واضحة.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use wrapcols
- convert array to columns
- apply array formula excel
- create excel workbook programmatically
- evaluate excel formula c#
language: ar
lastmod: 2026-07-13
og_description: كيفية استخدام WRAPCOLS في C# يتيح لك تحويل مصفوفة إلى أعمدة بسرعة،
  وتطبيق صيغة مصفوفية على طريقة Excel، وتقييم النتيجة برمجيًا.
og_image_alt: Screenshot showing how to use WRAPCOLS formula in a C# generated Excel
  sheet
og_title: كيفية استخدام WRAPCOLS في C# – إنشاء دفتر عمل Excel بسرعة
schemas:
- author: Aspose
  dateModified: '2026-07-13'
  description: How to use WRAPCOLS in C# to convert array to columns, apply array
    formula Excel, and create Excel workbook programmatically—all with clear steps.
  headline: How to Use WRAPCOLS – Complete Guide for C# Excel Automation
  type: TechArticle
- description: How to use WRAPCOLS in C# to convert array to columns, apply array
    formula Excel, and create Excel workbook programmatically—all with clear steps.
  name: How to Use WRAPCOLS – Complete Guide for C# Excel Automation
  steps:
  - name: What if I need more than two columns?
    text: 'Just change the second argument of WRAPCOLS. For example, `=WRAPCOLS({1,2,3,4,5,6},3)`
      would produce three columns:'
  - name: Can I feed a dynamic range instead of a hard‑coded array?
    text: 'Absolutely. You can build the array string programmatically:'
  - name: What about error handling?
    text: 'If the formula is malformed, `Calculate()` will throw a `CellsException`.
      Wrap the calculation in a try/catch block and log the error:'
  - name: Does this work with older Excel versions?
    text: WRAPCOLS was introduced in Excel 365/2021. When you save the file as an
      older `.xls` format, the formula may be lost. Stick to `.xlsx` if you need the
      function to survive outside the C# engine.
  type: HowTo
tags:
- Excel
- C#
- Aspose.Cells
title: كيفية استخدام WRAPCOLS – دليل كامل لأتمتة Excel باستخدام C#
url: /ar/net/excel-formulas-and-calculation-options/how-to-use-wrapcols-complete-guide-for-c-excel-automation/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية استخدام WRAPCOLS – دليل كامل لأتمتة Excel باستخدام C#

هل تساءلت يومًا **كيف تستخدم WRAPCOLS** عندما تحتاج إلى تحويل قائمة مسطحة إلى جدول منظم داخل ملف Excel يتم إنشاؤه من C#؟ لست وحدك. سواء كنت تبني محرك تقارير، أو تصدر نتائج استبيان، أو مجرد تجربة مع البيانات، فإن دالة WRAPCOLS يمكنها إعادة تشكيل مصفوفة إلى عدد الأعمدة الذي تحدده على الفور.  

في هذا الدرس سنستعرض العملية بالكامل: من **إنشاء مصنف Excel برمجياً** إلى **تطبيق صيغة مصفوفة على نمط Excel**، وأخيرًا **تقييم الصيغة باستخدام C#**. في النهاية ستتمكن من **تحويل المصفوفة إلى أعمدة** بسطر واحد من الشيفرة، دون الحاجة إلى تحريك الخلايا يدويًا.

> **ما ستحصل عليه:** عينة كود قابلة للتنفيذ، شرح لكل خطوة، نصائح لتجنب الأخطاء الشائعة، واقتراحات لتوسيع الحل.

---

## المتطلبات المسبقة

قبل أن نبدأ، تأكد من وجود ما يلي:

- .NET 6.0+ (أو أي نسخة حديثة من .NET)
- بيئة تطوير C# (Visual Studio، Rider، أو VS Code)
- مكتبة **Aspose.Cells for .NET** (الإصدار التجريبي المجاني يكفي) – فهي أسهل طريقة للتعامل مع ملفات Excel دون الحاجة لتثبيت Excel.
- إلمام أساسي بصياغة C# وصيغ Excel.

إذا كنت تفضل مكتبة أخرى (مثل EPPlus أو ClosedXML)، فإن الأفكار الأساسية تبقى نفسها—فقط استبدل استدعاءات الـ API.

---

## الخطوة 1: إعداد المشروع وإضافة مكتبة Excel

أولًا، أنشئ تطبيق console جديد وأضف Aspose.Cells عبر NuGet:

```bash
dotnet new console -n WrapColsDemo
cd WrapColsDemo
dotnet add package Aspose.Cells
```

> **نصيحة احترافية:** استخدم العلامة `--version` لتثبيت نسخة مستقرة معروفة، مثل `Aspose.Cells 24.9`.

الآن افتح `Program.cs`. سنبدأ بإضافة المساحات الاسمية المطلوبة:

```csharp
using System;
using Aspose.Cells;   // Main API for workbook manipulation
```

وجود المكتبة في المشروع يضمن أننا نستطيع **إنشاء مصنف Excel برمجياً** والعمل مع الصيغ.

---

## الخطوة 2: إنشاء مصنف جديد وتحديد الخلية المستهدفة

بعد ذلك، أنشئ مصنفًا جديدًا وحدد الخلية التي ستحتوي صيغة WRAPCOLS. في مصطلحات Excel، الخلية **A1** هي الصف 0، العمود 0.

```csharp
// Step 2.1: Create a new workbook (blank Excel file)
Workbook workbook = new Workbook();

// Step 2.2: Grab the first worksheet (default)
Worksheet sheet = workbook.Worksheets[0];

// Step 2.3: Define the target cell (A1)
Cell targetCell = sheet.Cells[0, 0];
```

لماذا نفعل ذلك؟ كائن `Workbook` هو الحاوية لجميع الأوراق، الأنماط، والحسابات. بالإشارة الصريحة إلى الخلية، نبقي الشيفرة واضحة ونتجنب “الأرقام السحرية” لاحقًا.

---

## الخطوة 3: إدراج صيغة مصفوفة WRAPCOLS

الآن يأتي جوهر الدرس—**كيفية استخدام WRAPCOLS**. الدالة تأخذ مصفوفة وعدد الأعمدة، ثم تُعيد نطاقًا ثنائي الأبعاد. بصيغة Excel تبدو هكذا:

```
=WRAPCOLS({1,2,3,4}, 2)
```

هذا يخبر Excel بترتيب الأرقام 1‑4 في **عمودين**، لتنتج:

| A | B |
|---|---|
| 1 | 3 |
| 2 | 4 |

لإدراج هذه الصيغة من C#:

```csharp
// Step 3: Apply the WRAPCOLS array formula to A1
targetCell.Formula = "=WRAPCOLS({1,2,3,4},2)";
```

لاحظ أننا نستخدم **سلسلة نصية** تعكس ما تكتبه في شريط صيغ Excel. هذه هي خطوة **تطبيق صيغة مصفوفة Excel**، وتتعامل Aspose.Cells تلقائيًا معها كصيغة مصفوفة لأن WRAPCOLS تُعيد نطاقًا.

---

## الخطوة 4: إجبار الحساب حتى تُقيم الصيغة

عادةً ما يُعيد Excel الحساب بشكل كسول—فقط عند فتح الملف. بما أننا نريد قراءة النتيجة فورًا، يجب أن نُطلق عملية حساب:

```csharp
// Step 4: Calculate the workbook so the WRAPCOLS formula resolves
workbook.Calculate();
```

استدعاء `Calculate()` هو فعل **تقييم صيغة Excel بـ C#** الذي يجبر المحرك على حساب كل الصيغ، بما فيها مصفوفة WRAPCOLS. بدون هذا الاستدعاء، ستظل قيمة `targetCell.Value` `null`.

---

## الخطوة 5: استرجاع النتيجة والتحقق منها

الآن بعد أن تم حساب المصنف، يمكننا جلب القيم من الخلايا التي احتلتها المصفوفة. الخلية العليا اليسرى (A1) تحمل العنصر الأول، بينما الخلايا المجاورة تحمل البقية. لنقرأ كامل المربع 2 × 2:

```csharp
// Step 5: Read the evaluated values from the resulting range
object[,] result = targetCell.GetArrayValue() as object[,];

// Simple sanity check: print the 2x2 matrix to console
if (result != null)
{
    for (int r = 0; r < result.GetLength(0); r++)
    {
        for (int c = 0; c < result.GetLength(1); c++)
        {
            Console.Write($"{result[r, c]}\t");
        }
        Console.WriteLine();
    }
}
else
{
    Console.WriteLine("No array result was returned.");
}
```

عند تشغيل البرنامج، يجب أن يظهر في وحدة التحكم:

```
1   3
2   4
```

هذا الإخراج يؤكد أننا نجحنا في **تحويل المصفوفة إلى أعمدة** باستخدام WRAPCOLS.

---

## الخطوة 6: حفظ المصنف (اختياري لكنه مفيد)

إذا رغبت في فتح الملف في Excel ورؤية الصيغة مباشرة، فقط احفظه:

```csharp
// Step 6: Persist the workbook to disk (optional)
workbook.Save("WrapColsDemo.xlsx");
Console.WriteLine("Workbook saved as WrapColsDemo.xlsx");
```

عند فتح الملف، ستظهر صيغة WRAPCOLS في A1 والنطاق المملوء بعمودين تحته. هذه الخطوة مفيدة للتصحيح أو لتسليم الملف للمستخدمين النهائيين.

---

## أسئلة شائعة وحالات خاصة

### ماذا لو احتجت إلى أكثر من عمودين؟

فقط غير الوسيط الثاني في WRAPCOLS. على سبيل المثال، `=WRAPCOLS({1,2,3,4,5,6},3)` سيُنتج ثلاثة أعمدة:

| A | B | C |
|---|---|---|
| 1 | 3 | 5 |
| 2 | 4 | 6 |

حدّث سطر C# وفقًا لذلك:

```csharp
targetCell.Formula = "=WRAPCOLS({1,2,3,4,5,6},3)";
```

### هل يمكنني تمرير نطاق ديناميكي بدلًا من مصفوفة ثابتة؟

بالطبع. يمكنك بناء سلسلة المصفوفة برمجيًا:

```csharp
int[] numbers = Enumerable.Range(1, 10).ToArray();
string arrayLiteral = "{" + string.Join(",", numbers) + "}";
targetCell.Formula = $"=WRAPCOLS({arrayLiteral},2)";
```

بهذه الطريقة يمكنك **تطبيق صيغة مصفوفة Excel** في الوقت الفعلي، وهو مثالي للتقارير ذات أحجام بيانات متغيرة.

### ماذا عن معالجة الأخطاء؟

إذا كانت الصيغة غير صحيحة، سيُطلق `Calculate()` استثناءً من نوع `CellsException`. احط العملية بكتلة try/catch وسجّل الخطأ:

```csharp
try
{
    workbook.Calculate();
}
catch (CellsException ex)
{
    Console.Error.WriteLine($"Formula evaluation failed: {ex.Message}");
}
```

### هل يعمل هذا مع إصدارات Excel القديمة؟

تم تقديم WRAPCOLS في Excel 365/2021. عند حفظ الملف بصيغة `.xls` القديمة، قد تُفقد الصيغة. احتفظ بالصيغة `.xlsx` إذا كنت تحتاج إلى بقاء الدالة صالحة خارج محرك C#.

---

## مثال كامل يعمل

نجمع كل ما سبق في برنامج جاهز للنسخ واللصق:

```csharp
using System;
using System.Linq;
using Aspose.Cells;

namespace WrapColsDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create a new workbook
            Workbook workbook = new Workbook();
            Worksheet sheet = workbook.Worksheets[0];
            Cell targetCell = sheet.Cells[0, 0];

            // 2️⃣ Build a dynamic array (optional)
            int[] numbers = Enumerable.Range(1, 8).ToArray(); // {1,2,3,4,5,6,7,8}
            string arrayLiteral = "{" + string.Join(",", numbers) + "}";

            // 3️⃣ Apply WRAPCOLS – convert array to columns (2 columns in this case)
            targetCell.Formula = $"=WRAPCOLS({arrayLiteral},2)";

            // 4️⃣ Force calculation – evaluate excel formula c#
            try
            {
                workbook.Calculate();
            }
            catch (CellsException ex)
            {
                Console.Error.WriteLine($"Failed to evaluate formula: {ex.Message}");
                return;
            }

            // 5️⃣ Retrieve the 2‑column result
            object[,] result = targetCell.GetArrayValue() as object[,];
            if (result != null)
            {
                Console.WriteLine("WRAPCOLS result:");
                for (int r = 0; r < result.GetLength(0); r++)
                {
                    for (int c = 0; c < result.GetLength(1); c++)
                    {
                        Console.Write($"{result[r, c]}\t");
                    }
                    Console.WriteLine();
                }
            }

            // 6️⃣ Save the file for visual inspection (optional)
            workbook.Save("WrapColsDemo.xlsx");
            Console.WriteLine("\nWorkbook saved as WrapColsDemo.xlsx");
        }
    }
}
```

نفّذ `dotnet run` وسترى المصفوفة مطبوعة، متبوعةً بتأكيد وجود ملف `.xlsx`.

---

## خلاصة وخطوات مستقبلية

غطّينا **كيفية استخدام WRAPCOLS** لت **تحويل المصفوفة إلى أعمدة**، وأظهرنا تقنية **تطبيق صيغة مصفوفة Excel** من C#، وأجبرنا حسابًا لت **تقييم صيغة Excel بـ C#**، وحفظنا النتيجة للاستخدام اللاحق.  

إذا كنت ترغب في المزيد:

- **عدد أعمدة ديناميكي:** اجعل عدد الأعمدة متغيرًا يُدخله المستخدم.
- **تنسيق المخرجات:** طبّق خطوطًا، حدودًا، أو تنسيقًا شرطيًا عبر Aspose.Cells بعد الحساب.
- **دمج مع دوال أخرى:** ضع WRAPCOLS داخل `LET` أو `FILTER`

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تُبني على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة شيفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [Aspose.Cells .NET: كيفية إنشاء وتنسيق مصنفات Excel برمجياً](/cells/english/net/formatting/aspose-cells-net-create-style-excel-workbooks/)
- [كيفية إنشاء وحفظ مصنف Excel بصيغة ODS باستخدام Aspose.Cells for .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)
- [كيفية إنشاء نطاقات مسماة محلية للمصنف في Excel باستخدام Aspose.Cells .NET](/cells/english/net/range-management/excel-workbook-scoped-named-ranges-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}