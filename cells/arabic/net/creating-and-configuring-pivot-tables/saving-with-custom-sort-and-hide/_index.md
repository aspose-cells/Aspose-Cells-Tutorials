---
"description": "تعلّم كيفية حفظ جداول البيانات المحورية مع فرز وإخفاء الصفوف حسب الطلب باستخدام Aspose.Cells لـ .NET. دليل خطوة بخطوة مع أمثلة عملية."
"linktitle": "حفظ جداول المحور باستخدام الفرز والإخفاء المخصصين في .NET"
"second_title": "واجهة برمجة تطبيقات معالجة Excel Aspose.Cells .NET"
"title": "حفظ جداول المحور باستخدام الفرز والإخفاء المخصصين في .NET"
"url": "/ar/net/creating-and-configuring-pivot-tables/saving-with-custom-sort-and-hide/"
"weight": 26
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# حفظ جداول المحور باستخدام الفرز والإخفاء المخصصين في .NET

## مقدمة
في عالم تحليل البيانات، تُعدّ جداول البيانات المحورية من أقوى الأدوات لتلخيص البيانات وتحليلها وعرضها بصيغة سهلة الفهم. إذا كنت تعمل باستخدام .NET وتبحث عن طريقة سهلة للتعامل مع جداول البيانات المحورية، وتحديدًا حفظها باستخدام فرز مخصص وإخفاء صفوف محددة، فأنت في المكان المناسب! سنشرح اليوم تقنية حفظ جداول البيانات المحورية باستخدام Aspose.Cells لـ .NET. سيشرح لك هذا الدليل كل شيء، من المتطلبات الأساسية إلى الأمثلة العملية، مما يضمن لك القدرة على التعامل مع مهام مماثلة بنفسك. هيا بنا!
## المتطلبات الأساسية
قبل الخوض في تفاصيل البرمجة، تأكد من توفر المتطلبات الأساسية التالية:
1. Visual Studio: من الناحية المثالية، قد ترغب في بيئة تطوير متكاملة قوية لإدارة مشاريع .NET الخاصة بك. يُعد Visual Studio خيارًا رائعًا.
2. Aspose.Cells لـ .NET: ستحتاج إلى الوصول إلى مكتبة Aspose لإدارة ملفات Excel برمجيًا. يمكنك [قم بتنزيل Aspose.Cells لـ .NET هنا](https://releases.aspose.com/cells/net/).
3. المعرفة الأساسية بلغة C#: إن الإلمام بمفاهيم البرمجة الأساسية والقواعد النحوية في لغة C# سيجعل العملية أكثر سلاسة.
4. ملف Excel النموذجي: سنستخدم ملفًا نموذجيًا باسم `PivotTableHideAndSortSample.xlsx`تأكد من وجود هذا الملف في دليل المستندات المخصص لك.
بمجرد إعداد بيئة التطوير الخاصة بك وتجهيز ملف العينة الخاص بك، فأنت جاهز تمامًا!
## استيراد الحزم
بعد استيفاء المتطلبات الأساسية، لنستورد الحزم اللازمة. في ملف C#، استخدم الأمر التالي لتضمين Aspose.Cells:
```csharp
using System;
using Aspose.Cells.Pivot;
```
يتيح لك هذا التوجيه الوصول إلى الفئات والأساليب التي توفرها مكتبة Aspose.Cells. تأكد من إضافة ملف Aspose.Cells.dll إلى مراجع مشروعك.
## الخطوة 1: إعداد المصنف
أولاً، علينا تحميل مصنف العمل. يُحقق ذلك مقطع الكود التالي:
```csharp
// دلائل للملفات المصدر والإخراج
string sourceDir = "Your Document Directory";
string outputDir = "Your Document Directory";
// تحميل المصنف
Workbook workbook = new Workbook(sourceDir + "PivotTableHideAndSortSample.xlsx");
```
في هذه الخطوة، يمكنك تحديد المجلدات التي سيتم تخزين ملفات المصدر والإخراج فيها. `Workbook` سيقوم المنشئ بتحميل ملف Excel الحالي لديك، مما يجعله جاهزًا للتعامل معه.
## الخطوة 2: الوصول إلى ورقة العمل والجدول المحوري
الآن، دعنا نصل إلى ورقة العمل المحددة داخل المصنف ونختار جدول المحور الذي نريد العمل معه.
```csharp
// الوصول إلى ورقة العمل الأولى
Worksheet worksheet = workbook.Worksheets[0];
// الوصول إلى الجدول المحوري الأول في ورقة العمل
var pivotTable = worksheet.PivotTables[0];
```
في هذه المقتطفة، `Worksheets[0]` يحدد الورقة الأولى في مستند Excel الخاص بك، و `PivotTables[0]` يسترجع الجدول المحوري الأول. يتيح لك هذا تحديد الجدول المحوري الذي ترغب في تعديله.
## الخطوة 3: فرز صفوف جدول المحور
بعد ذلك، سنُطبّق فرزًا مُخصّصًا لتنظيم بياناتنا. على وجه التحديد، سنُرتّب النتائج تنازليًا.
```csharp
// فرز حقل الصف الأول بالترتيب التنازلي
PivotField field = pivotTable.RowFields[0];
field.IsAutoSort = true;
field.IsAscendSort = false;  // خطأ في النزول
field.AutoSortField = 0;     // الفرز بناءً على العمود الأول
```
هنا، نحن نستخدم `PivotField` لتعيين معلمات الفرز. يُطلب من الجدول المحوري فرز حقل الصف المحدد بناءً على العمود الأول، بترتيب تنازلي. 
## الخطوة 4: تحديث البيانات وحسابها
بعد تطبيق الفرز، من الضروري تحديث بيانات جدول المحور للتأكد من أنه يعكس تعديلاتنا.
```csharp
// تحديث بيانات الجدول المحوري وحسابها
pivotTable.RefreshData();
pivotTable.CalculateData();
```
تُزامن هذه الخطوة جدول البيانات المحوري مع بياناتك الحالية، مع تطبيق أي تغييرات أجريتها على الفرز أو التصفية حتى الآن. يمكنك ببساطة الضغط على زر "تحديث" لرؤية التنظيم الجديد لبياناتك!
## الخطوة 5: إخفاء صفوف محددة
الآن، دعنا نخفي الصفوف التي تحتوي على درجات أقل من حد معين - على سبيل المثال، أقل من 60. هذا هو المكان الذي يمكننا فيه تصفية البيانات بشكل أكبر.
```csharp
// حدد الصف الأولي للتحقق من النتائج
int currentRow = 3;
int rowsUsed = pivotTable.DataBodyRange.EndRow;
// إخفاء الصفوف التي تحتوي على درجة أقل من 60
while (currentRow < rowsUsed)
{
    Cell cell = worksheet.Cells[currentRow, 1]; // بافتراض أن النتيجة موجودة في العمود الأول
    double score = Convert.ToDouble(cell.Value);
    if (score < 60)
    {
        worksheet.Cells.HideRow(currentRow);  // إخفاء الصف إذا كانت النتيجة أقل من 60
    }
    currentRow++;
}
```
في هذه الحلقة، نتحقق من كل صف ضمن نطاق بيانات الجدول المحوري. إذا كانت النتيجة أقل من 60، نخفي هذا الصف. يشبه الأمر تنظيف مساحة عملك - إزالة الفوضى التي تعيقك عن رؤية الصورة الكاملة!
## الخطوة 6: التحديث النهائي وحفظ المصنف
قبل الانتهاء، دعنا نقوم بتحديث جدول المحور للمرة الأخيرة للتأكد من أن إخفاء الصفوف ساري المفعول، ثم دعنا نحفظ المصنف في ملف جديد.
```csharp
// قم بتحديث البيانات وحسابها مرة أخيرة
pivotTable.RefreshData();
pivotTable.CalculateData();
// حفظ المصنف المعدل
workbook.Save(outputDir + "PivotTableHideAndSort_out.xlsx");
```
يضمن هذا التحديث النهائي أن كل شيء محدث، ومن خلال حفظ المصنف، يمكنك إنشاء ملف جديد يعكس كل التغييرات التي أجريناها.
## الخطوة 7: تأكيد النجاح
وأخيرًا، سنقوم بطباعة رسالة نجاح للتأكيد على اكتمال عمليتنا دون أي عوائق.
```csharp
Console.WriteLine("PivotTableSortAndHide executed successfully.");
```
يخدم هذا الخط غرضًا مزدوجًا يتمثل في تأكيد النجاح وتوفير التعليقات في وحدة التحكم الخاصة بك، مما يجعل العملية أكثر تفاعلية وسهولة في الاستخدام.
## خاتمة
ها قد انتهيت! لقد تعلمت بنجاح كيفية حفظ جداول البيانات المحورية مع وظائف الفرز والإخفاء المخصصة باستخدام Aspose.Cells لـ .NET. بدءًا من تحميل مصنفك ووصولًا إلى فرز البيانات وإخفاء التفاصيل غير الضرورية، توفر هذه الخطوات نهجًا منظمًا لإدارة جداول البيانات المحورية برمجيًا. سواء كنت تُحلل بيانات المبيعات، أو تتبّع أداء الفريق، أو تُنظّم المعلومات ببساطة، فإن إتقان هذه المهارات باستخدام Aspose.Cells سيوفر لك وقتًا ثمينًا ويُحسّن سير عمل تحليل البيانات لديك.
## الأسئلة الشائعة
### ما هو Aspose.Cells لـ .NET؟
Aspose.Cells for .NET هي مكتبة .NET تُمكّن المطورين من إنشاء جداول بيانات Excel ومعالجتها وتحويلها دون الاعتماد على Microsoft Excel. وهي مثالية لأتمتة المهام في مستندات Excel.
### هل يمكنني استخدام Aspose.Cells دون تثبيت Microsoft Office؟
بالتأكيد! Aspose.Cells مكتبة مستقلة، لذا لا تحتاج إلى تثبيت Microsoft Office على جهازك للعمل مع ملفات Excel.
### كيف يمكنني الحصول على ترخيص مؤقت لـ Aspose.Cells؟
يمكنك التقدم بطلب للحصول على ترخيص مؤقت من خلال [صفحة الترخيص المؤقت](https://purchase.aspose.com/temporary-license/).
### أين يمكنني العثور على الدعم لمشاكل Aspose.Cells؟
لأي أسئلة أو مشكلات، يمكنك زيارة [منتدى Aspose](https://forum.aspose.com/c/cells/9)حيث ستجد الدعم من المجتمع وفريق Aspose.
### هل هناك نسخة تجريبية مجانية متاحة لـ Aspose.Cells؟
نعم! يمكنك تنزيل نسخة تجريبية مجانية من Aspose.Cells لاختبار ميزاته قبل الشراء. تفضل بزيارة [صفحة التجربة المجانية](https://releases.aspose.com/) للبدء.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}