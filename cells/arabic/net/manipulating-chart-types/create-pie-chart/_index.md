---
"description": "تعلّم كيفية إنشاء مخطط دائري في Excel باستخدام Aspose.Cells لـ .NET من خلال هذا الدليل المفصّل. صوّر بياناتك بكل سهولة."
"linktitle": "إنشاء مخطط دائري"
"second_title": "واجهة برمجة تطبيقات معالجة Excel Aspose.Cells .NET"
"title": "إنشاء مخطط دائري"
"url": "/ar/net/manipulating-chart-types/create-pie-chart/"
"weight": 12
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء مخطط دائري

## مقدمة

يُعد إنشاء المخططات البيانية أمرًا أساسيًا لتمثيل البيانات بصريًا، وتُعدّ المخططات الدائرية من أكثر الطرق شيوعًا لتوضيح كيفية ترابط الأجزاء مع بعضها البعض. باستخدام Aspose.Cells for .NET، يمكنك بسهولة أتمتة إنشاء المخططات الدائرية في ملفات Excel. في هذا البرنامج التعليمي، سنتعمق في كيفية إنشاء مخطط دائري من الصفر باستخدام Aspose.Cells for .NET، مع دليل خطوة بخطوة لجعل العملية سلسة ومباشرة. سواء كنت جديدًا على هذه الأداة أو ترغب في تحسين مهاراتك في أتمتة Excel، فهذا الدليل سيُغطي احتياجاتك!

## المتطلبات الأساسية

قبل الغوص في الكود، تأكد من إعداد ما يلي:

1. مكتبة Aspose.Cells لـ .NET: تأكد من تثبيت Aspose.Cells في مشروعك. إذا لم تقم بتثبيته بعد، يمكنك تنزيله من [هنا](https://releases.aspose.com/cells/net/).
2. بيئة تطوير .NET: تأكد من إعداد مشروعك لاستخدام .NET Framework أو .NET Core.
3. المعرفة الأساسية بلغة C#: يجب أن تكون مرتاحًا في برمجة C#، وخاصة البرمجة الكائنية التوجه (OOP).

للمستخدمين المتقدمين، يُمكن استخدام ترخيص مؤقت لفتح جميع ميزات Aspose.Cells. يُمكنك طلبه من [هنا](https://purchase.aspose.com/temporary-license/).

## استيراد الحزم

للبدء، استورد مساحات الأسماء والحزم اللازمة لهذا البرنامج التعليمي. تتضمن هذه الحزم عمليات الإدخال/الإخراج الأساسية وحزمة Aspose.Cells.

```csharp
using System;
using System.IO;

using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
using Aspose.Cells.Charts;
```

## الخطوة 1: إنشاء مصنف جديد

أولاً، نحتاج إلى إنشاء مثيل لـ `Workbook` الفئة التي تُمثل ملف Excel. يحتوي المصنف على عدة أوراق، وفي مثالنا، سنعمل على ورقتين: واحدة للبيانات وأخرى للمخطط الدائري.

```csharp
Workbook workbook = new Workbook();
```

سيؤدي هذا إلى تهيئة مصنف Excel جديد. ولكن أين تذهب البيانات؟ لنتناول ذلك في الخطوة التالية.

## الخطوة 2: إضافة البيانات إلى ورقة العمل

بعد إنشاء المصنف، نحتاج إلى الوصول إلى ورقة العمل الأولى وتسميتها. هنا سنُدخل البيانات المطلوبة للمخطط الدائري.

```csharp
Worksheet sheet = workbook.Worksheets[0];
sheet.Name = "Data";
Cells cells = sheet.Cells;
```

الآن، يمكننا إدخال بعض بيانات المبيعات الوهمية التي تمثل مناطق مختلفة:

```csharp
cells["A1"].PutValue("Region");
cells["A2"].PutValue("France");
cells["A3"].PutValue("Germany");
cells["A4"].PutValue("England");
cells["A5"].PutValue("Sweden");
cells["A6"].PutValue("Italy");
cells["A7"].PutValue("Spain");
cells["A8"].PutValue("Portugal");

cells["B1"].PutValue("Sales");
cells["B2"].PutValue(70000);
cells["B3"].PutValue(55000);
cells["B4"].PutValue(30000);
cells["B5"].PutValue(40000);
cells["B6"].PutValue(35000);
cells["B7"].PutValue(32000);
cells["B8"].PutValue(10000);
```

هنا، نضيف عمودين: أحدهما للمناطق والآخر لأرقام المبيعات. سيتم تمثيل هذه البيانات في المخطط الدائري.

## الخطوة 3: إضافة ورقة الرسم البياني

بعد ذلك، دعنا نضيف ورقة عمل منفصلة لحمل مخطط الفطيرة.

```csharp
int sheetIndex = workbook.Worksheets.Add(SheetType.Chart);
Worksheet chartSheet = workbook.Worksheets[sheetIndex];
chartSheet.Name = "Chart";
```

ستستضيف هذه الورقة الجديدة المخطط الدائري. تسميتها "مخطط" يضمن للمستخدمين معرفة ما سيظهر لهم عند فتح الملف.

## الخطوة 4: إنشاء مخطط دائري

الآن حان وقت إنشاء المخطط الفعلي. سنحدد أننا نريد مخططًا دائريًا، وسنحدد موقعه على الورقة.

```csharp
int chartIndex = chartSheet.Charts.Add(Aspose.Cells.Charts.ChartType.Pie, 5, 0, 25, 10);
Aspose.Cells.Charts.Chart chart = chartSheet.Charts[chartIndex];
```

الطريقة `Add()` يقبل المعلمات لنوع الرسم البياني (في هذه الحالة، `ChartType.Pie`)، وموقعه في ورقة العمل. تُمثل الأرقام مواقع الصفوف والأعمدة.

## الخطوة 5: تخصيص مظهر الرسم البياني

لن يكتمل مخطط دائري بدون بعض التخصيص! لنجعل مخططنا جذابًا بصريًا من خلال تعديل الألوان والتسميات والعنوان.

### تعيين عنوان الرسم البياني
```csharp
chart.Title.Text = "Sales By Region";
chart.Title.Font.Color = Color.Blue;
chart.Title.Font.IsBold = true;
chart.Title.Font.Size = 12;
```

### تخصيص مساحة الرسم
```csharp
chart.PlotArea.Area.ForegroundColor = Color.Coral;
chart.PlotArea.Area.FillFormat.SetTwoColorGradient(Color.Yellow, Color.White, GradientStyleType.Vertical, 2);
chart.PlotArea.Border.IsVisible = false;
```

قمنا بتعيين تعبئة التدرج لمنطقة الرسم البياني وإخفاء الحدود للحصول على مظهر أنظف.

## الخطوة 6: تحديد بيانات الرسم البياني

حان الوقت لربط الرسم البياني ببياناتنا. `NSeries` تقوم خاصية الرسم البياني بربط أرقام المبيعات والمناطق بالرسم البياني الدائري.

```csharp
chart.NSeries.Add("Data!B2:B8", true);
chart.NSeries.CategoryData = "Data!A2:A8";
chart.NSeries.IsColorVaried = true;
```

يشير السطر الأول إلى أننا نستخدم بيانات المبيعات من الخلايا `B2:B8`. ونخبر أيضًا الرسم البياني باستخدام أسماء المناطق من `A2:A8` كعلامات الفئة.

## الخطوة 7: إضافة تسميات البيانات

إضافة تسميات مباشرةً إلى شرائح المخطط البياني تُسهّل الفهم. لنُدرِج أسماء المناطق وقيم المبيعات ضمن شرائح المخطط الدائري.

```csharp
for (int i = 0; i < chart.NSeries.Count; i++)
{
    DataLabels labels = chart.NSeries[i].DataLabels;
    labels.ShowCategoryName = true;
    labels.ShowValue = true;
    labels.Position = LabelPositionType.InsideBase;
}
```

## الخطوة 8: تخصيص منطقة الرسم البياني والأسطورة

أخيرًا، دعونا نضيف بعض اللمسات الأخيرة على منطقة الرسم البياني والتوضيح التوضيحي. هذا يُحسّن العرض العام للرسم البياني.

### منطقة الرسم البياني
```csharp
ChartArea chartArea = chart.ChartArea;
chartArea.Area.Formatting = FormattingType.Custom;
chartArea.Area.FillFormat.Texture = TextureType.BlueTissuePaper;
```

### أسطورة
```csharp
Legend legend = chart.Legend;
legend.Position = LegendPositionType.Left;
legend.Font.IsBold = true;
legend.Border.Color = Color.Blue;
legend.Area.FillFormat.Texture = TextureType.Bouquet;
```

## الخطوة 9: حفظ المصنف

أخيرًا، نحفظ المصنف في ملف Excel. يمكنك تحديد مجلد الإخراج واسم الملف حسب الحاجة.

```csharp
workbook.Save(outputDir + "outputHowToCreatePieChart.xlsx");
```

## خاتمة

إنشاء مخطط دائري باستخدام Aspose.Cells لـ .NET عملية سهلة وقابلة للتخصيص. باتباع هذا الدليل، يمكنك إنشاء مخطط ذو مظهر احترافي يعرض رؤى قيّمة في بضع خطوات فقط. سواءً كان ذلك لأغراض إعداد التقارير التجارية أو التعليمية، فإن إتقان إنشاء المخططات سيعزز مهاراتك في أتمتة Excel. تذكر أن Aspose.Cells يوفر لك المرونة اللازمة لإنشاء ملفات Excel رائعة قائمة على البيانات بكل سهولة.

## الأسئلة الشائعة

### هل يمكنني إنشاء أنواع أخرى من المخططات باستخدام Aspose.Cells لـ .NET؟
نعم! يدعم Aspose.Cells أنواعًا مختلفة من المخططات، بما في ذلك المخططات الشريطية، والمخططات الخطية، ومخططات التشتت.

### هل أحتاج إلى ترخيص مدفوع لاستخدام Aspose.Cells لـ .NET؟
يمكنك استخدام النسخة المجانية مع بعض القيود. للحصول على الميزات الكاملة، ستحتاج إلى ترخيص، والذي يمكنك شراؤه. [هنا](https://purchase.aspose.com/buy).

### هل يمكنني تصدير الرسم البياني إلى تنسيقات مثل PDF أو الصور؟
بالتأكيد! يتيح لك Aspose.Cells تصدير المخططات بتنسيقات مختلفة، بما في ذلك PDF وPNG.

### هل من الممكن تصميم كل شريحة فطيرة بألوان مختلفة؟
نعم، يمكنك تطبيق ألوان مختلفة على كل شريحة عن طريق ضبط `IsColorVaried` الممتلكات إلى `true`كما هو موضح في البرنامج التعليمي.

### هل يمكنني أتمتة إنشاء مخططات متعددة في مصنف واحد؟
نعم، يمكنك إنشاء وتخصيص عدد كبير من المخططات حسب الحاجة ضمن ملف Excel واحد.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}