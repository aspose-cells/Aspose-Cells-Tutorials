---
category: general
date: 2026-02-09
description: كيفية إنشاء مصفوفة في Excel باستخدام C# موضحة في دقائق – تعلم توليد أرقام
  متسلسلة، واستخدام COT، وحفظ المصنف كملف XLSX.
draft: false
keywords:
- how to create array
- create excel workbook c#
- generate sequence numbers
- save workbook as xlsx
- how to use cot
language: ar
og_description: كيفية إنشاء مصفوفة في Excel باستخدام C# مغطاة خطوة بخطوة، بما في ذلك
  توليد أرقام تسلسلية، واستخدام COT، وحفظ المصنف كملف XLSX.
og_title: كيفية إنشاء مصفوفة في إكسل باستخدام C# – دليل سريع
tags:
- C#
- Excel
- Aspose.Cells
title: كيفية إنشاء مصفوفة في Excel باستخدام C# – دليل خطوة بخطوة
url: /ar/net/data-manipulation/how-to-create-array-in-excel-with-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية إنشاء مصفوفة في Excel باستخدام C# – دليل خطوة بخطوة

هل تساءلت يومًا **how to create array** في Excel باستخدام C# دون قضاء ساعات في البحث في الوثائق؟ لست وحدك. يواجه العديد من المطورين صعوبة عندما يحتاجون إلى نطاق تفريغ ديناميكي، أو قيمة مثلثية سريعة، أو ببساطة ملف XLSX نظيف يُحفظ على القرص. في هذا الدرس سنحل هذه المشكلة فورًا — من خلال بناء دفتر عمل صغير يكتب صيغة مصفوفة متوسعة، ويضيف حساب الظل المقلوب (cotangent)، ويحفظ كل شيء كملف XLSX.  

سنضيف أيضًا بعض الحيل الإضافية: توليد أرقام تسلسلية، إتقان دالة `COT`، والتأكد من أن الملف يُحفظ في المكان الذي تريده. في النهاية ستحصل على مقتطف قابل لإعادة الاستخدام يمكنك إدراجه في أي مشروع .NET. لا إطالة، فقط كود يعمل.

> **نصيحة احترافية:** يستخدم المثال مكتبة **Aspose.Cells** الشهيرة، لكن المفاهيم قابلة للترجمة إلى حزم أتمتة Excel الأخرى (EPPlus, ClosedXML) مع تغييرات طفيفة فقط.

---

## ما ستحتاجه

- **.NET 6** أو أحدث (الكود يُجمّع على .NET Framework 4.7+ أيضًا)  
- **Aspose.Cells for .NET** – يمكنك الحصول عليها من NuGet (`Install-Package Aspose.Cells`)  
- محرر نصوص أو بيئة تطوير (Visual Studio, Rider, VS Code…)  
- صلاحية كتابة إلى المجلد الذي سيُحفظ فيه ملف الإخراج  

هذا كل شيء — لا إعدادات إضافية، لا تفاعل COM، فقط تجميع مُدار نظيف.

## الخطوة 1: How to create array in Excel – تهيئة دفتر العمل

أول شيء عندما تريد **how to create array** في ورقة Excel هو إنشاء كائن دفتر عمل. فكر في دفتر العمل كقماش فارغ؛ ورقة العمل هي المكان الذي سترسم فيه صيغك.

```csharp
using Aspose.Cells;

public class ExcelArrayDemo
{
    public static void Main()
    {
        // Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();               // <- fresh workbook
        Worksheet worksheet = workbook.Worksheets[0];    // first (and only) sheet

        // The rest of the steps follow...
```

لماذا نستخدم `Workbook()` بدون معلمات؟ يمنحك دفتر عمل في الذاكرة مع ورقة افتراضية، وهو مثالي للمهام البرمجية السريعة. إذا كنت بحاجة لفتح ملف موجود، ما عليك سوى تمرير مسار الملف إلى المُنشئ.

## الخطوة 2: توليد أرقام تسلسلية باستخدام EXPAND و SEQUENCE

الآن بعد أن لدينا ورقة، دعنا نجيب على جزء **generate sequence numbers** من اللغز. تسمح لنا وظائف المصفوفة الديناميكية الجديدة في Excel (`SEQUENCE`, `EXPAND`) بإنشاء قائمة عمودية مكوّنة من 3 صفوف وتفريغها تلقائيًا إلى نطاق 3 × 5.

```csharp
        // Write a dynamic array formula that expands a 3‑row sequence into a 3×5 spill range
        // EXPAND pads the result to 5 columns, SEQUENCE generates numbers 1‑3 vertically
        worksheet.Cells["A1"].Formula = "=EXPAND(SEQUENCE(3,1,1,1),5,1)";
```

**ما الذي يحدث هنا؟**  
- `SEQUENCE(3,1,1,1)` → ينتج مصفوفة عمودية `{1;2;3}`.  
- `EXPAND(...,5,1)` → يأخذ ذلك العمود المكوّن من ثلاثة صفوف ويمده إلى خمسة أعمدة، ملء الخلايا الإضافية بالفراغات.  

عند فتح ملف `output.xlsx` الناتج، سترى كتلة 3 × 5 تبدأ من **A1** حيث يحتوي العمود الأول على 1، 2، 3 والأعمدة الأربعة المتبقية فارغة. هذه التقنية هي العمود الفقري لنطاقات التفريغ بنمط **how to create array** دون كتابة كل خلية يدويًا.

## الخطوة 3: How to use COT – إضافة صيغة مثلثية

إذا كنت أيضًا فضوليًا حول **how to use cot** داخل صيغة Excel، فإن دالة `COT` طريقة مفيدة للحصول على ظل الزاوية المقلوب لزاوية معبرًا عنها بالراديان. لنحسب `cot(π/4)`، والتي يجب أن تُعطي **1**.

```csharp
        // Write a simple trigonometric formula that calculates cotangent of 45° (π/4)
        // COT(π/4) evaluates to 1
        worksheet.Cells["B1"].Formula = "=COT(PI()/4)";
```

لاحظ أننا استخدمنا `PI()` للحصول على قيمة الراديان للـ 180°، ثم قسمناها على 4 للوصول إلى 45°. Excel يقوم بالمعالجة، وستظهر القيمة `1` في الخلية **B1** بمجرد فتح دفتر العمل. هذا يوضح **how to use cot** للحسابات الهندسية أو المالية السريعة دون الحاجة إلى مكتبة رياضية منفصلة.

## الخطوة 4: حفظ دفتر العمل كـ XLSX – حفظ الملف

كل المتعة في إنشاء مصفوفة وإدراج صيغ تضيع إذا لم تقم بكتابة الملف إلى القرص. إليك الطريقة المبسطة لـ **save workbook as xlsx** باستخدام Aspose.Cells:

```csharp
        // Save the workbook to verify the formulas (optional)
        string outputPath = @"C:\Temp\output.xlsx";   // adjust to your folder
        workbook.Save(outputPath, SaveFormat.Xlsx);

        // Let the user know we’re done
        System.Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

لماذا نحدد `SaveFormat.Xlsx`؟ لأنه يضمن تنسيق OpenXML الحديث، القابل للقراءة عالميًا (Excel، LibreOffice، Google Sheets). إذا كنت بحاجة إلى ملف `.xls` أقدم، فقط استبدل الـ enum.

## مثال كامل يعمل (جميع الخطوات مجمعة)

فيما يلي البرنامج الكامل الجاهز للتنفيذ. انسخه والصقه في مشروع وحدة تحكم، استعد حزمة Aspose.Cells من NuGet، واضغط **F5**.

```csharp
using Aspose.Cells;

public class ExcelArrayDemo
{
    public static void Main()
    {
        // Step 1: Initialize workbook and worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Step 2: Create a dynamic spill range (how to create array)
        worksheet.Cells["A1"].Formula = "=EXPAND(SEQUENCE(3,1,1,1),5,1)";

        // Step 3: Calculate cotangent (how to use cot)
        worksheet.Cells["B1"].Formula = "=COT(PI()/4)";

        // Step 4: Persist the file (save workbook as xlsx)
        string outputPath = @"C:\Temp\output.xlsx";
        workbook.Save(outputPath, SaveFormat.Xlsx);

        System.Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

**النتيجة المتوقعة** بعد فتح `output.xlsx`:

| A | B | C | D | E |
|---|---|---|---|---|
| 1 | 1 |   |   |   |
| 2 |   |   |   |   |
| 3 |   |   |   |   |

- العمود A يُظهر الأرقام 1‑3 التي تم توليدها بواسطة `SEQUENCE`.  
- العمود B يحتوي على القيمة **1** من صيغة `COT`.  
- الأعمدة C‑E فارغة، توضح تأثير التوسيع باستخدام `EXPAND`.

## أسئلة شائعة وحالات خاصة

### ماذا لو احتجت إلى المزيد من الصفوف أو الأعمدة؟

فقط عدّل معاملات `SEQUENCE` و `EXPAND`.  
- `SEQUENCE(10,2,5,2)` سيعطي مصفوفة 10‑صفوف × 2‑أعمدة تبدأ من 5 وتزداد بمقدار 2.  
- `EXPAND(...,10,5)` سيضيف مساحة للنتيجة لتصبح 10 أعمدة و5 صفوف.

### هل يعمل هذا مع إصدارات Excel القديمة؟

وظائف المصفوفة الديناميكية (`SEQUENCE`, `EXPAND`) تتطلب Excel 365 أو 2019+. بالنسبة للملفات القديمة، يمكنك الرجوع إلى الصيغ الكلاسيكية أو كتابة القيم مباشرة عبر `Cells[row, col].PutValue(value)`.

### هل يمكنني كتابة الصيغة بنمط R1C1؟

بالطبع. استبدل `A1` بـ `Cells[0, 0]` واستخدم خاصية `FormulaR1C1`:

```csharp
worksheet.Cells[0, 0].FormulaR1C1 = "=EXPAND(SEQUENCE(3,1,1,1),5,1)";
```

### ماذا عن الفواصل العشرية الخاصة بالثقافة؟

Aspose.Cells يحترم إعدادات اللغة للدفتر. إذا كنت بحاجة إلى ثقافة محددة، اضبط `workbook.Settings.CultureInfo = new System.Globalization.CultureInfo("en-US");` قبل كتابة الصيغ.

## ملخص بصري

![كيفية إنشاء مصفوفة في Excel باستخدام C#](/images/how-to-create-array-excel-csharp.png "كيفية إنشاء مصفوفة في Excel باستخدام C#")

*تُظهر لقطة الشاشة نطاق التفريغ النهائي ونتيجة الظل المقلوب.*

## الخلاصة

ها قد حصلت على ذلك — **how to create array** في Excel باستخدام C# من الصفر، توليد أرقام تسلسلية، استغلال دالة `COT`، و **save workbook as XLSX** في برنامج واحد مرتب. النقاط الرئيسية هي:

1. استخدم كائنات `Workbook` و `Worksheet` لبدء أتمتة Excel.  
2. استفد من وظائف المصفوفة الديناميكية (`SEQUENCE`, `EXPAND`) للحصول على نطاقات تفريغ مرنة.  
3. أدخل الدوال المثلثية مثل `COT` للرياضيات السريعة دون مكتبات إضافية.  
4. احفظ النتيجة باستخدام `SaveFormat.Xlsx` للحصول على ملف قابل للقراءة عالميًا.

هل أنت مستعد للخطوة التالية؟ جرّب استبدال `COT(PI()/4)`

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}