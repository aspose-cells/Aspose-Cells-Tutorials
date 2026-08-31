---
category: general
date: 2026-02-23
description: تسمية أوراق إكسل تلقائيًا وتعلم كيفية إنشاء الأوراق تلقائيًا باستخدام
  SmartMarkers. دليل خطوة بخطوة بلغة C# للدفاتر الديناميكية.
draft: false
keywords:
- auto name excel sheets
- how to generate sheets
- Aspose.Cells SmartMarkers
- dynamic worksheet naming
- C# Excel automation
language: ar
og_description: قم بتسمية أوراق إكسل تلقائيًا على الفور. تعلم كيفية إنشاء الأوراق
  باستخدام SmartMarkers في C# – مثال كامل وقابل للتنفيذ.
og_title: تسمية أوراق إكسل تلقائيًا – دليل سريع بلغة C#
tags:
- C#
- Excel
- Aspose.Cells
title: تسمية أوراق إكسل تلقائيًا – طريقة سهلة لإنشاء الأوراق
url: /ar/net/smart-markers-dynamic-data/auto-name-excel-sheets-easy-way-to-generate-sheets/
---

placeholders or URLs. No URLs present.

Make sure to keep bold markers ** etc.

Now produce final answer.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تسمية أوراق Excel تلقائيًا – دليل C# الكامل

هل تساءلت يومًا كيف **auto name excel sheets** دون كتابة حلقة تعيد تسمية كل تبويب يدويًا؟ لست وحدك. في العديد من مشاريع التقارير يتزايد عدد الأوراق أثناء التشغيل، والحفاظ على الأسماء مرتبة يصبح نقطة ألم. الخبر السار؟ مع **SmartMarkers** في Aspose.Cells يمكنك ترك المكتبة تتولى التسمية لك، وحتى تسمح لك **how to generate sheets** أثناء التشغيل.

في هذا الدليل سنستعرض سيناريو واقعي: إنشاء مصنف، وتكوين خيارات SmartMarker بحيث يتم تسمية أوراق التفاصيل تلقائيًا *Detail*، *Detail1*، *Detail2*، …، ثم التحقق من ظهور الأوراق كما هو متوقع. في النهاية ستحصل على حل مستقل وجاهز للنسخ واللصق يمكنك تكييفه مع أي مشروع يحتاج إلى إنشاء أوراق عمل ديناميكية.

---

## ما ستحتاجه

- **.NET 6+** (أو .NET Framework 4.6.2+). يعمل الكود على أي بيئة تشغيل حديثة.
- حزمة NuGet **Aspose.Cells for .NET** – `Install-Package Aspose.Cells`.
- مشروع C# أساسي (تطبيق Console، WinForms، أو ASP.NET – يعمل نفس الكود في جميع الأماكن).
- Visual Studio، VS Code، أو بيئة التطوير المتكاملة المفضلة لديك.

لا توجد أي تداخلات إضافية مع Excel، ولا COM، فقط شفرة مُدارة خالصة.

---

## الخطوة 1: تسمية أوراق Excel تلقائيًا باستخدام SmartMarkers

أول شيء عليك فعله هو إخبار Aspose.Cells ما هو الاسم الأساسي الذي تريد للأوراق التفصيلية التي تُنشأ تلقائيًا. يتم ذلك عبر الفئة `SmartMarkerOptions`.

```csharp
using Aspose.Cells;
using Aspose.Cells.Tables;   // for SmartMarkers
using System;

class Program
{
    static void Main()
    {
        // Create a new workbook that will hold the master sheet.
        Workbook wb = new Workbook();
        Worksheet ws = wb.Worksheets[0];
        ws.Name = "Master";

        // -----------------------------------------------------------
        // Step 1: Configure SmartMarker options – set the base name
        // -----------------------------------------------------------
        SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions
        {
            // This tells SmartMarkers to create sheets named Detail, Detail1, Detail2, …
            DetailSheetNewName = "Detail"
        };
```

**لماذا هذا مهم:** من خلال تعيين `DetailSheetNewName`، تسلم منطق التسمية إلى المكتبة. لا حاجة لكتابة حلقة `for` تتحقق من أسماء الأوراق الموجودة وتزيد العداد – الـ API يقوم بذلك لك، مما يضمن أسماء فريدة حتى عندما يحتوي مصدر البيانات على عشرات الصفوف.

---

## الخطوة 2: إعداد مصدر البيانات

تعمل SmartMarkers مع أي مجموعة `IEnumerable`، أو `DataTable`، أو حتى قائمة بسيطة من الكائنات. في هذا العرض سنستخدم قائمة بسيطة من الكائنات التي تمثل تفاصيل الطلب.

```csharp
        // -----------------------------------------------------------
        // Step 2: Build a sample data source
        // -----------------------------------------------------------
        var orders = new[]
        {
            new { OrderId = 1001, Product = "Laptop", Qty = 2, Price = 1200.00 },
            new { OrderId = 1002, Product = "Mouse",   Qty = 5, Price =  25.99 },
            new { OrderId = 1003, Product = "Keyboard",Qty = 3, Price =  45.50 }
        };
```

**لماذا هذا مهم:** مصدر البيانات يحدد عدد أوراق التفاصيل التي سيتم إنشاؤها. كل عنصر في المجموعة ينشئ ورقة جديدة بناءً على قالب SmartMarker الذي سنضيفه لاحقًا.

---

## الخطوة 3: إدراج قالب SmartMarker في ورقة الماستر

قالب SmartMarker هو مجرد خلية (أو نطاق) يحتوي على عناصر نائبة. عندما يتم تشغيل طريقة `Apply`، يتم استبدال العناصر النائبة بالبيانات الفعلية، ولكل صف يتم إنشاء ورقة جديدة.

```csharp
        // -----------------------------------------------------------
        // Step 3: Add a SmartMarker template to the master sheet
        // -----------------------------------------------------------
        // Put a header row
        ws.Cells["A1"].PutValue("Order ID");
        ws.Cells["B1"].PutValue("Product");
        ws.Cells["C1"].PutValue("Quantity");
        ws.Cells["D1"].PutValue("Unit Price");

        // Insert SmartMarker placeholders starting at row 2
        ws.Cells["A2"].PutValue("&=orders.OrderId");
        ws.Cells["B2"].PutValue("&=orders.Product");
        ws.Cells["C2"].PutValue("&=orders.Qty");
        ws.Cells["D2"].PutValue("&=orders.Price");
```

**لماذا هذا مهم:** صيغة `&=` تخبر SmartMarkers بـ “خذ القيمة من مصدر البيانات”. عندما يتم تشغيل `Apply`، سيقوم Aspose.Cells بنسخ هذا الصف إلى ورقة جديدة لكل عنصر في `orders`، مع تسمية الورقة تلقائيًا بناءً على الخيار الذي حددناه مسبقًا.

---

## الخطوة 4: تطبيق خيارات SmartMarker – هنا يتم تسمية الأوراق تلقائيًا

الآن يأتي الوقت الذي تقوم فيه المكتبة بالعمل الشاق. استدعاء `Apply` يقرأ القالب، ينشئ أوراق التفاصيل، ويسميها وفقًا لـ `DetailSheetNewName`.

```csharp
        // -----------------------------------------------------------
        // Step 4: Apply SmartMarker – auto name excel sheets happens here
        // -----------------------------------------------------------
        ws.SmartMarkers.Apply(smartMarkerOptions, new { orders });

        // Save the workbook to verify the result
        wb.Save("AutoNamedSheets.xlsx");
        Console.WriteLine("Workbook saved. Open AutoNamedSheets.xlsx to see the result.");
    }
}
```

**لماذا هذا مهم:** طريقة `Apply` لا تملأ البيانات فقط بل تحترم أيضًا نمط التسمية الذي قدمناه. إذا فتحت *AutoNamedSheets.xlsx* سترى:

- **Detail** – يحتوي على الطلب الأول.
- **Detail1** – الطلب الثاني.
- **Detail2** – الطلب الثالث.

لا حاجة لإعادة تسمية يدويًا.

---

## الخطوة 5: التحقق من النتيجة – كيفية إنشاء الأوراق بشكل صحيح

بعد تشغيل البرنامج، افتح الملف المُولد. يجب أن ترى ثلاث أوراق عمل جديدة مسماة تمامًا كما هو موضح أعلاه. هذا يثبت أنك تعلمت بنجاح **how to generate sheets** تلقائيًا.

> **نصيحة احترافية:** إذا كنت بحاجة إلى لاحقة مخصصة (مثلاً “_Report”)، فقط عيّن `DetailSheetNewName = "Detail_Report"` وستضيف المكتبة أرقامًا بعد السلسلة الأساسية.

---

## الحالات الخاصة والأسئلة الشائعة

### ماذا لو كان الاسم الأساسي موجودًا بالفعل؟

يتحقق Aspose.Cells من وجود أسماء أوراق مسبقًا ويضيف رقمًا متزايدًا حتى يتم العثور على اسم فريد. لذا حتى إذا كانت ورقة تسمى *Detail* موجودة بالفعل في المصنف، فإن الورقة التالية التي تُنشأ ستصبح *Detail1*.

### هل يمكنني التحكم في ترتيب الأوراق المُنشأة؟

نعم. يتبع الترتيب تسلسل مصدر البيانات. إذا كنت بحاجة إلى ترتيب محدد، قم بفرز المجموعة قبل تمريرها إلى `Apply`.

### هل من الممكن إنشاء أوراق في مصنف مختلف؟

بالطبع. أنشئ نسخة ثانية من `Workbook`، أضف ورقة عمل كعنصر نائب، واستدعِ `Apply` على تلك الورقة. ينطبق نفس منطق التسمية.

### كيف يعمل هذا مع مجموعات بيانات كبيرة؟

تم تحسين SmartMarkers للأداء. حتى مع آلاف الصفوف، تقوم المكتبة ببث البيانات بكفاءة. فقط تأكد من أن لديك ذاكرة كافية لحجم المصنف النهائي.

---

## مثال كامل جاهز للتنفيذ (نسخ‑لصق)

فيما يلي البرنامج الكامل الذي يمكنك وضعه في مشروع Console جديد. لا توجد أجزاء مفقودة – كل شيء من توجيهات `using` إلى استدعاء `Save` النهائي مشمول.

```csharp
using Aspose.Cells;
using Aspose.Cells.Tables;
using System;

class AutoNameExcelSheetsDemo
{
    static void Main()
    {
        // 1️⃣ Create workbook and master worksheet
        Workbook workbook = new Workbook();
        Worksheet master = workbook.Worksheets[0];
        master.Name = "Master";

        // 2️⃣ Set up SmartMarker options – this is the key to auto‑naming
        SmartMarkerOptions options = new SmartMarkerOptions
        {
            DetailSheetNewName = "Detail"   // base name for generated sheets
        };

        // 3️⃣ Sample data source – each element will become a new sheet
        var orders = new[]
        {
            new { OrderId = 1001, Product = "Laptop",   Qty = 2, Price = 1200.00 },
            new { OrderId = 1002, Product = "Mouse",    Qty = 5, Price =  25.99 },
            new { OrderId = 1003, Product = "Keyboard", Qty = 3, Price =  45.50 }
        };

        // 4️⃣ Build a simple template on the master sheet
        master.Cells["A1"].PutValue("Order ID");
        master.Cells["B1"].PutValue("Product");
        master.Cells["C1"].PutValue("Quantity");
        master.Cells["D1"].PutValue("Unit Price");

        master.Cells["A2"].PutValue("&=orders.OrderId");
        master.Cells["B2"].PutValue("&=orders.Product");
        master.Cells["C2"].PutValue("&=orders.Qty");
        master.Cells["D2"].PutValue("&=orders.Price");

        // 5️⃣ Apply SmartMarkers – this auto‑creates and auto‑names the sheets
        master.SmartMarkers.Apply(options, new { orders });

        // 6️⃣ Save and inform the user
        workbook.Save("AutoNamedSheets.xlsx");
        Console.WriteLine("Done! Open AutoNamedSheets.xlsx – you’ll see Detail, Detail1, Detail2 …");
    }
}
```

شغّل البرنامج، افتح الملف الناتج *AutoNamedSheets.xlsx*، وسترى ميزة **auto name excel sheets** تعمل.

---

## أسئلة متابعة شائعة

- **هل يمكنني استخدام هذا مع ملف قالب موجود؟**  
  نعم. حمّل المصنف باستخدام `new Workbook("Template.xlsx")` وعيّن `master` إلى الورقة التي تحتوي على عناصر نائبة SmartMarker.

- **ماذا لو احتجت إلى صيغ تسمية مختلفة لكل نوع ورقة؟**  
  أنشئ عدة كائنات `SmartMarkerOptions`، كل منها يحتوي على `DetailSheetNewName` الخاص به، وطبقها على أوراق ماستر مختلفة.

- **هل هناك طريقة لإخفاء ورقة القاعدة (التي تحتوي على القالب)؟**  
  بعد `Apply`، يمكنك ببساطة حذف ورقة الماستر: `workbook.Worksheets.RemoveAt(0);` – تبقى أوراق التفاصيل دون تعديل.

---

## الخلاصة

أنت الآن تعرف **how to auto name excel sheets** باستخدام Aspose.Cells SmartMarkers، وقد رأيت أيضًا نمطًا قويًا لـ **how to generate sheets** بشكل ديناميكي في C#. الفكرة الأساسية بسيطة: قم بتكوين `SmartMarkerOptions.DetailSheetNewName`، وزود المكتبة بمجموعة، ودعها تتولى البقية. هذا النهج يلغي الحاجة إلى حلقات متكررة، يضمن أسماء فريدة، ويتوسع بسلاسة.

هل أنت مستعد للخطوة التالية؟ جرّب استبدال مصدر البيانات بـ `Data

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}