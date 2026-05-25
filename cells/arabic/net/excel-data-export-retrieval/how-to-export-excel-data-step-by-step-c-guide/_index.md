---
category: general
date: 2026-03-29
description: تعلم كيفية تصدير جداول Excel إلى نص عادي، كتابة سلسلة إلى ملف، وتحويل
  جدول Excel إلى CSV أو TXT باستخدام C#. يتضمن الكود الكامل والنصائح.
draft: false
keywords:
- how to export excel
- write string to file
- convert excel table
- export table as csv
- save txt file c#
language: ar
og_description: كيفية تصدير جداول Excel إلى ملفات نصية في C#. احصل على الحل الكامل،
  الكود، وأفضل الممارسات لتحويل جداول Excel وحفظ ملفات TXT.
og_title: كيفية تصدير بيانات إكسل – دليل C# الكامل
tags:
- C#
- Excel
- File I/O
title: كيفية تصدير بيانات Excel – دليل C# خطوة بخطوة
url: /ar/net/excel-data-export-retrieval/how-to-export-excel-data-step-by-step-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تصدير بيانات Excel – دليل C# الكامل

هل تساءلت يومًا **كيفية تصدير Excel** دون فتح جدول البيانات يدويًا؟ ربما تحتاج إلى تفريغ جدول إلى ملف نصي بسيط لنظام قديم، أو تريد تصدير CSV سريع لأنابيب تحليل البيانات. في هذا الدرس سنستعرض حلًا عمليًا من البداية إلى النهاية **يكتب سلسلة إلى ملف** ويظهر لك بالضبط كيف **تحويل جدول Excel** إلى تنسيق نصي محدد باستخدام C#.

سنتناول كل شيء بدءًا من تحميل دفتر العمل، اختيار الجدول المناسب، تكوين خيارات التصدير، وأخيرًا حفظ النتيجة كملف `.txt`. في النهاية ستتمكن من **تصدير الجدول كـ CSV** (أو أي فاصل تختاره) وسترى أيضًا بعض الحيل المفيدة لـ **حفظ ملف txt في C#**. لا حاجة لأدوات خارجية—فقط بعض حزم NuGet وقليل من الشيفرة.

---

## ما ستحتاجه

- **.NET 6.0+** (أو .NET Framework 4.7.2 إذا كنت تفضل الكلاسيكي)
- **Syncfusion.XlsIO** حزمة NuGet (فئة `ExportTableOptions` موجودة هنا)
- بيئة تطوير C# أساسية (Visual Studio، VS Code، Rider—أيًا كان)
- دفتر عمل Excel يحتوي على جدول واحد على الأقل (سنستخدم `ws.Tables[0]` في المثال)

> نصيحة احترافية: إذا لم تكن لديك مكتبة Syncfusion بعد، نفّذ  
> `dotnet add package Syncfusion.XlsIO.Net.Core` من سطر الأوامر.

---

## الخطوة 1 – فتح دفتر العمل والحصول على الجدول الأول  

الخطوة الأولى هي تحميل ملف Excel والحصول على مرجع إلى ورقة العمل التي تحتوي على الجدول. هذه الخطوة حاسمة لأن عملية **تحويل جدول Excel** تعمل على كائن `ITable`، وليس على نطاقات الخلايا الخام.

```csharp
using Syncfusion.XlsIO;
using System.IO;

class ExcelExporter
{
    static void Main()
    {
        // Load the workbook (replace with your actual file path)
        using (ExcelEngine excelEngine = new ExcelEngine())
        {
            IApplication application = excelEngine.Excel;
            application.DefaultVersion = ExcelVersion.Xlsx;

            // Open the file
            FileStream stream = new FileStream(@"C:\Data\Sample.xlsx", FileMode.Open, FileAccess.Read);
            IWorkbook workbook = application.Workbooks.Open(stream);
            IWorksheet ws = workbook.Worksheets[0];   // First worksheet
```

*لماذا هذا مهم:* فتح دفتر العمل باستخدام `using` يضمن تحرير جميع الموارد غير المُدارة، مما يمنع مشاكل قفل الملف لاحقًا عندما تحاول **كتابة سلسلة إلى ملف**.

---

## الخطوة 2 – تكوين خيارات التصدير (نص عادي، بدون رؤوس، فاصل الفاصلة المنقوطة)  

الآن نخبر Syncfusion كيف نريد تسلسل الجدول. تسمح لك `ExportTableOptions` بتبديل تضمين الرؤوس، اختيار الفاصل، وتحديد ما إذا كنت تريد الحصول على سلسلة أو مصفوفة بايت.

```csharp
            // Step 2: Configure export options – plain text, omit headers, ';' delimiter
            var exportOptions = new ExportTableOptions
            {
                ExportAsString = true,      // Returns a string we can write directly
                IncludeHeaders = false,     // Skip column headers if you don’t need them
                Delimiter = ";"             // Change to ',' for classic CSV
            };
```

*لماذا هذا مهم:* ضبط `IncludeHeaders = false` غالبًا ما يتطابق مع توقعات الأنظمة المتلقية التي تعرف بالفعل ترتيب الأعمدة. تغيير الفاصل هو الطريقة التي **تُصدّر الجدول كـ CSV** باستخدام فاصل مخصص.

---

## الخطوة 3 – تصدير الجدول إلى سلسلة  

مع إعداد الخيارات، نستدعي `ExportToString`. هذه الطريقة تستخرج الجدول بالكامل (بما في ذلك جميع الصفوف) وتعيد سلسلة واحدة جاهزة للإخراج إلى ملف.

```csharp
            // Step 3: Export the first table to a string using the configured options
            ITable firstTable = ws.Tables[0];               // Access the first table
            string tableText = firstTable.ExportToString(exportOptions);
```

*لماذا هذا مهم:* استدعاء `ExportToString` يقوم بالعمل الشاق لتحويل شبكة Excel إلى تنسيق محدد. يحترم `Delimiter` الذي ضبطته، لذا تحصل على نتيجة **تصدير جدول كـ csv** نظيفة دون معالجة إضافية.

---

## الخطوة 4 – كتابة النص المُصدّر إلى ملف  

أخيرًا، نقوم بحفظ السلسلة على القرص. `File.WriteAllText` هو أبسط طريقة لـ **حفظ ملف txt في C#**؛ فهو ينشئ الملف تلقائيًا إذا لم يكن موجودًا ويستبدله إذا كان موجودًا.

```csharp
            // Step 4: Write the exported text to a file
            string outputPath = @"C:\Data\ExportedTable.txt";
            File.WriteAllText(outputPath, tableText);
            System.Console.WriteLine($"Table exported successfully to {outputPath}");
        }
    }
}
```

*لماذا هذا مهم:* بكتابة السلسلة مباشرةً، تتجنب خطوة تحويل إضافية. يحتوي الملف الآن على صفوف مثل `Value1;Value2;Value3`، جاهزة لأي محلل لاحق.

---

## مثال كامل يعمل (جميع الخطوات في مكان واحد)  

فيما يلي البرنامج الكامل الجاهز للنسخ واللصق الذي يجمع كل ما ناقشناه. يتضمن معالجة الأخطاء وتعليقات للتوضيح.

```csharp
using Syncfusion.XlsIO;
using System;
using System.IO;

class ExcelExporter
{
    static void Main()
    {
        try
        {
            // 1️⃣ Load workbook and get first worksheet
            using (ExcelEngine excelEngine = new ExcelEngine())
            {
                IApplication app = excelEngine.Excel;
                app.DefaultVersion = ExcelVersion.Xlsx;

                string sourcePath = @"C:\Data\Sample.xlsx";
                using (FileStream fs = new FileStream(sourcePath, FileMode.Open, FileAccess.Read))
                {
                    IWorkbook wb = app.Workbooks.Open(fs);
                    IWorksheet ws = wb.Worksheets[0]; // first sheet

                    // 2️⃣ Set export options (plain text, no headers, ';' delimiter)
                    var opts = new ExportTableOptions
                    {
                        ExportAsString = true,
                        IncludeHeaders = false,
                        Delimiter = ";"
                    };

                    // 3️⃣ Export the first table to a string
                    ITable table = ws.Tables[0];
                    string csvText = table.ExportToString(opts);

                    // 4️⃣ Save the string to a .txt file
                    string destPath = @"C:\Data\ExportedTable.txt";
                    File.WriteAllText(destPath, csvText);

                    Console.WriteLine($"✅ Export complete! File saved at: {destPath}");
                }
            }
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"❌ Something went wrong: {ex.Message}");
        }
    }
}
```

**الناتج المتوقع** (محتوى `ExportedTable.txt`):

```
John;Doe;35
Jane;Smith;28
Bob;Brown;42
```

كل سطر يتCorrespond إلى صف من جدول Excel الأصلي، مع قيم مفصولة بفواصل منقوطة. إذا غيرت `Delimiter = ","` ستحصل على ملف CSV كلاسيكي بدلاً من ذلك.

---

## أسئلة شائعة وحالات خاصة  

### ماذا لو كان دفتر العمل يحتوي على جداول متعددة؟  
يمكنك ببساطة تغيير `ws.Tables[0]` إلى الفهرس المناسب، أو التكرار عبر `ws.Tables`:

```csharp
foreach (var tbl in ws.Tables)
{
    string txt = tbl.ExportToString(opts);
    // Save each table to a separate file or concatenate as needed
}
```

### كيف يمكنني تضمين رؤوس الأعمدة؟  
اضبط `IncludeHeaders = true` في `ExportTableOptions`. هذا مفيد عندما يتوقع النظام المتلقي صفًا رأسياً.

### هل يمكنني التصدير إلى مجلد مختلف بشكل ديناميكي؟  
بالطبع. استخدم `Path.Combine` مع `Environment.GetFolderPath(Environment.SpecialFolder.Desktop)` أو أي مسار يقدمه المستخدم لجعل الحل أكثر مرونة.

### ماذا عن الملفات الكبيرة؟  
للجداول الضخمة، فكر في تدفق الإخراج بدلاً من تحميل السلسلة بالكامل في الذاكرة:

```csharp
using (StreamWriter writer = new StreamWriter(outputPath))
{
    writer.Write(table.ExportToString(opts));
}
```

### هل يعمل هذا على .NET Core؟  
نعم—Syncfusion.XlsIO يدعم .NET 5/6/7. فقط أشر إلى حزمة NuGet المناسبة وستكون جاهزًا.

---

## نصائح احترافية لتصديرات موثوقة  

- **تحقق من صحة مسار الملف** قبل الكتابة. سيؤدي عدم وجود المجلد إلى رمي استثناء `DirectoryNotFoundException`.  
- **تحقق من `ExportAsString`** فقط عندما يتناسب الجدول بشكل مريح في الذاكرة؛ وإلا، استخدم `ExportToStream` لمجموعات البيانات الضخمة.  
- **انتبه للثقافة**: إذا كانت بياناتك تحتوي على فواصل كفواصل عشرية، اختر فاصلة منقوطة (`;`) أو علامة تبويب (`\t`) كفاصل لتجنب أخطاء تحليل CSV.  
- **قفل الإصدار**: تقوم Syncfusion أحيانًا بتغيير توقيعات API. قم بتثبيت نسخة NuGet (`<PackageReference Include="Syncfusion.XlsIO.Net.Core" Version="21.2.0.44" />`) للحفاظ على إمكانية إعادة بناء المشروع.

---

## الخاتمة  

في هذا الدليل أظهرنا **كيفية تصدير جداول Excel** إلى ملفات نصية عادية باستخدام C#. من خلال تحميل دفتر العمل، تكوين `ExportTableOptions`، تصدير الجدول إلى سلسلة، وأخيرًا **كتابة السلسلة إلى ملف**، لديك الآن نمط قوي لمهام **تحويل جدول Excel**، **تصدير جدول كـ csv**، و**حفظ ملف txt في C#**.

لا تتردد في التجربة—غيّر الفاصل، أضف الرؤوس، أو كرّر عبر جداول متعددة. نفس النهج يعمل على إنشاء تقارير CSV، إمداد البيانات إلى محللات قديمة، أو ببساطة أرشفة محتويات جداول البيانات كملفات نصية خفيفة.

هل لديك سيناريوهات أخرى ترغب في معالجتها؟ ربما تحتاج إلى **كتابة سلسلة إلى ملف** بشكل غير متزامن، أو تريد ضغط الإخراج مباشرة. اطلع على دروسنا القادمة حول *الإدخال/الإخراج غير المتزامن للملفات في C#* و*ضغط الملفات باستخدام .NET* للاستمرار في التقدم.

برمجة سعيدة! 🚀

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}