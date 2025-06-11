---
"description": "تعرّف على كيفية استخراج كائنات OLE من ملفات Excel باستخدام Aspose.Cells لـ .NET. دليل خطوة بخطوة لاستخراج سهل."
"linktitle": "استخراج كائن OLE من Excel"
"second_title": "واجهة برمجة تطبيقات معالجة Excel Aspose.Cells .NET"
"title": "استخراج كائن OLE من Excel"
"url": "/ar/net/excel-ole-picture-objects/extract-ole-object-from-excel/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# استخراج كائن OLE من Excel

## مقدمة
في عالمنا اليوم، الذي يتميز بالتقنية المتطورة، يُعد التعامل مع ملفات Excel مهمة شائعة، خاصةً للعاملين في تحليل البيانات والتمويل وإدارة المشاريع. ومن الجوانب التي غالبًا ما يتم إغفالها معالجة كائنات OLE (ربط الكائنات وتضمينها) داخل جداول بيانات Excel. قد تكون هذه الكائنات مستندات مُضمنة أو صورًا أو حتى أنواع بيانات معقدة تلعب دورًا حاسمًا في تحسين وظائف ملفات Excel وثرائها. إذا كنت من مستخدمي Aspose.Cells وترغب في استخراج كائنات OLE هذه برمجيًا باستخدام .NET، فأنت في المكان المناسب! سيرشدك هذا الدليل خلال العملية خطوة بخطوة، مما يضمن فهمك ليس فقط لكيفية القيام بذلك، بل ولأهمية كل جزء منها.
## المتطلبات الأساسية
قبل أن نتعمق في التفاصيل الدقيقة لاستخراج كائنات OLE، هناك بعض الأشياء التي يجب أن تكون موجودة لديك:
1. المعرفة الأساسية بلغة C#: إذا كنتَ مُلِمًّا بلغة C#، فأنتَ على الطريق الصحيح. وإن لم تكن كذلك، فلا تقلق! سنُوضِّح لك الأمور.
2. تثبيت Aspose.Cells: ستحتاج إلى مكتبة Aspose.Cells. يمكنك تنزيلها من الموقع. [هنا](https://releases.aspose.com/cells/net/).
3. بيئة تطوير متوافقة: تأكد من إعداد بيئة تطوير .NET، مثل Visual Studio، لتكون جاهزة للاستخدام.
4. ملف Excel نموذجي: ستحتاج إلى ملف Excel يحتوي على كائنات OLE مضمنة للاختبار. 
بمجرد توفر هذه المتطلبات الأساسية، يمكننا أن نبدأ رحلتنا إلى عالم استخراج كائنات OLE.
## استيراد الحزم
أولاً، لنستورد الحزم اللازمة التي سنستخدمها في درسنا. في مشروع C#، ستحتاج إلى تضمين مساحة اسم Aspose.Cells. إليك كيفية القيام بذلك:
```csharp
using System.IO;
using Aspose.Cells;
```
## الخطوة 1: تعيين دليل المستندات
في هذه الخطوة، سنحدد مسار ملف إكسل. قد تتساءل عن أهمية هذا. يشبه الأمر تهيئة المسرح لعرض مسرحي، فهو يساعد النص على تحديد مكان الممثلين (في حالتنا، ملف إكسل).
```csharp
string dataDir = "Your Document Directory";
```
يستبدل `"Your Document Directory"` مع المسار الفعلي الذي يوجد به ملف Excel الخاص بك (`book1.xls`) يتم تخزينها.
## الخطوة 2: افتح ملف Excel
بعد إعداد مجلد المستندات، الخطوة التالية هي فتح ملف Excel. تخيل هذا الأمر كأنك تفتح كتابًا قبل أن تبدأ القراءة، فمن الضروري أن ترى محتوياته.
```csharp
Workbook workbook = new Workbook(dataDir + "book1.xls");
```
## الخطوة 3: الوصول إلى مجموعة كائنات OLE
يمكن أن تحتوي كل ورقة عمل في مصنف Excel على كائنات متنوعة، بما في ذلك كائنات OLE. هنا، نصل إلى مجموعة كائنات OLE لورقة العمل الأولى. يشبه الأمر تحديد صفحة لعرض الصور والمستندات المضمنة.
```csharp
Aspose.Cells.Drawing.OleObjectCollection oles = workbook.Worksheets[0].OleObjects;
```
## الخطوة 4: التكرار عبر كائنات OLE
الآن يأتي الجزء الممتع: استعراض جميع كائنات OLE في مجموعتنا. هذه الخطوة بالغة الأهمية لأنها تُمكّننا من التعامل مع كائنات OLE متعددة بكفاءة. تخيّل البحث في صندوق كنز للعثور على أشياء ثمينة!
```csharp
for (int i = 0; i < oles.Count; i++)
{
    Aspose.Cells.Drawing.OleObject ole = oles[i];
    // مزيد من المنطق للتعامل مع كل كائن
}
```
## الخطوة 5: تحديد اسم ملف الإخراج
عند التعمق في كل كائن OLE، نحتاج إلى تحديد اسم ملف للكائنات المستخرجة. لماذا؟ لأنه بمجرد استخراجها، نريد تنظيم كل شيء ليسهل علينا العثور على كنوزنا لاحقًا.
```csharp
string fileName = dataDir + "ole_" + i + ".";
```
## الخطوة 6: تحديد نوع تنسيق الملف
يمكن أن يكون لكل كائن OLE أنواع مختلفة (مثل المستندات، وجداول البيانات، والصور). من الضروري تحديد نوع التنسيق لاستخراجه بشكل صحيح. الأمر أشبه بمعرفة وصفة طبق - عليك معرفة مكوناته!
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
الآن، لننتقل إلى حفظ كائن OLE. إذا كان الكائن ملف Excel، فسنحفظه باستخدام `MemoryStream` مما يسمح لنا بمعالجة البيانات في الذاكرة قبل كتابتها. هذه الخطوة أشبه بتغليف كنزك قبل إرساله إلى صديق.
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
بالنسبة للأنواع الأخرى من الملفات، سنستخدم `FileStream` لإنشاء الملف على القرص.
```csharp
else
{
    FileStream fs = File.Create(fileName);
    fs.Write(ole.ObjectData, 0, ole.ObjectData.Length);
    fs.Close();
}
```

## خاتمة
وهكذا، تكون قد أتقنتَ بنجاح استخراج كائنات OLE باستخدام Aspose.Cells لـ .NET! باتباع هذه الخطوات، يمكنك بسهولة استخراج الكائنات المضمنة وإدارتها من ملفات Excel. تذكر، كما هو الحال مع أي مهارة قيّمة، الممارسة تُكسبك الإتقان. لذا، خصّص وقتًا كافيًا لتجربة ملفات Excel المختلفة، وسرعان ما ستصبح خبيرًا في استخراج بيانات OLE!
## الأسئلة الشائعة
### ما هي كائنات OLE في Excel؟
كائنات OLE هي تقنية تسمح بتضمين المستندات والبيانات وربطها في تطبيقات أخرى داخل ورقة عمل Excel.
### لماذا أحتاج إلى استخراج كائنات OLE؟
يتيح لك استخراج كائنات OLE الوصول إلى المستندات أو الصور المضمنة ومعالجتها بشكل مستقل عن ملف Excel الأصلي.
### هل يمكن لـ Aspose.Cells التعامل مع جميع أنواع الملفات المضمنة؟
نعم، يمكن لـ Aspose.Cells إدارة كائنات OLE المختلفة، بما في ذلك مستندات Word، وجداول بيانات Excel، وعروض PowerPoint، والصور.
### كيف أقوم بتثبيت Aspose.Cells لـ .NET؟
يمكنك تثبيت Aspose.Cells عن طريق تنزيله من موقعهم [صفحة الإصدار](https://releases.aspose.com/cells/net/).
### أين يمكنني العثور على الدعم لـ Aspose.Cells؟
يمكنك الحصول على الدعم لـ Aspose.Cells على [منتدى الدعم](https://forum.aspose.com/c/cells/9).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}