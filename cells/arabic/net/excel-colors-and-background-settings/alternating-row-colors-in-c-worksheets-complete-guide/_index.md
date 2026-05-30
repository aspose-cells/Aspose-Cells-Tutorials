---
category: general
date: 2026-05-30
description: تعلم كيفية إضافة ألوان متناوبة للصفوف في أوراق العمل بلغة C#، وتعيين
  خلفية الخلية بنمط تعبئة صلبة، وتخصيص نمط خلية ورقة العمل بسهولة.
draft: false
keywords:
- alternating row colors
- set cell background
- solid fill pattern
- add background color
- worksheet cell style
language: ar
og_description: تلوين الصفوف المتناوبة في أوراق عمل C# بسهولة. تعلم كيفية ضبط خلفية
  الخلية، واستخدام نمط تعبئة صلبة، وإتقان نمط خلية ورقة العمل.
og_title: ألوان الصفوف المتناوبة في أوراق عمل C# – دليل كامل
schemas:
- author: Aspose
  dateModified: '2026-05-30'
  description: Learn how to add alternating row colors in C# worksheets, set cell
    background with a solid fill pattern, and customize worksheet cell style effortlessly.
  headline: Alternating Row Colors in C# Worksheets – Complete Guide
  type: TechArticle
- description: Learn how to add alternating row colors in C# worksheets, set cell
    background with a solid fill pattern, and customize worksheet cell style effortlessly.
  name: Alternating Row Colors in C# Worksheets – Complete Guide
  steps:
  - name: Why Use a **Solid Fill Pattern**?
    text: The `Pattern` property tells the engine how to render the color. A `Solid`
      fill guarantees that the entire cell background is painted, eliminating any
      faint gridlines that might otherwise show through. This is the most common way
      to **set cell background** when you want a clean look.
  - name: Change the Colors
    text: 'If your brand uses different hues, just replace `Color.LightYellow` and
      `Color.LightCyan` with any `System.Drawing.Color` you prefer. For example:'
  - name: Use a Different **Background Type**
    text: While `BackgroundType.Solid` is the most common, you can experiment with
      `BackgroundType.Gray125`, `BackgroundType.Horizontal`, or any pattern that the
      library supports. This changes the visual texture while still **adding background
      color**.
  - name: Apply a **Worksheet Cell Style** to Specific Columns
    text: 'Sometimes you only want the alternating effect on data columns, leaving
      the first column (e.g., IDs) untouched. Create a separate style for that column
      and assign it after the import:'
  type: HowTo
tags:
- C#
- Excel
- Aspose.Cells
- DataTable
- Styling
title: ألوان الصفوف المتناوبة في أوراق عمل C# – دليل شامل
url: /ar/net/excel-colors-and-background-settings/alternating-row-colors-in-c-worksheets-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ألوان الصفوف المتناوبة في أوراق عمل C# – دليل كامل

هل تساءلت يومًا كيف تجعل تصدير Excel الخاص بك يبدو مصقولًا باستخدام **alternating row colors**؟ لست وحدك—المطورون يطلبون باستمرار كيفية *add background color* للصفوف دون كتابة ملايين الأسطر من الشيفرة.  

في هذا البرنامج التعليمي سنستعرض طريقة بسيطة لـ **set cell background** لكل صف، وتطبيق **solid fill pattern**، والتحكم في **worksheet cell style** بحيث تكون النتيجة قابلة للقراءة وجذابة بصريًا.

## ما ستتعلمه

- استرجاع البيانات إلى `DataTable` (أو أي مصدر جدولي).  
- إنشاء مصفوفة من كائنات `Style` التي تتناوب بين لونين.  
- استيراد `DataTable` إلى ورقة عمل مع تطبيق تلك الأنماط.  
- التحقق من النتيجة وتعديل الألوان أو الأنماط إذا لزم الأمر.  

لا تحتاج إلى أدوات خارجية بخلاف بيئة .NET ومكتبة جداول البيانات (سنستخدم **Aspose.Cells** في الأمثلة). في النهاية ستحصل على طريقة قابلة لإعادة الاستخدام يمكنك إدراجها في أي خط أنابيب تقارير.

---

## الخطوة 1: استرجاع بيانات المصدر كـ `DataTable`

أولًا وقبل كل شيء—بدون بيانات لا شيء لتنسيقه. أدناه مساعد صغير يبني `DataTable` مع صفوف نموذجية. في مشروع حقيقي ستستبدله بنداء قاعدة بيانات أو محلل CSV.

```csharp
using System;
using System.Data;

static DataTable GetData()
{
    // Create a simple table with three columns
    DataTable table = new DataTable("Report");
    table.Columns.Add("ID", typeof(int));
    table.Columns.Add("Name", typeof(string));
    table.Columns.Add("Score", typeof(double));

    // Populate with dummy rows
    for (int i = 1; i <= 10; i++)
    {
        table.Rows.Add(i, $"Item {i}", Math.Round(new Random().NextDouble() * 100, 2));
    }

    return table;
}
```

> **لماذا هذا مهم:** وجود البيانات في `DataTable` يسمح لمحرك ورقة العمل *import* إياها في نداء واحد، مع الحفاظ على أسماء الأعمدة وأنواع البيانات تلقائيًا.

## الخطوة 2: إنشاء أنماط **Alternating Row Colors**

الآن سنولد مصفوفة من كائنات `Style`—واحدة لكل صف—بحيث تحصل الصفوف الزوجية على ظل أصفر فاتح بينما تتلقى الصفوف الفردية سينا خفيف. هذا هو جوهر تقنية **alternating row colors**.

```csharp
using Aspose.Cells;
using System.Drawing;

// Assume workbook and worksheet are already instantiated
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.Worksheets[0];

// Retrieve data
DataTable dataTable = GetData();

// Prepare an array of styles – one for each row in the table
Style[] rowStyles = new Style[dataTable.Rows.Count];

for (int i = 0; i < rowStyles.Length; i++)
{
    // Create a fresh style for the current row
    rowStyles[i] = workbook.CreateStyle();

    // **Add background color**: LightYellow for even rows, LightCyan for odd rows
    rowStyles[i].ForegroundColor = (i % 2 == 0)
        ? Color.LightYellow
        : Color.LightCyan;

    // **Set cell background** using a **solid fill pattern**
    rowStyles[i].Pattern = BackgroundType.Solid;

    // Optional: you could also set font color, borders, etc., here
}
```

### لماذا نستخدم **Solid Fill Pattern**؟

خاصية `Pattern` تخبر المحرك كيف يرسم اللون. تعبئة `Solid` تضمن أن خلفية الخلية بالكامل تُلون، مما يلغي أي خطوط شبكة خفيفة قد تظهر. هذه هي الطريقة الأكثر شيوعًا لـ **set cell background** عندما تريد مظهرًا نظيفًا.

## الخطوة 3: استيراد `DataTable` مع الأنماط المُعدة

مع جاهزية مصفوفة الأنماط، يصبح نداء الاستيراد سطرًا واحدًا. سيقوم Aspose.Cells بتطبيق النمط المقابل لكل صف تلقائيًا.

```csharp
// Import the DataTable into the worksheet, applying the prepared styles
worksheet.Cells.ImportDataTable(
    dataTable,                     // source
    true,                          // include column names
    0,                             // start row (0‑based)
    0,                             // start column (0‑based)
    rowStyles);                    // array of styles
```

> **ماذا يحدث خلف الكواليس؟**  
> تقوم المكتبة بالتكرار على كل صف، تنسخ القيم إلى الخلايا، ثم تطبق `Style` المطابق من `rowStyles`. لأننا عرّفنا بالفعل **solid fill pattern**، كل خلية في الصف ترث نفس لون الخلفية، مما يمنحك **alternating row colors** مثالية.

## الخطوة 4: حفظ المصنف والتحقق من النتيجة

حفظ سريع يتيح لك فتح الملف في Excel (أو أي عارض متوافق) ورؤية التأثير.

```csharp
// Save to disk – you can change the format to .xlsx, .xls, .csv, etc.
workbook.Save("AlternatingRowsReport.xlsx", SaveFormat.Xlsx);
Console.WriteLine("Workbook saved. Open 'AlternatingRowsReport.xlsx' to see the result.");
```

عند فتح الملف، ستكون الصفوف 1، 3، 5… أصفر فاتح، بينما الصفوف 2، 4، 6… سينا فاتح. تظل رؤوس الأعمدة بيضاء، مما يجعل البيانات بارزة.

![ورقة عمل تُظهر ألوان الصفوف المتناوبة](/images/alternating-row-colors.png "لقطة شاشة لورقة عمل بألوان الصفوف المتناوبة")

*نص بديل للصورة:* **alternating row colors** لقطة شاشة لورقة عمل حيث يتناوب خلفية كل صف بين الأصفر الفاتح والسينا الفاتح.

## الخطوة 5: تخصيص إضافي (اختياري)

### تغيير الألوان

إذا كانت علامتك التجارية تستخدم ألوانًا مختلفة، استبدل `Color.LightYellow` و `Color.LightCyan` بأي `System.Drawing.Color` تفضله. على سبيل المثال:

```csharp
rowStyles[i].ForegroundColor = (i % 2 == 0) ? Color.FromArgb(255, 235, 205) // Peach
                                            : Color.FromArgb(205, 235, 255); // Soft blue
```

### استخدم **Background Type** مختلفًا

بينما `BackgroundType.Solid` هو الأكثر شيوعًا، يمكنك تجربة `BackgroundType.Gray125`، `BackgroundType.Horizontal`، أو أي نمط تدعمه المكتبة. هذا يغيّر الملمس البصري مع الاستمرار في **adding background color**.

### تطبيق **Worksheet Cell Style** على أعمدة محددة

أحيانًا قد ترغب فقط في تأثير التناوب على أعمدة البيانات، مع ترك العمود الأول (مثل المعرفات) دون تغيير. أنشئ نمطًا منفصلًا لهذا العمود وعيّنه بعد الاستيراد:

```csharp
Style idStyle = workbook.CreateStyle();
idStyle.ForegroundColor = Color.White;
idStyle.Pattern = BackgroundType.Solid;

// Apply to the first column (A)
for (int row = 0; row < dataTable.Rows.Count + 1; row++) // +1 for header
{
    worksheet.Cells[row, 0].SetStyle(idStyle);
}
```

---

## الخاتمة

أصبح لديك الآن حل كامل وقابل لإعادة الاستخدام لـ **alternating row colors** في أوراق عمل C#. من خلال بناء مصفوفة من كائنات `Style`، **setting cell background** باستخدام **solid fill pattern**، واستيراد `DataTable` في نداء واحد، يمكنك إنتاج تقارير ذات مظهر احترافي بأقل قدر من الشيفرة.  

من هنا قد ترغب في:

- **Add background color** إلى صفوف العناوين لمزيد من التميز.  
- دمج التقنية مع التنسيق الشرطي للحصول على مؤشرات بصرية ديناميكية.  
- استكشاف خصائص أخرى لـ **worksheet cell style** مثل الخطوط، الحدود، أو تنسيقات الأرقام.

جرّبه في روتين التصدير التالي—سيشكرك المستخدمون على جداول البيانات الأنظف وأكثر قابلية للقراءة. برمجة سعيدة!

## ما الذي يجب أن تتعلمه بعد ذلك؟

- [تحديد ارتفاع الصف في ورقة العمل باستخدام Aspose.Cells لـ .NET](/cells/english/net/size-and-spacing-customization/setting-height-of-all-rows-in-worksheet/)
- [تحويل أسماء خلايا Excel إلى مؤشرات الصف والعمود باستخدام Aspose.Cells لـ .NET](/cells/english/net/cell-operations/convert-excel-cell-names-to-indices-aspose-cells-dotnet/)
- [تعيين ألوان علامات تبويب ورقة العمل في Excel باستخدام Aspose.Cells .NET - دليل شامل](/cells/english/net/worksheet-management/set-worksheet-tab-colors-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}