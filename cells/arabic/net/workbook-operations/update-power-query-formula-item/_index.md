---
"description": "تعرف على كيفية تحديث صيغ Power Query في Excel باستخدام Aspose.Cells لـ .NET في هذا الدليل الشامل خطوة بخطوة."
"linktitle": "تحديث عنصر صيغة Power Query في المصنف"
"second_title": "واجهة برمجة تطبيقات معالجة Excel Aspose.Cells .NET"
"title": "تحديث عنصر صيغة Power Query في المصنف"
"url": "/ar/net/workbook-operations/update-power-query-formula-item/"
"weight": 27
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# تحديث عنصر صيغة Power Query في المصنف

## مقدمة
يُعد فهم كيفية إدارة البيانات بكفاءة باستخدام Power Query في Excel أمرًا بالغ الأهمية لأي محلل بيانات أو خبير في Excel. إذا احتجت يومًا إلى تحديث عناصر الصيغ في مصنف Power Query، فأنت في المكان المناسب. صُمم هذا الدليل لمساعدتك على تعلم كيفية استخدام Aspose.Cells for .NET لتحديث صيغ Power Query بسلاسة في مصنف Excel. بخطوات بسيطة، ستتمكن من معالجة بياناتك وتبسيطها، مما يضمن بقاء مصنفاتك ديناميكية ومركزية.
## المتطلبات الأساسية
قبل أن تبدأ في الغوص في كود المثال والخطوات، دعنا نستعرض ما ستحتاج إليه:
1. الفهم الأساسي لـ C# و.NET: سيكون من المفيد التعرف على مفاهيم البرمجة في C# لأننا سنكتب بعض التعليمات البرمجية.
2. تثبيت Aspose.Cells لـ .NET: يجب أن تكون مكتبة Aspose.Cells مدمجة في مشروع .NET الخاص بك. يمكنك تنزيلها. [هنا](https://releases.aspose.com/cells/net/).
3. ملف إكسل جاهز للتعديل: تأكد من وجود ملف إكسل يحتوي على استعلام Power Query الذي ترغب في تحديثه. ستحتاج إلى مصنف نموذجي مثل `SamplePowerQueryFormula.xlsx` تحت تصرفكم.
## استيراد الحزم
للبدء، تأكد من تضمين المساحات الأسماء التالية في ملف C# الخاص بك:
```csharp
using Aspose.Cells.DigitalSignatures;
using Aspose.Cells.QueryTables;
using System;
using System.IO;
```
سيسمح لك هذا بالوصول إلى الوظائف التي توفرها مكتبة Aspose.Cells، وخاصةً للعمل مع المصنفات وبيانات Power Query.
## الخطوة 1: إعداد أدلة العمل الخاصة بك
أولاً وقبل كل شيء، عليك تحديد مكان وجود ملفات المصدر والملفات الناتجة. 
```csharp
string SourceDir = "Your Document Directory";
string outputDir = "Your Document Directory";
```
في هذه الخطوة، يمكنك تحديد مسارات الدليل. استبدل `"Your Document Directory"` مع المسار الفعلي لحفظ ملفات Excel. يُحدد هذا البرنامج مكان البحث عن ملف المصدر ومكان حفظ الملف المُحدّث.
## الخطوة 2: تحميل المصنف
الآن بعد أن قمت بتعيين أدلة العمل الخاصة بك، فإن الخطوة التالية هي تحميل ملف Excel الخاص بك إلى البرنامج.
```csharp
Workbook workbook = new Workbook(SourceDir + "SamplePowerQueryFormula.xlsx");
```
هنا، يمكنك إنشاء `Workbook` الكائن الذي يقوم بتحميل ملف Excel المحدد. `Workbook` تعتبر الفئة جزءًا من مكتبة Aspose.Cells وهي ضرورية لأي عمليات ستقوم بتنفيذها على ملف Excel هذا.
## الخطوة 3: الوصول إلى بيانات Power Query
بمجرد تحميل المصنف، حان الوقت للوصول إلى صيغ Power Query المخزنة بداخله.
```csharp
DataMashup mashupData = workbook.DataMashup;
```
في هذا الخط، `DataMashup` تتيح لك هذه الخاصية الوصول إلى هياكل بيانات Power Query داخل المصنف. تتيح لك هذه الخاصية التفاعل مع جوانب مختلفة من بيانات Power Query الموجودة في ملف Excel.
## الخطوة 4: تكرار صيغ Power Query
بعد أن أصبحت بيانات Power Query متاحة، فإن الخطوة التالية هي تكرار كل الصيغ الموجودة.
```csharp
foreach (PowerQueryFormula formula in mashupData.PowerQueryFormulas)
{
    foreach (PowerQueryFormulaItem item in formula.PowerQueryFormulaItems)
    {
        if (item.Name == "Source")
        {
            item.Value = "Excel.Workbook(File.Contents(\"" + SourceDir + "SamplePowerQueryFormulaSource.xlsx\"), null, true)";
        }
    }
}
```
هنا حيث يحدث السحر. نكرر كل شيء `PowerQueryFormula` ومن ثم من خلال كل `PowerQueryFormulaItem`. ال `if` يبحث البيان عن عنصر الصيغة المسمى "المصدر" ويُحدِّث قيمته ليصبح مسار ملف المصدر الذي تريد أن يشير إليه Power Query. يتيح لك هذا تغيير الملف الذي يسحب Power Query البيانات منه ديناميكيًا.
## الخطوة 5: حفظ المصنف المحدث
بعد تحديث عناصر الصيغة الضرورية، فإن خطوتك الأخيرة هي حفظ المصنف.
```csharp
workbook.Save(outputDir + "SamplePowerQueryFormula_out.xlsx");
```
يحفظ هذا السطر المصنف المعدل في ملف جديد، وبالتالي يحافظ على الأصل مع السماح لك بالعمل مع الإصدار المحدث.
## الخطوة 6: رسالة التأكيد
وأخيرًا، من الجيد أن تتأكد من تنفيذ الكود الخاص بك بشكل صحيح.
```csharp
Console.WriteLine("UpdatePowerQueryFormulaItem executed successfully.");
```
ستؤكد لك هذه الرسالة البسيطة في وحدة التحكم أن عمليتك كانت ناجحة، مما يوفر نهاية مطمئنة للعملية.
## خاتمة
ها قد انتهيت! يمكنك تحديث عناصر صيغ Power Query في Excel باستخدام Aspose.Cells لـ .NET بخطوات بسيطة. باتباع هذا الدليل، يمكنك إدارة اتصالات بيانات Excel بكفاءة والحفاظ على سلاسة عمل مصنفاتك. سواء كنت محترفًا متمرسًا أو مبتدئًا في معالجة البيانات، يوفر Aspose.Cells طريقة فعّالة لأتمتة سير عمل Excel وتحسينه. 
## الأسئلة الشائعة
### هل يمكنني استخدام Aspose.Cells مع أي إصدار من .NET؟
يعد Aspose.Cells متوافقًا مع إصدارات متعددة من .NET، بما في ذلك .NET Framework و.NET Core.
### هل استخدام Aspose.Cells مجاني؟
يقدم Aspose.Cells نسخة تجريبية مجانية، ولكن للاستخدام المستمر، يلزم الحصول على ترخيص. يمكنك الحصول على ترخيص مؤقت. [هنا](https://purchase.aspose.com/temporary-license/).
### ماذا لو كان ملف Excel الحالي الخاص بي لا يحتوي على Power Query؟
ترتكز العملية الموضحة على تحديث عناصر Power Query، لذا إذا كان ملفك يفتقر إليها، فستحتاج إلى دمج Power Query أولاً.
### أين يمكنني العثور على مزيد من المعلومات حول Aspose.Cells؟
راجع الوثائق للحصول على إرشادات شاملة وأمثلة. تفضل بزيارة [التوثيق](https://reference.aspose.com/cells/net/).
### كيف يمكنني الإبلاغ عن الأخطاء أو المشكلات المتعلقة بـ Aspose.Cells؟
يمكنك التواصل مع المنتدى المدعوم لديهم للحصول على المساعدة فيما يتعلق بأي مشكلات تواجهها.


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}