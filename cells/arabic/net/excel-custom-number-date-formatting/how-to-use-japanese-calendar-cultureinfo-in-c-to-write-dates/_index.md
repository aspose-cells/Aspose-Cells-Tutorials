---
category: general
date: 2026-10-26
description: تعلم كيفية استخدام CultureInfo للتقويم الياباني في C# عند تحليل تواريخ
  العصور وإدراجها في ورقة عمل Excel باستخدام NPOI.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- use japanese calendar cultureinfo
- japanese era date parsing
- cultureinfo with japanese calendar
- datetime parse with cultureinfo
- npoi excel cultureinfo
language: ar
lastmod: 2026-10-26
og_description: استخدم CultureInfo للتقويم الياباني في C# لتحليل تواريخ عصر ريووا
  وكتابتها إلى ورقة عمل Excel. كود كامل وقابل للتنفيذ مع شروحات.
og_image_alt: Screenshot of C# code parsing a Japanese era date and inserting it into
  an Excel cell
og_title: استخدام CultureInfo لتقويم اليابان في C# – مثال كامل على Excel
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Learn how to use Japanese calendar CultureInfo in C# when parsing era
    dates and inserting them into an Excel worksheet with NPOI.
  headline: How to use Japanese calendar CultureInfo in C# to write dates to Excel
  type: TechArticle
tags:
- C#
- CultureInfo
- Excel
- NPOI
- Internationalization
title: كيفية استخدام CultureInfo للتقويم الياباني في C# لكتابة التواريخ إلى Excel
url: /ar/net/excel-custom-number-date-formatting/how-to-use-japanese-calendar-cultureinfo-in-c-to-write-dates/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية استخدام CultureInfo للتقويم الياباني في C# لكتابة التواريخ إلى Excel

إذا كنت بحاجة إلى **استخدام CultureInfo للتقويم الياباني** أثناء التعامل مع التواريخ في C#، فإن هذا الدليل يوضح لك بالضبط كيف تفعل ذلك. ستتعلم كيفية تحليل سلسلة تاريخ تحتوي على اسم عصر ياباني (على سبيل المثال، *Reiwa 2/5/1*) ثم كتابة الـ `DateTime` الناتج في الخلية الأولى من ورقة عمل Excel باستخدام مكتبة NPOI.

تحليل التواريخ القائمة على العصور دون `CultureInfo` الصحيح يؤدي إلى `FormatException` أو قيم شهر/يوم غير صحيحة. من خلال ضبط `CultureInfo` على التقويم الياباني، تضمن أن بيئة تشغيل .NET تفسر العصر بشكل صحيح وأن القيمة التي تخزنها في Excel تتطابق مع الصياغة اليابانية الأصلية.

في هذا الدرس ستقوم بـ:

* إنشاء كائن `CultureInfo` يستخدم التقويم الياباني.  
* تحليل سلسلة تاريخ يابانية باستخدام `DateTime.Parse`.  
* إدراج الـ `DateTime` المحلل في خلية ورقة عمل NPOI.  
* مشاهدة البرنامج الكامل القابل للتنفيذ والنتيجة المتوقعة.

> **المتطلبات المسبقة** – .NET 6.0+ (أو .NET Core 3.1+)، حزمة **NPOI** من NuGet، وفهم أساسي لـ C# وتعامل ملفات Excel.

---

## ما ستحتاجه

| العنصر | السبب |
|--------|-------|
| **.NET SDK** (6.0 أو أحدث) | يوفّر وقت التشغيل والمكتبات الخاصة بـ `CultureInfo`. |
| **NPOI** (حزمة `NPOI` من NuGet) | يتيح لك إنشاء وتعديل ملفات Excel دون الحاجة إلى تثبيت Office. |
| **Visual Studio Code**، **Visual Studio** أو أي بيئة تطوير C# | لتجميع وتشغيل العينة. |
| **سلسلة تاريخ يابانية** (مثال: `"Reiwa 2/5/1"`) | توضح استخدام التقويم الياباني. |

---

## الخطوة 1: تثبيت NPOI

افتح طرفية في مجلد المشروع وشغّل:

```bash
dotnet add package NPOI --version 2.6.1
```

الحزمة توفر الأنواع `IWorkbook` و `ISheet` و `ICell` التي ستُستَخدم لاحقًا.

---

## الخطوة 2: إنشاء CultureInfo يستخدم التقويم الياباني

التقويم الياباني هو تقويم قائم على العصور. يجب طلب المتغيّر *Japanese* من إعدادات اللغة `ja-JP` وتعيين التقويم صراحةً إلى `JapaneseCalendar`.

```csharp
using System;
using System.Globalization;

// Create a CultureInfo based on Japanese locale and switch its calendar.
CultureInfo japaneseCulture = new CultureInfo("ja-JP");
japaneseCulture.DateTimeFormat.Calendar = new JapaneseCalendar();
```

> **لماذا هذا مهم** – الثقافة الافتراضية `ja-JP` تستخدم التقويم الميلادي. إعادة تعيين خاصية `Calendar` يضمن أن أسماء العصور مثل *Reiwa* تُعترف بها أثناء التحليل.

---

## الخطوة 3: تحليل سلسلة تاريخ يابانية

الآن بعد ضبط `CultureInfo`، يمكنك بأمان تحليل سلسلة تحتوي على اسم عصر.

```csharp
// Example Japanese era date: Reiwa 2 (2020) year, May 1st.
string eraDate = "Reiwa 2/5/1";

// Parse using the Japanese CultureInfo created earlier.
DateTime reiwaDate = DateTime.Parse(eraDate, japaneseCulture);
Console.WriteLine($"Parsed DateTime (UTC): {reiwaDate:u}");
```

**الناتج**

```
Parsed DateTime (UTC): 2020-05-01 00:00:00Z
```

طريقة `Parse` تفسّر *Reiwa 2* كالسنة الميلادية 2020، الشهر 5، اليوم 1.

### حالة خاصة: معالجة العصور غير الصالحة

إذا أدخل المستخدم عصرًا غير مدعوم (مثال: `"Heisei 31/4/30"` بعد انتهاء عصر Heisei)، فإن `DateTime.Parse` يطرح `FormatException`. احطِ الاستدعاء بكتلة try‑catch لتقديم رسالة خطأ ودية:

```csharp
try
{
    DateTime parsed = DateTime.Parse(input, japaneseCulture);
}
catch (FormatException)
{
    Console.Error.WriteLine($"'{input}' is not a valid Japanese era date.");
}
```

---

## الخطوة 4: كتابة الـ DateTime المحلل في ورقة عمل Excel

مع كائن `DateTime` جاهز، يمكنك تخزينه في خلية Excel. يقوم NPOI تلقائيًا بتنسيق قيم `DateTime` كتواريخ Excel.

```csharp
using NPOI.SS.UserModel;
using NPOI.XSSF.UserModel;
using System.IO;

// Create a new workbook and a sheet.
IWorkbook workbook = new XSSFWorkbook();
ISheet sheet = workbook.CreateSheet("Japanese Dates");

// Write the DateTime into cell A1 (row 0, column 0).
IRow row = sheet.CreateRow(0);
ICell cell = row.CreateCell(0);
cell.SetCellValue(reiwaDate);

// Optionally apply a date style that shows the era (Excel does not have a built‑in era format,
// so we keep the Gregorian representation).
ICellStyle dateStyle = workbook.CreateCellStyle();
short dateFormatId = workbook.CreateDataFormat().GetFormat("yyyy-mm-dd");
dateStyle.DataFormat = dateFormatId;
cell.CellStyle = dateStyle;

// Save the workbook to a file.
using (FileStream fs = new FileStream("JapaneseEraDate.xlsx", FileMode.Create, FileAccess.Write))
{
    workbook.Write(fs);
}
Console.WriteLine("Excel file 'JapaneseEraDate.xlsx' created successfully.");
```

**النتيجة** – عند فتح *JapaneseEraDate.xlsx* ستظهر التاريخ **2020‑05‑01** في الخلية A1.

### لماذا نستخدم NPOI؟

*يعمل على أي منصة* (Windows، Linux، macOS) ولا يتطلب Microsoft Office. هذا يجعل الحل مناسبًا لأنابيب CI، حاويات Docker، أو المعالجة على الخادم.

---

## الخطوة 5: برنامج كامل قابل للتنفيذ

بجمع كل ما سبق، إليك تطبيق console كامل يوضح سير العمل بالكامل:

```csharp
// File: Program.cs
using System;
using System.Globalization;
using System.IO;
using NPOI.SS.UserModel;
using NPOI.XSSF.UserModel;

class Program
{
    static void Main()
    {
        // 1️⃣ Configure CultureInfo for the Japanese calendar.
        CultureInfo japaneseCulture = new CultureInfo("ja-JP");
        japaneseCulture.DateTimeFormat.Calendar = new JapaneseCalendar();

        // 2️⃣ Parse a Japanese era date string.
        string eraDate = "Reiwa 2/5/1";
        DateTime reiwaDate;
        try
        {
            reiwaDate = DateTime.Parse(eraDate, japaneseCulture);
            Console.WriteLine($"Parsed DateTime: {reiwaDate:u}");
        }
        catch (FormatException)
        {
            Console.Error.WriteLine($"'{eraDate}' is not a valid Japanese era date.");
            return;
        }

        // 3️⃣ Create an Excel workbook and write the date.
        IWorkbook workbook = new XSSFWorkbook();
        ISheet sheet = workbook.CreateSheet("Japanese Dates");
        IRow row = sheet.CreateRow(0);
        ICell cell = row.CreateCell(0);
        cell.SetCellValue(reiwaDate);

        // Apply a simple Gregorian date format.
        ICellStyle style = workbook.CreateCellStyle();
        short fmt = workbook.CreateDataFormat().GetFormat("yyyy-mm-dd");
        style.DataFormat = fmt;
        cell.CellStyle = style;

        // 4️⃣ Save the workbook.
        const string fileName = "JapaneseEraDate.xlsx";
        using (FileStream fs = new FileStream(fileName, FileMode.Create, FileAccess.Write))
        {
            workbook.Write(fs);
        }

        Console.WriteLine($"Excel file '{fileName}' created successfully.");
    }
}
```

**كيفية التشغيل**

```bash
dotnet run
```

بعد التنفيذ، ستجد ملف `JapaneseEraDate.xlsx` في مجلد المشروع مع التاريخ الذي تم تحليله بشكل صحيح.

---

## الأخطاء الشائعة ونصائح الممارسات الأفضل

| الخطأ | الحل / التوصية |
|-------|----------------|
| نسيان ضبط `japaneseCulture.DateTimeFormat.Calendar` | احرص دائمًا على تعيين نسخة `JapaneseCalendar`؛ وإلا لن يتم التعرف على اسم العصر. |
| استخدام `DateTime.TryParse` دون تمرير `CultureInfo` المخصص | مرّر نفس `japaneseCulture` إلى `TryParse` للحفاظ على سلوك متسق. |
| توقع أن Excel يعرض اسم العصر | صيغ التاريخ المدمجة في Excel هي فقط ميلادية. إذا كنت بحاجة لعرض العصر، احفظ السلسلة الأصلية في عمود منفصل أو أنشئ تنسيق نصي مخصص. |
| عدم إغلاق `FileStream` | استخدم كتلة `using` (كما هو موضح) لضمان تحرير مقبض الملف فورًا. |
| خلط كائنات `CultureInfo` بين الخيوط | `CultureInfo` آمن للقراءة عبر الخيوط، لكن تجنّب تعديل خاصية `Calendar` بعد الإعداد الأولي. |

---

## الخلاصة

أنت الآن تعرف **كيفية استخدام CultureInfo للتقويم الياباني** في C# لتحليل تواريخ العصور اليابانية بدقة وكتابة الـ `DateTime` الناتج في ورقة عمل Excel باستخدام NPOI. يغطي المثال الكامل الإعداد، التحليل، معالجة الأخطاء، وإخراج Excel، مما يمنحك أساسًا قويًا لأي سيناريو تقارير دولية أو تبادل بيانات.

بعد ذلك، قد ترغب في استكشاف:

* **تنسيق التواريخ بنص مخصص** للحفاظ على اسم العصر داخل Excel.  
* **قراءة التواريخ من Excel** باستخدام `cell.DateCellValue` مع مراعاة التقويم الياباني.  
* **تطبيق التقنية نفسها** على تقاويم قائمة على العصور أخرى (مثل التقويم البوذي التايلاندي) عن طريق استبدال `JapaneseCalendar` بالفئة `Calendar` المناسبة.

لا تتردد في تجربة سلاسل عصور مختلفة، مجموعات بيانات أكبر، أو دمج هذه المنطق في واجهات ASP.NET Core التي تُنشئ تقارير Excel مباشرة. Happy coding!

## ما الذي ينبغي أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مورد يتضمن أمثلة شاملة مع شروح خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [Create Excel Workbook with Japanese Calendar Dates – Full Guide](/cells/english/net/excel-custom-number-date-formatting/create-excel-workbook-with-japanese-calendar-dates-full-guid/)
- [Parse Japanese Era Dates in Excel – Full Guide for C# Developers](/cells/english/net/data-loading-and-parsing/parse-japanese-era-dates-in-excel-full-guide-for-c-developer/)
- [How to create Excel workbook and parse Japanese dates in C#](/cells/english/net/excel-custom-number-date-formatting/how-to-create-excel-workbook-and-parse-japanese-dates-in-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}