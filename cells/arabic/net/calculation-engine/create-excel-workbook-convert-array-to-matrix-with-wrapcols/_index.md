---
category: general
date: 2026-03-29
description: إنشاء مصنف Excel وتعلم كيفية استخدام WRAPCOLS لتحويل المصفوفة إلى مصفوفة،
  وإجبار الحساب، وحفظ المصنف بصيغة XLSX.
draft: false
keywords:
- create excel workbook
- convert array to matrix
- save workbook as xlsx
- how to use wrapcols
- force workbook calculation
language: ar
og_description: إنشاء مصنف Excel باستخدام C#، تحويل المصفوفة إلى مصفوفة باستخدام WRAPCOLS،
  إجبار حساب المصنف وحفظه كملف XLSX. الكود الكامل والنصائح.
og_title: إنشاء مصنف إكسل – دليل خطوة بخطوة
tags:
- Aspose.Cells
- C#
- Excel automation
title: إنشاء مصنف إكسل – تحويل المصفوفة إلى مصفوفة باستخدام WRAPCOLS
url: /ar/net/calculation-engine/create-excel-workbook-convert-array-to-matrix-with-wrapcols/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء دفتر عمل Excel – تحويل المصفوفة إلى مصفوفة ثنائية الأبعاد باستخدام WRAPCOLS

هل احتجت يوماً إلى **إنشاء دفتر عمل Excel** من الصفر وفجأة واجهت صعوبة عند محاولة إعادة تشكيل البيانات؟ لست وحدك. العديد من المطورين يلجؤون إلى مصفوفة بسيطة، فقط ليكتشفوا أن Excel يتوقع نطاقًا ثنائي الأبعاد صحيحًا.  

في هذا الدرس سنوضح لك بالضبط كيف **تنشئ دفتر عمل Excel**، وتستخدم الدالة `WRAPCOLS` لت **تحويل المصفوفة إلى مصفوفة**، **تفرض حساب دفتر العمل**، وأخيرًا **تحفظ دفتر العمل كملف XLSX**. في النهاية ستحصل على برنامج C# قابل للتنفيذ يقوم بكل ذلك في بضع أسطر فقط.

> **نصيحة احترافية:** النمط نفسه يعمل مع مجموعات بيانات أكبر، لذا يمكنك التوسع من عرض توضيحي مكوّن من 4 عناصر إلى آلاف الصفوف دون تعديل المنطق الأساسي.

## ما ستحتاجه

- .NET 6 أو أحدث (أي بيئة تشغيل .NET حديثة تعمل)
- Aspose.Cells for .NET (المكتبة التي توفر `Workbook`، `Worksheet`، إلخ)
- محرر شفرة أو بيئة تطوير (Visual Studio، VS Code، Rider – اختر ما تفضله)
- صلاحية كتابة إلى مجلد سيتم حفظ الملف الناتج فيه

لا توجد حزم NuGet إضافية مطلوبة بخلاف Aspose.Cells؛ باقي الشيفرة هي C# نقي.

## الخطوة 1 – إنشاء دفتر عمل Excel (الكلمة المفتاحية الأساسية في التنفيذ)

لبدء العملية، نقوم بإنشاء كائن `Workbook` جديد ونستخرج الورقة الأولى. هذا هو الأساس لكل ما سيأتي بعد ذلك.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();               // creates a blank Excel file in memory
        Worksheet ws = workbook.Worksheets[0];           // default sheet is named "Sheet1"
```

**لماذا هذا مهم:**  
إنشاء دفتر عمل برمجيًا يمنحك التحكم الكامل في التنسيق، الصيغ، وإدخال البيانات قبل أن يلمس أي شيء القرص. كما يعني أنه يمكنك توليد ملفات على الخادم دون الحاجة لفتح Excel.

## الخطوة 2 – إدراج صيغة WRAPCOLS لتحويل المصفوفة إلى مصفوفة

`WRAPCOLS` هي دالة مدمجة في Excel تعيد تشكيل مصفوفة أحادية البُعد إلى مصفوفة ذات عدد أعمدة محدد. هنا نحول `{1,2,3,4}` إلى تخطيط بعمودين.

```csharp
        // Step 2: Insert a WRAPCOLS formula that converts a 1‑D array into a 2‑column matrix
        ws.Cells["A1"].Formula = "=WRAPCOLS({1,2,3,4},2)";
```

**كيف يعمل:**  
- الوسيط الأول `{1,2,3,4}` هو مصفوفة مضمنة مباشرة.  
- الوسيط الثاني `2` يخبر Excel بلف القيم إلى عمودين، مما ينتج:

| A | B |
|---|---|
| 1 | 2 |
| 3 | 4 |

إذا احتجت إلى شكل مختلف، فقط غيّر الوسيط الثاني – `WRAPCOLS({1,2,3,4,5,6},3)` سيعطيك ثلاثة أعمدة.

## الخطوة 3 – فرض حساب دفتر العمل حتى تظهر الصيغة

بشكل افتراضي، تقوم Aspose.Cells بتقييم الصيغ بشكل كسول. لضمان ظهور المصفوفة في الملف، نستدعي صراحةً `Calculate()`.

```csharp
        // Step 3: Force calculation so the formula result is materialized
        workbook.Calculate();   // forces evaluation of all formulas in the workbook
```

**لماذا فرض الحساب؟**  
إذا تخطيت هذه الخطوة، سيظل الملف المحفوظ يحتوي على الصيغة لكن الخلايا ستظهر فارغة حتى يفتح المستخدم دفتر العمل ويسمح لـ Excel بإعادة الحساب. في خطوط الأنابيب الآلية عادةً ما تريد القيم مدمجة مسبقًا.

## الخطوة 4 – حفظ دفتر العمل كملف XLSX (الكلمة المفتاحية الثانوية مضمونة)

الآن بعد أن أصبحت البيانات جاهزة، نكتب دفتر العمل إلى القرص. طريقة `Save` تكتشف تنسيق الملف تلقائيًا من الامتداد.

```csharp
        // Step 4: (Optional) Save the workbook to inspect the result
        string outputPath = @"C:\Temp\output.xlsx";   // adjust folder as needed
        workbook.Save(outputPath);                    // creates a .xlsx file on disk
        System.Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

عند فتح `output.xlsx` سترى المصفوفة مرتبة تمامًا كما هو موضح أعلاه. لا خطوات إضافية مطلوبة.

![مثال على إنشاء دفتر عمل Excel](/images/create-excel-workbook.png)

*نص بديل للصورة: “مثال على إنشاء دفتر عمل Excel يُظهر المصفوفة التي تم إنشاؤها بواسطة WRAPCOLS”*

## إضافي: تحويل مصفوفات أكبر – حالات استخدام واقعية

تخيل أنك تستقبل قائمة JSON مسطحة مكوّنة من 100 رقم من API وتحتاجها في جدول مكوّن من 10 أعمدة. يمكنك إعادة استخدام نفس النمط:

```csharp
int[] numbers = Enumerable.Range(1, 100).ToArray();
string arrayLiteral = "{" + string.Join(",", numbers) + "}";
ws.Cells["A1"].Formula = $"=WRAPCOLS({arrayLiteral},10)";
workbook.Calculate();
```

**حالات الحافة التي يجب الانتباه إليها**

- **عدد أعمدة كبير جدًا:** Excel يحد عدد الأعمدة إلى 16,384. إذا طلبت من WRAPCOLS أكثر من ذلك، ستعود الدالة بخطأ `#VALUE!`.
- **بيانات غير رقمية:** WRAPCOLS تعمل مع النص أيضًا، لكن يجب إحاطة السلاسل المزدوجة بعلامات اقتباس داخل المصفوفة (مثال: `{"Apple","Banana","Cherry"}`).
- **الأداء:** بالنسبة للمصفوفات الضخمة جدًا، قد يصبح بناء سلسلة المصفوفة عنق زجاجة. في هذه الحالات، فكر في كتابة القيم مباشرة إلى الخلايا بدلاً من استخدام صيغة.

## أسئلة شائعة (FAQ)

**هل يعمل هذا مع إصدارات Excel القديمة؟**  
نعم. تم تقديم `WRAPCOLS` في Excel 365 وExcel 2019، لكن Aspose.Cells يمكنه محاكاة ذلك للملفات القديمة (مثل `.xls`). سيظل الملف يفتح، رغم أن الصيغة قد تظهر كنص عادي إذا لم يدعم العارضها.

**ماذا لو أردت الاحتفاظ بالصيفة لتحديثات لاحقة؟**  
ما عليك سوى حذف `workbook.Calculate()`. سيحتفظ الملف المحفوظ بصيغة `WRAPCOLS`، مما يسمح للمستخدمين النهائيين بتحرير المصفوفة المصدرية ومشاهدة تحديث المصفوفة تلقائيًا.

**هل يمكنني تطبيق تنسيق بعد ظهور المصفوفة؟**  
بالطبع. بعد `Calculate()`، يمكنك الوصول إلى النطاق المملوء (`A1:B2` في المثال) وتطبيق خطوط، حدود، أو تنسيقات رقمية كأي نطاق خلايا آخر.

## مثال كامل جاهز للتنفيذ – نسخ‑لصق

فيما يلي البرنامج الكامل الذي يمكنك وضعه في تطبيق Console وتشغيله فورًا (تأكد فقط من إضافة حزمة Aspose.Cells عبر NuGet).

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet ws = workbook.Worksheets[0];

        // 2️⃣ Insert WRAPCOLS formula to convert a 1‑D array into a 2‑column matrix
        ws.Cells["A1"].Formula = "=WRAPCOLS({1,2,3,4},2)";

        // 3️⃣ Force calculation so the result is materialized
        workbook.Calculate();

        // 4️⃣ Save the workbook as XLSX
        string outputPath = @"C:\Temp\output.xlsx";
        workbook.Save(outputPath);
        Console.WriteLine($"✅ Workbook created and saved to {outputPath}");
    }
}
```

**الناتج المتوقع:**  
- ملف `output.xlsx` موجود في `C:\Temp\`.  
- خلايا `A1:B2` مملوءة بـ `1, 2, 3, 4` مرتبة في عمودين.  
- لا صيغ متبقية إذا استدعيت `Calculate()`؛ وإلا ستظل الصيغة مرئية.

## الخطوات التالية – توسيع الحل

الآن بعد أن عرفت **كيفية استخدام WRAPCOLS**، يمكنك استكشاف:

1. **عدد أعمدة ديناميكي** – احسب عدد الأعمدة بناءً على حجم البيانات (`Math.Ceiling(array.Length / desiredRows)`).
2. **أوراق عمل متعددة** – كرر النمط على أوراق مختلفة لإنشاء تقرير متعدد التبويبات.
3. **أتمتة التنسيق** – طبّق أنماط جداول، تنسيق شرطي، أو مخططات على المصفوفة المولدة.
4. **تصدير إلى صيغ أخرى** – يمكن لـ Aspose.Cells أيضًا حفظ كـ CSV، PDF، أو حتى HTML إذا احتجت مشاركة البيانات خارج Excel.

هذه الإضافات تحافظ على الفكرة الأساسية—**إنشاء دفتر عمل Excel**، **تحويل المصفوفة إلى مصفوفة**، **فرض حساب دفتر العمل**، و **حفظ دفتر العمل كملف XLSX**—مع إضافة لمسة عملية.

---

**الخلاصة:** لديك الآن طريقة مختصرة وعملية لإنشاء ملف Excel، إعادة تشكيل البيانات المسطحة باستخدام `WRAPCOLS`، التأكد من حساب القيم، وكتابة النتيجة إلى القرص. احصل على الشيفرة، عدّل المصفوفة، ودع مهمة تصدير البيانات التالية تكون سهلة للغاية. Happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}