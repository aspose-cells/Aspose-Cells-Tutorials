---
category: general
date: 2026-07-13
description: إنشاء مصنف Excel في C# وتعلم كيفية إضافة نطاق مسمى، وتعيين اسم للجدول،
  ومعالجة تعارضات الأسماء—كل ذلك في مثال واضح واحد.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook
- add named range
- assign name to table
- set table name
- how to add range
language: ar
lastmod: 2026-07-13
og_description: إنشاء مصنف Excel في C# باستخدام Aspose.Cells. تعلّم كيفية إضافة نطاق
  مسمى، تعيين اسم الجدول، وحل تعارضات الأسماء في دليل مختصر وقابل للتنفيذ.
og_image_alt: Screenshot showing an Excel workbook with a named range and a table
  name set using C# code
og_title: إنشاء مصنف Excel في C# – إضافة نطاق مسمى وتعيين اسم الجدول
schemas:
- author: Aspose
  dateModified: '2026-07-13'
  description: Create Excel Workbook in C# and learn how to add named range, assign
    name to table, and handle naming conflicts—all in one clear example.
  headline: Create Excel Workbook in C# – Add Named Range & Set Table Name
  type: TechArticle
- description: Create Excel Workbook in C# and learn how to add named range, assign
    name to table, and handle naming conflicts—all in one clear example.
  name: Create Excel Workbook in C# – Add Named Range & Set Table Name
  steps:
  - name: '**Use a consistent prefix** (`tbl_`, `rng_`, etc.) – it instantly tells
      you what the object is.'
    text: '**Use a consistent prefix** (`tbl_`, `rng_`, etc.) – it instantly tells
      you what the object is.'
  - name: '**Stay within 255 characters** – Excel’s limit for names.'
    text: '**Stay within 255 characters** – Excel’s limit for names.'
  - name: '**Avoid spaces and special characters** – only letters, numbers, and underscores
      are safe.'
    text: '**Avoid spaces and special characters** – only letters, numbers, and underscores
      are safe.'
  - name: '**Validate before assigning** – a quick `if (!sheet.Names.Contains(name))`
      check prevents the clash we demonstrated.'
    text: '**Validate before assigning** – a quick `if (!sheet.Names.Contains(name))`
      check prevents the clash we demonstrated.'
  type: HowTo
- questions:
  - answer: Yes, but you must qualify the address with the sheet name, e.g., `"Sheet1!A1:B5"`.
      The `Names.Add` method accepts that format.
    question: Can I add a named range that spans multiple worksheets?
  - answer: Absolutely. You can pass a formula string instead of a static address,
      such as `"=OFFSET(Sheet1!$A$1,0,0,COUNT(Sheet1!$A:$A),2)"`.
    question: Does Aspose.Cells support dynamic named ranges (like OFFSET formulas)?
  - answer: 'Just set `table.Name = " ## What Should You Learn Next?


      The following tutorials cover closely related topics that build on the techniques
      demonstrated in this guide. Each resource includes complete working code examples
      with step-by-step explanations to help you master additional API features and
      explore alternative implementation approaches in your own projects.

      - [How to Create Workbook Scoped Named Ranges in Excel Using Aspose.Cells .NET](/cells/english/net/range-management/excel-workbook-scoped-named-ranges-aspose-cells-net/)
      - [How to Implement a Named Range with Workbook Scope in Aspose.Cells Java for
      Enhanced Excel Data Management](/cells/english/java/tables-structured-references/implement-named-range-workbook-scope-aspose-cells-java/)
      - [Excel Automation&#58; Create a Workbook and Add a ListBox Using Aspose.Cells
      for .NET](/cells/english/net/automation-batch-processing/excel-automation-create-workbook-add-listbox-aspose-cells/)

      {{< /blocks/products/pf/tutorial-page-section >}} {{< /blocks/products/pf/main-container
      >}} {{< /blocks/products/pf/main-wrap-class >}} {{< blocks/products/products-backtop-button
      >}}'
    question: What if I need to rename an existing table?
  type: FAQPage
tags:
- C#
- Aspose.Cells
- Excel Automation
- .NET
title: إنشاء مصنف إكسل في C# – إضافة نطاق مسمى وتعيين اسم الجدول
url: /ar/net/excel-advanced-named-ranges/create-excel-workbook-in-c-add-named-range-set-table-name/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء مصنف Excel في C# – دليل كامل لإضافة النطاقات المسماة وتعيين أسماء الجداول

هل احتجت يوماً إلى **إنشاء مصنف Excel** من الصفر وتساءلت أين تضع نطاقًا مسمى أو كيف تعطي جدولًا معرفه الخاص؟ لست وحدك. في العديد من سيناريوهات التقارير أو تصدير البيانات، ستجد نفسك تتعامل مع النطاقات والجداول، وأحيانًا تصادم الأسماء.  

في هذا الدرس سنستعرض مثالًا قابلاً للتنفيذ بالكامل **ينشئ مصنف Excel**، **يضيف نطاقًا مسمى**، ثم **يعين اسمًا لجدول**—مُظهرًا لك بالضبط ما يجب فعله عندما تتصادم الأسماء. في النهاية ستعرف “كيف” و “لماذا” كل خطوة، بالإضافة إلى بعض النصائح للحفاظ على نظافة الكود.

> **فوز سريع:** يستخدم الكود مكتبة **Aspose.Cells**، التي تعمل مع .NET 6+ ولا تتطلب تثبيت Excel على الخادم.

---

## ما ستحتاجه

- **.NET 6 SDK** (أو أي إصدار حديث من .NET)  
- حزمة **Aspose.Cells for .NET** عبر NuGet  
- بيئة تطوير متكاملة جيدة (Visual Studio، Rider، أو VS Code)  
- معرفة أساسية بـ C#—لا شيء معقد، فقط عبارات `using` المعتادة

إذا كان لديك هذه الأدوات، يمكننا القفز مباشرة إلى عملية **create excel workbook**.

---

## ## إنشاء مصنف Excel – نظرة عامة خطوة بخطوة

فيما يلي البرنامج الكامل الجاهز للنسخ واللصق. يوضح كل شيء من إنشاء المصنف إلى معالجة تعارض الأسماء عندما تحاول **assign name to table**.

```csharp
using System;
using Aspose.Cells;

namespace ExcelNamingDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Create a new workbook
            Workbook workbook = new Workbook();

            // Step 2: Add some sample data so we have a table to work with
            Worksheet sheet = workbook.Worksheets[0];
            sheet.Cells["A1"].PutValue("Product");
            sheet.Cells["B1"].PutValue("Price");
            sheet.Cells["A2"].PutValue("Apple");
            sheet.Cells["B2"].PutValue(0.99);
            sheet.Cells["A3"].PutValue("Banana");
            sheet.Cells["B3"].PutValue(0.59);
            sheet.Cells["A4"].PutValue("Cherry");
            sheet.Cells["B4"].PutValue(2.99);
            sheet.Cells["A5"].PutValue("Date");
            sheet.Cells["B5"].PutValue(3.49);

            // Step 3: Convert the data range into a table (default name Table1)
            int tableIndex = sheet.Tables.Add(sheet.Cells.CreateRange("A1:B5"), true);
            ListObject table = sheet.Tables[tableIndex];
            // At this point the table name is "Table1"

            // Step 4: Add a named range that covers the same cells
            // This is the "add named range" part of the tutorial
            sheet.Names.Add("MyRange", "A1:B5");

            // Step 5: Try to give the table the same name – this will cause a conflict
            try
            {
                table.Name = "MyRange"; // <-- assign name to table
            }
            catch (Exception ex)
            {
                // Step 6: Handle the naming conflict by outputting the error message
                Console.WriteLine("Naming conflict detected:");
                Console.WriteLine(ex.Message);
            }

            // Optional: Save the workbook to verify everything works
            workbook.Save("DemoWorkbook.xlsx");
        }
    }
}
```

**المخرجات المتوقعة** عند تشغيل البرنامج:

```
Naming conflict detected:
A name with the same text already exists.
```

وإذا فتحت *DemoWorkbook.xlsx* ستجد جدولًا اسمه **Table1** ونطاقًا مسمىً **MyRange**—تمامًا ما قصدنا، دون أي تصادم.

---

## ## إضافة نطاق مسمى – لماذا هو مهم

النطاق المسمى **named range** هو في الأساس اسم مستعار لكتلة خلايا. بدلاً من الإشارة دائمًا إلى `A1:B5`، يمكنك كتابة `MyRange` في الصيغ، أو التحقق من صحة البيانات، أو حتى في الكود. هذا يحسن قابلية القراءة ويقلل من احتمال الأخطاء الناتجة عن الأخطاء المطبعية.

في المقتطف أعلاه نستدعي:

```csharp
sheet.Names.Add("MyRange", "A1:B5");
```

- الوسيط الأول هو **الاسم** الذي ستستخدمه لاحقًا.  
- الوسيط الثاني هو **العنوان** (نسبيًا إلى ورقة العمل).  

إذا احتجت يومًا إلى **how to add range** بشكل ديناميكي، يمكنك بناء سلسلة العنوان باستخدام `Cell.GetRefersTo()` أو استخدام `Range refRange = sheet.Cells.CreateRange(startRow, startCol, totalRows, totalCols)`.

---

## ## تعيين اسم للجدول – معالجة التعارضات

الجداول (المعروفة أيضًا بـ *list objects*) لديها خاصية اسم مدمجة. بشكل افتراضي تقوم Aspose.Cells بتسمية الجداول بـ `Table1`، `Table2`، إلخ. عندما تحاول إعطاء جدول نفس المعرف لنطاق مسمى موجود، تُطلق المكتبة استثناءً—تمامًا كما يحدث في Excel.

لماذا يحدث ذلك؟

- نطاق تسمية Excel هو **على مستوى المصنف** لكل من النطاقات والجداول.  
- الأسماء المكررة تجعل الصيغ غامضة، لذا يمنع المحرك ذلك.

### نصيحة احترافية

إذا كنت بحاجة فعلًا إلى مشاركة اسم منطقي بين جدول ونطاق، فكر في **إضافة بادئة** لأحدهما، مثال:

```csharp
table.Name = "tbl_MyRange";   // safe, no conflict
```

أو أعد تسمية النطاق أولًا:

```csharp
sheet.Names["MyRange"].Name = "DataRange";
```

كلا النهجين يحافظان على مساحة الأسماء مرتبة ويتجنبان أخطاء وقت التشغيل.

---

## ## تعيين اسم للجدول – أفضل الممارسات

عند **set table name** برمجيًا، احرص على اتباع الإرشادات التالية:

1. **استخدم بادئة ثابتة** (`tbl_`، `rng_`، إلخ) – تُظهر فورًا ما هو الكائن.  
2. **ابق ضمن 255 حرفًا** – الحد الأقصى لأسماء Excel.  
3. **تجنب المسافات والرموز الخاصة** – الأحرف، الأرقام، والشرطة السفلية (_) فقط هي الآمنة.  
4. **تحقق قبل التعيين** – فحص سريع `if (!sheet.Names.Contains(name))` يمنع التعارض الذي عرضناه.

إليك طريقة مساعدة يمكنك إضافتها إلى أي مشروع:

```csharp
static void SafeSetTableName(Worksheet sheet, ListObject table, string desiredName)
{
    string finalName = desiredName;
    int suffix = 1;
    while (sheet.Names.Contains(finalName) || sheet.Tables.Contains(finalName))
    {
        finalName = $"{desiredName}_{suffix}";
        suffix++;
    }
    table.Name = finalName;
}
```

استدعاء `SafeSetTableName(sheet, table, "MyRange")` سيحول تلقائيًا `MyRange` إلى `MyRange_1` إذا كان هناك تعارض، مما يضمن أن عملية **create excel workbook** لا تتوقف بشكل غير متوقع.

---

## ## مثال عملي كامل – جمع كل الأجزاء معًا

فيما يلي نسخة مختصرة يمكنك نسخها مباشرة إلى تطبيق Console. تتضمن روتين الأمان وتوضح تدفق العملية من البداية إلى النهاية.

```csharp
using System;
using Aspose.Cells;

namespace ExcelNamingDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create the workbook
            Workbook wb = new Workbook();
            Worksheet ws = wb.Worksheets[0];

            // Populate a simple dataset
            ws.Cells["A1"].PutValue("Item");
            ws.Cells["B1"].PutValue("Quantity");
            ws.Cells["A2"].PutValue("Pen");
            ws.Cells["B2"].PutValue(10);
            ws.Cells["A3"].PutValue("Notebook");
            ws.Cells["B3"].PutValue(5);

            // Turn data into a table
            int tblIdx = ws.Tables.Add(ws.Cells.CreateRange("A1:B3"), true);
            ListObject tbl = ws.Tables[tblIdx];

            // Add a named range covering the same cells
            ws.Names.Add("MyRange", "A1:B3");

            // Safely assign a name to the table
            SafeSetTableName(ws, tbl, "MyRange");

            // Save to verify
            wb.Save("FinalDemo.xlsx");
            Console.WriteLine($"Table name set to: {tbl.Name}");
        }

        static void SafeSetTableName(Worksheet sheet, ListObject table, string desiredName)
        {
            string candidate = desiredName;
            int i = 1;
            while (sheet.Names.Contains(candidate) || sheet.Tables.Contains(candidate))
            {
                candidate = $"{desiredName}_{i}";
                i++;
            }
            table.Name = candidate;
        }
    }
}
```

تشغيل هذا السكريبت ينتج ملف `FinalDemo.xlsx` حيث يُسمى الجدول `MyRange_1` (أو لاحقة فريدة أخرى) ويظل النطاق `MyRange`. لا استثناء، لا غموض—فقط تسمية نظيفة ومحددة.

---

## ## الأسئلة المتكررة (FAQ)

**س: هل يمكنني إضافة نطاق مسمى يمتد عبر عدة أوراق عمل؟**  
ج: نعم، لكن عليك تأهيل العنوان باسم الورقة، مثال: `"Sheet1!A1:B5"`. طريقة `Names.Add` تقبل هذا الشكل.

**س: هل تدعم Aspose.Cells النطاقات المسماة الديناميكية (مثل صيغ OFFSET)؟**  
ج: بالتأكيد. يمكنك تمرير سلسلة صيغة بدلاً من عنوان ثابت، مثل `"=OFFSET(Sheet1!$A$1,0,0,COUNT(Sheet1!$A:$A),2)"`.

**س: ماذا لو احتجت إلى إعادة تسمية جدول موجود؟**  
ج: ما عليك سوى تعيين `table.Name = "

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}