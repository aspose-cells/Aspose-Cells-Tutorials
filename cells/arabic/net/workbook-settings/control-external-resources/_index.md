---
title: التحكم في الموارد الخارجية باستخدام إعدادات المصنف
linktitle: التحكم في الموارد الخارجية باستخدام إعدادات المصنف
second_title: واجهة برمجة تطبيقات معالجة Excel الخاصة بـ Aspose.Cells .NET
description: تعرف على كيفية التحكم في الموارد الخارجية في Excel باستخدام Aspose.Cells for .NET من خلال البرنامج التعليمي الشامل الخاص بنا خطوة بخطوة.
weight: 10
url: /ar/net/workbook-settings/control-external-resources/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# التحكم في الموارد الخارجية باستخدام إعدادات المصنف

## مقدمة
في عالم معالجة البيانات وتقديمها، يمكن أن يكون التعامل مع الموارد الخارجية بكفاءة أمرًا بالغ الأهمية. إذا كنت تعمل مع ملفات Excel وترغب في إدارة الموارد الخارجية بسلاسة باستخدام Aspose.Cells for .NET، فقد وصلت إلى المكان الصحيح! في هذه المقالة، سنخوض بعمق في التحكم في الموارد الخارجية عند العمل مع مصنفات Excel. بحلول نهاية هذا الدليل، ستتمكن من تنفيذ حل مخصص لتحميل الصور والبيانات من مصادر خارجية دون عناء.
## المتطلبات الأساسية
قبل أن ننتقل إلى التفاصيل الدقيقة للترميز، هناك بعض المتطلبات الأساسية التي يجب أن تتوفر لديك. تأكد من:
1. احصل على Visual Studio: ستحتاج إلى بيئة تطوير متكاملة لكتابة تطبيقات .NET واختبارها. يعد Visual Studio الخيار الأكثر موصى به نظرًا للدعم الشامل وسهولة الاستخدام.
2.  تنزيل Aspose.Cells لـ .NET: إذا لم تقم بذلك بالفعل، فاحصل على مكتبة Aspose.Cells من[رابط التحميل](https://releases.aspose.com/cells/net/). 
3. الفهم الأساسي للغة C#: إن الإلمام بمفاهيم C# وإطار عمل .NET سيجعل العملية أكثر سلاسة بالنسبة لك.
4. إعداد البيئة الخاصة بك: تأكد من أن مشروعك يشير إلى مكتبة Aspose.Cells. يمكنك القيام بذلك عبر NuGet Package Manager ضمن Visual Studio.
5. ملفات العينة: قم بإعداد ملف Excel نموذجي يتضمن موردًا خارجيًا، مثل صورة مرتبطة. سيساعدك هذا الملف في توضيح الوظائف التي نناقشها.
بمجرد إعدادك لهذه العناصر، ستكون جاهزًا للتعمق في التحكم في الموارد الخارجية باستخدام Aspose.Cells.
## استيراد الحزم
للبدء في كتابة التعليمات البرمجية، ستحتاج إلى استيراد الحزم اللازمة في ملف C# الخاص بك. إليك ما تحتاجه:
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
 دعنا نقسمها إلى خطوات يمكن إدارتها لمساعدتك في التحكم في الموارد الخارجية باستخدام`Workbook Settings`سنشرح لك كيفية إنشاء موفر بث مخصص، وتحميل ملف Excel، وعرض ورقة عمل على صورة. لا تتردد في المتابعة!
## الخطوة 1: تحديد أدلة المصدر والإخراج
للبدء، نحتاج إلى تحديد الدلائل التي سنقرأ منها ملفاتنا والأماكن التي سنحفظ فيها مخرجاتنا. من الضروري تحديد المسارات الصحيحة لتجنب أخطاء عدم العثور على الملف.
```csharp
// دليل المصدر
static string sourceDir = "Your Document Directory";
// دليل الإخراج
static string outputDir = "Your Document Directory";
```
 يستبدل`"Your Document Directory"` مع المسار الفعلي الذي توجد به ملفاتك.
## الخطوة 2: تنفيذ واجهة IStreamProvider
 بعد ذلك، سنقوم بإنشاء فئة مخصصة لتنفيذ`IStreamProvider` ستتولى هذه الفئة إدارة كيفية الوصول إلى الموارد الخارجية (مثل الصور).
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
 في`InitStream` الطريقة هي أننا نفتح الملف الذي يعمل كمورد خارجي ونقوم بتعيينه إلى`Stream`الخاصية. يسمح هذا للمصنف بالوصول إلى المورد عند العرض.
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
 في هذا المقطع، نقوم بتحميل ملف Excel الخاص بنا وتعيين ملفنا المخصص`StreamProvider` التنفيذ للتعامل مع الموارد الخارجية.
## الخطوة 4: الوصول إلى ورقة العمل
بعد تحميل المصنف، يمكننا الوصول بسهولة إلى ورقة العمل المطلوبة. فلنأخذ الورقة الأولى.
```csharp
    // الوصول إلى ورقة العمل الأولى
    Worksheet ws = wb.Worksheets[0];
```
إنه أمر بسيط، أليس كذلك؟ يمكنك الوصول إلى أي ورقة عمل من خلال تحديد فهرسها.
## الخطوة 5: تكوين خيارات الصورة أو الطباعة
الآن سنحدد الشكل الذي نريد أن تبدو عليه الصورة الناتجة. وسنقوم بتكوين خيارات مثل التأكد من وجود صفحة واحدة لكل ورقة وتحديد نوع الصورة الناتجة.
```csharp
    // تحديد خيارات الصورة أو الطباعة
    ImageOrPrintOptions opts = new ImageOrPrintOptions();
    opts.OnePagePerSheet = true;
    opts.ImageType = Drawing.ImageType.Png;
```
يضمن اختيار تنسيق PNG كتنسيق الإخراج أن تظل الجودة واضحة ونقية!
## الخطوة 6: تحويل ورقة العمل إلى صورة
بعد إعداد كل شيء، دعنا نحوّل ورقة العمل التي اخترناها إلى ملف صورة! هذا هو الجزء المثير؛ حيث سترى ورقة Excel الخاصة بك تتحول إلى صورة جميلة.
```csharp
    // إنشاء عرض ورقة عن طريق تمرير المعلمات المطلوبة
    SheetRender sr = new SheetRender(ws, opts);
    // تحويل ورقة العمل بأكملها إلى صورة png
    sr.ToImage(0, outputDir + "outputControlExternalResourcesUsingWorkbookSetting_StreamProvider.png");
    
    Console.WriteLine("ControlExternalResourcesUsingWorkbookSetting_StreamProvider executed successfully.");
}
```
 ال`ToImage` تؤدي الوظيفة كل العمل الشاق، وتحويل الورقة إلى صورة. بمجرد اكتمال هذه الخطوة، ستجد الصورة محفوظة في دليل الإخراج الخاص بك.
## خاتمة
والآن، أصبحت تمتلك المعرفة اللازمة للتحكم في الموارد الخارجية عند العمل مع ملفات Excel باستخدام Aspose.Cells في .NET. وهذا لا يعزز قدرات تطبيقك فحسب، بل يجعل التعامل مع مجموعات البيانات والعروض التقديمية أمرًا سهلاً أيضًا. باتباع الخطوات المقدمة، يمكنك بسهولة تكرار هذه الوظيفة وتكييفها لتناسب احتياجات مشروعك المحددة.
## الأسئلة الشائعة
### ما هو Aspose.Cells؟
Aspose.Cells هي مكتبة قوية مصممة لمطوري C# و.NET لإنشاء ملفات Excel ومعالجتها وإدارتها دون الحاجة إلى تثبيت Microsoft Excel.
### كيف يمكنني تنزيل Aspose.Cells لـ .NET؟
 يمكنك تنزيله من[موقع اسبوس](https://releases.aspose.com/cells/net/).
### هل هناك نسخة تجريبية مجانية متاحة؟
 نعم! يمكنك الوصول إلى نسخة تجريبية مجانية من Aspose.Cells من موقعهم[صفحة الإصدار](https://releases.aspose.com/).
### ما هي أنواع الملفات التي يدعمها Aspose.Cells؟
يدعم Aspose.Cells تنسيقات Excel المختلفة، بما في ذلك XLS، وXLSX، وCSV، والمزيد.
### أين يمكنني العثور على الدعم لـ Aspose.Cells؟
 يمكنك زيارة منتدى دعم Aspose على[منتدى اسبوس](https://forum.aspose.com/c/cells/9) للحصول على المساعدة.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
