---
category: general
date: 2026-06-05
description: كيفية تقريب الأرقام أثناء تحويل Excel إلى PDF باستخدام C#. تعلم تصدير
  المصنف كملف PDF، حفظ Excel كملف PDF، والحفاظ على دقة الأرقام.
draft: false
keywords:
- how to round numbers
- convert excel to pdf
- export workbook as pdf
- save excel as pdf
- convert xlsx to pdf
language: ar
og_description: كيفية تقريب الأرقام أثناء تحويل Excel إلى PDF باستخدام C#. اتبع هذا
  الدليل لتصدير المصنف كملف PDF، وحفظ Excel كملف PDF، والتحكم في تنسيق الأرقام.
og_title: كيفية تقريب الأرقام عند تحويل Excel إلى PDF – خطوة بخطوة
schemas:
- author: Aspose
  dateModified: '2026-06-05'
  description: How to round numbers while you convert Excel to PDF using C#. Learn
    to export workbook as PDF, save Excel as PDF, and preserve numeric precision.
  headline: How to Round Numbers When Converting Excel to PDF – Complete C# Guide
  type: TechArticle
- description: How to round numbers while you convert Excel to PDF using C#. Learn
    to export workbook as PDF, save Excel as PDF, and preserve numeric precision.
  name: How to Round Numbers When Converting Excel to PDF – Complete C# Guide
  steps:
  - name: '**Load the Excel workbook** – `Workbook` reads the `.xlsx` file into memory.
      No Excel installation required, which makes this ideal for server‑side automation.'
    text: '**Load the Excel workbook** – `Workbook` reads the `.xlsx` file into memory.
      No Excel installation required, which makes this ideal for server‑side automation.'
  - name: '**Configure `PdfSaveOptions`** – The `SignificantDigits` enum controls
      numeric handling:'
    text: '**Configure `PdfSaveOptions`** – The `SignificantDigits` enum controls
      numeric handling:'
  - name: '**Export workbook as PDF** – `workbook.Save` writes the PDF to disk, applying
      the rounding rules we set.'
    text: '**Export workbook as PDF** – `workbook.Save` writes the PDF to disk, applying
      the rounding rules we set.'
  - name: '**Run the program** – Verify the console prints “PDF generated successfully…”.'
    text: '**Run the program** – Verify the console prints “PDF generated successfully…”.'
  - name: '**Open `output.pdf`** – Look at numeric columns; they should respect the
      rounding you configured.'
    text: '**Open `output.pdf`** – Look at numeric columns; they should respect the
      rounding you configured.'
  - name: '**Compare with Excel** – If numbers differ, double‑check the `SignificantDigits`
      and `Precision` settings.'
    text: '**Compare with Excel** – If numbers differ, double‑check the `SignificantDigits`
      and `Precision` settings.'
  - name: '**Automated test** – For CI pipelines, you can render the PDF to an image
      (`PdfRenderer`) and run pixel‑wise comparisons, ensuring the rounding appears
      as expected.'
    text: '**Automated test** – For CI pipelines, you can render the PDF to an image
      (`PdfRenderer`) and run pixel‑wise comparisons, ensuring the rounding appears
      as expected.'
  type: HowTo
tags:
- excel
- pdf
- csharp
- aspose.cells
title: كيفية تقريب الأرقام عند تحويل Excel إلى PDF – دليل C# الكامل
url: /ar/net/conversion-to-pdf/how-to-round-numbers-when-converting-excel-to-pdf-complete-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تقريب الأرقام عند تحويل Excel إلى PDF – دليل C# الكامل

هل تساءلت يومًا **كيف يتم تقريب الأرقام** عند تحويل مصنف Excel إلى PDF؟ لست وحدك—غالبًا ما يحتاج المطورون إلى الحفاظ على الأرقام المالية مرتبة أو البيانات العلمية قابلة للقراءة، وقد يتركك التحويل الافتراضي مع جدار من الكسور العشرية غير العملية.  

في هذا الدرس سنستعرض حلًا عمليًا من البداية إلى النهاية يتيح لك **تحويل Excel إلى PDF** مع التحكم في دقة الأرقام، باستخدام Aspose.Cells لـ .NET. بنهاية الدرس ستعرف كيف **تصدير المصنف كملف PDF**، **حفظ Excel كملف PDF**، والأهم من ذلك، كيف تقرر ما إذا كانت الأرقام تبقى كما هي، تُقرب، أو تُعرض بصيغة علمية.

> **نصيحة احترافية:** نفس النهج يعمل مع سيناريوهات **convert xlsx to pdf** على أي منصة .NET—فقط أضف حزمة NuGet وستكون جاهزًا.

## المتطلبات المسبقة

قبل أن نبدأ، تأكد من وجود ما يلي:

| المتطلب | لماذا يهم |
|-------------|----------------|
| .NET 6.0 أو أحدث (أو .NET Framework 4.7+) | Aspose.Cells يدعم كلاهما؛ الإصدارات الأحدث تعطي أداءً أفضل. |
| Visual Studio 2022 (أو أي بيئة تطوير تفضلها) | مفيدة للتصحيح ورؤية ملف PDF الناتج. |
| حزمة NuGet Aspose.Cells لـ .NET (`Install-Package Aspose.Cells`) | توفر الفئات `Workbook`، `PdfSaveOptions`، وتعدادات التقريب التي سنستخدمها. |
| ملف `input.xlsx` تجريبي يحتوي على بيانات رقمية | لرؤية تأثير التقريب عمليًا. |

لا حاجة لأي تفاعل COM إضافي أو تثبيت Office—Aspose.Cells مكتبة مُدارة بالكامل.

---

## كيفية تقريب الأرقام عند تحويل Excel إلى PDF

فيما يلي جوهر الحل. نقوم بتحميل المصنف، ضبط خيارات حفظ PDF لتحديد كيفية معالجة الأرقام، وأخيرًا نكتب ملف PDF. السطر الأساسي هو الخاصية `SignificantDigits`، التي تتحكم في سلوك التقريب.

```csharp
using Aspose.Cells;
using System;

class ExcelToPdfRounded
{
    static void Main()
    {
        // Step 1: Load the Excel workbook
        // Replace YOUR_DIRECTORY with the folder that holds your file.
        Workbook workbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");

        // Step 2: Create PDF save options and set how numeric values are handled
        PdfSaveOptions pdfOptions = new PdfSaveOptions();

        // Choose your rounding strategy:
        // - Preserve : keep original values (default)
        // - Round    : round to the number of significant digits
        // - Scientific : force scientific notation
        pdfOptions.SignificantDigits = SignificantDigits.Round; // <-- change as needed

        // Optional: define how many digits you consider significant
        pdfOptions.Precision = 4; // rounds to 4 significant digits

        // Step 3: Save the workbook as a PDF using the configured options
        workbook.Save(@"YOUR_DIRECTORY\output.pdf", pdfOptions);

        Console.WriteLine("PDF generated successfully with rounding applied.");
    }
}
```

### ما يفعله الكود خطوة بخطوة

1. **تحميل مصنف Excel** – `Workbook` يقرأ ملف `.xlsx` إلى الذاكرة. لا يلزم تثبيت Excel، مما يجعله مثاليًا للأتمتة على الخادم.
2. **ضبط `PdfSaveOptions`** – تعداد `SignificantDigits` يتحكم في معالجة الأرقام:
   * `Preserve` يحافظ على كل جزء عشري كما يخزنه Excel.
   * `Round` يقتصر الأرقام على دقة يحددها المستخدم (`Precision`). هذا هو الجزء المتعلق **بكيفية تقريب الأرقام** الذي طلبته.
   * `Scientific` يفرض عرضًا بصيغة علمية، مفيد للقيم الكبيرة جدًا أو الصغيرة جدًا.
3. **تصدير المصنف كملف PDF** – `workbook.Save` يكتب ملف PDF إلى القرص، مطبقًا قواعد التقريب التي حددناها.

سيظهر ملف `output.pdf` الناتج الأرقام مقربة إلى الدقة التي حددتها، بينما يبقى تنسيق الخلايا الآخر (الخطوط، الألوان، الحدود) كما هو.

---

## الخطوة 1: تحميل مصنف Excel (convert xlsx to pdf)

تحميل المصنف سهل، لكن هناك بعض النقاط التي تستحق الذكر:

* **المسارات المطلقة مقابل النسبية** – استخدام `@"C:\Path\To\File.xlsx"` يتجنب مشاكل أحرف الهروب. إذا كنت تفضل مسارًا نسبيًا، تأكد من ضبط دليل العمل بشكل صحيح (`Directory.SetCurrentDirectory` يمكن أن يساعد).
* **الملفات الكبيرة** – للمصنفات التي يزيد حجمها عن 200 ميغابايت، فكر في استخدام `LoadOptions` مع `MemorySetting` لتقليل الضغط على الذاكرة.

```csharp
Workbook workbook = new Workbook(@"C:\Data\financial_report.xlsx");
```

---

## الخطوة 2: ضبط خيارات حفظ PDF للتقريب (how to round numbers)

فئة `PdfSaveOptions` هي المكان الذي يحدث فيه السحر. لنستعرض أهم خاصيتين للتقريب:

| الخاصية | الوصف | القيم الشائعة |
|----------|-------------|----------------|
| `SignificantDigits` | تحدد وضع التقريب. | `Preserve`، `Round`، `Scientific` |
| `Precision` | عدد الأرقام ذات الدلالة عندما يتم اختيار `Round`. | 2‑6 شائع للتقارير المالية. |

إذا كنت تحتاج إلى تقريب مختلف لكل ورقة، يمكنك التكرار عبر الأوراق وتطبيق `PdfSaveOptions` لكل ورقة باستخدام `PdfSaveOptions.SetWorksheetOptions`. هذه حالة حافة مفيدة عندما تحتاج ورقة واحدة لأرقام محاسبية دقيقة وأخرى لعرض بيانات علمية.

```csharp
PdfSaveOptions options = new PdfSaveOptions
{
    SignificantDigits = SignificantDigits.Round,
    Precision = 3 // three significant digits
};
```

**لماذا هذا مهم:** التقريب أثناء مرحلة توليد PDF يتجنب خطوة تنظيف البيانات المنفصلة، مما يوفر الوقت ويقلل خطر وجود قيم غير متطابقة بين Excel والوثيقة النهائية.

---

## الخطوة 3: تصدير المصنف كملف PDF (save excel as pdf)

استدعاء `Save` النهائي يحترم كل خيار ضبطناه مسبقًا. إذا احتجت لإنشاء ملفات PDF متعددة من نفس المصنف مع قواعد تقريب مختلفة، ما عليك سوى استنساخ كائن `PdfSaveOptions`، تعديل الخصائص، ثم استدعاء `Save` مرة أخرى.

```csharp
// First PDF – rounded to 3 digits
workbook.Save(@"C:\Exports\rounded.pdf", options);

// Second PDF – preserve original values
options.SignificantDigits = SignificantDigits.Preserve;
workbook.Save(@"C:\Exports\preserved.pdf", options);
```

**الناتج المتوقع:** افتح ملف PDF المُولد بأي عارض؛ ستظهر الخلايا الرقمية قيمًا مقربة (مثال: `1234.5678` يصبح `1235` إذا كان `Precision = 4` ووضع التقريب هو `Round`). جميع التنسيقات الأخرى—ألوان الخلايا، الخلايا المدمجة، المخططات—تبقى تمامًا كما في ملف Excel الأصلي.

---

## اختياري: ضبط التقريب لخلايا محددة

أحيانًا تريد تقريب أعمدة معينة فقط (مثل عمود “السعر”) مع ترك البقية دون تعديل. يتيح لك Aspose.Cells تطبيق **تنسيق رقم مخصص** قبل الحفظ:

```csharp
Worksheet sheet = workbook.Worksheets[0];
CellRange priceRange = sheet.Cells.CreateRange("B2:B100");

// Apply a numeric format that rounds to two decimal places
priceRange.Style.Custom = "#,##0.00";
priceRange.ApplyStyle(priceRange.Style, new StyleFlag { NumberFormat = true });
```

عند استدعاء `workbook.Save` مع `SignificantDigits.Preserve`، يضمن التنسيق المخصص أن يظهر PDF أرقامًا مقربة، رغم أن القيمة الأساسية تظل دقيقة. هذه التقنية تجيب على سؤال “ماذا لو احتجت تقريبًا خاصًا بعمود معين؟” دون الحاجة إلى فروع برمجية إضافية.

---

## اختبار الناتج (convert excel to pdf)

فحص سريع يوفر لك ساعات من التصحيح:

1. **تشغيل البرنامج** – تحقق من أن وحدة التحكم تطبع “PDF generated successfully…”.
2. **فتح `output.pdf`** – راقب الأعمدة الرقمية؛ يجب أن تحترم التقريب الذي ضبطته.
3. **المقارنة مع Excel** – إذا اختلفت الأرقام، أعد فحص إعدادات `SignificantDigits` و `Precision`.
4. **اختبار آلي** – لخطوط أنابيب CI، يمكنك تحويل PDF إلى صورة (`PdfRenderer`) وإجراء مقارنة بكسل‑بكسل لضمان ظهور التقريب كما هو متوقع.

---

## الأخطاء الشائعة وكيفية تجنبها

| العَرَض | السبب المحتمل | الحل |
|---------|--------------|-----|
| لا تزال الأرقام تظهر عددًا كبيرًا من الكسور | ترك `SignificantDigits` على القيمة الافتراضية `Preserve` | عيّن `pdfOptions.SignificantDigits = SignificantDigits.Round`. |
| حجم PDF كبير (مئات الميغابايت) | الصور غير مضغوطة | استخدم `pdfOptions.ImageCompression = ImageCompression.Jpeg; pdfOptions.JpegQuality = 80;`. |
| لا يُطبق التقريب على ورقة معينة | تم تطبيق الخيارات عالميًا، ثم تم تجاوزها لاحقًا في الورقة | استدعِ `worksheet.PageSetup.PrintOptions.PreserveFormatting = true;` قبل الحفظ، أو استخدم خيارات لكل ورقة. |
| استثناء: `File not found` | فاصل المسار غير صحيح أو الملف مفقود | استخدم سلاسل النص الحرفية (`@"C:\Path\file.xlsx"`) وتأكد من وجود الملف. |

---

## خلاصة ما تعلمته

غطّينا **كيفية تقريب الأرقام** أثناء **تحويل Excel إلى PDF**، وعرضنا سير عمل **تصدير المصنف كملف PDF** الكامل، وأظهرنا لك كيفية **حفظ Excel كملف PDF** بدقة مخصصة. لديك الآن نمط قابل لإعادة الاستخدام يعمل مع مهام **convert xlsx to pdf** عبر سطح المكتب، الويب، أو الخدمات السحابية.

### الخطوات التالية

* استكشف توافق **PDF/A** (`PdfSaveOptions.Compliance = PdfCompliance.PdfA1b`) للوثائق الأرشيفية.
* اجمع هذا مع **Aspose.Slides** لتضمين المخططات كصور قبل التحويل.
* أتمتة المعالجة الدفعة—التكرار عبر مجلد من ملفات `.xlsx`، تطبيق قواعد تقريب مختلفة لكل ملف، وإسقاط ملفات PDF في حاوية التقارير.

لا تتردد في تجربة تعداد `SignificantDigits`، اللعب بـ `Precision`، وتكييف الكود مع قواعد عملك. إذا واجهت أي صعوبات، توثيق Aspose.Cells مرجع قوي، لكن النمط أعلاه يجب أن يغطي 90 % من السيناريوهات الواقعية.

برمجة سعيدة، ولتظهر ملفات PDF دائمًا الأرقام كما تحتاجها!

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة شفرة كاملة مع شرح خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [How to Convert Excel to PDF/A Using Aspose.Cells for .NET (Comprehensive Guide)](/cells/english/net/workbook-operations/convert-excel-to-pdf-a-aspose-cells-dotnet/)
- [How to Export Excel Charts to PDF Using Aspose.Cells for .NET: A Step-by-Step Guide](/cells/english/net/workbook-operations/export-excel-charts-pdf-aspose-cells-net/)
- [How to Save Specific Pages of an Excel File as PDF Using Aspose.Cells for .NET](/cells/english/net/workbook-operations/save-specific-excel-pages-pdf-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}