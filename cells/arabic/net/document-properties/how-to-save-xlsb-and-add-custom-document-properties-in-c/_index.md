---
category: general
date: 2026-07-03
description: تعلم كيفية حفظ ملفات XLSB في C# مع إضافة خصائص مستند مخصصة — دليل خطوة
  بخطوة لخصائص ملفات Excel المخصصة.
draft: false
keywords:
- how to save xlsb
- add custom document properties
- excel file custom properties
- create excel workbook programmatically
- add custom properties excel
language: ar
og_description: اكتشف كيفية حفظ ملفات XLSB في C# وإدراج خصائص مستند مخصصة لأتمتة Excel
  قوية.
og_title: كيفية حفظ ملف XLSB وإضافة خصائص مستند مخصصة في C#
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: Learn how to save XLSB files in C# while adding custom document properties—step‑by‑step
    guide for Excel file custom properties.
  headline: How to Save XLSB and Add Custom Document Properties in C#
  type: TechArticle
tags:
- Excel
- C#
- .NET
- Office Interop
title: كيفية حفظ ملف XLSB وإضافة خصائص مستند مخصصة في C#
url: /ar/net/document-properties/how-to-save-xlsb-and-add-custom-document-properties-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية حفظ XLSB وإضافة خصائص مستند مخصصة في C#

هل تساءلت يومًا **how to save XLSB** دون فقدان البيانات الوصفية التي أضفتها بعناء؟ لست وحدك. في العديد من خطوط تقارير البيانات، يُعد تنسيق XLSB الثنائي ضرورة لأنه سريع جدًا ومضغوط، ومع ذلك يواجه المطورون صعوبة عندما يحتاجون إلى إرفاق معلومات إضافية—مثل معرفات المشاريع، علامات المراجعة، أو طوابع الإصدارات.

في هذا الدرس سنستعرض مثالًا كاملاً قابلاً للتنفيذ يوضح **how to save XLSB** مع **adding custom document properties** إلى ورقة عمل Excel. في النهاية ستتمكن من إنشاء مصنف Excel برمجيًا، وإضافة أي خصائص مخصصة تريدها، وحفظ الملف كمصنف XLSB ثنائي. لا سحر، مجرد C# عادي ومكتبة Aspose.Cells.

## المتطلبات المسبقة

قبل أن نبدأ، تأكد من وجود ما يلي:

* .NET 6 SDK أو أحدث (الكود يعمل على .NET Framework 4.7+ أيضًا)  
* إشارة إلى **Aspose.Cells for .NET** – يمكنك الحصول عليها من NuGet باستخدام `dotnet add package Aspose.Cells`  
* إلمام أساسي بصياغة C#—لا حاجة لأي شيء معقد  
* مجلد قابل للكتابة على القرص حيث سيُحفظ الملف `CustomProps.xlsb` المُولد  

هذا كل شيء. إذا كنت تستخدم Visual Studio، أنشئ مشروع تطبيق Console جديد وقم بتثبيت حزمة NuGet؛ بقية الخطوات جاهزة للنسخ واللصق.

## الخطوة 1: إنشاء مصنف Excel برمجيًا

الشيء الأول الذي تحتاجه هو كائن مصنف جديد. فكر فيه كقماش فارغ ستملأه لاحقًا بالبيانات والبيانات الوصفية.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Instantiate a new workbook – this is the entry point for any Excel automation.
        Workbook workbook = new Workbook();

        // The workbook starts with a single default worksheet (index 0).
        // We'll work with that sheet in the next steps.
```

لماذا نبدأ بهذه الطريقة؟ إنشاء المصنف برمجيًا يمنحك التحكم الكامل في تنسيق الملف، ويتجنب عبء فتح ملف موجود، ويضمن أن الملف الناتج يحتوي فقط على العناصر التي تضيفها صراحة. كما أنها أنقى طريقة لتوضيح **create excel workbook programmatically** دون أي حالة مخفية.

## الخطوة 2: الوصول إلى الورقة الأولى وإضافة خصائص مستند مخصصة

الآن بعد أن لدينا مصنفًا، لنأخذ الورقة الأولى ونرفق بعض الخصائص المخصصة. هذه هي “الحقول الإضافية” التي يمكنك الاستعلام عنها لاحقًا، مشابهة لخصائص Author أو Title المدمجة ولكن تحت نظام تسمية خاص بك تمامًا.

```csharp
        // Step 2: Grab the first worksheet (index 0)
        Worksheet worksheet = workbook.Worksheets[0];

        // Add a string property called "ProjectId"
        worksheet.CustomProperties.Add("ProjectId", 12345);

        // Add a boolean flag indicating the sheet has been reviewed
        worksheet.CustomProperties.Add("Reviewed", true);

        // You can also add dates, numbers, or even complex objects if needed.
```

لاحظ الطريقة `CustomProperties.Add`. إنها تقبل اسمًا وقيمة، وستستنتج Aspose.Cells نوع البيانات الصحيح تلقائيًا. هذا هو جوهر **add custom document properties** ويعمل مع أي ورقة عمل داخل المصنف. إذا كنت تحتاج إلى **excel file custom properties** تنطبق على كامل المصنف بدلاً من ورقة واحدة، يمكنك استخدام `workbook.CustomProperties` بنفس الطريقة.

## الخطوة 3: How to Save XLSB – حفظ المصنف كملف ثنائي

مع وجود البيانات والبيانات الوصفية، الجزء الأخير هو حفظ الملف. هنا نجيب على سؤال العنوان: **how to save XLSB**.

```csharp
        // Step 3: Define the output path – make sure the directory exists.
        string outputPath = @"YOUR_DIRECTORY/CustomProps.xlsb";

        // Save the workbook in XLSB (binary) format.
        workbook.Save(outputPath, SaveFormat.Xlsb);

        // Inform the user that the operation succeeded.
        Console.WriteLine($"Workbook saved successfully to {outputPath}");
    }
}
```

بعض الأمور التي يجب مراعاتها:

* **XLSB** هو تنسيق ثنائي، لذا يكون أصغر حجمًا وأسرع في الفتح مقارنةً بـ XLSX القائم على XML.  
* تعداد `SaveFormat.Xlsb` يخبر Aspose.Cells بالوعاء الذي يجب استخدامه—لا خطوات تحويل إضافية مطلوبة.  
* إذا لم يكن المجلد المستهدف موجودًا، سيُطلق `workbook.Save` استثناءً؛ يمكنك الحماية من ذلك باستخدام `Directory.CreateDirectory(Path.GetDirectoryName(outputPath))` إذا رغبت.

هذا هو الجواب الكامل على **how to save xlsb** مع الحفاظ على البيانات الوصفية المخصصة الخاصة بك.

## التحقق من الخصائص المخصصة

بعد حفظ الملف، قد تتساءل: “هل تم تثبيت تلك الخصائص فعلاً؟” الطريقة السريعة للتحقق هي إعادة تحميل المصنف وقراءتها مرة أخرى.

```csharp
        // Reload the workbook to verify properties
        Workbook loaded = new Workbook(outputPath);
        Worksheet firstSheet = loaded.Worksheets[0];

        // Retrieve and print the custom properties
        var projectId = firstSheet.CustomProperties["ProjectId"].Value;
        var reviewed = firstSheet.CustomProperties["Reviewed"].Value;

        Console.WriteLine($"ProjectId: {projectId}, Reviewed: {reviewed}");
```

تشغيل هذا المقتطف يجب أن ينتج:

```
ProjectId: 12345, Reviewed: True
```

إذا رأيت تلك القيم، فقد نجحت في إضافة **excel file custom properties** وتأكدت من أن **how to save xlsb** يعمل من البداية إلى النهاية.

## الحالات الخاصة والمشكلات الشائعة

| الحالة | ما يجب مراقبته | الحل / التوصية |
|-----------|-------------------|----------------------|
| الحفظ إلى مجلد للقراءة فقط | `UnauthorizedAccessException` | تأكد من أن العملية لديها صلاحيات كتابة أو اختر مسارًا يمكن للمستخدم الكتابة فيه. |
| استخدام اسم خاصية موجود مسبقًا | `ArgumentException` | اختر أسماء فريدة أو استبدلها عبر استدعاء `CustomProperties["Name"].Value = newValue`. |
| الرغبة في خصائص على مستوى المصنف بدلاً من مستوى الورقة | الخلط بين `workbook.CustomProperties` و `worksheet.CustomProperties` | استخدم `workbook.CustomProperties.Add("GlobalTag", "Value")` للنطاق العام. |
| استهداف .NET Core بإصدار قديم من Aspose.Cells | فقدان تعداد `SaveFormat.Xlsb` | حدّث حزمة NuGet إلى أحدث نسخة تدعم .NET Core. |

نصيحة احترافية: إذا كنت تخطط لتوزيع ملف XLSB على مستخدمين قد يمتلكون إصدارات أقدم من Excel، اختبر الملف على Excel 2010 أو أحدث—تم دعم XLSB الثنائي منذ Excel 2007، لكن بعض الميزات الأحدث (مثل sparklines) قد لا تُعرض بشكل صحيح على العملاء القدامى جدًا.

## مثال كامل قابل للتنفيذ

بدمج كل ما سبق، إليك البرنامج الكامل الذي يمكنك وضعه في ملف `Program.cs` وتشغيله:

```csharp
using System;
using System.IO;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new workbook
        Workbook workbook = new Workbook();

        // 2️⃣ Access the first worksheet
        Worksheet worksheet = workbook.Worksheets[0];

        // 3️⃣ Add custom document properties
        worksheet.CustomProperties.Add("ProjectId", 12345);
        worksheet.CustomProperties.Add("Reviewed", true);

        // 4️⃣ Save the workbook as XLSB
        string outputPath = @"YOUR_DIRECTORY/CustomProps.xlsb";
        Directory.CreateDirectory(Path.GetDirectoryName(outputPath)!);
        workbook.Save(outputPath, SaveFormat.Xlsb);

        Console.WriteLine($"Workbook saved successfully to {outputPath}");

        // 5️⃣ Verify the properties (optional)
        Workbook loaded = new Workbook(outputPath);
        Worksheet firstSheet = loaded.Worksheets[0];
        var projectId = firstSheet.CustomProperties["ProjectId"].Value;
        var reviewed = firstSheet.CustomProperties["Reviewed"].Value;
        Console.WriteLine($"Verified - ProjectId: {projectId}, Reviewed: {reviewed}");
    }
}
```

قم بالترجمة باستخدام `dotnet build` وشغّلها بـ `dotnet run`. يجب أن ترى سطرين في وحدة التحكم يؤكدان عملية الحفظ والتحقق.

## الخلاصة

غطينا كل ما تحتاج معرفته حول **how to save XLSB** مع **adding custom document properties** باستخدام C#. بدءًا من مصنف نظيف، أظهرنا **create excel workbook programmatically**، أرفقنا **excel file custom properties**، حفظنا الملف كمصنف XLSB ثنائي، وتحققنا من صحة البيانات في دورة كاملة.

ما الخطوة التالية؟ جرّب إرفاق أنواع بيانات أغنى (تواريخ، GUIDs)، استكشف خصائص على مستوى المصنف، أو اجمع هذا النهج مع تعبئة البيانات المستندة إلى قاعدة بيانات (مثل سحب الصفوف من قاعدة بيانات). نفس النمط يعمل لتحويل CSV إلى XLSB، إنشاء تقارير آلية، وحتى وضع علامات بيانات وصفية جماعية للامتثال.

هل لديك تعديل ترغب في مشاركته؟ اترك تعليقًا، جرب، ودع مغامرة أتمتة الجداول تستمر. برمجة سعيدة!

## ماذا يجب أن تتعلم بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة شاملة مع شروح خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف نهج تنفيذ بديلة في مشاريعك.

- [How to Access Custom Document Properties in Excel Using Aspose.Cells for .NET](/cells/english/net/workbook-operations/access-custom-excel-properties-aspose-cells-net/)
- [How to Export Custom Excel Properties to PDF Using Aspose.Cells for Java](/cells/english/java/workbook-operations/export-excel-custom-properties-pdf-aspose-cells-java/)
- [Add Custom Content Type Properties to Excel Workbooks Using Aspose.Cells Java](/cells/english/java/tables-structured-references/aspose-cells-java-custom-content-types/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}