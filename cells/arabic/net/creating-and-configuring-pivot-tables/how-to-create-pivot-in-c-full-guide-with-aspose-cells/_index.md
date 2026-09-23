---
category: general
date: 2026-03-27
description: كيفية إنشاء Pivot في C# باستخدام Aspose.Cells – تعلم إضافة البيانات،
  تمكين التحديث، وحفظ المصنف كملف xlsx في دليل واحد.
draft: false
keywords:
- how to create pivot
- save workbook as xlsx
- how to enable refresh
- how to add data
- generate excel file c#
language: ar
og_description: كيفية إنشاء Pivot في C# باستخدام Aspose.Cells. يوضح لك هذا الدليل
  كيفية إضافة البيانات، تمكين التحديث، وحفظ المصنف كملف xlsx.
og_title: كيفية إنشاء Pivot في C# – دليل Aspose.Cells الكامل
tags:
- Aspose.Cells
- C#
- Excel automation
title: كيفية إنشاء جدول محوري في C# – دليل كامل مع Aspose.Cells
url: /ar/net/creating-and-configuring-pivot-tables/how-to-create-pivot-in-c-full-guide-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية إنشاء Pivot في C# – دليل Aspose.Cells الكامل

هل تساءلت يومًا **كيف تنشئ Pivot** في C# دون التعامل مع COM interop؟ لست وحدك. في العديد من التطبيقات المعتمدة على البيانات نحتاج إلى طريقة سريعة لتحويل أرقام المبيعات الخام إلى ملخص منظم، وAspose.Cells يجعل ذلك سهلًا للغاية.  

في هذا الدرس سنستعرض كل خطوة: إضافة البيانات، بناء جدول الـ Pivot، تفعيل التحديث التلقائي، وأخيرًا **حفظ المصنف كملف xlsx** حتى يتمكن المستخدمون من فتحه في Excel فورًا. في النهاية ستحصل على ملف `PivotRefresh.xlsx` جاهز للاستخدام وفهم قوي لأسباب أهمية كل سطر من الشيفرة.

## المتطلبات المسبقة

- .NET 6+ (أو .NET Framework 4.7.2 وما بعده) – أي نسخة حديثة من الـ runtime تعمل.
- Aspose.Cells for .NET – يمكنك الحصول عليها من NuGet (`Install-Package Aspose.Cells`).
- إلمام أساسي بصياغة C# – لا تحتاج إلى معرفة عميقة بـ Excel.

> **نصيحة محترف:** إذا كنت تعمل على جهاز مؤسسي، تأكد من تطبيق رخصة Aspose؛ وإلا ستحصل على علامة مائية على الملف المُولد.

## الخطوة 1 – كيفية إضافة بيانات إلى مصنف جديد

قبل أن يتواجد Pivot، يجب أن يكون هناك جدول مصدر. سننشئ مصنفًا جديدًا، نسمي الورقة الأولى *SalesData*، ونضيف بضع صفوف تحاكي بيانات مبيعات حقيقية.

```csharp
using Aspose.Cells;
using Aspose.Cells.Pivot;

class PivotRefreshTutorial
{
    static void Main()
    {
        // 1️⃣ Create a new workbook and grab the default sheet
        var workbook = new Workbook();
        var salesDataSheet = workbook.Worksheets[0];
        salesDataSheet.Name = "SalesData";

        // 2️⃣ Write column headers
        salesDataSheet.Cells["A1"].PutValue("Region");
        salesDataSheet.Cells["B1"].PutValue("Product");
        salesDataSheet.Cells["C1"].PutValue("Units");
        salesDataSheet.Cells["D1"].PutValue("Revenue");

        // 3️⃣ Insert a sample row – add more rows as your scenario demands
        salesDataSheet.Cells["A2"].PutValue("East");
        salesDataSheet.Cells["B2"].PutValue("Widget");
        salesDataSheet.Cells["C2"].PutValue(120);
        salesDataSheet.Cells["D2"].PutValue(5400);
```

**لماذا هذا مهم:**  
- استخدام `PutValue` يحدد نوع الخلية تلقائيًا، لذا لا تحتاج للقلق بشأن تعارض السلاسل النصية مع القيم الرقمية لاحقًا.  
- تعريف العناوين في الصف 1 يمنح محرك الـ Pivot ما يحتاجه للرجوع إليه عند تعيين الحقول.

## الخطوة 2 – إنشاء ورقة عمل ستستضيف جدول الـ Pivot

يعيش جدول الـ Pivot على ورقته الخاصة، مما يحافظ على نظافة بيانات المصدر وترتيب التقرير.

```csharp
        // 4️⃣ Add a dedicated sheet for the pivot
        var pivotSheet = workbook.Worksheets.Add("PivotReport");
```

> **ماذا لو كان لديك ورقة موجودة بالفعل؟** ما عليك سوى الإشارة إليها عبر الفهرس (`workbook.Worksheets["MySheet"]`) بدلاً من إضافة ورقة جديدة.

## الخطوة 3 – تعريف نطاق المصدر (كيفية إضافة بيانات → تعريف النطاق)

تحتاج Aspose.Cells إلى `CellArea` أو سلسلة نطاق تشمل كلًا من العناوين والبيانات. هنا نفترض حدًا أقصى قدره 100 صف؛ عدّل حسب الحاجة.

```csharp
        // 5️⃣ Build the source range (A1:D100 covers headers + up to 99 data rows)
        var sourceRange = salesDataSheet.Cells.CreateRange("A1:D100");
```

**حالة خاصة:** إذا كان مجموعة البيانات ديناميكية، يمكنك حساب آخر صف مستخدم عبر `salesDataSheet.Cells.MaxDataRow` وبناء النطاق بناءً عليه.

## الخطوة 4 – كيفية إنشاء Pivot – إدراج جدول الـ Pivot

الجزء الممتع الآن: نخبر Aspose.Cells بإنشاء Pivot مرتبط بالنطاق الذي حددناه للتو.

```csharp
        // 6️⃣ Insert the pivot table at cell A3 of the pivot sheet
        int pivotIndex = pivotSheet.PivotTables.Add("=SalesData!A1:D100", "A3", "SalesPivot");
        var pivotTable = pivotSheet.PivotTables[pivotIndex];
```

لاحظ إشارة النمط الصيغي (`=SalesData!A1:D100`). هذه هي نفس الصياغة التي تكتبها في Excel، مما يجعل الـ API بديهيًا.

## الخطوة 5 – تكوين حقول الصفوف، الأعمدة، والبيانات (كيفية إضافة بيانات → الحقول)

سنضع *Region* في الصفوف، *Product* في الأعمدة، ونجمع كل من *Units* و *Revenue*.

```csharp
        // 7️⃣ Set up row, column, and data fields
        pivotTable.RowFields.Add(0); // 0 = first column => Region
        pivotTable.ColumnFields.Add(1); // 1 = second column => Product
        pivotTable.DataFields.Add(2, "Sum of Units", PivotTableDataAggregationType.Sum);
        pivotTable.DataFields.Add(3, "Sum of Revenue", PivotTableDataAggregationType.Sum);
```

**لماذا هذه الفهارس؟**  
تبدأ فهارس الأعمدة في Aspose.Cells من 0، لذا `0` يشير إلى *Region*. تسمح لك طريقة `DataFields.Add` بإعادة تسمية الحقل (مثلاً “Sum of Units”) واختيار نوع التجميع – `Sum` هو الأكثر شيوعًا للبيانات الرقمية.

## الخطوة 6 – كيفية تمكين التحديث – جعل الـ Pivot يحدث تلقائيًا عند الفتح

إذا تغيرت بيانات المصدر لاحقًا، ربما تريد أن ينعكس ذلك تلقائيًا في الـ Pivot. هنا يأتي دور `RefreshDataOnOpen`.

```csharp
        // 8️⃣ Turn on automatic refresh when the file is opened
        pivotTable.RefreshDataOnOpen = true;
```

> **ملاحظة:** هذه العلامة تعمل فقط عندما يُفتح المصنف في Excel؛ لن تُعيد الحساب داخل Aspose.Cells إلا إذا استدعيت `pivotTable.RefreshData()` يدويًا.

## الخطوة 7 – حفظ المصنف كملف XLSX (كيفية حفظ المصنف كملف XLSX)

أخيرًا، نقوم بحفظ الملف على القرص. صيغة `.xlsx` هي صيغة Excel الحديثة القائمة على الـ zip والتي تعمل في كل مكان.

```csharp
        // 9️⃣ Save the workbook – this also satisfies the “save workbook as xlsx” requirement
        workbook.Save("PivotRefresh.xlsx");
    }
}
```

تشغيل البرنامج ينتج ملفًا باسم **PivotRefresh.xlsx** في مجلد التنفيذ. افتحه في Excel وسترى Pivot منظمًا مع صفوف *Region*، أعمدة *Product*، وقيم *Units* و *Revenue* المجمعة. وبما أننا فعلنا التحديث التلقائي، أي تعديل تجريه على ورقة *SalesData* سيُحدّث الـ Pivot تلقائيًا في المرة التالية التي تفتح فيها المصنف.

### النتيجة المتوقعة

| Region | Widget | Gadget | … |
|--------|--------|--------|---|
| East   | 120    | 0      |   |
| West   | 0      | 85     |   |
| **Grand Total** | **120** | **85** |   |

*(الأرقام قد تختلف بناءً على الصفوف التي تضيفها.)*

---

## أسئلة شائعة وبدائل

### ماذا لو احتجت إلى جداول Pivot متعددة؟

يمكنك تكرار **الخطوة 4** باختيار اسم وموقع مختلف. كل استدعاء لـ `PivotTables.Add` يُعيد فهرسًا جديدًا يمكنك استخدامه لاسترجاع كائن الجدول.

### كيف أغيّر التجميع إلى *Average* بدلًا من *Sum*؟

استبدل `PivotTableDataAggregationType.Sum` بـ `PivotTableDataAggregationType.Average` في استدعاءات `DataFields.Add`.

### هل يمكن تنسيق الـ Pivot (خطوط، ألوان)؟

نعم. بعد إنشاء الـ Pivot، يمكنك الوصول إلى خاصية `Style` أو تطبيق تنسيق خلايا على النطاق الذي يحتوي الـ Pivot. مثال:

```csharp
pivotTable.Style = workbook.Styles[workbook.Styles.Add()];
pivotTable.Style.Font.Color = System.Drawing.Color.DarkBlue;
```

### هل يمكن إضافة صفوف أخرى بعد حفظ المصنف؟

بالطبع. حمّل الملف عبر `new Workbook("PivotRefresh.xlsx")`، أضف صفوفًا إلى ورقة *SalesData*، ثم استدعِ `pivotTable.RefreshData()` قبل حفظه مرة أخرى.

---

## مثال كامل جاهز للتنفيذ (انسخه‑الصقه)

```csharp
using Aspose.Cells;
using Aspose.Cells.Pivot;

class PivotRefreshTutorial
{
    static void Main()
    {
        // Step 1: Create workbook & add sample data
        var workbook = new Workbook();
        var salesDataSheet = workbook.Worksheets[0];
        salesDataSheet.Name = "SalesData";

        salesDataSheet.Cells["A1"].PutValue("Region");
        salesDataSheet.Cells["B1"].PutValue("Product");
        salesDataSheet.Cells["C1"].PutValue("Units");
        salesDataSheet.Cells["D1"].PutValue("Revenue");

        // Sample rows – extend as needed
        salesDataSheet.Cells["A2"].PutValue("East");
        salesDataSheet.Cells["B2"].PutValue("Widget");
        salesDataSheet.Cells["C2"].PutValue(120);
        salesDataSheet.Cells["D2"].PutValue(5400);

        salesDataSheet.Cells["A3"].PutValue("West");
        salesDataSheet.Cells["B3"].PutValue("Gadget");
        salesDataSheet.Cells["C3"].PutValue(85);
        salesDataSheet.Cells["D3"].PutValue(4250);

        // Step 2: Add sheet for the pivot
        var pivotSheet = workbook.Worksheets.Add("PivotReport");

        // Step 3: Define source range (covers up to 100 rows)
        var sourceRange = salesDataSheet.Cells.CreateRange("A1:D100");

        // Step 4: Insert pivot table
        int pivotIndex = pivotSheet.PivotTables.Add("=SalesData!A1:D100", "A3", "SalesPivot");
        var pivotTable = pivotSheet.PivotTables[pivotIndex];

        // Step 5: Configure fields
        pivotTable.RowFields.Add(0); // Region
        pivotTable.ColumnFields.Add(1); // Product
        pivotTable.DataFields.Add(2, "Sum of Units", PivotTableDataAggregationType.Sum);
        pivotTable.DataFields.Add(3, "Sum of Revenue", PivotTableDataAggregationType.Sum);

        // Step 6: Enable automatic refresh
        pivotTable.RefreshDataOnOpen = true;

        // Step 7: Save as .xlsx
        workbook.Save("PivotRefresh.xlsx");
    }
}
```

احفظ الملف، شغّله، وافتح **PivotRefresh.xlsx** المُولد – لقد أتقنت الآن **كيفية إنشاء Pivot** في C#.

---

## الخلاصة

غطّينا **كيفية إنشاء جداول Pivot** برمجيًا، وكيفية **إضافة البيانات**، وكيفية **تمكين التحديث**، وأخيرًا كيفية **حفظ المصنف كملف xlsx** باستخدام Aspose.Cells. الكود

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}