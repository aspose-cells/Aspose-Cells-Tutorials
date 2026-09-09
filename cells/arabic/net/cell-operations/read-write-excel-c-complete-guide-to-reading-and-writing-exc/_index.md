---
category: general
date: 2026-03-01
description: دليل قراءة وكتابة Excel بلغة C# يوضح كيفية قراءة قيمة خلية Excel وكتابة
  تاريخ ووقت إلى Excel باستخدام C# و Aspose.Cells في بضع خطوات سهلة.
draft: false
keywords:
- read write excel c#
- read excel cell value
- write datetime to excel
- c# excel interop
- aspnet excel automation
language: ar
og_description: دليل C# لقراءة وكتابة Excel يشرح كيفية قراءة قيمة خلية Excel وكتابة
  التاريخ والوقت إلى Excel مع أمثلة شفرة واضحة وأفضل الممارسات.
og_title: قراءة وكتابة Excel C# – دليل خطوة بخطوة
tags:
- C#
- Excel
- Aspose.Cells
title: قراءة وكتابة Excel C# – الدليل الكامل لقراءة وكتابة خلايا Excel
url: /ar/net/cell-operations/read-write-excel-c-complete-guide-to-reading-and-writing-exc/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# قراءة وكتابة Excel C# – دليل شامل لقراءة وكتابة خلايا Excel

هل حاولت **قراءة وكتابة Excel C#** وانتهى بك الأمر باستثناء غامض أو تاريخ غير متطابق؟ لست وحدك. يواجه العديد من المطورين صعوبة عندما يحتاجون إلى استخراج تاريخ ياباني من ورقة عمل ثم تخزين `DateTime` صحيح في نفس الخلية.

في هذا الدليل سنستعرض خطوة بخطوة كيفية **قراءة قيمة خلية Excel** و**كتابة DateTime إلى Excel** باستخدام C# ومكتبة Aspose.Cells القوية. في النهاية ستحصل على مثال مكتمل، قابل للتنفيذ، يمكنك إدراجه في أي مشروع .NET.

## ما ستتعلمه

- كيفية تثبيت وإضافة مرجع Aspose.Cells في مشروع .NET 6+.  
- الشيفرة الدقيقة المطلوبة لجلب خلية تحتوي على سلسلة تاريخ ياباني مثل `"R3/5/12"`.  
- كيفية تحويل تلك السلسلة إلى `DateTime` باستخدام الثقافة `"ja-JP"`.  
- الخطوات اللازمة لإرجاع الـ `DateTime` الناتج إلى نفس خلية ورقة العمل.  
- نصائح للتعامل مع الحالات الحدية مثل الخلايا الفارغة أو صيغ العصور غير المتوقعة.  

لا تحتاج إلى خبرة مسبقة في Excel interop—فقط فهم أساسي لـ C# و .NET. لنبدأ.

![لقطة شاشة لعملية قراءة وكتابة Excel C# تُظهر الخلية B2 قبل وبعد التحويل](read-write-excel-csharp.png "مثال قراءة وكتابة Excel C#")

## الخطوة 1: إعداد المشروع – أسس قراءة وكتابة Excel C#

قبل الغوص في الشيفرة، نحتاج إلى أساس قوي.

1. **إنشاء تطبيق console جديد** (أو أي مشروع .NET) يستهدف .NET 6 أو أحدث:

   ```bash
   dotnet new console -n ExcelEraDemo
   cd ExcelEraDemo
   ```

2. **إضافة حزمة NuGet الخاصة بـ Aspose.Cells**. إنها مكتبة مُدارة بالكامل تعمل بدون COM interop:

   ```bash
   dotnet add package Aspose.Cells
   ```

3. **نسخ ملف Excel** (`EraDates.xlsx`) إلى جذر المشروع. يجب أن يحتوي هذا المصنف على ورقة تسمى `"Sheet1"` وتحتوي الخلية **B2** على قيمة مثل `"R3/5/12"` (ريوا 3، مايو 12).

هذا كل ما تحتاجه من بنية أساسية. يركز باقي الدليل على منطق **قراءة قيمة خلية Excel** و**كتابة DateTime إلى Excel** الفعلي.

## الخطوة 2: قراءة قيمة خلية Excel باستخدام C#

الآن بعد أن أصبح المشروع جاهزًا، لنستخرج السلسلة من ورقة العمل. المقتطف التالي يوضح سلسلة الاستدعاءات الدقيقة:

```csharp
using Aspose.Cells;
using System;
using System.Globalization;

class Program
{
    static void Main()
    {
        // Load the workbook (adjust the path as needed)
        Workbook wb = new Workbook("EraDates.xlsx");
        Worksheet ws = wb.Worksheets["Sheet1"];   // assumes the sheet is named Sheet1

        // Step 2: Get the cell that holds the Japanese era date string
        // B2 contains something like "R3/5/12"
        Cell dateCell = ws.Cells["B2"];  

        // Step 3: Read the string representation from the cell
        string eraDateString = dateCell.StringValue;  

        Console.WriteLine($"Original cell value: {eraDateString}");
        // -------------------------------------------------
        // From here we’ll convert the era string to a DateTime.
        // -------------------------------------------------
    }
}
```

**لماذا يعمل هذا:** `Cell.StringValue` يُعيد دائمًا النص المعروض، بغض النظر عن تنسيق الرقم الأساسي. هذا يضمن أننا نتعامل مع السلسلة الدقيقة `"R3/5/12"` التي يراها المستخدم.

### الأخطاء الشائعة

- **الخلايا الفارغة** – `StringValue` يُعيد سلسلة فارغة. احرص على التحقق قبل التحليل.  
- **الصيغ غير المتوقعة** – إذا احتوت الخلية على `"2023/05/12"` سيتسبب محلل العصور في استثناء؛ قد تحتاج إلى طريقة احتياطية.

## الخطوة 3: كتابة DateTime إلى Excel باستخدام C#

بعد الحصول على سلسلة العصر، نقوم الآن بتحليلها باستخدام `DateTime.ParseExact`. الصيغة `"ggyy/MM/dd"` تخبر .NET أن يتوقع عصرًا يابانيًا (`gg`)، سنة من رقمين (`yy`)، ومكوّنات الشهر/اليوم.

```csharp
        // Step 4: Convert the era date string to a DateTime using the Japanese culture
        DateTime parsedDate;
        try
        {
            parsedDate = DateTime.ParseExact(
                eraDateString,
                "ggyy/MM/dd",
                new CultureInfo("ja-JP"));
        }
        catch (FormatException)
        {
            Console.WriteLine("The cell value does not match the expected Japanese era format.");
            return;
        }

        Console.WriteLine($"Parsed DateTime (UTC): {parsedDate:u}");

        // Step 5: Store the resulting DateTime back into the same cell
        dateCell.PutValue(parsedDate);

        // Optional: Apply a standard date format so Excel shows it nicely
        dateCell.SetStyle(new Style { Number = 14 }); // 14 = "m/d/yyyy"

        // Save the workbook to a new file so we don’t overwrite the original
        wb.Save("EraDates_Converted.xlsx");
        Console.WriteLine("Workbook saved as EraDates_Converted.xlsx");
```

**لماذا نستخدم `PutValue`**: Aspose.Cells يكتشف تلقائيًا نوع .NET ويكتب النوع المناسب لخلية Excel. تمرير `DateTime` ينتج تاريخ Excel حقيقي، يمكن تنسيقه أو استخدامه في الصيغ لاحقًا.

### الحالات الحدية والنصائح

- **المناطق الزمنية** – كائنات `DateTime` تُخزن بدون معلومات المنطقة. إذا كنت تحتاج إلى UTC، استدعِ `DateTime.SpecifyKind`.  
- **العودة إلى ثقافات أخرى** – إذا كنت تتوقع ثقافات مختلفة، غلف عملية التحليل بدالة مساعدة تحاول عدة كائنات `CultureInfo`.  
- **الأداء** – عند معالجة آلاف الصفوف، أعد استخدام كائن `CultureInfo` واحد بدلاً من إنشاء جديد في كل دورة.

## الخطوة 4: مثال كامل يعمل – تجميع كل شيء معًا

فيما يلي البرنامج الكامل الجاهز للتنفيذ. انسخه إلى `Program.cs`، تأكد من وجود `EraDates.xlsx` بجوار الملف التنفيذي، ثم شغّله باستخدام `dotnet run`.

```csharp
using Aspose.Cells;
using System;
using System.Globalization;

class Program
{
    static void Main()
    {
        // Load workbook
        Workbook wb = new Workbook("EraDates.xlsx");
        Worksheet ws = wb.Worksheets["Sheet1"];   // Change if your sheet has a different name

        // -------------------------------------------------
        // 1️⃣ Read the Japanese era string from B2
        // -------------------------------------------------
        Cell dateCell = ws.Cells["B2"];
        string eraDateString = dateCell.StringValue?.Trim();

        if (string.IsNullOrEmpty(eraDateString))
        {
            Console.WriteLine("Cell B2 is empty. Nothing to convert.");
            return;
        }

        Console.WriteLine($"Original cell value: {eraDateString}");

        // -------------------------------------------------
        // 2️⃣ Parse the era string into a DateTime
        // -------------------------------------------------
        DateTime parsedDate;
        try
        {
            parsedDate = DateTime.ParseExact(
                eraDateString,
                "ggyy/MM/dd",
                new CultureInfo("ja-JP"));
        }
        catch (FormatException)
        {
            Console.WriteLine("The value does not match the expected Japanese era format (ggyy/MM/dd).");
            return;
        }

        Console.WriteLine($"Parsed DateTime: {parsedDate:u}");

        // -------------------------------------------------
        // 3️⃣ Write the DateTime back into the same cell
        // -------------------------------------------------
        dateCell.PutValue(parsedDate);

        // Apply a friendly date format (e.g., 2023/05/12)
        Style style = wb.CreateStyle();
        style.Number = 14; // Built‑in date format
        dateCell.SetStyle(style);

        // Save the updated workbook
        wb.Save("EraDates_Converted.xlsx");
        Console.WriteLine("Conversion complete – saved as EraDates_Converted.xlsx");
    }
}
```

**الناتج المتوقع**

```
Original cell value: R3/5/12
Parsed DateTime: 2021-05-12 00:00:00Z
Conversion complete – saved as EraDates_Converted.xlsx
```

عند فتح `EraDates_Converted.xlsx`، ستظهر الخلية **B2** تاريخًا عاديًا (مثلاً `5/12/2021`) ويمكن استخدامه في حسابات Excel كأي قيمة تاريخية أخرى.

## نصائح احترافية لكتابة كود قراءة وكتابة Excel C# قوي

- **التحقق قبل الكتابة** – استخدم `Cell.IsFormula` أو `Cell.Type` لتجنب الكتابة فوق الصيغ عن غير قصد.  
- **المعالجة الدفعية** – إذا كنت بحاجة لتحويل عمود كامل، كرّر عبر `ws.Cells.Columns[1]` (عمود B) وطبق نفس المنطق.  
- **سلامة الخيوط** – كائنات Aspose.Cells غير آمنة للـ multithreading؛ أنشئ مثيلات `Workbook` منفصلة لكل خيط عند التوازي.  
- **التسجيل** – في السكريبتات الإنتاجية، استبدل `Console.WriteLine` بمسجل مناسب (مثل Serilog) لتسجيل فشل التحليل.  
- **الاختبار** – اكتب اختبارات وحدة تغذي سلاسل عصر معروفة إلى دالة مساعدة وتتحقق من قيم `DateTime` الناتجة.

## الخاتمة

لقد أتقنت الآن **قراءة وكتابة Excel C#** من خلال تعلمك كيفية **قراءة قيمة خلية Excel**، تحليل سلسلة عصر ياباني، و**كتابة DateTime إلى Excel** بثقة. يُظهر المثال الكامل سير عمل نظيف من البداية إلى النهاية يمكنك تكييفه للعمليات الضخمة، ثقافات مختلفة، أو حتى خطوط أنابيب من Excel إلى قاعدة بيانات.

ما الخطوة التالية؟ جرّب توسيع السكريبت لمعالجة عمود كامل من تواريخ العصور، أو استكشف خيارات التنسيق الغنية في Aspose.Cells لتنسيق الخلايا الناتجة. يمكنك أيضًا تجربة مكتبات أخرى مثل EPPlus أو ClosedXML—معظم المنطق يبقى نفسه، فقط استدعاءات الـ API تختلف.

هل لديك أسئلة أو سيناريو Excel معقد؟ اترك تعليقًا أدناه، وتمنياتنا لك بالبرمجة السعيدة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}