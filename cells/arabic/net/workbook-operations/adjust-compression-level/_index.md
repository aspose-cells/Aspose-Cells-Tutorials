---
"description": "تعرّف على كيفية ضبط مستوى ضغط مصنفات Excel باستخدام Aspose.Cells لـ .NET من خلال هذا الدليل التفصيلي. حسّن إدارة ملفاتك."
"linktitle": "ضبط مستوى الضغط في المصنف"
"second_title": "واجهة برمجة تطبيقات معالجة Excel Aspose.Cells .NET"
"title": "ضبط مستوى الضغط في المصنف"
"url": "/ar/net/workbook-operations/adjust-compression-level/"
"weight": 14
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# ضبط مستوى الضغط في المصنف

## مقدمة
عندما يتعلق الأمر بإدارة ملفات Excel الكبيرة، يُعد الضغط أداةً ثورية. فهو لا يوفر مساحة تخزين فحسب، بل يُسهّل أيضًا نقل الملفات ويجعلها أكثر كفاءة. إذا كنت تستخدم Aspose.Cells لـ .NET، يمكنك بسهولة ضبط مستوى ضغط مصنفاتك. في هذا الدليل، سنشرح لك العملية خطوة بخطوة، مع التأكد من فهمك لكل جزء من الشيفرة البرمجية وكيفية عملها.
## المتطلبات الأساسية
قبل الغوص في الكود، هناك بعض المتطلبات الأساسية التي يجب أن تكون موجودة:
1. المعرفة الأساسية بلغة C#: ستساعدك المعرفة ببرمجة C# على فهم مقتطفات التعليمات البرمجية بشكل أفضل.
2. مكتبة Aspose.Cells: يجب تثبيت مكتبة Aspose.Cells. يمكنك تنزيلها من [هنا](https://releases.aspose.com/cells/net/).
3. Visual Studio: ستكون بيئة تطوير مثل Visual Studio ضرورية لتشغيل الكود.
4. .NET Framework: تأكد من إعداد مشروعك باستخدام إصدار متوافق من .NET Framework.
## استيراد الحزم
للبدء، عليك استيراد الحزم اللازمة في مشروع C# الخاص بك. إليك كيفية القيام بذلك:
```csharp
using Aspose.Cells.Rendering;
using Aspose.Cells.WebExtensions;
using System;
```
هذه الحزم ضرورية للعمل مع ملفات Excel باستخدام مكتبة Aspose.Cells. `Aspose.Cells` تحتوي مساحة الاسم على جميع الفئات التي تحتاجها للتعامل مع ملفات Excel، بينما `Aspose.Cells.Xlsb` يوفر خيارات لحفظ الملفات بتنسيق XLSB.
الآن، دعنا نقوم بتقسيم عملية ضبط مستوى الضغط في مصنف إلى خطوات قابلة للإدارة.
## الخطوة 1: تحديد أدلة المصدر والإخراج
أولاً، عليك تحديد مكان ملفات المصدر ومكان حفظ ملفات الإخراج. هذا ضروري لضمان معرفة برنامجك بمكان الملفات التي يحتاجها للعمل.
```csharp
// دليل المصدر
string sourceDir = "Your Document Directory";
string outDir = "Your Document Directory";
```
يستبدل `"Your Document Directory"` مع المسار الفعلي لمجلداتك. سيساعد هذا البرنامج على تحديد الملفات التي تريد ضغطها.
## الخطوة 2: تحميل المصنف
بعد ذلك، حمّل المصنف الذي تريد ضغطه. هنا تبدأ المغامرة!
```csharp
Workbook workbook = new Workbook(sourceDir + "LargeSampleFile.xlsx");
```
في هذا السطر، نقوم بإنشاء مثيل جديد لـ `Workbook` قم بتحميل ملف Excel موجود. تأكد من أن اسم الملف يطابق اسم الملف الموجود في مجلد المصدر.
## الخطوة 3: إعداد خيارات الحفظ
الآن حان وقت ضبط خيارات الحفظ. سنضبط نوع الضغط لملف الإخراج. 
```csharp
XlsbSaveOptions options = new XlsbSaveOptions();
```
ال `XlsbSaveOptions` تتيح لك الفئة تحديد خيارات مختلفة عند حفظ المصنف الخاص بك بتنسيق XLSB، بما في ذلك مستويات الضغط.
## الخطوة 4: قياس وقت الضغط للمستوى 1
لنبدأ بمستوى الضغط الأول. سنقيس المدة اللازمة لحفظ المصنف بهذا المستوى من الضغط.
```csharp
options.CompressionType = OoxmlCompressionType.Level1;
var watch = Stopwatch.StartNew();
workbook.Save(outDir + "LargeSampleFile_level_1_out.xlsb", options);
watch.Stop();
var elapsedMs = watch.ElapsedMilliseconds;
Console.WriteLine("Level 1 Elapsed Time: " + elapsedMs);
```
هنا، نضبط نوع الضغط على المستوى ١، ونحفظ المصنف، ثم نقيس الوقت المستغرق. هذا يُعطينا فكرة عن مدة العملية.
## الخطوة 5: قياس وقت الضغط للمستوى 6
الآن، دعونا نرى كيف يعمل ضغط المستوى 6.
```csharp
watch = Stopwatch.StartNew();
options.CompressionType = OoxmlCompressionType.Level6;
workbook.Save(outDir + "LargeSampleFile_level_6_out.xlsb", options);
watch.Stop();
elapsedMs = watch.ElapsedMilliseconds;
Console.WriteLine("Level 6 Elapsed Time: " + elapsedMs);
```
هذه الخطوة مشابهة للخطوة السابقة، ولكننا نقوم بتغيير مستوى الضغط إلى المستوى 6. ستلاحظ أن الوقت المستغرق قد يختلف بناءً على مدى تعقيد المصنف.
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
في هذه الخطوة، قمنا بتعيين مستوى الضغط إلى المستوى 9. وهذا هو المكان الذي ستشاهد فيه عادةً أكبر انخفاض في حجم الملف، ولكن قد يستغرق الأمر وقتًا أطول للمعالجة.
## الخطوة 7: الناتج النهائي
بعد تشغيل كافة مستويات الضغط، يمكنك إخراج رسالة تشير إلى اكتمال العملية بنجاح.
```csharp
Console.WriteLine("AdjustCompressionLevel executed successfully.");
```
يؤكد هذا السطر البسيط من التعليمات البرمجية أن برنامجك قد انتهى من التنفيذ دون أي عقبات.
## خاتمة
يُعدّ ضبط مستوى ضغط مصنفاتك باستخدام Aspose.Cells لـ .NET عمليةً سهلةً تُحقق فوائدَ كبيرةً من حيث حجم الملف والأداء. باتباع الخطوات الموضحة في هذا الدليل، يمكنك بسهولة تطبيق الضغط في تطبيقاتك وتحسين كفاءة إدارة ملفات Excel.
## الأسئلة الشائعة
### ما هو Aspose.Cells؟  
Aspose.Cells هي مكتبة قوية لـ .NET تسمح للمطورين بإنشاء ملفات Excel ومعالجتها وتحويلها دون الحاجة إلى Microsoft Excel.
### كيف أقوم بتثبيت Aspose.Cells؟  
يمكنك تنزيل Aspose.Cells وتثبيته من [موقع Aspose](https://releases.aspose.com/cells/net/).
### ما هي مستويات الضغط المتاحة؟  
يدعم Aspose.Cells مستويات ضغط متعددة تتراوح من المستوى 1 (أقل ضغط) إلى المستوى 9 (أعلى ضغط).
### هل يمكنني اختبار Aspose.Cells مجانًا؟  
نعم! يمكنك الحصول على نسخة تجريبية مجانية من Aspose.Cells [هنا](https://releases.aspose.com/).
### أين يمكنني العثور على الدعم لـ Aspose.Cells؟  
لأي استفسارات أو دعم، يمكنك زيارة منتدى دعم Aspose [هنا](https://forum.aspose.com/c/cells/9).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}