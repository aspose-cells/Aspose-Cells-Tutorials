---
category: general
date: 2026-05-04
description: إنشاء إكسل من قالب وربط JSON بملف إكسل مع تسمية أوراق العمل ديناميكيًا.
  تعلم كيفية تعبئة إكسل من JSON وتوليد إكسل باستخدام JSON في دقائق.
draft: false
keywords:
- create excel from template
- map json to excel
- populate excel from json
- dynamic worksheet naming excel
- generate excel using json
language: ar
og_description: إنشاء ملف إكسل من القالب بسرعة. يوضح هذا الدليل كيفية ربط JSON بملف
  إكسل، تعبئة إكسل من JSON، استخدام تسمية أوراق العمل الديناميكية، وإنشاء إكسل باستخدام
  JSON.
og_title: إنشاء إكسل من القالب – دورة .NET كاملة
tags:
- C#
- Aspose.Cells
- SmartMarker
- JSON
title: إنشاء ملف إكسل من القالب – دليل خطوة بخطوة لمطوري .NET
url: /ar/net/templates-reporting/create-excel-from-template-step-by-step-guide-for-net-develo/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء Excel من القالب – دليل .NET كامل

هل احتجت يومًا إلى **إنشاء Excel من القالب** لكن شعرت بالتعقيد عند التعامل مع بيانات JSON وأسماء الأوراق؟ لست وحدك. في العديد من مشاريع التقارير يكون القالب هو الذي يحدد التخطيط بينما تدفع حزمة JSON القيم الفعلية، وربطهما معًا قد يكون صداعًا.

الخبر السار؟ ببضع أسطر من C# ومحرك SmartMarker الخاص بـ Aspose Cells يمكنك **ملء Excel من JSON**، وإعادة تسمية أوراق التفاصيل أثناء التشغيل، وأخيرًا **إنشاء Excel باستخدام JSON** دون الحاجة للتعامل مع الواجهة الرسومية.

في هذا الدرس سنستعرض كامل الخطوات: تحميل القالب، ربط JSON بـ Excel، تكوين تسمية الأوراق الديناميكية، وحفظ المصنف النهائي. في النهاية ستحصل على قطعة شفرة قابلة لإعادة الاستخدام يمكنك إدراجها في أي خدمة .NET. لا أدوات خارجية، مجرد كود نقي.

---

## ما ستحتاجه

- **Aspose.Cells for .NET** (الإصدار 24.10 أو أحدث) – المكتبة التي تشغّل SmartMarker.  
- ملف **template.xlsx** يحتوي على وسوم SmartMarker مثل `{Master:Name}` و `{Detail:Item}`.  
- ملف **data.json** يتطابق مع بنية الماستر‑ديتف.  
- Visual Studio 2022 (أو أي بيئة تطوير تفضّلها) تستهدف .NET 6 أو أحدث.

هذا كل ما تحتاجه. إذا كان لديك هذه المكوّنات، فأنت جاهز للبدء.

---

## إنشاء Excel من القالب – نظرة عامة

الفكرة الأساسية بسيطة: اعتبر ملف Excel كـ *قالب* ودع SmartMarker يستبدل العناصر النائبة بالقيم من JSON الخاص بك. تتيح لك المكتبة أيضًا إعادة تسمية ورقة التفاصيل بناءً على حقل الماستر، وهو ما يجعل **تسمية أوراق العمل الديناميكية في Excel** تتألق.

فيما يلي الشيفرة الكاملة الجاهزة للتنفيذ. يمكنك نسخها ولصقها في تطبيق Console وتعديل المسارات لتتناسب مع ملفاتك.

```csharp
// ------------------------------------------------------------
// Full example: create Excel from template using JSON data
// ------------------------------------------------------------
using System;
using System.IO;
using Aspose.Cells;

namespace ExcelTemplateDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load the workbook that contains SmartMarker tags
            //    (e.g., {Master:Name} in the master sheet and {Detail:Item} in the detail sheet)
            string templatePath = @"C:\MyProject\Templates\template.xlsx";
            Workbook wb = new Workbook(templatePath);

            // 2️⃣ Read the JSON data that will populate the markers
            //    The JSON should match the structure expected by the template.
            string jsonPath = @"C:\MyProject\Data\data.json";
            string json = File.ReadAllText(jsonPath);

            // 3️⃣ Configure the SmartMarker processor to rename the detail sheet
            //    dynamically based on the master record’s Name field.
            //    This demonstrates dynamic worksheet naming excel.
            wb.SmartMarkerProcessor.Options.DetailSheetNewName = "Detail_{Master.Name}";

            // 4️⃣ Execute the SmartMarker processing using the JSON data.
            //    This step maps JSON to Excel and populates every marker.
            wb.SmartMarkerProcessor.Execute(json);

            // 5️⃣ Save the processed workbook – now it’s a brand‑new file.
            string outputPath = @"C:\MyProject\Output\output.xlsx";
            wb.Save(outputPath);

            Console.WriteLine("✅ Excel file generated successfully at: " + outputPath);
        }
    }
}
```

> **النتيجة المتوقعة:**  
> - ستظهر ورقة الماستر الاسم من `Master.Name`.  
> - ستُعاد تسمية ورقة التفاصيل إلى شيء مثل `Detail_JohnDoe`.  
> - جميع صفوف `{Detail:Item}` ستمتلئ بمصفوفة العناصر من JSON.

---

## ربط JSON بـ Excel – تحميل البيانات

قبل أن يتمكن محرك SmartMarker من تنفيذ سحره، يجب أن يكون JSON **مصاغًا بشكل صحيح** ويعكس التسلسل الهرمي المستخدم في القالب. مثال على JSON من نوع ماستر‑ديتف هو كالتالي:

```json
{
  "Master": {
    "Name": "John Doe",
    "Date": "2026-05-04"
  },
  "Detail": [
    { "Item": "Widget A", "Qty": 10, "Price": 2.5 },
    { "Item": "Widget B", "Qty": 5,  "Price": 5.0 }
  ]
}
```

**لماذا هذا مهم:**  
- المفاتيح `Master` و `Detail` تتطابق مباشرةً مع وسوم `{Master:…}` و `{Detail:…}`.  
- إذا اختلفت بنية JSON، لن يجد SmartMarker ما يطابقه، وستبقى الخلايا فارغة.

**نصيحة:** تحقق من صحة JSON باستخدام أداة تحقق سريعة على الإنترنت أو عبر `System.Text.Json.JsonDocument.Parse(json)` لاكتشاف أخطاء الصياغة مبكرًا.

---

## ملء Excel من JSON – إعداد SmartMarker

يعمل SmartMarker عن طريق فحص المصنف للعثور على الوسوم، ثم حقن البيانات. خطوة **populate excel from json** هي في الأساس استدعاء `Execute` الذي رأيناه سابقًا، لكن هناك بعض الإعدادات الاختيارية التي تستحق الذكر:

| الإعداد | ما يفعله | متى يُستخدم |
|---------|----------|-------------|
| `Options.CaseSensitive` | يعامل أسماء الوسوم بحساسية حالة الأحرف. | إذا كان القالب يخلط بين الأحرف الكبيرة والصغيرة وتحتاج إلى مطابقة دقيقة. |
| `Options.RemoveEmptyRows` | يحذف الصفوف التي لم تستقبل بيانات. | للحفاظ على نظافة الورقة النهائية عندما تكون بعض عناصر التفاصيل اختيارية. |
| `Options.EnableHyperlink` | يسمح للروابط داخل JSON بأن تصبح قابلة للنقر. | عندما تحتاج إلى عناوين URL قابلة للنقر في التقرير. |

يمكنك ربطها هكذا:

```csharp
wb.SmartMarkerProcessor.Options.CaseSensitive = true;
wb.SmartMarkerProcessor.Options.RemoveEmptyRows = true;
```

---

## تسمية أوراق العمل الديناميكية في Excel – تكوين اسم ورقة التفاصيل

أحد المتطلبات الأكثر تعقيدًا في العديد من المشاريع هو **تسمية أوراق العمل الديناميكية في Excel**. بدلاً من ورقة “Detail” ثابتة، قد ترغب أن يحمل كل تقرير اسم العميل أو رقم الطلب.

السطر:

```csharp
wb.SmartMarkerProcessor.Options.DetailSheetNewName = "Detail_{Master.Name}";
```

يفعل ذلك بالضبط. يتم استبدال العنصر النائب `{Master.Name}` *بعد* معالجة JSON، لذا يصبح اسم الورقة الجديد `Detail_JohnDoe`.

**حالة حافة:** إذا كان الاسم يحتوي على أحرف غير مسموح بها في أسماء الأوراق (`:`, `\`, `/`, `?`, `*`, `[`, `]`)، يقوم Aspose بتنظيفها تلقائيًا، لكن يمكنك تنظيف السلسلة مسبقًا في JSON إذا كنت تحتاج تنسيقًا محددًا.

---

## إنشاء Excel باستخدام JSON – التنفيذ والحفظ

السطران الأخيران في الشيفرة (`Execute` و `Save`) هما المكان الذي يحدث فيه سحر **generate excel using json**. في الخلفية، يقوم Aspose بتحليل JSON إلى جدول بيانات، يتنقل عبر القالب، ويكتب الملف الناتج.

إذا احتجت إلى إنشاء عدة مصنفات داخل حلقة (مثلاً واحد لكل عميل)، ما عليك سوى نقل إنشاء كائن `Workbook` داخل الحلقة وتغيير اسم ملف الإخراج وفقًا لذلك:

```csharp
foreach (var customerJson in customers)
{
    Workbook wb = new Workbook(templatePath);
    wb.SmartMarkerProcessor.Options.DetailSheetNewName = $"Detail_{customerJson.Master.Name}";
    wb.SmartMarkerProcessor.Execute(customerJson);
    wb.Save($@"C:\Reports\Report_{customerJson.Master.Name}.xlsx");
}
```

هذا النمط شائع في خدمات التقارير الدفعية.

---

## الأخطاء الشائعة & نصائح احترافية

- **الوسوم المفقودة:** إذا ما زالت الخلية تظهر `{Master:Name}`، فهذا يعني أن الوسم لم يُتعرف عليه. تحقق من التهجئة وأن الوسم داخل خلية وليس داخل تعليق.  
- **حجم JSON كبير:** للبيانات الضخمة، فكر في تدفق JSON أو استخدام `DataTable` بدلاً من سلسلة نصية لتقليل الضغط على الذاكرة.  
- **سلامة الخيوط:** كائنات `Workbook` غير آمنة للاستخدام المتوازي. أنشئ نسخة جديدة لكل خيط إذا كنت تشغّل مهامًا متوازية.  
- **قفل الملفات:** تأكد من أن القالب غير مفتوح في Excel أثناء تشغيل الكود؛ وإلا ستواجه `IOException`.

> **نصيحة احترافية:** احتفظ بنسخة من القالب الأصلي في مجلد للقراءة فقط. هذا يمنع الكتابة غير المقصودة أثناء عملية التصحيح.

---

## ملخص المثال الكامل العامل

إليك البرنامج بالكامل مرة أخرى، هذه المرة مع تعليقات داخلية لكل سطر غير واضح:

```csharp
using System;
using System.IO;
using Aspose.Cells;

namespace ExcelTemplateDemo
{
    class Program
    {
        static void Main()
        {
            // Path to the Excel template that contains SmartMarker tags.
            string templatePath = @"C:\MyProject\Templates\template.xlsx";

            // Load the workbook – this is the "create excel from template" step.
            Workbook wb = new Workbook(templatePath);

            // Read JSON data that maps directly to the template's tags.
            string jsonPath = @"C:\MyProject\Data\data.json";
            string json = File.ReadAllText(jsonPath);

            // OPTIONAL: tweak SmartMarker behavior (case‑sensitivity, empty rows, etc.).
            wb.SmartMarkerProcessor.Options.CaseSensitive = false;
            wb.SmartMarkerProcessor.Options.RemoveEmptyRows = true;

            // Set up dynamic worksheet naming based on the master record's Name field.
            wb.SmartMarkerProcessor.Options.DetailSheetNewName = "Detail_{Master.Name}";

            // Run the SmartMarker engine – this is where we "populate excel from json".
            wb.SmartMarkerProcessor.Execute(json);

            // Save the newly generated workbook – the final "generate excel using json" step.
            string outputPath = @"C:\MyProject\Output\output.xlsx";
            wb.Save(outputPath);

            Console.WriteLine("✅ Workbook created at: " + outputPath);
        }
    }
}
```

تشغيل هذا التطبيق Console سيولد `output.xlsx` مع ورقة تفاصيل مُعاد تسميتها وجميع البيانات مملوءة.

---

## الخطوات التالية والمواضيع ذات الصلة

- **التصدير إلى PDF:** بعد إنشاء المصنف، يمكنك استدعاء `wb.Save("report.pdf", SaveFormat.Pdf);` لتوليد نسخة PDF.  
- **ملء المخططات:** يدعم SmartMarker أيضًا مصادر بيانات المخططات؛ ما عليك سوى ربط مصفوفة JSON بنطاق سلسلة المخطط.  
- **التنسيق الشرطي:** استخدم قواعد Excel المدمجة في القالب؛ ستستمر بعد استبدال الوسوم.  
- **تحسين الأداء:** للسيناريوهات ذات الحجم العالي، أعد استخدام كائن `Workbook` واحد مع `Clone` لتجنب عمليات I/O المتكررة.

لا تتردد في تجربة هياكل JSON مختلفة، أنماط إعادة التسمية، أو حتى دمج قوالب متعددة في تشغيل واحد. مرونة **create excel from template** باستخدام Aspose.Cells تسمح لك بتكييف الحل لفواتير، لوحات معلومات، أو أي احتياج تقريري.

---

## ملخص بصري

![إنشاء Excel من القالب يوضح سير عمل JSON → SmartMarker → تسمية ورقة ديناميكية](/images/create-excel-from-template-workflow.png "مخطط سير عمل إنشاء Excel من القالب")

*(النص البديل يتضمن الكلمة المفتاحية الأساسية لتحسين محركات البحث)*

---

### الخاتمة

لقد غطينا كل ما تحتاجه لت **إنشاء Excel من القالب**، **ربط JSON بـ Excel**، **ملء Excel من JSON**، استخدام **تسمية أوراق العمل الديناميكية في Excel**، وأخيرًا **إنشاء Excel باستخدام JSON**. الشيفرة مكتملة، والشرح يوضح *لماذا* كل سطر مهم، والآن لديك أساس قوي لبناء خطوط تقارير أكبر.

هل لديك تعديل تريد تجربته؟ اترك تعليقًا أدناه، ولنساعدك على حل المشكلة معًا. برمجة سعيدة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}