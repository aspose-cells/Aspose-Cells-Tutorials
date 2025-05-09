---
"date": "2025-04-05"
"description": "تعرّف على كيفية تحويل ملفات Excel إلى صيغ PNG وTIFF وPDF باستخدام خطوط مخصصة مع Aspose.Cells لـ .NET. وتأكد من تناسق الطباعة في جميع تحويلات المستندات."
"title": "تحويل ملفات Excel إلى PNG وTIFF وPDF باستخدام الخطوط المخصصة في .NET باستخدام Aspose.Cells"
"url": "/ar/net/workbook-operations/render-excel-custom-fonts-aspose-net/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}


# تحويل ملفات Excel إلى PNG وTIFF وPDF باستخدام الخطوط المخصصة باستخدام Aspose.Cells لـ .NET

## مقدمة

يُعد الحفاظ على سلامة الخطوط أثناء تحويل ملفات Excel إلى صور أو ملفات PDF أمرًا بالغ الأهمية لضمان اتساق العلامة التجارية. يوفر Aspose.Cells for .NET حلاً فعالاً يتيح لك تحديد خطوط افتراضية مخصصة في تحويلات مستنداتك.

في هذا البرنامج التعليمي، سنرشدك خلال عملية تحويل ملفات Excel إلى صيغ PNG وTIFF وPDF باستخدام Aspose.Cells لـ .NET مع خطوط افتراضية مخصصة. هذا مثالي إذا كنت:
- هدفك هو الحصول على طباعة متسقة في المستندات المقدمة.
- يجب تخصيص إعدادات الخط أثناء التحويلات.
- هل تريد استكشاف خيارات التكوين داخل Aspose.Cells لـ .NET.

دعنا ننشئ بيئتك وننفذ هذه الميزات بسلاسة.

### المتطلبات الأساسية

قبل البدء، تأكد من أن لديك ما يلي:
- **بيئة .NET**:قم بإعداده على جهازك (يفضل .NET Core أو .NET Framework).
- **مكتبة Aspose.Cells لـ .NET**:تم تثبيته في مشروعك.
- **ملف اكسل**:مصنف Excel يحتوي على بيانات للتحويل.

### إعداد Aspose.Cells لـ .NET

للبدء، أضف مكتبة Aspose.Cells إلى مشروعك:

**استخدام .NET CLI:**
```bash
dotnet add package Aspose.Cells
```

**استخدام مدير الحزم:**
```powershell
PM> NuGet\Install-Package Aspose.Cells
```

احصل على ترخيص للوصول إلى الميزات الكاملة:
- **نسخة تجريبية مجانية**: يزور [نسخة تجريبية مجانية من Aspose](https://releases.aspose.com/cells/net/) للوصول الأولي.
- **رخصة مؤقتة**:احصل عليه من [ترخيص Aspose المؤقت](https://purchase.aspose.com/temporary-license/).
- **شراء**:للحصول على ترخيص دائم، توجه إلى [شراء Aspose](https://purchase.aspose.com/buy).

بعد الحصول على الترخيص الخاص بك، قم بتشغيل Aspose.Cells في تطبيقك:
```csharp
// قم بتعيين الترخيص لـ Aspose.Cells.
License license = new License();
license.SetLicense("path_to_your_license_file");
```

## دليل التنفيذ

### التقديم إلى PNG باستخدام الخط الافتراضي المخصص

تحويل ورقة عمل Excel إلى صيغة PNG مع ضبط خط افتراضي مخصص يضمن تناسقًا بصريًا. إليك الطريقة:

#### الخطوة 1: تكوين خيارات الصورة

قم بتكوين خيارات العرض لإخراج صورتك.
```csharp
using Aspose.Cells;
using Aspose.Cells.Rendering;

// تحديد الدلائل.
string SourceDir = @"YOUR_SOURCE_DIRECTORY";
string outputDir = @"YOUR_OUTPUT_DIRECTORY";

// افتح ملف Excel.
Workbook workbook = new Workbook(SourceDir + "sampleSetDefaultFontPropertyOfPdfSaveOptionsAndImageOrPrintOptions.xlsx");

// إعداد خيارات عرض الصورة.
ImageOrPrintOptions imgOpt = new ImageOrPrintOptions();
imgOpt.ImageType = Drawing.ImageType.Png;
imgOpt.CheckWorkbookDefaultFont = false; // استخدم خطًا مخصصًا للخطوط المفقودة في المصنف.
imgOpt.DefaultFont = "Times New Roman";
```

#### الخطوة 2: العرض والحفظ

قم بتحويل ورقة العمل الخاصة بك إلى ملف صورة باستخدام هذه الإعدادات.
```csharp
// تحويل ورقة العمل الأولى إلى صورة PNG.
SheetRender sr = new SheetRender(workbook.Worksheets[0], imgOpt);
sr.ToImage(0, outputDir + "out1_imagePNG.png");
```

### العرض بصيغة TIFF باستخدام الخط الافتراضي المخصص

تنسيق TIFF مثالي للصور عالية الجودة. إليك كيفية عرض مصنف كامل كملف TIFF:

#### الخطوة 3: إعداد خيارات الصورة لـ TIFF

قم بتكوين خيارات العرض خصيصًا لإخراج TIFF.
```csharp
// أعد استخدام الدلائل المحددة مسبقًا وافتح ملف Excel.
Workbook workbook = new Workbook(SourceDir + "sampleSetDefaultFontPropertyOfPdfSaveOptionsAndImageOrPrintOptions.xlsx");

// تكوين خيارات عرض الصور بتنسيق TIFF.
imgOpt.ImageType = Drawing.ImageType.Tiff;
```

#### الخطوة 4: تحويل المصنف بأكمله إلى TIFF

تحويل المصنف بأكمله إلى ملف TIFF واحد.
```csharp
// عرض المصنف كصورة TIFF.
WorkbookRender wr = new WorkbookRender(workbook, imgOpt);
wr.ToImage(outputDir + "out1_imageTIFF.tiff");
```

### تحويل إلى PDF باستخدام الخط الافتراضي المخصص

يعد حفظ مصنف Excel بتنسيق PDF مع ضمان اتساق الخط أمرًا بالغ الأهمية للتوثيق الاحترافي.

#### الخطوة 5: تكوين خيارات حفظ PDF

قم بإعداد الخيارات اللازمة لحفظ ملفك بتنسيق PDF.
```csharp
using Aspose.Cells;

// أعد فتح المصنف.
Workbook workbook = new Workbook(SourceDir + "sampleSetDefaultFontPropertyOfPdfSaveOptionsAndImageOrPrintOptions.xlsx");

// إعداد خيارات حفظ PDF.
PdfSaveOptions saveOptions = new PdfSaveOptions();
saveOptions.DefaultFont = "Times New Roman";
saveOptions.CheckWorkbookDefaultFont = false; // استخدم خطًا مخصصًا للخطوط المفقودة في المصنف.
```

#### الخطوة 6: الحفظ بتنسيق PDF

قم بتصدير المصنف الخاص بك إلى مستند PDF.
```csharp
// احفظ المصنف كملف PDF.
workbook.Save(outputDir + "out1_pdf.pdf", saveOptions);
```

## التطبيقات العملية

- **تقارير الأعمال**:تأكد من وجود علامة تجارية متسقة في جميع التقارير المصدرة باستخدام الخطوط المخصصة.
- **أرشفة المستندات**:تحويل ملفات Excel القديمة إلى ملفات PDF لسهولة مشاركتها وأرشفتها باستخدام الطباعة الموحدة.
- **التصميم الجرافيكي**:إنشاء صور TIFF عالية الدقة لبيانات Excel للعروض التقديمية أو مشاريع التصميم.

إن التكامل مع أنظمة أخرى، مثل منصات إدارة علاقات العملاء أو حلول إدارة المستندات، قد يعمل على تعزيز حالات الاستخدام هذه من خلال أتمتة عمليات التصدير استنادًا إلى عوامل تشغيل أو أحداث محددة.

## اعتبارات الأداء

إن تحسين عملية العرض الخاصة بك أمر بالغ الأهمية:
- **إدارة الذاكرة**:التخلص من `Workbook`، `SheetRender`، و `WorkbookRender` الأشياء على الفور لتحرير الموارد.
- **معالجة الدفعات**:إذا كنت تتعامل مع ملفات متعددة، فقم بتنفيذ المعالجة الدفعية للتعامل معها بكفاءة.
- **العمليات غير المتزامنة**:استخدم الأساليب غير المتزامنة حيثما أمكن لتحسين الاستجابة في التطبيقات.

## خاتمة

لقد أتقنتَ الآن تحويل مصنفات Excel إلى صيغ PNG وTIFF وPDF، مع ضبط خطوط افتراضية مخصصة باستخدام Aspose.Cells لـ .NET. تضمن هذه الميزة الحفاظ على سلامة مستنداتك البصرية عبر مختلف المنصات والاستخدامات.

استكشف الميزات الإضافية التي يقدمها Aspose.Cells لتحسين إمكانيات معالجة المستندات. لمزيد من المعلومات أو المساعدة، تفضل بزيارة [منتدى أسبوزي](https://forum.aspose.com/c/cells/9).

## قسم الأسئلة الشائعة

**1. ما هو Aspose.Cells لـ .NET؟**
   — Aspose.Cells for .NET هي مكتبة توفر ميزات قوية لإدارة ملفات Excel وتحويلها برمجيًا.

**2. هل يمكنني استخدام Aspose.Cells في تطبيقات الويب؟**
   — نعم، يمكن دمج Aspose.Cells في ASP.NET أو أي تطبيق ويب آخر يعتمد على .NET.

**3. كيف أتعامل مع الخطوط المفقودة أثناء العرض؟**
   — عن طريق ضبط `CheckWorkbookDefaultFont` إلى خطأ وتحديد `DefaultFont`، فإنك تضمن أن كل النص يستخدم الخط الذي اخترته، حتى لو لم يكن النص الأصلي متاحًا.

**4. هل هناك دعم لتنسيقات أخرى غير PNG و TIFF و PDF؟**
   — نعم، يدعم Aspose.Cells تنسيقات الصور المختلفة مثل JPEG وBMP وما إلى ذلك، ويوفر إمكانيات تحويل المستندات الشاملة.

**5. ما هي بعض أفضل الممارسات لاستخدام Aspose.Cells في التطبيقات واسعة النطاق؟**
   - استخدام تقنيات إدارة الذاكرة الفعالة، والمعالجة الدفعية للتعامل مع ملفات متعددة، والنظر في العمليات غير المتزامنة لتحسين أداء التطبيق.

## موارد
- **التوثيق**: [توثيق Aspose.Cells](https://reference.aspose.com/cells/net/)
- **تحميل**: [إصدارات Aspose.Cells](https://releases.aspose.com/cells/net/)
- **شراء**: [شراء Aspose.Cells](https://purchase.aspose.com/buy)
- **نسخة تجريبية مجانية**: [جرب Aspose.Cells مجانًا](https://releases.aspose.com/cells/net/)
- **رخصة مؤقتة**: [احصل على رخصة مؤقتة](https://purchase.aspose.com/temporary-license/) 


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}