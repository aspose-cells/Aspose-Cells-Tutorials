---
title: حماية خلايا محددة في ورقة العمل باستخدام Aspose.Cells
linktitle: حماية خلايا محددة في ورقة العمل باستخدام Aspose.Cells
second_title: واجهة برمجة تطبيقات معالجة Excel الخاصة بـ Aspose.Cells .NET
description: تعرف على كيفية حماية خلايا معينة في ورقة عمل Excel باستخدام Aspose.Cells for .NET. قم بتأمين البيانات الحساسة ومنع التغييرات العرضية في بضع خطوات فقط.
weight: 14
url: /ar/net/worksheet-security/protect-specific-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# حماية خلايا محددة في ورقة العمل باستخدام Aspose.Cells

## مقدمة
في هذا البرنامج التعليمي، سنطلعك على عملية حماية خلايا معينة في ورقة عمل Excel. وبحلول النهاية، ستتمكن من قفل الخلايا بثقة مثل المحترفين، ومنع التغييرات غير المصرح بها مع الحفاظ على مرونة ورقة العمل الخاصة بك عند الحاجة.
## المتطلبات الأساسية
قبل أن نتعمق في التفاصيل، دعنا نتأكد من أن لديك كل ما تحتاجه لمتابعة هذا البرنامج التعليمي بسلاسة:
1. Visual Studio – إذا لم تكن قد قمت بذلك بالفعل، فقم بتنزيل Visual Studio وتثبيته. سيكون هذا هو البيئة الأساسية التي يمكنك من خلالها تشغيل تطبيقات .NET.
2.  Aspose.Cells لـ .NET – ستحتاج إلى مكتبة Aspose.Cells للعمل مع ملفات Excel في تطبيقات .NET الخاصة بك. إذا لم تقم بتثبيتها بعد، فيمكنك الحصول على أحدث إصدار من[موقع اسبوس](https://releases.aspose.com/cells/net/).
3. .NET Framework أو .NET Core – يعمل هذا البرنامج التعليمي مع كل من .NET Framework و.NET Core. فقط تأكد من أن مشروعك متوافق مع Aspose.Cells.
بمجرد وضع هذه العناصر في مكانها، ستكون جاهزًا للبدء.
## استيراد الحزم
قبل الانتقال إلى الدليل التفصيلي خطوة بخطوة، يجب عليك التأكد من استيراد مساحات الأسماء اللازمة للعمل مع Aspose.Cells. في مشروعك، قم بتضمين عبارات الاستيراد التالية في أعلى الملف:
```csharp
using System.IO;
using Aspose.Cells;
```
ستتيح لك هذه المساحات الاسمية التفاعل مع ملفات Excel والفئات المطلوبة لتصميم خلايا ورقة العمل وحمايتها.
الآن، دعنا نقسم الأمر إلى خطوات بسيطة لحماية خلايا معينة في ورقة العمل الخاصة بك باستخدام Aspose.Cells لـ .NET. سنحمي الخلايا A1 وB1 وC1، مع ترك بقية ورقة العمل مفتوحة للتعديل.
## الخطوة 1: إنشاء مصنف وورقة عمل جديدة
أولاً وقبل كل شيء، عليك إنشاء مصنف جديد (ملف Excel) وورقة عمل بداخله. هذا هو المكان الذي ستطبق فيه حماية الخلية.
```csharp
// المسار إلى دليل المستندات.
string dataDir = "Your Document Directory";
// إنشاء الدليل إذا لم يكن موجودًا بالفعل.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
// إنشاء مصنف جديد.
Workbook wb = new Workbook();
// إنشاء كائن ورقة عمل والحصول على الورقة الأولى.
Worksheet sheet = wb.Worksheets[0];
```
 في هذه الخطوة، ستقوم أيضًا بإنشاء دليل لتخزين ملف Excel الناتج إذا لم يكن موجودًا بالفعل.`Workbook` تقوم الفئة بتهيئة ملف Excel جديد، و`Worksheets[0]` يسمح لنا بالعمل مع الورقة الأولى في المصنف.
## الخطوة 2: إلغاء قفل جميع الأعمدة
بعد ذلك، ستقوم بإلغاء قفل جميع الأعمدة في ورقة العمل. وهذا يضمن إمكانية تحرير جميع الخلايا في ورقة العمل بشكل افتراضي. وسنقوم لاحقًا بإلغاء قفل الخلايا التي نريد حمايتها فقط.
```csharp
// تعريف كائن النمط.
Style style;
// تعريف كائن styleflag
StyleFlag styleflag;
// قم بالمرور على جميع الأعمدة في ورقة العمل وإلغاء قفلها.
for (int i = 0; i <= 255; i++)
{
    style = sheet.Cells.Columns[(byte)i].Style;
    style.IsLocked = false;
    styleflag = new StyleFlag();
    styleflag.Locked = true;
    sheet.Cells.Columns[(byte)i].ApplyStyle(style, styleflag);
}
```
 في كتلة التعليمات البرمجية هذه، نقوم بالتكرار عبر جميع الأعمدة (حتى 255) وتعيين`IsLocked` الممتلكات ل`false`يؤدي هذا في الأساس إلى إلغاء قفل جميع الخلايا في تلك الأعمدة، مما يجعلها قابلة للتحرير افتراضيًا. ثم نطبق النمط على العمود الذي يحتوي على`ApplyStyle()` طريقة.
## الخطوة 3: قفل خلايا محددة (A1، B1، C1)
 الآن بعد أن تم إلغاء قفل جميع الأعمدة، سنركز على قفل خلايا معينة، وهي A1 وB1 وC1. سنعدل أنماط الخلايا ونحددها`IsLocked` الممتلكات ل`true`.
```csharp
// قم بإغلاق الخلايا الثلاث...أي A1، B1، C1.
style = sheet.Cells["A1"].GetStyle();
style.IsLocked = true;
sheet.Cells["A1"].SetStyle(style);
style = sheet.Cells["B1"].GetStyle();
style.IsLocked = true;
sheet.Cells["B1"].SetStyle(style);
style = sheet.Cells["C1"].GetStyle();
style.IsLocked = true;
sheet.Cells["C1"].SetStyle(style);
```
تضمن هذه الخطوة تأمين الخلايا A1 وB1 وC1. هذه هي الخلايا التي سيتم حمايتها ولن تكون قابلة للتحرير بمجرد تطبيق حماية ورقة العمل.
## الخطوة 4: حماية ورقة العمل
بعد قفل الخلايا الضرورية، تكون الخطوة التالية هي حماية ورقة العمل بأكملها. تجعل هذه الخطوة الخلايا المقفلة (A1، B1، C1) غير قابلة للتعديل، بينما تظل الخلايا الأخرى مفتوحة للتعديل.
```csharp
// وأخيرا، قم بحماية الورقة الآن.
sheet.Protect(ProtectionType.All);
```
 ال`Protect` يتم استدعاء الطريقة على ورقة العمل، مع تحديد ضرورة حماية كافة جوانب الورقة. يؤدي هذا إلى قفل الخلايا المحددة التي تم وضع علامة عليها`IsLocked = true` ويضمن عدم إمكانية تغييرها بواسطة المستخدمين.
## الخطوة 5: احفظ المصنف
بمجرد قفل الخلايا وحماية الورقة، يمكنك حفظ المصنف في الموقع المطلوب.
```csharp
// احفظ ملف Excel.
wb.Save(dataDir + "output.out.xls", SaveFormat.Excel97To2003);
```
هذه الخطوة تحفظ المصنف في`dataDir` المجلد الذي يحمل اسم الملف`output.out.xls`يمكنك تعديل اسم الملف والدليل بما يتناسب مع احتياجاتك. يتم حفظ الملف بتنسيق Excel 97-2003، ولكن يمكنك تعديله وفقًا لمتطلباتك.
## خاتمة
إن حماية خلايا معينة في ورقة عمل Excel باستخدام Aspose.Cells for .NET هي عملية بسيطة. باتباع الخطوات المذكورة أعلاه، يمكنك قفل خلايا معينة مع السماح لخلايا أخرى بالبقاء قابلة للتعديل. هذه الميزة مفيدة للغاية عند مشاركة المصنفات مع الآخرين، حيث تساعدك على التحكم في البيانات التي يمكن تعديلها والبيانات التي يجب أن تظل محمية. سواء كنت تعمل على بيانات حساسة أو ببساطة تمنع التغييرات العرضية، فإن Aspose.Cells يوفر حلاً مرنًا وقويًا.
## الأسئلة الشائعة
### كيف يمكنني حماية مجموعة محددة من الخلايا بدلاً من عدد قليل منها؟
يمكنك تعديل الكود للتنقل عبر نطاق محدد من الخلايا أو الأعمدة وقفله، بدلاً من قفل الخلايا الفردية يدويًا.
### هل يمكنني إضافة كلمات مرور لحماية ورقة العمل؟
نعم، يمكنك تحديد كلمة مرور عند الاتصال`Protect()` طريقة لتقييد المستخدمين من إلغاء حماية الورقة دون استخدام كلمة المرور الصحيحة.
### هل يمكنني حماية صفوف أو أعمدة محددة بدلاً من الخلايا؟
 نعم، يسمح لك Aspose.Cells بقفل الصفوف أو الأعمدة بالكامل عن طريق تعديل`IsLocked` الخاصية الخاصة بالصفوف أو الأعمدة، على غرار الطريقة التي قمنا بها بقفل الخلايا.
### كيف يمكنني إلغاء حماية ورقة العمل؟
 لإلغاء حماية ورقة العمل، استخدم`Unprotect()` الطريقة، مع توفير كلمة المرور اختياريًا إذا تم تعيين كلمة مرور أثناء الحماية.
### هل يمكنني استخدام Aspose.Cells لإجراء عمليات أخرى في Excel، مثل إضافة الصيغ أو المخططات البيانية؟
بالتأكيد! Aspose.Cells عبارة عن مكتبة قوية تتيح لك تنفيذ مجموعة واسعة من عمليات Excel، بما في ذلك إضافة الصيغ وإنشاء المخططات وغير ذلك الكثير.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
