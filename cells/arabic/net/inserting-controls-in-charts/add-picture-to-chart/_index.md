---
title: إضافة صورة إلى الرسم البياني
linktitle: إضافة صورة إلى الرسم البياني
second_title: واجهة برمجة تطبيقات معالجة Excel الخاصة بـ Aspose.Cells .NET
description: تعرف على كيفية إضافة الصور بسهولة إلى مخططات Excel باستخدام Aspose.Cells for .NET. قم بتحسين مخططاتك وعروضك التقديمية بخطوات بسيطة قليلة.
weight: 11
url: /ar/net/inserting-controls-in-charts/add-picture-to-chart/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إضافة صورة إلى الرسم البياني

## مقدمة

هل سئمت من المخططات المملة التي تفتقر إلى اللمسة الشخصية؟ هل تريد أن تتعلم كيفية إضافة صور إلى رسومات Excel الخاصة بك؟ حسنًا، أنت محظوظ! في هذا البرنامج التعليمي، سنتعمق في عالم Aspose.Cells for .NET ونتعلم كيفية إضافة الصور إلى المخططات في Excel. لذا، تناول فنجان القهوة المفضل لديك، ولنبدأ!

## المتطلبات الأساسية

قبل أن ننتقل إلى التفاصيل الدقيقة للترميز، هناك بعض المتطلبات الأساسية التي يجب أن تتوفر لديك لمتابعتها بسلاسة:

- Visual Studio: هنا يمكنك كتابة وتشغيل كود .NET الخاص بك. تأكد من تثبيته.
-  Aspose.Cells لـ .NET: ستحتاج إلى هذه المكتبة للعمل مع ملفات Excel. يمكنك[تحميله هنا](https://releases.aspose.com/cells/net/).
- الفهم الأساسي للغة C#: على الرغم من أنني سأرشدك خلال الكود، فإن فهم أساسيات لغة C# سيجعل الأمور أكثر وضوحًا.

### خطوات التثبيت

1. تثبيت Aspose.Cells: يمكنك إضافة Aspose.Cells إلى مشروع Visual Studio الخاص بك عبر NuGet Package Manager. يمكنك القيام بذلك بالانتقال إلى Tools > NuGet Package Manager > Manage NuGet Packages for Solution والبحث عن "Aspose.Cells". انقر فوق Install (تثبيت).
2. إعداد مشروعك: قم بإنشاء مشروع تطبيق وحدة تحكم C# جديد في Visual Studio.

## استيراد الحزم

بمجرد إعداد كل شيء، فإن الخطوة التالية هي استيراد الحزم اللازمة إلى مشروعك. وإليك كيفية القيام بذلك:

### استيراد المساحات المطلوبة

في الجزء العلوي من ملف الكود C# الخاص بك، ستحتاج إلى استيراد المساحات التالية:

```csharp
using Aspose.Cells;
using Aspose.Cells.Charts;
using Aspose.Cells.Drawing;
using System.IO;
```

يخبر هذا برنامجك، "مرحبًا! سأستخدم هذه الميزات الرائعة من Aspose.Cells."

الآن بعد أن أصبح لدينا المتطلبات الأساسية، دعونا نقوم بتقسيم العملية إلى خطوات صغيرة. 

## الخطوة 1: قم بتحديد الدلائل الخاصة بك

أولاً وقبل كل شيء، نحتاج إلى إعداد المسارات لملفات الإدخال والإخراج. هذه الخطوة بالغة الأهمية لأننا نحتاج إلى معرفة مكان العثور على ملف Excel الحالي ومكان حفظ الملف المعدل.

```csharp
//دليل المصدر
string sourceDir = "Your Document Directory/";

//دليل الإخراج
string outputDir = "Your Output Directory/";
```

 يستبدل`Your Document Directory` و`Your Output Directory` مع المسارات الفعلية على جهاز الكمبيوتر الخاص بك. 

## الخطوة 2: تحميل المصنف الموجود

الآن، دعنا نقوم بتحميل ملف Excel الموجود حيث نريد إضافة صورتنا إلى الرسم البياني.

```csharp
// افتح الملف الموجود.
Workbook workbook = new Workbook(sourceDir + "sampleAddingPictureInChart.xls");
```

يفتح هذا الكود المصنف، مما يجعله جاهزًا للتحرير.

## الخطوة 3: تحضير تدفق الصورة

قبل إضافة الصورة، نحتاج إلى قراءة الصورة التي نريد إدراجها في الرسم البياني. 

```csharp
// الحصول على ملف صورة إلى الدفق.
FileStream stream = new FileStream(sourceDir + "sampleAddingPictureInChart.png", FileMode.Open, FileAccess.Read);
```

تأكد من حفظ الصورة في الدليل المحدد.

## الخطوة 4: تحديد الهدف من الرسم البياني

الآن، دعنا نحدد الرسم البياني الذي سنضيف صورتنا إليه. في هذا المثال، سنستهدف الرسم البياني الأول في ورقة العمل الأولى.

```csharp
// احصل على مخطط المصمم في الورقة الثانية.
Worksheet sheet = workbook.Worksheets[0];
Aspose.Cells.Charts.Chart chart = sheet.Charts[0];
```

بإمكانك الوصول إلى أي ورقة عمل عن طريق تغيير الفهرس وفقًا لذلك.

## الخطوة 5: أضف الصورة إلى الرسم البياني

بعد تحديد الرسم البياني، حان الوقت لإضافة الصورة! 

```csharp
// أضف صورة جديدة إلى الرسم البياني.
Aspose.Cells.Drawing.Picture pic0 = chart.Shapes.AddPictureInChart(50, 50, stream, 200, 200);
```

 هنا،`50` و`50` هي إحداثيات X وY حيث سيتم وضع الصورة، و`200` هو عرض وارتفاع الصورة.

## الخطوة 6: تخصيص تنسيق خط الصورة

هل تريد إضافة بعض الأناقة إلى صورتك؟ يمكنك تخصيص حدودها! وإليك كيفية القيام بذلك:

```csharp
// احصل على نوع تنسيق الخط للصورة.
Aspose.Cells.Drawing.LineFormat lineformat = pic0.Line; 

// تعيين نمط الشرطة.
lineformat.DashStyle = MsoLineDashStyle.Solid;

// ضبط وزن الخط.
lineformat.Weight = 4;    
```

يتيح لك هذا المقطع اختيار شكل الحدود وسمكها. اختر أي نمط يتوافق مع عرضك التقديمي!

## الخطوة 7: احفظ المصنف المعدل

بعد كل هذا العمل الشاق، دعنا نحفظ تعديلاتك عن طريق تنفيذ سطر التعليمات البرمجية التالي:

```csharp
// احفظ ملف Excel.
workbook.Save(outputDir + "outputAddingPictureInChart.xls");
```

لقد تم الآن دمج صورتك بنجاح في الرسم البياني، وملف الإخراج الخاص بك جاهز للعرض!

## الخطوة 8: أشر إلى النجاح

وأخيرًا، يمكنك إضافة رسالة بسيطة لتأكيد نجاح عمليتك:

```csharp
Console.WriteLine("AddingPictureInChart executed successfully.");
```

## خاتمة

في هذا البرنامج التعليمي، استكشفنا كيفية إضافة بعض الشخصية إلى مخططات Excel الخاصة بك عن طريق إضافة الصور باستخدام Aspose.Cells for .NET. من خلال بضع خطوات بسيطة، يمكنك الارتقاء بعروضك التقديمية من عادية إلى عروض لا تُنسى. إذن، ما الذي تنتظره؟ جربه ودع مخططاتك تتألق!

## الأسئلة الشائعة

### هل يمكنني إضافة صور متعددة إلى مخطط واحد؟
 نعم يمكنك الاتصال بالرقم`AddPictureInChart` كرر الطريقة عدة مرات لإضافة عدد الصور الذي تريده.

### ما هي تنسيقات الصور التي يدعمها Aspose.Cells؟
يدعم Aspose.Cells مجموعة متنوعة من تنسيقات الصور، بما في ذلك PNG، وJPEG، وBMP، وGIF.

### هل يمكنني تخصيص موضع الصورة؟
 بالتأكيد! إحداثيات X وY في`AddPictureInChart` تسمح الطريقة بتحديد المواقع بدقة.

### هل استخدام Aspose.Cells مجاني؟
يقدم Aspose.Cells نسخة تجريبية مجانية، ولكن للحصول على الميزات الكاملة، يلزم الحصول على ترخيص. يمكنك العثور على الأسعار[هنا](https://purchase.aspose.com/buy).

### أين يمكنني العثور على المزيد من الأمثلة؟
 تحقق من[توثيق Aspose.Cells](https://reference.aspose.com/cells/net/) لمزيد من الأمثلة والوظائف التفصيلية.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
