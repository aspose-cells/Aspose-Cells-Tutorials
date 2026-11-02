---
category: general
date: 2026-06-17
description: تعيين تنسيق التاريخ في Excel باستخدام C# وتعيين خلفية الخلية، وتطبيق
  لون النص، وتلوين عمود Excel أثناء الاستيراد. تعلم خطوة بخطوة.
draft: false
keywords:
- set date format
- set cell background
- apply foreground color
- color excel column
- excel import formatting
language: ar
og_description: تعيين تنسيق التاريخ في Excel باستخدام C# مع ضبط خلفية الخلية، وتطبيق
  لون النص، وتلوين عمود Excel أثناء الاستيراد. دليل كامل.
og_title: ضبط تنسيق التاريخ في إكسل باستخدام C# – دليل كامل
schemas:
- author: Aspose
  dateModified: '2026-06-17'
  description: Set date format in Excel using C# and also set cell background, apply
    foreground color, and color Excel column during import. Learn step‑by‑step.
  headline: Set date format in Excel with C# – Full Import Formatting Guide
  type: TechArticle
- description: Set date format in Excel using C# and also set cell background, apply
    foreground color, and color Excel column during import. Learn step‑by‑step.
  name: Set date format in Excel with C# – Full Import Formatting Guide
  steps:
  - name: 2.1 Set Date Format for the First Column
    text: The first column (`OrderDate`) should display as “MM/dd/yyyy”. Aspose uses
      the built‑in number format index 14 for the short date, but you can also supply
      a custom format string if you prefer.
  - name: 2.2 Set Cell Background for the Second Column
    text: Let’s give the `CustomerName` column a light blue background. This is where
      **set cell background** comes into play.
  - name: 2.3 Apply Foreground (Text) Color – Optional Extra
    text: 'If you also want the text itself to be a contrasting color, you can tweak
      the same style:'
  - name: 3.1 Save the Workbook
    text: '```csharp // Save to a file – change path as needed wb.Save("FormattedReport.xlsx",
      SaveFormat.Xlsx); Console.WriteLine("Excel file created with date format and
      colors."); ```'
  - name: What if I have more than two columns?
    text: Just expand the `columnStyles` array and assign a `Style` to each index
      you care about. Unassigned indexes will fall back to the default style, which
      is perfectly fine.
  - name: How do I format a column as currency?
    text: '```csharp columnStyles[3] = wb.CreateStyle(); columnStyles[3].Number =
      164; // Built‑in currency format (e.g., $#,##0.00) ```'
  - name: Can I change the header row style separately?
    text: 'Yes. After the import, you can grab the first row and apply a distinct
      style:'
  - name: What if the DataTable contains null dates?
    text: 'Aspose will leave those cells blank. If you prefer a placeholder like “N/A”,
      you can preprocess the table:'
  type: HowTo
tags:
- excel
- csharp
- aspnet
- data-import
title: تعيين تنسيق التاريخ في Excel باستخدام C# – دليل كامل لتنسيق الاستيراد
url: /ar/net/excel-custom-number-date-formatting/set-date-format-in-excel-with-c-full-import-formatting-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تعيين تنسيق التاريخ في Excel باستخدام C# – دليل تنسيق الاستيراد الكامل

هل احتجت يومًا إلى **set date format** في ورقة Excel تم إنشاؤها من كود C#، ولكنك أيضًا أردت أن يكون للعمود خلفية مخصصة أو لون نص؟ لست وحدك. في العديد من سيناريوهات التقارير تقوم بسحب `DataTable` من قاعدة بيانات، وتضعه في ورقة عمل، ثم تحاول جاهدًا جعل التواريخ تظهر بشكل صحيح والعمود يبرز بالألوان المناسبة.  

في هذا البرنامج التعليمي سنستعرض حلًا نظيفًا من البداية إلى النهاية يقوم بـ **sets date format**, **sets cell background**, **applies foreground color**, وحتى **colors an Excel column** أثناء استيراد البيانات. في النهاية ستحصل على نمط قابل لإعادة الاستخدام يتعامل مع **excel import formatting** دون التجربة والخطأ المعتادة.

> **ما ستحتاجه**  
> * .NET 6+ (or .NET Framework 4.7+)  
> * Aspose.Cells for .NET (free trial works for testing)  
> * A `DataTable` source – any ADO.NET query will do  
> * Visual Studio or your favorite IDE  

هيا نبدأ.

---

## نظرة عامة على الحل

سنقسم المشكلة إلى ثلاث قطع منطقية:

1. **Retrieve the source data** – `DataTable` يحتوي على الصفوف التي تريد تصديرها.  
2. **Create column‑specific styles** – نمط واحد لعمود التاريخ، وآخر لعمود النص، بالإضافة إلى أي تنسيقات إضافية تريدها.  
3. **Import the table with styles** – استخدم `Worksheet.Cells.ImportDataTable` بحيث يرث كل عمود النمط الذي أعددته.

لماذا هذا النهج؟ لأن Aspose.Cells يتيح لك إرفاق مصفوفة `Style` مباشرةً إلى استدعاء `ImportDataTable`، مما يعني أنك لا تحتاج إلى تمريرة ثانية لإعادة تطبيق التنسيق. إنه أسرع، أقل عرضة للأخطاء، ويحافظ على نظافة الكود.

## الخطوة 1: استرجاع البيانات للتصدير

أولًا وقبل كل شيء – تحتاج إلى `DataTable`. في مشروع حقيقي ربما تستدعي إجراء مخزن أو تستخدم Entity Framework لملئه، ولكن للتوضيح سنقوم بإنشاء جدول بسيط يحتوي على عمود تاريخ وعمود نص.

```csharp
using System;
using System.Data;
using Aspose.Cells;

DataTable GetData()
{
    var table = new DataTable();
    table.Columns.Add("OrderDate", typeof(DateTime));
    table.Columns.Add("CustomerName", typeof(string));

    // Sample rows – replace with your DB call
    table.Rows.Add(DateTime.Today.AddDays(-2), "Acme Corp");
    table.Rows.Add(DateTime.Today.AddDays(-1), "Globex Inc");
    table.Rows.Add(DateTime.Today, "Soylent Co");

    return table;
}
```

> **نصيحة احترافية:** إذا كان المصدر يستخدم تواريخ قابلة للإلغاء (nullable)، تأكد من أن نوع العمود هو `typeof(DateTime?)` – سيظل Aspose يحترم التنسيق الذي تعينه لاحقًا.

## الخطوة 2: إعداد مصفوفة من الأنماط – واحد لكل عمود

الآن نقوم بإنشاء `Style[]` بطول يطابق عدد الأعمدة في `DataTable`. كل عنصر سيحمل التنسيق للعمود المقابل.

```csharp
// Create a new workbook and get the first worksheet
Workbook wb = new Workbook();
Worksheet ws = wb.Worksheets[0];

// Pull the data
DataTable dataTable = GetData();

// Allocate the style array
Style[] columnStyles = new Style[dataTable.Columns.Count];
```

### 2.1 تعيين تنسيق التاريخ للعمود الأول

العمود الأول (`OrderDate`) يجب أن يُعرض كـ “MM/dd/yyyy”. يستخدم Aspose الفهرس المدمج لتنسيق الأرقام رقم 14 للتاريخ القصير، ولكن يمكنك أيضًا توفير سلسلة تنسيق مخصصة إذا رغبت.

```csharp
// Style for the date column (index 0)
columnStyles[0] = wb.CreateStyle();
columnStyles[0].Number = 14;               // Built‑in short date format
// Or a custom pattern:
// columnStyles[0].Custom = "mm/dd/yyyy";
```

**Why this matters:** Excel يخزن التواريخ كأرقام تسلسلية. من خلال تعيين تنسيق رقم، تخبر Excel بعرض تلك الأرقام كتواريخ قابلة للقراءة بدلاً من أرقام خام.

### 2.2 تعيين خلفية الخلية للعمود الثاني

لنمنح عمود `CustomerName` خلفية زرقاء فاتحة. هنا يأتي دور **set cell background**.

```csharp
// Style for the text column (index 1)
columnStyles[1] = wb.CreateStyle();
columnStyles[1].ForegroundColor = System.Drawing.Color.LightBlue;
columnStyles[1].Pattern = BackgroundType.Solid; // Needed to show the color
```

> **ملاحظة:** بدون تعيين `Pattern` إلى `Solid`، لن يظهر لون المقدمة لأن النمط الافتراضي هو “None”.

### 2.3 تطبيق لون المقدمة (النص) – إضافي اختياري

إذا كنت تريد أيضًا أن يكون النص نفسه بلون متباين، يمكنك تعديل النمط نفسه:

```csharp
columnStyles[1].Font.Color = System.Drawing.Color.DarkBlue; // apply foreground color
```

هذا يلبي متطلبات **apply foreground color** مع الحفاظ على خلفية العمود كما هي.

## الخطوة 3: استيراد DataTable مع الأنماط المحددة

مع إعداد الأنماط، الخطوة الأخيرة هي سطر واحد يستورد البيانات ويطبق الأنماط عمودًا بعمود.

```csharp
// Import the DataTable starting at cell A1 (row 0, column 0)
// includeColumnNames = true to add a header row
ws.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);
```

**How it works:** Aspose يقرأ مصفوفة `columnStyles` ويربط كل `Style` بمؤشر العمود المقابل. صف العنوان يرث النمط الافتراضي ما لم تزود نمطًا منفصلًا للصف 0.

### 3.1 حفظ المصنف

```csharp
// Save to a file – change path as needed
wb.Save("FormattedReport.xlsx", SaveFormat.Xlsx);
Console.WriteLine("Excel file created with date format and colors.");
```

شغّل البرنامج، افتح *FormattedReport.xlsx*، وسترى:

- عمود **OrderDate** يُعرض كتاريخ (مثال: `06/15/2026`).  
- عمود **CustomerName** بخلفية زرقاء فاتحة ونص أزرق داكن.  

هذا هو كامل سير عمل **excel import formatting** في أقل من 30 سطرًا من C#.

## ملخص خطوة بخطوة (مع السبب)

| الخطوة | ما تقوم به | لماذا يهم |
|------|-------------|----------------|
| **Retrieve data** | استدعِ `GetData()` لملء `DataTable`. | يوفر مصدرًا منظمًا يمكن لـ Aspose استهلاكه مباشرةً. |
| **Create style array** | خصص `Style[]` بحيث يطابق عدد الأعمدة. | يتيح تنسيق كل عمود على حدة في استدعاء استيراد واحد. |
| **Set date format** | `columnStyles[0].Number = 14;` | يضمن عرض التواريخ بشكل صحيح في Excel. |
| **Set background color** | `ForegroundColor = LightBlue; Pattern = Solid;` | يبرز العمود، مستوفيًا **set cell background**. |
| **Apply foreground color** | `Font.Color = DarkBlue;` | يحسن قابلية القراءة ويستوفي **apply foreground color**. |
| **Import with styles** | `ImportDataTable(..., columnStyles);` | استيراد بتمرير واحد يحترم كل التنسيقات. |
| **Save workbook** | `wb.Save(...);` | يحفظ النتيجة للمستخدمين اللاحقين. |

## معالجة الحالات الخاصة والأسئلة الشائعة

### ماذا لو كان لدي أكثر من عمودين؟

فقط قم بتوسيع مصفوفة `columnStyles` وعيّن `Style` لكل فهرس يهمك. الفهارس غير المعينة ستعود إلى النمط الافتراضي، وهذا مقبول تمامًا.

```csharp
columnStyles[2] = wb.CreateStyle();
columnStyles[2].Number = 0; // General format for numeric columns
```

### كيف أقوم بتنسيق عمود كعملة؟

```csharp
columnStyles[3] = wb.CreateStyle();
columnStyles[3].Number = 164; // Built‑in currency format (e.g., $#,##0.00)
```

### هل يمكنني تغيير نمط صف العنوان بشكل منفصل؟

نعم. بعد الاستيراد، يمكنك الحصول على الصف الأول وتطبيق نمط مميز:

```csharp
Style headerStyle = wb.CreateStyle();
headerStyle.Font.IsBold = true;
headerStyle.ForegroundColor = System.Drawing.Color.Gold;
headerStyle.Pattern = BackgroundType.Solid;

ws.Cells.Rows[0].ApplyStyle(headerStyle, new StyleFlag { All = true });
```

### ماذا لو كان DataTable يحتوي على تواريخ فارغة (null)؟

سيترك Aspose تلك الخلايا فارغة. إذا كنت تفضل عنصرًا نائبيًا مثل “N/A”، يمكنك معالجة الجدول مسبقًا:

```csharp
foreach (DataRow row in dataTable.Rows)
{
    if (row.IsNull("OrderDate"))
        row["OrderDate"] = DateTime.MinValue; // or any sentinel
}
```

ثم عدل النمط لعرض تنسيق مخصص يُظهر “N/A” للقيمة الحارسة.

## مثال كامل يعمل

فيما يلي البرنامج الكامل الجاهز للنسخ واللصق. شغّله كتطبيق كونسول، وستحصل على ملف Excel مُنسق بشكل جميل.



## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مصدر يتضمن أمثلة كود كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [تعيين لون الخط في خلايا Excel باستخدام Aspose.Cells لـ .NET](/cells/english/net/formatting/setting-font-color/)
- [تعيين لون الخط في Excel .NET باستخدام Aspose.Cells](/cells/english/net/formatting/set-font-color-net-excel-aspose-cells/)
- [تعيين عرض أعمدة Excel بالبكسل باستخدام Aspose.Cells لـ .NET | دليل خطوة بخطوة](/cells/english/net/formatting/set-excel-column-width-pixels-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}