---
category: general
date: 2026-02-15
description: كيفية نسخ الخط وتطبيق نمط الخلية في C# مع مثال بسيط. تعلم كيفية الحصول
  على نمط الخلية واستخدام تنسيق الخلية لتعيين حجم خط مربع النص.
draft: false
keywords:
- how to copy font
- apply cell style
- get cell style
- use cell formatting
- set textbox font size
language: ar
og_description: كيفية نسخ الخط من خلية في ورقة العمل وتطبيق نمط الخلية على مربع نص.
  يوضح هذا الدليل كيفية الحصول على نمط الخلية، واستخدام تنسيق الخلية، وتعيين حجم خط
  مربع النص.
og_title: كيفية نسخ الخط من خلية إكسل – دليل C# الكامل
tags:
- C#
- EPPlus
- UI‑grid
- Excel‑interop
title: كيفية نسخ الخط من خلية إكسل إلى مربع النص – دليل خطوة بخطوة
url: /ar/net/working-with-fonts-in-excel/how-to-copy-font-from-an-excel-cell-to-a-textbox-step-by-ste/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية نسخ الخط من خلية Excel إلى TextBox – دليل C# الكامل

هل احتجت يومًا إلى **نسخ الخط** من خلية جدول بيانات وجعل مربع النص في الواجهة يبدو تمامًا نفسه؟ لست الوحيد. في العديد من أدوات التقارير أو لوحات التحكم المخصصة، ستجد نفسك تستخرج البيانات من Excel ثم تحاول الحفاظ على الدقة البصرية — عائلة الخط، الحجم، واللون — دون تغيير.  

الخبر السار هو أنه ببضع أسطر من C# يمكنك **الحصول على نمط الخلية**، قراءة خصائص الخط الخاصة بها، و**تطبيق نمط الخلية** على أي عنصر تحكم من نوع text‑box. في هذا الدليل سنستعرض مثالًا كاملاً قابلاً للتنفيذ يوضح كيفية **استخدام تنسيق الخلية** وحتى **تعيين حجم خط textbox** برمجيًا.

---

## ما ستتعلمه

- كيفية استرجاع كائن `TextBox` من مكوّن الشبكة (`gridJs` في مثالنا)
- كيفية قراءة عائلة الخط، الحجم، واللون من خلية Excel محددة (`B2`)
- كيفية نسخ تلك الخصائص الخطية إلى مربع النص بحيث يعكس الواجهة جدول البيانات
- المشكلات الشائعة (مثل تحويل اللون) وبعض **النصائح الاحترافية** للحفاظ على صلابة الكود
- مقتطف كود جاهز للتنفيذ يمكنك إدراجه في تطبيق console أو مشروع WinForms

**المتطلبات المسبقة**  
يجب أن تكون لديك:

1. .NET 6+ (أو .NET Framework 4.8) مثبت  
2. حزمة EPPlus من NuGet (للتعامل مع Excel)  
3. عنصر تحكم شبكة يعرض قاموس `TextBoxes` (المثال يستخدم `gridJs` الوهمي لكن الفكرة تعمل مع أي مكتبة واجهة مستخدم)

الآن، دعنا نتعمق.

---

## الخطوة 1: إعداد المشروع وتحميل ورقة العمل

أولاً، أنشئ مشروع console أو WinForms جديد وأضف EPPlus:

```bash
dotnet add package EPPlus --version 6.*
```

بعد ذلك، حمّل المصنف واحصل على الخلية التي تريد نسخ نمطها.

```csharp
using OfficeOpenXml;
using OfficeOpenXml.Style;
using System.Drawing;

// ...

// Load the Excel file (make sure the file exists at the given path)
var fileInfo = new FileInfo(@"C:\Data\Sample.xlsx");
using var package = new ExcelPackage(fileInfo);
ExcelWorksheet ws = package.Workbook.Worksheets["Sheet1"]; // adjust sheet name if needed

// Retrieve the style of cell B2
ExcelStyle cellStyle = ws.Cells["B2"].Style;
```

**لماذا هذا مهم:** توفر لك EPPlus وصولًا مباشرًا إلى كائن `Style`، الذي يحتوي على كائن فرعي `Font`. من هناك يمكنك قراءة `Name`، `Size`، و`Color`. هذا هو جوهر عملية **الحصول على نمط الخلية**.

---

## الخطوة 2: الحصول على TextBox الهدف من الشبكة الخاصة بك

بافتراض أن شبكة الواجهة (`gridJs`) تخزن مربعات النص في قاموس مفتاحه هو اسم العمود، يمكنك استرجاع العنصر المطلوب كما يلي:

```csharp
// Fake grid class for illustration – replace with your actual grid component
var gridJs = new MyGrid(); // MyGrid is a placeholder for your UI control

// Step 1: Retrieve the "Notes" text box from the grid
var notesTextBox = gridJs.TextBoxes["Notes"];
```

إذا كنت تستخدم WinForms، قد يكون `notesTextBox` عنصر تحكم `TextBox`؛ بالنسبة لـ WPF قد يكون عنصر `TextBox`، ولشبكة ويب قد يكون كائن تفاعل JavaScript. النقطة الأساسية هي أن لديك مرجعًا يمكنك التلاعب به.

---

## الخطوة 3: نقل عائلة الخط

الآن بعد أن لدينا كل من نمط المصدر وعنصر التحكم الوجهة، نقوم بنسخ عائلة الخط.

```csharp
// Apply the cell's font family to the text box
notesTextBox.FontFamily = cellStyle.Font.Name;
```

**نصيحة احترافية:** ليست كل أطر الواجهة تعرض خاصية `FontFamily` التي تقبل سلسلة نصية عادية. في WinForms ستقوم بتعيين `notesTextBox.Font = new Font(cellStyle.Font.Name, notesTextBox.Font.Size);`. عدّل وفقًا لذلك.

---

## الخطوة 4: نقل حجم الخط

يتم تخزين حجم الخط كقيمة `float` في EPPlus. قم بتطبيقه مباشرةً:

```csharp
// Apply the cell's font size to the text box
notesTextBox.FontSize = cellStyle.Font.Size;
```

إذا كان عنصر التحكم يستخدم النقاط (كما هو شائع)، يمكنك تعيين القيمة دون تحويل. بالنسبة للشبكات المعتمدة على CSS قد تحتاج إلى إلحاق `"pt"`.

---

## الخطوة 5: نقل لون الخط

تحويل اللون هو الجزء الأصعب لأن EPPlus يخزن الألوان كأعداد صحيحة ARGB، بينما العديد من أطر الواجهة تتوقع `System.Drawing.Color` أو سلسلة HEX للـ CSS.

```csharp
// Apply the cell's font colour to the text box
// EPPlus stores colour as a System.Drawing.Color when using .Color property
var excelColor = cellStyle.Font.Color?.GetColor();

// Fallback to black if the cell has no explicit colour
var safeColor = excelColor ?? Color.Black;

// Convert to the format your UI expects (example for WinForms)
notesTextBox.FontColor = safeColor;
```

> **لماذا هذا يعمل:** تقوم `GetColor()` بحل الألوان المعتمدة على السمة وتعيد `System.Drawing.Color` ملموسًا. إذا كانت الخلية تستخدم اللون الافتراضي (بدون إعداد صريح)، نعيد اللون الأسود لتجنب استثناءات الإشارة إلى null.

---

## مثال كامل يعمل

بجمع كل شيء معًا، إليك تطبيق console بسيط يقرأ ملف Excel، يستخرج الخط من **B2**، ويطبقه على مربع نص تجريبي.

```csharp
using OfficeOpenXml;
using OfficeOpenXml.Style;
using System;
using System.Collections.Generic;
using System.Drawing;

namespace FontCopyDemo
{
    // Mock grid control – replace with your real UI component
    public class MyGrid
    {
        public Dictionary<string, TextBoxMock> TextBoxes { get; } = new()
        {
            { "Notes", new TextBoxMock() }
        };
    }

    // Simple text box representation for demonstration
    public class TextBoxMock
    {
        public string FontFamily { get; set; }
        public float FontSize { get; set; }
        public Color FontColor { get; set; }

        public override string ToString()
        {
            return $"FontFamily: {FontFamily}, FontSize: {FontSize}, FontColor: {FontColor.Name}";
        }
    }

    class Program
    {
        static void Main()
        {
            // 1️⃣ Load Excel worksheet
            var fileInfo = new FileInfo(@"C:\Data\Sample.xlsx");
            using var package = new ExcelPackage(fileInfo);
            var ws = package.Workbook.Worksheets["Sheet1"];
            var cellStyle = ws.Cells["B2"].Style;

            // 2️⃣ Grab the target TextBox from the grid
            var gridJs = new MyGrid();
            var notesTextBox = gridJs.TextBoxes["Notes"];

            // 3️⃣ Apply font family
            notesTextBox.FontFamily = cellStyle.Font.Name;

            // 4️⃣ Apply font size
            notesTextBox.FontSize = cellStyle.Font.Size;

            // 5️⃣ Apply font colour (with safety net)
            var excelColor = cellStyle.Font.Color?.GetColor();
            notesTextBox.FontColor = excelColor ?? Color.Black;

            // Output the result for verification
            Console.WriteLine("TextBox after copying font:");
            Console.WriteLine(notesTextBox);
        }
    }
}
```

**الناتج المتوقع (بافتراض أن B2 يستخدم Arial، 12 pt، أزرق):**

```
TextBox after copying font:
FontFamily: Arial, FontSize: 12, FontColor: Blue
```

شغّل البرنامج، افتح واجهتك، وسترى أن مربع النص “Notes” الآن يعكس نمط الخط الدقيق للخلية **B2**. لا حاجة لتعديل يدوي.

---

## الأسئلة المتكررة والحالات الخاصة

### ماذا لو استخدمت الخلية لونًا من السمة بدلاً من قيمة RGB صريحة؟

تقوم `GetColor()` في EPPlus تلقائيًا بحل ألوان السمة إلى `System.Drawing.Color` ملموس. ومع ذلك، إذا كنت تستخدم مكتبة أقدم تُعيد فقط فهرس السمة، سيتعين عليك ربط ذلك الفهرس بلوحة ألوان بنفسك.

### هل يمكنني نسخ خصائص نمط أخرى (مثل الغامق، المائل)؟

بالطبع. كائن `ExcelStyle.Font` يعرض أيضًا `Bold`، `Italic`، `Underline`، و`Strike`. فقط عيّن الخصائص المقابلة على عنصر التحكم في الواجهة:

```csharp
notesTextBox.FontBold = cellStyle.Font.Bold;
notesTextBox.FontItalic = cellStyle.Font.Italic;
```

### ماذا لو لم يكن عنصر التحكم في الشبكة يعرض خاصية `FontColor`؟

معظم أطر الواجهة الحديثة تدعم ذلك، ولكن إذا كان إطارك يقبل فقط سلسلة CSS، حوّل `Color` إلى صيغة HEX:

```csharp
string hex = $"#{notesTextBox.FontColor.R:X2}{notesTextBox.FontColor.G:X2}{notesTextBox.FontColor.B:X2}";
notesTextBox.Style["color"] = hex; // for web‑based grids
```

### كيف يمكنني معالجة خلايا متعددة في آن واحد؟

قم بالتكرار على النطاق المطلوب، احصل على نمط كل خلية، وطبقه على مربع النص المقابل. تذكر تخزين كائنات النمط مؤقتًا إذا كنت تعالج العديد من الصفوف لتجنب تدهور الأداء.

---

## نصائح احترافية ومشكلات شائعة

- **Cache the ExcelPackage** – فتح وإغلاق الملف لكل خلية مكلف. حمّل المصنف مرة واحدة، ثم أعد استخدام كائن `ExcelWorksheet`.
- **Watch out for null colours** – الخلية التي ترث اللون الافتراضي تُعيد `null`. قدم دائمًا قيمة بديلة (أسود أو اللون الافتراضي للعنصر).
- **Mind DPI scaling** – إذا كنت تستهدف شاشات عالية الـ DPI، قد يظهر حجم الخط أكبر قليلاً. عدّل باستخدام `Graphics.DpiX` إذا لزم الأمر.
- **Thread safety** – EPPlus غير آمن للـ multithreading. إذا كنت تعالج أوراقًا متعددة بالتوازي، أنشئ `ExcelPackage` منفصل لكل خيط.

---

## الخلاصة

أنت الآن تعرف **كيفية نسخ الخط** من خلية Excel و**تطبيق نمط الخلية** على أي عنصر تحكم من نوع text‑box باستخدام C#. من خلال استرجاع `Style` الخلية، استخراج خصائص `Font` الخاصة بها، وتعيينها إلى عنصر الواجهة، تحافظ على التناسق البصري دون الحاجة إلى نسخ يدوي.

الحل الكامل — تحميل المصنف، الحصول على نمط الخلية، وتعيين عائلة الخط، الحجم، واللون لمربع النص — يغطي جوهر **استخدام تنسيق الخلية** ويظهر كيفية **تعيين حجم خط textbox** بشكل صحيح.

بعد ذلك، حاول توسيع المثال لنسخ ألوان الخلفية، الحدود، أو حتى محتويات الخلية بالكامل. إذا كنت تعمل مع مكتبة data‑grid تدعم عرض خلايا غني، يمكنك الآن تزويدها بنفس معلومات التنسيق التي استخرجتها من Excel، مما يحافظ على تزامن واجهتك وتقاريرك بشكل مثالي.

هل لديك أسئلة أخرى؟ اترك تعليقًا أو استكشف المواضيع ذات الصلة مثل “ربط Excel‑إلى‑الواجهة الديناميكي” و“تحويل اللون مع مراعاة السمة”. برمجة سعيدة!

![مثال على نسخ الخط](placeholder-image.jpg "كيفية نسخ الخط من خلية Excel إلى TextBox")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}