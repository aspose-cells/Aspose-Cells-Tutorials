---
"description": "تعرّف على كيفية إعداد رؤوس وتذييلات صفحات Excel بسهولة باستخدام Aspose.Cells لـ .NET من خلال دليلنا المفصل. مثالي للمستندات الاحترافية."
"linktitle": "تعيين رؤوس وتذييلات Excel"
"second_title": "مرجع واجهة برمجة التطبيقات Aspose.Cells لـ .NET"
"title": "تعيين رؤوس وتذييلات Excel"
"url": "/ar/net/excel-page-setup/set-excel-headers-and-footers/"
"weight": 100
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# تعيين رؤوس وتذييلات Excel

## مقدمة

عندما يتعلق الأمر بإدارة مستندات جداول البيانات، تلعب الرؤوس والتذييلات دورًا حاسمًا في توفير السياق. تخيل أنك تفتح ملف Excel، وترى في الأعلى اسم ورقة العمل والتاريخ، وربما حتى اسم الملف. يُضفي هذا على مستندك لمسة احترافية ويساعد على إيصال التفاصيل المهمة بسرعة. إذا كنت ترغب في تحسين احترافية جداول بيانات Excel باستخدام Aspose.Cells لـ .NET، فأنت في المكان المناسب! في هذا الدليل، سنشرح لك خطوات إعداد الرؤوس والتذييلات في جداول بيانات Excel بسهولة. 

## المتطلبات الأساسية

قبل أن نتعمق في التفاصيل، لنتأكد من توفر كل ما تحتاجه للبدء. أولًا، ستحتاج إلى:

1. Visual Studio: تأكد من تثبيت Visual Studio على جهازك. هنا ستكتب وتنفذ شيفرة C#.
2. مكتبة Aspose.Cells لـ .NET: يجب أن تكون لديك مكتبة Aspose.Cells. إذا لم تكن لديك بالفعل، يمكنك تنزيلها من [هنا](https://releases.aspose.com/cells/net/).
3. الفهم الأساسي لـ C#: إن الإلمام ببرمجة C# أمر بالغ الأهمية، حيث ستكون جميع عينات التعليمات البرمجية بهذه اللغة.
4. إعداد المشروع: قم بإنشاء مشروع C# جديد في Visual Studio حيث سننفذ منطق الرأس/التذييل الخاص بـ Excel.

بمجرد التأكد من أن لديك المتطلبات الأساسية المذكورة أعلاه، فقد حان الوقت للبدء في العمل!

## استيراد الحزم

للبدء في العمل مع Aspose.Cells، تحتاج إلى استيراد المساحات الأسماء المناسبة في الكود C# الخاص بك.

### افتح مشروع C# الخاص بك

افتح مشروعك في Visual Studio حيث ترغب في تطبيق إعدادات الرأس والتذييل. تأكد من أن لديك بنية واضحة تستوعب الكود الخاص بك.

### إضافة مرجع إلى Aspose.Cells

بعد إنشاء مشروعك أو فتحه، ستحتاج إلى إضافة مرجع إلى مكتبة Aspose.Cells. انقر بزر الماوس الأيمن على مشروعك في مستكشف الحلول، ثم اختر "إدارة حزم NuGet"، وابحث عن "Aspose.Cells". ثبّته في مشروعك.

### استيراد مساحة الاسم

في أعلى ملف C# الخاص بك، أضف السطر التالي لاستيراد مساحة اسم Aspose.Cells:

```csharp
using System.IO;
using Aspose.Cells;
using System;
```

من خلال استيراد مساحة الأسماء هذه، يمكنك استخدام الوظائف التي توفرها مكتبة Aspose.Cells دون أي عوائق.

رائع! الآن، بعد إعداد بيئتك واستيراد حزمك، لنبدأ بشرح عملية إعداد الرؤوس والتذييلات في Excel خطوة بخطوة.

## الخطوة 1: تهيئة المصنف

أولاً، نحتاج إلى إنشاء كائن Workbook، والذي يمثل ملف Excel الخاص بنا في الذاكرة.

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
Workbook excel = new Workbook();
```

الشرح: هنا، استبدل `YOUR DOCUMENT DIRECTORY` مع المسار الفعلي الذي تريد حفظ ملف Excel فيه. `Workbook` يعد الكائن نقطة الدخول الرئيسية لإنشاء ملفات Excel ومعالجتها.

## الخطوة 2: الحصول على مرجع PageSetup

بعد ذلك، نحتاج إلى الوصول إلى `PageSetup` خاصية ورقة العمل التي نريد تعيين الرؤوس والتذييلات فيها.

```csharp
PageSetup pageSetup = excel.Worksheets[0].PageSetup;
```

التوضيح: نقوم بالوصول إلى ورقة العمل الأولى (الفهرس) `0`) من كتاب العمل الخاص بنا. `PageSetup` توفر الفئة خصائص وطرقًا لتخصيص مظهر الصفحة عند الطباعة، بما في ذلك الرؤوس والتذييلات.

## الخطوة 3: تعيين الرأس

الآن، لنبدأ بإعداد الرأس. سنبدأ بالقسم الأيسر:

```csharp
pageSetup.SetHeader(0, "&A");
```

الشرح: `SetHeader` تسمح لنا الطريقة بتحديد محتوى الرأس. هنا، `&A` يشير إلى اسم ورقة العمل، والتي ستظهر على الجانب الأيسر من الرأس.

## الخطوة 4: تخصيص الرأس المركزي

بعد ذلك، سنقوم بتخصيص الرأس المركزي لعرض التاريخ والوقت الحاليين بخط محدد.

```csharp
pageSetup.SetHeader(1, "&\"Times New Roman,Bold\"&D-&T");
```

الشرح: `&D` و `&T` سيتم استبدال الرموز تلقائيًا بالتاريخ والوقت الحاليين، على التوالي. كما نحدد أن يكون خط هذا العنوان "Times New Roman" وغامقًا.

## الخطوة 5: تعيين الرأس الأيمن

لنبدأ الآن بتعيين القسم الأيمن من الرأس لإظهار اسم الملف.

```csharp
pageSetup.SetHeader(2, "&\"Times New Roman,Bold\"&12&F");
```

التوضيح: هنا، `&F` سيتم استبداله باسم الملف. نستخدم نفس الخط المستخدم في العنوان الرئيسي للحفاظ على تناسق المظهر.

## الخطوة 6: تكوين التذييل

بعد أن أصبحت رؤوس الصفحات أنيقة، لننتقل إلى التذييلات. سنبدأ بالتذييل الأيسر:

```csharp
pageSetup.SetFooter(0, "Hello World! &\"Courier New\"&14 123");
```

توضيح: نقوم بإدراج رسالة مخصصة في التذييل الأيسر، "مرحباً بالعالم!" مع النص `123` بنمط خط مختلف—Courier New.

## الخطوة 7: تكوين تذييل المركز

بعد ذلك، قمنا بتعيين تذييل المركز لعرض رقم الصفحة الحالية:

```csharp
pageSetup.SetFooter(1, "&P");
```

الشرح: `&P` يقوم الكود تلقائيًا بإدراج رقم الصفحة في منتصف التذييل - وهي طريقة مفيدة لتتبع الصفحات.

## الخطوة 8: تكوين التذييل الأيمن

لإكمال إعدادات التذييل، دعنا نضبط التذييل الأيمن لإظهار العدد الإجمالي للصفحات في المستند.

```csharp
pageSetup.SetFooter(2, "&N");
```

التوضيح: هنا، `&N` سيتم استبداله بإجمالي عدد الصفحات. يُضفي ذلك لمسة احترافية، خاصةً للمستندات الطويلة.

## الخطوة 9: حفظ المصنف

الآن وبعد إعداد كل شيء، كل ما عليك فعله هو حفظ المصنف لرؤية ثمار عملك.

```csharp
excel.Save(dataDir + "SetHeadersAndFooters_out.xls");
```

شرح: استبدال `"SetHeadersAndFooters_out.xls"` بالاسم الذي تريده. احفظ مصنفك، وانتهى الأمر!

## خاتمة

وهذا كل ما في الأمر! إعداد الرؤوس والتذييلات في Excel باستخدام Aspose.Cells لـ .NET سهل للغاية باتباع هذه الخطوات. لن تُحسّن مظهر مستندك فحسب، بل ستُحسّن أيضًا وظائفه من خلال توفير سياق مهم. سواء كنت تُعدّ تقارير، أو تُشارك قوالب، أو تُنظّم بياناتك فحسب، تُضيف الرؤوس والتذييلات لمسة احترافية لا تُضاهى. جرّبها الآن واكتشف سهولة إدارة مستندات Excel باستخدام هذه المكتبة الفعّالة!

## الأسئلة الشائعة

### ما هو Aspose.Cells؟
Aspose.Cells هي مكتبة .NET تستخدم لإنشاء ملفات Excel ومعالجتها وعرضها برمجيًا.

### هل يمكنني تجربة Aspose.Cells مجانًا؟
نعم! يمكنك تنزيل نسخة تجريبية مجانية من [هنا](https://releases.aspose.com/).

### هل Aspose.Cells متوافق مع تنسيقات Excel القديمة؟
بالتأكيد! يدعم Aspose.Cells تنسيقات ملفات Excel القديمة والجديدة.

### أين يمكنني العثور على مزيد من الوثائق؟
يمكنك التحقق من الوثائق التفصيلية على [توثيق Aspose.Cells](https://reference.aspose.com/cells/net/).

### كيف أحصل على الدعم لـ Aspose.Cells؟
للحصول على الدعم، قم بزيارة [منتدى دعم Aspose](https://forum.aspose.com/c/cells/9).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}