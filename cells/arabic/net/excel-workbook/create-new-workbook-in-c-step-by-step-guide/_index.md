---
category: general
date: 2026-02-15
description: إنشاء دفتر عمل جديد في C# وتعلم كيفية إضافة جدول، وتفعيل الفلتر، وحفظ
  دفتر العمل بصيغة xlsx. دليل سريع وشامل لأتمتة Excel.
draft: false
keywords:
- create new workbook
- save workbook as xlsx
- how to create workbook
- how to add table
- how to enable filter
language: ar
og_description: أنشئ مصنفًا جديدًا في C# وأضف جدولًا على الفور، وقم بتبديل الفلاتر،
  ثم احفظ المصنف بصيغة xlsx. اتبع هذا الدرس المختصر والعملي.
og_title: إنشاء دفتر عمل جديد في C# – دليل برمجي شامل
tags:
- C#
- Aspose.Cells
- Excel Automation
title: إنشاء دفتر عمل جديد في C# – دليل خطوة بخطوة
url: /ar/net/excel-workbook/create-new-workbook-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء دفتر عمل جديد في C# – دليل برمجة كامل

هل احتجت يومًا إلى **إنشاء دفتر عمل جديد** في C# لكن لم تكن متأكدًا من الكائنات التي يجب التعامل معها أولًا؟ لست وحدك؛ يواجه العديد من المطورين هذه المشكلة عند أتمتة ملفات Excel. في هذا الدرس سنستعرض إنشاء دفتر عمل جديد، إدراج جدول، تشغيل الفلتر التلقائي، وأخيرًا **حفظ دفتر العمل كملف xlsx**—كل ذلك مع كود واضح يمكن تشغيله.

سنجيب أيضًا على الأسئلة المتكررة “كيفية إضافة جدول” و “كيفية تمكين الفلتر” التي تظهر عادةً بعد إنشاء دفتر العمل الأولي. في النهاية ستحصل على مثال متكامل يمكنك إدراجه في أي مشروع .NET دون أي إضافات غير ضرورية.

## المتطلبات المسبقة والإعداد

قبل أن نبدأ، تأكد من وجود ما يلي:

- **.NET 6** (أو أي نسخة حديثة من .NET) مثبتة.
- حزمة **Aspose.Cells for .NET** عبر NuGet (`Install-Package Aspose.Cells`) – هذه المكتبة توفر الفئات `Workbook`، `Worksheet`، و `ListObject` المستخدمة أدناه.
- بيئة تطوير تفضّلها (Visual Studio، VS Code، Rider – اختر ما يناسبك).

لا تحتاج إلى أي إعداد إضافي؛ الكود يعمل مباشرةً بمجرد الإشارة إلى الحزمة.

![Screenshot showing a newly created workbook in Excel – create new workbook](image.png)

*نص بديل للصورة: “لقطة شاشة لإنشاء دفتر عمل جديد في Excel”*

## الخطوة 1: إنشاء دفتر عمل جديد والوصول إلى الورقة الأولى

أول شيء تحتاج إلى القيام به هو إنشاء كائن `Workbook`. فكر في ذلك كفتح ملف Excel جديد يحتوي حاليًا على ورقة افتراضية واحدة. بعد ذلك، احصل على مرجع للورقة حتى تتمكن من ملئها.

```csharp
using Aspose.Cells;

public class WorkbookDemo
{
    public static void Main()
    {
        // Step 1: Create a new workbook (this is the "create new workbook" part)
        Workbook workbook = new Workbook();

        // Access the first worksheet – by default it is named "Sheet1"
        Worksheet worksheet = workbook.Worksheets[0];
```

**لماذا هذا مهم:** إنشاء دفتر العمل يمنحك لوحة فارغة؛ والوصول إلى الورقة الأولى يضمن وجود هدف للجدول القادم. إذا تخطيت هذه الخطوة، فإن أي استدعاء لاحق لـ `ListObject` سيتسبب في حدوث استثناء مرجع فارغ.

## الخطوة 2: كيفية إضافة جدول إلى الورقة

الآن بعد أن لدينا ورقة، لنُدرج جدولًا يمتد عبر الخلايا **A1:C5**. في Aspose.Cells تُدير مجموعة `ListObjects` الجداول (المعروفة أيضًا باسم *list objects*). إضافة جدول هي عملية من خطوتين: استدعاء `Add` لإنشائه، ثم تخزين النتيجة في متغير `ListObject` لتسهيل التعامل معه.

```csharp
        // Step 2: Add a table named "MyTable" covering the range A1:C5
        int tableIndex = worksheet.ListObjects.Add("MyTable", "A1:C5", true);
        ListObject table = worksheet.ListObjects[tableIndex];
```

**ما الذي يحدث خلف الكواليس؟** طريقة `Add` تسجل الجدول في محرك الجداول الداخلي في Excel، وتُعطيه فهرسًا فريدًا. من خلال تخزين هذا الفهرس في `tableIndex` يمكننا استرجاع كائن `ListObject` الفعلي، مما يتيح لنا التحكم الكامل في خصائص الجدول.

### نصيحة احترافية
إذا كنت تخطط لإنشاء جداول متعددة، احتفظ بفهارسها في قائمة – سيسهل ذلك تحديثها لاحقًا.

## الخطوة 3: كيفية تمكين الفلتر على الجدول

تأتي الجداول في Excel مع صف فلتر تلقائي بشكل افتراضي، لكن اعتمادًا على طريقة إنشاء الجدول قد تحتاج إلى تشغيله صراحةً. خاصية `ShowAutoFilter` تُشغّل أو تُعطّل هذا الصف.

```csharp
        // Step 3: Enable the auto‑filter for the table
        table.ShowAutoFilter = true;
```

بعد التفعيل، يمكن للمستخدمين النقر على أسهم القوائم المنسدلة في صف العنوان لتصفية الصفوف بناءً على القيم. هذا مفيد جدًا للمجموعات الكبيرة من البيانات.

### ماذا لو لا تريد الفلتر؟
ما عليك سوى ضبط `ShowAutoFilter` إلى `false` وستختفي الأسهم. السطر التالي يوضح العملية العكسية:

```csharp
        // Disable (remove) the auto‑filter
        table.ShowAutoFilter = false;
```

## الخطوة 4: حفظ دفتر العمل كملف XLSX

اكتمل كل العمل الشاق؛ الآن نقوم بحفظ دفتر العمل على القرص. طريقة `Save` تقبل مسارًا كاملاً وتحدد تنسيق الملف تلقائيًا من الامتداد. هنا نقوم صراحةً **بحفظ دفتر العمل كملف xlsx**.

```csharp
        // Step 4: Save the workbook to a file
        string outputPath = @"C:\Temp\NoFilter.xlsx"; // Change to your desired folder
        workbook.Save(outputPath);
    }
}
```

عند فتح `NoFilter.xlsx` سترى ورقة واحدة تحتوي على جدول باسم **MyTable** يغطي A1:C5، وبما أننا ضبطنا `ShowAutoFilter` إلى `false` فلن تظهر أسهم الفلتر.

### النتيجة المتوقعة
- ملف باسم `NoFilter.xlsx` موجود في المجلد الذي حددته.
- Sheet1 يحتوي على جدول مكوّن من 5 صفوف و3 أعمدة مع بيانات افتراضية (خلايا فارغة ما لم تقم بملئها).
- لا يتم عرض صف الفلتر التلقائي.

## التنويعات والحالات الخاصة

### إبقاء الفلتر مفعلاً
إذا كان سيناريوك يتطلب إبقاء الفلتر مفعلاً، ما عليك سوى حذف السطر الذي يضبط `ShowAutoFilter = false`. سيظهر الجدول مع أسهم الفلتر جاهزة لتفاعل المستخدم.

### إضافة جداول متعددة
يمكنك تكرار **الخطوة 2** بنطاقات وأسماء مختلفة:

```csharp
int secondTableIdx = worksheet.ListObjects.Add("SecondTable", "E1:G10", true);
ListObject secondTable = worksheet.ListObjects[secondTableIdx];
secondTable.ShowAutoFilter = true;
```

### تعبئة بيانات الجدول
تتيح لك Aspose.Cells كتابة القيم مباشرةً إلى الخلايا قبل أو بعد إنشاء الجدول. على سبيل المثال، لملء العمود الأول بأرقام:

```csharp
for (int i = 0; i < 5; i++)
{
    worksheet.Cells[i, 0].PutValue(i + 1); // A1‑A5 = 1‑5
}
```

### ملاحظة حول التوافق
الكود يعمل مع **Aspose.Cells 23.9** وما بعدها. إذا كنت تستخدم نسخة أقدم، قد تختلف توقيعات طريقة `Add` قليلًا—تحقق من ملاحظات الإصدار للمكتبة.

## الأخطاء الشائعة وكيفية تجنّبها

- **نسيان الإشارة إلى Aspose.Cells** – سيظهر للمُصرّف خطأ حول أنواع غير معروفة. تأكد من تثبيت حزمة NuGet وإضافة `using Aspose.Cells;` في أعلى الملف.
- **سلسلة النطاق غير صحيحة** – نطاقات Excel غير حساسة لحالة الأحرف، لكنها يجب أن تكون صالحة (مثال: `"A1:C5"` وليس `"A1:C"`). أي خطأ إملائي سيسبب استثناء `CellsException`.
- **أذونات مسار الملف** – محاولة الحفظ في مجلد محمي (مثل `C:\Program Files`) ستؤدي إلى استثناء `UnauthorizedAccessException`. استخدم مجلدًا قابلًا للكتابة مثل `%TEMP%` أو مجلد ملفك الشخصي.

## مثال كامل جاهز للنسخ واللصق

```csharp
using Aspose.Cells;

public class WorkbookDemo
{
    public static void Main()
    {
        // 1️⃣ Create new workbook
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // 2️⃣ Add a table named "MyTable" covering A1:C5
        int tableIdx = worksheet.ListObjects.Add("MyTable", "A1:C5", true);
        ListObject table = worksheet.ListObjects[tableIdx];

        // 3️⃣ Enable auto‑filter (you can skip this if you don't need it)
        table.ShowAutoFilter = true;

        // OPTIONAL: Disable the filter if you don't want it visible
        // table.ShowAutoFilter = false;

        // 4️⃣ Save workbook as xlsx
        string outputPath = @"C:\Temp\NoFilter.xlsx";
        workbook.Save(outputPath);
    }
}
```

شغّل البرنامج، افتح الملف المُنشأ، وسترى النتيجة نفسها التي تم وصفها أعلاه.

## ملخص

بدأنا بـ **إنشاء دفتر عمل جديد**، ثم تعلمنا **كيفية إضافة جدول**، فعلنا خاصية **كيفية تمكين الفلتر**، وأخيرًا **حفظنا دفتر العمل كملف xlsx**. تم شرح كل خطوة مع *السبب* وراء أهميتها، وليس مجرد *ما* يجب كتابته، لتتمكن من تعديل النمط لسيناريوهات أكثر تعقيدًا.

## ما التالي؟

- **تنسيق الجدول** – استكشف `TableStyleType` لإضفاء مظهر احترافي على بياناتك.
- **إدراج صيغ** – استخدم `Cells[i, j].Formula = "=SUM(A2:A5)"` لإضافة حسابات.
- **تصدير إلى PDF** – يمكن لـ Aspose.Cells أيضًا تحويل دفتر العمل إلى PDF باستدعاء `Save` واحد.
- **قراءة دفاتر عمل موجودة** – استبدل `new Workbook()` بـ `new Workbook("ExistingFile.xlsx")` لتعديل ملفات موجودة مباشرة.

لا تتردد في تجربة هذه الأفكار، وإذا كان هناك أي شيء غير واضح أترك تعليقًا. برمجة سعيدة، واستمتع بأتمتة Excel باستخدام C#!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}