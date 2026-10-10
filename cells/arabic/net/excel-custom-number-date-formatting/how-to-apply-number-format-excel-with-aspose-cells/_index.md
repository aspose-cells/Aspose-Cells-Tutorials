---
category: general
date: 2026-10-10
description: تطبيق تنسيق الأرقام في إكسل بسرعة عن طريق استيراد DataTable، وضبط تنسيقات
  التاريخ والعملات، والحفاظ على صف العنوان في إكسل في خطوة واحدة.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- apply number format excel
- set date format excel
- format excel cells date
- set currency format excel
- preserve header row excel
language: ar
lastmod: 2026-10-10
og_description: تطبيق تنسيق الأرقام في إكسل باستخدام C# و Aspose.Cells. تعلّم كيفية
  تعيين تنسيق التاريخ في إكسل، وتعيين تنسيق العملة في إكسل، والحفاظ على صف العنوان
  في إكسل عند استيراد DataTable.
og_image_alt: Excel worksheet showing currency and date columns formatted after import
og_title: تطبيق تنسيق الأرقام في إكسل باستخدام C# – دليل خطوة بخطوة
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: apply number format excel quickly by importing a DataTable, setting
    date and currency formats, and preserving header row excel in a single step.
  headline: How to apply number format excel with Aspose.Cells
  type: TechArticle
tags:
- excel
- aspnet
- csharp
- excel-formatting
title: كيفية تطبيق تنسيق الأرقام في Excel باستخدام Aspose.Cells
url: /ar/net/excel-custom-number-date-formatting/how-to-apply-number-format-excel-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تطبيق تنسيق الأرقام في Excel باستخدام Aspose.Cells

إذا كنت بحاجة إلى **apply number format excel** أثناء تحميل البيانات من `DataTable`، فإن هذا الدليل يوضح لك بالضبط كيفية القيام بذلك. ستتعلم أيضًا كيفية **set date format excel**، **set currency format excel**، و **preserve header row excel** أثناء الاستيراد، بحيث يبدو ورقة العمل الناتجة احترافية دون معالجة إضافية.

سوف نغطي كل شيء بدءًا من تثبيت المكتبة حتى كتابة مقتطف كامل قابل للتنفيذ. في النهاية ستتمكن من استيراد أي `DataTable` إلى مصنف Excel، وتنسيق الأعمدة الرقمية تلقائيًا، والحفاظ على صف العنوان دون تغيير—كل ذلك في بضع أسطر فقط من C#.

## المتطلبات المسبقة

* .NET 6.0 أو أحدث (الكود يعمل أيضًا مع .NET Framework 4.6+)
* Visual Studio 2022 (أو أي بيئة تطوير C# تفضلها)
* **Aspose.Cells for .NET** – التثبيت عبر NuGet:

```bash
dotnet add package Aspose.Cells
```

* مصدر `DataTable` – يستخدم المثال طريقة مساعدة `GetTable()` التي تُرجع بيانات عينة.

> **نصيحة احترافية:** Aspose.Cells هي مكتبة تجارية، لكنها توفر وضع تقييم مجاني يعطل العلامة المائية لمدة تصل إلى 30 يومًا.

## الخطوة 1: إنشاء مصنف والوصول إلى ورقة العمل الأولى

كائن المصنف هو نقطة الدخول لجميع عمليات Excel. إنشاء مصنف جديد يمنحك ورقة عمل افتراضية في الفهرس 0.

```csharp
using Aspose.Cells;
using System;
using System.Data;

class Program
{
    static void Main()
    {
        // Create a new workbook
        Workbook wb = new Workbook();

        // Obtain reference to the first worksheet
        Worksheet sheet = wb.Worksheets[0];
```

*لماذا هذه الخطوة؟*  
`Workbook` يدير تنسيق الملف، محرك الحسابات، ومستودع الأنماط. الوصول إلى `Worksheet` مبكرًا يتيح لنا تمرير ورقة الهدف إلى طريقة الاستيراد لاحقًا.

## الخطوة 2: استرجاع البيانات المصدر كـ DataTable

في المشاريع الحقيقية غالبًا ما تأتي البيانات من استعلام قاعدة بيانات، أو محلل CSV، أو استجابة API. للتوضيح، نقوم بإنشاء `DataTable` بسيط يحتوي على ثلاثة أعمدة: **Product**، **Price**، و **ReleaseDate**.

```csharp
        // Step 2: Retrieve the source data as a DataTable
        DataTable sourceTable = GetTable();
```

```csharp
        // Helper method that builds a sample DataTable
        static DataTable GetTable()
        {
            DataTable dt = new DataTable();
            dt.Columns.Add("Product", typeof(string));
            dt.Columns.Add("Price", typeof(decimal));
            dt.Columns.Add("ReleaseDate", typeof(DateTime));

            dt.Rows.Add("Widget A", 12.99m, new DateTime(2023, 5, 1));
            dt.Rows.Add("Widget B", 23.50m, new DateTime(2023, 6, 15));
            dt.Rows.Add("Widget C", 7.75m, new DateTime(2023, 7, 30));
            return dt;
        }
```

*لماذا هذه الخطوة؟*  
`DataTable` يوفر تمثيلًا جدوليًا في الذاكرة يمكن لـ Aspose.Cells استيراده مباشرةً، مع الحفاظ على ترتيب الأعمدة وأنواع البيانات.

## الخطوة 3: إعداد مصفوفة `Style` – نمط واحد لكل عمود

يتيح لك Aspose.Cells تطبيق نمط مميز لكل عمود أثناء الاستيراد عن طريق تمرير مصفوفة من كائنات `Style`. يجب أن يتطابق طول المصفوفة مع عدد الأعمدة في جدول المصدر.

```csharp
        // Step 3: Prepare an array of Style objects – one for each column
        Style[] columnStyles = new Style[sourceTable.Columns.Count];
        for (int i = 0; i < columnStyles.Length; i++)
        {
            // Each entry must be instantiated before we can set properties
            columnStyles[i] = wb.CreateStyle();
        }
```

*لماذا هذه الخطوة؟*  
إذا تخطيت الإنشاء الصريح (`CreateStyle()`)، فإن محاولة تعيين `Number` ستؤدي إلى رمي `NullReferenceException`. تهيئة كل `Style` يضمن نجاح التعيينات اللاحقة.

## الخطوة 4: تعيين تنسيقات الأرقام – العملة والتاريخ

Excel يحدد تنسيقات الأرقام المدمجة عبر المعرف (ID).

* **14** – Currency (مثال، `$1,234.00`)
* **22** – Short Date (`mm/dd/yyyy`)

```csharp
        // Step 4: Assign number formats to the desired columns
        // Column 0 – Product name (no format needed)
        // Column 1 – Currency format (Number format ID 14)
        columnStyles[1].Number = 14;   // set currency format excel

        // Column 2 – Date format (Number format ID 22)
        columnStyles[2].Number = 22;   // set date format excel
```

> **ملاحظة:** إذا كنت بحاجة إلى تنسيق مخصص (مثال، `"¥#,##0.00"`)، استخدم `Style.Custom = "¥#,##0.00"` بدلاً من معرف مدمج.

*لماذا هذه الخطوة؟*  
تطبيق **number format** الصحيح أثناء الاستيراد يلغي الحاجة إلى تمريرة ثانية تمر عبر الخلايا لتغيير التنسيق. كما يضمن أن **format excel cells date** و **set currency format excel** يكونان متسقين عبر جميع الصفوف.

## الخطوة 5: استيراد DataTable مع الحفاظ على صف العنوان

طريقة `ImportDataTable` يمكنها نسخ البيانات، الحفاظ على الصف الأول كعنوان، وتطبيق أنماط الأعمدة التي أعددناها.

```csharp
        // Step 5: Import the DataTable into the worksheet
        // Parameters:
        //   sourceTable – the DataTable to import
        //   true        – preserve the header row (preserve header row excel)
        //   "A1"        – start cell
        //   columnStyles – array of styles for each column
        sheet.Cells.ImportDataTable(sourceTable, true, "A1", columnStyles);
```

```csharp
        // Save the workbook to disk
        wb.Save("FormattedReport.xlsx");
        Console.WriteLine("Workbook created successfully.");
    }
}
```

**الناتج المتوقع** – افتح `FormattedReport.xlsx` وسترى:

| Product | Price (currency) | ReleaseDate (date) |
|---------|------------------|--------------------|
| Widget A| $12.99           | 05/01/2023         |
| Widget B| $23.50           | 06/15/2023         |
| Widget C| $7.75            | 07/30/2023         |

صف العنوان يبقى كما هو، عمود **Price** يعرض رمز العملة، وعمود **ReleaseDate** يظهر تنسيق تاريخ قصير—كل ذلك دون أي كود تنسيق إضافي.

### التعامل مع الحالات الشائعة

| الحالة | الحل |
|--------|------|
| **المزيد من الأعمدة مقارنة بالأنماط** | تأكد من أن `columnStyles.Length` يساوي `sourceTable.Columns.Count`. القيم المفقودة تُستخدم النمط الافتراضي للمصنف. |
| **القيم الفارغة في الأعمدة الرقمية** | Excel يتعامل مع `null` كخلية فارغة؛ لا يزال تنسيق الرقم يُطبق عندما يتم إدخال قيمة لاحقًا. |
| **عملة مخصصة حسب الإعدادات المحلية** | استخدم `columnStyles[i].Custom = "\"€\"#,##0.00"` وضع `columnStyles[i].Number = -1` لتعطيل المعرف المدمج. |
| **جداول كبيرة ( > 100 000 صف )** | فكر في استخدام نسخة `ImportDataTable` مع `ImportTableOptions` لتدفق البيانات وتقليل الضغط على الذاكرة. |
| **تطبيق نفس النمط على أعمدة متعددة** | أعد استخدام نفس كائن `Style` في المصفوفة (مثال، `columnStyles[1] = columnStyles[2] = dateStyle;`). |

## مكافأة: استخدام سلسلة تنسيق مخصصة

إذا لم تلبي المعرفات المدمجة احتياجاتك، يمكنك تعريف تنسيق رقم مخصص:

```csharp
// Example: display Euro currency with no decimal places
Style euroStyle = wb.CreateStyle();
euroStyle.Custom = "\"€\"#,##0";
columnStyles[1] = euroStyle;   // replace the built‑in currency style
```

هذه الطريقة تمنحك تحكمًا كاملاً في **format excel cells date** و **set currency format excel** خارج المعرفات المحددة مسبقًا.

## الخلاصة

أنت الآن تعرف كيفية **apply number format excel** بفعالية عند استيراد `DataTable` باستخدام Aspose.Cells. من خلال إنشاء مصفوفة `Style` لكل عمود، وتعيين معرفات أرقام مدمجة أو مخصصة، واستخدام نسخة `ImportDataTable` التي **preserve header row excel**، يمكنك إنشاء أوراق عمل جاهزة للنشر في عملية واحدة.

### ما التالي؟

* استكشف **set date format excel** بأنماط مخصصة مثل `"dddd, mmmm dd, yyyy"`.
* دمج هذه التقنية مع **conditional formatting** لتسليط الضوء على القيم خارج النطاق.
* استخدم **format excel cells date** في جداول Pivot أو المخططات للتقارير الديناميكية.

لا تتردد في تجربة معرفات أرقام مختلفة أو سلاسل مخصصة لتتناسب مع دليل نمط مؤسستك. ترميز سعيد!

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مورد يتضمن أمثلة كود كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [تطبيق تنسيق الأرقام في Excel – دليل خطوة بخطوة لتنسيق الأعمدة](/cells/english/net/number-and-display-formats-in-excel/apply-number-format-excel-step-by-step-guide-to-formatting-c/)
- [إنشاء مصنف Excel C# – تطبيق تنسيق العملة واستيراد DataTable](/cells/english/net/excel-data-import-export/create-excel-workbook-c-apply-currency-format-and-import-dat/)
- [تعيين تنسيق التاريخ في Excel باستخدام C# – دليل كامل لتنسيق الاستيراد](/cells/english/net/excel-custom-number-date-formatting/set-date-format-in-excel-with-c-full-import-formatting-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}