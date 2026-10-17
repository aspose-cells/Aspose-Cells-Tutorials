---
category: general
date: 2026-06-27
description: نسخ جدول محوري إلى ورقة أخرى في C# باستخدام Aspose.Cells. تعلم خطوة بخطوة
  كيفية الحفاظ على بيانات الجدول المحوري والتنسيق.
draft: false
keywords:
- copy pivot table to another sheet
- Aspose.Cells copy pivot
- Excel pivot duplication
- preserve pivot formatting
- copy range with pivot
language: ar
og_description: نسخ جدول محوري إلى ورقة أخرى في C# باستخدام Aspose.Cells. يوضح هذا
  الدرس بالضبط كيفية تكرار جدول محوري مع الحفاظ على تنسيقه دون تغيير.
og_title: نسخ جدول محوري إلى ورقة أخرى – دليل C# الكامل
schemas:
- author: Aspose
  dateModified: '2026-06-27'
  description: Copy pivot table to another sheet in C# using Aspose.Cells. Learn step‑by‑step
    how to preserve pivot data and formatting.
  headline: Copy Pivot Table to Another Sheet – Complete C# Guide
  type: TechArticle
tags:
- Excel automation
- C#
- Aspose.Cells
title: نسخ جدول محوري إلى ورقة أخرى – دليل C# الكامل
url: /ar/net/pivot-tables/copy-pivot-table-to-another-sheet-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# نسخ جدول محوري إلى ورقة أخرى – دليل C# الكامل

هل احتجت يومًا إلى **نسخ جدول محوري إلى ورقة أخرى** لكنك كنت قلقًا من فقدان أدوات التقطيع، الحقول المحسوبة، أو التنسيق؟ لست وحدك. يواجه العديد من المطورين هذه المشكلة عند أتمتة تقارير Excel، والإحباط حقيقي. في هذا الدليل سنستعرض حلاً نظيفًا وشاملًا ي **يحافظ على الجدول المحوري** تمامًا كما هو.

سنستخدم **Aspose.Cells for .NET**، مكتبة قوية تتيح لك التعامل مع ملفات Excel دون الحاجة إلى فتح Excel نفسه. بنهاية هذا الشرح ستحصل على مقتطف C# جاهز للتنفيذ ينسخ جدولًا محوريًا من ورقة عمل إلى أخرى، مع الحفاظ على جميع اتصالات البيانات الأساسية.

## ما يغطيه هذا الشرح

- إعداد مشروع .NET وإضافة حزمة Aspose.Cells عبر NuGet.  
- تحميل مصنف موجود يحتوي بالفعل على جدول محوري.  
- تعريف كل من النطاق المصدر (الجدول المحوري الأصلي) والنطاق الهدف في ورقة مختلفة.  
- استخدام `CopyOptions` ل **preserve the pivot table** أثناء النسخ.  
- حفظ النتيجة والتحقق من أن الجدول المحوري يعمل في موقعه الجديد.  

لا أدوات خارجية، ولا نسخ‑لصق يدوي، ولا سحر مخفي—فقط كود بسيط يمكنك إدراجه في أي تطبيق كونسول C# أو خدمة.

> **Why you should care:** أتمتة تكرار الجداول المحورية توفر ساعات من العمل اليدوي، خاصةً في خطوط تقارير الليلية حيث تحتاج العشرات من المصنفات إلى هياكل محورية متطابقة عبر عدة أوراق.

---

## الخطوة 1: إعداد المشروع وإضافة Aspose.Cells

أولاً وقبل كل شيء. إذا لم تقم بذلك بعد، أنشئ مشروع كونسول .NET جديد:

```bash
dotnet new console -n PivotCopyDemo
cd PivotCopyDemo
```

الآن أضف حزمة Aspose.Cells:

```bash
dotnet add package Aspose.Cells
```

> **Pro tip:** استخدم أحدث نسخة مستقرة (اعتبارًا من يونيو 2026 v23.12). تتضمن إصلاحات للأخطاء المتعلقة بمعالجة `CopyPivotTable`.

## الخطوة 2: تحميل المصنف والوصول إلى أوراق العمل

افتح المصنف الذي يحتوي على جدول المحور المصدر. في معظم السيناريوهات الواقعية يكون الملف موجودًا على محرك مشترك، لكن لهذا العرض سنفترض أنه في مجلد محلي يُدعى `YOUR_DIRECTORY`.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Load the workbook containing the source pivot table
        Workbook workbook = new Workbook("YOUR_DIRECTORY/source.xlsx");

        // Step 2: Access the first worksheet (source sheet)
        Worksheet sourceSheet = workbook.Worksheets[0];

        // We'll also create (or reference) a destination sheet
        Worksheet destSheet = workbook.Worksheets.Add("CopyDestination");
```

هنا نقوم بإنشاء ورقة جديدة باسم **CopyDestination** حيث سيتم وضع الجدول المحوري. إذا كان لديك ورقة هدف بالفعل، فقط احصل عليها بالرقم أو الاسم.

## الخطوة 3: تعريف نطاقات المصدر والوجهة

الجدول المحوري موجود داخل كتلة مستطيلة من الخلايا. تحتاج إلى إخبار Aspose.Cells أي كتلة يجب نسخها. في هذا المثال يشغل الجدول المحوري الصفوف 0‑20 والأعمدة 0‑10 (فهرسة صفرية).

```csharp
        // Step 3: Define the source range that includes the pivot table (rows 0‑20, columns 0‑10)
        CellArea sourceRange = new CellArea(0, 0, 20, 10);

        // Step 4: Define the destination start cell (row 30, column 0) on the destination sheet
        // and calculate the target area size to match the source dimensions
        CellArea destinationRange = new CellArea(
            30,                                 // start row on destination sheet
            0,                                  // start column
            30 + sourceRange.RowCount - 1,     // end row (same height as source)
            sourceRange.ColumnCount - 1        // end column (same width as source)
        );
```

لاحظ كيف نحسب الصف والعمود النهائيين بشكل ديناميكي. بهذه الطريقة، حتى إذا غيرت حجم النطاق المصدر لاحقًا، سيتadjust الوجهة تلقائيًا.

## الخطوة 4: تنفيذ النسخ مع الحفاظ على الجدول المحوري

الآن يحدث السحر. بتمرير كائن `CopyOptions` مع `CopyPivotTable = true`، يعرف Aspose.Cells أنه يجب الحفاظ على تعريف الجدول المحوري دون تغيير.

```csharp
        // Step 5: Copy the range, preserving the pivot table
        destSheet.Cells.CopyRange(
            sourceRange,
            destinationRange,
            new CopyOptions { CopyPivotTable = true }
        );
```

تحت الغطاء، يقوم Aspose.Cells بإعادة إنشاء ذاكرة التخزين المؤقت للجدول المحوري، وتحديث مرجع مصدر البيانات، وإعادة تطبيق أي تنسيق. هذا هو **Excel pivot duplication** الذي كنت تبحث عنه.

## الخطوة 5: حفظ والتحقق من النتيجة

أخيرًا، اكتب المصنف مرة أخرى إلى القرص. يمكنك ترك الملف الأصلي دون تعديل عن طريق الحفظ باسم جديد.

```csharp
        // Step 6: Save the workbook with the copied pivot table
        workbook.Save("YOUR_DIRECTORY/copy-pivot.xlsx");

        // Optional: open the file automatically (Windows only)
        System.Diagnostics.Process.Start(new System.Diagnostics.ProcessStartInfo
        {
            FileName = "YOUR_DIRECTORY/copy-pivot.xlsx",
            UseShellExecute = true
        });
    }
}
```

افتح الملف الناتج `copy-pivot.xlsx` وسترى الجدول المحوري مكررًا تمامًا في ورقة **CopyDestination**، مع أدوات التقطيع، والحقول المحسوبة، والتنسيق. لا يزال مصدر البيانات الأساسي يشير إلى الجدول الأصلي، لذا يعمل التحديث كما كان من قبل.

> **What if the source pivot spans a dynamic range?**  
> استخدم `Worksheet.PivotTables[0].CacheDefinition.SourceData` لاسترجاع الحدود الفعلية، ثم أنشئ `sourceRange` من تلك المعلومات. هذا يتعامل مع الحالات التي قد تتوسع فيها الصفوف أو الأعمدة بمرور الوقت.

## مكافأة: الحفاظ على تنسيق الجدول المحوري عبر النسخ

أحيانًا يفقد النسخ الافتراضي التنسيق الشرطي أو تنسيقات الأرقام المخصصة. للحماية من ذلك، قم بتمديد `CopyOptions`:

```csharp
        var options = new CopyOptions
        {
            CopyPivotTable = true,
            CopyFormatting = true,      // copies cell styles, colors, fonts
            CopyConditionalFormatting = true
        };
        destSheet.Cells.CopyRange(sourceRange, destinationRange, options);
```

تفعيل `CopyFormatting` يضمن تلبية متطلب **preserve pivot formatting**، مما يمنحك نسخة مطابقة تمامًا.

## الناتج المتوقع

عند تشغيل البرنامج، سيخرج الكونسول بصمت (إلا إذا أضفت سجلات). فتح `copy-pivot.xlsx` يجب أن يظهر:

- الورقة 1: البيانات الأصلية والجدول المحوري دون تغيير.  
- **CopyDestination**: نسخة مطابقة تمامًا من الجدول المحوري، تبدأ من الصف 31 (نظرًا لأن الصفوف في واجهة Excel تبدأ من 1).  
- جميع أدوات التقطيع والفلاتر تعمل؛ النقر على “Refresh” يحدث كلا الجدولين المحوريين في آن واحد.

## الخلاصة

لقد عرضنا للتو كيفية **copy pivot table to another sheet** باستخدام Aspose.Cells في C#. الخطوات — إعداد المشروع، تحميل المصنف، تعريف النطاقات، النسخ باستخدام `CopyPivotTable = true`، والحفظ — تشكل نمطًا موثوقًا يمكنك إعادة استخدامه في أي خط أنابيب أتمتة.

إذا كنت ترغب في التقدم أكثر، فكر في:

- **Excel pivot duplication** عبر عدة مصنفات (التكرار عبر الملفات).  
- استخدام خيار **Aspose.Cells copy range with pivot** لنقل الجداول المحورية بين مصنفات مختلفة.  
- أتمتة عمليات التحديث باستخدام `PivotTable.RefreshData()` بعد النسخ.

لا تتردد في تجربة نطاقات مصدر مختلفة، أو دمج هذه التقنية مع إنشاء المخططات للحصول على لوحات تقارير مؤتمتة بالكامل. هل لديك أسئلة؟ اترك تعليقًا، وتمنياتنا لك بالبرمجة السعيدة!

![Screenshot showing copied pivot table in new sheet](copy-pivot-screenshot.png "copy pivot table to another sheet example")

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مورد يتضمن أمثلة شفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [كيفية تغيير مصدر بيانات الجدول المحوري باستخدام Aspose.Cells لـ .NET | دليل تحليل البيانات](/cells/english/net/data-analysis/change-pivot-table-source-aspose-cells-net/)
- [إتقان تنسيق الجداول المحورية في .NET باستخدام Aspose.Cells](/cells/english/net/formatting/format-pivot-tables-dotnet-aspose-cells/)
- [الوصول إلى مصادر البيانات الخارجية للجداول المحورية في .NET باستخدام Aspose.Cells](/cells/english/net/data-analysis/access-pivot-table-data-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}