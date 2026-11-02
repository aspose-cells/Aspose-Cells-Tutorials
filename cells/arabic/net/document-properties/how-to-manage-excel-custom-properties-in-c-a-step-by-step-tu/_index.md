---
category: general
date: 2026-10-07
description: تعلم درسًا حول خصائص Excel المخصصة باستخدام Aspose.Cells في C#. أضف،
  واقرأ، واحفظ الخصائص المخصصة في ملفات .xlsb.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- excel custom properties tutorial
- Aspose.Cells
- C# Excel workbook
- custom property API
- xlsb file
language: ar
lastmod: 2026-10-07
og_description: 'دروس خصائص Excel المخصصة: استخدم Aspose.Cells مع C# لإضافة وقراءة
  وحفظ الخصائص المخصصة في دفاتر العمل بصيغة .xlsb.'
og_image_alt: Diagram showing Excel custom properties workflow in a C# application
og_title: دليل شامل لتعليم الخصائص المخصصة في Excel باستخدام C#
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: Learn an excel custom properties tutorial using Aspose.Cells in C#.
    Add, read, and save custom properties in .xlsb files.
  headline: How to manage Excel custom properties in C# – a step-by-step tutorial
  type: TechArticle
- description: Learn an excel custom properties tutorial using Aspose.Cells in C#.
    Add, read, and save custom properties in .xlsb files.
  name: How to manage Excel custom properties in C# – a step-by-step tutorial
  steps:
  - name: Load the workbook that will hold the custom property
    text: '```csharp // Load an existing .xlsb workbook from disk Workbook workbook
      = new Workbook("YOUR_DIRECTORY/CustomProps.xlsb"); ```'
  - name: Add a custom property to the first worksheet
    text: '```csharp // Grab the first worksheet (index 0) Worksheet firstSheet =
      workbook.Worksheets[0];'
  - name: Retrieve the custom property value (e.g., for later use)
    text: '```csharp // Retrieve the value we just stored string reviewerName = firstSheet.CustomProperties["Reviewer"].Value.ToString();'
  - name: Save the workbook – the custom property is persisted in the .xlsb file
    text: '```csharp // Save the workbook; the custom property is now part of the
      file workbook.Save("YOUR_DIRECTORY/CustomPropsSaved.xlsb"); ```'
  - name: 'Pro tip: Use strong typing for numeric values'
    text: 'When you store numbers, Aspose.Cells preserves the data type, allowing
      you to retrieve them without conversion:'
  - name: 'Edge case: Updating an existing property'
    text: 'If you need to change a property''s value, you can either remove and re‑add
      it, or directly assign a new value:'
  type: HowTo
tags:
- Excel
- C#
- Aspose.Cells
- CustomProperties
title: كيفية إدارة الخصائص المخصصة في Excel باستخدام C# – دليل خطوة بخطوة
url: /ar/net/document-properties/how-to-manage-excel-custom-properties-in-c-a-step-by-step-tu/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# دليل خصائص Excel المخصصة – دليل كامل لمطوري C#

إذا كنت بحاجة إلى تخزين بيانات وصفية مثل أسماء المراجعين، أرقام الإصدارات، أو معرفات المشروع داخل مصنف Excel، فإن **excel custom properties tutorial** يوضح لك بالضبط كيفية القيام بذلك باستخدام C#. بنهاية الدليل ستكون قادرًا على إضافة، استرجاع، وحفظ الخصائص المخصصة في ملف *.xlsb* باستخدام مكتبة Aspose.Cells.

تخزين المعلومات الإضافية مباشرةً في المصنف يلغي الحاجة إلى ملفات إعدادات منفصلة ويحافظ على بياناتك مُدمجة. في هذا الدليل سنغطي الإعدادات المطلوبة، نتبع كل خطوة برمجية، ونناقش المشكلات الشائعة التي قد تواجهها.

## المتطلبات المسبقة

قبل أن تبدأ، تأكد من وجود:

* .NET 6.0 أو أحدث (الكود يعمل أيضًا مع .NET Framework 4.6+)
* ترخيص صالح لـ **Aspose.Cells** (التقييم المجاني يكفي للاختبار)
* Visual Studio 2022 (أو أي بيئة تطوير C# تفضلها)
* إلمام أساسي بـ C# وتنسيقات ملفات Excel

## نظرة عامة على دليل خصائص Excel المخصصة

الخصائص المخصصة هي أزواج مفتاح‑قيمة تُرفق بورقة عمل، مصنف، أو المستند بأكمله. تُخزن في جداول الخصائص الداخلية للملف وتظل موجودة عند فتح الملف في Microsoft Excel أو LibreOffice أو أي تطبيق جدول بيانات آخر يدعم معيار OpenXML.

في هذا الدليل سنقوم بـ:

1. تحميل مصنف *.xlsb* موجود.
2. إضافة خاصية مخصصة تسمى **Reviewer** إلى الورقة الأولى.
3. استرجاع قيمة الخاصية لمعالجة لاحقة.
4. حفظ المصنف بحيث تبقى الخاصية محفوظة.

جميع الخطوات تستخدم **Aspose.Cells** **custom property API**، الذي يُبسط التعامل مع XML منخفض المستوى.

## استخدام Aspose.Cells لإضافة خاصية مخصصة

أولاً، أضف حزمة Aspose.Cells NuGet إلى مشروعك:

```bash
dotnet add package Aspose.Cells
```

ثم استورد المساحات الاسمية المطلوبة:

```csharp
using Aspose.Cells;
using System;
```

### الخطوة 1: تحميل المصنف الذي سيحمل الخاصية المخصصة

```csharp
// Load an existing .xlsb workbook from disk
Workbook workbook = new Workbook("YOUR_DIRECTORY/CustomProps.xlsb");
```

*لماذا هذا مهم*: تحميل المصنف يمنحك الوصول إلى مجموعة `Worksheets`، وهي المكان الذي سنرفق فيه الخاصية المخصصة.

### الخطوة 2: إضافة خاصية مخصصة إلى الورقة الأولى

```csharp
// Grab the first worksheet (index 0)
Worksheet firstSheet = workbook.Worksheets[0];

// Add a custom property named "Reviewer" with the value "Alice"
firstSheet.CustomProperties.Add("Reviewer", "Alice");
```

تخزن **custom property API** الزوج في حقيبة خصائص الورقة. يمكنك إضافة عدد غير محدود من الخصائص؛ يجب أن يكون كل مفتاح فريدًا داخل النطاق نفسه.

### الخطوة 3: استرجاع قيمة الخاصية المخصصة (مثلاً للاستخدام لاحقًا)

```csharp
// Retrieve the value we just stored
string reviewerName = firstSheet.CustomProperties["Reviewer"].Value.ToString();

Console.WriteLine($"Reviewer: {reviewerName}");
```

استرجاع الخاصية يعمل تمامًا مثل البحث في القاموس. إذا لم يكن المفتاح موجودًا، تقوم Aspose.Cells بإلقاء استثناء `KeyNotFoundException`، لذا قد ترغب في حماية الاستدعاء باستخدام `ContainsKey` في الكود الإنتاجي.

### الخطوة 4: حفظ المصنف – الخاصية المخصصة تُحفظ في ملف .xlsb

```csharp
// Save the workbook; the custom property is now part of the file
workbook.Save("YOUR_DIRECTORY/CustomPropsSaved.xlsb");
```

الحفظ بنفس الصيغة (`.xlsb`) يضمن كتابة الخاصية إلى بنية المصنف الثنائية، والتي يدعمها Excel 2007 وما فوق بالكامل.

## العمل مع خصائص Excel المخصصة في مصنف C#

يمكنك أيضًا إضافة خصائص مخصصة على **مستوى المصنف** بدلاً من كل ورقة. الـ API هو نفسه، فقط استبدل `firstSheet` بـ `workbook`:

```csharp
workbook.CustomProperties.Add("ProjectId", 12345);
```

الخصائص على مستوى المصنف تظهر تحت **File → Info → Properties → Advanced Properties** في Excel، بينما الخصائص على مستوى الورقة تظهر في تبويب **Custom** داخل مربع حوار **Properties** لتلك الورقة.

### نصيحة احترافية: استخدم الأنواع القوية للقيم الرقمية

عند تخزين أرقام، تحافظ Aspose.Cells على نوع البيانات، مما يسمح لك باسترجاعها دون تحويل:

```csharp
firstSheet.CustomProperties.Add("Revision", 2);
int revision = (int)firstSheet.CustomProperties["Revision"].Value;
```

### حالة حافة: تحديث خاصية موجودة مسبقًا

إذا احتجت لتغيير قيمة خاصية، يمكنك إما إزالتها ثم إضافتها مرة أخرى، أو تعيين قيمة جديدة مباشرة:

```csharp
// Update the existing "Reviewer" property
firstSheet.CustomProperties["Reviewer"].Value = "Bob";
```

محاولة إضافة مفتاح مكرر دون تحديث ستؤدي إلى رفع استثناء `ArgumentException`.

## النتيجة المتوقعة

تشغيل الكود النموذجي أعلاه ينتج السطر التالي في وحدة التحكم:

```
Reviewer: Alice
```

بعد استدعاء `Save`، افتح `CustomPropsSaved.xlsb` في Excel، انتقل إلى **File → Info → Properties → Advanced Properties → Custom**، وسترى إدخال **Reviewer** بالقيمة **Alice** (أو **Bob** إذا قمت بتحديثها).

## المشكلات الشائعة وكيفية تجنبها

| المشكلة | لماذا يحدث | الحل |
|---------|------------|------|
| استخدام امتداد ملف غير صحيح (مثلاً `.xlsx` بدلاً من `.xlsb`) | تنسيق الثنائي يخزن الخصائص بطريقة مختلفة | احرص دائمًا على مطابقة الامتداد مع صيغة `Save` التي تنوي استخدامها |
| نسيان استدعاء مساحة الاسم `Aspose.Cells` | المترجم لا يستطيع العثور على `Workbook` أو `Worksheet` | أضف `using Aspose.Cells;` في أعلى الملف |
| الكتابة فوق خاصية موجودة عن غير قصد | `Add` يرفع استثناء إذا كان المفتاح موجودًا | استخدم الفهرس (`CustomProperties["Key"].Value = newValue`) لتحديث القيم |
| عدم معالجة المفاتيح غير الموجودة | الوصول إلى خاصية غير موجودة يرفع استثناء | تحقق من `CustomProperties.ContainsKey("Key")` قبل القراءة |

## مثال كامل قابل للتنفيذ

فيما يلي تطبيق console مكتمل يوضح كامل **excel custom properties tutorial**. انسخ الكود إلى مشروع console جديد وشغله كما هو.

```csharp
using Aspose.Cells;
using System;

namespace ExcelCustomPropertiesDemo
{
    class Program
    {
        static void Main()
        {
            // 1. Load the workbook
            string inputPath = "YOUR_DIRECTORY/CustomProps.xlsb";
            Workbook workbook = new Workbook(inputPath);

            // 2. Add a custom property to the first worksheet
            Worksheet firstSheet = workbook.Worksheets[0];
            firstSheet.CustomProperties.Add("Reviewer", "Alice");

            // 3. Retrieve the property
            if (firstSheet.CustomProperties.ContainsKey("Reviewer"))
            {
                string reviewer = firstSheet.CustomProperties["Reviewer"].Value.ToString();
                Console.WriteLine($"Reviewer: {reviewer}");
            }

            // 4. Save the workbook with the new property
            string outputPath = "YOUR_DIRECTORY/CustomPropsSaved.xlsb";
            workbook.Save(outputPath);

            Console.WriteLine($"Workbook saved to {outputPath}");
        }
    }
}
```

**ما يفعله الكود**:

* يحمل ملف *.xlsb* موجود.
* يضيف خاصية مخصصة على مستوى الورقة تسمى **Reviewer**.
* يطبع القيمة المخزنة في وحدة التحكم.
* يحفظ المصنف المعدل، محافظًا على الخاصية المخصصة.

## الخلاصة

هذا **excel custom properties tutorial** أرشدك إلى إضافة، قراءة، وحفظ الخصائص المخصصة في مصنف Excel بصيغة *.xlsb* باستخدام **Aspose.Cells** وC#. الآن تعرف كيف تتعامل مع استدعاءات **custom property API** على مستوى الورقة والمصنف، وتتعامل مع القيم الرقمية، وتحدّث الإدخالات الموجودة بأمان.

بعد ذلك، قد ترغب في استكشاف:

* تخزين حقول وصفية متعددة (مثل `Version`، `LastModified`) في مصنف واحد.
* تصدير الخصائص المخصصة إلى ملف JSON للتقارير الخارجية.
* استخدام النهج نفسه مع صيغ ملفات أخرى يدعمها Aspose.Cells، مثل `.xlsx` أو `.csv`.

جرّب نطاقات خصائص مختلفة وأنواع بيانات متنوعة لتلاحظ كيف تتصرف في واجهة Excel. برمجة سعيدة!

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة شاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [Create Excel Workbook – Add Custom Properties and Save as XLSB](/cells/english/net/document-properties/create-excel-workbook-add-custom-properties-and-save-as-xlsb/)
- [How to Access Custom Document Properties in Excel Using Aspose.Cells for .NET](/cells/english/net/workbook-operations/access-custom-excel-properties-aspose-cells-net/)
- [Master Excel Custom Properties Using Aspose.Cells .NET for Enhanced Data Management](/cells/english/net/data-manipulation/excel-custom-properties-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}