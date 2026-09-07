---
category: general
date: 2026-02-15
description: إنشاء دليل C# لإنشاء مصنف Excel يوضح كيفية إضافة خاصية مخصصة، حفظ المصنف
  بصيغة XLSB، واسترجاع قيمة الخاصية—كل ذلك في بضع أسطر من الشيفرة.
draft: false
keywords:
- create excel workbook c#
- save workbook as xlsb
- retrieve custom property value
- add custom property excel
language: ar
og_description: إنشاء دفتر عمل Excel باستخدام C# خطوة بخطوة. تعلم كيفية إضافة خاصية
  مخصصة، حفظ دفتر العمل بصيغة XLSB، واسترجاع قيمة الخاصية مع أمثلة شفرة واضحة.
og_title: إنشاء مصنف إكسل C# – إضافة خاصية مخصصة وحفظ بصيغة XLSB
tags:
- Aspose.Cells
- C#
- Excel Automation
title: إنشاء مصنف إكسل C# – إضافة خاصية مخصصة وحفظ بصيغة XLSB
url: /ar/net/document-properties/create-excel-workbook-c-add-custom-property-save-xlsb/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء دفتر عمل Excel C# – إضافة خاصية مخصصة وحفظ XLSB

هل تحتاج إلى **إنشاء دفتر عمل Excel C#** وإدراج بعض البيانات الوصفية المخصصة؟ في هذا الدليل سنستعرض إضافة خاصية مخصصة، **حفظ دفتر العمل كـ XLSB**، ثم **استرجاع قيمة الخاصية المخصصة**—كل ذلك باستخدام كود مختصر وجاهز للتنفيذ.  

إذا تساءلت يومًا لماذا قد يحتاج جدول بيانات إلى بيانات إضافية غير مرئية في الخلايا، فأنت في المكان الصحيح. فكر في الخصائص المخصصة كملاحظات مخفية تسافر مع الملف، مثالية لربط دفتر العمل بمعرف مشروع، علامة إصدار، أو أي مفتاح تجاري آخر.

## ما ستتعلمه

- كيفية إنشاء دفتر عمل جديد باستخدام Aspose.Cells for .NET.  
- الخطوات الدقيقة **لإضافة خاصية مخصصة** بأسلوب Excel، باستخدام مجموعة `CustomProperties`.  
- حفظ دفتر العمل بصيغة الـ XLSB الثنائية المدمجة.  
- تحميل الملف مرة أخرى واستخراج الخاصية المخزنة.  

لا ملفات إعدادات خارجية، ولا حيل غامضة—فقط C# صريح يمكنك لصقه في تطبيق Console ومشاهدة النتيجة. المتطلب الوحيد هو الإشارة إلى مكتبة Aspose.Cells (نسخة تجريبية مجانية أو مرخصة).  

لماذا يهمك ذلك؟ لأن تضمين المعرفات مباشرةً في الملف يلغي الحاجة إلى استعلام قاعدة بيانات منفصلة عند فتح دفتر العمل لاحقًا. إنها عادة صغيرة يمكن أن توفر ساعات من تصحيح الأخطاء في حلول التقارير على نطاق واسع.

---

![مثال إنشاء دفتر عمل Excel C#](https://example.com/images/create-excel-workbook-csharp.png "مثال إنشاء دفتر عمل Excel C#")

*الصورة تُظهر مشروع Console بسيط بلغة C# ينشئ دفتر عمل Excel، يضيف خاصية مخصصة، ويحفظه كـ XLSB.*

## الخطوة 1: تهيئة Workbook وإضافة خاصية مخصصة

أول شيء تحتاجه هو كائن `Workbook` جديد. بمجرد حصولك عليه، تعطيك مجموعة `Worksheets[0].CustomProperties` مكانًا نظيفًا لتخزين أزواج المفتاح/القيمة.

```csharp
using Aspose.Cells;

namespace ExcelCustomPropDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1 – Create a new workbook instance
            Workbook workbook = new Workbook();

            // Step 2 – Add a custom property named "ProjectId" with a numeric value
            // This is the "add custom property excel" part of the tutorial.
            workbook.Worksheets[0].CustomProperties.Add("ProjectId", 12345);
```

**لماذا هذا مهم:**  
- `Workbook()` ينشئ تمثيلًا في الذاكرة لملف Excel، دون أي عمليات I/O على القرص بعد.  
- إضافة الخاصية إلى *الورقة الأولى* (الفهرس 0) تضمن تخزينها على مستوى دفتر العمل، مما يجعلها متاحة بغض النظر عن الورقة التي يراها المستخدم.  

> **نصيحة احترافية:** يمكن للخصائص المخصصة أن تحمل سلاسل نصية، أرقام، تواريخ، أو حتى قيم منطقية. اختر النوع الذي يتناسب مع البيانات التي تنوي تخزينها.

## الخطوة 2: حفظ دفتر العمل كـ XLSB

XLSB (Excel Binary Workbook) هي صيغة مدمجة وسريعة التحميل—مثالية لمجموعات البيانات الكبيرة. طريقة `Save` تأخذ مسار الملف وتعداد `SaveFormat`.

```csharp
            // Step 3 – Save the workbook to disk in XLSB format
            string outputPath = @"C:\Temp\CustomProp.xlsb";
            workbook.Save(outputPath, SaveFormat.Xlsb);

            // At this point the file on disk already contains the custom property.
```

**لماذا نستخدم XLSB؟**  
- يقلل حجم الملف بنسبة تصل إلى 70 % مقارنةً بصيغة XLSX التقليدية.  
- التخزين الثنائي يسرّع عمليات الكتابة والقراءة، وهو مفيد لأتمتة الخوادم.

## الخطوة 3: تحميل دفتر العمل المحفوظ واسترجاع الخاصية

الآن نقلب السيناريو: نفتح الملف الذي كتبناه للتو ونستخرج القيمة المخفية. هذا يوضح أن الخاصية نجت من جولة الإرسال والاستقبال.

```csharp
            // Step 4 – Load the workbook we just saved
            Workbook loadedWorkbook = new Workbook(outputPath);

            // Step 5 – Retrieve the value of the "ProjectId" custom property
            object projectIdValue = loadedWorkbook.Worksheets[0]
                                                .CustomProperties["ProjectId"]
                                                .Value;

            // Display the retrieved value
            System.Console.WriteLine($"Retrieved ProjectId: {projectIdValue}");
        }
    }
}
```

**ما يجب أن تراه:**  
```
Retrieved ProjectId: 12345
```

إذا كان اسم الخاصية مكتوبًا بشكل خاطئ أو غير موجود، فإن الفهرس `CustomProperties` يرمي استثناء `KeyNotFoundException`. نهج دفاعي قد يكون:

```csharp
if (loadedWorkbook.Worksheets[0].CustomProperties.Contains("ProjectId"))
{
    // safe to read
}
```

## مثال كامل يعمل (جميع الخطوات مجمعة)

فيما يلي البرنامج الكامل، جاهز للنسخ واللصق في مشروع Console جديد. لا حاجة لأي بنية إضافية.

```csharp
using Aspose.Cells;
using System;

namespace ExcelCustomPropDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Create a new workbook
            Workbook workbook = new Workbook();

            // 2️⃣ Add a custom property named "ProjectId" (add custom property excel)
            workbook.Worksheets[0].CustomProperties.Add("ProjectId", 12345);

            // 3️⃣ Save the workbook as XLSB (save workbook as xlsb)
            string filePath = @"C:\Temp\CustomProp.xlsb";
            workbook.Save(filePath, SaveFormat.Xlsb);

            // 4️⃣ Load the saved workbook back into memory
            Workbook loaded = new Workbook(filePath);

            // 5️⃣ Retrieve the custom property value (retrieve custom property value)
            object retrieved = loaded.Worksheets[0].CustomProperties["ProjectId"].Value;
            Console.WriteLine($"Retrieved ProjectId: {retrieved}");
        }
    }
}
```

شغّل البرنامج، افتح `C:\Temp\CustomProp.xlsb` في Excel، وستلاحظ عدم وجود شيء غير عادي على السطح—لأن الخصائص المخصصة مخفية بطبيعتها. ومع ذلك، البيانات موجودة هناك، جاهزة لأي عملية لاحقة.

## حالات خاصة وتنوعات

| الحالة | ما الذي يجب تعديله |
|-----------|----------------|
| **أوراق عمل متعددة** | أضف الخاصية إلى أي ورقة؛ سيتم تكرارها على مستوى دفتر العمل. |
| **خاصية نصية** | `CustomProperties.Add("Status", "Approved")` – يعمل بنفس الطريقة. |
| **خاصية مفقودة** | استخدم `Contains` قبل الفهرسة لتجنب الاستثناءات. |
| **معرفات رقمية كبيرة** | احفظها كـ `long` أو `string` لتجنب الفيض. |
| **متعدد المنصات** | Aspose.Cells يعمل على .NET Core، .NET Framework، وحتى Mono، لذا يمكن تشغيل نفس الكود داخل حاويات Linux. |

## الأسئلة المتكررة

**س: هل يعمل هذا مع نسخة Aspose.Cells التجريبية المجانية؟**  
ج: نعم. النسخة التجريبية تدعم بالكامل `CustomProperties` وحفظ XLSB؛ فقط تذكر وجود العلامة المائية على ملف الإخراج.

**س: هل يمكنني عرض الخصائص المخصصة داخل Excel؟**  
ج: في Excel، انتقل إلى *ملف → معلومات → خصائص → خصائص متقدمة → مخصص*. سيظهر “ProjectId” الخاص بك هناك.

**س: ماذا لو أردت حذف خاصية؟**  
ج: استدعِ `CustomProperties.Remove("ProjectId")` قبل الحفظ.

## الخلاصة

أنت الآن تعرف كيف **تنشئ دفتر عمل Excel C#**، تضيف خاصية مخصصة، **تحفظ دفتر العمل كـ XLSB**، وتسترجع لاحقًا **قيمة الخاصية المخصصة**. تدفق العمل كله يندمج في طريقة واحدة، مما يجعل دمجه في خطوط تقارير أكبر أو خدمات توليد مستندات أمرًا سهلًا.

### ما التالي؟

- استكشف **إضافة خصائص مخصصة متعددة** للإصدار، المؤلف، أو رموز الأقسام.  
- اجمع هذه التقنية مع **بيانات على مستوى الخلايا** لبناء تقارير ذات وصف ذاتي.  
- ابحث عن **قراءة الخصائص المخصصة** من ملفات XLSX تابعة لأطراف ثالثة—Aspose.Cells يتعامل معها أيضًا.

لا تتردد في تعديل المثال، استبدال المعرف الرقمي بـ GUID، أو تجربة صيغ ملفات مختلفة. الـ API بسيط؛ القوة الحقيقية تكمن في كيفية استخدامك للبيانات الوصفية المخفية في منطق عملك.

برمجة سعيدة! 🚀

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}