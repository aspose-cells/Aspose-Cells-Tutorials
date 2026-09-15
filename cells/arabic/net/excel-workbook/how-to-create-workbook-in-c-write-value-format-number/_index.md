---
category: general
date: 2026-03-01
description: كيفية إنشاء دفتر عمل في C# بسرعة — تعلم كتابة قيمة في خلية، ضبط تنسيق
  رقم الخلية، وتنسيق رقم الخلية بخطوات بسيطة.
draft: false
keywords:
- how to create workbook
- write value to cell
- format cell number
- set cell number format
- how to write cell
language: ar
og_description: كيف تنشئ دفتر عمل في C#؟ يوضح لك هذا الدليل كيفية كتابة قيمة إلى خلية،
  وتعيين تنسيق رقم الخلية، وتنسيق رقم الخلية في بضع أسطر من الشيفرة فقط.
og_title: كيفية إنشاء دفتر عمل في C# – كتابة القيمة وتنسيق الرقم
tags:
- C#
- Aspose.Cells
- Excel Automation
title: كيفية إنشاء دفتر عمل في C# – كتابة القيمة وتنسيق الرقم
url: /ar/net/excel-workbook/how-to-create-workbook-in-c-write-value-format-number/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية إنشاء دفتر عمل في C# – كتابة قيمة وتنسيق الرقم

إنشاء دفتر عمل في C# مهمة شائعة عندما تحتاج إلى توليد ملفات Excel في الوقت الفعلي. في هذا الدليل سنرشدك إلى كيفية كتابة قيمة إلى خلية وتنسيق رقم الخلية بحيث يبدو الورق النهائي مصقلاً.

إذا سبق لك أن حدقت في جدول بيانات فارغ وتساءلت لماذا تظهر الأرقام بعدد كبير من الكسور العشرية، فأنت لست وحدك. سنغطي كل شيء من تهيئة كائن دفتر العمل إلى ضبط تنسيق رقم مخصص، وسنضيف بعض النصائح للحالات الخاصة التي قد تواجهها لاحقًا.

## ما ستتعلمه

- **تهيئة** كائن `Workbook` جديد.  
- **كتابة قيمة إلى خلية** باستخدام الطريقة `PutValue`.  
- **ضبط تنسيق رقم الخلية** باستخدام كائن `Style`، للحصول على عرض نظيف برقمين بعد الفاصلة.  
- التحقق من النتيجة بقراءة الخلية مرة أخرى أو فتح الملف في Excel.  

لا تحتاج إلى مكتبات خارجية بخلاف Aspose.Cells (أو أي API مشابه) القياسية، ويعمل الكود على .NET 6+ دون إعدادات إضافية.

---

## كيفية إنشاء دفتر عمل – تهيئة الكائن

أولاً وقبل كل شيء: تحتاج إلى كائن دفتر عمل يحمل أوراقك. فكر في `Workbook` كملف Excel بالكامل، بينما كل `Worksheet` هو تبويب واحد.

```csharp
// Step 1: Create a new workbook instance
Workbook workbook = new Workbook();
```

*لماذا هذا مهم:* إنشاء دفتر العمل يخصص البُنى الداخلية التي ستحمل لاحقًا الصفوف والأعمدة والتنسيقات. بدون هذا الكائن، لا مكان لكتابة قيمة إلى خلية.

> **نصيحة محترف:** إذا كنت تخطط للعمل على ملف موجود مسبقًا، استبدل `new Workbook()` بـ `new Workbook("template.xlsx")` لتحميل قالب والحفاظ على أنماطه.

## كتابة قيمة إلى خلية

الآن بعد أن لدينا دفتر عمل، لنضع رقمًا في الخلية **A1** في أول ورقة عمل.

```csharp
// Step 2: Access cell A1 in the first worksheet
Cell cellA1 = workbook.Worksheets[0].Cells["A1"];

// Step 3: Insert a numeric value into the cell
cellA1.PutValue(123.456789);
```

*لماذا نستخدم `PutValue`*: هذه الطريقة تكتشف نوع البيانات تلقائيًا، لذا لا تحتاج إلى تحويل أو إلقاء يدوي. كما أنها تحترم النمط الحالي للخلية، وهو مفيد عندما تقوم لاحقًا **بتعيين تنسيق رقم الخلية**.

### فحص سريع

إذا قرأت الخلية مرة أخرى، سترى القيمة الخام:

```csharp
double raw = cellA1.DoubleValue; // raw == 123.456789
```

هذه هي القيمة قبل تطبيق أي تنسيق.

## ضبط تنسيق رقم الخلية

عرض عدد مزدوج (double) خام مع العديد من الكسور العشرية ليس دائمًا صديقًا للمستخدم. لنحدده إلى رقمين مهمين.

```csharp
// Step 4: Apply a style that formats the number with two significant digits
cellA1.SetStyle(new Style() { Number = 2 });
```

خاصية `Number` تت对应 مع معرّفات تنسيقات الأرقام المدمجة في Excel. الرقم `2` يعني “عدد مع منزلتين عشريتين”. إذا احتجت تنسيقًا مختلفًا—مثل العملة أو التاريخ—ستستخدم معرّفًا آخر أو سلسلة تنسيق مخصصة.

### بديل: سلسلة تنسيق مخصصة

```csharp
Style customStyle = workbook.CreateStyle();
customStyle.Custom = "#,##0.00"; // forces two decimals with thousand separator
cellA1.SetStyle(customStyle);
```

*لماذا نختار نمطًا مخصصًا؟* يمنحك تحكمًا كاملاً، خاصة عندما لا تغطي المعرفات المدمجة إعداداتك الإقليمية.

## التحقق من النتيجة (اختياري لكن موصى به)

بعد تطبيق النمط، يمكنك حفظ دفتر العمل وفتحه في Excel لتأكيد المظهر.

```csharp
// Save the workbook to a file
workbook.Save("FormattedWorkbook.xlsx");

// Or, for quick verification in code:
string displayed = cellA1.StringValue; // "123.46"
Console.WriteLine($"Displayed value: {displayed}");
```

يجب أن ترى **123.46** في الخلية A1—بالضبط منزلتين عشريتين، بفضل التنسيق الذي وضعناه.

---

### مثال كامل يعمل

بدمج كل ما سبق، إليك برنامج مستقل يمكنك نسخه ولصقه في تطبيق Console.

```csharp
using System;
using Aspose.Cells;   // Ensure you have the Aspose.Cells NuGet package

class Program
{
    static void Main()
    {
        // Initialize the workbook
        Workbook workbook = new Workbook();

        // Access the first worksheet and cell A1
        Cell cellA1 = workbook.Worksheets[0].Cells["A1"];

        // Write a numeric value
        cellA1.PutValue(123.456789);

        // Apply a two‑decimal number format
        cellA1.SetStyle(new Style() { Number = 2 });

        // Save to disk (optional)
        workbook.Save("FormattedWorkbook.xlsx");

        // Output the displayed text for verification
        Console.WriteLine($"Cell A1 shows: {cellA1.StringValue}");
    }
}
```

**الناتج المتوقع عند تشغيل البرنامج:**

```
Cell A1 shows: 123.46
```

افتح `FormattedWorkbook.xlsx` في Excel وسترى نفس القيمة المنسقة.

---

## تنوعات شائعة وحالات خاصة

### 1. تنسيقات أرقام مختلفة

| الهدف | معرّف التنسيق | مقتطف الكود |
|------|-----------|--------------|
| عملة (منزلتين عشريتين) | 5 | `cellA1.SetStyle(new Style() { Number = 5 });` |
| نسبة مئوية (بدون كسور) | 10 | `cellA1.SetStyle(new Style() { Number = 10 });` |
| تدوين علمي | 11 | `cellA1.SetStyle(new Style() { Number = 11 });` |

إذا لم يتطابق أي من المعرفات المدمجة مع احتياجاتك، عُد إلى سلسلة مخصصة كما هو موضح سابقًا.

### 2. فواصل عشرية حسب الثقافة

بعض اللغات تستخدم الفواصل بدلاً من النقاط للكسور العشرية. يمكنك فرض تنسيق واعٍ للثقافة:

```csharp
Style cultureStyle = workbook.CreateStyle();
cultureStyle.Custom = "#,##0.00"; // works for most European locales
cellA1.SetStyle(cultureStyle);
```

### 3. كتابة نص بدلاً من أرقام

عندما تحتاج إلى **كيفية كتابة خلية** بسلسلة نصية، ما عليك سوى تمرير النص إلى `PutValue`:

```csharp
cellA1.PutValue("Total Revenue");
```

لا يلزم تنسيق رقم، لكن لا يزال بإمكانك تطبيق تنسيق الخط.

### 4. مجموعات بيانات ضخمة

إذا كنت تملأ آلاف الصفوف، فإن الإدخال على دفعات (`Cells.ImportArray`) أسرع من حلقة `PutValue`. يبقى نهج التنسيق كما هو؛ فقط طبق النمط على نطاق:

```csharp
Range range = workbook.Worksheets[0].Cells.CreateRange("B2:B1001");
range.ApplyStyle(new Style() { Number = 2 });
```

---

## الأسئلة المتكررة

**س: هل يعمل هذا مع .NET Core؟**  
ج: بالتأكيد. يدعم Aspose.Cells .NET Standard 2.0 وما بعده، لذا يمكنك استهداف .NET 5 أو .NET 6 أو .NET 7 دون تغييرات.

**س: ماذا لو احتجت أكثر من منزلتين عشريتين؟**  
ج: غيّر خاصية `Number` إلى المعرف المدمج المناسب (مثلاً `3` لثلاث منازل عشرية) أو عدّل سلسلة التنسيق المخصصة (`"#,##0.000"`).

**س: هل يمكنني تطبيق التنسيق على عمود كامل مرة واحدة؟**  
ج: نعم. استخدم `Cells["A:A"]` للحصول على العمود بالكامل ثم `SetStyle`.

---

## الخلاصة

أنت الآن تعرف **كيفية إنشاء دفتر عمل** في C#، **كتابة قيمة إلى خلية**، و**ضبط تنسيق رقم الخلية** بحيث تظهر الأرقام بالضبط كما تريد. من خلال إتقان هذه الأساسيات، ستكون قادرًا على توليد تقارير Excel احترافية، فواتير، أو تصدير بيانات بجهد قليل.

في الخطوة التالية، قد تستكشف **تنسيق رقم الخلية** للتواريخ أو النسب المئوية أو التنسيق الشرطي—كل منها يبني على المبادئ التي غطيناها. استعرض وثائق Aspose.Cells لمزيد من خيارات التنسيق المتقدمة، أو جرّب دمج أوراق عمل متعددة في دفتر واحد لتقارير أكثر غنى.

برمجة سعيدة، وتذكر: جدول بيانات منسق جيدًا هو مجرد

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}