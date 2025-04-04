---
title: إنشاء المجاميع الفرعية في Excel
linktitle: إنشاء المجاميع الفرعية في Excel
second_title: واجهة برمجة تطبيقات معالجة Excel الخاصة بـ Aspose.Cells .NET
description: تعرف على كيفية إنشاء إجماليات فرعية في Excel باستخدام Aspose.Cells لـ .NET من خلال هذا البرنامج التعليمي السهل خطوة بخطوة.
weight: 10
url: /ar/net/excel-subtotal-calculation/create-subtotals-in-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء المجاميع الفرعية في Excel

## مقدمة
هل أنت مستعد لرفع مستوى مهاراتك في Excel وجعل جداول البيانات الخاصة بك أكثر ديناميكية؟ يمكن أن يساعدك إنشاء مجاميع فرعية في Excel في تصنيف البيانات وتلخيصها بشكل فعال، مما يسمح بتفسير البيانات وإعداد التقارير بشكل أفضل. إذا كنت من الأشخاص الذين يجدون أنفسهم غالبًا في صراع مع أكوام من الأرقام، فإن إنشاء ملخصات منظمة أمر ضروري. اليوم، سنتعمق في كيفية إنشاء مجاميع فرعية بسهولة باستخدام Aspose.Cells for .NET، وهي مكتبة قوية مصممة للتعامل مع جميع معالجات ملفات Excel الخاصة بك.
## المتطلبات الأساسية
قبل أن نتعمق في التفاصيل الدقيقة لإنشاء الإجماليات الفرعية في Excel، هناك بعض المتطلبات الأساسية التي يجب أن تكون موجودة لديك:
1.  تم تثبيت Aspose.Cells لـ .NET: تأكد من إعداد مكتبة Aspose.Cells في بيئة التطوير الخاصة بك. إذا لم تقم بذلك بعد، فيمكنك بسهولة[تحميله هنا](https://releases.aspose.com/cells/net/).
2. بيئة .NET: يجب أن يكون لديك بيئة .NET صالحة للعمل حيث يمكننا العمل مع المكتبة. سواء كان ذلك باستخدام Visual Studio أو أي بيئة تطوير متكاملة أخرى، تأكد من أنك مرتاح في كتابة التعليمات البرمجية بلغة C#.
3. المعرفة الأساسية بلغة C#: ستكون المعرفة بلغة C# مفيدة. الأمثلة التي سنقدمها مكتوبة بلغة C#، لذا فإن الشعور بالراحة في التعامل معها سيساعدك على فهم العملية.
4.  ورقة عمل Excel: ملف Excel نموذجي للتدرب عليه. سنستخدم ملفًا يسمى`book1.xls` في برنامجنا التعليمي.
5.  الوصول إلى الوثائق والدعم عبر الإنترنت: التعرف على[توثيق Aspose.Cells](https://reference.aspose.com/cells/net/) يمكن أن يكون مفيدًا بشكل لا يصدق مع تقدمك في استخدام المكتبة.
الآن بعد أن وضعنا الأساس، دعونا ننتقل إلى الجزء الفني!
## استيراد الحزم
قبل البدء بالكود الفعلي، نحتاج إلى التأكد من أن لدينا جميع الحزم المطلوبة. فيما يلي كيفية استيراد المساحة المطلوبة في مشروعك:
```csharp
using System.IO;
using Aspose.Cells;
```
يستورد هذا كل ما نحتاجه من مكتبة Aspose للتعامل مع ملفات Excel. الآن، دعنا نحلل التعليمات البرمجية خطوة بخطوة لإنشاء إجماليات فرعية في ورقة عمل Excel.
## الخطوة 1: إعداد مسار الملف
للبدء، نحتاج إلى تحديد مكان وجود ملف Excel الخاص بنا. هنا نخبر البرنامج عن دليل المستندات الخاص بنا.
```csharp
string dataDir = "Your Document Directory";
```
 يستبدل`"Your Document Directory"` مع المسار الفعلي الذي تريده`book1.xls` يتم تخزينه. هذا يخبر البرنامج بمكان العثور على ملف Excel الذي سنقوم بمعالجته.
## الخطوة 2: إنشاء مصنف جديد
بعد ذلك، سنقوم بإنشاء مثيل جديد لكائن المصنف. سيسمح لنا هذا بفتح ملف Excel وتحريره.
```csharp
Workbook workbook = new Workbook(dataDir + "book1.xls");
```
 هنا، نقوم بإنشاء كائن`Workbook` وتحميله بالملفات المحددة لدينا`book1.xls` يحتوي كائن المصنف هذا الآن على كافة المعلومات من ملف Excel ويسمح لنا بتعديله.
## الخطوة 3: الوصول إلى مجموعة الخلايا
للعمل على محتويات ورقة عمل Excel، نحتاج إلى الوصول إلى مجموعة "الخلايا".
```csharp
Cells cells = workbook.Worksheets[0].Cells;
```
 يؤدي هذا إلى استرداد الخلايا من ورقة العمل الأولى (الفهرس 0) في مصنفنا.`cells` سوف يسمح لنا الكائن بالتفاعل مع الخلايا الفردية في جدول البيانات.
## الخطوة 4: تحديد مساحة الخلية للمجموعات الفرعية
الآن حان الوقت لتحديد نطاق الخلايا التي نريد تطبيق المجموع الفرعي عليها. 
```csharp
CellArea ca = new CellArea();
ca.StartRow = 2; // ب3
ca.StartColumn = 1; 
ca.EndRow = 18; // القرن التاسع عشر
ca.EndColumn = 2;
```
 هنا، نقوم بتعريف`CellArea` الذي يحدد النطاق الذي نهتم به. في هذه الحالة، اخترنا المنطقة من B3 (الصف 2، العمود 1) إلى C19 (الصف 18، العمود 2). هذا هو المكان الذي سنحسب فيه الإجماليات الفرعية.
## الخطوة 5: تطبيق المجاميع الفرعية
هذا هو جوهر عملنا - تطبيق المجموع الفرعي على مساحة الخلية المحددة.
```csharp
cells.Subtotal(ca, 0, ConsolidationFunction.Sum, new int[] { 1 });
```
 في هذا الخط، نسميه`Subtotal` الطريقة. المعلمات المحددة هي:
- `ca`:نطاق الخلايا الذي حددناه سابقًا.
- `0`:يشير هذا الفهرس إلى العمود الذي يحتوي على القيم التي سيتم جمعها جزئيًا. 
- `ConsolidationFunction.Sum`:يشير هذا إلى أننا نريد جمع القيم.
- `new int[] { 1 }`:يشير هذا إلى أننا نقوم بجمع القيم من العمود الثاني (العمود C).
## الخطوة 6: حفظ ملف Excel المعدّل
وأخيرًا، نحتاج إلى حفظ التغييرات في ملف Excel جديد. 
```csharp
workbook.Save(dataDir + "output.out.xls");
```
 ال`Save` تكتب الطريقة التغييرات في ملف جديد يسمى`output.out.xls`يمكنك تحديد أي اسم لملف الإخراج وفقًا لمتطلباتك.
## خاتمة
باستخدام هذه الخطوات البسيطة، تكون قد نجحت في إنشاء مجاميع فرعية في ورقة عمل Excel باستخدام Aspose.Cells for .NET! بدءًا من إنشاء مصنف إلى تطبيق المجاميع الفرعية وحفظ النتائج، قمنا بتغطية جميع الأساسيات. لا تعمل هذه المكتبة على تبسيط عمليات معالجة Excel فحسب، بل تمكنك أيضًا من التعامل مع البيانات بشكل أكثر فعالية.
الآن، انطلق وجرِّب الأمر! ستندهش من مدى سهولة إدارة البيانات في جداول البيانات عندما تعرف كيفية استخدام الأدوات المناسبة. 
## الأسئلة الشائعة
### ما هو Aspose.Cells لـ .NET؟
Aspose.Cells for .NET عبارة عن مكتبة قوية تتيح للمطورين التعامل مع ملفات Excel في تطبيقات .NET بشكل برمجي.
### هل أحتاج إلى تثبيت أي شيء خاص لاستخدام Aspose.Cells؟
 نعم، تحتاج إلى تنزيل مكتبة Aspose.Cells وإضافتها إلى مشروع .NET الخاص بك.[تحميل هنا](https://releases.aspose.com/cells/net/).
### هل من الممكن إنشاء أنواع أخرى من ميزات Excel باستخدام Aspose.Cells؟
بالتأكيد! يتيح لك Aspose.Cells تنفيذ عمليات مختلفة في Excel مثل إنشاء المخططات وإدارة أوراق العمل وتعديل تنسيقات الخلايا وغيرها الكثير.
### هل يمكنني استخدام Aspose.Cells مجانًا؟
 أنت تستطيع[جرب نسخة تجريبية مجانية](https://releases.aspose.com/) قم بزيارة Aspose.Cells لاستكشاف ميزاته قبل اتخاذ قرار الشراء.
### ما هي خيارات الدعم المتاحة؟
 لأي مشكلة، يمكنك زيارة[منتدى دعم Aspose](https://forum.aspose.com/c/cells/9) للحصول على المساعدة ومشاركة الأفكار مع مجتمع المستخدمين والمطورين.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
