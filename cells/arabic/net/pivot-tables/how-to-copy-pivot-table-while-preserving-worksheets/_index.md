---
category: general
date: 2026-09-15
description: تعلم كيفية نسخ جدول محوري، نسخ ورقة عمل مع جدول محوري، وحفظ المصنف كملف pptx
  باستخدام Aspose.Cells في C#. دليل كامل خطوة بخطوة.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy pivot table
- copy worksheet with pivot
- save workbook as pptx
language: ar
lastmod: 2026-09-15
og_description: كيفية نسخ جدول محوري، نسخ ورقة عمل تحتوي على جدول محوري، وحفظ المصنف
  كملف pptx باستخدام Aspose.Cells. تابع الأمثلة الكاملة القابلة للتنفيذ بلغة C#.
og_image_alt: Screenshot showing how to copy pivot table in a C# code editor
og_title: كيفية نسخ جدول المحور وتصدير أوراق العمل – دليل C# الكامل
schemas:
- author: Aspose
  dateModified: '2026-09-15'
  description: Learn how to copy pivot table, copy worksheet with pivot, and save
    workbook as pptx using Aspose.Cells in C#. Complete step‑by‑step guide.
  headline: How to copy pivot table while preserving worksheets
  type: TechArticle
- description: Learn how to copy pivot table, copy worksheet with pivot, and save
    workbook as pptx using Aspose.Cells in C#. Complete step‑by‑step guide.
  name: How to copy pivot table while preserving worksheets
  steps:
  - name: – Load the source workbook that holds the pivot table
    text: '```csharp // Load the workbook that contains the pivot table you want to
      copy Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/Source.xlsx"); ```'
  - name: – Create an empty destination workbook
    text: '```csharp // Create a new, empty workbook that will receive the copied
      data Workbook destinationWorkbook = new Workbook(); ```'
  - name: – Copy the rows that include the pivot table
    text: '```csharp // Copy rows 0‑19 (A1:G20) from the first worksheet of the source
      sourceWorkbook.Worksheets[0].Cells.CopyRows(0, 0, 20); ```'
  - name: – Copy the columns that contain the pivot table
    text: '```csharp // Copy columns 0‑6 (A‑G) from the same worksheet sourceWorkbook.Worksheets[0].Cells.CopyColumns(0,
      0, 7); ```'
  - name: – Transfer the prepared sheet into the destination workbook
    text: '```csharp // Move the fully prepared worksheet into the destination workbook
      sourceWorkbook.Worksheets[0].Copy(destinationWorkbook.Worksheets[0]); ```'
  - name: – Save the result – the pivot table remains intact
    text: '```csharp // Save the destination workbook; the pivot table works exactly
      like the original destinationWorkbook.Save("YOUR_DIRECTORY/CopyWithPivot.xlsx");
      ```'
  - name: – Load the workbook that includes the textbox
    text: '```csharp // Load the Excel file that contains an editable textbox shape
      Workbook workbookWithTextbox = new Workbook("YOUR_DIRECTORY/DocWithTextbox.xlsx");
      ```'
  - name: – Configure PPTX save options
    text: '```csharp // Create PPTX save options and enable the editable textbox feature
      (available from v25.11) PptxSaveOptions pptxOptions = new PptxSaveOptions {
      ExportEditableTextBox = true }; ```'
  - name: – Save the workbook as PPTX
    text: '```csharp // Export the workbook to a PPTX file; the textbox stays editable
      in PowerPoint workbookWithTextbox.Save("YOUR_DIRECTORY/Result.pptx", pptxOptions);
      ```'
  - name: – Prepare the SmartMarkerProcessor
    text: '```csharp // Initialise the processor that will fill Smart Markers SmartMarkerProcessor
      smartMarkerProcessor = new SmartMarkerProcessor(); ```'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: كيفية نسخ جدول محوري مع الحفاظ على أوراق العمل
url: /ar/net/pivot-tables/how-to-copy-pivot-table-while-preserving-worksheets/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية نسخ جدول محوري مع الحفاظ على أوراق العمل

إذا كنت بحاجة إلى **how to copy pivot table** من مصنف إلى آخر دون فقدان ذاكرة التخزين المؤقت للجدول المحوري، فإن هذا الدليل يوفر حلاً جاهزًا للتنفيذ. ستتعرف أيضًا على كيفية **copy worksheet with pivot** وكيفية **save workbook as pptx** مع الحفاظ على صناديق النص القابلة للتحرير. جميع الأمثلة تستخدم أحدث Aspose.Cells for .NET، لذا يمكنك إدراج الشيفرة في أي مشروع C# ورؤية النتائج فورًا.

العمل مع ملفات Excel برمجيًا غالبًا ما يتضمن نقل البيانات بين المصنفات، تصديرها إلى عروض تقديمية، أو إدراج Smart Markers معقدة. الثلاثة مقتطفات الشيفرة أدناه تغطي هذه السيناريوهات الشائعة وتوضح لماذا كل خطوة مهمة.

## المتطلبات المسبقة

قبل أن تبدأ، تأكد من أن لديك:

* .NET 6.0 أو أحدث مثبت  
* Aspose.Cells for .NET (الإصدار 25.11 أو أحدث) مُشار إليه في مشروعك  
* مجلد اسمه `YOUR_DIRECTORY` حيث سيتم قراءة الملفات النموذجية وكتابتها  

لا توجد حزم NuGet إضافية مطلوبة.

---

## كيفية نسخ جدول محوري باستخدام Aspose.Cells

نسخ نطاق يحتوي على جدول محوري مع الحفاظ على ذاكرة التخزين المؤقت للجدول المحوري هو طلب شائع. الخطوات التالية توضح التسلسل الدقيق الذي تحتاجه.

### الخطوة 1 – تحميل المصنف المصدر الذي يحتوي على الجدول المحوري

```csharp
// Load the workbook that contains the pivot table you want to copy
Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/Source.xlsx");
```

*لماذا*: تقوم Aspose.Cells بقراءة المصنف إلى الذاكرة، مما يمنحك الوصول إلى أوراق العمل، الخلايا، والجداول المحورية.

### الخطوة 2 – إنشاء مصنف وجهة فارغ

```csharp
// Create a new, empty workbook that will receive the copied data
Workbook destinationWorkbook = new Workbook();
```

*لماذا*: البدء بمصنف فارغ يضمن عدم وجود أنماط مخفية أو نطاقات مسماة تتداخل مع عملية النسخ.

### الخطوة 3 – نسخ الصفوف التي تشمل الجدول المحوري

```csharp
// Copy rows 0‑19 (A1:G20) from the first worksheet of the source
sourceWorkbook.Worksheets[0].Cells.CopyRows(0, 0, 20);
```

*لماذا*: `CopyRows` ينسخ قيم الخلايا الخام، التنسيقات، وإشارات ذاكرة التخزين المؤقت للجدول المحوري. يجب أن يشمل النطاق كامل مساحة الجدول المحوري.

### الخطوة 4 – نسخ الأعمدة التي تحتوي على الجدول المحوري

```csharp
// Copy columns 0‑6 (A‑G) from the same worksheet
sourceWorkbook.Worksheets[0].Cells.CopyColumns(0, 0, 7);
```

*لماذا*: الجداول المحورية تمتد عبر الصفوف والأعمدة؛ نسخ الأعمدة يضمن الحفاظ على تخطيط الجدول بالكامل.

### الخطوة 5 – نقل الورقة المُعدة إلى المصنف الوجهة

```csharp
// Move the fully prepared worksheet into the destination workbook
sourceWorkbook.Worksheets[0].Copy(destinationWorkbook.Worksheets[0]);
```

*لماذا*: طريقة `Copy` تستنسخ ورقة العمل، بما في ذلك ذاكرة التخزين المؤقت للجدول المحوري، لذا يظهر المصنف الوجهة جدولًا محوريًا مطابقًا.

### الخطوة 6 – حفظ النتيجة – يبقى الجدول المحوري سليمًا

```csharp
// Save the destination workbook; the pivot table works exactly like the original
destinationWorkbook.Save("YOUR_DIRECTORY/CopyWithPivot.xlsx");
```

*لماذا*: حفظ المصنف يكتب جميع البُنى الداخلية، مما يضمن إمكانية تحديث الجدول لاحقًا.

**نصيحة احترافية**: بعد النسخ، يمكنك استدعاء `destinationWorkbook.Worksheets[0].PivotTables[0].Refresh()` لتحديث البيانات إذا تغيرت بيانات المصدر.

---

## نسخ ورقة عمل مع جدول محوري – بديل مختصر

إذا كنت بحاجة فقط إلى تكرار ورقة عمل كاملة تحتوي بالفعل على جدول محوري، يمكنك تخطي خطوات نسخ الصفوف/الأعمدة واستخدام طريقة `Copy` على مستوى الورقة مباشرة.

```csharp
// Load source workbook
Workbook src = new Workbook("YOUR_DIRECTORY/SourceWithPivot.xlsx");

// Create destination workbook
Workbook dst = new Workbook();

// Copy the first worksheet (including its pivot table) to the destination
src.Worksheets[0].Copy(dst.Worksheets[0]);

// Save the new file
dst.Save("YOUR_DIRECTORY/WorksheetCopy.xlsx");
```

هذا النهج مفيد عندما لا تحتوي ورقة العمل على بيانات إضافية خارج منطقة الجدول المحوري. عملية **copy worksheet with pivot** تحافظ تلقائيًا على جميع التنسيقات، النطاقات المسماة، وذاكرة التخزين المؤقت للجداول المحورية.

---

## حفظ المصنف كملف PPTX مع صناديق نص قابلة للتحرير

تصدير ورقة Excel تحتوي على صندوق نص قابل للتحرير إلى PowerPoint قد يكون مطلوبًا لتقارير لوحة التحكم. الشيفرة أدناه توضح **save workbook as pptx** مع الحفاظ على قابلية تحرير صندوق النص.

### الخطوة 1 – تحميل المصنف الذي يتضمن صندوق النص

```csharp
// Load the Excel file that contains an editable textbox shape
Workbook workbookWithTextbox = new Workbook("YOUR_DIRECTORY/DocWithTextbox.xlsx");
```

### الخطوة 2 – تكوين خيارات حفظ PPTX

```csharp
// Create PPTX save options and enable the editable textbox feature (available from v25.11)
PptxSaveOptions pptxOptions = new PptxSaveOptions
{
    ExportEditableTextBox = true
};
```

*لماذا*: ضبط `ExportEditableTextBox` يخبر Aspose.Cells بترجمة صندوق النص في Excel إلى شكل PowerPoint يبقى قابلًا للتحرير بعد التصدير.

### الخطوة 3 – حفظ المصنف كملف PPTX

```csharp
// Export the workbook to a PPTX file; the textbox stays editable in PowerPoint
workbookWithTextbox.Save("YOUR_DIRECTORY/Result.pptx", pptxOptions);
```

**النتيجة المتوقعة**: افتح `Result.pptx` في PowerPoint، حدد صندوق النص، وحرّر محتواه كما تفعل مع أي شكل أصلي.

**سؤال شائع**: *ماذا لو أردت إبقاء صندوق النص مقفلًا؟*  
قم بتعيين `pptxOptions.ExportEditableTextBox = false`؛ سيتحول الشكل إلى صورة ثابتة بدلاً من ذلك.

---

## تصدير Smart Marker يحتوي على مصفوفة JSON كقيمة خلية واحدة

تتيح لك Smart Markers تعبئة قوالب Excel بهياكل بيانات معقدة. المثال التالي كامل يوضح **how to copy pivot table**‑style في معالجة البيانات أثناء إدراج مصفوفة JSON في خلية واحدة.

### الخطوة 1 – إعداد SmartMarkerProcessor

```csharp
// Initialise the processor that will fill Smart Markers
SmartMarkerProcessor smartMarkerProcessor = new SmartMarkerProcessor();
```

### الخطوة 2 – إدراج Smart Marker في الخلية A1

```csharp
// The marker ${Orders:ArrayAsSingle} tells the processor to write the whole array into one cell
Workbook workbook = new Workbook();
workbook.Worksheets[0].Cells["A1"].PutValue("${Orders:ArrayAsSingle}");
```

### الخطوة 3 – تعريف مصدر البيانات بمصفوفة على نمط JSON

```csharp
// Anonymous object that mimics a JSON array
var dataModel = new { Orders = new[] { "A", "B", "C" } };
```

### الخطوة 4 – معالجة المصنف

```csharp
// Fill the Smart Marker with the array data; the array becomes a comma‑separated string
smartMarkerProcessor.Process(workbook, dataModel);
```

### الخطوة 5 – حفظ المصنف الناتج

```csharp
// Persist the workbook; cell A1 now contains "A,B,C"
workbook.Save("YOUR_DIRECTORY/JsonSingleCell.xlsx");
```

**التحقق من النتيجة**: افتح `JsonSingleCell.xlsx` وتأكد من أن الخلية A1 تحتوي على `A,B,C`. يوضح هذا كيفية معالجة مجموعة كقيمة خلية واحدة، وهو نمط غالبًا ما يُحتاج إليه عند تصدير البيانات للأنظمة اللاحقة.

---

## مثال عملي كامل

فيما يلي برنامج واحد يجمع السيناريوهات الثلاثة. يمكنك نسخ الشيفرة إلى تطبيق Console، تعديل مسارات الملفات، وتشغيله لرؤية جميع المخرجات الثلاثة.

```csharp
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // 1. How to copy pivot table (preserve pivot cache)
        // -------------------------------------------------
        Workbook srcPivot = new Workbook("YOUR_DIRECTORY/Source.xlsx");
        Workbook dstPivot = new Workbook();
        srcPivot.Worksheets[0].Cells.CopyRows(0, 0, 20);
        srcPivot.Worksheets[0].Cells.CopyColumns(0, 0, 7);
        srcPivot.Worksheets[0].Copy(dstPivot.Worksheets[0]);
        dstPivot.Save("YOUR_DIRECTORY/CopyWithPivot.xlsx");

        // -------------------------------------------------
        // 2. Save workbook as PPTX with editable textbox
        // -------------------------------------------------
        Workbook txtWorkbook = new Workbook("YOUR_DIRECTORY/DocWithTextbox.xlsx");
        PptxSaveOptions pptxOpts = new PptxSaveOptions { ExportEditableTextBox = true };
        txtWorkbook.Save("YOUR_DIRECTORY/Result.pptx", pptxOpts);

        // -------------------------------------------------
        // 3. Export Smart Marker containing a JSON array
        // -------------------------------------------------
        SmartMarkerProcessor smProcessor = new SmartMarkerProcessor();
        Workbook smWorkbook = new Workbook();
        smWorkbook.Worksheets[0].Cells["A1"].PutValue("${Orders:ArrayAsSingle}");
        var model = new { Orders = new[] { "A", "B", "C" } };
        smProcessor.Process(smWorkbook, model);
        smWorkbook.Save("YOUR_DIRECTORY/JsonSingleCell.xlsx");
    }
}
```

تشغيل هذا البرنامج ينتج:

* `CopyWithPivot.xlsx` – نسخة مطابقة للجدول المحوري الأصلي.  
* `Result.pptx` – شريحة PowerPoint بصندوق نص قابل للتحرير.  
* `JsonSingleCell.xlsx` – ورقة يظهر فيها مصفوفة JSON في خلية واحدة.

---

## الخلاصة

أصبحت الآن تعرف **how to copy pivot table** بأمان، وكيفية **copy worksheet with pivot** في استدعاء واحد، وكيفية **save workbook as pptx** مع الحفاظ على صناديق النص القابلة للتحرير. تغطي هذه الأنماط أكثر سير عمل Excel‑to‑PowerPoint وExcel‑to‑JSON شيوعًا التي قد تواجهها في مشاريع أتمتة المؤسسات.

بعد ذلك، فكر في استكشاف:

* تحديث الجداول المحورية المنسوخة برمجيًا (`PivotTable.Refresh()`)  
* التصدير إلى صيغ أخرى مثل PDF أو HTML (`PdfSaveOptions`, `HtmlSaveOptions`)  
* استخدام خيارات Smart Marker المتقدمة مثل الدوال المخصصة أو التنسيق الشرطي  

لا تتردد في تجربة نطاقات مختلفة، أوراق عمل متعددة، أو هياكل JSON أكبر. توفر لك Aspose.Cells API تحكمًا دقيقًا، بحيث يمكنك تعديل هذه الأمثلة لأي سيناريو واقعي. برمجة سعيدة!

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مورد يتضمن أمثلة شيفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف نهج تنفيذ بديلة في مشاريعك.

- [إنشاء مصنف جديد – كيفية نسخ ورقة عمل مع جدول محوري](/cells/english/net/excel-copy-worksheet/create-new-workbook-how-to-copy-a-worksheet-with-a-pivot-tab/)
- [كيفية نسخ جدول محوري في C# – تحويل Excel إلى PPTX، نسخ نطاق وإضافة صندوق نص](/cells/english/net/pivot-tables/how-to-copy-pivot-table-in-c-convert-excel-to-pptx-copy-rang/)
- [نسخ أوراق داخل المصنف باستخدام Aspose.Cells for .NET - دليل خطوة بخطوة](/cells/english/net/worksheet-management/copy-sheets-within-workbook-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}