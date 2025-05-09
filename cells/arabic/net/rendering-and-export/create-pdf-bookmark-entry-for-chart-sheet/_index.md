---
"description": "تعرف على كيفية إنشاء إشارات مرجعية بتنسيق PDF لجداول البيانات في Aspose.Cells لـ .NET باستخدام هذا الدليل الشامل خطوة بخطوة."
"linktitle": "إنشاء إشارة مرجعية لملف PDF لورقة الرسم البياني في Aspose.Cells"
"second_title": "واجهة برمجة تطبيقات معالجة Excel Aspose.Cells .NET"
"title": "إنشاء إشارة مرجعية لملف PDF لورقة الرسم البياني في Aspose.Cells"
"url": "/ar/net/rendering-and-export/create-pdf-bookmark-entry-for-chart-sheet/"
"weight": 13
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء إشارة مرجعية لملف PDF لورقة الرسم البياني في Aspose.Cells

## مقدمة
يتيح Aspose.Cells لـ .NET للمطورين التعامل مع ملفات Excel برمجيًا. ومن ميزاته المفيدة إمكانية إنشاء إشارات مرجعية بصيغة PDF لأوراق المخططات الفردية. سيشرح هذا البرنامج التعليمي العملية خطوة بخطوة، مما يُسهّل عليك متابعتها، بغض النظر عن خبرتك البرمجية. جهّز محرر الأكواد، ولنبدأ!
## المتطلبات الأساسية
قبل أن نبدأ، دعونا نتأكد من أن لديك كل ما تحتاجه للمتابعة:
1. Aspose.Cells لـ .NET: ستحتاج إلى مكتبة Aspose.Cells. إذا لم تكن لديك بعد، يمكنك تنزيلها من [هنا](https://releases.aspose.com/cells/net/).
2. Visual Studio أو أي .NET IDE: ستحتاج إلى بيئة تطوير يمكنك من خلالها كتابة وتنفيذ كود C# الخاص بك.
3. الفهم الأساسي للغة C#: في حين أننا سنرشدك خلال كل خطوة، فإن المعرفة الأساسية بترميز C# ستكون مفيدة.
4. ملف إكسل نموذجي: احصل على ملف إكسل نموذجي يحتوي على مخططات بيانية. يمكنك إنشاء ملف بنفسك أو استخدام ملف نموذجي لهذا التمرين.
بمجرد استيفاء هذه المتطلبات الأساسية، ستكون جاهزًا لإنشاء إشارات مرجعية بتنسيق PDF لأوراق المخططات بكل سهولة!
## استيراد الحزم
بعد أن انتهينا من المتطلبات الأساسية، لنبدأ بشرح الكود. قبل البدء بمعالجة ملفات Excel، عليك استيراد الحزم اللازمة. إليك كيفية القيام بذلك:
### إعداد بيئة التطوير الخاصة بك
1. إنشاء مشروع جديد: افتح Visual Studio وأنشئ تطبيق وحدة تحكم C# جديدًا. لنسمِّه "AsposePDFBookmarkExample".
2. إضافة مرجع Aspose.Cells: انقر بزر الماوس الأيمن على مشروعك في مستكشف الحلول، ثم اختر "إدارة حزم NuGet"، وابحث عن "Aspose.Cells". ثبّت أحدث إصدار.
3. إضافة باستخدام التوجيهات:
فيك `Program.cs` الملف، أضف الأسطر التالية في الأعلى:
```csharp
using System;
using System.Collections;
using System.Linq;
using System.Text;
using Aspose.Cells;
using Aspose.Cells.Rendering;
```
تتيح لك هذه الحزم العمل مع ملفات Excel وتحويلها إلى ملفات PDF مع الإشارات المرجعية.
لنبدأ بشرح عملية إنشاء إشارات مرجعية في ملفات PDF. سنشرح كل جزء خطوة بخطوة.
## الخطوة 1: تحديد مسارات الدليل الخاص بك
لتنظيم الكود الخاص بك، دعنا نحدد مكان وجود ملفاتنا.
```csharp
string sourceDir = "Your Document Directory"; // على سبيل المثال، @"C:\Documents\"
string outputDir = "Your Document Directory"; // على سبيل المثال، @"C:\Documents\Output\"
```
يستبدل `Your Document Directory` مع المسارات الفعلية حيث يتم تخزين ملف Excel الخاص بك والمكان الذي تريد حفظ ملف PDF الناتج فيه.
## الخطوة 2: تحميل مصنف Excel
بعد ذلك، نحتاج إلى تحميل مصنف Excel الذي تريد التعامل معه.
```csharp
Workbook wb = new Workbook(sourceDir + "sampleCreatePdfBookmarkEntryForChartSheet.xlsx");
```
هنا نقوم بإنشاء مثيل لـ `Workbook` الصف، تحميل ملف Excel النموذجي. تأكد من أن اسم الملف يطابق ملفك الفعلي.
## الخطوة 3: الوصول إلى أوراق العمل
بمجرد تحميل المصنف، يمكنك الوصول إلى أوراق العمل الخاصة به. 
```csharp
Worksheet sheet1 = wb.Worksheets[0];
Worksheet sheet2 = wb.Worksheets[1];
Worksheet sheet3 = wb.Worksheets[2];
Worksheet sheet4 = wb.Worksheets[3];
```
يشير الكود إلى أوراق العمل الأربع في المصنف. تأكد من أن ملف Excel يحتوي على أربع أوراق عمل على الأقل.
## الخطوة 4: إنشاء إدخالات إشارة مرجعية لملف PDF
هنا يأتي السحر! سننشئ إدخالات إشارات مرجعية لكل ورقة.
```csharp
PdfBookmarkEntry ent1 = new PdfBookmarkEntry {
    Destination = sheet1.Cells["A1"],
    Text = "Bookmark-I"
};
PdfBookmarkEntry ent2 = new PdfBookmarkEntry {
    Destination = sheet2.Cells["A1"],
    Text = "Bookmark-II-Chart1"
};
PdfBookmarkEntry ent3 = new PdfBookmarkEntry {
    Destination = sheet3.Cells["A1"],
    Text = "Bookmark-III"
};
PdfBookmarkEntry ent4 = new PdfBookmarkEntry {
    Destination = sheet4.Cells["A1"],
    Text = "Bookmark-IV-Chart2"
};
```
كل `PdfBookmarkEntry` يحتوي الكائن على خلية وجهة وعلامة نصية. سيؤدي هذا الإعداد إلى إنشاء إشارات مرجعية في ملف PDF تتوافق مع المناطق في جداول بيانات Excel.
## الخطوة 5: ترتيب إدخالات الإشارة المرجعية
لإنشاء هيكل هرمي للإشارات المرجعية، نحتاج إلى تنظيمها.
```csharp
ArrayList lst = new ArrayList();
ent1.SubEntry = lst;
lst.Add(ent2);
lst.Add(ent3);
lst.Add(ent4);
```
يضيف هذا الكود الإشارات المرجعية الثانية والثالثة والرابعة كإدخالات فرعية تحت الإشارة المرجعية الأولى. الآن، عند النقر على "إشارة مرجعية-I" في ملف PDF، سينقلك إلى الإشارات المرجعية الأخرى.
## الخطوة 6: إنشاء خيارات حفظ PDF باستخدام إدخالات الإشارة المرجعية
الآن، دعونا نجهز خيارات حفظ ملف PDF باستخدام إشاراتنا المرجعية.
```csharp
PdfSaveOptions opts = new PdfSaveOptions();
opts.Bookmark = ent1;
```
ال `PdfSaveOptions` يتيح لنا التكوين تضمين الإشارات المرجعية عند حفظ ملف PDF.
## الخطوة 7: حفظ ملف PDF الناتج
وأخيرًا، حان الوقت لحفظ عملك!
```csharp
wb.Save(outputDir + "outputCreatePdfBookmarkEntryForChartSheet.pdf", opts);
```
يحفظ هذا الأمر المصنف في ملف PDF في مسار الإخراج المحدد، مع إشاراتك المرجعية الرائعة.
## الخطوة 8: تأكيد التنفيذ
وأخيرًا، دعنا نطبع رسالة نجاح لتأكيد أن كل شيء سار بسلاسة.
```csharp
Console.WriteLine("CreatePdfBookmarkEntryForChartSheet executed successfully.");
```
## خاتمة 
إنشاء إشارات مرجعية لملفات PDF لجداول البيانات باستخدام Aspose.Cells لـ .NET عملية سهلة تُحسّن من سهولة استخدام مستندات Excel. ببضعة أسطر فقط من التعليمات البرمجية، يمكنك التنقل بسهولة عبر ملف PDF، مما يوفر وقتًا ثمينًا ويُحسّن سير عملك.
سواءً كنت تُنشئ تقارير أو تُحافظ على مجموعات بيانات مُعقدة، تُسهّل هذه الإشارات المرجعية الوصول إلى المعلومات بشكل كبير. لذا، هيا، تحكّم في مستنداتك وأثريها بهذه الميزة الرائعة!
## الأسئلة الشائعة
### ما هو Aspose.Cells؟
Aspose.Cells عبارة عن مكتبة .NET قوية مصممة للتعامل مع عمليات معالجة ملفات Excel، بما في ذلك القراءة والكتابة وتحويل جداول البيانات.
### هل يمكنني إنشاء إشارات مرجعية لخلايا محددة فقط؟
نعم، يمكنك تعيين وجهة الإشارات المرجعية لتكون أي خلية في ورقة العمل الخاصة بك.
### هل أحتاج إلى ترخيص لاستخدام Aspose.Cells؟
على الرغم من أن Aspose.Cells يقدم نسخة تجريبية مجانية، إلا أنه يلزم الحصول على ترخيص مدفوع للحصول على الوظائف الكاملة للاستخدام الإنتاجي.
### هل يمكنني إنشاء إشارات مرجعية لأكثر من أربع أوراق؟
بالتأكيد! يمكنك إنشاء إشارات مرجعية لأي عدد تريده من الأوراق باتباع بنية مشابهة في الكود.
### أين يمكنني العثور على مزيد من المساعدة؟
يمكنك التحقق من [منتدى دعم مجتمع Aspose](https://forum.aspose.com/c/cells/9) لأي مشاكل أو استفسارات.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}