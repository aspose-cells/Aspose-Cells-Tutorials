---
category: general
date: 2026-10-07
description: تعلم كيف تقوم Aspose.Cells بحذف الصفوف من جدول Excel، وإزالة الصفوف باستثناء
  العنوان، والتعامل مع حذف صفوف الجدول المحمي باستخدام كود C# نظيف.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- aspose cells delete rows
- delete rows excel table
- excel table row deletion
- protect excel table rows
- remove rows except header
language: ar
lastmod: 2026-10-07
og_description: Aspose.Cells حذف الصفوف من جدول Excel مع الحفاظ على رأس الجدول. يوضح
  هذا الدليل الحل الكامل بلغة C#، مع معالجة الجداول المحمية وحالات الحافة الشائعة.
og_image_alt: Aspose.Cells delete rows example showing code and Excel screenshot
og_title: Aspose.Cells حذف الصفوف – إزالة جميع الصفوف ما عدا العنوان في C#
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: Learn how Aspose.Cells delete rows from an Excel table, remove rows
    except header, and handle protected table row deletion with clean C# code.
  headline: How to use Aspose.Cells to delete rows in an Excel table while keeping
    the header
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
title: كيفية استخدام Aspose.Cells لحذف الصفوف في جدول Excel مع الحفاظ على رأس الجدول
url: /ar/net/row-and-column-management/how-to-use-aspose-cells-to-delete-rows-in-an-excel-table-whi/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية استخدام Aspose.Cells لحذف الصفوف في جدول Excel مع الحفاظ على رأس الجدول

إذا كنت بحاجة إلى **aspose cells delete rows** من جدول ولكنك تريد الحفاظ على صف الرأس، فإن هذا الدليل يوضح حلاً كاملاً وقابلاً للتنفيذ. سترى لماذا فشل الاستدعاء المباشر لـ `ListObject.DeleteRows` عندما يكون الجدول محميًا، وكيفية تجاوز هذه القيود دون الإضرار بسلامة البيانات.

يغطي الدليل:

* تحميل مصنف يحتوي على جدول محمي.  
* اكتشاف وإلغاء حماية الجدول مؤقتًا.  
* حذف كل صف بيانات مع الحفاظ على الرأس.  
* استعادة حالة الحماية الأصلية.  

بنهاية المقال يمكنك تنفيذ عمليات **delete rows excel table** بثقة في أي مشروع Aspose.Cells.

## المتطلبات المسبقة

* .NET 6.0 أو أحدث (الكود يعمل أيضًا مع .NET Framework 4.7.2+).  
* Aspose.Cells for .NET 23.9 أو أحدث.  
* إلمام أساسي بـ C# وجداول Excel (المعروفة أيضًا باسم ListObjects).  

لا توجد حزم NuGet إضافية مطلوبة بخلاف Aspose.Cells.

## الخطوة 1: إعداد المشروع واستيراد المساحات الاسمية

أنشئ تطبيقًا كونسول جديدًا أو أضف الكود التالي إلى مشروع موجود. استورد مساحات أسماء Aspose.Cells حتى يتمكن المترجم من التعرف على `Workbook` و `Worksheet` و `ListObject`.

```csharp
using System;
using Aspose.Cells;

namespace AsposeCellsTableRowDeletion
{
    class Program
    {
        static void Main()
        {
            // The full solution starts in Step 2.
        }
    }
}
```

*لماذا هذه الخطوة مهمة* – استيراد المساحات الاسمية الصحيحة يمنع أخطاء الأنواع المتضاربة ويجعل بقية الكود أوضح.

## الخطوة 2: تحميل المصنف وتحديد جدول الهدف

استبدل `"YOUR_DIRECTORY/TableProtection.xlsx"` بالمسار إلى ملف Excel الخاص بك. يفترض المثال أن الجدول الذي تريد تعديله اسمه **Orders**.

```csharp
// Load the workbook that contains the protected table
Workbook workbook = new Workbook("YOUR_DIRECTORY/TableProtection.xlsx");

// Get the first worksheet (index 0) and the ListObject named "Orders"
Worksheet worksheet = workbook.Worksheets[0];
ListObject ordersTable = worksheet.ListObjects["Orders"];
```

*لماذا هذه الخطوة مهمة* – الوصول إلى `ListObject` يمنحك مقبضًا مباشرًا للجدول، وهو ما يلزم لأي عملية **excel table row deletion**.

## الخطوة 3: التحقق مما إذا كان الجدول محميًا

تمنع Aspose.Cells حذف جزء من الجدول عندما يكون محميًا. محاولة استدعاء `ordersTable.DeleteRows` في تلك الحالة تُثير استثناءً. اكتشف حالة الحماية أولًا.

```csharp
bool wasProtected = ordersTable.IsProtected;
Console.WriteLine($"Table protection status: {(wasProtected ? "protected" : "unprotected")}");
```

*لماذا هذه الخطوة مهمة* – معرفة حالة الحماية يتيح لك اتخاذ قرار بإلغاء الحماية مؤقتًا، مما يضمن احترام قاعدة **protect excel table rows** بعد العملية.

## الخطوة 4: إلغاء حماية الجدول مؤقتًا (إذا لزم الأمر)

إذا كان الجدول محميًا، استخدم `Unprotect` مع كلمة المرور (إن وجدت). للجداول بدون كلمة مرور، ما عليك سوى استدعاء `Unprotect()`.

```csharp
if (wasProtected)
{
    // Provide the password if the table was protected with one; otherwise, pass null.
    ordersTable.Unprotect(null);
    Console.WriteLine("Table temporarily unprotected.");
}
```

*لماذا هذه الخطوة مهمة* – إلغاء حماية الجدول يسمح لـ Aspose.Cells بتنفيذ **aspose cells delete rows** دون رفع استثناء، مع إمكانية استعادة الحماية لاحقًا.

## الخطوة 5: حذف جميع الصفوف باستثناء الرأس

يشغل الرأس الصف الأول من الجدول (`RowCount` تشمل الرأس). حذف الصفوف بدءًا من الفهرس 1 يزيل كل صف بيانات.

```csharp
int dataRows = ordersTable.RowCount - 1; // Exclude the header row
if (dataRows > 0)
{
    ordersTable.DeleteRows(1, dataRows);
    Console.WriteLine($"{dataRows} data rows removed, header preserved.");
}
else
{
    Console.WriteLine("Table contains only the header; nothing to delete.");
}
```

*لماذا هذه الخطوة مهمة* – هذا الكود ينفذ الوظيفة الأساسية **remove rows except header** مع تجنب الاستثناء الذي يحدث عند حذف جزئي في جداول محمية.

## الخطوة 6: إعادة تطبيق الحماية (إذا كانت مُعَدة أصلاً)

بعد حذف الصفوف، استعد الحالة الأصلية للحماية حتى يعود المصنف إلى سلوكه السابق تمامًا.

```csharp
if (wasProtected)
{
    // Re‑apply protection with the same password (null if none was used)
    ordersTable.Protect(null);
    Console.WriteLine("Table protection restored.");
}
```

*لماذا هذه الخطوة مهمة* – استعادة الحماية تحترم متطلب **protect excel table rows** وتبقي المصنف آمنًا للمستخدمين اللاحقين.

## الخطوة 7: حفظ المصنف المعدل

اختر اسم ملف جديد لتجنب الكتابة فوق الملف الأصلي، ما لم تكن الكتابة فوق مقصودة.

```csharp
string outputPath = "YOUR_DIRECTORY/TableProtection_Modified.xlsx";
workbook.Save(outputPath);
Console.WriteLine($"Modified workbook saved to: {outputPath}");
```

*لماذا هذه الخطوة مهمة* – الحفظ يُكمل عملية **excel table row deletion** ويعطيك نتيجة ملموسة يمكنك فتحها في Excel للتحقق.

## مثال كامل يعمل

جمع جميع الخطوات معًا ينتج برنامجًا ذاتيًا يمكنك نسخه، لصقه، وتشغيله.

```csharp
using System;
using Aspose.Cells;

namespace AsposeCellsTableRowDeletion
{
    class Program
    {
        static void Main()
        {
            // 1. Load workbook
            Workbook workbook = new Workbook("YOUR_DIRECTORY/TableProtection.xlsx");
            Worksheet worksheet = workbook.Worksheets[0];
            ListObject ordersTable = worksheet.ListObjects["Orders"];

            // 2. Remember protection state
            bool wasProtected = ordersTable.IsProtected;
            Console.WriteLine($"Table protection status: {(wasProtected ? "protected" : "unprotected")}");

            // 3. Unprotect if needed
            if (wasProtected)
            {
                ordersTable.Unprotect(null); // use password if applicable
                Console.WriteLine("Table temporarily unprotected.");
            }

            // 4. Delete all rows except header
            int dataRows = ordersTable.RowCount - 1;
            if (dataRows > 0)
            {
                ordersTable.DeleteRows(1, dataRows);
                Console.WriteLine($"{dataRows} data rows removed, header preserved.");
            }
            else
            {
                Console.WriteLine("Table contains only the header; nothing to delete.");
            }

            // 5. Restore protection
            if (wasProtected)
            {
                ordersTable.Protect(null); // re‑apply with original password if any
                Console.WriteLine("Table protection restored.");
            }

            // 6. Save the workbook
            string outputPath = "YOUR_DIRECTORY/TableProtection_Modified.xlsx";
            workbook.Save(outputPath);
            Console.WriteLine($"Modified workbook saved to: {outputPath}");
        }
    }
}
```

### النتيجة المتوقعة

```
Table protection status: protected
Table temporarily unprotected.
5 data rows removed, header preserved.
Table protection restored.
Modified workbook saved to: YOUR_DIRECTORY/TableProtection_Modified.xlsx
```

افتح `TableProtection_Modified.xlsx` في Excel. سترى جدول **Orders** مع بقاء صف الرأس فقط؛ جميع صفوف البيانات قد أزيلت.

## معالجة التغييرات الشائعة وحالات الحافة

| الوضع | التعديل الموصى به | السبب |
|-----------|-------------------|--------|
| الجدول يستخدم كلمة مرور | تمرير كلمة المرور إلى `Unprotect` و `Protect` | يضمن نفس مستوى الأمان بعد العملية |
| الجدول لا يحتوي على صفوف بيانات | تخطي استدعاء `DeleteRows` | يمنع حدوث `ArgumentOutOfRangeException` |
| عدة جداول تحتاج إلى التنظيف | التكرار عبر `worksheet.ListObjects` وتطبيق نفس المنطق | يوسع نمط **delete rows excel table** إلى كامل الورقة |
| تريد الاحتفاظ بالرأس والصف البيانات الأول | تغيير `DeleteRows(2, dataRows‑1)` | يبدأ الحذف بعد الصف الثاني، مع الحفاظ على الصف البيانات الأول |

تظهر هذه التغييرات معالجة قوية لـ **excel table row deletion** وتؤكد لماذا النهج المقدم هو الموصى به.

## نصائح احترافية

* **Batch processing** – إذا كنت بحاجة إلى حذف صفوف من العديد من المصنفات، غلف المنطق في طريقة قابلة لإعادة الاستخدام تستقبل معلمات `Workbook` و `tableName`.  
* **Performance** – حذف الصفوف في استدعاء واحد (`DeleteRows`) أسرع من حذف الصفوف واحدًا تلو الآخر لأن Aspose.Cells يحدث هياكل البيانات الداخلية مرة واحدة فقط.  
* **Safety** – اعمل دائمًا على نسخة من الملف الأصلي أو احتفظ بنسخة احتياطية قبل تطبيق الحذف، خاصةً عندما تكون **protect excel table rows** متضمنة.

## الخلاصة

الآن لديك حل كامل وجاهز للإنتاج لـ **aspose cells delete rows** مع الحفاظ على رأس جدول Excel. غطى الدليل تحميل المصنف، التعامل مع الجداول المحمية، تنفيذ عملية **remove rows except header**، واستعادة الحماية. طبّق النمط نفسه على أي سيناريو **excel table row deletion**، وعدّل الكود ليتناسب مع متطلبات إضافية مثل الجداول المحمية بكلمة مرور أو المعالجة الدفعية.

---

*الخطوات التالية* – استكشف مواضيع ذات صلة مثل **delete rows excel table** مع الفلاتر، دمج الخلايا بعد حذف الصفوف، أو استخدام Aspose.Cells لنسخ الجداول بين المصنفات. كلٌ منها يبني على المفاهيم الأساسية الموضحة هنا ويعمق إتقانك لأتمتة Excel باستخدام Aspose.Cells.

## ماذا يجب أن تتعلم بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مورد يتضمن أمثلة كود كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [Aspose Cells Delete Rows – Protect Header Row in Excel](/cells/english/net/row-and-column-management/aspose-cells-delete-rows-protect-header-row-in-excel/)
- [How to Insert and Delete Rows in Excel with Aspose.Cells for .NET: A Comprehensive Guide](/cells/english/net/data-manipulation/aspose-cells-net-insert-delete-excel-rows/)
- [How to Delete Blank Rows in Excel Using Aspose.Cells .NET for Data Cleanup](/cells/english/net/data-manipulation/delete-blank-rows-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}