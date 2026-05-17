---
category: general
date: 2026-02-21
description: إنشاء نمط خلية في C# بسرعة. تعلم كيفية تطبيق النمط على خلية، توسيط النص
  في الخلية، ضبط محاذاة الخلية، وإتقان تنسيق الخلية.
draft: false
keywords:
- create cell style
- apply style to cell
- center text in cell
- set cell alignment
- how to center text
language: ar
og_description: أنشئ نمط خلية في C# وتعلم كيفية تطبيق النمط على خلية، وتوسيط النص
  داخل الخلية، وتعيين محاذاة الخلية من خلال دليل واضح خطوة بخطوة.
og_title: إنشاء نمط خلية في C# – تطبيق النمط على خلية وتوسيط النص
tags:
- C#
- Aspose.Cells
- Excel automation
title: إنشاء نمط خلية في C# – كيفية تطبيق النمط على خلية وتوسيط النص
url: /ar/net/excel-formatting-and-styling/create-cell-style-in-c-how-to-apply-style-to-a-cell-and-cent/
---

يط النص"

Proceed.

Translate bullet points.

Also note the "Prerequisite:" line.

Translate "Step 1: Set Up Your Project and Import Namespaces" etc.

Make sure to keep code block placeholders.

Also translate the alt text for image.

Let's craft.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء نمط خلية في C# – دليل شامل لتطبيق الأنماط وتوسيط النص

هل احتجت يومًا إلى **إنشاء نمط خلية** في ورقة Excel ولكنك لم تكن متأكدًا من أين تبدأ؟ لست وحدك. في العديد من مشاريع الأتمتة، القدرة على **تطبيق نمط على خلية** هي الفارق بين جدول بيانات بسيط وتقرير مصقول.  

في هذا الدرس سنستعرض مثالًا كاملاً قابلاً للتنفيذ يوضح لك **كيفية توسيط النص** داخل خلية، وضبط المحاذاة، وإضافة حد رفيع—كل ذلك في بضع أسطر من C#. بنهاية الدرس ستعرف بالضبط لماذا كل جزء مهم وكيفية تعديلها لتناسب سيناريوهاتك الخاصة.

## ما ستستفيده

- فهم واضح لتدفق عمل **إنشاء نمط خلية** باستخدام Aspose.Cells (أو أي مكتبة مشابهة).
- الكود الدقيق الذي يمكنك نسخه‑ولصقه في تطبيق Console لت **تطبيق نمط على خلية**.
- نظرة عميقة على **توسيط النص في خلية**، **ضبط محاذاة الخلية**، ومعالجة الحالات الخاصة مثل الخلايا المدمجة أو تنسيقات الأرقام المخصصة.
- نصائح لتوسيع النمط—خطوط مختلفة، ألوان خلفية، أو تنسيق شرطي.

> **المتطلبات المسبقة:** Visual Studio 2022 (أو أي بيئة تطوير C#) وحزمة NuGet الخاصة بـ Aspose.Cells for .NET. لا توجد تبعيات أخرى مطلوبة.

---

## الخطوة 1: إعداد المشروع واستيراد المساحات الاسم

قبل أن نتمكن من **إنشاء نمط خلية**، نحتاج إلى مشروع يضم مكتبة Excel.

```csharp
// Program.cs – entry point
using System;
using Aspose.Cells;   // Make sure the Aspose.Cells NuGet package is installed

class Program
{
    static void Main()
    {
        // We'll fill in the rest of the steps here.
    }
}
```

*لماذا هذا مهم:* استيراد `Aspose.Cells` يتيح لنا الوصول إلى الفئات `Workbook`، `Worksheet`، `Style`، و `Border`. إذا كنت تستخدم مكتبة مختلفة (مثل EPPlus)، ستتغير أسماء الفئات لكن المفهوم يبقى نفسه.

---

## الخطوة 2: إنشاء مصنف والحصول على الخلية الأولى

الآن **ننشئ نمط خلية** أولاً بالحصول على مرجع للخلية التي نريد تنسيقها.

```csharp
// Inside Main()
Workbook workbook = new Workbook();           // New, empty workbook
Worksheet ws = workbook.Worksheets[0];        // First worksheet (index 0)

// Step 1: Get a reference to the first cell (row 0, column 0) in the worksheet
Cell firstCell = ws.Cells[0, 0];               // A1 in Excel terms
firstCell.PutValue("Hello, styled world!");
```

لاحظ أننا استخدمنا `Cell` بدلاً من `var` العام—الكتابة الصريحة تجعل الكود أوضح للمبتدئين. استدعاء `PutValue` يكتب سلسلة نصية حتى نتمكن من رؤية تأثير النمط لاحقًا.

---

## الخطوة 3: تعريف النمط – توسيط النص، إضافة حد رفيع

هذا هو جوهر عملية **إنشاء نمط خلية**. سنضبط محاذاة أفقية، حد رفيع، وبعض التحسينات الاختيارية.

```csharp
// Step 2: Define a style that centers the text and adds a thin border
Style cellStyle = workbook.CreateStyle();          // Create a fresh Style object
cellStyle.HorizontalAlignment = TextAlignmentType.Center; // Center text horizontally
cellStyle.VerticalAlignment = TextAlignmentType.Center;   // Center vertically – often forgotten
cellStyle.Borders[BorderType.TopBorder].LineStyle = CellBorderType.Thin;
cellStyle.Borders[BorderType.BottomBorder].LineStyle = CellBorderType.Thin;
cellStyle.Borders[BorderType.LeftBorder].LineStyle = CellBorderType.Thin;
cellStyle.Borders[BorderType.RightBorder].LineStyle = CellBorderType.Thin;

// Optional: set a light gray background to make the border pop
cellStyle.ForegroundColor = System.Drawing.Color.LightGray;
cellStyle.Pattern = BackgroundType.Solid;
```

*لماذا نفعل ذلك:*  
- **HorizontalAlignment** و **VerticalAlignment** معًا يجيبان على سؤال “**كيف يتم توسيط النص** في خلية؟”.  
- إضافة جميع الحدود الأربعة يضمن أن الخلية تبدو كملصق محاط، وهو مفيد للعناوين.  
- لون الخلفية ليس ضروريًا، لكنه يوضح كيف يمكنك توسيع النمط لاحقًا.

---

## الخطوة 4: تطبيق النمط المعرف على الخلية المختارة

الآن بعد أن أصبح النمط موجودًا، **نطبق النمط على الخلية** باستدعاء طريقة واحدة.

```csharp
// Step 3: Apply the defined style to the selected cell
firstCell.SetStyle(cellStyle);
```

هذا كل شيء—Aspose.Cells يتولى نسخ النمط إلى مجموعة الأنماط الداخلية للخلية. إذا احتجت نفس التنسيق لنطاق، يمكنك استخدام `ws.Cells.CreateRange("A1:D1").ApplyStyle(cellStyle, new StyleFlag { All = true });`.

---

## الخطوة 5: حفظ المصنف والتحقق من النتيجة

حفظ سريع يتيح لك فتح الملف في Excel والتأكد من أن النص مُوسَّط فعليًا وأن الحد ظاهر.

```csharp
// Save the workbook to disk
string outputPath = "StyledCell.xlsx";
workbook.Save(outputPath, SaveFormat.Xlsx);
Console.WriteLine($"Workbook saved to {outputPath}. Open it to see the styled cell.");
```

*الناتج المتوقع:* عند فتح **StyledCell.xlsx**، تحتوي الخلية **A1** على النص “Hello, styled world!” مُوسَّط أفقيًا وعموديًا، محاط بحد رمادي رفيع، وخلفية رمادية فاتحة.

---

## الاختلافات الشائعة والحالات الخاصة

### 1. توسيط النص في منطقة مدمجة

إذا دمجت الخلايا **A1:C1** ولا تزال تريد توسيط النص، يجب تطبيق النمط على الخلية العلوية‑اليسرى **بعد** الدمج:

```csharp
ws.Cells.Merge(0, 0, 1, 3); // Merge A1:C1
firstCell.SetStyle(cellStyle); // Style still works because it’s applied to the anchor cell
```

### 2. استخدام تنسيق رقمي

أحيانًا تحتاج إلى **ضبط محاذاة الخلية** *وعرض الأرقام* بتنسيق معين:

```csharp
cellStyle.Custom = "#,##0.00"; // Two decimal places
firstCell.PutValue(12345.678);
firstCell.SetStyle(cellStyle);
```

تظل المحاذاة مُوسَّطة بينما يظهر الرقم كـ `12,345.68`.

### 3. إعادة استخدام الأنماط بفعالية

إنشاء `Style` جديد لكل خلية قد يؤثر سلبًا على الأداء. بدلاً من ذلك، أنشئ كائن نمط واحد وأعد استخدامه عبر خلايا أو نطاقات متعددة. تسمح لك فئة `StyleFlag` بتطبيق الأجزاء التي تهمك فقط، مما يوفر الذاكرة.

```csharp
StyleFlag flag = new StyleFlag { HorizontalAlignment = true, Borders = true };
ws.Cells.CreateRange("B2:B10").ApplyStyle(cellStyle, flag);
```

---

## نصائح احترافية ومخاطر يجب الانتباه لها

- **لا تنس المحاذاة العمودية** – التوسيط الأفقي فقط غالبًا ما يبدو غير متوازن، خاصةً مع الصفوف العالية.
- **أنواع الحدود**: `CellBorderType.Thin` يناسب معظم التقارير، لكن يمكنك التحويل إلى `Medium` أو `Dashed` لإضفاء تسلسل بصري.
- **معالجة الألوان**: عند استهداف .NET Core، استخدم `System.Drawing.Color` من حزمة `System.Drawing.Common`؛ وإلا ستواجه خطأً أثناء التشغيل.
- **صيغة الحفظ**: إذا كنت تحتاج توافقًا مع إصدارات Excel القديمة، غيّر `SaveFormat.Xlsx` إلى `SaveFormat.Xls`.

---

![Create cell style example](https://example.com/images/create-cell-style.png "Create cell style in C#")

*نص بديل: لقطة شاشة تُظهر خلية بنص مُوسَّط وحد رفيع تم إنشاؤها بواسطة دليل إنشاء نمط خلية.*

---

## مثال كامل جاهز للنسخ واللصق

```csharp
using System;
using Aspose.Cells;
using System.Drawing; // For Color

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize workbook and worksheet
        Workbook workbook = new Workbook();
        Worksheet ws = workbook.Worksheets[0];

        // 2️⃣ Grab the first cell and put a sample value
        Cell firstCell = ws.Cells[0, 0];
        firstCell.PutValue("Hello, styled world!");

        // 3️⃣ Create the style: center text, thin border, light gray background
        Style cellStyle = workbook.CreateStyle();
        cellStyle.HorizontalAlignment = TextAlignmentType.Center;
        cellStyle.VerticalAlignment   = TextAlignmentType.Center;
        cellStyle.Borders[BorderType.TopBorder].LineStyle    = CellBorderType.Thin;
        cellStyle.Borders[BorderType.BottomBorder].LineStyle = CellBorderType.Thin;
        cellStyle.Borders[BorderType.LeftBorder].LineStyle   = CellBorderType.Thin;
        cellStyle.Borders[BorderType.RightBorder].LineStyle  = CellBorderType.Thin;
        cellStyle.ForegroundColor = Color.LightGray;
        cellStyle.Pattern = BackgroundType.Solid;

        // 4️⃣ Apply the style to the cell
        firstCell.SetStyle(cellStyle);

        // 5️⃣ Save the result
        string outputPath = "StyledCell.xlsx";
        workbook.Save(outputPath, SaveFormat.Xlsx);
        Console.WriteLine($"Workbook saved to {outputPath}. Open it to see the styled cell.");
    }
}
```

شغّل هذا البرنامج، افتح **StyledCell.xlsx**، وسترى النتيجة الدقيقة التي تم وصفها سابقًا. لا تتردد في تغيير النص، نمط الحد، أو لون الخلفية لتتناسب مع هوية علامتك التجارية.

---

## الخلاصة

لقد **أنشأنا نمط خلية** من الصفر، **طبقنا النمط على خلية**، وأظهرنا **كيفية توسيط النص** أفقيًا وعموديًا. من خلال إتقان هذه اللبنات الأساسية يمكنك الآن تنسيق العناوين، إبراز الإجماليات، أو بناء قوالب تقارير كاملة دون مغادرة C#.  

إذا كنت ترغب في الخطوات التالية، جرّب:

- **تطبيق نفس النمط على صف كامل** (`ws.Cells.CreateRange("A2:E2").ApplyStyle(cellStyle, new StyleFlag { All = true });`).
- **إضافة تنسيق شرطي** لتغيير الخلفية بناءً على قيم الخلية.
- **التصدير إلى PDF** مع الحفاظ على النمط.

تذكر، التنسيق يتعلق بوضوح القراءة بقدر ما يتعلق بالجماليات. جرب، عدّل، وسرعان ما ستصبح جداولك تبدو احترافية كما هو كودك.

*برمجة سعيدة!*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}