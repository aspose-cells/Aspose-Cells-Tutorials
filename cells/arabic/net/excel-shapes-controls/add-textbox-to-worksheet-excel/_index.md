---
"description": "تعرف على كيفية إضافة مربعات نص قابلة للتخصيص إلى Excel باستخدام Aspose.Cells لـ .NET في هذا البرنامج التعليمي خطوة بخطوة."
"linktitle": "إضافة مربع نص إلى ورقة العمل في Excel"
"second_title": "واجهة برمجة تطبيقات معالجة Excel Aspose.Cells .NET"
"title": "إضافة مربع نص إلى ورقة العمل في Excel"
"url": "/ar/net/excel-shapes-controls/add-textbox-to-worksheet-excel/"
"weight": 14
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# إضافة مربع نص إلى ورقة العمل في Excel

## مقدمة
هل ترغب في تحسين جداول بيانات Excel الخاصة بك بعناصر مرئية فريدة تجذب جمهورك؟ إضافة مربعات نصية طريقة رائعة لتحقيق ذلك! مع Aspose.Cells لـ .NET، يمكنك بسهولة دمج مربعات النص في جداول بيانات Excel، مما يجعل مستنداتك أكثر إفادة وجاذبية بصريًا. سيرشدك هذا الدليل خطوة بخطوة خلال عملية إضافة مربعات النص البسيطة باستخدام Aspose.Cells، موضحًا كيفية تخصيصها بالنص والألوان والروابط التشعبية والمزيد!
## المتطلبات الأساسية
قبل أن نتعمق في روعة البرمجة، إليك المتطلبات الأساسية لضمان تجربة إبحار سلسة:
1. بيئة تطوير .NET: ستحتاج إلى إطار عمل .NET فعال، بالإضافة إلى بيئة تطوير متكاملة مثل Visual Studio. تأكد من تحديثه إلى أحدث إصدار!
2. Aspose.Cells لـ .NET: تأكد من تنزيل مكتبة Aspose.Cells. يمكنك الحصول على أحدث إصدار من [هنا](https://releases.aspose.com/cells/net/).
3. معرفة البرمجة الأساسية: الإلمام بلغة C# وبعض المفاهيم العامة للتعامل مع ملفات Excel سوف يجعل هذا البرنامج التعليمي أسهل!
## استيراد الحزم
تأكد من استيراد الحزم اللازمة في بداية ملف C#. إليك كيفية القيام بذلك:
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
```
## تثبيت Aspose.Cells
إذا لم تقم بذلك بالفعل، فيمكنك إضافة Aspose.Cells من خلال NuGet Package Manager في Visual Studio:
1. افتح Visual Studio.
2. اذهب الى `Tools` -> `NuGet Package Manager` -> `Manage NuGet Packages for Solution`.
3. ابحث عن "Aspose.Cells" وقم بتثبيته لمشروعك.
الآن بعد أن وضعنا الأساس، دعونا ننتقل إلى الجزء الممتع!
## الخطوة 1: إعداد دليل المستندات الخاص بك
أولاً، لنُنشئ المجلد الذي ستُخزَّن فيه جميع مستندات Excel. من الضروري التأكد من وجود هذا المجلد قبل البدء في إنشاء مصنفنا.
```csharp
// المسار إلى دليل المستندات.
string dataDir = "Your Document Directory"; 
// إنشاء الدليل إذا لم يكن موجودًا بالفعل.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists) 
    System.IO.Directory.CreateDirectory(dataDir);
```
سيؤدي مقتطف التعليمات البرمجية هذا إلى إنشاء دليل باسم `Your Document Directory` (يرجى استبدال هذا بمسارك الحالي) إذا لم يكن موجودًا بالفعل. الأمر سهل للغاية، أليس كذلك؟
## الخطوة 2: إنشاء مصنف جديد
بعد ذلك، علينا إنشاء مصنف جديد لإضافة مربعات النص. يُمكن القيام بذلك بسهولة باستخدام بضعة أسطر من التعليمات البرمجية:
```csharp
// إنشاء مصنف جديد.
Workbook workbook = new Workbook();
```
هذا السطر من التعليمات البرمجية يُنشئ مصنف إكسل جديدًا. بسيط ومباشر!
## الخطوة 3: الوصول إلى ورقة العمل الأولى
الآن بعد أن أصبح المصنف جاهزًا، فلنبدأ في الحصول على ورقة العمل الأولى التي سنضيف إليها مربع النص:
```csharp
// احصل على ورقة العمل الأولى في الكتاب.
Worksheet worksheet = workbook.Worksheets[0];
```
بهذه الطريقة، أصبح لديك الآن إمكانية الوصول إلى ورقة العمل الأولى المسماة `worksheet`حان الوقت لجعله يلمع!
## الخطوة 4: إضافة مربع نص
حسنًا، حان وقت إضافة مربع النص الأول! إليك الطريقة:
```csharp
// أضف مربع نص جديد إلى المجموعة.
int textboxIndex = worksheet.TextBoxes.Add(2, 1, 160, 200);
```
في هذا السطر، نحدد الصف والعمود اللذين سيوضع فيهما مربع النص، بالإضافة إلى ضبط عرضه وارتفاعه (160 و200 على التوالي). يمكنك تعديل هذه الأرقام بما يتناسب مع تصميمك!
## الخطوة 5: الحصول على كائن مربع النص
بعد إضافة مربع النص، نحتاج إلى الحصول على مرجع له حتى نتمكن من تخصيص محتواه:
```csharp
// احصل على كائن مربع النص.
Aspose.Cells.Drawing.TextBox textbox0 = worksheet.TextBoxes[textboxIndex];
```
الآن، `textbox0` هذه هي تذكرتك الذهبية لتعديل مربع النص هذا!
## الخطوة 6: ملء مربع النص بالمحتوى
بعد ذلك، دعنا نقدم بعض النصوص لمربع النص:
```csharp
// إملأ النص.
textbox0.Text = "ASPOSE______The .NET & JAVA Component Publisher!";
```
إدراج النص في مربع النص الخاص بك هو بهذه البساطة! 
## الخطوة 7: تخصيص مظهر مربع النص
ما رأيك بتحسينه قليلًا؟ يمكنك تعديل ألوان الخطوط وأنماطها والمزيد!
```csharp
// ضبط لون الخط.
textbox0.Font.Color = Color.Blue;
// ضبط الخط إلى غامق.
textbox0.Font.IsBold = true;
// ضبط حجم الخط.
textbox0.Font.Size = 14;
// تعيين سمة الخط إلى مائل.
textbox0.Font.IsItalic = true;
```
لا تتردد في اللعب بألوان وأنماط مختلفة لترى ما هو الأفضل بصريًا!
## الخطوة 8: إضافة ارتباط تشعبي
هل تريد تحويل مربع النص إلى رابط قابل للنقر؟ لنقم بذلك:
```csharp
// أضف ارتباطًا تشعبيًا إلى مربع النص.
textbox0.AddHyperlink("http://www.aspose.com/");
```
الآن، أي شخص ينقر على مربع النص الخاص بك، سينتقل إلى موقع Aspose الإلكتروني. إنه أشبه بالسحر!
## الخطوة 9: تعيين نوع وضع مربع النص
لديك خيارات مختلفة لكيفية ظهور مربع النص في ورقة العمل. إليك مثال لكيفية ضبطه ليكون عائمًا:
```csharp
// تعيين الموضع.
textbox0.Placement = PlacementType.FreeFloating;
```
وبدلاً من ذلك، إذا كنت تريد تغيير حجمه ونقله مع الخلايا، فيمكنك تعيينه على النحو التالي:
```csharp
// قم بتعيين نوع الموضع حيث سيتم نقل مربع النص وتغيير حجمه مع الخلايا.
textbox1.Placement = PlacementType.MoveAndSize;
```
## الخطوة 10: تخصيص تنسيقات الخطوط والتعبئة
إليك كيفية تغيير مظهر حدود مربع النص وتعبئته:
```csharp
// احصل على تنسيق التعبئة لمربع النص.
Aspose.Cells.Drawing.FillFormat fillformat = textbox0.Fill;            
// احصل على نوع تنسيق الخط لمربع النص.
Aspose.Cells.Drawing.LineFormat lineformat = textbox0.Line;           
// ضبط وزن الخط.
lineformat.Weight = 6;
// اضبط نمط الشرطة على نقطة مربعة.
lineformat.DashStyle = MsoLineDashStyle.SquareDot;
```
باستخدام هذا، يمكنك تخصيص مربع النص الخاص بك بشكل أكبر، وإضافة عناصر مرئية تناسب أسلوبك.
## الخطوة 11: إضافة مربع نص آخر
لم يقل أحد إنه بإمكاننا إضافة مربع نص واحد فقط! لنضع مربعًا آخر بنص مختلف:
```csharp
// أضف مربع نص آخر.
textboxIndex = worksheet.TextBoxes.Add(15, 4, 85, 120);
// احصل على مربع النص الثاني.
Aspose.Cells.Drawing.TextBox textbox1 = worksheet.TextBoxes[textboxIndex];
// أدخل بعض النص إليه.
textbox1.Text = "This is another simple text box";
```
أنت الآن تقوم بتزيين ورقة Excel الخاصة بك بمربعات نصية متعددة!
## الخطوة 12: حفظ المصنف الخاص بك
أخيرًا، حان وقت حفظ تحفتنا الفنية! إليكم آخر سطر من الكود لهذا اليوم:
```csharp
// احفظ ملف الاكسل.
workbook.Save(dataDir + "book1.out.xls");
```
باستخدام هذا السطر الواحد من التعليمات البرمجية، قمت بإنشاء ملف Excel وتعديله بمربعات نصية قابلة للتخصيص!
## خاتمة
تهانينا! لقد نجحت في استكشاف عالم مربعات النص في Excel باستخدام Aspose.Cells لـ .NET. لم تتعلم فقط كيفية إضافة مربع نص، بل تعلمت أيضًا كيفية تخصيصه لجعل جداول بياناتك أكثر جاذبية. من تغيير الألوان والأنماط إلى إضافة روابط تشعبية، الإمكانيات لا حصر لها! 
هل أنت مستعد لبدء تحويل مستندات Excel الخاصة بك؟ أطلق العنان لإبداعك، وجرّب تخطيطات مختلفة!
## الأسئلة الشائعة
### ما هو Aspose.Cells لـ .NET؟
Aspose.Cells for .NET هي مكتبة قوية تسمح للمطورين بإنشاء ملفات Excel ومعالجتها وتحويلها بسهولة.
### هل يمكنني تجربة Aspose.Cells قبل الشراء؟
نعم! يمكنك تنزيل واستخدام نسخة تجريبية مجانية. [هنا](https://releases.aspose.com/).
### أين يمكنني العثور على الوثائق الخاصة بـ Aspose.Cells؟
يمكنك الوصول إلى الوثائق الشاملة على [توثيق Aspose.Cells](https://reference.aspose.com/cells/net/).
### هل هناك دعم متاح إذا واجهت مشاكل؟
بالتأكيد! إذا كنت بحاجة إلى مساعدة، توجه إلى [منتدى أسبوزي](https://forum.aspose.com/c/cells/9) للحصول على المساعدة.
### هل يمكنني استخدام Aspose.Cells بدون ترخيص؟
يمكنك استخدام نسخة تجريبية مجانية، ولكن للاستفادة من جميع الوظائف، ستحتاج إلى شراء ترخيص. اطلع على الأسعار. [هنا](https://purchase.aspose.com/buy).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}