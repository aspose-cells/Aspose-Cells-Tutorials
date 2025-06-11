---
"description": "تعرف على كيفية تعيين الخطوط الافتراضية لخيارات حفظ PDF باستخدام Aspose.Cells لـ .NET، مما يضمن ظهور مستنداتك بشكل مثالي في كل مرة."
"linktitle": "تعيين الخط الافتراضي لخيارات حفظ ملف PDF"
"second_title": "واجهة برمجة تطبيقات معالجة Excel Aspose.Cells .NET"
"title": "تعيين الخط الافتراضي لخيارات حفظ ملف PDF"
"url": "/ar/net/working-with-fonts-in-spreadsheets/set-default-font-for-pdf-save-options/"
"weight": 11
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# تعيين الخط الافتراضي لخيارات حفظ ملف PDF

## مقدمة
عند إنشاء التقارير أو الفواتير أو أي مستندات أخرى بصيغة PDF، فإن ضمان ظهور محتواك بالشكل الأمثل أمر بالغ الأهمية. تلعب الخطوط دورًا حيويًا في الحفاظ على المظهر الجذاب وسهولة قراءة مستنداتك. ولكن، ماذا يحدث عندما لا يتوفر الخط المستخدم في ملف Excel على النظام الذي تُنشئ ملف PDF عليه؟ هنا يأتي دور Aspose.Cells for .NET. تتيح لك هذه المكتبة القوية تعيين الخطوط الافتراضية لخيارات حفظ ملفات PDF، مما يضمن أن تبدو مستنداتك احترافية ومتناسقة، بغض النظر عن مكان فتحها.
## المتطلبات الأساسية
قبل أن نبدأ، تأكد من أن لديك ما يلي:
1. Visual Studio: ستحتاج إلى بيئة تطوير مثل Visual Studio لكتابة التعليمات البرمجية الخاصة بك وتنفيذها.
2. Aspose.Cells لـ .NET: يمكنك تنزيل الإصدار الأحدث من [هذا الرابط](https://releases.aspose.com/cells/net/)بدلاً من ذلك، يمكنك تثبيته عبر مدير الحزم NuGet في Visual Studio.
3. المعرفة الأساسية بلغة C#: إن فهم أساسيات لغة C# سيساعدك على متابعة أمثلة التعليمات البرمجية.
4. ملف إكسل نموذجي: جهّز ملف إكسل نموذجي للاختبار. يمكنك إنشاء ملف بخطوط وأنماط متنوعة لمعرفة كيفية تعامل Aspose.Cells مع الخطوط المفقودة.
## استيراد الحزم
قبل استخدام Aspose.Cells في مشروعك، عليك استيراد الحزم اللازمة. إليك كيفية القيام بذلك:
1. افتح مشروعك: قم بتشغيل Visual Studio وافتح مشروعك الحالي أو قم بإنشاء مشروع جديد.
2. إضافة المراجع: انقر بزر الماوس الأيمن على مشروعك في مستكشف الحلول وحدد "إدارة حزم NuGet".
3. تثبيت Aspose.Cells: ابحث عن "Aspose.Cells" وانقر على زر "تثبيت".
4. أضف استخدام التوجيهات: في الجزء العلوي من ملف C# الخاص بك، قم بتضمين المساحات التالية:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Aspose.Cells.Rendering;
using System.Drawing.Imaging;
```
## الخطوة 1: إعداد الدلائل الخاصة بك
قبل العمل مع الملفات، من المهم تحديد مجلدي المصدر والإخراج. هذا يُسهّل تحديد موقع ملف Excel المُدخل وحفظ ملفات الإخراج المُولّدة.
```csharp
// دليل المصدر
string sourceDir = "Your Document Directory";
// دليل الإخراج
string outputDir = "Your Document Directory";
```
يستبدل `"Your Document Directory"` مع المسار الفعلي إلى الدلائل الخاصة بك.
## الخطوة 2: افتح ملف Excel
الآن بعد أن قمنا بإعداد الدلائل، فلنفتح ملف Excel الذي تريد العمل عليه. `Workbook` يتم استخدام الفئة في Aspose.Cells لتحميل مستند Excel.
```csharp
// فتح ملف Excel
Workbook workbook = new Workbook(sourceDir + "sampleSetDefaultFontPropertyOfPdfSaveOptionsAndImageOrPrintOptions.xlsx");
```
تأكد من استبدال اسم الملف باسم الملف الفعلي الخاص بك.
## الخطوة 3: إعداد خيارات عرض الصورة
بعد ذلك، نحتاج إلى تهيئة خيارات العرض لتحويل ورقة Excel إلى صيغة صورة. سننشئ مثيلًا لـ `ImageOrPrintOptions`، تحديد نوع الصورة والخط الافتراضي.
```csharp
// تقديم إلى تنسيق ملف PNG
ImageOrPrintOptions imgOpt = new ImageOrPrintOptions();
imgOpt.ImageType = Drawing.ImageType.Png;
imgOpt.CheckWorkbookDefaultFont = false;
imgOpt.DefaultFont = "Times New Roman";
```
في مقتطف التعليمات البرمجية هذا، قمنا بتعيين `CheckWorkbookDefaultFont` الممتلكات إلى `false`، مما يعني أنه في حالة فقدان أي خطوط، سيتم استخدام الخط الافتراضي المحدد ("Times New Roman") بدلاً من ذلك.
## الخطوة 4: عرض الورقة كصورة
الآن، لنُقدّم الورقة الأولى من المصنف كصورة PNG. سنستخدم `SheetRender` الصف لإنجاز هذا.
```csharp
// تحويل ورقة العمل الأولى إلى صورة
SheetRender sr = new SheetRender(workbook.Worksheets[0], imgOpt);
sr.ToImage(0, outputDir + "out1_imagePNG.png");
```
## الخطوة 5: تغيير نوع الصورة وتقديمها إلى TIFF
إذا كنت تريد تقديم نفس الورقة إلى تنسيق صورة مختلف، مثل TIFF، فيمكنك ببساطة تغيير `ImageType` الخاصية وكرر عملية العرض.
```csharp
// ضبط على تنسيق TIFF
imgOpt.ImageType = Drawing.ImageType.Tiff;
WorkbookRender wr = new WorkbookRender(workbook, imgOpt);
wr.ToImage(outputDir + "out1_imageTIFF.tiff");
```
## الخطوة 6: تكوين خيارات حفظ PDF
بعد ذلك، لنُعِدّ خيارات حفظ ملف PDF. سنُنشئ نسخة من `PdfSaveOptions`، قم بتعيين الخط الافتراضي، وحدد أننا نريد التحقق من الخطوط المفقودة.
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
وأخيرًا، يُنصح بإعلام المستخدم بنجاح العملية. يمكنك تحقيق ذلك باستخدام رسالة بسيطة في لوحة التحكم.
```csharp
Console.WriteLine("SetDefaultFontPropertyOfPdfSaveOptionsAndImageOrPrintOptions executed successfully.\r\n");
```
## خاتمة
يوفر Aspose.Cells طريقة مرنة وفعّالة للتعامل مع ملفات Excel، مما يُسهّل على المطورين إنشاء مستندات جذابة بصريًا تحافظ على تنسيقها. سواء كنت تعمل على تقارير أو مستندات مالية أو أي شكل آخر من أشكال عرض البيانات، فإن التحكم في عرض الخطوط يُحسّن جودة مخرجاتك بشكل ملحوظ.
## الأسئلة الشائعة
### ما هو Aspose.Cells؟
Aspose.Cells مكتبة .NET فعّالة تُمكّن المطورين من التعامل مع ملفات Excel دون الحاجة إلى تثبيت Microsoft Excel. تدعم هذه المكتبة تنسيقات ملفات متنوعة وتوفر ميزات ثرية للعمل مع جداول البيانات.
### كيف يمكنني تعيين الخط الافتراضي لملفات Excel الخاصة بي؟
يمكنك تعيين الخط الافتراضي باستخدام `PdfSaveOptions` حدد الفئة واسم الخط المطلوب. هذا يضمن أنه حتى في حال عدم وجود خط، سيستخدم مستندك الخط الافتراضي الذي حددته.
### هل يمكنني تحويل ملفات Excel إلى تنسيقات أخرى غير PDF؟
بالتأكيد! يتيح لك Aspose.Cells تحويل ملفات Excel إلى صيغ متنوعة، بما في ذلك الصور (PNG وTIFF) وHTML وCSV وغيرها.
### هل استخدام Aspose.Cells مجاني؟
Aspose.Cells منتج تجاري، ولكن يمكنك تجربته مجانًا بإصدار تجريبي محدود. للاستفادة من جميع وظائفه، ستحتاج إلى شراء ترخيص.
### أين يمكنني العثور على الدعم لـ Aspose.Cells؟
يمكنك العثور على الدعم لـ Aspose.Cells من خلال زيارة [منتدى Aspose](https://forum.aspose.com/c/cells/9)، حيث يمكنك طرح الأسئلة ومشاركة الأفكار مع المستخدمين والمطورين الآخرين.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}