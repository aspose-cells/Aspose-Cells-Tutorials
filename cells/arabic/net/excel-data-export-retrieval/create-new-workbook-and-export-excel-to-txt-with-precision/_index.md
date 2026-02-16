---
category: general
date: 2026-02-15
description: إنشاء مصنف جديد وتصدير Excel إلى TXT مع ضبط الدقة العددية. تعلم كيفية
  تعيين الأرقام ذات الأهمية وتحديد الحد الأقصى للأرقام ذات الأهمية في C#.
draft: false
keywords:
- create new workbook
- export excel to txt
- set significant digits
- limit significant digits
- set numeric precision
language: ar
og_description: إنشاء مصنف جديد وتصدير Excel إلى TXT، مع ضبط الأرقام ذات الدقة المهمة
  للتمثيل الرقمي. دليل خطوة بخطوة بلغة C#.
og_title: إنشاء دفتر عمل جديد – تصدير إكسل إلى TXT بدقة
tags:
- C#
- Aspose.Cells
- Excel automation
title: إنشاء مصنف جديد وتصدير إكسل إلى TXT بدقة
url: /ar/net/excel-data-export-retrieval/create-new-workbook-and-export-excel-to-txt-with-precision/
---

}}

All unchanged.

Now produce final content with Arabic translations.

Make sure to keep markdown formatting exactly same.

Let's craft final answer.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء مصنف جديد – تصدير Excel إلى TXT مع تنسيق رقمي دقيق

هل تساءلت يومًا كيف تنشئ كائنات **create new workbook** في C# وتفريغها فورًا إلى ملف نصي عادي؟ لست وحدك. في العديد من سيناريوهات خطوط البيانات نحتاج إلى **export Excel to TXT** مع الحفاظ على قابلية قراءة الأرقام، مما يعني تحديد عدد الأرقام التي تظهر بعد الفاصلة العشرية.  

في هذا الدرس سنستعرض العملية بالكامل: من إنشاء مصنف جديد، إلى تكوين التصدير بحيث **sets significant digits** (أي تحديد الأرقام المهمة)، وأخيرًا كتابة الملف إلى القرص. في النهاية ستحصل على مقتطف جاهز للتنفيذ يحترم متطلبات **numeric precision** الخاصة بك—بدون مكتبات إضافية، بدون سحر.

> **نصيحة احترافية:** إذا كنت تستخدم Aspose.Cells بالفعل، فإن الفئات المعروضة أدناه هي جزء من تلك المكتبة. إذا كنت على منصة مختلفة، فإن المفاهيم لا تزال صالحة؛ فقط استبدل استدعاءات API.

---

## ما ستحتاجه

- .NET 6+ (الكود يُترجم على .NET Core و .NET Framework على حد سواء)  
- Aspose.Cells for .NET (نسخة تجريبية مجانية أو نسخة مرخصة) – التثبيت عبر NuGet: `dotnet add package Aspose.Cells`  
- أي بيئة تطوير تفضلها (Visual Studio, Rider, VS Code)  

هذا كل شيء. لا ملفات إعداد إضافية، ولا خطوات مخفية.

---

## الخطوة 1: إنشاء مصنف جديد

أول شيء هو **create new workbook**. فكر في فئة `Workbook` كملف Excel فارغ ينتظر الأوراق والخلايا والبيانات.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Instantiate a fresh workbook – this is the core of create new workbook logic
        Workbook workbook = new Workbook();

        // (Optional) Add some sample data so you can see the effect of numeric precision later
        Worksheet sheet = workbook.Worksheets[0];
        sheet.Cells["A1"].PutValue(12345.678901);
        sheet.Cells["A2"].PutValue(0.000123456);
        sheet.Cells["A3"].PutValue(Math.PI);
```

> **لماذا هذا مهم:** ببدء عملك بمصنف نظيف تتجنب أي تنسيق مخفي قد يتداخل مع إعدادات الدقة لاحقًا.

---

## الخطوة 2: تكوين خيارات حفظ النص – تحديد الأرقام المهمة

الآن نخبر Aspose.Cells عدد **significant digits** التي نريدها عند الكتابة إلى ملف `.txt`. فئة `TxtSaveOptions` تعرض خاصية `SignificantDigits` التي تقوم بذلك بالضبط.

```csharp
        // Step 2: Prepare save options – limit numeric precision to 5 significant digits
        TxtSaveOptions txtOptions = new TxtSaveOptions
        {
            // This limits the output to 5 digits that matter, rounding the rest
            SignificantDigits = 5
        };
```

> **شرح:** `SignificantDigits = 5` يعني أن المُصدّر سيحتفظ بأهم خمسة أرقام لأي عدد، بغض النظر عن موقع الفاصلة العشرية. إنها طريقة مفيدة لـ **set numeric precision** دون تنسيق كل خلية يدويًا.

---

## الخطوة 3: حفظ المصنف كملف نصي عادي

مع وجود المصنف والخيارات جاهزة، نقوم أخيرًا بـ **export Excel to txt**. طريقة `Save` تأخذ مسار الملف وكائن الخيارات الذي قمنا بتكوينه.

```csharp
        // Step 3: Write the workbook out as a TXT file using our precision settings
        string outputPath = @"C:\Temp\numbers.txt";
        workbook.Save(outputPath, txtOptions);

        System.Console.WriteLine($"Workbook exported to {outputPath} with 5 significant digits.");
    }
}
```

تشغيل البرنامج ينتج ملفًا يبدو هكذا:

```
12346
0.00012346
3.1416
```

لاحظ كيف أن كل رقم يحترم قاعدة **limit significant digits** التي وضعناها سابقًا.

---

## الخطوة 4: التحقق من النتيجة (اختياري لكن موصى به)

من السهل فتح الملف `numbers.txt` المُنشأ في أي محرر، لكن قد ترغب في أتمتة خطوة التحقق، خاصة في خطوط CI.

```csharp
        // Quick verification – read back the file and print each line
        foreach (var line in System.IO.File.ReadAllLines(outputPath))
        {
            System.Console.WriteLine($"Line: {line}");
        }
```

إذا أظهر الطرفية الثلاثة أسطر أعلاه، فقد نجحت في **set significant digits** وعمل التصدير كما هو مقصود.

---

## الأخطاء الشائعة وكيفية تجنّبها

| المشكلة | لماذا يحدث | الحل |
|-------|----------------|-----|
| الأرقام تظهر بعدد كبير من الأرقام العشرية | `SignificantDigits` تُركت على القيمة الافتراضية (0) | قم بتعيين `SignificantDigits` صراحةً إلى العدد المطلوب |
| تم إنشاء ملف فارغ | المصنف لم يتلق أي بيانات قبل الحفظ | املأ الخلايا **قبل** استدعاء `Save` |
| مسار الملف يثير استثناء `UnauthorizedAccessException` | محاولة الكتابة إلى مجلد محمي | استخدم مجلدًا لديك صلاحية كتابة فيه (مثل `C:\Temp` أو `%USERPROFILE%\Documents`) |
| الدقة تبدو غير صحيحة للأعداد الصغيرة جدًا | عدد الأرقام المهمة يشمل الأصفار الأولية بعد الفاصلة | تذكر أن “significant” يتجاهل الأصفار الأولية؛ 0.000123456 مع 5 أرقام يصبح `0.00012346` |

---

## مثال كامل يعمل (جاهز للنسخ واللصق)

فيما يلي البرنامج الكامل المستقل. الصقه في مشروع وحدة تحكم جديد واضغط **Run**.

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new workbook
        Workbook workbook = new Workbook();

        // Populate with sample numbers
        Worksheet sheet = workbook.Worksheets[0];
        sheet.Cells["A1"].PutValue(12345.678901);
        sheet.Cells["A2"].PutValue(0.000123456);
        sheet.Cells["A3"].PutValue(Math.PI);

        // 2️⃣ Set up export options – limit significant digits to 5
        TxtSaveOptions txtOptions = new TxtSaveOptions
        {
            SignificantDigits = 5
        };

        // 3️⃣ Export to TXT
        string outputPath = @"C:\Temp\numbers.txt";
        workbook.Save(outputPath, txtOptions);

        Console.WriteLine($"✅ Export completed: {outputPath}");
        Console.WriteLine("🔎 Verifying content:");
        foreach (var line in System.IO.File.ReadAllLines(outputPath))
        {
            Console.WriteLine($"   {line}");
        }
    }
}
```

**مخرجات الطرفية المتوقعة**

```
✅ Export completed: C:\Temp\numbers.txt
🔎 Verifying content:
   12346
   0.00012346
   3.1416
```

وسيحتوي ملف `numbers.txt` على الثلاثة أسطر المعروضة أعلاه.

---

## الخطوات التالية: التعمق أكثر من الأساسيات

- **Export other formats** – تدعم Aspose.Cells أيضًا CSV و HTML و PDF. استبدل `TxtSaveOptions` بـ `CsvSaveOptions` أو `PdfSaveOptions` حسب الحاجة.  
- **Dynamic precision** – يمكنك حساب `SignificantDigits` أثناء التشغيل بناءً على إدخال المستخدم أو ملفات الإعداد.  
- **Multiple worksheets** – قم بالتكرار على `workbook.Worksheets` وصدر كل واحدة إلى ملف `.txt` خاص بها.  
- **Localization** – تحكم في فاصل العلامة العشرية (`.` مقابل `,`) عبر `CultureInfo` إذا كنت بحاجة لمطابقة الإعدادات الإقليمية.  

كل هذه الإضافات لا تزال تعتمد على الفكرة الأساسية التي غطيناها: **create new workbook**، تكوين التصدير، و **set numeric precision** لتتناسب مع متطلبات تقاريرك.

---

## الخلاصة

لقد أخذنا نسخة جديدة من **create new workbook**، ملأناها بالبيانات، وأظهرنا كيفية **export Excel to TXT** مع **setting significant digits** لتقليل دقة الإخراج. المثال الكامل يعمل مباشرة، والشرح غطى *السبب* وراء كل سطر حتى تتمكن من تكييفه في مشاريعك.

لا تتردد في التجربة—غيّر قيمة `SignificantDigits`، أضف المزيد من الأوراق، أو غيّر تنسيق الإخراج. إذا واجهت مشكلة، راجع وثائق Aspose.Cells أو اترك تعليقًا أدناه. برمجة سعيدة!

---

![Create new workbook example](/images/create-new-workbook.png "Screenshot showing a C# IDE with the create new workbook code")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}