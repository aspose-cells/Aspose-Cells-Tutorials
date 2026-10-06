---
category: general
date: 2026-05-30
description: كيفية استخدام SmartMarkerProcessor لإعادة تسمية الورقة الحالية وأتمتة
  مهام إعادة تسمية أوراق Excel في بضع خطوات بسيطة.
draft: false
keywords:
- how to use smartmarkerprocessor
- rename existing sheet
- automate excel sheet rename
language: ar
og_description: كيفية استخدام SmartMarkerProcessor لإعادة تسمية الورقة الحالية وتلقائيًا
  مهام إعادة تسمية أوراق Excel في دليل مختصر خطوة بخطوة.
og_title: كيفية استخدام SmartMarkerProcessor – إعادة تسمية ورقة موجودة في Excel
schemas:
- author: Aspose
  dateModified: '2026-05-30'
  description: How to use SmartMarkerProcessor to rename existing sheet and automate
    Excel sheet rename tasks in a few simple steps.
  headline: How to Use SmartMarkerProcessor – Rename Existing Sheet in Excel
  type: TechArticle
- description: How to use SmartMarkerProcessor to rename existing sheet and automate
    Excel sheet rename tasks in a few simple steps.
  name: How to Use SmartMarkerProcessor – Rename Existing Sheet in Excel
  steps:
  - name: 1. Multiple Existing Detail Sheets
    text: If your template already contains **Detail**, **Detail_1**, and **Detail_2**,
      the processor will generate **Detail_3**. This behavior is deterministic, so
      you can rely on it for batch processing.
  - name: 2. Custom Prefixes or Suffixes
    text: You might want the new sheet to start with a date stamp, e.g., `"Detail_2023-09-01"`.
      Set `DetailSheetNewName = $"Detail_{DateTime.Today:yyyy-MM-dd}"`. The processor
      will still add numeric suffixes if needed.
  - name: 3. Renaming Other Sheets
    text: '`SmartMarkerOptions` also provides `HeaderSheetNewName` and `SummarySheetNewName`.
      Use them the same way to **rename existing sheet** types beyond the detail sheet.'
  - name: 4. Performance Considerations
    text: When processing large workbooks (hundreds of sheets), instantiate **one**
      `SmartMarkerProcessor` and reuse it across files. This reduces memory churn
      and speeds up the **automate excel sheet rename** workflow.
  type: HowTo
tags:
- Excel automation
- GemBox
- SmartMarker
title: كيفية استخدام SmartMarkerProcessor – إعادة تسمية ورقة موجودة في Excel
url: /ar/net/worksheet-management/how-to-use-smartmarkerprocessor-rename-existing-sheet-in-exc/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية استخدام SmartMarkerProcessor – إعادة تسمية ورقة موجودة في Excel

هل تساءلت يومًا **how to use SmartMarkerProcessor** لإعادة تسمية ورقة موجودة أثناء تعبئة البيانات؟ لست وحدك. يواجه العديد من المطورين عقبة عندما يحتوي القالب الخاص بهم بالفعل على ورقة عمل تسمى “Detail” ويحاول محرك SmartMarker إنشاء ورقة أخرى بنفس الاسم. الخبر السار؟ ببضع أسطر من الشيفرة يمكنك **automate Excel sheet rename** دون إفساد سير العمل.

في هذا الدرس سنستعرض مثالًا كاملاً وقابلًا للتنفيذ يوضح بالضبط كيفية تكوين المعالج، وإعادة تسمية الأوراق الموجودة، والحفاظ على ملفات Excel مرتبة. لا تخمين—فقط شيفرة واضحة، وتفسيرات لـ *why* كل سطر مهم، ونصائح للتعامل مع الحالات الحدية التي ستواجهها حتمًا.

---

## المتطلبات المسبقة

- **GemBox.Spreadsheet** (أو أي مكتبة توفر `SmartMarkerProcessor`) الإصدار 2024‑latest مثبت عبر NuGet.
- بيئة تطوير .NET (Visual Studio، VS Code، Rider—حسب اختيارك).
- قالب Excel أساسي (`Template.xlsx`) يحتوي بالفعل على ورقة عمل باسم **Detail**.
- مصدر بيانات بسيط (مثل `DataTable`، `List<T>`، أو كائن مجهول) ترغب في دمجه في القالب.

هذا كل شيء. إذا كنت تفتقد أيًا من هذه، احصل على حزمة NuGet الآن:

```bash
dotnet add package GemBox.Spreadsheet
```

---

![كيفية استخدام smartmarkerprocessor مثال](/images/smartmarkerprocessor-rename.png "how to use smartmarkerprocessor example")

*الصورة أعلاه توضح ورقة العمل قبل وبعد عملية إعادة التسمية.*

---

## الخطوة 1: إعداد كائن SmartMarkerProcessor  

أول شيء تحتاجه هو كائن **SmartMarkerProcessor**. فكر فيه كمحرك يقرأ القالب الخاص بك، يبحث عن Smart Markers (مثل `{{Name}}`)، ويكتب البيانات في الخلايا المناسبة.

```csharp
using GemBox.Spreadsheet;
using GemBox.Spreadsheet.SmartMarkers;

// Initialize the component (license key is optional for the free version)
SpreadsheetInfo.SetLicense("FREE-LIMITED-KEY");

// Load the workbook that contains the template sheet.
var wb = ExcelFile.Load("Template.xlsx");

// Create the processor instance.
SmartMarkerProcessor processor = new SmartMarkerProcessor();
```

> **لماذا هذا مهم:** إنشاء المعالج **مرة واحدة** وإعادة استخدامه عبر التطبيق يقلل من الحمل. أيضًا، تحميل المصنف أولًا يمنحك مقبضًا لمجموعة أوراق العمل، والتي سنحتاجها عند إعادة تسمية الأوراق.

---

## الخطوة 2: تكوين خيارات إعادة تسمية الورقة الموجودة  

الآن يأتي جوهر الموضوع: إخبار SmartMarker كيف يتصرف عندما يصادف تعارضًا في أسماء الأوراق. تُظهر فئة `SmartMarkerOptions` خاصية تسمى `DetailSheetNewName`. إذا كانت ورقة باسم `"Detail"` موجودة بالفعل، سيضيف المعالج تلقائيًا لاحقة (`_1`، `_2`، …) لتجنب التعارض.

```csharp
// Define processing options.
// The DetailSheetNewName property controls the base name for the detail sheet.
SmartMarkerOptions options = new SmartMarkerOptions
{
    // If "Detail" exists, the new sheet will become "Detail_1"
    DetailSheetNewName = "Detail"
};
```

> **نصيحة احترافية:** إذا كنت تفضل لاحقة مخصصة (مثل `"Detail-Backup"`)، فقط عيّن `DetailSheetNewName = "Detail-Backup"`. سيستمر المعالج في إضافة أرقام حسب الحاجة.

> **لماذا هذا مهم:** بدون هذا الخيار، سيتسبب SmartMarker في رمي استثناء أو استبدال الورقة الموجودة بصمت، مما يؤدي إلى فقدان البيانات. تكوين سلوك إعادة التسمية صراحةً **automates Excel sheet rename** ويحافظ على قوالبك سليمة.

---

## الخطوة 3: إعداد مصدر البيانات  

يمكن لـ SmartMarker العمل مع أي مصدر بيانات قابل للتعداد تقريبًا. للتوضيح، لنستخدم قائمة بسيطة من الكائنات المجهولة التي تمثل بنود الفاتورة.

```csharp
var dataSource = new[]
{
    new { Item = "Widget A", Quantity = 5, Price = 9.99 },
    new { Item = "Widget B", Quantity = 2, Price = 19.95 },
    new { Item = "Widget C", Quantity = 1, Price = 49.50 }
};
```

إذا كان لديك بالفعل `DataTable` أو `IEnumerable<T>`، فقط قم بربطه—لا حاجة لتحويل إضافي.

---

## الخطوة 4: تطبيق معالجة SmartMarker على ورقة العمل الأولى  

مع وجود المعالج، الخيارات، والبيانات جاهزة، حان الوقت لتشغيل الدمج. سنستهدف **ورقة العمل الأولى** (`wb.Worksheets[0]`) لأن القالب موجود هناك. طريقة `Process` تأخذ ثلاثة معطيات: ورقة العمل، مصدر البيانات، والخيارات التي عرّفناها سابقًا.

```csharp
// Apply SmartMarker processing.
// This will insert the data into the template and rename the detail sheet if needed.
processor.Process(wb.Worksheets[0], dataSource, options);
```

> **ماذا يحدث خلف الكواليس؟**  
> 1. يقوم SmartMarker بمسح ورقة العمل للبحث عن العلامات مثل `{{Item}}`، `{{Quantity}}`، إلخ.  
> 2. ينشئ ورقة تفصيلية جديدة باستخدام الاسم المحدد في `DetailSheetNewName`.  
> 3. إذا كانت هناك ورقة باسم “Detail” موجودة بالفعل، يتحول تلقائيًا إلى “Detail_1”.  
> 4. تُكتب صفوف البيانات إلى الورقة الجديدة مع الحفاظ على التنسيق.

---

## الخطوة 5: حفظ النتيجة والتحقق من إعادة التسمية  

بعد المعالجة، ستحتاج إلى حفظ المصنف على القرص والتحقق مرة أخرى من أن الورقة تم إعادة تسميتها بشكل صحيح.

```csharp
// Save the processed workbook.
wb.Save("Result.xlsx");

// Quick verification (optional console output)
Console.WriteLine("Worksheets in the resulting file:");
foreach (var sheet in wb.Worksheets)
    Console.WriteLine($"- {sheet.Name}");
```

عند فتح `Result.xlsx`، يجب أن ترى ورقة باسم **Detail_1** (أو **Detail_2** إذا كانت “Detail_1” موجودة بالفعل). ستظهر صفوف البيانات تحت صف الرأس الذي وضعته في القالب.

---

## التعامل مع الحالات الحدية الشائعة  

### 1. وجود عدة أوراق Detail موجودة  

إذا كان القالب الخاص بك يحتوي بالفعل على **Detail**، **Detail_1**، و **Detail_2**، سيولد المعالج **Detail_3**. هذا السلوك حتمي، لذا يمكنك الاعتماد عليه في المعالجة الدفعية.

### 2. البادئات أو اللاحقات المخصصة  

قد ترغب في أن تبدأ الورقة الجديدة بطابع تاريخ، مثل `"Detail_2023-09-01"`. عيّن `DetailSheetNewName = $"Detail_{DateTime.Today:yyyy-MM-dd}"`. سيظل المعالج يضيف لاحقات رقمية إذا لزم الأمر.

### 3. إعادة تسمية أوراق أخرى  

`SmartMarkerOptions` توفر أيضًا `HeaderSheetNewName` و `SummarySheetNewName`. استخدمهما بنفس الطريقة **rename existing sheet** لأنواع الأوراق الأخرى بخلاف ورقة التفاصيل.

```csharp
options.HeaderSheetNewName = "Header";
options.SummarySheetNewName = "Summary";
```

### 4. اعتبارات الأداء  

عند معالجة مصنفات كبيرة (مئات الأوراق)، أنشئ **معالجًا واحدًا** `SmartMarkerProcessor` وأعد استخدامه عبر الملفات. هذا يقلل من استهلاك الذاكرة ويسرّع سير عمل **automate excel sheet rename**.

---

## مثال كامل يعمل  

بجمع كل شيء معًا، إليك برنامجًا مستقلًا يمكنك نسخه ولصقه في تطبيق Console وتشغيله فورًا:

```csharp
using System;
using GemBox.Spreadsheet;
using GemBox.Spreadsheet.SmartMarkers;

class Program
{
    static void Main()
    {
        // 1. License & load template.
        SpreadsheetInfo.SetLicense("FREE-LIMITED-KEY");
        var wb = ExcelFile.Load("Template.xlsx");

        // 2. Create processor.
        SmartMarkerProcessor processor = new SmartMarkerProcessor();

        // 3. Define rename options.
        SmartMarkerOptions options = new SmartMarkerOptions
        {
            DetailSheetNewName = "Detail"
        };

        // 4. Prepare data source.
        var dataSource = new[]
        {
            new { Item = "Widget A", Quantity = 5, Price = 9.99 },
            new { Item = "Widget B", Quantity = 2, Price = 19.95 },
            new { Item = "Widget C", Quantity = 1, Price = 49.50 }
        };

        // 5. Process the first worksheet.
        processor.Process(wb.Worksheets[0], dataSource, options);

        // 6. Save the result.
        wb.Save("Result.xlsx");

        // 7. Verify sheet names.
        Console.WriteLine("Worksheets after processing:");
        foreach (var sheet in wb.Worksheets)
            Console.WriteLine($"- {sheet.Name}");
    }
}
```

**الناتج المتوقع** (في وحدة التحكم):

```
Worksheets after processing:
- Sheet1
- Detail_1
```

افتح `Result.xlsx` وسترى البيانات مُعبأة بشكل منظم تحت علامة التبويب الجديدة **Detail_1**.

---

## ملخص  

لقد غطينا **how to use SmartMarkerProcessor** لإعادة تسمية ورقة موجودة بأمان وتلقائيًا **automate Excel sheet rename**. النقاط الرئيسية هي:

1. إنشاء مثيل واحد من `SmartMarkerProcessor`.  
2. تعيين `DetailSheetNewName` (أو خيارات أسماء الأوراق الأخرى) للتحكم في منطق إعادة التسمية.  
3. تمرير مصدر البيانات والخيارات إلى `Process`.  
4. حفظ والتحقق من أن الورقة تم إعادة تسميتها كما هو متوقع.

مع هذه الخطوات، يمكنك دمج SmartMarker في أي خط أنابيب تقارير—سواء كنت تولد فواتير، سجلات تدقيق، أو لوحات تحكم شهرية. النهج قابل للتوسع، يتعامل مع تصادمات الأسماء بسلاسة، ويحافظ على قابلية إعادة استخدام قوالب Excel.

## ما التالي؟

- **استكشف خيارات SmartMarkerOptions الأخرى**: `HeaderSheetNewName`، `SummarySheetNewName`، و `InsertBlankRows` للحصول على تحكم أدق.  
- **اجمعها مع التنسيق**: استخدم API التنسيق الغني لـ GemBox لتطبيق الألوان، الحدود، أو التنسيق الشرطي بعد الدمج.  
- **معالجة دفعة من المصنفات المتعددة**: تكرار عبر دليل القوالب، وإعادة استخدام نفس مثيل المعالج لتحقيق أقصى إنتاجية.

لا تتردد في التجربة—ربما ستنشئ ورقة “Report_2024_Q1” التي تُضيف رقم نسخة تلقائيًا في كل تشغيل. الاحتمالات لا حصر لها، والآن لديك أساس قوي لأتمتة **rename existing sheet**.

برمجة سعيدة، ولتظل ملفات Excel منظمة دائمًا!

## ماذا يجب أن تتعلمه بعد ذلك؟

- [كيفية دمج وإعادة تسمية أوراق Excel باستخدام Aspose.Cells لـ .NET: دليل خطوة بخطوة](/cells/english/net/worksheet-management/merge-rename-excel-sheets-aspose-cells-net/)
- [كيفية تغيير معرفات أوراق Excel في .NET باستخدام Aspose.Cells: دليل شامل](/cells/english/net/worksheet-management/change-excel-sheet-id-net-aspose-cells/)
- [كيفية استخدام Aspose.Cells لـ .NET لتجميع الصفوف والأعمدة في Excel](/cells/english/net/data-analysis/excel-grouping-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}