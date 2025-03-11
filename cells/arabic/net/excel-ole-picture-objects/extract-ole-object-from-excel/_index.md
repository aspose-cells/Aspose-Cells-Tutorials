---
title: استخراج كائن OLE من Excel
linktitle: استخراج كائن OLE من Excel
second_title: واجهة برمجة تطبيقات معالجة Excel الخاصة بـ Aspose.Cells .NET
description: تعرف على كيفية استخراج كائنات OLE من ملفات Excel باستخدام Aspose.Cells for .NET. دليل خطوة بخطوة لاستخراج سهل.
weight: 10
url: /ar/net/excel-ole-picture-objects/extract-ole-object-from-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# استخراج كائن OLE من Excel

## مقدمة
في عالم اليوم الذي يتميز بالذكاء التكنولوجي، يعد التعامل مع ملفات Excel مهمة شائعة، وخاصة بالنسبة لأولئك الذين يعملون في تحليل البيانات والتمويل وإدارة المشاريع. أحد الجوانب التي غالبًا ما يتم تجاهلها هو التعامل مع كائنات OLE (ربط الكائنات وتضمينها) داخل جداول بيانات Excel. يمكن أن تكون هذه مستندات مضمنة أو صورًا أو حتى أنواع بيانات معقدة تلعب دورًا حاسمًا في تحسين وظائف ملفات Excel وثرائها. إذا كنت مستخدمًا لبرنامج Aspose.Cells وتبحث عن استخراج كائنات OLE هذه برمجيًا باستخدام .NET، فأنت في المكان المناسب! سيرشدك هذا الدليل خلال العملية خطوة بخطوة، مما يضمن فهمك ليس فقط لكيفية القيام بذلك، ولكن أيضًا لماذا كل جزء من العملية مهم.
## المتطلبات الأساسية
قبل أن نتعمق في التفاصيل الدقيقة لاستخراج كائنات OLE، هناك بعض الأشياء التي يجب أن تكون موجودة لديك:
1. المعرفة الأساسية بلغة C#: إذا كنت على دراية بلغة C#، فأنت على الطريق الصحيح بالفعل. وإذا لم تكن كذلك، فلا تقلق! سنبقي الأمور واضحة.
2. تم تثبيت Aspose.Cells: ستحتاج إلى مكتبة Aspose.Cells. يمكنك تنزيلها من الموقع[هنا](https://releases.aspose.com/cells/net/).
3. بيئة تطوير متوافقة: تأكد من إعداد بيئة تطوير .NET، مثل Visual Studio، لتكون جاهزة للاستخدام.
4. ملف Excel نموذجي: ستحتاج إلى ملف Excel يحتوي على كائنات OLE مضمنة للاختبار. 
بمجرد توفر هذه المتطلبات الأساسية، يمكننا أن نبدأ رحلتنا إلى عالم استخراج كائنات OLE.
## استيراد الحزم
أولاً، دعنا نستورد الحزم الضرورية التي سنستخدمها في البرنامج التعليمي الخاص بنا. في مشروع C# الخاص بك، ستحتاج إلى تضمين مساحة اسم Aspose.Cells. وإليك كيفية القيام بذلك:
```csharp
using System.IO;
using Aspose.Cells;
```
## الخطوة 1: تعيين دليل المستندات
في هذه الخطوة، سنحدد المسار الذي يوجد به ملف Excel الخاص بنا. قد تتساءل عن سبب أهمية ذلك. الأمر أشبه بإعداد المسرح لعرض مسرحي، فهو يساعد النص على معرفة مكان العثور على الممثلين (في حالتنا، ملف Excel).
```csharp
string dataDir = "Your Document Directory";
```
 يستبدل`"Your Document Directory"` مع المسار الفعلي الذي يوجد به ملف Excel الخاص بك (`book1.xls`) يتم تخزينها.
## الخطوة 2: افتح ملف Excel
الآن بعد أن قمنا بإعداد دليل المستندات، فإن الخطوة التالية هي فتح ملف Excel. فكر في هذا الأمر كما لو كنت تفتح كتابًا قبل أن تبدأ القراءة، فمن الضروري أن ترى ما بداخله.
```csharp
Workbook workbook = new Workbook(dataDir + "book1.xls");
```
## الخطوة 3: الوصول إلى مجموعة كائنات OLE
يمكن أن تحتوي كل ورقة عمل في مصنف Excel على كائنات مختلفة، بما في ذلك كائنات OLE. هنا، نقوم بالوصول إلى مجموعة كائنات OLE الخاصة بورقة العمل الأولى. الأمر أشبه بتحديد صفحة للتحقق من الصور والمستندات المضمنة.
```csharp
Aspose.Cells.Drawing.OleObjectCollection oles = workbook.Worksheets[0].OleObjects;
```
## الخطوة 4: التكرار عبر كائنات OLE
الآن يأتي الجزء الممتع - التنقل عبر جميع كائنات OLE في مجموعتنا. هذه الخطوة بالغة الأهمية لأنها تسمح لنا بالتعامل مع كائنات OLE متعددة بكفاءة. تخيل أنك تبحث في صندوق كنز للعثور على عناصر قيمة!
```csharp
for (int i = 0; i < oles.Count; i++)
{
    Aspose.Cells.Drawing.OleObject ole = oles[i];
    // مزيد من المنطق للتعامل مع كل كائن
}
```
## الخطوة 5: تحديد اسم ملف الإخراج
مع التعمق أكثر في كل كائن OLE، نحتاج إلى التوصل إلى اسم ملف للكائنات المستخرجة. لماذا؟ لأنه بمجرد استخراجها، نريد الاحتفاظ بكل شيء منظمًا حتى نتمكن من العثور على كنوزنا بسهولة لاحقًا.
```csharp
string fileName = dataDir + "ole_" + i + ".";
```
## الخطوة 6: تحديد نوع تنسيق الملف
يمكن أن يكون كل كائن OLE من أنواع مختلفة (على سبيل المثال، المستندات، وجداول البيانات، والصور). من المهم تحديد نوع التنسيق حتى تتمكن من استخراجه بشكل صحيح. الأمر أشبه بمعرفة وصفة طبق ما - فأنت بحاجة إلى معرفة المكونات!
```csharp
switch (ole.FileFormatType)
{
    case FileFormatType.Doc:
        fileName += "doc";
        break;
    case FileFormatType.Xlsx:
        fileName += "xlsx";
        break;
    case FileFormatType.Ppt:
        fileName += "ppt";
        break;
    case FileFormatType.Pdf:
        fileName += "pdf";
        break;
    case FileFormatType.Unknown:
        fileName += "jpg";
        break;
    default:
        // التعامل مع تنسيقات الملفات الأخرى
        break;
}
```
## الخطوة 7: حفظ كائن OLE
 الآن، دعنا ننتقل إلى حفظ كائن OLE. إذا كان الكائن عبارة عن ملف Excel، فسوف نحفظه باستخدام`MemoryStream` وهو ما يسمح لنا بالتعامل مع البيانات في الذاكرة قبل كتابتها. وهذه الخطوة تشبه تعبئة الكنز قبل إرساله إلى صديق.
```csharp
if (ole.FileFormatType == FileFormatType.Xlsx)
{
    MemoryStream ms = new MemoryStream();
    ms.Write(ole.ObjectData, 0, ole.ObjectData.Length);
    Workbook oleBook = new Workbook(ms);
    oleBook.Settings.IsHidden = false;
    oleBook.Save(dataDir + "Excel_File" + i + ".out.xlsx");
}
```
 بالنسبة للأنواع الأخرى من الملفات، سوف نستخدم`FileStream` لإنشاء الملف على القرص.
```csharp
else
{
    FileStream fs = File.Create(fileName);
    fs.Write(ole.ObjectData, 0, ole.ObjectData.Length);
    fs.Close();
}
```

## خاتمة
وهكذا تكون قد نجحت في الإبحار في مياه استخراج كائنات OLE باستخدام Aspose.Cells for .NET! باتباع هذه الخطوات، يمكنك استخراج الكائنات المضمنة وإدارتها بسهولة من ملفات Excel. تذكر، مثل أي مهارة قيمة، أن الممارسة تؤدي إلى الإتقان. لذا، خذ وقتك في تجربة ملفات Excel المختلفة، وسرعان ما ستصبح محترفًا في استخراج OLE!
## الأسئلة الشائعة
### ما هي كائنات OLE في Excel؟
كائنات OLE هي تقنية تسمح بتضمين المستندات والبيانات وربطها في تطبيقات أخرى داخل ورقة عمل Excel.
### لماذا أحتاج إلى استخراج كائنات OLE؟
يتيح لك استخراج كائنات OLE الوصول إلى المستندات أو الصور المضمنة ومعالجتها بشكل مستقل عن ملف Excel الأصلي.
### هل يمكن لـ Aspose.Cells التعامل مع جميع أنواع الملفات المضمنة؟
نعم، يمكن لـ Aspose.Cells إدارة كائنات OLE المختلفة، بما في ذلك مستندات Word، وجداول بيانات Excel، وعروض PowerPoint، والصور.
### كيف أقوم بتثبيت Aspose.Cells لـ .NET؟
 يمكنك تثبيت Aspose.Cells عن طريق تنزيله من موقعهم[صفحة الإصدار](https://releases.aspose.com/cells/net/).
### أين يمكنني العثور على الدعم لـ Aspose.Cells؟
يمكنك الحصول على الدعم لـ Aspose.Cells على[منتدى الدعم](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
