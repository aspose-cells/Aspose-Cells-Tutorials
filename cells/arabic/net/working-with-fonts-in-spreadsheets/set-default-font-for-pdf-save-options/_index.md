---
title: تعيين الخط الافتراضي لخيارات حفظ ملف PDF
linktitle: تعيين الخط الافتراضي لخيارات حفظ ملف PDF
second_title: واجهة برمجة تطبيقات معالجة Excel الخاصة بـ Aspose.Cells .NET
description: تعرف على كيفية تعيين الخطوط الافتراضية لخيارات حفظ PDF باستخدام Aspose.Cells لـ .NET، مما يضمن ظهور مستنداتك بشكل مثالي في كل مرة.
weight: 11
url: /ar/net/working-with-fonts-in-spreadsheets/set-default-font-for-pdf-save-options/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تعيين الخط الافتراضي لخيارات حفظ ملف PDF

## مقدمة
عندما يتعلق الأمر بإنشاء التقارير أو الفواتير أو أي مستندات أخرى بتنسيق PDF، فإن التأكد من أن المحتوى الخاص بك يبدو بالشكل الصحيح هو أمر بالغ الأهمية. تلعب الخطوط دورًا حيويًا في الحفاظ على الجاذبية البصرية وسهولة قراءة مستنداتك. ومع ذلك، ماذا يحدث عندما لا يتوفر الخط الذي استخدمته في ملف Excel على النظام الذي تقوم فيه بإنشاء ملف PDF الخاص بك؟ هنا يأتي دور Aspose.Cells for .NET. تتيح لك هذه المكتبة القوية تعيين الخطوط الافتراضية لخيارات حفظ PDF الخاصة بك، مما يضمن أن تبدو مستنداتك احترافية ومتسقة، بغض النظر عن مكان فتحها.
## المتطلبات الأساسية
قبل أن نبدأ، تأكد من أن لديك ما يلي:
1. Visual Studio: ستحتاج إلى بيئة تطوير مثل Visual Studio لكتابة التعليمات البرمجية الخاصة بك وتنفيذها.
2.  Aspose.Cells لـ .NET: يمكنك تنزيل الإصدار الأحدث من[هذا الرابط](https://releases.aspose.com/cells/net/)بدلاً من ذلك، يمكنك تثبيته عبر NuGet Package Manager في Visual Studio.
3. المعرفة الأساسية بلغة C#: إن فهم أساسيات لغة C# سيساعدك على متابعة أمثلة التعليمات البرمجية.
4. ملف Excel نموذجي: قم بإعداد ملف Excel نموذجي للاختبار. يمكنك إنشاء ملف Excel باستخدام خطوط وأنماط مختلفة لمعرفة كيفية تعامل Aspose.Cells مع الخطوط المفقودة.
## استيراد الحزم
قبل أن تتمكن من استخدام Aspose.Cells في مشروعك، يتعين عليك استيراد الحزم اللازمة. وإليك كيفية القيام بذلك:
1. افتح مشروعك: قم بتشغيل Visual Studio وافتح مشروعك الحالي أو قم بإنشاء مشروع جديد.
2. إضافة المراجع: انقر بزر الماوس الأيمن على مشروعك في مستكشف الحلول وحدد "إدارة حزم NuGet".
3. تثبيت Aspose.Cells: ابحث عن "Aspose.Cells" وانقر على زر "تثبيت".
4. إضافة استخدام التوجيهات: في الجزء العلوي من ملف C# الخاص بك، قم بتضمين المساحات التالية:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Aspose.Cells.Rendering;
using System.Drawing.Imaging;
```
## الخطوة 1: إعداد الدلائل الخاصة بك
قبل العمل بالملفات، من المهم تحديد دليل المصدر والإخراج. سيسهل هذا تحديد موقع ملف Excel المدخل وحفظ ملفات الإخراج الناتجة.
```csharp
// دليل المصدر
string sourceDir = "Your Document Directory";
// دليل الإخراج
string outputDir = "Your Document Directory";
```
 يستبدل`"Your Document Directory"` مع المسار الفعلي إلى الدلائل الخاصة بك.
## الخطوة 2: افتح ملف Excel
 الآن بعد أن قمنا بإعداد الدلائل الخاصة بنا، فلنفتح ملف Excel الذي تريد العمل به.`Workbook` يتم استخدام الفئة في Aspose.Cells لتحميل مستند Excel.
```csharp
// فتح ملف Excel
Workbook workbook = new Workbook(sourceDir + "sampleSetDefaultFontPropertyOfPdfSaveOptionsAndImageOrPrintOptions.xlsx");
```
تأكد من استبدال اسم الملف باسم الملف الفعلي الخاص بك.
## الخطوة 3: إعداد خيارات عرض الصورة
بعد ذلك، نحتاج إلى تكوين خيارات العرض لتحويل ورقة Excel الخاصة بنا إلى تنسيق صورة. سننشئ مثيلًا لـ`ImageOrPrintOptions`، تحديد نوع الصورة والخط الافتراضي.
```csharp
// تقديم إلى تنسيق ملف PNG
ImageOrPrintOptions imgOpt = new ImageOrPrintOptions();
imgOpt.ImageType = Drawing.ImageType.Png;
imgOpt.CheckWorkbookDefaultFont = false;
imgOpt.DefaultFont = "Times New Roman";
```
 في مقتطف التعليمات البرمجية هذا، قمنا بتعيين`CheckWorkbookDefaultFont` الممتلكات ل`false`، مما يعني أنه في حالة فقدان أي خطوط، سيتم استخدام الخط الافتراضي المحدد ("Times New Roman") بدلاً من ذلك.
## الخطوة 4: عرض الورقة كصورة
 الآن، دعنا نعرض الورقة الأولى من المصنف كصورة PNG. سنستخدم`SheetRender` الصف لإنجاز هذا.
```csharp
// تحويل ورقة العمل الأولى إلى صورة
SheetRender sr = new SheetRender(workbook.Worksheets[0], imgOpt);
sr.ToImage(0, outputDir + "out1_imagePNG.png");
```
## الخطوة 5: تغيير نوع الصورة وتقديمها إلى TIFF
 إذا كنت تريد عرض نفس الورقة بتنسيق صورة مختلف، مثل TIFF، فيمكنك ببساطة تغيير`ImageType` الممتلكات وكرر عملية العرض.
```csharp
// تم الضبط على تنسيق TIFF
imgOpt.ImageType = Drawing.ImageType.Tiff;
WorkbookRender wr = new WorkbookRender(workbook, imgOpt);
wr.ToImage(outputDir + "out1_imageTIFF.tiff");
```
## الخطوة 6: تكوين خيارات حفظ PDF
 بعد ذلك، دعنا نعد خيارات حفظ ملف PDF. سننشئ مثيلًا لـ`PdfSaveOptions`، قم بتعيين الخط الافتراضي، وحدد أننا نريد التحقق من الخطوط المفقودة.
```csharp
// تكوين خيارات حفظ PDF
PdfSaveOptions saveOptions = new PdfSaveOptions();
saveOptions.DefaultFont = "Times New Roman";
saveOptions.CheckWorkbookDefaultFont = false;
```
## الخطوة 7: احفظ المصنف بتنسيق PDF
بعد تكوين خيارات الحفظ، حان الوقت لحفظ مصنف Excel الخاص بنا كملف PDF. 
```csharp
// حفظ المصنف بصيغة PDF
workbook.Save(outputDir + "out1_pdf.pdf", saveOptions);
```
## الخطوة 8: تأكيد التنفيذ
أخيرًا، من الجيد إعلام المستخدم بأن العملية اكتملت بنجاح. يمكنك تحقيق ذلك باستخدام رسالة وحدة تحكم بسيطة.
```csharp
Console.WriteLine("SetDefaultFontPropertyOfPdfSaveOptionsAndImageOrPrintOptions executed successfully.\r\n");
```
## خاتمة
يوفر Aspose.Cells طريقة مرنة وقوية للتعامل مع عمليات معالجة ملفات Excel، مما يجعل من الأسهل على المطورين إنشاء مستندات جذابة بصريًا تحافظ على تنسيقها. سواء كنت تعمل على التقارير أو المستندات المالية أو أي شكل آخر من أشكال عرض البيانات، فإن التحكم في عرض الخطوط يمكن أن يعزز جودة الناتج بشكل كبير.
## الأسئلة الشائعة
### ما هو Aspose.Cells؟
Aspose.Cells هي مكتبة .NET قوية تتيح للمطورين التعامل مع ملفات Excel دون الحاجة إلى تثبيت Microsoft Excel. وهي تدعم تنسيقات ملفات مختلفة وتوفر ميزات غنية للعمل مع جداول البيانات.
### كيف يمكنني تعيين خط افتراضي لملفات Excel الخاصة بي؟
 يمكنك تعيين الخط الافتراضي باستخدام`PdfSaveOptions` حدد الفئة وحدد اسم الخط المطلوب. وهذا يضمن أنه حتى في حالة عدم وجود خط، ستستخدم مستندك الخط الافتراضي الذي حددته.
### هل يمكنني تحويل ملفات Excel إلى تنسيقات أخرى غير PDF؟
بالتأكيد! يتيح لك Aspose.Cells تحويل ملفات Excel إلى تنسيقات مختلفة، بما في ذلك الصور (PNG وTIFF) وHTML وCSV والمزيد.
### هل استخدام Aspose.Cells مجاني؟
Aspose.Cells هو منتج تجاري، ولكن يمكنك تجربته مجانًا من خلال إصدار تجريبي محدود. للحصول على الوظائف الكاملة، ستحتاج إلى شراء ترخيص.
### أين يمكنني العثور على الدعم لـ Aspose.Cells؟
 يمكنك العثور على الدعم لـ Aspose.Cells من خلال زيارة[منتدى اسبوس](https://forum.aspose.com/c/cells/9)حيث يمكنك طرح الأسئلة ومشاركة الأفكار مع المستخدمين والمطورين الآخرين.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
