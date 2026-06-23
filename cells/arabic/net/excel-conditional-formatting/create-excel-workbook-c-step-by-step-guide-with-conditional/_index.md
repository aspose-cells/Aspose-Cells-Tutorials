---
category: general
date: 2026-03-27
description: إنشاء مصنف Excel باستخدام C# و Aspose.Cells، تطبيق التنسيق الشرطي، استيراد
  DataTable إلى Excel وحفظ المصنف بصيغة xlsx—كل ذلك في دليل واحد.
draft: false
keywords:
- create excel workbook c#
- apply conditional formatting
- import datatable to excel
- save workbook as xlsx
- create excel file programmatically
language: ar
og_description: إنشاء مصنف Excel باستخدام C# و Aspose.Cells، تطبيق التنسيق الشرطي،
  استيراد جدول البيانات إلى Excel وحفظ المصنف بصيغة xlsx في دقائق.
og_title: إنشاء مصنف إكسل C# – دليل كامل مع التنسيق الشرطي
tags:
- Aspose.Cells
- C#
- Excel automation
title: إنشاء مصنف إكسل C# – دليل خطوة بخطوة مع التنسيق الشرطي
url: /ar/net/excel-conditional-formatting/create-excel-workbook-c-step-by-step-guide-with-conditional/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء دفتر عمل Excel باستخدام C# – دليل برمجة كامل

هل احتجت يوماً إلى **إنشاء دفتر عمل Excel C#** بشكل سريع ولم تعرف من أين تبدأ؟ لست وحدك—العديد من المطورين يواجهون هذه المشكلة عندما يبدأون بأتمتة التقارير. في هذا الدليل سنوضح لك بالضبط كيفية إنشاء دفتر عمل Excel C# باستخدام Aspose.Cells، وتطبيق التنسيق الشرطي، واستيراد DataTable إلى Excel وأخيراً حفظ الدفتر بصيغة xlsx.  

ما ستحصل عليه من هذا الشرح هو تطبيق Console جاهز للتنفيذ ينتج ملف Excel ملون، بالإضافة إلى شرح واضح لكل سطر لتتمكن من تعديلها وفق مشاريعك. لا حاجة إلى مستندات خارجية؛ فقط انسخ، الصق، وشغّل.  

### المتطلبات المسبقة

- .NET 6+ (أو .NET Framework 4.7.2+) مثبتة  
- Visual Studio 2022 أو أي محرر C# تفضله  
- Aspose.Cells for .NET (يمكنك الحصول على حزمة NuGet التجريبية المجانية)  

إذا كان لديك هذه المتطلبات، لنبدأ.

## إنشاء دفتر عمل Excel C# – تهيئة الـ Workbook

أول شيء عليك فعله هو **إنشاء دفتر عمل Excel C#** عن طريق إنشاء كائن من الفئة `Workbook`. هذا الكائن يمثل ملف Excel بالكامل في الذاكرة.

```csharp
using Aspose.Cells;
using Aspose.Cells.Tables;
using System.Data;
using System.Drawing;

class SmartMarkerConditionalDemo
{
    static void Main()
    {
        // Step 1: Create a new workbook and grab the first worksheet
        Workbook workbook = new Workbook();                // <-- creates the workbook
        Worksheet worksheet = workbook.Worksheets[0];      // first sheet (Sheet1)
```

> **لماذا هذا مهم:** فئة `Workbook` تُجرد تنسيق الملف، لذا لا تحتاج إلى التعامل مع XML منخفض المستوى أو COM interop. كما أنها تمنحك الوصول إلى الأنماط، الجداول، والعلامات الذكية مباشرةً.

## تطبيق التنسيق الشرطي

الآن بعد أن تم إنشاء دفتر العمل، دعنا **نطبق التنسيق الشرطي** لتسليط الضوء على الصفوف التي تتجاوز الكمية فيها 100. التنسيق الشرطي يُطبق على ورقة العمل، وليس على الخلية، مما يجعله قابلاً لإعادة الاستخدام.

```csharp
        // Step 4: Apply conditional formatting to highlight quantities > 100
        int cfIndex = worksheet.ConditionalFormattings.Add();               // add a new CF collection
        var conditionalFormatting = worksheet.ConditionalFormattings[cfIndex];
        var condition = conditionalFormatting.AddCondition(
            FormatConditionType.CellValue, OperatorType.Greater, "100");   // > 100

        // Define the style that will be applied when the condition is true
        condition.Style = workbook.CreateStyle();
        condition.Style.Font.Color = Color.Red;               // red font
        condition.Style.Pattern = BackgroundType.Solid;       // solid background
        condition.Style.ForegroundColor = Color.Yellow;      // yellow fill
```

> **نصيحة احترافية:** إذا كنت تحتاج إلى قواعد أكثر تعقيداً (مثلاً بين قيمتين)، ما عليك سوى استدعاء `AddCondition` مرة أخرى مع `OperatorType.Between`.

## كتابة العناوين والعلامات الذكية

قبل أن **نستورد DataTable إلى Excel**، نحتاج إلى خلايا نائبة—العلامات الذكية—التي ستستبدلها المكتبة بالبيانات الفعلية. فكر فيها كعلامات قالب.

```csharp
        // Step 2: Write the header row
        worksheet.Cells["A1"].PutValue("Product");
        worksheet.Cells["B1"].PutValue("Quantity");
        worksheet.Cells["C1"].PutValue("Status");

        // Step 3: Define smart markers that will be replaced by data
        worksheet.Cells["A2"].PutValue("&=Products.ProductName");
        worksheet.Cells["B2"].PutValue("&=Products.Quantity");
        worksheet.Cells["C2"].PutValue("&=Products.Quantity > 100 ? \"High\" : \"Low\"");
```

> **لماذا العلامات الذكية؟** تسمح لك بفصل تخطيط Excel عن الكود. تصمم الورقة مرة واحدة، ثم تُمرّر `DataTable` وتقوم المكتبة بالباقي.

## استيراد DataTable إلى Excel

هذا هو جوهر **استيراد DataTable إلى Excel**. نقوم بإنشاء `DataTable` يعكس حقول العلامات الذكية ونسلمها إلى `ImportDataTable`.

```csharp
        // Step 5: Build a simple DataTable that matches the smart marker fields
        DataTable products = new DataTable();
        products.Columns.Add("ProductName");
        products.Columns.Add("Quantity", typeof(int));
        products.Rows.Add("Apple", 120);
        products.Rows.Add("Banana", 80);
        products.Rows.Add("Cherry", 150);

        // Step 6: Populate the worksheet with the DataTable via smart markers
        worksheet.Cells.ImportDataTable(products, true, "A2");
```

> **حالة حافة:** إذا كان جدولك يحتوي على أعمدة أكثر مما تحتاج، ما عليك سوى إهمال الأعمدة الزائدة في العلامات الذكية؛ سيتم تجاهلها.

## حفظ دفتر العمل بصيغة XLSX

أخيراً، ن **نحفظ دفتر العمل بصيغة xlsx** على القرص. طريقة `Save` تحدد الصيغة تلقائياً بناءً على امتداد الملف.

```csharp
        // Step 7: Save the result to an Excel file
        workbook.Save("SmartMarkersConditional.xlsx");   // <-- saves as .xlsx
    }
}
```

هذا هو البرنامج بالكامل. عند تشغيله، ستجد ملفاً اسمه `SmartMarkersConditional.xlsx` في مجلد الإخراج.

### النتيجة المتوقعة

| المنتج | الكمية | الحالة |
|--------|--------|---------|
| Apple   | 120    | High    |
| Banana  | 80     | Low     |
| Cherry  | 150    | High    |

الصفوف التي تحتوي على **الكمية > 100** (Apple و Cherry) ستحصل على نص أحمر على خلفية صفراء بفضل التنسيق الشرطي الذي أضفناه مسبقاً.

## إنشاء ملف Excel برمجياً – القائمة الكاملة للمصدر

فيما يلي الشيفرة الكاملة، جاهزة للنسخ. تحتوي على كل ما ناقشنا، بالإضافة إلى بعض التعليقات الإضافية للتوضيح.

```csharp
using Aspose.Cells;
using Aspose.Cells.Tables;
using System.Data;
using System.Drawing;

class SmartMarkerConditionalDemo
{
    static void Main()
    {
        // 1️⃣ Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // 2️⃣ Write header cells
        worksheet.Cells["A1"].PutValue("Product");
        worksheet.Cells["B1"].PutValue("Quantity");
        worksheet.Cells["C1"].PutValue("Status");

        // 3️⃣ Insert smart markers – placeholders for our data
        worksheet.Cells["A2"].PutValue("&=Products.ProductName");
        worksheet.Cells["B2"].PutValue("&=Products.Quantity");
        worksheet.Cells["C2"].PutValue("&=Products.Quantity > 100 ? \"High\" : \"Low\"");

        // 4️⃣ Apply conditional formatting (highlight >100)
        int cfIdx = worksheet.ConditionalFormattings.Add();
        var cf = worksheet.ConditionalFormattings[cfIdx];
        var cond = cf.AddCondition(FormatConditionType.CellValue, OperatorType.Greater, "100");
        cond.Style = workbook.CreateStyle();
        cond.Style.Font.Color = Color.Red;
        cond.Style.Pattern = BackgroundType.Solid;
        cond.Style.ForegroundColor = Color.Yellow;

        // 5️⃣ Build a DataTable that matches the markers
        DataTable products = new DataTable();
        products.Columns.Add("ProductName");
        products.Columns.Add("Quantity", typeof(int));
        products.Rows.Add("Apple", 120);
        products.Rows.Add("Banana", 80);
        products.Rows.Add("Cherry", 150);

        // 6️⃣ Import the DataTable – this replaces the smart markers
        worksheet.Cells.ImportDataTable(products, true, "A2");

        // 7️⃣ Save the workbook – this will create an .xlsx file
        workbook.Save("SmartMarkersConditional.xlsx");
    }
}
```

> **نصيحة:** إذا كنت تحتاج إلى إنشاء عدة أوراق، ما عليك سوى تكرار الخطوات 2‑6 على كائن `Worksheet` جديد يتم الحصول عليه عبر `workbook.Worksheets.Add()`.

## لماذا نستخدم Aspose.Cells لأتمتة Excel في C#؟

- **الأداء:** يعمل بالكامل في الذاكرة، بدون COM interop، لذا يكون سريعاً حتى مع مجموعات بيانات كبيرة.  
- **غني بالميزات:** يدعم العلامات الذكية، التنسيق الشرطي، المخططات، الجداول المحورية، وأكثر.  
- **متعدد المنصات:** يعمل على Windows، Linux، و macOS مع .NET Core/5/6+.  

إذا واجهتك مشكلة في ميزة معينة—مثلاً إضافة مخطط أو حماية ورقة—ابحث عن “asp​ose.cells add chart c#” وستجد نمطاً مشابهاً.

## الخطوات التالية والمواضيع ذات الصلة

- **تصدير إلى PDF:** بعد أن **تنشئ دفتر عمل Excel C#**، يمكنك فوراً تصديره إلى PDF باستخدام `workbook.Save("output.pdf")`.  
- **قراءة ملفات Excel موجودة:** استخدم `new Workbook("ExistingFile.xlsx")` لتعديل قالب موجود.  
- **استيراد جماعي:** للبيانات الضخمة، فكر في استخدام `ImportArray` أو `ImportDataTable` مع `ImportOptions` لتحسين السرعة.  

لا تتردد في تجربة قواعد شرطية مختلفة، ألوان مختلفة، أو حتى إضافة صف إجمالي باستخدام الصيغ. السماء هي الحد عندما **تنشئ ملف Excel برمجياً**.

---

*هل أنت مستعد لتجربتها بنفسك؟ احصل على الشيفرة، شغّلها، وافتح الملف `SmartMarkersConditional.xlsx` الناتج. إذا واجهت أي صعوبات، اترك تعليقاً أدناه—برمجة سعيدة!*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}