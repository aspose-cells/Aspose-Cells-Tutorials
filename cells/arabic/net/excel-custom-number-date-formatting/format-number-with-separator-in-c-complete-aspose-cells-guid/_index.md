---
category: general
date: 2026-03-30
description: تعلم كيفية تنسيق الأرقام باستخدام الفاصل باستخدام Aspose.Cells في C#.
  يتضمن تعيين تنسيق رقم مخصص، إضافة فاصل الآلاف، تنسيق الأجزاء العشرية، وكيفية تنسيق
  الخلية.
draft: false
keywords:
- format number with separator
- set custom number format
- add thousands separator
- format decimal places
- how to format cell
language: ar
og_description: تنسيق الأرقام باستخدام الفاصل في C#. يوضح هذا الدليل كيفية تعيين تنسيق
  رقم مخصص، إضافة فاصل الآلاف، تنسيق الأجزاء العشرية، وكيفية تنسيق الخلية باستخدام
  Aspose.Cells.
og_title: تنسيق الرقم باستخدام الفاصل في C# – دليل Aspose.Cells
tags:
- C#
- Aspose.Cells
- Number Formatting
title: تنسيق الرقم باستخدام الفاصل في C# – دليل Aspose.Cells الكامل
url: /ar/net/excel-custom-number-date-formatting/format-number-with-separator-in-c-complete-aspose-cells-guid/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تنسيق الرقم بفاصل في C# – دليل Aspose.Cells الكامل

هل احتجت يوماً إلى **تنسيق رقم بفاصل** في جدول بيانات لكن لم تكن متأكدًا من أي استدعاء API تستخدمه؟ لست وحدك—المطورون يواجهون باستمرار فواصل الآلاف، المنازل العشرية، والأنماط المخصصة عند تصدير البيانات.  

خبر سار: Aspose.Cells يجعل الأمر سهلًا للغاية. في هذا الدرس سنستعرض مثالًا واقعيًا ي **يضبط تنسيق رقم مخصص**، **يضيف فاصل الآلاف**، **ينسق المنازل العشرية**، ويظهر **كيفية تنسيق الخلية** كقيمة نصية. في النهاية ستحصل على مقطع جاهز للتنفيذ يمكنك إدراجه في أي مشروع .NET.

## ما يغطيه هذا الدليل

* حزمة NuGet الدقيقة التي تحتاجها وكيفية تثبيتها.  
* كود خطوة بخطوة ينشئ مصنفًا، يكتب قيمة رقمية، ويطبق تنسيقًا مخصصًا.  
* لماذا `ExportTableOptions.ExportAsString` هو الطريقة المفضلة لاسترجاع قيمة منسقة.  
* الأخطاء الشائعة—مثل نسيان تمكين `ExportAsString` أو استخدام قناع تنسيق غير صحيح.  
* كيفية تعديل قناع التنسيق إذا كنت تحتاج عددًا مختلفًا من المنازل العشرية أو نمط فاصل مختلف.

لا توجد روابط توثيق خارجية مطلوبة؛ كل ما تحتاجه موجود هنا. لنبدأ.

---

## المتطلبات المسبقة

| المتطلب | السبب |
|-------------|--------|
| .NET 6.0 أو أحدث | Aspose.Cells 23.10+ يستهدف .NET Standard 2.0+، لذا .NET 6 آمن وحديث. |
| Visual Studio 2022 (أو أي بيئة تطوير C#) | يجعل عملية التصحيح وإدارة الحزم سهلة. |
| حزمة Aspose.Cells for .NET عبر NuGet | توفر الفئات `Workbook`، `Worksheet`، و `ExportTableOptions` التي سنستخدمها. |

يمكنك تثبيت الحزمة عبر وحدة تحكم مدير الحزم:

```powershell
Install-Package Aspose.Cells
```

هذا كل شيء—بدون ملفات DLL إضافية، بدون COM interop، مجرد مرجع NuGet واحد.

---

## الخطوة 1: تهيئة مصنف جديد (كيفية تنسيق الخلية)

أول شيء نقوم به هو إنشاء كائن `Workbook` جديد. فكر فيه كملف Excel فارغ جاهز لاستقبال البيانات.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Create a new workbook – this is where we’ll format the cell.
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];
```

> **لماذا هذا مهم:** `Workbook` هو نقطة الدخول لكل عملية في Aspose.Cells. من خلال الحصول على الورقة الأولى (`Worksheets[0]`) نحصل على مساحة عمل نظيفة دون الحاجة لتسمية الورقة.

---

## الخطوة 2: كتابة قيمة رقمية في الخلية المستهدفة

بعد ذلك، نضع رقمًا خامًا في الخلية **A1**. القيمة نفسها لم تُنسق بعد—إنها مجرد double.

```csharp
        // Step 2: Insert a raw numeric value.
        worksheet.Cells["A1"].PutValue(12345.6789);
```

> **نصيحة احترافية:** استخدم `PutValue` بدلاً من `PutString` عندما تنوي تطبيق تنسيق رقمي لاحقًا. هذا يحافظ على نوع البيانات الأساسي، مما يسمح بحسابات متوافقة مع Excel.

---

## الخطوة 3: ضبط تنسيق رقم مخصص (إضافة فاصل الآلاف وتنسيق المنازل العشرية)

الآن يأتي جوهر الدرس: تعريف قناع تنسيق يخبر Aspose.Cells كيف يعرض الرقم. القناع `#,##0.00` يقوم بثلاثة أشياء:

1. **`#,##0`** – يضيف فاصل الآلاف (الفاصلة الافتراضية).  
2. **`.00`** – يفرض منزلتين عشريتين بالضبط.  

إذا كنت تحتاج عددًا مختلفًا من المنازل العشرية، فقط غير عدد الـ `0` بعد النقطة العشرية.

```csharp
        // Step 3: Configure the custom number format.
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,          // Return the value as a formatted string.
            NumberFormat = "#,##0.00"       // Add thousands separator and fix to 2 decimals.
        };
```

> **لماذا نستخدم `ExportAsString`**: بشكل افتراضي، `ExportString` يُعيد القيمة الخام. ضبط `ExportAsString = true` يجبر الـ API على تطبيق قناع `NumberFormat` قبل التحويل إلى نص. هذا ضروري عندما تحتاج إلى تمثيل نصي دقيق للتقارير، أو حمولات JSON، أو عرض الواجهة.

---

## الخطوة 4: تصدير النص المنسق (كيفية تنسيق الخلية)

مع إعداد الخيارات، نستدعي `ExportString` على نفس الخلية. الطريقة تحترم القناع الذي عرّفناه وتعيد لنا سلسلة منسقة بشكل جميل.

```csharp
        // Step 4: Export the formatted value.
        string formattedCellText = worksheet.Cells["A1"].ExportString(exportOptions);

        // Step 5: Show the result.
        Console.WriteLine(formattedCellText); // Expected output: 12,345.68
    }
}
```

تشغيل البرنامج يطبع **`12,345.68`** إلى وحدة التحكم—تمامًا التنسيق الذي طلبناه.

> **حالة حافة:** إذا كان الرقم الأصلي يحتوي على أكثر من منزلتين عشريتين، القناع يقوم بالتقريب. إذا كنت تحتاج إلى قص بدلاً من التقريب، سيتعين عليك معالجة القيمة مسبقًا باستخدام `Math.Truncate` قبل استدعاء `PutValue`.

---

## الخطوة 5: تعديل التنسيق – تنويعات شائعة

### 5.1 تغيير دقة المنازل العشرية

هل تريد ثلاث منازل عشرية؟ فقط استبدل القناع:

```csharp
NumberFormat = "#,##0.000"   // → 12,345.679
```

### 5.2 استخدام فاصل آلاف مختلف

بعض اللغات تفضّل مساحة أو نقطة. يمكنك إدراج الحرف مباشرة:

```csharp
NumberFormat = "# ##0.00"    // Uses a non‑breaking space as separator.
```

أو الاعتماد على إعدادات الثقافة الخاصة بالمصنف:

```csharp
workbook.Settings.CultureInfo = new System.Globalization.CultureInfo("de-DE");
NumberFormat = "#.##0,00";   // German style: 12.345,68
```

### 5.3 البادئة أو اللاحقة (عملة، نسبة مئوية)

أضف علامة الدولار أو النسبة المئوية مباشرة في القناع:

```csharp
NumberFormat = "$#,##0.00";   // → $12,345.68
NumberFormat = "0.00%";       // → 1,234,568.00%
```

> **ملاحظة:** القناع حساس لحالة الأحرف. `$` و `%` هما رموز حرفية؛ لا يؤثران على القيمة الرقمية الأساسية.

---

## الخطوة 6: مثال كامل يعمل (جاهز للنسخ واللصق)

فيما يلي البرنامج الكامل الذي يمكنك نسخه إلى تطبيق Console جديد. يتضمن جميع الخطوات، التعليقات، والتحقق من النتيجة النهائية.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialise workbook and worksheet.
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // 2️⃣ Write raw numeric value to A1.
        worksheet.Cells["A1"].PutValue(12345.6789);

        // 3️⃣ Define custom format: thousands separator + two decimals.
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,
            NumberFormat = "#,##0.00"
        };

        // 4️⃣ Export the formatted string.
        string result = worksheet.Cells["A1"].ExportString(exportOptions);

        // 5️⃣ Display the outcome.
        Console.WriteLine(result); // Output: 12,345.68

        // Optional: keep console open.
        Console.WriteLine("Press any key to exit...");
        Console.ReadKey();
    }
}
```

شغّل البرنامج (`dotnet run` من الطرفية أو اضغط F5 في Visual Studio) وسترى الرقم المنسق يُطبع بالضبط كما هو موضح.

---

## الأسئلة المتكررة (FAQ)

**س: هل يعمل هذا مع إصدارات Excel القديمة؟**  
ج: نعم. قناع التنسيق يتبع صيغة تنسيق الأرقام الأصلية في Excel، لذا أي نسخة تفهم `#,##0.00` ستعرض السلسلة نفسها.

**س: ماذا لو أردت تنسيق نطاق من الخلايا؟**  
ج: قم بالتكرار على النطاق المطلوب وطبق نفس `ExportTableOptions` على كل خلية، أو اضبط الخاصية `Style.Custom` على النطاق ثم استدعِ `ExportString` على خلية واحدة.

**س: هل يمكنني تصدير مباشرة إلى CSV مع تطبيق هذه التنسيقات؟**  
ج: بالتأكيد. استخدم `Workbook.Save("output.csv", SaveFormat.CSV);` بعد ضبط التنسيق على كل خلية. Aspose.Cells يحترم `Style` الخلية عند توليد CSV.

---

## الخلاصة

لقد أظهرنا لك كيفية **تنسيق رقم بفاصل** في C# باستخدام Aspose.Cells، مع تغطية كل شيء من **ضبط تنسيق رقم مخصص** إلى **إضافة فاصل آلاف**، **تنسيق المنازل العشرية**، و**كيفية تنسيق الخلية** لتصدير النص. الكود مكتمل ذاتيًا، يعمل مع .NET 6+، ويمكن تكييفه لأي لغة أو دقة مطلوبة.

الخطوات التالية قد تشمل:

* تطبيق التقنية نفسها على التواريخ والأوقات (`NumberFormat = "dd‑MMM‑yyyy"`).  
* أتمتة تصدير مجموعات كبيرة حيث يحتاج كل عمود إلى قناع مختلف.  
* دمج السلاسل المنسقة في تقارير PDF باستخدام Aspose.Words.

جرّب ذلك وستصبح الشخص المرجعي لتنسيق الجداول في فريقك. برمجة سعيدة! (صورة: ![Screenshot showing formatted number with separator in Aspose.Cells](image-placeholder.png){alt="رقم منسق بفاصل معروض في مخرجات Aspose.Cells"} )

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}