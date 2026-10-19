---
category: general
date: 2026-06-17
description: كيفية إضافة بيانات تعريف Excel في C# عن طريق إنشاء مصنف Excel برمجيًا،
  وتعيين خصائص مخصصة للورقة، وحفظ المصنف بصيغة XLSB.
draft: false
keywords:
- how to add excel metadata
- create excel workbook programmatically
- save workbook as xlsb
- set worksheet custom properties
- write custom properties c#
language: ar
og_description: كيفية إضافة بيانات تعريف Excel في C# عن طريق إنشاء مصنف Excel برمجيًا،
  وضبط خصائص ورقة العمل المخصصة، وحفظه كملف XLSB.
og_title: كيفية إضافة بيانات تعريف Excel – دليل شامل لكتاب العمل C#
schemas:
- author: Aspose
  dateModified: '2026-06-17'
  description: How to add Excel metadata in C# by creating an Excel workbook programmatically,
    setting worksheet custom properties, and saving the workbook as XLSB.
  headline: How to Add Excel Metadata – Complete C# Workbook Guide
  type: TechArticle
- description: How to add Excel metadata in C# by creating an Excel workbook programmatically,
    setting worksheet custom properties, and saving the workbook as XLSB.
  name: How to Add Excel Metadata – Complete C# Workbook Guide
  steps:
  - name: '**Create Excel workbook programmatically** – set up the file container.'
    text: '**Create Excel workbook programmatically** – set up the file container.'
  - name: '**Set worksheet custom properties** – embed the metadata you care about.'
    text: '**Set worksheet custom properties** – embed the metadata you care about.'
  - name: '**Save workbook as XLSB** – choose the binary format for speed and compact
      size.'
    text: '**Save workbook as XLSB** – choose the binary format for speed and compact
      size.'
  type: HowTo
tags:
- excel
- csharp
- metadata
- aspnet
title: كيفية إضافة بيانات تعريف إكسل – دليل شامل لكتاب العمل بلغة C#
url: /ar/net/document-properties/how-to-add-excel-metadata-complete-c-workbook-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية إضافة بيانات تعريف Excel – دليل كامل لإنشاء دفتر عمل C#

هل تساءلت يومًا **كيفية إضافة بيانات تعريف Excel** إلى ملف دون فتح جدول البيانات يدويًا؟ لست الوحيد الذي يحيره هذا. في العديد من تطبيقات الأعمال تحتاج إلى وضع علامة على دفتر العمل بأشياء مثل معرف المشروع، اسم المالك، أو رقم الإصدار، وإن القيام بذلك برمجيًا يوفر ساعات من العمل المتكرر.

في هذا الدرس سنستعرض **كيفية إضافة بيانات تعريف Excel** باستخدام C#. سن **ننشئ دفتر عمل Excel برمجيًا**، نضيف بعض **خصائص ورقة العمل المخصصة**، وأخيرًا **نحفظ دفتر العمل كملف XLSB**. في النهاية ستحصل على مقتطف شفرة جاهز يمكنك إدراجه في أي مشروع .NET—دون الحاجة لتثبيت Excel إضافيًا.

> **ما ستحصل عليه:** مثال واحد مستقل يكتب خصائص مخصصة في C#، يشرح لماذا كل سطر مهم، ويظهر الملف النهائي على القرص.

---

## نظرة عامة خطوة بخطوة لإضافة بيانات تعريف Excel

فيما يلي خارطة الطريق العامة:

1. **إنشاء دفتر عمل Excel برمجيًا** – إعداد حاوية الملف.  
2. **تعيين خصائص ورقة العمل المخصصة** – تضمين البيانات الوصفية التي تهمك.  
3. **حفظ دفتر العمل كملف XLSB** – اختيار الصيغة الثنائية للسرعة والحجم المضغوط.  

كل خطوة موضحة في قسمها الخاص حتى يمكنك النسخ واللصق أو التعديل أو حتى إعادة الترتيب حسب متطلبات مشروعك.

---

## إنشاء دفتر عمل Excel برمجيًا

قبل أن نتمكن من إرفاق أي بيانات تعريف، نحتاج إلى كائن دفتر عمل. أسهل طريقة في C# هي استخدام مكتبة **Aspose.Cells**، التي تعمل دون الحاجة لتثبيت Excel على الخادم.

```csharp
using System;
using Aspose.Cells;               // NuGet package: Aspose.Cells
using Aspose.Cells.Tables;       // Optional, for table handling

namespace ExcelMetadataDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1: Instantiate a new, empty workbook.
            // This is the in‑memory representation of an Excel file.
            Workbook workbook = new Workbook();

            // OPTIONAL: Give the default worksheet a friendly name.
            Worksheet sheet = workbook.Worksheets[0];
            sheet.Name = "DataSheet";

            // The rest of the steps will follow here...
```

**لماذا هذا مهم:** `Workbook` هو الكائن الجذري؛ كل ما يليه (أوراق العمل، الخلايا، الأنماط) يتواجد تحته. بإنشائه في الشفرة نتجنب أي تفاعل مع واجهة المستخدم، وهو ما يناسب خطوط الأنابيب الآلية أو خدمات الويب.

---

## تعيين خصائص ورقة العمل المخصصة

الآن بعد أن لدينا دفتر عمل، لنضيف البيانات الوصفية. تسمي Excel هذه *الخصائص المخصصة* وتُخزن على مستوى ورقة العمل. يمكنك التفكير فيها كأزواج مفتاح‑قيمة مخفية يمكن للأنظمة الأخرى (أو حتى Excel نفسه) قراءتها لاحقًا.

```csharp
            // Step 2: Access the first worksheet (already referenced as 'sheet')
            // Add custom properties – these are the metadata entries.
            sheet.CustomProperties.Add("ProjectId", 12345);          // Numeric ID
            sheet.CustomProperties.Add("Owner", "John Doe");       // String value
            sheet.CustomProperties.Add("CreatedOn", DateTime.Now); // DateTime example
            sheet.CustomProperties.Add("IsConfidential", true);    // Boolean flag

            // Verify that the properties were added (useful for debugging)
            foreach (CustomProperty prop in sheet.CustomProperties)
            {
                Console.WriteLine($"{prop.Name} = {prop.Value}");
            }
```

**لماذا هذا مهم:** بكتابة **الخصائص المخصصة** مباشرةً على ورقة العمل تضمن أن البيانات تنتقل مع الملف. أي شخص يفتح دفتر العمل لاحقًا—سواء في Excel، أو تطبيق .NET آخر، أو سكريبت Python—يمكنه استعلام هذه الخصائص دون لمس الخلايا الظاهرة.

> **نصيحة احترافية:** احرص على أن تكون أسماء الخصائص قصيرة وبصيغة camel‑case؛ قد تقص واجهة Excel الأسماء الطويلة، مما يجعل قراءتها أصعب لاحقًا.

---

## حفظ دفتر العمل كملف XLSB

الخطوة الأخيرة هي حفظ دفتر العمل على القرص. بينما صيغة `.xlsx` الكلاسيكية جيدة، **الحفظ كـ XLSB** يمنحك ملفًا ثنائيًا أصغر عادةً بنسبة 30‑40 % ويُحمّل أسرع—مفيد خاصةً للمجموعات الكبيرة من البيانات.

```csharp
            // Step 3: Choose the XLSB format and specify the output path.
            string outputPath = @"C:\Temp\custom-metadata.xlsb";

            // SaveFormat.Xlsb tells Aspose.Cells to write a binary workbook.
            workbook.Save(outputPath, SaveFormat.Xlsb);

            Console.WriteLine($"Workbook saved successfully to {outputPath}");
        }
    }
}
```

**لماذا هذا مهم:** `SaveFormat.Xlsb` ينتج ملفًا ثنائيًا مضغوطًا لا يزال يدعم جميع ميزات Excel، بما في ذلك الخصائص المخصصة التي أضفناها للتو. إذا احتجت لاحقًا لمشاركة الملف عبر البريد الإلكتروني أو تخزينه في قاعدة بيانات، فإن الحجم الأصغر سيحدث فرقًا ملحوظًا.

---

## مثال كامل يعمل (جميع الخطوات معًا)

بدمج كل شيء، إليك البرنامج الكامل الذي يمكنك تشغيله كما هو. فقط تأكد من تثبيت حزمة **Aspose.Cells** عبر NuGet (`Install-Package Aspose.Cells`) وضبط مسار الإخراج إلى مجلد قابل للكتابة على جهازك.

```csharp
using System;
using Aspose.Cells;

namespace ExcelMetadataDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Create a new workbook.
            Workbook workbook = new Workbook();

            // 2️⃣ Access the first worksheet and give it a friendly name.
            Worksheet sheet = workbook.Worksheets[0];
            sheet.Name = "DataSheet";

            // 3️⃣ Add custom metadata to the worksheet.
            sheet.CustomProperties.Add("ProjectId", 12345);
            sheet.CustomProperties.Add("Owner", "John Doe");
            sheet.CustomProperties.Add("CreatedOn", DateTime.Now);
            sheet.CustomProperties.Add("IsConfidential", true);

            // Debug output – shows the properties in the console.
            foreach (CustomProperty prop in sheet.CustomProperties)
            {
                Console.WriteLine($"{prop.Name} = {prop.Value}");
            }

            // 4️⃣ Save the workbook as an XLSB file.
            string outputPath = @"C:\Temp\custom-metadata.xlsb";
            workbook.Save(outputPath, SaveFormat.Xlsb);

            Console.WriteLine($"Workbook saved successfully to {outputPath}");
        }
    }
}
```

**النتيجة المتوقعة:** بعد تشغيل البرنامج، ستجد الملف `custom-metadata.xlsb` في المجلد الذي حددته. فتحه في Excel → *File* → *Info* → *Properties* → *Advanced Properties* → *Custom* سيظهر الأربعة إدخالات التي أضفناها (`ProjectId`, `Owner`, `CreatedOn`, `IsConfidential`). سيكون حجم الملف أصغر بوضوح مقارنةً بملف `.xlsx` مكافئ.

---

## أسئلة شائعة وحالات خاصة

| السؤال | الجواب |
|----------|--------|
| *هل يمكنني إضافة بيانات تعريف إلى خلية محددة بدلاً من ورقة العمل؟* | Excel يدعم الخصائص المخصصة فقط على مستوى دفتر العمل أو ورقة العمل. للملاحظات على مستوى الخلية، استخدم تعليقات الخلايا أو أعمدة مساعدة مخفية. |
| *ماذا لو احتجت لقراءة هذه الخصائص لاحقًا؟* | استخدم `Worksheet.CustomProperties["PropertyName"]` لاسترجاع القيمة، مع التحويل إلى النوع المناسب. |
| *هل يدعم XLSB الإصدارات القديمة من Excel؟* | نعم—Excel 2007 وما بعده يمكنه فتح ملفات `.xlsb`. الإصدارات الأقدم (Excel 2003) تحتاج إلى حزمة Compatibility Pack. |
| *هل أحتاج إلى ترخيص لـ Aspose.Cells؟* | Aspose يقدم وضع تقييم مجاني مع علامة مائية. للإنتاج، الترخيص يزيل العلامة المائية ويفتح الأداء الكامل. |
| *هل يمكنني تعيين خصائص مخصصة على دفتر العمل نفسه؟* | بالتأكيد. استخدم `workbook.CustomProperties` إذا أردت أن تُطبق البيانات الوصفية على الملف بأكمله بدلاً من ورقة واحدة. |

---

## الخاتمة

لقد أوضحنا للتو **كيفية إضافة بيانات تعريف Excel** في C# عبر **إنشاء دفتر عمل Excel برمجيًا**، **تعيين خصائص ورقة العمل المخصصة**، و**حفظ دفتر العمل كملف XLSB**. المثال الكامل القابل للتنفيذ يُظهر كل سطر تحتاجه، سبب وجوده، وكيفية التحقق من النتائج.

إذا كنت مستعدًا للخطوة التالية، جرّب:

- **كتابة خصائص مخصصة في C#** لكامل دفتر العمل (`workbook.CustomProperties`).  
- تجربة **أنواع بيانات مختلفة** (مثل التواريخ، القيم المنطقية).  
- التحويل إلى **SaveFormat.Xlsx** لمقارنة أحجام الملفات.  
- أتمتة العملية في API باستخدام ASP.NET Core بحيث يمكن للمستخدمين رفع ملف CSV والحصول على XLSB غني بالبيانات الوصفية في المقابل.

لا تتردد في تعديل أسماء الخصائص، إضافة قيم أخرى، أو دمج هذا المقتطف في محرك تقارير أكبر. السماء هي الحد عندما يمكنك وضع علامات برمجية على ملفات Excel الخاصة بك.

برمجة سعيدة، ولتظل جداولك دائمًا تحمل البيانات الوصفية الصحيحة! 

![Screenshot showing Excel file properties with custom metadata – how to add excel metadata](/images/excel-metadata-screenshot.png "how to add excel metadata")

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مصدر يتضمن أمثلة شفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف طرق تنفيذ بديلة في مشاريعك.

- [إضافة ورقة عمل Excel إلى دفتر عمل موجود – دليل C#](/cells/english/net/excel-worksheet-csharp-tutorials/add-excel-worksheet-to-existing-workbook-csharp-tutorial/)
- [كيفية إنشاء وحفظ دفتر عمل Excel كملف ODS باستخدام Aspose.Cells لـ .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)
- [كيفية إنشاء وحفظ دفتر عمل Excel كملف SVG باستخدام Aspose.Cells لـ Java](/cells/english/java/workbook-operations/create-save-workbook-svg-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}