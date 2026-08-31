---
category: general
date: 2026-02-21
description: تعلم كيفية تنسيق الأعمدة عند استيراد DataTable إلى Excel باستخدام C#.
  يتضمن نصائح لتلوين العمود الثاني في Excel واستيراد DataTable إلى Excel باستخدام
  C#.
draft: false
keywords:
- how to style columns
- import datatable to excel
- how to import datatable
- color second column excel
- import datatable excel c#
language: ar
og_description: كيفية تنسيق الأعمدة عند استيراد DataTable إلى Excel باستخدام C#. كود
  خطوة بخطوة، تلوين العمود الثاني في Excel، وأفضل الممارسات.
og_title: كيفية تنسيق الأعمدة في إكسل باستخدام C# – دليل شامل
tags:
- C#
- Excel
- DataTable
- Aspose.Cells
title: كيفية تنسيق الأعمدة في Excel باستخدام C# – استيراد DataTable
url: /ar/net/excel-formatting-and-styling/how-to-style-columns-in-excel-with-c-import-datatable/
---

for any markdown links: none.

Check for any images: none.

Check for any code blocks: placeholders only.

Make sure to keep bold formatting (**text**) and inline code backticks.

Now produce final answer.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تنسيق الأعمدة في Excel باستخدام C# – استيراد DataTable

هل تساءلت يومًا **كيف تنسق الأعمدة** في ورقة عمل Excel أثناء سحب البيانات مباشرة من `DataTable`؟ لست الوحيد. يواجه العديد من المطورين صعوبة عندما يحتاجون إلى لمسة سريعة من اللون—ربما أحمر للعمود الأول، أزرق للثاني—دون تعديل كل خلية يدويًا بعد الاستيراد.  

الأخبار السارة؟ الجواب هو بضع أسطر من كود C#، وستحصل على ورقة مُنسقة بالكامل بمجرد وصول البيانات. في هذا الدرس سنغطي أيضًا **import datatable to excel**، ونظهر لك **color second column excel**، ونشرح لماذا تعمل الطريقة لكل من .NET Framework و .NET 6+.

---

## ما ستتعلمه

- استرجاع `DataTable` مُعبأ (أو إنشاؤه في الوقت الفعلي).  
- تعريف كائنات `Style` لكل عمود لتعيين ألوان النص.  
- إنشاء مصنف (workbook)، الحصول على ورقة العمل الأولى، واستيراد الجدول مع تطبيق الأنماط.  
- معالجة الحالات الخاصة مثل الجداول الفارغة، صفوف البداية المخصصة، وعدد الأعمدة الديناميكي.  

بنهاية الدرس، ستكون قادرًا على وضع ملف Excel مُنسق في أي خط أنابيب تقارير—دون الحاجة إلى معالجة لاحقة.

> **المتطلبات المسبقة:** إلمام أساسي بـ C# وإشارة إلى مكتبة جداول بيانات تدعم `ImportDataTable` (مثل Aspose.Cells، GemBox.Spreadsheet، أو EPPlus مع أداة مساعدة). الكود أدناه يستخدم **Aspose.Cells** لأن نسخة `ImportDataTable` الخاصة به تقبل مباشرةً `Style[]`.

## الخطوة 1: إعداد المشروع وإضافة مكتبة Excel

قبل أن نتمكن من تنسيق أي شيء، نحتاج إلى مشروع ي引用 مكتبة معالجة Excel.

```csharp
// Install-Package Aspose.Cells -Version 24.7
using Aspose.Cells;
using System;
using System.Data;
using System.Drawing;   // For Color
```

*نصيحة احترافية:* إذا كنت تستخدم .NET 6، أضف الحزمة عبر `dotnet add package Aspose.Cells`. المكتبة تعمل على Windows و Linux و macOS، لذا أنت مستقبليًا.

---

## الخطوة 2: استرجاع أو إنشاء DataTable المصدر

تركز جوهر الدرس على التنسيق، لكنك لا تزال بحاجة إلى `DataTable`. أدناه أداة مساعدة سريعة تنشئ بيانات عينة؛ استبدلها بنداء `GetTable()` الخاص بك في الإنتاج.

```csharp
/// <summary>
/// Returns a DataTable with three columns and five rows of demo data.
/// </summary>
static DataTable GetTable()
{
    var dt = new DataTable("Demo");
    dt.Columns.Add("ID", typeof(int));
    dt.Columns.Add("Name", typeof(string));
    dt.Columns.Add("Score", typeof(double));

    dt.Rows.Add(1, "Alice", 92.5);
    dt.Rows.Add(2, "Bob", 85.3);
    dt.Rows.Add(3, "Charlie", 78.9);
    dt.Rows.Add(4, "Diana", 88.1);
    dt.Rows.Add(5, "Ethan", 91.4);

    return dt;
}
```

> **لماذا هذا مهم:** استخدام `DataTable` يبقي مصدر البيانات غير محدد—سواء جاء من SQL أو CSV أو مجموعة في الذاكرة، يظل منطق الاستيراد هو نفسه. هذا هو أساس **how to import datatable** بفعالية.

## الخطوة 3: تعريف أنماط الأعمدة (جوهر “How to Style Columns”)

الآن نخبر ورقة العمل كيف يجب أن يبدو كل عمود. تسمح لك فئة `Style` بتعيين الخطوط، الألوان، الحدود، وأكثر. في هذا المثال نغير فقط لون النص.

```csharp
// Step 3: Define column styles – red for first, blue for second, default for others
Style[] columnStyles = new Style[3]; // Assuming three columns; adjust as needed

// Style for column 0 (first column) – red text
columnStyles[0] = new Style();
columnStyles[0].ForegroundColor = Color.Red;

// Style for column 1 (second column) – blue text
columnStyles[1] = new Style();
columnStyles[1].ForegroundColor = Color.Blue;

// Column 2 (third column) – keep default styling
columnStyles[2] = new Style(); // No changes, but array entry required
```

*ماذا لو كان لديك المزيد من الأعمدة؟* فقط قم بزيادة حجم المصفوفة واملأ الأنماط التي تهمك. الأعمدة غير المنسقة ترث تلقائيًا النمط الافتراضي لورقة العمل.

## الخطوة 4: إنشاء المصنف واستيراد DataTable مع الأنماط

مع وجود البيانات والأنماط جاهزة، حان الوقت لتجميع كل شيء.

```csharp
static void Main()
{
    // Retrieve the data
    DataTable dataTable = GetTable();

    // Initialize a new workbook (in‑memory)
    Workbook workbook = new Workbook();

    // Grab the first worksheet (index 0)
    Worksheet worksheet = workbook.Worksheets[0];

    // Import the DataTable starting at cell A1 (row 0, column 0)
    // The 'true' flag tells Aspose.Cells to include column headers
    worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);

    // Optional: Auto‑fit columns for a cleaner look
    worksheet.AutoFitColumns();

    // Save the result to disk
    string outputPath = "StyledDataTable.xlsx";
    workbook.Save(outputPath);

    Console.WriteLine($"Excel file saved to {outputPath}");
}
```

**ماذا حدث للتو؟**  
- `ImportDataTable` ينسخ الصفوف، الأعمدة، و*اختياريًا* صف العنوان.  
- بتمرير `columnStyles`، يحصل كل عمود على الـ `Style` الذي عرفناه مسبقًا.  
- الاستدعاء سطر واحد، مما يعني أن **import datatable excel c#** بسيط جدًا.

## الخطوة 5: التحقق من النتيجة – النتيجة المتوقعة

افتح `StyledDataTable.xlsx` في Excel (أو LibreOffice). يجب أن ترى:

| **ID** (أحمر) | **Name** (أزرق) | **Score** (افتراضي) |
|--------------|-----------------|----------------------|
| 1            | Alice           | 92.5                 |
| 2            | Bob             | 85.3                 |
| …            | …               | …                    |

- يظهر نص العمود الأول باللون **أحمر**، مما يلبي متطلب “how to style columns”.  
- نص العمود الثاني باللون **أزرق**، وهو أيضًا يجيب على استعلام **color second column excel**.

إذا فتح الملف دون أخطاء، فقد أتقنت بنجاح **how to import datatable** مع تنسيق الأعمدة.

## أسئلة شائعة وحالات خاصة

### ماذا لو كان DataTable فارغًا؟
`ImportDataTable` سيظل ينشئ صف العنوان (إذا مررت `true`). لا تُضاف صفوف بيانات، لكن الأنماط لا تزال تُطبق على خلايا العنوان.

### هل تحتاج إلى بدء الاستيراد من خلية مختلفة؟
غيّر معلمات `rowIndex` و `columnIndex` في `ImportDataTable`. على سبيل المثال، للبدء من `B2` استخدم `1, 1` بدلاً من `0, 0`.

### هل ترغب في تنسيق الصفوف بدلاً من الأعمدة؟
يمكنك التكرار عبر `worksheet.Cells.Rows` بعد الاستيراد وتعيين `Style` لكل صف. ومع ذلك، تنسيق الأعمدة أكثر كفاءة لأن المكتبة تطبق النمط مرة واحدة لكل عمود.

### هل تستخدم EPPlus أو ClosedXML؟
هذه المكتبات لا توفر نسخة مباشرة من `ImportDataTable` مع مصفوفة أنماط. الحل هو استيراد الجدول أولاً، ثم التكرار عبر نطاق الأعمدة وتعيين `Style.Font.Color.SetColor(...)`. يبقى المنطق هو نفسه، مع بضع أسطر إضافية.

## نصائح احترافية لكود جاهز للإنتاج

- **إعادة استخدام الأنماط:** إنشاء `Style` جديد لكل عمود قد يكون مهدراً. احفظ الأنماط القابلة لإعادة الاستخدام في قاموس مفتاحه اللون أو وزن الخط.  
- **تجنب عدد الأعمدة المرمّز صراحةً:** اكتشف `dataTable.Columns.Count` وابدأ مصفوفة `columnStyles` ديناميكياً.  
- **سلامة الخيوط:** إذا كنت تولد العديد من المصنفات بشكل متوازي، أنشئ `Workbook` منفصل لكل خيط؛ كائنات Aspose.Cells ليست آمنة للخيوط.  
- **الأداء:** للجداول التي تتجاوز 10 k صف، فكر في تعطيل `AutoFitColumns` (يقوم بمسح كل خلية) وتعيين عرض الأعمدة يدويًا.

## مثال كامل يعمل (جاهز للنسخ واللصق)

```csharp
// ------------------------------------------------------------
// Full example: How to style columns while importing a DataTable
// ------------------------------------------------------------
using Aspose.Cells;
using System;
using System.Data;
using System.Drawing;

class Program
{
    static void Main()
    {
        // 1️⃣ Retrieve data
        DataTable dataTable = GetTable();

        // 2️⃣ Define per‑column styles
        int colCount = dataTable.Columns.Count;
        Style[] columnStyles = new Style[colCount];

        // Red for first column
        columnStyles[0] = new Style { ForegroundColor = Color.Red };

        // Blue for second column (if it exists)
        if (colCount > 1)
            columnStyles[1] = new Style { ForegroundColor = Color.Blue };

        // Default style for remaining columns
        for (int i = 2; i < colCount; i++)
            columnStyles[i] = new Style(); // no special formatting

        // 3️⃣ Create workbook and import with styles
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.Worksheets[0];
        sheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);
        sheet.AutoFitColumns();

        // 4️⃣ Save to file
        string path = "StyledDataTable.xlsx";
        workbook.Save(path);
        Console.WriteLine($"File saved: {path}");
    }

    // Helper: sample DataTable
    static DataTable GetTable()
    {
        var dt = new DataTable("Demo");
        dt.Columns.Add("ID", typeof(int));
        dt.Columns.Add("Name", typeof(string));
        dt.Columns.Add("Score", typeof(double));

        dt.Rows.Add(1, "Alice", 92.5);
        dt.Rows.Add(2, "Bob", 85.3);
        dt.Rows.Add(3, "Charlie", 78.9);
        dt.Rows.Add(4, "Diana", 88.1);
        dt.Rows.Add(5, "Ethan", 91.4);
        return dt;
    }
}
```

شغّل البرنامج، افتح الملف `StyledDataTable.xlsx` المُولد، وسترى الأعمدة الملونة فورًا. هذا هو سير عمل **import datatable excel c#** بالكامل باختصار.

## الخلاصة

لقد غطينا للتو **how to style columns** عندما **import datatable to excel** باستخدام C#. من خلال تعريف مصفوفة `Style[]` وتمريرها إلى `ImportDataTable`، يمكنك تلوين العمود الأول بالأحمر، والعمود الثاني بالأزرق، وترك البقية دون تعديل—كل ذلك في سطر واحد من الكود.  

الطريقة قابلة للتوسع: أضف المزيد من كائنات `Style` لأعمدة إضافية، عدّل صفوف البداية، أو استبدل Aspose.Cells بمكتبة أخرى ذات واجهة مشابهة. الآن يمكنك إنشاء تقارير Excel مصقولة دون الحاجة إلى تعديل الملف يدويًا.

**الخطوات التالية** التي قد تستكشفها:

- استخدام **conditional formatting** لتسليط الضوء على القيم ديناميكيًا (يرتبط بـ “color second column excel”).  
- تصدير أوراق عمل متعددة من مجموعة `DataTable` واحدة (مفيد للوحة التحكم الشهرية).  
- دمج ذلك مع تحويل **CSV → DataTable** لبناء عملية من‑إلى‑

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}