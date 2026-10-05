---
category: general
date: 2026-02-26
description: تطبيق تنسيق الأرقام في Excel بسرعة وتعلم كيفية تنسيق العمود كعملة، وضبط
  تنسيق رقم العمود، وتغيير لون خط العمود في بضع أسطر فقط من C#.
draft: false
keywords:
- apply number format excel
- format column as currency
- set column number format
- format currency column
- set column font color
language: ar
og_description: تطبيق تنسيق الأرقام في إكسل باستخدام C# بخطوات سهلة. تعلم تنسيق العمود
  كعملة، وضبط تنسيق الأرقام للعمود، وتعيين لون خط العمود لجداول بيانات احترافية.
og_title: تطبيق تنسيق الأرقام في إكسل – الدليل الكامل لتنسيق الأعمدة
tags:
- C#
- Excel
- Aspose.Cells
- DataTable
- Styling
title: تطبيق تنسيق الأرقام في إكسل – دليل خطوة بخطوة لتنسيق الأعمدة
url: /ar/net/number-and-display-formats-in-excel/apply-number-format-excel-step-by-step-guide-to-formatting-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تطبيق تنسيق الأرقام في Excel – كيفية تنسيق أعمدة Excel في C#

هل تساءلت يومًا كيف **apply number format excel** بينما تقوم بالفعل بالتكرار عبر `DataTable`؟ أنت لست الوحيد. يواجه معظم المطورين صعوبة عندما يحتاجون إلى رأس بخط أزرق *و* عمود بتنسيق عملة في نفس عملية الاستيراد. الخبر السار؟ ببضع أسطر من C# والكائنات النمطية المناسبة، يمكنك القيام بذلك دون الحاجة إلى معالجة لاحقة للورقة.

في هذا الدرس سنستعرض مثالًا كاملاً وقابلًا للتنفيذ يوضح لك كيفية **format column as currency**، **set column number format** لأي عمود آخر، وحتى **set column font color** للرؤوس. في النهاية ستحصل على نمط قابل لإعادة الاستخدام يمكنك إدراجه في أي مشروع Aspose.Cells (أو مشابه).

## ما ستتعلمه

- كيفية استرجاع `DataTable` وربط كل عمود بـ `Style` محدد.
- الخطوات الدقيقة لـ **apply number format excel** باستخدام `Worksheet.Cells.ImportDataTable`.
- لماذا إنشاء الأنماط مسبقًا أكثر كفاءة من تنسيق الخلايا واحدةً تلو الأخرى.
- معالجة الحالات الحدية عندما يحتوي جدول المصدر على أعمدة أكثر مما قمت بتنسيقه.
- عينة شفرة كاملة جاهزة للنسخ واللصق يمكنك تشغيلها اليوم.

> **المتطلبات المسبقة:** يفترض هذا الدليل أنك تمتلك Aspose.Cells لـ .NET (أو أي مكتبة تعرض واجهات `Workbook`، `Worksheet`، `Style`) مُشار إليها في مشروعك. إذا كنت تستخدم مكتبة مختلفة، فإن المفاهيم تُترجم مباشرةً — فقط استبدل أسماء الأنواع.

## الخطوة 1: استرجاع بيانات المصدر كـ DataTable

قبل أن يتم أي تنسيق، تحتاج إلى البيانات الخام. في معظم السيناريوهات الواقعية، تُخزن البيانات في قاعدة بيانات، CSV، أو API. لتوضيح الفكرة، سنقوم بإنشاء `DataTable` بسيط يحتوي على عمودين: *Product* (string) و *Price* (decimal).

```csharp
using System;
using System.Data;
using Aspose.Cells;
using System.Drawing;

public static DataTable GetData()
{
    var dt = new DataTable();
    dt.Columns.Add("Product", typeof(string));
    dt.Columns.Add("Price", typeof(decimal));

    dt.Rows.Add("Apple", 1.25m);
    dt.Rows.Add("Banana", 0.75m);
    dt.Rows.Add("Cherry", 2.10m);

    return dt;
}
```

> **لماذا هذا مهم:** سحب البيانات إلى `DataTable` يمنحك تمثيلًا جدوليًا في الذاكرة يمكن لـ `ImportDataTable` استهلاكه مباشرةً، مما يلغي الحاجة إلى إدخال الخلايا يدويًا واحدةً تلو الأخرى.

## الخطوة 2: إنشاء مصفوفة من الأنماط – واحدة لكل عمود

الإصدار الزائد من `ImportDataTable` الذي سنستخدمه يقبل مصفوفة من كائنات `Style`. كل عنصر يتطابق مع فهرس عمود. إذا تركت العنصر `null`، سيورث العمود النمط الافتراضي للدفتر.

```csharp
// Initialize the workbook (Aspose.Cells)
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.Worksheets[0];

// Prepare the style array based on the number of columns
DataTable dataTable = GetData();
Style[] columnStyles = new Style[dataTable.Columns.Count];
```

> **نصيحة احترافية:** إعلان المصفوفة *بعد* الحصول على `DataTable` يضمن أن الحجم يتطابق تمامًا، مما يمنع حدوث `IndexOutOfRangeException` لاحقًا.

## الخطوة 3: تعيين لون خط العمود (أزرق) للعمود الأول

طلب شائع هو تمييز رؤوس أو أعمدة رئيسية بلون خط مميز. هنا نجعل نص العمود الأول أزرق.

```csharp
// Style for the first column – blue font
columnStyles[0] = workbook.CreateStyle();
columnStyles[0].Font.Color = Color.Blue;
```

> **لماذا نستخدم كائن النمط؟** الأنماط قابلة لإعادة الاستخدام وتُطبق دفعة واحدة، مما يجعلها أسرع بكثير من التكرار على كل خلية بعد الاستيراد. يقوم الدفتر بتخزين النمط مرة واحدة، ثم يعيد استخدامه لكل خلية في ذلك العمود.

## الخطوة 4: تنسيق العمود الثاني كعملة

تنسيقات الأرقام المدمجة في Excel تُحدد بواسطة فهرس. `14` يطابق تنسيق العملة الافتراضي (مثال: `$1,234.00`). إذا كنت تحتاج إلى تنسيق مخصص، يمكنك تعيين سلسلة تنسيق بدلاً من ذلك.

```csharp
// Style for the second column – built‑in currency format (ID 14)
columnStyles[1] = workbook.CreateStyle();
columnStyles[1].Number = 14; // 14 = built‑in currency format
```

> **حالة حدية:** إذا كان دفتر العمل يستخدم لغة حيث رمز العملة ليس `$`، فإن نفس الفهرس سيتكيف تلقائيًا (مثال: `€` للغات الألمانية).

## الخطوة 5: استيراد DataTable مع الأنماط المعرفة

الآن نجمع كل شيء معًا. طريقة `ImportDataTable` ستلصق البيانات بدءًا من الخلية `A1` (الصف 0، العمود 0) وتطبق الأنماط التي أعددناها.

```csharp
// Import the DataTable into the worksheet, applying the column styles
worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);
```

- المعامل الثاني `true` يخبر Aspose.Cells بأن يتعامل مع الصف الأول من `DataTable` كرؤوس أعمدة.
- الإحداثيات `0, 0` تحدد الزاوية العليا اليسرى حيث يبدأ الاستيراد.
- `columnStyles` يربط كل عمود بالنمط الخاص به.

## الخطوة 6: حفظ دفتر العمل (اختياري، لكنه مفيد للتحقق)

إذا أردت رؤية النتيجة في Excel، فقط احفظ دفتر العمل إلى القرص. هذه الخطوة ليست ضرورية لمنطق التنسيق، لكنها مفيدة للتصحيح.

```csharp
// Save the workbook to a file
workbook.Save("StyledReport.xlsx", SaveFormat.Xlsx);
Console.WriteLine("Workbook saved as StyledReport.xlsx");
```

### النتيجة المتوقعة

| **Product** (خط أزرق) | **Price** (عملة) |
|--------------------------|----------------------|
| Apple                    | $1.25                |
| Banana                   | $0.75                |
| Cherry                   | $2.10                |

- عمود *Product* يظهر باللون الأزرق، مما يجعله بارزًا.
- عمود *Price* يعرض القيم برمز العملة الافتراضي وبدقتين عشريتين.

## الأسئلة المتكررة والاختلافات

### كيف يمكنني **set column number format** لأكثر من عمودين؟

فقط قم بتمديد مصفوفة `columnStyles`. على سبيل المثال، لعرض نسبة مئوية في العمود الثالث:

```csharp
columnStyles[2] = workbook.CreateStyle();
columnStyles[2].Number = 10; // 10 = built‑in percentage format
```

### ماذا لو احتجت إلى تنسيق عملة *مخصص*، مثل “USD 1,234.00”؟

استبدل خاصية `Number` بسلسلة تنسيق:

```csharp
columnStyles[1].Custom = "\"USD\" #,##0.00";
```

### هل يمكنني تطبيق **set column font color** على عمود رقمي دون التأثير على تنسيق رقمه؟

بالتأكيد. الأنماط قابلة للتركيب. يمكنك تعيين كل من `Font.Color` و `Number` على نفس كائن `Style`:

```csharp
columnStyles[3] = workbook.CreateStyle();
columnStyles[3].Font.Color = Color.Green;
columnStyles[3].Number = 2; // 2 = built‑in date format (just an example)
```

### ماذا يحدث إذا كان `DataTable` يحتوي على أعمدة أكثر من الأنماط؟

أي عمود بدون نمط صريح (`null`) سيورث النمط الافتراضي للدفتر. لتجنب `null` غير مقصودة، يمكنك تهيئة المصفوفة بالكامل بنمط أساسي أولاً:

```csharp
Style defaultStyle = workbook.CreateStyle();
defaultStyle.Font.Size = 11;
for (int i = 0; i < columnStyles.Length; i++)
    columnStyles[i] = defaultStyle;
```

ثم قم بتجاوز فقط الأعمدة التي تهتم بها.

### هل يعمل هذا النهج مع مجموعات بيانات كبيرة (أكثر من 10k صف)؟

نعم. لأن التنسيق يُطبق *مرة واحدة لكل عمود* قبل الاستيراد، يبقى العملية O(N) بالنسبة للصفوف، واستخدام الذاكرة منخفض. تجنب التكرار على كل خلية بعد الاستيراد—هذا هو ما يسبب تدهور الأداء.

## مثال كامل يعمل (جاهز للنسخ واللصق)

```csharp
using System;
using System.Data;
using System.Drawing;
using Aspose.Cells;

class ExcelStyler
{
    static void Main()
    {
        // 1️⃣ Retrieve data
        DataTable dataTable = GetData();

        // 2️⃣ Create workbook and worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // 3️⃣ Prepare style array (one per column)
        Style[] columnStyles = new Style[dataTable.Columns.Count];

        // 4️⃣ Style first column – blue font
        columnStyles[0] = workbook.CreateStyle();
        columnStyles[0].Font.Color = Color.Blue;

        // 5️⃣ Style second column – built‑in currency format (ID 14)
        columnStyles[1] = workbook.CreateStyle();
        columnStyles[1].Number = 14;

        // 6️⃣ (Optional) Add more styles here – e.g., percentage, custom formats

        // 7️⃣ Import the DataTable with styles
        worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);

        // 8️⃣ Save to file for verification
        workbook.Save("StyledReport.xlsx", SaveFormat.Xlsx);
        Console.WriteLine("Excel file created: StyledReport.xlsx");
    }

    // Helper method to mock data
    public static DataTable GetData()
    {
        var dt = new DataTable();
        dt.Columns.Add("Product", typeof(string));
        dt.Columns.Add("Price", typeof(decimal));

        dt.Rows.Add("Apple", 1.25m);
        dt.Rows.Add("Banana", 0.75m);
        dt.Rows.Add("Cherry", 2.10m);
        return dt;
    }
}
```

شغّل البرنامج، افتح `StyledReport.xlsx`، وسترى نتيجة **apply number format excel** فورًا.

## الخلاصة

لقد عرضنا للتو طريقة نظيفة وفعّالة لـ **apply number format excel** على `DataTable` مستورد. من خلال إعداد مصفوفة `Style[]` مسبقًا، يمكنك **format column as currency**، **set column number format**، و **set column font color** في استدعاء واحد—دون الحاجة إلى معالجة لاحقة.  

لا تتردد في توسيع النمط: إضافة تنسيق شرطي، دمج خلايا للعناوين، أو حتى إدراج صيغ. نفس المبادئ تنطبق، مما يحافظ على نظافة الكود ومظهر جداول البيانات احترافيًا.

### ما التالي؟

- استكشف **conditional formatting** لتسليط الضوء على القيم التي تتجاوز عتبة معينة.
- اجمع هذه التقنية مع **pivot table generation** لتقارير ديناميكية.
- جرّب **set column number format** للتواريخ، النسب المئوية، أو الصيغة العلمية المخصصة.

هل جربت تعديلًا مختلفًا؟ شاركه في التعليقات—لنستمر في

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}