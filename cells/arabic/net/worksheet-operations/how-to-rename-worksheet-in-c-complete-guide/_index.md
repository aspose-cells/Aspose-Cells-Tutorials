---
category: general
date: 2026-05-23
description: كيفية إعادة تسمية ورقة العمل في C# باستخدام Aspose.Cells – تعلم إنشاء
  مصنف Excel، تعيين اسم ورقة العمل وإنشاء ورقة تقرير بسرعة.
draft: false
keywords:
- how to rename worksheet
- create excel workbook
- set worksheet name
- change worksheet name
- create report worksheet
language: ar
og_description: كيفية إعادة تسمية ورقة العمل في C# باستخدام Aspose.Cells. اتبع هذا
  الدليل خطوة بخطوة لإنشاء مصنف Excel، وتعيين اسم ورقة العمل، وبناء ورقة تقرير.
og_title: كيفية إعادة تسمية ورقة العمل في C# – دليل كامل
schemas:
- author: Aspose
  dateModified: '2026-05-23'
  description: How to rename worksheet in C# using Aspose.Cells – learn to create
    Excel workbook, set worksheet name and create report worksheet quickly.
  headline: How to Rename Worksheet in C# – Complete Guide
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel
- Worksheet
title: كيفية إعادة تسمية ورقة العمل في C# – دليل كامل
url: /ar/net/worksheet-operations/how-to-rename-worksheet-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية إعادة تسمية ورقة العمل في C# – دليل شامل

هل تساءلت يومًا **عن طريقة إعادة تسمية ورقة العمل** برمجياً دون فتح Excel؟ لست وحدك. يحتاج الكثير من المطورين إلى إنشاء تقارير في الوقت الفعلي، وأول سؤال يطرحهون هو كيفية إعادة تسمية ورقة العمل إلى اسم ذو معنى مثل “Report”. في هذا الدليل سنستعرض مثالًا كاملاً قابلاً للتنفيذ يوضح لك كيفية إعادة تسمية ورقة العمل، بالإضافة إلى بعض الحيل الإضافية مثل إنشاء مصنف Excel، تعيين اسم ورقة العمل، وحتى إنشاء ورقة تقرير يمكن إعادة استخدامها لاحقًا.

سنستخدم Aspose.Cells for .NET لأنه يتيح لك التعامل مع ملفات Excel دون الحاجة إلى Office Interop. بنهاية هذا الدرس ستكون قادرًا على:

* **إنشاء مصنف Excel** من الصفر.  
* **تعيين اسم ورقة العمل** (أو تغيير اسم ورقة العمل) بأمان.  
* بناء نمط **إنشاء ورقة تقرير** يمكنك دمجه في أي خط أنابيب تقارير.

بدون أدوات خارجية، بدون سحر COM—فقط كود C# نقي يمكنك وضعه في أي مشروع .NET.

## المتطلبات المسبقة

* .NET 6.0 أو أحدث (الكود يعمل أيضًا على .NET Framework 4.7+).  
* حزمة Aspose.Cells for .NET عبر NuGet – تثبيتها باستخدام `dotnet add package Aspose.Cells`.  
* بيئة تطوير معتدلة مثل Visual Studio 2022 أو VS Code.  

هذا كل ما تحتاجه. إذا كان لديك مشروع بالفعل، فقط أضف الحزمة وستكون جاهزًا للانطلاق.

---

## كيفية إعادة تسمية ورقة العمل – الخطوة 1: إنشاء مصنف Excel

قبل أن تتمكن من إعادة تسمية أي شيء، تحتاج إلى مصنف للعمل معه. فكر في المصنف كحاوية تحتوي على جميع الأوراق. إنشاء واحد هو ببساطة استدعاء مُنشئ `Workbook`.

```csharp
using Aspose.Cells;

namespace WorksheetDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Create a new Excel workbook
            Workbook workbook = new Workbook();   // <-- this creates an empty .xlsx file in memory
            // (Optional) you can also load an existing file:
            // Workbook workbook = new Workbook("template.xlsx");
```

**لماذا هذا مهم:**  
إنشاء مصنف جديد يمنحك صفحة فارغة، وهو مثالي عندما تريد **إنشاء ورقة تقرير** من الصفر. إذا قمت بتحميل قالب، فإن منطق إعادة التسمية يبقى نفسه—يتغير المصدر فقط.

---

## الخطوة 2: تعيين اسم ورقة العمل (إعادة تسمية الورقة الأولى)

بشكل افتراضي يحتوي المصنف الجديد على ورقة واحدة تسمى “Sheet1”. للإجابة على السؤال الأساسي—**كيف تعيد تسمية ورقة العمل**—ما عليك سوى تعيين سلسلة جديدة إلى خاصية `Name` لكائن `Worksheet`.

```csharp
            // Step 2: Access the first worksheet (index 0) and rename it
            Worksheet masterSheet = workbook.Worksheets[0];
            masterSheet.Name = "Report";   // <-- this is the new name
```

**ما الذي يحدث في الخلفية؟**  
`Worksheets[0]` يجلب الورقة الأولى، ومُحدد `Name` يحدّث XML الداخلي الذي يمثل تبويب الورقة. Aspose.Cells يتولى كل التفاصيل منخفضة المستوى، لذا لا تحتاج للقلق بشأن إتلاف المصنف.

> **نصيحة احترافية:** إذا كنت بحاجة إلى **تغيير اسم ورقة العمل** بناءً على إدخال المستخدم، تحقق دائمًا من صحة السلسلة أولًا—Excel لا يسمح بالأحرف مثل `:` `\` `/` `?` `*` `[` `]`.

---

## الخطوة 3: تكوين معالج SmartMarker (اختياري لكنه قوي)

إذا كنت تنشئ **ورقة تقرير** سيتم ملؤها لاحقًا بالبيانات، فإن SmartMarker ميزة مفيدة. يتيح لك تعريف عناصر نائبة في الورقة ثم تعبئتها من مصدر بيانات—دون كتابة حلقة.

```csharp
            // Step 3: Initialize SmartMarkerProcessor for advanced templating
            SmartMarkerProcessor processor = new SmartMarkerProcessor(workbook);

            // Optional: Allow duplicate detail sheet name if you plan to generate multiple reports
            processor.Options.DetailSheetNewName = "Report"; // ensures the detail sheet also gets the name "Report"
```

**لماذا نستخدم SmartMarker؟**  
عند وجود تقرير رئيس‑تفصيل، يمكن للمعالج استنساخ الورقة الرئيسية، إعادة تسمية النسخة، وإدخال الصفوف تلقائيًا. هذا يوفر عليك نسخ الأنماط والصيغ يدويًا.

---

## الخطوة 4: حفظ المصنف (شاهد النتيجة)

الآن بعد أن تم إعادة تسمية ورقة العمل، لنكتب الملف إلى القرص حتى تتمكن من فتحه في Excel والتحقق من التغيير.

```csharp
            // Step 4: Save the workbook to a file
            string outputPath = "RenamedWorksheetDemo.xlsx";
            workbook.Save(outputPath, SaveFormat.Xlsx);
            System.Console.WriteLine($"Workbook saved to {outputPath}");
        }
    }
}
```

**الناتج المتوقع:**  
عند فتح *RenamedWorksheetDemo.xlsx*، سيظهر التبويب في الأسفل مكتوبًا **Report** بدلًا من “Sheet1”. هذا هو الدليل البصري على أنك أتقنت **كيفية إعادة تسمية ورقة العمل**.

---

## المشكلات الشائعة والحالات الخاصة

| الحالة | ما الذي يجب الانتباه إليه | كيفية التعامل |
|-----------|----------------------|---------------|
| **اسم ورقة مكرر** | Excel يرمي استثناءً إذا حاولت تعيين اسم موجود مسبقًا. | استخدم `processor.Options.DetailSheetNewName` أو تحقق من وجود الاسم عبر `workbook.Worksheets.Exists("Report")` قبل إعادة التسمية. |
| **أحرف غير صالحة** | الأحرف `:*?/\[]` غير مسموح بها في أسماء الأوراق. | احذفها أو استبدلها بشرطات سفلية قبل تعيين `masterSheet.Name`. |
| **أسماء طويلة جدًا** | Excel يحدّ من طول أسماء الأوراق إلى 31 حرفًا. | قص السلسلة: `masterSheet.Name = name.Length > 31 ? name.Substring(0,31) : name;`. |
| **التعريب** | بعض اللغات تستخدم أسماء ورقة افتراضية مختلفة (مثل “Feuille1”). | النهج القائم على الفهرس (`Worksheets[0]`) يعمل بغض النظر عن الاسم الافتراضي. |

---

## إضافي: إنشاء ورقة تقرير باستخدام قالب

غالبًا ما تبدأ من قالب يحتوي بالفعل على رؤوس، صيغ، وتنسيق. إليك نمطًا سريعًا لـ **إنشاء ورقة تقرير** من قالب مع القدرة على **تعيين اسم ورقة العمل** ديناميكيًا.

```csharp
// Load a template file that has a sheet called "Template"
Workbook templateWb = new Workbook("ReportTemplate.xlsx");

// Clone the template sheet
Worksheet templateSheet = templateWb.Worksheets["Template"];
int newIndex = workbook.Worksheets.AddCopy(templateSheet);

// Rename the cloned sheet
Worksheet reportSheet = workbook.Worksheets[newIndex];
reportSheet.Name = "MonthlyReport";   // <-- set worksheet name for the new report
```

**لماذا الاستنساخ؟**  
الاستنساخ يحافظ على جميع التنسيقات، التحقق من صحة البيانات، والصيغ. كل ما عليك هو إعادة تسمية الورقة المستنسخة، وهو ما يشبه عملية **تغيير اسم ورقة العمل** التي قمنا بها سابقًا.

---

## مثال كامل يعمل (جميع الخطوات مجتمعة)

فيما يلي البرنامج الكامل الذي يمكنك نسخه ولصقه في تطبيق Console. يوضح **إنشاء مصنف Excel**، **تعيين اسم ورقة العمل**، **تغيير اسم ورقة العمل**، و**إنشاء ورقة تقرير** في خطوة واحدة.

```csharp
using System;
using Aspose.Cells;

namespace WorksheetDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create a new workbook
            Workbook workbook = new Workbook();

            // 2️⃣ Rename the default sheet to "Report"
            Worksheet masterSheet = workbook.Worksheets[0];
            masterSheet.Name = "Report";

            // 3️⃣ (Optional) Prepare SmartMarker for future data injection
            SmartMarkerProcessor processor = new SmartMarkerProcessor(workbook);
            processor.Options.DetailSheetNewName = "Report";

            // 4️⃣ (Bonus) Clone a template sheet if you have one
            // Uncomment the lines below if you have a template file.
            /*
            Workbook templateWb = new Workbook("ReportTemplate.xlsx");
            Worksheet templateSheet = templateWb.Worksheets["Template"];
            int copyIndex = workbook.Worksheets.AddCopy(templateSheet);
            Worksheet reportSheet = workbook.Worksheets[copyIndex];
            reportSheet.Name = "MonthlyReport";
            */

            // 5️⃣ Save the file
            string outputPath = "RenamedWorksheetDemo.xlsx";
            workbook.Save(outputPath, SaveFormat.Xlsx);
            Console.WriteLine($"Workbook saved to {outputPath}");
        }
    }
}
```

شغّل البرنامج، افتح ملف **RenamedWorksheetDemo.xlsx**، وسترى تبويبًا مسمى **Report**. إذا ألغيت التعليق عن القسم الإضافي ووفرت قالبًا، ستحصل أيضًا على ورقة **MonthlyReport**—مثالي لخطوط أنابيب التقارير المؤتمتة.

---

## الخلاصة

غطّينا **كيفية إعادة تسمية ورقة العمل** في C# من الصفر: ابدأ بـ **إنشاء مصنف Excel**، ثم **تعيين اسم ورقة العمل**، اختياريًا **تغيير اسم ورقة العمل** باستخدام SmartMarker، وأخيرًا **إنشاء ورقة تقرير** يمكن إعادة استخدامها. الكود مستقل، يعمل في أي بيئة .NET، ويتجنب الأخطاء الشائعة التي تعيق المبتدئين.

ما الخطوة التالية؟ جرّب إضافة بيانات إلى الورقة المعاد تسميتها، جرب تنسيق الخلايا، أو دمج عناصر SmartMarker لتعبئة الصفوف تلقائيًا من قاعدة بيانات. إمكانيات إنشاء تقارير Excel ديناميكية لا حدود لها.

إذا واجهت أي مشاكل—مثل خطأ “اسم ورقة غير صالح” أو مشكلة ورقة مكررة—اترك تعليقًا أدناه. برمجة سعيدة، واستمتع بقوة التلاعب البرمجي بملفات Excel!

## دروس ذات صلة

- [كيفية تقسيم أجزاء ورقة العمل في Excel باستخدام Aspose.Cells .NET لتحليل بيانات محسّن](/cells/english/net/worksheet-management/split-worksheet-panes-excel-aspose-cells-dotnet/)
- [تعيين ألوان تبويب ورقة العمل في Excel باستخدام Aspose.Cells .NET - دليل شامل](/cells/english/net/worksheet-management/set-worksheet-tab-colors-aspose-cells-net/)
- [كيفية فحص حماية كلمة مرور ورقة العمل في Excel باستخدام Aspose.Cells for .NET](/cells/english/net/security-protection/aspose-cells-dotnet-check-excel-worksheet-password-protection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}