---
category: general
date: 2026-03-22
description: تعلم كيفية تنسيق التاريخ والوقت إلى صيغة ISO أثناء استخراج التاريخ من
  Excel وعرض تاريخ ISO باستخدام Aspose.Cells في C#.
draft: false
keywords:
- format datetime to iso
- extract date from excel
- display iso date
- Aspose.Cells date parsing
- Japanese era dates
language: ar
og_description: تنسيق التاريخ والوقت إلى ISO بسهولة. يوضح هذا الدليل كيفية استخراج
  التاريخ من Excel وعرض تاريخ ISO باستخدام Aspose.Cells.
og_title: تنسيق التاريخ والوقت إلى ISO في C# – دليل خطوة بخطوة
tags:
- C#
- Aspose.Cells
- DateTime
- Excel
- ISO 8601
title: تنسيق التاريخ والوقت إلى ISO في C# – دليل كامل
url: /ar/net/number-and-display-formats-in-excel/format-datetime-to-iso-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تنسيق datetime إلى iso في C# – الدليل الكامل

هل احتجت يوماً إلى **format datetime to iso** لكن المصدر موجود داخل مصنف Excel؟ ربما تحتوي الخلية على عصر ياباني مثل “令和3年5月1日” وتجد نفسك تحاول معرفة كيفية تحويله إلى سلسلة نظيفة `2021‑05‑01`. لست وحدك. في هذا الدرس سنقوم بـ **extract date from excel**، وتحليل العصر الياباني، ثم **display iso date** على وحدة التحكم—كل ذلك ببضع أسطر من C# و Aspose.Cells.

سنستعرض كل ما تحتاجه: حزمة NuGet المطلوبة، الكود الدقيق الذي يمكنك نسخه‑ولصقه، سبب أهمية كل سطر، وبعض النصائح للتعامل مع الحالات الخاصة. في النهاية ستحصل على مقطع قابل لإعادة الاستخدام ينسق datetime إلى iso بغض النظر عن غرابة القيمة الأصلية في Excel.

## ما ستحتاجه

- .NET 6.0 أو أحدث (الكود يُجمّع أيضاً على .NET Framework 4.6+)
- Visual Studio 2022 (أو أي محرر تفضله)
- **Aspose.Cells for .NET** حزمة NuGet – `Install-Package Aspose.Cells`
- ملف Excel (أو مصنف جديد) يحتوي على تاريخ بصيغة العصر الياباني

هذا كل شيء. لا مكتبات إضافية، لا COM interop، مجرد طريقة واحدة موثقة جيداً.

## الخطوة 1: إنشاء مصنف وكتابة تاريخ بعصر ياباني  

أولاً، نحتاج إلى مصنف للعمل معه. إذا كان لديك ملف Excel بالفعل، يمكنك تحميله باستخدام `new Workbook("path")`. في هذا المثال سننشئ مصنفاً جديداً في الذاكرة ونضع سلسلة العصر الياباني في الخلية **A1**.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a fresh workbook
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.Worksheets[0];

        // 2️⃣ Write a Japanese era date (Reiwa 3 = 2021) into A1
        sheet.Cells["A1"].PutValue("令和3年5月1日");
```

> **Why we do this:** Aspose.Cells treats cell values as strings by default. By inserting the raw era text we simulate a real‑world scenario where a Japanese client has entered dates in their native calendar.

## الخطوة 2: تمكين تحليل العصر الياباني واستخراج التاريخ  

يمكن لـ Aspose.Cells ترجمة سلاسل العصر الياباني إلى كائنات .NET `DateTime` تلقائياً— بشرط أن تخبره بذلك. علم `DateTimeParseOptions.EnableJapaneseEra` يقوم بالعمل الشاق.

```csharp
        // 3️⃣ Retrieve the cell value while enabling Japanese era parsing
        CellValue parsed = sheet.Cells["A1"]
            .GetValue(CellValueType.DateTime, DateTimeParseOptions.EnableJapaneseEra);
```

> **Pro tip:** If you forget the `EnableJapaneseEra` option, the library will return the original string, and your subsequent conversion will fail. Always verify `parsed.Type` if you’re handling mixed content.

## الخطوة 3: تحويل DateTime المُحلل إلى ISO 8601  

الآن بعد أن حصلنا على `DateTime` صحيح، تحويله إلى سلسلة بصيغة ISO سهل جداً. نمط `"yyyy-MM-dd"` يتوافق مع جزء التاريخ في ISO 8601، وهو ما تتوقعه معظم الـ APIs.

```csharp
        // 4️⃣ Convert to ISO 8601 (yyyy‑MM‑dd) and display it
        string isoDate = parsed.DateTimeValue.ToString("yyyy-MM-dd");
        Console.WriteLine($"ISO date: {isoDate}");
    }
}
```

تشغيل البرنامج يطبع:

```
ISO date: 2021-05-01
```

هذا هو **display iso date** الذي كنت تبحث عنه.

## مثال كامل قابل للتنفيذ  

فيما يلي كتلة الكود الكاملة التي يمكنك نسخها مباشرة إلى مشروع Console. لا تبعيات مخفية، لا إعدادات إضافية.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Write a Japanese era date into cell A1
        worksheet.Cells["A1"].PutValue("令和3年5月1日");

        // Retrieve the cell value with Japanese era parsing enabled
        CellValue parsedValue = worksheet.Cells["A1"]
            .GetValue(CellValueType.DateTime, DateTimeParseOptions.EnableJapaneseEra);

        // Convert the DateTime to ISO 8601 format and output it
        string isoDate = parsedValue.DateTimeValue.ToString("yyyy-MM-dd");
        Console.WriteLine($"ISO date: {isoDate}");
    }
}
```

> **Expected output:** `ISO date: 2021-05-01`

## تحليل خطوة‑بخطوة (لماذا كل جزء مهم)

| الخطوة | ما يحدث | لماذا هو مهم |
|------|--------------|--------------------|
| **Create workbook** | Initializes an in‑memory Excel container. | Gives you a sandbox to test without touching the file system. |
| **PutValue** | Stores the raw Japanese era string in **A1**. | Mimics real data entry; ensures the parser sees the exact text. |
| **GetValue with `EnableJapaneseEra`** | Converts the era string into a .NET `DateTime`. | Handles the calendar conversion automatically—no manual lookup tables needed. |
| **`ToString("yyyy-MM-dd")`** | Formats the `DateTime` to ISO 8601. | Guarantees a culture‑invariant, sortable date string accepted by REST APIs, databases, etc. |
| **Console.WriteLine** | Shows the final ISO date. | Confirms the whole pipeline works end‑to‑end. |

## التعامل مع المتغيّرات الشائعة  

### 1. مواقع خلايا مختلفة  

إذا كان تاريخك في **B2** أو نطاق مسمى، استبدل ببساطة `"A1"` بالعنوان المناسب:

```csharp
worksheet.Cells["B2"].PutValue("令和2年12月31日");
var value = worksheet.Cells["B2"]
    .GetValue(CellValueType.DateTime, DateTimeParseOptions.EnableJapaneseEra);
```

### 2. تواريخ متعددة في عمود  

عند الحاجة إلى **extract date from excel** لعدة صفوف، قم بالتكرار عبر النطاق المستخدم:

```csharp
int lastRow = worksheet.Cells.MaxDataRow;
for (int i = 0; i <= lastRow; i++)
{
    var cell = worksheet.Cells[i, 0]; // column A
    var cv = cell.GetValue(CellValueType.DateTime, DateTimeParseOptions.EnableJapaneseEra);
    string iso = cv.DateTimeValue.ToString("yyyy-MM-dd");
    Console.WriteLine($"Row {i + 1}: {iso}");
}
```

### 3. حل احتياطي للتواريخ غير المرتبطة بالعصر  

إذا كانت الخلية تحتوي بالفعل على سلسلة تاريخ قياسية، فإن المحلل لا يزال يعمل، لكن قد ترغب في إضافة شبكة أمان:

```csharp
CellValue cv = cell.GetValue(CellValueType.DateTime,
    DateTimeParseOptions.EnableJapaneseEra | DateTimeParseOptions.TryParse);
```

علم `TryParse` يمنع الاستثناءات ويعيد القيمة الأصلية إذا فشل التحويل.

### 4. مكوّن الوقت  

إذا كنت تحتاج إلى جزء الوقت أيضاً، استخدم `"yyyy-MM-ddTHH:mm:ss"`:

```csharp
string isoDateTime = parsedValue.DateTimeValue.ToString("yyyy-MM-ddTHH:mm:ss");
```

سيعطيك ذلك طابعاً زمنياً كاملاً بصيغة ISO 8601 (`2021-05-01T00:00:00`).

## المساعدة البصرية  

![format datetime to iso example](image.png "An example of formatting datetime to iso in C#")

*نص بديل:* *مثال على تنسيق datetime إلى iso يظهر مخرجات وحدة التحكم*

## الأسئلة المتكررة  

- **هل يمكنني استخدام هذا مع ملفات .xls؟**  
  نعم. Aspose.Cells يدعم `.xls`،`.xlsx`،`.csv` والعديد من الصيغ الأخرى مباشرة.

- **ماذا لو كان المصنف محميًا بكلمة مرور؟**  
  حمّله باستخدام `new Workbook("file.xlsx", new LoadOptions { Password = "secret" })`.

- **هل صيغة ISO تعتمد على الإعدادات الإقليمية؟**  
  لا. نمط `"yyyy-MM-dd"` غير معتمد على الثقافة، مما يضمن نفس السلسلة على أي جهاز.

- **هل يعمل هذا على .NET Core؟**  
  بالتأكيد—Aspose.Cells متوافق مع .NET Standard 2.0.

## الخلاصة  

لقد غطينا كيفية **format datetime to iso** عن طريق **extracting date from excel**، وتحليل سلاسل العصر الياباني، وأخيراً **displaying iso date** على وحدة التحكم. الخطوات الأساسية—إنشاء مصنف، كتابة أو تحميل نص العصر، تمكين تحليل العصر الياباني، وتنسيق باستخدام `ToString("yyyy-MM-dd")`—هي كل ما تحتاجه لمعظم السيناريوهات.

بعد ذلك، قد ترغب في:

- كتابة تواريخ ISO مرة أخرى في عمود آخر للمعالجة اللاحقة.
- تصدير المصنف المحوّل إلى CSV للاستيراد الجماعي.
- دمج هذه المنطق مع واجهة ويب API تقبل تحميلات Excel وتعيد تواريخ ISO مشفّرة بصيغة JSON.

لا تتردد في تجربة صيغ تواريخ مختلفة، مناطق زمنية، أو حتى تقاويم مخصصة. مرونة Aspose.Cells تعني أنك نادراً ما تصطدم بحاجز.

برمجة سعيدة، ولتكن جميع تواريخك متوافقة تماماً مع ISO!  

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}