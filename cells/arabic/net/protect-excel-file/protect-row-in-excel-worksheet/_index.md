---
"description": "اكتشف في هذا البرنامج التعليمي كيفية حماية صفوف جدول بيانات Excel باستخدام Aspose.Cells لـ .NET. شرح خطوة بخطوة بلغة C#."
"linktitle": "حماية الصف في ورقة عمل Excel"
"second_title": "مرجع واجهة برمجة التطبيقات Aspose.Cells لـ .NET"
"title": "حماية الصف في ورقة عمل Excel"
"url": "/ar/net/protect-excel-file/protect-row-in-excel-worksheet/"
"weight": 60
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# حماية الصف في ورقة عمل Excel

## مقدمة

عند العمل مع جداول بيانات Excel، غالبًا ما يكون من الضروري حماية صفوف محددة للحفاظ على سلامة البيانات. سواء كنت تدير مشروعًا جماعيًا، أو تُشرف على تقرير مالي، أو تُشارك وثائق، فإن تقييد الوصول إلى صفوف معينة يُمكن أن يمنع التغييرات غير المرغوب فيها. في هذا البرنامج التعليمي، سنستكشف كيفية استخدام Aspose.Cells لـ .NET لحماية صفوف محددة في ورقة عمل Excel. هيا، هيا بنا نغوص في عالم البرمجة الشيق باستخدام لغة C#!

## المتطلبات الأساسية

قبل أن نبدأ بالتطبيق العملي، لنتأكد من إعداد كل شيء. إليك بعض المتطلبات الأساسية:

1. Aspose.Cells لـ .NET: قم بتنزيل المكتبة من [موقع Aspose](https://releases.aspose.com/cells/net/)تأكد من حصولك على الإصدار الأحدث لجميع الميزات الجديدة وإصلاحات الأخطاء.
2. Visual Studio: ستساعدك بيئة التطوير المتكاملة (IDE) مثل Visual Studio (Community أو Professional أو Enterprise) على تجميع وتشغيل كود C# الخاص بك بشكل فعال.
3. إطار عمل .NET: ستحتاج إلى إصدار متوافق من إطار عمل .NET. يدعم Aspose.Cells إصدارات متعددة، لذا تأكد من تحديث إصدارك. 
4. المعرفة الأساسية بلغة C#: سيكون الفهم الأساسي للغة C# مفيدًا أثناء كتابة الكود الخاص بنا طوال هذا الدليل.
5. الوثائق المرجعية: تعرف على [توثيق Aspose.Cells لـ .NET](https://reference.aspose.com/cells/net/) لمزيد من التفاصيل حول الأساليب والفئات المستخدمة.

## استيراد الحزم

الخطوة الأولى في رحلتنا هي استيراد الحزم اللازمة في مشروع C#. يعمل Aspose.Cells من خلال مجموعة من الفئات التي نحتاج إلى تضمينها:

```csharp
using System.IO;
using Aspose.Cells;
```

الآن بعد أن قمنا باستيراد الحزم المطلوبة، دعنا ننتقل إلى الخطوات اللازمة لإنشاء مصنف Excel وحماية صف معين. 

## الخطوة 1: تحديد الدليل

في هذه الخطوة، سنحدد مكان حفظ ملف إكسل. من المهم التأكد من وجود هذا المجلد، وإلا فسننشئه برمجيًا عند الحاجة.

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY"; // استبدل بمسار المستند الخاص بك
bool IsExists = Directory.Exists(dataDir);
if (!IsExists)
{
    Directory.CreateDirectory(dataDir);
}
```
في هذا الكود، استبدل `YOUR DOCUMENT DIRECTORY` مع المسار الفعلي الذي تريد حفظ ملف Excel فيه.

## الخطوة 2: إنشاء مصنف جديد

بعد ذلك، سننشئ دفتر عمل جديدًا لإجراء جميع التعديلات. هذه خطوة أساسية، تمامًا مثل وضع الأساس قبل بناء منزل أحلامك.

```csharp
Workbook wb = new Workbook();
```
يقوم هذا الخط بتهيئة مثيل جديد لـ `Workbook` الصف، إنشاء ورقة عمل جديدة لنا للعمل عليها.

## الخطوة 3: الوصول إلى ورقة العمل

بعد إنشاء مصنف العمل، لنبدأ بأول ورقة عمل. تذكر أن ملف Excel قد يحتوي على عدة أوراق عمل، لذا من الضروري اختيار الورقة المناسبة.

```csharp
Worksheet sheet = wb.Worksheets[0]; // الوصول إلى الورقة الأولى
```

## الخطوة 4: فتح جميع الأعمدة

قبل قفل صف معين، يُنصح بإلغاء قفل جميع الأعمدة أولًا. هذا يسمح لنا بالتحكم في البيانات التي تبقى قابلة للتعديل لاحقًا.

```csharp
Style style;
StyleFlag flag;

// قم بالمرور عبر جميع الأعمدة وفتحها
for (int i = 0; i <= 255; i++)
{
    style = sheet.Cells.Columns[(byte)i].Style;
    style.IsLocked = false;
    flag = new StyleFlag();
    flag.Locked = true;
    sheet.Cells.Columns[(byte)i].ApplyStyle(style, flag);
}
```
تتكرر هذه الحلقة خلال أول 256 عمودًا، وتفتح قفل كل عمود لضمان أذونات التحرير الافتراضية.

## الخطوة 5: قفل الصف المحدد

الآن، سنستهدف الصف الأول من ورقة العمل للقفل. تضمن هذه الخطوة عدم تمكن المستخدمين من إجراء تغييرات غير مصرح بها على البيانات المهمة في هذا الصف.

```csharp
style = sheet.Cells.Rows[0].Style; // احصل على نمط الصف الأول
style.IsLocked = true; // قفل الصف
flag = new StyleFlag();
flag.Locked = true; // ضبط علم القفل
sheet.Cells.ApplyRowStyle(0, style, flag); // تطبيق النمط على الصف الأول
```
هنا، نستعيد نمط الصف الأول، ونضع عليه علامة "مقفل"، ثم نطبق نمط القفل. هذا يُشبه وضع قفل على درج مهم - وهو أمر ضروري لتأمين المعلومات الحساسة!

## الخطوة 6: حماية الورقة

بعد قفل صفنا، لنتخذ خطوة إضافية ونحمي ورقة العمل بالكامل. سيؤدي هذا إلى تطبيق القفل على جميع الوظائف المحددة في `ProtectionType`.

```csharp
sheet.Protect(ProtectionType.All); // حماية الورقة بكل المميزات
```
من خلال تطبيق هذه الحماية، لا يمكن للمستخدمين تحرير الصف المقفل أو إجراء أي تغييرات قد تؤثر على المناطق المقفلة.

## الخطوة 7: حفظ المصنف

الخطوة الأخيرة هي حفظ مصنف العمل. هنا تُكلّل جهودنا بالنجاح، ونرى جدول بياناتنا الجميل والمحميّ ينبض بالحياة!

```csharp
wb.Save(dataDir + "output.out.xls", SaveFormat.Excel97To2003);
```
تأكد من أن اسم الملف المحفوظ وتنسيقه يتوافقان مع متطلباتك. في هذه الحالة، سنحفظه بتنسيق Excel قديم (Excel 97-2003).

## خاتمة

وها قد انتهيت! لقد تعلمت بنجاح كيفية حماية صف معين في ورقة عمل Excel باستخدام Aspose.Cells لـ .NET. ببضعة أسطر برمجية فقط، لم تنشئ مصنفًا فحسب، بل تمكنت أيضًا من تأمين معلومات حساسة، مما يضمن سلامة ملفات Excel وموثوقيتها. سواءً كان تقريرًا ماليًا، أو كشف حضور، أو خطة مشروع تعاوني، فإن حماية البيانات المهمة أمر بالغ الأهمية. 

## الأسئلة الشائعة

### ما هو Aspose.Cells؟
Aspose.Cells هي مكتبة قوية لـ .NET تسمح للمستخدمين بإنشاء ملفات Excel ومعالجتها وتحويلها برمجيًا.

### هل يمكنني حماية صفوف متعددة في وقت واحد باستخدام Aspose.Cells؟
نعم، يمكنك توسيع تقنية القفل عن طريق التكرار عبر صفوف متعددة وتطبيق تغييرات نمطية مماثلة على كل منها.

### هل هناك طريقة لفتح الصفوف بعد الحماية؟
نعم، يمكنك إلغاء حماية الورقة أولاً ثم ضبطها `IsLocked` خاصية الصفوف المطلوبة، ثم إعادة تطبيق الحماية لاحقًا.

### هل يدعم Aspose.Cells تنسيقات أخرى إلى جانب Excel؟
بالتأكيد! يُمكن لـ Aspose.Cells تحويل وحفظ مصنفات العمل بتنسيقات مُختلفة، بما في ذلك CSV وPDF وHTML.

### أين يمكنني الحصول على الدعم لـ Aspose.Cells؟
يمكنك زيارة [منتدى دعم Aspose](https://forum.aspose.com/c/cells/9) للحصول على المساعدة والتوجيه المجتمعي.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}