---
category: general
date: 2026-03-18
description: استخراج التاريخ من Excel وإخراج التاريخ بصيغة yyyy‑mm‑dd في تنسيق ISO.
  تعلم كيفية قراءة تواريخ العصور اليابانية، وتحويلها، وعرض تواريخ ISO في C#.
draft: false
keywords:
- extract date from excel
- output date yyyy-mm-dd
- display date iso format
language: ar
og_description: استخراج التاريخ من إكسل وإخراج التاريخ بصيغة yyyy‑mm‑dd في تنسيق ISO.
  دليل خطوة‑بخطوة بلغة C# مع الكود الكامل والشروحات.
og_title: استخراج التاريخ من إكسل – إخراج التاريخ بصيغة yyyy‑mm‑dd في C#
tags:
- C#
- Excel
- DateTime
- Aspose.Cells
title: استخراج التاريخ من Excel وإخراج التاريخ بصيغة yyyy‑mm‑dd – دليل C# الكامل
url: /ar/net/data-loading-and-parsing/extract-date-from-excel-and-output-date-yyyy-mm-dd-complete/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# استخراج التاريخ من Excel – كيفية إظهار التاريخ بصيغة yyyy‑mm‑dd في تنسيق ISO

هل احتجت يوماً إلى **استخراج التاريخ من Excel** لكنك لم تكن متأكدًا من كيفية التعامل مع تواريخ العصور اليابانية أو الحصول على سلسلة `yyyy‑mm‑dd` نظيفة؟ لست وحدك. في العديد من مشاريع ترحيل البيانات، يخزن ملف العمل المصدر التواريخ باستخدام تقويم إمبراطور اليابان، بينما يتوقع النظام اللاحق تاريخًا متوافقًا مع ISO مثل `2024-04-01`.  

في هذا الدليل سنستعرض حلًا كاملًا وقابلًا للتنفيذ يقرأ خلية، يفسر العصر الياباني، وي **يُظهر التاريخ بصيغة yyyy‑mm‑dd**. بنهاية القراءة ستعرف بالضبط كيف **تعرض التاريخ بصيغة ISO** في أي تطبيق .NET، وستحصل على مقتطف شفرة يمكن إعادة استخدامه في مشروعك.

## ما ستحتاجه

- **.NET 6+** (أو .NET Framework 4.7.2+).  
- **Aspose.Cells for .NET** – المكتبة التي تسمح لنا بتعيين تقويم مخصص عند تحميل ملف العمل.  
- ملف Excel (`japan-date.xlsx`) يحتوي على تاريخ مخزن في خلية باستخدام العصر الياباني (مثال: `令和3年4月1日`).  
- بيئة تطوير مفضلة – Visual Studio، Rider، أو حتى VS Code ستفي بالغرض.

لا توجد حزم NuGet إضافية مطلوبة بخلاف Aspose.Cells، وتعمل الشفرة على Windows أو Linux أو macOS.

## الخطوة 1: إعداد المشروع وتثبيت Aspose.Cells

أولاً، أنشئ تطبيقًا من نوع console:

```bash
dotnet new console -n ExcelDateDemo
cd ExcelDateDemo
dotnet add package Aspose.Cells
```

> **نصيحة محترف:** إذا كنت تعمل على خادم CI، قم بتثبيت نسخة الحزمة (`Aspose.Cells 23.12`) لتضمن بناءً قابلًا لإعادة الإنتاج.

## الخطوة 2: تحميل ملف العمل باستخدام تقويم إمبراطور اليابان

المفتاح لـ **استخراج التاريخ من Excel** عندما يستخدم المصدر تقويمًا غير غريغوري هو إخبار Aspose.Cells أي تقويم يجب تطبيقه أثناء التحميل. نفعل ذلك باستخدام `LoadOptions.Calendar`.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 2: Create load options and set the Japanese Emperor calendar
        LoadOptions loadOptions = new LoadOptions
        {
            // This tells Aspose.Cells to interpret era dates correctly
            Calendar = new JapaneseEmperorCalendar()
        };

        // Step 3: Open the workbook that contains Japanese era dates
        // Replace the path with the actual location of your Excel file
        string filePath = @"YOUR_DIRECTORY\japan-date.xlsx";
        Workbook workbook = new Workbook(filePath, loadOptions);
```

**لماذا هذا مهم:** بدون التقويم المخصص، سيتعامل Aspose.Cells مع الخلية كسلسلة نصية عادية، وستفقد معلومات العصر. عند تعيين `JapaneseEmperorCalendar`، تقوم المكتبة تلقائيًا بتحويل `令和3年4月1日` إلى `2021‑04‑01` خلف الكواليس.

## الخطوة 3: استرجاع التاريخ من خلية محددة

الآن بعد أن عرف ملف العمل كيفية تفسير العصر، يمكننا قراءة الخلية كـ `DateTime`. لنفترض أن التاريخ موجود في أول ورقة عمل، الخلية **A1** (الصف 0، العمود 0).

```csharp
        // Step 4: Retrieve the date value from the first worksheet, first cell
        Worksheet sheet = workbook.Worksheets[0];
        Cell dateCell = sheet.Cells[0, 0]; // A1

        // GetDateTime() returns a System.DateTime object
        DateTime extractedDate = dateCell.GetDateTime();
```

إذا كانت الخلية فارغة أو تحتوي على قيمة غير تاريخية، فإن `GetDateTime()` سيطرح استثناء. نهج دفاعي قد يبدو هكذا:

```csharp
        if (dateCell.Type != CellValueType.IsDateTime)
        {
            Console.WriteLine("The target cell does not contain a valid date.");
            return;
        }

        DateTime extractedDate = dateCell.GetDateTime();
```

**حالة حافة:** بعض ملفات Excel القديمة تخزن التواريخ كأرقام (تواريخ متسلسلة). يتعامل Aspose.Cells مع هذه تلقائيًا، لكن يجب عليك التحقق من نوع الخلية إذا كنت تتوقع محتوى مختلط.

## الخطوة 4: إظهار التاريخ بصيغة yyyy‑mm‑dd (ISO) والتحقق

مع وجود كائن `DateTime`، تنسيقه كـ **output date yyyy‑mm‑dd** يكون سطرًا واحدًا:

```csharp
        // Step 5: Output the date in ISO format (yyyy‑mm‑dd)
        string isoDate = extractedDate.ToString("yyyy-MM-dd");
        Console.WriteLine($"Extracted date (ISO): {isoDate}");
    }
}
```

تشغيل البرنامج ضد ملف يحتوي على `令和3年4月1日` سيطبع:

```
Extracted date (ISO): 2021-04-01
```

هذا هو **display date iso format** الدقيق الذي تتطلبه العديد من الـ APIs.

## مثال كامل يعمل

بدمج جميع الأجزاء معًا، إليك البرنامج الكامل جاهزًا للنسخ واللصق:

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Load the workbook with Japanese era support
        LoadOptions loadOptions = new LoadOptions
        {
            Calendar = new JapaneseEmperorCalendar()
        };

        string filePath = @"YOUR_DIRECTORY\japan-date.xlsx";
        Workbook workbook = new Workbook(filePath, loadOptions);

        // Access the cell that holds the date (A1)
        Worksheet sheet = workbook.Worksheets[0];
        Cell dateCell = sheet.Cells[0, 0];

        // Validate the cell contains a date
        if (dateCell.Type != CellValueType.IsDateTime)
        {
            Console.WriteLine("The target cell does not contain a valid date.");
            return;
        }

        // Extract the DateTime value
        DateTime extractedDate = dateCell.GetDateTime();

        // Convert to ISO format (yyyy‑mm‑dd)
        string isoDate = extractedDate.ToString("yyyy-MM-dd");
        Console.WriteLine($"Extracted date (ISO): {isoDate}");
    }
}
```

> **ملاحظة:** استبدل `YOUR_DIRECTORY` بالمجلد الفعلي الذي يحتوي على `japan-date.xlsx`. تعمل الشفرة مع أي ورقة وأي خلية – فقط عدل الفهارس حسب الحاجة.

## التعامل مع تقاويم أخرى (اختياري)

إذا احتجت يومًا إلى **استخراج التاريخ من Excel** يستخدم التقويم البوذي التايلاندي أو التقويم العبري، ما عليك سوى استبدال كائن التقويم:

```csharp
loadOptions.Calendar = new ThaiBuddhistCalendar();   // for Thai dates
// or
loadOptions.Calendar = new HebrewCalendar();         // for Hebrew dates
```

يبقى باقي المنطق دون تغيير، مما يوضح مرونة النهج.

## الأخطاء الشائعة وكيفية تجنبها

| المشكلة | السبب | الحل |
|-------|----------------|-----|
| `GetDateTime()` يطرح `InvalidCastException` | الخلية ليست تاريخًا (قد تكون نصًا) | تحقق من `Cell.Type` قبل الاستدعاء، أو استخدم `DateTime.TryParse` على `Cell.StringValue`. |
| السنة غير صحيحة بعد التحويل | تم تحميل ملف العمل دون تعيين `Calendar` | دائمًا أنشئ `LoadOptions` مع التقويم المناسب **قبل** فتح الملف. |
| مخرجات ISO تظهر جزء الوقت (`2021-04-01 00:00:00`) | استخدمت `ToString()` بدون تحديد تنسيق | استخدم المحدد `"yyyy-MM-dd"` لإجبار **output date yyyy‑mm‑dd**. |
| الملف غير موجود | المسار النسبي يشير إلى المجلد الخطأ | استخدم `Path.Combine(Environment.CurrentDirectory, "japan-date.xlsx")` أو قدم مسارًا مطلقًا. |

## نصائح احترافية لكود جاهز للإنتاج

1. **قم بتخزين ملف العمل مؤقتًا** إذا كنت بحاجة لقراءة تواريخ متعددة من نفس الملف – فتح ملف العمل مكلف نسبيًا.  
2. **غلف منطق الاستخراج** في طريقة قابلة لإعادة الاستخدام:

   ```csharp
   static string ExtractIsoDate(string file, int sheetIdx, int row, int col)
   {
       var opts = new LoadOptions { Calendar = new JapaneseEmperorCalendar() };
       var wb = new Workbook(file, opts);
       var cell = wb.Worksheets[sheetIdx].Cells[row, col];
       if (cell.Type != CellValueType.IsDateTime) return null;
       return cell.GetDateTime().ToString("yyyy-MM-dd");
   }
   ```

3. **سجّل سلسلة العصر الأصلية** (`cell.StringValue`) جنبًا إلى جنب مع مخرجات ISO لأغراض التدقيق.  
4. **اختبر الوحدة** للطريقة باستخدام بعض ملفات Excel المضمنة التي تغطي عصورًا مختلفة (Heisei, Reiwa) لضمان الدقة.

## نظرة بصرية

فيما يلي مخطط سريع يوضح تدفق البيانات – من خلية Excel إلى سلسلة ISO.  

![Extract date from Excel example showing Excel → LoadOptions → DateTime → ISO string]  

*النص البديل: “مخطط استخراج التاريخ من Excel” يوضح خط أنابيب التحويل.*

## الخلاصة

لقد غطينا كل ما تحتاجه لـ **استخراج التاريخ من Excel**، التعامل مع قيم العصور اليابانية، و**إظهار التاريخ بصيغة yyyy‑mm‑dd** بحيث يتوافق مع **display date iso format** الذي تحبه الـ APIs الحديثة. الحل مستقل، يعمل مع أي نسخة .NET تدعم Aspose.Cells، ويمكن توسيعه لتقويمات أخرى بتغيير سطر واحد فقط.

هل لديك تقويم مختلف في ذهنك؟ أو ربما تريد استخراج تواريخ من أعمدة متعددة؟ لا تتردد في تعديل الدالة `ExtractIsoDate` أو ترك تعليق أدناه. برمجة سعيدة، ولتظل تواريخك دائمًا متزامنة مع معيار ISO!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}