---
category: general
date: 2026-05-23
description: كيفية استخراج التاريخ من خلية إكسل باستخدام C#. تعلم حيل تنسيق الأرقام
  المخصص في إكسل، قراءة التاريخ من الخلية، وتطبيق تنسيق مخصص للحصول على نتائج دقيقة.
draft: false
keywords:
- how to parse date
- custom number format excel
- read date from cell
- format excel cell date
- apply custom format
language: ar
og_description: كيفية استخراج التاريخ من خلية إكسل باستخدام C#. يوضح هذا الدرس كيفية
  تطبيق تنسيق رقم مخصص في إكسل، قراءة التاريخ من الخلية، وتنسيق تاريخ خلية إكسل بشكل
  صحيح.
og_title: كيفية تحليل التاريخ في Excel باستخدام C# – دليل كامل
schemas:
- author: Aspose
  dateModified: '2026-05-23'
  description: How to parse date from an Excel cell using C#. Learn custom number
    format Excel tricks, read date from cell, and apply custom format for accurate
    results.
  headline: How to Parse Date in Excel with C# – Complete Guide
  type: TechArticle
- description: How to parse date from an Excel cell using C#. Learn custom number
    format Excel tricks, read date from cell, and apply custom format for accurate
    results.
  name: How to Parse Date in Excel with C# – Complete Guide
  steps:
  - name: Why a Custom Format Works
    text: Excel stores dates as serial numbers internally. By applying a locale‑aware
      format, Excel attempts to *interpret* the underlying text according to the pattern.
      The `[$-ja-JP]` prefix forces the Japanese calendar rules, while the rest of
      the pattern maps the characters to year, month, and day.
  - name: 1. Parsing European Dates (e.g., “12/05/2021” in French)
    text: '```csharp firstCell.PutValue("12/05/2021"); // day/month/year Style frStyle
      = workbook.CreateStyle(); frStyle.Custom = "[$-fr-FR]dd/mm/yyyy"; firstCell.SetStyle(frStyle);
      DateTime frDate = firstCell.DateTimeValue; // 2021-05-12 ```'
  - name: 2. When the Cell Already Contains a Serial Date
    text: 'If the source Excel file already stores a true date value, you can skip
      the custom format entirely:'
  - name: 3. Fallback to Manual Parsing
    text: 'Sometimes data is messy (extra spaces, hidden characters). A safe fallback
      is:'
  type: HowTo
tags:
- Excel
- C#
- Date Parsing
title: كيفية تحليل التاريخ في إكسل باستخدام C# – دليل شامل
url: /ar/net/excel-custom-number-date-formatting/how-to-parse-date-in-excel-with-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تحليل التاريخ في Excel باستخدام C# – دليل شامل

هل تساءلت يومًا **كيف يتم تحليل التاريخ** المخزن في ورقة عمل Excel دون العبث يدويًا بتحويل السلاسل؟ لست الوحيد. سواء كنت تستخرج تواريخ مالية يابانية، أو تركيبات شهر‑يوم أوروبية، أو أي سلسلة خاصة بالمنطقة، فإن الحصول على `DateTime` موثوق به في C# قد يشعر وكأنه مطاردة هدف متحرك.  

في هذا الدرس سنستعرض مثالًا ملموسًا من البداية إلى النهاية ي **يطبق تنسيق رقم مخصص في Excel** على خلية نصية، ثم **يقرأ التاريخ من الخلية** ككائن `DateTime` صحيح. بنهاية الدرس ستعرف بالضبط كيف **تنسيق تاريخ خلية Excel**، **تطبيق تنسيق مخصص**، وتجنب المشكلات الشائعة التي تعيق معظم المطورين.

## المتطلبات المسبقة

- .NET 6.0 أو أحدث (الكود يعمل مع .NET Core، .NET Framework، و .NET 5+)
- إشارة إلى مكتبة جداول بيانات تدعم تعديل الأنماط – العينة تستخدم **Aspose.Cells**، لكن المفاهيم يمكن تطبيقها على EPPlus أو ClosedXML أو NPOI.
- معرفة أساسية بـ C# (أنت تمتلكها، أليس كذلك؟)

> **نصيحة احترافية:** إذا لم تكن لديك Aspose.Cells بعد، يمكنك الحصول على نسخة تجريبية مجانية من موقعهم وإضافتها عبر NuGet: `dotnet add package Aspose.Cells`.

## نظرة عامة على الحل

1. **إنشاء مصنف** واستهداف الخلية الأولى في الورقة الأولى.  
2. **إدخال سلسلة تاريخ خاصة بالمنطقة** (يابانية في حالتنا).  
3. **تطبيق تنسيق رقم مخصص** يخبر Excel بمعالجة السلسلة ك تاريخ.  
4. **قراءة قيمة الخلية** مرة أخرى ككائن `DateTime`.

هذا هو سير العمل بالكامل – بدون تحليل يدوي، بدون تمارين `DateTime.ParseExact`. هيا نغوص في التفاصيل.

---

## الخطوة 1: إعداد المصنف والخلية المستهدفة

أولاً، أنشئ مصنفًا جديدًا واحصل على الخلية التي سنعمل عليها. هذا يعكس سيناريو “مصنف جديد” الذي تبدأ منه معظم وظائف المعالجة الدفعية.

```csharp
using Aspose.Cells;

// Create a new workbook
Workbook workbook = new Workbook();

// Get the first worksheet's first cell (A1)
Cell firstCell = workbook.Worksheets[0].Cells[0, 0];
```

> **لماذا هذا مهم:** تهيئة المصنف برمجيًا تضمن أننا نتحكم في كل جانب من جوانب الملف – دون مفاجآت تنسيق مخفية. كائن `Cell` هو نقطة الدخول لكل من المحتوى والنمط.

---

## الخطوة 2: إدخال سلسلة تاريخ يابانية

غالبًا ما يستقبل Excel التواريخ كنص عادي، خاصةً عندما تأتي البيانات من أنظمة قديمة. هنا نحاكي ذلك بوضع تاريخ ياباني للحقبة مباشرةً في الخلية.

```csharp
// Insert a Japanese date string (令和3年5月12日 = May 12, 2021)
firstCell.PutValue("令和3年5月12日");
```

> **ملاحظة حالة حافة:** إذا كانت الخلية تحتوي بالفعل على تاريخ Excel حقيقي (رقم تسلسلي)، يمكنك تخطي خطوة التنسيق المخصص. يركز هذا الدليل على مسار التحويل *من نص إلى تاريخ*.

---

## الخطوة 3: تطبيق تنسيق رقم مخصص يفسر النص ك تاريخ

الآن يأتي السحر: نخبر Excel بمعالجة السلسلة باستخدام نمط **تنسيق رقم مخصص في Excel** يحترم الإعداد المحلي الياباني. سلسلة التنسيق `[$-ja-JP]yyyy` تستخرج جزء السنة، لكن يمكنك توسيعها لتشمل الشهر واليوم حسب الحاجة.

```csharp
// Define a style with a custom number format for Japanese locale
Style style = workbook.CreateStyle();
style.Custom = "[$-ja-JP]yyyy\"年\"m\"月\"d\"日\"";

// Apply the style to the cell
firstCell.SetStyle(style);
```

### لماذا يعمل التنسيق المخصص

Excel يخزن التواريخ كأرقام تسلسلية داخليًا. من خلال تطبيق تنسيق واعٍ للمنطقة، يحاول Excel *تفسير* النص الأساسي وفقًا للنمط. البادئة `[$-ja-JP]` تفرض قواعد التقويم الياباني، بينما باقي النمط يربط الأحرف بالسنة والشهر واليوم.

> **بديل:** إذا كنت بحاجة إلى نهج أكثر عمومية، يمكنك استخدام `[$-en-US]mm/dd/yyyy` لتواريخ النمط الأمريكي، أو أي رمز ثقافة آخر يدعمه Windows.

---

## الخطوة 4: استرجاع التاريخ المحلل ككائن `DateTime`

أخيرًا، نطلب من الخلية قيمة `DateTimeValue`. تقوم Aspose.Cells تلقائيًا بتحويل النص المنسق إلى كائن `DateTime` صحيح.

```csharp
// Retrieve the cell value as a DateTime
DateTime parsedDate = firstCell.DateTimeValue;

// Output to console for verification
Console.WriteLine($"Parsed date: {parsedDate:yyyy-MM-dd}");
```

**المخرجات المتوقعة في وحدة التحكم**

```
Parsed date: 2021-05-12
```

> **ماذا لو أعاد `DateTime.MinValue`؟** هذا عادةً يعني أن التنسيق لم يتطابق مع محتوى الخلية. تحقق مرة أخرى من سلسلة التنسيق المخصص وتأكد من أن رمز المنطقة يتطابق مع لغة المصدر.

---

## إضافي: معالجة مناطق أخرى وتنوعات العالم الحقيقي

### 1. تحليل تواريخ أوروبية (مثال: “12/05/2021” بالفرنسية)

```csharp
firstCell.PutValue("12/05/2021"); // day/month/year
Style frStyle = workbook.CreateStyle();
frStyle.Custom = "[$-fr-FR]dd/mm/yyyy";
firstCell.SetStyle(frStyle);
DateTime frDate = firstCell.DateTimeValue; // 2021-05-12
```

### 2. عندما تحتوي الخلية بالفعل على تاريخ تسلسلي

إذا كان ملف Excel المصدر يخزن بالفعل قيمة تاريخ حقيقية، يمكنك تخطي التنسيق المخصص تمامًا:

```csharp
DateTime existingDate = firstCell.DateTimeValue; // works out‑of‑the‑box
```

### 3. اللجوء إلى التحليل اليدوي

أحيانًا تكون البيانات فوضوية (مسافات إضافية، أحرف مخفية). خيار آمن هو:

```csharp
string raw = firstCell.StringValue?.Trim();
if (DateTime.TryParseExact(raw, "yyyy/MM/dd", CultureInfo.InvariantCulture,
                           DateTimeStyles.None, out DateTime fallback))
{
    // use fallback
}
```

لكن نهج **تطبيق تنسيق مخصص** يكون عادةً أسرع وأقل عرضة للأخطاء لأنه يستفيد من محرك التحليل الخاص بـ Excel.

---

## المشكلات الشائعة وكيفية تجنبها

| المشكلة | العرض | الحل |
|---------|---------|-----|
| رمز المنطقة الخاطئ (`[$-ja-JP]` مقابل `[$-ja]`) | `DateTimeValue` يبقى عند `1/1/1900` | تحقق من سلسلة LCID الدقيقة؛ استخدم `CultureInfo.GetCultureInfo("ja-JP").LCID` للتأكد. |
| غياب علامات الاقتباس حول النص الثابت | Excel يتعامل مع `"年"` كعنصر نائب في التنسيق ويفشل | ضع الأحرف الثابتة بين علامات اقتباس مزدوجة، مثل `\"年\"`. |
| الخلية مُنسقة بالفعل كـ *نص* | تم تجاهل التنسيق المخصص | امسح `NumberFormat` للخلية أولاً: `firstCell.SetStyle(workbook.CreateStyle());` |
| استخدام مكتبة لا تدعم خاصية `Custom` | خطأ في التجميع | التبديل إلى مكتبة تُظهر تنسيقات رقم مخصصة (Aspose.Cells، EPPlus، ClosedXML). |

---

## مثال كامل يعمل (جاهز للنسخ واللصق)

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Create workbook and get target cell
        Workbook workbook = new Workbook();
        Cell firstCell = workbook.Worksheets[0].Cells[0, 0];

        // 2️⃣ Insert Japanese date string
        firstCell.PutValue("令和3年5月12日");

        // 3️⃣ Apply custom number format for Japanese locale
        Style style = workbook.CreateStyle();
        style.Custom = "[$-ja-JP]yyyy\"年\"m\"月\"d\"日\"";
        firstCell.SetStyle(style);

        // 4️⃣ Retrieve parsed DateTime
        DateTime parsedDate = firstCell.DateTimeValue;

        // Verify the result
        Console.WriteLine($"Parsed date: {parsedDate:yyyy-MM-dd}");
        // Expected: Parsed date: 2021-05-12

        // Optional: Save the workbook to see the formatted cell in Excel
        workbook.Save("ParsedDateExample.xlsx");
    }
}
```

شغّل البرنامج، افتح `ParsedDateExample.xlsx`، وسترى الخلية **A1** تعرض `2021年5月12日` بينما القيمة الأساسية هي تاريخ Excel صحيح.

---

## الخلاصة

لقد غطينا **كيفية تحليل سلاسل التاريخ** في Excel باستخدام C# عبر **تطبيق تنسيق رقم مخصص في Excel** ثم **قراءة التاريخ من الخلية** كـ `DateTime` أصلي. النقاط الرئيسية:

- استخدم تنسيقًا مخصصًا واعيًا للمنطقة (`[$-ja-JP]…`) لتترك Excel يقوم بالعمل الشاق.
- الوصول إلى `Cell.DateTimeValue` للحصول على `DateTime` نظيف دون تحليل يدوي.
- عدّل سلسلة التنسيق للثقافات الأخرى، وتأكد دائمًا من ذلك عبر طباعة سريعة في وحدة التحكم.

من هنا يمكنك **تنسيق تاريخ خلية Excel** للتقارير، إدخال `DateTime` في قواعد البيانات، أو إجراء حسابات مباشرة في تطبيق C# الخاص بك. جرّب مناطق مختلفة، اجمع عدة خلايا، أو حتى عالج دفعة كاملة من الأوراق – نفس المبادئ تنطبق.

هل لديك تنسيق تاريخ غريب لا تستطيع حله؟ اترك تعليقًا، وسنقوم بحل المشكلة معًا. برمجة سعيدة!

## دروس ذات صلة

- [تنسيق رقم وتاريخ مخصص في Excel](/cells/english/net/excel-custom-number-date-formatting/)
- [إتقان عرض البيانات في Excel: تنسيق الأرقام والتواريخ المخصصة باستخدام Aspose.Cells للـ Java](/cells/english/java/formatting/aspose-cells-java-data-formatting-excel/)
- [تنسيق رقم وتاريخ مخصص في Excel](/cells/german/net/excel-custom-number-date-formatting/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}