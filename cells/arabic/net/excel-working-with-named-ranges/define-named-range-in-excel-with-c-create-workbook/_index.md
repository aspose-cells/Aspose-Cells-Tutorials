---
category: general
date: 2026-08-07
description: حدد نطاقًا مسمىً في Excel باستخدام C# وتعلم كيفية إضافة جدول إلى ورقة
  العمل، ثم احفظ المصنف إلى ملف برمجيًا.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- define named range excel
- save workbook to file
- add named range excel
- add table to worksheet
- create excel workbook programmatically
language: ar
lastmod: 2026-08-07
og_description: عرّف نطاقًا مسمىً في Excel باستخدام C# وتعرّف على كيفية إضافة جدول،
  وإنشاء دفتر عمل برمجيًا، وحفظ دفتر العمل إلى ملف في تدفق واحد.
og_image_alt: Screenshot of C# code that creates an Excel workbook, adds a table,
  defines a named range, and saves the file
og_title: تعريف نطاق مسمى في إكسل باستخدام C# – دليل كامل للكتاب
schemas:
- author: Aspose
  dateModified: '2026-08-07'
  description: Define named range in Excel with C# and learn how to add a table to
    a worksheet, then save workbook to file programmatically.
  headline: Define named range in Excel with C# – create workbook
  type: TechArticle
tags:
- Excel
- C#
- Aspose.Cells
- named range
- programmatic Excel
title: تعريف نطاق مسمى في Excel باستخدام C# – إنشاء دفتر عمل
url: /ar/net/excel-working-with-named-ranges/define-named-range-in-excel-with-c-create-workbook/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تعريف نطاق مسمى في Excel باستخدام C# – إنشاء دفتر عمل

إذا كنت بحاجة إلى **define named range in Excel** من كود C#، يوضح لك هذا الدرس بالضبط كيفية القيام بذلك. سترى أيضًا كيفية **add a table to a worksheet**، وإنشاء دفتر العمل **programmatically**، وأخيرًا **save workbook to file** دون مغادرة بيئة التطوير المتكاملة.

العمل مع ملفات Excel برمجياً يوفر الوقت، يزيل الأخطاء اليدوية، ويمكنك من إنشاء خطوط أنابيب تقارير مؤتمتة. في هذا الدليل ستقوم بـ:

* إنشاء دفتر عمل Excel جديد من الصفر.  
* إضافة جدول يغطي نطاق خلايا محدد.  
* تعريف نطاق مسمى ومعالجة تعارضات الأسماء.  
* حفظ دفتر العمل على القرص.

جميع الخطوات تستخدم مكتبة **Aspose.Cells for .NET**، التي تعمل مع .NET 6+ و .NET Framework 4.6+. لا يلزم أي تفاعل COM إضافي أو تثبيت Office.

## المتطلبات المسبقة

* .NET 6 SDK (أو .NET Framework 4.6+).  
* Visual Studio 2022 أو أي بيئة تطوير متوافقة مع C#.  
* حزمة NuGet لـ Aspose.Cells for .NET (`Install-Package Aspose.Cells`).  

> **نصيحة احترافية:** استخدم ترخيص التقييم المجاني أثناء الاختبار؛ استبدله بترخيص إنتاج قبل النشر.

## الخطوة 1: إنشاء دفتر عمل Excel برمجياً

العملية الأولى هي إنشاء كائن `Workbook`. هذا الكائن يمثل ملف Excel بالكامل في الذاكرة.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Create a new workbook in memory
        Workbook workbook = new Workbook();               // create an empty workbook
        Worksheet worksheet = workbook.Worksheets[0];    // get the first (default) worksheet
```

*لماذا هذا مهم*: إنشاء دفتر العمل في الكود يمنحك تحكمًا كاملاً في الأوراق، الأنماط، والبيانات قبل أن يلمس أي ملف القرص.

## الخطوة 2: إضافة جدول إلى ورقة العمل

الجدول (المعروف أيضًا باسم ListObject) يوفر تصفية، فرز، وتنسيق مدمجين. هنا نقوم بإنشاء جدول يغطي الخلايا **A1:B5** ونعطيه الاسم **SalesData**.

```csharp
        // Step 2: Define a range and convert it into a table
        Range tableRange = worksheet.Cells.CreateRange("A1:B5", true);
        ListObject table = worksheet.Tables[worksheet.Tables.Add(tableRange, true)];
        table.Name = "SalesData";

        // Populate the table with sample data
        worksheet.Cells["A1"].PutValue("Product");
        worksheet.Cells["B1"].PutValue("Units");
        worksheet.Cells["A2"].PutValue("Apples");
        worksheet.Cells["B2"].PutValue(120);
        worksheet.Cells["A3"].PutValue("Bananas");
        worksheet.Cells["B3"].PutValue(85);
        worksheet.Cells["A4"].PutValue("Cherries");
        worksheet.Cells["B4"].PutValue(45);
        worksheet.Cells["A5"].PutValue("Dates");
        worksheet.Cells["B5"].PutValue(30);
```

*لماذا هذا مهم*: إضافة جدول مبكرًا يتيح لك الإشارة إلى البيانات لاحقًا باستخدام **named range**، ويمكن استخدام المرجع الهيكلي للجدول في الصيغ.

## الخطوة 3: تعريف نطاق مسمى في Excel – معالجة التعارضات

**named range** هو معرف يشير إلى خلية أو نطاق، مما يجعل الصيغ أسهل للقراءة. إذا كان الاسم موجودًا بالفعل (مثلاً اسم الجدول **SalesData**)، فإن Excel يطرح تعارضًا. يوضح الكود أدناه كيفية التقاط هذا الاستثناء والمتابعة بأمان.

```csharp
        // Step 3: Attempt to define a named range with the same identifier as the table
        try
        {
            // This will raise an exception because "SalesData" is already used by the table
            worksheet.Names.Add("SalesData", "A1");
        }
        catch (Exception ex)
        {
            Console.WriteLine("Name conflict prevented: " + ex.Message);
        }

        // Step 4: Add a different named range – this succeeds
        worksheet.Names.Add("SalesTotal", "B6");
        worksheet.Cells["B6"].Formula = "=SUM(SalesData[Units])";
```

*لماذا هذا مهم*: معالجة تصادم الأسماء يمنع تعطل البرنامج أثناء التشغيل في الوظائف المؤتمتة. النطاق المسمى الثاني **SalesTotal** يوضح الإشارة إلى عمود الجدول في صيغة.

## الخطوة 4: حفظ دفتر العمل إلى ملف

بعد جميع التعديلات، احفظ دفتر العمل على القرص. طريقة `Save` تدعم صيغًا متعددة؛ هنا نستخدم الصيغة الافتراضية `.xlsx`.

```csharp
        // Step 5: Save the workbook to the file system
        string outputPath = @"C:\Temp\NameConflictHandled.xlsx";
        workbook.Save(outputPath, SaveFormat.Xlsx);

        Console.WriteLine($"Workbook saved successfully to {outputPath}");
    }
}
```

*لماذا هذا مهم*: استخدام **save workbook to file** برمجياً يتيح المعالجة الدفعية، توليد تقارير مجدولة، وتكامل مع واجهات برمجة تطبيقات الويب.

## الكود الكامل في عرض واحد

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Create a new workbook
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Add a table covering A1:B5 and name it "SalesData"
        Range tableRange = worksheet.Cells.CreateRange("A1:B5", true);
        ListObject table = worksheet.Tables[worksheet.Tables.Add(tableRange, true)];
        table.Name = "SalesData";

        // Fill the table with sample data
        worksheet.Cells["A1"].PutValue("Product");
        worksheet.Cells["B1"].PutValue("Units");
        worksheet.Cells["A2"].PutValue("Apples");   worksheet.Cells["B2"].PutValue(120);
        worksheet.Cells["A3"].PutValue("Bananas");  worksheet.Cells["B3"].PutValue(85);
        worksheet.Cells["A4"].PutValue("Cherries"); worksheet.Cells["B4"].PutValue(45);
        worksheet.Cells["A5"].PutValue("Dates");    worksheet.Cells["B5"].PutValue(30);

        // Try to create a defined name with the same identifier – handle the conflict
        try
        {
            worksheet.Names.Add("SalesData", "A1");
        }
        catch (Exception ex)
        {
            Console.WriteLine("Name conflict prevented: " + ex.Message);
        }

        // Add a different defined name – this succeeds
        worksheet.Names.Add("SalesTotal", "B6");
        worksheet.Cells["B6"].Formula = "=SUM(SalesData[Units])";

        // Save the workbook
        string outputPath = @"C:\Temp\NameConflictHandled.xlsx";
        workbook.Save(outputPath, SaveFormat.Xlsx);

        Console.WriteLine($"Workbook saved successfully to {outputPath}");
    }
}
```

### النتيجة المتوقعة

* ملف Excel باسم **NameConflictHandled.xlsx** يظهر في `C:\Temp`.  
* الورقة 1 تحتوي على جدول منسق **SalesData** مع صفوف المنتج‑الوحدة.  
* الخلية **B6** تظهر مجموع عمود **Units**، محسوبًا عبر النطاق المسمى **SalesTotal**.  
* وحدة التحكم تطبع رسالة حول تعارض الاسم (إن وجد) وتؤكد موقع الملف.

## أسئلة شائعة وحالات حافة

| السؤال | الجواب |
|----------|--------|
| **هل يمكنني تعريف نطاق مسمى يمتد عبر عدة أوراق عمل؟** | نعم. استخدم `worksheet.Names.Add("GlobalRange", "'Sheet1'!A1:B5")` وارجع إليه من أي ورقة. |
| **ماذا لو احتجت إلى استبدال ملف موجود؟** | استدعِ `workbook.Save(path, SaveFormat.Xlsx, new SaveOptions { Overwrite = true })`. |
| **كيف يمكنني إضافة نطاق مسمى دون حدوث تعارض عندما يكون الاسم موجودًا بالفعل؟** | استخدم `worksheet.Names.Remove("ExistingName")` قبل إضافة الجديد، أو أنشئ معرفًا فريدًا (مثلاً `Guid.NewGuid().ToString("N")`). |
| **هل هناك طريقة لتطبيق نمط على الجدول تلقائيًا؟** | عيّن `table.Style = workbook.Styles[BuiltInStyleId.TableStyleMedium9];` بعد إنشاء الجدول. |
| **هل يعمل هذا على .NET Core؟** | تدعم Aspose.Cells .NET Core، .NET 5/6/7، و .NET Framework. فقط استدعِ نفس حزمة NuGet. |

## الخلاصة

الآن تعرف كيف **define named range in Excel** باستخدام C#، **add a table to a worksheet**، و **save workbook to file** برمجياً. المثال الكامل يوضح إنشاء دفتر عمل Excel من الصفر، معالجة تعارضات الأسماء، وتوليد ملف تقرير قابل للاستخدام في تدفق واحد قابل للتكرار.

بعد ذلك، استكشف المواضيع ذات الصلة مثل **adding charts to a worksheet**، **exporting to PDF**، أو **reading existing workbooks**. كل منها يبني على الأساسيات نفسها التي تم تغطيتها هنا، لذا ستكون مستعدًا لتوسيع الحل إلى سيناريوهات أتمتة أكثر تعقيدًا. برمجة سعيدة!

## ماذا يجب أن تتعلم بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مورد يتضمن أمثلة كود كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [إنشاء نطاق مسمى للخلايا في Excel](/cells/english/net/excel-creating-formatting-named-ranges/create-named-range-of-cells/)
- [كيفية تنفيذ صيغ النطاق المسمى في .NET باستخدام Aspose.Cells لأتمتة Excel](/cells/english/net/formulas-functions/implement-named-range-formulas-net-aspose-cells/)
- [كيفية إنشاء نطاقات مسماة محلية لدفتر العمل في Excel باستخدام Aspose.Cells .NET](/cells/english/net/range-management/excel-workbook-scoped-named-ranges-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}