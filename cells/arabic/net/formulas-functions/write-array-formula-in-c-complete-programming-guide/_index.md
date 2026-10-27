---
category: general
date: 2026-07-03
description: اكتب صيغة مصفوفة في C# لإنشاء مصفوفة من عمودين، احسب خلية Excel ولف القائمة
  إلى أعمدة. اتبع هذا المثال خطوة بخطوة باستخدام Aspose.Cells.
draft: false
keywords:
- write array formula
- calculate excel cell
- wrap list into columns
- create 2‑column array
- generate excel array
language: ar
og_description: اكتب صيغة مصفوفة في C# لإنشاء مصفوفة من عمودين، احسب خلية إكسل ولف
  القائمة إلى أعمدة. تعلّم العملية بالكامل مع كود قابل للتنفيذ.
og_title: كتابة صيغة المصفوفة في C# – دليل خطوة بخطوة
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: Write array formula in C# to create a 2‑column array, calculate Excel
    cell and wrap list into columns. Follow this step‑by‑step example using Aspose.Cells.
  headline: Write array formula in C# – Complete Programming Guide
  type: TechArticle
- description: Write array formula in C# to create a 2‑column array, calculate Excel
    cell and wrap list into columns. Follow this step‑by‑step example using Aspose.Cells.
  name: Write array formula in C# – Complete Programming Guide
  steps:
  - name: What if I need a dynamic range rather than a hard‑coded list?
    text: 'You can construct the list part of the formula at runtime:'
  - name: Does `WRAPCOLS` work on older Excel versions?
    text: '`WRAPCOLS` is available starting with Excel 365/2019. If you target older
      versions, you’ll need to simulate the behavior with `INDEX` and `MOD` tricks,
      but that quickly becomes messy. Using Aspose.Cells lets you keep the modern
      formula and still produce a compatible file for most users.'
  - name: Can I write the formula to a range instead of a single cell?
    text: 'Yes—assign the same formula to the top‑left cell of the range, then call
      `Calculate()` on the range object:'
  type: HowTo
tags:
- C#
- Excel
- Aspose.Cells
- automation
title: كتابة صيغة المصفوفة في C# – دليل برمجة شامل
url: /ar/net/formulas-functions/write-array-formula-in-c-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كتابة صيغة مصفوفة في C# – دليل برمجة كامل

هل احتجت إلى **كتابة صيغة مصفوفة** في C# لكن لم تكن متأكدًا من كيفية جعل Excel ينتج قائمة مُنسقة بشكل جميل؟ لست وحدك. يواجه العديد من المطورين صعوبة عندما يحاولون *إنشاء نتائج مصفوفة Excel* دون فتح الواجهة. في هذا الدرس سنستعرض مثالًا مختصرًا وشاملًا ي **يكتب صيغة مصفوفة**، **يحسب خلية Excel**، و **يُعيد ترتيب القائمة إلى أعمدة** لإنشاء **مصفوفة ذات عمودين** يمكنك حفظها وفحصها.

سنستخدم مكتبة Aspose.Cells الشهيرة لأنها تتيح لك التعامل مع المصنفات بالكامل عبر الشيفرة. بنهاية الدرس ستحصل على مقطع جاهز للتنفيذ، شرح واضح لكل سطر، وأفكار لتوسيع النمط إلى مجموعات بيانات أكبر. لا حشو—فقط الأجزاء العملية التي يمكنك نسخها ولصقها اليوم.

## ما ستحتاجه

قبل أن نبدأ، تأكد من وجود التالي:

* .NET 6.0 أو أحدث (الكود يعمل على .NET Core أيضًا)  
* إشارة إلى **Aspose.Cells** (يمكنك الحصول عليها من NuGet: `Install-Package Aspose.Cells`)  
* مجلد يمكنك القراءة/الكتابة فيه لملفات Excel – سنسميه `YOUR_DIRECTORY` في الأمثلة  

هذا كل شيء. لا تحتاج إلى أي تفاعل إضافي مع Excel، ولا COM، فقط كود مُدار نقي.

![مثال كتابة صيغة مصفوفة في C#](write-array-formula.png "لقطة شاشة تُظهر المصفوفة ذات العمودين المُولدة في Excel – كتابة صيغة مصفوفة في C#")

## الخطوة 1: كتابة صيغة مصفوفة باستخدام Aspose.Cells

أول شيء يجب القيام به هو **كتابة صيغة مصفوفة** داخل خلية. في صياغة Excel، دالة `WRAPCOLS` تأخذ قائمة مسطحة وتعيد تشكيلها إلى مصفوفة. إليك كيفية القيام بذلك برمجيًا:

```csharp
// Step 1: Load the workbook (or create a new one)
var workbook = new Aspose.Cells.Workbook(); // creates a blank workbook

// Access the first worksheet – this is where we’ll work
var worksheet = workbook.Worksheets[0];

// Write array formula into A1 that wraps {1,2,3,4} into 2 columns
worksheet.Cells["A1"].Formula = "=WRAPCOLS({1,2,3,4},2)";
```

**لماذا هذا مهم:** خاصية `Formula` تخزن سلسلة صيغة Excel الحرفية. باستخدام `WRAPCOLS` نخبر Excel بأخذ المصفوفة الخطية `{1,2,3,4}` وترتيبها في تخطيط بعمودين، مما ينتج **إنشاء مصفوفة ذات عمودين**. الصيغة نفسها هي *صيغة مصفوفة*—ستلاحظ الأقواس المعقوفة حول الأرقام.

## الخطوة 2: حساب خلية Excel حتى يتم تقييم الصيغة

كتابة الصيغة ليست كافية؛ نحتاج إلى **حساب خلية Excel** حتى يقوم المحرك بتقييمها. Aspose.Cells لن يقوم بإعادة الحساب تلقائيًا إلا إذا طلبت ذلك:

```csharp
// Step 2: Force calculation of the cell containing the array formula
worksheet.Cells["A1"].Calculate();
```

**لماذا هذه الخطوة حاسمة:** بدون استدعاء `Calculate()`، تبقى الخلية في حالة “معلقة” وسيحتوي المصنف الذي تحفظه على الصيغة الخام، وليس القيم المحسوبة. من خلال إعادة الحساب صراحةً، نضمن أن مصفوفة الإخراج تُصبح مادة في الملف.

## الخطوة 3: إعادة ترتيب القائمة إلى أعمدة – شاهد النتيجة

في هذه المرحلة يحتوي ورقة العمل الآن على كتلة بعمودين تبدأ من `A1`. إذا فتحت الملف سترى:

| A | B |
|---|---|
| 1 | 2 |
| 3 | 4 |

هذا هو التمثيل البصري لـ **إعادة ترتيب القائمة إلى أعمدة** باستخدام دالة `WRAPCOLS`. إذا رغبت في عدد أعمدة مختلف، فقط غيّر الوسيط الثاني:

```csharp
worksheet.Cells["A1"].Formula = "=WRAPCOLS({1,2,3,4,5,6},3)"; // creates 3 columns
worksheet.Cells["A1"].Calculate();
```

الآن تبدو المصفوفة هكذا:

| A | B | C |
|---|---|---|
| 1 | 2 | 3 |
| 4 | 5 | 6 |

**نصيحة احترافية:** عند التعامل مع مجموعات بيانات أكبر، قم ببناء سلسلة القائمة ديناميكيًا (مثلاً باستخدام `string.Join(",", myNumbers)`) لتجنب كتابة القيم يدويًا.

## الخطوة 4: حفظ المصنف والتحقق من النتيجة

أخيرًا، نقوم بحفظ المصنف على القرص حتى تتمكن من فتحه في Excel وتأكيد عمل **إنشاء مصفوفة Excel**:

```csharp
// Step 4: Save the workbook – you’ll see the calculated array in Excel
workbook.Save("YOUR_DIRECTORY/output.xlsx");
```

افتح `output.xlsx` وسترى مصفوفة العمودين بالضبط كما هو موضح. إذا غيرت الصيغة وأعدت الحساب، سيتحدث الملف المحفوظ تلقائيًا—بدون الحاجة لتحديث يدوي.

## مثال كامل قابل للتنفيذ

بجمع كل ما سبق، إليك البرنامج الكامل الذي يمكنك وضعه في تطبيق Console:

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // 1️⃣ Load (or create) a workbook
        var workbook = new Workbook(); // blank workbook

        // 2️⃣ Access the first worksheet
        var worksheet = workbook.Worksheets[0];

        // 3️⃣ Write the array formula that wraps a list into 2 columns
        worksheet.Cells["A1"].Formula = "=WRAPCOLS({1,2,3,4},2)";

        // 4️⃣ Calculate the cell so the formula is evaluated
        worksheet.Cells["A1"].Calculate();

        // 5️⃣ (Optional) Save the workbook to view the result
        workbook.Save("YOUR_DIRECTORY/output.xlsx");

        Console.WriteLine("Workbook saved – check output.xlsx to see the 2‑column array.");
    }
}
```

**الناتج المتوقع:** عند فتح `output.xlsx`، تحتوي الخلايا `A1:B2` على الأرقام 1‑4 مرتبة في عمودين. يطبع الـ Console رسالة تأكيد ودية.

## الحالات الحدية والأسئلة الشائعة

### ماذا لو احتجت إلى نطاق ديناميكي بدلًا من قائمة ثابتة؟

يمكنك إنشاء جزء القائمة من الصيغة في وقت التشغيل:

```csharp
int[] values = { 10, 20, 30, 40, 50, 60 };
string list = "{" + string.Join(",", values) + "}";
worksheet.Cells["A1"].Formula = $"=WRAPCOLS({list},3)";
worksheet.Cells["A1"].Calculate();
```

ما زال هذا **ينتج مصفوفة Excel**، لكن الآن تأتي البيانات المصدرية من منطق تطبيقك.

### هل تعمل `WRAPCOLS` على إصدارات Excel القديمة؟

دالة `WRAPCOLS` متوفرة بدءًا من Excel 365/2019. إذا كنت تستهدف إصدارات أقدم، ستحتاج إلى محاكاة السلوك باستخدام `INDEX` و`MOD`، لكن ذلك يصبح معقدًا بسرعة. استخدام Aspose.Cells يتيح لك الاحتفاظ بالصيغ الحديثة وإنتاج ملف متوافق مع معظم المستخدمين.

### هل يمكنني كتابة الصيغة إلى نطاق بدلاً من خلية واحدة؟

نعم—عيّن الصيغة نفسها إلى الخلية العليا‑اليسرى للنطاق، ثم استدعِ `Calculate()` على كائن النطاق:

```csharp
var range = worksheet.Cells.CreateRange("A1", 2, 2); // 2x2 block
range.Formula = "=WRAPCOLS({1,2,3,4},2)";
range.Calculate();
```

النتيجة هي نفسها، لكن لديك تحكم أكبر في موقع المصفوفة.

## اعتبارات الأداء

عند **حساب خلية Excel** للعديد من الصيغ، يمكن لـ Aspose.Cells تجميع الحسابات لزيادة السرعة. إذا كنت تُنشئ آلاف المصفوفات، استدعِ `workbook.CalculateFormula()` مرة واحدة بعد ضبط جميع الصيغ، بدلاً من `Calculate()` على كل خلية. هذا يقلل من الحمل بشكل كبير.

## الخطوات التالية

الآن بعد أن عرفت كيفية **كتابة صيغة مصفوفة**، **حساب خلية Excel**، و**إعادة ترتيب القائمة إلى أعمدة** لإنشاء **مصفوفة ذات عمودين**، يمكنك استكشاف:

* **إنشاء مصفوفة Excel** لتقارير متعددة الأوراق  
* تطبيق التنسيق (الحدود، تنسيقات الأرقام) على النطاق الناتج  
* تصدير المصنف إلى PDF أو CSV للمعالجة اللاحقة  
* دمج قواعد التحقق من البيانات لإنشاء جداول بيانات تفاعلية  

كل من هذه يبني على التقنية الأساسية التي غطيناها، مما يتيح لك أتمتة تدفقات عمل Excel المعقدة بالكامل من C#.

---

**باختصار**، يوضح لك هذا الدليل كيفية **كتابة صيغة مصفوفة** في C# باستخدام Aspose.Cells، وإجبار خطوة **حساب خلية Excel**، و**إعادة ترتيب القائمة إلى أعمدة** لإنشاء **مصفوفة ذات عمودين** يمكنك **إنشاء ملفات مصفوفة Excel** بها. الشيفرة قابلة للتنفيذ بالكامل، والشروحات تغطي *السبب* وراء كل سطر، ولديك نصائح للتوسع ومعالجة الحالات الحدية.

جرّبها، غير عدد الأعمدة، أدخل بياناتك الخاصة، وشاهد Excel يقوم بالعمل الشاق نيابةً عنك. برمجة سعيدة!

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة شفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [Master Excel Array Formulas with Aspose.Cells Java: Streamline Calculations and Formatting](/cells/english/java/formulas-functions/aspose-cells-java-array-formulas-custom-calculations/)
- [Create Excel List Objects Using Aspose.Cells .NET: A Step-by-Step Guide](/cells/english/net/tables-structured-references/create-excel-list-objects-aspose-cells-net/)
- [Import Multi Dimensional Array Excel Aspose Cells Java](/cells/german/java/import-export/import-multi-dimensional-array-excel-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}