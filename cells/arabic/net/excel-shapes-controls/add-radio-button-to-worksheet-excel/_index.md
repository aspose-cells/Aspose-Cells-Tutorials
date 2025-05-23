---
"description": "تعرّف على كيفية إضافة أزرار اختيارية إلى ورقة عمل Excel باستخدام Aspose.Cells لـ .NET من خلال هذا الدليل السهل خطوة بخطوة. مثالي لإنشاء نماذج Excel تفاعلية."
"linktitle": "إضافة زر الاختيار إلى ورقة العمل في Excel"
"second_title": "واجهة برمجة تطبيقات معالجة Excel Aspose.Cells .NET"
"title": "إضافة زر الاختيار إلى ورقة العمل في Excel"
"url": "/ar/net/excel-shapes-controls/add-radio-button-to-worksheet-excel/"
"weight": 19
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# إضافة زر الاختيار إلى ورقة العمل في Excel

## مقدمة
هل تساءلت يومًا عن كيفية إضفاء لمسة مميزة على جداول بيانات Excel باستخدام عناصر تفاعلية مثل أزرار الاختيار؟ سواء كنت تُنشئ استبيانًا أو نموذجًا أو أداة تحليل، فإن إضافة أزرار الاختيار تُحسّن تفاعل المستخدم بشكل كبير. في هذا البرنامج التعليمي، سنشرح لك عملية إضافة أزرار الاختيار إلى جداول بيانات Excel باستخدام Aspose.Cells لـ .NET. سنُفصّل كل شيء في خطوات سهلة، مما يضمن لك الاحتراف بنهاية هذه المقالة. هل أنت مستعد للبدء؟ هيا بنا!
## المتطلبات الأساسية
قبل أن ننتقل إلى الجزء الممتع من إضافة أزرار الراديو، دعنا نتأكد من إعداد كل شيء للبدء.
1. Aspose.Cells لـ .NET: أولاً، تأكد من تنزيل وتثبيت [Aspose.Cells لـ .NET](https://releases.aspose.com/cells/net/) يمكنك الحصول عليها عبر NuGet في Visual Studio أو من صفحة التنزيل.
2. IDE (بيئة التطوير المتكاملة): ستحتاج إلى IDE مثل Visual Studio لكتابة وتنفيذ كود C# الخاص بك.
3. .NET Framework: تأكد من تثبيت .NET Framework 4.0 أو أحدث على جهازك. يتطلب Aspose.Cells هذا ليعمل.
4. الفهم الأساسي للغة C#: إن الإلمام بقواعد لغة C# وبرمجة .NET سيجعل الأمور أسهل أثناء متابعتك.
بمجرد وضع كل شيء في مكانه، فنحن جاهزون للانطلاق!
## استيراد الحزم
قبل البدء بالبرمجة، من الضروري استيراد مساحات الأسماء اللازمة لتجنب أي أخطاء لاحقًا. أضف ما يلي إلى الكود:
```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
using Aspose.Cells.Drawing;
```
تُعد هذه الاستيرادات ضرورية للوصول إلى وظائف المصنف، وإضافة أزرار الاختيار، ومعالجة عمليات الملف.
## الخطوة 1: إعداد المصنف
أولاً وقبل كل شيء، دعنا نقوم بإنشاء مصنف Excel جديد.
للبدء، ستحتاج إلى إنشاء مثيل جديد `Workbook` هذا الكائن سيمثل ملف Excel الخاص بك في الكود.
```csharp
// إنشاء مصنف جديد.
Workbook excelbook = new Workbook();
```
في هذه الخطوة، ستنشئ مصنفًا فارغًا. تخيّل أنه لوحة عمل فارغة ستضيف إليها أزرار الاختيار في الخطوات اللاحقة.
## الخطوة 2: إضافة قيمة خلية وتنسيقها
بعد ذلك، لنُضِف عنوانًا لورقة العمل. سنُضيف نصًا إلى الخلية `C2` ونسّقها لجعلها غامقة. هذه الخطوة تُضيف سياقًا لأزرار الاختيار.
### إدراج نص في الخلية
```csharp
// أدخل قيمة في الخلية C2.
excelbook.Worksheets[0].Cells["C2"].PutValue("Age Groups");
```
### جعل النص غامقًا
```csharp
// تعيين نص الخط في الخلية C2 إلى غامق.
excelbook.Worksheets[0].Cells["C2"].GetStyle().Font.IsBold = true;
```
هنا، أضفنا عنوانًا بسيطًا، "المجموعات العمرية"، في الخلية `C2`وجعلته جريئًا ليبرز. سهل، أليس كذلك؟
## الخطوة 3: إضافة زر الراديو الأول
الآن يأتي الجزء المثير: إضافة زر الاختيار الأول إلى ورقة العمل!
### إضافة زر راديو
```csharp
// أضف زر الاختيار إلى الورقة الأولى.
Aspose.Cells.Drawing.RadioButton radio1 = excelbook.Worksheets[0].Shapes.AddRadioButton(3, 0, 2, 0, 30, 110);
```
يضيف هذا السطر زر الاختيار إلى موضع محدد في ورقة العمل. تشير الأرقام إلى موضعه وحجمه. يشبه الأمر ضبط إحداثيات X وY للزر.
### تعيين نص زر الراديو
```csharp
// تعيين سلسلة النص الخاصة به.
radio1.Text = "20-29";
```
هنا، قمنا بإعطاء زر الاختيار تسمية "20-29"، والتي تمثل الفئة العمرية.
### ربط زر الراديو بخلية
```csharp
// تعيين الخلية A1 كخلية مرتبطة لزر الاختيار.
radio1.LinkedCell = "A1";
```
يربط هذا زر الاختيار بالخلية `A1`وهذا يعني أن نتيجة اختيار الزر سيتم تخزينها في تلك الخلية.
### إضافة تأثير ثلاثي الأبعاد
```csharp
// جعل زر الراديو ثلاثي الأبعاد.
radio1.Shadow = true;
```
نظرًا لأننا نريد أن يظهر زر الراديو هذا، فقد أضفنا تأثيرًا ثلاثي الأبعاد.
### تخصيص خط زر الراديو
```csharp
// ضبط وزن خط زر الراديو.
radio1.Line.Weight = 4;
// تعيين نمط الشرطة لخط زر الاختيار.
radio1.Line.DashStyle = MsoLineDashStyle.Solid;
```
تعمل أسطر التعليمات البرمجية هذه على ضبط سمك ونمط حدود زر الاختيار لجعله أكثر جاذبية من الناحية البصرية.
## الخطوة 4: إضافة أزرار راديو إضافية
لنُضِف زري اختيار إضافيين للفئات العمرية المتبقية: "30-39" و"40-49". الخطوات هي نفسها، مع اختلافات طفيفة في الإحداثيات والتسميات.
### إضافة زر الاختيار الثاني
```csharp
// أضف زر اختيار آخر إلى الورقة الأولى.
Aspose.Cells.Drawing.RadioButton radio2 = excelbook.Worksheets[0].Shapes.AddRadioButton(6, 0, 2, 0, 30, 110);
// تعيين سلسلة النص الخاصة به.
radio2.Text = "30-39";
// تعيين الخلية A1 كخلية مرتبطة لزر الاختيار.
radio2.LinkedCell = "A1";
// جعل زر الراديو ثلاثي الأبعاد.
radio2.Shadow = true;
// ضبط وزن زر الراديو.
radio2.Line.Weight = 4;
// تعيين نمط الشرطة لزر الاختيار.
radio2.Line.DashStyle = MsoLineDashStyle.Solid;
```
### إضافة زر الاختيار الثالث
```csharp
// أضف زر اختيار آخر إلى الورقة الأولى.
Aspose.Cells.Drawing.RadioButton radio3 = excelbook.Worksheets[0].Shapes.AddRadioButton(9, 0, 2, 0, 30, 110);
// تعيين سلسلة النص الخاصة به.
radio3.Text = "40-49";
// تعيين الخلية A1 كخلية مرتبطة لزر الاختيار.
radio3.LinkedCell = "A1";
// جعل زر الراديو ثلاثي الأبعاد.
radio3.Shadow = true;
// ضبط وزن زر الراديو.
radio3.Line.Weight = 4;
// تعيين نمط الشرطة لزر الاختيار.
radio3.Line.DashStyle = MsoLineDashStyle.Solid;
```
## الخطوة 5: حفظ ملف Excel
بمجرد إضافة جميع أزرار الراديو وتنسيقها، حان الوقت لحفظ الملف.
```csharp
// احفظ ملف الاكسل.
string dataDir = "Your Document Directory";
excelbook.Save(dataDir + "book1.out.xls");
```
في هذه الخطوة، يُحفظ المصنف في المجلد المُحدد. الأمر بهذه البساطة - ورقة العمل التفاعلية جاهزة الآن!
## خاتمة
هذا كل ما في الأمر! لقد أضفتَ للتو أزرار اختيار إلى ورقة عمل Excel باستخدام Aspose.Cells لـ .NET. غطّى هذا البرنامج التعليمي كل شيء، بدءًا من إعداد المصنف، وإدراج قيمة وتنسيقها، وإضافة أزرار اختيار متعددة، وربطها بخلية. الآن، أنت جاهز لإنشاء جداول بيانات Excel تفاعلية، ليس فقط بمظهرها الرائع، بل أيضًا بتجربة مستخدم مُحسّنة. استمتع باستكشاف المزيد من الإمكانيات مع Aspose.Cells!
## الأسئلة الشائعة
### هل يمكنني إضافة المزيد من أزرار الاختيار إلى أوراق مختلفة؟  
بالتأكيد! يمكنك تكرار العملية على أي ورقة عمل بتحديد فهرس ورقة العمل الصحيح.
### هل يمكنني تخصيص مظهر أزرار الراديو بشكل أكبر؟  
نعم، يوفر Aspose.Cells مجموعة متنوعة من خيارات التخصيص، بما في ذلك تغيير الألوان والأحجام وسمات التنسيق الأخرى.
### كيف يمكنني معرفة زر الراديو المحدد؟  
ستعرض الخلية المرتبطة (مثل A1) مؤشر زر الاختيار المحدد. يمكنك التحقق من قيمة الخلية المرتبطة لمعرفة أيها محدد.
### هل هناك حد لعدد أزرار الاختيار التي يمكنني إضافتها؟  
لا، لا يوجد حد أقصى لعدد أزرار الاختيار التي يمكنك إضافتها. مع ذلك، يُنصح بجعل الواجهة سهلة الاستخدام.
### هل يمكنني استخدام Aspose.Cells مع لغات برمجة أخرى؟  
نعم، يدعم Aspose.Cells لغات برمجة متعددة، بما فيها Java. لكن هذا البرنامج التعليمي يركز تحديدًا على .NET.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}