---
category: general
date: 2026-10-01
description: تعلم كيفية إنشاء مصنف Excel باستخدام C# وتطبيق تنسيق رقم مخصص، وتحديد
  عدد المنازل العشرية للخلية، وحفظ المصنف بصيغة XLSX في دليل شامل خطوة بخطوة.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook c#
- apply custom number format
- how to format numbers excel
- set cell decimal places
- save workbook as xlsx
language: ar
lastmod: 2026-10-01
og_description: إنشاء مصنف Excel باستخدام C# مع تنسيق رقم مخصص، وتحديد عدد المنازل
  العشرية للخلية، وحفظ المصنف بصيغة XLSX. اتبع هذا الدليل الكامل للحصول على مخرجات
  رقمية دقيقة.
og_image_alt: Screenshot of an Excel sheet showing numbers rounded to four significant
  digits
og_title: إنشاء مصنف Excel باستخدام C# – تنسيق أرقام مخصص وتصدير XLSX
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Learn how to create Excel workbook C# and apply custom number format,
    set cell decimal places, and save workbook as XLSX in a complete step‑by‑step
    guide.
  headline: How to create Excel workbook C# with custom number formatting
  type: TechArticle
- description: Learn how to create Excel workbook C# and apply custom number format,
    set cell decimal places, and save workbook as XLSX in a complete step‑by‑step
    guide.
  name: How to create Excel workbook C# with custom number formatting
  steps:
  - name: Run the program (`dotnet run`).
    text: Run the program (`dotnet run`).
  - name: Open `SigDigits.xlsx`.
    text: Open `SigDigits.xlsx`.
  - name: Confirm that **A1** reads `123.5`.
    text: Confirm that **A1** reads `123.5`.
  - name: If you open the file’s XML (`.xlsx` is a zip archive), you’ll see the custom
      format `"0.######"` stored in the `<c>` element’s `s` attribute.
    text: If you open the file’s XML (`.xlsx` is a zip archive), you’ll see the custom
      format `"0.######"` stored in the `<c>` element’s `s` attribute.
  type: HowTo
tags:
- Excel
- C#
- Aspose.Cells
title: كيفية إنشاء مصنف إكسل باستخدام C# مع تنسيق أرقام مخصص
url: /ar/net/excel-custom-number-date-formatting/how-to-create-excel-workbook-c-with-custom-number-formatting/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية إنشاء ملف Excel باستخدام C# مع تنسيق أرقام مخصص

إذا كنت بحاجة إلى **إنشاء ملف Excel باستخدام C#** يعرض الأرقام بالضبط كما تريد، يوضح لك هذا الدليل كيفية القيام بذلك في بضع خطوات واضحة. ستتعلم تطبيق تنسيق رقم مخصص، ضبط عدد المنازل العشرية للخلية، وأخيرًا **حفظ الملف بصيغة xlsx** للاستخدام اللاحق.

التعامل مع البيانات الرقمية غالبًا ما يتطلب موازنة بين الدقة وسهولة القراءة. بنهاية هذا الشرح ستحصل على نمط قابل لإعادة الاستخدام يحد من عدد الأرقام المعروضة إلى عدد محدد من الأرقام ذات الدلالة مع الحفاظ على القيمة الأصلية في الملف. لا تحتاج إلى أي سكريبتات خارجية—فقط C# ومكتبة Aspose.Cells.

## المتطلبات المسبقة

قبل أن تبدأ، تأكد من وجود ما يلي:

* .NET 6.0 SDK أو أحدث مثبت  
* Visual Studio 2022 (أو أي بيئة تطوير C#)  
* حزمة **Aspose.Cells for .NET** من NuGet (`Install-Package Aspose.Cells`) – هذه المكتبة توفر الفئات `Workbook`، `Worksheet`، و `ExportTableOptions` المستخدمة في الأمثلة.  

هذه المتطلبات قليلة؛ نفس الكود يعمل على .NET Core، .NET Framework، وحتى في Azure Functions.

## الخطوة 1: إنشاء ملف Excel C# – تهيئة الملف

العملية الأولى هي إنشاء كائن `Workbook` جديد. هذا الكائن يمثل ملف Excel بالكامل في الذاكرة ويحتوي تلقائيًا على ورقة عمل افتراضية.

```csharp
using Aspose.Cells;

namespace ExcelDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Create a new workbook and get the first worksheet
            Workbook workbook = new Workbook();               // creates an empty .xlsx container
            Worksheet sheet = workbook.Worksheets[0];         // reference to the default sheet
```

**لماذا هذا مهم:**  
إنشاء الملف مسبقًا يمنحك لوحة رسم نظيفة. ورقة العمل الافتراضية (`Worksheets[0]`) جاهزة لإدخال البيانات، لذا لا تحتاج إلى إضافة ورقة جديدة إلا إذا كان سيناريوك يتطلب عدة علامات تبويب.

## الخطوة 2: كتابة قيمة رقمية إلى خلية

الآن ضع رقمًا تجريبيًا في الخلية **A1**. القيمة التي نستخدمها (`123.456789`) تحتوي على منازل عشرية أكثر مما نريد عرضه في النهاية، مما يسمح لنا بإظهار عملية التقريب لاحقًا.

```csharp
            // Step 2: Write a numeric value to cell A1
            sheet.Cells[0, 0].PutValue(123.456789); // row 0, column 0 = A1
```

**نصيحة:** `PutValue` يكتشف نوع البيانات تلقائيًا، لذا لا تحتاج إلى تحويل الرقم إلى سلسلة.

## الخطوة 3: تطبيق تنسيق رقم مخصص – تحديد عدد المنازل العشرية الظاهرة

للتحكم في طريقة عرض Excel للرقم، ننشئ كائن `Style` مع **تنسيق رقم مخصص**. النمط `"0.######"` يخبر Excel بعرض حتى ستة منازل عشرية مع حذف الأصفار الزائدة في النهاية.

```csharp
            // Step 3: Define a custom number format (up to 6 decimal places) and apply it
            Style customStyle = workbook.CreateStyle();
            customStyle.Custom = "0.######";               // up to 6 decimals, no trailing zeros
            sheet.Cells[0, 0].SetStyle(customStyle);
```

**كيف يعمل ذلك:**  
سلسلة التنسيق تتبع صsyntax تنسيق Excel المخصص. `0` يجبر وجود رقم، بينما `#` يعرض الرقم فقط إذا كان ذا دلالة. بدمجهما تحصل على عرض مرن لا يزال يحافظ على الدقة الأصلية.

## الخطوة 4: ضبط منازل الأرقام للخلية – باستخدام ExportTableOptions

إذا كنت بحاجة إلى **ضبط منازل الأرقام للخلية** للبيانات المصدرة (مثلًا عند التحويل إلى DataTable)، تتيح لك Aspose.Cells تحديد عدد **الأرقام ذات الدلالة**. هذه الخطوة تضمن أن ملف CSV أو DataTable المصدّر يحترم قواعد التقريب التي طبقتها في المصنف.

```csharp
            // Step 4: Configure export options to limit the output to 4 significant digits
            ExportTableOptions exportOptions = new ExportTableOptions();
            exportOptions.SignificantDigits = 4;           // round to 4 significant figures
```

**لماذا نستخدم `SignificantDigits`؟**  
على عكس عدد ثابت من المنازل العشرية، الأرقام ذات الدلالة تحافظ على مقدار الرقم مع تقليل الدقة، وهو ما يتوقعه المحللون غالبًا عند تلخيص البيانات.

## الخطوة 5: تصدير بيانات الورقة و**حفظ الملف بصيغة xlsx**

أخيرًا، صدّر البيانات (إذا كنت تحتاج إلى DataTable) واحفظ المصنف على القرص. استدعاء `ExportDataTable` يطبق خيارات `ExportTableOptions` التي ضبطناها، و`workbook.Save` يكتب ملف XLSX قياسي.

```csharp
            // Step 5: Export the worksheet data using the configured options and save the workbook
            sheet.ExportDataTable(sheet.Cells.MaxDisplayRange, true, exportOptions);
            workbook.Save("SigDigits.xlsx");               // saves to the application’s working folder
        }
    }
}
```

**النتيجة المتوقعة:**  
عند فتح *SigDigits.xlsx* في Excel، تظهر الخلية **A1** القيمة `123.5`. القيمة الفعلية تظل `123.456789`، لكن الرقم المعروض يلتزم بقاعدة الأربعة أرقام ذات دلالة. إذا صدّرت الورقة إلى DataTable، ستظهر القيمة في الجدول أيضًا مقربة إلى `123.5`.

---

## تطبيق تنسيق رقم مخصص على خلايا إضافية

إذا كنت بحاجة إلى تنسيق نطاق بدلاً من خلية واحدة، أعد استخدام كائن `Style`:

```csharp
// Apply the same custom style to B2:C5
Range range = sheet.Cells.CreateRange("B2:C5");
range.ApplyStyle(customStyle, new StyleFlag { NumberFormat = true });
```

**نصيحة احترافية:** إعادة استخدام كائن النمط يقلل من استهلاك الذاكرة ويضمن تنسيقًا متسقًا عبر الورقة بأكملها.

## كيفية تنسيق أرقام Excel باستخدام C# – تنويعات شائعة

| السيناريو | سلسلة التنسيق | النتيجة |
|----------|---------------|--------|
| عدد ثابت بمكانين عشريين | `"0.00"` | `123.46` |
| عملة (US) | `"$#,##0.00"` | `$123.46` |
| نسبة مئوية بمنزل عشري واحد | `"0.0%"` | `12,346.0%` |
| صيغة علمية | `"0.00E+00"` | `1.23E+02` |

اختر النمط الذي يتوافق مع متطلبات تقاريرك. جميع الأنماط متوافقة مع الخاصية `Style.Custom` التي تم توضيحها سابقًا.

## ضبط منازل الأرقام للخلية ديناميكيًا بناءً على إدخال المستخدم

أحيانًا لا تكون الدقة المطلوبة معروفة وقت التجميع. يمكنك بناء سلسلة التنسيق في وقت التشغيل:

```csharp
int decimals = 3; // could come from a UI textbox
string format = "0." + new string('#', decimals);
customStyle.Custom = format;
sheet.Cells["A2"].PutValue(987.654321);
sheet.Cells["A2"].SetStyle(customStyle);
```

**حالة حافة:** إذا كان `decimals` يساوي صفرًا، يصبح التنسيق `"0"` (عرض كعدد صحيح). احرص دائمًا على التحقق من صحة إدخال المستخدم لتجنب سلاسل تنسيق غير صالحة.

## حفظ الملف بصيغة XLSX – أفضل الممارسات

* **استخدام مسارات مطلقة** عند الكتابة إلى دليل معروف (`Path.Combine(Environment.CurrentDirectory, "output.xlsx")`).  
* **تحرير** كائن `Workbook` إذا وضعتَه داخل عبارة `using` لتحرير الموارد غير المُدارة بسرعة:

```csharp
using (Workbook wb = new Workbook())
{
    // ...populate workbook...
    wb.Save(Path.Combine(@"C:\Exports", "Report.xlsx"));
}
```

* **توافق الإصدارات:** Aspose.Cells يكتب ملفات متوافقة مع Excel 2010‑2023، لذا لن يواجه المستخدمون اللاحقون مشاكل تنسيق.

---

## مثال كامل يعمل

فيما يلي البرنامج الكامل الذي يمكنك نسخه، لصقه، وتشغيله فورًا. يتضمن جميع توجيهات `using` الضرورية، التعليقات، ومعالجة الأخطاء.

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
            try
            {
                // 1️⃣ Create workbook and get the first worksheet
                Workbook workbook = new Workbook();
                Worksheet sheet = workbook.Worksheets[0];

                // 2️⃣ Write a high‑precision number to A1
                sheet.Cells[0, 0].PutValue(123.456789);

                // 3️⃣ Apply a custom number format (up to 6 decimals)
                Style customStyle = workbook.CreateStyle();
                customStyle.Custom = "0.######";
                sheet.Cells[0, 0].SetStyle(customStyle);

                // 4️⃣ Configure export options for 4 significant digits
                ExportTableOptions exportOptions = new ExportTableOptions
                {
                    SignificantDigits = 4
                };

                // 5️⃣ Export data (optional) and save the workbook as XLSX
                sheet.ExportDataTable(sheet.Cells.MaxDisplayRange, true, exportOptions);
                string outputPath = Path.Combine(Environment.CurrentDirectory, "SigDigits.xlsx");
                workbook.Save(outputPath);

                Console.WriteLine($"Workbook saved successfully at: {outputPath}");
                Console.WriteLine("Cell A1 displays: " + sheet.Cells["A1"].StringValue);
            }
            catch (Exception ex)
            {
                Console.Error.WriteLine($"Error creating workbook: {ex.Message}");
            }
        }
    }
}
```

**خطوات التحقق**

1. شغّل البرنامج (`dotnet run`).  
2. افتح `SigDigits.xlsx`.  
3. تأكد من أن **A1** يقرأ `123.5`.  
4. إذا فتحت ملف XML الخاص بالملف (`.xlsx` هو أرشيف zip)، ستجد التنسيق المخصص `"0.######"` مخزنًا في سمة `s` للعنصر `<c>`.

---

## الخلاصة

في هذا الشرح تعلمت كيفية **إنشاء ملف Excel باستخدام C#**، **تطبيق تنسيق رقم مخصص**، **ضبط منازل الأرقام للخلية**، و**حفظ الملف بصيغة xlsx** باستخدام Aspose.Cells. يوضح الحل كلًا من التنسيق البصري داخل Excel وتقريب البيانات عند التصدير عبر `ExportTableOptions`.  

من هنا يمكنك:

* توسيع النهج ليشمل نطاقات أو جداول كاملة.  
* دمج أنماط متعددة (خطوط، حدود) باستخدام `StyleFlag`.  
* أتمتة إنشاء التقارير عبر حلقة على مصادر البيانات وتطبيق نفس منطق التنسيق.  

لا تتردد في تجربة سلاسل تنسيق مختلفة، عدد المنازل العشرية، أو خيارات التصدير لتتناسب مع احتياجات تقاريرك الخاصة. برمجة سعيدة!

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مورد يتضمن أمثلة شاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [Create Excel Workbook C# – Apply Currency Format and Import DataTable](/cells/english/net/excel-data-import-export/create-excel-workbook-c-apply-currency-format-and-import-dat/)
- [Create Excel Workbook C# – Step‑by‑Step Guide with Conditional Formatting](/cells/english/net/excel-conditional-formatting/create-excel-workbook-c-step-by-step-guide-with-conditional/)
- [Create Excel Workbook C# – Add Comment & Save as XLSX](/cells/english/net/excel-comment-annotation/create-excel-workbook-c-add-comment-save-as-xlsx/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}