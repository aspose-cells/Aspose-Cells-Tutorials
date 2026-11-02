---
category: general
date: 2026-07-03
description: كيفية تمكين الخطوط أثناء تحويل Excel إلى XPS باستخدام Aspose.Cells. تعلّم
  الإعداد خطوة بخطوة، والكود، والنصائح للحفاظ على الخطوط بلا عيوب.
draft: false
keywords:
- how to enable fonts
- convert excel to xps
- Aspose.Cells XPS export
- preserve font variations
- C# Excel automation
language: ar
og_description: كيفية تمكين الخطوط في تحويل Excel إلى XPS. اتبع هذا الدليل للحصول
  على مثال C# يعمل يحافظ على تنوع الخطوط.
og_title: كيفية تمكين الخطوط عند تحويل Excel إلى XPS – دليل كامل
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: How to enable fonts while you convert Excel to XPS using Aspose.Cells.
    Learn step‑by‑step setup, code, and tips for flawless font preservation.
  headline: How to Enable Fonts When Converting Excel to XPS – Complete Guide
  type: TechArticle
- description: How to enable fonts while you convert Excel to XPS using Aspose.Cells.
    Learn step‑by‑step setup, code, and tips for flawless font preservation.
  name: How to Enable Fonts When Converting Excel to XPS – Complete Guide
  steps:
  - name: What Does `FontVariationSelectors = true` Actually Do?
    text: '- **Preserves custom weight & style variations** (e.g., a font that supports
      multiple thicknesses via OpenType features). - **Ensures the XPS viewer renders
      the exact glyphs** you see in Excel, rather than falling back to a generic font.
      - **Adds a small overhead** to the file size because the selec'
  - name: Expected Result
    text: '- The file `WithSelectors.xps` will appear in the target folder. - Open
      it in any XPS viewer (e.g., Windows XPS Viewer or Edge). - You should see the
      same font weights, italics, and any custom OpenType variations that were present
      in the original Excel file.'
  - name: Next Steps
    text: '- Experiment with other `XpsSaveOptions` properties like `Compress` or
      `EmbedStandardFonts`. - Try converting to PDF first, then to XPS, to compare
      file sizes and fidelity. - Dive into Aspose.Cells’ **image handling** (`ImageOrPrintOptions`)
      if your workbook contains charts or pictures you also need'
  type: HowTo
tags:
- Aspose.Cells
- C#
- XPS
- Excel
title: كيفية تمكين الخطوط عند تحويل Excel إلى XPS – دليل كامل
url: /ar/net/xps-and-pdf-operations/how-to-enable-fonts-when-converting-excel-to-xps-complete-gu/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تمكين الخطوط عند تحويل Excel إلى XPS – دليل كامل

هل تساءلت يومًا **كيف يتم تمكين الخطوط** حتى يبدو تحويل Excel‑to‑XPS مطابقة تمامًا للدفتر الأصلي؟ لست وحدك. يواجه العديد من المطورين مشكلة عندما يزيل ملف XPS الناتج تنوعات الخطوط المخصصة، مما يجعل المستند يبدو باهتًا.  

في هذا الدرس سنستعرض حلًا عمليًا لا يوضح فقط **كيف يتم تمكين الخطوط** بل يُظهر أيضًا أفضل طريقة لـ **تحويل Excel إلى XPS** باستخدام Aspose.Cells. في النهاية ستحصل على مقطع C# جاهز للتنفيذ، شرح واضح لكل إعداد، وبعض النصائح الاحترافية لضمان أن يكون إخراج XPS مثاليًا بالبكسل.

## ما ستحتاجه

قبل أن نبدأ، تأكد من وجود التالي:

- **Aspose.Cells for .NET** (أحدث إصدار حتى 2026‑07).  
- بيئة تطوير .NET (Visual Studio 2022 أو VS Code مع امتداد C# تعمل بشكل جيد).  
- دفتر Excel (`VariationFont.xlsx`) يحتوي على محددات تنوع الخط التي تريد الحفاظ عليها.  

هذا كل شيء—لا حزم NuGet إضافية، لا تعقيدات COM interop، مجرد C# بسيط.

![مخطط يوضح التدفق من دفتر Excel إلى مستند XPS – كيفية تمكين الخطوط أثناء التحويل](https://example.com/images/enable-fonts-xps.png "كيفية تمكين الخطوط في تحويل Excel إلى XPS")

## الخطوة 1: إعداد المشروع واستيراد المساحات الاسمية

أولاً، أنشئ تطبيق console جديد (أو أدمجه في حل موجود). أضف مرجع Aspose.Cells عبر NuGet:

```bash
dotnet add package Aspose.Cells
```

ثم، استورد المساحات الاسمية الضرورية:

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Drawing;   // optional, for advanced graphics handling
```

> **نصيحة احترافية:** إذا كنت تستهدف .NET 6+، يمكنك استخدام ميزة `global using` الضمنية للحفاظ على ملفاتك مرتبة.

## الخطوة 2: تحميل دفتر Excel

تحميل الدفتر هو الأساس؛ بدون كائن `Workbook` صحيح لا يمكنك تعديل أي خيارات حفظ.

```csharp
// Step 2: Load the Excel workbook you want to convert
Workbook workbook = new Workbook("YOUR_DIRECTORY/VariationFont.xlsx");

// Quick sanity check – make sure at least one worksheet is present
if (workbook.Worksheets.Count == 0)
{
    throw new InvalidOperationException("The workbook contains no worksheets.");
}
```

> **لماذا هذا مهم:** عندما تقوم لاحقًا بتمكين محددات تنوع الخط، تحتاج Aspose.Cells إلى دفتر مُهيأ بالكامل؛ وإلا سيتجاهل الخيار بصمت.

## الخطوة 3: إنشاء وتكوين خيارات حفظ XPS – هنا يتم **تمكين الخطوط**

قلب الدرس يكمن في هذه الخطوة. بشكل افتراضي، تقوم Aspose.Cells بإزالة محددات تنوع الخط لتقليل حجم ملف XPS. للحفاظ عليها، اضبط `FontVariationSelectors` إلى `true`.

```csharp
// Step 3: Create XPS save options and enable font variation selectors
XpsSaveOptions xpsOptions = new XpsSaveOptions
{
    // This flag tells Aspose.Cells to keep any OpenType font variation selectors
    FontVariationSelectors = true,

    // Optional: keep the original DPI for sharper rendering (default is 96)
    Dpi = 300
};
```

### ماذا يفعل `FontVariationSelectors = true` فعليًا؟

- **يحافظ على تنوعات الوزن والنمط المخصصة** (مثل الخط الذي يدعم عدة سماكات عبر ميزات OpenType).  
- **يضمن أن عارض XPS يعرض الحروف الدقيقة** التي تراها في Excel، بدلاً من الرجوع إلى خط عام.  
- **يضيف حمولة صغيرة** إلى حجم الملف لأن بيانات المحدد تُخزن داخل حزمة XPS.

إذا أردت **تحويل Excel إلى XPS** دون الحفاظ على هذه المحددات، ما عليك سوى ضبط الخاصية إلى `false` (أو إهمالها، حيث `false` هو الإعداد الافتراضي).

## الخطوة 4: حفظ الدفتر كملف XPS باستخدام الخيارات المكوَّنة

الآن بعد أن أصبحت الخيارات جاهزة، استدعِ `Save` مع تعداد `SaveFormat.Xps` ومرّر كائن الخيارات.

```csharp
// Step 4: Save the workbook as an XPS document with the font‑preserving options
string outputPath = "YOUR_DIRECTORY/WithSelectors.xps";
workbook.Save(outputPath, SaveFormat.Xps, xpsOptions);

Console.WriteLine($"Workbook successfully saved to XPS at: {outputPath}");
```

### النتيجة المتوقعة

- سيظهر الملف `WithSelectors.xps` في المجلد المستهدف.  
- افتحه بأي عارض XPS (مثل Windows XPS Viewer أو Edge).  
- يجب أن ترى نفس أوزان الخطوط، المائل، وأي تنوعات OpenType مخصصة كانت موجودة في ملف Excel الأصلي.

إذا بدت الخطوط مختلفة، تحقق من أن ملف Excel المصدر يستخدم خطًا يدعم محددات التنوع وأن العارض الذي تستخدمه يدعمها.

## المشكلات الشائعة وكيفية تجنّبها

| العَرَض | السبب المحتمل | الحل |
|---------|--------------|-----|
| النص يظهر بخط عام بديل | ترك `FontVariationSelectors` على القيمة الافتراضية (`false`) | اضبط `xpsOptions.FontVariationSelectors = true`. |
| حجم ملف XPS ينتفخ بشكل غير متوقع | إعداد DPI عالي مع محددات الخط | قلل `Dpi` إلى 150 أو 96 إذا كان الحجم أهم من الدقة. |
| استثناء “File not found” عند إنشاء `Workbook` | مسار غير صحيح أو ملف مفقود | استخدم مسارًا مطلقًا أو `Path.Combine(Environment.CurrentDirectory, "VariationFont.xlsx")`. |

## الخطوة 5: التحقق من التحويل (اختبار آلي اختياري)

إذا كنت تُؤتمت عمليات البناء، قد ترغب في التأكد من وجود ملف XPS وأنه غير فارغ:

```csharp
if (!System.IO.File.Exists(outputPath) || new System.IO.FileInfo(outputPath).Length == 0)
{
    throw new Exception("XPS conversion failed – file is missing or empty.");
}
```

تشغيل هذا الفحص كجزء من خط أنابيب CI يضمن أن **كيفية تمكين الخطوط** تعمل في كل مرة تدفع فيها كودًا.

## الخلاصة: ما غطيناه

- **كيفية تمكين الخطوط** أثناء تحويل Excel إلى XPS عبر ضبط `FontVariationSelectors`.  
- المقطع الكامل بـ C# الذي يحمل دفترًا، يكوّن `XpsSaveOptions`، ويحفظ النتيجة.  
- نصائح لتصحيح الأخطاء والتحقق من المستند النهائي.  

الآن يمكنك بثقة **تحويل Excel إلى XPS** مع الحفاظ على كل تفاصيل الطباعة.

### الخطوات التالية

- جرّب خصائص أخرى في `XpsSaveOptions` مثل `Compress` أو `EmbedStandardFonts`.  
- جرب التحويل إلى PDF أولاً، ثم إلى XPS، لمقارنة أحجام الملفات والدقة.  
- استكشف **معالجة الصور** في Aspose.Cells (`ImageOrPrintOptions`) إذا كان دفترك يحتوي على مخططات أو صور تحتاج إلى الحفاظ عليها.

هل لديك أسئلة حول سيناريوهات متقدمة—مثل تضمين خطوط مخصصة غير مثبتة على الجهاز الهدف؟ اترك تعليقًا أدناه، ونتمنى لك برمجة سعيدة!

## ما الذي يجب أن تتعلمه لاحقًا؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم استعراضها في هذا الدليل. كل مورد يتضمن أمثلة كود كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف نهج تنفيذ بديلة في مشاريعك.

- [How to Set Font Styles in Excel Using Aspose.Cells for .NET (Step-by-Step Guide)](/cells/english/net/formatting/aspose-cells-dotnet-set-font-styles-excel/)
- [How to Extract Fonts from Excel Files Using Aspose.Cells for .NET](/cells/english/net/formatting/extract-fonts-excel-aspose-cells-dotnet-guide/)
- [How to Convert Excel Sheets to Images Using Aspose.Cells .NET (Step-by-Step Guide)](/cells/english/net/workbook-operations/convert-excel-sheets-images-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}