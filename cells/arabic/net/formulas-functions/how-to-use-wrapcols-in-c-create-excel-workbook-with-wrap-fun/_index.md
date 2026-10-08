---
category: general
date: 2026-03-30
description: تعلم كيفية استخدام WRAPCOLS في C# لإنشاء مصنف Excel، وإضافة البيانات
  إلى Excel، وإجبار حساب الصيغ مع استخدام WRAPROWS أيضًا.
draft: false
keywords:
- how to use wrapcols
- create excel workbook c#
- add data to excel
- force formula calculation
- how to use wraprows
language: ar
og_description: اكتشف كيفية استخدام WRAPCOLS في C# لإنشاء مصنف Excel، وإضافة البيانات،
  وإجبار حساب الصيغ، والاستفادة من WRAPROWS للصيغ المصفوفية.
og_title: كيفية استخدام WRAPCOLS في C# – دليل كامل
tags:
- Aspose.Cells
- C#
- Excel Automation
title: كيفية استخدام WRAPCOLS في C# – إنشاء مصنف Excel باستخدام وظائف التغليف
url: /ar/net/formulas-functions/how-to-use-wrapcols-in-c-create-excel-workbook-with-wrap-fun/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية استخدام WRAPCOLS في C# – إنشاء دفتر عمل Excel باستخدام وظائف الالتفاف

هل تساءلت يومًا **كيف تستخدم WRAPCOLS** عندما تقوم بأتمتة Excel باستخدام C#؟ لست وحدك—العديد من المطورين يواجهون صعوبة عندما يحتاجون إلى تحويل نطاق أفقي إلى مصفوفة عمودية دون كتابة الكثير من الشيفرة. الخبر السار هو أن Aspose.Cells يجعل ذلك سهلًا للغاية.

في هذا البرنامج التعليمي سنستعرض مثالًا كاملًا قابلًا للتنفيذ يُظهر **كيف تستخدم WRAPCOLS**، وكيف **تنشئ دفتر عمل Excel بأسلوب C#**، وكيف **تضيف بيانات إلى Excel**، وحتى كيف **تجبر حساب الصيغ** لتظهر النتائج فورًا. سنضيف أيضًا **كيفية استخدام WRAPROWS** للتحويل العكسي. في النهاية ستحصل على برنامج جاهز للتنفيذ وفهم واضح لأهمية كل خطوة.

---

![How to use WRAPCOLS in C# example](alt="Screenshot showing Excel workbook after using WRAPCOLS in C#")

## ما يغطيه هذا الدليل

* إعداد دفتر عمل جديد باستخدام Aspose.Cells.
* ملء الخلايا برمجيًا (**add data to Excel**).
* تطبيق دالة `WRAPCOLS` لتحويل صف إلى عمود.
* استخدام `WRAPROWS` لإعادة عمود إلى صف (**how to use wraprows**).
* إجبار المحرك على حساب الصيغ فورًا (**force formula calculation**).
* حفظ الملف والتحقق من النتيجة.

لا حاجة إلى أي وثائق خارجية—كل ما تحتاجه موجود هنا.

---

## كيفية استخدام WRAPCOLS في C# – تنفيذ خطوة بخطوة

فيما يلي ملف المصدر الكامل. يمكنك نسخه ولصقه في مشروع وحدة تحكم جديد، إضافة حزمة Aspose.Cells عبر NuGet، ثم الضغط على **F5**.

```csharp
// ------------------------------------------------------------
// How to Use WRAPCOLS in C# – Complete Example
// ------------------------------------------------------------
using System;
using Aspose.Cells;

namespace WrapFunctionsDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create a fresh workbook (this is how we **create excel workbook c#** style)
            Workbook workbook = new Workbook();

            // 2️⃣ Grab the first worksheet – it's created by default
            Worksheet sheet = workbook.Worksheets[0];

            // 3️⃣ **Add data to Excel**: place two numbers side‑by‑side
            sheet.Cells["A1"].PutValue(1);   // first value
            sheet.Cells["B1"].PutValue(2);   // second value

            // 4️⃣ **How to use WRAPCOLS** – turn the horizontal range A1:B1 into a vertical array
            //    The second argument (1) tells WRAPCOLS to create 1 column per element.
            sheet["C1"].Formula = "WRAPCOLS(A1:B1, 1)";

            // 5️⃣ **How to use WRAPROWS** – the opposite; turn the same range into a horizontal array
            //    Here we ask for 2 rows per element, which produces a single row with both values.
            sheet["C2"].Formula = "WRAPROWS(A1:B1, 2)";

            // 6️⃣ **Force formula calculation** so the workbook reflects the results immediately
            workbook.CalculateFormula();

            // 7️⃣ Save the workbook to disk – change the path to a folder you own
            string outputPath = @"WrapFunctions.xlsx";
            workbook.Save(outputPath);

            Console.WriteLine($"Workbook saved to {outputPath}");
            Console.WriteLine("Check cells C1 and C2 for the WRAPCOLS / WRAPROWS results.");
        }
    }
}
```

### لماذا كل سطر مهم

| الخطوة | الشرح |
|------|-------------|
| **1️⃣ إنشاء دفتر عمل جديد** | هذا هو الأساس. Aspose.Cells يتعامل مع كائن `Workbook` كملف Excel كامل، لذا أنت فعليًا **تنشئ دفتر عمل Excel بأسلوب C#**. |
| **2️⃣ الحصول على ورقة العمل الأولى** | يحتوي دفتر العمل الجديد دائمًا على ورقة عمل واحدة على الأقل (`Worksheets[0]`). الوصول إليها مبكرًا يجنبك مفاجآت الـ null‑reference. |
| **3️⃣ إضافة بيانات إلى Excel** | باستخدام `PutValue` نحن **نضيف بيانات إلى Excel** دون القلق بشأن تنسيق الخلية. الأرقام `1` و `2` هي بيانات الاختبار لدوال الالتفاف. |
| **4️⃣ كيفية استخدام WRAPCOLS** | `WRAPCOLS(A1:B1, 1)` يخبر Excel بأخذ النطاق `A1:B1` وإسقاط قيمه عموديًا، قيمة واحدة لكل صف. النتيجة تُوضع في `C1` وتستمر إلى الأسفل (`C1`, `C2`, …). |
| **5️⃣ كيفية استخدام WRAPROWS** | `WRAPROWS(A1:B1, 2)` يقوم بالعكس: يُنشئ إسقاطًا أفقيًا، يضع القيمتين في صف واحد يبدأ من `C2`. |
| **6️⃣ إجبار حساب الصيغة** | بشكل افتراضي قد يؤجل Aspose.Cells الحساب حتى يُفتح الملف في Excel. استدعاء `CalculateFormula()` **يجبر حساب الصيغة** حتى يمكنك قراءة النتائج فورًا بعد الحفظ. |
| **7️⃣ حفظ دفتر العمل** | الخطوة الأخيرة تكتب كل شيء إلى القرص. افتح الملف الناتج `WrapFunctions.xlsx` لرؤية النتيجة. |

---

## إنشاء دفتر عمل Excel C# – إعداد البيئة

قبل تشغيل الشيفرة، تأكد من توفر الأدوات الصحيحة:

1. **.NET 6.0+** – أحدث نسخة LTS هي الأنسب.
2. **Visual Studio 2022** (أو VS Code مع امتداد C#).
3. **Aspose.Cells for .NET** – تثبيت عبر NuGet:  
   ```bash
   dotnet add package Aspose.Cells
   ```
4. مجلد قابل للكتابة لحفظ الملف الناتج.

هذه المتطلبات قليلة؛ لا حاجة إلى COM interop أو تثبيت Office، وهذا هو السبب في أن Aspose.Cells خيار شائع لإنشاء Excel على الخادم.

---

## إضافة بيانات إلى Excel – أفضل الممارسات

عند **إضافة بيانات إلى Excel** برمجيًا، ضع في اعتبارك النصائح التالية:

* **استخدم `PutValue`** للأرقام أو السلاسل الخام؛ فهو يكتشف نوع البيانات تلقائيًا.
* **تجنب كتابة عناوين الخلايا يدويًا** في المشاريع الكبيرة—استخدم الحلقات أو النطاقات المسماة لتسهيل التوسع.
* **قم بتطبيق الأنماط على الخلايا باعتدال**؛ كل تغيير نمط يضيف عبئًا. إذا احتجت تنسيقًا، أنشئ كائن نمط واحد وطبقه على خلايا متعددة.

في مثالنا الصغير نُدخل رقمين فقط، لكن النمط نفسه يمكن توسيعه لآلاف الصفوف.

---

## كيفية استخدام WRAPROWS – مثال على مصفوفة أفقية

إذا كنت تحتاج إلى عكس `WRAPCOLS`، فإن `WRAPROWS` هو ما يلزمك. الصياغة هي:

```
WRAPROWS(source_range, [rows_per_item])
```

* `source_range` – النطاق الذي تريد تحويله.
* `rows_per_item` – اختياري؛ يحدد عدد الصفوف التي يشغلها كل عنصر. في مثالنا استخدمنا `2` لإجبار القيمتين على التواجد في صف واحد.

يمكنك التجربة بتغيير الوسيط الثاني:

```csharp
// Example: split each value into its own column, three rows per item
sheet["D1"].Formula = "WRAPROWS(A1:B1, 3)";
```

افتح دفتر العمل وسترى القيم تُسقط عبر ثلاثة أعمدة، كل عمود يحتوي على الأرقام الأصلية مكررة حسب الحاجة.

---

## إجبار حساب الصيغة – متى ولماذا

قد تتساءل، “هل أحتاج حقًا لاستدعاء `CalculateFormula()`؟” الجواب **نعم** إذا:

* كنت تخطط لقراءة القيم المحسوبة **برمجيًا** بعد الحفظ.
* تريد ضمان أن الملف يفتح في Excel مع عرض النتائج الصحيحة مسبقًا.
* تعمل في **بيئة بدون واجهة** (مثل API ويب) حيث لا يُجري المستخدم إعادة حساب يدويًا.

تخطي هذه الخطوة لن يُكسر دفتر العمل، لكن الخلايا ستظهر نص الصيغة (`=WRAPCOLS(...)`) بدلاً من القيم المحسوبة حتى يقوم Excel بإعادة الحساب.

---

## النتيجة المتوقعة – ما الذي تبحث عنه

بعد تشغيل البرنامج وفتح `WrapFunctions.xlsx`:

| الخلية | الصيغة | القيمة المعروضة |
|------|---------|-----------------|
| **C1** | `=WRAPCOLS(A1:B1, 1)` | `1` (في C1) و `2` (في C2) – قائمة عمودية |
| **C2** | `=WRAPROWS(A1:B1, 2)` | `1` في C2 و `2` في D2 – قائمة أفقية |

سترى عمودًا من القيم يبدأ من **C1** وصفًا من القيم يبدأ من **C2**. هذا يؤكد أن كلتا دالتي الالتفاف عملتا كما هو متوقع.

---

## الحالات الخاصة والتنوعات

| السيناريو | ما الذي يتغير؟ | التعديل المقترح |
|----------|---------------|-----------------|
| **نطاق كبير (A1:Z1)** | مزيد من القيم لتُسقط عموديًا | زيادة الوسيط الثاني لـ `WRAPCOLS` إذا أردت أعمدة متعددة لكل مجموعة. |
| **بيانات غير رقمية** | السلاسل تُعامل بنفس الطريقة | لا تغيير في الشيفرة؛ `PutValue` يقبل أي كائن. |
| **نطاق ديناميكي** | لا تعرف الحجم أثناء التجميع | استخدم `sheet.Cells.MaxDataColumn` و `MaxDataRow` لبناء سلسلة العنوان. |
| **عدة أوراق عمل** | تحتاج لتطبيق دوال الالتفاف على أوراق مختلفة | أشِر إلى ورقة العمل الصحيحة (`workbook.Worksheets["Sheet2"]`). |

بتوقع هذه الاختلافات، يمكنك تعديل النمط الأساسي ليتناسب مع أي سيناريو أتمتة تقريبًا.

---

## نصائح احترافية من الميدان

* **نصيحة احترافية:** ضع إنشاء دفتر العمل داخل كتلة `using` إذا كنت تستهدف .NET Core 3.1+ لضمان تحرير جميع الموارد بسرعة.
* **احذر من:** تعيين الصيغة نفسها على نطاق كبير دون استدعاء `CalculateFormula()` قد يسبب اختناقات أداء. عالج الصيغ على دفعات عندما يكون ذلك ممكنًا.
* **نصيحة:** إذا كنت بحاجة لقراءة القيم المحسوبة مرة أخرى في الشيفرة، استدعِ `

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}