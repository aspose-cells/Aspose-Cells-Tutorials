---
title: إضافة إشارات مرجعية لملفات PDF مع وجهات مسماة في Aspose.Cells
linktitle: إضافة إشارات مرجعية لملفات PDF مع وجهات مسماة في Aspose.Cells
second_title: واجهة برمجة تطبيقات معالجة Excel الخاصة بـ Aspose.Cells .NET
description: تعرف على كيفية إنشاء ملفات PDF تفاعلية تحتوي على إشارات مرجعية باستخدام Aspose.Cells for .NET. هذا الدليل التفصيلي يجعل الأمر سهلاً.
weight: 10
url: /ar/net/rendering-and-export/add-pdf-bookmarks/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إضافة إشارات مرجعية لملفات PDF مع وجهات مسماة في Aspose.Cells

## مقدمة
إذا سبق لك العمل مع مستندات PDF طويلة، فأنت تعلم مدى صعوبة التنقل عبر الصفحات تلو الصفحات من المعلومات. تلعب الإشارات المرجعية دورًا حيويًا في تحسين تجربة المستخدم من خلال تقديم نقاط تنقل سريعة. في هذا البرنامج التعليمي، سنستكشف كيفية إضافة إشارات مرجعية ذات وجهات مسماة في ملف PDF تم إنشاؤه من ملف Excel باستخدام Aspose.Cells for .NET.
## المتطلبات الأساسية
قبل أن ننتقل إلى التفاصيل الدقيقة، دعنا نتأكد من أن كل شيء في مكانه الصحيح. لمتابعة هذا البرنامج التعليمي، ستحتاج إلى:
1. Visual Studio: هو بيئة التطوير المتكاملة المثالية لتطوير .NET. تأكد من تثبيته على جهازك.
2.  Aspose.Cells لـ .NET: يجب أن يكون لديك مكتبات Aspose.Cells. يمكنك[تحميله هنا](https://releases.aspose.com/cells/net/) إذا كنت تريد تجربته أولاً، فاحصل على[تجربة مجانية هنا](https://releases.aspose.com/).
3. .NET Framework: تأكد من تثبيت إصدار متوافق. يدعم Aspose.Cells إصدارات متعددة من .NET.
4. المعرفة الأساسية بلغة C#: إن فهم قواعد لغة C# سيساعدك على فهم مقتطفات التعليمات البرمجية بشكل أفضل.
بفضل هذه العناصر الموجودة في مجموعة أدواتك، أصبحنا جاهزين لإنشاء مستند PDF يحتوي على إشارات مرجعية!
## استيراد الحزم
أولاً، نحتاج إلى التأكد من أن مشروعنا يمكنه الاستفادة من وظائف Aspose.Cells. ابدأ بإنشاء مشروع C# جديد في Visual Studio. بعد ذلك، ستحتاج إلى استيراد الحزم الضرورية. ستفعل ذلك عادةً في أعلى ملف التعليمات البرمجية الخاص بك:
```csharp
using System;
using System.Collections;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Aspose.Cells.Rendering;
using System.Drawing.Imaging;
```
هل ترى مدى سهولة ذلك؟ إن إضافة بضعة أسطر فقط ستفتح لك مجموعة أدوات قوية للتعامل مع ملفات Excel.
## الخطوة 1: إعداد الدلائل
لبدء العمل، ستحتاج إلى تحديد دليل المصدر والإخراج. هذا هو المكان الذي يوجد فيه ملف Excel الأولي ومكان حفظ ملف PDF.
```csharp
string sourceDir = "Your Document Directory"; // على سبيل المثال، "C:\\MyFiles\\"
string outputDir = "Your Document Directory"; // على سبيل المثال، "C:\\MyOutput\\"
```
فكر في هذه الخطوة باعتبارها تحضيرًا لمساحة العمل الخاصة بك. فكما أن الرسام لن يبدأ العمل بدون حامل أو لوحة قماشية، فلا ينبغي لك أن تبدأ في كتابة التعليمات البرمجية دون تحديد مواقع الملفات الخاصة بك.
## الخطوة 2: تحميل ملف Excel المصدر
بعد ذلك، نحتاج إلى تحميل ملف Excel الخاص بك إلى الذاكرة باستخدام فئة المصنف.
```csharp
Workbook wb = new Workbook(sourceDir + "samplePdfBookmarkEntry_DestinationName.xlsx");
```
إن تحميل المصنف يشبه فتح مستند مليء بالإمكانات. فهو يوفر إمكانية الوصول إلى كافة أوراق العمل والخلايا وإمكانيات التنسيق في ملف Excel الأصلي.
## الخطوة 3: الوصول إلى ورقة العمل
الآن بعد أن قمنا بتحميل المصنف، فلننتقل إلى ورقة العمل الأولى. توجد الخلايا التي سنشير إليها لإشاراتنا المرجعية هنا.
```csharp
Worksheet ws = wb.Worksheets[0];
```
يحتاج كل فنان إلى لوحة رسم! في هذا السيناريو، تعمل ورقة العمل كلوحة رسم، حيث ستحدد الخلايا التي ستحمل العلامات المرجعية.
## الخطوة 4: إنشاء الإشارات المرجعية
### الوصول إلى خلايا محددة
لنقم بإنشاء إشارة مرجعية لخلية معينة، لنقل الخلية C5. سننشئ إدخال إشارة مرجعية، ونربطه بتلك الخلية، ونحدد له اسمًا. 
```csharp
Cell cell = ws.Cells["C5"];
PdfBookmarkEntry bookmarkEntry = new PdfBookmarkEntry();
bookmarkEntry.Text = "Text"; // قم بالتغيير إلى اسم الإشارة المرجعية المفضل لديك
bookmarkEntry.Destination = cell;
bookmarkEntry.DestinationName = "AsposeCells--" + cell.Name;
```
يمكنك التفكير في هذا الأمر على أنه وضع ملاحظة لاصقة على مستندك. يشير العنوان إلى المكان الذي يؤدي إليه الإشارة المرجعية، بينما الوجهة (الخلية C5) هي المكان الذي تأخذك إليه في ملف PDF.
### إضافة إشارات مرجعية فرعية
يمكننا تحسين تجربة المستخدم من خلال إضافة إشارات مرجعية فرعية. سنتمكن الآن من الوصول إلى خليتين إضافيتين (G56 وL4) وإعدادهما كإشارات مرجعية فرعية.
```csharp
cell = ws.Cells["G56"];
PdfBookmarkEntry subbookmarkEntry1 = new PdfBookmarkEntry();
subbookmarkEntry1.Text = "Text1"; // أول إشارة مرجعية فرعية
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
## الخطوة 5: حفظ ملف PDF باستخدام الإشارات المرجعية
### إنشاء خيارات حفظ ملف Pdf
لقد حان الوقت لإنشاء خيارات حفظ PDF وإضافة الإشارة المرجعية التي قمنا بإنشائها.
```csharp
PdfSaveOptions opts = new PdfSaveOptions();
opts.Bookmark = bookmarkEntry;
```
تُعد هذه الخطوة هي المكان الذي تتجمع فيه كل استعداداتك السابقة. فأنت تقول في الأساس: "أريد أن يكون ملف PDF الخاص بي ليس مجرد مستند مسطح، بل دليلاً تفاعليًا!"
### حفظ المستند
وأخيرًا، نحفظ المصنف بتنسيق PDF، ونقوم بدمج إشاراتنا المرجعية في هذا الإجراء.
```csharp
wb.Save(outputDir + "outputPdfBookmarkEntry_DestinationName.pdf", opts);
```
بهذه الطريقة، ستؤتي كل جهودك الشاقة ثمارها في صورة مستند PDF منظم جيدًا ومليء بالإشارات المرجعية المفيدة!
## خاتمة
تهانينا! لقد نجحت في إنشاء ملف PDF يحتوي على إشارات مرجعية ووجهات مسماة باستخدام Aspose.Cells for .NET. لقد تعلمت كيفية التنقل عبر ملفات Excel والوصول إلى خلايا معينة وإنشاء إشارات مرجعية تعزز تفاعل المستخدم. تخيل فقط مدى سهولة التنقل عبر مستندات PDF الخاصة بك باستخدام هذه الإشارات المرجعية المفيدة.
## الأسئلة الشائعة
### ما هو Aspose.Cells لـ .NET؟
Aspose.Cells هي مكتبة قوية للعمل مع ملفات Excel، مما يسمح لك بإنشاء جداول البيانات وتعديلها وتحويلها برمجيًا.
### هل يمكنني استخدام Aspose.Cells في مشروع مجاني؟
نعم! تقدم Aspose نسخة تجريبية مجانية إذا كنت ترغب في استكشاف ميزاتها قبل شراء الترخيص.
### كيف يمكنني الحصول على ترخيص لـ Aspose.Cells؟
 يمكنك شراء الترخيص مباشرة منهم[صفحة الشراء](https://purchase.aspose.com/buy).
### ما هي أنواع المستندات التي يمكن لـ Aspose.Cells العمل معها؟
يمكنه العمل مع تنسيقات مختلفة، بما في ذلك XLSX، XLS، CSV، PDF، وغيرها الكثير.
### أين يمكنني الحصول على المساعدة إذا واجهت مشاكل؟
 يمكنك العثور على الدعم في[منتديات اسبوس](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
