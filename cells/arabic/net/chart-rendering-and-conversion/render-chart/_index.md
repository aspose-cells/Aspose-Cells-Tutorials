---
"description": "اكتشف كيفية عرض المخططات البيانية في .NET باستخدام Aspose.Cells. اتبع دليلنا خطوة بخطوة لإنشاء رسومات مذهلة بسهولة."
"linktitle": "رسم بياني"
"second_title": "واجهة برمجة تطبيقات معالجة Excel Aspose.Cells .NET"
"title": "رسم بياني"
"url": "/ar/net/chart-rendering-and-conversion/render-chart/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# رسم بياني

## مقدمة

تُعد المخططات البيانية عنصرًا أساسيًا في عرض البيانات وتحليلها، إذ تُسهّل استيعاب المعلومات المعقدة. إذا كنت تعمل باستخدام .NET وتحتاج إلى إنشاء مخططات بيانية برمجيًا، فإن Aspose.Cells مكتبة فعّالة توفر ميزات بديهية ومتقدمة للتعامل مع ملفات Excel والمخططات البيانية. في هذا الدليل، سنشرح عملية عرض مخطط بياني باستخدام Aspose.Cells لـ .NET. استعد للتعمق في هذا البرنامج التعليمي المفصل، المصمم ليكون شيقًا وسهل المتابعة!

## المتطلبات الأساسية

قبل أن نبدأ بشرح الكود، تأكد من تجهيز كل شيء. إليك ما تحتاجه:

1. بيئة .NET: تأكد من إعداد بيئة تطوير .NET لديك. يمكنك استخدام Visual Studio أو أي بيئة تطوير متكاملة أخرى تدعم .NET.
2. Aspose.Cells لـ .NET: يجب تثبيت مكتبة Aspose.Cells. يمكنك تنزيلها من [صفحة إصدار Aspose](https://releases.aspose.com/cells/net/).
3. المعرفة الأساسية بلغة C#: ستساعدك المعرفة ببرمجة C# على فهم الأمثلة بشكل أفضل، ولكن لا تقلق إذا كنت جديدًا - سيشرح هذا الدليل كل شيء خطوة بخطوة!

## استيراد الحزم

الخطوة الأولى في رحلة البرمجة الخاصة بك هي استيراد الحزم اللازمة. افتح مشروعك في بيئة التطوير المتكاملة (IDE) وأضف مساحة الأسماء التالية:

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Aspose.Cells.Rendering;
```

ستوفر لك هذه المساحات الاسمية إمكانية الوصول إلى الوظائف التي توفرها مكتبة Aspose.Cells، مما يسمح لك بإنشاء مخططاتك ومعالجتها بسلاسة.


بعد أن تناولنا المتطلبات الأساسية والواردات، لننتقل إلى جوهر عملية عرض المخطط! سنُقسّمها إلى خطوات واضحة وسهلة التنفيذ.

## الخطوة 1: إعداد دليل الإخراج الخاص بك

قبل إنشاء مصنف العمل والمخطط، علينا تحديد مكان حفظ مخرجاتنا. بهذه الطريقة، عند إنشاء المخطط، ستعرف مكانه بالضبط.

```csharp
string outputDir = "Your Output Directory"; // حدد دليل الإخراج هنا.
```

تأكد من استبدال "دليل الإخراج الخاص بك" بالمسار الذي تريد حفظ صور الرسم البياني الخاصة بك فيه.

## الخطوة 2: إنشاء مصنف

بعد ذلك، سننشئ مصنفًا جديدًا. هنا تبدأ كل الأحداث الرائعة!

```csharp
Workbook workbook = new Workbook();
```

يؤدي هذا الخط إلى إنشاء مثيل جديد لـ `Workbook` الصف الذي يسمح لنا بالعمل مع الجداول والرسوم البيانية.

## الخطوة 3: إضافة ورقة عمل جديدة

الآن وقد أصبح لدينا مصنف العمل، حان الوقت لإضافة ورقة عمل جديدة. تخيل أوراق العمل كصفحات مختلفة في دفتر ملاحظات، حيث يمكنك تنظيم بياناتك.

```csharp
int sheetIndex = workbook.Worksheets.Add();
Worksheet worksheet = workbook.Worksheets[sheetIndex];
```

هنا، نضيف ورقة عمل جديدة ونحصل على مرجع لها. ستعمل على هذه الورقة لإدخال بياناتك ومخططاتك.

## الخطوة 4: إدخال قيم العينة

بعد إنشاء ورقة العمل، لنُضِف بعض البيانات النموذجية إلى الخلايا. هذه البيانات هي ما سيُبنى عليه مخططك، لذا اختر قيمًا مناسبة لنوع مخططك!

```csharp
worksheet.Cells["A1"].PutValue(50);
worksheet.Cells["A2"].PutValue(100);
worksheet.Cells["A3"].PutValue(150);
worksheet.Cells["B1"].PutValue(4);
worksheet.Cells["B2"].PutValue(20);
worksheet.Cells["B3"].PutValue(50);
```

في هذا المقطع، نقوم بملء الخلايا من "A1" إلى "A3" ببعض القيم الرقمية، والخلايا من "B1" إلى "B3" بمجموعة أخرى من القيم. لا تتردد في تخصيص هذه الأرقام لتناسب احتياجاتك!

## الخطوة 5: إنشاء مخطط

الآن، حان وقت إنشاء مخططك. سنضيف مخططًا عموديًا، وهو مثالي لمقارنة القيم.

```csharp
int chartIndex = worksheet.Charts.Add(ChartType.Column, 5, 0, 15, 5);
Aspose.Cells.Charts.Chart chart = worksheet.Charts[chartIndex];
```

هنا، نضيف مخططًا في الموقع المحدد عن طريق تحديد تخطيطه: تمثل المجموعة الأولى من الأرقام موضع المخطط على الشبكة.

## الخطوة 6: إضافة سلسلة البيانات إلى الرسم البياني

بعد إنشاء الرسم البياني، نحتاج الآن إلى ربطه بالبيانات التي أدخلناها في الخطوات السابقة.

```csharp
chart.NSeries.Add("A1:B3", true);
```

يربط هذا الخط سلسلة بيانات الرسم البياني بالقيم في الخلايا من "A1" إلى "B3". هذا يعني أن الرسم البياني سيعرض البيانات بصريًا كما هو مقصود.

## الخطوة 7: حفظ الرسم البياني كصورة

الآن دعنا نقوم بتحويل مخططنا إلى تنسيق صورة، حتى يمكن مشاركته وعرضه بسهولة.

```csharp
chart.ToImage(outputDir + "outputChartRendering.emf", System.Drawing.Imaging.ImageFormat.Emf);
```

في هذه الخطوة، نحفظ الرسم البياني كصورة EMF (ملف تعريفي مُحسَّن) في مجلد الإخراج المُحدَّد. يمكنك أيضًا حفظه بتنسيقات مختلفة مثل BMP أو PNG.

## الخطوة 8: تحويل الرسم البياني إلى خريطة نقطية

إذا كنت تفضل العمل مع الخرائط النقطية، فإليك كيفية تحويل الرسم البياني الخاص بك إلى تنسيق الخريطة النقطية.

```csharp
System.Drawing.Bitmap bitmap = chart.ToImage();
bitmap.Save(outputDir + "outputChartRendering.bmp", System.Drawing.Imaging.ImageFormat.Bmp);
```

سيؤدي هذا إلى حفظ مخططك كصورة BMP. تذكر أن ملفات BMP عادةً ما تكون أكبر حجمًا، لكنها تتميز بجودة عالية جدًا!

## الخطوة 9: العرض باستخدام الخيارات المتقدمة

يمكننا أيضًا عرض الرسم البياني بخيارات صور متقدمة لتحسين الجودة والدقة. لنبدأ بإعداد بعض الخيارات:

```csharp
ImageOrPrintOptions options = new ImageOrPrintOptions()
{
    VerticalResolution = 300,
    HorizontalResolution = 300,
    SmoothingMode = System.Drawing.Drawing2D.SmoothingMode.AntiAlias
};
```

تساعد هذه الخيارات على تحسين الجودة المرئية للصورة التي تقوم بإنشائها، وهي مفيدة بشكل خاص للعروض التقديمية أو المنشورات.

## الخطوة 10: تحويل الرسم البياني إلى صورة باستخدام خيارات متقدمة

الآن دعنا نقوم فعليًا بتحويل الرسم البياني باستخدام الخيارات المتقدمة التي قمنا بتعيينها للتو.

```csharp
chart.ToImage(outputDir + "outputChartRendering.png", options);
```

يؤدي هذا إلى حفظ الرسم البياني الخاص بك كملف PNG مع إعدادات جودة محسنة.

## الخطوة 11: تصدير الرسم البياني إلى PDF

أخيرًا، إذا كنت تريد مستندًا مصقولًا وقابلًا للمشاركة بسهولة، فيمكنك تصدير الرسم البياني الخاص بك مباشرةً إلى تنسيق PDF.

```csharp
chart.ToPdf(outputDir + "outputChartRendering.pdf");
```

ستؤدي هذه الخطوة إلى إنشاء ملف PDF يحتوي على الرسم البياني الخاص بك، مما يجعله مثاليًا للتقارير الرقمية أو المشاركة مع الزملاء.

## خاتمة 

تهانينا! لقد نجحت في عرض مخطط بياني باستخدام Aspose.Cells لـ .NET. تُبسّط هذه المكتبة الفعّالة إنشاء ملفات Excel والمخططات البيانية ومعالجتها، مما يجعل بياناتك أكثر سهولة في الوصول إليها وجاذبية بصرية. سواء كنت تُعدّ تقارير أو تحليلات أو عروضًا تقديمية، فإن للمخططات البيانية تأثيرًا كبيرًا، ومع Aspose، يمكنك إنشاؤها برمجيًا بسهولة.

## الأسئلة الشائعة

### ما هي أنواع المخططات البيانية التي يمكنني إنشاؤها باستخدام Aspose.Cells لـ .NET؟
يمكنك إنشاء مجموعة متنوعة من المخططات البيانية، بما في ذلك المخططات العمودية والخطية والدائرية والشريطية، وغيرها.

### هل يمكنني تخصيص مظهر الرسوم البيانية؟
نعم، يسمح Aspose.Cells بالتخصيص الشامل، بما في ذلك الألوان والأنماط وعناصر الرسم البياني.

### هل هناك نسخة تجريبية مجانية متاحة؟
بالتأكيد! يمكنك تنزيل نسخة تجريبية مجانية من [هنا](https://releases.aspose.com/).

### أين يمكنني الحصول على الدعم لـ Aspose.Cells؟
يمكنك العثور على الدعم والموارد المجتمعية في [منتدى دعم Aspose](https://forum.aspose.com/c/cells/9).

### هل أحتاج إلى ترخيص لاستخدام Aspose.Cells؟
نعم، يلزم الحصول على ترخيص للاستخدام المستمر بعد انتهاء الفترة التجريبية، ولكن يمكنك التقدم بطلب للحصول على ترخيص مؤقت [هنا](https://purchase.aspose.com/temporary-license/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}