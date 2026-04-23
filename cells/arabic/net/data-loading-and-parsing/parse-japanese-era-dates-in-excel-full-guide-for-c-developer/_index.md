---
category: general
date: 2026-02-14
description: قم بتحليل تواريخ العصور اليابانية في إكسل باستخدام تحليل مخصص للتواريخ.
  تعلم كيفية تحميل المصنف من ملف باستخدام load excel مع الخيارات وتجنب الأخطاء الشائعة.
draft: false
keywords:
- parse japanese era dates
- load excel with options
- load workbook from file
- custom date parsing excel
language: ar
og_description: تحليل تواريخ العصور اليابانية في Excel باستخدام Aspose.Cells. يوضح
  هذا الدليل كيفية تحميل المصنف من ملف مع خيارات تحليل تاريخ مخصصة.
og_title: تحليل تواريخ العصور اليابانية – دليل C# خطوة بخطوة
tags:
- Aspose.Cells
- C#
- Excel automation
title: تحليل تواريخ العصور اليابانية في إكسل – دليل كامل لمطوري C#
url: /ar/net/data-loading-and-parsing/parse-japanese-era-dates-in-excel-full-guide-for-c-developer/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تحليل تواريخ العصور اليابانية – دليل C# كامل

هل احتجت يومًا إلى **تحليل تواريخ العصور اليابانية** من ورقة Excel وتساءلت لماذا تتحول القيم إلى أرقام غريبة؟ لست وحدك. يواجه العديد من المطورين هذه المشكلة عندما لا يتعرف محلل `DateTime` الافتراضي على النمط “Reiwa 1/04/01” المستخدم في التقويمات اليابانية.  

أخبار سارة: يمكنك إخبار Aspose.Cells بمعالجة تلك الخلايا كتواريخ عصور يابانية منذ لحظة **تحميل Excel مع الخيارات**. في هذا الدليل سنستعرض تحميل مصنف من ملف، ضبط تحليل التاريخ المخصص، والتحقق من أن التواريخ تظهر بالضبط كما تتوقع.

بحلول نهاية هذا الدرس ستتمكن من:

* تحميل مصنف من ملف مع تحديد `DateTimeParsing.JapaneseEra`.
* الوصول إلى قيم الخلايا ككائنات `DateTime` صحيحة.
* التعامل مع الحالات الخاصة مثل الخلايا الفارغة أو التقويمات المختلطة.
* توسيع النهج لأي سيناريو **custom date parsing excel** قد تواجهه.

> **المتطلبات المسبقة** – تحتاج إلى مكتبة Aspose.Cells for .NET (الإصدار 23.9 أو أحدث) وبيئة تطوير متوافقة مع .NET (Visual Studio، Rider، إلخ). لا توجد حزم أخرى مطلوبة.

---

## الخطوة 1: تكوين خيارات تحميل النص لتحليل العصور اليابانية  

أول شيء نفعله هو إخبار المحمل كيف يفسر النص الذي يبدو كتواريخ عصور يابانية. يتم ذلك عبر `TxtLoadOptions` وتعداد `DateTimeParsing`.

```csharp
using Aspose.Cells;

// Step 1: Set up load options to understand Japanese era dates
TxtLoadOptions loadOptions = new TxtLoadOptions
{
    // This flag makes the parser treat “R1/04/01” as 2024‑04‑01, etc.
    DateTimeParsing = DateTimeParsing.JapaneseEra
};
```

**لماذا هذا مهم:** بدون علم `JapaneseEra`، يتعامل Aspose.Cells مع الخلية كسلسلة نصية عادية، مما يجبرك على تقسيم اسم العصر وتحويله يدويًا. العلم يقوم بالعمل الشاق، مما يبقي الكود نظيفًا وأقل عرضة للأخطاء.

---

## الخطوة 2: تحميل المصنف من ملف باستخدام الخيارات  

الآن نفتح ملف Excel فعليًا. لاحظ كيف يتم تمرير كائن `loadOptions` إلى مُنشئ `Workbook`—هذه هي خطوة **load workbook from file** التي تحترم قواعد التحليل المخصصة الخاصة بنا.

```csharp
// Step 2: Load the workbook with the configured options
string filePath = Path.Combine(Environment.CurrentDirectory, "japan_dates.xlsx");
Workbook workbook = new Workbook(filePath, loadOptions);
```

إذا كان الملف موجودًا في موقع آخر (مثلاً مشاركة شبكة)، فقط عدّل `filePath` وفقًا لذلك. الجزء المهم هو أن نفس نسخة `loadOptions` تُستخدم؛ وإلا لن يحدث تحويل العصور اليابانية.

---

## الخطوة 3: الوصول إلى التواريخ التي تم تحليلها  

مع تحميل المصنف، يمكنك سحب قيم الخلايا كما تفعل مع أي تاريخ عادي. تُعيد الـ API تلقائيًا كائن `DateTime`.

```csharp
// Step 3 (optional): Read a date from the first worksheet, cell A1
Worksheet sheet = workbook.Worksheets[0];
Cell dateCell = sheet.Cells["A1"];

// The Value property is already a DateTime because of our parsing option
DateTime parsedDate = dateCell.DateTimeValue;

// Quick sanity check – print to console
Console.WriteLine($"Parsed date from A1: {parsedDate:yyyy-MM-dd}");
```

**الناتج المتوقع** (بافتراض أن A1 يحتوي على “R1/04/01”):

```
Parsed date from A1: 2024-04-01
```

إذا كانت الخلية تحتوي على تاريخ ميلادي مثل “2023‑12‑31”، يظل المحلل يعمل—فهو يُعيد التاريخ الأصلي دون تعديل.

---

## الخطوة 4: التحقق من جميع التواريخ في عمود  

غالبًا ما تحتاج إلى فحص عمود كامل من تواريخ العصور اليابانية. أدناه حلقة مختصرة تُظهر كيفية التعامل مع الخلايا الفارغة والمحتوى المختلط بسلاسة.

```csharp
// Step 4: Iterate through column B (index 1) and print each parsed date
int firstRow = 0;
int lastRow = sheet.Cells.MaxDataRow; // last row with data

for (int row = firstRow; row <= lastRow; row++)
{
    Cell cell = sheet.Cells[row, 1]; // column B
    if (cell.Type == CellValueType.IsDateTime)
    {
        Console.WriteLine($"Row {row + 1}: {cell.DateTimeValue:yyyy-MM-dd}");
    }
    else if (!cell.IsNull)
    {
        // Fallback: show raw string for non‑date cells
        Console.WriteLine($"Row {row + 1}: (non‑date) {cell.StringValue}");
    }
}
```

**نصيحة احترافية:** `CellValueType.IsDateTime` هي الطريقة الأكثر أمانًا للتحقق مما إذا كان التحليل قد نجح. تحميك من `InvalidCastException` عندما تحتوي الخلية على نص غير متوقع.

---

## الخطوة 5: المشكلات الشائعة وكيفية التعامل معها  

| المشكلة | سبب حدوثها | الحل |
|-------|----------------|-----|
| **الخلايا الفارغة تُعيد `DateTime.MinValue`** | يعامل المحلل السلاسل الفارغة كأقل تاريخ. | تحقق من `cell.IsNull` قبل الوصول إلى `DateTimeValue`. |
| **تقويمات مختلطة (يابانية + ميلادية) في نفس العمود** | يدعم المحلل كلا النوعين، لكن قد تحتاج إلى التمييز للتقارير. | استخدم `cell.StringValue` لتفحص النص الأصلي عندما يكون `cell.Type` هو `IsString`. |
| **العصر غير الصحيح (مثال: “H30” للهييسي بعد 2019)** | انتهى عهد الهييسي في 2019؛ التواريخ اللاحقة يجب أن تستخدم “R”. | تحقق من بادئة العصر قبل الاعتماد على النتيجة التي تم تحليلها. |
| **تباطؤ الأداء في الملفات الضخمة** | إضافة خيارات مخصصة يضيف عبئًا بسيطًا. | حمّل الأوراق المطلوبة فقط (`Workbook.LoadOptions.LoadAllWorksheets = false`). |

---

## الخطوة 6: مثال عملي كامل  

نجمع كل ما سبق في تطبيق console مستقل يمكنك نسخه ولصقه وتشغيله. يوضح **custom date parsing excel** من البداية حتى النهاية.

```csharp
// FullExample.cs
using System;
using System.IO;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Configure load options for Japanese era dates
        TxtLoadOptions loadOptions = new TxtLoadOptions
        {
            DateTimeParsing = DateTimeParsing.JapaneseEra
        };

        // 2️⃣ Load the workbook from file with those options
        string filePath = Path.Combine(Environment.CurrentDirectory, "japan_dates.xlsx");
        if (!File.Exists(filePath))
        {
            Console.WriteLine($"File not found: {filePath}");
            return;
        }

        Workbook workbook = new Workbook(filePath, loadOptions);
        Worksheet sheet = workbook.Worksheets[0];

        // 3️⃣ Read a single cell (A1) – demonstrates automatic parsing
        Cell a1 = sheet.Cells["A1"];
        Console.WriteLine($"A1 raw value: {a1.StringValue}");
        Console.WriteLine($"A1 parsed date: {a1.DateTimeValue:yyyy-MM-dd}");

        // 4️⃣ Loop through column B to show batch parsing
        Console.WriteLine("\n--- Column B Dates ---");
        int lastRow = sheet.Cells.MaxDataRow;
        for (int row = 0; row <= lastRow; row++)
        {
            Cell cell = sheet.Cells[row, 1]; // B column
            if (cell.Type == CellValueType.IsDateTime)
                Console.WriteLine($"Row {row + 1}: {cell.DateTimeValue:yyyy-MM-dd}");
            else if (!cell.IsNull)
                Console.WriteLine($"Row {row + 1}: (non‑date) {cell.StringValue}");
        }

        // 5️⃣ Optional: Save a copy with dates converted to ISO format
        // This shows that the workbook now holds proper DateTime objects.
        workbook.Save("japan_dates_converted.xlsx");
        Console.WriteLine("\nWorkbook saved as japan_dates_converted.xlsx");
    }
}
```

**ما يجب أن تراه** عندما يحتوي `japan_dates.xlsx` على:

| A | B |
|---|---|
| R1/04/01 | 2023‑12‑31 |
| H30/12/31 | R2/01/01 |
| (blank) | R2/02/15 |

مخرجات وحدة التحكم:

```
A1 raw value: R1/04/01
A1 parsed date: 2024-04-01

--- Column B Dates ---
Row 1: 2023-12-31
Row 2: 2025-01-01
Row 3: (non-date) 
Row 4: 2025-02-15
Workbook saved as japan_dates_converted.xlsx
```

الملف المحفوظ الآن يخزن خلايا تاريخية صحيحة، ويمكنك فتحه في Excel ورؤية تنسيق التاريخ المعتاد.

---

## الخلاصة  

لقد أظهرنا لك كيفية **تحليل تواريخ العصور اليابانية** في Excel عبر تكوين `TxtLoadOptions`، **تحميل المصنف من ملف** بهذه الخيارات، والعمل مع قيم `DateTime` الناتجة. النمط نفسه—ضبط أعلام التحليل المخصصة ثم تحميل المصنف—ينطبق على أي متطلب **custom date parsing excel**، سواء كنت تتعامل مع فترات مالية، أرقام أسابيع ISO، أو صيغ مملوكة.

هل لديك عصر مختلف أو جدول مختلط التقويمات؟ فقط استبدل `DateTimeParsing.JapaneseEra` بقيمة تعداد أخرى (مثل `DateTimeParsing.Custom`) وقدم صيغة تنسيق. مرونة Aspose.Cells تعني أنك نادراً ما تحتاج إلى كتابة كود تحويل يدوي مرة أخرى.

**الخطوات التالية** التي قد تستكشفها:

* **Load Excel with options** لملفات CSV (`CsvLoadOptions`) لمعالجة الفواصل الخاصة باللغات.
* استخدم `Workbook.Save` مع `SaveFormat.Xlsx` لتصدير البيانات المنقحة.
* دمج هذا النهج مع **Aspose.Slides** أو **Aspose.Words** لإنشاء خطوط تقارير متكاملة.

جرّبه، عدّل الخيارات، ودع المكتبة تقوم بالعمل الشاق. Happy coding!  

![لقطة شاشة لتواريخ العصور اليابانية التي تم تحليلها في نافذة وحدة التحكم – مثال تحليل تواريخ العصور اليابانية](/images/parse-japanese-era-dates.png)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}