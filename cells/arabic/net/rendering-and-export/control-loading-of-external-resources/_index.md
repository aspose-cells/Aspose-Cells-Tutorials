---
title: التحكم في الموارد الخارجية في Excel إلى PDF في Aspose.Cells
linktitle: التحكم في الموارد الخارجية في Excel إلى PDF في Aspose.Cells
second_title: واجهة برمجة تطبيقات معالجة Excel الخاصة بـ Aspose.Cells .NET
description: اكتشف كيفية التحكم في الموارد الخارجية في تحويل Excel إلى PDF باستخدام Aspose.Cells لـ .NET من خلال دليلنا السهل المتابعة.
weight: 12
url: /ar/net/rendering-and-export/control-loading-of-external-resources/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# التحكم في الموارد الخارجية في Excel إلى PDF في Aspose.Cells

## مقدمة
في العصر الرقمي الحالي، يعد تحويل جداول بيانات Excel إلى مستندات PDF مهمة شائعة. سواء كنت تقوم بإعداد التقارير أو البيانات المالية أو مواد العرض التقديمي، فأنت تريد التأكد من أن ملفات PDF الخاصة بك تبدو بالضبط كما تريدها. Aspose.Cells for .NET هي مكتبة قوية تتيح لك التحكم في عملية التحويل هذه حتى أدق التفاصيل، وخاصة عند التعامل مع الموارد الخارجية مثل الصور التي تصاحب ملفات Excel الخاصة بك. في هذا الدليل، نتعمق في كيفية التحكم في الموارد الخارجية أثناء عملية تحويل Excel إلى PDF باستخدام Aspose.Cells. لذا، احصل على مشروبك المفضل، ولنبدأ!
## المتطلبات الأساسية
قبل أن ننتقل إلى التفاصيل الدقيقة، دعنا نتأكد من أنك تمتلك كل ما تحتاجه للبدء. إليك قائمة مرجعية سريعة:
1. Visual Studio أو أي بيئة تطوير متكاملة متوافقة مع .NET: ستحتاج إلى بيئة لكتابة واختبار التعليمات البرمجية الخاصة بك.
2.  Aspose.Cells لـ .NET: إذا لم تقم بتثبيته بعد، فتوجه إلى[تنزيلات Aspose](https://releases.aspose.com/cells/net/) الصفحة والحصول على الإصدار الأحدث.
3. المعرفة الأساسية بلغة C#: ستكون المعرفة بلغة البرمجة C# مفيدة. إذا لم تكن متأكدًا من أي مفاهيم، فلا تتردد في البحث عنها.
4. ملف Excel نموذجي: قم بإعداد ملف Excel باستخدام أي موارد خارجية ترغب في تحويلها. يمكنك استخدام ملف العينة المقدم "samplePdfSaveOptions_StreamProvider.xlsx".
5. ملف صورة للاختبار: سيتم استخدامه كمورد خارجي أثناء التحويل. ملف الصورة "newPdfSaveOptions_StreamProvider.png" هو بديل جيد.
## استيراد الحزم
لبدء العمل، ستحتاج إلى استيراد مساحات الأسماء الضرورية من مكتبة Aspose.Cells. وهذا أمر بالغ الأهمية للوصول إلى وظائفها. تأكد من إضافة التعليمات التالية باستخدام أعلى الملف:
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
 أول أمر يجب عليك القيام به هو إنشاء فئة موفر البث التي تنفذ`IStreamProvider` ستتيح لك هذه الفئة التحكم في كيفية تحميل الموارد الخارجية.
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
- CloseStream: سيتم استدعاء هذه الطريقة عند إغلاق الدفق. في الوقت الحالي، نقوم فقط بكتابة رسالة تصحيح للتتبع.
-  InitStream: هنا تبدأ السحر. هنا، ستقرأ صورتك الخارجية كمجموعة بايتات، وتحولها إلى مجرى ذاكرة، وتعينها إلى`options.Stream` ملكية.
## الخطوة 2: إعداد أدلة المصدر والإخراج
الآن بعد أن أصبح موفر البث الخاص بك جاهزًا، فقد حان الوقت لتحديد مكان وجود ملف Excel والمكان الذي تريد حفظ ملف PDF فيه.
```csharp
// دليل المصدر
string sourceDir = "Your Document Directory";
// دليل الإخراج
string outputDir = "Your Document Directory";
```
 ببساطة استبدل`"Your Document Directory"` مع المسار الفعلي على جهاز الكمبيوتر الخاص بك حيث توجد ملفاتك. يعد الحفاظ على تنظيم ملفاتك أمرًا بالغ الأهمية!
## الخطوة 3: تحميل ملف Excel الخاص بك
بعد ذلك، ستقوم بتحميل ملف Excel الذي تريد إنشاء ملف PDF منه.
```csharp
// تحميل ملف Excel المصدر الذي يحتوي على صور خارجية
Workbook wb = new Workbook(sourceDir + "samplePdfSaveOptions_StreamProvider.xlsx");
```
 نحن نستخدم`Workbook` الفئة من Aspose.Cells، والتي تمثل ملف Excel الخاص بك. يمكن أن يتضمن الملف موارد خارجية متنوعة مثل الصور التي تريد التحكم فيها أثناء التحويل.
## الخطوة 4: تعيين خيارات حفظ PDF
قبل حفظ المصنف بتنسيق PDF، دعنا نحدد الطريقة التي تريد حفظه بها. يمكنك تعديل هذه الخيارات وفقًا لمتطلباتك.
```csharp
// تحديد خيارات حفظ ملف PDF - موفر البث
PdfSaveOptions opts = new PdfSaveOptions();
opts.OnePagePerSheet = true; // احفظ كل ورقة في صفحة جديدة
```
 هنا، نقوم بإنشاء مثيل جديد لـ`PdfSaveOptions` ، مما يسمح لك بتخصيص كيفية تنسيق ملف PDF الخاص بك.`OnePagePerSheet`يعد هذا الخيار مفيدًا لضمان حصول كل ورقة Excel على صفحة خاصة بها في ملف PDF النهائي.
## الخطوة 5: تعيين موفر البث الخاص بك
بعد تعيين خيارات PDF الخاصة بك، يتعين عليك إخبار Aspose باستخدام موفر البث المخصص للموارد الخارجية.
```csharp
wb.Settings.StreamProvider = new MyStreamProvider();
```
 هذا الخط يربطك`Workbook` مثال مع`MyStreamProvider` الفئة التي أنشأتها سابقًا. وهذا يعني أنه عند مواجهة موارد خارجية أثناء التحويل، سيتعامل معها مزود الخدمة الخاص بك كما هو محدد.
## الخطوة 6: احفظ المصنف بصيغة PDF
بعد إعداد كل شيء، حان الوقت أخيرًا لحفظ مصنف Excel الخاص بك بتنسيق PDF.
```csharp
// حفظ المصنف بصيغة Pdf
wb.Save(outputDir + "outputPdfSaveOptions_StreamProvider.pdf", opts);
```
 من خلال الاتصال`Save` من خلال تطبيق الطريقة على كائن المصنف وتمرير دليل الإخراج الخاص بك مع خيارات PDF، يمكنك تحويل ملف Excel إلى ملف PDF منسق بشكل جميل.
## الخطوة 7: تأكيد التنفيذ الناجح
ولاختتام الأمر، من الجميل دائمًا التأكد من نجاح عمليتك!
```csharp
Console.WriteLine("ControlLoadingOfExternalResourcesInExcelToPDF executed successfully.\r\n");
```
إن طباعة رسالة نجاح على وحدة التحكم يساعدك على البقاء على اطلاع بحالة العملية. ومن الجيد تضمين هذه التأكيدات الصغيرة في الكود الخاص بك.
## خاتمة
هذا كل ما في الأمر! باتباع هذه الخطوات البسيطة، يمكنك التحكم بمهارة في كيفية التعامل مع الموارد الخارجية أثناء تحويل ملفات Excel إلى PDF باستخدام Aspose.Cells. وهذا يعني أن مستنداتك يمكنها الآن تضمين الصور والعناصر الخارجية الأخرى بدقة، مما يضمن الحصول على منتج نهائي مصقول في كل مرة.
## الأسئلة الشائعة
### ما هو Aspose.Cells؟  
Aspose.Cells هي مكتبة قوية لمطوري .NET تتيح لك إنشاء ملفات Excel ومعالجتها وتحويلها وعرضها بتنسيقات مختلفة.
### كيف يمكنني تنزيل Aspose.Cells؟  
 يمكنك تنزيل أحدث إصدار من Aspose.Cells من[رابط التحميل](https://releases.aspose.com/cells/net/).
### هل يمكنني تجربة Aspose.Cells مجانًا؟  
 نعم! يمكنك الحصول على نسخة تجريبية مجانية من خلال زيارة[صفحة التجربة المجانية](https://releases.aspose.com/).
### أين يمكنني العثور على الدعم لـ Aspose.Cells؟  
 لأي استفسارات تتعلق بالدعم، يمكنك زيارة[منتدى دعم Aspose](https://forum.aspose.com/c/cells/9).
### كيف يمكنني الحصول على ترخيص مؤقت لـ Aspose.Cells؟  
 يمكنك التقدم بطلب للحصول على ترخيص مؤقت[هنا](https://purchase.aspose.com/temporary-license/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
