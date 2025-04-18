---
title: تنسيق عرض بيانات جدول المحور وترتيبها في .NET
linktitle: تنسيق عرض بيانات جدول المحور وترتيبها في .NET
second_title: واجهة برمجة تطبيقات معالجة Excel الخاصة بـ Aspose.Cells .NET
description: تعرف على كيفية إنشاء تنسيق عرض بيانات جدول محوري وإدارته في .NET باستخدام Aspose.Cells من خلال هذا الدليل خطوة بخطوة.
weight: 30
url: /ar/net/creating-and-configuring-pivot-tables/pivot-table-data-display-format-ranking/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تنسيق عرض بيانات جدول المحور وترتيبها في .NET

## مقدمة
عندما يتعلق الأمر بتحليل البيانات، وخاصة في Excel، فإن جداول البيانات المحورية هي أفضل أصدقائك. فهي تساعدك على تلخيص البيانات واستكشافها وتصورها بطرق لا تستطيع الجداول العادية القيام بها. إذا كنت تعمل في بيئة .NET وترغب في الاستفادة من قوة جداول البيانات المحورية، فإن Aspose.Cells هي مكتبة مثالية. بفضل واجهة برمجة التطبيقات سهلة الاستخدام والميزات الشاملة، تمكنك من التعامل مع ملفات Excel مثل المحترفين. في هذا البرنامج التعليمي، سنستكشف كيفية إعداد ترتيب تنسيق عرض بيانات جداول البيانات المحورية في .NET باستخدام Aspose.Cells، وتقسيمها خطوة بخطوة لفهم واضح.
## المتطلبات الأساسية
قبل أن نتعمق في التفاصيل، دعنا نتأكد من إعداد كل شيء للمتابعة. إليك ما ستحتاج إليه:
1. بيئة التطوير: تأكد من أن لديك بيئة تطوير .NET صالحة للعمل. قد تكون هذه البيئة هي Visual Studio أو أي بيئة تطوير متكاملة أخرى متوافقة.
2. مكتبة Aspose.Cells: ستحتاج إلى مكتبة Aspose.Cells. يمكنك تنزيلها من[موقع](https://releases.aspose.com/cells/net/)تتوفر أيضًا نسخة تجريبية مجانية يمكنك البدء بها دون أي تكاليف فورية.
3.  بيانات العينة: في هذا البرنامج التعليمي، سنستخدم ملف Excel باسم`PivotTableSample.xlsx`تأكد من تنظيم بياناتك بشكل صحيح في هذا الملف لإنشاء جدول محوري.
الآن بعد أن قمنا بتغطية أساسياتنا، دعنا نتعمق في الكود!
## استيراد الحزم
للبدء، تحتاج إلى استيراد مساحات الأسماء الضرورية في مشروع .NET الخاص بك. هذه خطوة بالغة الأهمية لضمان قدرة تطبيقك على الوصول إلى وظيفة Aspose.Cells. إليك كيفية القيام بذلك:
### استيراد مساحة اسم Aspose.Cells
```csharp
using System;
using Aspose.Cells.Pivot;
```
من خلال هذا السطر في أعلى ملف C#، ستتمكن من الوصول إلى جميع الميزات التي تحتاجها للعمل مع ملفات Excel.
## الخطوة 1: إعداد الدلائل
قبل تحميل مستند Excel، يجب عليك تحديد مكان وجود بيانات المصدر والمكان الذي ترغب في حفظ النتائج فيه. وفيما يلي كيفية إعداد هذه الدلائل:
```csharp
// الدلائل
string sourceDir = "Your Document Directory"; // التحديث باستخدام الدليل الفعلي الخاص بك
string outputDir = "Your Document Directory"; // التحديث باستخدام الدليل الفعلي الخاص بك
```
 تأكد من الاستبدال`"Your Document Directory"` مع المسار الفعلي الذي يتم تخزين ملفاتك فيه.
## الخطوة 2: تحميل المصنف
بعد ذلك، ستحتاج إلى تحميل ملف Excel الذي يحتوي على جدول Pivot Table. وإليك الطريقة:
```csharp
// تحميل ملف القالب
Workbook workbook = new Workbook(sourceDir + "PivotTableSample.xlsx");
```
 ال`Workbook` تُعد الفئة بمثابة بوابة للعمل مع ملفات Excel. من خلال تمرير مسار ملف الإدخال الخاص بك، فأنت تخبر Aspose.Cells بتحميل هذا الملف إلى الذاكرة.
## الخطوة 3: الوصول إلى ورقة العمل
بعد تحميل المصنف، ستحتاج إلى الوصول إلى ورقة العمل المحددة التي تحتوي على جدول Pivot الخاص بك:
```csharp
// احصل على ورقة العمل الأولى
Worksheet worksheet = workbook.Worksheets[0];
```
يقوم مقتطف التعليمات البرمجية هذا باسترجاع ورقة العمل الأولى من المصنف الخاص بك. إذا كان جدول البيانات المحوري الخاص بك موجودًا في ورقة مختلفة، فما عليك سوى ضبط الفهرس وفقًا لذلك.
## الخطوة 4: الوصول إلى جدول البيانات المحوري
الآن حان الوقت للوصول إلى لب الموضوع - جدول البيانات المحوري. فلنبدأ في الوصول إليه:
```csharp
int pivotIndex = 0; // فهرس الجدول المحوري
PivotTable pivotTable = worksheet.PivotTables[pivotIndex];
```
في هذا السيناريو، نصل إلى جدول Pivot الأول. إذا كان لديك جداول Pivot متعددة، فاضبط`pivotIndex`.
## الخطوة 5: الوصول إلى حقول البيانات
بعد الوصول إلى جدول البيانات المحوري، تكون الخطوة التالية هي البحث في حقول البيانات الخاصة به. وإليك الطريقة:
```csharp
// الوصول إلى حقول البيانات.
PivotFieldCollection pivotFields = pivotTable.DataFields;
```
تحتوي هذه المجموعة على كافة حقول البيانات المرتبطة بجدول المحور.
## الخطوة 6: تكوين تنسيق عرض البيانات
الآن يأتي الجزء الممتع - إعداد تنسيق عرض البيانات للترتيب. هنا يمكنك إخبار جدول البيانات المحوري بكيفية عرض البيانات:
```csharp
// الوصول إلى حقل البيانات الأول في حقول البيانات.
PivotField pivotField = pivotFields[0];
// ضبط تنسيق عرض البيانات
pivotField.DataDisplayFormat = PivotFieldDataDisplayFormat.RankLargestToSmallest;
```
من خلال القيام بذلك، فأنت بذلك تأمر جدول البيانات المحوري بعرض حقل البيانات الأول بترتيب تنازلي. وإذا كنت ترغب في عرضه بترتيب تصاعدي، فيمكنك تغيير تنسيق العرض وفقًا لذلك.
## الخطوة 7: حساب البيانات
لن تسري التغييرات التي أجريتها على جدول Pivot إلا بعد إعادة حساب البيانات. وإليك كيفية القيام بذلك:
```csharp
pivotTable.CalculateData();
```
يقوم هذا السطر بتحديث جدول المحور، وتطبيق أي تغييرات قمت بإجرائها.
## الخطوة 8: احفظ الناتج
أخيرًا، احفظ المصنف المعدّل في دليل الإخراج المحدد:
```csharp
// حفظ ملف Excel
workbook.Save(outputDir + "PivotTableDataDisplayFormatRanking_out.xlsx");
```
سيؤدي هذا إلى إنشاء ملف Excel جديد بتنسيق العرض المطبق. 
## الخطوة 9: رسالة التأكيد
من الجيد دائمًا التأكد من أن كل شيء يعمل كما هو متوقع. يمكنك إضافة إخراج بسيط لوحدة التحكم لإعلامك بما يلي:
```csharp
Console.WriteLine("PivotTableDataDisplayFormatRanking executed successfully.");
```
## خاتمة
تهانينا! لقد تعلمت للتو كيفية إعداد تنسيق عرض بيانات جدول محوري باستخدام Aspose.Cells لـ .NET. من خلال الاستفادة من قوة هذه المكتبة، تصبح إدارة جداول البيانات الخاصة بك أكثر كفاءة وقادرة على إنتاج تحليلات مفيدة. لا تنس تجربة تنسيقات بيانات مختلفة لمعرفة كيف يمكنها مساعدتك في تصور بياناتك بشكل أفضل. 
## الأسئلة الشائعة
### ما هو Aspose.Cells؟
Aspose.Cells هي مكتبة .NET تتيح للمطورين العمل مع ملفات Excel دون الحاجة إلى Microsoft Excel. فهي تسمح بقراءة مستندات Excel وكتابتها ومعالجتها بسلاسة.
### هل أحتاج إلى الدفع مقابل Aspose.Cells؟
على الرغم من أن Aspose.Cells يقدم نسخة تجريبية مجانية، فإنه يتطلب الشراء للحصول على الميزات الكاملة. يمكنك التحقق من[صفحة الشراء](https://purchase.aspose.com/buy) لمزيد من التفاصيل.
### هل يمكنني إنشاء جداول محورية باستخدام Aspose.Cells؟
نعم، يوفر Aspose.Cells ميزات قوية لإنشاء جداول البيانات المحورية وإدارتها برمجيًا.
### أين يمكنني العثور على مزيد من المعلومات حول استخدام Aspose.Cells؟
 يمكنك الرجوع إلى الدليل الشامل[توثيق Aspose.Cells](https://reference.aspose.com/cells/net/) للحصول على إرشادات مفصلة ومراجع API.
### ماذا لو واجهت مشاكل؟
 إذا واجهت أي مشاكل، فلا تتردد في التواصل مع المجتمع والحصول على الدعم على[منتدى اسبوس](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
