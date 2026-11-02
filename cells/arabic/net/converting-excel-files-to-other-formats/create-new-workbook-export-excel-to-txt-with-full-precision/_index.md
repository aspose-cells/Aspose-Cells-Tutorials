---
category: general
date: 2026-03-18
description: إنشاء مصنف جديد وتصدير Excel إلى TXT مع الحفاظ على الدقة العددية. تعلّم
  كيفية حفظ ورقة العمل كملف TXT وتحويل ورقة العمل إلى TXT بكفاءة.
draft: false
keywords:
- create new workbook
- export excel to txt
- save excel as txt
- save worksheet as txt
- convert worksheet to txt
language: ar
og_description: إنشاء مصنف جديد وتصدير Excel إلى TXT بدقة. يوضح هذا الدليل كيفية حفظ
  ورقة العمل كملف TXT وتحويل ورقة العمل إلى TXT باستخدام C#.
og_title: إنشاء دفتر عمل جديد – دليل تصدير إكسل إلى TXT
tags:
- Aspose.Cells
- C#
- Excel automation
title: إنشاء مصنف جديد – تصدير إكسل إلى TXT بدقة كاملة
url: /ar/net/converting-excel-files-to-other-formats/create-new-workbook-export-excel-to-txt-with-full-precision/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء دفتر عمل جديد – تصدير Excel إلى TXT بدقة كاملة

هل احتجت يومًا إلى **create new workbook** في C# فقط لتفريغ بعض البيانات في ملف نصي عادي؟ ربما تقوم بسحب تقرير من نظام قديم والأداة اللاحقة لا تقبل سوى تغذية `.txt`. الخبر السار؟ لا تحتاج إلى التضحية بدقة الأرقام، وبالتأكيد لا تحتاج إلى إنشاء سلاسل CSV يدوياً.

في هذا الدليل سنستعرض العملية الكاملة لـ **export excel to txt**، مع تغطية كل شيء من تهيئة دفتر العمل إلى الحفاظ على الأصفار المت trailing عندما **save worksheet as txt**. في النهاية ستحصل على مقطع جاهز للتنفيذ يمكنك إدراجه في أي مشروع .NET—دون الحاجة إلى أدوات إضافية.

## ما ستحتاجه

- **ASP.NET/ .NET 6+** (الكود يعمل على .NET Framework 4.6+ أيضًا)  
- **Aspose.Cells for .NET** – المكتبة التي تدعم الفئات `Workbook` و `Worksheet` و `TxtSaveOptions`. يمكنك الحصول عليها من NuGet باستخدام `Install-Package Aspose.Cells`.  
- فهم أساسي للغة C# (إذا كنت مرتاحًا مع عبارات `using`، فأنت جاهز للانطلاق).  

هذا كل شيء—بدون تفاعل مع Excel، بدون كائنات COM، وبالتأكيد بدون تجميع سلاسل يدوي.

---

## الخطوة 1: تهيئة دفتر عمل جديد (الكلمة المفتاحية الأساسية)

أول شيء عليك القيام به هو **create new workbook**. فكر في دفتر العمل كقماش فارغ ستلصق فيه لاحقًا الأرقام أو النصوص أو الصيغ.

```csharp
using System;
using Aspose.Cells;

namespace ExcelToTxtDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1: Create a new workbook and get the first worksheet
            Workbook workbook = new Workbook();                 // <‑‑ creates new workbook
            Worksheet worksheet = workbook.Worksheets[0];       // first sheet (index 0)
```

> **لماذا هذا مهم:** إنشاء كائن `Workbook` دون تحميل ملف يمنحك صفحة نظيفة. يمكنك بعد ذلك إضافة البيانات برمجياً، وهو مثالي لسيناريوهات **convert worksheet to txt** حيث لا يوجد لديك ملف `.xlsx` موجود.

## الخطوة 2: ملء الخلايا – الحفاظ على الأصفار المت trailing

مشكلة شائعة عند تفريغ الأرقام إلى نص هي فقدان الأصفار المت trailing (`123.45000` تصبح `123.45`). إذا كانت الأنظمة اللاحقة تعتمد على حقول ذات عرض ثابت، فإن هذا الفقدان قد يسبب فشلًا كاملًا.

```csharp
            // Step 2: Write a numeric value that contains trailing zeros
            // PutValue respects the data type; we’ll later tell the saver to keep precision.
            worksheet.Cells[0, 0].PutValue(123.45000);
```

> **نصيحة احترافية:** `PutValue` يستنتج نوع البيانات تلقائيًا. إذا كنت تحتاج إلى سلسلة تبدو كرقم، استخدم `PutValue("123.45000")` بدلاً من ذلك.

## الخطوة 3: ضبط خيارات حفظ TXT – الحفاظ على الدقة الرقمية

هنا يحدث السحر. من خلال تفعيل `PreserveNumericPrecision`، تُخبر Aspose.Cells بكتابة القيمة الدقيقة التي أدخلتها، بما في ذلك أي أصفار غير ذات معنى.

```csharp
            // Step 3: Configure TXT save options to keep the original numeric precision
            TxtSaveOptions txtSaveOptions = new TxtSaveOptions(SaveFormat.Txt)
            {
                PreserveNumericPrecision = true   // retain all digits, even trailing zeros
            };
```

> **لماذا تفعله؟** عندما **save excel as txt**، السلوك الافتراضي يزيل الكسور غير الضرورية. ضبط `PreserveNumericPrecision = true` يضمن أن يكون الناتج مطابقًا للقيمة المعروضة في الخلية، وهو أمر حيوي لتقارير المالية أو البيانات العلمية.

## الخطوة 4: حفظ الورقة كملف TXT – التصدير النهائي

الآن نقوم فعليًا بـ **save worksheet as txt**. يمكنك تحديد المسار في أي مكان لديك صلاحية كتابة؛ المثال يستخدم مجلدًا نسبيًا يُدعى `output`.

```csharp
            // Step 4: Save the worksheet as a TXT file using the configured options
            string outputPath = "output/num-preserve.txt";
            worksheet.Save(outputPath, txtSaveOptions);

            Console.WriteLine($"File saved to {outputPath}");
        }
    }
}
```

> **الناتج المتوقع** (`num-preserve.txt`):

```
123.45000
```

لاحظ أن الأصفار المت trailing لا تزال موجودة—بالضبط ما طلبته.

## الخطوة 5: التحقق من النتيجة – فحص سريع

بعد تشغيل البرنامج، افتح `num-preserve.txt` في أي محرر نصوص. يجب أن ترى السطر الوحيد `123.45000`. إذا وجدت `123.45` بدلاً من ذلك، تحقق مرة أخرى من أن `PreserveNumericPrecision` مضبوط على `true` وأنك تستخدم نسخة حديثة من Aspose.Cells (v23.10+).

## تنوعات شائعة وحالات حافة

### تصدير خلايا أو نطاقات متعددة

إذا كنت بحاجة إلى **export excel to txt** لنطاق كامل، ما عليك سوى ملء المزيد من الخلايا قبل الحفظ:

```csharp
worksheet.Cells["A1"].PutValue(100);
worksheet.Cells["A2"].PutValue(200.500);
worksheet.Cells["A3"].PutValue(300.00);
```

ستقوم Aspose بكتابة كل خلية في سطر جديد افتراضيًا. يمكنك أيضًا تغيير الفاصل (علامة تبويب، فاصلة) عبر `txtSaveOptions.Separator`.

### تحويل الورقة إلى TXT بترميزات مختلفة

أحيانًا تتطلب الأنظمة اللاحقة ترميز UTF‑8 BOM أو ASCII. اضبط الترميز هكذا:

```csharp
txtSaveOptions.Encoding = System.Text.Encoding.UTF8;
```

### التعامل مع دفاتر عمل كبيرة

عند التعامل مع أوراق ضخمة (مئات الآلاف من الصفوف)، فكر في تدفق الإخراج:

```csharp
txtSaveOptions.EnableCache = true; // writes data in chunks to reduce memory footprint
```

## نصائح احترافية وملاحظات

- **لا تنس إنشاء دليل الإخراج** قبل استدعاء `Save`، وإلا ستحصل على `DirectoryNotFoundException`.  
- **احذر الفواصل العشرية الخاصة بالموقع**. إذا كان بيئتك تستخدم الفواصل (`,`) مثل `1,23`، اضبط `txtSaveOptions.DecimalSeparator = '.'` لفرض النقطة.  
- **توافق الإصدارات**: تم تقديم علم `PreserveNumericPrecision` في Aspose.Cells 20.6. إذا كنت تستخدم إصدارًا أقدم، فلن يكون هذا العلم موجودًا وستحتاج إلى تنسيق الخلية كنص قبل الحفظ.

![إنشاء دفتر عمل جديد مثال](excel-to-txt.png "إنشاء دفتر عمل جديد")

*نص بديل للصورة: "إنشاء دفتر عمل جديد وتصدير Excel إلى TXT مع الحفاظ على الدقة الرقمية"*

## ملخص – ما تم تغطيته

- **Create new workbook** باستخدام Aspose.Cells.  
- ملء خلية برقم يتضمن أصفارًا مت trailing.  
- ضبط `TxtSaveOptions.PreserveNumericPrecision = true` لـ **save excel as txt** دون فقدان الدقة.  
- كتابة الملف إلى القرص، مع التحقق من أن الناتج يطابق القيمة الأصلية.  

## الخطوات التالية والمواضيع ذات الصلة

الآن بعد أن يمكنك **export excel to txt** بدقة مثالية، قد ترغب في استكشاف:

- **Exporting to CSV** باستخدام فواصل مخصصة (`TxtSaveOptions.Separator`).  
- **Saving as other plain‑text formats** مثل TSV (`SaveFormat.TabDelimited`).  
- **Batch processing** لعدة دفاتر عمل في مجلد باستخدام `Directory.GetFiles`.  
- **Integrating with Azure Functions** للتحويل حسب الطلب في السحابة.  

كل من هذه يبني على نمط `Workbook` → `Worksheet` → `TxtSaveOptions` نفسه، لذا ستشعر بالراحة.

### فكرة نهائية

إذا تابعت الخطوات، فأنت الآن تعرف بالضبط كيف **create new workbook**، وتملأه، و**save worksheet as txt** مع الحفاظ على كل رقم عشري يهمك. إنها قطعة صغيرة من الكود، لكنها تحل مشكلة شائعة بشكل مفاجئ عندما تتطلب خطوط الأنابيب القديمة مدخلات نصية عادية.

جرّبها، عدّل الخيارات، ودع البيانات تتدفق بالضبط كما تحتاج. برمجة سعيدة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}