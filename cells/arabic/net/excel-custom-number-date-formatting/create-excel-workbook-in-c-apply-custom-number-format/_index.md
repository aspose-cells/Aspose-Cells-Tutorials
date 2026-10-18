---
category: general
date: 2026-05-23
description: إنشاء مصنف إكسل في C# وتعلم كيفية تطبيق تنسيق رقم مخصص، وضبط نمط الخلية
  برمجيًا، وتنسيق الخلية بالصيغة العلمية، ثم حفظ المصنف بصيغة xlsx.
draft: false
keywords:
- create excel workbook
- apply custom number format
- format cell scientific notation
- set cell style programmatically
- save workbook to xlsx
language: ar
og_description: إنشاء مصنف إكسل في C# بسرعة. تعلم تطبيق تنسيق أرقام مخصص، وتنسيق الخلايا
  برمجياً، وتنسيق الصيغة العلمية، وحفظه كملف xlsx.
og_title: إنشاء مصنف إكسل في C# – تطبيق تنسيق رقم مخصص
schemas:
- author: Aspose
  dateModified: '2026-05-23'
  description: Create excel workbook in C# and learn how to apply custom number format,
    set cell style programmatically, format cell scientific notation, then save workbook
    to xlsx.
  headline: Create Excel Workbook in C# – Apply Custom Number Format
  type: TechArticle
tags:
- C#
- Excel
- Aspose.Cells
- Automation
title: إنشاء مصنف Excel في C# – تطبيق تنسيق رقم مخصص
url: /ar/net/excel-custom-number-date-formatting/create-excel-workbook-in-c-apply-custom-number-format/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء مصنف Excel في C# – تطبيق تنسيق رقم مخصص

إنشاء مصنف Excel في C# أسهل مما قد تتصور. في هذا الدليل سنرشدك إلى تطبيق تنسيق رقم مخصص، تنسيق خلية بصيغة علمية، ضبط نمط الخلية برمجياً، وأخيراً حفظ المصنف كملف xlsx.

إذا كنت قد حدقت يوماً في جدول بيانات فارغ وتساءلت كيف يمكنك أتمتة كل شيء—من ملء البيانات إلى جعل الأرقام تظهر بالضبط كما تحتاج—فهذا الدرس لك. في النهاية ستحصل على ملف Excel كامل الوظائف يمكنك فتحه في أي برنامج جداول، وستفهم **لماذا** كل خطوة مهمة، وليس فقط **كيف** تكتب الكود.

## ما ستحتاجه

- **.NET 6+** (أو أي إطار .NET حديث يدعم المكتبة)  
- **Aspose.Cells for .NET** (أو أي API آخر يعرّف الفئات `Workbook`، `Cell`، و `CellFormat`)  
- قليل من الخبرة في C# – إذا كنت تستطيع كتابة `Console.WriteLine` فأنت جاهز.

لا ملفات إعداد إضافية، لا تفاعل COM، وبالتأكيد لا حاجة لتثبيت Excel يدويًا.

---

## إنشاء مصنف Excel – تهيئة كائن Workbook

أول شيء علينا فعله هو إنشاء مصنف فارغ. فكر في فئة `Workbook` كقماش فارغ سترسم عليه الصفوف والأعمدة والأنماط.

```csharp
using Aspose.Cells;   // Make sure the Aspose.Cells namespace is referenced

// Step 1: Create a new workbook instance
Workbook workbook = new Workbook();
```

هذا كل شيء—سطر واحد وستحصل على ملف Excel جديد كليًا في الذاكرة. منشئ `Workbook` ينشئ مجموعة الأوراق الافتراضية، لذا يمكنك البدء في إضافة البيانات فورًا.

> **نصيحة احترافية:** إذا كنت بحاجة إلى عدة أوراق، يمكنك استدعاء `workbook.Worksheets.Add()` قبل البدء في ملء الخلايا.

![مثال على إنشاء مصنف Excel](image-placeholder.png "لقطة شاشة لإنشاء مصنف Excel")

*نص بديل للصورة: مثال على إنشاء مصنف Excel يظهر ورقة Excel فارغة في بيئة التطوير المتكاملة.*

## تطبيق تنسيق رقم مخصص على خلية

الآن بعد أن المصنف موجود، دعنا نضع رقمًا في الخلية **A1** ونمنحه تنسيقًا مخصصًا. تنسيقات الأرقام المخصصة تتيح لك التحكم في طريقة ظهور الأرقام—عملة، نسب مئوية، تواريخ، أو في حالتنا، صيغة علمية.

```csharp
// Step 2: Grab the first worksheet and the cell at A1 (row 0, column 0)
Worksheet sheet = workbook.Worksheets[0];
Cell cell = sheet.Cells[0, 0];

// Step 3: Insert a numeric value
cell.PutValue(12345.6789);

// Step 4: Retrieve the current style so we can modify its Number format
Style style = cell.GetStyle();

// Step 5: Define a custom scientific notation format with two decimal places
style.Custom = "0.00E+00";   // This is the “apply custom number format” part

// Step 6: Push the modified style back onto the cell
cell.SetStyle(style);
```

لماذا نُجلب النمط أولاً؟ لأن كائن `Cell` يخزن كائن **Style** يحتوي على الخطوط، الحدود، المحاذاة، وتنسيق الأرقام كلها في مكان واحد. بتعديل خاصية `Custom` نخبر Excel بـ “عرض هذه القيمة بصيغة علمية مع منزلتين عشريتين”.

> **سؤال شائع:** *هل يمكنني استخدام تنسيق مدمج بدلًا من مخصص؟*  
> نعم—عيّن `style.Number = 10` للحصول على تنسيق علمي مدمج، لكن السلسلة المخصصة تمنحك تحكمًا دقيقًا في عدد الأرقام العشرية.

## ضبط نمط الخلية برمجياً (ما وراء تنسيق الرقم)

غالبًا ما تريد أكثر من مجرد تنسيق رقم. دعنا نضيف خطًا عريضًا وخلفية رمادية فاتحة لجعل الخلية بارزة.

```csharp
// Optional: Enhance the cell appearance
style.Font.IsBold = true;
style.ForegroundColor = System.Drawing.Color.LightGray;
style.Pattern = BackgroundType.Solid;

// Re‑apply the enriched style
cell.SetStyle(style);
```

لاحظ أننا نعيد استخدام نفس كائن `style` الذي عدلناه سابقًا. هذه هي ميزة **ضبط نمط الخلية برمجياً**—تستدعي النمط مرة واحدة فقط، تعدل الخصائص التي تحتاجها، وتعيد كتابته. لا حاجة لإعادة إنشاء الكائنات أو فقدان تنسيق الرقم الذي حددته مسبقًا.

## تنسيق الخلية بصيغة علمية (معالجة الحالات الخاصة)

إذا كنت تتعامل مع أرقام كبيرة جدًا أو صغيرة جدًا، فإن الصيغة العلمية تنقذ الموقف. التنسيق المخصص الذي استخدمناه (`0.00E+00`) يضمن رقمين بعد الفاصلة العشرية ويضيف علامة زائد للأسس. إليك فحصًا سريعًا:

```csharp
// Verify the format by inserting another extreme value
Cell extraCell = sheet.Cells[1, 0]; // B2
extraCell.PutValue(0.00001234);
extraCell.SetStyle(style); // Reuse the same style with scientific notation
```

عند فتح الملف الناتج، ستظهر الخلية B2 كـ `1.23E-05`، مما يؤكد أن توجيه **تنسيق الخلية بصيغة علمية** يعمل لكل من الأرقام الكبيرة والصغيرة.

## حفظ المصنف كملف XLSX

تنتهي المتعة عندما تقوم فعليًا بكتابة الملف إلى القرص. طريقة `Save` تتولى الجزء الصعب، حيث تحول التمثيل داخل الذاكرة إلى حزمة `.xlsx` صحيحة.

```csharp
// Step 7: Persist the workbook
string outputPath = @"C:\Temp\CustomFormatted.xlsx";
workbook.Save(outputPath, SaveFormat.Xlsx);
```

هذا السطر يحقق هدف **حفظ المصنف كملف xlsx**. إذا لم يكن الدليل موجودًا، ستُطلق `Save` استثناءً—لذا تأكد من إنشاء المجلد مسبقًا أو غلف الاستدعاء بكتلة try/catch.

```csharp
try
{
    workbook.Save(outputPath, SaveFormat.Xlsx);
    Console.WriteLine($"Workbook saved successfully to {outputPath}");
}
catch (Exception ex)
{
    Console.Error.WriteLine($"Failed to save workbook: {ex.Message}");
}
```

الآن لديك ملف Excel جاهز للمشاركة يحتوي على رقم علمي منسق بشكل جميل، نمط عريض، وخلفية رمادية فاتحة.

## مثال كامل يعمل

فيما يلي البرنامج الكامل الجاهز للنسخ واللصق الذي يجمع كل الأجزاء معًا. يتم تجميعه كتطبيق Console، لكن يمكنك نقل المنطق إلى أي مشروع C#.

```csharp
using System;
using Aspose.Cells;
using System.Drawing;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new workbook
        Workbook workbook = new Workbook();

        // 2️⃣ Access the first worksheet and target cell A1
        Worksheet sheet = workbook.Worksheets[0];
        Cell cell = sheet.Cells[0, 0];

        // 3️⃣ Insert a numeric value
        cell.PutValue(12345.6789);

        // 4️⃣ Retrieve and customize the cell style
        Style style = cell.GetStyle();
        style.Custom = "0.00E+00";               // apply custom number format (scientific)
        style.Font.IsBold = true;               // set cell style programmatically
        style.ForegroundColor = Color.LightGray;
        style.Pattern = BackgroundType.Solid;

        // 5️⃣ Apply the style back to the cell
        cell.SetStyle(style);

        // 6️⃣ Add another example to prove scientific notation works for tiny numbers
        Cell tinyCell = sheet.Cells[1, 0]; // B2
        tinyCell.PutValue(0.00001234);
        tinyCell.SetStyle(style);

        // 7️⃣ Save the workbook to an XLSX file
        string outputPath = @"C:\Temp\CustomFormatted.xlsx";
        try
        {
            workbook.Save(outputPath, SaveFormat.Xlsx);
            Console.WriteLine($"Workbook saved successfully to {outputPath}");
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Failed to save workbook: {ex.Message}");
        }
    }
}
```

**النتيجة المتوقعة:** افتح `CustomFormatted.xlsx` وسترى:

| A1               | B2            |
|------------------|---------------|
| 1.23E+04         | 1.23E-05      |

كلا الخليتين عريضتين، مملوءتين باللون الرمادي الفاتح، وتعرضان الأرقام بصيغة علمية مع منزلتين عشريتين.

---

## الخلاصة

لقد قمنا للتو **بإنشاء مصنف Excel** من الصفر، **بتطبيق تنسيق رقم مخصص**، **بتنسيق الخلية بصيغة علمية**، **بضبط نمط الخلية برمجياً**، و**بحفظ المصنف كملف xlsx**—كل ذلك في بضع أسطر من C#. النهج قابل للتوسع: فقط كرّر عبر الصفوف، استنسخ كائن `style`، وستحصل على تقرير كامل الأنماط في ثوانٍ.

### ما التالي؟

- **تنسيق ديناميكي:** تغيير التنسيقات بناءً على حجم القيمة (مثلاً، عملة مقابل نسبة مئوية).  
- **أوراق متعددة:** استخدم `workbook.Worksheets.Add("Summary")` لبناء لوحات معلومات.  
- **تنسيق متقدم:** حدود، تنسيق شرطي، والتحقق من صحة البيانات

## دروس ذات صلة

- [كيفية إنشاء وحفظ مصنف Excel كملف ODS باستخدام Aspose.Cells for .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)
- [إنشاء وحفظ مصنف Excel باستخدام Aspose Cells .NET](/cells/hongkong/net/workbook-operations/create-save-excel-workbook-aspose-cells-dotnet/)
- [إنشاء وحفظ مصنف Excel كملف PDF باستخدام Aspnet Aspose Cells](/cells/hongkong/net/workbook-operations/create-save-excel-workbook-pdf-aspnet-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}