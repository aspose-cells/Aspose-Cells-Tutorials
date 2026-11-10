---
category: general
date: 2026-10-20
description: انسخ جدول المحور إلى مصنف جديد باستخدام Aspose.Cells وتعلم كيفية تصدير
  شكل قابل للتعديل إلى PowerPoint في دليل واحد.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy pivot table to new workbook
- copy rows between worksheets
- Aspose.Cells copy rows
- export shape to PowerPoint
- editable textbox in PowerPoint
language: ar
lastmod: 2026-10-20
og_description: نسخ جدول محوري إلى مصنف جديد باستخدام Aspose.Cells وتصدير شكل قابل
  للتحرير إلى PowerPoint — كود خطوة بخطوة يمكنك تشغيله اليوم.
og_image_alt: Screenshot showing copy pivot table to new workbook using Aspose.Cells
og_title: نسخ جدول محوري إلى مصنف جديد، تصدير الشكل إلى PowerPoint
schemas:
- author: Aspose
  dateModified: '2026-10-20'
  description: Copy pivot table to new workbook using Aspose.Cells and learn how to
    export an editable shape to PowerPoint in a single guide.
  headline: Copy pivot table to new workbook, export shape to PowerPoint
  type: TechArticle
- description: Copy pivot table to new workbook using Aspose.Cells and learn how to
    export an editable shape to PowerPoint in a single guide.
  name: Copy pivot table to new workbook, export shape to PowerPoint
  steps:
  - name: – Load the source workbook and select the first worksheet
    text: '```csharp // Load the workbook that already contains the pivot table Workbook
      srcWorkbook = new Workbook("YOUR_DIRECTORY/Source.xlsx");'
  - name: – Define the cell area that includes the pivot table
    text: '```csharp // CellArea(startRow, startColumn, endRow, endColumn) // Here
      we copy rows 0‑20 and columns 0‑10, which covers the whole pivot table CellArea
      sourceArea = new CellArea(0, 0, 20, 10); ```'
  - name: – Create the destination workbook and get its first worksheet
    text: '```csharp // Create an empty workbook that will receive the copied range
      Workbook destWorkbook = new Workbook();'
  - name: – Copy the rows from the source area to the destination sheet
    text: '```csharp // CopyRows(startRow, endRow, destinationCells, destinationStartRow)
      srcWorksheet.Cells.CopyRows( sourceArea.StartRow, sourceArea.EndRow, destWorksheet.Cells,
      0); // start at row 0 in the destination sheet ```'
  - name: – Save the new workbook
    text: '```csharp destWorkbook.Save("YOUR_DIRECTORY/CopyWithPivot.xlsx"); ```'
  - name: – Create a new workbook and access its first worksheet
    text: '```csharp Workbook workbook = new Workbook(); // Empty workbook Worksheet
      worksheet = workbook.Worksheets[0]; // First (and only) sheet ```'
  - name: – Add a textbox shape to the worksheet
    text: '```csharp // AddTextBox(startRow, startColumn, width, height, text) int
      shapeIndex = worksheet.Shapes.AddTextBox(10, 10, 200, 50, "Editable text");
      ```'
  - name: – Retrieve the shape and modify its text
    text: '```csharp Shape textShape = worksheet.Shapes[shapeIndex]; textShape.Text
      = "Change me in PowerPoint"; ```'
  - name: – Save the workbook as a PowerPoint presentation
    text: '```csharp workbook.Save("YOUR_DIRECTORY/Presentation.pptx", SaveFormat.Pptx);
      ```'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Pivot Table
- PowerPoint Export
title: نسخ جدول محوري إلى مصنف جديد، تصدير الشكل إلى PowerPoint
url: /ar/net/pivot-tables/copy-pivot-table-to-new-workbook-export-shape-to-powerpoint/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# نسخ جدول محوري إلى مصنف جديد، وتصدير الشكل إلى PowerPoint

إذا كنت بحاجة إلى **copy pivot table to new workbook** مع الحفاظ على وظيفتها، يوضح لك هذا الدليل بالضبط كيفية القيام بذلك باستخدام Aspose.Cells. سترى أيضًا أسرع طريقة لـ **export an editable shape to PowerPoint**، بحيث يبقى مربع النص قابلاً للتحرير بعد التحويل.

يفترض العديد من المطورين أن نسخ نطاق يحتوي على جدول محوري سيفقد منطق الجدول المحوري، أو أن الأشكال تصبح صورًا ثابتة عند حفظها كملف PPTX. ينفي هذا البرنامج التعليمي تلك الأساطير ويقدم لك حلاً موثوقًا وجاهزًا للإنتاج.

في الأقسام التالية سوف:

* تحميل مصنف المصدر ونسخ نطاق يتضمن جدولًا محوريًا.
* إنشاء مصنف وجهة يحتوي على نفس الجدول المحوري.
* إضافة شكل مربع نص، تعديل نصه، وحفظ المصنف كعرض تقديمي PowerPoint حيث يبقى مربع النص قابلاً للتحرير.
* فهم سبب ضرورة كل استدعاء API وكيفية تجنب المشكلات الشائعة.

**Prerequisites**

* .NET 6.0 أو أحدث (الكود يعمل أيضًا مع .NET Framework 4.7+).
* Aspose.Cells for .NET مثبت (`Install-Package Aspose.Cells`).
* معرفة أساسية بـ C# و Visual Studio (أو أي بيئة تطوير تفضلها).

---

## نسخ جدول محوري إلى مصنف جديد

هذا القسم خطوة بخطوة يوضح كيفية نسخ نطاق يحتوي على جدول محوري والاحتفاظ بتعريف الجدول المحوري في الملف الجديد.

### Step 1 – Load the source workbook and select the first worksheet

```csharp
// Load the workbook that already contains the pivot table
Workbook srcWorkbook = new Workbook("YOUR_DIRECTORY/Source.xlsx");

// The first worksheet (index 0) holds the pivot table we want to copy
Worksheet srcWorksheet = srcWorkbook.Worksheets[0];
```

*لماذا؟*  
`Workbook` هو نقطة الدخول لأي تعديل على Excel في Aspose.Cells. اختيار الورقة الصحيحة يضمن أننا نتعامل مع موقع الجدول المحوري بالضبط.

### Step 2 – Define the cell area that includes the pivot table

```csharp
// CellArea(startRow, startColumn, endRow, endColumn)
// Here we copy rows 0‑20 and columns 0‑10, which covers the whole pivot table
CellArea sourceArea = new CellArea(0, 0, 20, 10);
```

*لماذا؟*  
الجدول المحوري موجود داخل مجموعة محددة من الخلايا. بتحديد `CellArea` يغطي الجدول بالكامل، يتعرف Aspose.Cells على ضرورة نسخ ذاكرة التخزين المؤقت للجدول المحوري أيضًا.

### Step 3 – Create the destination workbook and get its first worksheet

```csharp
// Create an empty workbook that will receive the copied range
Workbook destWorkbook = new Workbook();

// Destination worksheet (also index 0)
Worksheet destWorksheet = destWorkbook.Worksheets[0];
```

*لماذا؟*  
مصنف جديد يضمن عدم وجود نطاقات مسماة متضاربة أو جداول محورية موجودة، مما يجعل عملية النسخ نظيفة.

### Step 4 – Copy the rows from the source area to the destination sheet

```csharp
// CopyRows(startRow, endRow, destinationCells, destinationStartRow)
srcWorksheet.Cells.CopyRows(
    sourceArea.StartRow,
    sourceArea.EndRow,
    destWorksheet.Cells,
    0); // start at row 0 in the destination sheet
```

*لماذا؟*  
`CopyRows` هو جزء من **Aspose.Cells copy rows** API. ينسخ قيم الخلايا وذاكرة التخزين المؤقت المخفية للجدول المحوري، لذا يبقى الجدول المحوري فعالًا بعد النقل.

### Step 5 – Save the new workbook

```csharp
destWorkbook.Save("YOUR_DIRECTORY/CopyWithPivot.xlsx");
```

*Result*  
افتح `CopyWithPivot.xlsx` في Excel. يظهر الجدول المحوري تمامًا كما كان في الملف الأصلي، ويمكنك تحديثه أو تعديلّه بشكل طبيعي.

---

## Export editable shape to PowerPoint

الآن سنضيف شكل مربع نص، نغيّر محتواه، ونحفظ المصنف كملف PPTX. يبقى الشكل قابلًا للتحرير بالكامل عند فتحه في PowerPoint.

### Step 1 – Create a new workbook and access its first worksheet

```csharp
Workbook workbook = new Workbook();          // Empty workbook
Worksheet worksheet = workbook.Worksheets[0]; // First (and only) sheet
```

### Step 2 – Add a textbox shape to the worksheet

```csharp
// AddTextBox(startRow, startColumn, width, height, text)
int shapeIndex = worksheet.Shapes.AddTextBox(10, 10, 200, 50, "Editable text");
```

*لماذا؟*  
`AddTextBox` ينشئ **editable textbox in PowerPoint**‑compatible shape. الإحداثيات بوحدات النقاط؛ عدّلها لتناسب تخطيطك.

### Step 3 – Retrieve the shape and modify its text

```csharp
Shape textShape = worksheet.Shapes[shapeIndex];
textShape.Text = "Change me in PowerPoint";
```

*لماذا؟*  
الوصول المباشر إلى كائن `Shape` يتيح لك تغيير خصائص مثل `Text` أو `Font` أو `Fill`. يوضح هذا الخطوة كيفية تعيين المحتوى الأولي برمجيًا.

### Step 4 – Save the workbook as a PowerPoint presentation

```csharp
workbook.Save("YOUR_DIRECTORY/Presentation.pptx", SaveFormat.Pptx);
```

*Result*  
افتح `Presentation.pptx` في Microsoft PowerPoint. يظهر مربع النص في الشريحة الأولى، ويمكنك النقر المزدوج لتعديل النص كما هو الحال مع أي شكل أصلي في PowerPoint.

---

## Expected output

| File | What you’ll see |
|------|-----------------|
| `CopyWithPivot.xlsx` | ورقة عمل تحتوي على الجدول المحوري الأصلي، تعمل بالكامل (التحديث يعمل). |
| `Presentation.pptx` | شريحة واحدة بها مربع نص قابل للتحرير يحتوي على النص “Change me in PowerPoint”. |

---

## Common pitfalls and best‑practice tips

* **Pivot cache loss** – إذا قمت بنسخ قيم الخلايا فقط (مثلاً باستخدام `CopyRows` مع تعيين علم `PasteOptions` إلى `PasteValues`)، يتم حذف ذاكرة التخزين المؤقت للجدول المحوري ويصبح الجدول ثابتًا. استخدم دائمًا النسخة الافتراضية من `CopyRows` كما هو موضح.
* **Shape positioning** – `AddTextBox` يستخدم وحدات النقاط، وليس مؤشرات خلايا Excel. اختبر الإحداثيات على ملف تجريبي لتجنب وضع الشكل خارج الشريحة.
* **File format mismatch** – حفظ المصنف كـ PPTX باستخدام `SaveFormat.Pptx` يحول جميع الأشكال المدعومة تلقائيًا. محاولة الحفظ كـ `Pdf` ستحول الشكل إلى صورة نقطية، مما يجعله غير قابل للتحرير.

---

## Conclusion

أنت الآن تعرف كيف **copy pivot table to new workbook** وكيف **export an editable shape to PowerPoint** باستخدام Aspose.Cells for .NET. تغطي أمثلة الشيفرة الكاملة والقابلة للتنفيذ كل استدعاء API مطلوب، وتشرح سبب أهمية كل خطوة، وتظهر النتائج المتوقعة.

بعد ذلك، قد ترغب في استكشاف:

* **Working with charts** – نسخ المخططات مع الجداول المحورية (`Aspose.Cells copy rows between worksheets`).
* 

## What Should You Learn Next?

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مورد يتضمن أمثلة شيفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [إنشاء مصنف جديد – كيفية نسخ ورقة عمل تحتوي على جدول محوري](/cells/english/net/excel-copy-worksheet/create-new-workbook-how-to-copy-a-worksheet-with-a-pivot-tab/)
- [نسخ جدول محوري وتصدير Excel إلى PPTX باستخدام Aspose.Cells](/cells/english/net/converting-excel-files-to-other-formats/copy-pivot-table-and-export-excel-to-pptx-with-aspose-cells/)
- [إنشاء مصنف جديد في C# – نسخ جدول محوري](/cells/english/net/pivot-tables/create-new-workbook-in-c-copy-pivot-table/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}