---
category: general
date: 2026-03-22
description: إنشاء مصنف Excel، إضافة خصائص مخصصة، تعيين اسم ورقة العمل، وحفظه كملف
  ثنائي XLSB باستخدام C#.
draft: false
keywords:
- create excel workbook
- add custom properties
- save as xlsb
- set worksheet name
- write binary excel file
language: ar
og_description: إنشاء مصنف Excel، إضافة خصائص مخصصة، تعيين اسم ورقة العمل، وحفظه كملف
  ثنائي XLSB باستخدام C#.
og_title: إنشاء مصنف إكسل – إضافة خصائص مخصصة وحفظه كملف XLSB
tags:
- C#
- Aspose.Cells
- Excel automation
title: إنشاء مصنف إكسل – إضافة خصائص مخصصة وحفظه كملف XLSB
url: /ar/net/document-properties/create-excel-workbook-add-custom-properties-and-save-as-xlsb/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء مصنف Excel – إضافة خصائص مخصصة وحفظه كـ XLSB

هل احتجت يومًا إلى **إنشاء مصنف Excel** برمجيًا مع الحفاظ على بعض البيانات الوصفية المرفقة؟ ربما تقوم ببناء محرك تقارير يضع معرف التقرير، اسم المؤلف، أو رقم الإصدار على كل ملف. في هذه الحالة، سيوفر لك تعلم كيفية **إضافة خصائص مخصصة** أثناء **تعيين اسم ورقة العمل** وأخيرًا **حفظه كـ XLSB** الكثير من المعالجة اليدوية بعد الإنشاء.

في هذا الدرس سنستعرض مثالًا كاملاً وقابلًا للتنفيذ يوضح بالضبط كيفية **كتابة ملف Excel ثنائي** باستخدام C#. ستتعرف على سبب كون صيغة XLSB الخيار المناسب لنقل الخصائص المخصصة، وكيفية تجنب أكثر الأخطاء شيوعًا، وما يجب فعله إذا كنت بحاجة لدعم إصدارات Excel أقدم.

---

## ما ستحتاجه

- **.NET 6+** (أو .NET Framework 4.6+). يعمل الكود على أي بيئة تشغيل حديثة.
- **Aspose.Cells for .NET** (نسخة تجريبية مجانية أو مرخصة). توفر الفئات `Workbook`، `Worksheet`، و `CustomProperties` المستخدمة أدناه.
- بيئة تطوير مريحة لك – Visual Studio، Rider، أو حتى VS Code تكفي.
- صلاحية كتابة إلى مجلد سيتم حفظ الملف المُولَّد فيه.

لا توجد مكتبات طرف ثالث أخرى مطلوبة.

---

## الخطوة 1: تثبيت Aspose.Cells

للبدء، أضف حزمة NuGet الخاصة بـ Aspose.Cells إلى مشروعك:

```bash
dotnet add package Aspose.Cells
```

> **نصيحة احترافية:** إذا كنت تعمل على خادم CI، احفظ مفتاح الترخيص في متغيّر بيئي وحمّله وقت التشغيل – هذا يمنع ظهور علامة “evaluation” على المخرجات.

---

## الخطوة 2: إنشاء مصنف Excel – نظرة عامة

الإجراء الحقيقي الأول هو **إنشاء مصنف Excel**. هذا الكائن يمثل الملف بالكامل في الذاكرة ويمنحك الوصول إلى أوراق العمل، الأنماط، والخصائص المخصصة.

```csharp
using Aspose.Cells;

namespace ExcelDemo
{
    class Program
    {
        static void Main()
        {
            // Step 2.1: Instantiate a new workbook (empty by default)
            Workbook workbook = new Workbook();

            // The rest of the steps follow...
```

لماذا ننشئ `Workbook` جديدًا بدلاً من تحميل قالب؟ يضمن المصنف الفارغ عدم وجود أنماط مخفية أو خصائص مخصصة متبقية، وهو أمر مهم خاصةً عندما تنوي **كتابة ملف Excel ثنائي** لأنظمة لاحقة تتوقع بداية نظيفة.

---

## الخطوة 3: تعيين اسم ورقة العمل (ولماذا يهم)

تكون أسماء أوراق Excel افتراضيًا “Sheet1”، “Sheet2”، إلخ. إعطاء الورقة اسمًا ذا معنى يجعل المعالجة اللاحقة – مثل Power Query أو ماكرو VBA – أسهل كثيرًا للقراءة.

```csharp
            // Step 3.1: Grab the first worksheet (index 0) and rename it
            Worksheet worksheet = workbook.Worksheets[0];
            worksheet.Name = "Data"; // clear, concise, and self‑describing
```

إذا حاولت تعيين اسم مكرر، سيطرح Aspose.Cells استثناءً من نوع `ArgumentException`. لتجنب ذلك، يمكنك التحقق من وجود الاسم مسبقًا باستخدام `Worksheets.Exists("Data")` قبل إعادة التسمية.

---

## الخطوة 4: إضافة خصائص مخصصة

تُخزن الخصائص المخصصة في XML الداخلي للمصنف وتنتقل مع الملف بغض النظر عن الصيغة. إنها مثالية لتضمين معلومات مثل `ReportId` أو `GeneratedBy`.

```csharp
            // Step 4.1: Add a numeric property
            workbook.CustomProperties.Add("ReportId", 12345);

            // Step 4.2: Add a string property
            workbook.CustomProperties.Add("GeneratedBy", "MyApp");
```

> **لماذا نستخدم الخصائص المخصصة؟**  
> • يمكن الوصول إليها عبر لوحة “File → Info → Properties” في Excel.  
> • يمكن للشفرة التي تستهلك المصنف قراءتها دون الحاجة إلى فحص محتويات الخلايا.  
> • تبقى موجودة بعد تحويل الصيغ (XLSX ↔ XLSB) لأنها جزء من بيانات التعريف للملف.

يمكنك أيضًا تخزين تواريخ، قيم منطقية، أو حتى كتل ثنائية، لكن احرص على أن تكون الحمولة صغيرة – Excel ليس قاعدة بيانات.

---

## الخطوة 5: حفظ كـ XLSB (كتابة ملف Excel ثنائي)

صيغة XLSB تخزن البيانات في بنية ثنائية، مما يجعل الملف أصغر وأسرع في الفتح. والأهم في هذا الدرس، **تُدمج الخصائص المخصصة في التيار الثنائي**، مما يضمن انتقالها مع الملف.

```csharp
            // Step 5.1: Define the output path
            string outputPath = Path.Combine(
                Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
                "WithCustomProps.xlsb");

            // Step 5.2: Save the workbook as a binary XLSB file
            workbook.Save(outputPath, SaveFormat.Xlsb);

            Console.WriteLine($"Workbook saved to {outputPath}");
        }
    }
}
```

### النتيجة المتوقعة

بعد تشغيل البرنامج، ستجد الملف `WithCustomProps.xlsb` على سطح المكتب. افتحه في Excel، انتقل إلى **File → Info → Properties** وسترى `ReportId` و `GeneratedBy` مدرجة تحت *Custom*.

---

## الخطوة 6: الحالات الخاصة والأسئلة الشائعة

### ماذا لو كان المجلد المستهدف للكتابة للقراءة فقط؟

غلف استدعاء `Save` داخل كتلة `try/catch` واستخدم موقعًا يمكن للمستخدم الكتابة فيه، مثل `%TEMP%`. هذا يمنع تعطل التطبيق بسبب أخطاء الأذونات.

```csharp
try
{
    workbook.Save(outputPath, SaveFormat.Xlsb);
}
catch (UnauthorizedAccessException)
{
    string fallback = Path.GetTempFileName().Replace(".tmp", ".xlsb");
    workbook.Save(fallback, SaveFormat.Xlsb);
    Console.WriteLine($"Saved to fallback location: {fallback}");
}
```

### هل يمكنني **حفظ كـ XLSX** مع الحفاظ على الخصائص المخصصة؟

نعم – فقط غيّر `SaveFormat.Xlsb` إلى `SaveFormat.Xlsx`. تُخزن الخصائص في نفس الجزء XML، لذا تبقى بعد تغيير الصيغة. ومع ذلك، تكون ملفات XLSX أكبر لأنها XML مضغوط، بينما XLSB يقدم أداءً أفضل لمجموعات البيانات الكبيرة.

### كيف أقرأ الخصائص المخصصة لاحقًا؟

```csharp
Workbook loaded = new Workbook(outputPath);
foreach (CustomProperty prop in loaded.CustomProperties)
{
    Console.WriteLine($"{prop.Name} = {prop.Value}");
}
```

تطبع هذه الشريحة كل خاصية مخصصة، مما يجعل من السهل على الخدمات اللاحقة التحقق من مصدر الملف.

---

## مثال كامل يعمل

فيما يلي البرنامج الكامل الذي يمكنك نسخه‑ولصقه في مشروع وحدة تحكم جديد. لا توجد أجزاء مفقودة – كل شيء من عبارات `using` إلى `Console.WriteLine` النهائي مشمول.

```csharp
using System;
using System.IO;
using Aspose.Cells;

namespace ExcelDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create a new workbook instance
            Workbook workbook = new Workbook();

            // 2️⃣ Access the first worksheet and give it a meaningful name
            Worksheet worksheet = workbook.Worksheets[0];
            worksheet.Name = "Data";

            // 3️⃣ Add custom properties (they travel with the file)
            workbook.CustomProperties.Add("ReportId", 12345);
            workbook.CustomProperties.Add("GeneratedBy", "MyApp");

            // 4️⃣ Define where to save the binary XLSB file
            string outputPath = Path.Combine(
                Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
                "WithCustomProps.xlsb");

            // 5️⃣ Save the workbook as a binary XLSB file
            try
            {
                workbook.Save(outputPath, SaveFormat.Xlsb);
                Console.WriteLine($"✅ Workbook saved to {outputPath}");
            }
            catch (Exception ex)
            {
                Console.WriteLine($"❌ Failed to save workbook: {ex.Message}");
            }
        }
    }
}
```

شغّل البرنامج، افتح الملف الناتج، وتأكد من وجود الخصائص المخصصة. هذه هي العملية الكاملة لـ **إنشاء مصنف Excel**، **إضافة خصائص مخصصة**، **تعيين اسم ورقة العمل**، و **حفظه كـ XLSB** في تدفق واحد منظم.

---

## الخلاصة

أنت الآن تعرف بالضبط كيف **تنشئ مصنف Excel**، تعطي ورقته اسمًا واضحًا عبر **set worksheet name**، تدمج بيانات وصفية مفيدة باستخدام **add custom properties**، وأخيرًا **تحفظه كـ XLSB** لتنتج ملف Excel ثنائي مضغوط. هذه العملية موثوقة، تعمل عبر إصدارات .NET المختلفة، وتتكيف بسهولة سواء كنت تولد تقريرًا واحدًا أو ألف تقرير.

ما الخطوة التالية؟ جرّب إضافة جدول بيانات إلى ورقة “Data”، جرب أنواع خصائص مختلفة (تواريخ، قيم منطقية)، أو غيّر الإخراج إلى **save as xlsb** لمجموعات بيانات ضخمة. يمكنك أيضًا استكشاف حماية المصنف بكلمة مرور – Aspose.Cells يجعل ذلك سطرًا واحدًا فقط.

لا تتردد في ترك تعليق إذا واجهت أي صعوبة، أو مشاركة كيف طوّرت هذا النمط في مشاريعك الخاصة. برمجة سعيدة!  

---  

![Create Excel workbook screenshot](image.png){alt="إنشاء مصنف Excel مع خصائص مخصصة"}

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}