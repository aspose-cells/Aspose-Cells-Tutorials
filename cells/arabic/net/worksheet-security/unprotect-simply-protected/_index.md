---
title: إلغاء حماية ورقة العمل المحمية ببساطة باستخدام Aspose.Cells
linktitle: إلغاء حماية ورقة العمل المحمية ببساطة باستخدام Aspose.Cells
second_title: واجهة برمجة تطبيقات معالجة Excel الخاصة بـ Aspose.Cells .NET
description: يمكنك إلغاء حماية أوراق عمل Excel بسهولة دون الحاجة إلى كلمات مرور باستخدام Aspose.Cells for .NET. تعرّف على الإعداد وخطوات الترميز وحفظ النتائج بسلاسة.
weight: 20
url: /ar/net/worksheet-security/unprotect-simply-protected/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إلغاء حماية ورقة العمل المحمية ببساطة باستخدام Aspose.Cells

## مقدمة
إن إزالة الحماية من ورقة عمل Excel قد تكون بمثابة منقذ للحياة عندما تحتاج إلى إجراء تغييرات على الخلايا المقفلة أو تحديث البيانات. باستخدام Aspose.Cells for .NET، يمكنك القيام بذلك بسلاسة من خلال التعليمات البرمجية، مما يسمح لك بأتمتة إزالة الحماية من أوراق العمل دون الحاجة إلى كلمة مرور إذا كانت محمية ببساطة. سيرشدك هذا البرنامج التعليمي خلال كل خطوة، من إعداد المتطلبات الأساسية إلى كتابة التعليمات البرمجية اللازمة، كل ذلك بطريقة مباشرة تحافظ على الأمور بسيطة وفعالة.
## المتطلبات الأساسية
قبل أن نتعمق في الأمر، دعنا نتأكد من إعداد كل شيء لبدء إلغاء حماية أوراق العمل باستخدام Aspose.Cells لـ .NET:
-  Aspose.Cells for .NET: ستحتاج إلى هذه المكتبة للعمل مع ملفات Excel برمجيًا. يمكنك تنزيلها من[صفحة تحميل Aspose.Cells](https://releases.aspose.com/cells/net/) أو الوصول إلى نطاقها الواسع[التوثيق](https://reference.aspose.com/cells/net/).
- بيئة التطوير: بيئة مناسبة لتطبيقات .NET، مثل Visual Studio.
- الفهم الأساسي لـ C#: سيكون من المفيد الحصول على بعض المعرفة الأساسية لبرمجة C# لمتابعة أمثلة التعليمات البرمجية.
## استيراد الحزم
لاستخدام Aspose.Cells في مشروع .NET الخاص بك، ستحتاج أولاً إلى استيراد مكتبة Aspose.Cells. ويمكن القيام بذلك عن طريق إضافة حزمة Aspose.Cells NuGet إلى مشروعك. فيما يلي دليل سريع:
1. افتح مشروعك في Visual Studio.
2. في مستكشف الحلول، انقر بزر الماوس الأيمن فوق مشروعك وحدد "إدارة حزم NuGet".
3. ابحث عن "Aspose.Cells" وقم بتثبيت الإصدار الأحدث.
4. بمجرد التثبيت، أضف الاستيراد التالي إلى أعلى ملف الكود الخاص بك:
```csharp
using System.IO;
using Aspose.Cells;
```
الآن، دعونا نتعمق في العملية الفعلية لإلغاء حماية ورقة عمل Excel!
دعنا نقسم العملية إلى خطوات سهلة المتابعة. يفترض هذا المثال أن ورقة العمل التي تعمل عليها لا تحتوي على قفل محمي بكلمة مرور.
## الخطوة 1: تعيين دليل الملف
في هذه الخطوة، نحدد الدليل الذي نخزن فيه ملفات Excel. وهذا من شأنه أن يسهل علينا الوصول إلى ملف الإدخال وحفظ ملف الإخراج في المكان المطلوب.
```csharp
// المسار إلى دليل المستندات.
string dataDir = "Your Document Directory";
```
 عن طريق تعيين مسار الدليل في`dataDir`، يمكنك إنشاء اختصار مناسب للوصول إلى الملفات وحفظها دون الحاجة إلى كتابة المسار الكامل بشكل متكرر.
## الخطوة 2: تحميل مصنف Excel
 الآن، دعنا نحمل ملف Excel الذي نريد العمل عليه. هنا، نقوم بإنشاء`Workbook` الكائن الذي يمثل ملف Excel بأكمله.
```csharp
// إنشاء كائن مصنف
Workbook workbook = new Workbook(dataDir + "book1.xls");
   ```
 ال`Workbook` الكائن هو جزء أساسي من Aspose.Cells ويتيح لك تنفيذ إجراءات مختلفة على ملف Excel. من خلال تمرير مسار`"book1.xls"`يقوم هذا السطر بتحميل ملف الهدف إلى البرنامج.
## الخطوة 3: الوصول إلى ورقة العمل التي تريد إلغاء حمايتها
بمجرد تحميل المصنف، فإن الخطوة التالية هي تحديد ورقة العمل التي تريد إلغاء حمايتها. في هذا المثال، سنتمكن من الوصول إلى ورقة العمل الأولى في المصنف.
```csharp
// الوصول إلى ورقة العمل الأولى في ملف Excel
Worksheet worksheet = workbook.Worksheets[0];
```
 ال`Worksheets` تتيح لنا الخاصية الوصول إلى جميع أوراق العمل الموجودة داخل المصنف. من خلال تحديد`[0]`نحن الآن نصل إلى ورقة العمل الأولى. يمكنك تعديل هذا الفهرس إذا كانت ورقة العمل المستهدفة في موضع مختلف.
## الخطوة 4: إلغاء حماية ورقة العمل
الآن يأتي الجزء الأساسي: إلغاء حماية ورقة العمل. نظرًا لأن هذا البرنامج التعليمي يركز على أوراق العمل المحمية ببساطة (تلك التي لا تحتوي على كلمة مرور)، فإن إلغاء الحماية أمر بسيط.
```csharp
// إلغاء حماية ورقة العمل بدون كلمة مرور
worksheet.Unprotect();
```
 هنا،`Unprotect()` يُطلق عليه`worksheet` نظرًا لأننا نتعامل مع ورقة عمل غير محمية بكلمة مرور، فلا حاجة إلى معلمات إضافية. يجب أن تكون ورقة العمل الآن غير محمية وقابلة للتعديل.
## الخطوة 5: احفظ المصنف المحدث
بعد إلغاء حماية ورقة العمل، نحتاج إلى حفظ المصنف. يمكنك اختيار الكتابة فوق الملف الأصلي أو حفظه كملف جديد.
```csharp
// حفظ المصنف
workbook.Save(dataDir + "output.xls", SaveFormat.Excel97To2003);
```
 في هذا السطر، نقوم بحفظ المصنف باستخدام`Save` الطريقة.`SaveFormat.Excel97To2003` يضمن حفظ المصنف بتنسيق Excel الأقدم، وهو ما قد يكون مفيدًا إذا كان التوافق يشكل مشكلة. غيّر التنسيق إذا كنت تستخدم إصدارات أحدث من Excel.
## خاتمة
وهذا كل شيء! فباستخدام بضعة أسطر من التعليمات البرمجية، نجحت في إلغاء حماية ورقة عمل محمية ببساطة في ملف Excel باستخدام Aspose.Cells for .NET. هذا النهج رائع لأتمتة المهام في ملفات Excel، مما يوفر لك الوقت والجهد. بالإضافة إلى ذلك، باستخدام Aspose.Cells، ستتمتع بأدوات قوية لإدارة ملفات Excel والتلاعب بها برمجيًا، مما يفتح لك عالمًا من الاحتمالات لأتمتة سير عمل جداول البيانات الخاصة بك.
## الأسئلة الشائعة
### ما هو Aspose.Cells لـ .NET؟
Aspose.Cells for .NET هي مكتبة قوية للعمل مع ملفات Excel في تطبيقات .NET. فهي تتيح لك إنشاء ملفات Excel وتحريرها وتحويلها ومعالجتها دون الحاجة إلى تثبيت Microsoft Excel.
### هل يمكنني إلغاء حماية ورقة عمل محمية بكلمة مرور باستخدام هذه الطريقة؟
 لا، هذه الطريقة لا تعمل إلا مع أوراق العمل المحمية ببساطة. بالنسبة للأوراق المحمية بكلمة مرور، ستحتاج إلى تقديم كلمة المرور في`Unprotect()` طريقة.
### هل أحتاج إلى تثبيت Microsoft Excel لاستخدام Aspose.Cells؟
لا، يعمل Aspose.Cells بشكل مستقل عن Microsoft Excel، لذا لا تحتاج إلى تثبيته على نظامك.
### هل يمكنني حفظ ورقة العمل غير المحمية بتنسيقات Excel الأحدث؟
 نعم، يمكنك ذلك. يدعم Aspose.Cells تنسيقات متعددة، بما في ذلك`XLSX` . فقط قم بتغيير تنسيق الحفظ وفقًا لذلك في`Save` طريقة.
### هل Aspose.Cells متاح لمنصات أخرى غير .NET؟
نعم، يحتوي Aspose.Cells على إصدارات خاصة بـ Java ومنصات أخرى، مما يسمح بوظائف مماثلة عبر بيئات برمجة مختلفة.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
