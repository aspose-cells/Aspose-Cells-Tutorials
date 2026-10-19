---
category: general
date: 2026-10-10
description: إنشاء مصنف Excel باستخدام C# واستخدام الدالة WRAPCOLS لتقسيم بيانات المصفوفة
  إلى أعمدة. اتبع دليلًا كاملاً خطوة بخطوة مع كود قابل للتنفيذ.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook
- excel formula split data
- use wrapcols function
- how to use wrapcols
- split array columns
language: ar
lastmod: 2026-10-10
og_description: إنشاء مصنف Excel باستخدام C# وتطبيق دالة WRAPCOLS لتقسيم بيانات المصفوفة
  إلى أعمدة. يوضح هذا الدليل الشيفرة الكاملة ويشرح كل خطوة.
og_image_alt: Screenshot of an Excel sheet showing three columns filled by the WRAPCOLS
  formula
og_title: إنشاء مصنف إكسل وتقسيم البيانات باستخدام WRAPCOLS في C#
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: Create Excel workbook in C# and use the WRAPCOLS function to split
    array data into columns. Follow a complete step‑by‑step guide with runnable code.
  headline: How to create Excel workbook and split data with WRAPCOLS in C#
  type: TechArticle
- description: Create Excel workbook in C# and use the WRAPCOLS function to split
    array data into columns. Follow a complete step‑by‑step guide with runnable code.
  name: How to create Excel workbook and split data with WRAPCOLS in C#
  steps:
  - name: Using the function with different data types
    text: 'The `WRAPCOLS` function is not limited to numbers. You can split text values,
      dates, or mixed types:'
  - name: Variable column count at runtime
    text: 'Often the number of columns you need depends on user input. You can build
      the formula string dynamically:'
  - name: Large arrays and performance
    text: '`WRAPCOLS` can handle thousands of elements, but evaluating extremely large
      arrays in a single cell may increase calculation time. If you notice slowdown:'
  - name: Handling empty cells
    text: If the source array contains empty strings (`""`) or `NULL` values, `WRAPCOLS`
      inserts blank cells, preserving the column layout. This behavior is useful when
      you need placeholder columns for later data entry.
  - name: Using named ranges instead of literals
    text: 'For maintainability, define a named range that holds the source data, then
      reference it:'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: كيفية إنشاء مصنف إكسل وتقسيم البيانات باستخدام WRAPCOLS في C#
url: /ar/net/excel-formulas-and-calculation-options/how-to-create-excel-workbook-and-split-data-with-wrapcols-in/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية إنشاء مصنف Excel وتقسيم البيانات باستخدام WRAPCOLS في C#

إذا كنت بحاجة إلى **إنشاء مصنف Excel** برمجياً، يوضح لك هذا الدليل بالضبط كيفية القيام بذلك وكيفية **تقسيم بيانات المصفوفة** عبر الأعمدة باستخدام الدالة `WRAPCOLS`. ستحصل على مثال كامل قابل للتنفيذ ينتج ملف `.xlsx` مع توزيع البيانات على ثلاثة أعمدة.

يغطي الدرس كل ما تحتاجه: حزم NuGet المطلوبة، كل سطر من الشيفرة، لماذا تعمل صيغة `WRAPCOLS`، وكيفية تعديل الحل لأحجام مصفوفات أو عدد أعمدة مختلفة. في النهاية ستتمكن من دمج تقنية **استخدام دالة wrapcols** في أي مشروع C# يولد ملفات Excel.

## المتطلبات المسبقة

قبل أن تبدأ، تأكد من وجود ما يلي:

* .NET 6.0 SDK أو أحدث مثبت  
* بيئة تطوير C# (Visual Studio، VS Code، Rider، إلخ)  
* حزمة **Aspose.Cells for .NET** من NuGet – المكتبة التي توفر الفئة `Workbook` المستخدمة في الأمثلة  

لا تحتاج إلى تثبيت Office؛ فـ Aspose.Cells يكتب ملف `.xlsx` مباشرة.

## الخطوة 1 – إنشاء مصنف Excel

المهمة الأولى هي إنشاء كائن مصنف جديد والحصول على مرجع إلى ورقة العمل الأولى. هذه الخطوة هي الأساس لأي تعديل لاحق.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Create a new workbook and get the first worksheet
        Workbook wb = new Workbook();                // creates an empty Excel file in memory
        Worksheet ws = wb.Worksheets[0];             // the default worksheet is at index 0
```

`Workbook` تمثل الملف بالكامل، بينما `Worksheet` تمثل ورقة واحدة. بإنشاء المصنف في الذاكرة تتجنب عمليات الإدخال/الإخراج على القرص حتى تقوم بحفظه صراحةً.

## الخطوة 2 – تطبيق WRAPCOLS لتقسيم أعمدة المصفوفة

الآن ستضع صيغة في الخلية **A1** تستخدم `WRAPCOLS`. تستقبل الدالة معاملين: مصفوفة المصدر وعدد الأعمدة التي تريد أن تُلف المصفوفة إليها.

```csharp
        // Step 2: Apply the WRAPCOLS formula to split the array into 3 columns
        // The array {1,2,3,4,5,6} will be distributed as:
        // 1 2 3
        // 4 5 6
        ws.Cells[0, 0].Formula = "=WRAPCOLS({1,2,3,4,5,6},3)";
```

**لماذا يعمل هذا:** `WRAPCOLS` تأخذ المصفوفة المسطحة `{1,2,3,4,5,6}` وتملأ ورقة العمل صفاً بصف، مُنشئة ثلاثة أعمدة لكل صف. يمكن أن يكون المعامل الأول أي مصفوفة Excel حرفية، نطاق مسمى، أو صيغة مصفوفة ديناميكية. المعامل الثاني (`3`) يخبر Excel بكم عدد الأعمدة التي يجب توليدها قبل الانتقال إلى الصف التالي.

### استخدام الدالة مع أنواع بيانات مختلفة

دالة `WRAPCOLS` ليست محصورة بالأرقام. يمكنك تقسيم قيم نصية، تواريخ، أو أنواع مختلطة:

```csharp
        // Example with mixed data: strings and numbers
        ws.Cells[2, 0].Formula = "=WRAPCOLS({\"Jan\",\"Feb\",\"Mar\",100,200,300},3)";
```

عندما تحتوي مصفوفة المصدر على سلاسل نصية، يتعامل Excel تلقائياً مع النتيجة كخلايا نصية. هذه المرونة تتيح لك **تقسيم البيانات باستخدام صيغة Excel** للتقارير، لوحات المعلومات، أو مهام ترحيل البيانات.

## الخطوة 3 – حساب الصيغ لتعبئة ورقة العمل

تُخزن الصيغ كسلاسل نصية حتى تطلب من المصنف تقييمها. استدعاء `CalculateFormula` يجبر على التقييم ويكتب القيم في الخلايا.

```csharp
        // Step 3: Calculate formulas so the worksheet is populated
        wb.CalculateFormula();   // evaluates all formulas in the workbook
```

بدون هذا الاستدعاء سيحتوي الملف المحفوظ على نص الصيغة فقط، وليس القيم المحسوبة. تعمل الطريقة على كامل المصنف، لذا يمكنك وضع صيغ إضافية في أماكن أخرى وسيتم حلها جميعاً بنداء واحد.

## الخطوة 4 – حفظ المصنف لرؤية النتيجة

أخيراً، اكتب المصنف إلى القرص. اختر مجلداً لديك صلاحية كتابة فيه، ومنح الملف اسمًا واضحًا.

```csharp
        // Step 4: Save the workbook to see the result
        string outputPath = @"output.xlsx";
        wb.Save(outputPath);      // creates output.xlsx in the application directory
    }
}
```

عند فتح `output.xlsx` في Excel (أو أي عارض متوافق)، ستظهر لك:

| A | B | C |
|---|---|---|
| 1 | 2 | 3 |
| 4 | 5 | 6 |

إذا استخدمت مثال النوع المختلط، فإن الصفين 3‑4 سيحتويان على النصوص والأرقام وفقًا لذلك.

## تنويعات متقدمة ومعالجة الحالات الطرفية

### عدد أعمدة متغير في وقت التشغيل

غالبًا ما يعتمد عدد الأعمدة الذي تحتاجه على إدخال المستخدم. يمكنك بناء سلسلة الصيغة ديناميكيًا:

```csharp
int columns = 4; // could come from UI, config, etc.
string arrayLiteral = "{10,20,30,40,50,60,70,80}";
ws.Cells[5, 0].Formula = $"=WRAPCOLS({arrayLiteral},{columns})";
```

### مصفوفات كبيرة والأداء

يمكن لـ `WRAPCOLS` معالجة آلاف العناصر، لكن تقييم مصفوفات ضخمة جدًا في خلية واحدة قد يزيد من زمن الحساب. إذا لاحظت بطءً:

* قسم مصفوفة المصدر إلى قطع أصغر واكتب كل قطعة في خلية بدء مختلفة.  
* استخدم `WorkbookSettings` لتمكين الحساب متعدد الخيوط:

```csharp
wb.Settings.CalcMode = CalculationModeType.Automatic;
wb.Settings.EnableMultiThreadedCalc = true;
```

### معالجة الخلايا الفارغة

إذا احتوت مصفوفة المصدر على سلاسل فارغة (`""`) أو قيم `NULL`، فإن `WRAPCOLS` تُدرج خلايا فارغة، محافظًا على تخطيط الأعمدة. هذا السلوك مفيد عندما تحتاج إلى أعمدة نائبة لإدخال بيانات لاحقًا.

### استخدام النطاقات المسماة بدلاً من القيم الحرفية

لتحسين الصيانة، عرّف نطاقًا مسمىً يحمل بيانات المصدر، ثم أشر إليه:

```csharp
ws.Cells["D1:D6"].PutValue(new object[] { 11, 12, 13, 14, 15, 16 });
ws.Cells["E1"].Formula = "=WRAPCOLS(D1:D6,3)";
```

الآن تقرأ الصيغة البيانات من ورقة العمل نفسها، مما يتيح **كيفية استخدام wrapcols** في سيناريوهات التقارير الديناميكية.

## الأخطاء الشائعة ونصائح الخبراء

* **لا تُهمل المعامل الثاني.** `WRAPCOLS(array)` بدون عدد الأعمدة تُعيد عمودًا واحدًا، مما يُفقد الغرض من تقسيم البيانات.  
* **تجنب خلط أبعاد المصفوفة.** يجب أن تكون مصفوفة المصدر أحادية البُعد؛ توفير مصفوفة ثنائية البُعد (مثل `{ {1,2},{3,4} }`) يسبب خطأ `#VALUE!`.  
* **احفظ بعد الحساب.** إذا استدعيت `wb.Save` قبل `CalculateFormula`، سيحتوي الملف على نص الصيغة فقط.  
* **تحقق من أذونات الملف.** عند التشغيل في بيئات مقيدة (مثل ASP.NET)، تأكد من أن هوية العملية يمكنها الكتابة إلى المجلد المستهدف.  

## مثال كامل يعمل

فيما يلي البرنامج الكامل الذي يمكنك نسخه، لصقه، وتشغيله. يتضمن جميع الاستيرادات، معالجة الأخطاء، والتعليقات.

```csharp
using System;
using Aspose.Cells;

class ExcelWrapColsDemo
{
    static void Main()
    {
        // Create a new workbook and get the first worksheet
        Workbook wb = new Workbook();
        Worksheet ws = wb.Worksheets[0];

        // Split a numeric array into 3 columns
        ws.Cells[0, 0].Formula = "=WRAPCOLS({1,2,3,4,5,6},3)";

        // Split a mixed array (text + numbers) into 3 columns, starting at row 3
        ws.Cells[2, 0].Formula = "=WRAPCOLS({\"Jan\",\"Feb\",\"Mar\",100,200,300},3)";

        // Dynamically build a formula with a variable column count
        int columnCount = 4;
        string sourceArray = "{10,20,30,40,50,60,70,80}";
        ws.Cells[5, 0].Formula = $"=WRAPCOLS({sourceArray},{columnCount})";

        // Evaluate all formulas
        wb.CalculateFormula();

        // Save the workbook
        string outputPath = "output.xlsx";
        wb.Save(outputPath);
        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

تشغيل البرنامج ينتج `output.xlsx` مع ثلاث مناطق مميزة تُظهر **تقسيم البيانات باستخدام صيغة Excel** عبر دالة `WRAPCOLS`.

## الخلاصة

أنت الآن تعرف كيف **تنشئ ملفات مصنف Excel** في C# وكيف **تستخدم دالة wrapcols** لت **تقسيم أعمدة المصفوفة** بفعالية. الخطوات الأساسية—إنشاء `Workbook`، إدراج صيغة `WRAPCOLS`، حساب القيم، وحفظ الملف—تشكل نمطًا قابلاً لإعادة الاستخدام لأي مهمة أتمتة تتطلب توزيع البيانات عبر الأعمدة.

من هنا يمكنك:

* دمج `WRAPCOLS` مع دوال مصفوفة ديناميكية أخرى مثل `FILTER` أو `SORT`.  
* تصدير مجموعات بيانات كبيرة من قواعد البيانات وترك Excel يتولى تنسيقها تلقائيًا.  
* بناء تقارير موجهة للمستخدم حيث يتم اختيار عدد الأعمدة عبر عنصر تحكم في الواجهة.

جرّب مصادر مصفوفة مختلفة، عدد أعمدة مختلف، وصيغ إضافية لتوسيع هذا الأساس. برمجة سعيدة!

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة شيفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف نهج تنفيذ بديلة في مشاريعك.

- [How to Use WRAPCOLS in C# – Create Excel Workbook with Wrap Functions](/cells/english/net/formulas-functions/how-to-use-wrapcols-in-c-create-excel-workbook-with-wrap-fun/)
- [Create Excel Workbook – Convert Array to Matrix with WRAPCOLS](/cells/english/net/calculation-engine/create-excel-workbook-convert-array-to-matrix-with-wrapcols/)
- [Create Excel Workbook C# – Step‑by‑Step Guide](/cells/english/net/excel-workbook/create-excel-workbook-c-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}