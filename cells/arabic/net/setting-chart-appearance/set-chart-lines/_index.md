---
title: تعيين خطوط الرسم البياني
linktitle: تعيين خطوط الرسم البياني
second_title: واجهة برمجة تطبيقات معالجة Excel الخاصة بـ Aspose.Cells .NET
description: تعرف على كيفية تخصيص خطوط الرسم البياني في Excel باستخدام Aspose.Cells for .NET من خلال دليلنا المفصل خطوة بخطوة.
weight: 14
url: /ar/net/setting-chart-appearance/set-chart-lines/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تعيين خطوط الرسم البياني

## مقدمة

إن إنشاء مخططات جذابة بصريًا وغنية بالمعلومات أمر ضروري لتمثيل البيانات. سواء كنت محلل بيانات أو مدير أعمال أو مجرد شخص يحب تنظيم البيانات، فإن المخططات البيانية يمكن أن تعزز بشكل كبير الطريقة التي تعرض بها معلوماتك. سيرشدك هذا البرنامج التعليمي خلال عملية تعيين خطوط المخططات البيانية باستخدام Aspose.Cells for .NET، وهي مكتبة قوية للتعامل مع ملفات Excel. في النهاية، ستعرف كيفية إنشاء مخططات بيانية مذهلة مليئة بالتخصيصات لجعل بيانات Excel الخاصة بك بارزة!

## المتطلبات الأساسية

قبل الغوص في جزء الترميز، تأكد من أنك مجهز بما يلي:

- Visual Studio: تأكد من تثبيت Visual Studio. يوصى بشدة باستخدام أحدث إصدار للاستفادة من كافة الميزات.
- .NET Framework: يجب أن يعتمد مشروعك على .NET Framework (أو .NET Core) حيث ستنفذ Aspose.Cells.
-  Aspose.Cells لـ .NET: قم بتنزيل Aspose.Cells وتثبيته من[موقع اسبوس](https://releases.aspose.com/cells/net/).
- الفهم الأساسي للغة البرمجة C#: سيكون التعرف على لغة البرمجة C# مفيدًا أثناء الترميز.

## استيراد الحزم

للبدء في استخدام Aspose.Cells، ستحتاج إلى استيراد المساحات الأساسية اللازمة إلى مشروعك. سيتيح لك هذا الوصول إلى جميع الميزات والوظائف الرائعة التي يوفرها Aspose.Cells. إليك كيفية استيراد الحزم في ملف C# الخاص بك:

```csharp
using Aspose.Cells;
using Aspose.Cells.Charts;
using System.Drawing;
```

دعونا نقسم العملية إلى خطوات قابلة للإدارة حتى تتمكن من متابعتها بسهولة.

## الخطوة 1: قم بتحديد دليل الإخراج الخاص بك

أولاً وقبل كل شيء، ستحتاج إلى مكان لحفظ ملف Excel الذي أنشأته حديثًا. حدد دليل الإخراج في أعلى الكود الخاص بك على النحو التالي:

```csharp
// دليل الإخراج
string outputDir = "Your Output Directory";
```

 الشرح: استبدل "دليل الإخراج الخاص بك" بالمسار الذي تريد أن يحفظ فيه Aspose.Cells الملف، مثل`C:\\MyExcelFiles\\`.

## الخطوة 2: إنشاء مثيل لكائن مصنف

الآن، سنقوم بإنشاء كائن مصنف، والذي سيكون بمثابة حاوية لجدول البيانات الخاص بك.

```csharp
// إنشاء كائن مصنف
Workbook workbook = new Workbook();
```

 الشرح: هذا السطر ينشئ مثيلًا لـ`Workbook`من مكتبة Aspose.Cells. الأمر أشبه بفتح ملف Excel فارغ جديد حيث يمكنك البدء في إضافة أوراقك وبياناتك.

## الخطوة 3: الرجوع إلى ورقة العمل

بعد ذلك، ستحتاج إلى العمل على ورقة عمل محددة في المصنف الخاص بك. سنأخذ ورقة العمل الأولى.

```csharp
// الحصول على مرجع ورقة العمل المضافة حديثًا عن طريق تمرير فهرس الورقة الخاصة بها
Worksheet worksheet = workbook.Worksheets[0];
```

 الشرح: يتم فهرسة أوراق العمل بدءًا من 0، لذا`worksheets[0]` يشير إلى ورقة العمل الأولى.

## الخطوة 4: إضافة قيم العينة إلى الخلايا

دعونا نملأ بعض الخلايا بالبيانات التي سنستخدمها لاحقًا لإنشاء مخططنا.

```csharp
// إضافة قيم العينة إلى الخلايا
worksheet.Cells["A1"].PutValue(50);
worksheet.Cells["A2"].PutValue(100);
worksheet.Cells["A3"].PutValue(150);
worksheet.Cells["B1"].PutValue(60);
worksheet.Cells["B2"].PutValue(32);
worksheet.Cells["B3"].PutValue(50);
```

الشرح: هنا نقوم بملء الخلايا "A1" إلى "A3" و"B1" إلى "B3" ببعض القيم الرقمية. سيتم رسم هذه القيم في مخططنا لاحقًا.

## الخطوة 5: إضافة مخطط إلى ورقة العمل

الآن حان الوقت لإنشاء مخطط! سنضيف نوعًا من المخطط العمودي.

```csharp
// إضافة مخطط إلى ورقة العمل
int chartIndex = worksheet.Charts.Add(Aspose.Cells.Charts.ChartType.Column, 5, 0, 25, 10);
```

الشرح: يضيف هذا الخط مخططًا عموديًا عند إحداثيات محددة في ورقة العمل. تحدد المعلمات المكان الذي سيتم فيه رسم المخطط على الشبكة.

## الخطوة 6: الوصول إلى الرسم البياني المُضاف حديثًا

أنت الآن بحاجة إلى الرجوع إلى الرسم البياني الذي قمت بإنشائه للتو.

```csharp
// الوصول إلى مثيل الرسم البياني المضاف حديثًا
Aspose.Cells.Charts.Chart chart = worksheet.Charts[chartIndex];
```

الشرح: يتيح لك هذا التحكم في مثيل الرسم البياني مما يسمح لك بتخصيصه وتصميمه بشكل أكبر.

## الخطوة 7: إضافة سلسلة البيانات إلى الرسم البياني

دعونا نضيف سلسلة البيانات إلى مخططنا.

```csharp
// إضافة SeriesCollection (مصدر بيانات الرسم البياني) إلى الرسم البياني الذي يتراوح من الخلية "A1" إلى "B3"
chart.NSeries.Add("A1:B3", true);
```

الشرح: يوجه هذا السطر الرسم البياني لسحب البيانات من النطاق المحدد. يحدد المعلمة الثانية ما إذا كانت نطاقات البيانات تتضمن فئات أم لا.

## الخطوة 8: تخصيص مظهر الرسم البياني

الآن حان الوقت للجزء الممتع - تخصيص الرسم البياني الخاص بك! دعنا نغير بعض الألوان.

```csharp
// ضبط لون المقدمة لمنطقة الرسم البياني
chart.PlotArea.Area.ForegroundColor = Color.Blue;

// ضبط لون المقدمة لمنطقة الرسم البياني
chart.ChartArea.Area.ForegroundColor = Color.Yellow;

// ضبط لون المقدمة لمنطقة المجموعة من السلسلة الأولى
chart.NSeries[0].Area.ForegroundColor = Color.Red;

// ضبط لون المقدمة لمنطقة نقطة المجموعة من السلسلة الأولى
chart.NSeries[0].Points[0].Area.ForegroundColor = Color.Cyan;

// ملء منطقة المجموعة من السلسلة الثانية بتدرج لوني
chart.NSeries[1].Area.FillFormat.SetOneColorGradient(Color.Lime, 1, Aspose.Cells.Drawing.GradientStyleType.Horizontal, 1);
```

الشرح: هنا، تقوم بتخصيص ألوان المكونات المختلفة للرسم البياني لجعله جذابًا بصريًا. يستهدف كل سطر مناطق مختلفة من الرسم البياني.

## الخطوة 9: تطبيق أنماط الخطوط

بعد ذلك، يمكنك تعديل أنماط الخطوط لسلسلة البيانات الخاصة بك لجعل الرسم البياني الخاص بك ليس جميلًا فحسب، بل احترافيًا أيضًا.

```csharp
// تطبيق نمط الخط المنقط على أسطر SeriesCollection
chart.NSeries[0].Border.Style = Aspose.Cells.Drawing.LineType.Dot;

// تطبيق نمط علامة مثلثة على علامات البيانات لمجموعة SeriesCollection
chart.NSeries[0].Marker.MarkerStyle = Aspose.Cells.Charts.ChartMarkerType.Triangle;

// تعيين وزن جميع الأسطر في SeriesCollection إلى متوسط
chart.NSeries[1].Border.Weight = Aspose.Cells.Drawing.WeightType.MediumLine;
```

الشرح: يقوم الكود أعلاه بتخصيص حدود سلسلة الرسم البياني، وإعطائها خطًا منقطًا وحتى تغيير علامات نقاط البيانات إلى مثلثات. كل هذا يتعلق باللمسة الشخصية!

## الخطوة 10: احفظ المصنف الخاص بك

الآن، دعنا نحفظ عملك الشاق في ملف Excel.

```csharp
// حفظ ملف Excel
workbook.Save(outputDir + "outputSettingChartLines.xlsx");
```

الشرح: يحفظ هذا السطر المصنف الخاص بك بالاسم المحدد في دليل الإخراج الذي حددته. يمكنك الآن فتحه ورؤية الرسم البياني الرائع الخاص بك!

## الخطوة 11: تأكيد التنفيذ

وأخيرا، دعونا نؤكد أن كل شيء سار بسلاسة.

```csharp
Console.WriteLine("SettingChartLines executed successfully.");
```

الشرح: رسالة بسيطة لإعلامك بأن الكود الخاص بك تم تنفيذه دون أي مشاكل.

## خاتمة

تهانينا! لقد أتقنت الآن أساسيات إنشاء المخططات وتخصيصها باستخدام Aspose.Cells for .NET. باتباع بضع خطوات بسيطة، يمكنك الارتقاء بعرض البيانات الخاص بك، مما يجعله أكثر قابلية للفهم وجاذبية من الناحية البصرية. وبينما تجرب خيارات التخصيص الأخرى، تذكر أن المخطط الرائع لا يروي قصة فحسب، بل إنه يجذب جمهورك أيضًا.

## الأسئلة الشائعة

### ما هو Aspose.Cells لـ .NET؟  
Aspose.Cells for .NET هي مكتبة قوية للتعامل مع جداول بيانات Excel في تطبيقات .NET.

### هل يمكنني استخدام Aspose.Cells مجانًا؟  
 نعم، يوفر Aspose نسخة تجريبية مجانية لاختبار وظائفه. يمكنك تنزيلها[هنا](https://releases.aspose.com/).

### هل يتوفر الدعم لـ Aspose.Cells؟  
 بالتأكيد! يمكنك الحصول على الدعم من خلال[منتدى اسبوس](https://forum.aspose.com/c/cells/9).

### هل يمكنني إنشاء أنواع أخرى من الرسوم البيانية باستخدام Aspose.Cells؟  
نعم، يدعم Aspose أنواعًا مختلفة من المخططات البيانية بما في ذلك المخططات الخطية والدائرية والمساحية.

### كيف يمكنني الحصول على ترخيص مؤقت لـ Aspose.Cells؟  
 يمكنك التقدم بطلب للحصول على[رخصة مؤقتة](https://purchase.aspose.com/temporary-license/) من خلال موقع Aspose.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
