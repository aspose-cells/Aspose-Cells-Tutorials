---
category: general
date: 2026-06-27
description: كيفية تنسيق أعمدة Excel في C# بألوان متناوبة. تعلم إنشاء دفتر عمل Excel
  باستخدام C#، استيراد DataTable إلى Excel، وتصديره كملف .xlsx.
draft: false
keywords:
- how to format excel columns
- create excel workbook c#
- import datatable to excel
- apply alternating column colors
- export datatable as xlsx
language: ar
og_description: كيفية تنسيق أعمدة Excel في C# بألوان متناوبة. اتبع هذا الدليل خطوة
  بخطوة لإنشاء دفتر عمل Excel باستخدام C#، استيراد DataTable، وتصديره كملف .xlsx.
og_title: كيفية تنسيق أعمدة Excel في C# – دليل شامل
schemas:
- author: Aspose
  dateModified: '2026-06-27'
  description: How to format Excel columns in C# with alternating colors. Learn to
    create Excel workbook C#, import DataTable to Excel, and export as .xlsx.
  headline: How to Format Excel Columns in C# – Complete Guide
  type: TechArticle
tags:
- C#
- Excel
- DataTable
title: كيفية تنسيق أعمدة Excel في C# – دليل شامل
url: /ar/net/formatting-rows-and-columns-in-excel/how-to-format-excel-columns-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيف تنسق أعمدة إكسل في C# – دليل شامل

هل تساءلت يومًا **كيف تنسق أعمدة إكسل** في C# دون أن تشعر بالإحباط؟ لست وحدك. سواء كنت تُخرج تقرير مبيعات أو تُفرغ قاعدة بيانات إلى جدول بيانات، فإن جعل تلك الأعمدة تبدو مرتبة يمكن أن يحدث الفارق بين “عادي” و “مميز”.

في هذا الدرس سنستعرض **مثالًا كاملاً قابلاً للتنفيذ** يوضح لك كيفية **إنشاء دفتر عمل إكسل C#**، **استيراد DataTable إلى إكسل**، و**تطبيق ألوان متناوبة على الأعمدة** بحيث يبرز كل عمود. في النهاية ستعرف أيضًا كيفية **تصدير DataTable كملف xlsx** بسطر واحد من الكود. لا إطالة، فقط كود عملي يمكنك نسخه‑ولصقه.

> **ما ستحتاجه**  
> - .NET 6 أو أحدث (أي نسخة حديثة تعمل)  
> - حزمة NuGet **Aspose.Cells** (أو أي حزمة مشابهة) – سنستخدمها لأنها مكتوبة بالكامل بـ C# ولا تحتاج إلى تثبيت إكسل.  
> - مصدر `DataTable` بسيط – سنولده مباشرةً لأغراض العرض.

هيا نبدأ.

![مثال على تنسيق أعمدة إكسل في C#](excel-columns.png "مثال على تنسيق أعمدة إكسل في C#")

## الخطوة 1: إنشاء دفتر عمل إكسل في C#  

أول شيء عليك فعله هو إنشاء دفتر عمل جديد. فكر فيه كدفتر ملاحظات جديد ستكتب فيه بياناتك لاحقًا.

```csharp
using Aspose.Cells;
using System;
using System.Data;
using System.Drawing;

class ExcelDemo
{
    static void Main()
    {
        // 1️⃣ Create a new workbook – this is the container for all sheets.
        Workbook workbook = new Workbook();

        // 2️⃣ Grab the first worksheet (index 0) – it’s already there.
        Worksheet worksheet = workbook.Worksheets[0];

        // The rest of the steps will fill this sheet with data and styling.
        // …
    }
}
```

**لماذا هذا مهم:** `Workbook` هو نقطة الدخول لكل عملية في إكسل. إن إنشاؤه **creates excel workbook c#** يعني أنك لا تحتاج إلى أي تفاعل COM، والكائن يبقى في الذاكرة بالكامل حتى تقرر حفظه.

> **نصيحة احترافية:** إذا كنت تستهدف بيئة خادم، فضلًا استخدم مكتبة لا تعتمد على تثبيت Microsoft Office. Aspose.Cells، EPPlus، أو ClosedXML كلها تلبي المتطلبات.

## الخطوة 2: إعداد الأنماط – تطبيق ألوان متناوبة على الأعمدة  

الآن يأتي الجزء الممتع: جعل كل عمود ثاني بلون مختلف. هذه الإشارة البصرية تساعد القارئ على مسح الجداول الكبيرة بسرعة.

```csharp
// Assume we already have a DataTable called dataTable (we’ll create it later).
int columnCount = dataTable.Columns.Count;

// Create an array to hold a style per column.
Style[] columnStyles = new Style[columnCount];

for (int i = 0; i < columnCount; i++)
{
    // Each column gets its own Style object.
    columnStyles[i] = workbook.CreateStyle();

    // Alternate between blue and green fonts.
    columnStyles[i].Font.Color = (i % 2 == 0) ? Color.Blue : Color.Green;

    // Optional: make the header bold for extra clarity.
    if (i == 0) // just an example, you could set this for all headers.
        columnStyles[i].Font.IsBold = true;
}
```

**ما الذي يحدث؟**  
- `workbook.CreateStyle()` يمنحنا لوحة نظيفة لكل عمود.  
- العبارة الشرطية `(i % 2 == 0) ? Color.Blue : Color.Green` هي جوهر **apply alternating column colors** – الأعمدة ذات الفهرس الزوجي تصبح زرقاء، والفردية تصبح خضراء.  
- يمكنك توسيع هذا الجزء لتعيين تعبئة خلفية، حدود، أو تنسيقات رقمية دون تغيير باقي الكود.

> **حالة حافة:** إذا كان جدولك يحتوي على أكثر من بضعة عشرات من الأعمدة، فإن إنشاء نمط لكل عمود قد يستهلك الذاكرة. في هذه الحالة، أعد استخدام كائنين نمط (blueStyle، greenStyle) وعيّنهما بناءً على فهرس العمود.

## الخطوة 3: بناء DataTable تجريبي (أو استخدم الخاص بك)  

لعرض مستقل سنولد `DataTable` يحتوي على بضع صفوف. في المشاريع الحقيقية ستستبدل `GetSampleData()` بمنطق جلب البيانات الفعلي الخاص بك.

```csharp
static DataTable GetSampleData()
{
    DataTable dt = new DataTable();

    // Define columns.
    dt.Columns.Add("ID", typeof(int));
    dt.Columns.Add("Name", typeof(string));
    dt.Columns.Add("Score", typeof(double));
    dt.Columns.Add("Date", typeof(DateTime));

    // Populate rows.
    for (int i = 1; i <= 5; i++)
    {
        dt.Rows.Add(i, $"Student {i}", 75 + i * 2, DateTime.Today.AddDays(-i));
    }

    return dt;
}
```

الآن اربط هذا بالتدفق الرئيسي:

```csharp
DataTable dataTable = GetSampleData();   // <-- import datatable to excel
```

## الخطوة 4: استيراد DataTable إلى ورقة العمل مع الأنماط  

Aspose.Cells تجعل عملية الاستيراد سطرًا واحدًا. التحميل الزائد (overload) الذي نستخدمه يسمح بتمرير مصفوفة الأنماط التي أنشأناها مسبقًا.

```csharp
// 0️⃣ Row and column offsets – start at A1 (0,0).
int startRow = 0;
int startColumn = 0;

// The 'true' flag tells the method that the first row in the DataTable
// contains column headers, which will be written to the sheet.
worksheet.Cells.ImportDataTable(dataTable, true, startRow, startColumn, columnStyles);
```

**لماذا نستخدم هذا التحميل الزائد؟**  
- يحترم صف العنوان، لذا لا تحتاج إلى كتابة أسماء الأعمدة يدويًا.  
- يطبق مصفوفة **columnStyles** عمودًا بعمود، مما يمنحنا الألوان المتناوبة دون حلقات إضافية.  
- سريع – الجدول كله يُحمَّل في الذاكرة بند واحد.

## الخطوة 5: حفظ دفتر العمل – تصدير DataTable كملف .xlsx  

أخيرًا، نقوم بحفظ دفتر العمل على القرص. هنا يحدث **export datatable as xlsx**.

```csharp
// Choose a folder that exists on your machine.
string outputPath = Path.Combine(Environment.CurrentDirectory, "output.xlsx");

// Save in the modern Office Open XML format.
workbook.Save(outputPath, SaveFormat.Xlsx);

Console.WriteLine($"Workbook saved to: {outputPath}");
```

عند فتح `output.xlsx` سترى:

| **المعرف** | **الاسم**      | **النتيجة** | **التاريخ**    |
|------------|----------------|-------------|----------------|
| *1* (أزرق) | *Student 1* (أخضر) | *77* (أزرق) | *2026‑06‑26* (أخضر) |
| *2* (أخضر) | *Student 2* (أزرق) | *79* (أخضر) | *2026‑06‑25* (أزرق) |
| …          | …              | …           | …              |

*خطوط زرقاء وخضراء تتناوب حسب العمود، تمامًا كما برمجنا.*

## الخطوة 6: المشكلات الشائعة وكيفية تجنبها  

| المشكلة | السبب | الحل |
|---------|-------|------|
| **عدم تطبيق الأنماط** | تمرير `null` أو مصفوفة بطول غير متطابق إلى `ImportDataTable`. | تأكد من أن `columnStyles.Length == dataTable.Columns.Count`. |
| **قفل الملف بعد الحفظ** | عملية أخرى (مثل إكسل) تفتح الملف. | أغلق أي عارضات قبل التشغيل، أو احفظ إلى مسار مؤقت ثم انقل الملف بعد ذلك. |
| **استهلاك الذاكرة مع جداول ضخمة** | إنشاء نمط لكل عمود لآلاف الأعمدة. | أعد استخدام نمطين فقط وعيّنهما بناءً على `(col % 2)`. |
| **تنسيق تاريخ خاطئ** | إكسل يفسر `DateTime` كرقم. | عيّن `columnStyles[i].Number = 14; // تنسيق تاريخ مدمج` للأعمدة التي تحتوي تواريخ. |

## الخطوة 7: الخطوات التالية – ما بعد التنسيق البسيط  

الآن بعد أن أتقنت **how to format Excel columns** بألوان متناوبة، يمكنك تجربة ما يلي:

- **التنسيق الشرطي** – إبراز الخلايا التي تلبي قواعد العمل.  
- **كائنات الجداول** – تحويل النطاق إلى Table في إكسل لتفعيل الفلاتر التلقائية.  
- **إنشاء المخططات** – تصور البيانات مباشرةً من دفتر العمل.  
- **تدفق تصدير كبير** – استخدم `SaveOptions` لكتابة ملفات ضخمة دون تحميل كل شيء في الذاكرة.

جميع هذه التقنيات تبنى على المفاهيم الأساسية التي غطيناها: إنشاء دفتر عمل، تنسيق الخلايا، استيراد البيانات، وحفظها.

---

### الخلاصة  

لقد تعلمت الآن **how to format Excel columns** في C# من البداية إلى النهاية: إنشاء دفتر عمل إكسل C#، تطبيق ألوان متناوبة على الأعمدة، استيراد DataTable إلى إكسل، وأخيرًا تصدير DataTable كملف .xlsx. الكود الكامل القابل للنسخ‑واللصق أعلاه يعمل مباشرةً، والشروحات توضح “لماذا” وراء كل سطر.

لا تتردد في تعديل الألوان، إضافة حدود، أو الانتقال إلى مكتبة أخرى إذا رغبت. النمط يبقى نفسه، والنتيجة دائمًا جدول بيانات نظيف واحترافي جاهز لأصحاب المصلحة.

هل لديك أسئلة أو تريد مشاركة حيلك في التنسيق؟ اترك تعليقًا أدناه ولنستمر في النقاش. برمجة سعيدة!

## ماذا تتعلم بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مصدر يتضمن أمثلة كود كاملة مع شروحات خطوة‑بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف نهج تنفيذ بديلة في مشاريعك.

- [How to Import DataTable into Excel Using Aspose.Cells for .NET (Step-by-Step Guide)](/cells/english/net/import-export/import-datatable-excel-aspose-cells-net/)
- [How to Create and Configure Excel Workbooks with Aspose.Cells .NET&#58; A Step-by-Step Guide](/cells/english/net/getting-started/create-configure-excel-workbook-aspose-cells-net/)
- [How to Create and Style Excel Tables Using Aspose.Cells for .NET | Step‑By‑Step Guide](/cells/english/net/tables-structured-references/aspose-cells-net-excel-tables-styling/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}