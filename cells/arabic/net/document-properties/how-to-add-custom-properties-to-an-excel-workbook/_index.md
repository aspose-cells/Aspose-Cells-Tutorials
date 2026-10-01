---
category: general
date: 2026-10-01
description: تعلم كيفية إضافة خصائص مخصصة إلى مصنف Excel باستخدام Aspose.Cells. يوضح
  هذا الدليل أيضًا كيفية إضافة معرف المشروع وقراءة الخصائص المخصصة.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add custom properties
- how to add custom
- excel custom properties
- add project id
- read custom properties
language: ar
lastmod: 2026-10-01
og_description: أضف خصائص مخصصة إلى مصنف Excel باستخدام Aspose.Cells. اتبع هذا الدرس
  الكامل لإضافة معرف المشروع، وتعيين معلومات المراجع، وقراءة الخصائص المخصصة برمجيًا.
og_image_alt: Screenshot of an Excel worksheet displaying custom properties added
  via Aspose.Cells
og_title: إضافة خصائص مخصصة إلى مصنف Excel – دليل خطوة بخطوة
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Learn how to add custom properties to an Excel workbook using Aspose.Cells.
    This guide also shows how to add project ID and read custom properties.
  headline: How to add custom properties to an Excel workbook
  type: TechArticle
- description: Learn how to add custom properties to an Excel workbook using Aspose.Cells.
    This guide also shows how to add project ID and read custom properties.
  name: How to add custom properties to an Excel workbook
  steps:
  - name: Open the saved `DataWithProps.xlsb` file in Microsoft Excel.
    text: Open the saved `DataWithProps.xlsb` file in Microsoft Excel.
  - name: Go to **File → Info → Properties → Advanced Properties**.
    text: Go to **File → Info → Properties → Advanced Properties**.
  - name: Select the **Custom** tab.
    text: Select the **Custom** tab.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: كيفية إضافة خصائص مخصصة إلى مصنف Excel
url: /ar/net/document-properties/how-to-add-custom-properties-to-an-excel-workbook/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية إضافة خصائص مخصصة إلى مصنف Excel

إذا كنت بحاجة إلى **إضافة خصائص مخصصة** إلى مصنف Excel، يوضح لك هذا الدليل بالضبط كيفية القيام بذلك باستخدام Aspose.Cells for .NET. ستتعلم أيضًا كيفية إضافة معرف المشروع، تعيين اسم المراجع، ثم **قراءة الخصائص المخصصة** لاحقًا من الملف.

يسمح لك العمل مع البيانات الوصفية المخصصة بدمج معلومات خاصة بالأعمال مباشرة داخل جدول البيانات، مما يجعل من السهل تتبع الملكية أو الإصدار أو أي سياق آخر دون الحاجة إلى قاعدة بيانات منفصلة. تغطي الخطوات أدناه سير العمل الكامل من إنشاء المصنف إلى حفظ الخصائص الجديدة.

## المتطلبات المسبقة

قبل أن تبدأ، تأكد من وجود ما يلي:

* .NET 6.0 أو أحدث مثبت  
* ترخيص صالح لـ Aspose.Cells for .NET (أو نسخة تجريبية مجانية)  
* Visual Studio 2022 (أو أي بيئة تطوير C#)  

لا توجد حزم NuGet إضافية مطلوبة بخلاف `Aspose.Cells`.

## الخطوة 1: إعداد المشروع واستيراد المساحات الاسمية

أنشئ تطبيقًا جديدًا من نوع console وأضف مرجع Aspose.Cells:

```csharp
using System;
using Aspose.Cells;

namespace ExcelCustomPropertiesDemo
{
    class Program
    {
        static void Main()
        {
            // The rest of the code lives here
        }
    }
}
```

تحتوي مساحة الأسماء `Aspose.Cells` على الفئات `Workbook` و `Worksheet` و `CustomPropertyCollection` التي سنستخدمها.

## الخطوة 2: تحميل مصنف موجود (أو إنشاء مصنف جديد)

يمكنك البدء بملف `.xlsb` موجود أو إنشاء مصنف جديد. المثال أدناه يحمل ملفًا باسم **Data.xlsb** موجودًا في مجلد يسمى `YOUR_DIRECTORY`.

```csharp
// Load the existing workbook
var workbookPath = @"YOUR_DIRECTORY\Data.xlsb";
var workbook = new Workbook(workbookPath);
```

إذا لم يكن الملف موجودًا، استبدل الكود بـ `new Workbook();` لإنشاء مصنف فارغ.

## الخطوة 3: إضافة خصائص مخصصة إلى الورقة الأولى

العملية الأساسية هي **إضافة خصائص مخصصة** إلى ورقة العمل. يخزن Aspose.Cells الخصائص المخصصة في مجموعة تتصرف كقاموس.

```csharp
// Get the first worksheet (index 0)
var worksheet = workbook.Worksheets[0];

// Add a numeric ProjectId property
worksheet.CustomProperties.Add("ProjectId", 12345);

// Add a string Reviewer property
worksheet.CustomProperties.Add("Reviewer", "John Doe");

// Optional: add a DateTime property for the creation timestamp
worksheet.CustomProperties.Add("CreatedOn", DateTime.UtcNow);
```

نستخدم `CustomProperties.Add` بدلاً من `CustomProperties["Name"] = value` لأن طريقة `Add` تنشئ الإدخال إذا لم يكن موجودًا وتضمن تخزين النوع الصحيح للبيانات. هذا النهج يمنع حدوث تعارضات نوعية قد تؤدي إلى أخطاء وقت التشغيل عند قراءة القيم لاحقًا.

## الخطوة 4: حفظ المصنف بالخصائص الجديدة

بعد حقن البيانات الوصفية، احفظ التغييرات في ملف جديد بحيث يبقى الأصلي دون تعديل.

```csharp
// Save the workbook with the custom properties
var outputPath = @"YOUR_DIRECTORY\DataWithProps.xlsb";
workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to {outputPath}");
```

في هذه المرحلة يحتوي ملف Excel على البيانات الوصفية المخصصة التي عرّفتها. يمكنك التحقق من الخصائص باستخدام الخطوات في القسم التالي.

## الخطوة 5: قراءة الخصائص المخصصة من المصنف

قراءة **خصائص Excel المخصصة** تتبع نفس نمط المجموعة. يوضح هذا المقتطف كيفية استرجاع القيم التي تم تخزينها للتو.

```csharp
// Load the workbook that contains custom properties
var loadedWorkbook = new Workbook(outputPath);
var loadedWorksheet = loadedWorkbook.Worksheets[0];
var props = loadedWorksheet.CustomProperties;

// Retrieve each property safely
int projectId = props["ProjectId"] != null ? (int)props["ProjectId"].Value : -1;
string reviewer = props["Reviewer"] != null ? props["Reviewer"].Value.ToString() : "Unknown";
DateTime createdOn = props["CreatedOn"] != null ? (DateTime)props["CreatedOn"].Value : DateTime.MinValue;

Console.WriteLine($"ProjectId: {projectId}");
Console.WriteLine($"Reviewer: {reviewer}");
Console.WriteLine($"CreatedOn (UTC): {createdOn:u}");
```

المؤشر في `CustomPropertyCollection` يُعيد كائن `CustomProperty`؛ الوصول إلى خاصية `Value` يعطيك البيانات المخزنة بنوعها الأصلي. التحقق من `null` قبل التحويل يمنع حدوث `NullReferenceException` إذا كانت الخاصية غير موجودة.

### ناتج وحدة التحكم المتوقع

```
ProjectId: 12345
Reviewer: John Doe
CreatedOn (UTC): 2026-10-01 12:34:56Z
```

ستعكس الطابع الزمني اللحظة التي استدعيت فيها `Add` في الخطوة 3.

## نصيحة احترافية: تحديث خاصية مخصصة موجودة

إذا احتجت إلى **إضافة معلومات مخصصة** لاحقًا (مثل تغيير المراجع)، استخدم مُعيّن `CustomPropertyCollection`:

```csharp
// Change the reviewer name
if (props["Reviewer"] != null)
{
    props["Reviewer"].Value = "Jane Smith";
}
else
{
    // Property does not exist; add it
    props.Add("Reviewer", "Jane Smith");
}
```

يضمن هذا النمط أن الخاصية إما تُحدّث أو تُنشأ، وهو مفيد في سير عمل تكراري مثل توليد التقارير تلقائيًا.

## الخطوة 6: التحقق من الخصائص داخل Excel (اختياري)

يمكنك أيضًا عرض الخصائص المخصصة مباشرة في Excel:

1. افتح الملف `DataWithProps.xlsb` المحفوظ في Microsoft Excel.  
2. انتقل إلى **File → Info → Properties → Advanced Properties**.  
3. اختر علامة التبويب **Custom**.  

سترى الإدخالات `ProjectId` و `Reviewer` و `CreatedOn` مدرجة مع القيم الخاصة بها.

## مثال كامل يعمل

فيما يلي البرنامج الكامل المتكامل الذي يجمع جميع المقاطع السابقة. انسخه إلى `Program.cs` وشغّله؛ سيعرض وحدة التحكم القيم المسترجعة.

```csharp
using System;
using Aspose.Cells;

namespace ExcelCustomPropertiesDemo
{
    class Program
    {
        static void Main()
        {
            // Paths (adjust to your environment)
            var sourcePath = @"YOUR_DIRECTORY\Data.xlsb";
            var resultPath = @"YOUR_DIRECTORY\DataWithProps.xlsb";

            // Load or create workbook
            var workbook = new Workbook(sourcePath);
            var worksheet = workbook.Worksheets[0];

            // Add custom properties
            worksheet.CustomProperties.Add("ProjectId", 12345);
            worksheet.CustomProperties.Add("Reviewer", "John Doe");
            worksheet.CustomProperties.Add("CreatedOn", DateTime.UtcNow);

            // Save the workbook
            workbook.Save(resultPath);
            Console.WriteLine($"Saved workbook with custom properties to {resultPath}");

            // Load the saved workbook to read properties
            var loadedWorkbook = new Workbook(resultPath);
            var loadedWorksheet = loadedWorkbook.Worksheets[0];
            var props = loadedWorksheet.CustomProperties;

            // Read properties
            int projectId = props["ProjectId"] != null ? (int)props["ProjectId"].Value : -1;
            string reviewer = props["Reviewer"] != null ? props["Reviewer"].Value.ToString() : "Unknown";
            DateTime createdOn = props["CreatedOn"] != null ? (DateTime)props["CreatedOn"].Value : DateTime.MinValue;

            Console.WriteLine($"ProjectId: {projectId}");
            Console.WriteLine($"Reviewer: {reviewer}");
            Console.WriteLine($"CreatedOn (UTC): {createdOn:u}");
        }
    }
}
```

تشغيل هذا البرنامج ينتج ناتج وحدة التحكم الموضح سابقًا ويُنشئ ملف `DataWithProps.xlsb` يحتوي على البيانات الوصفية المدمجة.

## أسئلة شائعة وحالات خاصة

| السؤال | الجواب |
|---|---|
| **هل يمكنني تخزين أنواع غير بدائية؟** | يدعم Aspose.Cells الأنواع `string` و `int` و `double` و `DateTime` و `bool`. بالنسبة للكائنات المعقدة، قم بتحويلها إلى JSON أو XML أولاً وخزن السلسلة. |
| **ماذا لو كان المصنف محميًا بكلمة مرور؟** | افتح المصنف باستخدام كلمة مرور (`new Workbook(path, password)`) قبل الوصول إلى `CustomProperties`. لا تزال الخصائص متاحة بعد فك التشفير. |
| **هل تبقى الخصائص المخصصة بعد تحويل الصيغة؟** | عند الحفظ بصيغة مختلفة (مثل `.xlsx`)، يحتفظ Aspose.Cells بالخصائص المخصصة طالما أن الصيغة الهدف تدعمها. |
| **كيف أحذف خاصية مخصصة؟** | استخدم `worksheet.CustomProperties.Remove("PropertyName");`. هذا يزيل الإدخال من المجموعة. |

## الخطوات التالية

الآن بعد أن عرفت **إضافة خصائص مخصصة**، يمكنك استكشاف المواضيع ذات الصلة مثل:

* **excel custom properties** لإصدار المستندات  
* **read custom properties** من أوراق عمل متعددة داخل مصنف واحد  
* استخدام **Aspose.Cells** لإنشاء جداول محورية تُشير إلى البيانات الوصفية المخصصة  
* تصدير المصنف إلى PDF مع الحفاظ على الخصائص المخصصة  

جرّب أنواع بيانات مختلفة، اجمع بين الخصائص المخصصة وتعليقات الخلايا، أو دمج البيانات الوصفية في نظام إدارة مستندات أوسع.

---

**هل أنت مستعد لأتمتة تقارير Excel الخاصة بك؟** أضف الشيفرة أعلاه إلى مشروعك، عدّل أسماء الخصائص لتتناسب مع احتياجات عملك، وستحصل على مصنف ذاتي الوصف جاهز للمعالجة اللاحقة.

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مورد يتضمن أمثلة شيفرة كاملة مع شرح خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [Create Excel Workbook – Add Custom Properties and Save as XLSB](/cells/english/net/document-properties/create-excel-workbook-add-custom-properties-and-save-as-xlsb/)
- [How to Access Custom Document Properties in Excel Using Aspose.Cells for .NET](/cells/english/net/workbook-operations/access-custom-excel-properties-aspose-cells-net/)
- [Master Excel Custom Properties Using Aspose.Cells .NET for Enhanced Data Management](/cells/english/net/data-manipulation/excel-custom-properties-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}