---
category: general
date: 2026-03-21
description: إنشاء مصنف Excel باستخدام C# وتعلم كيفية إضافة تعليق إلى Excel، وتعبئة
  التعليق تلقائيًا باستخدام Smart Markers. دليل خطوة بخطوة للمطورين.
draft: false
keywords:
- create excel workbook c#
- add comment to excel
- how to add comment
- how to fill comment
- fill excel comment
language: ar
og_description: إنشاء مصنف إكسل باستخدام C# وإضافة تعليق بسرعة إلى إكسل، ثم ملء التعليق
  باستخدام العلامات الذكية. دليل كامل مع الشيفرة.
og_title: إنشاء مصنف إكسل C# – إضافة وتعبئة التعليقات
tags:
- C#
- Excel automation
- Aspose.Cells
title: إنشاء مصنف Excel باستخدام C# – إضافة وتعبئة التعليقات باستخدام العلامات الذكية
url: /ar/net/excel-comment-annotation/create-excel-workbook-c-add-and-fill-comments-with-smart-mar/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء مصنف Excel C# – إضافة وتعبئة التعليقات باستخدام Smart Markers

هل احتجت يومًا إلى **create Excel workbook C#** وتساءلت كيف يمكنك تضمين تعليق يتحدث نفسه تلقائيًا؟ لست وحدك. في العديد من سيناريوهات التقارير تريد تعليق خلية يقول *“Created by Alice on 2024‑07‑15”* دون كتابة الاسم أو التاريخ يدويًا في كل مرة.  

في هذا الدرس سنوضح لك بالضبط **how to add comment to Excel**، ثم **how to fill comment** باستخدام Smart Markers من Aspose.Cells. في النهاية ستحصل على برنامج جاهز للتنفيذ ينشئ مصنفًا، يضيف تعليقًا ديناميكيًا، ويحفظ الملف—كل ذلك في بضع خطوات بسيطة.

> **ما ستحصل عليه:** تطبيق كونسول C# كامل وقابل للترجمة، شرح لكل سطر، نصائح لتجنب الأخطاء الشائعة، وأفكار لتوسيع الحل.

## المتطلبات المسبقة

- .NET 6.0 SDK أو أحدث (الكود يعمل مع .NET Core و .NET Framework أيضًا)  
- Visual Studio 2022 أو أي بيئة تطوير تفضّلها  
- **Aspose.Cells for .NET** حزمة NuGet (`Install-Package Aspose.Cells`) – هذه المكتبة تدعم الفئات `Workbook` و `Worksheet` و `SmartMarkerProcessor` المستخدمة أدناه.  
- إلمام أساسي بصياغة C# – إذا كتبت `Console.WriteLine` فأنت جاهز للبدء.

الآن بعد أن أُنجزت الأساسيات، دعنا نغوص في التفاصيل.

![Create Excel workbook C# example screenshot](excel-workbook.png "Create Excel workbook C# example")

## الخطوة 1: تهيئة مصنف جديد – أساسيات إنشاء مصنف Excel C#

أولًا نحتاج إلى كائن مصنف نظيف. فكر في `Workbook` كقماش فارغ؛ بدونها لا يمكنك وضع أي خلايا أو صفوف أو تعليقات.

```csharp
using System;
using Aspose.Cells;

namespace ExcelCommentDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1: Create a new workbook and get the first worksheet
            Workbook workbook = new Workbook();               // fresh Excel file
            Worksheet worksheet = workbook.Worksheets[0];    // default sheet named "Sheet1"
```

**لماذا هذا مهم:** `Workbook` تنشئ تلقائيًا ورقة عمل افتراضية، لذا لا تحتاج إلى استدعاء `Add` إلا إذا كنت بحاجة إلى أوراق إضافية. الوصول إلى `Worksheets[0]` هو أسرع طريقة لبدء تعبئة البيانات.

## الخطوة 2: إدراج تعليق باستخدام Smart Marker – كيفية إضافة تعليق مع الرموز

بعد ذلك نضع تعليقًا في الخلية **B2** يحتوي على رموز Smart Marker (`«UserName»` و `«CreatedDate»`). سيتم استبدال هذه الرموز لاحقًا بالقيم الفعلية.

```csharp
            // Step 2: Add a comment that contains Smart Marker tokens
            var comment = worksheet.Cells["B2"].CreateComment();
            comment.Note = "Created by «UserName» on «CreatedDate»";
```

**شرح:**  
- `CreateComment()` ينشئ كائن التعليق إذا لم يكن موجودًا؛ وإلا فإنه يُعيد الكائن الموجود.  
- خاصية `Note` تحتفظ بالنص الظاهر. من خلال وضع العناصر النائبة داخل `« »` نخبر Aspose.Cells بأنها **Smart Markers** – عناصر نائبة يمكن استبدالها دفعة واحدة.

> **نصيحة احترافية:** إذا كنت بحاجة إلى تعليق متعدد الأسطر، استخدم `\n` داخل السلسلة، مثال: `"Line1\nLine2"`.

## الخطوة 3: إعداد كائن البيانات – كيفية تعبئة التعليق ديناميكيًا

تحتاج Smart Markers إلى مصدر بيانات. في C# أسهل طريقة هي النوع المجهول (anonymous type) الذي يطابق أسماء العناصر النائبة.

```csharp
            // Step 3: Prepare the data that will replace the tokens
            var markerData = new
            {
                UserName = "Alice",
                CreatedDate = DateTime.Now   // will be formatted automatically
            };
```

**لماذا النوع المجهول؟**  
إنه خفيف الوزن، لا يتطلب ملف **class** إضافي، ويتطابق أسماء الخصائص (`UserName`, `CreatedDate`) تمامًا مع أسماء الرموز. إذا كنت تفضّل نموذجًا قويًا النوع، فقط أنشئ فئة بنفس الخصائص.

## الخطوة 4: معالجة Smart Markers – كيفية تعبئة التعليق باستخدام كائن البيانات

الآن يحدث السحر. يقوم `SmartMarkerProcessor` بمسح المصنف بحثًا عن أي رموز `«…»` ويستبدلها بالقيم من `markerData`.

```csharp
            // Step 4: Process the Smart Markers in the worksheet using the data object
            SmartMarkerProcessor processor = new SmartMarkerProcessor(workbook);
            processor.Process(worksheet, markerData);
```

**ما الذي يحدث خلف الكواليس؟**  
`SmartMarkerProcessor` يتجول عبر كل خلية، تعليق، رأس، إلخ، يبحث عن نمط `«Token»`. عندما يجد واحدًا، يستخدم الـ reflection لقراءة الخاصية المطابقة من `markerData` ويكتب القيمة مرة أخرى. لا حاجة إلى حلقات يدوية.

## الخطوة 5: حفظ المصنف – تعبئة تعليق Excel وحفظ الملف

أخيرًا نكتب المصنف إلى القرص. الآن يظهر التعليق شيئًا مثل *“Created by Alice on 03/21/2026 10:15 AM”*.

```csharp
            // Step 5: Save the workbook with the filled comment
            string outputPath = @"YOUR_DIRECTORY\CommentFilled.xlsx";
            workbook.Save(outputPath);

            Console.WriteLine($"Workbook saved to {outputPath}");
        }
    }
}
```

**التحقق من النتيجة:** افتح `CommentFilled.xlsx` في Excel، مرّر المؤشر فوق الخلية **B2**، وسترى التعليق مع اسم المستخدم الفعلي والطابع الزمني. لا حاجة لتغييرات إضافية في الكود للتشغيلات المستقبلية—فقط غيّر قيم `markerData`.

---

## الاختلافات الشائعة وحالات الحافة

### استخدام تنسيق تاريخ مخصص

إذا كنت تريد التاريخ بتنسيق `yyyy‑MM‑dd`، عدّل كائن البيانات:

```csharp
CreatedDate = DateTime.Now.ToString("yyyy-MM-dd")
```

### إضافة تعليقات متعددة

يمكنك تكرار **الخطوة 2** لخلايا أخرى. كل تعليق يمكن أن يحتوي على مجموعة خاصة من الرموز، أو يشارك نفس الرموز إذا كانت المعلومات عامة.

### العمل مع مصنفات موجودة

بدلاً من `new Workbook()`، حمّل ملفًا موجودًا:

```csharp
Workbook workbook = new Workbook(@"ExistingFile.xlsx");
```

بقية الخطوات تبقى كما هي—Smart Markers تعمل على الملفات الجديدة والموجودة على حد سواء.

### معالجة القيم الفارغة

إذا كان من الممكن أن يكون الرمز مفقودًا، ضع الخاصية في نوع قابل للـ null أو قدم قيمة احتياطية:

```csharp
UserName = user?.Name ?? "Unknown"
```

المعالج سيُدرج *“Unknown”* عندما يكون المصدر `null`.

---

## مثال كامل جاهز للتنفيذ (نسخ‑لصق)

فيما يلي **البرنامج الكامل** الذي يمكنك وضعه في مشروع تطبيق كونسول وتشغيله فورًا (فقط استبدل `YOUR_DIRECTORY` بمسار مجلد حقيقي).

```csharp
using System;
using Aspose.Cells;

namespace ExcelCommentDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1: Create a new workbook and get the first worksheet
            Workbook workbook = new Workbook();
            Worksheet worksheet = workbook.Worksheets[0];

            // Step 2: Add a comment that contains Smart Marker tokens
            var comment = worksheet.Cells["B2"].CreateComment();
            comment.Note = "Created by «UserName» on «CreatedDate»";

            // Step 3: Prepare the data that will replace the tokens
            var markerData = new
            {
                UserName = "Alice",
                CreatedDate = DateTime.Now
            };

            // Step 4: Process the Smart Markers in the worksheet using the data object
            SmartMarkerProcessor processor = new SmartMarkerProcessor(workbook);
            processor.Process(worksheet, markerData);

            // Step 5: Save the workbook with the filled comment
            string outputPath = @"YOUR_DIRECTORY\CommentFilled.xlsx";
            workbook.Save(outputPath);

            Console.WriteLine($"Workbook saved to {outputPath}");
        }
    }
}
```

شغّل البرنامج، افتح الملف المُنشأ، وسترى التعليق الديناميكي في الخلية **B2**. سهل، أليس كذلك؟

---

## الأسئلة المتكررة (FAQ)

**س: هل يعمل هذا مع .NET Framework 4.7؟**  
ج: بالتأكيد. Aspose.Cells يدعم .NET Framework 4.0+ و .NET Core/5/6/7. فقط قم بالإشارة إلى DLL أو حزمة NuGet المناسبة.

**س: هل يمكنني استخدام هذا النهج للتحقق من صحة البيانات أو التنسيق الشرطي؟**  
ج: Smart Markers تُستخدم أساسًا لإدخال القيم في الخلايا، التعليقات، الرؤوس، والتذييلات. للتنسيق الشرطي ستظل تستخدم واجهات برمجة `Style` العادية.

**س: ماذا لو احتجت لإضافة تعليق إلى ورقة عمل **مختلفة**؟**  
ج: استخرج ورقة العمل المستهدفة (`workbook.Worksheets["MySheet"]`) وكرر **الخطوة 2** على خلايا تلك الورقة.

---

## الخطوات التالية والمواضيع ذات الصلة

- **How to add comment to Excel** برمجيًا لعدة خلايا (التكرار عبر نطاق).  
- **Fill Excel comment** ببيانات من قاعدة بيانات (استخدم `DataTable` كمصدر بيانات لـ Smart Markers).  
- استكشف **Smart Marker arrays** لإنشاء جداول تلقائيًا.  
- تعلم حول **Aspose.Cells styling** لتنسيق خط التعليق، لونه، وحجمه.

جرّب المقاطع البرمجية، استبدل مصدر البيانات، وستتمكن بسرعة من إتقان **how to fill comment** في أي سيناريو أتمتة Excel.

---

### الخلاصة

لقد استعرضنا الآن العملية الكاملة لـ **create excel workbook c#**، **add comment to excel**، و **fill excel comment** باستخدام Smart Markers. الحل مدمج، قابل لإعادة الاستخدام، وجاهز للإنتاج.  

جرّبه، عدّل العناصر النائبة، ودع المكتبة تتولى الجزء الصعب. إذا واجهت أي صعوبات، اترك تعليقًا أدناه — برمجة سعيدة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}