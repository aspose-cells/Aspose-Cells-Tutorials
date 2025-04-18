---
title: إضافة عنصر التحكم Spinner إلى ورقة العمل في Excel
linktitle: إضافة عنصر التحكم Spinner إلى ورقة العمل في Excel
second_title: واجهة برمجة تطبيقات معالجة Excel الخاصة بـ Aspose.Cells .NET
description: تعرف على كيفية إضافة عنصر تحكم Spinner إلى ورقة عمل Excel باستخدام Aspose.Cells لـ .NET في هذا البرنامج التعليمي خطوة بخطوة.
weight: 23
url: /ar/net/excel-shapes-controls/add-spinner-control-to-worksheet-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إضافة عنصر التحكم Spinner إلى ورقة العمل في Excel

## مقدمة
إذا كنت تتعمق في عالم أتمتة Excel باستخدام .NET، فربما صادفت الحاجة إلى عناصر تحكم أكثر تفاعلية داخل جداول البيانات الخاصة بك. أحد هذه العناصر هو Spinner، الذي يسمح للمستخدمين بزيادة أو تقليل قيمة بسهولة. في هذا البرنامج التعليمي، سنستكشف كيفية إضافة عنصر تحكم Spinner إلى ورقة عمل Excel باستخدام Aspose.Cells لـ .NET. سنقسمها إلى خطوات سهلة الفهم حتى تتمكن من متابعتها بسلاسة. 
## المتطلبات الأساسية
قبل أن ننتقل إلى الكود، دعنا نتأكد من إعداد كل شيء للحصول على تجربة سلسة:
1.  Aspose.Cells لـ .NET: تأكد من أن لديك مكتبة Aspose.Cells. إذا لم تقم بتثبيتها بعد، يمكنك الحصول على أحدث إصدار من[رابط التحميل](https://releases.aspose.com/cells/net/).
2. Visual Studio: يجب أن يكون لديك تثبيت عمل لبرنامج Visual Studio أو أي .NET IDE آخر تفضله.
3. المعرفة الأساسية بلغة C#: ستساعدك المعرفة ببرمجة C# على فهم مقتطفات التعليمات البرمجية بسهولة. إذا كنت قد بدأت للتو، فلا تقلق! سأشرح لك كل جزء.
## استيراد الحزم
لاستخدام Aspose.Cells في مشروعك، تحتاج إلى استيراد المساحات الأساسية اللازمة. إليك كيفية إعداد بيئتك:
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
```
تتيح لك مساحات الأسماء هذه الوصول إلى الوظائف الأساسية لـ Aspose.Cells، بما في ذلك معالجة المصنف وإمكانيات الرسم للأشكال مثل Spinner.
الآن بعد أن قمنا بتغطية المتطلبات الأساسية واستيراد الحزم اللازمة، فلننتقل إلى الدليل خطوة بخطوة. تم تصميم كل خطوة لتكون واضحة وموجزة حتى تتمكن من تنفيذها بسهولة.
## الخطوة 1: إعداد دليل المشروع الخاص بك
قبل أن تبدأ في كتابة التعليمات البرمجية، من الجيد أن تنظم ملفاتك. فلنبدأ بإنشاء دليل لملفات Excel الخاصة بنا.
```csharp
// المسار إلى دليل المستندات.
string dataDir = "Your Document Directory";
// إنشاء الدليل إذا لم يكن موجودًا بالفعل.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
هنا، نحدد مسارًا لدليل المستندات الخاص بنا. إذا لم يكن الدليل موجودًا، نقوم بإنشائه. يضمن هذا أن جميع الملفات التي تم إنشاؤها لها منزل محدد.
## الخطوة 2: إنشاء مصنف جديد
الآن حان الوقت لإنشاء مصنف Excel حيث سنضيف عنصر التحكم Spinner الخاص بنا.
```csharp
// إنشاء مصنف جديد.
Workbook excelbook = new Workbook();
```
 ال`Workbook` تمثل الفئة ملف Excel. من خلال إنشائها، نقوم بإنشاء مصنف جديد جاهز للتعديل.
## الخطوة 3: الوصول إلى ورقة العمل الأولى
سوف نضيف Spinner الخاص بنا إلى ورقة العمل الأولى في المصنف.
```csharp
// احصل على ورقة العمل الأولى.
Worksheet worksheet = excelbook.Worksheets[0];
```
يؤدي هذا السطر إلى الوصول إلى ورقة العمل الأولى (الفهرس 0) من مصنفنا. يمكنك الحصول على أوراق عمل متعددة، ولكن في هذا المثال، سنبقي الأمر بسيطًا.
## الخطوة 4: العمل مع الخلايا
بعد ذلك، دعنا نعمل على الخلايا الموجودة في ورقة العمل الخاصة بنا. وسنحدد بعض القيم والأنماط.
```csharp
// احصل على خلايا ورقة العمل.
Cells cells = worksheet.Cells;
// أدخل قيمة السلسلة في الخلية A1.
cells["A1"].PutValue("Select Value:");
// تعيين لون الخط للخلية.
cells["A1"].GetStyle().Font.Color = Color.Red;
// تعيين خط النص عريضًا.
cells["A1"].GetStyle().Font.IsBold = true;
// أدخل القيمة في الخلية A2.
cells["A2"].PutValue(0);
```
هنا، نقوم بملء الخلية A1 بمطالبة، وتطبيق لون أحمر، وجعل النص غامقًا. كما نقوم أيضًا بتعيين الخلية A2 إلى قيمة أولية 0، والتي سيتم ربطها بـ Spinner.
## الخطوة 5: تصميم الخلية A2
بعد ذلك، دعنا نطبق بعض الأنماط على الخلية A2 لجعلها أكثر جاذبية بصريًا.
```csharp
// ضبط لون التظليل إلى اللون الأسود مع خلفية صلبة.
cells["A2"].GetStyle().ForegroundColor = Color.Black;
cells["A2"].GetStyle().Pattern = BackgroundType.Solid;
// تعيين لون الخط للخلية.
cells["A2"].GetStyle().Font.Color = Color.White;
// تعيين خط النص عريضًا.
cells["A2"].GetStyle().Font.IsBold = true;
```
نضيف خلفية سوداء بنمط متين إلى الخلية A2 ونضبط لون الخط إلى الأبيض. وهذا التباين سيجعله بارزًا في ورقة العمل.
## الخطوة 6: إضافة عنصر التحكم الدوار
الآن، أصبحنا جاهزين لإضافة عنصر التحكم Spinner إلى ورقة العمل الخاصة بنا.
```csharp
// إضافة عنصر التحكم الدوار.
Aspose.Cells.Drawing.Spinner spinner = excelbook.Worksheets[0].Shapes.AddSpinner(1, 0, 1, 0, 20, 18);
```
يضيف هذا السطر عنصر تحكم Spinner إلى ورقة العمل. تحدد المعلمات موضع وحجم Spinner (الصف، العمود، العرض، الارتفاع).
## الخطوة 7: تكوين خصائص الدوار
دعونا نقوم بتخصيص سلوك Spinner ليناسب احتياجاتنا.
```csharp
// ضبط نوع وضع الدوار.
spinner.Placement = PlacementType.FreeFloating;
// تعيين الخلية المرتبطة بالتحكم.
spinner.LinkedCell = "A2";
// تعيين الحد الأقصى للقيمة.
spinner.Max = 10;
//تعيين الحد الأدنى للقيمة.
spinner.Min = 0;
// تعيين تغيير الزيادة لعنصر التحكم.
spinner.IncrementalChange = 2;
// ضبط التظليل ثلاثي الأبعاد.
spinner.Shadow = true;
```
هنا، نقوم بتعيين خصائص Spinner. نقوم بربطه بالخلية A2، مما يسمح له بالتحكم في القيمة المعروضة هناك. تحدد القيم الدنيا والقصوى النطاق الذي يمكن لـ Spinner العمل ضمنه، بينما يحدد التغيير التدريجي مقدار تغير القيمة مع كل نقرة. إضافة تظليل ثلاثي الأبعاد يمنحه مظهرًا مصقولًا.
## الخطوة 8: حفظ ملف Excel
أخيرًا، دعنا نحفظ مصنف Excel الخاص بنا مع تضمين Spinner.
```csharp
// احفظ ملف Excel.
excelbook.Save(dataDir + "book1.out.xls");
```
يحفظ هذا الأمر المصنف في الدليل المحدد. ويمكنك تغيير اسم الملف حسب الحاجة.
## خاتمة
والآن، لقد نجحت في إضافة عنصر تحكم Spinner إلى ورقة عمل Excel باستخدام Aspose.Cells for .NET. يعمل هذا العنصر التفاعلي على تحسين تجربة المستخدم من خلال السماح بإجراء تعديلات سريعة على القيم. سواء كنت تقوم بإنشاء أداة إعداد تقارير ديناميكية أو نموذج إدخال بيانات، يمكن أن يكون عنصر التحكم Spinner إضافة قيمة. 
## الأسئلة الشائعة
### ما هو عنصر التحكم Spinner في Excel؟
يتيح عنصر التحكم Spinner للمستخدمين زيادة أو تقليل قيمة رقمية بسهولة، مما يوفر طريقة بديهية لإجراء التحديدات.
### هل يمكنني تخصيص مظهر Spinner؟
نعم، يمكنك تعديل حجمه وموقعه وحتى تظليله ثلاثي الأبعاد للحصول على مظهر أكثر أناقة.
### هل أحتاج إلى ترخيص لاستخدام Aspose.Cells؟
 يقدم Aspose.Cells نسخة تجريبية مجانية، ولكن يلزم الحصول على ترخيص مدفوع للاستخدام الإنتاجي. تحقق من[خيارات الشراء](https://purchase.aspose.com/buy).
### كيف يمكنني الحصول على المساعدة مع Aspose.Cells؟
 للحصول على الدعم، قم بزيارة[منتدى اسبوس](https://forum.aspose.com/c/cells/9) حيث يمكنك طرح الأسئلة والعثور على الإجابات.
### هل من الممكن إضافة عدة غزالات إلى نفس ورقة العمل؟
بالتأكيد! يمكنك إضافة عدد لا حصر له من الدوارات باتباع نفس الخطوات لكل عنصر تحكم.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
