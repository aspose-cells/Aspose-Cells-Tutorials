---
"description": "تعرّف على كيفية إنشاء ملفات PDF تفاعلية مع إشارات مرجعية باستخدام Aspose.Cells لـ .NET. هذا الدليل المفصّل يُسهّل الأمر."
"linktitle": "إضافة إشارات مرجعية لملفات PDF مع وجهات مسماة في Aspose.Cells"
"second_title": "واجهة برمجة تطبيقات معالجة Excel Aspose.Cells .NET"
"title": "إضافة إشارات مرجعية لملفات PDF مع وجهات مسماة في Aspose.Cells"
"url": "/ar/net/rendering-and-export/add-pdf-bookmarks/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# إضافة إشارات مرجعية لملفات PDF مع وجهات مسماة في Aspose.Cells

## مقدمة
إذا سبق لك العمل مع مستندات PDF طويلة، فأنت تعلم مدى صعوبة التنقل بين صفحات المعلومات. تلعب الإشارات المرجعية دورًا حيويًا في تحسين تجربة المستخدم من خلال توفير نقاط تنقل سريعة. في هذا البرنامج التعليمي، سنستكشف كيفية إضافة إشارات مرجعية ذات وجهات مُسمّاة في ملف PDF مُنشأ من ملف Excel باستخدام Aspose.Cells لـ .NET.
## المتطلبات الأساسية
قبل أن ندخل في التفاصيل، لنتأكد من أن كل شيء جاهز. لمتابعة هذا البرنامج التعليمي، ستحتاج إلى:
1. Visual Studio: بيئة التطوير المتكاملة المثالية لتطوير .NET. تأكد من تثبيته على جهازك.
2. Aspose.Cells لـ .NET: يجب أن يكون لديك مكتبات Aspose.Cells. يمكنك [قم بتحميله هنا](https://releases.aspose.com/cells/net/)إذا كنت تريد تجربته أولاً، فاحصل على [تجربة مجانية هنا](https://releases.aspose.com/).
3. إطار عمل .NET: تأكد من تثبيت إصدار متوافق. يدعم Aspose.Cells إصدارات متعددة من .NET.
4. المعرفة الأساسية بلغة C#: إن فهم قواعد لغة C# سيساعدك على فهم مقتطفات التعليمات البرمجية بشكل أفضل.
بفضل هذه العناصر الموجودة في مجموعة أدواتك، أصبحنا جاهزين لإنشاء مستند PDF يحتوي على إشارات مرجعية!
## استيراد الحزم
أولاً، علينا التأكد من أن مشروعنا قادر على استخدام وظائف Aspose.Cells. ابدأ بإنشاء مشروع C# جديد في Visual Studio. بعد ذلك، ستحتاج إلى استيراد الحزم اللازمة. عادةً ما تفعل ذلك في أعلى ملف الكود الخاص بك:
```csharp
using System;
using System.Collections;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Aspose.Cells.Rendering;
using System.Drawing.Imaging;
```
هل ترى مدى سهولة ذلك؟ مجرد إضافة بضعة أسطر سيفتح لك مجموعة أدوات فعّالة للتعامل مع ملفات Excel.
## الخطوة 1: إعداد الدلائل
للبدء، ستحتاج إلى تحديد مجلدي المصدر والإخراج. هذا هو المكان الذي يوجد فيه ملف Excel الأصلي، وهو المكان الذي سيتم حفظ ملف PDF فيه.
```csharp
string sourceDir = "Your Document Directory"; // على سبيل المثال، "C:\\MyFiles\\"
string outputDir = "Your Document Directory"; // على سبيل المثال، "C:\\MyOutput\\"
```
اعتبر هذه الخطوة بمثابة تجهيز مساحة عملك. فكما أن الرسام لا يبدأ بدون حامل أو لوحة رسم، لا تبدأ البرمجة دون تحديد مواقع ملفاتك.
## الخطوة 2: تحميل ملف Excel المصدر
بعد ذلك، نحتاج إلى تحميل ملف Excel الخاص بك إلى الذاكرة باستخدام فئة المصنف.
```csharp
Workbook wb = new Workbook(sourceDir + "samplePdfBookmarkEntry_DestinationName.xlsx");
```
تحميل مصنف العمل أشبه بفتح مستند مليء بالإمكانات. فهو يتيح الوصول إلى جميع أوراق العمل والخلايا وخيارات التنسيق في ملف Excel الأصلي.
## الخطوة 3: الوصول إلى ورقة العمل
بعد تحميل مصنفنا، لننتقل إلى ورقة العمل الأولى. ستجد هنا الخلايا التي سنستخدمها للإشارة المرجعية.
```csharp
Worksheet ws = wb.Worksheets[0];
```
يحتاج كل فنان إلى لوحة رسم! في هذه الحالة، ستكون ورقة العمل بمثابة لوحة الرسم، حيث ستحدد الخلايا التي ستحتوي على العلامات المرجعية.
## الخطوة 4: إنشاء الإشارات المرجعية
### الوصول إلى خلايا محددة
لننشئ إشارة مرجعية لخلية محددة، لنفترض الخلية C5. سننشئ مدخل إشارة مرجعية، ونربطه بتلك الخلية، ونُسمّيه اسمًا. 
```csharp
Cell cell = ws.Cells["C5"];
PdfBookmarkEntry bookmarkEntry = new PdfBookmarkEntry();
bookmarkEntry.Text = "Text"; // التغيير إلى اسم الإشارة المرجعية المفضل لديك
bookmarkEntry.Destination = cell;
bookmarkEntry.DestinationName = "AsposeCells--" + cell.Name;
```
يمكنك تشبيه هذا بوضع ملاحظة لاصقة على مستندك. يشير العنوان إلى ما تقود إليه إشارتك المرجعية، بينما الوجهة (الخلية C5) هي المكان الذي تأخذك إليه في ملف PDF.
### إضافة إشارات مرجعية فرعية
يمكننا تحسين تجربة المستخدم بإضافة إشارات مرجعية فرعية. سنصل الآن إلى خليتين إضافيتين (G56 وL4) ونُعدّهما كإشارات مرجعية فرعية.
```csharp
cell = ws.Cells["G56"];
PdfBookmarkEntry subbookmarkEntry1 = new PdfBookmarkEntry();
subbookmarkEntry1.Text = "Text1"; // الإشارة المرجعية الفرعية الأولى
subbookmarkEntry1.Destination = cell;
subbookmarkEntry1.DestinationName = "AsposeCells--" + cell.Name;
cell = ws.Cells["L4"];
PdfBookmarkEntry subbookmarkEntry2 = new PdfBookmarkEntry();
subbookmarkEntry2.Text = "Text2"; // الإشارة المرجعية الفرعية الثانية
subbookmarkEntry2.Destination = cell;
subbookmarkEntry2.DestinationName = "AsposeCells--" + cell.Name;
```
تعمل هذه الإشارات المرجعية الفرعية مثل فصول الكتاب، حيث توجه المستخدمين إلى محتوى أكثر تحديدًا داخل المستند.
### إضافة إشارات مرجعية فرعية إلى القائمة
بعد ذلك، سنقوم بتجميع الإشارات المرجعية الفرعية لدينا أسفل الإشارة المرجعية الرئيسية التي أنشأناها سابقًا.
```csharp
ArrayList list = new ArrayList();
list.Add(subbookmarkEntry1);
list.Add(subbookmarkEntry2);
bookmarkEntry.SubEntry = list;
```
يؤدي هذا التنظيم إلى إنشاء هيكل هرمي يسهل عملية التنقل - التزم بـ "أساسيات وضع الإشارات المرجعية" للحصول على تجربة مستخدم مثالية!
## الخطوة 5: حفظ ملف PDF مع الإشارات المرجعية
### إنشاء خيارات حفظ ملف Pdf
لقد حان الوقت لإنشاء خيارات حفظ PDF وإضافة الإشارة المرجعية التي قمنا بإنشائها.
```csharp
PdfSaveOptions opts = new PdfSaveOptions();
opts.Bookmark = bookmarkEntry;
```
في هذه الخطوة، تجتمع كل استعداداتك السابقة. أنت تقول ببساطة: "أريد أن يكون ملف PDF الخاص بي ليس مجرد مستند عادي، بل دليلاً تفاعليًا!"
### حفظ المستند
وأخيرًا، نقوم بحفظ المصنف بتنسيق PDF، مع دمج إشاراتنا المرجعية في هذا الإجراء.
```csharp
wb.Save(outputDir + "outputPdfBookmarkEntry_DestinationName.pdf", opts);
```
بهذه السهولة، ستجني ثمار كل عملك الشاق من خلال الحصول على مستند PDF منظم جيدًا ومليء بالإشارات المرجعية المفيدة!
## خاتمة
تهانينا! لقد نجحت في إنشاء ملف PDF مع إشارات مرجعية ووجهات مُسمّاة باستخدام Aspose.Cells لـ .NET. لقد تعلمت كيفية التنقل عبر ملفات Excel، والوصول إلى خلايا مُحددة، وإنشاء إشارات مرجعية تُحسّن تفاعل المستخدم. تخيّل كم سيكون التنقل في مستندات PDF أسهل باستخدام هذه الإشارات المرجعية المفيدة.
## الأسئلة الشائعة
### ما هو Aspose.Cells لـ .NET؟
Aspose.Cells هي مكتبة قوية للعمل مع ملفات Excel، مما يسمح لك بإنشاء جداول البيانات وتعديلها وتحويلها برمجيًا.
### هل يمكنني استخدام Aspose.Cells في مشروع مجاني؟
نعم! يُقدّم Aspose نسخة تجريبية مجانية إذا كنت ترغب في استكشاف ميزاته قبل شراء ترخيص.
### كيف يمكنني الحصول على ترخيص لـ Aspose.Cells؟
يمكنك شراء الترخيص مباشرة منهم [صفحة الشراء](https://purchase.aspose.com/buy).
### ما هي أنواع المستندات التي يمكن لـ Aspose.Cells العمل معها؟
يمكنه العمل مع تنسيقات مختلفة، بما في ذلك XLSX، XLS، CSV، PDF، وغيرها الكثير.
### أين يمكنني الحصول على المساعدة إذا واجهت مشاكل؟
يمكنك العثور على الدعم في [منتديات Aspose](https://forum.aspose.com/c/cells/9).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}