---
category: general
date: 2026-05-04
description: كيفية حساب قاطع الظل أثناء إنشاء مصنف Excel بلغة C#. تعلّم كيفية استخدام
  دالة EXPAND، حفظ المصنف، وأتمتة الحسابات.
draft: false
keywords:
- how to calculate cotangent
- create excel workbook
- how to use expand
- how to save workbook
- use expand function
language: ar
og_description: كيفية حساب قاطع الظل في Excel باستخدام C#. يوضح هذا الدرس كيفية إنشاء
  مصنف Excel، واستخدام EXPAND، وحفظ الملف.
og_title: كيفية حساب قاطع الظل في إكسل – دليل كامل لدفتر عمل C#
tags:
- C#
- Aspose.Cells
- Excel Automation
title: كيفية حساب قاطع الزاوية في Excel باستخدام C# – إنشاء مصنف، استخدام EXPAND،
  وحفظه
url: /ar/net/formulas-functions/how-to-calculate-cotangent-in-excel-with-c-create-workbook-u/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية حساب الظل المقلوب في Excel باستخدام C# – دليل كامل

هل تساءلت يومًا **كيفية حساب الظل المقلوب** مباشرة داخل ملف Excel تم إنشاؤه بواسطة C#؟ ربما تقوم ببناء نموذج مالي، أو تقرير علمي، أو مجرد أتمتة مهمة مملة في جدول البيانات. الخبر السار؟ يمكنك القيام بذلك ببضع أسطر من الشيفرة—دون صيغ يدوية، دون تمارين النسخ‑اللصق.

في هذا الدرس سنستعرض إنشاء مصنف Excel، توسيع مصفوفة باستخدام دالة **EXPAND**، إدراج صيغة **COT** لحساب الظل المقلوب للزاوية 45°، وأخيرًا حفظ الملف حتى تتمكن من فتحه في Excel ورؤية النتائج. على طول الطريق سنغطي أيضًا **how to use expand**، **how to save workbook**، وبعض النصائح المفيدة التي غالبًا ما تُغفل.

> **Quick answer:** استخدم Aspose.Cells (أو Microsoft Interop) لإنشاء مصنف، عيّن `ws.Cells["A1"].Formula = "=EXPAND({1,2,3},5,1)"`، عيّن `ws.Cells["B1"].Formula = "=COT(PI()/4)"`، ثم استدعِ `workbook.Save("output.xlsx")`.

## ما الذي ستحتاجه

- **.NET 6+** (أو أي بيئة تشغيل .NET حديثة).  
- **Aspose.Cells for .NET** (نسخة تجريبية مجانية أو نسخة مرخصة).  
- فهم أساسي لبنية جمل C#.  
- Visual Studio، Rider، أو أي محرر تفضله.

لا يلزم أي إضافات Excel إضافية؛ كل شيء يعمل على الخادم والملف الناتج يعمل على أي نسخة حديثة من Excel.

## الخطوة 1: إنشاء مصنف Excel من C#

إنشاء مصنف هو الأساس. فكر فيه كفتح دفتر جديد قبل أن تبدأ الكتابة.

```csharp
using Aspose.Cells;

// Step 1: Initialize a new workbook object
Workbook workbook = new Workbook();               // Empty workbook
Worksheet ws = workbook.Worksheets[0];            // Grab the first sheet
```

**لماذا هذا مهم:**  
`Workbook` يمثل الحزمة الكاملة `.xlsx`. بشكل افتراضي تحتوي على ورقة واحدة، التي نصل إليها عبر `Worksheets[0]`. إذا احتجت أوراقًا إضافية لاحقًا، يمكنك إضافتها باستخدام `workbook.Worksheets.Add()`.

> **Pro tip:** إذا كنت تستهدف .NET Core، تأكد من أن حزمة Aspose.Cells NuGet تتطابق مع بيئة التشغيل الخاصة بك لتجنب فقدان التبعيات الأصلية.

## الخطوة 2: استخدام دالة EXPAND لملء عمود

دالة **EXPAND** هي طريقة Excel لتحويل مصفوفة ثابتة إلى نطاق ديناميكي. إنها مثالية عندما تريد توليد عمود من القيم دون كتابة كل خلية يدويًا.

```csharp
// Step 2: Write an EXPAND formula in cell A1
ws.Cells["A1"].Formula = "=EXPAND({1,2,3},5,1)"; // Expands to a 5‑row column
```

### كيف تعمل

- `{1,2,3}` هي مصفوفة المصدر (ثلاثة أرقام).  
- `5` تخبر Excel بإنتاج **5 صفوف**.  
- `1` تخبر Excel بإنتاج **عمود واحد**.  

عند فتح الملف المحفوظ، الخلايا من A1 إلى A5 ستحتوي على `1, 2, 3, 0, 0` (الصفوف الإضافية مملوءة بالأصفار).

**حالة خاصة:** إذا كان معامل `rows` أصغر من طول مصفوفة المصدر، يقوم Excel بقطع المصفوفة. لذا `=EXPAND({1,2,3},2,1)` سيظهر فقط `1` و `2`.

## الخطوة 3: إدراج صيغة COT لحساب الظل المقلوب

الآن نأتي إلى نجمة العرض: **how to calculate cotangent** في Excel. دالة `COT` تتوقع زاوية بالراديان، لذا نمرر لها `PI()/4` (التي تساوي 45°).

```csharp
// Step 3: Write a COT formula in cell B1
ws.Cells["B1"].Formula = "=COT(PI()/4)"; // Returns 1
```

### لماذا نستخدم COT بدلاً من Tan؟

الظل المقلوب هو مقلوب الظل (`cot = 1 / tan`). بينما يمكنك كتابة `=1/TAN(PI()/4)`, فإن استخدام `COT` أنظف ويتجنب أخطاء القسمة على الصفر عندما تكون الزاوية 0° أو 180°.

**النتيجة المتوقعة:** فتح `output.xlsx` سيظهر `1` في B1، لأن الظل المقلوب للزاوية 45° (π/4 راديان) يساوي 1.

**ماذا لو أحتاج إلى درجات؟**  
دوال المثلثات في Excel تعمل بالراديان. حوّل الدرجات باستخدام `RADIANS(deg)`. على سبيل المثال: `=COT(RADIANS(60))`.

## الخطوة 4: حفظ المصنف حتى تتمكن من مشاهدة النتائج

الحفظ هو القطعة الأخيرة من اللغز. يمكنك الكتابة إلى أي مجلد لديك صلاحية كتابة فيه.

```csharp
// Step 4: Persist the workbook to disk
string outputPath = Path.Combine(
    Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
    "output.xlsx");

// Save the workbook (the default format is .xlsx)
workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to {outputPath}");
```

### كيفية الحفظ بصيغ مختلفة

- **XLS** – `workbook.Save("output.xls", SaveFormat.Excel97To2003);`  
- **CSV** – `workbook.Save("output.csv", SaveFormat.CSV);`  

إذا احتجت أبدًا إلى تدفق الملف (مثلاً لواجهة برمجة تطبيقات ويب)، استخدم `workbook.Save(stream, SaveFormat.Xlsx)` بدلاً من ذلك.

## مثال كامل يعمل

بجمع كل ذلك معًا، إليك برنامج مستقل يمكنك نسخه ولصقه في تطبيق كونسول.

```csharp
using System;
using System.IO;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet ws = workbook.Worksheets[0];

        // 2️⃣ Expand an array {1,2,3} into a 5‑row column starting at A1
        ws.Cells["A1"].Formula = "=EXPAND({1,2,3},5,1)";

        // 3️⃣ Calculate cotangent of 45° (π/4) in B1
        ws.Cells["B1"].Formula = "=COT(PI()/4)";

        // 4️⃣ Define where to save the file (Desktop for easy access)
        string outputPath = Path.Combine(
            Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
            "output.xlsx");

        // 5️⃣ Save the workbook
        workbook.Save(outputPath);
        Console.WriteLine($"✅ Workbook saved at: {outputPath}");
    }
}
```

**التحقق من النتيجة:**  
- افتح `output.xlsx`.  
- يجب أن يحتوي العمود A على `1, 2, 3, 0, 0`.  
- يجب أن تعرض الخلية B1 القيمة `1`.  

إذا رأيت تلك القيم، فقد تعلمت بنجاح **how to calculate cotangent** برمجيًا وكيفية **create excel workbook**، **use expand function**، و **save workbook**—كل ذلك في خطوة واحدة.

## أسئلة شائعة ومشكلات محتملة

### هل تعمل `COT` في إصدارات Excel القديمة؟

نعم، `COT` موجود منذ Excel 2007. إذا كنت تستهدف Excel 2003 (`.xls`)، ستحتاج إلى استبداله بـ `1/TAN(...)` لأن `COT` غير متوفر هناك.

### ماذا لو لم تقم الصيغة بإعادة الحساب تلقائيًا؟

Aspose.Cells يقوم بتقييم الصيغ بشكل كسول. استدعِ `workbook.CalculateFormula()` قبل الحفظ إذا كنت بحاجة إلى القيم المحسوبة مدمجة في الملف.

```csharp
workbook.CalculateFormula();
workbook.Save(outputPath);
```

### هل يمكنني كتابة النتيجة مباشرة دون صيغة؟

بالتأكيد، يمكنك حساب القيمة في C# (`Math.Cos(Math.PI / 4) / Math.Sin(Math.PI / 4)`) وتعيينها إلى `ws.Cells["B1"].Value = result;`. يركز الدرس على صيغ Excel لأنها تظل ديناميكية—تغيير الزاوية لاحقًا سيؤدي إلى تحديث تلقائي.

## نصائح احترافية للمشاريع الواقعية

- **Batch operations:** إذا كنت تملأ آلاف الصفوف، عطل الحساب (`workbook.Settings.CalculateFormulaOnOpen = false`) أثناء الكتابة، ثم فعّله مرة واحدة.  
- **Naming ranges:** استخدم `ws.Cells.CreateRange("MyArray", "A1:A5")` واشر إلى الاسم في الصيغ للحصول على جداول بيانات أوضح.  
- **Error handling:** غلف `workbook.Save` داخل try/catch لإظهار مشاكل الأذونات (`UnauthorizedAccessException`).  

## الخاتمة

لقد غطينا **how to calculate cotangent** في ورقة Excel تم إنشاؤها بواسطة C#، وأظهرنا **how to use expand** لملء عمود، وعرضنا **how to save workbook** للفحص الفوري. المثال الكامل القابل للتنفيذ أعلاه يمنحك أساسًا قويًا لأتمتة أي جدول بيانات يجمع بين البيانات الثابتة والحسابات المثلثية.

الخطوات التالية؟ جرّب استبدال الزاوية في صيغة `COT` بخلية مرجعية (`=COT(PI()*A1/180)`) لتسمح للمستخدمين بإدخال درجات. أو استكشف دوال رياضية أخرى مثل `SIN`، `COS`، و `ATAN2`—جميعها تعمل بنفس الطريقة داخل مصنف مُولد.

برمجة سعيدة، ولتظل جداول بياناتك خالية من الأخطاء! 🚀

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}