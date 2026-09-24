---
category: general
date: 2026-03-27
description: كيفية ربط البيانات في C# باستخدام Aspose.Cells – تعلم حفظ المصنف كملف
  XLSX، إضافة مخطط، وتصدير Excel مع المخطط في دقائق.
draft: false
keywords:
- how to bind data
- save workbook as xlsx
- create excel workbook c#
- how to add chart
- export excel with chart
language: ar
og_description: كيفية ربط البيانات في C# باستخدام Aspose.Cells. يوضح لك هذا الدليل
  كيفية حفظ المصنف كملف XLSX، إضافة مخطط، وتصدير Excel مع المخطط.
og_title: كيفية ربط البيانات في C# – إنشاء مصنف إكسل
tags:
- Aspose.Cells
- C#
- Excel Automation
title: كيفية ربط البيانات في C# – إنشاء مصنف إكسل
url: /ar/net/excel-data-import-export/how-to-bind-data-in-c-create-excel-workbook/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية ربط البيانات في C# – إنشاء دفتر عمل Excel

هل تساءلت يومًا **كيف تربط البيانات** بمخطط في C# دون أن تشعر بالإحباط؟ لست وحدك. يواجه العديد من المطورين صعوبة عندما يحتاجون إلى إنشاء ملفات Excel برمجيًا تبدو فعليًا *مثل* تلك التي كانوا يبنونها يدويًا.  

في هذا الدرس سنستعرض مثالًا كاملًا وجاهزًا للتنفيذ يُنشئ دفتر عمل Excel، يملأه بالبيانات، يربط تلك البيانات بمخطط Waterfall، وأخيرًا يحفظ الملف بصيغة `.xlsx`. في النهاية ستعرف بالضبط كيف **تحفظ دفتر العمل كملف XLSX**، **كيف تضيف مخططًا** إلى ورقة العمل، وكيف **تصدّر Excel مع المخطط** للتقارير اللاحقة.

> **المتطلبات المسبقة** – تحتاج إلى Aspose.Cells for .NET (الإصدار التجريبي المجاني يكفي) وبيئة تطوير .NET مثل Visual Studio 2022. لا توجد حزم NuGet أخرى مطلوبة.

---

## ما يغطيه هذا الدليل

- **إنشاء دفتر عمل Excel C#** – إعداد `Workbook` جديد وورقة عمل.  
- **كيفية ربط البيانات** – ربط السلسلة الرقمية وعناوين الفئات بمصدر بيانات المخطط.  
- **كيفية إضافة مخطط** – إدراج مخطط Waterfall وتكوين عنوانه.  
- **حفظ دفتر العمل كملف XLSX** – حفظ الملف على القرص بحيث يمكن لأي شخص فتحه في Excel.  
- **تصدير Excel مع المخطط** – المنتج النهائي هو دفتر عمل كامل الوظائف يمكنك مشاركته.

إذا كنت مرتاحًا مع أساسيات صياغة C#، فستجد هذا سهلًا للغاية. لنبدأ.

---

## الخطوة 1: إنشاء دفتر عمل Excel في C#

أولًا، نحتاج إلى كائن دفتر عمل للعمل معه. فكر في فئة `Workbook` كدفتر ملاحظات فارغ ستملأه لاحقًا بالصفحات (أوراق العمل) والمحتوى.

```csharp
using Aspose.Cells;
using Aspose.Cells.Charts;

class WaterfallDemo
{
    static void Main()
    {
        // Initialize a new workbook – this is your blank Excel file.
        Workbook workbook = new Workbook();

        // Grab the first worksheet (index 0). It’s already created for us.
        Worksheet worksheet = workbook.Worksheets[0];
```

> **نصيحة احترافية:** إذا احتجت إلى عدة أوراق، ما عليك سوى استدعاء `workbook.Worksheets.Add()` والاحتفاظ بإشارة إلى كل `Worksheet` جديد.

---

## الخطوة 2: ملء ورقة العمل بالفئات والقيم

الآن سنقوم **بإنشاء بيانات على نمط excel workbook c#**. يستخدم المثال سيناريو Waterfall كلاسيكي: البداية، الإيرادات، التكلفة، الربح، والنهاية.  

```csharp
        // Add header labels.
        worksheet.Cells["A1"].PutValue("Category");
        worksheet.Cells["B1"].PutValue("Amount");

        // Sample data – you can replace these with your own source (database, API, etc.).
        string[] categoryLabels = { "Start", "Revenue", "Cost", "Profit", "End" };
        double[] values = { 0, 150, -70, 0, 80 };

        // Fill rows 2‑6 with the data.
        for (int i = 0; i < categoryLabels.Length; i++)
        {
            worksheet.Cells[i + 1, 0].PutValue(categoryLabels[i]); // Column A
            worksheet.Cells[i + 1, 1].PutValue(values[i]);       // Column B
        }
```

لماذا نضع `0` لـ “Start” و “Profit”؟ في مخطط Waterfall تعمل تلك الأصفار كـ *موصلات* تجعل التدفق البصري صحيحًا. إذا تخطيتها سيظهر المخطط معطوبًا.

---

## الخطوة 3: كيفية إضافة مخطط – إدراج مخطط Waterfall  

مع وجود البيانات، حان الوقت لـ **كيفية إضافة مخطط**. تجعل Aspose.Cells ذلك سهلًا كاستدعاء `Charts.Add`.  

```csharp
        // Insert a Waterfall chart starting at row 7, column 0 and spanning to row 25, column 10.
        int chartIndex = worksheet.Charts.Add(ChartType.Waterfall, 7, 0, 25, 10);
        Chart waterfallChart = worksheet.Charts[chartIndex];

        // Give the chart a meaningful title.
        waterfallChart.Title.Text = "Quarterly Waterfall";
```

الإحداثيات `(7,0,25,10)` تحدد الخلية العليا اليسرى والخلية السفلية اليمنى لمربع حدود المخطط. عدّلها لتناسب تخطيطك.

---

## الخطوة 4: كيفية ربط البيانات – ربط السلاسل والفئات  

هذا هو جوهر الدرس: **كيفية ربط البيانات** بالمخطط. طريقة `NSeries.Add` تأخذ نطاق قيم Y، بينما `CategoryData` تشير إلى تسميات المحور X.  

```csharp
        // Bind the numeric series (values) – the second parameter “true” tells Aspose to treat it as a series.
        waterfallChart.NSeries.Add("B2:B6", true);

        // Bind the category (X‑axis) labels.
        waterfallChart.NSeries.CategoryData = "A2:A6";
```

لاحظ أننا نشير إلى نفس الخلايا التي ملأناها سابقًا (`A2:A6` للفئات، `B2:B6` للمبالغ). إذا غيرت تخطيط البيانات، ما عليك سوى تحديث هذه النطاقات وفقًا لذلك.

---

## الخطوة 5: حفظ دفتر العمل كملف XLSX – تخزين الملف  

أخيرًا، نقوم **بحفظ دفتر العمل كملف XLSX**. طريقة `Save` تختار تلقائيًا الصيغة الصحيحة بناءً على امتداد الملف.  

```csharp
        // Save the workbook to disk. Replace YOUR_DIRECTORY with an actual path.
        workbook.Save("YOUR_DIRECTORY/WaterfallChart.xlsx");
    }
}
```

عند فتح `WaterfallChart.xlsx` في Excel سترى مخطط Waterfall مُصممًا بشكل جيد يعكس البيانات التي أدخلناها. بذلك يكتمل جزء **تصدير Excel مع المخطط**.

---

## النتيجة المتوقعة  

- **ملف Excel:** `WaterfallChart.xlsx` موجود في المجلد الذي حددته.  
- **تخطيط ورقة العمل:** العمود A يحتوي على الفئات، العمود B يحتوي على القيم، والمخطط يقع أسفل الجدول.  
- **مظهر المخطط:** مخطط Waterfall بعنوان “Quarterly Waterfall” مع خمسة أعمدة تمثل Start، Revenue، Cost، Profit، و End.  

![مثال على مخطط Waterfall لربط البيانات](waterfall_chart.png "مخطط Waterfall تم إنشاؤه بواسطة Aspose.Cells")

*يتضمن نص alt الصورة الكلمة المفتاحية الأساسية، مما يساعد في تحسين SEO والاقتباس بواسطة الذكاء الاصطناعي.*

---

## الأسئلة الشائعة والحالات الخاصة  

### ماذا لو كان مصدر البيانات ديناميكيًا؟  
استبدل المصفوفات الثابتة بحلقة تقرأ من قاعدة بيانات أو API. طالما أنك تكتب القيم إلى نفس نطاق الخلايا، يبقى كود الربط دون تغيير.

### هل يمكنني تغيير نوع المخطط؟  
بالطبع. استبدل `ChartType.Waterfall` بـ `ChartType.Column` أو `ChartType.Line` وغيرها. فقط تذكّر تعديل بيانات السلسلة إذا كان المخطط الجديد يتوقع ترتيبًا مختلفًا.

### كيف أضبط ألوان المخطط؟  
استخدم `waterfallChart.NSeries[0].Format.Fill.ForeColor = Color.Yellow;` (أو أي `System.Drawing.Color`). هذا مفيد عندما تريد إبراز عمود “Profit”.

### ماذا لو احتجت إلى تصدير إلى PDF بدلاً من XLSX؟  
استدعِ `workbook.Save("Report.pdf", SaveFormat.Pdf);`. سيتم عرض المخطط في ملف PDF تلقائيًا.

---

## نصائح لكتابة كود جاهز للإنتاج  

- **Dispose objects** – ضع `Workbook` داخل كتلة `using` إذا كنت تستخدم .NET Core لتحرير الموارد بسرعة.  
- **Path handling** – استخدم `Path.Combine(Environment.CurrentDirectory, "WaterfallChart.xlsx")` لتجنب كتابة الفواصل يدويًا.  
- **Error handling** – احرص على التقاط `Exception` حول `Save` لتظهر مشاكل الأذونات أو مساحة القرص مبكرًا.  
- **Version check** – قدم Aspose.Cells 23.10+ تحسينًا لدعم Waterfall؛ تأكد من أنك تستخدم نسخة حديثة للحصول على أفضل النتائج.

---

## الخلاصة  

أصبح لديك الآن مثال كامل من البداية إلى النهاية يوضح **كيفية ربط البيانات** في C#، **إنشاء دفتر عمل Excel C#**، **كيفية إضافة مخطط**، **حفظ دفتر العمل كملف xlsx**، و**تصدير Excel مع المخطط**. الكود جاهز للإدراج في أي مشروع .NET، والمفاهيم قابلة للتوسيع لمجموعات بيانات أكبر وأنواع مخططات مختلفة.

هل أنت مستعد للخطوة التالية؟ جرّب إضافة سلاسل متعددة، أو تجربة المخططات المتكدسة، أو أتمتة إنشاء التقارير الشهرية التي تُرسل بالبريد الإلكتروني إلى أصحاب المصلحة. السماء هي الحد عندما تتقن أساسيات أتمتة Excel باستخدام Aspose.Cells.

برمجة سعيدة، ولتظهر جداولك دائمًا بشكل مثالي!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}