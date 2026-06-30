---
category: general
date: 2026-06-30
description: إنشاء تنسيق شرطي في مصنف Excel باستخدام Aspose.Cells. تعلم كيفية ضبط
  خلفية الخلية، ترتيب الخلايا، وإنشاء الملف برمجيًا.
draft: false
keywords:
- create conditional formatting
- create excel workbook
- set cell background
- how to rank cells
- how to use aspose
language: ar
og_description: إنشاء تنسيق شرطي في مصنف Excel باستخدام Aspose.Cells. اتبع هذا الدرس
  الكامل لتعيين خلفية الخلية، ترتيب الخلايا، وأتمتة Excel.
og_title: إنشاء تنسيق شرطي في إكسل باستخدام Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Create conditional formatting in an Excel workbook using Aspose.Cells.
    Learn how to set cell background, rank cells, and build the file programmatically.
  headline: Create Conditional Formatting in Excel with Aspose.Cells – Step‑by‑Step
    Guide
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
title: إنشاء تنسيق شرطي في إكسل باستخدام Aspose.Cells – دليل خطوة بخطوة
url: /ar/net/excel-conditional-formatting/create-conditional-formatting-in-excel-with-aspose-cells-ste/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء تنسيق شرطي في Excel باستخدام Aspose.Cells – دليل خطوة بخطوة

هل تساءلت يومًا كيف يمكنك **إنشاء تنسيق شرطي** في ملف Excel دون فتح الواجهة؟ لست وحدك. يحتاج العديد من المطورين إلى **إنشاء مصنف Excel** بشكل سريع، وإن القيام بذلك برمجيًا يوفر ساعات من العمل اليدوي. في هذا الدرس سنوضح لك بالضبط كيف **إنشاء تنسيق شرطي**، وتنسيق الخلايا، وحتى ترتيب القيم العليا—كل ذلك باستخدام مكتبة Aspose.Cells القوية لـ .NET.

سنستعرض مثالًا واقعيًا: إنشاء ورقة درجات، تمييز الدرجات العالية باللون الأخضر الفاتح، ووضع خلفية ذهبية لأفضل 3 مشاركين. في النهاية ستعرف **كيفية تعيين خلفية الخلية**، **كيفية ترتيب الخلايا**، و**كيفية استخدام Aspose** لأتمتة Excel المتقدمة. لا إطالة، مجرد حل كامل قابل للتنفيذ يمكنك إدراجه في أي مشروع C#.

## ما ستتعلمه

- كيف **إنشاء مصنف Excel** باستخدام Aspose.Cells  
- كيف تعبئة نطاق ببيانات عشوائية (درجات)  
- كيف **تعيين خلفية الخلية** بألوان صلبة  
- كيف تطبيق قاعدة مبنية على صيغة لـ **ترتيب الخلايا** وتظليل الثلاثة الأفضل  
- كيف حفظ النتيجة كملف .xlsx  

المتطلبات المسبقة: .NET 6+ (أو .NET Framework 4.6+)، Visual Studio (أو أي بيئة تطوير C#)، وإشارة إلى حزمة Aspose.Cells عبر NuGet. إذا لم تستخدم Aspose من قبل، لا تقلق—سنغطي **كيفية استخدام Aspose** من الصفر.

---

![Create conditional formatting example](https://example.com/images/create-conditional-formatting.png "لقطة شاشة تُظهر التنسيق الشرطي في ملف Excel المُولد")

*نص بديل للصورة: مثال على إنشاء تنسيق شرطي في مصنف Excel تم إنشاؤه باستخدام Aspose.Cells.*

## كيفية إنشاء مصنف Excel باستخدام Aspose.Cells

أولاً وقبل كل شيء: تحتاج إلى كائن مصنف للعمل معه. تجعل Aspose.Cells هذا الأمر سطرًا واحدًا.

```csharp
using Aspose.Cells;
using System.Drawing;

void CreateConditionalFormattingWorkbook()
{
    // Step 1: Instantiate a new workbook and give the first sheet a friendly name
    Workbook workbook = new Workbook();                 // creates an empty workbook
    Worksheet sheet = workbook.Worksheets[0];           // grab the default worksheet
    sheet.Name = "Scores";                              // rename it to something meaningful
```

لماذا نعيد تسمية الورقة؟ اسم واضح (مثل **Scores**) يجعل من السهل الإشارة إليه لاحقًا، خاصةً عندما تشارك الملف مع مستخدمين غير تقنيين.  

الآن بعد أن تم إنشاء المصنف، دعنا نملأ العمود A بالدرجات العشوائية.

## كيفية ملء البيانات – إنشاء درجات عشوائية

```csharp
    // Step 2: Populate A2:A21 with random values between 40 and 99
    Random random = new Random();
    for (int i = 0; i < 20; i++)               // 20 rows of data
    {
        sheet.Cells[i + 1, 0].PutValue(random.Next(40, 100));
    }
```

ملاحظة سريعة: `PutValue` يكتشف نوع البيانات تلقائيًا، لذا لا تحتاج إلى تحويل إلى `int`. يبدأ الحلقة عند `i = 0` ولكنها تكتب إلى الصف `i + 1` لأن صفوف Excel تبدأ من 1 بينما مجموعة `Cells` تبدأ من 0.

## كيفية تعيين خلفية الخلية للدرجات العالية

الآن سنقوم **بإنشاء تنسيق شرطي** يلون أي درجة ≥ 80 بظل أخضر فاتح.

```csharp
    // Step 3: Define a conditional formatting range (A2:A21)
    int firstRow = 1, lastRow = 20;                     // zero‑based indices for rows 2‑21
    int cfIndex = sheet.ConditionalFormattings.Add(firstRow, 0, lastRow, 0);
    ConditionalFormatting cf = sheet.ConditionalFormattings[cfIndex];

    // Add a rule: cell value >= 80 → light‑green background
    FormatCondition highScoreCondition = cf.AddCondition(
        FormatConditionType.CellValue,
        OperatorType.GreaterOrEqual,
        "80");

    highScoreCondition.Style.ForegroundColor = Color.LightGreen;
    highScoreCondition.Style.Pattern = BackgroundType.Solid;
```

خاصية `ForegroundColor` تتحكم في لون التعبئة، بينما `Pattern = BackgroundType.Solid` تخبر Excel باستخدام تعبئة صلبة بدلاً من تدرج أو نمط. هذا هو جوهر **كيفية تعيين خلفية الخلية** بناءً على حد رقمي.

## كيفية ترتيب الخلايا وتظليل الثلاثة الأوائل

الترتيب أصعب قليلاً لأننا نحتاج إلى صيغة تقيم كل خلية مقابل النطاق الكامل. تسمح لك Aspose.Cells باستخدام نفس صيغة Excel التي تكتبها في الواجهة.

```csharp
    // Step 4: Add a formula‑based rule to color the top‑3 scores gold
    FormatCondition topThreeCondition = cf.AddCondition(
        FormatConditionType.Formula,
        null,
        null);

    // The formula uses the RANK function; note the absolute references ($) lock the range
    topThreeCondition.Formula1 = "=RANK(A2,$A$2:$A$21)<=3";

    topThreeCondition.Style.ForegroundColor = Color.Gold;
    topThreeCondition.Style.Pattern = BackgroundType.Solid;
```

لماذا `A2` في الصيغة؟ تقوم Aspose بتقييم الصيغة بالنسبة لكل خلية في النطاق، لذا يتحول `A2` تلقائيًا إلى `A3`، `A4`، إلخ، عندما تُطبق القاعدة صفًا بصف. تُعيد الدالة `RANK` موضع القيمة داخل النطاق المحدد، والجزء `<=3` يضمن أن الثلاث درجات الأعلى فقط ستحصل على تعبئة ذهبية.

## كيفية حفظ المصنف

```csharp
    // Step 5: Persist the workbook to disk
    workbook.Save("YOUR_DIRECTORY/Scores_ConditionalFormatting.xlsx");
}
```

استبدل `YOUR_DIRECTORY` بمسار مطلق أو نسبي يمكن لتطبيقك الكتابة إليه. بعد تشغيل الطريقة، افتح الملف في Excel وسترى:

- خلايا خضراء فاتحة لأي درجة ≥ 80  
- خلايا ذهبية لأعلى ثلاث درجات، بغض النظر عما إذا كانت أيضًا ≥ 80  

هذه هي سلسلة **إنشاء تنسيق شرطي** الكاملة.

---

## مثال كامل قابل للتنفيذ

إليك الطريقة بالكامل مرة أخرى، جاهزة للنسخ واللصق في تطبيق console أو أي فئة C#:

```csharp
using Aspose.Cells;
using System.Drawing;

void CreateConditionalFormattingWorkbook()
{
    // Step 1: Create a new workbook and name the first worksheet
    Workbook workbook = new Workbook();
    Worksheet sheet = workbook.Worksheets[0];
    sheet.Name = "Scores";

    // Step 2: Fill column A (A2:A21) with random scores between 40 and 99
    Random random = new Random();
    for (int i = 0; i < 20; i++)
    {
        sheet.Cells[i + 1, 0].PutValue(random.Next(40, 100));
    }

    // Step 3: Highlight scores >= 80 with a light‑green background
    int firstRow = 1, lastRow = 20;
    int cfIndex = sheet.ConditionalFormattings.Add(firstRow, 0, lastRow, 0);
    ConditionalFormatting cf = sheet.ConditionalFormattings[cfIndex];
    FormatCondition highScoreCondition = cf.AddCondition(
        FormatConditionType.CellValue,
        OperatorType.GreaterOrEqual,
        "80");
    highScoreCondition.Style.ForegroundColor = Color.LightGreen;
    highScoreCondition.Style.Pattern = BackgroundType.Solid;

    // Step 4: Color the top‑3 scores with a gold background using a formula rule
    FormatCondition topThreeCondition = cf.AddCondition(
        FormatConditionType.Formula,
        null,
        null);
    topThreeCondition.Formula1 = "=RANK(A2,$A$2:$A$21)<=3";
    topThreeCondition.Style.ForegroundColor = Color.Gold;
    topThreeCondition.Style.Pattern = BackgroundType.Solid;

    // Step 5: Save the workbook
    workbook.Save("YOUR_DIRECTORY/Scores_ConditionalFormatting.xlsx");
}
```

### النتيجة المتوقعة

عند فتح `Scores_ConditionalFormatting.xlsx`:

- الخلايا التي قيمتها **80** أو أعلى تضيء باللون الأخضر الفاتح.  
- أعلى ثلاثة أرقام (حتى وإن كانت أقل من 80) تظهر بخلفية **ذهبية**.  
- جميع الخلايا الأخرى تحتفظ بخلفية بيضاء افتراضية.

هذه الإشارة البصرية تخبر المدير فورًا من هم أفضل الأداءات، دون أي فرز يدوي.

---

## أسئلة شائعة وحالات خاصة

**ماذا لو احتجت إلى أكثر من ثلاث درجات أعلى؟**  
فقط غيّر الجزء `<=3` في الصيغة إلى `<=5` (أو أي عدد تريده). ستتكيف القاعدة تلقائيًا.

**هل يمكنني تطبيق نطاقات تنسيق متعددة؟**  
بالطبع. استدعِ `sheet.ConditionalFormattings.Add` مرة أخرى بنطاق مختلف، ثم أضف الشروط إلى كائن `ConditionalFormatting` الجديد.

**ماذا عن إصدارات Excel القديمة؟**  
تحفظ Aspose.Cells بالصيغة الحديثة `.xlsx` بشكل افتراضي، وهي متوافقة مع Excel 2007 وما بعده. إذا كنت تحتاج إلى `.xls`، مرّر `SaveFormat.Excel97To2003` إلى طريقة `Save`.

**هل هناك تأثير على الأداء للأوراق الكبيرة؟**  
يتم تخزين التنسيق الشرطي كبيانات وصفية، لذا لا يؤثر بشكل كبير على حجم الملف. ومع ذلك، قد يزيد توليد مئات الآلاف من الصفوف من استهلاك الذاكرة—فكر في المعالجة على دفعات.

---

## الخطوات التالية

الآن بعد أن أتقنت **كيفية إنشاء تنسيق شرطي**، قد ترغب في استكشاف:

- **كيفية إنشاء مخططات Excel** برمجيًا (ميزة أخرى في Aspose.Cells)  
- **كيفية تعيين خلفية الخلية** بناءً على قيم نصية (مثل “Pass/Fail”)  
- **كيفية استخدام Aspose.Cells للتحقق من صحة البيانات** والقوائم المنسدلة  

كل من هذه المواضيع يبني على الأساسيات نفسها التي تعلمتها للتو، لذا ستشعر بالراحة.

---

## الخلاصة

لقد استعرضنا للتو مثالًا كاملاً من البداية إلى النهاية حول كيفية **إنشاء تنسيق شرطي** في مصنف Excel باستخدام Aspose.Cells. من تهيئة المصنف، ملء البيانات، **تعيين خلفية الخلية**، ترتيب أفضل الأداءات، وحتى حفظ الملف، تم تغطية كل خطوة مع التركيز على **كيفية ترتيب الخلايا** و**كيفية استخدام Aspose**.  

جرّب الكود، عدّل الحدود، وشاهد مدى السرعة التي يمكنك بها إنشاء تقارير مصقولة لأي سيناريو تجاري. هل لديك تعديل ترغب في مشاركته؟ اترك تعليقًا أدناه—برمجة سعيدة!

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة شفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [أتمتة تنسيق شرطي في Excel باستخدام Aspose.Cells للـ Java: دليل كامل](/cells/english/java/formatting/automate-conditional-formatting-excel-aspose-cells-java/)
- [كيفية إنشاء وتنسيق خلايا Excel باستخدام Aspose.Cells للـ Java: دليل خطوة بخطوة](/cells/english/java/formatting/aspose-cells-java-excel-automation-guide/)
- [إنشاء مصنف Excel باستخدام Aspose.Cells في Java: دليل خطوة بخطوة](/cells/english/java/getting-started/create-excel-workbook-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}