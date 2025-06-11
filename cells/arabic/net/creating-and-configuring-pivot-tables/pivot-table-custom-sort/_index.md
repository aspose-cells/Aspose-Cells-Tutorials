---
"description": "تعرّف على كيفية فرز جداول البيانات المحورية برمجيًا في .NET باستخدام Aspose.Cells. دليل خطوة بخطوة يشمل الإعداد والتكوين والفرز وحفظ النتائج كملفات Excel وPDF."
"linktitle": "فرز جدول محوري مخصص برمجيًا في .NET"
"second_title": "واجهة برمجة تطبيقات معالجة Excel Aspose.Cells .NET"
"title": "فرز جدول محوري مخصص برمجيًا في .NET"
"url": "/ar/net/creating-and-configuring-pivot-tables/pivot-table-custom-sort/"
"weight": 29
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# فرز جدول محوري مخصص برمجيًا في .NET

## مقدمة
عند استخدام Excel في بيئة .NET، تبرز مكتبة واحدة من بين البقية: Aspose.Cells. ألا يعجبك حقًا أن تتيح لك أداةٌ ما التعامل مع جداول البيانات برمجيًا؟ هذا بالضبط ما تفعله Aspose.Cells! في درس اليوم، سنتعمق في عالم جداول البيانات المحورية ونوضح لك كيفية تنفيذ الفرز المخصص برمجيًا باستخدام هذه المكتبة متعددة الاستخدامات.
## المتطلبات الأساسية
قبل أن نشمر عن سواعدنا ونبدأ في فهم الكود، تأكد من أن لديك بعض الأشياء في مكانها الصحيح:
1. Visual Studio: ستحتاج إلى إصدار عامل من Visual Studio. إنه ساحة اللعب حيث تحدث كل هذه الإبداعات.
2. إطار عمل .NET: الإلمام ببرمجة .NET أمرٌ أساسي. سواءً كنتَ من مُحبي .NET Core أو .NET Framework، فأنتَ جاهزٌ للبدء.
3. مكتبة Aspose.Cells: يجب تثبيت مكتبة Aspose.Cells. يمكنك الحصول عليها من [رابط التحميل](https://releases.aspose.com/cells/net/) وأضفه إلى مشروعك.
4. الفهم الأساسي لجداول المحور: على الرغم من أنك لست بحاجة إلى أن تكون خبيرًا، إلا أن القليل من المعرفة حول كيفية عمل جداول المحور سيكون مفيدًا أثناء قيامنا بهذا البرنامج التعليمي.
5. ملف Excel نموذجي: احصل على ملف Excel نموذجي باسم `SamplePivotSort.xlsx` جاهز في دليل العمل الخاص بك للاختبار.
## استيراد الحزم
بعد تجهيز جميع المتطلبات الأساسية، الخطوة الأولى هي استيراد الحزم اللازمة. للقيام بذلك، أضف الأسطر التالية أعلى الكود:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Aspose.Cells;
using Aspose.Cells.Pivot;
```
توفر هذه الحزمة كافة الوظائف التي تحتاجها للتعامل مع ملفات Excel باستخدام Aspose.Cells.

حسنًا، لنبدأ الجزء الممتع! سنُقسّم عملية إنشاء جدول محوري وتطبيق الفرز المخصص إلى خطوات سهلة.
## الخطوة 1: إعداد المصنف
للبدء، علينا إعداد مصنف العمل. إليك الطريقة:
```csharp
string sourceDir = "Your Document Directory";
string outputDir = "Your Document Directory";
Workbook wb = new Workbook(sourceDir + "SamplePivotSort.xlsx");
```
في هذه الخطوة، نقوم بتهيئة ملف جديد `Workbook` مثال مع مسار ملف Excel. هذا يُمثل لوحة الرسم التي سيُظهر فيها جدولنا المحوري.
## الخطوة 2: الوصول إلى ورقة العمل
بعد ذلك، نحتاج إلى الوصول إلى ورقة العمل حيث سنضيف جدولنا المحوري.
```csharp
Worksheet sheet = wb.Worksheets[0];
PivotTableCollection pivotTables = sheet.PivotTables;
```
هنا، نأخذ ورقة العمل الأولى في مصنفنا ونستدعي `PivotTableCollection`تتيح لنا هذه المجموعة إدارة كافة جداول البيانات المحورية الموجودة في ورقة العمل هذه.
## الخطوة 3: إنشاء جدول محوري أول
الآن حان الوقت لإنشاء جدول محوري.
```csharp
int index = pivotTables.Add("=Sheet1!A1:C10", "E3", "PivotTable1");
PivotTable pivotTable = pivotTables[index];
```
نضيف جدولًا محوريًا جديدًا إلى ورقة العمل، مع تحديد نطاق البيانات وموقعه. يشير "E3" إلى المكان الذي نريد أن يبدأ منه الجدول المحوري. ثم نشير إلى هذا الجدول المحوري الجديد باستخدام فهرسه.
## الخطوة 4: تكوين إعدادات جدول المحور
لنُهيئ جدولنا المحوري! هذا يعني التحكم في جوانب مثل الإجماليات الكلية وترتيب الحقول.
```csharp
pivotTable.RowGrand = false;
pivotTable.ColumnGrand = false;
pivotTable.AddFieldToArea(PivotFieldType.Row,1);
PivotField rowField = pivotTable.RowFields[0];
rowField.IsAutoSort = true;
rowField.IsAscendSort = true;
```
نضمن عدم عرض الإجماليات الكلية للصفوف والأعمدة، مما يُحسّن البيانات. ثم نضيف الحقل الأول إلى منطقة الصف، مما يُمكّن الفرز التلقائي والفرز التصاعدي.
## الخطوة 5: إضافة الأعمدة وحقول البيانات
بمجرد تعيين الصفوف، دعنا نضيف حقول العمود والبيانات.
```csharp
pivotTable.AddFieldToArea(PivotFieldType.Column,0);
PivotField colField = pivotTable.ColumnFields[0];
colField.NumberFormat = "dd/mm/yyyy";
colField.IsAutoSort = true;
colField.IsAscendSort = true;
```
نضيف الحقل الثاني كعمود وننسقه كتاريخ. ونُفعّل الفرز التلقائي والترتيب التصاعدي للحفاظ على تنظيم البيانات. وأخيرًا، نضيف الحقل الثالث إلى منطقة البيانات:
```csharp
pivotTable.AddFieldToArea(PivotFieldType.Data,2);
```
## الخطوة 6: تحديث جدول البيانات المحوري وحسابه
بعد إضافة جميع الحقول اللازمة، دعنا نتأكد من أن جدول Pivot الخاص بنا جديد وجاهز.
```csharp
pivotTable.RefreshData();
pivotTable.CalculateData();
```
تعمل هذه الطرق على تحديث البيانات وإعادة حسابها، مما يضمن تحديث كل شيء وعرضه بشكل صحيح في جدولنا المحوري.
## الخطوة 7: فرز مخصص استنادًا إلى قيم حقل الصف
دعنا نضيف القليل من الأناقة عن طريق فرز جدول المحور استنادًا إلى قيم محددة، مثل "المأكولات البحرية".
```csharp
index = pivotTables.Add("=Sheet1!A1:C10", "E10", "PivotTable2");
pivotTable = pivotTables[index];
```
نكرر العملية بإنشاء جدول محوري آخر وإعداده بشكل مشابه للأول. يمكننا الآن تخصيصه بشكل أكبر:
```csharp
pivotTable.AddFieldToArea(PivotFieldType.Row,1);
rowField = pivotTable.RowFields[0];
rowField.IsAutoSort = true;
rowField.IsAscendSort = true;
```
## الخطوة 8: تخصيص الفرز الإضافي دعنا نحاول طريقة فرز أخرى استنادًا إلى تاريخ محدد:
```csharp
// إضافة جدول محوري آخر للفرز حسب التاريخ
index = pivotTables.Add("=Sheet1!A1:C10", "E18", "PivotTable3");
pivotTable = pivotTables[index];
// كرر إعدادات الصفوف والأعمدة على غرار الخطوات السابقة
```
كل ما عليك فعله هو تكرار نفس العملية، وإنشاء جدول محوري ثالث بمعايير فرز مخصصة لاحتياجاتك.
## الخطوة 9: احفظ المصنف حان الوقت لحفظ كل العمل الشاق الذي بذلناه!
```csharp
wb.Save(outputDir + "out.xlsx");
PdfSaveOptions options = new PdfSaveOptions();
options.OnePagePerSheet = true;
wb.Save(outputDir + "out.pdf", options);
```
هنا، يمكنك حفظ المصنف كملف Excel وملف PDF. `PdfSaveOptions` يسمح بتنسيق أفضل، مما يضمن ظهور كل ورقة على صفحة منفصلة عند التحويل.
## الخطوة 10: إنهاء الأمر قم بإنهاء الأمر من خلال إعلام المستخدم بأن كل شيء على ما يرام.
```csharp
Console.WriteLine("PivotTableCustomSort executed successfully.");
```
## خاتمة
لقد تعلمتَ الآن كيفية تسخير قوة Aspose.Cells لإنشاء جداول محورية وتخصيصها في تطبيقات .NET. من الإعداد الأولي إلى الفرز المخصص، تتكامل كل خطوة لتقديم تجربة سلسة. سواءً كنتَ بحاجة إلى عرض بيانات المبيعات السنوية أو تتبُّع إحصاءات المخزون، فإن هذه المهارات ستفيدك كثيرًا!
## الأسئلة الشائعة
### ما هو الجدول المحوري؟
الجدول المحوري هو أداة لمعالجة البيانات في Excel تتيح لك تلخيص البيانات وتحليلها، مما يوفر طريقة مرنة لاستخراج المعلومات بسهولة.
### كيف أقوم بتثبيت Aspose.Cells؟
يمكنك تثبيته عبر NuGet في Visual Studio أو تنزيله مباشرة من [رابط التحميل](https://releases.aspose.com/cells/net/).
### هل هناك نسخة تجريبية من Aspose.Cells؟
نعم! يمكنك تجربته مجانًا بزيارة [رابط التجربة المجانية](https://releases.aspose.com/).
### هل يمكنني فرز حقول متعددة في جدول محوري؟
بالتأكيد! يمكنك إضافة وفرز عدة حقول حسب احتياجاتك.
### أين يمكنني العثور على الدعم لـ Aspose.Cells؟
المجتمع نشط للغاية، ويمكنك طرح الأسئلة على منتداه [هنا](https://forum.aspose.com/c/cells/9).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}