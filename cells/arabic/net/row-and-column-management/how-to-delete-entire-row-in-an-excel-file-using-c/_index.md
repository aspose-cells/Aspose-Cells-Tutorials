---
category: general
date: 2026-10-10
description: تعلم كيفية حذف صف كامل في مصنف Excel باستخدام C#. يغطي هذا الدليل خطوة
  بخطوة أيضًا كيفية حذف صف حسب الفهرس وإزالة صف حسب الفهرس باستخدام Aspose.Cells.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- delete entire row
- how to delete row
- remove row by index
- delete row excel
- delete row c#
language: ar
lastmod: 2026-10-10
og_description: احذف الصف بالكامل في مصنف Excel باستخدام C#. اتبع هذا الدليل لتتعلم
  كيفية حذف الصف حسب الفهرس، وإزالة الصف حسب الفهرس، وحفظ الملف بأمان.
og_image_alt: Screenshot of an Excel worksheet before and after deleting an entire
  row with C# code
og_title: حذف الصف بالكامل في إكسل باستخدام C# – دليل برمجي كامل
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: Learn how to delete entire row in an Excel workbook with C#. This step‑by‑step
    guide also covers how to delete row by index and remove row by index using Aspose.Cells.
  headline: How to delete entire row in an Excel file using C#
  type: TechArticle
tags:
- Excel
- C#
- Aspose.Cells
title: كيفية حذف الصف بالكامل في ملف Excel باستخدام C#
url: /ar/net/row-and-column-management/how-to-delete-entire-row-in-an-excel-file-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# حذف صف كامل في ملف Excel باستخدام C#

إذا كنت بحاجة إلى **حذف صف كامل** في مصنف Excel، يوضح لك هذا الدليل بالضبط كيفية القيام بذلك باستخدام C#. سواءً كنت تقوم بتنظيف البيانات المستوردة أو بناء أداة تقارير، فإن الخطوات أدناه تتيح لك إزالة صف بناءً على فهرسه وحفظ النتيجة دون فقدان البيانات الأخرى.

سترى أيضًا كيف يجيب النهج نفسه على سؤال **how to delete row** حسب الفهرس، وكيفية **remove row by index**، ولماذا يعمل هذا في سيناريوهات **delete row excel** باستخدام C#.

## المتطلبات المسبقة

* .NET 6.0 أو أحدث (الكود يعمل مع .NET Framework 4.6+ أيضًا)  
* مكتبة **Aspose.Cells for .NET** (متوفرة عبر NuGet: `Install-Package Aspose.Cells`)  
* إلمام أساسي بمشاريع C# للكونسول أو سطح المكتب  

لا توجد حاجة لمكوّنات Excel interop أو COM إضافية، مما يجعل الحل خفيف الوزن وآمنًا للتنفيذ على الخادم.

## الخطوة 1: إعداد المشروع واستيراد المساحات الاسمية

أنشئ تطبيق كونسول جديد (أو أضف الكود إلى مشروع موجود) وأضف توجيهات `using` المطلوبة:

```csharp
using System;
using Aspose.Cells;

namespace ExcelRowDeletion
{
    class Program
    {
        static void Main(string[] args)
        {
            // The rest of the tutorial code lives here.
        }
    }
}
```

*لماذا هذا مهم*: استيراد `Aspose.Cells` يمنحك الوصول إلى `Workbook` و `Worksheet` وطريقة `DeleteRows` التي تقوم بالحذف الفعلي للصف.

## الخطوة 2: تحميل المصنف واختيار ورقة العمل

يجب عليك تحميل ملف المصدر (`input.xlsx`) والحصول على ورقة العمل التي تريد تعديلها. يتم الوصول إلى ورقة العمل الأولى باستخدام الفهرس `0`.

```csharp
// Load the workbook from disk
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

// Get the first worksheet (you can also use workbook.Worksheets["SheetName"])
Worksheet ws = workbook.Worksheets[0];
```

> **نصيحة**: إذا كنت بحاجة للعمل مع ورقة معينة، استبدل الفهرس باسم الورقة: `workbook.Worksheets["Data"]`.

## الخطوة 3: حذف الصف بالكامل باستخدام فهرسه الصفري

تستخدم Aspose.Cells الفهرسة الصفريّة، لذا فإن الصف الأول هو `0`. لحذف الصف 5 (الصف البصري السادس)، استدعِ `DeleteRows` مع `DeleteOptions.DeleteEntireRow`.

```csharp
// Delete one row starting at index 5 (zero‑based) and remove the whole row
ws.Cells[5, 0].DeleteRows(1, DeleteOptions.DeleteEntireRow);
```

*شرح*:

* `ws.Cells[5, 0]` يشير إلى الخلية الأولى في الصف الذي تريد حذفه.  
* `DeleteRows(1, DeleteOptions.DeleteEntireRow)` يخبر Aspose.Cells بحذف **1** صف، وعلم `DeleteEntireRow` يضمن أن **الصف بأكمله** يختفي، مع إزاحة الصفوف أدناه إلى الأعلى.

### كيفية حذف صف حسب الفهرس في سيناريوهات أخرى

* **حذف عدة صفوف متتالية** – غيّر الوسيط الأول إلى عدد الصفوف التي تريد مسحها:

  ```csharp
  // Remove rows 5, 6 and 7 (three rows total)
  ws.Cells[5, 0].DeleteRows(3, DeleteOptions.DeleteEntireRow);
  ```

* **حذف الصف الأخير** – استخدم `ws.Cells.MaxDataRow` للحصول على فهرس أسفل صف ممتلئ:

  ```csharp
  int lastRow = ws.Cells.MaxDataRow;
  ws.Cells[lastRow, 0].DeleteRows(1, DeleteOptions.DeleteEntireRow);
  ```

هذه القطع البرمجية تجيب على متطلبات **remove row by index** مع الحفاظ على سهولة قراءة الكود.

## الخطوة 4: حفظ المصنف بعد إزالة الصف

بعد الحذف، اكتب المصنف المعدل مرة أخرى إلى القرص. يمكنك استبدال الملف الأصلي أو إنشاء ملف جديد.

```csharp
// Save the workbook to a new file (or overwrite the original)
workbook.Save("YOUR_DIRECTORY/output.xlsx");
```

إذا كنت بحاجة للحفاظ على الملف الأصلي دون تغيير، ما عليك سوى تعديل مسار الإخراج. تدعم طريقة `Save` العديد من الصيغ (`.xls`, `.csv`, `.pdf`, إلخ) – فقط غيّر امتداد الملف.

## مثال كامل يعمل

بجمع كل شيء معًا، إليك برنامج كامل وجاهز للتنفيذ:

```csharp
using System;
using Aspose.Cells;

namespace ExcelRowDeletion
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the workbook
            Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

            // 2️⃣ Select the first worksheet
            Worksheet ws = workbook.Worksheets[0];

            // 3️⃣ Delete the entire row at index 5 (sixth visual row)
            ws.Cells[5, 0].DeleteRows(1, DeleteOptions.DeleteEntireRow);

            // 4️⃣ Save the result
            workbook.Save("YOUR_DIRECTORY/output.xlsx");

            Console.WriteLine("Row deleted successfully. Output saved to output.xlsx");
        }
    }
}
```

**الناتج المتوقع**: بعد تشغيل البرنامج، سيحتوي `output.xlsx` على جميع الصفوف الأصلية باستثناء الصف الذي بدأ في الصف البصري 6. جميع البيانات أسفل الصف المحذوف تُرفع تلقائيًا، مع الحفاظ على الصيغ والتنسيق.

## الأخطاء الشائعة وكيفية تجنبها

| المشكلة | لماذا يحدث | الحل |
|-------|----------------|-----|
| **فهرس خارج النطاق** | محاولة حذف فهرس صف غير موجود (مثال: `ws.Cells[1000,0]` في ورقة تحتوي على 200 صف) | استخدم `ws.Cells.MaxDataRow` للتحقق من أعلى فهرس صالح قبل استدعاء `DeleteRows`. |
| **حذف جزئي للصف** | إغفال `DeleteOptions.DeleteEntireRow` يؤدي إلى مسح محتويات الخلايا فقط | دائمًا مرّر `DeleteOptions.DeleteEntireRow` عندما تحتاج إلى حذف الصف بالكامل. |
| **تغييرات غير متوقعة في الصيغ** | حذف صفوف تشكل جزءًا من نطاق صيغ قد يكسر المراجع | أعد تقييم الصيغ بعد الحذف (`workbook.CalculateFormula()`) إذا كان المصنف يعتمد على نطاقات ديناميكية. |
| **الحفظ في موقع للقراءة فقط** | استدعاء `Save` يطرح استثناءً إذا كان المجلد محميًا | تأكد من أن الدليل الهدف قابل للكتابة أو شغّل البرنامج بالأذونات المناسبة. |

معالجة هذه القضايا تجعل الحل قويًا للاستخدام في الإنتاج ويُلبي استفسارات **delete row excel** و **delete row c#**.

## متقدم: حذف الصفوف بناءً على شرط

أحيانًا تحتاج إلى إزالة الصفوف التي تلبي معيارًا معينًا (مثال: الصفوف التي يكون فيها العمود A فارغًا). الحلقة التالية توضح طريقة آمنة للمسح من الأسفل إلى الأعلى وحذف الصفوف المطابقة:

```csharp
int lastRow = ws.Cells.MaxDataRow;
for (int row = lastRow; row >= 0; row--)
{
    // Check if column A (index 0) is empty
    if (ws.Cells[row, 0].StringValue == string.Empty)
    {
        ws.Cells[row, 0].DeleteRows(1, DeleteOptions.DeleteEntireRow);
    }
}
workbook.Save("YOUR_DIRECTORY/cleaned.xlsx");
```

المسح من الأسفل إلى الأعلى يمنع مشكلة تغيير الفهرس التي تحدث عند حذف الصفوف أثناء التكرار من الأعلى إلى الأسفل.

## الخلاصة

الآن تعرف كيف **تحذف صفًا كاملًا** في مصنف Excel باستخدام C#. يغطي الدليل:

* تحميل مصنف واختيار ورقة العمل  
* استخدام `DeleteRows` مع `DeleteOptions.DeleteEntireRow` لـ **how to delete row** حسب الفهرس  
* حفظ الملف المعدل بأمان  
* معالجة الحالات الطرفية، نصائح الأداء، ومثال على الحذف الشرطي  

باستخدام هذه المعرفة يمكنك تنفيذ وظيفة **remove row by index** بثقة، أتمتة تنظيف البيانات، وتكامل معالجة Excel في أي تطبيق C#.

**الخطوات التالية**: استكشف ميزات أخرى في Aspose.Cells مثل إدراج الصفوف، نسخ النطاقات، أو تحويل المصنف إلى PDF—كل منها يبني على نفس كائنات `Workbook` و `Worksheet` التي تعلمتها للتو. برمجة سعيدة!

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مصدر يتضمن أمثلة كود كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [كيفية حذف صف Excel باستخدام Aspose.Cells .NET: دليل شامل](/cells/english/net/worksheet-management/delete-excel-row-aspose-cells-net-tutorial/)
- [Aspose Cells حذف الصفوف – حماية صف الرأس في Excel](/cells/english/net/row-and-column-management/aspose-cells-delete-rows-protect-header-row-in-excel/)
- [إدارة الصفوف بكفاءة في Excel باستخدام Aspose.Cells للـ Java: إدراج وحذف الصفوف](/cells/english/java/worksheet-management/aspose-cells-java-row-operations-excel/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}