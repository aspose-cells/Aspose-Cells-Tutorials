---
title: حفظ المصنف بصيغة نصية CSV
linktitle: حفظ المصنف بصيغة نصية CSV
second_title: واجهة برمجة تطبيقات معالجة Excel الخاصة بـ Aspose.Cells .NET
description: تعرف على كيفية تحويل مصنفات Excel إلى تنسيق CSV بسهولة باستخدام Aspose.Cells في هذا البرنامج التعليمي الشامل خطوة بخطوة المصمم لمطوري .NET.
weight: 17
url: /ar/net/saving-files-in-different-formats/save-workbook-to-text-csv-format/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# حفظ المصنف بصيغة نصية CSV

## مقدمة
عند التعامل مع البيانات، يمكن للتنسيق الذي تختاره أن يحدد مدى سهولة التعامل معها. من بين التنسيقات الأكثر شيوعًا للتعامل مع البيانات الجدولية تنسيق CSV (القيم المفصولة بفواصل). إذا كنت مطورًا تعمل مع ملفات Excel وتحتاج إلى تحويل المصنفات إلى تنسيق CSV، فإن Aspose.Cells for .NET هي مكتبة رائعة تبسط هذه المهمة. في هذا البرنامج التعليمي، سنوضح الخطوات لتحويل مصنف Excel إلى تنسيق CSV نصي بسلاسة.
## المتطلبات الأساسية
قبل أن نبدأ، دعنا نتأكد من أن كل شيء جاهز للبدء:
1. المعرفة الأساسية بلغة C# و.NET: نظرًا لأننا سنكتب التعليمات البرمجية بلغة C#، فإن الإلمام باللغة وإطار عمل .NET أمر ضروري.
2. مكتبة Aspose.Cells: تأكد من تثبيت مكتبة Aspose.Cells for .NET في بيئة التطوير الخاصة بك. يمكنك تنزيلها[هنا](https://releases.aspose.com/cells/net/).
3. Visual Studio أو أي بيئة تطوير متكاملة C#: ستحتاج إلى بيئة تطوير متكاملة لكتابة وتنفيذ التعليمات البرمجية الخاصة بك. Visual Studio هو خيار شائع.
4. مصنف Excel: قم بإعداد مصنف Excel نموذجي (على سبيل المثال، "book1.xls") يحتوي على بعض البيانات لاختبار التحويل.
## استيراد الحزم
الآن بعد أن قمنا بتغطية المتطلبات الأساسية، فإن الخطوة الأولى في العملية هي استيراد الحزم اللازمة. في مشروع C# الخاص بك، تحتاج إلى تضمين مساحة الأسماء التالية في أعلى ملف التعليمات البرمجية الخاص بك:
```csharp
using System.IO;
using Aspose.Cells;
using System;
```
ستتيح لك هذه المساحات الأسماء الوصول إلى الفئات والطرق اللازمة للعمل مع ملفات Excel وإدارة تدفقات الذاكرة.
## الخطوة 1: تحديد المسار إلى دليل المستندات
الخطوة الأولى في عمليتنا هي تحديد مكان تخزين مستنداتنا (دفاتر عمل Excel). وهذا أمر ضروري لأنه يسمح لبرنامجنا بمعرفة مكان العثور على الملفات التي يحتاج إلى معالجتها. 
```csharp
// المسار إلى دليل المستندات.
string dataDir = "Your Document Directory";
```
 تأكد من الاستبدال`"Your Document Directory"` مع المسار الفعلي الذي يوجد به ملف "book1.xls" الخاص بك. قد يكون هذا دليلاً على جهاز الكمبيوتر الخاص بك أو مسارًا إلى خادم.
## الخطوة 2: قم بتحميل مصنف المصدر الخاص بك
بعد ذلك، نحتاج إلى تحميل مصنف Excel الذي سيتم تحويله إلى تنسيق CSV.
```csharp
// قم بتحميل مصنف المصدر الخاص بك
Workbook workbook = new Workbook(dataDir + "book1.xls");
```
 ال`Workbook` تسمح الفئة من مكتبة Aspose.Cells بالتعامل مع مصنفات Excel والوصول إليها. من خلال تمرير مسار الملف، نقوم بتحميل المصنف المحدد للمعالجة.
## الخطوة 3: تهيئة مجموعة بايتات لبيانات المصنف
قبل أن نبدأ في تحويل المصنف إلى ملف CSV، نحتاج إلى تهيئة مصفوفة بايتات فارغة والتي ستحتوي في النهاية على كافة بيانات ورقة العمل.
```csharp
// مصفوفة مكونة من 0 بايت
byte[] workbookData = new byte[0];
```
ستقوم مجموعة البايتات هذه بدمج البيانات من كل ورقة عمل في بنية واحدة يمكننا كتابتها في ملف لاحقًا.
## الخطوة 4: إعداد خيارات حفظ النص
الآن، دعنا نحدد الخيارات الخاصة بكيفية حفظ تنسيق النص. يمكنك اختيار فواصل مخصصة أو الالتزام بعلامات التبويب.
```csharp
// خيارات حفظ النص. يمكنك استخدام أي نوع من الفواصل
TxtSaveOptions opts = new TxtSaveOptions();
opts.Separator = '\t'; // تعيين علامة التبويب كفاصل
```
 في هذا المثال، نستخدم حرف علامة التبويب كفاصل. يمكنك استبدال`'\t'` مع أي حرف تريده، مثل الفاصلة (`,`)، اعتمادًا على كيفية رغبتك في تنسيق ملف CSV الخاص بك.
## الخطوة 5: التكرار في كل ورقة عمل
 بعد ذلك، سنقوم بالتكرار خلال جميع أوراق العمل داخل المصنف، وحفظ كل واحدة منها في`workbookData` المصفوفة، ولكن يجب عليك أولاً تحديد ورقة العمل التي ستعمل عليها.
```csharp
// انسخ بيانات كل ورقة عمل بتنسيق نصي داخل مجموعة بيانات المصنف
for (int idx = 0; idx < workbook.Worksheets.Count; idx++)
{
    // حفظ ورقة العمل النشطة بتنسيق نصي
    MemoryStream ms = new MemoryStream();
    workbook.Worksheets.ActiveSheetIndex = idx;
    workbook.Save(ms, opts);
```
 تمر الحلقة عبر كل ورقة عمل في المصنف.`ActiveSheetIndex` تم ضبطه بحيث نقوم في كل مرة من خلال الحلقة بحفظ ورقة العمل الحالية. سيتم حفظ النتائج في الذاكرة باستخدام`MemoryStream`.
## الخطوة 6: استرداد بيانات ورقة العمل
 بعد حفظ ورقة عمل في مجرى الذاكرة، فإن الخطوة التالية هي استرداد هذه البيانات وإضافتها إلى`workbookData` مصفوفة.
```csharp
    // حفظ بيانات ورقة العمل في مصفوفة بيانات الورقة
    ms.Position = 0; // إعادة تعيين موضع تدفق الذاكرة
    byte[] sheetData = ms.ToArray(); // الحصول على مجموعة البايتات
```
`ms.Position = 0;` يعيد تعيين موضع القراءة بعد الكتابة. ثم نستخدم`ToArray()` لتحويل مجرى الذاكرة إلى مصفوفة بايتات تحتوي على بيانات ورقة العمل.
## الخطوة 7: دمج بيانات ورقة العمل
 الآن، سنقوم بدمج البيانات من كل ورقة عمل في ورقة عمل واحدة`workbookData` تم تهيئه المصفوفة في وقت سابق.
```csharp
    // دمج بيانات ورقة العمل هذه في مجموعة بيانات المصنف
    byte[] combinedArray = new byte[workbookData.Length + sheetData.Length];
    Array.Copy(workbookData, 0, combinedArray, 0, workbookData.Length);
    Array.Copy(sheetData, 0, combinedArray, workbookData.Length, sheetData.Length);
    workbookData = combinedArray;
}
```
نقوم بإنشاء مصفوفة جديدة كبيرة بما يكفي لاستيعاب بيانات المصنف الحالية وبيانات ورقة العمل الجديدة. ثم نقوم بنسخ البيانات الحالية والجديدة إلى هذه المصفوفة المدمجة لاستخدامها لاحقًا.
## الخطوة 8: حفظ بيانات المصنف بالكامل في ملف
 وأخيرًا، مع جمع كافة البيانات في`workbookData` المصفوفة، يمكننا حفظ هذه المصفوفة في مسار ملف محدد.
```csharp
//حفظ بيانات المصنف بالكامل في ملف
File.WriteAllBytes(dataDir + "out.txt", workbookData);
```
`WriteAllBytes` يأخذ مجموعة البايتات المجمعة ويكتبها في ملف نصي يسمى "out.txt" في الدليل المحدد.
## خاتمة
والآن، لقد نجحت في تحويل مصنف Excel إلى تنسيق CSV باستخدام Aspose.Cells for .NET. ولا تعد هذه العملية فعّالة فحسب، بل إنها تتيح أيضًا معالجة بيانات Excel بسهولة لمزيد من التحليل أو إعداد التقارير. والآن يمكنك أتمتة مهام معالجة البيانات أو حتى دمج هذه الوظيفة في تطبيقات أكبر.
## الأسئلة الشائعة
### هل يمكنني استخدام فواصل مختلفة لملف CSV؟
 نعم يمكنك تغيير`opts.Separator` إلى أي حرف تريده، مثل الفواصل أو الأنابيب.
### هل استخدام Aspose.Cells مجاني؟
 Aspose.Cells ليس مجانيًا، ولكن يمكنك الحصول على نسخة تجريبية مجانية[هنا](https://releases.aspose.com/).
### ما هي أنواع التنسيقات التي يمكنني الحفظ بها بالإضافة إلى CSV؟
يتيح لك Aspose.Cells الحفظ بتنسيقات متعددة بما في ذلك XLSX وPDF والمزيد.
### هل يمكنني معالجة ملفات Excel كبيرة الحجم باستخدام Aspose.Cells؟
نعم، تم تصميم Aspose.Cells للتعامل مع الملفات الكبيرة بكفاءة، ولكن الأداء قد يعتمد على موارد النظام.
### أين يمكنني العثور على المزيد من الوثائق التفصيلية؟
يمكنك العثور على وثائق وأمثلة شاملة على[موقع مرجعي](https://reference.aspose.com/cells/net/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
