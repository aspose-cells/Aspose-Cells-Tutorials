---
category: general
date: 2026-05-23
description: ضبط خلفية العمود في Excel باستخدام C# بسرعة. تعلم كيفية تنسيق عمود محدد،
  استيراد جدول بيانات Excel وتطبيق نمط العمود باستخدام مثال كود بسيط.
draft: false
keywords:
- set column background
- style specific column
- background color excel column
- import datatable excel
- apply column style
language: ar
og_description: ضبط خلفية العمود في Excel باستخدام C# في ثوانٍ. يوضح هذا الدليل كيفية
  تنسيق عمود محدد، استيراد جدول بيانات Excel، وتطبيق نمط العمود باستخدام Aspose.Cells.
og_title: تعيين خلفية العمود في إكسل باستخدام C# – دليل كامل
schemas:
- author: Aspose
  dateModified: '2026-05-23'
  description: Set column background in Excel with C# quickly. Learn how to style
    specific column, import datatable excel and apply column style using a simple
    code example.
  headline: Set Column Background in Excel with C# – Complete Guide
  type: TechArticle
- description: Set column background in Excel with C# quickly. Learn how to style
    specific column, import datatable excel and apply column style using a simple
    code example.
  name: Set Column Background in Excel with C# – Complete Guide
  steps:
  - name: Expected Output
    text: 'When you open *StyledEmployees.xlsx*, you’ll notice:'
  - name: What if I need to style multiple columns?
    text: 'Just assign a custom `Style` to each index in the `columnStyles` array.
      For example, to give column C a yellow fill:'
  - name: Can I use a different library (e.g., EPPlus)?
    text: 'Yes, the concept stays the same: create a style, apply it to a column,
      then load the `DataTable`. EPPlus uses `ExcelRange.Style.Fill` instead of `BackgroundType.Solid`.
      The code would be a bit longer, but the steps—*prepare data, create style, import,
      save*—remain identical.'
  - name: How do I handle large data sets?
    text: When dealing with thousands of rows, consider using `ImportDataTable`’s
      overload that accepts a `DataTable` **without** loading the entire sheet into
      memory. Aspose.Cells streams data efficiently, but always test memory usage
      if you’re processing massive tables.
  type: HowTo
tags:
- C#
- Excel
- Aspose.Cells
- DataTable
title: تعيين خلفية العمود في إكسل باستخدام C# – دليل كامل
url: /ar/net/excel-colors-and-background-settings/set-column-background-in-excel-with-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تعيين خلفية العمود في Excel باستخدام C# – دليل كامل

هل احتجت يومًا إلى **set column background** في ورقة عمل Excel من C# لكنك لم تكن متأكدًا من أين تبدأ؟ لست وحدك—العديد من المطورين يواجهون هذه المشكلة عندما يحاولون تنسيق جداول البيانات برمجيًا للمرة الأولى. الخبر السار؟ ببضع أسطر من الشيفرة يمكنك **style specific column**, تغيير **background color excel column**, وحتى **import datatable excel** في عملية واحدة سلسة.

في هذا البرنامج التعليمي سنستعرض مثالًا عمليًا يغطي كل شيء من إنشاء دفتر عمل إلى تطبيق نمط مخصص على العمود الأول. بحلول النهاية ستحصل على مقتطف قابل لإعادة الاستخدام يتيح لك **apply column style** دون أي جهد.

## المتطلبات الأساسية

- .NET 6.0 أو أحدث (الكود يعمل مع .NET Framework أيضًا)
- Visual Studio 2022 (أو أي بيئة تطوير C# تفضلها)
- حزمة **Aspose.Cells** على NuGet (أو أي مكتبة مشابهة تدعم `ImportDataTable` والتنسيق)
- فهم أساسي لكائنات `DataTable`

لا حاجة لأي تكوين إضافي—فقط تطبيق console بسيط يكفي.

## الخطوة 1: إعداد المشروع وتثبيت Aspose.Cells

للبدء، أنشئ مشروع console جديد:

```bash
dotnet new console -n ExcelStyleDemo
cd ExcelStyleDemo
dotnet add package Aspose.Cells
```

> **نصيحة احترافية:** إذا كنت تستخدم Visual Studio، انقر بزر الماوس الأيمن على المشروع → *Manage NuGet Packages* → ابحث عن *Aspose.Cells* وقم بتثبيتها.

توفر الحزمة لنا الفئات `Workbook` و `Style` و `BackgroundType` التي نحتاجها لاحقًا لـ **set column background**.

## الخطوة 2: تحضير DataTable تجريبي

هدفنا هو **import datatable excel** إلى ورقة العمل الأولى. لننشئ `DataTable` سريعًا ببضع صفوف حتى تتمكن من رؤية التنسيق عمليًا.

```csharp
using System;
using System.Data;
using Aspose.Cells;
using System.Drawing;   // For Color

// Helper method that returns a populated DataTable
DataTable GetSampleTable()
{
    var dt = new DataTable("Employees");
    dt.Columns.Add("Name", typeof(string));
    dt.Columns.Add("Department", typeof(string));
    dt.Columns.Add("Salary", typeof(decimal));

    dt.Rows.Add("Alice", "Finance", 72000);
    dt.Rows.Add("Bob",   "HR",      56000);
    dt.Rows.Add("Carol", "IT",      95000);
    return dt;
}
```

لماذا طريقة مساعدة؟ لأنها تحافظ على نظافة التدفق الرئيسي وتسهّل استبدال مصدر البيانات الخاص بك لاحقًا—ربما استعلام قاعدة بيانات أو استجابة API.

## الخطوة 3: إنشاء Workbook وتعريف أنماط الأعمدة

الآن سننشئ `Workbook` جديدًا ونصنع كائن `Style` يمنح العمود الأول **light‑blue background**. هذا هو جوهر **set column background**.

```csharp
// Initialize a new workbook
Workbook wb = new Workbook();

// Prepare a style array – one entry per column
Style[] columnStyles = new Style[dt.Columns.Count];

// Create a style for the first column (light‑blue background)
columnStyles[0] = wb.CreateStyle();
columnStyles[0].ForegroundColor = Color.LightBlue;
columnStyles[0].Pattern = BackgroundType.Solid;

// Optional: Define a different style for other columns (e.g., no background)
for (int i = 1; i < columnStyles.Length; i++)
{
    columnStyles[i] = wb.CreateStyle(); // default style
}
```

**لماذا نستخدم مصفوفة؟** النسخة الزائدة من `ImportDataTable` التي سنستدعيها لاحقًا تقبل مصفوفة أنماط، وتطبق كل عنصر على العمود المقابل تلقائيًا. هذه هي الطريقة الأكثر كفاءة لـ **apply column style** دون الحاجة للتكرار عبر الخلايا واحدةً تلو الأخرى.

## الخطوة 4: استيراد DataTable باستخدام مصفوفة الأنماط

هذه هي السطر السحري الذي يجمع كل شيء معًا—**import datatable excel** مع تطبيق النمط الذي عرّفناه للتو.

```csharp
// Grab the first worksheet (index 0)
Worksheet sheet = wb.Worksheets[0];

// Import the DataTable, include column headers, start at cell A1 (0,0)
sheet.Cells.ImportDataTable(dt, true, 0, 0, columnStyles);
```

علامة `true` تخبر Aspose.Cells بنسخ رؤوس الأعمدة، لذا سيظهر ملف Excel الخاص بك تمامًا كما هو في `DataTable`. مصفوفة `columnStyles` تضمن أن العمود الأول يحصل على تعبئة light‑blue بينما تبقى الأعمدة الأخرى بالافتراضي.

## الخطوة 5: حفظ Workbook والتحقق من النتيجة

أخيرًا، احفظ الـ workbook إلى القرص. يمكنك فتح الملف في Excel لرؤية **background color excel column** عمليًا.

```csharp
// Save the workbook
string outputPath = "StyledEmployees.xlsx";
wb.Save(outputPath, SaveFormat.Xlsx);

Console.WriteLine($"Workbook saved to {outputPath}. Open it to see the styled column.");
```

### النتيجة المتوقعة

عند فتح *StyledEmployees.xlsx*، ستلاحظ ما يلي:

- العمود **A** (Name) يحتوي على خلفية light‑blue.
- الأعمدة **B** و **C** تحتفظ بخلفية بيضاء افتراضية.
- جميع الصفوف من `DataTable` تظهر مع رؤوسها كما هي.

هذا كل شيء—اكتمل أول تنسيق برمجي لك في Excel.

## مثال كامل يعمل

فيما يلي البرنامج الكامل الجاهز للتنفيذ الذي يجمع جميع الخطوات معًا. انسخه إلى `Program.cs` واضغط **F5**.

```csharp
using System;
using System.Data;
using Aspose.Cells;
using System.Drawing;   // Required for Color

class Program
{
    static void Main()
    {
        // Step 2: Create sample data
        DataTable dt = GetSampleTable();

        // Step 3: Initialize workbook and define styles
        Workbook wb = new Workbook();
        Style[] columnStyles = new Style[dt.Columns.Count];

        // Style for first column (light‑blue)
        columnStyles[0] = wb.CreateStyle();
        columnStyles[0].ForegroundColor = Color.LightBlue;
        columnStyles[0].Pattern = BackgroundType.Solid;

        // Default styles for remaining columns
        for (int i = 1; i < columnStyles.Length; i++)
        {
            columnStyles[i] = wb.CreateStyle();
        }

        // Step 4: Import data with style array
        Worksheet sheet = wb.Worksheets[0];
        sheet.Cells.ImportDataTable(dt, true, 0, 0, columnStyles);

        // Step 5: Save the file
        string outputPath = "StyledEmployees.xlsx";
        wb.Save(outputPath, SaveFormat.Xlsx);
        Console.WriteLine($"Workbook saved to {outputPath}. Open it to see the styled column.");
    }

    // Helper: generate a demo DataTable
    static DataTable GetSampleTable()
    {
        var dt = new DataTable("Employees");
        dt.Columns.Add("Name", typeof(string));
        dt.Columns.Add("Department", typeof(string));
        dt.Columns.Add("Salary", typeof(decimal));

        dt.Rows.Add("Alice", "Finance", 72000);
        dt.Rows.Add("Bob",   "HR",      56000);
        dt.Rows.Add("Carol", "IT",      95000);
        return dt;
    }
}
```

![مثال على تعيين خلفية العمود](/images/set-column-background.png "تعيين خلفية العمود في Excel باستخدام C#")

*نص بديل للصورة:* **set column background** – لقطة شاشة لملف Excel المُنشأ تُظهر العمود الأول المُنسق.

## أسئلة شائعة وحالات خاصة

### ماذا لو احتجت لتنسيق أعمدة متعددة؟

ما عليك سوى تعيين `Style` مخصص لكل فهرس في مصفوفة `columnStyles`. على سبيل المثال، لإعطاء العمود C تعبئة صفراء:

```csharp
columnStyles[2] = wb.CreateStyle();
columnStyles[2].ForegroundColor = Color.Yellow;
columnStyles[2].Pattern = BackgroundType.Solid;
```

### هل يمكنني استخدام مكتبة مختلفة (مثل EPPlus)؟

نعم، المفهوم يبقى نفسه: أنشئ نمطًا، طبقه على عمود، ثم حمّل `DataTable`. يستخدم EPPlus `ExcelRange.Style.Fill` بدلاً من `BackgroundType.Solid`. سيكون الكود أطول قليلًا، لكن الخطوات—*prepare data, create style, import, save*—تبقى متطابقة.

### كيف أتعامل مع مجموعات بيانات كبيرة؟

عند التعامل مع آلاف الصفوف، فكر في استخدام النسخة الزائدة من `ImportDataTable` التي تقبل `DataTable` **بدون** تحميل الورقة بالكامل في الذاكرة. تقوم Aspose.Cells ببث البيانات بكفاءة، لكن اختبر دائمًا استهلاك الذاكرة إذا كنت تعالج جداول ضخمة.

## الخلاصة

لقد أوضحنا للتو كيفية **set column background** في Excel باستخدام C#. من خلال إنشاء مصفوفة أنماط وتمريرها إلى `ImportDataTable`، يمكنك **style specific column**, التحكم في **background color excel column**, واستيراد **import datatable excel** بسلاسة—كل ذلك مع الحفاظ على شفرة مختصرة وسهلة الصيانة.

بعد ذلك، قد ترغب في استكشاف:

- إضافة **border styles** أو **font formatting** لجعل العناوين بارزة.
- استخدام التنسيق الشرطي لتسليط الضوء على الصفوف بناءً على القيم.
- التصدير إلى صيغ أخرى مثل CSV أو PDF مع الحفاظ على الأنماط.

لا تتردد في تعديل الألوان، توسيع مصفوفة الأنماط، أو ربط مصدر بياناتك الخاص. السماء هي الحد عندما تجمع بين API القوي لـ Aspose.Cells وقليل من إبداع C#. برمجة سعيدة!

## دروس ذات صلة

- [كيفية تعيين عرض عمود Excel بالبكسل باستخدام Aspose.Cells .NET | دليل للمطورين](/cells/english/net/formatting/set-column-width-pixels-aspose-cells-dotnet/)
- [كيفية تعيين عرض العمود في Excel باستخدام Aspose.Cells لـ .NET - دليل كامل](/cells/english/net/formatting/set-column-width-excel-aspose-cells-net/)
- [تعيين عرض أعمدة Excel بالبكسل باستخدام Aspose.Cells لـ .NET | دليل خطوة بخطوة](/cells/english/net/formatting/set-excel-column-width-pixels-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}