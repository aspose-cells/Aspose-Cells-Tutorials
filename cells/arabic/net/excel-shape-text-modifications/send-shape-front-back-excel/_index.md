---
title: إرسال الشكل للأمام أو للخلف في Excel
linktitle: إرسال الشكل للأمام أو للخلف في Excel
second_title: واجهة برمجة تطبيقات معالجة Excel الخاصة بـ Aspose.Cells .NET
description: اكتشف كيفية إرسال الأشكال إلى الأمام أو الخلف في Excel باستخدام Aspose.Cells for .NET. يوفر هذا الدليل برنامجًا تعليميًا خطوة بخطوة مع نصائح.
weight: 16
url: /ar/net/excel-shape-text-modifications/send-shape-front-back-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إرسال الشكل للأمام أو للخلف في Excel

## مقدمة
عند العمل مع ملفات Excel، قد تجد نفسك في حاجة إلى مزيد من التحكم في العناصر المرئية في جدول البيانات الخاص بك. يمكن للأشكال، مثل الصور والرسومات، أن تعزز عرض البيانات. ولكن ماذا يحدث عندما تتداخل هذه الأشكال أو تحتاج إلى إعادة ترتيبها؟ هذا هو المكان الذي يبرز فيه Aspose.Cells for .NET. في هذا البرنامج التعليمي، سنرشدك خلال الخطوات اللازمة للتعامل مع الأشكال في ورقة عمل Excel، وتحديدًا إرسال الأشكال إلى مقدمة أو خلفية الأشكال الأخرى. إذا كنت مستعدًا لتحسين أدائك في Excel، فلنبدأ على الفور!
## المتطلبات الأساسية
قبل أن نبدأ، ستحتاج إلى توفير بعض الأشياء:
1.  تثبيت مكتبة Aspose.Cells: تأكد من تثبيت مكتبة Aspose.Cells لـ .NET. يمكنك العثور عليها[هنا](https://releases.aspose.com/cells/net/).
2. بيئة التطوير: تأكد من إعداد بيئة تطوير لديك مع دعم .NET، مثل Visual Studio.
3. المعرفة الأساسية بلغة C#: ستساعدك المعرفة ببرمجة C# على فهم مقتطفات التعليمات البرمجية بشكل أفضل.
حسنًا، هل استوفيت جميع الشروط المطلوبة في قائمة المتطلبات الأساسية؟ رائع! لننتقل إلى الجزء الممتع - كتابة بعض التعليمات البرمجية!
## استيراد الحزم
قبل أن نتعمق في الترميز الفعلي، دعنا نستورد الحزم اللازمة. ما عليك سوى إضافة الأمر التالي باستخدام في أعلى ملف C# الخاص بك:
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System;
```
تُعد هذه المساحات الأساسية بالغة الأهمية لأنها تحتوي على الفئات والطرق التي سنستخدمها للتعامل مع ملفات وأشكال Excel.
## الخطوة 1: تحديد مسارات الملفات الخاصة بك
في هذه الخطوة الأولى، نحتاج إلى تحديد دليل المصدر ودليل الإخراج. هذا هو المكان الذي يوجد فيه ملف Excel والمكان الذي تريد حفظ الملف المعدل فيه.
```csharp
//دليل المصدر
string sourceDir = "Your Document Directory";
//دليل الإخراج
string outputDir = "Your Document Directory";
```
 يستبدل`"Your Document Directory"` مع المسار الفعلي الذي يتم تخزين ملفات Excel فيه.
## الخطوة 2: تحميل المصنف
الآن بعد أن قمنا بتعيين الدلائل الخاصة بنا، فلنقم بتحميل المصنف (ملف Excel) الذي يحتوي على الأشكال التي نريد معالجتها.
```csharp
//تحميل ملف Excel المصدر
Workbook wb = new Workbook(sourceDir + "sampleToFrontOrBack.xlsx");
```
 يقوم هذا السطر من التعليمات البرمجية بتهيئة سطر جديد`Workbook` الكائن، تحميل ملف Excel المحدد في الذاكرة حتى نتمكن من العمل معه.
## الخطوة 3: الوصول إلى ورقة العمل 
بعد ذلك، نحتاج إلى الوصول إلى ورقة العمل المحددة التي توجد بها الأشكال الخاصة بنا. في هذا المثال، سنستخدم ورقة العمل الأولى.
```csharp
//الوصول إلى ورقة العمل الأولى
Worksheet ws = wb.Worksheets[0];
```
 من خلال الإشارة`Worksheets[0]`نحن نستهدف الورقة الأولى من المصنف الخاص بنا. إذا كانت الأشكال موجودة على ورقة مختلفة، فقم بتعديل الفهرس وفقًا لذلك.
## الخطوة 4: الوصول إلى الأشكال
بعد أن أصبح الوصول إلى ورقة العمل جاهزًا، فلننتقل إلى الأشكال التي تهمنا. في هذا المثال، سننتقل إلى الشكلين الأول والرابع.
```csharp
//الوصول إلى الشكل الأول والرابع
Shape sh1 = ws.Shapes[0];
Shape sh4 = ws.Shapes[3];
```
تحصل هذه الخطوط على الأشكال المحددة من ورقة العمل استنادًا إلى فهرسها.
## الخطوة 5: طباعة موضع الترتيب Z للأشكال
قبل تحريك أي شكل، دعنا نطبع موضعه الحالي على الترتيب Z. يساعدنا هذا في تتبع موضعه قبل إجراء أي تغييرات.
```csharp
//طباعة موضع الترتيب Z للشكل
Console.WriteLine("Z-Order Shape 1: " + sh1.ZOrderPosition);
```
 عن طريق الاتصال`ZOrderPosition`يمكننا أن نرى مكان كل شكل في ترتيب الرسم.
## الخطوة 6: إرسال الشكل الأول إلى الأمام
الآن حان وقت العمل! لنرسل الشكل الأول إلى مقدمة Z-Order.
```csharp
//أرسل هذا الشكل إلى الأمام
sh1.ToFrontOrBack(2);
```
 بالمرور`2` ل`ToFrontOrBack`نحن نطلب من Aspose.Cells إحضار هذا الشكل إلى المقدمة. 
## الخطوة 7: طباعة موضع الترتيب Z للشكل الثاني
قبل أن نرسل الشكل الثاني إلى الخلف، دعونا نتحقق من مكانه.
```csharp
//طباعة موضع الترتيب Z للشكل
Console.WriteLine("Z-Order Shape 4: " + sh4.ZOrderPosition);
```
وهذا يمنحنا نظرة ثاقبة على موضع الشكل الرابع قبل إجراء أي تغييرات.
## الخطوة 8: أرسل الشكل الرابع إلى الخلف
وأخيرًا، سنقوم بإرسال الشكل الرابع إلى الجزء الخلفي من كومة Z-Order.
```csharp
//أرسل هذا الشكل إلى الخلف
sh4.ToFrontOrBack(-2);
```
 استخدام`-2` حيث يقوم المعامل بإرسال الشكل نحو الجزء الخلفي من المكدس، مما يضمن عدم عرقلة الأشكال أو النصوص الأخرى.
## الخطوة 9: احفظ المصنف 
الخطوة الأخيرة هي حفظ المصنف الخاص بك بالأشكال الموضوعة حديثًا.
```csharp
//حفظ ملف Excel الناتج
wb.Save(outputDir + "outputToFrontOrBack.xlsx");
```
يقوم هذا الأمر بحفظ المصنف المعدل في دليل الإخراج المحدد.
## الخطوة 10: رسالة التأكيد
وأخيرًا، دعونا نقدم تأكيدًا بسيطًا لإعلامنا بأن مهمتنا اكتملت بنجاح.
```csharp
Console.WriteLine("SendShapeFrontOrBackInWorksheet executed successfully.\r\n");
```
وهذا يختتم الكود لبرنامجنا التعليمي!
## خاتمة
إن التعامل مع الأشكال في Excel باستخدام Aspose.Cells for .NET ليس بالأمر السهل فحسب، بل إنه قوي أيضًا. باتباع هذا الدليل، يجب أن تتمكن الآن من إرسال الأشكال إلى الأمام أو الخلف بسهولة، مما يسمح بتحكم أفضل في عروض Excel التقديمية الخاصة بك. باستخدام هذه الأدوات، أنت جاهز لتحسين المظهر المرئي لجداول البيانات الخاصة بك.
## الأسئلة الشائعة
### ما هي لغة البرمجة التي أحتاجها لـ Aspose.Cells؟  
يجب عليك استخدام C# أو أي لغة تدعم .NET للعمل مع Aspose.Cells.
### هل يمكنني تجربة Aspose.Cells مجانًا؟  
 نعم، يمكنك البدء بإصدار تجريبي مجاني من Aspose.Cells[هنا](https://releases.aspose.com/).
### ما هي أنواع الأشكال التي يمكنني التعامل معها في Excel؟  
يمكنك التعامل مع أشكال مختلفة مثل المستطيلات والدوائر والخطوط والصور.
### كيف يمكنني الحصول على الدعم لـ Aspose.Cells؟  
 يمكنك زيارة منتدى مجتمعهم للحصول على أي دعم أو استفسارات[هنا](https://forum.aspose.com/c/cells/9).
### هل هناك ترخيص مؤقت متاح لـ Aspose.Cells؟  
 نعم يمكنك طلب ترخيص مؤقت[هنا](https://purchase.aspose.com/temporary-license/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
