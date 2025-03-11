---
title: تعيين هوامش للتعليق أو الشكل في Excel
linktitle: تعيين هوامش للتعليق أو الشكل في Excel
second_title: واجهة برمجة تطبيقات معالجة Excel الخاصة بـ Aspose.Cells .NET
description: تعرف على كيفية تعيين هوامش للتعليقات والأشكال في Excel باستخدام Aspose.Cells for .NET. يتضمن دليلًا خطوة بخطوة لسهولة التنفيذ.
weight: 18
url: /ar/net/excel-shape-text-modifications/set-margins-comment-shape-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تعيين هوامش للتعليق أو الشكل في Excel

## مقدمة
عندما يتعلق الأمر بالتعامل مع ملفات Excel في تطبيقات .NET، يقدم Aspose.Cells حلاً قويًا. سواء كنت مطورًا يبحث عن معالجة مستندات Excel أو متحمسًا يهدف إلى تبسيط سير عملك، فإن معرفة كيفية تعيين الهوامش للتعليقات أو الأشكال في Excel يمكن أن ترفع من مستوى مشروعك. سيرشدك هذا البرنامج التعليمي خطوة بخطوة، مما يضمن لك فهم "الكيفية" و"السبب" وراء هذه الوظيفة.
## المتطلبات الأساسية
قبل الانطلاق في مغامرة البرمجة، دعنا نتأكد من أنك مجهز بكل ما تحتاجه لتنفيذ هذا البرنامج التعليمي بنجاح.
### المعرفة الأساسية
يجب أن يكون لديك فهم أساسي لـ C# و.NET. تم تصميم هذا البرنامج التعليمي خصيصًا لأولئك الذين لديهم على الأقل فهم أساسي لمفاهيم البرمجة.
### إعداد البيئة
1. Visual Studio: تأكد من تثبيت Visual Studio. فهو بيئة تطوير تبسط عملية الترميز.
2.  مكتبة Aspose.Cells: أنت بحاجة إلى مكتبة Aspose.Cells. إذا لم تكن قد قمت بتنزيلها بالفعل، يمكنك تنزيلها[هنا](https://releases.aspose.com/cells/net/).
3. ملف Excel نموذجي: قم بإنشاء ملف Excel نموذجي أو تنزيله. في هذا البرنامج التعليمي، سنستخدم ملفًا باسم`sampleSetMarginsOfCommentOrShapeInsideTheWorksheet.xlsx`.
## استيراد الحزم
تتضمن الخطوة الأولى في رحلتنا استيراد الحزم اللازمة. ستحتاج إلى تضمين مساحات أسماء Aspose.Cells في مشروعك. سيمنحك هذا إمكانية الوصول إلى جميع الوظائف التي يوفرها Aspose.Cells.
### افتح مشروعك
افتح Visual Studio ومشروعك الحالي الذي ستنفذ فيه وظيفة Aspose.Cells.
### إضافة مرجع إلى Aspose.Cells
لاستخدام Aspose.Cells، عليك إضافته كمرجع. اتبع الخطوات البسيطة التالية:
1. انقر بزر الماوس الأيمن على مشروعك في مستكشف الحلول.
2. حدد "إدارة حزم NuGet".
3. ابحث عن "Aspose.Cells" وانقر على زر التثبيت.
4. تأكد من اكتمال التثبيت دون أخطاء.
### تضمين استخدام التوجيهات
في الجزء العلوي من ملف C# الخاص بك، قم بتضمين المساحات التالية:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Aspose.Cells.Drawing;
```
يتيح لك هذا الوصول إلى جميع الفئات والوظائف المتعلقة بـ Excel.

الآن يأتي الجزء المثير: التنفيذ الفعلي! فيما يلي شرح تفصيلي لكيفية تعيين الهوامش للتعليقات أو الأشكال داخل ورقة عمل Excel باستخدام Aspose.Cells.
## الخطوة 1: قم بتحديد الدلائل الخاصة بك
قبل القيام بأي شيء بملف Excel الخاص بك، نحتاج إلى تحديد مكان وجوده والمكان الذي سنحفظ فيه الملف المعدل.
```csharp
//دليل المصدر
string sourceDir = "Your Document Directory";
//دليل الإخراج
string outputDir = "Your Document Directory";
```
تأكد من استبداله`"Your Document Directory"` مع المسار الفعلي الذي يتم تخزين ملفاتك فيه.
## الخطوة 2: تحميل ملف Excel
 في هذه الخطوة، سنفتح ملف Excel الذي نخطط للعمل عليه. فلنستغل قوة`Workbook` فصل.
```csharp
Workbook wb = new Workbook(sourceDir + "sampleSetMarginsOfCommentOrShapeInsideTheWorksheet.xlsx");
```
يقوم هذا السطر من التعليمات البرمجية بتحميل ملف Excel الخاص بك في الذاكرة، مما يمهد الطريق لإجراء التعديلات.
## الخطوة 3: الوصول إلى ورقة العمل
بعد ذلك، نحتاج إلى الوصول إلى ورقة العمل المحددة التي تحتوي على الأشكال أو التعليقات. سنعمل بورقة العمل الأولى لتبسيط الأمر.
```csharp
Worksheet ws = wb.Worksheets[0];
```
يستهدف هذا الكود ورقة العمل الأولى، والتي تم فهرستها عند 0.
## الخطوة 4: التكرار عبر الأشكال
الآن، نحتاج إلى تكرار كل الأشكال الموجودة في ورقة العمل. سيسمح لنا هذا بتطبيق إعدادات الهامش على كل شكل نجده.
```csharp
foreach (Shape sh in ws.Shapes)
```
نحن نستخدم حلقة foreach هنا. إنها طريقة بسيطة للتعامل مع كل شكل على حدة.
## الخطوة 5: ضبط محاذاة النص
قد يكون لكل شكل إعداد محاذاة نحتاج إلى تعديله. هنا، نصل إلى محاذاة نص الشكل ونحدد أننا سنقوم بتعيين الهوامش يدويًا.
```csharp
Aspose.Cells.Drawing.Texts.ShapeTextAlignment txtAlign = sh.TextBody.TextAlignment;
txtAlign.IsAutoMargin = false;
```
 عن طريق الإعداد`IsAutoMargin`إلى خطأ، لدينا الآن السيطرة على الهوامش.
## الخطوة 6: تعيين الهوامش
هذه هي الخطوة الحاسمة التي نحدد فيها الهوامش. يمكنك تخصيص هذه القيم وفقًا لاحتياجاتك.
```csharp
txtAlign.TopMarginPt = 10;
txtAlign.LeftMarginPt = 10;
txtAlign.BottomMarginPt = 10;
txtAlign.RightMarginPt = 10;
```
في هذا المثال، نقوم بتعيين جميع الهوامش بشكل موحد إلى 10 نقاط. لا تتردد في تعديل هذه القيم. 
## الخطوة 7: احفظ ملف Excel المعدّل
بمجرد إجراء التغييرات، حان الوقت لحفظ ملف Excel. فلنقم بذلك!
```csharp
wb.Save(outputDir + "outputSetMarginsOfCommentOrShapeInsideTheWorksheet.xlsx");
```
سيحفظ هذا السطر ملفك المعدّل في دليل الإخراج الذي حددته مسبقًا.
## الخطوة 8: تأكيد الإخراج
أخيرًا، من الجيد دائمًا أن تعرف أن كل شيء سار بسلاسة. سيؤكد لك إخراج بسيط من وحدة التحكم أن العملية كانت ناجحة.
```csharp
Console.WriteLine("SetMarginsOfCommentOrShapeInsideTheWorksheet executed successfully.");
```
## خاتمة
تهانينا! لقد تعلمت للتو كيفية تعيين هوامش للتعليقات أو الأشكال في Excel باستخدام Aspose.Cells for .NET. لا تعمل هذه الوظيفة على منح مستندات Excel مظهرًا مصقولًا فحسب، بل إنها تعمل أيضًا على تحسين قابلية القراءة، مما يضمن عرض بياناتك بوضوح. سواء كنت تقوم بتطوير تطبيق يقوم بأتمتة مهام إعداد التقارير أو ببساطة تحسين مشاريعك، فمن المؤكد أن هذه المعرفة ستكون مفيدة.
## الأسئلة الشائعة
### ما هو Aspose.Cells؟
Aspose.Cells عبارة عن مكتبة .NET مصممة لإنشاء ملفات Excel ومعالجتها وتحويلها دون الحاجة إلى تثبيت Microsoft Excel.
### هل يمكنني استخدام Aspose.Cells مجانًا؟
 نعم! يقدم Aspose.Cells نسخة تجريبية مجانية. يمكنك تنزيلها[هنا](https://releases.aspose.com/).
### كيف يمكنني شراء ترخيص لـ Aspose.Cells؟
 يمكنك شراء ترخيص Aspose.Cells من خلال زيارة هذا[رابط الشراء](https://purchase.aspose.com/buy).
### هل من السهل دمج المكتبة في المشاريع القائمة؟
بالتأكيد! يتكامل Aspose.Cells بسهولة مع مشاريع .NET، كما أن واجهة برمجة التطبيقات الخاصة به بسيطة.
### أين يمكنني العثور على الدعم لـ Aspose.Cells؟
 يمكنك الحصول على الدعم من خلال Aspose[منتدى](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
