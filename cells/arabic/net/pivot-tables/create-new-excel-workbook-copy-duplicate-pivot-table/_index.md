---
category: general
date: 2026-02-09
description: أنشئ مصنف Excel جديد وتعلم كيفية نسخ جداول Pivot بسهولة. يوضح هذا الدليل
  كيفية تكرار جدول Pivot وحفظ المصنف كجديد.
draft: false
keywords:
- create new excel workbook
- how to copy pivot
- duplicate pivot table
- save workbook as new
- how to copy worksheet
language: ar
og_description: إنشاء مصنف Excel جديد في C# ونسخ جدول محوري فورًا. تعلم كيفية تكرار
  الجدول المحوري وحفظ المصنف كجديد مع مثال كامل للكود.
og_title: إنشاء مصنف إكسل جديد – نسخ الجدول المحوري خطوة بخطوة
tags:
- excel
- csharp
- aspose.cells
- automation
title: إنشاء مصنف إكسل جديد – نسخ وتكرار الجدول المحوري
url: /ar/net/pivot-tables/create-new-excel-workbook-copy-duplicate-pivot-table/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء مصنف Excel جديد – نسخ وتكرار جدول Pivot

هل احتجت يوماً إلى **إنشاء مصنف Excel جديد** يحمل جدول Pivot معقد من ملف موجود؟ لست وحدك—العديد من المطورين يواجهون هذه المشكلة عند أتمتة خطوط تقاريرهم. الخبر السار هو أنه ببضع أسطر من C# ومكتبة Aspose.Cells يمكنك **كيفية نسخ Pivot** بسرعة، **تكرار جدول Pivot**، و**حفظ المصنف كجديد** دون فتح Excel يدوياً.

في هذا الدليل سنستعرض العملية بالكامل، من تحميل المصنف المصدر إلى حفظ النسخة المكررة. في النهاية ستحصل على مقتطف جاهز للتنفيذ يمكنك إدراجه في أي مشروع .NET. لا إطالة، مجرد حل عملي يمكنك اختباره اليوم.

## ما يغطيه هذا الدرس

* **المتطلبات المسبقة** – .NET 6+ (أو .NET Framework 4.6+)، Visual Studio، وحزمة NuGet الخاصة بـ Aspose.Cells for .NET.
* كود خطوة بخطوة **ينشئ مصنف Excel جديد**، ينسخ الـ Pivot، ويكتب النتيجة إلى القرص.
* شرح **لماذا** كل سطر مهم، وليس فقط **ماذا** يفعل.
* نصائح للتعامل مع الحالات الخاصة مثل الأوراق المخفية أو نطاقات البيانات الكبيرة.
* نظرة سريعة على **كيفية نسخ ورقة العمل** إذا احتجت إلى النسخ الكامل للورقة بدلاً من الـ Pivot فقط.

هل أنت مستعد؟ لنبدأ.

![إنشاء مصنف Excel جديد توضيحي](image.png "مخطط يوضح المصنف المصدر، نسخة الـ Pivot، والمصنف الوجهة")

## الخطوة 1: إعداد المشروع وتثبيت Aspose.Cells

قبل أن نتمكن من **إنشاء مصنف Excel جديد**، نحتاج إلى مشروع يشتمل على المكتبة الصحيحة.

```csharp
// Install the Aspose.Cells package via NuGet:
//   dotnet add package Aspose.Cells
using Aspose.Cells;   // Provides Workbook, Worksheet, Range, etc.
using System;        // For basic .NET types
```

*لماذا هذا مهم:* Aspose.Cells يعمل بالكامل في الذاكرة، لذا لا تحتاج أبداً إلى تشغيل Excel على الخادم. كما أنه يحافظ على معلومات ذاكرة التخزين المؤقت للـ Pivot، وهو أمر أساسي للحصول على **تكرار جدول Pivot** حقيقي.

> **نصيحة احترافية:** إذا كنت تستهدف .NET Core، تأكد من أن معرف وقت تشغيل المشروع (RID) يتطابق مع المنصة التي ستنشر عليها؛ وإلا قد تواجه أخطاء تحميل المكتبة الأصلية.

## الخطوة 2: تحميل المصنف المصدر الذي يحتوي على الـ Pivot

الآن سنقوم بـ **كيفية نسخ Pivot** من ملف موجود. يمكن أن يكون المصنف المصدر في أي مكان على القرص، أو في تدفق (stream)، أو حتى في مصفوفة بايت.

```csharp
// Step 2: Load the source workbook that contains the pivot table
string sourcePath = @"C:\Reports\source.xlsx";
Workbook sourceWorkbook = new Workbook(sourcePath);

// Grab the first worksheet (adjust the index if your pivot lives elsewhere)
Worksheet sourceSheet = sourceWorkbook.Worksheets[0];

// Define the range that encloses the pivot table – A1:D20 in this example
Range sourceRange = sourceSheet.Cells.CreateRange("A1:D20");
```

*لماذا نختار نطاقاً:* جدول الـ Pivot يعيش داخل نطاق خلايا عادي، لكنه يحتوي أيضاً على بيانات مخفية في الذاكرة مرفقة بالورقة. بنسخ النطاق **بما يشمل الـ Pivot**، يضمن Aspose.Cells نقل الذاكرة المؤقتة معه، مما يمنحك **تكرار جدول Pivot** فعال في الملف الوجهة.

## الخطوة 3: إنشاء مصنف Excel جديد لاستقبال البيانات المنسوخة

هنا نُنشئ فعلياً **مصنف Excel جديد** سيحمل الـ Pivot المكرر.

```csharp
// Step 3: Create a fresh workbook (empty) for the destination
Workbook destinationWorkbook = new Workbook(); // Starts with a default empty sheet
Worksheet destinationSheet = destinationWorkbook.Worksheets[0];

// Destination starts at A1 – you could offset if you need space for other data
Range destinationRange = destinationSheet.Cells.CreateRange("A1");
```

> **لماذا مصنف جديد؟** البدء من صفيحة نظيفة يضمن عدم وجود تنسيقات أو كائنات مخفية قد تتداخل مع الـ Pivot المنسوخ. كما يجعل الملف الناتج أصغر حجماً، وهو أمر مفيد للمرفقات البريدية الأوتوماتيكية.

## الخطوة 4: نسخ نطاق الـ Pivot إلى المصنف الجديد

الآن نقوم بتنفيذ عملية **كيفية نسخ Pivot** الفعلية.

```csharp
// Step 4: Copy the range (including the pivot) from source to destination
sourceRange.Copy(destinationRange);
```

هذا السطر الواحد يقوم بالعمل الشاق:

* يتم نقل قيم الخلايا، الصيغ، والتنسيقات.
* يتم تكرار ذاكرة التخزين المؤقت للـ Pivot، لذا يبقى الـ Pivot الجديد فعالاً بالكامل.
* أي مراجع نسبية داخل الـ Pivot تُعدل تلقائياً لتتناسب مع الموقع الجديد.

### التعامل مع الحالات الخاصة

* **الأوراق المخفية:** إذا كانت ورقة المصدر مخفية، يظل الـ Pivot ينسخ بشكل صحيح، لكن قد ترغب في إظهار ورقة الوجهة للمستخدم:
  ```csharp
  destinationSheet.IsVisible = true;
  ```
* **مجموعات البيانات الكبيرة:** بالنسبة للنطاقات التي تتجاوز بضعة آلاف صف، فكر في استخدام `CopyTo` مع `CopyOptions` لبث العملية وتقليل الضغط على الذاكرة.

## الخطوة 5: حفظ المصنف الوجهة كملف جديد

أخيراً، نـ **حفظ المصنف كجديد** ونتحقق من النتيجة.

```csharp
// Step 5: Save the destination workbook with the duplicated pivot table
string destPath = @"C:\Reports\copied.xlsx";
destinationWorkbook.Save(destPath, SaveFormat.Xlsx);

// Quick verification – open the file manually or read a cell value
Console.WriteLine($"Workbook saved to {destPath}");
```

إذا فتحت `copied.xlsx` ستجد نسخة مطابقة تماماً للـ Pivot الأصلي، جاهزة لمزيد من المعالجة أو التوزيع.

### اختياري: كيفية نسخ ورقة العمل بدلاً من الـ Pivot فقط

أحياناً قد تحتاج إلى نسخ الورقة بالكامل، ليس فقط الـ Pivot. نفس الـ API يجعل ذلك سهلًا:

```csharp
// Copy the whole worksheet (including all charts, tables, etc.)
sourceSheet.CopyTo(destinationWorkbook, 0); // Inserts at index 0
destinationWorkbook.Save(@"C:\Reports\full_copy.xlsx");
```

هذا يلبي استفسار **كيفية نسخ ورقة العمل** ويمكن أن يكون مفيدًا عندما تحتاج إلى الحفاظ على إعدادات الورقة على مستوى أعلى.

## مثال كامل يعمل

نجمع كل ما سبق في تطبيق console مستقل يمكنك تجميعه وتشغيله:

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // 1️⃣ Load source workbook
        string sourcePath = @"C:\Reports\source.xlsx";
        Workbook sourceWorkbook = new Workbook(sourcePath);
        Worksheet sourceSheet = sourceWorkbook.Worksheets[0];
        Range sourceRange = sourceSheet.Cells.CreateRange("A1:D20");

        // 2️⃣ Create destination workbook
        Workbook destinationWorkbook = new Workbook();
        Worksheet destinationSheet = destinationWorkbook.Worksheets[0];
        Range destinationRange = destinationSheet.Cells.CreateRange("A1");

        // 3️⃣ Copy the pivot (range)
        sourceRange.Copy(destinationRange);

        // 4️⃣ Save as new file
        string destPath = @"C:\Reports\copied.xlsx";
        destinationWorkbook.Save(destPath, SaveFormat.Xlsx);

        Console.WriteLine($"✅ Successfully created new Excel workbook with duplicated pivot table at {destPath}");
    }
}
```

**الناتج المتوقع:** يطبع الـ console رسالة نجاح، وتظهر `copied.xlsx` في `C:\Reports` مع Pivot فعال مطابق للـ Pivot الموجود في `source.xlsx`.

## أسئلة شائعة ومخاطر محتملة

* **هل ستتعطل الصيغ داخل الـ Pivot؟** لا—لأن ذاكرة التخزين المؤقت للـ Pivot تنتقل مع النطاق، جميع الحقول المحسوبة تبقى سليمة.
* **ماذا لو كان الـ Pivot المصدر يستخدم اتصالات بيانات خارجية؟** تلك الاتصالات *لا* تُنسخ. ستحتاج إلى إعادة إنشائها في المصنف الوجهة أو تحويل الـ Pivot إلى جدول ثابت أولاً.
* **هل يمكنني نسخ عدة Pivot في آن واحد؟** بالتأكيد—ما عليك سوى تعريف نطاق أكبر يضم جميع الـ Pivot، أو التكرار عبر كل كائن `PivotTable` في `sourceSheet.PivotTables` ونسخه بشكل منفصل.
* **هل يجب أن أفرغ كائنات `Workbook`؟** هي تنفذ `IDisposable`، لذا من المستحسن وضعها داخل عبارات `using`، خاصة في الخدمات ذات الحمل العالي.

## الخلاصة

الآن تعرف **كيفية إنشاء مصنف Excel جديد**، نسخ Pivot، **تكرار جدول Pivot**، و**حفظ المصنف كجديد** باستخدام C# و Aspose.Cells. الخطوات بسيطة: تحميل، إنشاء، نسخ، وحفظ. مع المقتطف الاختياري **كيفية نسخ ورقة العمل** لديك أيضاً خيار لتكرار الورقة بالكامل.

ما يمكنك استكشافه لاحقًا:

* إضافة تنسيقات مخصصة للـ Pivot المكرر.
* تحديث ذاكرة التخزين المؤقت للـ Pivot برمجياً بعد تغيّر البيانات.
* تصدير المصنف إلى PDF أو CSV للأنظمة المت downstream.

جرّبه، عدّل النطاق، ودع الأتمتة تتولى العمل الشاق في سير تقاريرك. Happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}