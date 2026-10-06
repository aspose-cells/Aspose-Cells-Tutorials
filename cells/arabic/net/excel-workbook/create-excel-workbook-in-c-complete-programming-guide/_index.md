---
category: general
date: 2026-06-05
description: إنشاء مصنف Excel في C# بسرعة وتعلم كيفية تعيين تنسيق رقم الخلية، وتصدير
  خلية Excel، وتحويل قيمة الخلية إلى سلسلة بدقة منزلتين عشريتين.
draft: false
keywords:
- create excel workbook
- set cell number format
- format number with two decimals
- how to export excel cell
- convert cell value to string
language: ar
og_description: إنشاء مصنف Excel في C# وإتقان ضبط تنسيق أرقام الخلايا، وتصدير خلية
  Excel كسلسلة، وتنسيق الأرقام بدقتين عشريتين.
og_title: إنشاء مصنف إكسل في C# – دليل كامل خطوة بخطوة
schemas:
- author: Aspose
  dateModified: '2026-06-05'
  description: Create Excel workbook in C# quickly and learn how to set cell number
    format, export Excel cell, and convert cell value to string with two‑decimal precision.
  headline: Create Excel Workbook in C# – Complete Programming Guide
  type: TechArticle
- description: Create Excel workbook in C# quickly and learn how to set cell number
    format, export Excel cell, and convert cell value to string with two‑decimal precision.
  name: Create Excel Workbook in C# – Complete Programming Guide
  steps:
  - name: What if the cell already has a style?
    text: The `GetStyle` method returns a copy of the existing style, so any previous
      formatting (font, color, etc.) is retained. You only overwrite the `Custom`
      property, leaving everything else untouched.
  - name: How does culture affect the decimal separator?
    text: 'Aspose.Cells respects the thread’s `CultureInfo`. If you need a comma instead
      of a dot, set:'
  - name: Can I export a range of cells at once?
    text: Yes—use `Worksheet.ExportDataTable` or `Worksheet.ExportString` with a range
      address. The `ExportTableOptions` you defined for a single cell can be reused
      for the whole range.
  - name: What if I don’t want the value rounded but truncated?
    text: 'Change the custom format to `"0.00"` with a rounding mode, or manually
      truncate before putting the value:'
  type: HowTo
tags:
- C#
- Excel
- Aspose.Cells
title: إنشاء مصنف إكسل في C# – دليل برمجة شامل
url: /ar/net/excel-workbook/create-excel-workbook-in-c-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء دفتر عمل Excel في C# – دليل برمجة كامل

هل تساءلت يومًا كيف **create Excel workbook** في C# دون التعامل مع COM interop أو حيل CSV الفوضوية؟ لست وحدك. يحتاج العديد من المطورين إلى طريقة نظيفة، أصلية لـ .NET لإنشاء ملف .xlsx، ووضع رقم في خلية، ثم تصدير تلك القيمة كسلسلة منسقة بشكل جميل.  

في هذا الدرس سنستعرض ذلك خطوة بخطوة—بدءًا من دفتر عمل فارغ، تعيين تنسيق رقم الخلية، تنسيق الرقم بمكانين عشريين، وأخيرًا تعلم **how to export Excel cell** كبيانات نصية. في النهاية سترى أيضًا كيف **convert cell value to string** دون فقدان الدقة.

> **Pro tip:** النهج أدناه يستخدم مكتبة **Aspose.Cells for .NET**، وهي API تجارية مختبرة على أرض الواقع. إذا كنت تبحث عن بديل مجاني، فـ EPPlus أو ClosedXML يعملان بشكل مشابه، لكن مقتطفات الشيفرة ستختلف قليلًا.

## المتطلبات المسبقة

قبل أن نبدأ، تأكد من وجود ما يلي:

- .NET 6.0 SDK (أو أي نسخة حديثة من .NET) مثبتة.
- Visual Studio 2022 أو VS Code مع امتداد C#.
- حزمة **Aspose.Cells** من NuGet (`Install-Package Aspose.Cells`).

لا توجد تبعيات أخرى مطلوبة—كل شيء آخر موجود داخل المكتبة.

## الخطوة 1: تثبيت Aspose.Cells وإعداد المشروع

افتح الطرفية (أو Package Manager Console) وشغّل:

```powershell
dotnet new console -n ExcelDemo
cd ExcelDemo
dotnet add package Aspose.Cells
```

هذا ينشئ تطبيق console جديد باسم `ExcelDemo` ويضيف تجميع `Aspose.Cells`.  

لماذا هذه الخطوة مهمة: بدون المكتبة، لا يمكنك **create Excel workbook** أو تعديل الخلايا بطريقة آمنة من حيث النوع.

## الخطوة 2: إنشاء دفتر العمل والحصول على ورقة العمل الأولى

الآن افتح `Program.cs` واستبدل الشيفرة الافتراضية بالمقتطف أدناه. يوضح هذا أول ما تقوم به عند **create Excel workbook**—إنشاء كائن `Workbook` والحصول على مرجع إلى الورقة الافتراضية.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 2: Create a workbook and get the first worksheet
        Workbook workbook = new Workbook();               // creates a new .xlsx in memory
        Worksheet ws = workbook.Worksheets[0];           // first (default) sheet

        // The rest of the steps will follow here...
```

> **Why?** كائن `Workbook` هو تمثيل الملف Excel في الذاكرة. بشكل افتراضي يحتوي على ورقة عمل واحدة، يمكن الوصول إليها عبر الفهرس الصفري.

## الخطوة 3: وضع قيمة رقمية في خلية محددة

دعنا نستهدف الصف 5، العمود 2 (فهارس صفرية) ونُدخل رقمًا عشريًا. هذا يوضح **format number with two decimals** لاحقًا.

```csharp
        // Step 3: Access the cell at row 5, column 2 (zero‑based) and insert a number
        Cell cell = ws.Cells[5, 2];          // corresponds to cell C6 in Excel UI
        cell.PutValue(12345.6789);          // raw value with many decimal places
```

طريقة `PutValue` تخزن القيمة الثنائية الخام. في هذه المرحلة، سيعرض Excel الدقة الكاملة ما لم نطبق تنسيقًا.

## الخطوة 4: تعيين تنسيق رقم الخلية (مكانيين عشريين)

هنا نطبق **set cell number format**. سنستخدم كائن `Style` لتحديد تنسيق رقم مخصص `"0.00"`—بالضبط مكانين عشريين.

```csharp
        // Step 4: Apply a number format to show only two decimal places
        Style style = cell.GetStyle();               // clone existing style
        style.Custom = "0.00";                       // forces two digits after the dot
        cell.SetStyle(style);                        // apply the style back to the cell
```

لماذا نستخدم نمطًا بدلاً من تحويل السلسلة؟ الحفاظ على الخلية كنوع رقمي يحافظ على قابليتها للحساب (يمكنك الجمع، المتوسط، إلخ) مع عرض ما تحتاجه بالضبط.

## الخطوة 5: تصدير قيمة الخلية كسلسلة منسقة

أحيانًا تحتاج إلى قيمة **how to export excel cell** كنص عادي—ربما لكتابتها في ملف سجل أو إرسالها عبر API ويب. تسمح لك Aspose.Cells بإرفاق خيارات تصدير إلى خلية، لتخبر المكتبة بتصيير القيمة كسلسلة باستخدام نفس تنسيق الرقم.

```csharp
        // Step 5: Configure export options to get the formatted string
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,          // forces string output
            NumberFormat = "0.00"           // matches the style we set earlier
        };
        cell.ExportOptions = exportOptions; // attach options to the cell
```

الآن عندما نقرأ قيمة الخلية عبر API التصدير، سنحصل على سلسلة تحترم قاعدة المكانين العشريين.

## الخطوة 6: استرجاع السلسلة المنسقة (Convert Cell Value to String)

لنقم فعليًا بالتصدير ونرى النتيجة. طريقة `ExportString` تُعيد محتوى الخلية كسلسلة، مع تطبيق أي `ExportTableOptions` أرفقناها.

```csharp
        // Step 6: Export the cell as a formatted string
        string formattedValue = cell.ExportString();
        Console.WriteLine($"Formatted cell value: {formattedValue}");
```

عند تشغيل البرنامج، ستطبع وحدة التحكم:

```
Formatted cell value: 12345.68
```

لاحظ التقريب من `12345.6789` إلى `12345.68`—هذا هو تأثير **format number with two decimals**.

## الخطوة 7: (اختياري) حفظ دفتر العمل على القرص

إذا أردت أيضًا رؤية النتيجة داخل ملف `.xlsx` فعلي، فقط استدعِ `Save`:

```csharp
        // Optional: write the workbook to a file so you can open it in Excel
        workbook.Save("DemoWorkbook.xlsx");
    }
}
```

فتح `DemoWorkbook.xlsx` يُظهر نفس الرقم في الخلية **C6**، مُنسقًا بمكانين عشريين.

## حالات الحافة والأسئلة الشائعة

### ماذا لو كانت الخلية لديها نمط بالفعل؟

طريقة `GetStyle` تُعيد نسخة من النمط الحالي، لذا أي تنسيق سابق (خط، لون، إلخ) يُحفظ. أنت فقط تُعيد كتابة الخاصية `Custom`، مع ترك باقي الخصائص دون تغيير.

### كيف يؤثر الإعداد الثقافي على الفاصل العشري؟

تُراعي Aspose.Cells إعداد `CultureInfo` الخاص بالخيط. إذا كنت تحتاج إلى فاصلة بدلاً من نقطة، عيّن:

```csharp
System.Threading.Thread.CurrentThread.CurrentCulture = new System.Globalization.CultureInfo("fr-FR");
```

نفس تنسيق `"0.00"` سيعرض الآن `12 345,68`.

### هل يمكنني تصدير نطاق من الخلايا مرة واحدة؟

نعم—استخدم `Worksheet.ExportDataTable` أو `Worksheet.ExportString` مع عنوان نطاق. يمكن إعادة استخدام `ExportTableOptions` التي عرّفتها لخلية واحدة على النطاق بأكمله.

### ماذا لو لم أرغب في تقريب القيمة بل في قطعها؟

غيّر التنسيق المخصص إلى `"0.00"` مع وضعية تقطيع، أو قم بقطع القيمة يدويًا قبل وضعها:

```csharp
double raw = Math.Truncate(12345.6789 * 100) / 100; // yields 12345.67
cell.PutValue(raw);
```

## مثال كامل يعمل (جاهز للنسخ واللصق)

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 2: Create a workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet ws = workbook.Worksheets[0];

        // Step 3: Access the cell at row 5, column 2 (zero‑based) and insert a number
        Cell cell = ws.Cells[5, 2];
        cell.PutValue(12345.6789);

        // Step 4: Apply a number format to show only two decimal places
        Style style = cell.GetStyle();
        style.Custom = "0.00";
        cell.SetStyle(style);

        // Step 5: Configure export options to get the formatted string
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,
            NumberFormat = "0.00"
        };
        cell.ExportOptions = exportOptions;

        // Step 6: Export the cell as a formatted string
        string formattedValue = cell.ExportString();
        Console.WriteLine($"Formatted cell value: {formattedValue}");

        // Optional: save the workbook for visual verification
        workbook.Save("DemoWorkbook.xlsx");
    }
}
```

**الإخراج المتوقع في وحدة التحكم**

```
Formatted cell value: 12345.68
```

افتح `DemoWorkbook.xlsx` → انتقل إلى الخلية **C6** → سترى نفس الرقم بمكانين عشريين.

## الخلاصة

لقد غطينا كل ما تحتاجه لت **create Excel workbook** في C#، **set cell number format**، **format number with two decimals**، فهم **how to export Excel cell** كبيانات، و **convert cell value to string** للمعالجة اللاحقة.  

النقاط الرئيسية هي:

1. استخدم `Workbook` و `Worksheet` لإنشاء ملف Excel في الذاكرة.  
2. طبّق نمطًا مخصصًا (`"0.00"`) لفرض عرض بمكانين عشريين.  
3. أرفق `ExportTableOptions` بخلية عندما تحتاج إلى تمثيل نصي يحافظ على نفس التنسيق.  

من هنا يمكنك التجربة—إضافة خلايا أخرى، تطبيق تنسيق شرطي، أو حتى إنشاء مخططات. إذا كنت مهتمًا بتنسيق الخطوط أو إضافة صيغ، راجع وثائق Aspose.Cells حول **cell styling** و **formula evaluation**.

هل لديك أسئلة إضافية حول أتمتة Excel في C#؟ اترك تعليقًا، وتمنياتنا لك بالبرمجة السعيدة!

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تُبنى على التقنيات التي تم استعراضها في هذا الدليل. كل مورد يتضمن أمثلة شيفرة كاملة مع شرح خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف نهج تنفيذ بديلة في مشاريعك.

- [إتقان عمليات دفتر العمل في Aspose.Cells .NET: تحميل ملفات Excel وتتبع سابقة الخلايا بفعالية](/cells/english/net/workbook-operations/aspose-cells-net-master-workbook-operations/)
- [إتقان تنسيق خلايا Excel وإدارة دفتر العمل باستخدام Aspose.Cells لـ .NET](/cells/english/net/formatting/excel-formatting-aspose-cells-net/)
- [إتقان Aspose.Cells لـ .NET: إدارة متقدمة لدفتر عمل Excel والخلية](/cells/english/net/advanced-features/excel-aspose-cells-net-create-manage/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}