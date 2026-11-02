---
category: general
date: 2026-09-24
description: تحليل DateTime مع عهد الإمبراطور الياباني باستخدام Aspose.Cells في C#.
  تمكين تقويم العصور اليابانية، كتابة سلاسل العصور، واسترجاع قيم DateTime دقيقة.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- Parse DateTime with Japanese Emperor Reign
- Aspose.Cells
- C# date parsing
- Japanese era calendar
- Workbook Settings
- DateTimeValue
language: ar
lastmod: 2026-09-24
og_description: تحليل DateTime باستخدام عهد الإمبراطور الياباني عبر Aspose.Cells في
  C#. يوضح هذا الدليل كيفية تمكين تقويم العصور اليابانية، كتابة سلاسل العصور، وقراءة
  DateTime صحيح.
og_image_alt: Screenshot of C# code parsing a Japanese era date with Aspose.Cells
og_title: تحليل DateTime باستخدام فترة حكم الإمبراطور الياباني مع Aspose.Cells – دليل
  C#
schemas:
- author: Aspose
  dateModified: '2026-09-24'
  description: Parse DateTime with Japanese Emperor Reign using Aspose.Cells in C#.
    Enable the Japanese era calendar, write era strings, and retrieve accurate DateTime
    values.
  headline: Parse DateTime with Japanese Emperor Reign using Aspose.Cells
  type: TechArticle
- description: Parse DateTime with Japanese Emperor Reign using Aspose.Cells in C#.
    Enable the Japanese era calendar, write era strings, and retrieve accurate DateTime
    values.
  name: Parse DateTime with Japanese Emperor Reign using Aspose.Cells
  steps:
  - name: Multiple era formats
    text: 'Aspose.Cells recognises several era representations:'
  - name: Invalid strings
    text: 'When the string cannot be parsed (e.g., `"令和99年13月40日"`), `DateTimeValue`
      returns `DateTime.MinValue`. You can check for this condition:'
  - name: Disabling the feature
    text: 'If you later need to store raw era strings without conversion, set the
      flag back to `false`:'
  - name: Performance tip
    text: Enabling the era calendar adds a small overhead to every `PutValue` call
      that involves strings. If you only parse a handful of cells, enable the flag
      right before the operation and disable it afterward to minimise impact.
  type: HowTo
tags:
- Aspose.Cells
- C#
- DateTime
- Japanese era
- .NET
title: تحليل التاريخ والوقت باستخدام عهد الإمبراطور الياباني مع Aspose.Cells
url: /ar/net/excel-custom-number-date-formatting/parse-datetime-with-japanese-emperor-reign-using-aspose-cell/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تحليل DateTime مع عهد الإمبراطور الياباني باستخدام Aspose.Cells

إذا كنت بحاجة إلى **تحليل DateTime مع عهد الإمبراطور الياباني** في تطبيق .NET، يوضح لك هذا الدليل بالضبط كيفية القيام بذلك باستخدام Aspose.Cells. من خلال تمكين تقويم العصور اليابانية، كتابة سلسلة تعتمد على العصر، وقراءة قيمة `DateTime` الناتجة، ستحصل على تواريخ موثوقة ومراعية للثقافة دون الحاجة إلى معالجة السلاسل يدوياً.

العمل مع تواريخ العصور اليابانية شائع في المالية، الحكومة، والأنظمة القديمة التي لا تزال تخزن تواريخ مثل “令和3年5月10日”. يغطي هذا البرنامج التعليمي سير العمل الكامل، من إعداد المشروع إلى استرجاع كائن `DateTime` يمكنك استخدامه في الحسابات، السجلات، أو عرض واجهة المستخدم.

## ما ستتعلمه

- كيفية إضافة حزمة Aspose.Cells NuGet إلى مشروع C#.
- كيفية تشغيل **تقويم العصور اليابانية** عبر `Workbook.Settings`.
- كيفية كتابة سلسلة تاريخ ياباني بالحقبة في خلية وترك Aspose.Cells يقوم بتحليلها تلقائياً.
- كيفية قراءة `DateTime` المُحلل باستخدام خاصية `DateTimeValue`.

**المتطلبات المسبقة**  
- .NET 6.0 أو أحدث (الكود يعمل أيضاً مع .NET Framework 4.7+).  
- إلمام أساسي بـ C# و Visual Studio (أو أي بيئة تطوير متكاملة).  
- اتصال بالإنترنت لتحميل حزمة Aspose.Cells.

---

## الخطوة 1: تثبيت Aspose.Cells

افتح مجلد مشروعك في الطرفية أو في وحدة تحكم مدير الحزم NuGet وشغّل:

```bash
dotnet add package Aspose.Cells
```

أو، في Visual Studio، انقر بزر الماوس الأيمن على المشروع → **Manage NuGet Packages** → ابحث عن **Aspose.Cells** وانقر **Install**.  
هذا يضيف تجميع `Aspose.Cells`، الذي يوفر `Workbook` و `Worksheet` وقدرات التحليل التي نحتاجها.

## الخطوة 2: تمكين تقويم العصور اليابانية

Aspose.Cells يعطل تحليل العصور اليابانية افتراضياً. يجب عليك تفعيله عبر العلامة `Workbook.Settings.UseJapaneseEraCalendar`.

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // Create a new workbook instance
        Workbook workbook = new Workbook();

        // Enable parsing of Japanese era dates (e.g., 令和, 平成)
        workbook.Settings.UseJapaneseEraCalendar = true;
```

ضبط `UseJapaneseEraCalendar` إلى `true` يخبر المكتبة بتفسير السلاسل التي تحتوي على أسماء العصور (`令和`، `平成`، `昭和`، إلخ) وفقاً للقواعد الرسمية لتقويم اليابان.

## الخطوة 3: كتابة سلسلة تاريخ ياباني بالحقبة في خلية

بعد ذلك، احصل على ورقة العمل الأولى وضع سلسلة تاريخ ياباني بالحقبة في الخلية **A1**.

```csharp
        // Access the first worksheet (index 0)
        Worksheet sheet = workbook.Worksheets[0];

        // Write the era‑based date string into cell A1
        sheet.Cells["A1"].PutValue("令和3年5月10日");
```

**لماذا يعمل هذا:**  
عند تفعيل `UseJapaneseEraCalendar`، تقوم `PutValue` بفحص السلسلة، وتكتشف بادئة العصر (`令和`)، وتحوّلها داخلياً إلى السنة الميلادية المقابلة (2021). ثم تقوم المكتبة بتخزين القيمة ككائن `DateTime` حقيقي، وليس كنص فقط.

## الخطوة 4: استرجاع قيمة `DateTime` المُحللة

الآن اقرأ `DateTimeValue` للخلية. تقوم Aspose.Cells تلقائياً بإرجاع التاريخ الميلادي.

```csharp
        // Retrieve the parsed DateTime from cell A1
        DateTime parsedDate = sheet.Cells["A1"].DateTimeValue;

        // Output the result to the console
        Console.WriteLine($"Parsed Gregorian date: {parsedDate:yyyy-MM-dd}");
    }
}
```

Running the program prints:

```
Parsed Gregorian date: 2021-05-10
```

يؤكد الإخراج أن **تحليل DateTime مع عهد الإمبراطور الياباني** حول بنجاح “令和3年5月10日” إلى 10 مايو 2021.

## الخطوة 5: التعامل مع الحالات الحدية والأنماط الشائعة

### صيغ العصور المتعددة

Aspose.Cells يتعرف على عدة تمثيلات للعصور:

| العصر (ياباني) | نطاق السنة الميلادية |
|----------------|----------------------|
| 明治 (Meiji)   | 1868‑1912            |
| 大正 (Taishō)  | 1912‑1926            |
| 昭和 (Shōwa)   | 1926‑1989            |
| 平成 (Heisei)  | 1989‑2019            |
| 令和 (Reiwa)   | 2019‑present         |

إذا كان مصدر البيانات الخاص بك يخلط بين الأحرف ذات العرض الكامل، المسافات، أو يستخدم الأحرف الصينية “年”، “月”، “日”، فإن المحلل لا يزال ينجح. على سبيل المثال، `"平成31年4月30日"` يتحول إلى `2019-04-30`.

### سلاسل غير صالحة

عند عدم إمكانية تحليل السلسلة (مثال: `"令和99年13月40日"`)، تُعيد `DateTimeValue` القيمة `DateTime.MinValue`. يمكنك التحقق من هذا الشرط:

```csharp
if (parsedDate == DateTime.MinValue)
{
    Console.WriteLine("The cell does not contain a valid Japanese era date.");
}
```

### تعطيل الميزة

إذا احتجت لاحقاً لتخزين سلاسل العصور الأصلية دون تحويل، عُد بالعلامة إلى `false`:

```csharp
workbook.Settings.UseJapaneseEraCalendar = false;
```

### نصيحة الأداء

تمكين تقويم العصور يضيف عبئاً صغيراً على كل استدعاء `PutValue` يتضمن سلاسل. إذا كنت تحلل عددًا قليلًا من الخلايا فقط، فعّل العلامة قبل العملية مباشرةً وعطّلها بعدها لتقليل التأثير.

## مثال كامل قابل للتنفيذ

فيما يلي البرنامج الكامل الذي يمكنك نسخه، لصقه، وتشغيله فوراً.

```csharp
using Aspose.Cells;
using System;

class ParseJapaneseEraDemo
{
    static void Main()
    {
        // 1️⃣ Create a new workbook
        Workbook workbook = new Workbook();

        // 2️⃣ Turn on Japanese era parsing
        workbook.Settings.UseJapaneseEraCalendar = true;

        // 3️⃣ Access the first worksheet
        Worksheet sheet = workbook.Worksheets[0];

        // 4️⃣ Write an era date string into A1
        sheet.Cells["A1"].PutValue("令和3年5月10日");

        // 5️⃣ Retrieve the parsed DateTime
        DateTime parsedDate = sheet.Cells["A1"].DateTimeValue;

        // Verify the result
        Console.WriteLine($"Parsed Gregorian date: {parsedDate:yyyy-MM-dd}");
        // Expected output: Parsed Gregorian date: 2021-05-10
    }
}
```

**الإخراج المتوقع**

```
Parsed Gregorian date: 2021-05-10
```

البرنامج يوضح سير العمل من البداية إلى النهاية لـ **تحليل DateTime مع عهد الإمبراطور الياباني** باستخدام Aspose.Cells، بدءًا من إنشاء دفتر العمل وصولاً إلى الحصول على كائن `DateTime` قابل للاستخدام.

---

## الخلاصة

أنت الآن تعرف كيفية **تحليل DateTime مع عهد الإمبراطور الياباني** في C# عن طريق:

1. تثبيت **Aspose.Cells**.  
2. تمكين **تقويم العصور اليابانية** عبر `Workbook.Settings`.  
3. كتابة سلاسل تعتمد على العصر في الخلايا.  
4. قراءة `DateTimeValue` الناتج.  

هذه الطريقة تلغي الحاجة إلى منطق التحليل اليدوي، تحترم حدود العصور الرسمية، وتندمج بسلاسة مع كود معالجة التواريخ الموجود في .NET.  

**الخطوات التالية**  
- استكشاف ميزات أخرى خاصة بالثقافات في Aspose.Cells، مثل **تحليل تواريخ C#** للتقويم الهجري أو التقويم البوذي التايلاندي.  
- دمج هذه التقنية مع **إعدادات Workbook** مثل `CalcEngine` لتقييم الصيغ التي تشير إلى تواريخ العصور.  
- استخدام `DateTime` المُحلل في التقارير، تخزين قواعد البيانات، أو مكونات واجهة المستخدم التي تتطلب تواريخ ميلادية.

لا تتردد في تجربة سلاسل عصور مختلفة، معالجة المدخلات غير الصالحة، ودمج الحل في خطوط استيراد بيانات أكبر. برمجة سعيدة!

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مورد يتضمن أمثلة كود كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [Parse Japanese Era Dates in Excel – Full Guide for C# Developers](/cells/english/net/data-loading-and-parsing/parse-japanese-era-dates-in-excel-full-guide-for-c-developer/)
- [How to Parse Japanese Dates in C# – Complete Guide](/cells/english/net/data-loading-and-parsing/how-to-parse-japanese-dates-in-c-complete-guide/)
- [How to Implement Date Validation in .NET Using Aspose.Cells: A Comprehensive Guide](/cells/english/net/data-validation/implement-date-validation-net-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}