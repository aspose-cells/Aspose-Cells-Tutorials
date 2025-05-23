---
"description": "تعلّم كيفية إضافة روابط داخلية إلى الخلايا في جداول بيانات Excel باستخدام Aspose.Cells لـ .NET. حسّن عملية التنقل في جداول بياناتك بسهولة."
"linktitle": "إضافة رابط إلى خلية ورقة أخرى في Excel"
"second_title": "واجهة برمجة تطبيقات معالجة Excel Aspose.Cells .NET"
"title": "إضافة رابط إلى خلية ورقة أخرى في Excel"
"url": "/ar/net/excel-working-with-hyperlinks/add-link-to-other-sheet-cell/"
"weight": 11
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# إضافة رابط إلى خلية ورقة أخرى في Excel

## مقدمة
تخيل أنك تتنقل عبر مطار مزدحم؛ لن ترغب في إضاعة الوقت في البحث عن بوابتك. بدلاً من ذلك، سترشدك اللافتات الواضحة والروابط المفيدة بسلاسة إلى وجهتك. وبالمثل، في برامج جداول البيانات مثل Excel، تُسهّل إضافة الروابط التشعبية عملية التنقل وتجعل بياناتك أكثر سهولة في الاستخدام. سواء كنت تدير ميزانية معقدة، أو تتتبّع المبيعات، أو تتعامل مع أي مجموعة بيانات كبيرة، فإن إمكانية الربط بجداول بيانات أخرى توفر عليك الكثير من الوقت والجهد. سنتناول اليوم كيفية إضافة رابط إلى خلية في جدول بيانات آخر باستخدام Aspose.Cells لـ .NET. سيشرح لك هذا الدليل خطوة بخطوة العملية، مما يضمن لك إمكانية تطبيق هذه الميزة الفعّالة في جداول بيانات Excel.
## المتطلبات الأساسية
قبل أن نبدأ، هناك بعض الأشياء التي ستحتاجها:
1. Visual Studio: تأكد من تثبيت Visual Studio على جهاز الكمبيوتر الخاص بك. إنه أداة مفيدة لتطوير .NET.
2. مكتبة Aspose.Cells: ستحتاج إلى تنزيل مكتبة Aspose.Cells لـ .NET وتثبيتها. يمكنك الحصول عليها من [صفحة تنزيلات Aspose Cells](https://releases.aspose.com/cells/net/).
3. معرفة أساسية بلغة C#: يُعدّ فهم أساسيات برمجة C# ركيزةً أساسيةً في نجاحك. يفترض هذا الدليل أنك على درايةٍ جيدةٍ بقواعد لغة C#.
4. Microsoft Excel: يساعدك وجود Excel على جهازك على تصور نتائج ما ستقوم بإنشائه.
5. .NET Framework: تأكد من أنك تعمل ضمن إصدار متوافق من .NET Framework الذي يدعم مكتبة Aspose.Cells.
## استيراد الحزم
لبدء مشروعك، ستحتاج إلى استيراد مساحات الأسماء اللازمة. إليك كيفية القيام بذلك في ملف C#:
```csharp
using System;
using System.IO;
using Aspose.Cells;
```
باستخدام هذا الاستيراد، ستكون جاهزًا تمامًا لاستخدام الميزات القوية لـ Aspose.Cells. 
الآن، دعونا نقوم بتقسيم المهمة الأساسية - إضافة ارتباط تشعبي إلى خلية في ورقة أخرى من نفس ملف Excel! 
## الخطوة 1: إعداد بيئة مشروعك
قبل كتابة أي كود، نحتاج إلى إنشاء مشروع C# جديد. 
1. افتح Visual Studio.
2. إنشاء مشروع تطبيق وحدة التحكم C# جديد. 
3. قم بتسمية مشروعك بشيء وصفي مثل "ExcelLinkDemo".
4. أضف مرجعًا إلى ملف Aspose.Cells.dll. يمكنك القيام بذلك بالنقر بزر الماوس الأيمن على "المراجع" في مستكشف الحلول، ثم اختيار "إضافة مرجع"، والانتقال إلى مكان تثبيت Aspose.Cells.
## الخطوة 2: تحديد دليل الإخراج الخاص بك
بعد ذلك، عليك تحديد مكان حفظ ملف إكسل الناتج. إليك كيفية تحديده في الكود:
```csharp
// دليل الإخراج لملف Excel الخاص بك
string outputDir = "Your Document Directory"; // استبدل بالدليل الخاص بك
```
تأكد من الاستبدال `"Your Document Directory"` مع المسار الذي تريد أن يوجد فيه ملف الإخراج.
## الخطوة 3: إنشاء كائن المصنف
أنت الآن جاهز لإنشاء مصنف Excel الخاص بك! هنا ستُحفظ جميع أوراقك وبياناتك.
```csharp
// إنشاء كائن مصنف
Workbook workbook = new Workbook();
```
يقوم هذا السطر بإنشاء مصنف عمل جديد في الذاكرة، مما يوفر لك لوحة قماشية فارغة للعمل عليها.
## الخطوة 4: إضافة ورقة عمل جديدة
في Excel، يمكن أن يحتوي كل مصنف على عدة أوراق. لنُضِف ورقةً واحدةً إلى مصنفنا.
```csharp
// إضافة ورقة عمل جديدة إلى كائن المصنف
workbook.Worksheets.Add(); // يضيف ورقة عمل فارغة جديدة بشكل افتراضي
```
يضيف هذا الأمر ورقة عمل جديدة، والآن يحتوي المصنف الخاص بك على ورقة واحدة على الأقل يمكنك التعامل معها.
## الخطوة 5: الوصول إلى ورقة العمل الأولى
للعمل مع ورقة العمل الأولى (المعروفة باسم الورقة الافتراضية)، ستحتاج إلى الرجوع إليها.
```csharp
// الحصول على مرجع ورقة العمل الأولى (الافتراضية)
Worksheet worksheet = workbook.Worksheets[0];
```
الآن، `worksheet` هو إشارة إلى الورقة الأولى التي سنضيف إليها ارتباطنا التشعبي.
## الخطوة 6: إضافة ارتباط تشعبي داخلي
إليكم الجزء المثير! سننشئ رابطًا تشعبيًا في الخلية "B3" يشير إلى الخلية "B9" في ورقة عمل أخرى.
```csharp
// إضافة ارتباط تشعبي داخلي إلى الخلية "B9" من ورقة العمل الأخرى "Sheet2"
worksheet.Hyperlinks.Add("B3", 1, 1, "Sheet2!B9");
```
في هذا الأمر، نطلب من Excel تحويل الخلية "B3" إلى رابط. المعلمات هي:
- موقع الخلية للرابط التشعبي ("B3").
- فهرس الورقة الذي نربط به (1، والذي يشير إلى الورقة الثانية).
- الخلية المستهدفة التي نريد الارتباط بها (الخلية الموجودة في "Sheet2").
## الخطوة 7: إضافة نص العرض للارتباط التشعبي
عند النقر على رابط تشعبي، ستحتاج إلى نص عرض لتوضيح وجهة الرابط. وهنا يأتي دور السطر التالي.
```csharp
worksheet.Hyperlinks[0].TextToDisplay = "Link To Other Sheet Cell";
```
سيؤدي هذا إلى ظهور "الارتباط بخلية ورقة أخرى" في الخلية "B3"، مما يرشد أي شخص يستخدم جدول البيانات.
## الخطوة 8: احفظ مصنفك
بعد إعداد كل شيء، حان الوقت لحفظ المصنف الذي قمت بإنشائه حديثًا باستخدام الارتباط التشعبي المضمن.
```csharp
// حفظ ملف Excel مع الارتباط التشعبي
workbook.Save(outputDir + "outputAddingLinkToOtherSheetCell.xlsx");
```
تأكد من تحديد المسار الصحيح في `outputDir` حتى يتم حفظ ملف Excel الخاص بك بشكل صحيح.
## الخطوة 9: تأكيد العملية
وأخيرا، دعونا نعلم المستخدم أن العملية تمت بنجاح.
```csharp
Console.WriteLine("AddingLinkToOtherSheetCell executed successfully.");
```
وها أنت ذا! لقد أنشأتَ برنامج C# أساسيًا يضيف رابطًا تشعبيًا داخليًا إلى مصنف Excel باستخدام Aspose.Cells لـ .NET.
## خاتمة
في هذا البرنامج التعليمي، شرحنا الخطوات اللازمة لإضافة رابط تشعبي إلى ورقة عمل أخرى في مصنف Excel باستخدام Aspose.Cells لـ .NET. تُعدّ الروابط في جداول البيانات بمثابة معالم بارزة في بحر من البيانات، مما يُسهّل عملية التنقل. تخيّل مدى كفاءة سير عملك مع جداول بيانات مُرتبطة بشكل صحيح! الآن وقد أصبحت هذه الأداة الفعّالة بين يديك، لا تتردد في تجربة المزيد من إمكانيات Aspose.Cells لتحسين إنتاجيتك.
## الأسئلة الشائعة
### ما هو Aspose.Cells؟  
Aspose.Cells هي مكتبة .NET قوية لإنشاء ملفات Excel ومعالجتها دون استخدام Microsoft Excel.
### هل يمكنني استخدام Aspose.Cells مجانًا؟  
نعم! يمكنك تنزيل نسخة تجريبية مجانية من [هنا](https://releases.aspose.com/).
### هل أحتاج إلى تثبيت Microsoft Excel لاستخدام Aspose.Cells؟  
لا، يعمل Aspose.Cells بشكل مستقل عن Microsoft Excel.
### هل من الممكن ربط صفحات متعددة؟  
بالتأكيد! يمكنك إنشاء عدة روابط تشعبية تُشير إلى أوراق مختلفة باستخدام نفس النهج.
### أين يمكنني الحصول على الدعم لـ Aspose.Cells؟  
يمكنك التواصل مع مجتمع Aspose للحصول على الدعم [هنا](https://forum.aspose.com/c/cells/9).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}