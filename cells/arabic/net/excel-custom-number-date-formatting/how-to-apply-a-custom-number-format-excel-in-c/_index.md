---
category: general
date: 2026-10-26
description: تعلم كيفية تعيين تنسيق رقم مخصص لملف إكسل في C# عن طريق ضبط الأرقام ذات
  الأهمية، وإنشاء مصنف إكسل، وحفظه كملف XLSX.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- custom number format excel
- set significant digits
- how to set number format
- create excel workbook c#
- save workbook xlsx
language: ar
lastmod: 2026-10-26
og_description: تنسيق الأرقام المخصص في Excel باستخدام C# يتيح لك التحكم في الأرقام
  الهامة، وإنشاء مصنف Excel، وحفظه كملف XLSX. اتبع هذا الدليل الكامل.
og_image_alt: Excel cell A1 displaying a number formatted with 4 significant digits
  using C#
og_title: تنسيق رقم مخصص في Excel باستخدام C# – دليل خطوة بخطوة
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Learn how to set a custom number format excel file in C# by configuring
    significant digits, creating an Excel workbook, and saving it as an XLSX document.
  headline: How to apply a custom number format excel in C#
  type: TechArticle
- description: Learn how to set a custom number format excel file in C# by configuring
    significant digits, creating an Excel workbook, and saving it as an XLSX document.
  name: How to apply a custom number format excel in C#
  steps:
  - name: Using a custom format string instead of global options
    text: 'If you need a format that applies only to a single range, you can assign
      a format string directly:'
  - name: Applying the setting to an entire column
    text: '```csharp // Apply the same significant‑digit rule to column B ws.Cells.Columns[1].ApplyNumberFormatOptions(
      new NumberFormatOptions { SignificantDigits = 4 }); ```'
  - name: Dealing with negative numbers
    text: 'The global `SignificantDigits` option works uniformly for positive and
      negative numbers. If you want a different display for negatives, combine it
      with a custom format:'
  type: HowTo
tags:
- Excel
- C#
- Aspose.Cells
title: كيفية تطبيق تنسيق رقم مخصص في Excel باستخدام C#
url: /ar/net/excel-custom-number-date-formatting/how-to-apply-a-custom-number-format-excel-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تطبيق تنسيق رقم مخصص في Excel باستخدام C#

إذا كنت بحاجة إلى **custom number format excel** يُظهر عددًا محددًا من الأرقام ذات الدلالة، فإن هذا الدليل يوضح لك بالضبط كيفية القيام بذلك في C#. سترى كيفية تعيين الأرقام ذات الدلالة، وإنشاء مصنف Excel، وحفظ المصنف كملف XLSX—كل ذلك بضع أسطر من الشيفرة.

العمل مع ملفات Excel برمجيًا يعني غالبًا أنك تحتاج إلى التحكم في طريقة ظهور الأرقام. باستخدام Aspose.Cells لـ .NET يمكنك تعريف خيار تنسيق رقم عالمي يُجبر كل خلية رقمية على احترام عدد محدد من الأرقام ذات الدلالة. يغطي هذا البرنامج التعليمي سير العمل الكامل، من إعداد المشروع إلى التحقق من النتيجة في Excel.

## المتطلبات المسبقة

* .NET 6.0 أو أحدث مثبت (الكود يعمل أيضًا مع .NET Framework 4.7.2+)
* Visual Studio 2022 أو أي بيئة تطوير C# تفضلها
* حزمة NuGet **Aspose.Cells** (`Install-Package Aspose.Cells`) – مكتبة مُدارة بالكامل لمعالجة Excel
* إلمام أساسي بصياغة C#

## الخطوة 1: إنشاء مصنف Excel في C#

العملية الأولى هي إنشاء كائن `Workbook` جديد. هذا الكائن يمثل ملف Excel بالكامل في الذاكرة.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Create a new workbook instance
        Workbook wb = new Workbook();

        // The workbook now contains a default worksheet named "Sheet1"
        // You can access it via the Worksheets collection.
        Worksheet ws = wb.Worksheets[0];
```

**لماذا هذا مهم:** `Workbook` هو نقطة الدخول لكل عملية في Excel. بإنشائه أولًا، تضمن ملفًا نظيفًا يمكنك لاحقًا حفظه كـ XLSX.

## الخطوة 2: تكوين تنسيق الرقم لتعيين الأرقام ذات الدلالة

توفر Aspose.Cells إعدادًا عالميًا يُدعى `NumberFormatOptions`. بتعيين `SignificantDigits = 4`، ستعرض كل خلية رقمية حتى أربعة أرقام ذات دلالة ما لم يتجاوزها تنسيق أكثر تحديدًا.

```csharp
        // Step 2: Set the global number‑format option to 4 significant digits
        WorkbookSettings.SetNumberFormatOptions(
            new NumberFormatOptions { SignificantDigits = 4 });
```

**لماذا هذا مهم:** استخدام `SetNumberFormatOptions` يتيح لك تعريف **custom number format excel** دون كتابة سلسلة تنسيق لكل خلية. وهو يعكس خيار “الأرقام ذات الدلالة” الذي ستجده في مربع حوار Excel *Format Cells → Number → Custom*.

## الخطوة 3: كتابة القيم والتحقق من تنسيق الرقم المخصص

الآن ضع قيمة رقمية في خلية. سيطبق الإعداد العالمي قاعدة الأربعة أرقام تلقائيًا.

```csharp
        // Step 3: Write a numeric value into cell A1 (row 0, column 0)
        ws.Cells[0, 0].PutValue(123.456789);

        // Optional: Add a label so you can see the effect in Excel
        ws.Cells[0, 1].PutValue("Original value:");
        ws.Cells[0, 2].PutValue(123.456789);
```

عند فتح الملف المحفوظ، ستظهر الخلية **A1** القيمة `123.5` (مقربة إلى أربعة أرقام ذات دلالة). القيمة الأصلية تظل دون تغيير في البيانات الأساسية، ويمكنك التأكد من ذلك بالنظر إلى شريط الصيغة.

**نصيحة للحالات الخاصة:** إذا خزنت رقمًا كبيرًا جدًا مثل `12345678.9`، سيعرض الإعداد نفسه `1.235E+07` (صيغة علمية) لأن Excel يختار أكثر تمثيل مضغوط مع الحفاظ على أربعة أرقام ذات دلالة.

## الخطوة 4: حفظ المصنف كملف XLSX

أخيرًا، احفظ المصنف على القرص. طريقة `Save` تختار تلقائيًا تنسيق الملف بناءً على الامتداد.

```csharp
        // Step 4: Save the workbook to an XLSX file
        string outputPath = @"C:\Temp\SigDigits.xlsx";
        wb.Save(outputPath);

        // Inform the user
        System.Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

**لماذا هذا مهم:** الحفظ كـ **XLSX** (`save workbook xlsx`) يضمن أقصى توافق مع إصدارات Excel الحديثة، Office 365، وأدوات الجداول الأخرى.

## النتيجة المتوقعة

افتح *C:\Temp\SigDigits.xlsx* في Microsoft Excel. يجب أن ترى:

| A          | B               | C               |
|------------|-----------------|-----------------|
| **123.5**  | القيمة الأصلية: | **123.456789**  |

*الخلية A1* تُظهر الرقم مقربًا إلى أربعة أرقام ذات دلالة، بينما *C1* يحتفظ بالدقة الكاملة للمقارنة.

## الاختلافات الشائعة وكيفية تعيين تنسيق الرقم لخلايا محددة

### استخدام سلسلة تنسيق مخصصة بدلاً من الخيارات العالمية

إذا كنت بحاجة إلى تنسيق يطبق فقط على نطاق واحد، يمكنك تعيين سلسلة تنسيق مباشرةً:

```csharp
ws.Cells["D1"].PutValue(0.0012345);
Style style = wb.CreateStyle();
style.Custom = "0.####"; // shows up to 4 decimal places, not significant digits
ws.Cells["D1"].SetStyle(style);
```

### تطبيق الإعداد على عمود كامل

```csharp
// Apply the same significant‑digit rule to column B
ws.Cells.Columns[1].ApplyNumberFormatOptions(
    new NumberFormatOptions { SignificantDigits = 4 });
```

### التعامل مع الأعداد السالبة

خيار `SignificantDigits` العالمي يعمل بشكل موحد للأعداد الموجبة والسالبة. إذا أردت عرضًا مختلفًا للسالبة، اجمعه مع تنسيق مخصص:

```csharp
Style negStyle = wb.CreateStyle();
negStyle.Custom = "#,##0.###;[Red]-#,##0.###";
ws.Cells["E1"].PutValue(-9876.54321);
ws.Cells["E1"].SetStyle(negStyle);
```

## نصائح احترافية ومخاطر

* **نصيحة احترافية:** عيّن خيارات تنسيق الرقم **قبل** كتابة أي بيانات. تغيير الخيار بعد ملء الخلايا لا يعيد تنسيق القيم الموجودة بأثر رجعي.
* **احذر من:** استخدام `PutValue` مع **سلسلة** تبدو كرقم (مثال، `"123.45"`). سيعامل Excel ذلك كنص، ولن يُطبق التنسيق المخصص.
* **ملاحظة أداء:** الإعدادات العالمية قليلة التكلفة، لكن تطبيق نمط على ملايين الخلايا قد يزيد من استهلاك الذاكرة. استخدم تنسيق على مستوى العمود عندما يكون ذلك ممكنًا.

## الخطوات التالية

الآن بعد أن يمكنك **custom number format excel** للملفات مع الأرقام ذات الدلالة، قد ترغب في استكشاف:

* **كيفية تعيين تنسيق الرقم** للتواريخ والعملات باستخدام `Style.Custom`.
* **إنشاء مخططات** تحترم تنسيقاتك المخصصة.
* **التصدير إلى CSV** مع الحفاظ على دقة الأرقام (`save workbook xlsx` → `wb.Save("file.csv", SaveFormat.Csv)`).

هذه المواضيع تبني على نفس مفاهيم `Workbook` و `Worksheet` التي تم توضيحها هنا.

---

**الملخص**

لقد تعلمت كيفية **custom number format excel** عن طريق تكوين `NumberFormatOptions` لت **تعيين الأرقام ذات الدلالة**، وإنشاء مصنف Excel في C#، وكتابة القيم، و**حفظ المصنف كملف XLSX**. الشيفرة الكاملة القابلة للتنفيذ أعلاه تُظهر كل خطوة، وتوضح لماذا كل جزء ضروري، وتقدم نصائح للاختلافات الشائعة. لا تتردد في تعديل المقاطع لتناسب مشاريعك الخاصة وتجربة سيناريوهات تنسيق أخرى.

## ماذا يجب أن تتعلم بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مصدر يتضمن أمثلة شيفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [تنسيق رقم مخصص في Excel باستخدام C# – دليل كامل](/cells/english/net/excel-custom-number-date-formatting/custom-number-format-excel-in-c-complete-guide/)
- [إنشاء مصنف Excel C# – تحديد حد للأرقام ذات الدلالة في Excel](/cells/english/net/excel-custom-number-date-formatting/create-excel-workbook-c-limit-significant-digits-excel/)
- [كيفية تطبيق تنسيق رقم Excel باستخدام Aspose.Cells](/cells/english/net/excel-custom-number-date-formatting/how-to-apply-number-format-excel-with-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}