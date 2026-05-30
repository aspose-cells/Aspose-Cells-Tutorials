---
category: general
date: 2026-05-30
description: تغيير حجم خط مربع النص في Excel باستخدام C#. تعلم كيفية تعديل خط مربع
  النص في Excel بسرعة باستخدام كود خطوة بخطوة.
draft: false
keywords:
- change textbox font size
- modify excel textbox font
language: ar
og_description: تغيير حجم خط مربع النص في Excel باستخدام C#. يوضح هذا الدليل كيفية
  تعديل خط مربع النص في Excel بأمان وكفاءة.
og_title: تغيير حجم خط مربع النص في Excel باستخدام C# – دليل كامل
schemas:
- author: Aspose
  dateModified: '2026-05-30'
  description: Change textbox font size in Excel using C#. Learn how to modify excel
    textbox font quickly with step‑by‑step code.
  headline: Change Textbox Font Size in Excel with C# – Complete Guide
  type: TechArticle
- description: Change textbox font size in Excel using C#. Learn how to modify excel
    textbox font quickly with step‑by‑step code.
  name: Change Textbox Font Size in Excel with C# – Complete Guide
  steps:
  - name: Why this matters
    text: Opening the workbook via COM gives us a live object model—meaning any change
      we make reflects instantly in the file. Setting `Visible = false` speeds things
      up and avoids popping windows during automation.
  - name: Why we use `TextFrame2`
    text: '`TextFrame2` is the newer object model introduced with Office 2007. It
      supports advanced typographic features and is generally more reliable than the
      older `TextFrame`. Using it ensures our **change textbox font size** operation
      works across modern Excel versions.'
  - name: 1. Change *all* textboxes on a sheet
    text: '```csharp foreach (Excel.Shape s in xlWorksheet.Shapes) { if (s.Type.HasFlag(Excel.MsoShapeType.msoTextBox))
      { var tr = s.TextFrame2.TextRange; tr.Font.Name = fontName; tr.Font.Size = newSize;
      } } ```'
  - name: 2. Identify a textbox by its **Name** instead of index
    text: 'If you gave your textbox a meaningful name (e.g., “TitleBox”), you can
      fetch it directly:'
  type: HowTo
tags:
- Excel Interop
- C#
- Office Automation
title: تغيير حجم خط مربع النص في Excel باستخدام C# – دليل كامل
url: /ar/net/excel-shape-text-modifications/change-textbox-font-size-in-excel-with-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تغيير حجم خط صندوق النص في Excel باستخدام C# – دليل كامل

هل تحتاج إلى **تغيير حجم خط صندوق النص** في ورقة عمل Excel باستخدام C#؟ أنت في المكان الصحيح. سواءً كنت تُنشئ تقارير، تبني لوحة معلومات، أو فقط تُعدّل قالبًا، فإن تعديل مظهر صندوق النص يمكن أن يجعل جدول البيانات الخاص بك يبدو أكثر احترافية.

في هذا الدرس سنقوم أيضًا **بتعديل خط صندوق النص في Excel** بما يتجاوز مجرد الحجم — فكر في عائلة الخط، الوزن (التغميق)، وحتى التعامل مع أشكال متعددة. في النهاية ستحصل على مقطع جاهز للتنفيذ يغطي كل جانب من العملية، من فتح المصنف إلى تنظيف كائنات COM. لا إطالة، فقط كود عملي يمكنك إدراجه في مشروعك اليوم.

## المتطلبات المسبقة — ما ستحتاجه

| المتطلب | سبب الأهمية |
|-------------|----------------|
| **.NET 6+** (أو .NET Framework 4.7.2+) | يوفر مترجم C# وبيئة التشغيل. |
| **Microsoft.Office.Interop.Excel** حزمة NuGet | توفر لنا أنواع التفاعل مع COM اللازمة للتواصل مع Excel. |
| **Excel مثبت** (أي نسخة حديثة) | طبقة Interop تعمل فقط عندما يكون تطبيق Office موجودًا. |
| **معرفة أساسية بـ C#** | ستتمكن من المتابعة بسهولة، لكننا سنشرح كل سطر. |

إذا كان أي من هذه العناصر مفقودًا، توقف الآن وقم بتثبيتها؛ باقي الدليل يفترض أنها موجودة.

## الخطوة 1: إعداد المشروع واستيراد المساحات الاسمية

أولاً وقبل كل شيء—أنشئ تطبيقًا جديدًا من نوع console (أو دمجه في مشروع موجود) واستورد مساحة الأسماء الخاصة بالتفاعل.

```csharp
using System;
using Excel = Microsoft.Office.Interop.Excel;

namespace ExcelTextboxDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // We'll call the helper method that does the heavy lifting.
            ChangeTextboxFontSize(@"C:\Temp\Sample.xlsx", "Sheet1", 0, 14, "Calibri");
        }
    }
}
```

**نصيحة احترافية:** إذا كنت تستهدف .NET 6+، أضف حزمة `Microsoft.Office.Interop.Excel` عبر الأمر `dotnet add package Microsoft.Office.Interop.Excel`. هذا يضمن أن الاسم المستعار `Excel` يتم حله بشكل صحيح.

## الخطوة 2: فتح المصنف والحصول على ورقة العمل المستهدفة

الآن نحتاج إلى تشغيل Excel، فتح الملف، وتحديد الورقة التي تحتوي على صندوق النص. تغليف ذلك داخل كتلة `try/finally` يضمن تحرير كائنات COM حتى إذا حدث خطأ.

```csharp
static void ChangeTextboxFontSize(string workbookPath,
                                  string sheetName,
                                  int textboxIndex,
                                  double newSize,
                                  string fontName)
{
    Excel.Application xlApp = null;
    Excel.Workbook xlWorkbook = null;
    Excel.Worksheet xlWorksheet = null;

    try
    {
        xlApp = new Excel.Application
        {
            // Keep Excel hidden; set to true if you want to watch the changes.
            Visible = false,
            DisplayAlerts = false
        };

        xlWorkbook = xlApp.Workbooks.Open(workbookPath);
        xlWorksheet = xlWorkbook.Worksheets[sheetName] as Excel.Worksheet;
        if (xlWorksheet == null)
            throw new ArgumentException($"Worksheet '{sheetName}' not found.");
```

### لماذا هذا مهم

فتح المصنف عبر COM يمنحنا نموذج كائنات حي — أي أن أي تعديل نجريه ينعكس فورًا في الملف. ضبط `Visible = false` يسرّع العملية ويتجنب ظهور نوافذ أثناء الأتمتة.

## الخطوة 3: استرجاع شكل صندوق النص

يتعامل Excel مع صناديق النص ككائنات `Shape` ضمن مجموعة `Shapes`، وليس كمجموعة `TextBox` مخصصة. لهذا السبب يبدو الكود أدناه مختلفًا قليلاً عن المقتطف الذي قد تكون رأيته على الإنترنت.

```csharp
        // Excel stores all drawing objects (including textboxes) in the Shapes collection.
        Excel.Shapes shapes = xlWorksheet.Shapes;

        // Guard against an out‑of‑range index.
        if (textboxIndex < 0 || textboxIndex >= shapes.Count)
            throw new IndexOutOfRangeException("Textbox index is out of range.");

        // Grab the specific shape; we assume it’s a textbox.
        Excel.Shape textboxShape = shapes.Item(textboxIndex + 1); // COM collections are 1‑based.
        if (!textboxShape.Type.HasFlag(Excel.MsoShapeType.msoTextBox))
            throw new InvalidOperationException("Selected shape is not a textbox.");
```

**احذر:** مجموعة `Shapes` تبدأ من الفهرس 1، لذا نضيف `+1` إلى `textboxIndex` الذي يبدأ من الصفر الذي تمرره. نسيان ذلك يؤدي إلى أخطاء “فهرس خارج النطاق” التي قد تكون محبطة في عملية التصحيح.

## الخطوة 4: تغيير حجم خط صندوق النص (والاسم)

هنا نُجري أخيرًا **تغيير حجم خط صندوق النص**. خاصية `TextFrame2` تمنحنا الوصول إلى خيارات تنسيق النص الغني، والتي تشمل `Font.Name` و `Font.Size`.

```csharp
        // Access the text range inside the textbox.
        Excel.TextRange2 textRange = textboxShape.TextFrame2.TextRange;

        // Change the font name – this also “modifies excel textbox font”.
        textRange.Font.Name = fontName;

        // Change the font size – the core of our tutorial.
        textRange.Font.Size = newSize;

        // Optional: make the text bold for extra emphasis.
        // textRange.Font.Bold = Microsoft.Office.Core.MsoTriState.msoTrue;
```

### لماذا نستخدم `TextFrame2`

`TextFrame2` هو نموذج الكائنات الأحدث الذي تم تقديمه مع Office 2007. يدعم ميزات طباعية متقدمة وعادةً ما يكون أكثر موثوقية من `TextFrame` القديم. استخدامه يضمن أن عملية **تغيير حجم خط صندوق النص** تعمل عبر إصدارات Excel الحديثة.

## الخطوة 5: الحفظ، التنظيف، والتحقق

بعد تعديل الخط، نحتاج إلى حفظ التغييرات وإطلاق كل مرجع COM. تخطي عملية التنظيف قد يترك عمليات Excel معزولة تعمل في الخلفية.

```csharp
        // Save the workbook – you can also use SaveAs to create a copy.
        xlWorkbook.Save();

        Console.WriteLine($"Successfully changed textbox font size to {newSize} pt and font to '{fontName}'.");
    }
    catch (Exception ex)
    {
        Console.Error.WriteLine($"Error: {ex.Message}");
    }
    finally
    {
        // Release COM objects in reverse order of creation.
        if (xlWorksheet != null) System.Runtime.InteropServices.Marshal.ReleaseComObject(xlWorksheet);
        if (xlWorkbook != null)
        {
            xlWorkbook.Close(false);
            System.Runtime.InteropServices.Marshal.ReleaseComObject(xlWorkbook);
        }
        if (xlApp != null)
        {
            xlApp.Quit();
            System.Runtime.InteropServices.Marshal.ReleaseComObject(xlApp);
        }

        // Force garbage collection to clean up any remaining RCWs.
        GC.Collect();
        GC.WaitForPendingFinalizers();
    }
}
```

**نصيحة احترافية:** إذا كنت بحاجة إلى **تعديل خط صندوق النص في Excel** على العديد من أوراق العمل، غلف المنطق الداخلي داخل حلقة تتكرر عبر `Workbook.Worksheets`. فقط تذكر إعادة تعيين `textboxIndex` لكل ورقة.

## معالجة الحالات الخاصة — صناديق نص متعددة وأشكال مفقودة

في جداول البيانات الواقعية نادرًا ما يحتوي على صندوق نص واحد فقط. أدناه استراتيجيتان سريعتان يمكنك اعتمادهما دون إعادة كتابة الطريقة بالكامل.

### 1. تغيير *جميع* صناديق النص في ورقة

```csharp
foreach (Excel.Shape s in xlWorksheet.Shapes)
{
    if (s.Type.HasFlag(Excel.MsoShapeType.msoTextBox))
    {
        var tr = s.TextFrame2.TextRange;
        tr.Font.Name = fontName;
        tr.Font.Size = newSize;
    }
}
```

### 2. تحديد صندوق النص بواسطة **اسمه** بدلاً من الفهرس

إذا قمت بإعطاء صندوق النص اسمًا ذا معنى (مثلاً، “TitleBox”)، يمكنك استرجاعه مباشرةً:

```csharp
Excel.Shape namedBox = xlWorksheet.Shapes.Item("TitleBox");
namedBox.TextFrame2.TextRange.Font.Size = newSize;
```

كلا النهجين يتيحان لك **تعديل خط صندوق النص في Excel** بدقة، بغض النظر عن بنية المصنف.

## نظرة بصرية (اختياري)

إذا كنت تفضّل إشارة بصرية سريعة، تخيّل المخطط التالي:

![لقطة شاشة تُظهر ورقة عمل Excel مع صندوق نص مُبرز – توضح كيفية تغيير حجم خط صندوق النص](change-textbox-font-size.png)

*نص بديل:* *تغيير حجم خط صندوق النص في Excel – صندوق نص مُبرز جاهز لتعديل الخط.*

## مثال عملي كامل

بجمع كل شيء معًا، إليك ملفًا واحدًا يمكنك نسخه ولصقه في مشروع console وتشغيله فورًا (فقط حدّث مسار الملف واسم الورقة).

```csharp
using System;
using Excel = Microsoft.Office.Interop.Excel;

namespace ExcelTextboxDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Adjust these parameters for your environment.
            string workbookPath = @"C:\Temp\Sample.xlsx";
            string sheetName = "Sheet1";
            int textboxIndex = 0;          // First textbox on the sheet.
            double newFontSize = 14;       // Desired font size.
            string newFontName = "Calibri";

            ChangeTextboxFontSize(workbookPath, sheetName, textboxIndex, newFontSize, newFontName);
        }

        static void ChangeTextboxFontSize(string workbookPath,
                                          string sheetName,
                                          int textboxIndex,
                                          double newSize,
                                          string fontName)
        {
            Excel.Application xlApp = null;
            Excel.Workbook xlWorkbook = null;
            Excel.Worksheet xlWorksheet = null;

            try
            {
                xlApp = new Excel.Application { Visible = false, DisplayAlerts = false };
                xlWorkbook = xlApp.Workbooks.Open(workbookPath);
                xlWorksheet = xlWorkbook.Worksheets[sheetName] as Excel.Worksheet;

                if (xlWorksheet == null)


## ما الذي يجب أن تتعلمه بعد ذلك؟

- [تغيير حجم الخط في Excel](/cells/english/net/working-with-fonts-in-excel/changing-font-size/)
- [كيفية تخصيص حجم الخط في خلايا Excel باستخدام Aspose.Cells .NET | دليل كامل](/cells/english/net/formatting/customize-font-size-excel-aspose-cells-dotnet/)
- [كيفية تعيين أنماط الخط في Excel باستخدام Aspose.Cells للـ .NET (دليل خطوة بخطوة)](/cells/english/net/formatting/aspose-cells-dotnet-set-font-styles-excel/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}