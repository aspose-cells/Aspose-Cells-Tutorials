---
category: general
date: 2026-05-04
description: كيفية تضمين الخطوط عند تحويل مصنف Excel إلى PDF باستخدام C#. تعلّم حفظ
  المصنف كملف PDF مع تضمين الخطوط القياسية وتجنّب مشاكل الخطوط المفقودة.
draft: false
keywords:
- how to embed fonts
- save workbook as pdf
- convert excel to pdf
- export spreadsheet to pdf
- how to save pdf
language: ar
og_description: كيفية تضمين الخطوط عند تحويل مصنف Excel إلى PDF باستخدام C#. يوضح
  هذا الدليل الكود الكامل، ويشرح لماذا يُعد التضمين مهمًا، ويغطي الأخطاء الشائعة.
og_title: كيفية تضمين الخطوط في PDF – حفظ المصنف كملف PDF في C#
tags:
- C#
- Aspose.Cells
- PDF generation
title: كيفية تضمين الخطوط في PDF – حفظ المصنف كملف PDF في C#
url: /ar/net/conversion-to-pdf/how-to-embed-fonts-in-pdf-save-workbook-as-pdf-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تضمين الخطوط في PDF – حفظ دفتر العمل كملف PDF في C#

هل تساءلت يومًا **كيف يتم تضمين الخطوط** عند تصدير جدول بيانات Excel إلى PDF؟ أنت لست وحدك. يواجه العديد من المطورين تحذير "الخط مفقود" المخيف بعد حفظ دفتر العمل كملف PDF، فقط ليكتشفوا أن الملف النهائي يبدو غير صحيح على جهاز آخر.  

الخبر السار هو أن الحل بسيط إلى حد كبير باستخدام Aspose.Cells for .NET. في هذا الدرس سنستعرض الخطوات الدقيقة **لحفظ دفتر العمل كملف PDF** مع تضمين الخطوط القياسية، وسنتطرق أيضًا إلى **convert excel to pdf**، **export spreadsheet to pdf**، وحتى نجيب على **how to save pdf** مع الخيارات الصحيحة. في النهاية ستحصل على مثال كامل قابل للتنفيذ يمكنك إدراجه في أي مشروع C#.

## المتطلبات المسبقة

قبل أن نبدأ، تأكد من أن لديك:

* .NET 6 أو أحدث (الكود يعمل أيضًا على .NET Framework 4.7+)  
* ترخيص صالح لـ Aspose.Cells for .NET (الإصدار التجريبي المجاني يعمل، لكن الترخيص يزيل العلامات المائية للتقييم)  
* Visual Studio 2022 أو أي بيئة تطوير تفضلها  
* فهم أساسي لصياغة C# – إذا كنت تستطيع كتابة “Hello World”، فأنت جاهز للانطلاق  

إذا كان أي من هذه غير مألوف لك، خذ لحظة لتجهيزها؛ باقي الدليل يفترض أنها موجودة بالفعل.

## الخطوة 1: إضافة حزمة Aspose.Cells عبر NuGet

أولاً، تحتاج إلى المكتبة التي تتعامل فعليًا مع ملفات Excel. افتح وحدة تحكم NuGet في مشروعك وشغّل الأمر التالي:

```powershell
Install-Package Aspose.Cells
```

هذا السطر الواحد يجلب لك كل ما تحتاجه، بما في ذلك الفئات `Workbook` و `PdfSaveOptions` التي سنستخدمها لاحقًا.  

*نصيحة محترف:* إذا كنت تستخدم خط أنابيب CI/CD، قم بتثبيت نسخة محددة من الحزمة (مثال، `Aspose.Cells -Version 24.9`) لتجنب التغييرات المفاجئة التي قد تكسر عملك.

## الخطوة 2: إنشاء أو تحميل دفتر عمل

الآن إما ننشئ دفتر عمل جديد تمامًا أو نحمل ملف `.xlsx` موجود. للشرح، لننشئ ورقة بسيطة تحتوي على بضع صفوف من البيانات.

```csharp
using Aspose.Cells;

namespace PdfExportDemo
{
    class Program
    {
        static void Main()
        {
            // Step 2: Create a fresh workbook (or replace with Workbook("input.xlsx"))
            Workbook workbook = new Workbook();

            // Populate the first worksheet with sample data
            Worksheet sheet = workbook.Worksheets[0];
            sheet.Cells["A1"].PutValue("Product");
            sheet.Cells["B1"].PutValue("Quantity");
            sheet.Cells["A2"].PutValue("Apples");
            sheet.Cells["B2"].PutValue(120);
            sheet.Cells["A3"].PutValue("Oranges");
            sheet.Cells["B3"].PutValue(85);
```

لقد أنشأنا للتو قائمة جرد صغيرة. إذا كان لديك ملف Excel بالفعل، استبدل استدعاء `new Workbook()` بـ `new Workbook("path/to/file.xlsx")` وتخطى كتلة إدخال البيانات.

## الخطوة 3: تكوين خيارات حفظ PDF لتضمين الخطوط القياسية

هنا يحدث السحر. بشكل افتراضي قد يشير Aspose.Cells إلى خطوط النظام بدلاً من تضمينها، مما يؤدي إلى مشكلة “الخط غير موجود” على أجهزة أخرى. ضبط `EmbedStandardFonts` على `true` يجبر كاتب PDF على تضمين أكثر الخطوط شيوعًا (Arial، Times New Roman، إلخ).

```csharp
            // Step 3: Set PDF options – embed standard fonts for portability
            PdfSaveOptions pdfOptions = new PdfSaveOptions
            {
                // Ensures that fonts like Arial, Times New Roman are embedded
                EmbedStandardFonts = true,

                // Optional: keep the original layout (no scaling)
                OnePagePerSheet = false
            };
```

**لماذا نضمّن الخطوط؟** تخيل أنك ترسل PDF إلى زميل لا يمتلك سوى Helvetica. بدون التضمين، يلجأ عارضه إلى بديل، مما يغيّر شكل الجداول ويكسر التصميم. التضمين يضمن أن يظهر PDF بنفس الشكل على جميع الأجهزة.

## الخطوة 4: حفظ دفتر العمل كملف PDF

أخيرًا، نستدعي `Save` ونحدد مسار المجلد الوجهة. الطريقة تقبل مسار الملف والخيارات التي قمنا بتكوينها للتو.

```csharp
            // Step 4: Save the workbook as a PDF with embedded fonts
            string outputPath = @"C:\Temp\InventoryReport.pdf";
            workbook.Save(outputPath, pdfOptions);

            // Let the user know we’re done
            Console.WriteLine($"PDF saved successfully to {outputPath}");
        }
    }
}
```

شغّل البرنامج، وستجد `InventoryReport.pdf` في `C:\Temp`. افتحه على أي جهاز—ستبقى الخطوط في مكانها، والجداول متراصة، والتخطيط مطابق لورقة Excel الأصلية.

> **النتيجة المتوقعة:** يحتوي PDF على جدول ذو عمودين تمامًا كما هو موضح في Excel، مع تضمين Arial (أو الخط الافتراضي للنظام). لا تظهر تحذيرات الخط المفقود في Adobe Reader أو أي عارض آخر.

## الخطوة 5: التحقق من تضمين الخطوط (اختياري لكن مفيد)

إذا أردت التأكد من أن الخطوط فعلاً مضمّنة، افتح PDF في Adobe Acrobat وانتقل إلى **File → Properties → Fonts**. يجب أن ترى مدخلات مثل “ArialMT (Embedded Subset)”.

بدلاً من ذلك، يمكن استخدام أداة مجانية مثل **PDF‑Info** (`pdfinfo` على Linux) لعرض الخطوط المضمّنة من سطر الأوامر:

```bash
pdfinfo -meta InventoryReport.pdf | grep Font
```

رؤية كلمة “Embedded” بجانب كل خط مدرج يؤكد أنك نفذت العملية بشكل صحيح.

## حالات الحافة الشائعة وكيفية التعامل معها

| الحالة | ما الذي يجب فعله |
|-----------|------------|
| **خط الشركة المخصص** (مثال، `MyCompanySans`) | عيّن `PdfSaveOptions.CustomFonts = new string[] { @"C:\Fonts\MyCompanySans.ttf" };` واحتفظ بـ `EmbedStandardFonts = true`. |
| **دفتر عمل كبير (العديد من الأوراق)** | فعّل `PdfSaveOptions.OnePagePerSheet = true` لتجنب الصفحات الضخمة الصعبة القراءة. |
| **لم يتم تطبيق الترخيص** | الإصدار التجريبي يضيف علامة مائية. سجّل ترخيصك باستخدام `License license = new License(); license.SetLicense("Aspose.Cells.lic");` قبل إنشاء دفتر العمل. |
| **مخاوف الأداء** | أعد استخدام نسخة واحدة من `PdfSaveOptions` لعمليات حفظ متعددة، وفكّر في `PdfSaveOptions.Compression = PdfCompressionLevel.Maximum;` لتقليل حجم الملف. |

هذه التعديلات تحافظ على قوة خط أنابيب **convert excel to pdf** الخاص بك، مهما كان مصدر البيانات.

## الأسئلة المتكررة

**س: هل `EmbedStandardFonts` يضمّن أيضًا الخطوط غير القياسية؟**  
ج: لا. فهو يضمن فقط الخطوط الأساسية الـ14 في PDF. للخطوط المخصصة يجب توفيرها عبر مجموعة `CustomFonts` كما هو موضح أعلاه.

**س: هل سيزداد حجم PDF بشكل كبير؟**  
ج: تضمين عدد قليل من الخطوط القياسية يضيف فقط بضع كيلوبايت. إذا قمت بتضمين العديد من الخطوط المخصصة الكبيرة، توقع زيادة معتدلة — لا تزال أصغر بكثير من تضمين الصور بحجم كامل.

**س: هل يمكنني تضمين الخطوط عند استخدام مكتبات أخرى (مثل iTextSharp)؟**  
ج: بالطبع، لكن واجهة البرمجة تختلف. يركز هذا الدليل على Aspose.Cells لأنه يتعامل مع تحويل Excel إلى PDF في خطوة واحدة، مما يبسط سير عمل **export spreadsheet to pdf**.

## مثال كامل يعمل (جاهز للنسخ واللصق)

فيما يلي البرنامج الكامل، جاهز للترجمة. يتضمن جميع بيانات `using` اللازمة، ومقتطف الترخيص (معلق)، وتعليقات توضيحية مفصلة.

```csharp
using System;
using Aspose.Cells;

namespace PdfExportDemo
{
    class Program
    {
        static void Main()
        {
            // Uncomment and set the path if you have a license file
            // License lic = new License();
            // lic.SetLicense(@"C:\Path\To\Aspose.Cells.lic");

            // -------------------------------------------------
            // Step 1: Create or load a workbook
            // -------------------------------------------------
            Workbook workbook = new Workbook(); // Replace with new Workbook("input.xlsx") to load an existing file

            // -------------------------------------------------
            // Step 2: Populate sample data (optional)
            // -------------------------------------------------
            Worksheet sheet = workbook.Worksheets[0];
            sheet.Cells["A1"].PutValue("Product");
            sheet.Cells["B1"].PutValue("Quantity");
            sheet.Cells["A2"].PutValue("Apples");
            sheet.Cells["B2"].PutValue(120);
            sheet.Cells["A3"].PutValue("Oranges");
            sheet.Cells["B3"].PutValue(85);

            // -------------------------------------------------
            // Step 3: Configure PDF save options – embed fonts
            // -------------------------------------------------
            PdfSaveOptions pdfOptions = new PdfSaveOptions
            {
                EmbedStandardFonts = true, // <-- This is the key to how to embed fonts
                OnePagePerSheet = false,
                // Uncomment and set custom fonts if needed
                // CustomFonts = new string[] { @"C:\Fonts\MyCompanySans.ttf" }
            };

            // -------------------------------------------------
            // Step 4: Save the workbook as a PDF file
            // -------------------------------------------------
            string outputPath = @"C:\Temp\InventoryReport.pdf";
            workbook.Save(outputPath, pdfOptions);

            Console.WriteLine($"PDF saved successfully to {outputPath}");
        }
    }
}
```

احفظه باسم `Program.cs`، ابنِ المشروع، وشغّله. سيظهر PDF تمامًا في المكان الذي حددت فيه `outputPath`، مع الخطوط مضمّنة بثبات.

## الخلاصة

لقد غطينا **كيفية تضمين الخطوط** عند **حفظ دفتر العمل كملف PDF** باستخدام Aspose.Cells، استعرضنا كل سطر من الكود، وشرحنا لماذا يعتبر التضمين مهمًا لسير عمل **convert excel to pdf** موثوق. الآن تعرف كيف **تصدير جدول بيانات إلى PDF**، وتتحقق من التضمين، وتتعامل مع الحالات الشائعة مثل الخطوط المخصصة أو دفاتر العمل الكبيرة.  

بعد ذلك، قد ترغب في استكشاف إضافة رؤوس/تذييلات، حماية PDF بكلمة مرور، أو معالجة دفاتر عمل متعددة في تشغيل واحد. Each

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}