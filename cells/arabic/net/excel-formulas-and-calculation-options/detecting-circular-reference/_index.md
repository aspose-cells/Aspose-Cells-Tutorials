---
"description": "اكتشف بسهولة المراجع الدائرية في Excel باستخدام Aspose.Cells لـ .NET. اتبع دليلنا خطوة بخطوة لضمان دقة الحسابات في جداول البيانات."
"linktitle": "اكتشاف المرجع الدائري في Excel برمجيًا"
"second_title": "واجهة برمجة تطبيقات معالجة Excel Aspose.Cells .NET"
"title": "اكتشاف المرجع الدائري في Excel برمجيًا"
"url": "/ar/net/excel-formulas-and-calculation-options/detecting-circular-reference/"
"weight": 13
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# اكتشاف المرجع الدائري في Excel برمجيًا

## مقدمة
عند العمل مع ملفات Excel، تُعدّ المراجع الدائرية من أكثر المشاكل المزعجة التي قد تواجهها. يحدث هذا عندما تُرجع الصيغة إلى الخلية الخاصة بها، سواءً بشكل مباشر أو غير مباشر، مما يُؤدي إلى حلقة قد تُربك مُحرك العمليات الحسابية في Excel. لكن لا تقلق! مع Aspose.Cells لـ .NET، يُمكنك برمجيًا اكتشاف هذه المراجع الدائرية المُزعجة، مما يضمن بقاء جداول بياناتك عملية ودقيقة. في هذا الدليل، سنشرح لك العملية خطوة بخطوة، مُبسطة للغاية.
## المتطلبات الأساسية
قبل أن نتعمق في التفاصيل الدقيقة لكشف المراجع الدائرية، دعنا نتأكد من أن لديك كل ما تحتاجه للبدء:
1. Visual Studio: تأكد من تثبيت Visual Studio على جهازك. ستكون هذه بيئة التطوير الخاصة بك.
2. .NET Framework: تأكد من أنك تستخدم إصدارًا متوافقًا من .NET Framework (على الأقل .NET Framework 4.0).
3. مكتبة Aspose.Cells: يجب أن يكون لديك مكتبة Aspose.Cells. يمكنك تنزيلها من [موقع Aspose](https://releases.aspose.com/cells/net/).
4. المعرفة الأساسية بلغة C#: ستكون المعرفة ببرمجة C# مفيدة، حيث سنقوم بكتابة التعليمات البرمجية بهذه اللغة.
5. ملف إكسل: جهّز ملف إكسل يحتوي على مراجع دائرية للاختبار. يمكنك إنشاء ملف بسيط أو تنزيل نموذج.
الآن بعد أن وضعنا المتطلبات الأساسية في مكانها، فلننتقل إلى الجزء الممتع!
## استيراد الحزم
قبل البدء بالبرمجة، عليك استيراد الحزم اللازمة. إليك كيفية القيام بذلك:
### إنشاء مشروع جديد
- افتح Visual Studio وقم بإنشاء مشروع تطبيق وحدة التحكم C# جديد.
### إضافة مرجع Aspose.Cells
- انقر بزر الماوس الأيمن على مشروعك في مستكشف الحلول.
- حدد "إدارة حزم NuGet".
- ابحث عن "Aspose.Cells" وقم بتثبيت الإصدار الأحدث.
### استيراد مساحات الأسماء المطلوبة
في الجزء العلوي من `Program.cs` الملف، استيراد المساحات الأساسية اللازمة:
```csharp
using System;
using System.Collections;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

الآن بعد أن قمنا بإعداد كل شيء، دعنا ننتقل إلى الكود الخاص باكتشاف المراجع الدائرية في ملف Excel.
## الخطوة 1: تحديد دليل الإدخال
أولاً، عليك تحديد المجلد الذي يحتوي على ملف Excel. هنا سيتم تحميل ملف Excel.
```csharp
// دليل الإدخال
string sourceDir = "Your Document Directory";
```
يستبدل `"Your Document Directory"` مع المسار الفعلي لملف Excel الخاص بك.
## الخطوة 2: تحميل المصنف باستخدام LoadOptions
بعد ذلك، ستُحمّل مصنف Excel الخاص بك. وهنا تبدأ المغامرة!
```csharp
LoadOptions loadOptions = new LoadOptions();
var objWB = new Aspose.Cells.Workbook(sourceDir + "Circular Formulas.xls", loadOptions);
```
هنا، نقوم بإنشاء مثيل جديد لـ `LoadOptions` وحمّل المصنف من المسار المحدد. تأكد من تطابق اسم ملف Excel لديك!
## الخطوة 3: تمكين إعدادات التكرار
للسماح بالمراجع الدائرية، يجب عليك تمكين إعدادات التكرار في المصنف.
```csharp
objWB.Settings.Iteration = true;
```
يخبر هذا Aspose.Cells بالسماح بالمراجع الدائرية أثناء الحساب.
## الخطوة 4: إنشاء خيارات الحساب والمراقبة الدائرية
الآن، دعنا نقوم بإنشاء خيارات الحساب وشاشتنا الدائرية المخصصة.
```csharp
CalculationOptions copts = new CalculationOptions();
CircularMonitor cm = new CircularMonitor();
copts.CalculationMonitor = cm;
```
هنا، نقوم بإنشاء مثيل لـ `CalculationOptions` وعرف `CircularMonitor`ستساعدك هذه الشاشة على تتبع أي مراجع دائرية تم العثور عليها أثناء العمليات الحسابية.
## الخطوة 5: حساب الصيغ
الآن، حان الوقت لحساب الصيغ في المصنف الخاص بك.
```csharp
objWB.CalculateFormula(copts);
```
يقوم هذا الخط بتنفيذ الحساب والتحقق من المراجع الدائرية.
## الخطوة 6: حساب المراجع الدائرية
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
لإكمال العملية، ستحتاج إلى تنفيذ `CircularMonitor` الصف. هذه الفئة سوف ترث من `AbstractCalculationMonitor` والتعامل مع اكتشاف المراجع الدائرية.
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
يُعدّ اكتشاف المراجع الدائرية في Excel باستخدام Aspose.Cells لـ .NET عمليةً سهلةً بمجرد تقسيمها إلى خطواتٍ سهلة. باتباع هذا الدليل، يمكنك بسهولة تحديد المراجع الدائرية في جداول البيانات ومعالجتها، مما يضمن دقة حساباتك وموثوقيتها. سواءً كنت مطورًا محترفًا أو مبتدئًا، يوفر Aspose.Cells أدواتٍ فعّالة لتحسين قدراتك على التعامل مع Excel. 
## الأسئلة الشائعة
### ما هو المرجع الدائري في Excel؟
يحدث المرجع الدائري عندما تشير الصيغة إلى الخلية الخاصة بها، مما يتسبب في حلقة لا نهاية لها في العمليات الحسابية.
### كيف يمكنني اكتشاف المراجع الدائرية برمجيًا؟
بإمكانك استخدام مكتبة Aspose.Cells في .NET لاكتشاف المراجع الدائرية برمجيًا عن طريق تنفيذ مراقب حسابات مخصص.
### ما هي المتطلبات الأساسية لاستخدام Aspose.Cells؟
يجب أن يكون لديك Visual Studio، و.NET Framework، ومكتبة Aspose.Cells مثبتة.
### هل يمكنني استخدام Aspose.Cells مجانًا؟
نعم، يوفر Aspose.Cells نسخة تجريبية مجانية يمكنك استخدامها لاستكشاف ميزاته.
### أين يمكنني العثور على مزيد من المعلومات حول Aspose.Cells؟
يمكنك زيارة [توثيق Aspose.Cells](https://reference.aspose.com/cells/net/) لمزيد من المعلومات والأمثلة التفصيلية.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}