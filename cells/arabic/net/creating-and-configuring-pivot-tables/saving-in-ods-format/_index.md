---
"description": "تعرف على كيفية حفظ جداول البيانات المحورية بتنسيق ODS باستخدام Aspose.Cells لـ .NET من خلال هذا الدليل خطوة بخطوة."
"linktitle": "حفظ جدول محوري بتنسيق ODS برمجيًا في .NET"
"second_title": "واجهة برمجة تطبيقات معالجة Excel Aspose.Cells .NET"
"title": "حفظ جدول محوري بتنسيق ODS برمجيًا في .NET"
"url": "/ar/net/creating-and-configuring-pivot-tables/saving-in-ods-format/"
"weight": 25
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# حفظ جدول محوري بتنسيق ODS برمجيًا في .NET

## مقدمة
عندما يتعلق الأمر بإدارة البيانات في جداول البيانات، لا شيء يضاهي قوة جداول البيانات المحورية. إنها أداة مثالية لتلخيص وتحليل وعرض مجموعات البيانات المعقدة. اليوم، سنتعمق في استخدام Aspose.Cells لـ .NET لحفظ جدول بيانات محوري بتنسيق ODS. سواء كنت مطورًا متمرسًا أو مبتدئًا في استخدام .NET، ستجد هذا الدليل سهلًا وبسيطًا. 
دعونا نبدأ!
## المتطلبات الأساسية
قبل أن ننتقل إلى الكود، هناك بعض الأساسيات التي ستحتاجها:
### 1. المعرفة الأساسية بـ .NET
إن الحصول على فهم أساسي لـ .NET ومفاهيم البرمجة الخاصة به سيساعدك على المتابعة بسهولة.
### 2. Aspose.Cells لـ .NET
ستحتاج إلى تثبيت Aspose.Cells لـ .NET. يمكنك تنزيله من [صفحة إصدارات Aspose](https://releases.aspose.com/cells/net/). تتوفر أيضًا نسخة تجريبية [هنا](https://releases.aspose.com/).
### 3. بيئة التطوير
تأكد من أن لديك IDE مثل Visual Studio حيث يمكنك كتابة واختبار كود .NET الخاص بك.
### 4. القليل من الصبر
كما هو الحال في أي مشروع برمجة، الصبر مفتاح النجاح. لا تقلق إذا لم تنجح الأمور من المرة الأولى؛ فتصحيح الأخطاء جزء لا يتجزأ من العملية.
## استيراد الحزم
للعمل مع Aspose.Cells، ستحتاج إلى استيراد مساحات الأسماء اللازمة. أضف الأمر التالي باستخدام في بداية ملف الكود:
```csharp
using System;
using Aspose.Cells.Pivot;
```
يتيح لك هذا السطر الوصول إلى جميع الوظائف داخل مكتبة Aspose.Cells، مما يجعل عملية الترميز الخاصة بك سهلة للغاية.
الآن، دعونا نقسم العملية إلى خطوات قابلة للإدارة.
## الخطوة 1: إعداد دليل الإخراج الخاص بك
أولاً، عليك تحديد مكان حفظ ملف ODS. هذا تحديد بسيط لمسار الدليل.
```csharp
string outputDir = "Your Document Directory";
```
في هذا السطر، استبدل `"Your Document Directory"` مع المسار الذي تريد حفظ الملف فيه.
## الخطوة 2: إنشاء مصنف جديد
بعد ذلك، ستقوم بإنشاء كائن مصنف جديد، والذي سيحمل كل بياناتك وهياكلك، بما في ذلك جدول البيانات المحوري.
```csharp
Workbook workbook = new Workbook();
```
هنا، يمكنك البدء من جديد بشكل أساسي - فكر في الأمر باعتباره لوحة قماشية فارغة حيث ستنشئ تحفتك الفنية.
## الخطوة 3: الوصول إلى ورقة العمل
الآن وقد أصبح لدينا مصنف العمل، علينا البدء بالعمل على ورقة العمل. يتيح لك Aspose.Cells الوصول بسهولة إلى أول ورقة عمل متاحة.
```csharp
Worksheet sheet = workbook.Worksheets[0];
```
يؤدي بنا هذا الخط إلى الورقة الأولى الجاهزة لإدخال البيانات.
## الخطوة 4: ملء الخلايا بالبيانات
حان الوقت لملء ورقة العمل ببعض البيانات. سنستخدم مثالاً بسيطاً لبيانات مبيعات رياضية. 
إليك كيفية تعيين القيم في خلايا مختلفة:
```csharp
Cells cells = sheet.Cells;
cells["A1"].PutValue("Sport");
cells["B1"].PutValue("Quarter");
cells["C1"].PutValue("Sales");
cells["A2"].PutValue("Golf");
cells["A3"].PutValue("Golf");
cells["A4"].PutValue("Tennis");
cells["A5"].PutValue("Tennis");
cells["A6"].PutValue("Tennis");
cells["A7"].PutValue("Tennis");
cells["A8"].PutValue("Golf");
cells["B2"].PutValue("Qtr3");
cells["B3"].PutValue("Qtr4");
cells["B4"].PutValue("Qtr3");
cells["B5"].PutValue("Qtr4");
cells["B6"].PutValue("Qtr3");
cells["B7"].PutValue("Qtr4");
cells["B8"].PutValue("Qtr3");
cells["C2"].PutValue(1500);
cells["C3"].PutValue(2000);
cells["C4"].PutValue(600);
cells["C5"].PutValue(1500);
cells["C6"].PutValue(4070);
cells["C7"].PutValue(5000);
cells["C8"].PutValue(6430);
```
في هذه السطور، نُحدد العناوين ونُضيف بيانات المبيعات. تشبه هذه الخطوة تجهيز مخزنك قبل طهي وجبة؛ فكلما كانت مكوناتك (البيانات) أفضل، كانت وجبتك أفضل (التحليل).
## الخطوة 5: إنشاء جدول محوري
الآن يأتي الجزء الممتع: إنشاء جدول محوري! إليك كيفية إضافته إلى ورقة العمل:
```csharp
PivotTableCollection pivotTables = sheet.PivotTables;
// إضافة جدول محوري إلى ورقة العمل
int index = pivotTables.Add("=A1:C8", "E3", "PivotTable2");
```
في هذا المقطع، نحدد نطاق بيانات الجدول المحوري ومكان وضعه في ورقة العمل. نطاق البيانات `=A1:C8` يغطي المنطقة التي توجد بها بياناتنا.
## الخطوة 6: تخصيص جدول المحور الخاص بك
بعد ذلك، ستحتاج إلى تخصيص جدولك المحوري ليناسب احتياجاتك. يتضمن ذلك التحكم في ما يظهر، وكيفية تصنيفه، وكيفية حساب البيانات.
```csharp
PivotTable pivotTable = pivotTables[index];
// عدم إظهار الإجماليات الكبرى للصفوف.
pivotTable.RowGrand = false;
// سحب الحقل الأول إلى منطقة الصف.
pivotTable.AddFieldToArea(PivotFieldType.Row, 0);
// سحب الحقل الثاني إلى منطقة العمود.
pivotTable.AddFieldToArea(PivotFieldType.Column, 1);
// سحب الحقل الثالث إلى منطقة البيانات.
pivotTable.AddFieldToArea(PivotFieldType.Data, 2);
pivotTable.CalculateData();
```
هنا، أنت تُحدد حقول البيانات التي تُلخّصها وكيفية تمثيلها. الأمر أشبه بتجهيز مائدة عشاء؛ أنت تُقرر ما يُناسبها وكيفية عرضها.
## الخطوة 7: احفظ مصنفك
أخيرًا، أنت جاهز لحفظ عملك بتنسيق ODS المطلوب. إليك الطريقة:
```csharp
workbook.Save(outputDir + "PivotTableSaveInODS_out.ods");
```
مع هذه الخطوة، تكون قد أنهيت مشروعك وحافظت عليه في الدليل الذي اخترته - وهي نهاية مرضية!
## الخطوة 8: التحقق من الناتج الخاص بك
وأخيرًا، يُنصح دائمًا بالتحقق من اكتمال العملية بنجاح. يمكنك إضافة رسالة بسيطة إلى وحدة التحكم:
```csharp
Console.WriteLine("PivotTableSaveInODS executed successfully.");
```
ستظهر هذه الرسالة على لوحة التحكم لديك لتأكيد نجاح كل شيء. تمامًا كما يتحقق الطاهي من نضج كل شيء قبل التقديم!
## خاتمة 
ها قد انتهيت! لم تكتفِ بإنشاء جدول محوري باستخدام Aspose.Cells، بل حفظته أيضًا بتنسيق ODS. لقد شرح لك هذا الدليل كل خطوة، مما يضمن لك المعرفة والثقة اللازمة للتعامل مع مهام مماثلة في المستقبل.
## الأسئلة الشائعة
### ما هو Aspose.Cells؟
Aspose.Cells هي مكتبة متطورة تتيح لك إنشاء ملفات Excel ومعالجتها في تطبيقات .NET.
### هل يمكنني استخدام Aspose.Cells مجانًا؟
نعم، يمكنك تنزيل نسخة تجريبية مجانية من [موقع Aspose](https://releases.aspose.com/).
### ما هي التنسيقات التي يدعمها Aspose.Cells؟
إنه يدعم العديد من التنسيقات، بما في ذلك XLSX، XLS، ODS، PDF، وغيرها الكثير.
### كيف أحصل على الدعم لـ Aspose.Cells؟
يمكنك العثور على المساعدة على [منتدى دعم Aspose](https://forum.aspose.com/c/cells/9).
### هل يوجد ترخيص مؤقت متاح؟
نعم يمكنك التقدم بطلب للحصول على ترخيص مؤقت من خلال موقع Aspose [هنا](https://purchase.aspose.com/temporary-license/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}