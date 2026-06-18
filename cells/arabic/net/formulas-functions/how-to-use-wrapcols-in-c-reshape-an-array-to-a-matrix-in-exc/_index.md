---
category: general
date: 2026-06-17
description: كيفية استخدام WRAPCOLS في C# لإعادة تشكيل مصفوفة إلى مصفوفة (ماتريكس)،
  كتابة صيغة مصفوفة إلى خلية، وتحميل ملفات Excel الموجودة باستخدام Aspose.Cells.
draft: false
keywords:
- how to use wrapcols
- reshape array to matrix
- write array formula
- write formula to cell
- load existing excel
language: ar
og_description: كيفية استخدام WRAPCOLS في C# لإعادة تشكيل مصفوفة إلى مصفوفة (ماتريكس)
  بسرعة، كتابة صيغة مصفوفة في خلية، والعمل مع ملفات Excel الموجودة.
og_title: كيفية استخدام WRAPCOLS في C# – إعادة تشكيل مصفوفة إلى مصفوفة
schemas:
- author: Aspose
  dateModified: '2026-06-17'
  description: How to use WRAPCOLS in C# to reshape an array to a matrix, write array
    formula to a cell, and load existing Excel files with Aspose.Cells.
  headline: How to Use WRAPCOLS in C# – Reshape an Array to a Matrix in Excel
  type: TechArticle
- description: How to use WRAPCOLS in C# to reshape an array to a matrix, write array
    formula to a cell, and load existing Excel files with Aspose.Cells.
  name: How to Use WRAPCOLS in C# – Reshape an Array to a Matrix in Excel
  steps:
  - name: 'Optional: Write a Dynamic Array Reference'
    text: 'If you prefer to reference a range instead of a hard‑coded list, you can
      use:'
  - name: 1. What if I need a different number of rows?
    text: '`WRAPCOLS` only takes the column count; the row count is inferred. To force
      a specific row count, you can combine it with `WRAPROWS` or pad the source array
      with empty strings.'
  - name: 2. Does WRAPCOLS work with text values?
    text: 'Absolutely. Replace the numbers with quoted strings:'
  - name: 3. Can I apply formatting to the generated matrix?
    text: 'After calculation, you can style the range programmatically:'
  - name: 4. How do I handle very large arrays?
    text: Aspose.Cells can process tens of thousands of elements, but keep an eye
      on memory. If you hit limits, consider writing the data in chunks or using `Workbook.Settings.MemorySetting
      = MemorySetting.MemoryPreference;`.
  type: HowTo
tags:
- excel
- csharp
- aspose.cells
title: كيفية استخدام WRAPCOLS في C# – إعادة تشكيل مصفوفة إلى مصفوفة في Excel
url: /ar/net/formulas-functions/how-to-use-wrapcols-in-c-reshape-an-array-to-a-matrix-in-exc/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيف تستخدم WRAPCOLS في C# – تحويل مصفوفة إلى مصفوفة ثنائية الأبعاد في Excel

هل تساءلت يومًا **كيف تستخدم WRAPCOLS** لتحويل قائمة مسطحة من الأرقام إلى جدول مرتب داخل Excel؟ لست وحدك. سواء كنت تبني أداة تقارير أو تلعب فقط بالبيانات، فإن تحويل مصفوفة إلى مصفوفة ثنائية الأبعاد يمكن أن يوفر لك الكثير من النسخ واللصق اليدوي.

في هذا الدرس سنستعرض مثالًا كاملًا قابلًا للتنفيذ يوضح لك كيفية **كتابة صيغة مصفوفة إلى خلية**، حساب النتيجة، وحتى **تحميل ملف Excel** موجود إذا احتجت. في النهاية ستحصل على مقتطف جاهز للنسخ واللصق يعمل مع أحدث نسخة من Aspose.Cells لـ .NET.

## ما ستتعلمه

- هدف دالة `WRAPCOLS` ومتى تكون مفيدة.  
- كيفية **تحويل مصفوفة إلى مصفوفة ثنائية الأبعاد** باستخدام صيغة واحدة.  
- كود خطوة بخطوة **للكتابة صيغة إلى خلية** وإجبار الحساب.  
- تقنيات اختيارية **لتحميل ملف Excel** موجود قبل تطبيق الصيغة.  
- الأخطاء الشائعة ونصائح لتوسيع النهج إلى مجموعات بيانات أكبر.

لا حاجة لأي وثائق خارجية—كل ما تحتاجه هنا.

## المتطلبات المسبقة

- .NET 6.0 أو أحدث (الكود يعمل أيضًا على .NET Framework 4.7+).  
- Aspose.Cells لـ .NET مثبت (`dotnet add package Aspose.Cells`).  
- فهم أساسي لصياغة C#؛ إذا كنت مرتاحًا لإنشاء تطبيق Console، فأنت جاهز.

> **نصيحة احترافية:** إذا كنت تستخدم Visual Studio، فعّل *nullable reference types* (`<Nullable>enable</Nullable>`) لتكتشف أخطاء الـ null مبكرًا.

## الخطوة 1: إعداد المشروع واستيراد المساحات الاسمية

أولًا، أنشئ مشروع Console جديد (أو ضع الكود في مشروع موجود). ثم أضف توجيهات `using` اللازمة حتى يعرف المترجم مكان وجود `Workbook` و `Worksheet`.

```csharp
using System;
using Aspose.Cells;   // Main library for Excel manipulation

namespace WrapColsDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // We'll fill in the logic in the next steps
        }
    }
}
```

> **لماذا هذا مهم:** استيراد `Aspose.Cells` يمنحك الوصول إلى محرك Excel عالي الأداء الذي يقيم `WRAPCOLS` دون الحاجة إلى تثبيت Excel على الجهاز.

## الخطوة 2: إنشاء أو تحميل دفتر عمل

يمكنك البدء من الصفر أو فتح ملف موجود. المقتطف التالي يوضح الخيارين؛ فقط علق (comment) الجزء الذي لا تحتاجه.

```csharp
// Option A – Create a brand‑new workbook
Workbook workbook = new Workbook();   // starts with a single empty worksheet

// Option B – Load an existing Excel file (useful when you have templates)
// string inputPath = @"C:\Data\input.xlsx";
// Workbook workbook = new Workbook(inputPath);
```

> **حالة خاصة:** إذا كان الملف الذي تحمّله محميًا بكلمة مرور، مرّر كلمة المرور كوسيط ثاني: `new Workbook(path, "password")`.

## الخطوة 3: الحصول على ورقة العمل المستهدفة

في معظم الأحيان الورقة الأولى (`Worksheets[0]`) هي ما تريد، لكن يمكنك أيضًا الإشارة إلى ورقة بالاسم.

```csharp
Worksheet sheet = workbook.Worksheets[0];               // by index
// Worksheet sheet = workbook.Worksheets["DataSheet"]; // by name (if it exists)
```

## الخطوة 4: كتابة صيغة WRAPCOLS إلى خلية

هذا هو جوهر الدرس. `WRAPCOLS` تأخذ مصفوفة وعدد الأعمدة، ثم توزع القيم صفًا بصف. سنضع الصيغة في **A1** بحيث يبدأ المصفوفة من الزاوية العليا اليسرى.

```csharp
// Write the WRAPCOLS formula that turns {1,2,3,4,5,6} into 2 rows × 3 columns
sheet.Cells["A1"].Formula = "=WRAPCOLS({1,2,3,4,5,6},3)";
```

> **ما الذي يحدث؟**  
> - بناء القوسين `{1,2,3,4,5,6}` ينشئ ثابت مصفوفة مضمن.  
> - الوسيط الثاني (`3`) يخبر Excel بإنشاء ثلاثة أعمدة، مع تغليف العناصر المتبقية تلقائيًا إلى صفوف جديدة.  
> - لأننا نستخدم Aspose.Cells، تُخزن الصيغة تمامًا كما تكتبها في Excel، وسيقوم المحرك بتقييمها عند الطلب.

### اختياري: كتابة مرجع مصفوفة ديناميكي

إذا كنت تفضّل الإشارة إلى نطاق بدلاً من قائمة ثابتة، يمكنك استخدام:

```csharp
// Assume B1:B6 already contains numbers you want to reshape
sheet.Cells["A1"].Formula = "=WRAPCOLS(B1:B6,3)";
```

بهذه الطريقة يتم تحديث المصفوفة تلقائيًا كلما تغير النطاق المصدر.

## الخطوة 5: إجبار الحساب وحفظ النتيجة

Aspose.Cells لا يحسب الصيغ إلا عندما تطلب ذلك. استدعاء `Calculate()` يُجسد النتيجة، محولًا مخرجات الصيغة إلى قيم خلية فعلية.

```csharp
// Force calculation so the WRAPCOLS output appears in the sheet
workbook.Calculate();

// Save the workbook – adjust the path as needed
string outputPath = @"C:\Data\output.xlsx";
workbook.Save(outputPath);
```

عند فتح `output.xlsx` في Excel، سترى:

| A | B | C |
|---|---|---|
| 1 | 2 | 3 |
| 4 | 5 | 6 |

هذا هو تأثير **تحويل مصفوفة إلى مصفوفة ثنائية الأبعاد** الذي كنت تبحث عنه.

## مثال كامل يعمل

بجمع كل الأجزاء معًا، إليك برنامج جاهز للتنفيذ:

```csharp
using System;
using Aspose.Cells;

namespace WrapColsDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Create a new workbook (or load an existing one)
            Workbook workbook = new Workbook(); // new Workbook(@"C:\Data\input.xlsx");

            // 2️⃣ Get the first worksheet
            Worksheet sheet = workbook.Worksheets[0];

            // 3️⃣ Write the WRAPCOLS formula – reshape {1..6} into 2×3
            sheet.Cells["A1"].Formula = "=WRAPCOLS({1,2,3,4,5,6},3)";

            // 4️⃣ Force calculation so the matrix is materialized
            workbook.Calculate();

            // 5️⃣ Save the result
            string outputPath = @"C:\Data\output.xlsx";
            workbook.Save(outputPath);

            Console.WriteLine($"Workbook saved to {outputPath}");
        }
    }
}
```

شغّل البرنامج، افتح `output.xlsx`، وسترى المصفوفة بالضبط كما هو موضح أعلاه.

## أسئلة شائعة ومشكلات محتملة

### 1. ماذا لو أردت عدد صفوف مختلف؟

`WRAPCOLS` يأخذ فقط عدد الأعمدة؛ عدد الصفوف يُستنتج تلقائيًا. لفرض عدد صفوف محدد، يمكنك دمجه مع `WRAPROWS` أو إضافة عناصر فارغة إلى المصفوفة المصدر.

```csharp
// Example: Force 3 rows, 2 columns (will add blanks if needed)
sheet.Cells["A1"].Formula = "=WRAPROWS({1,2,3,4,5,6},3)";
```

### 2. هل يعمل WRAPCOLS مع قيم نصية؟

بالطبع. استبدل الأرقام بسلاسل محاطة بعلامات اقتباس:

```csharp
sheet.Cells["A1"].Formula = "=WRAPCOLS({\"Jan\",\"Feb\",\"Mar\",\"Apr\",\"May\",\"Jun\"},3)";
```

### 3. هل يمكنني تطبيق تنسيق على المصفوفة المُنشأة؟

بعد الحساب، يمكنك تنسيق النطاق برمجيًا:

```csharp
Range matrix = sheet.Cells.CreateRange("A1:C2");
Style style = workbook.CreateStyle();
style.Font.Color = System.Drawing.Color.Blue;
style.Font.IsBold = true;
matrix.ApplyStyle(style, new StyleFlag() { Font = true });
```

### 4. كيف أتعامل مع مصفوفات ضخمة جدًا؟

Aspose.Cells يمكنه معالجة عشرات الآلاف من العناصر، لكن راقب استهلاك الذاكرة. إذا وصلت للحدود، فكر في كتابة البيانات على دفعات أو استخدم `Workbook.Settings.MemorySetting = MemorySetting.MemoryPreference;`.

## نصائح احترافية للكود الإنتاجي

- **احفظ مرجع الورقة** إذا كنت تكتب صيغًا متعددة داخل حلقة؛ يقلل ذلك من تكلفة البحث.  
- **عطّل الحساب التلقائي** (`workbook.Settings.CalculateFormulaOnOpen = false;`) عندما تخطط لكتابة عشرات الصيغ دفعة واحدة، ثم استدعِ `Calculate()` مرة واحدة في النهاية.  
- **غلف عمليات I/O بكتلة try/catch** لتظهر أخطاء الأذونات مبكرًا:

```csharp
try
{
    workbook.Save(outputPath);
}
catch (Exception ex)
{
    Console.Error.WriteLine($"Failed to save workbook: {ex.Message}");
}
```

- **تحقق من صحة الإدخال** قبل بناء سلسلة الصيغة—خاصة إذا كنت تجمع قيمًا يقدمها المستخدم—لتجنب صيغ غير صحيحة.

## ملخص بصري

![How to use WRAPCOLS result matrix in Excel](wrapcols-output.png "How to use WRAPCOLS in C# to reshape an array to a matrix")

*تظهر الصورة المصفوفة 2 × 3 التي ينتجها صيغة WRAPCOLS.*

## الخلاصة

غطّينا **كيفية استخدام WRAPCOLS** في C# من البداية إلى النهاية: إنشاء أو تحميل دفتر عمل، كتابة صيغة مصفوفة إلى خلية، إجبار الحساب، وحفظ النتيجة. الآن تعرف كيف **تحول مصفوفة إلى مصفوفة ثنائية الأبعاد**، **تكتب صيغة مصفوفة**، و**تحمّل ملفات Excel** موجودة—كل ذلك بضع أسطر من الكود النظيف والقابل للصيانة.

بعد ذلك، قد ترغب في استكشاف:

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة كود كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [How to Load Excel Files Efficiently Using Aspose.Cells in .NET](/cells/english/net/workbook-operations/efficient-excel-load-aspose-cells-net/)
- [How to Load and Modify Excel Files Using Aspose.Cells for .NET: A Comprehensive Guide](/cells/english/net/workbook-operations/load-modify-excel-aspose-cells-net/)
- [How to Set Language in Excel Files Using Aspose.Cells .NET for Multilingual Support](/cells/english/net/formulas-functions/specify-language-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}