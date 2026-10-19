---
category: general
date: 2026-03-22
description: تعلم كيفية تصدير Excel إلى PowerPoint، وتحديد منطقة الطباعة في Excel،
  وحفظ Excel كملف PPTX مع مخططات قابلة للتعديل وكائنات OLE في بضع خطوات فقط.
draft: false
keywords:
- export excel to powerpoint
- set print area excel
- save excel as pptx
- editable charts PowerPoint
- OLE objects export
language: ar
og_description: تصدير Excel إلى PowerPoint بسرعة. يوضح هذا البرنامج التعليمي كيفية
  تحديد منطقة الطباعة في Excel وحفظ Excel كملف PPTX مع مخططات قابلة للتحرير وكائنات
  OLE.
og_title: تصدير إكسل إلى باوربوينت – دليل C# الكامل
tags:
- Aspose.Cells
- C#
- Office Automation
title: تصدير إكسل إلى باوربوينت – دليل C# الكامل
url: /ar/net/converting-excel-files-to-other-formats/export-excel-to-powerpoint-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تصدير Excel إلى PowerPoint – دليل C# كامل

هل تحتاج إلى **تصدير Excel إلى PowerPoint**؟ أنت في المكان الصحيح. سواء كنت تُعد عرض مبيعات أسبوعي أو تُؤتمت خط أنابيب تقارير، فإن تحويل ورقة عمل Excel إلى مجموعة شرائح PowerPoint يمكن أن يوفر لك ساعات من النسخ واللصق اليدوي.  

في هذا الدرس سنستعرض مثالًا عمليًا لا يقتصر فقط على **export excel to powerpoint**، بل يوضح لك أيضًا كيفية **set print area Excel** و **save excel as pptx** بحيث تبقى المخططات وكائنات OLE قابلة للتحرير بالكامل في الشرائح الناتجة. في النهاية ستحصل على برنامج C# جاهز للتنفيذ ينتج ملف `.pptx` احترافي دون أي تعديل يدوي.

## ما الذي ستحتاجه

- **.NET 6+** (أي بيئة تشغيل .NET حديثة؛ الكود يستخدم صsyntax C# 10)
- **Aspose.Cells for .NET** – المكتبة التي تُجري عملية التصدير. يمكنك الحصول عليها من NuGet (`Install-Package Aspose.Cells`).
- مصنف Excel يحتوي على مخطط واحد على الأقل و/أو كائن OLE (يُستخدم ملف العينة `ChartAndOle.xlsx` في الكود).
- بيئة تطوير مفضلة (Visual Studio، Rider، أو VS Code – ما تفضله).

هذا كل شيء. لا حاجة لتقنية COM interop، ولا يتطلب تثبيت Office.  

> **لماذا نستخدم مكتبة؟**  
> تقنية Office Interop المدمجة هشة، وتحتاج إلى Office على الخادم، وغالبًا ما تُنتج صورًا نقطية عندما تحتاج إلى أشكال قابلة للتحرير ومُعتمدة على المتجهات. Aspose.Cells تتولى الجزء الثقيل وتبقي كل شيء قابلًا للتحرير في PowerPoint.

---

## الخطوة 1: تحميل مصنف Excel  

أولًا نقوم بتحميل الملف المصدر إلى الذاكرة. فئة `Workbook` تمثل ملف Excel بالكامل، وتمنحنا الوصول إلى الأوراق، المخططات، وكائنات OLE.

```csharp
using Aspose.Cells;

try
{
    // Load the Excel file that contains the chart and OLE object.
    // Adjust the path to point to your own workbook.
    Workbook workbook = new Workbook(@"C:\MyProjects\ChartAndOle.xlsx");
}
catch (Exception ex)
{
    Console.WriteLine($"Failed to load workbook: {ex.Message}");
    return;
}
```

**لماذا هذا مهم:** تحميل المصنف هو الأساس. إذا كان المسار غير صحيح أو الملف تالفًا، فإن بقية العملية لن تعمل. كتلة `try…catch` تُظهر لك رسالة خطأ ودية بدلاً من تعطل البرنامج.

---

## الخطوة 2: تعيين منطقة الطباعة في Excel  

قبل التصدير، عادةً ما ترغب في حصر المخرجات على نطاق معين. هنا يأتي دور **set print area excel**. بتحديد منطقة الطباعة، تخبر Aspose.Cells بالخللايا (والكائنات المرتبطة) التي يجب أن تظهر على الشريحة.

```csharp
// Assuming we want to export only the range A1:H30 on the first worksheet.
Worksheet sheet = workbook.Worksheets[0];
sheet.PageSetup.PrintArea = "A1:H30";
```

> **نصيحة احترافية:** إذا كان لديك عدة أوراق عمل، كرّر تعيين `PrintArea` لكل ورقة تخطط لتصديرها. ترك منطقة الطباعة غير مُحددة سيؤدي إلى تصدير الورقة بأكملها، مما قد يثقل ملف PowerPoint.

---

## الخطوة 3: تكوين خيارات التصدير – الحفاظ على المخططات وOLE قابلة للتحرير  

توفر Aspose.Cells كائنًا غنيًا يُدعى `ImageOrPrintOptions`. من خلال تفعيل `ExportChartObjects` و `ExportOleObjects` نحافظ على طبيعة المخططات المتجهية وقابلية تحرير كائنات OLE (مثل مستندات Word أو PDF المدمجة).

```csharp
ImageOrPrintOptions pptExportOptions = new ImageOrPrintOptions
{
    SaveFormat = SaveFormat.Pptx,   // We want a PPTX, not a PNG or PDF.
    ExportChartObjects = true,      // Charts stay editable in PowerPoint.
    ExportOleObjects = true         // OLE objects remain live (you can double‑click to edit).
};
```

**ماذا يحدث خلف الكواليس؟**  
عند ضبط `ExportChartObjects` على `true`، تقوم Aspose بتحويل المخطط إلى شكل مخطط PowerPoint أصلي، مع الحفاظ على السلاسل والمحاور والتنسيق. وعند تفعيل `ExportOleObjects` تُدرج الكائنات المدمجة كإطارات OLE، بحيث يمكن النقر المزدوج عليها في PowerPoint لفتح التطبيق الأصلي (Word، Excel، إلخ) للتحرير.

---

## الخطوة 4: حفظ الورقة كملف PowerPoint قابل للتحرير  

الآن نجمع كل شيء معًا. طريقة `Save` تكتب ملف `.pptx` باستخدام الخيارات التي ضبطناها. النتيجة هي مجموعة شرائح حيث تتحول كل ورقة عمل إلى شريحة (أو سلسلة شرائح إذا امتدت منطقة الطباعة على عدة صفحات).

```csharp
// Save the first worksheet as an editable PowerPoint presentation.
workbook.Save(@"C:\MyProjects\EditableChartOle.pptx", pptExportOptions);
Console.WriteLine("Export completed! Check EditableChartOle.pptx.");
```

### النتيجة المتوقعة

- **موقع الملف:** `C:\MyProjects\EditableChartOle.pptx`
- **المحتوى:**  
  - شريحة تُظهر النطاق `A1:H30` تمامًا كما هو في Excel.  
  - جميع المخططات هي كائنات مخطط PowerPoint — انقر على عمود لتعديل البيانات.  
  - كائنات OLE (مثل مستند Word مدمج) يمكن فتحها وتحريرها مباشرة من الشريحة.

إذا فتحت ملف PPTX في PowerPoint، يجب أن ترى شريحة نظيفة بمكونات قابلة للتحرير بالكامل—بدون لقطات شاشة نقطية.

---

## الحالات الخاصة والبدائل  

### أوراق عمل متعددة → شرائح متعددة  
إذا أردت أن تتحول كل ورقة عمل إلى شريحة خاصة بها، ببساطة قم بالتكرار عبر `workbook.Worksheets` واستدعِ `Save` مع `SheetToImageOptions` تستهدف فهرس ورقة محدد. ستُنشئ Aspose شريحة جديدة تلقائيًا لكل تكرار.

```csharp
for (int i = 0; i < workbook.Worksheets.Count; i++)
{
    ImageOrPrintOptions opts = new ImageOrPrintOptions
    {
        SaveFormat = SaveFormat.Pptx,
        ExportChartObjects = true,
        ExportOleObjects = true,
        OnePagePerSheet = true   // Ensures each sheet starts on a new slide.
    };
    workbook.Save($"Sheet{i + 1}.pptx", opts);
}
```

### نطاقات كبيرة والأداء  
تصدير منطقة طباعة ضخمة (مثل `A1:Z1000`) قد يزيد من استهلاك الذاكرة. لتخفيف ذلك، ضع في اعتبارك:
- تقسيم النطاق إلى أجزاء أصغر وتصدير كل جزء كشريحة منفصلة.  
- استخدام `WorkbookSettings` لزيادة `MemorySetting` إذا واجهت `OutOfMemoryException`.

### قضايا التوافق  
ملف PPTX المُولد يعمل مع PowerPoint 2016 والإصدارات الأحدث. قد تفتح الإصدارات القديمة الملف ولكن قد تفقد بعض ميزات المخطط المتقدمة. اختبر دائمًا على نسخة Office المستهدفة إذا كنت ستوزع العرض على نطاق واسع.

---

## مثال كامل جاهز للتنفيذ (انسخه‑الصقه)

```csharp
// ---------------------------------------------------------------
// Export Excel to PowerPoint – Complete C# Example
// ---------------------------------------------------------------

using System;
using Aspose.Cells;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load the workbook.
            string excelPath = @"C:\MyProjects\ChartAndOle.xlsx";
            Workbook workbook;
            try
            {
                workbook = new Workbook(excelPath);
            }
            catch (Exception ex)
            {
                Console.WriteLine($"Error loading Excel file: {ex.Message}");
                return;
            }

            // 2️⃣ Set the print area (set print area excel).
            Worksheet sheet = workbook.Worksheets[0];
            sheet.PageSetup.PrintArea = "A1:H30";

            // 3️⃣ Configure export options – keep charts & OLE objects editable.
            ImageOrPrintOptions pptExportOptions = new ImageOrPrintOptions
            {
                SaveFormat = SaveFormat.Pptx,
                ExportChartObjects = true,
                ExportOleObjects = true
            };

            // 4️⃣ Save as PPTX (save excel as pptx).
            string pptxPath = @"C:\MyProjects\EditableChartOle.pptx";
            try
            {
                workbook.Save(pptxPath, pptExportOptions);
                Console.WriteLine($"Success! PPTX created at: {pptxPath}");
            }
            catch (Exception ex)
            {
                Console.WriteLine($"Failed to save PPTX: {ex.Message}");
            }
        }
    }
}
```

> **نصيحة:** استبدل المسارات الصلبة بقيم من ملف إعدادات أو وسائط سطر الأوامر للحصول على أداة أكثر مرونة.

---

## الأسئلة المتكررة  

**س: هل يمكنني تصدير مخطط فقط دون الخلايا المحيطة؟**  
ج: نعم. استخدم `ExportChartObjects` وحده وحدد منطقة الطباعة لتغطي نطاق المخطط فقط. سيظهر المخطط في وسط الشريحة.

**س: ماذا لو كان المصنف يحتوي على ماكرو؟**  
ج: Aspose.Cells يتجاهل ماكرو VBA أثناء التصدير. إذا كنت بحاجة إلى وظائف ماكرو في PowerPoint، سيتعين عليك إعادة إنشائها باستخدام VBA الخاص بـ PowerPoint أو الإضافات.

**س: هل يعمل هذا على Linux/macOS؟**  
ج: بالتأكيد. Aspose.Cells مكتبة .NET صافية؛ طالما لديك بيئة تشغيل .NET، يعمل الكود عبر الأنظمة.

---

## الخلاصة  

لقد تعلمت الآن كيفية **export Excel to PowerPoint** مع ضبط **set print area excel** و **save excel as pptx** مع مخططات وكائنات OLE قابلة للتحرير بالكامل. الخطوات الأساسية هي تحميل المصنف، تعريف منطقة الطباعة، تكوين `ImageOrPrintOptions`، وأخيرًا حفظ ملف PPTX.  

من هنا يمكنك استكشاف:
- تصدير أوراق عمل متعددة إلى مجموعة شرائح واحدة.  
- إضافة عناوين شرائح أو ملاحظات مخصصة برمجيًا.  
- تحويل PPTX إلى PDF للتوزيع (استخدم `SaveFormat.Pdf`).  

جرّب الكود، عدّل منطقة الطباعة، وشاهد بيانات Excel تتحول سحريًا إلى PowerPoint—دون الحاجة إلى نسخ‑لصق يدوي. إذا واجهت أي صعوبات، راجع وثائق Aspose.Cells أو اترك تعليقًا أدناه. برمجة سعيدة!  

![مخطط يوضح سير عمل تصدير excel إلى powerpoint](/images/export-excel-to-powerpoint.png "export excel to powerpoint workflow")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}