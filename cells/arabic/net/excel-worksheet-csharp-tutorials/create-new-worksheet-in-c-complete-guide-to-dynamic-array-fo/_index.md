---
category: general
date: 2026-05-23
description: إنشاء ورقة عمل جديدة في C# مع دليل خطوة بخطوة. تعلم كيفية إنشاء دفتر
  عمل، واستخدام صيغة مصفوفة ديناميكية، وتصدير البيانات المرتبة وحفظ دفتر العمل.
draft: false
keywords:
- create new worksheet
- how to create workbook
- how to save workbook
- export sorted data
- dynamic array formula
language: ar
og_description: إنشاء ورقة عمل جديدة في C# باستخدام Aspose.Cells. يوضح هذا الدليل
  كيفية إنشاء دفتر عمل، وتطبيق صيغة مصفوفة ديناميكية، وتصدير البيانات المرتبة، وحفظ
  دفتر العمل.
og_title: إنشاء ورقة عمل جديدة في C# – دليل برمجة كامل
schemas:
- author: Aspose
  dateModified: '2026-05-23'
  description: Create new worksheet in C# with a step‑by‑step tutorial. Learn how
    to create workbook, use a dynamic array formula, export sorted data and save workbook.
  headline: Create New Worksheet in C# – Complete Guide to Dynamic Array Formulas
  type: TechArticle
- questions:
  - answer: The file will open, but the `SORT` formula will appear as text and show
      a `#NAME?` error. For backward compatibility, generate the sorted list in code
      and write the values directly.
    question: Does this work on older Excel versions that don’t support dynamic arrays?
  - answer: Absolutely. Use `=SORT(A2:C10, {1,2}, {1,-1})` where the second argument
      specifies the column indices and the third the sort order.
    question: Can I sort by multiple columns?
  - answer: 'After saving the workbook, load it again and call `worksheet.Cells.ExportDataTableAsString`
      or use `CsvSaveOptions` if your library provides one. --- ## Next Steps - **Explore
      other dynamic array functions** such as `FILTER`, `UNIQUE`, and `SEQUENCE`.
      - **Automate chart creation** on the same worksh'
    question: What if I need to export the sorted data to CSV?
  type: FAQPage
tags:
- C#
- Excel Automation
- Aspose.Cells
- Spreadsheet
title: إنشاء ورقة عمل جديدة في C# – الدليل الكامل لصيغ المصفوفات الديناميكية
url: /ar/net/excel-worksheet-csharp-tutorials/create-new-worksheet-in-c-complete-guide-to-dynamic-array-fo/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء ورقة عمل جديدة في C# – دليل كامل لصيغ المصفوفات الديناميكية

هل تساءلت يومًا كيف **تنشئ ورقة عمل جديدة** في C# دون فتح Excel يدويًا؟ لست وحدك. يحتاج العديد من المطورين إلى إنشاء تقارير، فرز البيانات في الوقت الفعلي، وإرسال النتيجة كملف .xlsx — كل ذلك من خلال الكود.  

في هذا الدرس سنستعرض ذلك بالضبط: سنوضح **كيفية إنشاء دفتر عمل**، نضع **صيغة مصفوفة ديناميكية** في ورقة جديدة، **نصدر البيانات المرتبة**، وأخيرًا **كيفية حفظ دفتر العمل** لتتمكن من مشاركته مع أي شخص. لا إطالة، مجرد مثال عملي يمكنك نسخه ولصقه اليوم.

## ما ستتعلمه

- المتطلبات المسبقة لاستخدام Aspose.Cells (أو أي مكتبة .NET Excel مماثلة).  
- كيفية **إنشاء ورقة عمل جديدة**، كتابة صيغة `SORT`، والسماح لنطاق الانسكاب (spill range) في Excel أن يملأ الخلايا تلقائيًا.  
- نصائح للتعامل مع الحالات الخاصة مثل نطاقات المصدر الفارغة أو مجموعات البيانات الكبيرة.  
- كيفية **تصدير البيانات المرتبة** إلى ملف جديد والتحقق من النتيجة.  
- نظرة سريعة على الأساليب البديلة إذا كنت تفضل `OpenXML` أو `EPPlus`.  

بنهاية هذا الدليل سيكون لديك برنامج مستقل ينتج قائمة مرتبة في ورقة عمل جديدة، جاهزة للمعالجة اللاحقة.

---

## الخطوة 1: إعداد المشروع – كيفية إنشاء دفتر عمل

أولًا، لنجهز البيئة. سنستخدم **Aspose.Cells for .NET** لأنه يدعم محرك حساب Excel الكامل، بما في ذلك أحدث **صيغ المصفوفات الديناميكية** مثل `SORT`. إذا كنت تستخدم مكتبة مختلفة، فإن المفاهيم تبقى نفسها — فقط استبدل مساحة الاسم.

```csharp
// Add the Aspose.Cells NuGet package
//   dotnet add package Aspose.Cells
using Aspose.Cells;

namespace WorksheetDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Create a new workbook (or load an existing one)
            Workbook workbook = new Workbook();   // <-- this is how we **how to create workbook**
```

**لماذا هذا مهم:**  
إنشاء كائن `Workbook` يُنشئ تمثيلًا في الذاكرة لملف Excel. لا حاجة لتفاعل COM، ولا يتطلب تثبيت Excel. هذا يجعل الحل قابلًا للنقل عبر Windows، Linux، وحاويات Docker.

> **نصيحة احترافية:** إذا كان لديك ملف قالب جاهز، مرّر مساره إلى `new Workbook("template.xlsx")` بدلاً من البدء من الصفر.

---

## الخطوة 2: إضافة ورقة جديدة – إنشاء ورقة عمل جديدة

الآن بعد أن لدينا دفتر عمل، نحتاج إلى مكان لوضع بياناتنا. بشكل افتراضي، يُنشئ Aspose ورقة واحدة تسمى “Sheet1”. سنضيف ورقة أخرى لتبقى الأمثلة منظمة.

```csharp
            // Step 2: Add a new worksheet to hold the sorted output
            int newSheetIndex = workbook.Worksheets.Add();
            Worksheet sheet = workbook.Worksheets[newSheetIndex];   // <-- **create new worksheet**
```

**ما الذي يحدث في الخلفية؟**  
`Worksheets.Add()` تُعيد الفهرس الصفري (zero‑based) للورقة التي أُضيفت حديثًا. ثم نسترجع كائن `Worksheet` لنتمكن من تعديل الخلايا مباشرة.

> **احذر:** إذا استدعيت `Add()` بشكل متكرر دون حفظ الفهرس، قد تفقد تتبع الورقة التي تكتب فيها. احتفظ دائمًا بمرجع.

---

## الخطوة 3: ملء بعض البيانات التجريبية (اختياري)

لكي تكون صيغة `SORT` لديها ما تُفرزه، نحتاج إلى نطاق مصدر. لنملأ `A2:A6` ببعض القيم غير المرتبة.

```csharp
            // Populate source data (A2:A6) – this mimics a raw data table
            string[] rawValues = { "Delta", "Alpha", "Echo", "Bravo", "Charlie" };
            for (int i = 0; i < rawValues.Length; i++)
            {
                sheet.Cells[i + 1, 0].PutValue(rawValues[i]); // Row i+1, Column 0 (A column)
            }
```

لماذا نضع البيانات في *نفس* الورقة؟ لأن دالة `SORT` يمكنها الإشارة إلى نطاق في نفس ورقة العمل؛ هذا يبقي العرض مختصرًا. في السيناريوهات الواقعية قد تقرأ البيانات من قاعدة بيانات، CSV، أو ورقة أخرى.

---

## الخطوة 4: كتابة صيغة المصفوفة الديناميكية – تصدير البيانات المرتبة

هذا هو جوهر الدرس: سنُدخل **صيغة مصفوفة ديناميكية** تنسكب تلقائيًا بالقائمة المرتبة في الخلايا المجاورة.

```csharp
            // Step 4: Write a SORT formula into cell A1 (row 0, column 0)
            sheet.Cells[0, 0].Formula = "=SORT(A2:A6)";   // <-- **dynamic array formula**
```

عند تقييم Excel للمعادلة `=SORT(A2:A6)`, ينتج مصفوفة عمودية بالقيم مرتبة أبجديًا. بفضل سلوك الانسكاب (spill) الذي أُدخل في Excel 365، تحتل النتائج تلقائيًا `A1:A5`.

> **سؤال شائع:** *ماذا لو كان نطاق المصدر فارغًا؟*  
> تُعيد الصيغة خطأ `#SPILL!`. تجنّب ذلك بالتحقق من `rawValues.Length` قبل كتابة الصيغة، أو غلفها بـ `IFERROR(SORT(...), "")`.

---

## الخطوة 5: إجبار الحساب – تشغيل الصيغة

Aspose.Cells لا يُعيد حساب الصيغ تلقائيًا بعد تعيينها، لذا نحتاج إلى إخبار المحرك بإجراء العملية الحسابية.

```csharp
            // Recalculate the workbook so the spill range is populated
            workbook.CalculateFormula();   // <-- triggers **export sorted data**
```

**ما يحدث في الخلفية:** محرك الحساب يحلل شجرة الصيغة، يحل مراجع الخلايا، ويكتب المصفوفة الناتجة مرة أخرى في الورقة. هذه الخطوة أساسية؛ وإلا ستظهر النص `=SORT(A2:A6)` في الملف.

---

## الخطوة 6: حفظ الملف – كيفية حفظ دفتر العمل

أخيرًا، نقوم بحفظ دفتر العمل على القرص. يمكنك اختيار أي مجلد تفضله؛ فقط تأكد من أن العملية لديها صلاحية كتابة.

```csharp
            // Step 6: Save the workbook to view the result
            string outputPath = @"YOUR_DIRECTORY\sorted_output.xlsx";
            workbook.Save(outputPath);   // <-- **how to save workbook**
            System.Console.WriteLine($"Workbook saved to {outputPath}");
        }
    }
}
```

**لماذا نستخدم `Save` بدلاً من `SaveCopyAs`؟**  
`Save` يستبدل الملف الهدف، وهو مناسب لتصدير لمرة واحدة. إذا كنت بحاجة للحفاظ على الأصل دون تعديل، استدعِ `workbook.SaveCopyAs("backup.xlsx")` أولًا.

---

## مثال كامل يعمل

بجمع كل ما سبق، إليك البرنامج الكامل الذي يمكنك تجميعه الآن:

```csharp
using Aspose.Cells;
using System;

namespace WorksheetDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create a new workbook
            Workbook workbook = new Workbook();

            // 2️⃣ Add a fresh worksheet
            int sheetIdx = workbook.Worksheets.Add();
            Worksheet sheet = workbook.Worksheets[sheetIdx];

            // 3️⃣ Seed unsorted data (A2:A6)
            string[] values = { "Delta", "Alpha", "Echo", "Bravo", "Charlie" };
            for (int i = 0; i < values.Length; i++)
                sheet.Cells[i + 1, 0].PutValue(values[i]);

            // 4️⃣ Insert the SORT dynamic array formula in A1
            sheet.Cells[0, 0].Formula = "=SORT(A2:A6)";

            // 5️⃣ Calculate so the spill range fills
            workbook.CalculateFormula();

            // 6️⃣ Save the workbook
            string outFile = @"C:\Temp\sorted_output.xlsx";
            workbook.Save(outFile);
            Console.WriteLine($"✅ Workbook saved – open {outFile} to see the sorted list.");
        }
    }
}
```

### النتيجة المتوقعة

عند فتح `sorted_output.xlsx`, ستحتوي الخلية **A1** على “Alpha”، **A2** على “Bravo”، **A3** على “Charlie”، **A4** على “Delta”، و**A5** على “Echo”. تظل القائمة غير المرتبة الأصلية في **A2:A6** (نطاق المصدر)، مما يثبت أن **صيغة المصفوفة الديناميكية** نجحت في تصدير البيانات المرتبة.

---

## معالجة الحالات الخاصة والبدائل

| الحالة | ما الذي يجب فعله |
|-----------|------------|
| **نطاق المصدر أكبر من 1,048,576 صف** | ينطبق حد الصفوف في Excel؛ قسّم البيانات على عدة أوراق أو استخدم قاعدة بيانات للمعالجة الثقيلة. |
| **أنواع بيانات مختلطة (أرقام + نص)** | `SORT` يضع الأرقام قبل النص افتراضيًا. استخدم `SORTBY` مع مفتاح ترتيب مخصص إذا احتجت ترتيبًا مختلفًا. |
| **تحتاج القيم المرتبة كنطاق ثابت** | بعد الحساب، انسخ نطاق الانسكاب والصق القيم فقط (`PasteSpecial`)، ثم احذف الصيغة. |
| **استخدام OpenXML/EPPlus بدلاً من Aspose** | الخطوات هي نفسها؛ فقط استبدل `Workbook`/`Worksheet` بما يعادله في المكتبة واستدعِ `Package.Save()`. |

---

## الأسئلة المتكررة

**س: هل يعمل هذا على إصدارات Excel القديمة التي لا تدعم المصفوفات الديناميكية؟**  
ج: سيفتح الملف، لكن صيغة `SORT` ستظهر كنص وتظهر خطأ `#NAME?`. للتوافق مع الإصدارات القديمة، أنشئ القائمة المرتبة في الكود واكتب القيم مباشرة.

**س: هل يمكنني الفرز حسب عدة أعمدة؟**  
ج: بالتأكيد. استخدم `=SORT(A2:C10, {1,2}, {1,-1})` حيث يحدد الوسيط الثاني مؤشرات الأعمدة والوسيط الثالث ترتيب الفرز.

**س: ماذا لو أردت تصدير البيانات المرتبة إلى CSV؟**  
ج: بعد حفظ دفتر العمل، أعد تحميله واستدعِ `worksheet.Cells.ExportDataTableAsString` أو استخدم `CsvSaveOptions` إذا كانت مكتبتك توفر ذلك.

---

## الخطوات التالية

- **استكشاف وظائف المصفوفة الديناميكية الأخرى** مثل `FILTER`، `UNIQUE`، و`SEQUENCE`.  
- **أتمتة إنشاء المخططات** في نفس الورقة لتصوير النتائج المرتبة.  
- **دمجها مع ASP.NET Core** لتمكين المستخدمين من تنزيل الملف المُولد مباشرة عبر واجهة برمجة تطبيقات ويب.  

كل من هذه المواضيع يبني على الأساسيات التي غطيناها هنا — إنشاء دفتر عمل، إضافة ورقة، تطبيق صيغ، وحفظ الملف.

---

## الخلاصة

لقد أظهرنا لك كيفية **إنشاء ورقة عمل جديدة** في C#، وضع **صيغة مصفوفة ديناميكية**، **تصدير البيانات المرتبة**، وأخيرًا **كيفية حفظ دفتر العمل**. النهج بسيط، يتطلب بضع أسطر من الكود فقط، ويعمل بثبات عبر المنصات.  

جرّبه، عدّل نطاق المصدر، استبدل `SORT` بـ `FILTER`، أو وجه الناتج إلى خدمة تقارير. السماء هي الحد عندما تتقن أساسيات التعامل البرمجي مع Excel.

Happy coding, and may your spreadsheets always stay sorted!

## دروس ذات صلة

- [How to Create and Save an Excel Workbook as ODS Using Aspose.Cells for .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)
- [Create and Save Excel Workbook as PDF in ASP.NET Using Aspose.Cells](/cells/english/net/workbook-operations/create-save-excel-workbook-pdf-aspnet-aspose-cells/)
- [How to Create and Style Excel Tables Using Aspose.Cells for .NET | Step-by-Step Guide](/cells/english/net/tables-structured-references/aspose-cells-net-excel-tables-styling/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}