---
title: ضبط مستوى الضغط في المصنف
linktitle: ضبط مستوى الضغط في المصنف
second_title: واجهة برمجة تطبيقات معالجة Excel الخاصة بـ Aspose.Cells .NET
description: تعرف على كيفية ضبط مستوى ضغط مصنفات Excel باستخدام Aspose.Cells for .NET من خلال هذا الدليل التفصيلي. قم بتحسين إدارة الملفات لديك.
weight: 14
url: /ar/net/workbook-operations/adjust-compression-level/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ضبط مستوى الضغط في المصنف

## مقدمة
عندما يتعلق الأمر بإدارة ملفات Excel الكبيرة، فإن الضغط يعد أمرًا بالغ الأهمية. فهو لا يوفر مساحة تخزين فحسب، بل يجعل نقل الملفات أسرع وأكثر كفاءة أيضًا. إذا كنت تعمل مع Aspose.Cells لـ .NET، فيمكنك بسهولة ضبط مستوى الضغط في مصنفاتك. في هذا الدليل، سنرشدك خلال العملية خطوة بخطوة، مع التأكد من فهمك لكل جزء من التعليمات البرمجية وكيفية عملها.
## المتطلبات الأساسية
قبل الغوص في الكود، هناك بعض المتطلبات الأساسية التي يجب أن تكون موجودة:
1. المعرفة الأساسية بلغة C#: ستساعدك المعرفة ببرمجة C# على فهم مقتطفات التعليمات البرمجية بشكل أفضل.
2.  مكتبة Aspose.Cells: يجب أن يكون لديك مكتبة Aspose.Cells مثبتة. يمكنك تنزيلها من[هنا](https://releases.aspose.com/cells/net/).
3. Visual Studio: ستكون بيئة تطوير مثل Visual Studio ضرورية لتشغيل الكود.
4. .NET Framework: تأكد من إعداد مشروعك باستخدام إصدار متوافق من .NET Framework.
## استيراد الحزم
للبدء، تحتاج إلى استيراد الحزم اللازمة في مشروع C# الخاص بك. إليك كيفية القيام بذلك:
```csharp
using Aspose.Cells.Rendering;
using Aspose.Cells.WebExtensions;
using System;
```
 تعد هذه الحزم ضرورية للعمل مع ملفات Excel باستخدام مكتبة Aspose.Cells.`Aspose.Cells` تحتوي مساحة الاسم على جميع الفئات التي تحتاجها للتعامل مع ملفات Excel، بينما`Aspose.Cells.Xlsb` يوفر خيارات لحفظ الملفات بتنسيق XLSB.
الآن، دعونا نقوم بتقسيم عملية ضبط مستوى الضغط في مصنف إلى خطوات قابلة للإدارة.
## الخطوة 1: تحديد أدلة المصدر والإخراج
أولاً، عليك تحديد مكان وجود ملفات المصدر والمكان الذي تريد حفظ ملفات الإخراج فيه. وهذا أمر بالغ الأهمية لضمان معرفة برنامجك بمكان العثور على الملفات التي يحتاج إلى العمل بها.
```csharp
// دليل المصدر
string sourceDir = "Your Document Directory";
string outDir = "Your Document Directory";
```
 يستبدل`"Your Document Directory"` مع المسار الفعلي إلى المجلدات الخاصة بك. سيساعد هذا البرنامج في تحديد موقع الملفات التي تريد ضغطها.
## الخطوة 2: تحميل المصنف
بعد ذلك، قم بتحميل المصنف الذي تريد ضغطه. وهنا تبدأ السحر!
```csharp
Workbook workbook = new Workbook(sourceDir + "LargeSampleFile.xlsx");
```
في هذا السطر، نقوم بإنشاء مثيل جديد لـ`Workbook` قم بتحميل ملف Excel الموجود. تأكد من أن اسم الملف يتطابق مع الاسم الموجود في دليل المصدر.
## الخطوة 3: إعداد خيارات الحفظ
الآن حان الوقت لتكوين خيارات الحفظ. سنقوم بتعيين نوع الضغط لملف الإخراج. 
```csharp
XlsbSaveOptions options = new XlsbSaveOptions();
```
 ال`XlsbSaveOptions` تتيح لك الفئة تحديد خيارات مختلفة عند حفظ المصنف الخاص بك بتنسيق XLSB، بما في ذلك مستويات الضغط.
## الخطوة 4: قياس وقت الضغط للمستوى 1
لنبدأ بمستوى الضغط الأول. سنقيس المدة التي يستغرقها حفظ المصنف بهذا المستوى من الضغط.
```csharp
options.CompressionType = OoxmlCompressionType.Level1;
var watch = Stopwatch.StartNew();
workbook.Save(outDir + "LargeSampleFile_level_1_out.xlsb", options);
watch.Stop();
var elapsedMs = watch.ElapsedMilliseconds;
Console.WriteLine("Level 1 Elapsed Time: " + elapsedMs);
```
هنا، نقوم بتعيين نوع الضغط على المستوى 1، ثم نحفظ المصنف، ثم نقيس الوقت المنقضي. وهذا يمنحنا فكرة عن المدة التي تستغرقها العملية.
## الخطوة 5: قياس وقت الضغط للمستوى 6
الآن، دعونا نرى كيفية أداء ضغط المستوى 6.
```csharp
watch = Stopwatch.StartNew();
options.CompressionType = OoxmlCompressionType.Level6;
workbook.Save(outDir + "LargeSampleFile_level_6_out.xlsb", options);
watch.Stop();
elapsedMs = watch.ElapsedMilliseconds;
Console.WriteLine("Level 6 Elapsed Time: " + elapsedMs);
```
هذه الخطوة مشابهة للخطوة السابقة، ولكننا نغير مستوى الضغط إلى المستوى 6. ستلاحظ أن الوقت المستغرق قد يختلف بناءً على تعقيد المصنف.
## الخطوة 6: قياس وقت الضغط للمستوى 9
وأخيرًا، دعونا نلقي نظرة على الأداء بأعلى مستوى ضغط.
```csharp
watch = Stopwatch.StartNew();
options.CompressionType = OoxmlCompressionType.Level9;
workbook.Save(outDir + "LargeSampleFile_level_9_out.xlsb", options);
watch.Stop();
elapsedMs = watch.ElapsedMilliseconds;
Console.WriteLine("Level 9 Elapsed Time: " + elapsedMs);
```
في هذه الخطوة، قمنا بتعيين مستوى الضغط إلى المستوى 9. وهذا هو المكان الذي سترى فيه عادةً أكبر انخفاض في حجم الملف، ولكن قد يستغرق الأمر وقتًا أطول للمعالجة.
## الخطوة 7: الناتج النهائي
بعد تشغيل كافة مستويات الضغط، يمكنك إخراج رسالة تشير إلى اكتمال العملية بنجاح.
```csharp
Console.WriteLine("AdjustCompressionLevel executed successfully.");
```
يؤكد هذا السطر البسيط من التعليمات البرمجية أن برنامجك قد انتهى من التنفيذ دون أي عقبات.
## خاتمة
إن ضبط مستوى ضغط المصنفات باستخدام Aspose.Cells for .NET هو عملية بسيطة يمكن أن تؤدي إلى فوائد كبيرة من حيث حجم الملف والأداء. باتباع الخطوات الموضحة في هذا الدليل، يمكنك بسهولة تنفيذ الضغط في تطبيقاتك وتحسين كفاءة إدارة ملفات Excel.
## الأسئلة الشائعة
### ما هو Aspose.Cells؟  
Aspose.Cells هي مكتبة قوية لـ .NET تتيح للمطورين إنشاء ملفات Excel ومعالجتها وتحويلها دون الحاجة إلى Microsoft Excel.
### كيف أقوم بتثبيت Aspose.Cells؟  
 يمكنك تنزيل Aspose.Cells وتثبيته من[موقع اسبوس](https://releases.aspose.com/cells/net/).
### ما هي مستويات الضغط المتاحة؟  
يدعم Aspose.Cells مستويات ضغط متعددة تتراوح من المستوى 1 (أقل ضغط) إلى المستوى 9 (أعلى ضغط).
### هل يمكنني اختبار Aspose.Cells مجانًا؟  
 نعم! يمكنك الحصول على نسخة تجريبية مجانية من Aspose.Cells[هنا](https://releases.aspose.com/).
### أين يمكنني العثور على الدعم لـ Aspose.Cells؟  
 لأي استفسارات أو دعم، يمكنك زيارة منتدى دعم Aspose[هنا](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
