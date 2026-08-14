---
category: general
date: 2026-08-14
description: تصدير Excel إلى PowerPoint باستخدام Aspose.Cells وتعلم كيفية حساب صيغ
  Excel في الشيفرة. مثال خطوة‑بخطوة بلغة C# مع المصدر الكامل.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel to powerpoint
- calculate excel formulas in code
- Aspose.Cells copy pivot table
- export editable objects pptx
- dynamic array EXPAND function
- C# workbook automation
language: ar
lastmod: 2026-08-14
og_description: تصدير Excel إلى PowerPoint باستخدام Aspose.Cells وحساب صيغ Excel في
  الشيفرة. اتبع هذا الدليل الكامل لإنشاء ملفات PPTX قابلة للتعديل من المصنفات.
og_image_alt: Screenshot showing an Excel sheet being exported to a PowerPoint slide
  with editable textboxes
og_title: تصدير Excel إلى PowerPoint باستخدام Aspose.Cells – دليل C# كامل
schemas:
- author: Aspose
  dateModified: '2026-08-14'
  description: Export Excel to PowerPoint using Aspose.Cells and learn how to calculate
    Excel formulas in code. Step‑by‑step C# example with full source.
  headline: Export Excel to PowerPoint with Aspose.Cells – complete programming guide
  type: TechArticle
- description: Export Excel to PowerPoint using Aspose.Cells and learn how to calculate
    Excel formulas in code. Step‑by‑step C# example with full source.
  name: Export Excel to PowerPoint with Aspose.Cells – complete programming guide
  steps:
  - name: Why this works
    text: '* **`Workbook`** loads the entire Excel file into memory, giving you full
      API access. * **`CopyRange`** with `CopyPivotTable = true` ensures the pivot
      table’s data source, cache, and layout are duplicated exactly—something older
      versions of Aspose.Cells could not do. * Adding a new worksheet (`Copy`'
  - name: Explanation
    text: '* **`WorkbookDesigner`** is a high‑level helper that prepares the workbook
      for export, handling Smart Markers, named ranges, and layout adjustments. *
      Setting `ExportEditableObjects = true` tells Aspose.Cells to translate Excel
      drawings into PowerPoint shapes rather than flattening them into images.'
  - name: Why you might use this
    text: '* **Uniform data type:** Exporting as strings avoids type‑mismatch errors
      when the consumer expects text. * **Custom formatting:** Replace `value.ToString()`
      with any custom formatter (e.g., `value.ToString("yyyy-MM-dd")` for dates).'
  - name: How the calculation engine works
    text: '* The `Formula` property stores the expression exactly as you would type
      it in Excel. * `CalculateFormula()` triggers a full workbook recalculation,
      respecting dependencies between cells. * The `EXPAND` function (available in
      Excel 365) returns a spill range based on the source cell (`B1`) and the s'
  - name: What to verify
    text: '* Open `result.xlsx` in Excel to confirm the pivot table copy, the `EXPAND`
      formula result, and any custom‑exported strings. * Open `output.pptx` in PowerPoint;
      you should see a slide that mirrors the Excel layout, and all charts/textboxes
      should be editable.'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
- PowerPoint export
- Office 365 functions
title: تصدير Excel إلى PowerPoint باستخدام Aspose.Cells – دليل برمجي كامل
url: /ar/net/converting-excel-files-to-other-formats/export-excel-to-powerpoint-with-aspose-cells-complete-progra/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تصدير Excel إلى PowerPoint باستخدام Aspose.Cells – دليل برمجة كامل

إذا كنت بحاجة إلى **تصدير Excel إلى PowerPoint** برمجياً، يوضح لك هذا الدليل بالضبط كيفية القيام بذلك باستخدام Aspose.Cells for .NET. ستتعلم أيضًا كيفية **حساب صيغ Excel في الكود**، نسخ جداول Pivot دون فقدان التعريفات، واستخدام الدالة الجديدة Office‑365 EXPAND للمصفوفات الديناميكية.

في الأقسام التالية سنستعرض مثالًا واقعيًا بلغة C#، نشرح لماذا كل سطر مهم، ونغطي المشكلات الشائعة حتى تتمكن من تعديل الحل وفقًا لمشاريعك.

## ما يغطيه هذا الدرس

* تحميل مصنف موجود (`input.xlsx`)  
* نسخ نطاق يحتوي على جدول Pivot مع الحفاظ على تعريفه  
* تصدير المصنف إلى ملف PowerPoint (`.pptx`) مع مربعات نص وأشكال قابلة للتحرير  
* تصدير نطاق خلايا كسلاسل نصية باستخدام منطق مخصص  
* حساب صيغ Excel في الكود، بما في ذلك دالة Office‑365 EXPAND  
* حفظ المصنف النهائي مع تطبيق جميع التغييرات  

**المتطلبات المسبقة**  
* .NET 6.0 أو أحدث (الكود يعمل أيضًا مع .NET Framework 4.7.2+)  
* Aspose.Cells for .NET v25.11 أو أحدث (تم تقديم خيار `CopyPivotTable` في الإصدار v25.11)  
* فهم أساسي للغة C# ومفاهيم Excel مثل النطاقات، جداول Pivot، والصيغ  

> **نصيحة احترافية:** قم بتثبيت Aspose.Cells عبر NuGet (`Install-Package Aspose.Cells`) للحفاظ على مشروعك محدثًا بأحدث الميزات.

## تصدير Excel إلى PowerPoint باستخدام Aspose.Cells

المهمة الرئيسية الأولى هي تحويل المصنف إلى عرض تقديمي PowerPoint مع الحفاظ على قابلية تحرير جميع العناصر البصرية. هذا أمر أساسي عندما تريد إنشاء شرائح من تقارير مالية أو لوحات معلومات تلقائيًا.

```csharp
using Aspose.Cells;
using Aspose.Cells.Export;      // ExportTableOptions, ExportOptions, etc.
using Aspose.Cells.Pivot;      // Pivot‑table APIs
using Aspose.Cells.Drawing;    // Shapes, textboxes, etc.

// Step 1: Load the workbook
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

// Step 2: Copy a range that contains a pivot table (preserves the definition)
Worksheet sourceSheet = workbook.Worksheets["Source"];
Range sourceRange = sourceSheet.Cells.CreateRange("A1:G20");   // includes a pivot table
Worksheet destinationSheet = workbook.Worksheets.Add("Copy");
destinationSheet.Cells.CopyRange(sourceRange, destinationSheet.Cells, new CopyOptions
{
    CopyPivotTable = true   // new option in v25.11
});
```

### لماذا يعمل هذا

* **`Workbook`** يقوم بتحميل ملف Excel بالكامل إلى الذاكرة، مما يمنحك وصولًا كاملًا إلى الـ API.  
* **`CopyRange`** مع `CopyPivotTable = true` يضمن نسخ مصدر بيانات جدول Pivot والذاكرة المؤقتة والتخطيط بدقة—وهو ما لم تستطع الإصدارات القديمة من Aspose.Cells القيام به.  
* إضافة ورقة عمل جديدة (`Copy`) يتيح لك الحفاظ على الورقة الأصلية دون تعديل، وهو مفيد لتتبع التدقيق.

## تصدير المصنف إلى PowerPoint مع كائنات قابلة للتحرير

الآن نقوم بتحويل المصنف إلى ملف PowerPoint. من خلال تمكين `ExportEditableObjects`، يصبح كل مخطط أو شكل أو مربع نص كائنًا أصليًا في PowerPoint يمكن للمستخدمين تحريره مباشرة بعد التصدير.

```csharp
// Step 3: Export the workbook to PowerPoint with editable textboxes/shapes
WorkbookDesigner designer = new WorkbookDesigner(workbook);
designer.Process();   // processes Smart Markers if present
designer.ExportToPptx("YOUR_DIRECTORY/output.pptx", new ExportOptions
{
    ExportEditableObjects = true   // makes objects editable in the PPTX
});
```

### شرح

* **`WorkbookDesigner`** هو أداة مساعدة عالية المستوى تُعد المصنف للتصدير، وتتعامل مع Smart Markers، النطاقات المسماة، وتعديلات التخطيط.  
* ضبط `ExportEditableObjects = true` يُخبر Aspose.Cells بترجمة رسومات Excel إلى أشكال PowerPoint بدلاً من تحويلها إلى صور مسطحة. هذا ينتج **عرض شرائح قابل للتحرير بالكامل**.

> **حالة حافة:** إذا كان المصنف يحتوي على مخططات معقدة مُنشأة من اتصالات بيانات خارجية، تأكد من حل تلك الاتصالات قبل استدعاء `ExportToPptx`، وإلا قد يظهر المخطط فارغًا.

## تصدير نطاق كسلاسل نصية باستخدام منطق مخصص

أحيانًا تحتاج إلى قيم نصية خام للمعالجة اللاحقة (مثل تغذية محلل CSV). تسمح لك فئة `ExportTableOptions` بالتحكم في كيفية تحويل كل خلية.

```csharp
// Step 4: Export a range as strings using custom logic
ExportTableOptions tableOptions = new ExportTableOptions
{
    ExportAsString = true,
    CustomExport = (cell, value) => value.ToString()   // simple conversion for each cell
};
workbook.Worksheets[0].Cells.ExportTableAsString(tableOptions, "A1:D10");
```

### لماذا قد تستخدم هذا

* **نوع بيانات موحد:** التصدير كسلاسل نصية يتجنب أخطاء عدم توافق الأنواع عندما يتوقع المستهلك نصًا.  
* **تنسيق مخصص:** استبدل `value.ToString()` بأي مُنسق مخصص (مثل `value.ToString("yyyy-MM-dd")` للتواريخ).

## حساب صيغ Excel في الكود

متطلب شائع هو **حساب صيغ Excel في الكود** دون فتح Excel. توفر Aspose.Cells محرك حساب مدمج يعمل دون اتصال ويدعم أحدث وظائف Office‑365، بما في ذلك `EXPAND`.

```csharp
// Step 5: Use the new Office‑365 EXPAND function to create a dynamic array
Worksheet firstSheet = workbook.Worksheets[0];
firstSheet.Cells["A1"].Formula = "EXPAND(B1,5,3)";   // expands array starting at B1
workbook.CalculateFormula();   // forces recalculation of the formula
```

### كيف يعمل محرك الحساب

* خاصية `Formula` تخزن التعبير تمامًا كما تكتبه في Excel.  
* `CalculateFormula()` يُطلق إعادة حساب كاملة للمصنف، مع مراعاة الاعتمادات بين الخلايا.  
* دالة `EXPAND` (متاحة في Excel 365) تُرجع نطاقًا ممتدًا بناءً على الخلية المصدر (`B1`) وعدد الصفوف المحدد (`5`) والأعمدة (`3`).  

> **نصيحة:** إذا كنت بحاجة إلى حساب جزء فقط من المصنف، استخدم `Worksheet.CalculateFormula()` لتحديد النطاق وتحسين الأداء.

## حفظ المصنف مع تطبيق جميع التغييرات

أخيرًا، احفظ المصنف المعدل مرة أخرى على القرص. يمكنك الحفظ بأي من الصيغ المدعومة (`.xlsx`, `.xls`, `.csv`, إلخ) عن طريق تغيير امتداد الملف.

```csharp
// Step 6: Save the workbook with all changes applied
workbook.Save("YOUR_DIRECTORY/result.xlsx");
```

### ما يجب التحقق منه

* افتح `result.xlsx` في Excel لتأكيد نسخ جدول Pivot، نتيجة صيغة `EXPAND`، وأي سلاسل نصية مُصدرة مخصصًا.  
* افتح `output.pptx` في PowerPoint؛ يجب أن ترى شريحة تعكس تخطيط Excel، وجميع المخططات/مربعات النص يجب أن تكون قابلة للتحرير.

## الأسئلة الشائعة وحلول المشكلات

| السؤال | الجواب |
|----------|--------|
| **هل أحتاج إلى ترخيص لاستخدام Aspose.Cells؟** | نعم. النسخة التجريبية تعمل للتقييم، لكن الترخيص الكامل يزيل علامات التقييم المائية ويفتح ميزة `CopyPivotTable`. |
| **ماذا إذا كان ملف PPTX المُصدّر يظهر أشكالًا فارغة؟** | تأكد من أن كائنات الرسم في المصنف غير مخفية (`Visible = true`) وأن أي روابط صور خارجية مضمَّنة قبل التصدير. |
| **هل يمكنني تصدير عدة أوراق عمل إلى شرائح PPTX منفصلة؟** | استخدم `WorkbookDesigner.ExportToPptx` داخل حلقة، مع تحديد `ExportOptions` مختلفة لكل ورقة عمل، أو اجمعها في عرض تقديمي واحد بإضافة الشرائح يدويًا عبر Aspose.Slides. |
| **هل `CalculateFormula` آمن للاستخدام في بيئات متعددة الخيوط؟** | لا. قم بإجراء الحسابات على خيط واحد أو استنسخ المصنف لكل خيط لتجنب حالات السباق. |

## الخلاصة

الآن لديك **حل كامل من البداية إلى النهاية لتصدير Excel إلى PowerPoint** باستخدام Aspose.Cells، وتفهم كيفية **حساب صيغ Excel في الكود**—بما في ذلك الدالة الحديثة `EXPAND`. غطى الدرس تحميل المصنف، نسخ جداول Pivot، التصدير إلى PowerPoint قابل للتحرير، تصدير السلاسل النصية المخصصة، حساب الصيغ، والحفظ النهائي.

من هنا يمكنك:

* توسيع التصدير ليشمل عدة شرائح لكل ورقة عمل (الكلمة المفتاحية الثانوية: *calculate Excel formulas in code* يمكن إعادة استخدامها عند توليد بيانات المخططات).  
* دمج Aspose.Slides لإضافة الرسوم المتحركة أو تخطيطات الشرائح الرئيسية.  
* استبدال التفويض البسيط `CustomExport` بتنسيق يدعم اللغة المحلية للمشاريع الدولية.  

لا تتردد في تجربة نطاقات مختلفة، استكشاف وظائف Office‑365 أخرى (مثل `FILTER`, `SORT`)، ودمج هذا سير العمل مع إرسال البريد الإلكتروني الآلي لإنشاء خطوط تقارير تلقائية بالكامل.

---

## ماذا يجب أن تتعلم بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مصدر يتضمن أمثلة كود كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [أتمتة تصدير بيانات Excel باستخدام Aspose.Cells لـ .NET: دليل خطوة بخطوة](/cells/english/net/automation-batch-processing/automate-excel-data-export-aspose-cells-net/)
- [كيفية تصدير مخططات Excel إلى PDF باستخدام Aspose.Cells لـ .NET: دليل خطوة بخطوة](/cells/english/net/workbook-operations/export-excel-charts-pdf-aspose-cells-net/)
- [تصدير خلايا Excel إلى صورة باستخدام Aspose.Cells .NET: دليل خطوة بخطوة](/cells/english/net/import-export/export-excel-cells-to-image-aspose-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}