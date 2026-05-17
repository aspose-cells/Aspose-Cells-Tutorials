---
category: general
date: 2026-02-21
description: احفظ ملف Excel كملف txt مع تحكم دقيق في الأرقام ذات الدقة. صدّر ملف Excel
  إلى txt باستخدام C# واضبط الأرقام ذات الدقة بسهولة.
draft: false
keywords:
- save excel as txt
- export excel to txt
- set significant digits
- save workbook as text
- export numbers to txt
language: ar
og_description: احفظ ملف Excel كملف txt بسرعة. تعلّم كيفية تصدير Excel إلى txt، وضبط
  الأرقام ذات الدقة، والتحكم في إخراج النص باستخدام C#.
og_title: حفظ Excel كملف txt – تصدير الأرقام ذات الخانات المهمة في C#
tags:
- C#
- Aspose.Cells
- Excel automation
title: حفظ إكسل كملف txt – دليل C# الشامل لتصدير الأرقام ذات الخانات الهامة
url: /ar/net/converting-excel-files-to-other-formats/save-excel-as-txt-complete-c-guide-to-export-numbers-with-si/
---

Image alt text: "*Alt text: “Numbers.txt file displaying 12350, 0.0001235, and -98800 after saving Excel as txt with 4 significant digits.”*" translate alt text but keep quotes and numbers.

Also the image line "*Image: A screenshot of the generated `Numbers.txt` file showing rounded values.*" translate.

Make sure to keep markdown formatting.

Let's produce final content.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# حفظ Excel كملف txt – دليل C# الكامل لتصدير الأرقام بالأرقام ذات الدقة المهمة

هل احتجت يوماً إلى **حفظ Excel كملف txt** لكنك كنت قلقاً من فقدان الأرقام لدقتها؟ لست وحدك. يواجه العديد من المطورين صعوبة عندما يحاولون تصدير Excel إلى txt وينتهي بهم الأمر إما بوجود عدد كبير من المنازل العشرية أو بنتيجة مقربة غير دقيقة.  

في هذا الدرس سنظهر لك طريقة مباشرة لـ **تصدير Excel إلى txt** مع **تحديد الأرقام ذات الدقة المهمة** بحيث يكون الناتج بالضبط كما تريد. في النهاية ستحصل على مقطع C# جاهز للتنفيذ يحفظ دفتر عمل كنص، يصدر الأرقام إلى txt، ويمنحك التحكم الكامل في تنسيق الأرقام.

## ما ستتعلمه

- كيفية إنشاء دفتر عمل جديد وكتابة بيانات رقمية.
- الطريقة الصحيحة لـ **تحديد الأرقام ذات الدقة المهمة** باستخدام `TxtSaveOptions`.
- كيفية **حفظ دفتر العمل كنص** والتحقق من النتيجة.
- معالجة الحالات الخاصة (أرقام كبيرة، قيم سلبية، مشاكل الإعدادات الإقليمية).
- نصائح سريعة لتعديل المخرجات أكثر (تغيير الفاصل، الترميز).

### المتطلبات المسبقة

- .NET 6.0 أو أحدث (الكود يعمل أيضاً على .NET Framework 4.6+).
- حزمة **Aspose.Cells** من NuGet (`Install-Package Aspose.Cells`).
- فهم أساسي لصياغة C# — لا تحتاج إلى معرفة عميقة بـ Excel interop.

> **نصيحة احترافية:** إذا كنت تستخدم Visual Studio، فعّل *nullable reference types* (`<Nullable>enable</Nullable>`) لتكتشف أخطاء الـ null مبكراً.

---

## الخطوة 1: تهيئة دفتر العمل وكتابة رقم

أولاً، نحتاج إلى كائن دفتر عمل. فكر فيه كتمثيل في الذاكرة لملف Excel.  

```csharp
using Aspose.Cells;
using System;

// Create a new workbook (starts with one worksheet by default)
var workbook = new Workbook();
var worksheet = workbook.Worksheets[0];

// Write a numeric value into cell A1 (row 0, column 0)
worksheet.Cells[0, 0].PutValue(12345.6789);
```

**لماذا هذا مهم:**  
إنشاء دفتر العمل برمجياً يتجنب عبء COM interop، وتقوم `PutValue` تلقائياً باكتشاف نوع البيانات، مما يضمن أن تُعامل الخلية كرقم—not كـ string.

---

## الخطوة 2: ضبط TxtSaveOptions للتحكم في الأرقام ذات الدقة المهمة

فئة `TxtSaveOptions` هي المكان الذي يحدث فيه السحر. من خلال ضبط `SignificantDigits`، تخبر Aspose.Cells بعدد الأرقام ذات المعنى التي يجب الاحتفاظ بها عند كتابة الملف.

```csharp
// Configure text save options – keep only 4 significant digits
var txtSaveOptions = new TxtSaveOptions
{
    // 4 significant digits means 12345.6789 becomes 12350
    SignificantDigits = 4,

    // Optional: change delimiter if you need CSV‑style output
    // Delimiter = ',',

    // Optional: force UTF‑8 encoding for broader character support
    // Encoding = System.Text.Encoding.UTF8
};
```

**لماذا يجب ضبط هذا:**  
عند **تصدير الأرقام إلى txt**، غالباً ما تحتاج إلى تمثيل مختصر (مثلاً لأنظمة التقارير التي تقبل دقة معينة فقط). خاصية `SignificantDigits` تضمن تقريباً ثابتاً بغض النظر عن طول الرقم الأصلي.

---

## الخطوة 3: حفظ دفتر العمل كملف نصي

الآن نكتب دفتر العمل إلى القرص باستخدام الخيارات التي عرّفناها للتو.

```csharp
// Define the output path – adjust to your environment
string outputPath = @"C:\Temp\Numbers.txt";

// Save the workbook as a .txt file with the configured options
workbook.Save(outputPath, txtSaveOptions);

Console.WriteLine($"Workbook saved as txt at: {outputPath}");
```

**ما ستراه:**  
افتح `Numbers.txt` وستحصل على سطر واحد:

```
12350
```

تم تقريب الرقم الأصلي `12345.6789` إلى **أربعة أرقام ذات دقة مهمة**، تماماً كما طلبت.

---

## الخطوة 4: التحقق من النتيجة (اختياري لكن موصى به)

الاختبارات الآلية عادةً عادة جيدة. إليك فحص سريع يمكنك تشغيله مباشرة بعد الحفظ:

```csharp
// Read back the file to confirm the content
string fileContent = System.IO.File.ReadAllText(outputPath).Trim();

if (fileContent == "12350")
{
    Console.WriteLine("✅ Export succeeded – significant digits applied correctly.");
}
else
{
    Console.WriteLine($"⚠️ Unexpected output: {fileContent}");
}
```

تشغيل هذا المقطع سيطبع علامة صح خضراء إذا كان كل شيء متطابقاً، مما يمنحك الثقة أن عملية **حفظ Excel كملف txt** سارت كما هو متوقع.

---

## الاختلافات الشائعة والحالات الخاصة

### تصدير خلايا أو نطاقات متعددة

إذا كنت بحاجة إلى **تصدير Excel إلى txt** لنطاق كامل، فقط املأ خلايا أكثر قبل الحفظ:

```csharp
worksheet.Cells[0, 1].PutValue(0.000123456);
worksheet.Cells[0, 2].PutValue(-98765.4321);
```

ستطبق نفس `TxtSaveOptions` قاعدة الأربعة أرقام على كل قيمة، لتنتج:

```
12350
0.0001235
-98800
```

### تغيير الفاصل

بعض الأنظمة المستقبلة تتوقع قيماً مفصولة بعلامة تبويب. عدّل الفاصل هكذا:

```csharp
txtSaveOptions.Delimiter = '\t'; // Tab character
```

الآن كل خلية في الصف تظهر مفصولة بعلامة تبويب.

### معالجة الفواصل العشرية حسب الإعدادات الإقليمية

إذا كان جمهورك يستخدم الفواصل بدلاً من النقاط، اضبط الثقافة:

```csharp
txtSaveOptions.CultureInfo = new System.Globalization.CultureInfo("fr-FR");
```

سيتوافق الناتج مع الإعداد الإقليمي، محوّلاً `12350` إلى `12 350` (مسافة كفاصل آلاف في الفرنسية).

---

## مثال كامل جاهز للنسخ واللصق

```csharp
using Aspose.Cells;
using System;
using System.IO;

class Program
{
    static void Main()
    {
        // 1️⃣ Create workbook and write numbers
        var workbook = new Workbook();
        var sheet = workbook.Worksheets[0];
        sheet.Cells[0, 0].PutValue(12345.6789);
        sheet.Cells[0, 1].PutValue(0.000123456);
        sheet.Cells[0, 2].PutValue(-98765.4321);

        // 2️⃣ Configure save options – 4 significant digits
        var txtOptions = new TxtSaveOptions
        {
            SignificantDigits = 4,
            // Delimiter = '\t',               // Uncomment for TSV
            // Encoding = System.Text.Encoding.UTF8,
            // CultureInfo = new System.Globalization.CultureInfo("en-US")
        };

        // 3️⃣ Save to text file
        string path = Path.Combine(Environment.GetFolderPath(Environment.SpecialFolder.Desktop), "Numbers.txt");
        workbook.Save(path, txtOptions);
        Console.WriteLine($"File saved to {path}");

        // 4️⃣ Verify result (optional)
        string result = File.ReadAllText(path).Trim();
        Console.WriteLine($"File content: {result}");
    }
}
```

**المحتوى المتوقع لملف `Numbers.txt` (الفاصل الافتراضي، 4 أرقام ذات دقة مهمة):**

```
12350	0.0001235	-98800
```

تظهر علامة التبويب (`\t`) لأننا تركنا الفاصل على قيمته الافتراضية (تبويب) في المثال؛ غيّرها إلى فاصلة إذا كنت تفضّل CSV.

---

## الخلاصة

أنت الآن تعرف بالضبط **كيفية حفظ Excel كملف txt** مع التحكم في عدد الأرقام ذات الدقة المهمة. الخطوات — إنشاء دفتر عمل، ضبط `TxtSaveOptions.SignificantDigits`، والحفظ — هي كل ما تحتاجه لتقوم بـ **تصدير Excel إلى txt** بثقة.  

من هنا يمكنك:

- **تصدير الأرقام إلى txt** لمجموعات بيانات أكبر.
- تعديل الفواصل، الترميز، أو إعدادات الثقافة لتتناسب مع أي نظام مستقبلي.
- دمج هذا النهج مع ميزات أخرى من Aspose.Cells (أنماط، صيغ) قبل التصدير.

جرّبه، عدّل `SignificantDigits` إلى 2 أو 6، وشاهد كيف يتغيّر الناتج. مرونة **حفظ دفتر العمل كنص** تجعلها أداة مفيدة في أي خط أنابيب لتبادل البيانات.

---

### مواضيع ذات صلة قد ترغب في استكشافها لاحقاً

- **تصدير Excel إلى CSV** مع ترتيب أعمدة مخصص.
- **قراءة ملفات txt مرة أخرى إلى دفتر عمل** (`Workbook.Load` مع `LoadOptions`).
- **معالجة دفعات** لعدة أوراق عمل وتوحيدها في ملف txt واحد.
- **تحسين الأداء** لتصدير واسع النطاق (البث مقابل الذاكرة).

لا تتردد في ترك تعليق إذا واجهت أي صعوبات، أو مشاركة كيفية تخصيصك للتصدير في مشاريعك. Happy coding!  

---  

*صورة: لقطة شاشة لملف `Numbers.txt` المُولد تُظهر القيم المقربة.*  
*النص البديل: “ملف Numbers.txt يعرض 12350، 0.0001235، و -98800 بعد حفظ Excel كملف txt بأربعة أرقام ذات دقة مهمة.”*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}