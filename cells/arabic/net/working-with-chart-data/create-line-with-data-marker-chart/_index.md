---
"description": "تعرّف على كيفية إنشاء مخطط خطي بعلامات بيانات في Excel باستخدام Aspose.Cells لـ .NET. اتبع هذا الدليل خطوة بخطوة لإنشاء المخططات وتخصيصها بسهولة."
"linktitle": "إنشاء خط باستخدام مخطط علامة البيانات"
"second_title": "واجهة برمجة تطبيقات معالجة Excel Aspose.Cells .NET"
"title": "إنشاء خط باستخدام مخطط علامة البيانات"
"url": "/ar/net/working-with-chart-data/create-line-with-data-marker-chart/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء خط باستخدام مخطط علامة البيانات

## مقدمة

هل تساءلت يومًا عن كيفية إنشاء مخططات بيانية مذهلة في Excel برمجيًا؟ حسنًا، استعد، لأننا اليوم سنتعمق في إنشاء مخطط بياني بخط مع علامة بيانات باستخدام Aspose.Cells لـ .NET. سيرشدك هذا البرنامج التعليمي خلال كل خطوة، مما يضمن لك فهمًا متينًا لإنشاء المخططات البيانية، حتى لو كنت قد بدأت للتو في استخدام Aspose.Cells.

## المتطلبات الأساسية

قبل أن نبدأ، تأكد من أن كل شيء جاهز لمتابعتك بسلاسة.

1. مكتبة Aspose.Cells لـ .NET - ستحتاج إلى تثبيتها. يمكنك تنزيلها. [هنا](https://releases.aspose.com/cells/net/).
2. .NET Framework – تأكد من إعداد بيئة التطوير الخاصة بك باستخدام أحدث إصدار من .NET.
3. يُنصح باستخدام IDE (بيئة التطوير المتكاملة) – Visual Studio.
4. ترخيص Aspose.Cells صالح - إذا لم يكن لديك ترخيص، يمكنك طلب ترخيص [رخصة مؤقتة](https://purchase.aspose.com/temporary-license/) أو تحقق من ذلك [نسخة تجريبية مجانية](https://releases.aspose.com/).

هل أنت مستعد للانطلاق؟ لنبدأ بشرح الأمر!

## استيراد الحزم الضرورية

للبدء، تأكد من استيراد مساحات الأسماء التالية إلى مشروعك. ستوفر هذه المساحات الفئات والطرق اللازمة لإنشاء مخططك.

```csharp
using System;
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Charts;
using System.Drawing;
```

بمجرد حصولك على ذلك، يمكننا البدء في الترميز!

## الخطوة 1: إعداد المصنف وورقة العمل الخاصة بك

أولاً وقبل كل شيء، عليك إنشاء مصنف جديد والوصول إلى ورقة العمل الأولى.

```csharp
//دليل الإخراج
static string outputDir = "Your Document Directory";
		
// إنشاء مصنف
Workbook workbook = new Workbook();

// الوصول إلى ورقة العمل الأولى
Worksheet worksheet = workbook.Worksheets[0];
```

اعتبر مصنف العمل كملف إكسل، وورقة العمل هي الورقة المحددة فيه. في هذه الحالة، نعمل على الورقة الأولى.

## الخطوة 2: ملء ورقة العمل بالبيانات

الآن وقد أصبحت لدينا ورقة العمل، فلنملأها ببعض البيانات. سننشئ نقاط بيانات عشوائية لسلسلتين من القيم.

```csharp
// تعيين عنوان الأعمدة
worksheet.Cells[0, 0].Value = "X";
worksheet.Cells[0, 1].Value = "Y";

// بيانات عشوائية لتوليد الرسم البياني
Random R = new Random();

// إنشاء بيانات عشوائية وحفظها في الخلايا
for (int i = 1; i < 21; i++)
{
    worksheet.Cells[i, 0].Value = i;
    worksheet.Cells[i, 1].Value = 0.8;
}

for (int i = 21; i < 41; i++)
{
    worksheet.Cells[i, 0].Value = i - 20;
    worksheet.Cells[i, 1].Value = 0.9;
}
```

هنا، نستخدم أرقامًا عشوائية لمحاكاة البيانات، ولكن في التطبيقات الواقعية، يمكنك ملؤها بالقيم الفعلية من مجموعة البيانات الخاصة بك.

## الخطوة 3: إضافة الرسم البياني إلى ورقة العمل

بعد ذلك، نضيف الرسم البياني إلى ورقة العمل ونختار النوع - في هذه الحالة، الرسم البياني الخطي مع علامات البيانات.

```csharp
// إضافة مخطط إلى ورقة العمل
int idx = worksheet.Charts.Add(ChartType.LineWithDataMarkers, 1, 3, 20, 20);

// الوصول إلى الرسم البياني الذي تم إنشاؤه حديثًا
Chart chart = worksheet.Charts[idx];
```

يضيف هذا المقطع مخططًا خطيًا مع علامات بيانات إلى ورقة العمل، ويضعه ضمن نطاق محدد (من ١،٣ إلى ٢٠،٢٠). بسيط جدًا، أليس كذلك؟

## الخطوة 4: تخصيص مظهر الرسم البياني

بعد إنشاء الرسم البياني، يمكنك تصميمه حسب رغبتك. لنُغيّر الخلفية والعنوان ونمط الرسم البياني.

```csharp
// تعيين نمط الرسم البياني
chart.Style = 3;

// تعيين قيمة التوسع التلقائي إلى true
chart.AutoScaling = true;

// تعيين لون المقدمة إلى الأبيض
chart.PlotArea.Area.ForegroundColor = Color.White;

// تعيين خصائص عنوان الرسم البياني
chart.Title.Text = "Sample Chart";

// تعيين نوع الرسم البياني
chart.Type = ChartType.LineWithDataMarkers;
```

هنا، نقوم بإضفاء مظهر نظيف على الرسم البياني من خلال تعيين خلفية بيضاء، وضبط الحجم تلقائيًا، وإعطائه عنوانًا ذا معنى.

## الخطوة 5: تحديد السلسلة ورسم نقاط البيانات

الآن بعد أن أصبح الرسم البياني الخاص بنا يبدو جيدًا، نحتاج إلى تحديد سلسلة البيانات التي سيتم رسمها.

```csharp
// تعيين خصائص عنوان محور الفئة
chart.CategoryAxis.Title.Text = "Units";

// تعريف سلسلتين للرسم البياني
int s2_idx = chart.NSeries.Add("A2: A21", true);
int s3_idx = chart.NSeries.Add("A22: A41", true);
```

تتوافق هذه السلسلة مع نطاقات نقاط البيانات التي قمنا بملئها سابقًا.

## الخطوة 6: إضافة الألوان وتخصيص علامات السلسلة

دعونا نجعل هذا الرسم البياني أكثر جاذبية من خلال إضافة ألوان مخصصة إلى علامات البيانات الخاصة بنا.

```csharp
// تخصيص السلسلة الأولى
chart.NSeries[s2_idx].Marker.Area.ForegroundColor = Color.Yellow;
chart.NSeries[s2_idx].Marker.Border.IsVisible = false;

// تخصيص السلسلة الثانية
chart.NSeries[s3_idx].Marker.Area.ForegroundColor = Color.Green;
chart.NSeries[s3_idx].Marker.Border.IsVisible = false;
```

من خلال تخصيص الألوان، يمكنك جعل الرسم البياني ليس عمليًا فحسب، بل وجذابًا بصريًا أيضًا!

## الخطوة 7: تعيين قيم X وY لكل سلسلة

وأخيرًا، دعنا نخصص قيم X وY لكل سلسلة من سلاسلنا.

```csharp
// تعيين قيم X وY للسلسلة الأولى
chart.NSeries[s2_idx].XValues = "A2: A21";
chart.NSeries[s2_idx].Values = "B2: B21";

// تعيين قيم X وY للسلسلة الثانية
chart.NSeries[s3_idx].XValues = "A22: A41";
chart.NSeries[s3_idx].Values = "B22: B41";
```

تعتمد القيم على البيانات التي قمنا بملئها في الخطوة 2.

## الخطوة 8: حفظ المصنف

الآن بعد أن أصبح كل شيء جاهزًا، فلنحفظ المصنف حتى نتمكن من رؤية الرسم البياني أثناء العمل.

```csharp
// حفظ المصنف
workbook.Save(outputDir + @"LineWithDataMarkerChart.xlsx", Aspose.Cells.SaveFormat.Xlsx);
```

وهذا كل شيء! لقد أنشأتَ للتو مخططًا خطيًا بعلامات بيانات باستخدام Aspose.Cells لـ .NET.

## خاتمة

قد يبدو إنشاء المخططات برمجيًا في Excel أمرًا شاقًا، ولكن مع Aspose.Cells لـ .NET، يصبح الأمر سهلًا للغاية، إذ يكفي اتباع التعليمات خطوة بخطوة. من إعداد مصنفك إلى تخصيص مظهر المخطط، تتولى هذه المكتبة القوية كل ذلك. سواء كنت تُنشئ تقارير أو لوحات معلومات أو عروضًا بيانية للبيانات، تُمكّنك Aspose.Cells من القيام بذلك بسهولة.

## الأسئلة الشائعة

### هل يمكنني تخصيص الرسم البياني بشكل أكبر؟  
بالتأكيد! يوفر Aspose.Cells خيارات تخصيص متعددة، من الخطوط إلى خطوط الشبكة، وغيرها.

### هل أحتاج إلى ترخيص لاستخدام Aspose.Cells؟  
نعم، يلزم الحصول على ترخيص للاستفادة الكاملة من الميزات. يمكنك الحصول على ترخيص [رخصة مؤقتة](https://purchase.aspose.com/temporary-license/) أو ابدأ بـ [نسخة تجريبية مجانية](https://releases.aspose.com/).

### كيف يمكنني إضافة المزيد من سلاسل البيانات؟  
فقط قم بإضافة سلسلة إضافية باستخدام `NSeries.Add` الطريقة، تحديد نطاقات الخلايا للبيانات الجديدة.

### هل يمكنني تصدير الرسم البياني كصورة؟  
نعم، يمكنك تصدير المخططات البيانية مباشرة كصور باستخدام `Chart.ToImage` طريقة.

### هل يدعم Aspose.Cells المخططات ثلاثية الأبعاد؟  
نعم، يدعم Aspose.Cells مجموعة واسعة من أنواع المخططات، بما في ذلك المخططات ثلاثية الأبعاد.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}