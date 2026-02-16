---
category: general
date: 2026-02-15
description: كيفية استخدام WRAPCOLS لإنشاء تخطيط بعمودين، إضافة صيغة، وإنشاء مصفوفة
  تسلسل في أوراق عمل C# – دليل خطوة بخطوة.
draft: false
keywords:
- how to use wrapcols
- create two column layout
- how to add formula
- how to create columns
- generate sequence array
language: ar
og_description: كيفية استخدام WRAPCOLS لإنشاء تخطيط بعمودين، إضافة صيغ وتوليد مصفوفة
  تسلسلية في ورقة عمل C# – دليل كامل.
og_title: 'كيفية استخدام WRAPCOLS: تخطيط بعمودين في C#'
tags:
- CSharp
- ExcelAutomation
- WorksheetFormula
title: 'كيفية استخدام WRAPCOLS: إنشاء تخطيط بعمودين في C#'
url: /ar/net/row-and-column-management/how-to-use-wrapcols-create-a-two-column-layout-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية استخدام WRAPCOLS: إنشاء تخطيط بعمودين في C#

هل تساءلت يومًا **كيف تستخدم WRAPCOLS** عندما تحتاج إلى عرض سريع بعمودين داخل ورقة عمل تشبه Excel؟ لست وحدك. يواجه العديد من المطورين صعوبة عندما يحاولون تقسيم قائمة مُولَّدة إلى أعمدة مرتبة دون كتابة حلقة لكل خلية. الخبر السار؟ باستخدام دالة `WRAPCOLS` يمكنك وضع صيغة واحدة في `A1` وتترك Excel (أو محرك متوافق) يقوم بالعمل الشاق.

في هذا الدرس سنستعرض **كيفية إضافة صيغة** التي تُنشئ **تخطيطًا بعمودين**، وسنُظهر لك **كيفية إنشاء الأعمدة** بشكل ديناميكي، وحتى **إنشاء مصفوفة تسلسلية** في الوقت الفعلي. في النهاية ستحصل على مقطع C# قابل للتنفيذ بالكامل يمكنك لصقه في مشروعك، تشغيله، ورؤية كتلة مرتبة بعمودين تظهر فورًا.

## ما ستتعلمه

- غرض `WRAPCOLS` ولماذا تُعد بديلاً أفضل عن التكرار اليدوي.  
- كيفية **إضافة صيغة** إلى خلية ورقة عمل باستخدام C#.  
- كيفية إنشاء مصفوفة تسلسلية باستخدام `SEQUENCE` وإدخالها في `WRAPCOLS`.  
- نصائح لإعادة حساب الورقة بحيث تُحل الصيغة فورًا.  
- معالجة الحالات الحدية (مثل أوراق العمل الفارغة، عدد الأعمدة المخصص).

لا تحتاج إلى مكتبات خارجية بخلاف حزمة معالجة Excel القياسية – سنستخدم **ClosedXML** لواجهة برمجة التطبيقات البسيطة الخاصة به، لكن المفاهيم يمكن تطبيقها على EPPlus أو SpreadsheetGear أو حتى Google Sheets عبر API الخاص به.

---

## المتطلبات المسبقة

- .NET 6.0 أو أحدث (الكود يُترجم على .NET Core و .NET Framework).  
- إشارة إلى **ClosedXML** (`dotnet add package ClosedXML`).  
- معرفة أساسية بـ C# – يجب أن تكون مرتاحًا مع عبارات `using` وتهيئة الكائنات.  

إذا كان لديك دفتر عمل مفتوح بالفعل، يمكنك تخطي جزء إنشاء الملف والانتقال مباشرة إلى قسم الصيغة.

---

## الخطوة 1: إعداد ورقة العمل (كيفية إنشاء الأعمدة)

أولاً نحتاج إلى كائن `Worksheet` للعمل معه. في ClosedXML تحصل عليه من `XLWorkbook`. المقتطف أدناه ينشئ دفتر عمل جديد، يضيف ورقة تسمى *Demo*، ويحصل على مرجع باسم `worksheet` للتوضيح.

```csharp
using ClosedXML.Excel;

namespace WrapColsDemo
{
    class Program
    {
        static void Main()
        {
            // Create a fresh workbook and add a worksheet named "Demo"
            using var workbook = new XLWorkbook();
            var ws = workbook.Worksheets.Add("Demo");

            // Rename for clarity – this is the worksheet we’ll manipulate
            var worksheet = ws;   // <-- same object, just a clearer name

            // --------------------------------------------------------------
            // Next step: write the WRAPCOLS formula
            // --------------------------------------------------------------
```

> **لماذا إعادة التسمية؟**  
> الحفاظ على اسم المتغير قصيرًا (`worksheet`) يجعل الكود اللاحق أسهل للقراءة، خاصةً عندما تسلسل عمليات متعددة. كما أنه يعكس نمط التسمية الذي ستراه في معظم الوثائق، مما يقلل العبء الإدراكي.

---

## الخطوة 2: كتابة الصيغة (كيفية إضافة صيغة + إنشاء مصفوفة تسلسلية)

الآن يأتي السطر السحري. سنضع صيغة في الخلية **A1** تقوم بشيئين:

1. **إنشاء مصفوفة تسلسلية** من ستة أرقام (`SEQUENCE(6)` → 1,2,3,4,5,6).  
2. **تغليف تلك الأرقام في عمودين** (`WRAPCOLS(..., 2)`).

```csharp
            // Write the WRAPCOLS formula into A1
            worksheet.Cell("A1").FormulaA1 = "=WRAPCOLS(SEQUENCE(6), 2)";

            // --------------------------------------------------------------
            // Finally, force the engine to evaluate the formula
            // --------------------------------------------------------------
```

> **ما الذي يحدث؟**  
> `SEQUENCE(6)` تُنشئ مصفوفة عمودية `{1;2;3;4;5;6}`. ثم تقوم `WRAPCOLS` بأخذ تلك المصفوفة و“تغليفها” في عدد الأعمدة المحدد — في هذه الحالة **2**. النتيجة هي كتلة من 3 صفوف × 2 عمود تبدو كالتالي:

| A | B |
|---|---|
| 1 | 4 |
| 2 | 5 |
| 3 | 6 |

إذا غيرت الوسيط الثاني إلى **3**، ستحصل على تخطيط بثلاثة أعمدة بدلاً من ذلك. هذا هو جوهر **كيفية إنشاء الأعمدة** في الوقت الفعلي دون حلقات يدوية.

---

## الخطوة 3: إعادة حساب ورقة العمل (ضمان تقييم الصيغة)

ClosedXML لا يقوم تلقائيًا بتقييم الصيغ عند كتابتها. تحتاج إلى استدعاء `Calculate()` على دفتر العمل (أو على ورقة العمل المحددة) لإجبار التقييم.

```csharp
            // Recalculate so the formula is evaluated immediately
            worksheet.Calculate();

            // Optional: save the workbook to inspect the result
            workbook.SaveAs("WrapColsDemo.xlsx");
        }
    }
}
```

> **نصيحة احترافية:** إذا كنت تتعامل مع دفاتر عمل كبيرة، استدعِ `Calculate()` فقط على الأوراق التي تغيرت فعليًا. هذا يوفر الذاكرة ويسرّع المعالجة.

عند فتح `WrapColsDemo.xlsx` سترى تخطيط العمودين مُعبأً بشكل مرتب في **A1:B3**. لم يُطلب أي كود إضافي للتكرار عبر الصفوف أو الأعمدة – `WRAPCOLS` تعامل مع كل شيء.

---

## الخطوة 4: التحقق من النتيجة (ما المتوقع)

بعد تشغيل البرنامج، افتح الملف المُنشأ. يجب أن ترى:

| A | B |
|---|---|
| 1 | 4 |
| 2 | 5 |
| 3 | 6 |

إذا ظهرت الأرقام عموديًا (أي كلها في العمود A)، تحقق مرة أخرى من أنك استدعيت `worksheet.Calculate()` **بعد** تعيين الصيغة. بعض المحركات تحتاج أيضًا إلى `workbook.Calculate()`؛ المقتطف أعلاه يعمل مع مُقَيِّم ClosedXML المدمج.

---

## الاختلافات الشائعة والحالات الحدية

### تغيير عدد الأعمدة

لـ **إنشاء تخطيط بعمودين** مع عدد صفوف مختلف، قم ببساطة بتعديل حجم `SEQUENCE` أو الوسيط الثاني لـ `WRAPCOLS`:

```csharp
worksheet.Cell("A1").FormulaA1 = "=WRAPCOLS(SEQUENCE(12), 3)";
```

هذا ينتج كتلة من 4 صفوف × 3 أعمدة (12 رقمًا موزعة عبر ثلاثة أعمدة).

### استخدام عدد أعمدة ديناميكي

إذا كان عدد الأعمدة يأتي من متغير، أدخله باستخدام الاستبدال النصي (string interpolation):

```csharp
int colCount = 4;
worksheet.Cell("A1").FormulaA1 = $"=WRAPCOLS(SEQUENCE(8), {colCount})";
```

الآن لديك **كيفية إضافة صيغة** تتكيف أثناء وقت التشغيل.

### أوراق عمل فارغة

إذا كانت ورقة العمل فارغة، فإن `Calculate()` لا يزال يعمل – ستملأ الصيغة الخلايا بدءًا من A1. ومع ذلك، إذا حذفت لاحقًا صفوفًا/أعمدة تتقاطع مع نطاق الإخراج، قد ترى أخطاء `#REF!`. لتجنب ذلك، امسح نطاق الهدف أولاً:

```csharp
worksheet.Range("A1:Z100").Clear(); // wipes any leftovers
```

### التوافق

`WRAPCOLS` و `SEQUENCE` جزء من وظائف **المصفوفة الديناميكية** في Excel، التي تم تقديمها في Office 365. إذا استهدفت إصدارات Excel أقدم، فإن هذه الدوال لن تكون موجودة، وستحتاج إلى حلقة يدوية. مُقَيِّم ClosedXML يعكس سلوك Excel الأحدث، لذا فهو آمن للبيئات الحديثة.

---

## مثال كامل يعمل (جاهز للنسخ واللصق)

```csharp
using ClosedXML.Excel;

namespace WrapColsDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create workbook & worksheet
            using var workbook = new XLWorkbook();
            var ws = workbook.Worksheets.Add("Demo");
            var worksheet = ws;   // clearer name

            // 2️⃣ Write WRAPCOLS formula that generates a sequence array
            worksheet.Cell("A1").FormulaA1 = "=WRAPCOLS(SEQUENCE(6), 2)";

            // 3️⃣ Force calculation so the formula resolves immediately
            worksheet.Calculate();

            // 4️⃣ Save the file (optional, but handy for verification)
            workbook.SaveAs("WrapColsDemo.xlsx");
        }
    }
}
```

**النتيجة المتوقعة:** عند فتح *WrapColsDemo.xlsx* سيظهر تخطيط بعمودين مرتب مع الأرقام 1‑6 كما هو موضح سابقًا.

---

## الخلاصة

لقد غطينا **كيفية استخدام WRAPCOLS** لإنشاء **تخطيط بعمودين**، وعرضنا **كيفية إضافة صيغة** برمجيًا، ورأينا كيف تسمح لك `SEQUENCE` **بإنشاء مصفوفة تسلسلية** دون الحاجة إلى حلقة. من خلال الاستفادة من وظائف المصفوفة الديناميكية في Excel عبر C#، يمكنك الحفاظ على شفرتك مختصرة، قابلة للقراءة، وسهلة الصيانة.

بعد ذلك، قد تستكشف:

- **إنشاء عدد صفوف ديناميكي** باستخدام `ROWS` أو `COUNTA`.  
- **تنسيق المخرجات** (الحدود، تنسيقات الأرقام) باستخدام API التنسيق في ClosedXML.  
- **التصدير إلى CSV** بعد بناء التخطيط، للمعالجة اللاحقة.

جرّبه، عدّل عدد الأعمدة، وشاهد مدى السرعة التي يمكنك بها إنشاء نماذج جداول بيانات معقدة. برمجة سعيدة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}