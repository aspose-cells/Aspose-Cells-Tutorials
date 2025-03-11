---
title: إيقاف التحويل أو التحميل باستخدام مراقبة المقاطعة
linktitle: إيقاف التحويل أو التحميل باستخدام مراقبة المقاطعة
second_title: واجهة برمجة تطبيقات معالجة Excel الخاصة بـ Aspose.Cells .NET
description: تعلم كيفية إيقاف تحويل المصنف في Aspose.Cells لـ .NET باستخدام Interrupt Monitor، مع البرنامج التعليمي المفصل خطوة بخطوة.
weight: 26
url: /ar/net/workbook-operations/stop-conversion-or-loading/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إيقاف التحويل أو التحميل باستخدام مراقبة المقاطعة

## مقدمة
غالبًا ما يتضمن العمل مع ملفات Excel الكبيرة عمليات طويلة قد تستهلك الوقت والموارد. ولكن ماذا لو كان بإمكانك إيقاف عملية التحويل في منتصفها عندما تدرك أن هناك شيئًا يحتاج إلى التغيير؟ يحتوي Aspose.Cells for .NET على ميزة تسمى Interrupt Monitor، والتي تتيح لك مقاطعة تحويل المصنف إلى تنسيق آخر مثل PDF. يمكن أن يكون هذا منقذًا للحياة، خاصة عند العمل مع ملفات بيانات كبيرة. في هذا الدليل، سنشرح كيفية مقاطعة عملية التحويل باستخدام Interrupt Monitor في Aspose.Cells for .NET.
## المتطلبات الأساسية
قبل الغوص، تأكد من توفر ما يلي:
1.  Aspose.Cells لـ .NET - تنزيله[هنا](https://releases.aspose.com/cells/net/).
2. بيئة تطوير .NET - مثل Visual Studio.
3. المعرفة الأساسية لبرمجة C# - الإلمام بقواعد لغة C# سوف يساعدك على المتابعة.
## استيراد الحزم
للبدء، دعنا نستورد الحزم اللازمة. تتضمن هذه الحزم:
- Aspose.Cells: المكتبة الرئيسية للتعامل مع ملفات Excel.
- System.Threading: لإدارة الخيوط، حيث سيعمل هذا المثال على تشغيل عمليتين متوازيتين.
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading;
using System.IO;
```
دعنا نقسم العملية إلى خطوات تفصيلية. ستساعدك كل خطوة على فهم أهمية إعداد واستخدام أداة مراقبة المقاطعة لإدارة تحويل مصنف Excel.
## الخطوة 1: إنشاء الفئة وتعيين دليل الإخراج
أولاً، نحتاج إلى فئة لتغليف وظائفنا، بالإضافة إلى دليل حيث سيتم حفظ ملف الإخراج.
```csharp
class StopConversionOrLoadingUsingInterruptMonitor
{
    static string outputDir = "Your Document Directory";
}
```
 يستبدل`"Your Document Directory"` مع المسار الفعلي الذي تريد حفظ ملف PDF فيه.
## الخطوة 2: إنشاء مثيل لمراقب المقاطعة
بعد ذلك، قم بإنشاء كائن InterruptMonitor. سيساعد هذا الكائن في التحكم في العملية من خلال إعداد القدرة على مقاطعتها في أي نقطة معينة.
```csharp
InterruptMonitor im = new InterruptMonitor();
```
سيتم إرفاق مراقب المقاطعة هذا بكتاب العمل الخاص بنا، مما يسمح لنا بإدارة عملية التحويل.
## الخطوة 3: إعداد المصنف للتحويل
الآن، دعنا نقوم بإنشاء كائن مصنف، ونقوم بتعيين InterruptMonitor إليه، ثم نقوم بالوصول إلى ورقة العمل الأولى لإدراج بعض النصوص النموذجية.
```csharp
void CreateWorkbookAndConvertItToPdfFormat()
{
    Workbook wb = new Workbook();
    wb.InterruptMonitor = im;
    Worksheet ws = wb.Worksheets[0];
    Cell cell = ws.Cells["J1000000"];
    cell.PutValue("This is text.");
}
```
يقوم الكود أعلاه بإنشاء مصنف، وتعيين InterruptMonitor له، ووضع النص في خلية بعيدة (`J1000000`إن وضع النص في موضع الخلية هذا يضمن أن معالجة المصنف ستستغرق وقتًا أطول، مما يمنح InterruptMonitor وقتًا كافيًا للتدخل.
## الخطوة 4: حفظ المصنف بتنسيق PDF والتعامل مع المقاطعة
 الآن، دعنا نحاول حفظ المصنف بتنسيق PDF. سنستخدم ملف`try-catch` كتلة للتعامل مع أي انقطاع قد يحدث.
```csharp
try
{
    wb.Save(outputDir + "output_InterruptMonitor.pdf");
}
catch (Aspose.Cells.CellsException ex)
{
    Console.WriteLine("Process Interrupted - Message: " + ex.Message);
}
```
إذا تمت مقاطعة العملية، فسوف يلتقطها الاستثناء ويعرض رسالة مناسبة. وإلا، فسيتم حفظ المصنف بتنسيق PDF.
## الخطوة 5: مقاطعة عملية التحويل
 الميزة الرئيسية هنا هي القدرة على مقاطعة العملية. سنضيف تأخيرًا باستخدام`Thread.Sleep` ومن ثم اتصل`Interrupt()` طريقة إيقاف التحويل بعد 10 ثواني.
```csharp
void WaitForWhileAndThenInterrupt()
{
    Thread.Sleep(1000 * 10);
    im.Interrupt();
}
```
يمنح هذا التأخير المصنف وقتًا للبدء في التحويل إلى PDF قبل إرسال إشارة المقاطعة.
## الخطوة 6: تنفيذ الخيوط في وقت واحد
لتجميع كل شيء معًا، نحتاج إلى بدء كلتا الوظيفتين في خيوط منفصلة. بهذه الطريقة، يمكن أن يحدث تحويل المصنف وانتظار المقاطعة في نفس الوقت.
```csharp
public void TestRun()
{
    ThreadStart ts1 = new ThreadStart(this.CreateWorkbookAndConvertItToPdfFormat);
    Thread t1 = new Thread(ts1);
    t1.Start();
    ThreadStart ts2 = new ThreadStart(this.WaitForWhileAndThenInterrupt);
    Thread t2 = new Thread(ts2);
    t2.Start();
    t1.Join();
    t2.Join();
}
```
 يتم تشغيل الكود أعلاه`CreateWorkbookAndConvertItToPdfFormat` و`WaitForWhileAndThenInterrupt` في خيوط متوازية، وربطها بمجرد انتهاء العمليتين.
## الخطوة 7: التنفيذ النهائي
 وأخيرًا، سنضيف`Run()` طريقة لتنفيذ الكود.
```csharp
public static void Run()
{
    new StopConversionOrLoadingUsingInterruptMonitor().TestRun();
    Console.WriteLine("StopConversionOrLoadingUsingInterruptMonitor executed successfully.");
}
```
 هذا`Run` الطريقة هي نقطة الدخول للبدء ومراقبة الانقطاع أثناء العمل.
## خاتمة
في هذا البرنامج التعليمي، استكشفنا كيفية مقاطعة عملية التحويل في Aspose.Cells لـ .NET. تُعد أداة Interrupt Monitor أداة مفيدة عند العمل مع ملفات Excel كبيرة، حيث تتيح لك إيقاف العمليات دون انتظار اكتمالها. وهذا مفيد بشكل خاص في السيناريوهات التي يكون فيها الوقت والموارد ثمينين، وتكون هناك حاجة إلى ملاحظات سريعة.
## الأسئلة الشائعة
### ما هو مراقب المقاطعة في Aspose.Cells لـ .NET؟  
يتيح لك "مراقب المقاطعة" إيقاف عملية تحويل المصنف أو عملية التحميل في منتصف العملية.
### هل يمكنني استخدام Interrupt Monitor لتنسيقات أخرى غير PDF؟  
نعم، يمكنك مقاطعة التحويلات إلى التنسيقات المدعومة الأخرى أيضًا.
### كيف يؤثر Thread.Sleep() على توقيت المقاطعة؟  
إن Thread.Sleep() ينشئ تأخيرًا قبل تشغيل المقاطعة، مما يمنح الوقت لبدء التحويل.
### هل يمكنني مقاطعة العملية قبل 10 ثواني؟  
 نعم، تعديل التأخير في`WaitForWhileAndThenInterrupt()` إلى وقت أقصر.
### هل ستؤثر عملية المقاطعة على الأداء؟  
إن التأثير ضئيل، وهو مفيد للغاية لإدارة العمليات الطويلة الأمد.
 لمزيد من المعلومات، راجع[توثيق Aspose.Cells لـ .NET](https://reference.aspose.com/cells/net/) إذا كنت بحاجة إلى مساعدة، تحقق من[منتدى الدعم](https://forum.aspose.com/c/cells/9)أو الحصول على[نسخة تجريبية مجانية](https://releases.aspose.com/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
