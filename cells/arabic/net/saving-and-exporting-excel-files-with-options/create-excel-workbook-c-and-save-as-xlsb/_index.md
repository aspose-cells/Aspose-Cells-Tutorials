---
category: general
date: 2026-11-25
description: إنشاء مصنف Excel باستخدام C# وحفظه كملف XLSB مع تعيين خاصية مخصصة للورقة
  لتخزين بيانات تعريف التقرير.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook c#
- save workbook as xlsb
- set worksheet custom property
- Aspose.Cells Excel export
- C# Excel automation
language: ar
lastmod: 2026-11-25
og_description: إنشاء مصنف إكسل باستخدام C# وحفظه كملف XLSB. يوضح هذا الدليل كيفية
  تعيين خاصية مخصصة للورقة بحيث تحتفظ تقاريرك بمعلومات المالك.
og_image_alt: Screenshot of a C# program creating an Excel workbook and saving it
  as XLSB
og_title: إنشاء دفتر عمل Excel باستخدام C# – حفظ كملف XLSB مع خصائص مخصصة
schemas:
- author: Aspose
  dateModified: '2026-11-25'
  description: Create Excel workbook C# and save as XLSB while setting worksheet custom
    property for report metadata.
  headline: Create Excel workbook C# and save as XLSB
  type: TechArticle
- description: Create Excel workbook C# and save as XLSB while setting worksheet custom
    property for report metadata.
  name: Create Excel workbook C# and save as XLSB
  steps:
  - name: '**Create a new workbook** – the in‑memory representation of an Excel file.'
    text: '**Create a new workbook** – the in‑memory representation of an Excel file.'
  - name: '**Set worksheet custom property** – attach key/value metadata to the first
      sheet.'
    text: '**Set worksheet custom property** – attach key/value metadata to the first
      sheet.'
  - name: '**Save workbook as XLSB** – write the file in the binary XLSB format, which
      keeps the custom property intact.'
    text: '**Save workbook as XLSB** – write the file in the binary XLSB format, which
      keeps the custom property intact.'
  type: HowTo
tags:
- excel
- csharp
- xlsb
- custom-properties
title: إنشاء مصنف إكسل C# وحفظه كملف XLSB
url: /ar/net/saving-and-exporting-excel-files-with-options/create-excel-workbook-c-and-save-as-xlsb/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء مصنف Excel C# وحفظه كـ XLSB

إذا كنت بحاجة إلى **إنشاء مصنف Excel C#** لروتين تقارير، فمن المحتمل أنك تريد أيضًا أن يحتوي الملف على بيانات تعريفية إضافية مثل مالك التقرير. يوضح هذا الدرس كيفية **تعيين خاصية مخصصة للورقة** ثم **حفظ المصنف كـ XLSB** في سير عمل واحد قابل لإعادة الإنتاج.

سوف تحصل في النهاية على ملف XLSB مشفر ثنائيًا يفتح في Excel، ويحافظ على الخاصية المخصصة، وجاهز للتوزيع. لا تحتاج إلى أي سكريبتات خارجية—فقط مكتبة Aspose.Cells لـ .NET وبعض أسطر C#.

## المتطلبات المسبقة

قبل أن تبدأ، تأكد من وجود ما يلي:

* .NET 6.0 (أو أحدث) مثبت – تدعم Aspose.Cells .NET Standard 2.0+.
* ترخيص Aspose.Cells صالح (أو مفتاح تقييم مجاني).  
* Visual Studio 2022 أو أي بيئة تطوير C# تفضلها.

أضف حزمة NuGet:

```bash
dotnet add package Aspose.Cells
```

> **نصيحة احترافية:** استخدم النسخة التجريبية المجانية من **Aspose.Cells** لتجنب أخطاء الترخيص أثناء الاختبار.

## إنشاء مصنف Excel C# – نظرة عامة

يتكون العملية من ثلاث خطوات أساسية:

1. **إنشاء مصنف جديد** – تمثيل الذاكرة لمصنف Excel.
2. **تعيين خاصية مخصصة للورقة** – إرفاق بيانات تعريفية مفتاح/قيمة بالورقة الأولى.
3. **حفظ المصنف كـ XLSB** – كتابة الملف بصيغة XLSB الثنائية، التي تحتفظ بالخاصية المخصصة دون تعديل.

كل خطوة موضحة بكود كامل قابل للتنفيذ.

![لقطة شاشة لإنشاء مصنف Excel C#](excel_workbook.png)

## الخطوة 1: تهيئة مصنف جديد

```csharp
using Aspose.Cells;

namespace ExcelAutomation
{
    class Program
    {
        static void Main()
        {
            // Step 1: Create a new workbook
            Workbook workbook = new Workbook();          // creates a default workbook with one worksheet
            Worksheet worksheet = workbook.Worksheets[0]; // reference to the first worksheet
```

**لماذا هذا مهم** – `Workbook` هو نقطة الدخول لجميع عمليات Excel. عندما تنشئه بدون معلمات، تقوم Aspose.Cells بإنشاء مصنف نظيف بورقة عمل واحدة، وهو مثالي للتوليد البرمجي.

## الخطوة 2: تعيين خاصية مخصصة للورقة

```csharp
            // Step 2: Add a custom property to the worksheet (e.g., the report owner)
            worksheet.CustomProperties.Add("ReportOwner", "Alice");
```

*`set worksheet custom property`* هو الاستدعاء الدقيق الذي يخزن المفتاح **ReportOwner** بالقيمة **Alice** داخل مجموعة الخصائص المخصصة للورقة. يمكن لـ Excel لاحقًا قراءة هذه الخاصية عبر **File → Info → Properties → Advanced Properties**.

> **سؤال شائع:** *ماذا لو احتجت إلى خصائص متعددة؟*  
> ما عليك سوى استدعاء `Add` بشكل متكرر بأسماء مختلفة، مثل `worksheet.CustomProperties.Add("Department", "Finance");`.

## الخطوة 3: حفظ المصنف كـ XLSB

```csharp
            // Step 3: Save the workbook in XLSB format – the custom property is preserved
            string outputPath = @"YOUR_DIRECTORY\custom_props.xlsb";
            workbook.Save(outputPath, SaveFormat.Xlsb);
        }
    }
}
```

السطر **save workbook as xlsb** يكتب الملف باستخدام صيغة XLSB الثنائية. مقارنةً بصيغة XLSX الكلاسيكية، فإن XLSB يحمل أسرع للمجموعات الكبيرة من البيانات ويحافظ على الخصائص المخصصة دون خطوات إضافية.

### النتيجة المتوقعة

بعد تشغيل البرنامج:

* يظهر الملف `custom_props.xlsb` في `YOUR_DIRECTORY`.
* فتح الملف في Excel يعرض ورقة واحدة دون بيانات مرئية (لقد أضفنا فقط بيانات تعريفية).
* انتقل إلى **File → Info → Properties → Advanced Properties → Custom** – سترى **ReportOwner = Alice**.

## التحقق من الخاصية المخصصة برمجيًا (اختياري)

إذا أردت التأكد من أن الخاصية نجت من عملية القراءة والكتابة، يمكنك إعادة تحميل الملف:

```csharp
            // Verify the property after loading
            Workbook loaded = new Workbook(outputPath);
            string owner = loaded.Worksheets[0].CustomProperties["ReportOwner"].Value.ToString();
            System.Console.WriteLine($"Report owner: {owner}"); // should print "Alice"
```

تشغيل هذا المقتطف يطبع:

```
Report owner: Alice
```

## الحالات الخاصة وأفضل الممارسات

| الحالة                                   | التوصية                                                                      |
|------------------------------------------|------------------------------------------------------------------------------|
| مصنفات كبيرة (>10 000 صف)                | استخدم **XLSB** لأن ضغطه الثنائي يقلل من استهلاك الذاكرة.                     |
| الحاجة إلى الحفاظ على بيانات خاصة بالثقافة | عيّن `Workbook.Settings.CultureInfo` قبل إضافة القيم.                        |
| عدة أوراق عمل تحتاج نفس الخاصية          | كرّر الحلقة عبر `workbook.Worksheets` وأضف الخاصية إلى كل ورقة.               |
| التشغيل على Linux/macOS                  | تأكد من الإشارة إلى بناء Aspose.Cells .NET Standard؛ لا توجد واجهات Windows‑only. |

> **احذر من:** حفظ الملف في دليل لا يملك صلاحية كتابة سيؤدي إلى رمي `UnauthorizedAccessException`. تحقق دائمًا من المسار أو استخدم `Path.GetTempPath()` للملفات المؤقتة.

## مثال كامل قابل للتنفيذ

```csharp
using System;
using Aspose.Cells;

namespace ExcelAutomation
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create Excel workbook C#
            Workbook workbook = new Workbook();
            Worksheet worksheet = workbook.Worksheets[0];

            // 2️⃣ Set worksheet custom property
            worksheet.CustomProperties.Add("ReportOwner", "Alice");
            worksheet.CustomProperties.Add("ReportDate", DateTime.Today.ToShortDateString());

            // 3️⃣ Save workbook as XLSB
            string outputPath = @"C:\Temp\custom_props.xlsb";
            workbook.Save(outputPath, SaveFormat.Xlsb);

            // Optional verification
            Workbook loaded = new Workbook(outputPath);
            string owner = loaded.Worksheets[0].CustomProperties["ReportOwner"].Value.ToString();
            Console.WriteLine($"Report owner verified: {owner}");
        }
    }
}
```

انسخ الكود إلى مشروع وحدة تحكم جديد، استبدل `C:\Temp\` بمجلد تملكه، وشغّله. سيظهر في وحدة التحكم النص `Report owner verified: Alice`، مما يثبت أن **إنشاء مصنف Excel C#**، **تعيين خاصية مخصصة للورقة**، و**حفظ المصنف كـ XLSB** جميعها عملت معًا.

## الخلاصة

أنت الآن تعرف كيف **تنشئ مصنف Excel C#**، وتضيف **خاصية مخصصة للورقة**، وت **حفظ المصنف كـ XLSB** بنمط نظيف وجاهز للإنتاج. هذا النهج مثالي لأنابيب التقارير الآلية، خدمات تصدير البيانات، أو أي سيناريو يحتاج إلى نقل البيانات التعريفية مع ملف Excel.

الخطوات التالية قد تشمل:

* إضافة جداول بيانات وتنسيقها (`Cells`, `Style` objects).
* التصدير إلى صيغ أخرى مثل **XLSX** أو **CSV** مع الحفاظ على الخصائص.
* استخدام **Aspose.Cells** لقراءة الخصائص المخصصة من المصنفات الموجودة.

لا تتردد في تجربة أسماء خصائص مختلفة، أوراق عمل متعددة، أو مجموعات بيانات كبيرة. نمط الخطوات الثلاثة هذا يتوسع من ملف ورقة واحدة بسيط إلى حلول تقارير على مستوى المؤسسة. happy coding!

## ماذا يجب أن تتعلم بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مورد يتضمن أمثلة كود كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف نهج تنفيذ بديلة في مشاريعك.

- [Create Excel Workbook C# – Add Custom Property & Save XLSB](/cells/english/net/document-properties/create-excel-workbook-c-add-custom-property-save-xlsb/)
- [Create Excel Workbook – Add Custom Properties and Save as XLSB](/cells/english/net/document-properties/create-excel-workbook-add-custom-properties-and-save-as-xlsb/)
- [How to create Excel workbook C# with custom formatting and save as XLSX](/cells/english/net/excel-formatting-and-styling/how-to-create-excel-workbook-c-with-custom-formatting-and-sa/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}