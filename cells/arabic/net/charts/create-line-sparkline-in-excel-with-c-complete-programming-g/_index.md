---
category: general
date: 2026-06-30
description: إنشاء سباركلين خطي في Excel باستخدام C# بسرعة. تعلّم كيفية إضافة سباركلين،
  إنشاء مصنف Excel باستخدام C#، وإضافة السباركلين إلى خلية في بضع خطوات.
draft: false
keywords:
- create line sparkline
- how to add sparkline
- add line sparkline
- create excel workbook c#
- add sparkline to cell
language: ar
og_description: إنشاء مخطط خطي صغير في Excel باستخدام C#. يوضح هذا الدرس كيفية إضافة
  مخطط sparkline، وإنشاء مصنف Excel باستخدام C#، وتضمين المخطط في خلية.
og_title: إنشاء مخطط سباركل خطي في Excel باستخدام C# – دليل خطوة بخطوة
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Create line sparkline in Excel with C# quickly. Learn how to add sparkline,
    create Excel workbook C#, and add sparkline to cell in a few steps.
  headline: Create line sparkline in Excel with C# – Complete Programming Guide
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
title: إنشاء مخطط سباركل خطي في إكسل باستخدام C# – دليل برمجة شامل
url: /ar/net/charts/create-line-sparkline-in-excel-with-c-complete-programming-g/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء مخطط خطي صغير في Excel باستخدام C# – دليل برمجة كامل

هل تساءلت يومًا كيف **تنشئ مخططًا خطيًا صغيرًا** في ملف Excel باستخدام C#؟ لست وحدك—المطورون يسألون باستمرار: “كيف أضيف مخططًا صغيرًا إلى تقرير دون فتح Excel يدويًا؟” الخبر السار هو أنه ببضع أسطر من الشيفرة يمكنك توليد مخطط خطي أنيق داخل المصنف، دون الحاجة إلى واجهة مستخدم.

في هذا الدرس سنستعرض كل ما تحتاج معرفته: من أساسيات **إنشاء مصنف Excel C#**، إلى تعبئة البيانات، ثم الخطوات الدقيقة لـ **إضافة مخطط خطي صغير** و**إضافة مخطط صغير إلى خلية**. في النهاية ستحصل على ملف *.xlsx* جاهز يُظهر اتجاهات المبيعات الشهرية بنظرة واحدة. لا إطالة، مجرد حل عملي قابل للتنفيذ.

---

## ما ستبنيه

- مصنف Excel جديد اسمه *KPI_Sparklines.xlsx*  
- ورقة عمل تسمى **KPI** تحتوي على أرقام مبيعات نموذجية  
- **مخطط خطي صغير** موضعه في الخلية **D2** ويشير إلى نطاق البيانات **B2:B13**  
- تنسيق أساسي (لون، وزن الخط) لجعل المخطط يبرز  

المتطلبات المسبقة؟ فقط .NET SDK (3.1+ أو .NET 6) ومكتبة Aspose.Cells for .NET المجانية (متوفرة عبر NuGet). إذا لم تستخدم Aspose.Cells من قبل، فكر فيها كمحرك Excel قوي يمكنك استدعاؤه من الشيفرة—بدون COM interop، بدون الحاجة لتثبيت Excel.

---

![إنشاء مخطط خطي صغير في Excel باستخدام C#](https://example.com/images/create-line-sparkline.png "إنشاء مخطط خطي صغير في Excel باستخدام C#")

*نص بديل للصورة: مثال على إنشاء مخطط خطي صغير في Excel باستخدام كود C#*

---

## الخطوة 1: **إنشاء مصنف Excel C#** – إعداد الملف وورقة العمل

أولًا وقبل كل شيء. نحتاج إلى كائن مصنف (Workbook) وورقة عمل (Worksheet) حيث ستُحفظ البيانات. هذا هو الأساس لأي أتمتة Excel، سواء أضفت لاحقًا **مخططًا خطيًا صغيرًا** أو كتبت صيغًا.

```csharp
using Aspose.Cells;
using System.Drawing;

// Initialize a new workbook
Workbook workbook = new Workbook();

// Grab the first worksheet (index 0) and give it a meaningful name
Worksheet worksheet = workbook.Worksheets[0];
worksheet.Name = "KPI";   // “KPI” will hold our key performance indicators
```

> **لماذا هذا مهم:** تمثل فئة `Workbook` الملف بأكمله، بينما `Worksheet` هي القماش الذي تُرسم عليه الصفوف والأعمدة، وفي النهاية مخططنا الصغير. تسمية الورقة مبكرًا تجعل الملف منظمًا ويوثق نفسه تلقائيًا.

---

## الخطوة 2: تعبئة البيانات – نطاق المصدر للمخطط الصغير

المخطط الصغير يحتاج إلى بيانات ليُرسمها. لنُحاكي 12 شهرًا من أرقام المبيعات. يمكنك سحب هذه القيم من قاعدة بيانات، لكن للتوضيح سنولدها مباشرةً.

```csharp
// Fill column B (index 1) with monthly sales numbers
for (int month = 0; month < 12; month++)
{
    // Example pattern: start at 5,000 and increase by 750 each month
    worksheet.Cells[month + 1, 1].PutValue(5000 + month * 750);
}
```

> **نصيحة:** `PutValue` يكتشف نوع البيانات تلقائيًا، لذا لا تحتاج إلى تحويلها إلى `double` أو `int`. إذا احتجت لتنسيق الخلايا (عملة، فواصل آلاف)، يمكنك تطبيق كائن `Style` لاحقًا.

---

## الخطوة 3: **إنشاء مخطط خطي صغير** – إضافة المخطط إلى خلية محددة

الآن نصل إلى نجم العرض: **المخطط الخطّي الصغير**. تقوم Aspose.Cells بتجميع المخططات الصغيرة في مجموعات، لذا أولًا ننشئ `SparklineGroup` من النوع `Line`، ثم نحدد مكان ظهور الصورة البصرية.

```csharp
// Add a new SparklineGroup of type Line
int groupIndex = worksheet.SparklineGroups.Add(SparklineType.Line);
SparklineGroup sparklineGroup = worksheet.SparklineGroups[groupIndex];

// Add a sparkline that lives in D2 (row 1, column 3) and reads data from B2:B13
// Parameters: firstRow, firstColumn, lastRow, lastColumn, firstDataRow, lastDataRow
sparklineGroup.Add(1, 3, 1, 3, 1, 12);   // D2 ↔ B2:B13
```

> **كيف يعمل:**  
> - `firstRow/firstColumn` و `lastRow/lastColumn` يحددان *الخلية المستهدفة* (حيث يظهر المخطط).  
> - `firstDataRow/lastDataRow` يشيران إلى نطاق المصدر.  
> لأننا نستخدم **مخططًا خطيًا صغيرًا**، ستكون الصورة خطًا رفيعًا يتبع اتجاه الأرقام.

### اختياري: **كيفية إضافة مخطط صغير** مع تنسيق مخصص

إذا أردت أن يبرز المخطط، عدّل بعض الخصائص:

```csharp
sparklineGroup.LineWeight = 1.0;               // Thickness of the line
sparklineGroup.SeriesColor = Color.DarkBlue;  // Color of the sparkline line
sparklineGroup.ShowMarkers = true;             // Show data markers (optional)
sparklineGroup.MarkerColor = Color.OrangeRed;  // Marker color
```

> **لماذا نُنسق؟** خط أزرق داكن على خلفية بيضاء مريح للعين، بينما تُعطي العلامات إشارة سريعة إلى القيم الفردية—مفيد للعروض التقديمية.

---

## الخطوة 4: حفظ المصنف – التحقق من النتيجة

بعد وضع المخطط، نحتاج فقط إلى كتابة الملف على القرص. اختر مجلدًا لديك صلاحية كتابة فيه؛ المثال يستخدم مسارًا مؤقتًا يجب استبداله.

```csharp
// Save the workbook as an .xlsx file
string outputPath = @"C:\Temp\KPI_Sparklines.xlsx";
workbook.Save(outputPath);
```

> **التحقق:** افتح الملف المُولد في Excel (أو أي عارض يدعم .xlsx). يجب أن ترى **مخططًا خطيًا صغيرًا** في الخلية **D2** يعكس أرقام المبيعات المتزايدة في العمود **B**. تمرير الفأرة فوق المخطط سيظهر تلميحًا يحتوي على القيم الأساسية.

---

## الخطوة 5: المشكلات الشائعة عند **إضافة مخطط صغير إلى خلية**

حتى المثال البسيط قد يواجه مبتدئين بعض العقبات. إليك بعض الأمور التي يجب الانتباه لها:

| المشكلة | لماذا يحدث | الحل |
|-------|------------|-----|
| إحداثيات الخلية غير صحيحة | هدف المخطط يستخدم فهرس عمود يبدأ من الصفر لكن فهرس الصف يبدأ من الواحد. | تذكر أن `Cells[row, column]` حيث `row` و `column` كلاهما يبدأ من الصفر. في `SparklineGroup.Add`، الصفوف والأعمدة **تبدأ من الواحد**. |
| لا تُعرض البيانات | نطاق المصدر فارغ أو يحتوي على قيم غير رقمية. | تأكد أن النطاق (مثال: `B2:B13`) يحتوي أرقامًا. استخدم `PutValue` مع أنواع رقمية. |
| يختفي المخطط بعد الحفظ | عدم توافق نسخة المكتبة أو عدم وجود ترخيص. | استخدم أحدث حزمة Aspose.Cells ووفّر ترخيصًا صالحًا إذا تجاوزت حدود التقييم. |
| التنسيق غير مطبق | تم تعديل النمط قبل إنشاء المخطط. | ضع التنسيق **بعد** إنشاء المجموعة، كما هو موضح أعلاه. |

---

## الشيفرة الكاملة – نسخة واحدة للنسخ واللصق

فيما يلي البرنامج الكامل الجاهز للتنفيذ. الصقه في مشروع Console جديد، أضف حزمة Aspose.Cells عبر NuGet، ثم اضغط **F5**.

```csharp
using Aspose.Cells;
using System.Drawing;

namespace SparklineDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // Step 1: Create Excel workbook C#
            // -------------------------------------------------
            Workbook workbook = new Workbook();
            Worksheet worksheet = workbook.Worksheets[0];
            worksheet.Name = "KPI";

            // -------------------------------------------------
            // Step 2: Populate monthly sales data (B2:B13)
            // -------------------------------------------------
            for (int month = 0; month < 12; month++)
            {
                worksheet.Cells[month + 1, 1].PutValue(5000 + month * 750);
            }

            // -------------------------------------------------
            // Step 3: Create line sparkline and add it to D2
            // -------------------------------------------------
            int groupIdx = worksheet.SparklineGroups.Add(SparklineType.Line);
            SparklineGroup sparklineGroup = worksheet.SparklineGroups[groupIdx];
            sparklineGroup.Add(1, 3, 1, 3, 1, 12); // D2 ↔ B2:B13

            // -------------------------------------------------
            // Step 4: Optional formatting (how to add sparkline with style)
            // -------------------------------------------------
            sparklineGroup.LineWeight = 1.0;
            sparklineGroup.SeriesColor = Color.DarkBlue;
            sparklineGroup.ShowMarkers = true;
            sparklineGroup.MarkerColor = Color.OrangeRed;

            // -------------------------------------------------
            // Step 5: Save the workbook
            // -------------------------------------------------
            string outputPath = @"C:\Temp\KPI_Sparklines.xlsx";
            workbook.Save(outputPath);

            System.Console.WriteLine($"Workbook saved to {outputPath}");
        }
    }
}
```

**الناتج المتوقع:** عند فتح *KPI_Sparklines.xlsx*، سيظهر العمود **B** يحتوي على 12 رقمًا (5,000 → 13,250) وتحتوي الخلية **D2** على مخطط خطي صغير أزرق داكن يتصاعد بسلاسة. إذا فعلت `ShowMarkers` ستظهر العلامات كنقاط برتقالية‑حمراء صغيرة.

---

## ما التالي؟ توسيع مهارات المخططات الصغيرة

بعد إتقانك **إنشاء مخطط خطي صغير** باستخدام Aspose.Cells، فكر في استكشاف المواضيع ذات الصلة:

- **إضافة مخطط عمودي صغير** – مثالي لعرض بيانات مكدسة.  
- **إنشاء مجموعات متعددة من المخططات الصغيرة** على نفس الورقة للمقارنة جنبًا إلى جنب.  
- **التصدير إلى PDF** مع الحفاظ على المخططات الصغيرة (Aspose.Cells يدعم تحويل PDF).  
- **مصادر بيانات ديناميكية** – سحب أرقام المبيعات الحقيقية من قاعدة بيانات SQL بدلاً من القيم الثابتة.  

كل هذه تبني على المفاهيم الأساسية نفسها: **إنشاء مصنف Excel C#**، تعبئة البيانات، و**إضافة مخطط صغير إلى خلية** بالأسلوب المطلوب.

---

### TL;DR

عرضنا كيفية **إنشاء مخطط خطي صغير** في مصنف Excel باستخدام C#. الخطوات—*إنشاء المصنف، ملء البيانات، إضافة المخطط، تنسيقه، وحفظه*—مجمعة في برنامج واحد مكتمل. لا تتردد في تعديل الألوان، وزن الخط، أو نطاق المصدر لتتناسب مع احتياجات تقاريرك.

هل لديك تعديل أو تحسين ترغب بمشاركته؟ اترك تعليقًا أدناه، ونتمنى لك برمجة سعيدة!

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تُبنى على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة شاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [أتمتة Excel: إنشاء دفتر عمل وإضافة ListBox باستخدام Aspose.Cells لـ .NET](/cells/english/net/automation-batch-processing/excel-automation-create-workbook-add-listbox-aspose-cells/)
- [أتمتة Excel: إنشاء دفتر عمل وإضافة ListBox باستخدام Aspose.Cells لـ .NET](/cells/german/net/automation-batch-processing/excel-automation-create-workbook-add-listbox-aspose-cells/)
- [أتمتة Excel: إنشاء دفتر عمل وإضافة ListBox باستخدام Aspose.Cells لـ .NET](/cells/french/net/automation-batch-processing/excel-automation-create-workbook-add-listbox-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}