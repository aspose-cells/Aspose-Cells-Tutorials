---
"description": "تعرّف على كيفية حماية الأعمدة في Excel باستخدام Aspose.Cells لـ .NET. اتبع هذا البرنامج التعليمي المفصل لتأمين الأعمدة في جداول بيانات Excel بفعالية."
"linktitle": "حماية الأعمدة في ورقة العمل باستخدام Aspose.Cells"
"second_title": "واجهة برمجة تطبيقات معالجة Excel Aspose.Cells .NET"
"title": "حماية الأعمدة في ورقة العمل باستخدام Aspose.Cells"
"url": "/ar/net/worksheet-security/protect-columns/"
"weight": 13
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# حماية الأعمدة في ورقة العمل باستخدام Aspose.Cells

## مقدمة
عند العمل برمجيًا مع ملفات Excel، قد تحتاج إلى حماية أجزاء معينة من ورقة العمل من التعديل. من أكثر المهام شيوعًا حماية أعمدة ورقة العمل، مع السماح بتعديل أجزاء أخرى منها. وهنا يأتي دور Aspose.Cells for .NET. في هذا البرنامج التعليمي، سنشرح لك خطوة بخطوة عملية حماية أعمدة محددة في ورقة عمل Excel باستخدام Aspose.Cells for .NET.
## المتطلبات الأساسية
قبل أن تغوص في حماية الأعمدة، هناك بعض الأشياء التي تحتاج إلى وضعها في مكانها:
- Visual Studio: يجب أن يكون لديك Visual Studio أو أي IDE متوافق مع .NET مثبتًا على جهازك.
- Aspose.Cells لـ .NET: يجب أن تكون مكتبة Aspose.Cells لـ .NET مُدمجة في مشروعك. يمكنك تنزيلها من [موقع إلكتروني](https://releases.aspose.com/cells/net/).
- المعرفة الأساسية بلغة C#: يفترض هذا البرنامج التعليمي أن لديك فهمًا أساسيًا لبرمجة C#.
إذا كنت جديدًا على Aspose.Cells، فمن المفيد التحقق من [التوثيق](https://reference.aspose.com/cells/net/) لفهم المزيد عن وظائف المكتبة وكيفية العمل معها.
## استيراد الحزم
للبدء، عليك استيراد مساحات الأسماء اللازمة للعمل مع Aspose.Cells. فيما يلي الاستيرادات اللازمة لهذا المثال:
```csharp
using System.IO;
using Aspose.Cells;
```
- Aspose.Cells: تعد هذه المساحة الأساسية ضرورية لأنها توفر الوصول إلى جميع الفئات المطلوبة للعمل مع ملفات Excel.
- النظام: هذه المساحة مخصصة للوظائف الأساسية للنظام مثل التعامل مع الملفات.
الآن بعد أن قمت باستيراد الحزم اللازمة، دعنا ننتقل إلى العملية الفعلية لحماية الأعمدة في ورقة العمل.
## دليل خطوة بخطوة لحماية الأعمدة في ورقة العمل
سنُقسّم هذه العملية إلى خطوات سهلة التنفيذ لتتمكن من متابعتها بسهولة. إليك كيفية حماية الأعمدة باستخدام Aspose.Cells لـ .NET.
## الخطوة 1: إعداد دليل المستندات
أولاً، علينا التأكد من وجود المجلد الذي سيتم حفظ الملف فيه. إذا لم يكن موجودًا، فسننشئه. هذا مهم لتجنب الأخطاء عند محاولة حفظ المصنف لاحقًا.
```csharp
string dataDir = "Your Document Directory";
// إنشاء الدليل إذا لم يكن موجودًا بالفعل.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
- dataDir: مسار الدليل الذي ستخزن فيه ملف الإخراج الخاص بك.
- Directory.Exists(): يتحقق هذا من وجود الدليل بالفعل.
- Directory.CreateDirectory(): إذا لم يكن الدليل موجودًا، فسيتم إنشاءه.
## الخطوة 2: إنشاء مصنف جديد
بعد تحديد المجلد، لننشئ مصنفًا جديدًا. سيكون هذا المصنف بمثابة الملف الأساسي الذي سنجري عليه التغييرات.
```csharp
Workbook wb = new Workbook();
```
- مصنف: هذا هو العنصر الرئيسي الذي يُمثل ملف Excel. يُمكن اعتباره حاويةً لجميع الأوراق والبيانات.
## الخطوة 3: الوصول إلى ورقة العمل الأولى
يحتوي كل مصنف على أوراق عمل متعددة، ونحن بحاجة إلى الوصول إلى الورقة الأولى حيث سنطبق حماية العمود.
```csharp
Worksheet sheet = wb.Worksheets[0];
```
- أوراق العمل[0]: يؤدي هذا إلى استرداد ورقة العمل الأولى في المصنف (أوراق عمل Excel مفهرسة بالصفر).
## الخطوة 4: تحديد كائنات Style وStyleFlag
بعد ذلك، سنقوم بتعريف كائنين، Style وStyleFlag، واللذان يتم استخدامهما لتخصيص إعدادات المظهر والحماية للخلايا.
```csharp
Style style;
StyleFlag flag;
```
- النمط: يسمح لنا بتغيير خصائص مثل الخط واللون وإعدادات الحماية للخلايا أو الأعمدة.
- StyleFlag: يستخدم هذا لتحديد الخصائص التي سيتم تطبيقها عند استخدام طريقة ApplyStyle.
## الخطوة 5: فتح جميع الأعمدة
افتراضيًا، يُقفل Excel جميع خلايا ورقة العمل عند تطبيق الحماية. لكننا نريد فتح جميع الأعمدة أولًا، لنتمكن لاحقًا من قفل أعمدة محددة، مثل العمود الأول.
```csharp
for (int i = 0; i <= 255; i++)
{
    style = sheet.Cells.Columns[(byte)i].Style;
    style.IsLocked = false;
    flag = new StyleFlag();
    flag.Locked = true;
    sheet.Cells.Columns[(byte)i].ApplyStyle(style, flag);
}
```
- الأعمدة[(بايت)i]: يتيح لك هذا الوصول إلى عمود محدد في ورقة العمل من خلال فهرسه (نقوم بالتنقل عبر الأعمدة من 0 إلى 255 هنا).
- style.IsLocked = false: يؤدي هذا إلى إلغاء قفل جميع الخلايا الموجودة في العمود.
- ApplyStyle(): يتم تطبيق النمط (مقفل أو غير مقفل) على العمود استنادًا إلى العلم.
## الخطوة 6: قفل العمود الأول
بعد فتح جميع الأعمدة، لنقفل العمود الأول لحمايته. هذا هو العمود الذي لن يتمكن المستخدمون من تعديله.
```csharp
style = sheet.Cells.Columns[0].Style;
style.IsLocked = true;
flag = new StyleFlag();
flag.Locked = true;
sheet.Cells.Columns[0].ApplyStyle(style, flag);
```
- الأعمدة[0]: يؤدي هذا إلى الوصول إلى العمود الأول (المؤشر 0).
- style.IsLocked = true: يؤدي هذا إلى قفل العمود الأول، مما يمنع المستخدمين من إجراء أي تغييرات عليه.
## الخطوة 7: حماية ورقة العمل
بعد أن حدّدنا حماية العمود الأول، علينا تطبيق الحماية على ورقة العمل بأكملها. هذا يضمن عدم إمكانية تعديل أي خلايا مقفلة (مثل العمود الأول) إلا بعد إزالة الحماية.
```csharp
sheet.Protect(ProtectionType.All);
```
- sheet.Protect(): يُطبّق هذا الخيار الحماية على كامل الورقة. نُحدّد ProtectionType.All لمنع أي تغييرات، ولكن يُمكنك تعديله لتمكين المستخدمين من التفاعل مع عناصر مُعيّنة.
## الخطوة 8: حفظ المصنف
أخيرًا، نحفظ المصنف في مكان محدد. في هذا المثال، نحفظه في المجلد الذي أنشأناه سابقًا.
```csharp
wb.Save(dataDir + "output.out.xls", SaveFormat.Excel97To2003);
```
- حفظ (): هذا يحفظ المصنف في نظام الملفات.
- SaveFormat.Excel97To2003: نحفظ المصنف بتنسيق Excel 97-2003 القديم. يمكنك تغيير هذا التنسيق إلى SaveFormat.Xlsx للتنسيق الأحدث.
## خاتمة
في هذا البرنامج التعليمي، شرحنا لك عملية حماية الأعمدة في ورقة عمل باستخدام Aspose.Cells لـ .NET. باتباع هذه الخطوات، يمكنك بسهولة تخصيص الأعمدة القابلة للتعديل والأعمدة المحمية، مما يمنحك تحكمًا أفضل في مستندات Excel. يوفر Aspose.Cells طريقة فعّالة للتعامل مع ملفات Excel برمجيًا، وبقليل من الممارسة، يمكنك إتقان هذه المهام لأتمتة سير عملك.
## الأسئلة الشائعة
### هل يمكنني حماية أكثر من عمود في وقت واحد؟  
نعم، يمكنك حماية عدة أعمدة عن طريق تطبيق القفل على كل عمود منها، تمامًا كما فعلنا مع العمود الأول.
### هل يمكنني السماح للمستخدمين بتحرير أعمدة محددة مع حماية الباقي؟  
بالتأكيد! يمكنك فتح أعمدة محددة عن طريق ضبط `style.IsLocked = false` بالنسبة لهم، ثم قم بتطبيق الحماية على ورقة العمل.
### كيف يمكنني إزالة الحماية من ورقة العمل؟  
لإزالة الحماية، ما عليك سوى الاتصال بـ `sheet.Unprotect()`يمكنك تمرير كلمة مرور إذا تم تعيين كلمة مرور أثناء الحماية.
### هل يمكنني تعيين كلمة مرور لحماية ورقة العمل؟  
نعم، يمكنك تمرير كلمة المرور كمعلمة إلى `sheet.Protect("yourPassword")` للتأكد من أن المستخدمين المصرح لهم فقط هم من يمكنهم إلغاء حماية الورقة.
### هل من الممكن حماية الخلايا الفردية بدلاً من الأعمدة بأكملها؟  
نعم، يمكنك قفل الخلايا الفردية عن طريق الوصول إلى نمط كل خلية وتطبيق خاصية القفل عليها.


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}