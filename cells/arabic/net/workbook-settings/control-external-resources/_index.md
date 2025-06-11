---
"description": "تعرف على كيفية التحكم في الموارد الخارجية في Excel باستخدام Aspose.Cells لـ .NET من خلال البرنامج التعليمي الشامل الخاص بنا خطوة بخطوة."
"linktitle": "التحكم في الموارد الخارجية باستخدام إعدادات المصنف"
"second_title": "واجهة برمجة تطبيقات معالجة Excel Aspose.Cells .NET"
"title": "التحكم في الموارد الخارجية باستخدام إعدادات المصنف"
"url": "/ar/net/workbook-settings/control-external-resources/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# التحكم في الموارد الخارجية باستخدام إعدادات المصنف

## مقدمة
في مجال معالجة البيانات وعرضها، تُحدث معالجة الموارد الخارجية بكفاءة نقلة نوعية. إذا كنت تعمل على ملفات Excel وترغب في إدارة الموارد الخارجية بسلاسة باستخدام Aspose.Cells لـ .NET، فأنت في المكان المناسب! في هذه المقالة، سنتعمق في كيفية التحكم في الموارد الخارجية عند العمل مع مصنفات Excel. بنهاية هذا الدليل، ستتمكن من تطبيق حل مُخصص لتحميل الصور والبيانات من مصادر خارجية بسهولة.
## المتطلبات الأساسية
قبل أن نتعمق في تفاصيل البرمجة، هناك بعض المتطلبات الأساسية التي يجب توافرها. تأكد من:
1. استخدم Visual Studio: ستحتاج إلى بيئة تطوير متكاملة لكتابة تطبيقات .NET واختبارها. يُعد Visual Studio الخيار الأمثل بفضل دعمه الشامل وسهولة استخدامه.
2. تنزيل Aspose.Cells لـ .NET: إذا لم تقم بذلك بالفعل، فاحصل على مكتبة Aspose.Cells من [رابط التحميل](https://releases.aspose.com/cells/net/). 
3. الفهم الأساسي للغة C#: إن الإلمام بمفاهيم C# وإطار عمل .NET سيجعل العملية أكثر سلاسة بالنسبة لك.
4. إعداد بيئتك: تأكد من أن مشروعك يعتمد على مكتبة Aspose.Cells. يمكنك القيام بذلك عبر مدير الحزم NuGet ضمن Visual Studio.
5. ملفات نموذجية: جهّز ملف Excel نموذجيًا يتضمن موردًا خارجيًا، مثل صورة مرتبطة. سيساعدك هذا الملف على توضيح الوظائف التي نناقشها.
بمجرد إعدادك لهذه العناصر، ستكون جاهزًا للتعمق في التحكم في الموارد الخارجية باستخدام Aspose.Cells.
## استيراد الحزم
لبدء البرمجة، ستحتاج إلى استيراد الحزم اللازمة في ملف C#. إليك ما تحتاجه:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.IO;
using Aspose.Cells.Rendering;
using System.Drawing.Imaging;
```
توفر هذه المساحات الأسماء إمكانية الوصول إلى الوظائف المطلوبة لمعالجة ملفات Excel ومعالجة الصور.
دعنا نقسمها إلى خطوات يمكن التحكم فيها لمساعدتك في التحكم في الموارد الخارجية باستخدام `Workbook Settings`سنشرح كيفية إنشاء موفر بث مخصص، وتحميل ملف إكسل، وتحويل ورقة العمل إلى صورة. تابعونا!
## الخطوة 1: تحديد أدلة المصدر والإخراج
للبدء، علينا تحديد المجلدات التي سنقرأ منها ملفاتنا ونحفظ مخرجاتنا. من الضروري تحديد المسارات الصحيحة لتجنب أخطاء عدم العثور على الملف.
```csharp
// دليل المصدر
static string sourceDir = "Your Document Directory";
// دليل الإخراج
static string outputDir = "Your Document Directory";
```
يستبدل `"Your Document Directory"` مع المسار الفعلي الذي توجد به ملفاتك.
## الخطوة 2: تنفيذ واجهة IStreamProvider
بعد ذلك، سنقوم بإنشاء فئة مخصصة لتنفيذ `IStreamProvider` ستتولى هذه الفئة إدارة كيفية الوصول إلى الموارد الخارجية (مثل الصور).
```csharp
class SP : IStreamProvider
{
    public void CloseStream(StreamProviderOptions options)
    {
        // تنظيف أي موارد إذا لزم الأمر
    }
    public void InitStream(StreamProviderOptions options)
    {
        // فتح مجرى الملفات للمورد الخارجي
        FileStream fi = new FileStream(sourceDir + "sampleControlExternalResourcesUsingWorkbookSetting_StreamProvider.png", FileMode.OpenOrCreate, FileAccess.Read);
        options.Stream = fi;
    }
}
```
في `InitStream` الطريقة هي أننا نفتح الملف الذي يعمل كمورد خارجي ونقوم بتعيينه إلى `Stream` الخاصية. يسمح هذا للمصنف بالوصول إلى المورد عند العرض.
## الخطوة 3: تحميل ملف Excel
الآن بعد أن أصبح مزود البث جاهزًا، فلنقم بتحميل مصنف Excel الذي يحتوي على المورد الخارجي.
```csharp
public static void Run()
{
    // تحميل ملف Excel النموذجي
    Workbook wb = new Workbook(sourceDir + "sampleControlExternalResourcesUsingWorkbookSetting_StreamProvider.xlsx");
    
    // توفير تنفيذك لـ IStreamProvider
    wb.Settings.StreamProvider = new SP();
```
في هذا المقطع، نقوم بتحميل ملف Excel الخاص بنا وتعيين الإعدادات المخصصة لدينا `StreamProvider` التنفيذ للتعامل مع الموارد الخارجية.
## الخطوة 4: الوصول إلى ورقة العمل
بعد تحميل المصنف، يُمكننا الوصول بسهولة إلى ورقة العمل المطلوبة. لنبدأ بالأولى.
```csharp
    // الوصول إلى ورقة العمل الأولى
    Worksheet ws = wb.Worksheets[0];
```
الأمر بسيط، أليس كذلك؟ يمكنك الوصول إلى أي ورقة عمل بتحديد فهرسها.
## الخطوة 5: تكوين خيارات الصورة أو الطباعة
سنحدد الآن شكل الصورة الناتجة. سنضبط خيارات مثل تخصيص صفحة واحدة لكل ورقة، وتحديد نوع الصورة الناتجة.
```csharp
    // تحديد خيارات الصورة أو الطباعة
    ImageOrPrintOptions opts = new ImageOrPrintOptions();
    opts.OnePagePerSheet = true;
    opts.ImageType = Drawing.ImageType.Png;
```
يضمن اختيار PNG كتنسيق الإخراج أن تظل الجودة واضحة ونقية!
## الخطوة 6: تحويل ورقة العمل إلى صورة
بعد إعداد كل شيء، لنحوّل ورقة العمل التي اخترناها إلى ملف صورة! هذا هو الجزء المثير؛ ستشاهد ورقة Excel الخاصة بك وقد تحولت إلى صورة جميلة.
```csharp
    // إنشاء عرض الورقة عن طريق تمرير المعلمات المطلوبة
    SheetRender sr = new SheetRender(ws, opts);
    // تحويل ورقة العمل بأكملها إلى صورة png
    sr.ToImage(0, outputDir + "outputControlExternalResourcesUsingWorkbookSetting_StreamProvider.png");
    
    Console.WriteLine("ControlExternalResourcesUsingWorkbookSetting_StreamProvider executed successfully.");
}
```
ال `ToImage` تقوم هذه الوظيفة بكل العمل الشاق، وهي تحويل الورقة إلى صورة. بعد اكتمال هذه الخطوة، ستجد الصورة محفوظة في مجلد الإخراج.
## خاتمة
ها قد انتهيت! أنت الآن تمتلك الخبرة اللازمة للتحكم في الموارد الخارجية عند العمل مع ملفات Excel باستخدام Aspose.Cells في .NET. هذا لا يُحسّن قدرات تطبيقك فحسب، بل يُسهّل أيضًا التعامل مع مجموعات البيانات والعروض التقديمية. باتباع الخطوات المُقدّمة، يمكنك بسهولة تكرار هذه الوظيفة وتكييفها لتناسب احتياجات مشروعك المُحدّدة.
## الأسئلة الشائعة
### ما هو Aspose.Cells؟
Aspose.Cells هي مكتبة قوية مصممة لمطوري C# و.NET لإنشاء ملفات Excel ومعالجتها وإدارتها دون الحاجة إلى تثبيت Microsoft Excel.
### كيف يمكنني تنزيل Aspose.Cells لـ .NET؟
يمكنك تنزيله من [موقع Aspose](https://releases.aspose.com/cells/net/).
### هل هناك نسخة تجريبية مجانية متاحة؟
نعم! يمكنك الوصول إلى نسخة تجريبية مجانية من Aspose.Cells من [صفحة الإصدار](https://releases.aspose.com/).
### ما هي أنواع الملفات التي يدعمها Aspose.Cells؟
يدعم Aspose.Cells تنسيقات Excel المختلفة، بما في ذلك XLS، وXLSX، وCSV، والمزيد.
### أين يمكنني العثور على الدعم لـ Aspose.Cells؟
يمكنك زيارة منتدى دعم Aspose على [منتدى أسبوزي](https://forum.aspose.com/c/cells/9) للحصول على المساعدة.


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}