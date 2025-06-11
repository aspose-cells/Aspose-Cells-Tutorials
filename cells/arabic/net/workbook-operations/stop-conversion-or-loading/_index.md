---
"description": "تعلم كيفية إيقاف تحويل المصنف في Aspose.Cells لـ .NET باستخدام Interrupt Monitor، مع البرنامج التعليمي التفصيلي خطوة بخطوة."
"linktitle": "إيقاف التحويل أو التحميل باستخدام مراقبة المقاطعة"
"second_title": "واجهة برمجة تطبيقات معالجة Excel Aspose.Cells .NET"
"title": "إيقاف التحويل أو التحميل باستخدام مراقبة المقاطعة"
"url": "/ar/net/workbook-operations/stop-conversion-or-loading/"
"weight": 26
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# إيقاف التحويل أو التحميل باستخدام مراقبة المقاطعة

## مقدمة
غالبًا ما يتطلب العمل مع ملفات Excel كبيرة الحجم عمليات طويلة تستهلك الوقت والموارد. ولكن ماذا لو استطعت إيقاف عملية التحويل في منتصفها عندما تدرك أن هناك حاجة إلى تغيير؟ يوفر Aspose.Cells لـ .NET ميزة تسمى "مراقبة المقاطعة"، والتي تتيح لك إيقاف تحويل المصنف إلى تنسيق آخر مثل PDF. قد يكون هذا حلاً فعالاً، خاصةً عند العمل مع ملفات بيانات ضخمة. في هذا الدليل، سنشرح كيفية إيقاف عملية التحويل باستخدام "مراقبة المقاطعة" في Aspose.Cells لـ .NET.
## المتطلبات الأساسية
قبل الغوص، تأكد من أن لديك ما يلي في مكانه:
1. Aspose.Cells لـ .NET - تنزيله [هنا](https://releases.aspose.com/cells/net/).
2. بيئة تطوير .NET - مثل Visual Studio.
3. المعرفة الأساسية ببرمجة C# - الإلمام بقواعد لغة C# سوف يساعدك على المتابعة.
## استيراد الحزم
للبدء، لنستورد الحزم اللازمة. تتضمن هذه الاستيرادات:
- Aspose.Cells: المكتبة الرئيسية للتعامل مع ملفات Excel.
- System.Threading: لإدارة الخيوط، حيث سيقوم هذا المثال بتشغيل عمليتين متوازيتين.
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading;
using System.IO;
```
دعونا نقسم العملية إلى خطوات مفصلة. ستساعدك كل خطوة على فهم أهمية إعداد واستخدام مراقب المقاطعة لإدارة تحويل مصنفات Excel.
## الخطوة 1: إنشاء الفئة وتعيين دليل الإخراج
أولاً، نحتاج إلى فئة لتغليف وظائفنا، بالإضافة إلى الدليل الذي سيتم حفظ ملف الإخراج فيه.
```csharp
class StopConversionOrLoadingUsingInterruptMonitor
{
    static string outputDir = "Your Document Directory";
}
```
يستبدل `"Your Document Directory"` مع المسار الفعلي الذي تريد حفظ ملف PDF فيه.
## الخطوة 2: إنشاء مثيل لمراقب المقاطعة
بعد ذلك، أنشئ كائن InterruptMonitor. سيساعد هذا الكائن في التحكم بالعملية من خلال إعداد إمكانية مقاطعتها في أي وقت.
```csharp
InterruptMonitor im = new InterruptMonitor();
```
سيتم إرفاق مراقب المقاطعة هذا بمصنف العمل الخاص بنا، مما يسمح لنا بإدارة عملية التحويل.
## الخطوة 3: إعداد المصنف للتحويل
الآن، دعنا نقوم بإنشاء كائن مصنف، ونقوم بتعيين InterruptMonitor إليه، ثم نصل إلى ورقة العمل الأولى لإدراج بعض النصوص النموذجية.
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
الآن، لنحاول حفظ المصنف كملف PDF. سنستخدم `try-catch` كتلة للتعامل مع أي انقطاع قد يحدث.
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
في حال انقطاع العملية، سيلتقطها الاستثناء ويعرض رسالة مناسبة. وإلا، فسيتم حفظ المصنف كملف PDF.
## الخطوة 5: مقاطعة عملية التحويل
الميزة الرئيسية هنا هي إمكانية مقاطعة العملية. سنضيف تأخيرًا باستخدام `Thread.Sleep` ومن ثم اتصل بـ `Interrupt()` طريقة إيقاف التحويل بعد 10 ثواني.
```csharp
void WaitForWhileAndThenInterrupt()
{
    Thread.Sleep(1000 * 10);
    im.Interrupt();
}
```
يمنح هذا التأخير المصنف وقتًا للبدء في التحويل إلى PDF قبل إرسال إشارة المقاطعة.
## الخطوة 6: تنفيذ الخيوط في وقت واحد
لدمج كل شيء، نحتاج إلى بدء كلتا الدالتين في خيطين منفصلين. بهذه الطريقة، يمكن إجراء تحويل المصنف وانتظار المقاطعة في آنٍ واحد.
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
يتم تشغيل الكود أعلاه `CreateWorkbookAndConvertItToPdfFormat` و `WaitForWhileAndThenInterrupt` في خيوط متوازية، وربطها بمجرد انتهاء العمليتين.
## الخطوة 7: التنفيذ النهائي
وأخيرًا، سنضيف `Run()` طريقة لتنفيذ الكود.
```csharp
public static void Run()
{
    new StopConversionOrLoadingUsingInterruptMonitor().TestRun();
    Console.WriteLine("StopConversionOrLoadingUsingInterruptMonitor executed successfully.");
}
```
هذا `Run` الطريقة هي نقطة الدخول للبدء ومراقبة الانقطاع أثناء العمل.
## خاتمة
في هذا البرنامج التعليمي، استكشفنا كيفية إيقاف عملية التحويل في Aspose.Cells لـ .NET. يُعدّ مُراقب المقاطعة أداةً مفيدةً عند العمل مع ملفات Excel كبيرة الحجم، إذ يسمح لك بإيقاف العمليات دون انتظار اكتمالها. يُعدّ هذا مفيدًا بشكل خاص في الحالات التي يكون فيها الوقت والموارد ثمينين، وتتطلب ملاحظات سريعة.
## الأسئلة الشائعة
### ما هو مراقب المقاطعة في Aspose.Cells لـ .NET؟  
يتيح لك "مراقب المقاطعة" إيقاف عملية تحويل المصنف أو تحميله في منتصف العملية.
### هل يمكنني استخدام Interrupt Monitor لتنسيقات أخرى غير PDF؟  
نعم، يمكنك مقاطعة التحويلات إلى التنسيقات المدعومة الأخرى أيضًا.
### كيف يؤثر Thread.Sleep() على توقيت المقاطعة؟  
إن Thread.Sleep() ينشئ تأخيرًا قبل تشغيل المقاطعة، مما يتيح الوقت لبدء التحويل.
### هل يمكنني مقاطعة العملية قبل 10 ثواني؟  
نعم، تعديل التأخير في `WaitForWhileAndThenInterrupt()` إلى وقت أقصر.
### هل ستؤثر عملية المقاطعة على الأداء؟  
إن التأثير ضئيل، وهو مفيد للغاية لإدارة العمليات الطويلة الأمد.
لمزيد من المعلومات، راجع [توثيق Aspose.Cells لـ .NET](https://reference.aspose.com/cells/net/)إذا كنت بحاجة إلى مساعدة، تحقق من [منتدى الدعم](https://forum.aspose.com/c/cells/9) أو احصل على [نسخة تجريبية مجانية](https://releases.aspose.com/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}