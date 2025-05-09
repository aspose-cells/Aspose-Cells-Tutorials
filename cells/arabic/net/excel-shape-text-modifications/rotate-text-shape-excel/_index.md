---
"description": "تعلّم كيفية تدوير النص مع الأشكال في Excel باستخدام Aspose.Cells لـ .NET. اتبع هذا الدليل خطوة بخطوة لعرض مثالي في Excel."
"linktitle": "تدوير النص مع الشكل في Excel"
"second_title": "واجهة برمجة تطبيقات معالجة Excel Aspose.Cells .NET"
"title": "تدوير النص مع الشكل في Excel"
"url": "/ar/net/excel-shape-text-modifications/rotate-text-shape-excel/"
"weight": 12
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# تدوير النص مع الشكل في Excel

## مقدمة
في عالم إكسل، يُعدّ التمثيل المرئي بنفس أهمية البيانات نفسها. سواء كنت تُنشئ تقريرًا أو تُصمّم لوحة معلومات ديناميكية، فإن طريقة عرض المعلومات تُؤثّر بشكل كبير على سهولة قراءتها ومظهرها العام. فهل رغبت يومًا في تدوير النص لمواءمته بشكل أنيق مع الأشكال؟ أنت محظوظ! في هذا البرنامج التعليمي، سنتناول بالتفصيل كيفية تدوير النص مع الأشكال باستخدام Aspose.Cells لـ .NET، مما يضمن أن تكون جداول بياناتك مُفيدة ومُلفتة للنظر.
## المتطلبات الأساسية
قبل أن نبدأ، دعونا نتأكد من أنك حصلت على كل ما تحتاجه:
1. Visual Studio: تأكد من تثبيت Visual Studio على جهازك، حيث سنكتب الكود الخاص بنا هناك.
2. Aspose.Cells لـ .NET: ستحتاج إلى مكتبة Aspose.Cells. يمكنك [قم بتنزيل الإصدار الأحدث هنا](https://releases.aspose.com/cells/net/) أو جربه مجانًا مع [نسخة تجريبية مجانية](https://releases.aspose.com/).
3. المعرفة الأساسية بلغة C#: ستكون المعرفة ببيئة C# و.NET مفيدة، على الرغم من أننا سنرشدك في كل خطوة على الطريق.
4. ملف Excel: ملف Excel نموذجي، دعنا نسميه `sampleRotateTextWithShapeInsideWorksheet.xlsx`لاختبار الكود الخاص بنا، يجب وضع هذا الملف في مجلد يسهل الوصول إليه.
هل جهزتم كل شيء؟ رائع! لننتقل إلى الجزء الممتع.
## استيراد الحزم
للبدء، نحتاج إلى استيراد الحزم اللازمة إلى مشروعنا. إليك كيفية القيام بذلك:
### إنشاء مشروع جديد
1. افتح Visual Studio.
2. حدد "إنشاء مشروع جديد".
3. اختر "تطبيق وحدة التحكم" ثم حدد C# كلغة البرمجة المفضلة لديك.
### تثبيت Aspose.Cells
الآن، لنُضِف Aspose.Cells إلى مشروعك. يمكنك القيام بذلك باستخدام مدير حزم NuGet:
1. افتح "الأدوات" في القائمة العلوية.
2. حدد "NuGet Package Manager" ثم "إدارة حزم NuGet للحل".
3. ابحث عن "Aspose.Cells."
4. انقر فوق "تثبيت" لإضافته إلى مشروعك.
### إضافة باستخدام التوجيه
في الجزء العلوي من ملف C# الرئيسي الخاص بك، تحتاج إلى إضافة التوجيه التالي:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Aspose.Cells.Drawing;
```
الآن أصبحنا جاهزين لبدء الترميز!
لنُقسّم العملية إلى خطوات سهلة الفهم. إليك كيفية تدوير النص باستخدام الأشكال في ملف Excel:
## الخطوة 1: إعداد مسارات الدليل الخاصة بك
أولاً، عليك إعداد مجلدات المصدر والإخراج لتخزين ملفات Excel. إليك الطريقة:
```csharp
//دليل المصدر
string sourceDir = "Your Document Directory"; // تعيين دليل المستندات الخاص بك
//دليل الإخراج
string outputDir = "Your Document Directory"; // قم بتعيين دليل الإخراج الخاص بك
```
يستبدل `"Your Document Directory"` مع المسار الفعلي الذي تريده `sampleRotateTextWithShapeInsideWorksheet.xlsx` تم العثور على الملف.
## الخطوة 2: تحميل ملف Excel النموذجي
الآن، لنحمّل ملف Excel النموذجي. هذا مهم جدًا، إذ نريد معالجة البيانات الموجودة.
```csharp
//تحميل ملف Excel العينة.
Workbook wb = new Workbook(sourceDir + "sampleRotateTextWithShapeInsideWorksheet.xlsx");
```
## الخطوة 3: الوصول إلى ورقة العمل
بعد تحميل الملف، نحتاج إلى الوصول إلى ورقة العمل المحددة التي نريد تعديلها. في حالتنا، هي ورقة العمل الأولى.
```csharp
//الوصول إلى ورقة العمل الأولى.
Worksheet ws = wb.Worksheets[0];
```
## الخطوة 4: تعديل الخلية
بعد ذلك، سنُعدِّل خليةً مُحدَّدةً لعرض رسالة. في مثالنا، سنستخدم الخلية B4.
```csharp
//قم بالوصول إلى الخلية B4 وأضف رسالة بداخلها.
Cell b4 = ws.Cells["B4"];
b4.PutValue("Text is not rotating with shape because RotateTextWithShape is false.");
```
تتعلق هذه الخطوة بالتواصل - التأكد من أن الشخص الذي يفتح هذه الورقة يفهم ما نقوم بتعديله.
## الخطوة 5: الوصول إلى الشكل الأول
لتدوير النص، نحتاج إلى شكل للعمل عليه. هنا، سنصل إلى الشكل الأول في ورقة العمل.
```csharp
//الوصول إلى الشكل الأول.
Shape sh = ws.Shapes[0];
```
## الخطوة 6: ضبط محاذاة نص الشكل
هنا يأتي السحر. سنضبط خصائص محاذاة النص للشكل.
```csharp
//الوصول إلى محاذاة نص الشكل.
Aspose.Cells.Drawing.Texts.ShapeTextAlignment shapeTextAlignment = sh.TextBody.TextAlignment;
//لا تقم بتدوير النص مع الشكل عن طريق تعيين RotateTextWithShape على False.
shapeTextAlignment.RotateTextWithShape = false;
```
عن طريق الإعداد `RotateTextWithShape` إلى خطأ، نتأكد من أن النص يظل مستقيمًا ولا يدور مع الشكل، وبالتالي نحافظ على كل شيء أنيقًا ومنظمًا.
## الخطوة 7: حفظ ملف Excel الناتج
أخيرًا، لنحفظ تغييراتنا في ملف إكسل جديد. هذا يضمن عدم فقدان تعديلاتنا والحصول على نتائج منظمة.
```csharp
//احفظ ملف Excel الناتج.
wb.Save(outputDir + "outputRotateTextWithShapeInsideWorksheet.xlsx");
```
وهذا كل شيء! تم الآن حفظ ملف الإخراج، بما في ذلك النص في الخلية B4 والتعديلات التي أجريتها على الشكل.
## الخطوة 8: تنفيذ الكود
فيك `Main` قم بتغليف جميع أجزاء الكود المذكورة أعلاه، ثم شغّل مشروعك. شاهد التغييرات تنعكس في ملف الإخراج!
```csharp
Console.WriteLine("RotateTextWithShapeInsideWorksheet executed successfully.");
```
## خاتمة
قد تبدو عملية تدوير النصوص مع الأشكال في Excel باستخدام Aspose.Cells لـ .NET عملية معقدة للوهلة الأولى، لكنها سهلة للغاية بمجرد فهمها. باتباع هذه الخطوات البسيطة، يمكنك تخصيص جداول بياناتك لتبدو أكثر احترافية وجاذبية بصريًا. الآن، سواء كنت تقوم بذلك لعميل أو لمشاريعك الشخصية، سيُشيد الجميع بجودة عملك!
## الأسئلة الشائعة
### هل يمكنني استخدام Aspose.Cells مجانًا؟
نعم! يمكنك استخدام [نسخة تجريبية مجانية](https://releases.aspose.com/) لتجربة المكتبة.
### ما هي إصدارات Excel التي يدعمها Aspose.Cells؟
يدعم Aspose.Cells مجموعة متنوعة من تنسيقات Excel، بما في ذلك XLS، وXLSX، وCSV، والمزيد.
### هل من الممكن تدوير النص مع الأشكال في إصدارات Excel القديمة؟
نعم، يمكن تطبيق الوظيفة على التنسيقات القديمة التي يدعمها Aspose.Cells.
### أين يمكنني العثور على مزيد من الوثائق حول Aspose.Cells؟
يمكنك استكشاف الشامل [التوثيق](https://reference.aspose.com/cells/net/) لمزيد من الأفكار.
### كيف أحصل على الدعم لـ Aspose.Cells؟
يمكنك طلب الدعم من خلال زيارة [منتدى Aspose](https://forum.aspose.com/c/cells/9).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}