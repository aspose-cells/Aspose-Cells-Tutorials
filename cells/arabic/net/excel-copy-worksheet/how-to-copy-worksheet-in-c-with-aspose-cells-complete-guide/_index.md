---
category: general
date: 2026-03-30
description: كيفية نسخ ورقة العمل في C# باستخدام Aspose.Cells – دليل خطوة بخطوة يغطي
  نسخ نطاق الخلايا، نسخ الأعمدة بين الأوراق، نسخ جدول محوري لورقة العمل وإضافة كود
  ورقة عمل جديدة.
draft: false
keywords:
- how to copy worksheet
- copy cell range
- copy columns between sheets
- copy worksheet pivot table
- add new worksheet code
language: ar
og_description: تعلم كيفية نسخ ورقة العمل في C# باستخدام Aspose.Cells. يوضح هذا الدليل
  نسخ نطاق الخلايا، الحفاظ على جداول Pivot، نسخ الأعمدة بين الأوراق، وإضافة كود ورقة
  عمل جديدة.
og_title: كيفية نسخ ورقة العمل في C# – دليل Aspose.Cells الكامل
tags:
- Aspose.Cells
- C#
- Excel Automation
title: كيفية نسخ ورقة العمل في C# باستخدام Aspose.Cells – دليل كامل
url: /ar/net/excel-copy-worksheet/how-to-copy-worksheet-in-c-with-aspose-cells-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية نسخ ورقة العمل في C# باستخدام Aspose.Cells – دليل كامل

هل تساءلت يومًا **how to copy worksheet** في C# دون فقدان أي جدول محوري أو صيغة؟ لست وحدك—العديد من المطورين يواجهون صعوبة عندما يحتاجون إلى تكرار ورقة مع الحفاظ على جميع العناصر intact. في هذا الدرس سنستعرض حلًا عمليًا من البداية إلى النهاية لا ينسخ البيانات فحسب بل يحافظ أيضًا على **copy worksheet pivot table**، ويتعامل مع **copy cell range**، ويظهر لك **add new worksheet code** التي ستحتاجها.

سنغطي كل شيء من تحميل دفتر العمل المصدر إلى حفظ ملف الوجهة، بحيث يمكنك **copy columns between sheets**، والحفاظ على الكائنات، والحفاظ على نظافة الكود الخاص بك. لا مراجع غامضة، فقط مثال كامل قابل للتنفيذ يمكنك إدراجه في مشروعك اليوم.

## ما يغطيه هذا الدرس

- تحميل ملف Excel موجود باستخدام Aspose.Cells  
- استخدام **add new worksheet code** لإنشاء ورقة هدف  
- تعريف **copy cell range** التي تشمل جدولًا محوريًا  
- إعداد **CopyOptions** للحفاظ على المخططات والصيغ والجداول المحورية دون تغيير  
- تنفيذ **copy columns between sheets** بدقة على مستوى الصفوف  
- حفظ النتيجة والتحقق من أن ورقة العمل تم نسخها بشكل صحيح  

بنهاية هذا الدليل ستتمكن من الإجابة على سؤال “how to copy worksheet” بثقة، سواء كنت تقوم بأتمتة التقارير أو بناء واجهة مستخدم تعتمد على جداول البيانات.

## كيفية نسخ ورقة العمل – نظرة عامة

قبل أن نغوص في الكود، دعنا نحدد التدفق عالي المستوى. فكر فيه كالوصفة:

1. **Load** دفتر العمل المصدر (`Source.xlsx`).  
2. **Add** ورقة عمل جديدة لتحتوي النسخة (`add new worksheet code`).  
3. **Define** المنطقة التي تريد تكرارها (`copy cell range`).  
4. **Configure** خيارات النسخ بحيث يبقى الجدول المحوري (`copy worksheet pivot table`).  
5. **Copy** الصفوف والأعمدة (`copy columns between sheets`).  
6. **Save** دفتر العمل الجديد (`Destination.xlsx`).  

هذا كل شيء—ست خطوات، لا سحر. كل خطوة مشروحة أدناه مع مقتطفات الكود والمنطق وراءها.

## الخطوة 1 – تحميل دفتر العمل المصدر

أولًا وقبل كل شيء: تحتاج إلى كائن `Workbook` يشير إلى الملف الذي تريد نسخه. هذه الخطوة أساسية لأن Aspose.Cells يعمل مباشرة مع نظام الملفات، وليس مع واجهة Office.

```csharp
using Aspose.Cells;

// Path to the original file
string sourcePath = "YOUR_DIRECTORY/Source.xlsx";
string destinationPath = "YOUR_DIRECTORY/Destination.xlsx";

// Load the workbook – this is the starting point for how to copy worksheet
Workbook workbook = new Workbook(sourcePath);
```

*لماذا هذا مهم:* تحميل الملف ينشئ تمثيلًا في الذاكرة لكل ورقة، خلية، وكائن. بدون ذلك، لا شيء لنسخه، وأي محاولة لـ `add new worksheet code` لاحقًا ستفشل لأن بيانات المصدر غير موجودة.

## الخطوة 2 – إضافة ورقة عمل جديدة (add new worksheet code)

الآن نحتاج إلى مكان للصق البيانات المنسوخة. هنا يتألق **add new worksheet code**. يمكنك تسمية الورقة بأي اسم تريده؛ هنا نسميها `"Copy"`.

```csharp
// Grab the first worksheet (the one we want to copy)
Worksheet sourceSheet = workbook.Worksheets[0];

// Add a fresh worksheet to receive the copy
Worksheet copySheet = workbook.Worksheets.Add("Copy");
```

*نصيحة محترف:* إذا كنت تخطط لنسخ عدة أوراق، استدعِ `Worksheets.Add` داخل حلقة وأعط كل ورقة اسمًا فريدًا. بهذه الطريقة تتجنب تصادم الأسماء وتحافظ على تنظيم دفتر العمل.

## الخطوة 3 – تعريف نطاق الخلايا للنسخ

**copy cell range** يخبر Aspose.Cells بالضبط أي صفوف وأعمدة يجب تكرارها. في العديد من السيناريوهات الواقعية يتضمن النطاق جدولًا محوريًا، لذا يجب أن نكون دقيقين.

```csharp
// Define the area that contains the pivot table (A1:G20)
CellArea sourceRange = new CellArea
{
    StartRow = 0,      // Row 1 (zero‑based)
    StartColumn = 0,   // Column A
    EndRow = 19,       // Row 20
    EndColumn = 6      // Column G
};

// Destination range – we start at the same top‑left corner
CellArea destinationRange = new CellArea
{
    StartRow = 0,
    StartColumn = 0,
    EndRow = 19,
    EndColumn = 6
};
```

*لماذا نحتاج هذا:* بتحديد النطاق صراحةً، تتجنب نسخ الورقة بأكملها (وهو ما قد يكون مهدراً) وتضمن أن الجدول المحوري يبقى داخل المنطقة المنسوخة. هذا هو جوهر **how to copy worksheet** عندما تحتاج فقط جزءًا من الورقة.

## الخطوة 4 – ضبط خيارات النسخ (preserve copy worksheet pivot table)

Aspose.Cells توفر كائن `CopyOptions` الذي يتحكم فيما يتم لصقه. للحفاظ على الجدول المحوري، المخططات، والصيغ، نقوم بتعيين `PasteType.All` وتفعيل `PasteSpecial`.

```csharp
CopyOptions copyOptions = new CopyOptions
{
    PasteType = PasteType.All,   // Copy everything: values, formats, objects
    PasteSpecial = true          // Enable special paste to retain pivot tables
};
```

*شرح:* `PasteType.All` هو الخيار الأكثر شمولاً، بينما `PasteSpecial` يطلب من المحرك معالجة الكائنات المعقدة—مثل الجداول المحورية—بشكل صحيح. تخطي هذه الخطوة هو خطأ شائع؛ سيفقد الورقة المنسوخة ميزاتها التفاعلية.

## الخطوة 5 – نسخ الصفوف والأعمدة (copy columns between sheets)

الآن يأتي الجزء الصعب: نقل البيانات فعليًا. سنستخدم `CopyRows` و `CopyColumns` للتعامل مع **copy columns between sheets**. تنفيذ كلاهما يضمن الحفاظ على الخلايا المدمجة وعرض الأعمدة.

```csharp
// Copy rows from the source to the destination sheet
sourceSheet.Cells.CopyRows(
    sourceRange.StartRow,
    sourceRange.EndRow,
    copySheet.Cells,
    destinationRange.StartRow,
    copyOptions);

// Copy columns from the source to the destination sheet
sourceSheet.Cells.CopyColumns(
    sourceRange.StartColumn,
    sourceRange.EndColumn,
    copySheet.Cells,
    destinationRange.StartColumn,
    copyOptions);
```

*ما يحدث:* `CopyRows` ينقل البيانات صفًا بصف، بينما `CopyColumns` يفعل ذلك عمودًا بعمود. تشغيل كلاهما يضمن تكرار الكتلة المستطيلة بالكامل، وهو أمر أساسي عندما تحتاج إلى **copy columns between sheets** التي لها أعمدة بعرض مختلف أو أعمدة مخفية.

## الخطوة 6 – حفظ دفتر العمل

أخيرًا، اكتب التغييرات إلى القرص. هذه الخطوة تكمل عملية **how to copy worksheet**.

```csharp
// Save the workbook with the newly copied sheet
workbook.Save(destinationPath);
```

*نصيحة للتحقق:* افتح `Destination.xlsx` وتأكد أن ورقة `"Copy"` تبدو مطابقة للأصل، الجداول المحورية تعمل، وعرض الأعمدة متطابق. إذا لاحظت أي اختلاف، راجع إعدادات `CopyOptions`.

## الحالات الخاصة والاختلافات الشائعة

### نسخ عدة أوراق عمل

إذا كنت بحاجة لتكرار عدة أوراق، ضع المنطق السابق داخل حلقة `foreach`:

```csharp
foreach (Worksheet ws in workbook.Worksheets)
{
    Worksheet newWs = workbook.Worksheets.Add(ws.Name + "_Copy");
    // Re‑use sourceRange/destinationRange or calculate per sheet
    // Then call CopyRows/CopyColumns as shown earlier
}
```

### الحفاظ على الصيغ عبر دفاتر عمل مختلفة

عندما تكون دفاتر العمل المصدر والوجهة لديها نطاقات مسماة مختلفة، اضبط `copyOptions` إلى `PasteType.Formulas` بالإضافة إلى `All`:

```csharp
copyOptions.PasteType = PasteType.All | PasteType.Formulas;
```

### النطاقات الكبيرة والأداء

للمجموعات الضخمة من البيانات (مئات الآلاف من الصفوف)، فكر في استخدام `CopyRows` فقط وتخطي `CopyColumns` إذا لم يكن عرض الأعمدة مهمًا. هذا يمكن أن يوفر بضع ثوانٍ.

## مثال كامل يعمل

فيما يلي البرنامج الكامل الجاهز للتنفيذ الذي يجسد كل ما ناقشنا. الصقه في تطبيق كونسول، عدل مسارات الملفات، واضغط **F5**.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // ---------- Step 1: Load the source workbook ----------
        string sourcePath = "YOUR_DIRECTORY/Source.xlsx";
        string destinationPath = "YOUR_DIRECTORY/Destination.xlsx";
        Workbook workbook = new Workbook(sourcePath);

        // ---------- Step 2: Add a new worksheet (add new worksheet code) ----------
        Worksheet sourceSheet = workbook.Worksheets[0];
        Worksheet copySheet = workbook.Worksheets.Add("Copy");

        // ---------- Step 3: Define the copy cell range ----------
        CellArea sourceRange = new CellArea
        {
            StartRow = 0,
            StartColumn = 0,
            EndRow = 19,
            EndColumn = 6
        };
        CellArea destinationRange = new CellArea
        {
            StartRow = 0,
            StartColumn = 0,
            EndRow = 19,
            EndColumn = 6
        };

        // ---------- Step 4: Set copy options (preserve copy worksheet pivot table) ----------
        CopyOptions copyOptions = new CopyOptions
        {
            PasteType = PasteType.All,
            PasteSpecial = true
        };

        // ---------- Step 5: Copy rows and columns (copy columns between sheets) ----------
        sourceSheet.Cells.CopyRows(
            sourceRange.StartRow,
            sourceRange.EndRow,
            copySheet.Cells,
            destinationRange.StartRow,
            copyOptions);

        sourceSheet.Cells.CopyColumns(
            sourceRange.StartColumn,
            sourceRange.EndColumn,
            copySheet.Cells,
            destinationRange.StartColumn,
            copyOptions);

        // ---------- Step 6: Save the workbook ----------
        workbook.Save(destinationPath);
    }
}
```

**النتيجة المتوقعة:** فتح `Destination.xlsx` يظهر ورقة باسم **Copy** تعكس الورقة الأولى من `Source.xlsx`—بما في ذلك أي جداول محورية، تنسيقات، وعرض الأعمدة. الملف الأصلي يبقى دون تغيير.

## الأسئلة المتكررة

**س: هل يعمل هذا مع ملفات .xlsx التي تم إنشاؤها بواسطة Excel 2019؟**  
ج: بالتأكيد. Aspose.Cells يدعم جميع صيغ Excel الحديثة، لذا يعمل نفس الكود مع ملفات `.xlsx`، `.xlsm`، وحتى ملفات `.xls` القديمة

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}