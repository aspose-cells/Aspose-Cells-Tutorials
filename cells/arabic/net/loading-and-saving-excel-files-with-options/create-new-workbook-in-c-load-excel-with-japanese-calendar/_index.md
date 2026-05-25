---
category: general
date: 2026-02-26
description: أنشئ مصنفًا جديدًا بلغة C# وتعلم كيفية تحميل ملفات Excel، وضبط التقويم
  على اليابانية، واستخراج التواريخ من Excel بسهولة.
draft: false
keywords:
- create new workbook
- how to load excel
- how to set calendar
- extract date from excel
- read japanese dates
language: ar
og_description: أنشئ دفتر عمل جديد في C# وتعلم بسرعة كيفية تحميل Excel، وتعيين تقويم
  ياباني، واستخراج التواريخ من ملفات Excel.
og_title: إنشاء دفتر عمل جديد في C# – تحميل إكسل مع التقويم الياباني
tags:
- C#
- Excel
- Aspose.Cells
- DateTime
title: إنشاء مصنف جديد في C# – تحميل Excel بالتقويم الياباني
url: /ar/net/loading-and-saving-excel-files-with-options/create-new-workbook-in-c-load-excel-with-japanese-calendar/
---

same number of # signs.

Now produce final output with all translated content.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء مصنف جديد في C# – تحميل Excel مع التقويم الياباني

هل احتجت يومًا إلى **create new workbook** في C# لكنك لم تكن متأكدًا من كيفية جعل Excel يحترم التقويم الياباني؟ أنت لست وحدك. في العديد من سيناريوهات المؤسسات ستحصل على جداول بيانات تخزن التواريخ بنظام العصور اليابانية، واستخراج تلك التواريخ بشكل صحيح قد يبدو كفك شفرة لغة سرية.

الأمر هو: يمكنك **create new workbook**، وإخبار المحمل (loader) بتفسير التواريخ باستخدام التقويم الياباني، ثم **extract date from excel** ببضع أسطر من الشيفرة فقط. في هذا الدليل سنستعرض *how to load excel*، *how to set calendar* لتواريخ يابانية، وأخيرًا *read Japanese dates* من خلية. بدون إطالة—مجرد مثال كامل قابل للتنفيذ يمكنك نسخه‑ولصقه في مشروعك.

## المتطلبات المسبقة

- .NET 6.0 أو أحدث (الشيفرة تعمل على .NET Framework 4.6+ أيضًا)  
- مكتبة **Aspose.Cells** (نسخة تجريبية مجانية أو نسخة مرخصة). قم بتثبيتها عبر NuGet:

```bash
dotnet add package Aspose.Cells
```

- ملف Excel (`JapanDates.xlsx`) يحتوي على تواريخ بنظام العصور اليابانية في الخلية A1.

هذا كل شيء. إذا كان لديك هذه المتطلبات، يمكننا البدء مباشرة.

---

## إنشاء مصنف جديد وتعيين التقويم الياباني

الخطوة الأولى هي إنشاء كائن **create new workbook** وتكوين `LoadOptions` بحيث يعرف المحلل أي تقويم يستخدم.

```csharp
using Aspose.Cells;
using System;

class JapaneseDateReader
{
    static void Main()
    {
        // Step 1: Create a new workbook instance
        Workbook workbook = new Workbook();

        // Step 2: Set load options to interpret dates using the Japanese calendar
        workbook.LoadOptions = new LoadOptions { Calendar = CalendarType.Japanese };

        // Step 3: Load the workbook from a file
        workbook.Load("YOUR_DIRECTORY/JapanDates.xlsx");

        // Step 4: Access cell A1 – it now contains a proper DateTime value
        var cellA1 = workbook.Worksheets[0].Cells["A1"];
        DateTime dateValue = cellA1.GetDateTime();

        Console.WriteLine($"The Japanese date in A1 is: {dateValue:yyyy-MM-dd}");
    }
}
```

> **نصيحة احترافية:** خاصية `LoadOptions.Calendar` تقبل عدة تعداد (`Gregorian`، `Japanese`، `Hijri`، إلخ). اختيار الأنسب يضمن أن المكتبة تُحوِّل نص العهد (مثلاً “令和3年”) إلى كائن .NET `DateTime`.

![إنشاء مصنف جديد مثال لقطة شاشة](image-url.png "لقطة شاشة تُظهر مثيل مصنف جديد مع إعدادات التقويم الياباني"){: .align-center alt="إنشاء مصنف جديد مثال لقطة شاشة"}

### لماذا يعمل هذا

- **إنشاء المصنف**: `new Workbook()` يمنحك صفحة نظيفة—لا أوراق عمل مخفية، لا بيانات افتراضية.
- **LoadOptions**: عبر تعيين `CalendarType.Japanese` *قبل* استدعاء `Load`، يتعامل المحلل مع أي سلاسل مبنية على العصور كتواريخ بدلاً من نص عادي.
- **GetDateTime()**: بعد التحميل، `cellA1.GetDateTime()` تُعيد كائن `DateTime` حقيقي، مما يتيح لك إجراء عمليات حسابية، تنسيق، أو إدراج في قاعدة بيانات دون خطوات تحويل إضافية.

---

## كيفية تحميل ملف Excel بشكل صحيح

قد تتساءل، “هل هناك طريقة خاصة لـ **how to load excel** عند التعامل مع تقاويم غير غريغورية؟” الجواب نعم—دائمًا قم بتعيين `LoadOptions` *قبل* استدعاء `Load`. إذا قمت بالتحميل أولاً ثم غيرت التقويم، فإن التواريخ تكون قد تم تحليلها بشكل غير صحيح.

```csharp
// Example of a wrong order – will treat Japanese dates as plain strings
Workbook badWorkbook = new Workbook();
badWorkbook.Load("JapanDates.xlsx");          // Loads with default Gregorian calendar
badWorkbook.LoadOptions.Calendar = CalendarType.Japanese; // Too late!
```

المقتطف أعلاه يوضح فخًا شائعًا. الترتيب الصحيح (كما هو موضح في القسم السابق) يضمن أن المحرك يفسر الخلايا *كتواريخ* منذ البداية.

---

## كيفية تعيين التقويم لتواريخ يابانية

إذا كنت بحاجة لتبديل التقويمات أثناء التشغيل—مثلاً، معالجة دفعة من الملفات التي تستخدم أنظمة عصور مختلفة—يمكنك إعادة استخدام نفس كائن `Workbook` مع `LoadOptions` جديد في كل مرة.

```csharp
void LoadWithCalendar(string filePath, CalendarType calendar)
{
    Workbook wb = new Workbook
    {
        LoadOptions = new LoadOptions { Calendar = calendar }
    };
    wb.Load(filePath);
    // Now you can read dates according to the chosen calendar
}
```

استدعاء `LoadWithCalendar("JapanDates.xlsx", CalendarType.Japanese)` ينتج نفس النتيجة كما في مثالنا الرئيسي، بينما `CalendarType.Gregorian` سيعامل نفس الخلية كنص عادي (أو يرمي استثناء إذا كان التنسيق غير قابل للتعرف).

---

## استخراج التاريخ من Excel – قراءة تواريخ يابانية

الآن بعد أن تم تحميل المصنف بالتقويم المناسب، استخراج التاريخ يصبح بسيطًا. طريقة `Cell.GetDateTime()` تُعيد كائن `DateTime` يحترم تحويل العهد.

```csharp
DateTime ExtractJapaneseDate(Workbook wb, string address)
{
    var cell = wb.Worksheets[0].Cells[address];
    return cell.GetDateTime(); // Returns a .NET DateTime
}

// Usage
DateTime japaneseDate = ExtractJapaneseDate(workbook, "A1");
Console.WriteLine($"Extracted date: {japaneseDate:d}");
```

### حالات الحافة والسيناريوهات الافتراضية

| الحالة                                 | ما الذي يجب فعله                                                                                         |
|----------------------------------------|----------------------------------------------------------------------------------------------------------|
| الخلية تحتوي على **نص** بدلاً من تاريخ | استدعِ `cell.GetString()` أولاً، تحقق باستخدام `DateTime.TryParse`، أو فرض التحقق من البيانات في Excel. |
| الحاجة لمعالجة أوراق عمل متعددة        | قم بالتكرار عبر `workbook.Worksheets` وطبق نفس منطق الاستخراج على كل ورقة.                              |
| التواريخ مخزنة كـ **أرقام** (تسلسل Excel) | `cell.GetDateTime()` لا يزال يعمل لأن Aspose.Cells يحول الأرقام المتسلسلة تلقائيًا.                    |
| الملف **محمي بكلمة مرور**               | استخدم `LoadOptions.Password = "yourPwd"` قبل استدعاء `Load`.                                           |

---

## مثال كامل يعمل (جاهز للنسخ‑اللصق)

فيما يلي البرنامج الكامل الذي يمكنك إدراجه في تطبيق Console. يتضمن معالجة الأخطاء ويظهر جميع الكلمات المفتاحية الثانوية الأربعة في السياق.

```csharp
using Aspose.Cells;
using System;

class JapaneseDateReader
{
    static void Main()
    {
        // --------------------------------------------------------------------
        // 1️⃣  Create new workbook and configure calendar (primary keyword)
        // --------------------------------------------------------------------
        Workbook workbook = new Workbook
        {
            LoadOptions = new LoadOptions { Calendar = CalendarType.Japanese }
        };

        // --------------------------------------------------------------------
        // 2️⃣  How to load excel – correct order matters (secondary keyword)
        // --------------------------------------------------------------------
        try
        {
            workbook.Load("YOUR_DIRECTORY/JapanDates.xlsx");
        }
        catch (Exception ex)
        {
            Console.WriteLine($"Failed to load Excel file: {ex.Message}");
            return;
        }

        // --------------------------------------------------------------------
        // 3️⃣  How to set calendar – already done before loading (secondary)
        // --------------------------------------------------------------------
        // (If you need to change it later, see the LoadWithCalendar method above.)

        // --------------------------------------------------------------------
        // 4️⃣  Extract date from excel – read Japanese dates (secondary keywords)
        // --------------------------------------------------------------------
        try
        {
            var cell = workbook.Worksheets[0].Cells["A1"];
            DateTime japaneseDate = cell.GetDateTime(); // Proper DateTime thanks to the calendar setting
            Console.WriteLine($"Japanese date in A1 → {japaneseDate:yyyy-MM-dd}");
        }
        catch (Exception ex)
        {
            Console.WriteLine($"Error extracting date: {ex.Message}");
        }
    }
}
```

**الناتج المتوقع** (بافتراض أن A1 يحتوي على “令和3年5月12日”):

```
Japanese date in A1 → 2021-05-12
```

إذا كانت الخلية تحتوي على تاريخ غريغوري مثل “2021‑05‑12”، فإن نفس الشيفرة لا تزال تعمل لأن المكتبة تعود بسلاسة إلى التفسير الغريغوري.

---

## الخلاصة

أنت الآن تعرف كيف **create new workbook**، وكيف **how to load excel** بشكل صحيح، وتعيين **how to set calendar** المناسب، وأخيرًا **extract date from excel** بينما **read Japanese dates** دون أي تحليل يدوي. الفكرة الأساسية هي أن التقويم يجب أن يُحدد *قبل* التحميل؛ بمجرد أن يكون المصنف في الذاكرة، تكون التواريخ قد تم تجسيدها ككائنات `DateTime` صحيحة.

### ما التالي؟

- **معالجة دفعات**: تكرار عبر مجلد من الملفات، واستدعاء `LoadWithCalendar` لكل منها.
- **التصدير إلى صيغ أخرى**: استخدم `workbook.Save("output.csv")` بعد التحويل.
- **التعريب**: دمج `CultureInfo` مع `DateTime.ToString` لعرض التواريخ بلغة المستخدم المفضلة.

لا تتردد في التجربة—استبدل `CalendarType.Japanese` بـ `CalendarType.Hijri` أو `CalendarType.Gregorian` وشاهد الشيفرة نفسها تتكيف تلقائيًا. إذا واجهت أي مشاكل، اترك تعليقًا أدناه أو راجع توثيق Aspose.Cells للحصول على رؤى أعمق حول الـ API.

برمجة سعيدة، واستمتع بتحويل تلك التواريخ اليابانية الغامضة إلى قيم .NET `DateTime` نظيفة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}