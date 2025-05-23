---
"description": "تعلّم كيفية الإشارة إلى خلية صورة في Excel باستخدام Aspose.Cells لـ .NET من خلال هذا البرنامج التعليمي خطوة بخطوة. حسّن جداول بياناتك."
"linktitle": "خلية الصورة المرجعية في Excel"
"second_title": "واجهة برمجة تطبيقات معالجة Excel Aspose.Cells .NET"
"title": "خلية الصورة المرجعية في Excel"
"url": "/ar/net/excel-ole-picture-objects/reference-picture-cell-excel/"
"weight": 15
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# خلية الصورة المرجعية في Excel

## مقدمة
إذا كنت تعمل على جداول بيانات Excel، فمن المرجح أنك واجهت مواقف تُحسّن فيها العناصر المرئية عرض بياناتك بشكل ملحوظ. تخيل أنك تريد ربط صورة بخلايا محددة لتمثيل البيانات بصريًا. حسنًا، استعد، لأننا اليوم سنتعمق في استخدام Aspose.Cells لـ .NET للإشارة إلى خلية صورة في Excel. بنهاية هذا الدليل، ستصبح محترفًا في دمج الصور في جداول بياناتك بسلاسة. لنبدأ الآن!
## المتطلبات الأساسية
قبل أن نبدأ، دعونا نتأكد من أن لديك كل ما تحتاجه:
- Visual Studio: تأكد من تثبيت إصدار متوافق من Visual Studio على جهازك للتعامل مع مشروع .NET.
- Aspose.Cells لـ .NET: ستحتاج إلى مكتبة Aspose.Cells. إذا لم تقم بتنزيلها بعد، فتفضل بزيارة [صفحة تنزيلات Aspose](https://releases.aspose.com/cells/net/) و احصل على الإصدار الأحدث.
- المعرفة الأساسية بلغة C#: يفترض هذا الدليل أنك مُلِمٌّ بمفاهيم برمجة C# و.NET. إذا كنتَ جديدًا، فلا تقلق؛ سأشرح كل خطوة بالتفصيل.
الآن بعد أن أصبح كل شيء جاهزًا، فلنبدأ في استيراد الحزم الضرورية!
## استيراد الحزم
للاستفادة من قوة Aspose.Cells، عليك استيراد مساحات الأسماء ذات الصلة إلى مشروعك. إليك كيفية القيام بذلك:
1. إنشاء مشروع جديد: افتح Visual Studio وقم بإنشاء تطبيق وحدة تحكم C# جديد.
2. إضافة مراجع: تأكد من إضافة مرجع إلى مكتبة Aspose.Cells. يمكنك القيام بذلك بالنقر بزر الماوس الأيمن على مشروعك، ثم اختيار "إضافة"، ثم "مرجع"، ثم الانتقال إلى المكان الذي نزّلت منه ملف Aspose.Cells DLL.
```csharp
using System.IO;
using System;
using Aspose.Cells;
using Aspose.Cells.Drawing;
```
الآن، دعنا نكتب بعض التعليمات البرمجية لتحقيق هدفنا المتمثل في الإشارة إلى صورة في Excel.
## الخطوة 1: إعداد البيئة الخاصة بك
أولاً، علينا إنشاء مصنف جديد وإعداد الخلايا اللازمة. إليك الطريقة:
```csharp
// المسار إلى دليل المستندات.
string dataDir = "Your Document Directory";
// إنشاء مصنف جديد
Workbook workbook = new Workbook();
// احصل على مجموعة خلايا ورقة العمل الأولى
Cells cells = workbook.Worksheets[0].Cells;
```
 
- قم بتحديد المسار الذي تريد حفظ ملف Excel فيه.
- إنشاء جديد `Workbook` المثال الذي يمثل ملف Excel الخاص بك.
- قم بالوصول إلى الخلايا الموجودة في ورقة العمل الأولى حيث سنقوم بإدخال بياناتنا وصورتنا.
## الخطوة 2: إضافة قيم السلسلة إلى الخلايا
الآن، دعونا نضيف بعض قيم السلسلة إلى الخلايا. 
```csharp
// إضافة قيم السلسلة إلى الخلايا
cells["A1"].PutValue("A1");
cells["C10"].PutValue("C10");
```
 
- باستخدام `PutValue` في هذه الطريقة، نملأ الخلية A1 بالسلسلة "A1" والخلية C10 بالسلسلة "C10". هذا مجرد مثال بسيط، ولكنه سيساعدنا على توضيح كيفية ارتباط صورتنا بهذه المناطق.
## الخطوة 3: إضافة صورة فارغة
بعد ذلك، سنضيف شكل الصورة إلى ورقة العمل الخاصة بنا:
```csharp
// إضافة صورة فارغة إلى الخلية D1
Picture pic = workbook.Worksheets[0].Shapes.AddPicture(0, 3, 10, 6, null);
```
 
- في هذا السطر، نضيف صورة فارغة عند الإحداثيات (0، 3) المقابلة للصف 1، العمود 4 (D1). تُحدد الأبعاد (10، 6) عرض الصورة وارتفاعها بالبكسل.
## الخطوة 4: تحديد صيغة مرجع الصورة
دعونا نربط صورتنا بالخلايا التي ملأناها مسبقًا.
```csharp
// حدد الصيغة التي تشير إلى نطاق المصدر للخلايا
pic.Formula = "A1:C10";
```

- هنا، نُعِدّ صيغةً للصورة تُشير إلى النطاق من A1 إلى C10. سيُتيح هذا للصورة تمثيل البيانات في هذا النطاق بصريًا. تخيّل أن خلاياك هي لوحة الرسم، وستُصبح الصورة نقطةً محوريةً مذهلة!
## الخطوة 5: تحديث القيمة المحددة للأشكال
لضمان انعكاس تغييراتنا في ورقة العمل، نحتاج إلى تحديث الأشكال:
```csharp
// تحديث قيمة الأشكال المحددة في ورقة العمل
workbook.Worksheets[0].Shapes.UpdateSelectedValue();
```

- تضمن هذه الخطوة أن يتعرف Excel على تحديثاتنا لشكل الصورة وأي مراجع للخلايا.
## الخطوة 6: حفظ ملف Excel
وأخيرًا، دعنا نحفظ مصنفنا في الدليل المخصص:
```csharp
// احفظ ملف Excel.
workbook.Save(dataDir + "output.out.xls");
```

- ال `Save` تحدد هذه الطريقة مسار حفظ ملف Excel، بالإضافة إلى اسمه. بعد تنفيذ هذه الطريقة، ستجد ملف Excel الذي أنشأته حديثًا في المجلد المحدد.
## الخطوة 7: معالجة الأخطاء
ولتلخيص كل ذلك، لا تنس تضمين بعض معالجة الأخطاء حتى تتمكن من التقاط أي استثناءات قد تنشأ أثناء تشغيل الكود الخاص بك:
```csharp
catch (Exception ex)
{
    Console.WriteLine(ex.Message);
}
```

- سيؤدي هذا إلى عرض أي رسائل خطأ على وحدة التحكم، مما يساعدك على تصحيح أي خطأ في حال عدم عمله كما هو متوقع. تذكر، حتى أفضل المبرمجين يواجهون بعض المشاكل أحيانًا!
## خاتمة
وها قد انتهيت! نجحت في الإشارة إلى صورة في خلية Excel باستخدام Aspose.Cells لـ .NET. هذه التقنية البسيطة والفعّالة تُحسّن طريقة عرض البيانات، مما يجعل جداول بياناتك أكثر إفادة وجاذبية بصريًا. سواء كنت تُنشئ تقارير أو لوحات معلومات أو عروضًا تقديمية للبيانات، فإن إمكانية تضمين صور مرتبطة ببيانات الخلايا لا تُقدّر بثمن.
## الأسئلة الشائعة
### ما هو Aspose.Cells؟
Aspose.Cells هي مكتبة .NET لإدارة ملفات Excel، مما يسمح للمطورين بإنشاء مستندات Excel ومعالجتها وتحويلها دون الحاجة إلى تثبيت Microsoft Excel.
### هل يمكنني استخدام Aspose.Cells مع Xamarin؟
نعم، يمكن استخدام Aspose.Cells في مشاريع Xamarin، مما يتيح إمكانيات التطوير عبر الأنظمة الأساسية لإدارة ملفات Excel.
### هل هناك نسخة تجريبية مجانية متاحة؟
بالتأكيد! يمكنك الحصول على نسخة تجريبية مجانية من [صفحة التجربة المجانية لـ Aspose](https://releases.aspose.com/).
### ما هي التنسيقات التي يمكنني حفظ ملفات Excel بها؟
يدعم Aspose.Cells تنسيقات مختلفة، بما في ذلك XLSX، وXLS، وCSV، وPDF، والمزيد.
### كيف يمكنني طلب الدعم إذا واجهت مشاكل؟
يمكنك الحصول على الدعم من خلال [منتدى دعم Aspose](https://forum.aspose.com/c/cells/9)حيث يمكن للمجتمع وموظفي Aspose مساعدتك في استفساراتك.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}