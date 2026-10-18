---
category: general
date: 2026-06-30
description: إنشاء مصنف إكسل باستخدام Aspose.Cells، تطبيق نمط جدول، حفظ كملف xlsx،
  تصدير الإكسل إلى PDF وتضمين الخطوط في PDF للحصول على مخرجات خالية من العيوب.
draft: false
keywords:
- create excel workbook
- apply table style
- save as xlsx
- export excel to pdf
- embed fonts pdf
language: ar
og_description: إنشاء مصنف إكسل باستخدام Aspose.Cells، تطبيق نمط جدول، حفظه كملف xlsx،
  تصديره إلى PDF وتضمين الخطوط في ملف PDF في دليل واحد سلس.
og_title: إنشاء مصنف إكسل – Aspose.Cells خطوة بخطوة
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Create excel workbook using Aspose.Cells, apply table style, save as
    xlsx, export excel to pdf and embed fonts pdf for flawless output.
  headline: Create Excel Workbook with Aspose.Cells – Full Guide
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
- PDF export
title: إنشاء دفتر عمل إكسل باستخدام Aspose.Cells – دليل كامل
url: /ar/net/excel-workbook/create-excel-workbook-with-aspose-cells-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء دفتر عمل Excel – دليل Aspose.Cells الكامل

هل حاولت يومًا **إنشاء دفتر عمل Excel** برمجيًا وصادفت صعوبة عندما كان الناتج بسيطًا أو فقد ملف PDF خطوطه؟ لست وحدك. في العديد من المشاريع الواقعية—مثل تقارير المبيعات الشهرية أو لوحات التحكم المالية الآلية—تحتاج إلى جدول بيانات مصقول **و** ملف PDF يحافظ على هوية العلامة التجارية للشركة.  

في هذا الدليل سنستعرض كل ما تحتاج معرفته: من إنشاء دفتر عمل جديد، إلى تنسيق البيانات كجدول صحيح، إلى حفظ الملف كـ **xlsx**، وأخيرًا **تصدير Excel إلى PDF** مع **تضمين الخطوط في PDF** للحصول على جودة أرشيفية مثالية. لا إطالة، مجرد حل قابل للتنفيذ يمكنك إدراجه في تطبيق .NET Console اليوم.

## المتطلبات المسبقة

قبل أن نبدأ، تأكد من وجود ما يلي:

- .NET 6‑or‑later SDK (الكود يعمل على .NET Core و .NET Framework على حد سواء)  
- Aspose.Cells for .NET مثبت (`dotnet add package Aspose.Cells`)  
- مجلد يمكنك الكتابة إليه (استبدل `YOUR_DIRECTORY` في المثال)  
- إلمام أساسي بـ C#—لا شيء معقد، فقط عبارات `using` المعتادة

هل لديك كل ذلك؟ رائع، لنبدأ.

## الخطوة 1: إنشاء دفتر عمل Excel وفتح ورقة العمل الأولى

أول شيء هو **إنشاء دفتر عمل Excel**. توفر لك Aspose.Cells فئة `Workbook` التي تبدأ بحالة ورقة عمل فارغة واحدة.

```csharp
using Aspose.Cells;
using System.Drawing;

void CreateWorkbook()
{
    // Step 1: Instantiate a new workbook (contains one empty worksheet)
    var workbook = new Workbook();

    // Grab the first worksheet so we can start populating it
    var worksheet = workbook.Worksheets[0];
    worksheet.Name = "SalesData";
```

لماذا نسمي الورقة فورًا؟ الاسم المعنوي يجعل الإشارات اللاحقة (مثل عندما تفتح الملف يدويًا) أوضح بكثير، خاصة إذا نما دفتر العمل إلى أكثر من ورقة.

## الخطوة 2: ملء الورقة ببيانات نموذجية

بعد ذلك نضيف أسماء الأشهر وأرقام الإيرادات. هذا يحاكي تقرير مبيعات شهري نموذجي.

```csharp
    // Header row
    worksheet.Cells["A1"].PutValue("Month");
    worksheet.Cells["B1"].PutValue("Revenue");

    // Sample data arrays
    string[] months   = { "Jan", "Feb", "Mar", "Apr", "May", "Jun" };
    double[] revenue  = { 12500, 15800, 14200, 16700, 19000, 21000 };

    // Populate rows
    for (int i = 0; i < months.Length; i++)
    {
        worksheet.Cells[i + 1, 0].PutValue(months[i]);   // Column A
        worksheet.Cells[i + 1, 1].PutValue(revenue[i]); // Column B
    }
```

لاحظ استخدام `PutValue`—فهو يستنتج نوع الخلية تلقائيًا، لذا تبقى الأرقام رقمية والنصوص نصًا. هذا مهم لاحقًا عندما نجمع عمود الإيرادات.

## الخطوة 3: تحويل النطاق إلى جدول و**تطبيق نمط الجدول**

النطاق العادي يبدو مملًا. تحويله إلى جدول Excel يمنحك تصفية مدمجة، وتنسيق تلقائي، وصف إجمالي بسطر واحد من الكود.

```csharp
    // Determine the used range (including header)
    int totalRows = months.Length + 1; // +1 for header

    // Add a ListObject (Excel table) that covers A1:B{totalRows}
    var tableIndex = worksheet.ListObjects.Add(0, 0, totalRows - 1, 1, true);
    var salesTable = worksheet.ListObjects[tableIndex];

    // Apply a built‑in style – this is where we **apply table style**
    salesTable.TableStyleType = TableStyleType.TableStyleMedium9;
```

`TableStyleMedium9` هو نمط رمادي مخطط نظيف يعمل جيدًا على الشاشة وعلى PDF المطبوع. يمكنك استبداله بأي من الأنماط المدمجة الـ70+؛ فقط غير قيمة الـ enum.

## الخطوة 4: إظهار صف الإجماليات الذي يجمع عمود الإيرادات

وجود مجموع في الأسفل مطلوب تقريبًا دائمًا في التقارير المالية.

```csharp
    // Enable the totals row
    salesTable.ShowTotals = true;

    // Set the second column (Revenue) to calculate a SUM
    salesTable.Columns[1].TotalsCalculation = TotalsCalculationType.Sum;
```

تقوم Aspose.Cells بالعمل الشاق—لا حاجة لكتابة صيغة منفصلة. سيتحدث صف الإجماليات تلقائيًا إذا قمت بتعديل البيانات لاحقًا.

## الخطوة 5: **حفظ كـ XLSX** – تنسيق Excel الأصلي

الآن بعد أن أصبحت الورقة جيدة المظهر، نقوم بحفظها كملف Excel مناسب.

```csharp
    // Step 5: Save the workbook as an XLSX file
    workbook.Save("YOUR_DIRECTORY/SalesReport.xlsx", SaveFormat.Xlsx);
```

لماذا نستخدم `SaveFormat.Xlsx` صراحةً؟ لأنه يضمن توافق الملف مع معيار Office Open XML، وهو أمر أساسي إذا كانت الأدوات اللاحقة تتوقع ملف `.xlsx` حديث.

## الخطوة 6: **تصدير Excel إلى PDF** مع **تضمين الخطوط في PDF**

إنشاء PDF سهل، لكن ضمان أن يكون PDF جاهزًا للأرشفة (PDF/A‑1b) وأن جميع الخطوط مضمَّنة يتطلب بعض الخيارات.

```csharp
    // Step 6: Export to PDF with PDF/A‑1b compliance and embed Windows fonts
    var pdfOptions = new PdfSaveOptions
    {
        Compliance = PdfCompliance.PdfA1b,          // PDF/A‑1b for long‑term preservation
        EmbedStandardWindowsFonts = true           // This **embed fonts pdf** flag
    };

    workbook.Save("YOUR_DIRECTORY/SalesReport.pdf", pdfOptions);
}
```

إعداد `PdfCompliance.PdfA1b` يجبر الناتج على الالتزام بمواصفات PDF/A‑1b—مثالي للأرشفة القانونية أو التنظيمية. في الوقت نفسه، `EmbedStandardWindowsFonts = true` يضمن أن خطوط Calibri و Arial وغيرها من الخطوط الافتراضية تُضمَّن داخل PDF، بحيث يبدو المستند متطابقًا على أي جهاز.

### الكود الكامل (جاهز للنسخ واللصق)

```csharp
using Aspose.Cells;
using System.Drawing;

void CreateWorkbook()
{
    // Step 1: Create a new workbook (contains one empty worksheet)
    var workbook = new Workbook();

    // Step 2: Get the first worksheet and give it a meaningful name
    var worksheet = workbook.Worksheets[0];
    worksheet.Name = "SalesData";

    // Step 3: Populate the worksheet with sample month and revenue data
    worksheet.Cells["A1"].PutValue("Month");
    worksheet.Cells["B1"].PutValue("Revenue");
    string[] months = { "Jan", "Feb", "Mar", "Apr", "May", "Jun" };
    double[] revenue = { 12500, 15800, 14200, 16700, 19000, 21000 };

    for (int i = 0; i < months.Length; i++)
    {
        worksheet.Cells[i + 1, 0].PutValue(months[i]);   // Column A
        worksheet.Cells[i + 1, 1].PutValue(revenue[i]); // Column B
    }

    // Step 4: Convert the data range into an Excel table and **apply table style**
    int totalRows = months.Length + 1;
    var tableIdx = worksheet.ListObjects.Add(0, 0, totalRows - 1, 1, true);
    var salesTable = worksheet.ListObjects[tableIdx];
    salesTable.TableStyleType = TableStyleType.TableStyleMedium9;

    // Step 5: Show a total row that sums the Revenue column
    salesTable.ShowTotals = true;
    salesTable.Columns[1].TotalsCalculation = TotalsCalculationType.Sum;

    // Step 6: **Save as xlsx** – the native Excel format
    workbook.Save("YOUR_DIRECTORY/SalesReport.xlsx", SaveFormat.Xlsx);

    // Step 7: **Export excel to pdf** with **embed fonts pdf**
    var pdfOptions = new PdfSaveOptions
    {
        Compliance = PdfCompliance.PdfA1b,
        EmbedStandardWindowsFonts = true
    };
    workbook.Save("YOUR_DIRECTORY/SalesReport.pdf", pdfOptions);
}
```

## النتيجة المتوقعة

- **SalesReport.xlsx** – افتحه في Excel وسترى جدولًا مُنسقًا بشكل جميل (خطوط رمادية، أسهم تصفية، وصف إجمالي يُظهر مجموع عمود Revenue).  
- **SalesReport.pdf** – عند فتح PDF، سيطابق تخطيط الجدول عرض Excel تمامًا. الخطوط مضمَّنة، لذا حتى على جهاز لا يحتوي على Calibri يبقى النص واضحًا. تم تعليم PDF كـ PDF/A‑1b، ويمكنك التحقق من ذلك في Adobe Acrobat تحت *File → Properties → Description*.

## الأسئلة المتكررة (وإجابات سريعة)

**ماذا لو احتجت نمط جدول مختلف؟**  
فقط غيّر `TableStyleMedium9` إلى أي قيمة أخرى من تعداد `TableStyleType`، مثل `TableStyleLight1` للحصول على مظهر أنظف.

**هل يمكنني إضافة أوراق عمل إضافية قبل الحفظ؟**  
بالتأكيد. استدعِ `workbook.Worksheets.Add("AnotherSheet")` وكرر خطوات تعبئة البيانات.

**هل يجب أن أضمّن الخطوط للامتثال لـ PDF/A؟**  
مواصفة PDF/A‑1b تتطلب تضمين جميع الخطوط. ضبط `EmbedStandardWindowsFonts = true` يفي بهذا المتطلب للخطوط النظامية الافتراضية. بالنسبة للخطوط المخصصة، يجب تحميلها أولًا في مجموعة خطوط المستند.

**هل الكود متوافق مع .NET Framework 4.5؟**  
نعم—Aspose.Cells يدعم .NET Framework 4.0 وما فوق، لذا يمكن تشغيل المقتطف نفسه دون تغييرات.

## الخلاصة

أنت الآن تعرف كيف **إنشاء دفتر عمل Excel** باستخدام Aspose.Cells، **تطبيق نمط الجدول**، **حفظ كـ xlsx**، و**تصدير Excel إلى PDF** مع **تضمين الخطوط في PDF** للحصول على مخرجات موثوقة ومتوافقة مع المعايير. يغطي هذا التدفق الشامل معظم الجوانب الأساسية.

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مورد يتضمن أمثلة كود كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك الخاصة.

- [Create and Save Excel Workbook as PDF in ASP.NET Using Aspose.Cells](/cells/english/net/workbook-operations/create-save-excel-workbook-pdf-aspnet-aspose-cells/)
- [Create Save Excel Workbook Pdf Aspnet Aspose Cells](/cells/german/net/workbook-operations/create-save-excel-workbook-pdf-aspnet-aspose-cells/)
- [Create Save Excel Workbook Pdf Aspnet Aspose Cells](/cells/french/net/workbook-operations/create-save-excel-workbook-pdf-aspnet-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}