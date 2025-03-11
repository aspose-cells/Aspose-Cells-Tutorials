---
title: اكتشاف المرجع الدائري في برنامج Excel برمجيًا
linktitle: اكتشاف المرجع الدائري في برنامج Excel برمجيًا
second_title: واجهة برمجة تطبيقات معالجة Excel الخاصة بـ Aspose.Cells .NET
description: يمكنك اكتشاف المراجع الدائرية بسهولة في Excel باستخدام Aspose.Cells for .NET. اتبع دليلنا خطوة بخطوة لضمان دقة الحسابات في جداول البيانات الخاصة بك.
weight: 13
url: /ar/net/excel-formulas-and-calculation-options/detecting-circular-reference/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# اكتشاف المرجع الدائري في برنامج Excel برمجيًا

## مقدمة
عندما يتعلق الأمر بالعمل مع ملفات Excel، فإن إحدى أكثر المشكلات المزعجة التي قد تواجهها هي المرجع الدائري. يحدث هذا عندما تشير الصيغة إلى الخلية الخاصة بها، إما بشكل مباشر أو غير مباشر، مما يؤدي إلى إنشاء حلقة يمكن أن تربك محرك حساب Excel. ولكن لا تقلق! باستخدام Aspose.Cells for .NET، يمكنك اكتشاف هذه المراجع الدائرية المزعجة برمجيًا، مما يضمن بقاء جداول البيانات الخاصة بك وظيفية ودقيقة. في هذا الدليل، سنرشدك خلال العملية خطوة بخطوة، مما يجعلها بسيطة للغاية.
## المتطلبات الأساسية
قبل أن نتعمق في التفاصيل الدقيقة لكشف المراجع الدائرية، دعنا نتأكد من أن لديك كل ما تحتاجه للبدء:
1. Visual Studio: تأكد من تثبيت Visual Studio على جهازك. ستكون هذه بيئة التطوير الخاصة بك.
2. .NET Framework: تأكد من أنك تستخدم إصدارًا متوافقًا من .NET Framework (على الأقل .NET Framework 4.0).
3.  مكتبة Aspose.Cells: يجب أن يكون لديك مكتبة Aspose.Cells. يمكنك تنزيلها من[موقع اسبوس](https://releases.aspose.com/cells/net/).
4. المعرفة الأساسية بلغة C#: ستكون المعرفة ببرمجة C# مفيدة، حيث سنقوم بكتابة التعليمات البرمجية بهذه اللغة.
5. ملف Excel: قم بإعداد ملف Excel يحتوي على مراجع دائرية للاختبار. يمكنك إنشاء ملف بسيط أو تنزيل عينة.
الآن بعد أن أصبح لدينا المتطلبات الأساسية، دعونا ننتقل إلى الجزء الممتع!
## استيراد الحزم
قبل أن تتمكن من البدء في كتابة التعليمات البرمجية، يتعين عليك استيراد الحزم اللازمة. وإليك كيفية القيام بذلك:
### إنشاء مشروع جديد
- افتح Visual Studio وقم بإنشاء مشروع تطبيق وحدة تحكم C# جديد.
### إضافة مرجع Aspose.Cells
- انقر بزر الماوس الأيمن على مشروعك في مستكشف الحلول.
- حدد "إدارة حزم NuGet".
- ابحث عن “Aspose.Cells” وقم بتثبيت الإصدار الأحدث.
### استيراد المساحات المطلوبة
 في الجزء العلوي من`Program.cs` الملف، استيراد المساحات الأساسية الضرورية:
```csharp
using System;
using System.Collections;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

الآن بعد أن قمنا بإعداد كل شيء، دعنا نتعمق في الكود الخاص باكتشاف المراجع الدائرية في ملف Excel.
## الخطوة 1: تحديد دليل الإدخال
أولاً، عليك تحديد الدليل الذي يوجد به ملف Excel الخاص بك. هذا هو المكان الذي ستحمل فيه ملف Excel الخاص بك.
```csharp
// دليل الإدخال
string sourceDir = "Your Document Directory";
```
 يستبدل`"Your Document Directory"` مع المسار الفعلي لملف Excel الخاص بك.
## الخطوة 2: تحميل المصنف باستخدام LoadOptions
بعد ذلك، ستقوم بتحميل مصنف Excel الخاص بك. وهنا تبدأ السحر!
```csharp
LoadOptions loadOptions = new LoadOptions();
var objWB = new Aspose.Cells.Workbook(sourceDir + "Circular Formulas.xls", loadOptions);
```
 هنا، نقوم بإنشاء مثيل جديد لـ`LoadOptions` وتحميل المصنف من المسار المحدد. تأكد من تطابق اسم ملف Excel الخاص بك!
## الخطوة 3: تمكين إعدادات التكرار
للسماح بالمراجع الدائرية، يجب عليك تمكين إعدادات التكرار في المصنف.
```csharp
objWB.Settings.Iteration = true;
```
يخبر هذا Aspose.Cells بالسماح بالمراجع الدائرية أثناء الحساب.
## الخطوة 4: إنشاء خيارات الحساب والشاشة الدائرية
الآن، دعنا نقوم بإنشاء خيارات الحساب وشاشتنا الدائرية المخصصة.
```csharp
CalculationOptions copts = new CalculationOptions();
CircularMonitor cm = new CircularMonitor();
copts.CalculationMonitor = cm;
```
 هنا، نقوم بإنشاء مثيل لـ`CalculationOptions` و عادة`CircularMonitor`ستساعدك هذه الشاشة على تتبع أي مراجع دائرية تم العثور عليها أثناء العمليات الحسابية.
## الخطوة 5: حساب الصيغ
الآن، حان الوقت لحساب الصيغ في المصنف الخاص بك.
```csharp
objWB.CalculateFormula(copts);
```
يقوم هذا الخط بتنفيذ الحساب والتحقق من المراجع الدائرية.
## الخطوة 6: إحصاء المراجع الدائرية
بعد الحساب، يمكنك حساب عدد المراجع الدائرية التي تم العثور عليها.
```csharp
long lngCircularRef = cm.circulars.Count;
Console.WriteLine("Circular References found - " + lngCircularRef);
```
سيؤدي هذا إلى إخراج عدد المراجع الدائرية التي تم اكتشافها في ملف Excel الخاص بك.
## الخطوة 7: عرض النتائج
وأخيرًا، دعنا نعرض النتائج ونؤكد أن طريقتنا تم تنفيذها بنجاح.
```csharp
Console.WriteLine("DetectCircularReference executed successfully.\r\n");
```
## الخطوة 8: تنفيذ فئة CircularMonitor
 لإكمال العملية، ستحتاج إلى تنفيذ`CircularMonitor` الصف. هذه الفئة سوف ترث من`AbstractCalculationMonitor` والتعامل مع اكتشاف المراجع الدائرية.
```csharp
public class CircularMonitor : AbstractCalculationMonitor
{
    public ArrayList circulars = new ArrayList();
    public ArrayList Circulars { get { return circulars; } }
    public override bool OnCircular(IEnumerator circularCellsData)
    {
        CalculationCell cc = null;
        ArrayList cur = new ArrayList();
        while (circularCellsData.MoveNext())
        {
            cc = (CalculationCell)circularCellsData.Current;
            cur.Add(cc.Worksheet.Name + "!" + CellsHelper.CellIndexToName(cc.CellRow, cc.CellColumn));
        }
        circulars.Add(cur);
        return true;
    }
}
```
تلتقط هذه الفئة تفاصيل كل مرجع دائري تم العثور عليه، بما في ذلك اسم ورقة العمل وفهرس الخلية.
## خاتمة
إن اكتشاف المراجع الدائرية في Excel باستخدام Aspose.Cells for .NET عملية بسيطة بمجرد تقسيمها إلى خطوات يمكن إدارتها. باتباع هذا الدليل، يمكنك بسهولة تحديد المراجع الدائرية في جداول البيانات الخاصة بك ومعالجتها، مما يضمن دقة حساباتك وموثوقيتها. سواء كنت مطورًا متمرسًا أو مبتدئًا، توفر Aspose.Cells أدوات قوية لتعزيز قدراتك على التعامل مع Excel. 
## الأسئلة الشائعة
### ما هو المرجع الدائري في Excel؟
يحدث المرجع الدائري عندما تشير الصيغة إلى الخلية الخاصة بها، مما يتسبب في حلقة لا نهاية لها في العمليات الحسابية.
### كيف يمكنني اكتشاف المراجع الدائرية برمجيا؟
بإمكانك استخدام مكتبة Aspose.Cells في .NET للكشف عن المراجع الدائرية برمجيًا عن طريق تنفيذ مراقب حسابات مخصص.
### ما هي المتطلبات الأساسية لاستخدام Aspose.Cells؟
يجب عليك تثبيت Visual Studio و.NET Framework ومكتبة Aspose.Cells.
### هل يمكنني استخدام Aspose.Cells مجانًا؟
نعم، يقدم Aspose.Cells نسخة تجريبية مجانية يمكنك استخدامها لاستكشاف ميزاته.
### أين يمكنني العثور على مزيد من المعلومات حول Aspose.Cells؟
 يمكنك زيارة[توثيق Aspose.Cells](https://reference.aspose.com/cells/net/) للحصول على معلومات مفصلة وأمثلة.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
