---
category: general
date: 2026-04-07
description: اكتب التاريخ والوقت إلى Excel باستخدام C#. تعلم كيفية إدراج التاريخ في
  ورقة العمل، ومعالجة قيمة تاريخ الخلية في Excel، وتحويل تاريخ التقويم الياباني في
  بضع خطوات فقط.
draft: false
keywords:
- write datetime to excel
- excel cell date value
- insert date into worksheet
- convert japanese calendar date
language: ar
og_description: اكتب التاريخ والوقت إلى Excel بسرعة. يوضح هذا الدليل كيفية إدراج التاريخ
  في ورقة العمل، وإدارة قيمة تاريخ الخلية في Excel، وتحويل تاريخ التقويم الياباني
  باستخدام C#.
og_title: كتابة التاريخ والوقت إلى Excel – دليل C# خطوة بخطوة
tags:
- C#
- Excel automation
- Aspose.Cells
title: كتابة التاريخ والوقت إلى إكسل – دليل شامل لمطوري C#
url: /ar/net/excel-custom-number-date-formatting/write-datetime-to-excel-complete-guide-for-c-developers/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كتابة التاريخ والوقت إلى Excel – دليل كامل لمطوري C#

هل احتجت يومًا إلى **كتابة التاريخ والوقت إلى Excel** لكنك لم تكن متأكدًا من أي استدعاء API يخزن تاريخ Excel صحيح؟ لست الوحيد. في العديد من الأدوات المؤسسية نحتاج إلى إدراج كائن C# `DateTime` في جدول بيانات، ويجب أن يتصرف الناتج ك تاريخ Excel حقيقي—قابل للفرز، والتصفية، وجاهز لجداول المحور.

في هذا الدرس سنستعرض الخطوات الدقيقة لـ *إدراج تاريخ في ورقة العمل* باستخدام Aspose.Cells، ونشرح لماذا إعداد الثقافة مهم، وحتى نوضح كيفية **تحويل تاريخ التقويم الياباني** إلى `DateTime` عادي قبل كتابته. في النهاية ستحصل على مقتطف مستقل يمكنك نسخه ولصقه في أي مشروع .NET.

## ما ستحتاجه

- **.NET 6+** (أو أي نسخة حديثة من .NET؛ الكود يعمل أيضًا على .NET Framework)  
- **Aspose.Cells for .NET** – حزمة NuGet تتيح لك تعديل ملفات Excel دون الحاجة لتثبيت Office.  
- فهم أساسي لـ C# `DateTime` والثقافات.  

لا تحتاج إلى مكتبات إضافية، ولا إلى COM interop، ولا إلى تثبيت Excel. إذا كان لديك بالفعل كائن ورقة عمل (`ws`)، فأنت جاهز للبدء.

## الخطوة 1: إعداد الثقافة اليابانية (تحويل تاريخ التقويم الياباني)

عند استلامك لتاريخ مثل `"R02/05/01"` (ريوا 2، 1 مايو) يجب إخبار .NET كيف يفسر رموز العصور. التقويم الياباني ليس التقويم الميلادي الافتراضي، لذا نقوم بإنشاء `CultureInfo` يستبدل تقويمه بـ `JapaneseCalendar`.

```csharp
using System;
using System.Globalization;
using Aspose.Cells;   // Make sure Aspose.Cells is referenced

// Assume you already have a worksheet instance named "ws"
Worksheet ws = /* your worksheet instance */;

// 1️⃣ Configure a Japanese culture that uses the Japanese calendar
CultureInfo japaneseCulture = new CultureInfo("ja-JP");
japaneseCulture.DateTimeFormat.Calendar = new JapaneseCalendar();
```

**لماذا هذا مهم:**  
إذا قمت بتحليل السلسلة باستخدام الثقافة الافتراضية، سيطرح .NET استثناء تنسيق لأنه لا يستطيع ربط `R` (عصر ريوا) بسنة. من خلال استبدال `JapaneseCalendar`، يفهم المحلل رموز العصور ويحولها إلى السنة الميلادية الصحيحة.

## الخطوة 2: تحليل السلسلة المعتمدة على العصر إلى `DateTime`

الآن بعد أن تم إعداد الثقافة، يمكننا استدعاء `DateTime.ParseExact` بأمان. سلسلة التنسيق `"ggyy/MM/dd"` تخبر المحلل بـ:

- `gg` – محدد العصر (مثال: `R` للريوا)  
- `yy` – السنة ذات الرقمين داخل العصر  
- `MM/dd` – الشهر واليوم.  

```csharp
// 2️⃣ Parse a date string in the Japanese era format (ggyy/MM/dd)
string japaneseDate = "R02/05/01";          // Reiwa 2, May 1st
DateTime parsedDate = DateTime.ParseExact(
    japaneseDate,
    "ggyy/MM/dd",
    japaneseCulture,
    DateTimeStyles.None
);
```

**نصيحة احترافية:** إذا كان من الممكن أن تستقبل تواريخ بصيغ أخرى (مثال: `"Heisei 30/12/31"`)، غلف عملية التحليل داخل `try/catch` واستخدم `DateTime.TryParseExact` كبديل. هذا يمنع تعطل عملية الاستيراد بأكملها بسبب صف واحد غير صالح.

## الخطوة 3: كتابة `DateTime` في خلية Excel (قيمة تاريخ خلية Excel)

يتعامل Aspose.Cells مع .NET `DateTime` كقيمة تاريخ Excel أصلية عندما تستخدم `PutValue`. تقوم المكتبة تلقائيًا بتحويل الـ ticks إلى الرقم التسلسلي في Excel (عدد الأيام منذ 1900‑01‑00). هذا يعني أن الخلية ستظهر **قيمة تاريخ خلية Excel** صحيحة ويمكنك تنسيقها لاحقًا باستخدام أنماط التاريخ المدمجة في Excel.

```csharp
// 3️⃣ Write the resulting DateTime value into cell C1 of the worksheet
Cell targetCell = ws.Cells["C1"];
targetCell.PutValue(parsedDate);

// Optional: apply a standard date format so users see "yyyy-MM-dd"
targetCell.Style.Number = 14;   // built‑in Excel format ID for "m/d/yy"
```

**ما ستراه في Excel:**  
الخلية C1 الآن تحتوي على الرقم التسلسلي `44796`، والذي يعرضه Excel كـ `2020‑05‑01` (أو أي تنسيق قمت بتطبيقه). القيمة الأساسية هي تاريخ حقيقي، وليس نصًا، لذا يعمل الفرز كما هو متوقع.

## الخطوة 4: حفظ المصنف (الختام)

إذا لم تقم بحفظ المصنف بعد، فافعل ذلك الآن. هذه الخطوة ليست متعلقة مباشرة بكتابة التاريخ والوقت، لكنها تكمل سير العمل.

```csharp
// Save the workbook to a file (or a MemoryStream if you need it in‑memory)
Workbook workbook = ws.Workbook;   // get the parent workbook
workbook.Save("Output.xlsx", SaveFormat.Xlsx);
```

هذا كل شيء—أربع خطوات مختصرة، وقد نجحت في **كتابة التاريخ والوقت إلى Excel**، مع معالجة تاريخ العصر الياباني على طول الطريق.

---

![مثال كتابة التاريخ والوقت إلى Excel](/images/write-datetime-to-excel.png "لقطة شاشة تُظهر مشروع C# يكتب DateTime في خلية Excel C1")

*الصورة أعلاه توضح ملف Excel النهائي مع عرض التاريخ بشكل صحيح في الخلية C1.*

## أسئلة شائعة وحالات خاصة

### ماذا لو لم يكن متغير ورقة العمل جاهزًا بعد؟

يمكنك إنشاء مصنف جديد مباشرةً:

```csharp
Workbook workbook = new Workbook();
Worksheet ws = workbook.Worksheets[0];   // default first sheet
```

### كيف أحافظ على سلسلة العصر الياباني الأصلية في الورقة؟

إذا كنت بحاجة إلى كل من السلسلة الأصلية والتاريخ المحلل، اكتبهما في خلايا متجاورة:

```csharp
ws.Cells["B1"].PutValue(japaneseDate);   // original text
ws.Cells["C1"].PutValue(parsedDate);     // parsed DateTime
```

### هل يعمل هذا مع إصدارات .NET القديمة؟

نعم. `JapaneseCalendar` موجود منذ .NET 2.0، و Aspose.Cells يدعم .NET Framework 4.5+. فقط تأكد من الإشارة إلى التجميع الصحيح.

### ماذا عن المناطق الزمنية؟

`DateTime.ParseExact` يُعيد **Kind** بقيمة `Unspecified`. إذا كانت تواريخ المصدر بتوقيت UTC، قم بتحويلها أولاً:

```csharp
DateTime utcDate = DateTime.SpecifyKind(parsedDate, DateTimeKind.Utc);
DateTime localDate = utcDate.ToLocalTime();
targetCell.PutValue(localDate);
```

### هل يمكنني تعيين تنسيق تاريخ مخصص (مثال: “yyyy年MM月dd日” )؟

بالطبع. استخدم الخاصية `Style.Custom`:

```csharp
targetCell.Style.Custom = "yyyy\"年\"mm\"月\"dd\"日\"";
```

الآن سيظهر Excel `2020年05月01日` مع استمرار تخزين قيمة تاريخ حقيقية.

## ملخص

لقد غطينا كل ما تحتاجه **للكتابة التاريخ والوقت إلى Excel** من C#:

1. **تهيئة** ثقافة يابانية باستخدام `JapaneseCalendar` لـ **تحويل تاريخ التقويم الياباني**.  
2. **تحليل** السلسلة المعتمدة على العصر باستخدام `DateTime.ParseExact`.  
3. **إدراج** الـ `DateTime` الناتج في خلية، مع ضمان **قيمة تاريخ خلية Excel** صحيحة.  
4. **حفظ** المصنف لضمان بقاء البيانات.  

مع هذه الخطوات الأربع يمكنك بأمان **إدراج تاريخ في ورقة العمل** بغض النظر عن تنسيق المصدر. الشيفرة قابلة للتنفيذ بالكامل، تحتاج فقط إلى Aspose.Cells، وتعمل على أي بيئة تشغيل .NET حديثة.

## ما التالي؟

- **استيراد جماعي:** تكرار عبر الصفوف في ملف CSV، تحليل كل تاريخ ياباني، وكتابته في خلايا متتالية.  
- **التنسيق:** تطبيق تنسيق شرطي لتسليط الضوء على التواريخ المتأخرة.  
- **الأداء:** استخدم `WorkbookDesigner` أو تخزين `CellStyle` مؤقتًا عند التعامل مع آلاف الصفوف.  

لا تتردد في التجربة—استبدل العصر الياباني بالتقويم الميلادي، غير الخلية المستهدفة، أو صدّر إلى تنسيق ملف مختلف (CSV، ODS). الفكرة الأساسية تبقى نفسها: تحليل، تحويل، و **كتابة التاريخ والوقت إلى Excel** بثقة.

برمجة سعيدة، ولتكن جداولك دائمًا مرتبة بشكل صحيح!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}