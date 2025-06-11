---
"description": "اكتشف كيفية التحكم في الموارد الخارجية في تحويل Excel إلى PDF باستخدام Aspose.Cells لـ .NET من خلال دليلنا السهل المتابعة."
"linktitle": "التحكم في الموارد الخارجية في Excel إلى PDF في Aspose.Cells"
"second_title": "واجهة برمجة تطبيقات معالجة Excel Aspose.Cells .NET"
"title": "التحكم في الموارد الخارجية في Excel إلى PDF في Aspose.Cells"
"url": "/ar/net/rendering-and-export/control-loading-of-external-resources/"
"weight": 12
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# التحكم في الموارد الخارجية في Excel إلى PDF في Aspose.Cells

## مقدمة
في عصرنا الرقمي، أصبح تحويل جداول بيانات Excel إلى مستندات PDF مهمة شائعة. سواءً كنتَ تُعِدّ تقارير أو بيانات مالية أو مواد عروض تقديمية، فأنتَ ترغب في ضمان ظهور ملفات PDF بالشكل الذي تُريده بالضبط. Aspose.Cells for .NET هي مكتبة فعّالة تُتيح لك التحكم في عملية التحويل هذه حتى أدق التفاصيل، خاصةً عند التعامل مع موارد خارجية مثل الصور المُرفقة بملفات Excel. في هذا الدليل، سنتناول بالتفصيل كيفية التحكم في الموارد الخارجية أثناء عملية تحويل Excel إلى PDF باستخدام Aspose.Cells. لذا، هيا بنا نبدأ!
## المتطلبات الأساسية
قبل أن ندخل في التفاصيل، لنتأكد من تجهيز كل ما تحتاجه للبدء. إليك قائمة مرجعية سريعة:
1. Visual Studio أو أي بيئة تطوير متكاملة متوافقة مع .NET: ستحتاج إلى بيئة لكتابة واختبار الكود الخاص بك.
2. Aspose.Cells لـ .NET: إذا لم تقم بتثبيته بعد، فتوجه إلى [تنزيلات Aspose](https://releases.aspose.com/cells/net/) الصفحة والحصول على الإصدار الأحدث.
3. المعرفة الأساسية بلغة C#: الإلمام بلغة البرمجة C# مفيد. إذا لم تكن متأكدًا من أي مفاهيم، فلا تتردد في البحث عنها.
4. ملف إكسل نموذجي: جهّز ملف إكسل باستخدام أي موارد خارجية ترغب في تحويلها. يمكنك استخدام الملف النموذجي المرفق "samplePdfSaveOptions_StreamProvider.xlsx".
5. ملف صورة للاختبار: سيتم استخدامه كمورد خارجي أثناء التحويل. ملف الصورة "newPdfSaveOptions_StreamProvider.png" يُمثل مرجعًا بديلًا مناسبًا.
## استيراد الحزم
للبدء، ستحتاج إلى استيراد مساحات الأسماء اللازمة من مكتبة Aspose.Cells. هذا ضروري للوصول إلى وظائفها. تأكد من إضافة توجيهات الاستخدام التالية في أعلى ملفك:
```csharp
using System.IO;
using System.Drawing;
using System.Drawing.Imaging;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using Aspose.Cells.Rendering;
using System;
```
ستوفر لك هذه الحزم جميع الفئات والأساليب الأساسية التي ستحتاجها لأداء مهامك.
## الخطوة 1: إنشاء فئة موفر البث الخاص بك
أول أمر يجب عليك القيام به هو إنشاء فئة موفر تدفق تنفذ `IStreamProvider` ستتيح لك هذه الفئة التحكم في كيفية تحميل الموارد الخارجية.
```csharp
class MyStreamProvider : IStreamProvider
{
    public void CloseStream(StreamProviderOptions options)
    {
        Debug.WriteLine("-----Close Stream-----");
    }
    public void InitStream(StreamProviderOptions options)
    {
        string sourceDir = "Your Document Directory";
        Debug.WriteLine("-----Init Stream-----");
        // قراءة الصورة الجديدة في مجرى الذاكرة وتعيينها إلى خاصية المجرى
        byte[] bts = File.ReadAllBytes(sourceDir + "newPdfSaveOptions_StreamProvider.png");
        MemoryStream ms = new MemoryStream(bts);
        options.Stream = ms;
    }
}
```
في هذه الفئة:
- إغلاق التدفق: سيتم استدعاء هذه الطريقة عند إغلاق التدفق. حاليًا، نكتب رسالة تصحيح أخطاء للتتبع فقط.
- InitStream: هنا تبدأ العملية. هنا، ستقرأ صورتك الخارجية كمصفوفة بايتات، وتحولها إلى تدفق ذاكرة، ثم تُعيّنها إلى `options.Stream` ملكية.
## الخطوة 2: إعداد أدلة المصدر والإخراج
الآن بعد أن أصبح موفر البث الخاص بك جاهزًا، فقد حان الوقت لتحديد مكان ملف Excel والمكان الذي تريد حفظ ملف PDF فيه.
```csharp
// دليل المصدر
string sourceDir = "Your Document Directory";
// دليل الإخراج
string outputDir = "Your Document Directory";
```
استبدل ببساطة `"Your Document Directory"` مع المسار الفعلي لملفاتك على جهاز الكمبيوتر. تنظيم ملفاتك هو الأساس!
## الخطوة 3: تحميل ملف Excel الخاص بك
بعد ذلك، ستقوم بتحميل ملف Excel الذي تريد إنشاء ملف PDF منه.
```csharp
// تحميل ملف Excel المصدر الذي يحتوي على صور خارجية
Workbook wb = new Workbook(sourceDir + "samplePdfSaveOptions_StreamProvider.xlsx");
```
نحن نستخدم `Workbook` فئة من Aspose.Cells، تُمثل ملف Excel الخاص بك. يمكن أن يتضمن الملف موارد خارجية متنوعة، مثل الصور، والتي ترغب في التحكم بها أثناء التحويل.
## الخطوة 4: تعيين خيارات حفظ PDF
قبل حفظ المصنف بصيغة PDF، حدد طريقة الحفظ. يمكنك تعديل هذه الخيارات حسب احتياجاتك.
```csharp
// تحديد خيارات حفظ ملف PDF - موفر البث
PdfSaveOptions opts = new PdfSaveOptions();
opts.OnePagePerSheet = true; // احفظ كل ورقة في صفحة جديدة
```
هنا، نقوم بإنشاء مثيل جديد لـ `PdfSaveOptions`، مما يسمح لك بتخصيص كيفية تنسيق ملف PDF الخاص بك. `OnePagePerSheet` يعد هذا الخيار مفيدًا لضمان حصول كل ورقة Excel على صفحة خاصة بها في ملف PDF النهائي.
## الخطوة 5: تعيين موفر البث الخاص بك
بعد تعيين خيارات PDF الخاصة بك، يتعين عليك إخبار Aspose باستخدام موفر البث المخصص للموارد الخارجية.
```csharp
wb.Settings.StreamProvider = new MyStreamProvider();
```
هذا الخط يربطك `Workbook` مثال مع `MyStreamProvider` الفئة التي أنشأتها سابقًا. هذا يعني أنه عند مواجهة موارد خارجية أثناء التحويل، سيتعامل معها مزود الخدمة كما هو محدد.
## الخطوة 6: حفظ المصنف بتنسيق PDF
بعد إعداد كل شيء، حان الوقت أخيرًا لحفظ مصنف Excel الخاص بك بتنسيق PDF.
```csharp
// احفظ المصنف بصيغة Pdf
wb.Save(outputDir + "outputPdfSaveOptions_StreamProvider.pdf", opts);
```
عن طريق الاتصال `Save` من خلال تطبيق الطريقة على كائن المصنف وتمرير دليل الإخراج الخاص بك مع خيارات PDF، يمكنك تحويل ملف Excel إلى ملف PDF بتنسيق جميل.
## الخطوة 7: تأكيد التنفيذ الناجح
ولاختتام الأمور، من الجميل دائمًا التأكد من نجاح عمليتك!
```csharp
Console.WriteLine("ControlLoadingOfExternalResourcesInExcelToPDF executed successfully.\r\n");
```
طباعة رسالة نجاح على لوحة التحكم تُبقيك على اطلاع دائم بحالة عمليتك. من الجيد تضمين هذه التأكيدات الصغيرة في الكود.
## خاتمة
هذا كل ما في الأمر! باتباع هذه الخطوات البسيطة، يمكنك التحكم باحترافية في كيفية التعامل مع الموارد الخارجية أثناء تحويل ملفات Excel إلى PDF باستخدام Aspose.Cells. هذا يعني أن مستنداتك الآن قادرة على تضمين الصور والعناصر الخارجية الأخرى بدقة، مما يضمن لك منتجًا نهائيًا متقنًا في كل مرة.
## الأسئلة الشائعة
### ما هو Aspose.Cells؟  
Aspose.Cells هي مكتبة قوية لمطوري .NET تسمح لك بإنشاء ملفات Excel ومعالجتها وتحويلها وعرضها بتنسيقات مختلفة.
### كيف يمكنني تنزيل Aspose.Cells؟  
يمكنك تنزيل أحدث إصدار من Aspose.Cells من [رابط التحميل](https://releases.aspose.com/cells/net/).
### هل يمكنني تجربة Aspose.Cells مجانًا؟  
نعم! يمكنك الحصول على نسخة تجريبية مجانية بزيارة [صفحة التجربة المجانية](https://releases.aspose.com/).
### أين يمكنني العثور على الدعم لـ Aspose.Cells؟  
لأي استفسارات تتعلق بالدعم، يمكنك زيارة [منتدى دعم Aspose](https://forum.aspose.com/c/cells/9).
### كيف يمكنني الحصول على ترخيص مؤقت لـ Aspose.Cells؟  
يمكنك التقدم بطلب للحصول على ترخيص مؤقت [هنا](https://purchase.aspose.com/temporary-license/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}