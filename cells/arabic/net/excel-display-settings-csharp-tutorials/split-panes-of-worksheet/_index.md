---
"description": "تعرّف على كيفية تقسيم أجزاء ورقة العمل في Aspose.Cells لـ .NET من خلال دليلنا المفصل. حسّن تصفح ملفات Excel مع هذا البرنامج التعليمي السهل."
"linktitle": "تقسيم أجزاء ورقة العمل"
"second_title": "مرجع واجهة برمجة التطبيقات Aspose.Cells لـ .NET"
"title": "تقسيم أجزاء ورقة العمل"
"url": "/ar/net/excel-display-settings-csharp-tutorials/split-panes-of-worksheet/"
"weight": 130
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# تقسيم أجزاء ورقة العمل

## مقدمة

هل أنت مستعد لتقسيم أجزاء ورقة عمل Excel باستخدام Aspose.Cells لـ .NET؟ تخيل هذا: لديك ورقة عمل Excel ضخمة، وقد سئمت من التمرير المتكرر إلى العناوين فقط لتذكر العمود الذي تعمل عليه. استخدم "تقسيم الأجزاء". تتيح لك هذه الميزة المفيدة تجميد جزء من ورقة العمل، مما يُسهّل التنقل فيها بشكل كبير. سواء كنت تعمل على بيانات مالية، أو إدارة مخزون، أو مجموعات بيانات ضخمة، فإن تقسيم الأجزاء يُحسّن إنتاجيتك بشكل كبير. 

## المتطلبات الأساسية

قبل أن نبدأ بتقسيم الأجزاء كما لو كنا نستخدم معالج جداول البيانات، لنبدأ بإعدادها بشكل صحيح. إليك ما ستحتاجه:

- Aspose.Cells لـ .NET: تأكد من تنزيله وتثبيته. إذا لم تقم بذلك بعد، فاحصل عليه. [هنا](https://releases.aspose.com/cells/net/).
- .NET Framework: يفترض هذا الدليل أنك تعمل في بيئة .NET.
- مصنف Excel: سنستخدم ملف Excel نموذجيًا لإظهار كيفية عمل هذه الميزة.
- ترخيص مؤقت أو كامل: يتطلب Aspose.Cells ترخيصًا. إذا كنت تجربه للتو، فاحصل عليه. [رخصة مؤقتة مجانية](https://purchase.aspose.com/temporary-license/) لتجنب قيود التقييم.

## استيراد الحزم

قبل التعمق في البرمجة، لنبدأ باستيراد مساحات الأسماء اللازمة. لا يمكنك فعل أي شيء في Aspose.Cells دون تضمينها.

```csharp
using System.IO;
using Aspose.Cells;
```

الآن بعد أن قمنا بتغطية الأساسيات، دعنا ننتقل إلى الجزء المثير - تقسيم الألواح!

## الخطوة 1: إنشاء مصنف

الخطوة الأولى في هذه العملية هي إنشاء `Workbook` كائن، يُمثل ملف Excel الذي تريد تعديله. في هذه الحالة، سنحمّل ملفًا من مجلد. هذه هي لوحتك، ورقة Excel التي ستُجري عليها تعديلاتك السحرية.

قبل أن نتمكن من تقسيم الألواح، نحتاج إلى كتاب عمل! هذه الخطوة أساسية كفتح كتاب قبل البدء بقراءته.

```csharp
// المسار إلى دليل المستندات
string dataDir = "YOUR DOCUMENT DIRECTORY";

// إنشاء مصنف جديد وفتح ملف قالب
Workbook book = new Workbook(dataDir + "Book1.xls");
```

في الكود أعلاه، استبدل `"YOUR DOCUMENT DIRECTORY"` مع المسار الفعلي الذي يوجد به ملف Excel الخاص بك. `Workbook` يقوم class بتحميل ملف Excel إلى الذاكرة.

## الخطوة 2: تعيين الخلية النشطة

بعد تحميل المصنف، حان وقت تحديد الخلية النشطة. في إكسل، الخلية النشطة هي الخلية المحددة حاليًا أو التي يتم التركيز عليها. في هذا البرنامج التعليمي، سنحدد الخلية `A20` في ورقة العمل الأولى.

يُعدّ ضبط الخلية النشطة أمرًا بالغ الأهمية، لأن تقسيم اللوحة يبدأ منها. الأمر أشبه باختيار مكان القطع الأول في البيتزا - اختر شريحتك!

```csharp
// تعيين الخلية النشطة
book.Worksheets[0].ActiveCell = "A20";
```

هذه القطعة من الكود تجعل `A20` الخلية النشطة. هذا مهم لأن التقسيم يحدث حول هذه النقطة، تمامًا كما يتركز التنقل في Excel غالبًا حول خلية محددة.

## الخطوة 3: تقسيم ورقة العمل

بعد تحديد الخلية النشطة، لننتقل إلى الجزء الممتع: تقسيم ورقة العمل! في هذه الخطوة، ستُحدث المفاجأة. ستتمكن من تقسيم ورقة العمل إلى عدة أجزاء لتسهيل العرض والتنقل.

هذا هو جوهر البرنامج التعليمي بأكمله. بتقسيم ورقة العمل، تُنشئ أجزاءً منفصلة تُتيح لك التمرير عبر أقسام مختلفة من ورقة Excel دون إغفال العناوين أو المناطق المهمة الأخرى.

```csharp
// تقسيم نافذة ورقة العمل
book.Worksheets[0].Split();
```

مع `Split()` الطريقة هي أنك تطلب من Aspose.Cells تقسيم ورقة العمل عند الخلية النشطة (`A20` من هذه النقطة، يقوم Excel بإنشاء قسم في الورقة يفصل الأجزاء حتى تتمكن من التنقل بينها بشكل مستقل.

## الخطوة 4: حفظ المصنف

بعد تقسيم الأجزاء، كل ما تبقى هو حفظ عملك. ستضمن هذه الخطوة الأخيرة حفظ تغييراتك في ملف الإخراج المحدد.

ما فائدة كل هذا الجهد إن لم تحفظه؟ الحفظ يضمن لك الحفاظ على لوحاتك المقسّمة بشكل جميل سليمة للاستخدام المستقبلي.

```csharp
// حفظ ملف Excel
book.Save(dataDir + "output.xls");
```

هنا، `Save()` تحفظ هذه الطريقة المصنف مع الأجزاء المقسمة حديثًا في ملف Excel. التغييرات التي أجريتها جاهزة الآن للاستخدام من قِبلك أو من قِبل أي شخص آخر.

## خاتمة

ها قد انتهيت! لقد تعلمت للتو كيفية تقسيم أجزاء ورقة عمل Excel باستخدام Aspose.Cells لـ .NET. لا مزيد من التمرير المتواصل أو فقدان بياناتك. هذه الطريقة تجعل التعامل مع ملفات Excel الكبيرة أسهل بكثير وأكثر كفاءة. بفضل إمكانية تقسيم الأجزاء، يمكنك الآن تتبع نقاط البيانات المهمة أثناء العمل على جداول بيانات معقدة.

## الأسئلة الشائعة

### هل يمكنني تقسيم أكثر من جزءين؟  
نعم، يمكنك تقسيم ورقة العمل إلى أجزاء متعددة عن طريق تحديد خلايا نشطة مختلفة واستدعاء `Split()` طريقة.

### ما الفرق بين تقسيم الألواح وتجميد الألواح؟  
يتيح لك تقسيم الأجزاء التمرير في كلا الجزئين بشكل مستقل. يؤدي تجميد الأجزاء إلى قفل العناوين أو الصفوف/الأعمدة المحددة بحيث تبقى مرئية عند التمرير.

### هل يمكنني إزالة التقسيم بعد تطبيقه؟  
نعم، يمكنك إزالة الانقسام إما عن طريق إغلاق المصنف ثم إعادة فتحه أو إعادة تعيينه برمجيًا.

### هل تعمل أجزاء التقسيم بنفس الطريقة بالنسبة لتنسيقات ملفات Excel المختلفة (XLS، XLSX)؟  
نعم، `Split()` تعمل الطريقة مع تنسيقات XLS وXLSX.

### هل يمكنني استخدام Aspose.Cells بدون ترخيص؟  
نعم، ولكن له حدود. للحصول على تجربة كاملة، يُفضل استخدام [مؤقت](https://purchase.aspose.com/tempأوary-license/) or [رخصة مدفوعة](https://purchase.aspose.com/buy).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}